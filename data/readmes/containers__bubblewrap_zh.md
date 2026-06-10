# bubblewrap

许多容器运行时工具（如 `systemd-nspawn`、`docker` 等）主要面向系统管理员和编排工具（例如 Kubernetes），旨在提供运行容器的基础设施。这些工具不适合交给非特权用户使用，因为利用此类访问权限轻易就能在宿主机上获取完全特权的 root shell。

## 用户命名空间（user namespaces）

Linux 内核中有一个称为**用户命名空间（user namespaces）**的特性，它允许非特权用户使用容器功能。bubblewrap 利用这些特性来构建沙箱环境，使得任何用户都可以使用该工具。

历史上，对于不支持非特权用户命名空间的系统，bubblewrap 也曾支持过 setuid 模式。不过该模式已被移除。

原始的 bubblewrap 代码诞生于用户命名空间出现之前——它继承了 [xdg-app helper](https://cgit.freedesktop.org/xdg-app/xdg-app/tree/common/xdg-app-helper.c?id=4c3bf179e2e4a2a298cd1db1d045adaf3f564532) 的代码，而该代码又间接源自 [linux-user-chroot](https://git.gnome.org/browse/linux-user-chroot)。

## 系统安全性

该工具的维护者认为，即使与发行版中安装的典型软件结合使用，它也不会导致权限提升。不过，它可能会增加已登录用户发起拒绝服务（DoS）攻击的能力。

特别是，bubblewrap 会使用 `PR_SET_NO_NEW_PRIVS` 来禁用 setuid 二进制文件，这是退出 chroot 等环境的传统方式之一。

## 沙箱安全性

bubblewrap 是一个用于构建沙箱环境的工具。它本身并不是一个具有特定安全策略的完整、开箱即用的沙箱。

bubblewrap 的部分使用场景需要在沙箱与真实系统之间建立安全边界；而其他场景则希望能够为沙箱内的进程更改文件系统布局，但并不旨在充当安全边界。因此，沙箱进程与宿主机之间的保护级别完全由传递给 bubblewrap 的参数决定。

任何负责为 bubblewrap 构造命令行参数的程序（通常是 Flatpak、libgnome-desktop、sandwine 等较大框架或临时脚本）都需自行定义其安全模型，并选择合适的 bubblewrap 命令行参数来实现该安全模型。

沙箱安全性中需要特别注意的某些方面将在下方的 [Limitations](#limitations) 章节中进行说明。

## 用户

该程序可由所有执行非 root 操作的容器工具共享，例如：
 - [Flatpak](https://www.flatpak.org)
 - [rpm-ostree unprivileged](https://github.com/projectatomic/rpm-ostree/pull/209)
 - [bwrap-oci](https://github.com/projectatomic/bwrap-oci)

我们也希望能在 Kubernetes/OpenShift 集群中提供此工具。允许非特权用户使用容器功能将显著简化交互式调试等场景的操作。

## 安装

大多数 Linux 发行版的软件包仓库中都已收录 bubblewrap，可直接从中安装。
如果你需要从源码构建 bubblewrap，可以使用 meson：

```sh
meson _builddir
meson compile -C _builddir
meson test -C _builddir
meson install -C _builddir
```

## 用法

bubblewrap 的工作原理是创建一个新的、完全空的挂载命名空间（mount namespace），其根目录位于一个对宿主机不可见的 tmpfs 上，并在最后一个进程退出时自动清理。随后，你可以使用命令行选项来构建该命名空间内的根文件系统、进程环境以及要运行的命令。

源码中包含一个更完整的 [demo script](./demos/bubblewrap-shell.sh)，这里提供一个精简版本，它启动一个新 shell 并复用宿主机的 `/usr`：

```
bwrap \
    --ro-bind /usr /usr \
    --symlink usr/lib64 /lib64 \
    --proc /proc \
    --dev /dev \
    --unshare-pid \
    --new-session \
    bash
```

这是一个不完整的示例，但有助于说明原理。实际上，你通常不会使用宿主机的文件系统树来创建容器，而是针对一个 chroot 环境进行操作。在这种情况下，你可能不需要在 tmpfs 中创建 `lib64 -> usr/lib64` 的软链接，因为该链接可能已经存在于目标根文件系统中了。

## 沙箱机制

bubblewrap 的目标是在沙箱中运行应用程序，限制其对操作系统部分功能或用户数据（如主目录）的访问。
bubblewrap 始终会创建一个新的挂载命名空间，用户可以精确指定沙箱中应可见的文件系统部分。你指定的任何此类目录默认都会以 `nodev` 选项挂载，并且可以设置为只读。

此外，你还可以利用以下内核特性：

- **用户命名空间（CLONE_NEWUSER）**：此功能对沙箱隐藏除当前 uid 和 gid 之外的所有标识。你也可以更改沙箱中 uid/gid 的值。
- **IPC 命名空间（CLONE_NEWIPC）**：沙箱将获得一份独立的 IPC（进程间通信）副本，例如 SysV 共享内存和信号量。
- **PID 命名空间（CLONE_NEWPID）**：沙箱将看不到任何外部进程。此外，bubblewrap 会在你的容器内运行一个简化的 pid1 进程，以处理回收子进程的需求。这避免了目前众所周知的 [Docker pid 1 问题](https://blog.phusion.nl/docker-and-the-pid-1-zombie-reaping-problem/)。
- **网络命名空间（CLONE_NEWNET）**：沙箱将无法访问宿主机网络，而是拥有自己的网络命名空间，仅包含一个回环设备（loopback）。
- **UTS 命名空间（CLONE_NEWUTS）**：沙箱将拥有独立的 hostname。
- **Seccomp 过滤器**：你可以传入 seccomp 过滤器，以限制在沙箱中允许执行的系统调用。更多信息请参阅 [Seccomp](https://en.wikipedia.org/wiki/Seccomp)。

## Limitations（局限性）

正如上文 [Sandbox security](#sandbox-security) 章节所述，沙箱进程与宿主机之间的保护级别完全由传递给 bubblewrap 的参数决定。此处列出一些需要特别注意的方面：

- 如果你未使用 seccomp 过滤器过滤 `TIOCSTI` 命令，则必须添加参数 `--new-session` 以防止沙箱外的命令执行（参见 [CVE-2017-5226](https://github.com/containers/bubblewrap/issues/142)）。
- 挂载到沙箱中的所有内容都可能被用于权限提升。例如，如果你将 D-Bus socket 挂载到沙箱中，它可能被用来通过 systemd 执行命令。你可以使用 [xdg-dbus-proxy](https://github.com/flatpak/xdg-dbus-proxy) 来过滤 D-Bus 通信。
- 某些应用程序会部署自己的沙箱机制，而这些机制可能会受到 bubblewrap 沙箱约束的限制。例如，一些通过 seccomp 配置子进程以禁止访问文件系统的 Web 浏览器。如果你限制了系统调用并禁用了 seccomp 相关 syscall，浏览器将无法应用这些限制。同样，如果这些规则被编译到沙箱内不可用的文件中，浏览器也无法从该文件加载规则并应用限制。

## 相关项目对比：Firejail

[Firejail](https://github.com/netblue30/firejail/tree/HEAD/src/firejail) 在 bubblewrap 从 Flatpak 中拆分出来之前，与 Flatpak 类似，它将一个 setuid 工具与大量桌面特定的沙箱功能结合在一起。例如，Firejail 原生支持 Pulseaudio，而 bubblewrap 则不支持。

bubblewrap 的维护者认为，审计一个小型的 setuid 程序要容易得多，并且像 Pulseaudio 过滤这样的功能应作为非特权进程保留（正如现在 Flatpak 中的做法）。

此外，@cgwalters 认为尝试[白名单文件路径](https://github.com/netblue30/firejail/blob/37a5a3545ef6d8d03dad8bbd888f53e13274c9e5/src/firejail/fs_whitelist.c#L176)是个糟糕的主意，因为用户操纵路径的方式多种多样，系统管理员配置系统的途径也千差万别。bubblewrap 的做法是仅保留少数特定的 Linux 能力（如 `CAP_SYS_ADMIN`），但始终以调用者的 uid 访问文件系统。这能彻底杜绝此类 [TOCTTOU 攻击](https://cwe.mitre.org/data/definitions/367.html)。

## 相关项目对比：Sandstorm.io

[Sandstorm.io](https://sandstorm.io/) 需要非特权用户命名空间来设置其沙箱，尽管它也可以轻松适配为 setuid 模式运行。@cgwalters 认为他们的代码相当不错，但统一使用 bubblewrap 仍有一定合理性。然而，Sandstorm 的 @kentonv 认为，虽然原则上可行，但目前迁移成本高于实际收益。该决定未来可能会重新评估，但目前并未积极推进。

## 相关项目对比：runc/binctr

[runC](https://github.com/opencontainers/runc) 目前正在支持[无根容器（rootless containers）](https://github.com/opencontainers/runc/pull/774)，无需在运行 runC 的安装、创建和管理过程中使用 `setuid` 或其他特权（而是采用非特权用户命名空间）。不过，runC 的标准使用模式与 [systemd nspawn](https://www.freedesktop.org/software/systemd/man/systemd-nspawn.html) 类似，即设计为供 root 调用的工具。

bubblewrap 的维护者认为，runc 和 systemd-nspawn 并非设计用于 setuid 模式，且距离支持该模式尚远。不过，借助无根容器功能，runC 将能够覆盖 bubblewrap 支持的某些使用场景（同时具备标准化且完整的 OCI 运行时优势）。

[binctr](https://github.com/jfrazelle/binctr) 仅是 runC 的一个包装器，因此继承了其所有的设计权衡。

## 为什么叫这个名字？！

选择 `bubblewrap` 这个名字是为了传达这样一个概念：该工具作为应用程序的父进程运行（某种意义上将其包裹），并在其周围创建一个保护层（即沙箱）。

![](bubblewrap.jpg)

（由 [dancing_stupidity](https://www.flickr.com/photos/27549668@N03/) 绘制的 bubblewrap 猫）
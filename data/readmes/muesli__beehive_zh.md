# Beehive
=======

[![Build Status](https://travis-ci.org/muesli/beehive.svg?branch=master)](https://travis-ci.org/muesli/beehive)
[![Go ReportCard](https://goreportcard.com/badge/muesli/beehive)](https://goreportcard.com/report/muesli/beehive)
[![GoDoc](https://godoc.org/github.com/golang/gddo?status.svg)](https://godoc.org/github.com/muesli/beehive)

Beehive 是一个事件与智能体（agent）系统，允许你创建自己的智能体来执行由事件和过滤器触发的自动化任务。它采用模块化设计，灵活且易于扩展。Beehive 包含多个模块（我们称之为 *Hive*），因此它可以与 Twitter、Tumblr、电子邮件、IRC、Jabber、RSS、Jenkins、Hue 等平台进行交互、通信或获取信息——仅举几例。你可以在我们的 Wiki 中查看 [可用的 Hive 完整列表](https://github.com/muesli/beehive/wiki/Available-Hives)。

将这些模块相互连接，你就能构建出极具价值的智能体。

#### Beehive 能为你做的一些示例：
* 将推文重新发布到你的 Tumblr 博客上
* 转发收到的聊天消息到你的邮箱
* 当温度降至特定阈值以下时，自动开启供暖系统
* 运行你自己的 IRC 机器人，让你能够触发 Jenkins CI 的构建任务
* 控制你的 Hue 照明系统
* 当某只股票价格跌破设定值时通知你

![beehive's Logo](/assets/logo_256.png?raw=true)

## 安装

### 软件包与二进制文件

- Arch Linux：beehive（[AUR](https://aur.archlinux.org/packages/beehive/)）
- [Linux 静态版 64位](https://github.com/muesli/beehive/releases/download/v0.4.0/beehive_0.4.0_Linux_x86_64.tar.gz)
- [Linux 静态版 armv6](https://github.com/muesli/beehive/releases/download/v0.4.0/beehive_0.4.0_Linux_armv6.tar.gz)
- [macOS 64位](https://github.com/muesli/beehive/releases/download/v0.4.0/beehive_0.4.0_Darwin_x86_64.tar.gz)
- [Windows 64位](https://github.com/muesli/beehive/releases/download/v0.4.0/beehive_0.4.0_Windows_x86_64.tar.gz)

你可以在[这里](https://github.com/muesli/beehive/releases)找到更多官方发行版。

### 部署工具
- Docker：`docker run --name beehive -d -p 8181:8181 fribbledom/beehive`
- [Ansible](https://github.com/morbidick/ansible-role-beehive)

### 从源码构建

Beehive 需要 Go 1.13 或更高版本。请确保你的环境中已正确安装并配置好 Go。详见[安装指南](https://golang.org/doc/install.html)。

推荐的做法是拉取源码后运行 `make`。

    git clone --recursive https://github.com/muesli/beehive.git
    cd beehive
    make

你也可以像安装其他 Go 项目一样使用 `go get` 构建并安装 `beehive` 二进制文件，但需要确保 Beehive 能够找到其资源文件（图片、JavaScript、CSS 等）。更多详细信息请参阅“故障排除与注意事项”部分。

运行 `beehive --help` 可查看完整的参数列表。

## 配置

你可以将 Hive 视为小型插件，通过定义可响应的事件（event）和可执行的操作（action），来扩展 Beehive 的功能。

例如，Twitter 插件可以：
 - 响应你关注的人发布的推文（事件）
 - 为你发布新推文（操作）
 - ……

或者 RSS 插件可以让你：
 - 监控 RSS 订阅源并响应新的内容项（另一种事件）

以及邮件插件让你能够：
 - 发送邮件（另一种操作）

每个 Hive 允许你在其中创建一只或多只 Bee，它们彼此独立运行。这使得你可以创建独立的插件实例，例如：为私人邮箱创建一个邮件 Bee，再为工作邮箱创建另一个。

### 创建 Bee

听起来很复杂？其实不然！为了演示，我们来配置一下：每当 RSS 订阅源更新时，让 Beehive 给你发一封邮件。启动 `beehive` 并在浏览器中打开 <http://localhost:8181/>。请注意，除非你通过 `-config` 选项指定了其他文件，否则 Beehive 会在当前工作目录下自动生成配置文件 `beehive.conf`。

注意：如果你使用 `go build` 而非 `make` 构建 Beehive，则必须在源码目录下启动 `beehive`，以便它找到管理界面所需的所有资源。详情请参阅本 README 的“故障排除与注意事项”部分。

管理界面会列出所有可用的 Hive。我们需要在这里创建两只 Bee，一只用于 RSS 订阅源，另一只用于你的邮箱账号。

![New Bees](https://github.com/muesli/beehive-docs/raw/master/screencaps/new_bees.gif)

### 配置 Chain（链）

接下来我们需要创建一个新的 Chain，将刚才创建的两只 Bee 连接起来。首先选择我们要响应的事件与对应的 Bee，然后选择要执行操作的 Bee。RSS-Bee 的事件提供了一组可用的参数：例如内容项的标题、链接和描述等。你可以利用内置的模板语言对这些参数进行处理和组合。例如我们可以将邮件内容设置为：

```
Title: {{.title}} - Link: {{index .links 0}}
```

每当该操作被执行时，Beehive 会将 `{{.title}}` 替换为 RSS 事件中的 `title` 参数（即获取到的内容项标题）。同理，`{{index .links 0}}` 会被替换为该事件的 `links` 数组中的第一个 URL。

![New Chain](https://github.com/muesli/beehive-docs/raw/master/screencaps/new_chain.gif)

配置完成！每当 RSS 订阅源更新时，Beehive 就会给你发送邮件了。让不同的 Bee 无缝协作并为你执行各种智能操作非常简单。不妨亲自试一试！

关于如何配置 Beehive 的更多详情和示例，请参阅[我们的 Wiki](https://github.com/muesli/beehive/wiki/Configuration)。

## 故障排除与注意事项

默认情况下，Web 界面及其他资源文件已嵌入到二进制文件中。如果使用 `make noembed` 构建，Beehive 会尝试在当前工作目录下查找这些文件。因此，如果你计划使用 Web 界面，建议从 Git 仓库目录内启动 Beehive。

如果仍然无法访问 Web 界面，请检查 Git 仓库中的 `config` 目录是否为空。如果是空的，请运行 `git submodule update --init` 初始化 Git 子模块。

Web 界面目前尚不支持身份验证。默认情况下，Beehive 仅接受来自本地回环地址（loopback）的连接。

若想将 Beehive 绑定到其他网络接口或地址，请使用 `-bind` 和 `-canonicalurl` 参数运行：

    beehive -bind "192.168.0.1:8181" -canonicalurl "http://192.168.0.1:8181"

或者

    docker run --name beehive -d -e CANONICAL_URL="http://192.168.0.1:8181" -p 8181:8181 fribbledom/beehive

## 开发

需要帮助？想自己开发 Hive？欢迎加入我们的 IRC（irc://freenode.net/#beehive）或 [Gitter](https://gitter.im/the_beehive/Lobby)。也可以在 [Twitter](https://twitter.com/beehive_app) 上关注 Beehive！
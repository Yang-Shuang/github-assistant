# <img src="/docs/template/logo.png" alt="DeepMind Lab">

*DeepMind Lab* 是一个基于 id Software 的 [Quake III Arena](https://github.com/id-Software/Quake-III-Arena)、[ioquake3](https://github.com/ioquake/ioq3) 以及[其他开源软件](#upstream-sources) 构建的 3D 学习环境。

<div align="center">
  <a href="https://www.youtube.com/watch?v=M40rN7afngY" target="_blank">
    <img src="http://img.youtube.com/vi/M40rN7afngY/0.jpg"
         alt="DeepMind Lab - Nav Maze Level 1"
         width="240" height="180" border="10" />
  </a>
  <a href="https://www.youtube.com/watch?v=gC_e8AHzvOw" target="_blank">
    <img src="http://img.youtube.com/vi/gC_e8AHzvOw/0.jpg"
         alt="DeepMind Lab - Stairway to Melon Level"
         width="240" height="180" border="10" />
  </a>
  <a href="https://www.youtube.com/watch?v=7syZ42HWhHE" target="_blank">
    <img src="http://img.youtube.com/vi/7syZ42HWhHE/0.jpg"
         alt="DeepMind Lab - Laser Tag Space Bounce Level (Hard)"
         width="240" height="180" border="10" />
  </a>
  <br /><br />
</div>

*DeepMind Lab* 为学习智能体（agent）提供了一系列具有挑战性的 3D 导航与解谜任务。其主要目的是作为人工智能研究，尤其是深度强化学习的测试平台。

## About

**免责声明：** 本产品并非 Google 官方产品。

如果你在研究中使用了 *DeepMind Lab* 并希望引用该环境，建议引用 [DeepMind Lab 论文](https://arxiv.org/abs/1612.03801)。

你可以通过 [lab@deepmind.com](mailto:lab@deepmind.com) 联系我们。

## Getting started on Linux

* 从 [bazel.io](https://docs.bazel.build/versions/master/install.html) 获取 Bazel。

* 克隆 DeepMind Lab，例如运行以下命令：

```shell
$ git clone https://github.com/deepmind/lab
$ cd lab
```

若要查看随机智能体的实时演示示例，请运行：

```shell
lab$ bazel run :python_random_agent --define graphics=sdl -- \
               --length=10000 --width=640 --height=480
```

此处提供了一些[更详细的构建文档](/docs/users/build.md)，其中包括如何安装依赖项（如果你尚未安装的话）。

若要启用编译器优化，请在每个 `bazel build`、`bazel test` 和 `bazel run` 命令中传入参数 `--compilation_mode=opt`（或简写为 `-c opt`）。出于简洁考虑，示例中省略了该参数，但在实际训练与评估等对性能有要求的场景中应使用此参数。

### Play as a human

若要使用人类输入控件测试游戏，请运行：

```shell
lab$ bazel run :game -- --level_script=tests/empty_room_test --level_setting=logToStdErr=true
# or:
lab$ bazel run :game -- -l tests/empty_room_test -s logToStdErr=true
```

不设置 `logToStdErr` 可禁用大部分日志输出。

若要打印环境暴露的观测值，只需为每个感兴趣的观测添加 `--observation OBSERVATION_NAME` 参数即可。该参数将在每一步输出对应的观测值：

```shell
lab$ bazel run :game -- --level_script=lt_chasm --observation VEL.TRANS --observation VEL.ROT
```

### Train an agent

*DeepMind Lab* 自带一个位于 [`python/random_agent.py`](python/random_agent.py) 的随机智能体示例，可作为实现学习智能体的起点。若要使用该智能体与 DeepMind Lab 交互进行训练，请运行：

```shell
lab$ bazel run :python_random_agent
```

智能体与环境的交互使用 [Python API](/docs/users/python_api.md)。我们还提供了对 DeepMind 强化学习通用 API "[dm_env](https://github.com/deepmind/dm_env)" 的绑定支持，以及构建独立 PIP 包的方法；详见[单独文档](python/pip_package/README.md)。

*DeepMind Lab* 自带[多种关卡](/docs/levels.md)，实现了不同的任务。这些任务可使用 Lua 脚本进行配置，具体说明见 [Lua API](/docs/developers/reference/lua_api.md)。

-----------------

## Upstream sources

*DeepMind Lab* 基于 ioquake3 游戏引擎构建，并使用 `q3map2` 和 `bspc` 工具进行地图创建。来自这些上游项目的 bug 修复与代码清理工作，建议优先在上游仓库完成修复，然后再合并到 *DeepMind Lab* 中。

* `bspc` 取自 [github.com/TTimo/bspc](https://github.com/TTimo/bspc)，版本为 d9a372db3fb6163bc49ead41c76c801a3d14cf80。我们几乎没有进行本地修改，尽管我们将此代码与主 ioq3 代码进行了集成，且未使用其 `deps` 目录中的副本。我们认为该代码是稳定的。

* `q3map2` 取自 [github.com/TTimo/GtkRadiant](https://github.com/TTimo/GtkRadiant)，版本为 d3d00345c542c8d7cc74e2e8a577bdf76f79c701。我们进行了一些微小的本地修改以添加同步功能。我们认为该代码也是稳定的。

* `ioquake3` 取自 [github.com/ioquake/ioq3](https://github.com/ioquake/ioq3)，版本为 29db64070aa0bae49953bddbedbed5e317af48ba。该代码包含大量的修改与新增内容。我们计划偶尔合并上游的更新。

非常感谢这些仓库维护者在维护高质量代码库方面所付出的辛勤努力。

## External dependencies, prerequisites and porting notes

*DeepMind Lab* 目前仅提供源代码形式发布。它依赖少数几个外部软件库，我们采用多种方式提供这些依赖：

 * `zlib`、`glib`、`libxml2`、`jpeg` 和 `png` 库被引用为外部 Bazel 源，并提供了相应的 Bazel BUILD 文件。依赖代码本身应具有较高的可移植性，但我们提供的 BUILD 规则仅针对 x86 Linux 平台定制。若要在其他平台上构建，你可能需要编辑这些 BUILD 文件。

 * 本包包含了消息摘要算法（位于 `//third_party/md`），取自各自 RFC 的参考实现。此外还包含了一个“通用强化学习 API”（位于 `//third_party/rl_api`），该部分代码同样由 *DeepMind Lab* 作者创建。此段代码具有可移植性。

 * 本包包含了 EGL 头文件（位于 `//third_party/GL/{[`EGL`](third_party/GL/EGL)`,`[`KHR`](third_party/GL/KHR)`}`），取自 Khronos OpenGL/OpenGL ES XML API Registry（[www.khronos.org/registry/EGL](http://www.khronos.org/registry/EGL/)）。头文件经过轻微修改，以移除 EGL 对 X11 的依赖。

 * 还需要几个额外的库，但未以任何形式随包提供；它们必须已存在于你的系统中：
   * SDL 2
   * gettext（`glib` 所需依赖）
   * OpenGL：人类玩家进行硬件加速游戏需要相应的硬件驱动与库。机器学习智能体使用的无头（headless）库可根据 `--define headless=...` 构建设置，选择通过 EGL 或 GLX 进行硬件加速渲染，或通过 OSMesa 进行软件渲染。
   * Python 2.7（其他版本可能也可用），需安装 NumPy、PIL（部分测试要求 NumPy 版本至少为 1.8）；或者使用 Python 3（至少 3.5），需安装 NumPy 和 Pillow。

构建规则使用了一些仅针对 GCC 的编译器设置。如果你的编译器无法识别某些参数（通常是特定的警告抑制标志），你可能需要手动编辑这些标志。这些警告通常只是输出较多，但无害。
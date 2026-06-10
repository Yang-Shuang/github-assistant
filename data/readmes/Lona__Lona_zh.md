<p align="center">
  <img src="studio/LonaStudio/Assets.xcassets/AppIcon.appiconset/icon_256x256@2x.png" width="256" height="256" />
</p>

<h1 align="center">Lona（开发者预览版）</h1>

<br />

> 该项目处于早期阶段，文档尚不完善——但经过一定摸索后，你可以非常有效地使用它。如果你有兴趣参与贡献或在公司内部使用，欢迎提交 GitHub Issue 或通过 Twitter [@dvnabbott](https://twitter.com/dvnabbott) 联系我。我目前正协助少数几位早期采用者。
> Airbnb 不为该项目提供官方支持。其代码和自动化测试的技术严谨性与其他 Airbnb 项目相比尚有差距。

## 概述

[![Build Status](https://travis-ci.org/airbnb/Lona.svg?branch=master)](https://travis-ci.org/airbnb/Lona)

Lona 是一套用于构建设计系统，并利用该系统生成跨平台 UI 代码、Sketch 文件及其他产物的工具集合。

Lona 主要由以下三个部分组成：

- [Lona Components](#lona-components) - 用于跨平台组件的数据格式（`.component`）
- [Lona Studio](#lona-studio) - 用于设计 `.component` 文件的图形界面（GUI）工具
- [Lona Compiler](#lona-compiler) - 从 `.component` 文件生成 UI 代码的命令行工具（CLI）与 API

为什么选择 Lona？了解更多关于大规模跨平台设计系统面临的挑战，以及 Lona 如何解决这些问题的详情，请查看[此处](./docs/overview/background.md)。

### Lona Components

设计系统在 JSON 中定义为一组集合：

- 组件（支持嵌套）
- 颜色、文本样式、渐变和阴影
- 数据类型

这些文件的规范详见 [文档](./docs/file-formats/README.md)。

### Lona Studio

Lona Studio 提供了用于操作 `.component` 文件的图形界面。

Lona Studio 主要用于构建组件系统，但也可用于以下场景：

- 基于现有组件快速搭建新页面原型
- 使用 JSON 文件或 API 的真实数据查看设计稿
- 在不同屏幕尺寸下测试设计方案
- 自动化设计任务，例如为不同语言本地化截图并批量导出数百张图片
- 处理动画（Lottie）并从中渲染视频
- 以及更多功能！

如果你已安装 Xcode，可按照 [安装说明](./studio/README.md) 进行尝试。

> 想知道它是否能替代 Sketch？为什么采用原生 Mac 应用形式？你可以在 [常见问题解答（FAQ）](./docs/overview/faq.md) 中找到一些常见问题的回答。

### Lona Compiler

Lona Compiler 负责将 `.component` 文件转换为面向不同平台的 UI 代码。

目前支持以下目标平台：

- iOS / macOS（Swift）
- React DOM / React Native / React Sketchapp（JavaScript）

计划支持：

- Android（Kotlin）

目前功能最完善的目标平台是 Swift，但整体仍较为粗糙。如果你想尝试使用，请查看 [安装说明](./compiler/core/README.md)。

如需查看生成的代码示例，请参考 [测试用例](./examples/generated/test)

## 核心团队

- 由 [@dvnabbott](https://twitter.com/dvnabbott) 创建
- 设计工具集成与基础设施开发由 [@mathieudutour](https://twitter.com/mathieudutour) 负责

### 贡献者

- Lona Compiler 开发：[@outdooricon](https://github.com/outdooricon)
- 设计与开发支持：[@ryngonzalez](https://twitter.com/ryngonzalez)
- Logo 设计：[@pablocar0](https://twitter.com/pablocar0)
- Lona Studio 开发：[Nghia Tran](https://github.com/NghiaTranUIT)
- Swift 代码生成支持：[Laura Skelton](https://twitter.com/skelovenko)
- Lona Compiler 开发：[Jason Zurita](https://twitter.com/jasonalexzurita)
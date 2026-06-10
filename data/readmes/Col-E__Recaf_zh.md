# Recaf [![Discord](https://dcbadge.limes.pink/api/server/https://discord.gg/Bya5HaA?style=flat)](https://discord.gg/Bya5HaA) [![codecov](https://codecov.io/gh/Col-E/Recaf/graph/badge.svg?token=N8GslpI1lL)](https://codecov.io/gh/Col-E/Recaf)  ![downloads](https://img.shields.io/github/downloads/Col-E/Recaf/total.svg) [![Contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](CONTRIBUTING.md)

![Recaf 4x UI](recaf.png)

Recaf 是一款易于使用的现代 Java 字节码编辑器，抽象化了 Java 程序的复杂细节。

## 下载
- [启动器（Launcher）](https://github.com/Col-E/Recaf-Launcher)
  - 使用说明与操作指南请参阅启动器仓库
- [快照版本（Snapshot releases）](https://github.com/Col-E/Recaf-Launcher/blob/master/MANUAL.md)
  - 发布制品请参见 [CI 构建任务](https://github.com/Col-E/Recaf/actions/workflows/build.yml)
- [独立发行版（Independent releases）](https://github.com/Col-E/Recaf/releases) _(目前暂无 4X 版本)_

## 功能特性
- 轻松编辑 Java 字节码，支持高级或低级操作 _(省去了繁琐的干扰部分)_
    - Recaf 编辑器抽象化了编译后 Java 应用的复杂细节，例如：
        - 常量池（Constant pool）
        - 栈帧计算（Stack frame calculation）
        - 按需使用宽指令（Wide instructions）
        - 以及更多！
- 易于使用的可导航界面，支持上下文敏感操作
- 同时支持标准 Java 和 Android 应用
- 内置多种反编译器供切换，所有参数均可完全自定义配置
- 内置编译器，支持重新编译已反编译的类，即使部分引用的类缺失也能尝试处理 *（具体支持情况取决于代码复杂度和混淆程度）*
- 提供语法简洁的字节码汇编器及配套工具
    - 随时查看方法中局部变量和栈值的状态
    - 支持通过名称而非索引访问变量，使反汇编代码更清晰易读
    - 自动将 Java 源代码片段转换为字节码序列
- 支持搜索多种内容：字符串/数值常量、类与成员引用、指令模式等
- 代码去混淆工具集
    - 当在 Recaf 中打开恶意构造的 class 文件时，会自动进行修复以阻止其导致逆向工程工具崩溃
    - 按照 JVM 的标准读取特制的 jar/zip 文件，绕过可能误导逆向工具显示错误数据的隐藏技巧
    - 支持自动重命名被混淆的类及其成员
    - 支持手动重命名类及其成员 *（并可将这些映射关系导出为多种格式，供其他工具使用）*
    - 提供字节码转换器，用于简化常见的混淆策略
- 支持附加到正在运行的 Java 进程，并提供插桩（Instrumentation）能力
- 以及更多功能...

完整的功能列表请参阅[用户文档](https://recaf.coley.software/user/index.html)。

## 脚本与插件
Recaf 通过模块化 API 暴露了其几乎全部功能。你可以轻松使用脚本来自动化操作，或在更复杂的场景中使用插件。此外，还可以通过插件添加额外功能，这些插件可以在提供相应钩子（Hooks）的 API 中注册回调。

如需创建自己的脚本或插件，请参阅[开发者文档](https://recaf.coley.software/dev/index.html)中的“插件与脚本”章节。

## 命令行
Recaf 可作为命令行应用程序运行，这在配合启动时提供的脚本使用时尤为方便。你可以通过传入 `--help` 参数查看所有当前的启动选项。

## 开发环境搭建
通过以下命令克隆仓库：`git clone https://github.com/Col-E/Recaf.git`
在 IDE 中打开项目，或使用 Gradle 生成构建文件。

**使用 IDE**：
1. 从 `build.gradle` 文件导入项目
2. 创建运行配置，主类设置为 `software.coley.recaf.Main`

**不使用 IDE**：
1. 执行 `gradlew build`
    - 构建产物路径为：`recaf-ui/build/libs/recaf-ui-{VERSION}-all.jar`
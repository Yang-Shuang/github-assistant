<picture align="center">
  <source media="(prefers-color-scheme: dark)" srcset="./static/mobilerun-dark.png">
  <source media="(prefers-color-scheme: light)" srcset="./static/mobilerun.png">
  <img src="./static/mobilerun.png"  width="full">
</picture>

<p align="center">
  <strong>Mobilerun is an open-source framework for controlling Android and iOS devices with LLM agents.</strong><br>
  **Mobilerun 是一个开源框架，用于通过大语言模型（LLM）智能体控制 Android 和 iOS 设备。**<br>
  It gives agents mobile-native tools to inspect UI state, understand screenshots, tap, swipe, type, plan multi-step workflows, and return results through a CLI or Python API.
  **它为智能体提供了移动原生工具，用于检查 UI 状态、理解截图、执行点击/滑动/输入操作、规划多步工作流，并通过 CLI 或 Python API 返回结果。**
</p>

<div align="center">

<a href="https://docs.mobilerun.ai">📕 Documentation</a>
·
<a href="https://cloud.mobilerun.ai">☁️ Mobilerun Cloud</a>

[![GitHub stars](https://img.shields.io/github/stars/droidrun/mobilerun?style=social)](https://github.com/droidrun/mobilerun/stargazers)
[![mobilerun.ai](https://img.shields.io/badge/mobilerun.ai-white)](https://mobilerun.ai)
[![Twitter Follow](https://img.shields.io/twitter/follow/mobilerun_ai?style=social)](https://x.com/mobilerun_ai)
[![Discord](https://img.shields.io/discord/1360219330318696488?color=white&label=Discord&logo=discord&logoColor=white)](https://discord.gg/ZZbKEZZkwK)
[![Benchmark](https://img.shields.io/badge/Benchmark-91.4﹪-white)](https://mobilerun.ai/benchmark)



<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://api.producthunt.com/widgets/embed-image/v1/top-post-badge.svg?post_id=983810&theme=dark&period=daily&t=1753948032207">
  <source media="(prefers-color-scheme: light)" srcset="https://api.producthunt.com/widgets/embed-image/v1/top-post-badge.svg?post_id=983810&theme=neutral&period=daily&t=1753948125523">
  <a href="https://www.producthunt.com/products/droidrun-framework-for-mobile-agent?embed=true&utm_source=badge-top-post-badge&utm_medium=badge&utm_source=badge-droidrun" target="_blank"><img src="https://api.producthunt.com/widgets/embed-image/v1/top-post-badge.svg?post_id=983810&theme=neutral&period=daily&t=1753948125523" alt="Droidrun - Give&#0032;AI&#0032;native&#0032;control&#0032;of&#0032;physical&#0032;&#0038;&#0032;virtual&#0032;phones&#0046; | Product Hunt" style="width: 200px; height: 54px;" width="200" height="54" /></a>
</picture>


[Deutsch](https://zdoc.app/de/droidrun/mobilerun) | 
[Español](https://zdoc.app/es/droidrun/mobilerun) | 
[français](https://zdoc.app/fr/droidrun/mobilerun) | 
[日本語](https://zdoc.app/ja/droidrun/mobilerun) | 
[한국어](https://zdoc.app/ko/droidrun/mobilerun) | 
[Português](https://zdoc.app/pt/droidrun/mobilerun) | 
[Русский](https://zdoc.app/ru/droidrun/mobilerun) | 
[中文](https://zdoc.app/zh/droidrun/mobilerun)

</div>


<p align="center">
  <img src="./static/mobilerun-demo.gif" alt="Mobilerun automating a phone with natural language" width="320">
</p>

- 🤖 Control Android and iOS devices with natural language commands -> **🤖 通过自然语言命令控制 Android 和 iOS 设备**
- 🔀 Use OpenAI, Anthropic, Gemini, Ollama, DeepSeek, OpenRouter, and OpenAI-compatible models -> **🔀 支持 OpenAI、Anthropic、Gemini、Ollama、DeepSeek、OpenRouter 以及兼容 OpenAI 的模型**
- 🧠 Run direct tasks or enable reasoning mode for complex multi-step automation -> **🧠 执行直接任务，或启用推理模式（Reasoning Mode）以处理复杂的多步自动化**
- 💻 Automate from the CLI, a terminal UI, Docker, or Python code -> **💻 通过 CLI、终端界面（TUI）、Docker 或 Python 代码实现自动化**
- 🐍 Extend agents with custom tools, structured output, app cards, and credentials -> **🐍 使用自定义工具、结构化输出、应用卡片和凭据扩展智能体功能**
- 📸 Combine accessibility trees with screenshots for visual understanding -> **📸 结合无障碍树（Accessibility Trees）与截图实现视觉理解**
- 🫆 Trace execution with Arize Phoenix or Langfuse -> **🫆 使用 Arize Phoenix 或 Langfuse 追踪执行过程**

Use the framework when you want to run the agent on your machine. Use [Mobilerun Cloud](https://cloud.mobilerun.ai) when you want a ready-to-go solution for your local phones or cloud-hosted virtual/physical phones, managed infrastructure, and API-driven device workflows without running the agent on your local machine. [Check out our benchmark results](https://mobilerun.ai/benchmark).
**如果你希望在本地机器上运行智能体，请使用该框架。如果你需要一个开箱即用的解决方案（用于控制本地手机或云端托管的虚拟/物理手机），并希望获得托管基础设施和基于 API 的设备工作流，而无需在本地运行智能体，请使用 [Mobilerun Cloud](https://cloud.mobilerun.ai)。[查看我们的基准测试结果](https://mobilerun.ai/benchmark)。**

## 📦 Installation

> **Note:** Python 3.14 is not currently supported. Please use Python `>=3.11,<3.14`.
> **注意：** 目前暂不支持 Python 3.14。请使用 Python `>=3.11,<3.14`。

Install Mobilerun with [`uv`](https://docs.astral.sh/uv/):
使用 [`uv`](https://docs.astral.sh/uv/) 安装 Mobilerun：

```bash
# CLI usage
uv tool install mobilerun
```

```bash
# CLI + Python integration
uv pip install mobilerun
```

Most LLM providers are included by default. For Anthropic support, install the optional extra:
大多数大语言模型提供商已默认包含。如需支持 Anthropic，请安装可选依赖：

```bash
uv tool install "mobilerun[anthropic]"
```

## 🚀 Quickstart

```bash
uv tool install mobilerun
mobilerun setup
mobilerun configure
mobilerun run "Open settings and turn on dark mode"
```

Before starting, make sure you have [ADB](https://developer.android.com/studio/releases/platform-tools) installed and an Android device with Developer options and USB debugging enabled. iOS setup is supported separately through the iOS Portal flow.
在开始之前，请确保已安装 [ADB](https://developer.android.com/studio/releases/platform-tools)，并且你的 Android 设备已启用开发者选项和 USB 调试。iOS 设备的设置需通过 iOS Portal 流程单独完成。

### 1. Install the Portal on your device
### 1. 在设备上安装 Portal

```bash
mobilerun setup
```

This installs the Mobilerun Portal app, enables its accessibility service, and prepares the device for local control.
此命令将安装 Mobilerun Portal 应用，启用其无障碍服务，并为本地控制做好准备。

### 2. Verify the connection
### 2. 验证连接

```bash
mobilerun ping
```

You should see confirmation that the Portal is installed and accessible.
你将看到确认信息，表明 Portal 已安装并可正常访问。

### 3. Configure your LLM provider
### 3. 配置大语言模型提供商

```bash
mobilerun configure
```

The wizard walks you through choosing a provider, auth method, and model. You can also use provider environment variables such as `GOOGLE_API_KEY`, `OPENAI_API_KEY`, or `ANTHROPIC_API_KEY`.
向导将引导你选择提供商、认证方式和模型。你也可以直接使用提供商的环境变量，例如 `GOOGLE_API_KEY`、`OPENAI_API_KEY` 或 `ANTHROPIC_API_KEY`。

### 4. Run your first command
### 4. 运行你的第一条命令

```bash
mobilerun run "Open the settings app and tell me the Android version"
```

Useful run options:
**常用运行参数：**

```bash
mobilerun run "Open settings and turn on dark mode"
mobilerun run "What app is currently open?" --vision
mobilerun run "Find a contact named John and send him an email" --reasoning
mobilerun run "Take a screenshot" --ios
mobilerun run "Open Settings" --steps 30 --debug
```

Read the full [framework documentation](https://docs.mobilerun.ai/framework/quickstart).
阅读完整的[框架文档](https://docs.mobilerun.ai/framework/quickstart)。

[![Quickstart Video](https://img.youtube.com/vi/4WT7FXJah2I/0.jpg)](https://www.youtube.com/watch?v=4WT7FXJah2I)

## ⚙️ Features
## ⚙️ 功能特性

- **CLI and TUI:** Run one-off natural language tasks, inspect devices, replay macros, and debug from the terminal. -> **CLI 与终端界面（TUI）：** 执行一次性自然语言任务、检查设备状态、回放宏命令，并在终端中进行调试。
- **Python API:** Build custom mobile automation workflows with Python and use custom tools. -> **Python API：** 使用 Python 构建自定义移动自动化工作流，并集成自定义工具。
- **Android and iOS support:** Control Android through the Portal app or target iOS through the iOS Portal flow. -> **Android 与 iOS 支持：** 通过 Portal 应用控制 Android 设备，或通过 iOS Portal 流程管理 iOS 设备。
- **Portal-based control:** Use UI trees, screenshots, text input, gestures, app launching, and device state from the Portal runtime. -> **基于 Portal 的控制：** 利用 Portal 运行时提供的 UI 树、截图、文本输入、手势操作、应用启动及设备状态进行控制。
- **Vision mode:** Send screenshots to the LLM with `--vision`, or use screenshot-only control with `--vision-only` (useful for the apps that do not have a11y tree information). -> **视觉模式（Vision Mode）：** 使用 `--vision` 将截图发送给大语言模型，或使用 `--vision-only` 进行仅基于截图的控制（适用于没有无障碍树信息的 App）。
- **Reasoning mode:** Use `--reasoning` for manager-executor planning on longer or more complex tasks. -> **推理模式（Reasoning Mode）：** 针对较长或更复杂的任务，使用 `--reasoning` 启用经理-执行者（Manager-Executor）规划机制。
- **Tracing and telemetry:** Debug execution with Arize Phoenix, Langfuse, saved trajectories, and detailed logs. -> **追踪与遥测：** 借助 Arize Phoenix、Langfuse、保存的轨迹记录及详细日志进行调试。
- **Structured output:** Return structured data from mobile workflows. -> **结构化输出：** 从移动工作流中返回结构化数据。
- **App cards and custom tools:** Add app-specific guidance to make agent perform better on your use-cases. -> **应用卡片与自定义工具：** 添加特定于应用的指导信息，以提升智能体在你使用场景中的表现。
- **Docker:** Run Mobilerun in a container for repeatable local environments. -> **Docker：** 在容器中运行 Mobilerun，以创建可复现的本地环境。

## ☁️ Framework vs Cloud
## ☁️ 框架与云端对比

| | Mobilerun Framework | Mobilerun Cloud |
| --- | --- | --- |
| Best for -> **适用场景** | Running agents locally on your own machine and devices -> 在自有机器和设备上本地运行智能体 | Ready-to-go local phone control, hosted real or virtual devices, API workflows, and managed device operations -> 开箱即用的本地手机控制、托管的真实或虚拟设备、API 工作流及托管的设备运维 |
| Runtime -> **运行时环境** | Your machine -> 你的本地机器 | Mobilerun-managed infrastructure -> Mobilerun 托管的基础设施 |
| Interface -> **交互接口** | CLI, TUI, Docker, and Python API -> CLI、TUI、Docker 和 Python API | Dashboard, REST API, SDKs, and hosted devices -> Dashboard（仪表盘）、REST API、SDK 及托管设备 |

Use the framework when you want full local control of the agent runtime. Use [Mobilerun Cloud](https://cloud.mobilerun.ai) when you want managed devices, fleet workflows, or cloud APIs without running the agent locally. Learn more in the [framework overview](https://docs.mobilerun.ai/framework/overview) and the [cloud docs](https://docs.mobilerun.ai).
**如果你希望完全掌控智能体的运行时环境，请使用该框架。如果你需要托管设备、集群工作流或云 API，而无需在本地运行智能体，请使用 [Mobilerun Cloud](https://cloud.mobilerun.ai)。更多详情请参阅[框架概览](https://docs.mobilerun.ai/framework/overview) 和[云端文档](https://docs.mobilerun.ai)。**

### Which should I choose?
### 我应该如何选择？

- Choose **Mobilerun Framework** for local agent execution and code-level control. -> 选择 **Mobilerun Framework** 进行本地智能体执行与代码级控制。
- Choose **Mobilerun Cloud** for managed phones, APIs, and scale without running agents locally. -> 选择 **Mobilerun Cloud** 实现托管手机、API 调用及规模化扩展，无需在本地运行智能体。

### Cloud Device Types
### 云端设备类型

| Device type -> **设备类型** | What it is -> **说明** | Best for -> **适用场景** |
| --- | --- | --- |
| Personal（个人） | Your own hardware connected to Mobilerun Cloud -> 连接到 Mobilerun Cloud 的自有硬件 | Quick automation on devices you own -> 在你拥有的设备上快速实现自动化 |
| Cloud Phone (Hosted)（云端手机-托管） | Instantly available cloud-hosted phone -> 即时可用的云端托管手机 | Scalable hosted automation -> 可扩展的托管自动化 |
| Physical Phone (Hosted)（物理手机-托管） | Real hardware with stronger identity characteristics -> 具备更强身份标识特性的真实硬件 | Workflows that need high device authenticity and trust -> 需要高设备真实性与信任度的工作流 |

## 🎬 Demo Videos
## 🎬 演示视频

### Book accommodation from a prompt
### 通过提示词预订住宿

Shows multi-step navigation, text input, and app-state reasoning while Mobilerun searches for accommodation.
展示了 Mobilerun 搜索住宿时的多步导航、文本输入及应用状态推理过程。

<a href="https://youtu.be/VUpCyq1PSXw">
  <img src="./static/demo-apartment-search.gif" alt="Mobilerun booking accommodation from a prompt" width="800">
</a>

### Find trending content
### 发现热门内容

Shows browsing, app navigation, and result extraction from a natural-language task.
展示了从自然语言任务中进行的浏览、应用导航及结果提取过程。

<a href="https://youtu.be/7V8S2f8PnkQ">
  <img src="./static/demo-reddit-trends.gif" alt="Mobilerun finding trending content from a prompt" width="800">
</a>

### Maintain an app streak
### 保持 App 连续使用记录（打卡）

Shows a short recurring mobile workflow that can be automated from a prompt.
展示了一个简短的循环移动工作流，可通过提示词实现自动化。

<a href="https://youtu.be/B5q2B467HKw">
  <img src="./static/demo-duolingo-streak.gif" alt="Mobilerun maintaining an app streak from a prompt" width="800">
</a>

## 💡 Example Use Cases
## 💡 典型应用场景

- Mobile app QA and regression testing -> 移动端应用测试与回归测试
- Guided workflows for non-technical users -> 面向非技术用户的引导式工作流
- Repetitive task automation on mobile devices -> 移动设备上的重复性任务自动化
- Event-driven automation from schedules, notifications, or custom triggers -> 基于日程、通知或自定义触发器的事件驱动型自动化
- Data extraction from native mobile apps -> 从原生移动端应用提取数据
- Running automations on multiple devices at once -> 同时在多台设备上运行自动化任务

## 📚 Documentation
## 📚 文档资源

- [Framework quickstart](https://docs.mobilerun.ai/framework/quickstart) -> [框架快速入门](https://docs.mobilerun.ai/framework/quickstart)
- [Mobilerun cloud quickstart](https://docs.mobilerun.ai/quickstart) -> [Mobilerun Cloud 快速入门](https://docs.mobilerun.ai/quickstart)
- [Device setup](https://docs.mobilerun.ai/framework/guides/device-setup) -> [设备设置](https://docs.mobilerun.ai/framework/guides/device-setup)
- [CLI guide](https://docs.mobilerun.ai/framework/guides/cli) -> [CLI 指南](https://docs.mobilerun.ai/framework/guides/cli)
- [SDK reference](https://docs.mobilerun.ai/framework/sdk/reference) -> [SDK 参考文档](https://docs.mobilerun.ai/framework/sdk/reference)
- [Custom tools](https://docs.mobilerun.ai/framework/features/custom-tools) -> [自定义工具](https://docs.mobilerun.ai/framework/features/custom-tools)
- [Agent architecture](https://docs.mobilerun.ai/framework/concepts/architecture) -> [智能体架构](https://docs.mobilerun.ai/framework/concepts/architecture)
- [Structured output](https://docs.mobilerun.ai/framework/features/structured-output) -> [结构化输出](https://docs.mobilerun.ai/framework/features/structured-output)
- [Tracing](https://docs.mobilerun.ai/framework/features/tracing) -> [执行追踪](https://docs.mobilerun.ai/framework/features/tracing)

## 👥 Contributing
## 👥 贡献指南

Contributions are welcome. Please feel free to submit a pull request or open an issue.
欢迎贡献代码。请随时提交 Pull Request 或创建 Issue。

## 📄 License
## 📄 许可证

This project is licensed under the MIT License. See [LICENSE](./LICENSE) for details.
本项目采用 MIT 许可证开源。详情请参阅 [LICENSE](./LICENSE)。

## Security Checks
## 🔒 安全检查

To help catch security issues before submitting changes, run:
为在提交更改前发现潜在的安全问题，请运行：

```bash
bandit -r mobilerun
safety scan
```
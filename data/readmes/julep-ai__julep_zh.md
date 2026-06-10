<sup><div align="center">
  <!-- Keep these links. Translations will automatically update with the README. -->
  [Deutsch](https://www.readme-i18n.com/julep-ai/julep?lang=de) | 
  [Español](https://www.readme-i18n.com/julep-ai/julep?lang=es) | 
  [français](https://www.readme-i18n.com/julep-ai/julep?lang=fr) | 
  [日本語](https://www.readme-i18n.com/julep-ai/julep?lang=ja) | 
  [한국어](https://www.readme-i18n.com/julep-ai/julep?lang=ko) | 
  [Português](https://www.readme-i18n.com/julep-ai/julep?lang=pt) | 
  [Русский](https://www.readme-i18n.com/julep-ai/julep?lang=ru) | 
  [中文](https://www.readme-i18n.com/julep-ai/julep?lang=zh)
</div></sup>


<div align="center">

```
      ██╗ ██╗   ██╗ ██║      ███████╗ ██████╗       █████╗  ██╗
      ██║ ██║   ██║ ██║      ██╔════╝ ██╔══██╗     ██╔══██╗ ██║
      ██║ ██║   ██║ ██║      █████╗   ██████╔╝     ███████║ ██║
 ██   ██║ ██║   ██║ ██║      ██╔══╝   ██╔═══╝      ██╔══██║ ██║
 ╚█████╔╝ ╚██████╔╝ ███████╗ ███████╗ ██║          ██║  ██║ ██║
  ╚════╝   ╚═════╝  ╚══════╝ ╚══════╝ ╚═╝          ╚═╝  ╚═╝ ╚═╝
```

<br>
  <p>
   <a href="https://www.npmjs.com/package/@julep/sdk"><img src="https://img.shields.io/npm/v/%40julep%2Fsdk?style=social&amp;logo=npm&amp;link=https%3A%2F%2Fwww.npmjs.com%2Fpackage%2F%40julep%2Fsdk" alt="NPM Version" height="28"></a>
    <span>&nbsp;</span>
    <a href="https://pypi.org/project/julep"><img src="https://img.shields.io/pypi/v/julep?style=social&amp;logo=python&amp;label=PyPI&amp;link=https%3A%2F%2Fpypi.org%2Fproject%2Fjulep" alt="PyPI - Version" height="28"></a>
    <span>&nbsp;</span>
    <a href="https://hub.docker.com/u/julepai"><img src="https://img.shields.io/docker/v/julepai/agents-api?sort=semver&amp;style=social&amp;logo=docker&amp;link=https%3A%2F%2Fhub.docker.com%2Fu%2Fjulepai" alt="Docker Image Version" height="28"></a>
    <span>&nbsp;</span>
    <a href="https://choosealicense.com/licenses/apache/"><img src="https://img.shields.io/github/license/julep-ai/julep" alt="GitHub License" height="28"></a>
  </p>
  
  <h3 align="center">
    <a href="https://discord.com/invite/JTSBGRZrzj" rel="dofollow"><img src="https://user.githubusercontent.com/74038190/235294015-47144047-25ab-417c-af1b-6746820a20ff.gif" width="45"></a>
    ·
    <a href="https://x.com/julep_ai" rel="dofollow"><img src="https://raw.githubusercontent.com/gist/IgnaceMaes/744cd9cf41ec6acf46fc8f4e9f370f86/raw/d16658c2945d30c8a953b35cb17dd7085111b46c/x-logo.svg" width="32"></a>
    ·
    <a href="https://www.linkedin.com/company/julep-ai" rel="dofollow"><img src="https://user.githubusercontent.com/74038190/235294012-0a55e343-37ad-4b0f-924f-c8431d9d2483.gif" width="45"></a>

  </h3>
</div>

**今天就开始使用 Julep：** 访问 **[Julep 官网](https://julep.ai)** · 在 **[Julep 控制台](https://dashboard.julep.ai)** 快速上手（免费 API key）· 阅读 **[文档](https://docs.julep.ai/introduction/julep)**

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
<h3>📖 Table of Contents</h3>

- [为什么选择 Julep？](#why-julep)
- [快速上手](#getting-started)
- [文档与示例](#documentation-and-examples)
- [社区与贡献](#community-and-contributions)
- [许可证](#license)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->




## 为什么选择 Julep？

Julep 是一个开源平台，用于构建基于**智能体（Agent）的 AI 工作流**，其能力远超简单的提示词链。它让你能够编排复杂的、多步骤的流程，结合大型语言模型（LLM）和工具，且**完全无需管理任何基础设施**。借助 Julep，你可以创建具备**记忆过往交互能力**的 AI 智能体，并通过分支逻辑、循环、并行执行以及外部 API 集成来处理复杂任务。简而言之，Julep 就像是为 AI 智能体打造的 *“Firebase”*，为大规模的智能工作流提供强大的后端支持。

**核心特性与优势：**

* **持久化记忆（Persistent Memory）：** 构建能够在对话中保持上下文和长期记忆的 AI 智能体，使其能够随时间推移不断学习和优化。
* **模块化工作流（Modular Workflows）：** 使用条件逻辑、循环和错误处理将复杂任务定义为模块化步骤（支持 YAML 或代码）。Julep 的工作流引擎会自动管理多步骤流程和决策。
* **工具编排（Tool Orchestration）：** 轻松集成外部工具和 API（如网页搜索、数据库、第三方服务等），作为智能体工具箱的一部分。Julep 的智能体可调用这些工具来增强自身能力，支持检索增强生成（RAG）等功能。
* **并行与可扩展：** 为提升效率，可同时运行多个操作，底层由 Julep 自动处理扩缩容和并发。该平台采用无服务器架构，无需额外的运维成本即可无缝扩展工作流。
* **可靠执行：** 无需担心运行异常——Julep 内置重试机制、自修复步骤和完善的错误处理，确保长时任务稳定推进。同时提供实时监控与日志记录，方便你追踪进度。
* **易于集成：** 通过我们的 **Python** 和 **Node.js** SDK 快速上手，或使用 Julep CLI 进行脚本编写。如需直接与其他系统集成，也可使用 Julep 的 REST API。

<img src="./.github/julep.gif"/>

**专注于你的 AI 逻辑与创意，繁重的底层工作交由 Julep 处理！** <img src="https://github.com/Anmol-Baranwal/Cool-GIFs-For-GitHub/assets/74038190/2c0eef4b-7b75-42bd-9722-4bea97a2d532" width="20">



## 快速上手
<p>
    <a href="https://dashboard.julep.ai">
      <img src="https://img.shields.io/badge/Get_API_Key-FF5733?style=logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCIgZmlsbD0id2hpdGUiPjxwYXRoIGQ9Ik0xMiAxTDMgNXYxNGw5IDQgOS00VjVsLTktNHptMCAyLjh2MTYuNEw1IDE2LjJWNi44bDctMy4yem0yIDguMmwtMi0yLTIgMiAyIDIgMi0yeiIvPjwvc3ZnPg==" alt="Get API Key" height="28">
    </a>
    <span>&nbsp;</span>
    <a href="https://docs.julep.ai">
      <img src="https://img.shields.io/badge/Documentation-4B32C3?style=logo=gitbook&logoColor=white" alt="Documentation" height="28">
    </a>
  </p>
快速上手 Julep 非常简单：

1. **注册与获取 API Key：** 首先在 **[Julep 控制台](https://dashboard.julep.ai)** 注册账号并获取你的 API Key（用于验证 SDK 调用）。
2. **安装 SDK：** 为你偏好的语言安装 Julep SDK：

   * <img src="https://user.githubusercontent.com/74038190/212257472-08e52665-c503-4bd9-aa20-f5a4dae769b5.gif" width="20"> **Python：** `pip install julep`
   * <img src="https://user.githubusercontent.com/74038190/212257454-16e3712e-945a-4ca2-b238-408ad0bf87e6.gif" width="20"> **Node.js：** `npm install @julep/sdk`（或 `yarn add @julep/sdk`）
3. **定义智能体：** 使用 SDK 或 YAML 定义一个智能体及其任务工作流。例如，你可以指定智能体的记忆配置、可调用的工具以及分步的任务逻辑。（详见文档中的 **[快速入门](https://docs.julep.ai/introduction/quick-start)** 指南以获取详细步骤。）
4. **运行工作流：** 通过 SDK 调用你的智能体以执行任务。Julep 平台将在云端编排整个工作流，并为你管理状态、工具调用和 LLM 交互。你可以查看智能体的输出结果，在控制台中监控执行情况，并根据需要进行迭代优化。

就是这么简单！你的第一个 AI 智能体只需几分钟即可运行起来。如需完整教程，请查阅文档中的 **[快速入门指南](https://docs.julep.ai/introduction/quick-start)**。

> **注意：** Julep 还提供命令行界面（CLI）（目前 Python 版本处于测试阶段），用于管理工作流和智能体。如果你偏好无代码方式或希望编写脚本处理常见任务，请参阅 **[Julep CLI 文档](https://docs.julep.ai/responses/quickstart#cli-installation)** 获取详细信息。



## 文档与示例

想要深入探索？ **[Julep 文档](https://docs.julep.ai)** 涵盖了掌握该平台所需的一切内容——从核心概念（智能体、任务、会话、工具）到高级主题，如智能体记忆管理和架构内部细节。关键资源包括：

* **[概念指南](https://docs.julep.ai/concepts/)：** 了解 Julep 的架构、会话与记忆的工作原理、工具使用、长对话管理等。
* **[API 与 SDK 参考手册](https://docs.julep.ai/api-reference/)：** 查找所有 SDK 方法和 REST API 端点的详细参考文档，以便将 Julep 集成到你的应用中。
* **[教程](https://docs.julep.ai/tutorials/)：** 分步指南，教你构建实际应用（例如具备网页搜索功能的科研智能体、旅行规划助手或拥有自定义知识库的聊天机器人）。
* **[食谱示例](https://github.com/julep-ai/julep/tree/dev/cookbooks)：** 探索 **Julep Cookbook**，获取现成的示例工作流和智能体。这些示例展示了常见模式和使用场景——通过实例学习的绝佳途径。*浏览本仓库中的 [`cookbooks/`](https://github.com/julep-ai/julep/tree/dev/cookbooks) 目录以查看示例智能体定义。*
* **[IDE 集成](https://context7.com/julep-ai/julep)：** 直接在 IDE 中访问 Julep 文档！在编码时获取即时答案的理想选择。



## 社区与贡献

加入我们不断壮大的开发者与 AI 爱好者社区！以下是参与和支持我们的几种方式：

* **Discord 社区：** 有疑问或想法？加入我们的 **[官方 Discord 服务器](https://discord.gg/7H5peSN9QP)**，与 Julep 团队及其他用户交流。我们很乐意协助排查问题或头脑风暴新用例。
* **GitHub Discussions 与 Issues：** 欢迎使用 GitHub 报告错误、请求新功能或讨论实现细节。如果你想参与贡献，请查看 **[适合新手的问题（good first issues）](https://github.com/julep-ai/julep/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22)**——我们欢迎任何形式的贡献。
* **参与贡献：** 如果你想提交代码或提出改进建议，请参阅我们的 **[贡献指南](.github/CONTRIBUTING.md)** 了解如何开始。我们非常感谢所有的 Pull Request（PR）和反馈。通过协作，我们可以让 Julep 变得更好！

* **小贴士：** <img src="https://github.com/Anmol-Baranwal/Cool-GIFs-For-GitHub/assets/74038190/e379a33a-b428-4385-b44f-3da16e7bac9f" width="35"> 给我们的仓库点个 Star 以获取最新动态——我们会持续添加新功能与示例。    

<br/>

无论贡献大小，对我们都弥足珍贵。让我们一起打造令人惊叹的作品！    <img src="https://github.com/Anmol-Baranwal/Cool-GIFs-For-GitHub/assets/74038190/2c0eef4b-7b75-42bd-9722-4bea97a2d532" width="20">
 <img src="https://user.githubusercontent.com/74038190/216125640-2783ebd5-e63e-4ed1-b491-627a40b24850.png" width="20">

<h4>Our Amazing Contributors:</h4>

<a href="https://github.com/julep-ai/julep/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=julep-ai/julep" />
</a>

<br/>

## 许可证

Julep 基于 **Apache 2.0 许可证** 提供，这意味着你可以免费在自己的项目中使用。详细信息请参阅 **[LICENSE](.github/LICENSE)** 文件。祝你使用 Julep 开发愉快！
<p align='center'>
<img src='./build/icon.png' width="150" height="150" alt="DeepChat AI Assistant Icon" />
</p>

<h1 align="center">DeepChat - 强大的开源 AI Agent 平台</h1>

<p align="center">DeepChat 是一个功能丰富的开源 AI Agent 平台，统一了模型、工具和代理：支持多 LLM 对话、MCP 工具调用、Skills（技能）、ACP 代理集成以及远程控制。</p>

<p align="center">
  <a href="https://github.com/ThinkInAIXYZ/deepchat/stargazers"><img src="https://img.shields.io/github/stars/ThinkInAIXYZ/deepchat" alt="Stars Badge"/></a>
  <a href="https://github.com/ThinkInAIXYZ/deepchat/network/members"><img src="https://img.shields.io/github/forks/ThinkInAIXYZ/deepchat" alt="Forks Badge"/></a>
  <a href="https://github.com/ThinkInAIXYZ/deepchat/pulls"><img src="https://img.shields.io/github/issues-pr/ThinkInAIXYZ/deepchat" alt="Pull Requests Badge"/></a>
  <a href="https://github.com/ThinkInAIXYZ/deepchat/issues"><img src="https://img.shields.io/github/issues/ThinkInAIXYZ/deepchat" alt="Issues Badge"/></a>
  <a href="https://github.com/ThinkInAIXYZ/deepchat/blob/main/LICENSE"><img src="https://img.shields.io/github/license/ThinkInAIXYZ/deepchat" alt="License Badge"/></a>
  <a href="https://github.com/ThinkInAIXYZ/deepchat/releases/latest"><img src="https://img.shields.io/endpoint?url=https://api.pinstudios.net/api/badges/downloads/ThinkInAIXYZ/deepchat/total" alt="Downloads"></a>
  <a href="https://deepwiki.com/ThinkInAIXYZ/deepchat"><img src="https://deepwiki.com/badge.svg" alt="Ask DeepWiki"></a>
</p>

<div align="center">
  <a href="https://trendshift.io/repositories/15162" target="_blank"><img src="https://trendshift.io/api/badge/repositories/15162" alt="ThinkInAIXYZ%2Fdeepchat | Trendshift" style="width: 250px; height: 55px;" width="250" height="55"/></a>
</div>

<div align="center">
  <a href="./README.zh.md">中文</a> / <a href="./README.md">English</a> / <a href="./README.jp.md">日本語</a>
</div>

## 📑 目录

- [📑 目录](#-table-of-contents)
- [🚀 项目简介](#-project-introduction)
- [💡 为什么选择 DeepChat](#-why-choose-deepchat)
- [🔥 核心功能](#-main-features)
- [🧠 Skills（技能）支持](#-skills-support)
- [🧩 ACP 集成（代理客户端协议）](#-acp-integration-agent-client-protocol)
- [📡 远程控制](#-remote-control)
- [🤖 支持的模型提供商](#-supported-model-providers)
  - [兼容任何采用 OpenAI/Gemini/Anthropic API 格式的模型提供商](#compatible-with-any-model-provider-in-openaigeminianthropic-api-format)
- [🔍 应用场景](#-use-cases)
- [📦 快速开始](#-quick-start)
  - [下载与安装](#download-and-install)
  - [配置模型](#configure-models)
  - [开始对话](#start-conversations)
- [💻 开发指南](#-development-guide)
  - [安装依赖](#install-dependencies)
  - [启动开发](#start-development)
  - [构建项目](#build)
- [👥 社区与贡献](#-community--contribution)
- [⭐ Star 历史](#-star-history)
- [👨‍💻 贡献者](#-contributors)
- [📃 许可证](#-license)

## 🚀 项目简介

无论你是使用 OpenAI、Gemini、Anthropic 等云端 API，还是本地部署的 Ollama 模型，DeepChat 都能提供流畅的用户体验。它是一款强大的开源 AI Agent 平台，将模型、工具和代理运行时整合到一个桌面应用中。

除了对话功能，DeepChat 还支持智能体工作流：通过 MCP（模型上下文协议）实现丰富的工具调用、可安装的 Skills 用于特定任务、独特的 ACP（代理客户端协议）集成允许将兼容的 ACP 代理作为一等公民“模型”运行并提供专用工作区 UI，以及来自聊天应用的远程控制。

<table align="center">
  <tr>
    <td align="center" style="padding: 10px;">
      <img src='https://github.com/user-attachments/assets/6e932a65-78e0-4d2e-9654-ccc010f78bf7' alt="DeepChat Light Mode" width="400"/>
      <br/>
    </td>
    <td align="center" style="padding: 10px;">
      <img src='https://github.com/user-attachments/assets/ea6cc65-32af-4bc1-91cc-e72703bdc1ff' alt="DeepChat Dark Mode" width="400"/>
      <br/>
    </td>
  </tr>
</table>

## 💡 为什么选择 DeepChat

与其他 AI 工具相比，DeepChat 具备以下独特优势：

- **统一的模型管理**：一个应用支持几乎所有主流大语言模型，无需在多个应用间切换
- **无缝的本地模型集成**：内置 Ollama 支持，让你无需命令行操作即可管理和使用本地模型
- **智能体协议生态**：内置 MCP 支持实现工具调用（代码执行、网页访问等），Skills 添加可复用的任务专业知识，内置 ACP 支持将外部代理无缝接入 DeepChat 并提供原生工作区体验
- **强大的搜索增强**：支持多种搜索引擎，使 AI 回复更准确及时，提供可快速自定义的非标准网页搜索范式
- **随时随地的远程控制**：通过 Telegram、飞书/Lark、QQBot、Discord 和微信 iLink 控制 DeepChat 会话
- **注重隐私安全**：本地数据存储和网络代理支持降低信息泄露风险
- **商业友好**：基于 Apache License 2.0 开源协议，适用于商业和个人使用

## 🔥 核心功能

- 🌐 **多云端大模型支持**：DeepSeek、OpenAI、Moonshot/Kimi、Grok、Gemini、Anthropic 等
- 🏠 **本地模型部署支持**：
  - 集成 Ollama，具备全面管理能力
  - 无需命令行即可控制和管理 Ollama 模型的下载、部署和运行
- 🚀 **丰富易用的对话功能**
  - 完整支持 Markdown 渲染，基于业界领先的 [CodeMirror](https://codemirror.net/) 实现代码块高亮
  - 多窗口+多标签页架构，全面支持并行多会话操作，像使用浏览器一样使用大模型，非阻塞体验带来卓越效率
  - 支持 Artifacts（工件）渲染以多样化结果展示，结合 MCP 集成可显著节省 Token 消耗
  - 消息支持重试生成多种变体；对话可自由分叉，确保总有合适的思路走向
  - 支持渲染图片、Mermaid 图表等多模态内容；支持 GPT-4o、Gemini、Grok 的文生图能力
  - 支持在内容中高亮搜索结果等外部信息源
- 🔍 **强大的搜索扩展能力**
  - 通过 MCP 模式内置集成 BoSearch、Brave Search 等主流搜索引擎 API，让模型智能决定何时进行搜索
  - 支持通过模拟用户网页浏览的方式接入 Google、Bing、百度和搜狗公众号等主流搜索引擎，使 LLM 能像人类一样阅读搜索结果
  - 支持读取任意搜索引擎；只需配置一个搜索辅助模型即可对接各类信息源（内网、无 API 引擎或垂直领域搜索引擎）
- 🔧 **卓越的 MCP（模型上下文协议）支持**
  - 完整支持 MCP 协议的三大核心能力：Resources、Prompts/Tools
  - 支持语义工作流，通过理解任务含义和上下文实现更复杂智能的自动化
  - 配置界面极其友好
  - 工具调用展示美观清晰
  - 提供详细的工具调试窗口，自动格式化参数与返回数据
  - 内置 Node.js 运行环境；类似 npx/node 的服务无需额外配置即可开箱即用
  - 支持 StreamableHTTP/SSE/Stdio 传输协议
  - 支持 inMemory 服务，内置代码执行、网页信息检索和文件操作等实用工具，满足大多数常见场景需求，二次安装成本极低
  - 通过内置 MCP 服务将视觉模型能力转化为任何模型均可使用的通用函数
- 🧠 **Skills（技能）**
  - 可从文件夹、ZIP 文件或 URL 安装 Skills
  - 按对话启用，使 DeepChat 加载特定任务指令、参考文件和可选脚本
  - 支持与 AI 编程助手导入导出 Skills
  - 内置 Skills 涵盖代码审查、文档协作、Office/PDF 处理、前端设计、MCP 开发等
- 🤝 **ACP（代理客户端协议）集成**
  - 将兼容的 ACP 代理作为可选“模型”运行
  - 提供结构化计划、工具调用和终端输出的专用工作区 UI
- 📡 **远程控制**
  - 通过 Telegram、飞书/Lark、QQBot、Discord 和微信 iLink 控制会话
  - 将远程端点绑定到会话，从聊天应用管理对话
  - 支持在远端创建或切换会话、停止生成、打开桌面会话、处理待交互请求、切换模型及查看状态
- 💻 **跨平台支持**：Windows、macOS、Linux
- 🎨 **美观易用的界面**：以用户为中心的设计，精心打磨的亮色与暗色主题
- 🔗 **丰富的 DeepLink 支持**：通过链接发起对话，实现与其他应用的无缝集成；同时支持一键安装 MCP 服务，简单快捷
- 🚑 **安全优先设计**：聊天数据与配置数据预留加密接口及代码混淆能力
- 🛡️ **隐私保护**：支持屏幕投影隐藏、网络代理等隐私保护措施，降低信息泄露风险
- 💰 **商业友好**：
  - 基于 Apache License 2.0 开源协议，企业使用无忧
  - 企业集成仅需少量配置代码即可调用预留的加密混淆安全能力
  - 代码结构清晰，模型提供商与 MCP 服务高度解耦，可低成本自由定制
  - 架构合理，数据交互与 UI 行为分离，充分利用 Electron 性能优势，拒绝简单网页套壳，运行流畅

更多功能使用指南，请参阅 [文档索引](./docs/README.md)。

## 🧠 Skills（技能）支持

DeepChat 的 Skills 旨在兼容标准的 Agent Skills 规范。一个 Skill 可包含任务指令、参考文件、资源及可选脚本，启用后 DeepChat 将更像一个领域专家。

你可通过文件夹、ZIP 文件或 URL 安装 Skills，并支持与 Claude Code、Codex、Cursor、Windsurf、GitHub Copilot、Kiro、Antigravity、OpenCode、Goose、Kilo Code 等兼容工具进行导入/导出。内置 Skills 涵盖生成式艺术、代码审查、DeepChat 设置、文档协作、DOCX、前端设计、Git 提交信息、信息图语法、MCP 构建、PDF、PPTX、Skill 创建、Web Artifacts 及 XLSX 工作流等。

快速开始：
1. 打开 **Settings → Skills**
2. 安装或导入一个 Skill
3. 在需要该能力的对话中启用它

## 🧩 ACP（代理客户端协议）集成

DeepChat 内置支持 [Agent Client Protocol (ACP)](https://agentclientprotocol.com)，允许你将外部代理运行时以原生 UI 形式集成到 DeepChat。启用后，ACP 代理将作为一等公民出现在模型选择器中，以便你直接在 DeepChat 内使用代码代理和任务代理。

快速开始：
1. 打开 **Settings → ACP Agents** 并启用 ACP
2. 启用内置的 ACP 代理或添加自定义兼容命令
3. 在模型选择器中选择该 ACP 代理以启动会话

探索兼容代理与客户端生态，请访问：https://agentclientprotocol.com/overview/clients

## 📡 远程控制

你可以通过聊天应用控制 DeepChat，即使离开电脑也能保持会话运行。在 **Settings → Remote** 中配置远程频道。

支持的频道包括 Telegram、飞书/Lark、QQBot、Discord 和微信 iLink。远程端点可绑定至单个 DeepChat 会话，随后支持创建新会话、列出并切换最近会话、停止生成、在桌面打开当前会话、回答待处理问题或权限请求、切换模型及查看运行状态。

常用命令包括 `/start`、`/help`、`/pair`、`/new`、`/sessions`、`/use`、`/stop`、`/open`、`/pending`、`/model` 和 `/status`。

## 🤖 支持的模型提供商

<table>
  <tr align="center">
    <td>
      <img src="./src/renderer/src/assets/llm-icons/deepseek-color.svg" width="50" height="50" alt="Deepseek Icon"><br/>
      <a href="https://deepseek.com/">Deepseek</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/moonshot.svg" width="50" height="50" alt="Moonshot Icon"><br/>
      <a href="https://moonshot.ai/">Moonshot</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/openai.svg" width="50" height="50" alt="OpenAI Icon"><br/>
      <a href="https://openai.com/">OpenAI</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/gemini-color.svg" width="50" height="50" alt="Gemini Icon"><br/>
      <a href="https://gemini.google.com/">Gemini</a>
    </td>
  </tr>
  <tr align="center">
    <td>
      <img src="./src/renderer/src/assets/llm-icons/ollama.svg" width="50" height="50" alt="Ollama Icon"><br/>
      <a href="https://ollama.com/">Ollama</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/qiniu.svg" width="50" height="50" alt="Qiniu Icon"><br/>
      <a href="https://www.qiniu.com">Qiniu</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/newapi.svg" width="50" height="50" alt="New API Icon"><br/>
      <a href="https://www.newapi.ai/">New API</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/grok.svg" width="50" height="50" alt="Grok Icon"><br/>
      <a href="https://x.ai/">Grok</a>
    </td>
  </tr>
  <tr align="center">
    <td>
      <img src="./src/renderer/src/assets/llm-icons/zhipu-color.svg" width="50" height="50" alt="Zhipu Icon"><br/>
      <a href="https://open.bigmodel.cn/">Zhipu</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/ppio-color.svg" width="50" height="50" alt="PPIO Icon"><br/>
      <a href="https://ppinfra.com/">PPIO</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/minimax-color.svg" width="50" height="50" alt="MiniMax Icon"><br/>
      <a href="https://platform.minimaxi.com/">MiniMax</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/fireworks-color.svg" width="50" height="50" alt="Fireworks Icon"><br/>
      <a href="https://fireworks.ai/">Fireworks</a>
    </td>
  </tr>
  <tr align="center">
    <td>
      <img src="./src/renderer/src/assets/llm-icons/aihubmix.png" width="50" height="50" alt="AIHubMix Icon"><br/>
      <a href="https://aihubmix.com/">AIHubMix</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/doubao-color.svg" width="50" height="50" alt="Doubao Icon"><br/>
      <a href="https://console.volcengine.com/ark/">Doubao</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/alibabacloud-color.svg" width="50" height="50" alt="DashScope Icon"><br/>
      <a href="https://www.aliyun.com/product/bailian">DashScope</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/groq.svg" width="50" height="50" alt="Groq Icon"><br/>
      <a href="https://groq.com/">Groq</a>
    </td>
  </tr>
  <tr align="center">
    <td>
      <img src="./src/renderer/src/assets/llm-icons/jiekou-color.svg" width="50" height="50" alt="JieKou.AI Icon"><br/>
      <a href="https://jiekou.ai?utm_source=github_deepchat">JieKou.AI</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/zenmux-color.svg" width="50" height="50" alt="ZenMux Icon"><br/>
      <a href="https://zenmux.ai/">ZenMux</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/github.svg" width="50" height="50" alt="GitHub Models Icon"><br/>
      <a href="https://github.com/marketplace/models">GitHub Models</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/lmstudio.svg" width="50" height="50" alt="LM Studio Icon"><br/>
      <a href="https://lmstudio.ai/docs/app">LM Studio</a>
    </td>
  </tr>
  <tr align="center">
    <td>
      <img src="./src/renderer/src/assets/llm-icons/hunyuan-color.svg" width="50" height="50" alt="Hunyuan Icon"><br/>
      <a href="https://cloud.tencent.com/product/hunyuan">Hunyuan</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/302ai.svg" width="50" height="50" alt="302.AI Icon"><br/>
      <a href="https://302.ai">302.AI</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/together-color.svg" width="50" height="50" alt="Together Icon"><br/>
      <a href="https://www.together.ai/">Together</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/poe-color.svg" width="50" height="50" alt="Poe Icon"><br/>
      <a href="https://poe.com/">Poe</a>
    </td>
  </tr>
  <tr align="center">
    <td>
      <img src="./src/renderer/src/assets/llm-icons/vercel.svg" width="50" height="50" alt="Vercel AI Gateway Icon"><br/>
      <a href="https://vercel.com/ai">Vercel AI Gateway</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/openrouter.svg" width="50" height="50" alt="OpenRouter Icon"><br/>
      <a href="https://openrouter.ai/">OpenRouter</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/azure-color.svg" width="50" height="50" alt="Azure OpenAI Icon"><br/>
      <a href="https://azure.microsoft.com/en-us/products/ai-services/openai-service">Azure OpenAI</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/tokenflux-color.svg" width="50" height="50" alt="TokenFlux Icon"><br/>
      <a href="https://tokenflux.ai/">TokenFlux</a>
    </td>
  </tr>
  <tr align="center">
    <td>
      <img src="./src/renderer/src/assets/llm-icons/burncloud-color.svg" width="50" height="50" alt="BurnCloud Icon"><br/>
      <a href="https://www.burncloud.com/">BurnCloud</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/openai.svg" width="50" height="50" alt="OpenAI Responses Icon"><br/>
      <a href="https://openai.com/">OpenAI Responses</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/cherryin-color.png" width="50" height="50" alt="CherryIn Icon"><br/>
      <a href="https://open.cherryin.ai/console">CherryIn</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/modelscope-color.svg" width="50" height="50" alt="ModelScope Icon"><br/>
      <a href="https://modelscope.cn/">ModelScope</a>
    </td>
  </tr>
  <tr align="center">
    <td>
      <img src="./src/renderer/src/assets/llm-icons/aws-bedrock.svg" width="50" height="50" alt="AWS Bedrock Icon"><br/>
      <a href="https://aws.amazon.com/bedrock/">AWS Bedrock</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/voiceai.svg" width="50" height="50" alt="Voice.ai Icon"><br/>
      <a href="https://voice.ai/">Voice.ai</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/vertexai-color.svg" width="50" height="50" alt="Vertex AI Icon"><br/>
      <a href="https://cloud.google.com/vertex-ai">Vertex AI</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/githubcopilot.svg" width="50" height="50" alt="GitHub Copilot Icon"><br/>
      <a href="https://github.com/features/copilot">GitHub Copilot</a>
    </td>
  </tr>
  <tr align="center">
    <td>
      <img src="./src/renderer/src/assets/llm-icons/xiaomi.png" width="50" height="50" alt="Xiaomi Icon"><br/>
      <a href="https://platform.xiaomimimo.com/#/docs/quick-start/first-api-call">Xiaomi</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/o3-fan.png" width="50" height="50" alt="o3.fan Icon"><br/>
      <a href="https://o3.fan">o3.fan</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/novitaai.svg" width="50" height="50" alt="Novita AI Icon"><br/>
      <a href="https://novita.ai/">Novita AI</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/astraflow.png" width="50" height="50" alt="Astraflow Icon"><br/>
      <a href="https://astraflow.ucloud.cn/">Astraflow</a>
    </td>
  </tr>
  <tr align="center">
    <td>
      <img src="./src/renderer/src/assets/llm-icons/anthropic.svg" width="50" height="50" alt="Anthropic Icon"><br/>
      <a href="https://www.anthropic.com/">Anthropic</a>
    </td>
    <td>
      <img src="./src/renderer/src/assets/llm-icons/siliconcloud-color.svg" width="50" height="50" alt="SiliconFlow Icon"><br/>
      <a href="https://www.siliconflow.cn/">SiliconFlow</a>
    </td>
  </tr>

</table>

### 兼容任何采用 OpenAI/Gemini/Anthropic API 格式的模型提供商

## 🔍 应用场景

DeepChat 适用于多种 AI 应用场景：

- **日常助手**：问答、建议、写作辅助
- **开发辅助**：代码生成、调试、技术问题解决
- **学习工具**：概念解释、知识探索、学习指导
- **内容创作**：文案撰写、创意灵感、内容优化
- **数据分析**：数据解读、图表生成、报告编写

## 📦 快速开始

### 下载与安装

你可通过以下任一方式安装 DeepChat：

**选项 1：GitHub Releases**

从 [GitHub Releases](https://github.com/ThinkInAIXYZ/deepchat/releases) 页面下载对应系统的最新版本：

- Windows：`.exe` 安装包
- macOS：`.dmg` 安装包
- Linux：`.AppImage` 或 `.deb` 安装包

**选项 2：官方网站**

从 [官网](https://deepchatai.cn/#/download) 下载。

**选项 3：Homebrew（仅限 macOS）**

macOS 用户可通过 Homebrew 安装 DeepChat：

```bash
brew install --cask deepchat
```

### 配置模型

1. 启动 DeepChat 应用
2. 点击设置图标
3. 选择“Model Providers”选项卡
4. 添加你的 API Keys 或配置本地 Ollama

### 开始对话

1. 点击“+”按钮创建新对话
2. 选择你要使用的模型
3. 开始与 AI 助手交流

获取全面的入门指南及所有功能使用说明，请参阅 [文档索引](./docs/README.md)。

## 💻 开发指南

请阅读 [贡献指南](./CONTRIBUTING.md)

Windows 和 Linux 由 GitHub Action 打包。Mac 相关的签名与打包请参考 [Mac Release Guide](https://github.com/ThinkInAIXYZ/deepchat/wiki/Mac-Release-Guide)。

### 安装依赖

```bash
$ pnpm install
$ pnpm run installRuntime
# if got err: No module named 'distutils'
$ pip install setuptools
```

* Windows：为使非管理员用户能够创建符号链接和硬链接，请在设置中启用 `Developer Mode` 或使用管理员账户。否则 `pnpm` 操作将失败。

### 启动开发

```bash
$ pnpm run dev
```

### 构建项目

```bash
# For Windows
$ pnpm run build:win

# For macOS
$ pnpm run build:mac

# For Linux
$ pnpm run build:linux

# Specify architecture packaging
$ pnpm run build:win:x64
$ pnpm run build:win:arm64
$ pnpm run build:mac:x64
$ pnpm run build:mac:arm64
$ pnpm run build:linux:x64
$ pnpm run build:linux:arm64
```

如需更详细的开发指南、项目结构及架构说明，请参阅 [开发者指南](./docs/developer-guide.md)。

## 👥 社区与贡献

DeepChat 是一个活跃的开源社区项目，欢迎任何形式的贡献：

- 🐛 [报告问题](https://github.com/ThinkInAIXYZ/deepchat/issues)
- 💡 [提交功能建议](https://github.com/ThinkInAIXYZ/deepchat/issues)
- 🔧 [提交代码改进](https://github.com/ThinkInAIXYZ/deepchat/pulls)
- 📚 [完善文档](https://github.com/ThinkInAIXYZ/deepchat/wiki)
- 🌍 [协助翻译](https://github.com/ThinkInAIXYZ/deepchat/tree/main/locales)

查看 [贡献指南](./CONTRIBUTING.md) 了解更多参与方式。

## ⭐ Star 历史

[![Star History Chart](https://api.star-history.com/svg?repos=ThinkInAIXYZ/deepchat&type=Timeline)](https://www.star-history.com/#ThinkInAIXYZ/deepchat&Timeline)

## 👨‍💻 贡献者

感谢所有考虑为 deepchat 做出贡献的开发者！贡献指南可在 [贡献指南](./CONTRIBUTING.md) 中查看。

<a href="https://openomy.com/thinkinaixyz/deepchat" target="_blank" style="display: block; width: 100%;" align="center">
  <img src="https://openomy.com/svg?repo=thinkinaixyz/deepchat&chart=bubble&latestMonth=3" target="_blank" alt="Contribution Leaderboard" style="display: block; width: 100%;" />
</a>

## 🙏🏻 鸣谢

本项目得益于以下优秀库和项目的支持：

- [Vue](https://vuejs.org/)
- [Electron](https://www.electronjs.org/)
- [Electron-Vite](https://electron-vite.org/)
- [oxlint](https://github.com/oxc-project/oxc)
- [Bub](https://github.com/bubbuild/bub)，其 tape 模型启发了 DeepChat 的会话时间轴设计。如需了解底层 tape 架构，请访问 [tape.systems](https://tape.systems/)。

## 📃 许可证

[LICENSE](./LICENSE)
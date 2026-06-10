# 🚀 Agent Starter Pack

![Version](https://img.shields.io/pypi/v/agent-starter-pack?color=blue) [![1-Minute Video Overview](https://img.shields.io/badge/1--Minute%20Overview-gray)](https://youtu.be/jHt-ZVD660g) [![Docs](https://img.shields.io/badge/Documentation-gray)](https://googlecloudplatform.github.io/agent-starter-pack/) <a href="https://studio.firebase.google.com/new?template=https%3A%2F%2Fgithub.com%2FGoogleCloudPlatform%2Fagent-starter-pack%2Ftree%2Fmain%2Fagent_starter_pack%2Fresources%2Fidx">
  <picture>
    <source
      media="(prefers-color-scheme: dark)"
      srcset="https://cdn.firebasestudio.dev/btn/try_light_20.svg">
    <source
      media="(prefers-color-scheme: light)"
      srcset="https://cdn.firebasestudio.dev/btn/try_dark_20.svg">
    <img
      height="20"
      alt="Try in Firebase Studio"
      src="https://cdn.firebasestudio.dev/btn/try_blue_20.svg">
  </picture>
</a> [![Launch in Cloud Shell](https://img.shields.io/badge/Launch-in_Cloud_Shell-white)](https://shell.cloud.google.com/cloudshell/editor?cloudshell_git_repo=https%3A%2F%2Fgithub.com%2Feliasecchig%2Fasp-open-in-cloud-shell&cloudshell_print=open-in-cs) ![Stars](https://img.shields.io/github/stars/GoogleCloudPlatform/agent-starter-pack?color=yellow)

> ## ⚠️ Agent Starter Pack 已进入维护模式 — 请切换至 `agents-cli`
>
> **活跃开发已移至 [`agents-cli`](https://github.com/google/agents-cli)**，这是 Agent Starter Pack 的下一代演进版本。ASP（Agent Starter Pack）将仅接收关键修复——**不再新增功能、模板或部署目标**。新项目应使用 `agents-cli`；现有项目请进行迁移。
>
> ```bash
> uvx google-agents-cli setup
> ```
>
> **迁移仅需几分钟** —— 你的 Agent 代码、测试用例、Terraform 配置以及 CI/CD 流水线均可无缝继承，无需重写。
>
> **你将获得：**
> - 🛠️ **统一的 CLI** 替代 Makefile —— `run`、`deploy`、`eval run`、`eval compare`、`playground`、`lint` 等
> - 🧠 **内置编码 Agent 技能**，将 Claude Code、Gemini CLI 或 Codex 转变为 ADK 专家
> - 🔁 **端到端生命周期工具链**：脚手架生成 → 评估 → 部署 → 发布 → 可观测性监控
> - ☁️ **原生支持** Google Cloud Agent Platform
>
> **→ [迁移指南](https://google.github.io/agents-cli/reference/from-agent-starter-pack/) &nbsp;•&nbsp; [快速上手](https://google.github.io/agents-cli/) &nbsp;•&nbsp; [文档](https://google.github.io/agents-cli/) &nbsp;•&nbsp; [GitHub](https://github.com/google/agents-cli) &nbsp;•&nbsp; [PyPI](https://pypi.org/project/google-agents-cli/)**

---

一个提供面向 Google Cloud 的 GenAI（生成式人工智能）Agent **生产就绪模板** 的 Python 包。

专注于你的 Agent 逻辑——该 Starter Pack 负责其余一切：基础设施、CI/CD、可观测性与安全性。

| ⚡️ 快速启动 | 🧪 实验测试 | ✅ 部署上线 | 🛠️ 自定义扩展 |
|---|---|---|---|
| [预构建的 Agent 模板](./agent_starter_pack/agents/)（ReAct、RAG、多 Agent、Live API）。 | [Vertex AI 评估](https://cloud.google.com/vertex-ai/generative-ai/docs/models/evaluation-overview)及交互式 Playground。 | 生产就绪的基础设施，配备[监控与可观测性](https://googlecloudplatform.github.io/agent-starter-pack/guide/observability)，以及部署到 [Cloud Run](https://cloud.google.com/run) 或 [Agent Engine](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview) 的 [CI/CD](https://googlecloudplatform.github.io/agent-starter-pack/guide/deployment)。 | 根据你的需求扩展和自定义模板。🆕 现已集成 [Gemini CLI](https://github.com/google-gemini/gemini-cli) |

---

## ⚡️ 1分钟快速上手

**使用 [`uv`](https://docs.astral.sh/uv/getting-started/installation/)，60秒内从零构建生产就绪的 Agent：**

```bash
uvx agent-starter-pack create
```

<details>
<summary> ✨ 替代方案：使用 pip</summary>

如果你尚未安装 [`uv`](https://github.com/astral-sh/uv)，可以使用 pip：
```bash
# 创建并激活 Python 虚拟环境
python -m venv .venv && source .venv/bin/activate

# 安装 Agent Starter Pack
pip install --upgrade agent-starter-pack

# 创建新的 Agent 项目
agent-starter-pack create
```
</details>

**就是这样！** 你现在拥有了一个功能完整的 Agent 项目——包含后端、前端和部署基础设施，随时可供你探索与自定义。

### 🔧 增强现有 Agent

已经有一个 Agent？只需在项目的根目录运行以下命令，即可为其添加生产就绪的部署配置与基础设施：

```bash
uvx agent-starter-pack enhance
```

详见 [安装指南](https://googlecloudplatform.github.io/agent-starter-pack/guide/installation) 获取更多选项，或在 [Firebase Studio](https://studio.firebase.google.com/new?template=https%3A%2F%2Fgithub.com%2FGoogleCloudPlatform%2Fagent-starter-pack%2Ftree%2Fmain%2Fsrc%2Fresources%2Fidx) / [Cloud Shell](https://shell.cloud.google.com/cloudshell/editor?cloudshell_git_repo=https%3A%2F%2Fgithub.com%2Feliasecchig%2Fasp-open-in-cloud-shell&cloudshell_print=open-in-cs) 中体验零配置启动。

---

## 🤖 Agent 模板

| Agent 名称                  | 描述                                                                                                                       |
|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| `adk`      | 基于 Google [Agent Development Kit (ADK)](https://github.com/google/adk-python) 实现的基线 ReAct Agent |
| `adk_a2a`  | 支持 [Agent2Agent (A2A) 协议](https://a2a-protocol.org/) 的 ADK Agent，用于分布式通信与互操作 |
| `agentic_rag` | 面向文档检索与问答的 RAG（检索增强生成）Agent。支持 [Vertex AI Search](https://cloud.google.com/generative-ai-app-builder/docs/enterprise-search-introduction) 和 [Vector Search](https://cloud.google.com/vertex-ai/docs/vector-search/overview)。       |
| `langgraph`      | 基于 LangChain [LangGraph](https://github.com/langchain-ai/langgraph) 实现的基线 ReAct Agent |
| `adk_java`   | 基于 Google [Java版 ADK](https://github.com/google/adk-java) 实现的基线 ReAct Agent |
| `adk_live`       | 由 Gemini 驱动的实时多模态 RAG Agent，支持音频/视频/文本对话     |

**更多 Agent 正在开发中！** 我们正不断扩充我们的 [Agent 库](https://googlecloudplatform.github.io/agent-starter-pack/agents/overview)。有特定的 Agent 类型需求？[提交功能请求 Issue！](https://github.com/GoogleCloudPlatform/agent-starter-pack/issues/new?labels=enhancement)

**🔍 ADK 示例**

想探索更多 ADK 示例？请查看 [ADK Samples 仓库](https://github.com/google/adk-samples)，获取更多展示 ADK 能力的用例与代码。

---

## 🌟 社区精选

探索由 Agent Starter Pack 构建的精彩项目！ 

**[查看社区精选 →](https://googlecloudplatform.github.io/agent-starter-pack/guide/community-showcase)**

## 核心功能

`agent-starter-pack` 提供以下核心功能，助你加速并简化 Agent 开发：
- **🔄 [CI/CD 自动化](https://googlecloudplatform.github.io/agent-starter-pack/cli/setup_cicd)** - 一条命令即可为所有环境搭建完整的 CI/CD（持续集成与持续交付）流水线，同时支持 **Google Cloud Build** 和 **GitHub Actions**。
- **📥 [基于 Terraform/CI-CD 的 RAG 数据管道](https://googlecloudplatform.github.io/agent-starter-pack/guide/data-ingestion)** - 无缝集成数据处理管道以生成嵌入向量（embeddings），并将其接入你的 Agent 系统。支持 [Vertex AI Search](https://cloud.google.com/generative-ai-app-builder/docs/enterprise-search-introduction) 和 [Vector Search](https://cloud.google.com/vertex-ai/docs/vector-search/overview)。
- **[远程模板](https://googlecloudplatform.github.io/agent-starter-pack/remote-templates/)**：从任意 Git 仓库创建并分享你自己的 Agent Starter Pack 模板。
- **🤖 Gemini CLI 集成** - 使用 [Gemini CLI](https://github.com/google-gemini/gemini-cli) 及内置的 `GEMINI.md` 上下文文件，随时询问关于你的模板、Agent 架构及生产路径的问题。直接在终端获取即时指导与代码示例。

## 整体架构

该 Starter Pack 涵盖 Agent 开发的各个环节，从原型设计与评估到部署与监控。

![High Level Architecture](docs/images/asp_high_level_architecture.png "Architecture")

---

## 🔧 环境要求

- Python 3.10+
- [Google Cloud SDK](https://cloud.google.com/sdk/docs/install)
- [Terraform](https://developer.hashicorp.com/terraform/downloads)（用于部署）
- [Make](https://www.gnu.org/software/make/)（用于开发任务）


## 📚 文档

访问我们的[文档站点](https://googlecloudplatform.github.io/agent-starter-pack/)获取全面指南与参考！

🔍 **不熟悉代码库？** 探索 [CodeWiki](https://codewiki.google/github.com/googlecloudplatform/agent-starter-pack) 以获得 AI 驱动的代码理解与导航体验。

- [快速上手指南](https://googlecloudplatform.github.io/agent-starter-pack/guide/getting-started) - agent-starter-pack 入门步骤
- [安装指南](https://googlecloudplatform.github.io/agent-starter-pack/guide/installation) - 环境配置说明
- [部署指南](https://googlecloudplatform.github.io/agent-starter-pack/guide/deployment) - 将你的 Agent 投入生产环境
- [Agent 模板概览](https://googlecloudplatform.github.io/agent-starter-pack/agents/overview) - 探索可用的 Agent 架构模式
- [CLI 参考文档](https://googlecloudplatform.github.io/agent-starter-pack/cli/) - 命令行工具使用说明


### 🎬 视频导览：

- **[从演示到生产：使用 Agent Starter Pack](https://www.youtube.com/watch?v=mtJMYgJkTt8)**：了解 Agent Starter Pack 如何充当“自动化架构师”，在数秒内为你的 AI 项目构建专业基础设施。涵盖为何大多数 AI 项目在部署阶段失败，以及 ASP 如何通过自动化 Terraform、CI/CD 和可观测性来解决问题。

- **[6分钟快速入门](https://www.youtube.com/live/eZ-8UQ_t4YM?feature=shared&t=2791)**（2025年4月）：介绍 Agent Starter Pack 及其核心功能演示。作为 Kaggle GenAI 强化课程的一部分。

需要更多 Google Cloud 生成式 AI 的示例与资源？请查看 [GoogleCloudPlatform/generative-ai](https://github.com/GoogleCloudPlatform/generative-ai) 仓库，内含大量 Notebook、代码片段及其他资料！

## 贡献指南

欢迎贡献！详见 [贡献指南](CONTRIBUTING.md)。

## 反馈与建议

我们非常重视你的意见！你的反馈将帮助我们改进此 Starter Pack，使其更好地服务于社区。

### 获取帮助

如果遇到任何问题或有具体建议，请首先在我们的 GitHub 仓库提交 [Issue](https://github.com/GoogleCloudPlatform/generative-ai/issues)。

### 分享你的体验

对于其他类型的反馈，或如果你想分享使用本 Starter Pack 的成功经验与正面评价，我们非常期待听到你的声音！你可以通过 <a href="mailto:agent-starter-pack@google.com">agent-starter-pack@google.com</a> 联系我们。

感谢你的贡献！

## 免责声明

本仓库仅用于演示目的，并非 Google 官方支持的产品。

## 服务条款

`agent-starter-pack` 的模板化 CLI 及本 Starter Pack 中的模板调用了 Google Cloud API。使用本 Starter Pack 时，你将在自己的 Google Cloud 项目中部署资源，并需对这些资源负责。请查阅 [Google Cloud 服务条款](https://cloud.google.com/terms/service-terms) 了解相关 API 的服务协议详情。
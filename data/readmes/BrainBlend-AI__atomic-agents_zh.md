# Atomic Agents

<img src="./.assets/logo.png" alt="Atomic Agents" width="350"/>

[![PyPI version](https://badge.fury.io/py/atomic-agents.svg)](https://badge.fury.io/py/atomic-agents)
[![Documentation](https://img.shields.io/badge/docs-read%20the%20docs-blue?logo=readthedocs&style=flat-square)](https://brainblend-ai.github.io/atomic-agents/)
[![Build Docs](https://github.com/BrainBlend-AI/atomic-agents/actions/workflows/docs.yml/badge.svg)](https://github.com/BrainBlend-AI/atomic-agents/actions/workflows/docs.yml)
[![Code Quality](https://github.com/BrainBlend-AI/atomic-agents/actions/workflows/code-quality.yml/badge.svg)](https://github.com/BrainBlend-AI/atomic-agents/actions/workflows/code-quality.yml)
[![Discord](https://img.shields.io/badge/chat-on%20discord-7289DA?logo=discord&style=flat-square)](https://discord.gg/J3W9b5AZJR)
[![PyPI downloads](https://img.shields.io/pypi/dm/atomic-agents?style=flat-square)](https://pypi.org/project/atomic-agents/)
[![Python Versions](https://img.shields.io/pypi/pyversions/atomic-agents?style=flat-square)](https://pypi.org/project/atomic-agents/)
[![License: MIT](https://img.shields.io/badge/license-MIT-yellow?style=flat-square)](LICENSE)
[![GitHub Stars](https://img.shields.io/github/stars/BrainBlend-AI/atomic-agents?style=social)](https://github.com/BrainBlend-AI/atomic-agents/stargazers)
[![GitHub Forks](https://img.shields.io/github/forks/BrainBlend-AI/atomic-agents?style=social)](https://github.com/BrainBlend-AI/atomic-agents/network/members)
[![Ask DeepWiki](https://deepwiki.com/badge.svg)](https://deepwiki.com/BrainBlend-AI/atomic-agents)

## 什么是 Atomic Agents？

Atomic Agents 框架围绕“原子性”（atomicity）概念设计，是一个极其轻量且高度模块化的框架，用于构建 Agentic AI 工作流与应用，同时不牺牲开发者体验与代码可维护性。

你可以将其视为用乐高积木搭建 AI 应用——每个组件（智能体、工具、上下文提供者）都具备以下特点：
- **单一职责**：专注完成单项任务且性能优异
- **可复用**：可在多个工作流中重复使用
- **易组合**：能够与其他组件轻松拼接
- **行为可预测**：输出稳定可靠

该框架基于 [Instructor](https://github.com/jxnl/instructor) 和 [Pydantic](https://docs.pydantic.dev/latest/) 构建，让你能够运用熟悉的软件工程原则来创建 AI 应用。

**新增：欢迎加入我们的 Discord 社区 [discord.gg/J3W9b5AZJR](https://discord.gg/J3W9b5AZJR) 以及官方 subreddit [/r/AtomicAgents](https://www.reddit.com/r/AtomicAgents/)！**

## 目录

- [Atomic Agents](#atomic-agents)
  - [什么是 Atomic Agents？](#what-is-atomic-agents)
  - [目录](#table-of-contents)
  - [快速入门](#getting-started)
    - [安装](#installation)
    - [快速示例](#quick-example)
  - [为什么选择 Atomic Agents？](#why-atomic-agents)
  - [核心概念](#core-concepts)
    - [智能体（Agent）的构成](#anatomy-of-an-agent)
    - [上下文提供者（Context Providers）](#context-providers)
    - [模式与智能体的链式调用](#chaining-schemas-and-agents)
  - [示例与文档](#examples--documentation)
    - [快速入门示例](#quickstart-examples)
    - [完整示例](#complete-examples)
  - [🚀 v2.0 版本已发布！](#-version-20-released)
    - [v2.0 主要变更：](#key-changes-in-v20)
    - [⚠️ 从 v1.x 升级指南](#️-upgrading-from-v1x)
  - [Atomic Forge 与 CLI](#atomic-forge--cli)
    - [运行 CLI](#running-the-cli)
  - [项目结构](#project-structure)
  - [Provider 与模型兼容性](#provider--model-compatibility)
  - [贡献指南](#contributing)
  - [许可证](#license)
  - [其他资源](#additional-resources)
  - [星标历史](#star-history)

## 快速入门

### 安装
要安装 Atomic Agents，可使用 pip：

```bash
pip install atomic-agents
```

请确保同时安装你打算使用的 Provider（模型服务提供方）。Provider SDK 作为 instructor 的可选依赖提供：

```bash
pip install instructor[groq]        # 用于 Groq
pip install instructor[anthropic]   # 用于 Anthropic
pip install instructor[google-genai] # 用于 Gemini
```

OpenAI 默认已包含在内。完整支持的 Provider 列表请参阅 [Instructor 文档](https://python.useinstructor.com/integrations/)。

此命令还会安装 CLI 工具 *Atomic Assembler*，可用于下载 Tools（未来也将支持 Agents 和 Pipelines）。

### 快速示例

以下代码片段展示了使用 Atomic Agents 创建强大智能体的便捷性：

```python
from pydantic import Field
from openai import OpenAI
import instructor
from atomic_agents import AtomicAgent, AgentConfig, BasicChatInputSchema, BaseIOSchema
from atomic_agents.context import SystemPromptGenerator, ChatHistory

# Define a custom output schema
class CustomOutputSchema(BaseIOSchema):
    """
    docstring for the custom output schema
    """
    chat_message: str = Field(..., description="The chat message from the agent.")
    suggested_questions: list[str] = Field(..., description="Suggested follow-up questions.")

# Set up the system prompt
system_prompt_generator = SystemPromptGenerator(
    background=["This assistant is knowledgeable, helpful, and suggests follow-up questions."],
    steps=[
        "Analyze the user's input to understand the context and intent.",
        "Formulate a relevant and informative response.",
        "Generate 3 suggested follow-up questions for the user."
    ],
    output_instructions=[
        "Provide clear and concise information in response to user queries.",
        "Conclude each response with 3 relevant suggested questions for the user."
    ]
)

# Initialize OpenAI client
client = instructor.from_openai(OpenAI())

# Initialize the agent
agent = AtomicAgent[BasicChatInputSchema, CustomOutputSchema](
    config=AgentConfig(
        client=client,
        model="gpt-5-mini",
        system_prompt_generator=system_prompt_generator,
        history=ChatHistory(),
    )
)

# Example usage
if __name__ == "__main__":
    user_input = "Tell me about atomic agents framework"
    response = agent.run(BasicChatInputSchema(chat_message=user_input))
    print(f"Agent: {response.chat_message}")
    print("Suggested questions:")
    for question in response.suggested_questions:
        print(f"- {question}")
```

## 为什么选择 Atomic Agents？
现有的 Agentic AI 框架通常专注于构建自主的多智能体系统，但往往缺乏实际应用场景所需的控制力与可预测性。企业需要能够产出一致、可靠输出，且符合品牌调性与业务目标的 AI 系统。

Atomic Agents 通过以下方式满足这一需求：

- **模块化**：通过组合小型、可复用的组件来构建 AI 应用。
- **行为可预测**：定义清晰的输入与输出模式（Schema），确保运行结果一致可靠。
- **易于扩展**：轻松替换或集成新组件，且不会破坏现有系统结构。
- **完全可控**：可对系统的每个部分进行独立微调，从系统提示词到工具集成均可精准掌控。

所有逻辑与控制流均使用 Python 编写，使开发者能够沿用传统软件开发中的最佳实践与工作流，同时不牺牲灵活性与代码清晰度。

## 核心概念

### 智能体（Agent）的构成
在 Atomic Agents 中，一个智能体由以下几个关键组件构成：

- **系统提示词**（System Prompt）：定义智能体的行为与目标。
- **输入模式**（Input Schema）：指定智能体输入的格式与校验规则。
- **输出模式**（Output Schema）：指定智能体输出的格式与校验规则。
- **历史记录**（History）：存储对话历史或其他相关数据。
- **上下文提供者**（Context Providers）：在运行时向系统提示词中注入动态上下文信息。

以下是高层架构图示：
<!-- ![alt text](./.assets/architecture_highlevel_overview.png) -->
<img src="./.assets/architecture_highlevel_overview.png" alt="High-level architecture overview of Atomic Agents" width="600"/>
<img src="./.assets/what_is_sent_in_prompt.png" alt="Diagram showing what is sent to the LLM in the prompt" width="600"/>

### 上下文提供者（Context Providers）

Atomic Agents 允许你通过**上下文提供者**（Context Providers）为智能体注入动态上下文。上下文提供者使你能在运行时向系统提示词中附加额外信息，从而提升智能体的灵活性与情境感知能力。

要使用上下文提供者，请创建一个继承自 `BaseDynamicContextProvider` 的类，并实现返回待添加上下文字符串的 `get_info()` 方法。

以下是一个简单示例：

```python
from atomic_agents.context import BaseDynamicContextProvider

class SearchResultsProvider(BaseDynamicContextProvider):
    def __init__(self, title: str, search_results: List[str]):
        super().__init__(title=title)
        self.search_results = search_results

    def get_info(self) -> str:
        return "\n".join(self.search_results)
```

随后可将你的上下文提供者注册到智能体中：

```python
# Initialize your context provider with dynamic data
search_results_provider = SearchResultsProvider(
    title="Search Results",
    search_results=["Result 1", "Result 2", "Result 3"]
)

# Register the context provider with the agent
agent.register_context_provider("search_results", search_results_provider)
```

这使得智能体能够在系统提示词中包含搜索结果（或其他任何上下文），从而基于最新信息优化其回复。

### 模式与智能体的链式调用

Atomic Agents 通过对齐输入与输出模式，使智能体与工具之间的链式调用变得异常简单。该设计让你能够无缝替换组件，从而在 AI 应用中实现模块化与可复用性。

假设你有一个负责生成搜索查询的智能体，并希望将这些查询用于不同的搜索工具中。通过将智能体的输出模式与搜索工具的输入模式对齐，你可以轻松地将它们串联起来或切换不同的搜索服务。

实现方式如下：

```python
import instructor
import openai
from pydantic import Field
from atomic_agents import BaseIOSchema, AtomicAgent, AgentConfig
from atomic_agents.context import SystemPromptGenerator

# Import the search tool you want to use
from web_search_agent.tools.searxng_search import SearXNGSearchTool

# Define the input schema for the query agent
class QueryAgentInputSchema(BaseIOSchema):
    """Input schema for the QueryAgent."""
    instruction: str = Field(..., description="Instruction to generate search queries for.")
    num_queries: int = Field(..., description="Number of queries to generate.")

# Initialize the query agent
query_agent = AtomicAgent[QueryAgentInputSchema, SearXNGSearchTool.input_schema](
    config=AgentConfig(
        client=instructor.from_openai(openai.OpenAI()),
        model="gpt-5-mini",
        system_prompt_generator=SystemPromptGenerator(
            background=[
                "You are an intelligent query generation expert.",
                "Your task is to generate a specified number of diverse and highly relevant queries based on a given instruction."
            ],
            steps=[
                "Receive the instruction and the number of queries to generate.",
                "Generate the queries in JSON format."
            ],
            output_instructions=[
                "Ensure each query is unique and relevant.",
                "Provide the queries in the expected schema."
            ],
        ),
    )
)
```

在该示例中：

- **模块化**：通过将 `query_agent` 的 `output_schema` 设置为与 `SearXNGSearchTool.input_schema` 匹配，你可以直接将智能体的输出作为工具的输入。
- **可替换性**：若决定切换到其他搜索服务，只需导入新的搜索工具并相应更新 `output_schema` 即可。

例如，若要切换到另一个搜索服务：

```python
# Import a different search tool
from web_search_agent.tools.another_search import AnotherSearchTool

# Update the output schema
query_agent.config.output_schema = AnotherSearchTool.input_schema
```

这种设计模式简化了智能体与工具的串联流程，使你的 AI 应用更具适应性且更易于维护。

## 示例与文档

[![Read the Docs](https://img.shields.io/badge/docs-read%20the%20docs-blue?logo=readthedocs&style=for-the-badge)](https://brainblend-ai.github.io/atomic-agents/)

[访问文档站点 »](https://brainblend-ai.github.io/atomic-agents/)

### 快速入门示例

完整示例列表位于 [examples](./atomic-examples/) 目录中。我们致力于详尽记录每个示例，若有任何不清楚之处，欢迎随时提交 Issue 或 Pull Request 以完善文档。

如需完整可运行的示例代码，请参考 `atomic-examples/quickstart/quickstart/` 目录下的以下文件：

- [基础聊天机器人](/atomic-examples/quickstart/quickstart/1_0_basic_chatbot.py) - 用于快速上手的极简聊天机器人示例。
- [自定义聊天机器人](/atomic-examples/quickstart/quickstart/2_basic_custom_chatbot.py) - 带有自定义系统提示词的进阶示例。
- [带模式的自定义聊天机器人](/atomic-examples/quickstart/quickstart/3_0_basic_custom_chatbot_with_custom_schema.py) - 包含自定义输出模式的高级示例。
- [多 Provider 聊天机器人](/atomic-examples/quickstart/quickstart/4_basic_chatbot_different_providers.py) - 演示如何使用 Ollama、Groq 等不同服务提供方。

### 完整示例

除快速入门示例外，我们还提供了更多复杂示例，以展示 Atomic Agents 的强大功能：

- [Hook 机制（Hooks System）](/atomic-examples/hooks-example/README.md): 全面演示用于监控、错误处理及性能指标（含智能重试机制）的 AtomicAgent Hook 系统。
- [基础多模态（Basic Multimodal）](/atomic-examples/basic-multimodal/README.md): 展示如何结合文本分析图像，重点演示利用 GPT-4 Vision 能力从营养标签中提取结构化信息。
- [深度研究（Deep Research）](/atomic-examples/deep-research/README.md): 高级示例，演示如何执行深度研究任务。
- [编排智能体（Orchestration Agent）](/atomic-examples/orchestration-agent/README.md): 展示如何创建编排智能体（Orchestrator Agent），根据用户输入智能决策使用不同工具（搜索或计算器）。
- [RAG 聊天机器人（RAG Chatbot）](/atomic-examples/rag-chatbot/README.md): 基于检索增强生成（RAG）技术实现，提供具有上下文感知能力的回复。
- [网页搜索智能体（Web Search Agent）](/atomic-examples/web-search-agent/README.md): 执行网页搜索并根据结果回答问题的智能体。
- [YouTube 视频摘要（YouTube Summarizer）](/atomic-examples/youtube-summarizer/README.md): 从 YouTube 视频中提取并总结知识的智能体。
- [YouTube 菜谱生成（YouTube to Recipe）](/atomic-examples/youtube-to-recipe/README.md): 演示如何从烹饪视频中提取结构化菜谱信息，展示复杂的信息抽取与结构化能力。

完整示例列表请参阅 [examples 目录](/atomic-examples/)。

## 🚀 v2.0 版本已发布！

[![What's New in V2.0](./.assets/whats-new-v2-thumbnail.png)](https://www.youtube.com/watch?v=ro-pM2bPmr0)

[**观看：Atomic Agents v2.0 新功能介绍**](https://www.youtube.com/watch?v=ro-pM2bPmr0)

**Atomic Agents v2.0 现已正式发布，带来重大升级！** 本次更新包含多项破坏性变更（Breaking Changes），显著提升了开发者体验：

### v2.0 主要变更：
- **更简洁的导入路径**：移除了导入路径中的 `.lib`
- **类名重命名**：`BaseAgent` → `AtomicAgent`，`BaseAgentConfig` → `AgentConfig` 等
- **更强的类型安全**：为工具与智能体引入泛型类型参数（Generic Type Parameters）
- **增强的流式处理**：新增 `run_stream()` 和 `run_async_stream()` 方法
- **更优的模块结构**：重构了 `context`、`connectors` 等模块的组织方式

### ⚠️ 从 v1.x 升级指南
如果你正从 v1.x 版本升级，请查阅详细的 [**升级指南**](UPGRADE_DOC.md)。

## Atomic Forge 与 CLI

Atomic Forge 是一组可与 Atomic Agents 配合使用以扩展其功能的工具。当前包含的工具如下：

- arXiv 搜索
- BoCha 搜索
- 计算器
- 日期时间
- Fía 信号
- Hacker News 搜索
- PDF 阅读器
- SearXNG 搜索
- Tavily 搜索
- 网页抓取器
- 天气查询
- 维基百科搜索
- YouTube 字幕提取

关于如何使用和创建工具的更多信息，请参阅 [Atomic Forge README](/atomic-forge/README.md)。

### 运行 CLI

要运行 CLI，只需执行以下命令：

```bash
atomic
```

若通过克隆的仓库使用 uv 运行：

```bash
uv run atomic
```

运行该命令后，你将看到一个菜单，允许你下载所需工具。

每个工具均包含以下独立内容：

- 输入模式（Input schema）
- 输出模式（Output schema）
- 使用示例（Usage example）
- 依赖项（Dependencies）
- 安装说明（Installation instructions）

![Atomic CLI tool example](./.assets/atomic-cli-tool-menu.png)

`atomic-assembler` CLI 让你完全掌控工具的使用，避免不必要的依赖堆积。它还使修改工具变得简单直观；此外，每个工具都附带专属测试套件以保障可靠性。

**但你不仅限于使用 CLI！** 如果你更倾向于手动操作，也可以直接访问工具文件夹，按需复制粘贴进行自主管理。

![Atomic CLI menu](./.assets/atomic-cli.png)

## 项目结构

Atomic Agents 采用 Monorepo（单体仓库）架构，主要包含以下组件：

1. `atomic-agents/`：Atomic Agents 核心库
2. `atomic-assembler/`：用于管理 Atomic Agents 组件的 CLI 工具
3. `atomic-examples/`：展示 Atomic Agents 用法的示例项目
4. `atomic-forge/`：可与 Atomic Agents 配合使用的工具集合

本地开发时，可从仓库进行安装：

```bash
git clone https://github.com/BrainBlend-AI/atomic-agents.git
cd atomic-agents
uv sync
```

若要安装所有工作区包（示例与工具）：

```bash
uv sync --all-packages
```

## Provider 与模型兼容性

Atomic Agents 依赖 [Instructor](https://github.com/jxnl/instructor) 包。这意味着在所有使用 OpenAI 的示例中，只要 Instructor 支持的其他 API 均可无缝替换——例如 Ollama、Groq、Mistral、Cohere、Anthropic、Gemini、[MiniMax](https://www.minimax.io/) 等。完整列表请参阅 Instructor 文档中的 [GitHub 页面](https://github.com/jxnl/instructor)。

## 贡献指南

我们欢迎所有形式的贡献！有关如何为 Atomic Agents 做出贡献的详细信息，请参阅 [贡献指南](/docs/contributing.md)。以下是一些快速步骤：

1. Fork 本仓库
2. 创建新分支（`git checkout -b feature-branch`）
3. 进行修改
4. 运行测试（`uv run pytest --cov=atomic_agents atomic-agents`）
5. 格式化代码（`uv run black atomic-agents atomic-assembler atomic-examples atomic-forge`）
6. 代码检查（`uv run flake8 --extend-exclude=.venv atomic-agents atomic-assembler atomic-examples atomic-forge`）
7. 提交更改（`git commit -m 'Add some feature'`）
8. 推送到分支（`git push origin feature-branch`）
9. 创建 Pull Request

完整的开发环境配置与规范指南，请参阅 [开发者指南](/guides/DEV_GUIDE.md)。

## 许可证

本项目采用 MIT 许可证开源——详情请参阅 [LICENSE](LICENSE) 文件。

## 其他资源

若想深入了解 Atomic Agents 的设计初衷与核心理念，推荐阅读这篇 Medium 文章（无需登录）：[链接](https://ai.gopubby.com/want-to-build-ai-agents-c83ab4535411?sk=b9429f7c57dbd3bda59f41154b65af35)。

**视频资源：**
- [观看概述视频](https://www.youtube.com/watch?v=Sp30YsjGUW0) - 了解框架理念与设计原则
- [观看快速入门视频](https://www.youtube.com/watch?v=CyZxRU0ax3Q) - 通过代码示例快速上手

## 星标历史

[![Star History Chart](https://api.star-history.com/svg?repos=BrainBlend-AI/atomic-agents&type=Date)](https://star-history.com/#BrainBlend-AI/atomic-agents&Date)
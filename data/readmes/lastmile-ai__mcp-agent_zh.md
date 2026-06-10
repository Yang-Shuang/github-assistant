<p align="center">
  <a href="https://docs.mcp-agent.com"><img src="https://github.com/user-attachments/assets/c8d059e5-bd56-4ea2-a72d-807fb4897bde" alt="Logo" width="300" /></a>
</p>

<p align="center">
  <em>使用简单、可组合的模式，通过模型上下文协议（Model Context Protocol）构建高效的智能体。</em>

<p align="center">
  <a href="https://github.com/lastmile-ai/mcp-agent/tree/main/examples" target="_blank"><strong>示例</strong></a>
  |
  <a href="https://docs.mcp-agent.com/mcp-agent-sdk/effective-patterns/overview" target="_blank"><strong>构建高效智能体</strong></a>
  |
  <a href="https://modelcontextprotocol.io/introduction" target="_blank"><strong>MCP</strong></a>
</p>

<p align="center">
<a href="https://docs.mcp-agent.com"><img src="https://img.shields.io/badge/docs-8F?style=flat&link=https%3A%2F%2Fdocs.mcp-agent.com%2F" /><a/>
<a href="https://pypi.org/project/mcp-agent/"><img src="https://img.shields.io/pypi/v/mcp-agent?color=%2334D058&label=pypi" /></a>
<img alt="Pepy Total Downloads" src="https://img.shields.io/pepy/dt/mcp-agent?label=pypi%20%7C%20downloads"/>
<a href="https://github.com/lastmile-ai/mcp-agent/blob/main/LICENSE"><img src="https://img.shields.io/badge/License-Apache_2.0-blue.svg"/></a>
<a href="https://lmai.link/discord/mcp-agent"><img src="https://img.shields.io/badge/Discord-%235865F2.svg?logo=discord&logoColor=white" alt="discord"/></a>
</p>

<p align="center">
<a href="https://trendshift.io/repositories/13216" target="_blank"><img src="https://trendshift.io/api/badge/repositories/13216" alt="lastmile-ai%2Fmcp-agent | Trendshift" style="width: 250px; height: 55px;" width="250" height="55"/></a>
</p>

## 概述

**`mcp-agent`** 是一个简单、可组合的框架，用于使用 [模型上下文协议](https://modelcontextprotocol.io/introduction) 构建高效的智能体。

> [!Note]
> `mcp-agent` 的愿景是：_构建智能体只需 MCP，且对于交付高质量智能体而言，简单的模式比复杂的架构更稳健。*_

`mcp-agent` 为你提供以下内容：

1. **完整的 MCP 支持**：它*完全*实现了 MCP，并处理了管理 MCP 服务器连接生命周期的繁琐工作，让你无需操心。
2. **高效的智能体模式**：它以*可组合*的方式实现了 Anthropic [构建高效智能体](https://www.anthropic.com/engineering/building-effective-agents) 中描述的所有模式，允许你将这些模式串联使用。
3. **持久化智能体**：它既适用于简单智能体，也能扩展到基于 [Temporal](https://temporal.io/) 构建的复杂工作流，让你无需更改智能体的 API 即可暂停、恢复和重试。

<u>总而言之，这是构建健壮的智能体应用最简单、最便捷的方式</u>。

我们欢迎各种 [贡献](/CONTRIBUTING.md)、反馈以及帮助改进此项目的力量。

<a id="minimal-example"></a>
**最小示例**

```python
import asyncio

from mcp_agent.app import MCPApp
from mcp_agent.agents.agent import Agent
from mcp_agent.workflows.llm.augmented_llm_openai import OpenAIAugmentedLLM

app = MCPApp(name="hello_world")

async def main():
    async with app.run():
        agent = Agent(
            name="finder",
            instruction="Use filesystem and fetch to answer questions.",
            server_names=["filesystem", "fetch"],
        )
        async with agent:
            llm = await agent.attach_llm(OpenAIAugmentedLLM)
            answer = await llm.generate_str("Summarize README.md in two sentences.")
            print(answer)


if __name__ == "__main__":
    asyncio.run(main())

# Add your LLM API key to `mcp_agent.secrets.yaml` or set it in env.
# The [Getting Started guide](https://docs.mcp-agent.com/get-started/overview) walks through configuration and secrets in detail.

```

## 概览

<table>
  <tr>
    <td width="50%" valign="top">
      <h3>构建智能体</h3>
      <p>将大语言模型（LLM）连接到 MCP 服务器，使用 map-reduce、orchestrator、evaluator-optimizer、router 等简单可组合的模式。</p>
      <p>
        <a href="https://docs.mcp-agent.com/get-started/overview">快速入门 ↗</a> | 
        <a href="https://docs.mcp-agent.com/mcp-agent-sdk/overview">文档 ↗</a>
      </p>
    </td>
    <td width="50%" valign="top">
      <h3>创建任意类型的 MCP 服务器</h3>
      <p>使用兼容 FastMCP 的 API 创建 MCP 服务器。你甚至可以将智能体暴露为 MCP 服务器。</p>
      <p>
        <a href="https://docs.mcp-agent.com/mcp-agent-sdk/mcp/agent-as-mcp-server">MCP Agent Server ↗</a> | 
        <a href="https://docs.mcp-agent.com/cloud/use-cases/deploy-chatgpt-apps">🎨 构建 ChatGPT 应用 ↗</a> | 
        <a href="https://github.com/lastmile-ai/mcp-agent/tree/main/examples/mcp_agent_server">示例 ↗</a>
      </p>
    </td>
  </tr>
    <tr>
    <td width="50%" valign="top">
      <h3>完整的 MCP 支持</h3>
      <p><b>核心：</b>工具 ✅ 资源 ✅ 提示词 ✅ 通知 ✅<br/>
      <b>高级功能</b>：OAuth ✅ 采样（Sampling）✅ 信息获取（Elicitation）✅ 根目录（Roots）✅</p>
      <p>
        <a href="https://github.com/lastmile-ai/mcp-agent/tree/main/examples/mcp">示例 ↗</a> | 
        <a href="https://modelcontextprotocol.io/docs/getting-started/intro">MCP 文档 ↗</a>
      </p>
    </td>
    <td width="50%" valign="top">
      <h3>持久化执行（Temporal）</h3>
      <p>使用 Temporal 作为智能体运行时后端，无需任何 API 更改即可扩展到生产级负载。</p>
      <p>
        <a href="https://docs.mcp-agent.com/mcp-agent-sdk/advanced/durable-agents">文档 ↗</a> | 
        <a href="https://github.com/lastmile-ai/mcp-agent/tree/main/examples/temporal">示例 ↗</a>
      </p>
    </td>
  </tr>
  <tr>
    <td width="50%" valign="top">
      <h3>☁️ 部署到云端</h3>
      <p><b>测试版：</b>自行部署智能体，或使用 <b>mcp-c</b> 获得托管的智能体运行时。所有应用均以 MCP 服务器形式部署。</p>
      <p>
        <a href="https://www.youtube.com/watch?v=0C4VY-3IVNU">演示 ↗</a> |
        <a href="https://docs.mcp-agent.com/get-started/cloud">云端快速入门 ↗</a> | 
        <a href="https://github.com/lastmile-ai/mcp-agent/tree/main/examples/cloud">示例 ↗</a>
      </p>
    </td>
  </tr>
</table>

## 文档与使用 LLM 构建

`mcp-agent` 的完整文档位于 **[docs.mcp-agent.com](https://docs.mcp-agent.com)**，包含完整的 SDK 指南、CLI 参考和高级模式。本 README 提供了帮助你入门的高级概述。

- [`llms-full.txt`](https://docs.mcp-agent.com/llms-full.txt)：包含全部文档内容。
- [`llms.txt`](https://docs.mcp-agent.com/llms.txt)：列出文档中关键页面的站点地图。
- [docs MCP 服务器](https://docs.mcp-agent.com/mcp)

## 目录

- [概述](#overview)
- [最小示例](#minimal-example)
- [快速入门](#get-started)
- [为什么选择 `mcp-agent`](#why-use-mcp-agent)
- [核心概念](#core-components)
  - [MCPApp](#mcpapp)
  - [智能体与 AgentSpec](#agents--agentspec)
  - [增强型 LLM（Augmented LLM）](#augmented-llm)
  - [工作流与装饰器](#workflows--decorators)
  - [配置与密钥](#configuration--secrets)
  - [MCP 集成](#mcp-integration)
- [工作流模式](#workflow-patterns)
- [CLI 参考](#cli-reference)
- [身份验证](#authentication)
- [高级功能](#advanced)
  - [可观测性与控制](#observability--controls)
  - [组合工作流](#composing-workflows)
  - [持久化执行](#durable-execution)
  - [智能体服务器](#agent-servers)
  - [信号与人工输入](#signals--human-input)
  - [应用配置](#app-configuration)
  - [图标](#icons)
  - [MCP 服务器管理](#mcp-server-management)
- [云端部署](#cloud-deployment)
- [示例](#examples)
- [常见问题](#faqs)
- [社区与贡献](#contributing)

## 快速入门

> [!TIP]
> CLI 可通过 `uvx mcp-agent` 使用。
> 要快速上手，
> 请使用 `uvx mcp-agent init` 创建项目脚手架，并使用 `uvx mcp-agent deploy my-agent` 进行部署。
>
> 你可以通过运行以下命令在 2 分钟内完成配置：
>
> ```bash
> mkdir hello-mcp-agent && cd hello-mcp-agent
> uvx mcp-agent init
> uv init
> uv add "mcp-agent[openai]"
> # Add openai API key to `mcp_agent.secrets.yaml` or set `OPENAI_API_KEY`
> uv run main.py
> ```

### 安装

我们建议使用 [uv](https://docs.astral.sh/uv/) 来管理你的 Python 项目（`uv init`）。

```bash
uv add "mcp-agent"
```

或者：

```bash
pip install mcp-agent
```

同时为 LLM 提供商添加可选包（例如 `uv add "mcp-agent[openai, anthropic, google, azure, bedrock]"`）。

### 快速入门指南

> [!TIP]
> [`examples`](/examples) 目录中提供了多个示例应用以帮助你起步。
> 要运行示例，请克隆此仓库（或使用 `uvx mcp-agent init --template basic --dir my-first-agent` 生成一个）：
>
> ```bash
> cd examples/basic/mcp_basic_agent # Or any other example
> # Option A: secrets YAML
> # cp mcp_agent.secrets.yaml.example mcp_agent.secrets.yaml && edit mcp_agent.secrets.yaml
> uv run main.py
> ```

这是一个基础的“查找（finder）”智能体，它使用 fetch 和 filesystem 服务器来查找文件、阅读博客并撰写推文。[示例链接](./examples/basic/mcp_basic_agent/)：

<details open>
<summary>finder_agent.py</summary>

```python
import asyncio
import os

from mcp_agent.app import MCPApp
from mcp_agent.agents.agent import Agent
from mcp_agent.workflows.llm.augmented_llm_openai import OpenAIAugmentedLLM

app = MCPApp(name="hello_world_agent")

async def example_usage():
    async with app.run() as mcp_agent_app:
        logger = mcp_agent_app.logger
        # This agent can read the filesystem or fetch URLs
        finder_agent = Agent(
            name="finder",
            instruction="""You can read local files or fetch URLs.
                Return the requested information when asked.""",
            server_names=["fetch", "filesystem"], # MCP servers this Agent can use
        )

        async with finder_agent:
            # Automatically initializes the MCP servers and adds their tools for LLM use
            tools = await finder_agent.list_tools()
            logger.info(f"Tools available:", data=tools)

            # Attach an OpenAI LLM to the agent (defaults to GPT-4o)
            llm = await finder_agent.attach_llm(OpenAIAugmentedLLM)

            # This will perform a file lookup and read using the filesystem server
            result = await llm.generate_str(
                message="Show me what's in README.md verbatim"
            )
            logger.info(f"README.md contents: {result}")

            # Uses the fetch server to fetch the content from URL
            result = await llm.generate_str(
                message="Print the first two paragraphs from https://www.anthropic.com/research/building-effective-agents"
            )
            logger.info(f"Blog intro: {result}")

            # Multi-turn interactions by default
            result = await llm.generate_str("Summarize that in a 128-char tweet")
            logger.info(f"Tweet: {result}")

if __name__ == "__main__":
    asyncio.run(example_usage())

```

</details>

<details>
<summary>mcp_agent.config.yaml</summary>

```yaml
execution_engine: asyncio
logger:
  transports: [console] # You can use [file, console] for both
  level: debug
  path: "logs/mcp-agent.jsonl" # Used for file transport
  # For dynamic log filenames:
  # path_settings:
  #   path_pattern: "logs/mcp-agent-{unique_id}.jsonl"
  #   unique_id: "timestamp"  # Or "session_id"
  #   timestamp_format: "%Y%m%d_%H%M%S"

mcp:
  servers:
    fetch:
      command: "uvx"
      args: ["mcp-server-fetch"]
    filesystem:
      command: "npx"
      args:
        [
          "-y",
          "@modelcontextprotocol/server-filesystem",
          "<add_your_directories>",
        ]

openai:
  # Secrets (API keys, etc.) are stored in an mcp_agent.secrets.yaml file which can be gitignored
  default_model: gpt-4o
```

</details>

<details>
<summary>Agent output</summary>
<img width="2398" alt="Image" src="https://github.com/user-attachments/assets/eaa60fdf-bcc6-460b-926e-6fa8534e9089" />
</details>

## 为什么选择 `mcp-agent`？

市面上已经有很多 AI 框架了，但 `mcp-agent` 是唯一一个专为共享协议——[MCP](https://modelcontextprotocol.io/introduction)——而设计的。[mcp-agent](https://docs.mcp-agent.com/get-started/welcome) 将 Anthropic 的构建高效智能体模式与开箱即用的 MCP 运行时相结合，让你专注于业务逻辑而非样板代码。团队选择它是因为：

- **可组合（Composable）** – 每个模式都作为可复用的工作流提供，你可以自由混合搭配。
- **原生支持 MCP（MCP-native）** – 任何 MCP 服务器（filesystem、fetch、Slack、Jira、FastMCP 应用）均可直接连接，无需自定义适配器。
- **生产就绪（Production ready）** – 基于 Temporal 的持久化能力、结构化日志记录、Token 计量以及云端部署均为一等公民功能。
- **符合 Python 风格（Pythonic）** – 仅通过少量装饰器和上下文管理器即可将所有组件串联起来。

文档：[欢迎使用 mcp-agent](https://docs.mcp-agent.com/get-started/welcome) • [高效模式概览](https://docs.mcp-agent.com/mcp-agent-sdk/effective-patterns/overview)。

## 核心概念

每个项目都围绕单个 `MCPApp` 运行时展开，它负责加载配置、注册智能体和 MCP 服务器，并暴露工具和工作流。[核心组件指南](https://docs.mcp-agent.com/mcp-agent-sdk/overview) 详细介绍了这些构建块。

### MCPApp

初始化配置、日志记录、链路追踪和执行引擎，使所有组件共享同一个上下文。

```python
from mcp_agent.app import MCPApp

app = MCPApp(name="finder_app")

async def main():
    async with app.run() as running_app:
        logger = running_app.logger
        logger.info("App ready", data={"servers": list(running_app.context.server_registry.registry)})
```

文档：[MCPApp](https://docs.mcp-agent.com/mcp-agent-sdk/core-components/mcpapp) • 示例：[`examples/basic/mcp_basic_agent`](./examples/basic/mcp_basic_agent/)。

### 智能体与 AgentSpec

智能体将指令与其可调用的 MCP 服务器（及可选函数）绑定在一起。`AgentSpec` 定义可以从磁盘加载，并通过工厂辅助方法转换为智能体或增强型 LLM。

```python
from pathlib import Path
from mcp_agent.agents.agent import Agent
from mcp_agent.workflows.factory import load_agent_specs_from_file

agent = Agent(
    name="researcher",
    instruction="Research topics using web and filesystem access",
    server_names=["fetch", "filesystem"],
)

async with agent:
    tools = await agent.list_tools()

async with app.run() as running_app:
    specs = load_agent_specs_from_file(
        str(Path("examples/basic/agent_factory/agents.yaml")),
        context=running_app.context,
    )
```

文档：[智能体](https://docs.mcp-agent.com/mcp-agent-sdk/core-components/agents) • [Agent 工厂辅助方法](https://docs.mcp-agent.com/mcp-agent-sdk/core-components/agents#agentspec-and-factory-helpers) • 示例：[`examples/basic/agent_factory`](./examples/basic/agent_factory/)。

### 增强型 LLM（Augmented LLM）

增强型 LLM 将提供商 SDK 与智能体的工具、记忆和结构化输出辅助方法包装在一起。将其附加到智能体上即可解锁 `generate`、`generate_str` 和 `generate_structured` 功能。

```python
from pydantic import BaseModel
from mcp_agent.workflows.llm.augmented_llm import RequestParams
from mcp_agent.workflows.llm.augmented_llm_openai import OpenAIAugmentedLLM

class Summary(BaseModel):
    title: str
    verdict: str

async with agent:
    llm = await agent.attach_llm(OpenAIAugmentedLLM)
    report = await llm.generate_str(
        message="Draft a 3-sentence release note from CHANGELOG.md",
        request_params=RequestParams(maxTokens=400, temperature=0.2),
    )
    structured = await llm.generate_structured(
        message="Return a JSON object with `title` and `verdict` summarising the README.",
        response_model=Summary,
    )
```

文档：[增强型 LLM](https://docs.mcp-agent.com/mcp-agent-sdk/core-components/augmented-llm) • 示例：[`examples/basic/mcp_basic_agent`](./examples/basic/mcp_basic_agent/) 以及 [gallery.md](gallery.md#workflow-patterns) 中列出的工作流项目。

### 工作流与装饰器

`MCPApp` 装饰器将协程转换为持久化工作流和工具。相同的注解同时适用于 `asyncio` 和 Temporal 执行引擎。

```python
from datetime import timedelta
from mcp_agent.executor.workflow import Workflow, WorkflowResult

@app.workflow
class PublishArticle(Workflow[WorkflowResult[str]]):
    @app.workflow_task(schedule_to_close_timeout=timedelta(minutes=5))
    async def draft(self, topic: str) -> str:
        return f"- intro to {topic}\n- highlights\n- next steps"

    @app.workflow_run
    async def run(self, topic: str) -> WorkflowResult[str]:
        outline = await self.draft(topic)
        return WorkflowResult(value=outline)
```

文档：[装饰器参考](https://docs.mcp-agent.com/reference/decorators) • 示例：[`examples/workflows`](./examples/workflows/)。

### 配置与密钥

设置从 `mcp_agent.config.yaml`、`mcp_agent.secrets.yaml`、环境变量和可选的预加载字符串中加载。请将密钥保留在版本控制之外。

```yaml
# mcp_agent.config.yaml
execution_engine: asyncio
mcp:
  servers:
    fetch:
      command: "uvx"
      args: ["mcp-server-fetch"]
    filesystem:
      command: "npx"
      args: ["-y", "@modelcontextprotocol/server-filesystem"]
openai:
  default_model: gpt-4o-mini

# mcp_agent.secrets.yaml (gitignored)
openai:
  api_key: "${OPENAI_API_KEY}"
```

文档：[配置参考](https://docs.mcp-agent.com/reference/configuration) • [指定密钥](https://docs.mcp-agent.com/mcp-agent-sdk/core-components/specify-secrets)。

### MCP 集成

通过编程方式连接到现有的 MCP 服务器，或将多个服务器聚合为一个外观（Facade）。

```python
from mcp_agent.mcp.gen_client import gen_client

async with app.run():
    async with gen_client("filesystem", app.server_registry, context=app.context) as client:
        resources = await client.list_resources()
        app.logger.info("Filesystem resources", data={"uris": [r.uri for r in resources.resources]})
```

文档：[MCP 集成概览](https://docs.mcp-agent.com/mcp/overview) • 示例：[`examples/mcp`](./examples/mcp/)。

## 工作流模式

关键智能体模式已实现为 `AugmentedLLM`。使用工厂辅助方法进行连接，或查看 [gallery.md](gallery.md#workflow-patterns) 中列出的可运行项目。

| 模式                  | 辅助方法                                                                          | 摘要                                                                                                                                                                                                                                                                                                                                                                                                                                                            | 文档                                                                                                   |
| --------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------ |
| 并行（Map-Reduce）    | `create_parallel_llm(...)`                                                      | 分发至多个专家并聚合报告。<br><a href="https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F406bb032ca007fd1624f261af717d70e6ca86286-2401x1000.png&w=3840&q=75"><img src="https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F406bb032ca007fd1624f261af717d70e6ca86286-2401x1000.png&w=3840&q=75" width="260"/></a>     | [并行](https://docs.mcp-agent.com/mcp-agent-sdk/effective-patterns/map-reduce)                     |
| 路由器                | `create_router_llm(...)` / `create_router_embedding(...)`                       | 将请求路由至最佳智能体、服务器或函数。<br><a href="https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F5c0c0e9fe4def0b584c04d37849941da55e5e71c-2401x1000.png&w=3840&q=75"><img src="https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F5c0c0e9fe4def0b584c04d37849941da55e5e71c-2401x1000.png&w=3840&q=75" width="260"/></a> | [路由器](https://docs.mcp-agent.com/mcp-agent-sdk/effective-patterns/router)                           |
| 意图分类器            | `create_intent_classifier_llm(...)` / `create_intent_classifier_embedding(...)` | 在自动化之前将用户输入归类到特定意图中。                                                                                                                                                                                                                                                                                                                                                                                                                  | [意图分类器](https://docs.mcp-agent.com/mcp-agent-sdk/effective-patterns/intent-classifier)     |
| 编排器与工作者        | `create_orchestrator(...)`                                                      | 生成计划并协调工作者智能体。<br><a href="https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F8985fc683fae4780fb34eab1365ab78c7e51bc8e-2401x1000.png&w=3840&q=75"><img src="https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F8985fc683fae4780fb34eab1365ab78c7e51bc8e-2401x1000.png&w=3840&q=75" width="260"/></a>           | [规划器](https://docs.mcp-agent.com/mcp-agent-sdk/effective-patterns/planner)                         |
| 深度研究              | `create_deep_orchestrator(...)`                                                 | 支持长周期研究，具备知识提取和政策检查功能。                                                                                                                                                                                                                                                                                                                                                                                                                 | [深度研究](https://docs.mcp-agent.com/mcp-agent-sdk/effective-patterns/deep-research)             |
| 评估器-优化器         | `create_evaluator_optimizer_llm(...)`                                           | 迭代直到评估器批准结果。<br><a href="https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F14f51e6406ccb29e695da48b17017e899a6119c7-2401x1000.png&w=3840&q=75"><img src="https://www.anthropic.com/_next/image?url=https%3A%2F%2Fwww-cdn.anthropic.com%2Fimages%2F4zrzovbb%2Fwebsite%2F14f51e6406ccb29e695da48b17017e899a6119c7-2401x1000.png&w=3840&q=75" width="260"/></a>        | [评估器-优化器](https://docs.mcp-agent.com/mcp-agent-sdk/effective-patterns/evaluator-optimizer) |
| 蜂群（Swarm）         | `create_swarm(...)`                                                             | 与 OpenAI Swarm 兼容的多智能体交接机制。<br><a href="https://github.com/openai/swarm/blob/main/assets/swarm_diagram.png?raw=true"><img src="https://github.com/openai/swarm/blob/main/assets/swarm_diagram.png?raw=true" width="220"/></a>                                                                                                                                                                                                               | [蜂群](https://docs.mcp-agent.com/mcp-agent-sdk/effective-patterns/swarm)                             |

## 持久化执行

将 `execution_engine` 切换为 `temporal` 即可支持暂停/恢复、重试、人工输入和持久化历史记录，且无需更改工作流代码。在应用旁运行一个 worker 来托管活动（Activities）。

```python
from mcp_agent.executor.temporal import create_temporal_worker_for_app

async with create_temporal_worker_for_app(app) as worker:
    await worker.run()
```

文档：[持久化智能体](https://docs.mcp-agent.com/mcp-agent-sdk/advanced/durable-agents) • [Temporal 后端](https://docs.mcp-agent.com/advanced/temporal) • 示例：[`examples/temporal`](./examples/temporal/)。

## 智能体服务器

将 `MCPApp` 暴露为标准 MCP 服务器，以便 Claude Desktop、Cursor 或自定义客户端调用你的工具和流程。

```python
from mcp_agent.server import create_mcp_server_for_app

@app.tool
def grade_story(story: str) -> str:
    return "Report..."

if __name__ == "__main__":
    server = create_mcp_server_for_app(app)
    server.run_stdio()
```

文档：[智能体服务器](https://docs.mcp-agent.com/mcp-agent-sdk/mcp/agent-as-mcp-server) • 示例：[`examples/mcp_agent_server`](./examples/mcp_agent_server/)。

## CLI 参考

`uvx mcp-agent` 用于创建项目脚手架、管理密钥、检查工作流以及部署到云端。

```bash
uvx mcp-agent init --template basic             # 创建新项目脚手架
uvx mcp-agent deploy my-agent                   # 部署至 mcp-agent Cloud
```

文档：[CLI 参考](https://docs.mcp-agent.com/reference/cli) • [入门指南](https://docs.mcp-agent.com/get-started/quickstart)。

## 身份验证

从密钥文件中加载 API 密钥，或使用内置的 OAuth 客户端获取并持久化 MCP 服务器的令牌。

```yaml
# mcp_agent.config.yaml excerpt
oauth:
  providers:
    github:
      client_id: "${GITHUB_CLIENT_ID}"
      client_secret: "${GITHUB_CLIENT_SECRET}"
      scopes: ["repo", "user"]
```

文档：[高级身份验证](https://docs.mcp-agent.com/mcp-agent-sdk/advanced/authentication) • [服务器认证](https://docs.mcp-agent.com/mcp-agent-sdk/mcp/server-authentication) • 示例：[`examples/basic/oauth_basic_agent`](./examples/basic/oauth_basic_agent/)。

## 高级功能

### 可观测性与控制

通过配置启用结构化日志记录和 OpenTelemetry，并通过编程方式跟踪 Token 使用情况。

```yaml
# mcp_agent.config.yaml
logger:
  transports: [console]
  level: info
otel:
  enabled: true
  exporters:
    - console
```

`TokenCounter` 用于追踪智能体、工作流和 LLM 节点的 Token 使用情况。附加监听器以流式传输更新或触发警报。

```python
# Inside `async with app.run() as running_app:`
# token_counter lives on the running app context when tracing is enabled.
token_counter = running_app.context.token_counter

class TokenMonitor:
    async def on_token_update(self, node, usage):
        print(f"[{node.name}] total={usage.total_tokens}")

monitor = TokenMonitor()
watch_id = await token_counter.watch(
    callback=monitor.on_token_update,
    node_type="llm",
    threshold=1_000,
    include_subtree=True,
)

await token_counter.unwatch(watch_id)
```

文档：[可观测性](https://docs.mcp-agent.com/mcp-agent-sdk/advanced/observability) • 示例：[`examples/tracing`](./examples/tracing/)。

### 组合工作流

混合搭配 AgentSpecs，使用工厂辅助方法构建更高级别的工作流——路由器、并行流水线、编排器等。

```python
from mcp_agent.workflows.factory import create_router_llm

# specs are loaded via load_agent_specs_from_file as shown above.
async with app.run() as running_app:
    router = await create_router_llm(
        agents=specs,
        provider="openai",
        context=running_app.context,
    )
```

文档：[工作流组合](https://docs.mcp-agent.com/mcp-agent-sdk/advanced/composition) • 示例：[`examples/basic/agent_factory`](./examples/basic/agent_factory/)。

### 信号与人工输入

暂停工作流以等待审批或额外数据。Temporal 会持久化存储状态，直到操作员恢复运行。

```python
from mcp_agent.human_input.types import HumanInputRequest

response = await self.context.request_human_input(
    HumanInputRequest(
        prompt="Approve the draft?",
        required=True,
        metadata={"workflow_id": self.context.workflow_id},
    )
)
```

使用 `mcp-agent cloud workflows resume … --payload '{"content": "approve"}'` 恢复运行。文档：[部署智能体 – 人工输入](https://docs.mcp-agent.com/cloud/use-cases/deploy-agents#human-in-the-loop-patterns) • 示例：[`examples/human_input/temporal`](./examples/human_input/temporal/)。

### 应用配置

当你需要动态配置（如测试、多租户主机）而不是 YAML 文件时，可通过编程方式构建 `Settings` 对象。

```python
from mcp_agent.config import Settings, MCPSettings, MCPServerSettings

settings = Settings(
    execution_engine="asyncio",
    mcp=MCPSettings(
        servers={
            "fetch": MCPServerSettings(command="uvx", args=["mcp-server-fetch"]),
        }
    ),
)
app = MCPApp(name="configured_app", settings=settings)
```

文档：[配置你的应用](https://docs.mcp-agent.com/mcp-agent-sdk/core-components/configuring-your-application)。

### 图标

为智能体和工具添加图标，以便支持图像渲染的 MCP 客户端（如 Claude Desktop、Cursor）呈现更丰富的 UI。

```python
from base64 import standard_b64encode
from pathlib import Path
from mcp_agent.icons import Icon

icon_data = standard_b64encode(Path("my-icon.png").read_bytes()).decode()
icon = Icon(src=f"data:image/png;base64,{icon_data}", mimeType="image/png", sizes=["64x64"])

app = MCPApp(name="my_app_with_icon", icons=[icon])

@app.tool(icons=[icon])
async def my_tool() -> str:
    return "Hello with style"
```

文档：[`MCPApp` 图标](https://docs.mcp-agent.com/mcp-agent-sdk/core-components/mcpapp#icons) • 示例：[`examples/mcp_agent_server/asyncio`](./examples/mcp_agent_server/asyncio/)。

### MCP 服务器管理

使用 `MCPAggregator` 或 `gen_client` 来管理 MCP 服务器连接并暴露组合工具集。

```python
from mcp_agent.mcp.mcp_aggregator import MCPAggregator

async with MCPAggregator.create(server_names=["fetch", "filesystem"]) as aggregator:
    tools = await aggregator.list_tools()
```

文档：[连接到 MCP 服务器](https://docs.mcp-agent.com/mcp-agent-sdk/core-components/connecting-to-mcp-servers) • 示例：[`examples/basic/mcp_server_aggregator`](./examples/basic/mcp_server_aggregator/)。

## 云端部署

部署到 mcp-agent Cloud 以获取托管的 Temporal 执行、密钥管理和 HTTPS MCP 端点。

```bash
uvx mcp-agent login
uvx mcp-agent deploy my-agent
uvx mcp-agent cloud apps list
```

文档：[云端概览](https://docs.mcp-agent.com/cloud/overview) • [部署快速入门](https://docs.mcp-agent.com/cloud/deployment-quickstart) • 示例：[`examples/cloud`](./examples/cloud/)。

## 示例

浏览 [gallery.md](gallery.md) 查看按概念分类的可运行示例、演示视频和社区项目。每个条目都引用了文档页面以及你在本地运行它所需的命令。

## 常见问题

### 使用 mcp-agent 的核心优势是什么？

mcp-agent 提供了一种简化的方法来构建利用 **MCP**（模型上下文协议）服务器暴露能力的 AI 智能体。

MCP 本身相当底层，而该框架处理了连接到服务器、与大语言模型交互、处理外部信号（如人工输入）以及通过持久化执行支持状态保持的机械细节。这让你作为开发者可以专注于 AI 应用的核心业务逻辑。

核心优势：
- 🤝 **互操作性**：确保任何 MCP 服务器暴露的工具都能无缝接入你的智能体。
- ⛓️ **可组合性与自定义性**：实现了定义明确的工作流，但以可组合的方式支持复合工作流，并允许对模型提供商、日志记录、编排器等进行全面定制。
- 💻 **编程式控制流**：保持开发简单，开发者只需编写代码即可，无需在图、节点和边之间进行思维转换。对于分支逻辑，你编写 `if` 语句；对于循环，使用 `while` 循环。
- 🖐️ **人工输入与信号**：支持暂停工作流以等待外部信号（如人工输入），这些信号作为智能体可调用的工具调用暴露。

### 必须拥有 MCP 客户端才能使用 mcp-agent 吗？

不需要，你可以在任何地方使用 mcp-agent，因为它会为你处理 `MCPClient` 的创建。这允许你在 MCP 主机（如 Claude Desktop）之外利用 MCP 服务器。

以下是你可以设置 mcp-agent 应用的所有方式：

#### MCP-Agent Server

你可以将 mcp-agent 应用本身暴露为 MCP 服务器（参见 [示例](./examples/mcp_agent_server)），允许 MCP 客户端使用 MCP 服务器的标准工具 API 与复杂的 AI 工作流进行交互。这本质上是一个“服务器中的服务器”。

#### MCP 客户端或主机

你可以直接在 MCP 客户端中嵌入 mcp-agent，以管理多个 MCP 服务器之间的编排。

#### 独立运行

你可以独立使用 mcp-agent 应用（即它们不属于任何 MCP 客户端）。[`examples`](/examples/) 目录中的所有示例均为独立应用。

### 如何部署到云端？

在使用 `uvx mcp-agent login` 登录后，运行 `uvx mcp-agent deploy <app-name>`。CLI 会打包你的项目、配置密钥，并暴露一个由持久化 Temporal 运行时支持的 MCP 端点。请参阅 [云端快速入门](https://docs.mcp-agent.com/get-started/cloud) 获取分步截图和 CLI 输出示例。

### API 参考文档在哪里？

每个类、装饰器和 CLI 命令都在 [docs.mcp-agent.com](https://docs.mcp-agent.com) 上有详细文档。[API 参考](https://docs.mcp-agent.com/reference) 和 [`llms-full.txt`](https://docs.mcp-agent.com/llms-full.txt) 的设计旨在让 LLM（或你）能够轻松摄入整个接口面。

### 分享一个有趣的事实

我曾考虑将此项目命名为 _silsila_ (سلسلہ)，这在乌尔都语中意为“事件链”。mcp-agent 这个名字更直白，但项目中仍然隐藏着一个向 silsila 致敬的彩蛋。

## 社区与贡献

我们欢迎各种规模的贡献——错误修复、新示例、文档或功能请求。请从 [CONTRIBUTING.md](./CONTRIBUTING.md) 开始，发起讨论，或前往 [Discord](https://lmai.link/discord/mcp-agent)。

如果没有众多开源贡献者的不懈努力，mcp-agent 就不可能实现。谢谢你们！

<p align="center">
  <a href="https://github.com/lastmile-ai/mcp-agent/graphs/contributors">
    <img src="https://contrib.rocks/image?repo=lastmile-ai/mcp-agent" alt="Contributor faces" />
  </a>
</p>
<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset=".github/images/logo_dark.png" />
    <source media="(prefers-color-scheme: light)" srcset=".github/images/logo_light.png" />
    <img alt="PraisonAI Logo" src=".github/images/logo_light.png" width="250" />
  </picture>
</p>

<!-- mcp-name: io.github.MervinPraison/praisonai -->

<p align="center">
<a href="https://github.com/MervinPraison/PraisonAI"><img src="https://static.pepy.tech/badge/PraisonAI" alt="Total Downloads" /></a>
<a href="https://github.com/MervinPraison/PraisonAI"><img src="https://img.shields.io/github/v/release/MervinPraison/PraisonAI" alt="Latest Stable Version" /></a>
<a href="https://github.com/MervinPraison/PraisonAI"><img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="License" /></a>
<a href="https://registry.modelcontextprotocol.io/servers/io.github.MervinPraison/praisonai"><img src="https://img.shields.io/badge/MCP-Registry-blue" alt="MCP Registry" /></a>
</p>

<div align="center">

# PraisonAI 🦞

<a href="https://trendshift.io/repositories/9130" target="_blank"><img src="https://trendshift.io/api/badge/repositories/9130" alt="MervinPraison%2FPraisonAI | Trendshift" style="width: 250px; height: 55px;" width="250" height="55"/></a>

</div>

PraisonAI 🦞 — **雇佣一支全天候（24/7）的 AI 劳动力。** 停止编写样板代码，开始交付自主运行、自我优化的智能体。它们能在你的应用中研究、规划并执行任务。从单个智能体到整个组织体系，仅需 5 行代码即可部署。

```bash
curl -fsSL https://praison.ai/install.sh | bash
```

<div align="center">
  <br>
  <a href="https://x.com/elonmusk/status/1893870468249141688" target="_blank">
    <img src="https://img.shields.io/badge/Highlighted_by_Elon_Musk-000000?style=for-the-badge&logo=x&logoColor=white" alt="Highlighted by Elon Musk" />
  </a>
  <br>
</div>

<p align="center">
  <img src=".github/images/dashboard.png" alt="PraisonAI Dashboard" width="800" />
</p>

<p align="center">
  <img src=".github/images/agentflow.gif" alt="PraisonAI AgentFlow" width="800" />
</p>

```
 ██████╗ ██████╗  █████╗ ██╗███████╗ ██████╗ ███╗   ██╗     █████╗ ██╗
 ██╔══██╗██╔══██╗██╔══██╗██║██╔════╝██╔═══██╗████╗  ██║    ██╔══██╗██║
 ██████╔╝██████╔╝███████║██║███████╗██║   ██║██╔██╗ ██║    ███████║██║
 ██╔═══╝ ██╔══██╗██╔══██║██║╚════██║██║   ██║██║╚██╗██║    ██╔══██║██║
 ██║     ██║  ██║██║  ██║██║███████║╚██████╔╝██║ ╚████║    ██║  ██║██║
 ╚═╝     ╚═╝  ╚═╝╚═╝  ╚═╝╚═╝╚══════╝ ╚═════╝ ╚═╝  ╚═══╝    ╚═╝  ╚═╝╚═╝

 pip install praisonai
```

<p align="center">
  <img src=".github/images/latest_ai_news_and_crawl_each_url_to_find_info.gif" alt="PraisonAI command execution" width="800" />
</p>

\* `export TAVILY_API_KEY=xxxxx`

<div align="center">
  <a href="https://docs.praison.ai">
    <p align="center">
      <img src="https://img.shields.io/badge/📚_Documentation-Visit_docs.praison.ai-blue?style=for-the-badge&logo=bookstack&logoColor=white" alt="Documentation" />
    </p>
  </a>
</div>

---

## 🎯 应用场景

AI 智能体在各行业解决现实问题：

| 应用场景 | 描述 |
|----------|-------------|
| 🔍 **研究与分析** | 自动开展深度研究，从多源收集信息并生成洞察 |
| 💻 **代码生成** | 编写、调试和重构代码。AI 智能体理解你的代码库与需求 |
| ✍️ **内容创作** | 通过多智能体团队协作，生成博客文章、文档、营销文案和技术写作 |
| 📊 **数据管道** | 自动从 API、数据库和网络源提取、转换和分析数据 |
| 🤖 **客户支持** | 在 Telegram、Discord、Slack 部署全天候客服机器人，具备记忆与知识库问答能力 |
| ⚙️ **工作流自动化** | 通过智能体交接任务、验证结果并自我修正，实现多步骤业务流程自动化 |

---

## 🚀 认识你的第一个智能体（1 分钟内完成）

1. 安装轻量级核心 SDK：
```bash
pip install praisonaiagents
export OPENAI_API_KEY="your-api-key"
```

2. 运行你的第一个自主智能体：
```python
from praisonaiagents import Agent

# Give your agent a goal, and watch it work.
agent = Agent(instructions="You are a senior data analyst.")
agent.start("Analyze the top 3 tech trends of 2026 and format as a markdown table.")
```

---

## 🌌 PraisonAI 生态系统

你可以从核心 SDK 开始，随时扩展至完整的可视化构建器和仪表盘。

*   **核心 SDK (`praisonaiagents`)**: 适用于纯 Python 开发。`pip install praisonaiagents`
*   💻 **PraisonAI CLI (`praisonai`)**: 面向终端开发者。 `pip install praisonai`
*   🦞 **Claw Dashboard**: 将智能体直接接入 Telegram、Slack 或 Discord。 `pip install "praisonai[claw]"`
*   🔗 **Flow Visual Builder**: 拖拽式工作流创建工具。 `pip install "praisonai[flow]"`
*   🤖 **PraisonAI UI**: 简洁的聊天界面。 `pip install "praisonai[ui]"`

### JavaScript SDK

```bash
npm install praisonai
```

## 🧠 支持的提供商与功能特性

支持 100+ 大语言模型（LLM），包括 OpenAI、Anthropic、Gemini 及本地模型。

<p align="center">
<img src="https://img.shields.io/badge/OpenAI-412991?style=flat&logo=openai&logoColor=white" alt="OpenAI" />
<img src="https://img.shields.io/badge/Anthropic-191919?style=flat&logo=anthropic&logoColor=white" alt="Anthropic" />
<img src="https://img.shields.io/badge/Google_Gemini-4285F4?style=flat&logo=google&logoColor=white" alt="Google Gemini" />
<img src="https://img.shields.io/badge/DeepSeek-566AB2?style=flat" alt="DeepSeek" />
<img src="https://img.shields.io/badge/Azure-0078D4?style=flat&logo=microsoftazure&logoColor=white" alt="Azure" />
<img src="https://img.shields.io/badge/Ollama-000000?style=flat" alt="Ollama" />
<img src="https://img.shields.io/badge/Groq-F05237?style=flat" alt="Groq" />
<img src="https://img.shields.io/badge/Mistral-FF7000?style=flat" alt="Mistral" />
<img src="https://img.shields.io/badge/Cerebras-F05A28?style=flat" alt="Cerebras" />
<img src="https://img.shields.io/badge/Cohere-39594D?style=flat" alt="Cohere" />
<img src="https://img.shields.io/badge/OpenRouter-6467F2?style=flat" alt="OpenRouter" />
<img src="https://img.shields.io/badge/Perplexity-20808D?style=flat" alt="Perplexity" />
<img src="https://img.shields.io/badge/Fireworks-FF6B35?style=flat" alt="Fireworks" />
<img src="https://img.shields.io/badge/AWS_Bedrock-FF9900?style=flat&logo=amazonaws&logoColor=white" alt="AWS Bedrock" />
<img src="https://img.shields.io/badge/xAI_Grok-000000?style=flat" alt="xAI Grok" />
<img src="https://img.shields.io/badge/Vertex_AI-4285F4?style=flat&logo=googlecloud&logoColor=white" alt="Vertex AI" />
<img src="https://img.shields.io/badge/HuggingFace-FFD21E?style=flat&logo=huggingface&logoColor=black" alt="HuggingFace" />
<img src="https://img.shields.io/badge/Together_AI-000000?style=flat" alt="Together AI" />
<img src="https://img.shields.io/badge/Databricks-FF3621?style=flat&logo=databricks&logoColor=white" alt="Databricks" />
<img src="https://img.shields.io/badge/Replicate-262626?style=flat" alt="Replicate" />
<img src="https://img.shields.io/badge/Cloudflare-F38020?style=flat&logo=cloudflare&logoColor=white" alt="Cloudflare" />
</p>

<details>
<summary><strong>查看所有 24 个提供商示例</strong></summary>

| Provider | Example |
|----------|:-------:|
| OpenAI | [Example](examples/python/providers/openai/openai_gpt4_example.py) |
| Anthropic | [Example](examples/python/providers/anthropic/anthropic_claude_example.py) |
| Google Gemini | [Example](examples/python/providers/google/google_gemini_example.py) |
| Ollama | [Example](examples/python/providers/ollama/ollama-agents.py) |
| Groq | [Example](examples/python/providers/groq/kimi_with_groq_example.py) |
| DeepSeek | [Example](examples/python/providers/deepseek/deepseek_example.py) |
| xAI Grok | [Example](examples/python/providers/xai/xai_grok_example.py) |
| Mistral | [Example](examples/python/providers/mistral/mistral_example.py) |
| Cohere | [Example](examples/python/providers/cohere/cohere_example.py) |
| Perplexity | [Example](examples/python/providers/perplexity/perplexity_example.py) |
| Fireworks | [Example](examples/python/providers/fireworks/fireworks_example.py) |
| Together AI | [Example](examples/python/providers/together/together_ai_example.py) |
| OpenRouter | [Example](examples/python/providers/openrouter/openrouter_example.py) |
| HuggingFace | [Example](examples/python/providers/huggingface/huggingface_example.py) |
| Azure OpenAI | [Example](examples/python/providers/azure/azure_openai_example.py) |
| AWS Bedrock | [Example](examples/python/providers/aws/aws_bedrock_example.py) |
| Google Vertex | [Example](examples/python/providers/vertex/vertex_example.py) |
| Databricks | [Example](examples/python/providers/databricks/databricks_example.py) |
| Cloudflare | [Example](examples/python/providers/cloudflare/cloudflare_example.py) |
| AI21 | [Example](examples/python/providers/ai21/ai21_example.py) |
| Replicate | [Example](examples/python/providers/replicate/replicate_example.py) |
| SageMaker | [Example](examples/python/providers/sagemaker/sagemaker_example.py) |
| Moonshot | [Example](examples/python/providers/moonshot/moonshot_example.py) |
| vLLM | [Example](examples/python/providers/vllm/vllm_example.py) |

</details>

<div align="center">
  <a href="https://x.com/elonmusk/status/1893870468249141688" target="_blank">
    <img src=".github/images/elon_musk_praisonai.png" alt="Highlighted by Elon Musk" width="600" />
  </a>
  <p><em>"Grok 3 customer support" — <a href="https://x.com/elonmusk/status/1893870468249141688">Elon Musk quoting PraisonAI's tutorial</a></em></p>
</div>
<br>

---

## 🌟 为什么选择 PraisonAI？

| | 功能特性 | 实现方式 |
|--|---------|-----|
| 🔌 | **MCP 协议** — stdio、HTTP、WebSocket、SSE | `tools=MCP("npx ...")` |
| 🧠 | **规划模式** —— 规划 → 执行 → 推理 | `planning=True` |
| 🔍 | **深度研究** —— 多步自主研究流程 | [文档](https://docs.praison.ai/docs/agents/deep-research) |
| 🤖 | **外部智能体** —— 编排 Claude Code、Gemini CLI、Codex | [文档](https://docs.praison.ai/docs/code/external-agents) |
| 🔄 | **智能体交接** —— 无缝对话传递 | `handoff=True` |
| 🛡️ | **安全护栏（Guardrails）** —— 输入/输出验证 | [文档](https://docs.praison.ai/docs/concepts/guardrails) |
|  | **网页搜索与抓取** —— 原生浏览能力 | `web_search=True` |
| 🪞 | **自我反思** —— 智能体审查自身输出 | [文档](https://docs.praison.ai/docs/concepts/reflection) |
| 🔀 | **工作流模式** —— 路由、并行、循环、重复执行 | [文档](https://docs.praison.ai/docs/concepts/agentflow) |
| 🧠 | **记忆（零依赖）** —— 开箱即用 | `memory=True` |

<details>
<summary><strong>查看所有 25 项功能特性</strong></summary>

| | 功能特性 | 实现方式 |
|--|---------|-----|
| 💡 | **提示词缓存** —— 降低延迟与成本 | `prompt_caching=True` |
| 💾 | **会话与自动保存** —— 重启后状态持久化 | `auto_save="my-project"` |
| 💭 | **思考预算（Thinking Budgets）** —— 控制推理深度 | `thinking_budget=1024` |
| 📚 | **RAG + 质量感知 RAG** —— 自动评分检索 | [文档](https://docs.praison.ai/docs/concepts/rag) |
| 📊 | **模型路由（Model Router）** —— 自动路由至最便宜且可用的模型 | [文档](https://docs.praison.ai/docs/features/model-router) |
| 🧊 | **Shadow Git 检查点** —— 失败时自动回滚 | [文档](https://docs.praison.ai/docs/features/checkpoints) |
| 📡 | **A2A 协议** —— 智能体间互操作 | [文档](https://docs.praison.ai/docs/features/a2a) |
| 📏 | **上下文压缩（Context Compaction）** —— 永不触发 Token 限制 | [文档](https://docs.praison.ai/docs/features/context-compaction) |
| 📡 | **遥测（Telemetry）** —— OpenTelemetry 追踪、跨度与指标 | [文档](https://docs.praison.ai/docs/features/telemetry) |
| 📜 | **策略引擎** —— 声明式智能体行为控制 | [文档](https://docs.praison.ai/docs/features/policy-engine) |
| 🔄 | **后台任务** —— 异步触发执行 | [文档](https://docs.praison.ai/docs/features/background-tasks) |
| 🔁 | **死循环检测（Doom Loop Detection）** —— 自动恢复卡死的智能体 | [文档](https://docs.praison.ai/docs/features/doom-loop-detection) |
| 🕸️ | **图记忆** —— Neo4j 风格的关联追踪 | [文档](https://docs.praison.ai/docs/features/graph-memory) |
| 🏖️ | **沙箱执行** —— 隔离代码运行环境 | [文档](https://docs.praison.ai/docs/features/sandbox) |
| 🖥️ | **Bot Gateway** —— 跨渠道多智能体路由 | [文档](https://docs.praison.ai/docs/features/bot-gateway) |

</details>




---

## 📘 Python 代码使用示例

### 1. 单个智能体

```python
from praisonaiagents import Agent
agent = Agent(instructions="You are a helpful AI assistant")
agent.start("Write a movie script about a robot in Mars")
```

### 2. 多智能体协作

```python
from praisonaiagents import Agent, Agents

research_agent = Agent(instructions="Research about AI")
summarise_agent = Agent(instructions="Summarise research agent's findings")
agents = Agents(agents=[research_agent, summarise_agent])
agents.start()
```

### 3. MCP（模型上下文协议）

```python
from praisonaiagents import Agent, MCP

# stdio - Local NPX/Python servers
agent = Agent(tools=MCP("npx @modelcontextprotocol/server-memory"))

# Streamable HTTP - Production servers
agent = Agent(tools=MCP("https://api.example.com/mcp"))

# WebSocket - Real-time bidirectional
agent = Agent(tools=MCP("wss://api.example.com/mcp", auth_token="token"))

# With environment variables
agent = Agent(
    tools=MCP(
        command="npx",
        args=["-y", "@modelcontextprotocol/server-brave-search"],
        env={"BRAVE_API_KEY": "your-key"}
    )
)
```

> 📖 [完整 MCP 文档](https://docs.praison.ai/docs/mcp/transports) —— stdio、HTTP、WebSocket、SSE 传输协议

### 4. 自定义工具

```python
from praisonaiagents import Agent, tool

@tool
def search(query: str) -> str:
    """Search the web for information."""
    return f"Results for: {query}"

@tool
def calculate(expression: str) -> float:
    """Safely evaluate a numeric arithmetic expression."""
    import ast
    import operator
    
    # Define allowed operations
    _OPS = {
        ast.Add: operator.add,
        ast.Sub: operator.sub,
        ast.Mult: operator.mul,
        ast.Div: operator.truediv,
        ast.Pow: operator.pow,
        ast.USub: operator.neg,
        ast.UAdd: operator.pos,
    }
    
    def _safe_eval(node):
        if isinstance(node, ast.Constant) and isinstance(node.value, (int, float)):
            return node.value
        elif isinstance(node, ast.BinOp) and type(node.op) in _OPS:
            return _OPS[type(node.op)](_safe_eval(node.left), _safe_eval(node.right))
        elif isinstance(node, ast.UnaryOp) and type(node.op) in _OPS:
            return _OPS[type(node.op)](_safe_eval(node.operand))
        else:
            raise ValueError("Unsupported expression")
    
    try:
        return _safe_eval(ast.parse(expression, mode="eval").body)
    except (ValueError, SyntaxError, TypeError, ZeroDivisionError, OverflowError):
        raise ValueError("Invalid arithmetic expression")

agent = Agent(
    instructions="You are a helpful assistant",
    tools=[search, calculate]
)
agent.start("Search for AI news and calculate 15*4")
```

> ⚠️ **安全提示：** 切勿在接收 LLM 生成内容或用户输入的工具函数中使用 `eval()`、`exec()` 或 `subprocess`。务必对输入进行验证和清理，以防止代码注入攻击。
> 📖 [完整工具文档](https://docs.praison.ai/docs/tools/tools) —— BaseTool、工具包及内置 100+ 工具

### 5. 持久化（数据库）

```python
from praisonaiagents import Agent, db

agent = Agent(
    name="Assistant",
    db=db(database_url="postgresql://localhost/mydb"),
    session_id="my-session"
)
agent.chat("Hello!")  # Auto-persists messages, runs, traces
```

> 📖 [完整持久化文档](https://docs.praison.ai/docs/databases/overview) —— PostgreSQL、MySQL、SQLite、MongoDB、Redis 及 20+ 其他数据库支持

### 6. PraisonAI Claw 🦞（仪表盘界面）

将你的 AI 智能体接入 **Telegram、Discord、Slack、WhatsApp** 等平台——仅需一条命令。

```bash
pip install "praisonai[claw]"
praisonai claw
```

#### 所需环境变量

复制 `.env.example` 至 `.env` 并配置以下变量：

| 变量 | 是否必需 | 描述 |
|----------|----------|-------------|
| `OPENAI_API_KEY` | 是 | 所有大语言模型调用的 OpenAI API 密钥 |
| `TAVILY_API_KEY` | 是（Claw） | 内置网页搜索工具的 Tavily 密钥。可在 https://app.tavily.com 免费获取 |

打开 **http://localhost:8082** —— 仪表盘自带 13 个内置页面：聊天、智能体、记忆、知识库、渠道、安全护栏、定时任务等。可直接在 UI 中添加消息渠道。

> 📖 [完整 Claw 文档](https://docs.praison.ai/docs/concepts/claw) —— 平台令牌、CLI 选项、Docker 及 YAML 智能体模式

### 7. Langflow 集成 🔗（可视化工作流构建器）

在 Langflow 中使用 **拖拽组件** 直观构建多智能体工作流。

```bash
pip install "praisonai[flow]"
praisonai flow
```

打开 **http://localhost:7861** —— 使用 **Agent** 和 **Agent Team** 组件创建顺序或并行工作流。连接 Chat Input → Agent Team → Chat Output 即可快速搭建多智能体流水线。

> 📖 [完整 Flow 文档](https://docs.praison.ai/docs/concepts/agentflow) —— 可视化构建、组件参考与部署指南

### 8. PraisonAI UI 🤖（简洁聊天界面）

专为 AI 智能体打造的轻量级聊天界面。

```bash
pip install "praisonai[ui]"
praisonai ui
```

---

## 📄 YAML 使用示例（无需编写代码）

### 示例 1：两个智能体协作

创建 `agents.yaml`：

```yaml
framework: praisonai
topic: "Write a blog post about AI"

agents:
  researcher:
    role: Research Analyst
    goal: Research AI trends and gather information
    instructions: "Find accurate information about AI trends"
    
  writer:
    role: Content Writer
    goal: Write engaging blog posts
    instructions: "Write clear, engaging content based on research"
```

运行：
```bash
praisonai agents.yaml
```

> 智能体会自动按顺序协作完成工作

### 示例 2：带自定义工具的智能体

在同一文件夹下创建两个文件：

**agents.yaml:**
```yaml
framework: praisonai
topic: "Calculate the sum of 25 and 15"

agents:
  calculator_agent:
    role: Calculator
    goal: Perform calculations
    instructions: "Use the add_numbers tool to help with calculations"
    tools:
      - add_numbers
```

**tools.py:**
```python
def add_numbers(a: float, b: float) -> float:
    """
    Add two numbers together.
    
    Args:
        a: First number
        b: Second number
    
    Returns:
        The sum of a and b
    """
    return a + b
```

运行：
```bash
praisonai agents.yaml
```

> 💡 **提示：** 
> - 在 `tools` 列表中使用函数名（例如 `add_numbers`），而非文件名
> - `tools.py` 中的工具会自动被发现
> - 函数的文档字符串有助于 AI 理解如何调用它

---

## 🎯 CLI 快速参考

| 类别 | 命令 |
|----------|----------|
| **执行** | `praisonai`, `--auto`, `--interactive`, `--chat` |
| **研究** | `research`, `--query-rewrite`, `--deep-research` |
| **规划** | `--planning`, `--planning-tools`, `--planning-reasoning` |
| **工作流** | `workflow run`, `workflow list`, `workflow auto` |
| **记忆** | `memory show`, `memory add`, `memory search`, `memory clear` |
| **知识库** | `knowledge add`, `knowledge query`, `knowledge list` |
| **会话** | `session list`, `session resume`, `session delete` |
| **工具** | `tools list`, `tools info`, `tools search` |
| **MCP** | `mcp list`, `mcp create`, `mcp enable` |
| **开发** | `commit`, `docs`, `checkpoint`, `hooks` |
| **定时任务** | `schedule start`, `schedule list`, `schedule stop` |

> 📖 [完整 CLI 参考](https://docs.praison.ai/docs/cli/cli-reference)

---

## ✨ 核心功能特性

<details open>
<summary><strong>🤖 核心智能体</strong></summary>

| Feature | Code | Docs |
|---------|:----:|:----:|
| Single Agent | [Example](examples/python/agents/single-agent.py) | [📖](https://docs.praison.ai/docs/agents/single) |
| Multi Agents | [Example](examples/python/general/mini_agents_example.py) | [📖](https://docs.praison.ai/docs/concepts/agents) |
| Auto Agents | [Example](examples/python/general/auto_agents_example.py) | [📖](https://docs.praison.ai/docs/features/autoagents) |
| Self Reflection AI Agents | [Example](examples/python/concepts/self-reflection-details.py) | [📖](https://docs.praison.ai/docs/concepts/reflection) |
| Reasoning AI Agents | [Example](examples/python/concepts/reasoning-extraction.py) | [📖](https://docs.praison.ai/docs/features/reasoning) |
| Multi Modal AI Agents | [Example](examples/python/general/multimodal.py) | [📖](https://docs.praison.ai/docs/features/multimodal) |

</details>

<details>
<summary><strong>🔄 工作流（Workflows）</strong></summary>

| Feature | Code | Docs |
|---------|:----:|:----:|
| Simple Workflow | [Example](examples/python/workflows/simple_workflow.py) | [📖](https://docs.praison.ai/docs/concepts/agentflow) |
| Workflow with Agents | [Example](examples/python/workflows/workflow_with_agents.py) | [📖](https://docs.praison.ai/docs/concepts/agentflow) |
| Agentic Routing (`route()`) | [Example](examples/python/workflows/workflow_routing.py) | [📖](https://docs.praison.ai/docs/features/routing) |
| Parallel Execution (`parallel()`) | [Example](examples/python/workflows/workflow_parallel.py) | [📖](https://docs.praison.ai/docs/features/parallelisation) |
| Loop over List/CSV (`loop()`) | [Example](examples/python/workflows/workflow_loop_csv.py) | [📖](https://docs.praison.ai/docs/features/repetitive) |
| Evaluator-Optimizer (`repeat()`) | [Example](examples/python/workflows/workflow_repeat.py) | [📖](https://docs.praison.ai/docs/concepts/evaluation) |
| Conditional Steps | [Example](examples/python/workflows/workflow_conditional.py) | [📖](https://docs.praison.ai/docs/concepts/agentflow) |
| Workflow Branching | [Example](examples/python/workflows/workflow_branching.py) | [📖](https://docs.praison.ai/docs/concepts/agentflow) |
| Workflow Early Stop | [Example](examples/python/workflows/workflow_early_stop.py) | [📖](https://docs.praison.ai/docs/concepts/agentflow) |
| Workflow Checkpoints | [Example](examples/python/workflows/workflow_checkpoints.py) | [📖](https://docs.praison.ai/docs/concepts/agentflow) |

</details>

<details>
<summary><strong>💻 代码与开发</strong></summary>

| Feature | Code | Docs |
|---------|:----:|:----:|
| Code Interpreter Agents | [Example](examples/python/agents/code-agent.py) | [📖](https://docs.praison.ai/docs/features/codeagent) |
| AI Code Editing Tools | [Example](examples/python/code/code_editing_example.py) | [📖](https://docs.praison.ai/docs/code/editing) |
| External Agents (All) | [Example](examples/python/code/external_agents_example.py) | [📖](https://docs.praison.ai/docs/code/external-agents) |
| Claude Code CLI | [Example](examples/python/code/claude_code_example.py) | [📖](https://docs.praison.ai/docs/code/claude-code) |
| Gemini CLI | [Example](examples/python/code/gemini_cli_example.py) | [📖](https://docs.praison.ai/docs/code/gemini-cli) |
| Codex CLI | [Example](examples/python/code/codex_cli_example.py) | [📖](https://docs.praison.ai/docs/code/codex-cli) |
| Cursor CLI | [Example](examples/python/code/cursor_cli_example.py) | [📖](https://docs.praison.ai/docs/code/cursor-cli) |

</details>

<details>
<summary><strong>🧠 记忆与知识库</strong></summary>

| Feature | Code | Docs |
|---------|:----:|:----:|
| Memory (Short & Long Term) | [Example](examples/python/general/memory_example.py) | [📖](https://docs.praison.ai/docs/concepts/memory) |
| File-Based Memory | [Example](examples/python/general/memory_example.py) | [📖](https://docs.praison.ai/docs/concepts/memory) |
| Claude Memory Tool | [Example](examples/python/memory/claude_memory_example.py) | [📖](https://docs.praison.ai/docs/features/claude-memory-tool) |
| Add Custom Knowledge | [Example](examples/python/concepts/knowledge-agents.py) | [📖](https://docs.praison.ai/docs/concepts/knowledge) |
| RAG Agents | [Example](examples/python/concepts/rag-agents.py) | [📖](https://docs.praison.ai/docs/concepts/rag) |
| Chat with PDF Agents | [Example](examples/python/concepts/chat-with-pdf.py) | [📖](https://docs.praison.ai/docs/features/chat-with-pdf) |
| Data Readers (PDF, DOCX, etc.) | [CLI](https://docs.praison.ai/docs/cli/knowledge) | [📖](https://docs.praison.ai/docs/features/chunking-strategies) |
| Vector Store Selection | [CLI](https://docs.praison.ai/docs/cli/knowledge) | [📖](https://docs.praison.ai/docs/features/knowledge-backends) |
| Retrieval Strategies | [CLI](https://docs.praison.ai/docs/cli/knowledge) | [📖](https://docs.praison.ai/docs/features/retrieval-strategies) |
| Rerankers | [CLI](https://docs.praison.ai/docs/cli/knowledge) | [📖](https://docs.praison.ai/docs/features/smart-retrieval) |
| Index Types (Vector/Keyword/Hybrid) | [CLI](https://docs.praison.ai/docs/cli/knowledge) | [📖](https://docs.praison.ai/docs/features/incremental-indexing) |
| Query Engines (Sub-Question, etc.) | [CLI](https://docs.praison.ai/docs/cli/knowledge) | [📖](https://docs.praison.ai/docs/features/retrieval) |

</details>

<details>
<summary><strong>🔬 研究与智能分析</strong></summary>

| Feature | Code | Docs |
|---------|:----:|:----:|
| Deep Research Agents | [Example](examples/python/agents/research-agent.py) | [📖](https://docs.praison.ai/docs/agents/deep-research) |
| Query Rewriter Agent | [Example](examples/python/agents/query-rewriter-agent.py) | [📖](https://docs.praison.ai/docs/agents/query-rewriter) |
| Native Web Search | [Example](examples/python/agents/websearch-agent.py) | [📖](https://docs.praison.ai/docs/agents/websearch) |
| Built-in Search Tools | [Example](examples/python/agents/websearch-agent.py) | [📖](https://docs.praison.ai/docs/tools/tavily) |
| Unified Web Search | [Example](src/praisonai-agents/examples/web_search_example.py) | [📖](https://docs.praison.ai/docs/tools/web-search) |
| Web Fetch (Anthropic) | [Example](examples/python/agents/web-fetch-agent.py) | [📖](https://docs.praison.ai/docs/features/model-capabilities) |

</details>

<details>
<summary><strong>📋 规划与执行</strong></summary>

| Feature | Code | Docs |
|---------|:----:|:----:|
| Planning Mode | [Example](examples/python/agents/planning-agent.py) | [📖](https://docs.praison.ai/docs/concepts/planning) |
| Planning Tools | [Example](examples/python/agents/planning-agent.py) | [📖](https://docs.praison.ai/docs/concepts/planning) |
| Planning Reasoning | [Example](examples/python/agents/planning-agent.py) | [📖](https://docs.praison.ai/docs/concepts/planning) |
| Prompt Chaining | [Example](examples/python/general/prompt_chaining.py) | [📖](https://docs.praison.ai/docs/features/promptchaining) |
| Evaluator Optimiser | [Example](examples/python/general/evaluator-optimiser.py) | [📖](https://docs.praison.ai/docs/concepts/evaluation) |
| Orchestrator Workers | [Example](examples/python/general/orchestrator-workers.py) | [📖](https://docs.praison.ai/docs/concepts/orchestration) |

</details>

<details>
<summary><strong>👥 专用智能体</strong></summary>

| Feature | Code | Docs |
|---------|:----:|:----:|
| Data Analyst Agent | [Example](examples/python/agents/data-analyst-agent.py) | [📖](https://docs.praison.ai/docs/agents/data-analyst) |
| Finance Agent | [Example](examples/python/agents/finance-agent.py) | [📖](https://docs.praison.ai/docs/agents/finance) |
| Shopping Agent | [Example](examples/python/agents/shopping-agent.py) | [📖](https://docs.praison.ai/docs/agents/shopping) |
| Recommendation Agent | [Example](examples/python/agents/recommendation-agent.py) | [📖](https://docs.praison.ai/docs/agents/recommendation) |
| Wikipedia Agent | [Example](examples/python/agents/wikipedia-agent.py) | [📖](https://docs.praison.ai/docs/agents/wikipedia) |
| Programming Agent | [Example](examples/python/agents/programming-agent.py) | [📖](https://docs.praison.ai/docs/agents/programming) |
| Math Agents | [Example](examples/python/agents/math-agent.py) | [📖](https://docs.praison.ai/docs/features/mathagent) |
| Markdown Agent | [Example](examples/python/agents/markdown-agent.py) | [📖](https://docs.praison.ai/docs/agents/markdown) |
| Prompt Expander Agent | [Example](examples/python/agents/prompt-expander-agent.py) | [📖](https://docs.praison.ai/docs/agents/prompt-expander) |

</details>

<details>
<summary><strong>🎨 媒体与多模态</strong></summary>

| Feature | Code | Docs |
|---------|:----:|:----:|
| Image Generation Agent | [Example](examples/python/image/image-agent.py) | [📖](https://docs.praison.ai/docs/features/image-generation) |
| Image to Text Agent | [Example](examples/python/agents/image-to-text-agent.py) | [📖](https://docs.praison.ai/docs/agents/image-to-text) |
| Video Agent | [Example](examples/python/agents/video-agent.py) | [📖](https://docs.praison.ai/docs/agents/video) |
| Camera Integration | [Example](examples/python/camera/) | [📖](https://docs.praison.ai/docs/features/camera-integration) |

</details>

<details>
<summary><strong>🔌 协议与集成</strong></summary>

| Feature | Code | Docs |
|---------|:----:|:----:|
| MCP Transports | [Example](examples/python/mcp/mcp-transports-overview.py) | [📖](https://docs.praison.ai/docs/mcp/transports) |
| WebSocket MCP | [Example](examples/python/mcp/websocket-mcp.py) | [📖](https://docs.praison.ai/docs/mcp/sse-transport) |
| MCP Security | [Example](examples/python/mcp/mcp-security.py) | [📖](https://docs.praison.ai/docs/mcp/transports) |
| MCP Resumability | [Example](examples/python/mcp/mcp-resumability.py) | [📖](https://docs.praison.ai/docs/mcp/sse-transport) |
| MCP Config Management | [Docs](https://docs.praison.ai/docs/cli/mcp) | [📖](https://docs.praison.ai/docs/cli/mcp) |
| LangChain Integrated Agents | [Example](examples/python/general/langchain_example.py) | [📖](https://docs.praison.ai/docs/features/langchain) |

</details>

<details>
<summary><strong>🛡️ 安全与控制</strong></summary>

| Feature | Code | Docs |
|---------|:----:|:----:|
| Guardrails | [Example](examples/python/guardrails/comprehensive-guardrails-example.py) | [📖](https://docs.praison.ai/docs/concepts/guardrails) |
| Human Approval | [Example](examples/python/general/human_approval_example.py) | [📖](https://docs.praison.ai/docs/concepts/approval) |
| Rules & Instructions | [Docs](https://docs.praison.ai/docs/features/rules) | [📖](https://docs.praison.ai/docs/features/rules) |

</details>

<details>
<summary><strong>⚙️ 高级功能特性</strong></summary>

| Feature | Code | Docs |
|---------|:----:|:----:|
| Async & Parallel Processing | [Example](examples/python/general/async_example.py) | [📖](https://docs.praison.ai/docs/features/async) |
| Parallelisation | [Example](examples/python/general/parallelisation.py) | [📖](https://docs.praison.ai/docs/features/parallelisation) |
| Repetitive Agents | [Example](examples/python/concepts/repetitive-agents.py) | [📖](https://docs.praison.ai/docs/features/repetitive) |
| Agent Handoffs | [Example](examples/python/handoff/handoff_basic.py) | [📖](https://docs.praison.ai/docs/concepts/handoffs) |
| Stateful Agents | [Example](examples/python/stateful/workflow-state-example.py) | [📖](https://docs.praison.ai/docs/features/stateful-agents) |
| Autonomous Workflow | [Example](examples/python/general/autonomous-agent.py) | [📖](https://docs.praison.ai/docs/concepts/autonomy) |
| Structured Output Agents | [Example](examples/python/general/structured_agents_example.py) | [📖](https://docs.praison.ai/docs/features/structured) |
| Model Router | [Example](examples/python/agents/router-agent-cost-optimization.py) | [📖](https://docs.praison.ai/docs/features/model-router) |
| Prompt Caching | [Example](examples/python/agents/prompt-caching-agent.py) | [📖](https://docs.praison.ai/docs/features/model-capabilities) |
| Fast Context | [Example](examples/context/00_agent_fast_context_basic.py) | [📖](https://docs.praison.ai/docs/features/fast-context) |

</details>

<details>
<summary><strong>🛠️ 工具与配置</strong></summary>

| Feature | Code | Docs |
|---------|:----:|:----:|
| 100+ Custom Tools | [Example](examples/python/general/tools_example.py) | [📖](https://docs.praison.ai/docs/tools/tools) |
| YAML Configuration | [Example](examples/cookbooks/yaml/secondary_market_research_agents.yaml) | [📖](https://docs.praison.ai/docs/developers/agents-playbook) |
| 100+ LLM Support | [Example](examples/python/providers/openai/openai_gpt4_example.py) | [📖](https://docs.praison.ai/docs/models) |
| Callback Agents | [Example](examples/python/general/advanced-callback-systems.py) | [📖](https://docs.praison.ai/docs/concepts/hooks) |
| Hooks | [Example](examples/python/hooks/hooks_example.py) | [📖](https://docs.praison.ai/docs/concepts/hooks) |
| Middleware System | [Example](examples/middleware/basic_middleware.py) | [📖](https://docs.praison.ai/docs/features/middleware) |
| Configurable Model | [Example](examples/middleware/configurable_model.py) | [📖](https://docs.praison.ai/docs/features/configurable-model) |
| Rate Limiter | [Example](examples/middleware/rate_limiter.py) | [📖](https://docs.praison.ai/docs/features/rate-limiter) |
| Injected Tool State | [Example](examples/middleware/injected_state.py) | [📖](https://docs.praison.ai/docs/features/injected-state) |
| Shadow Git Checkpoints | [Example](examples/checkpoints/basic_checkpoint.py) | [📖](https://docs.praison.ai/docs/features/checkpoints) |
| Background Tasks | [Example](examples/background/basic_background.py) | [📖](https://docs.praison.ai/docs/features/background-tasks) |
| Policy Engine | [Example](examples/policy/basic_policy.py) | [📖](https://docs.praison.ai/docs/features/policy-engine) |
| Thinking Budgets | [Example](examples/thinking/basic_thinking.py) | [📖](https://docs.praison.ai/docs/features/thinking-budgets) |
| Output Styles | [Example](examples/output/basic_output.py) | [📖](https://docs.praison.ai/docs/features/output-styles) |
| Context Compaction | [Example](examples/compaction/basic_compaction.py) | [📖](https://docs.praison.ai/docs/features/context-compaction) |

</details>

<details>
<summary><strong>📊 监控与管理</strong></summary>

| Feature | Code | Docs |
|---------|:----:|:----:|
| Sessions Management | [Example](examples/python/sessions/comprehensive-session-management.py) | [📖](https://docs.praison.ai/docs/concepts/session-management) |
| Auto-Save Sessions | [Docs](https://docs.praison.ai/docs/cli/session) | [📖](https://docs.praison.ai/docs/cli/session) |
| History in Context | [Docs](https://docs.praison.ai/docs/cli/session) | [📖](https://docs.praison.ai/docs/cli/session) |
| Telemetry | [Example](examples/python/telemetry/production-telemetry-example.py) | [📖](https://docs.praison.ai/docs/features/telemetry) |
| Langfuse Tracing | [Docs](https://docs.praison.ai/docs/observability/langfuse) | [📖](https://docs.praison.ai/docs/observability/langfuse) |
| Project Docs (.praison/docs/) | [Docs](https://docs.praison.ai/docs/cli/docs) | [📖](https://docs.praison.ai/docs/cli/docs) |
| AI Commit Messages | [Docs](https://docs.praison.ai/docs/cli/commit) | [📖](https://docs.praison.ai/docs/cli/commit) |
| @Mentions in Prompts | [Docs](https://docs.praison.ai/docs/cli/mentions) | [📖](https://docs.praison.ai/docs/cli/mentions) |

</details>

<details>
<summary><strong>🖥️ CLI 功能特性</strong></summary>

| Feature | Code | Docs |
|---------|:----:|:----:|
| Slash Commands | [Example](examples/python/cli/slash_commands_example.py) | [📖](https://docs.praison.ai/docs/cli/slash-commands) |
| Autonomy Modes | [Example](examples/python/cli/autonomy_modes_example.py) | [📖](https://docs.praison.ai/docs/cli/autonomy-modes) |
| Cost Tracking | [Example](examples/python/cli/cost_tracking_example.py) | [📖](https://docs.praison.ai/docs/cli/cost-tracking) |
| Repository Map | [Example](examples/python/cli/repo_map_example.py) | [📖](https://docs.praison.ai/docs/cli/repo-map) |
| Interactive TUI | [Example](examples/python/cli/interactive_tui_example.py) | [📖](https://docs.praison.ai/docs/cli/interactive-tui) |
| Git Integration | [Example](examples/python/cli/git_integration_example.py) | [📖](https://docs.praison.ai/docs/cli/git-integration) |
| Sandbox Execution | [Example](examples/python/cli/sandbox_execution_example.py) | [📖](https://docs.praison.ai/docs/cli/sandbox-execution) |
| CLI Compare | [Example](examples/compare/cli_compare_basic.py) | [📖](https://docs.praison.ai/docs/cli/compare) |
| Profile/Benchmark | [Docs](https://docs.praison.ai/docs/cli/profile) | [📖](https://docs.praison.ai/docs/cli/profile) |
| Auto Mode | [Docs](https://docs.praison.ai/docs/cli/auto) | [📖](https://docs.praison.ai/docs/cli/auto) |
| Init | [Docs](https://docs.praison.ai/docs/cli/init) | [📖](https://docs.praison.ai/docs/cli/init) |
| File Input | [Docs](https://docs.praison.ai/docs/cli/file-input) | [📖](https://docs.praison.ai/docs/cli/file-input) |
| Final Agent | [Docs](https://docs.praison.ai/docs/cli/final-agent) | [📖](https://docs.praison.ai/docs/cli/final-agent) |
| Max Tokens | [Docs](https://docs.praison.ai/docs/cli/max-tokens) | [📖](https://docs.praison.ai/docs/cli/max-tokens) |

</details>

<details>
<summary><strong>🧪 评估（Evaluation）</strong></summary>

| Feature | Code | Docs |
|---------|:----:|:----:|
| Accuracy Evaluation | [Example](examples/eval/accuracy_example.py) | [📖](https://docs.praison.ai/docs/cli/eval) |
| Performance Evaluation | [Example](examples/eval/performance_example.py) | [📖](https://docs.praison.ai/docs/cli/eval) |
| Reliability Evaluation | [Example](examples/eval/reliability_example.py) | [📖](https://docs.praison.ai/docs/cli/eval) |
| Criteria Evaluation | [Example](examples/eval/criteria_example.py) | [📖](https://docs.praison.ai/docs/cli/eval) |

</details>

<details>
<summary><strong>🎯 智能体技能（Agent Skills）</strong></summary>

| Feature | Code | Docs |
|---------|:----:|:----:|
| Skills Management | [Example](examples/skills/basic_skill_usage.py) | [📖](https://docs.praison.ai/docs/concepts/skills) |
| Custom Skills | [Example](examples/skills/custom_skill_example.py) | [📖](https://docs.praison.ai/docs/concepts/skills) |

</details>

<details>
<summary><strong>⏰ 24/7 定时调度</strong></summary>

| Feature | Code | Docs |
|---------|:----:|:----:|
| Agent Scheduler | [Example](examples/python/scheduled_agents/news_checker_live.py) | [📖](https://docs.praison.ai/docs/cli/scheduler) |

</details>

---

## 💻 JavaScript 代码使用示例

```bash
npm install praisonai
export OPENAI_API_KEY=xxxxxxxxxxxxxxxxxxxxxx
```

```javascript
const { Agent } = require('praisonai');
const agent = new Agent({ instructions: 'You are a helpful AI assistant' });
agent.start('Write a movie script about a robot in Mars');
```

---

## ⚡ 性能表现

PraisonAI 专为速度而生，智能体实例化时间低于 4μs。这降低了系统开销，提升了响应速度，并帮助多智能体系统在真实生产负载中高效扩展。

| Performance Metric | PraisonAI |
|--------------------|-----------|
| Avg Instantiation Time | **3.77 μs** |

---



---

## ⭐ Star 历史

[![Star History Chart](https://api.star-history.com/svg?repos=MervinPraison/PraisonAI&type=Date)](https://docs.praison.ai)

---

## 🔍 Langfuse 追踪（Tracing）

```bash
pip install "praisonai[langfuse]"
praisonai langfuse
```

<p align="center">
  <img src=".github/images/langfuse.png" alt="PraisonAI Langfuse Tracing" width="800" />
</p>

---

## 🎓 视频教程

通过我们的系列视频学习 PraisonAI：

<details>
<summary><strong>查看所有 22 个视频教程</strong></summary>

| Topic | Video |
|-------|--------|
| AI Agents with Self Reflection | [![Self Reflection](https://img.youtube.com/vi/vLXobEN2Vc8/0.jpg)](https://www.youtube.com/watch?v=vLXobEN2Vc8) |
| Reasoning Data Generating Agent | [![Reasoning Data](https://img.youtube.com/vi/fUT332Y2zA8/0.jpg)](https://www.youtube.com/watch?v=fUT332Y2zA8) |
| AI Agents with Reasoning | [![Reasoning](https://img.youtube.com/vi/KNDVWGN3TpM/0.jpg)](https://www.youtube.com/watch?v=KNDVWGN3TpM) |
| Multimodal AI Agents | [![Multimodal](https://img.youtube.com/vi/hjAWmUT1qqY/0.jpg)](https://www.youtube.com/watch?v=hjAWmUT1qqY) |
| AI Agents Workflow | [![Workflow](https://img.youtube.com/vi/yWTH44QPl2A/0.jpg)](https://www.youtube.com/watch?v=yWTH44QPl2A) |
| Async AI Agents | [![Async](https://img.youtube.com/vi/VhVQfgo00LE/0.jpg)](https://www.youtube.com/watch?v=VhVQfgo00LE) |
| Mini AI Agents | [![Mini](https://img.youtube.com/vi/OkvYp5aAGSg/0.jpg)](https://www.youtube.com/watch?v=OkvYp5aAGSg) |
| AI Agents with Memory | [![Memory](https://img.youtube.com/vi/1hVfVxvPnnQ/0.jpg)](https://www.youtube.com/watch?v=1hVfVxvPnnQ) |
| Repetitive Agents | [![Repetitive](https://img.youtube.com/vi/dAYGxsjDOPg/0.jpg)](https://www.youtube.com/watch?v=dAYGxsjDOPg) |
| Introduction | [![Introduction](https://img.youtube.com/vi/Fn1lQjC0GO0/0.jpg)](https://www.youtube.com/watch?v=Fn1lQjC0GO0) |
| Tools Overview | [![Tools Overview](https://img.youtube.com/vi/XaQRgRpV7jo/0.jpg)](https://www.youtube.com/watch?v=XaQRgRpV7jo) |
| Custom Tools | [![Custom Tools](https://img.youtube.com/vi/JSU2Rndh06c/0.jpg)](https://www.youtube.com/watch?v=JSU2Rndh06c) |
| Firecrawl Integration | [![Firecrawl](https://img.youtube.com/vi/UoqUDcLcOYo/0.jpg)](https://www.youtube.com/watch?v=UoqUDcLcOYo) |
| User Interface | [![UI](https://img.youtube.com/vi/tg-ZjNl3OCg/0.jpg)](https://www.youtube.com/watch?v=tg-ZjNl3OCg) |
| Crawl4AI Integration | [![Crawl4AI](https://img.youtube.com/vi/KAvuVUh0XU8/0.jpg)](https://www.youtube.com/watch?v=KAvuVUh0XU8) |
| Chat Interface | [![Chat](https://img.youtube.com/vi/sw3uDqn2h1Y/0.jpg)](https://www.youtube.com/watch?v=sw3uDqn2h1Y) |
| Code Interface | [![Code](https://img.youtube.com/vi/_5jQayO-MQY/0.jpg)](https://www.youtube.com/watch?v=_5jQayO-MQY) |
| Mem0 Integration | [![Mem0](https://img.youtube.com/vi/KIGSgRxf1cY/0.jpg)](https://www.youtube.com/watch?v=KIGSgRxf1cY) |
| Training | [![Training](https://img.youtube.com/vi/aLawE8kwCrI/0.jpg)](https://www.youtube.com/watch?v=aLawE8kwCrI) |
| Realtime Voice Interface | [![Realtime](https://img.youtube.com/vi/frRHfevTCSw/0.jpg)](https://www.youtube.com/watch?v=frRHfevTCSw) |
| Call Interface | [![Call](https://img.youtube.com/vi/m1cwrUG2iAk/0.jpg)](https://www.youtube.com/watch?v=m1cwrUG2iAk) |
| Reasoning Extract Agents | [![Reasoning Extract](https://img.youtube.com/vi/2PPamsADjJA/0.jpg)](https://www.youtube.com/watch?v=2PPamsADjJA) |

</details>

---

## 👥 参与贡献

我们欢迎你的贡献！请 Fork 仓库，创建分支并提交 PR → [贡献指南](https://github.com/MervinPraison/PraisonAI/blob/main/CONTRIBUTING.md)。

---

## ❓ 常见问题与故障排除（FAQ）

<details>
<summary><strong>ModuleNotFoundError: No module named 'praisonaiagents'</strong></summary>

安装对应包：
```bash
pip install praisonaiagents
```

</details>

<details>
<summary><strong>API key not found / Authentication error（未找到 API 密钥/认证失败）</strong></summary>

请确保已设置你的 API 密钥：
```bash
export OPENAI_API_KEY=your_key_here
```

其他提供商请参考 [模型文档](https://docs.praison.ai/docs/models)。

</details>

<details>
<summary><strong>如何本地运行模型（Ollama）？</strong></summary>

```bash
# 先启动 Ollama 服务
ollama serve

# 设置环境变量
export OPENAI_BASE_URL=http://localhost:11434/v1
```

更多细节请查看 [模型文档](https://docs.praison.ai/docs/models)。

</details>

<details>
<summary><strong>如何将对话持久化到数据库？</strong></summary>

使用 `db` 参数：
```python
from praisonaiagents import Agent, db

agent = Agent(
    name="Assistant",
    db=db(database_url="postgresql://localhost/mydb"),
    session_id="my-session"
)
```

支持的数据库请参考 [持久化文档](https://docs.praison.ai/docs/databases/overview)。

</details>

<details>
<summary><strong>如何启用智能体记忆？</strong></summary>

```python
from praisonaiagents import Agent

agent = Agent(
    name="Assistant",
    memory=True,  # Enables file-based memory (no extra deps!)
    user_id="user123"
)
```

更多选项请参考 [记忆文档](https://docs.praison.ai/docs/concepts/memory)。

</details>

<details>
<summary><strong>如何同时运行多个智能体？</strong></summary>

```python
from praisonaiagents import Agent, Agents

agent1 = Agent(instructions="Research topics")
agent2 = Agent(instructions="Summarize findings")
agents = Agents(agents=[agent1, agent2])
agents.start()
```

更多示例请参考 [智能体文档](https://docs.praison.ai/docs/concepts/agents)。

</details>

<details>
<summary><strong>如何使用 MCP 工具？</strong></summary>

```python
from praisonaiagents import Agent, MCP

agent = Agent(
    tools=MCP("npx @modelcontextprotocol/server-memory")
)
```

所有传输协议选项请参考 [MCP 文档](https://docs.praison.ai/docs/mcp/transports)。

</details>

### 获取帮助

- 📚 [完整文档](https://docs.praison.ai)
- 🐛 [报告问题](https://github.com/MervinPraison/PraisonAI/issues)
- 💬 [讨论区](https://github.com/MervinPraison/PraisonAI/discussions)

---

<div align="center">
  <p><strong>由 PraisonAI 团队 ❤️ 打造</strong></p>
  <p>
    <a href="https://docs.praison.ai">📚 文档</a> •
    <a href="https://github.com/MervinPraison/PraisonAI">GitHub</a> •
    <a href="https://youtube.com/@MervinPraison">▶️ YouTube</a> •
    <a href="https://x.com/MervinPraison">𝕏 X</a> •
    <a href="https://linkedin.com/in/mervinpraison">💼 LinkedIn</a>
  </p>
</div>
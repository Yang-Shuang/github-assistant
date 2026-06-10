<div align="center">
  <img src="docs/source/_static/img/PlanoTagline.svg" alt="Plano Logo" width="75%" height=auto>
</div>
<div align="center">

 _面向智能体应用的 AI 原生代理服务器与数据平面。<br><br>
 Plano 抽离了繁琐的底层基础设施工作，让你摆脱脆弱的框架抽象束缚。它将本不应在每个代码库中单独实现的核心功能集中管理——例如智能体路由与编排、用于持续改进的丰富智能体信号（Signals）与追踪记录、用于安全审核的护栏过滤器，以及支持模型灵活调用的智能 LLM 路由 API。使用任意编程语言或 AI 框架，即可将智能体更快推向生产环境。


[快速入门指南](https://docs.planoai.dev/get_started/quickstart.html) •
[使用 Plano 构建智能体应用](#Build-Agentic-Apps-with-Plano) •
[文档](https://docs.planoai.dev) •
[联系方式](#Contact)

[![CI](https://github.com/katanemo/plano/actions/workflows/ci.yml/badge.svg)](https://github.com/katanemo/plano/actions/workflows/ci.yml)
[![Docker Image](https://github.com/katanemo/plano/actions/workflows/docker-push-main.yml/badge.svg)](https://github.com/katanemo/plano/actions/workflows/docker-push-main.yml)
[![Build and Deploy Documentation](https://github.com/katanemo/plano/actions/workflows/static.yml/badge.svg)](https://github.com/katanemo/plano/actions/workflows/static.yml)

如果觉得 Plano 有用，欢迎给仓库点个 ⭐️ —— 新版本和更新将第一时间在此发布。
</div>

# 概述
构建智能体演示应用很容易，但安全、可靠且可重复地将它们部署到生产环境却很难。在体验了快速原型开发的快感后，你最终不得不自行搭建“隐式中件”才能上线：包括路由逻辑以调用正确的智能体、用于安全审核的护栏钩子（hooks）、用于持续学习的评估与可观测性胶水代码，以及散落在各个框架和应用代码中的模型/供应商适配问题。

Plano 通过将核心交付关注点移至统一的进程外数据平面来解决这一问题。

- **🚦 编排（Orchestration）：** 智能体间的低延迟编排；无需修改应用代码即可添加新智能体。
- **🔗 模型敏捷性（Model Agility）：** 支持[按模型名称、别名（语义名称）或通过偏好设置自动进行路由](#use-plano-as-a-llm-router)。
- **🕵 智能体信号（Agentic Signals™）：** 零代码捕获[信号（Signals）](https://docs.planoai.dev/concepts/signals.html)，以及跨所有智能体的 OpenTelemetry (OTEL) 追踪与指标。
- **🛡️ 审核与记忆钩子（Moderation & Memory Hooks）：** 通过[过滤器链（Filter Chains）](https://docs.planoai.dev/concepts/filter_chain.html)构建防越狱保护、统一添加审核策略与记忆功能。

Plano 将繁琐的底层基础设施工作从你的框架中抽离，让你专注于最重要的事情：智能体应用的核心产品逻辑。Plano 由[行业领先的 LLM 研究](https://planoai.dev/research)提供支持，并由其核心贡献者基于 [Envoy](https://envoyproxy.io) 构建，这些贡献者曾为现代工作负载构建了大规模的关键基础设施。

**高层网络时序图**：
![high-level network plano architecture for Plano](docs/source/_static/img/plano_network_diagram_high_level.png)

跳转至我们的[文档](https://docs.planoai.dev)，了解如何使用 Plano 提升智能体应用的开发速度、安全性与可观测性。

> [!IMPORTANT]
> Plano 及 Plano 系列的 LLM（如 Plano-Orchestrator）在美国中部区域免费提供托管，旨在为你带来出色的首次运行开发者体验。若要扩展规模并在生产环境中运行，你可以选择本地部署这些 LLM，或通过 [Discord](https://discord.gg/pGZf2gcwEc) 联系我们获取 API 密钥。

---

## 使用 Plano 构建智能体应用

Plano 将**编排、模型管理与可观测性**作为模块化构建块——让你只需配置所需部分（例如用于智能体编排与护栏的边缘代理，或服务的 LLM 路由，或两者结合），即可无缝融入现有架构。下面展示了一个使用 Plano 构建的简单多智能体旅行助手示例，涵盖了全部三项核心能力：

> 📁 **完整可运行代码：** 参见 [`demos/agent_orchestration/travel_agents/`](demos/agent_orchestration/travel_agents/) 获取完整的天气与航班智能体，可在本地直接运行。



### 1. 在 YAML 中定义你的智能体

```yaml
# config.yaml
version: v0.3.0

# What you declare: Agent URLs and natural language descriptions
# What you don't write: Intent classifiers, routing logic, model fallbacks, provider adapters, or tracing instrumentation

agents:
  - id: weather_agent
    url: http://localhost:10510
  - id: flight_agent
    url: http://localhost:10520

model_providers:
  - model: openai/gpt-4o
    access_key: $OPENAI_API_KEY
    default: true
  - model: anthropic/claude-3-5-sonnet
    access_key: $ANTHROPIC_API_KEY

listeners:
  - type: agent
    name: travel_assistant
    port: 8001
    router: plano_orchestrator_v1  # Powered by our 4B-parameter routing model. You can change this to different models
    agents:
      - id: weather_agent
        description: |
          Gets real-time weather and forecasts for any city worldwide.
          Handles: "What's the weather in Paris?", "Will it rain in Tokyo?"

      - id: flight_agent
        description: |
          Searches flights between airports with live status and schedules.
          Handles: "Flights from NYC to LA", "Show me flights to Seattle"

tracing:
  random_sampling: 100  # Auto-capture traces for evaluation
```

### 2. 编写简单的智能体代码

你的智能体只是实现了 OpenAI 兼容聊天补全接口的 HTTP 服务器。可以使用任意编程语言或框架：

```python
# weather_agent.py
from fastapi import FastAPI, Request
from fastapi.responses import StreamingResponse
from openai import AsyncOpenAI

app = FastAPI()

# Point to Plano's LLM gateway - it handles model routing for you
llm = AsyncOpenAI(base_url="http://localhost:12001/v1", api_key="EMPTY")

@app.post("/v1/chat/completions")
async def chat(request: Request):
    body = await request.json()
    messages = body.get("messages", [])
    days = 7

    # Your agent logic: fetch data, call APIs, run tools
    # See demos/agent_orchestration/travel_agents/ for the full implementation
    weather_data = await get_weather_data(request, messages, days)

    # Stream the response back through Plano
    async def generate():
        stream = await llm.chat.completions.create(
            model="openai/gpt-4o",
            messages=[{"role": "system", "content": f"Weather: {weather_data}"}, *messages],
            stream=True
        )
        async for chunk in stream:
            yield f"data: {chunk.model_dump_json()}\n\n"

    return StreamingResponse(generate(), media_type="text/event-stream")
```

### 3. 启动 Plano 并查询你的智能体

**前置条件：** 请按照[前置条件指南](https://docs.planoai.dev/get_started/quickstart.html#prerequisites)安装 Plano 并配置你的环境。

```bash
# Start Plano
planoai up config.yaml
...

# Query - Plano intelligently routes to both agents in a single conversation
curl http://localhost:8001/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-4o",
    "messages": [
      {"role": "user", "content": "I want to travel from NYC to Paris next week. What is the weather like there, and can you find me some flights?"}
    ]
  }'
# → Plano routes to weather_agent for Paris weather ✓
# → Then routes to flight_agent for NYC → Paris flights ✓
# → Returns a complete travel plan with both weather info and flight options
```

### 4. 免费获得可观测性与模型敏捷性

每个请求都会通过 OpenTelemetry 进行端到端追踪——无需编写任何埋点代码。

![Automatic Tracing](docs/source/_static/img/demo_tracing.png)

### 你无需自行构建的部分

| 基础设施关注点 | 无 Plano | 使用 Plano |
|---------|---------------|------------|
| **智能体编排** | 编写意图分类器 + 路由逻辑 | 在 YAML 中声明智能体描述 |
| **模型管理** | 处理各供应商的 API 差异 | 统一 LLM API 并内置状态管理 |
| **丰富追踪** | 使用 OTEL 为每个服务添加埋点 | 自动端到端追踪与日志记录 |
| **学习信号** | 构建管道以捕获/导出追踪跨度（spans） | 零代码智能体信号 |
| **新增智能体** | 更新路由代码、测试、重新部署 | 添加到配置中并重启服务 |

**为何高效：** Plano 采用专为路由设计的轻量级 LLM（如我们的 40 亿参数编排器），而非依赖重量级框架或 GPT-4——以极低的成本和延迟，为你提供生产级别的路由能力。

---

## 联系方式
如需联系我们，请加入我们的 [Discord 服务器](https://discord.gg/pGZf2gcwEc)。我们会积极在此监控并提供支持。

## 快速开始

准备好尝试 Plano 了吗？请查阅我们的完整文档：

- **[快速入门指南](https://docs.planoai.dev/get_started/quickstart.html)** - 几分钟内即可上手运行
- **[LLM 路由](https://docs.planoai.dev/guides/llm_router.html)** - 按模型名称、别名或智能偏好进行路由
- **[智能体编排](https://docs.planoai.dev/guides/orchestration.html)** - 构建多智能体工作流
- **[过滤器链](https://docs.planoai.dev/concepts/filter_chain.html)** - 添加护栏、审核与记忆钩子
- **[提示词目标（Prompt Targets）]** - 将提示词转换为确定性 API 调用
- **[可观测性](https://docs.planoai.dev/guides/observability/observability.html)** - 追踪、指标与日志

## 贡献指南
我们非常期待你针对[路线图](https://github.com/orgs/katanemo/projects/1)的反馈，也热烈欢迎为 **Plano** 做出贡献！无论你是修复 Bug、添加新功能、改进文档还是制作教程，我们都非常感谢你的帮助。请访问我们的[贡献指南](CONTRIBUTING.md)了解更多详情

如果觉得 Plano 有用，欢迎给仓库点个 ⭐️ —— 新版本和更新将第一时间在此发布。
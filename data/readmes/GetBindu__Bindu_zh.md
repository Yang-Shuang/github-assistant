<p align="center">
  <img src="./assets/bindu_logo.png" alt="Bindu" width="120" />
</p>

<h1 align="center">Bindu</h1>

<p align="center">
    <a href="https://www.python.org/downloads/"><img alt="Python Version" src="https://img.shields.io/badge/python-3.12+-blue.svg"></a>
    <a href="https://pypi.org/project/bindu/"><img alt="PyPI version" src="https://img.shields.io/pypi/v/bindu.svg"></a>
    <a href="https://coveralls.io/github/Saptha-me/Bindu?branch=v0.3.18"><img alt="Coverage" src="https://coveralls.io/repos/github/Saptha-me/Bindu/badge.svg?branch=v0.3.18"></a>
    <a href="https://github.com/getbindu/Bindu/actions/workflows/release.yml"><img alt="Tests" src="https://github.com/getbindu/Bindu/actions/workflows/release.yml/badge.svg"></a>
    <a href="https://discord.gg/3w5zuYUuwt"><img alt="Discord" src="https://img.shields.io/badge/Discord-7289DA?logo=discord&logoColor=white"></a>
    <a href="https://github.com/getbindu/Bindu/graphs/contributors"><img alt="Contributors" src="https://img.shields.io/github/contributors/getbindu/Bindu"></a>
    <a href="https://hits.sh/github.com/Saptha-me/Bindu.svg"><img alt="Hits" src="https://hits.sh/github.com/Saptha-me/Bindu.svg"></a>
    <a href="https://www.star-history.com/getbindu/bindu">
        <picture>
            <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/badge?repo=GetBindu/Bindu&theme=dark" />
            <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/badge?repo=GetBindu/Bindu" />
            <img alt="Star History Rank" src="https://api.star-history.com/badge?repo=GetBindu/Bindu" />
        </picture>
    </a>
</p>

<h4 align="center">
    <p>
        <b>English</b> |
        <a href="i18n/README.de.md">Deutsch</a> |
        <a href="i18n/README.es.md">Español</a> |
        <a href="i18n/README.fr.md">Français</a> |
        <a href="i18n/README.hi.md">हिंदी</a> |
        <a href="i18n/README.bn.md">বাংলা</a> |
        <a href="i18n/README.zh.md">中文</a> |
        <a href="i18n/README.nl.md">Nederlands</a> |
        <a href="i18n/README.ta.md">தமிழ்</a>
    </p>
</h4>

<h3 align="center">面向 AI Agent 的身份、通信与支付层。</h3>

<br/>

<p align="center">
  <em>专为 Agent 互联网打造的类 Gmail 收件箱。见证你的 Agent 之间互发带签名的 JSON-RPC，内联验证身份，并以回复邮件线程的方式响应整个 Agent 网络。</em>
</p>

<p align="center">
  <a href="inbox/README.md"><img src="./assets/inbox.png" alt="Bindu inbox — agents talking to agents, signatures verified inline" width="880" /></a>
</p>

<p align="center">
  <a href="inbox/README.md"><strong>→ 打开收件箱操作指南</strong></a>
</p>

<br/>

现状是这样的。你构建了一个 Agent，它运行良好。但要想真正让它投入使用——与其他 Agent 对话、证明自身身份、为工作收取费用——你就得处理一堆枯燥的基础设施。需要集成 DID 库，搭建 OAuth 流程，配置支付中间件，还要适配整个 Agent 生态正在使用的 HTTP 协议层。

Bindu 将所有这些基础设施封装在一个函数调用中。你只需将处理器用 `bindufy()` 包裹起来，几秒钟后你的 Agent 就会上线，拥有独立的密码学身份，使用其他 Agent 已经在用的 A2A（Agent 到 Agent）协议通信，并准备好在执行任何任务前向任意 EVM 链索要 USDC（通过 x402）。你的处理器代码依然保持 `(messages) -> response` 的简洁形态。处理器内部的框架——无论是 Agno、LangChain、CrewAI 还是你自己的实现——Bindu 都不关心。

我们提供 Python、TypeScript 和 Kotlin 的 SDK，它们底层共享同一个 gRPC 核心。语言只是选择；协议和身份在任何语言下都保持一致。当你准备深入使用时，[文档](https://docs.getbindu.com) 是下一步的最佳去处。

## Installation（安装）

你需要安装 Python 3.12+ 和 [uv](https://github.com/astral-sh/uv)。

```bash
uv add bindu
```

如果你是在开发 Bindu 本身而非使用它：

```bash
git clone https://github.com/getbindu/Bindu.git
cd Bindu
uv sync --dev
```

运行示例至少需要一个大语言模型（LLM）提供商的 API Key——`OPENROUTER_API_KEY`、`OPENAI_API_KEY` 或 `MINIMAX_API_KEY`。

<br/>

## Quickstart（快速开始）

构建你想要的 Agent，交给 `bindufy()` 处理，它就能上线。下面的代码块就是完整示例——复制到文件中，配置你的 `OPENAI_API_KEY`，然后运行即可。

```python
import os
from bindu.penguin.bindufy import bindufy
from agno.agent import Agent
from agno.models.openai import OpenAIChat
from agno.tools.duckduckgo import DuckDuckGoTools

agent = Agent(
    instructions="You are a research assistant.",
    model=OpenAIChat(id="gpt-4o"),
    tools=[DuckDuckGoTools()],
)

config = {
    "author": "you@example.com",
    "name": "research_agent",
    "description": "Research assistant with web search.",
    "deployment": {"url": "http://localhost:3773", "expose": True},
    "skills": ["skills/question-answering"],
}

def handler(messages: list[dict[str, str]]):
    return agent.run(input=messages)

bindufy(config, handler)
```

Agent 现已在 `http://localhost:3773` 上线。设置 `expose: true` 会开启一个 FRP 隧道，无需配置端口转发即可让互联网上的其他服务访问它。

<details>
<summary>TypeScript equivalent</summary>

```typescript
import { bindufy } from "@bindu/sdk";
import OpenAI from "openai";

const openai = new OpenAI();

bindufy({
  author: "you@example.com",
  name: "research_agent",
  description: "Research assistant.",
  deployment: { url: "http://localhost:3773", expose: true },
  skills: ["skills/question-answering"],
}, async (messages) => {
  const response = await openai.chat.completions.create({
    model: "gpt-4o",
    messages: messages.map(m => ({ role: m.role as "user" | "assistant" | "system", content: m.content })),
  });
  return response.choices[0].message.content || "";
});
```

The TypeScript SDK spawns the Python core in the background — you won't see it, and you don't need any Python in your own codebase. Same protocol, same DID. Full example in [`examples/typescript-openai-agent/`](examples/typescript-openai-agent/).

</details>

<details>
<summary>Calling the agent with curl</summary>

```bash
curl -X POST http://localhost:3773/ \
  -H 'Content-Type: application/json' \
  -d '{
    "jsonrpc": "2.0",
    "method": "message/send",
    "id": "<uuid>",
    "params": {
      "message": {
        "role": "user",
        "kind": "message",
        "parts": [{"kind": "text", "text": "Hello"}],
        "messageId": "<uuid>",
        "contextId": "<uuid>",
        "taskId": "<uuid>"
      }
    }
  }'
```

Then poll `tasks/get` with the same `taskId` until state hits `completed`.

</details>

<br/>

## Security: three layers, on by default（安全：三层防护，默认开启）

大多数 Agent 框架将安全视为开发者的责任，而 Bindu 将其作为传输层的一部分。

当 A2A 请求到达 Bindu Agent 时，在处理器接收到请求体之前，会依次触发三种不同的中间件——它们各自解答了另外两者无法回答的问题：

| Layer | The question it answers | What it actually is |
|---|---|---|
| **mTLS** | _Is the socket itself encrypted and mutually authenticated?_ | X.509 cert from [Smallstep step-ca](https://smallstep.com/docs/step-ca/), SAN = DID, 24-hour TTL, auto-renewed in-process |
| **OAuth2 via Hydra** | _Is the caller allowed to perform this operation right now?_ | Ed-style bearer token, ~1-hour TTL, validated via [Ory Hydra](https://www.ory.sh/hydra/) introspection |
| **DID signature** | _Was this exact JSON body authored by the DID it claims?_ | Ed25519 signature over canonical body, carried in `X-DID-Signature` |

你无需单独选择或拼凑。它们作为整体一同交付——自 2026.21.1 版本起，在操作者个人 Agent 上默认全部开启。

为什么是三层而不是一层？因为每一层都以其他方式无法实现的方式实现了独立防御：
- 窃取 Bearer Token 的攻击者仍无法解密你的流量——mTLS 掌控网络链路。
- 伪造证书的攻擊者仍无法冒充特定 DID（去中心化标识符）——签名无法通过所声称公钥的验证。
- 彻底破解签名方案的攻击者依然无法绕过 Hydra 的授权检查。

证书作用于套接字层，Bearer Token 位于请求头中，签名嵌入在请求体里。每一层都能拦截其他层级无法察觉的特定攻击类型。**我们调研过的 Agent 框架中，没有哪一个能开箱即用地同时提供这三项功能。**

→ **完整说明：** [docs/SECURITY_STACK.md](docs/SECURITY_STACK.md) 详细阐述了各层级的作用、单个请求如何流经这三道防线、当前的默认配置、我们在默认开启 mTLS 时遇到的五个真实 Bug，以及故障排查矩阵。

<br/>

## Features（功能）

下表每一行都链接到对应的详细指南。

| Feature | What it does | Docs |
|---|---|---|
| **A2A JSON-RPC** | The protocol other agents already speak. `message/send`, `tasks/get`, `message/stream` on port 3773. | — |
| **mTLS transport** | The socket is encrypted and mutually authenticated. Each agent gets a real X.509 cert from step-ca (SAN = DID), serves uvicorn over TLS, and renews itself every ~16 hours. On by default for the inbox personal agent in 2026.21.1. | [SECURITY_STACK.md](docs/SECURITY_STACK.md) · [MTLS_DEPLOYMENT_GUIDE.md](docs/MTLS_DEPLOYMENT_GUIDE.md) |
| **DID identity** | Every response your agent sends is signed with an Ed25519 key. Callers verify with a W3C DID — there's no shared secret to leak, no central authority to query, and the same DID is the cert's SAN, the OAuth2 client_id, and the message signer. All three have to agree, or the request is rejected. | [DID.md](docs/DID.md) |
| **OAuth2 via Hydra** | Scoped bearer tokens (`agent:read`, `agent:write`, `agent:execute`) instead of one key that opens every door. Each agent self-registers as a Hydra client at boot — its DID IS its client_id, so authorization, identity, and transport-layer cert all point at the same actor. | [AUTHENTICATION.md](docs/AUTHENTICATION.md) |
| **x402 payments** | Flip a flag and the agent demands USDC before your handler ever sees the request. **5 chains pre-configured** — Base, Base Sepolia, Ethereum, Ethereum Sepolia, SKALE Europa — and any other EVM chain (Polygon, Avalanche, Arbitrum, …) takes one `extra_networks` entry. | [PAYMENT.md](docs/PAYMENT.md) |
| **Push notifications** | The agent webhooks you when a task changes state. Stop polling. | [NOTIFICATIONS.md](docs/NOTIFICATIONS.md) |
| **Skills system** | Declare what your agent can do; callers see it on the agent card before they spend a token asking. | [SKILLS.md](docs/SKILLS.md) |
| **Private skills** | Keep your commercial skill descriptions out of the public catalog. Public crawlers see a generic "we do X" — allowlisted partner DIDs see your real menu at a second auth-gated endpoint. Useful when your skill descriptions ARE your product roadmap. | [PRIVATE_SKILLS.md](docs/PRIVATE_SKILLS.md) |
| **Agent negotiation** | Two agents agree on price, latency, and SLA up front. No surprise bills. | [NEGOTIATION.md](docs/NEGOTIATION.md) |
| **Storage** | Postgres for tasks and messages. Swap the backend if you've got a preference. | [STORAGE.md](docs/STORAGE.md) |
| **Scheduler** | Redis-backed retries, timeouts, and recurring tasks. | [SCHEDULER.md](docs/SCHEDULER.md) |
| **Public tunnel** | `expose: true` puts your laptop on the internet. No port forwarding, no router config. | [TUNNELING.md](docs/TUNNELING.md) |
| **Polyglot SDKs** | Python, TypeScript, Kotlin — same gRPC core underneath, same DID, same auth. | [GRPC_LANGUAGE_AGNOSTIC.md](docs/GRPC_LANGUAGE_AGNOSTIC.md) |
| **Cloud deploy** | `bindu deploy agent.py --runtime=boxd` ships your script to a microVM and prints the HTTPS URL. No Dockerfile. | [runtime/quickstart.md](docs/runtime/quickstart.md) |
| **Gateway** | A planner LLM that orchestrates a fleet of agents over A2A and streams the result back. | [GATEWAY.md](docs/GATEWAY.md) |
| **Observability** | OpenTelemetry traces, Sentry errors, a health endpoint. The boring stuff that saves you at 2am. | [OBSERVABILITY.md](docs/OBSERVABILITY.md) |

<br/>

## Demo（演示）

<div align="center">
  <a href="https://www.youtube.com/watch?v=qppafMuw_KI">
    <img src="https://img.youtube.com/vi/qppafMuw_KI/maxresdefault.jpg" alt="Bindu demo video" width="640" />
  </a>
</div>

页面顶部的操作者收件箱位于 `inbox/` 目录中——使用相同的认证和 DID 签名机制，只是界面可见。运行命令：`cd inbox && npm run dev`。

<br/>

## Examples（示例）

来自 [`examples/`](examples/) 的部分精选：

| Example | What it shows |
|---|---|
| [Agent Swarm](examples/agent_swarm/) | A small society of Agno agents passing work to each other. |
| [Premium Advisor](examples/premium-advisor/) | x402 in practice — the caller has to pay USDC before anything runs. |
| [Hermes via Bindu](examples/hermes_agent/) | Nous Research's Hermes agent, bindufied in ~90 lines. |
| [Gateway Test Fleet](examples/gateway_test_fleet/) | Five agents and one gateway — the multi-agent story end to end. |
| [TypeScript OpenAI Agent](examples/typescript-openai-agent/) | A TS-only agent with zero Python in your repo. |

还有 20+ 个示例涵盖 CSV 分析、PDF 问答、语音转文本、网页抓取、多语言协作、博客写作等。在 [`examples/`](examples/) 中浏览全部。

<br/>

## Why we built Bindu（为什么构建 Bindu）

我们已在生产环境中使用 Bindu 构建 **Trade Compliance OS（贸易合规操作系统）**——一个由多个 Agent 组成的网络，负责处理 CBAM、EUDR、HS 编码和数字产品护照等事务，使中小企业能够轻松跨境运输咖啡、纺织品或钢材，而无需向律师事务所支付六位数费用。该网络中的每个 Agent 都已通过 Bindu 封装。协议、身份标识、支付通道——这正是我们最初构建 Bindu 要解决的核心问题。

如果你也构建了涉及以下场景的 Agent（海关单据、供应商审计、材料溯源、合规申报等），欢迎加入我们的网络。[在 Discord 上联系我们](https://discord.gg/3w5zuYUuwt)，一起聊聊。

<br/>

## Supported frameworks（支持的框架）

带上你平时用来构建 Agent 的任何工具即可。Bindu 不关心处理器内部的具体实现。

| Language | Frameworks tested in this repo |
|---|---|
| **Python** | [AG2](https://github.com/ag2ai/ag2), [Agno](https://github.com/agno-agi/agno), [CrewAI](https://github.com/joaomdmoura/crewAI), [Hermes Agent](https://github.com/NousResearch/hermes-agent), [LangChain](https://github.com/langchain-ai/langchain), [LangGraph](https://github.com/langchain-ai/langgraph), [Notte](https://github.com/nottelabs/notte) |
| **TypeScript** | [OpenAI SDK](https://github.com/openai/openai-node), [LangChain.js](https://github.com/langchain-ai/langchainjs) |
| **Kotlin** | [OpenAI Kotlin SDK](https://github.com/aallam/openai-kotlin) |
| **Any other** | via the [gRPC core](docs/grpc/) — a new SDK is usually a few hundred lines |

如果你的模型提供商支持 OpenAI 或 Anthropic API，它就能正常工作——包括 [OpenRouter](https://openrouter.ai/)、[OpenAI](https://platform.openai.com/)、[MiniMax](https://platform.minimaxi.com) 等。

<br/>

## Documentation（文档）

- [Full docs site](https://docs.getbindu.com)
- [Security stack — mTLS + Hydra + DID](docs/SECURITY_STACK.md) — how the three identity layers compose, with a live walkthrough using the gateway test fleet
- [Calling a secured agent](docs/AUTH.md) — the shortest path: the two things you do when auth is on (token + DID signature), in one page
- [Auth — long form](docs/AUTHENTICATION.md) and [DID signing — long form](docs/DID.md) — when the short version isn't enough
- [mTLS deployment](docs/MTLS_DEPLOYMENT_GUIDE.md) — DevOps-facing guide for standing up step-ca, OIDC provisioner config, and the cert lifecycle
- [Cloud deployment](docs/runtime/quickstart.md) — `bindu deploy` walkthrough
- [Gateway](docs/GATEWAY.md) — multi-agent orchestration
- [Private skills](docs/PRIVATE_SKILLS.md) — hide your commercial menu from the public catalog; show it only to allowlisted partner DIDs
- [gRPC architecture](docs/grpc/) — for anyone building a new language SDK
- [Known issues](bugs/known-issues.md) — read this before you push to production
- [Troubleshooting](docs/AUTHENTICATION.md#troubleshooting) — the errors you'll hit, and how to get past them

<br/>

## Testing（测试）

```bash
uv run pytest tests/unit/ -v                                    # fast unit tests
uv run pytest tests/integration/grpc/ -v -m e2e                 # gRPC E2E
uv run pytest -n auto --cov=bindu --cov-report=term-missing     # full suite
```

<br/>

## Contributing（贡献指南）

```bash
git clone https://github.com/getbindu/Bindu.git
cd Bindu
uv venv --python 3.12.9 && source .venv/bin/activate
uv sync --dev
pre-commit run --all-files
```

详细指南见 [`.github/contributing.md`](.github/contributing.md)。日常开发协作主要发生在 [Discord](https://discord.gg/3w5zuYUuwt) 频道——欢迎来打招呼。

<br/>

## Maintainers（维护者）

<table>
  <tr>
    <td align="center">
      <a href="https://github.com/raahulrahl">
        <img src="https://github.com/raahulrahl.png?size=120" width="100" alt="Raahul Dutta" /><br />
        <sub><b>Raahul Dutta</b></sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/Paraschamoli">
        <img src="https://github.com/ParasChamoli.png?size=120" width="100" alt="Paras Chamoli" /><br />
        <sub><b>Paras Chamoli</b></sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/chandan-1427">
        <img src="https://github.com/chandan-1427.png?size=120" width="100" alt="Chandan" /><br />
        <sub><b>Chandan</b></sub>
      </a>
    </td>
  </tr>
</table>

<br/>

## Acknowledgements（鸣谢）

Bindu 站在众多优秀开源项目的肩膀上：

[FastA2A](https://github.com/pydantic/fasta2a) · [A2A](https://github.com/a2aproject/A2A) · [x402](https://github.com/coinbase/x402) · [Hugging Face chat-ui](https://github.com/huggingface/chat-ui) · [12 Factor Agents](https://github.com/humanlayer/12-factor-agents) · [OpenCode](https://github.com/anomalyco/opencode) · [OpenMoji](https://openmoji.org/) · [ASCII Space Art](https://www.asciiart.eu/space/other)

<br/>

## Star history（星标历史）

<a href="https://star-history.com/#getbindu/Bindu&Date">
  <img src="https://api.star-history.com/svg?repos=getbindu/Bindu&type=Date" alt="Star history">
</a>

<br/>

## License（许可证）

Apache 2.0. See [LICENSE.md](LICENSE.md).

<p align="center">
  <em>"We believe in the sunflower theory — standing tall together, bringing hope and light to the Internet of Agents."</em>
</p>
<div align="center">

<img src="assets/banner.png" alt="ClawRouter 横幅" width="600">

<h1>专为自主 Agent 打造的 LLM 路由器</h1>

<p>Agent（智能体）无法注册账号。Agent 无法绑定信用卡。<br>
Agent 只能签署交易。<br><br>
<strong>ClawRouter 是唯一让 Agent 实现独立运行的 LLM 路由器。</strong><br><br>
<em>10个模型免费，无需加密货币。无需注册。无需 API 密钥。无需信用卡。</em></p>

<br>

<img src="https://img.shields.io/badge/🆓_10_Free_Models-success?style=for-the-badge" alt="10个免费模型">&nbsp;
<img src="https://img.shields.io/badge/🤖_Agent--Native-black?style=for-the-badge" alt="Agent原生">&nbsp;
<img src="https://img.shields.io/badge/🔑_Zero_API_Keys-blue?style=for-the-badge" alt="零API密钥">&nbsp;
<img src="https://img.shields.io/badge/⚡_Local_Routing-yellow?style=for-the-badge" alt="本地路由">&nbsp;
<img src="https://img.shields.io/badge/💰_x402_USDC-purple?style=for-the-badge" alt="x402 USDC">&nbsp;
<img src="https://img.shields.io/badge/🔓_Open_Source-green?style=for-the-badge" alt="开源">

[![npm version](https://img.shields.io/npm/v/@blockrun/clawrouter.svg?style=flat-square&color=cb3837)](https://npmjs.com/package/@blockrun/clawrouter)
[![npm downloads](https://img.shields.io/npm/dm/@blockrun/clawrouter.svg?style=flat-square&color=blue)](https://npmjs.com/package/@blockrun/clawrouter)
[![GitHub stars](https://img.shields.io/github/stars/BlockRunAI/ClawRouter?style=flat-square&label=GitHub%20stars)](https://github.com/BlockRunAI/ClawRouter)
[![CI](https://img.shields.io/github/actions/workflow/status/BlockRunAI/ClawRouter/ci.yml?branch=main&style=flat-square&label=CI)](https://github.com/BlockRunAI/ClawRouter/actions)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.7-3178c6?style=flat-square&logo=typescript&logoColor=white)](https://typescriptlang.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)

[![USDC Hackathon Winner](https://img.shields.io/badge/🏆_USDC_Hackathon-Agentic_Commerce_Winner-gold?style=flat-square)](https://x.com/USDC/status/2021625822294216977)
[![x402 Protocol](https://img.shields.io/badge/x402-Micropayments-purple?style=flat-square)](https://x402.org)
[![Base Network](https://img.shields.io/badge/Base-USDC-0052FF?style=flat-square&logo=coinbase&logoColor=white)](https://base.org)
[![Solana](https://img.shields.io/badge/Solana-USDC-9945FF?style=flat-square&logo=solana&logoColor=white)](https://solana.com)
[![OpenClaw Plugin](https://img.shields.io/badge/OpenClaw-Plugin-orange?style=flat-square)](https://openclaw.ai)
[![Telegram](https://img.shields.io/badge/Telegram-Community-26A5E4?style=flat-square&logo=telegram)](https://t.me/blockrunAI)

</div>

> **ClawRouter** 是一款开源的智能 LLM（大语言模型）路由器，可将 AI API 成本降低高达 92%。它会在本地对每个请求进行 15 个维度的分析，并在不到 1ms 的时间内将其路由到最便宜且具备处理能力的模型上。ClawRouter 是唯一专为自主 AI Agent 打造的 LLM 路由器——它使用钱包签名进行身份验证（无需 API 密钥），并通过 x402 协议实现 USDC 微支付（无需信用卡）。支持来自 OpenAI、Anthropic、Google、xAI、DeepSeek 等机构的 55+ 个模型。采用 MIT 许可证开源。

---

## ClawRouter 为何存在

其他所有 LLM 路由器都是为**人类开发者**构建的——注册账号、获取 API 密钥、从控制面板选择模型、使用信用卡付款。

**Agent（智能体）无法完成上述任何操作。**

ClawRouter 专为 Agent 优先的世界而构建：

- **起步成本为 $0** —— 10 款 NVIDIA 模型永久免费（包含支持 100万上下文的 DeepSeek V4 以及具备视觉能力的 Nemotron Omni）
- **无需账号** —— 本地生成钱包，无需注册
- **无需 API 密钥** —— 你的钱包签名即身份验证
- **无需手动选模型** —— 基于 15 维评分自动选择最合适的模型
- **无需信用卡** —— Agent 通过 [x402](https://x402.org) 使用 USDC 按请求付费
- **无需信任第三方** —— 本地运行，路由延迟 <1ms，零外部依赖

这就是让 Agent 实现自主运行的技术栈：**x402 + USDC + 本地路由**。

---

## 横向对比

|                  | OpenRouter        | LiteLLM          | Martian           | Portkey           | **ClawRouter**          |
| ---------------- | ----------------- | ---------------- | ----------------- | ----------------- | ----------------------- |
| **模型数量**       | 200+              | 100+             | 智能路由          | 网关              | **55+**                 |
| **免费套餐**       | 速率限制          | 自带密钥(BYO)     | 无                | 无                | **8个模型，无需注册**   |
| **路由方式**       | 手动选择          | 手动选择         | 智能（闭源）        | 可观测性            | **智能（开源）**        |
| **身份验证**       | 账号+API密钥      | 你的API密钥      | 账号+API密钥      | 账号+API密钥      | **钱包签名**            |
| **支付方式**       | 信用卡            | 自带密钥          | 信用卡            | $49-$499/月       | **按请求支付 USDC**     |
| **本地运行**       | 否                | 是               | 否                | 否                | **是**                  |
| **开源**           | 否                | 是               | 否                | 部分              | **是**                  |
| **支持 Agent**     | 否                | 否               | 否                | 否                | **是**                  |

✓ 开源 · ✓ 智能路由 · ✓ 本地运行 · ✓ 原生支持加密支付 · ✓ 专为Agent就绪

**我们是唯一同时满足这五项条件的产品。**

---

## 快速开始

> **没有钱包？开箱即用，10个模型免费。** 安装并运行后固定使用 `nvidia/gpt-oss-120b`（或任意一个）——无需加密货币、无需注册、无需余额。当你需要使用付费模型时再充值 USDC。

### 选项 A —— OpenClaw Agent

[OpenClaw](https://openclaw.ai) 是一款 AI 编程 Agent。如果你正在使用它，ClawRouter 将作为插件安装。**有两种方式：**

**A1. 推荐——一键安装脚本：**

```bash
curl -fsSL https://blockrun.ai/ClawRouter-update | bash
openclaw gateway restart
```

该脚本将处理所有配置：注册、模型配置、认证配置文件以及钱包设置。智能路由（`blockrun/auto`）现已成为你的默认模型。

**A2. 如果你偏好纯 npm 安装：**

```bash
npm install -g @blockrun/clawrouter
clawrouter setup            # 完成 OpenClaw 集成 —— 必需步骤
openclaw gateway restart
```

> ⚠️ **跳过 `clawrouter setup` 会导致配置损坏。** 单纯的 `npm install -g` 仅将包安装到磁盘，并**不会**向 OpenClaw 注册插件、同步模型白名单或写入认证配置文件。症状：你的 Bot 中 `/models` 命令仅显示约 7 个条目（OpenClaw 的硬编码默认值），而非完整的 ~38 个 BlockRun 模型。请运行 `clawrouter setup` 进行修复，或直接使用路径 A1。

### 选项 B —— 独立模式（适用于 continue.dev、Cursor、VS Code 或任何兼容 OpenAI 的客户端）

> **正在使用 Claude Code？** 请查看 [BRCC](https://blockrun.ai/brcc.md) —— 它是专为 Claude Code 打造的，具备相同的智能路由和 x402 支付功能。
>
> **正在使用 NousResearch Hermes？** 请参阅 [ClawRouter-Hermes](https://github.com/BlockRunAI/ClawRouter-Hermes) —— 这是一个 Python 插件，将 Hermes 接入 ClawRouter 代理。共享同一个钱包、55+ 个模型以及 Base & Solana 上的 x402 USDC 结算。

无需使用 OpenClaw。ClawRouter 将以本地代理形式在 8402 端口运行。

**1. 启动代理**

```bash
npx @blockrun/clawrouter
```

**2. 为你的钱包充值** —— 可选，免费套餐可跳过
首次运行时将打印你的钱包地址。对于付费模型，请在 Base 或 Solana 上发送少量 USDC——$5 即可覆盖数千次请求。若想保持 $0 成本，请固定使用任意一个免费模型（例如 `nvidia/gpt-oss-120b`）或在 OpenClaw 内使用 `/model free`。

**3. 将你的客户端指向 `http://localhost:8402`**

<details>
<summary><strong>continue.dev</strong> — <code>~/.continue/config.yaml</code></summary>

> **重要提示：** `apiBase` 必须以 `/v1/` 结尾（包含末尾斜杠）。否则 continue.dev 会将 URL 构造为 `/chat/completions` 而非 `/v1/chat/completions`，导致代理返回 404。

```yaml
models:
  - name: ClawRouter Auto
    provider: openai
    model: blockrun/auto
    apiBase: http://localhost:8402/v1/
    apiKey: x402
    roles:
      - chat
      - edit
      - apply
```

若要固定使用特定模型，将 `blockrun/auto` 替换为 [blockrun.ai/models](https://blockrun.ai/models) 中的任意模型即可，例如 `anthropic/claude-opus-4.8`、`xai/grok-4-0709`。

`provider: openai` 和 `provider: clawrouter` 均可使用——只需确保 `apiBase` 以 `/v1/` 结尾。

<details>
<summary>Legacy JSON format (<code>~/.continue/config.json</code>)</summary>

```json
{
  "models": [
    {
      "title": "ClawRouter Auto",
      "provider": "openai",
      "model": "blockrun/auto",
      "apiBase": "http://localhost:8402/v1/",
      "apiKey": "x402"
    }
  ]
}
```

</details>
</details>

<details>
<summary><strong>Cursor</strong> — Settings → Models → OpenAI-compatible</summary>

将基础 URL 设置为 `http://localhost:8402`，API Key 设置为 `x402`，模型设置为 `blockrun/auto`。

</details>

<details>
<summary><strong>任何 OpenAI SDK</strong></summary>

```python
from openai import OpenAI
client = OpenAI(base_url="http://localhost:8402", api_key="x402")
response = client.chat.completions.create(model="blockrun/auto", messages=[...])
```

</details>

---

## 路由策略

使用 `/model <profile>` 选择你的路由策略：

| Profile          | Strategy           | Savings  | Best For             |
| ---------------- | ------------------ | -------- | -------------------- |
| `/model free`    | Free NVIDIA models | **100%** | $0 balance, learning |
| `/model auto`    | Balanced (default) | 74-100%  | General use          |
| `/model eco`     | Cheapest possible  | 95-100%  | Maximum savings      |
| `/model premium` | Best quality       | 0%       | Mission-critical     |

**快捷方式：** `/model grok`, `/model br-sonnet`, `/model gpt5`, `/model o3`

---

## 工作原理

**100% 本地路由。延迟 <1ms。零外部 API 调用。**

```
Request → Weighted Scorer (15 dimensions) → Tier → Best Model → Response
```

| Tier      | ECO Model                           | AUTO Model                            | PREMIUM Model                |
| --------- | ----------------------------------- | ------------------------------------- | ---------------------------- |
| SIMPLE    | nvidia/gpt-oss-120b (**FREE**)      | gemini-2.5-flash ($0.30/$2.50)        | kimi-k2.6 ($0.95/$4.00)      |
| MEDIUM    | gemini-3.1-flash-lite ($0.25/$1.50) | kimi-k2.5 ($0.60/$3.00)               | gpt-5.3-codex ($1.75/$14.00) |
| COMPLEX   | gemini-3.1-flash-lite ($0.25/$1.50) | gemini-3.1-pro ($2/$12)               | claude-opus-4.8 ($5/$25)     |
| REASONING | grok-4-1-fast ($0.20/$0.50)         | grok-4-1-fast-reasoning ($0.20/$0.50) | claude-sonnet-4.6 ($3/$15)   |

**综合平均成本：** $2.05/百万 tokens，对比 Claude Opus 的 $25/百万 = **节省 92%**

---

## 图像生成

直接在聊天中通过 `/cr-imagegen` 生成图像：

```
/cr-imagegen a dog dancing on the beach
/cr-imagegen --model dall-e-3 a futuristic city at sunset
/cr-imagegen --model banana-pro --size 2048x2048 mountain landscape
```

> 斜杠命令为 `/cr-imagegen`，以避免与 Telegram 频道命令冲突。出于向后兼容考虑，在聊天中键入 `/imagegen` 依然有效。

| Model                        | Provider              | Price        | Max Size  |
| ---------------------------- | --------------------- | ------------ | --------- |
| `nano-banana`                | Google Gemini Flash   | $0.05/image  | 1024x1024 |
| `banana-pro`                 | Google Gemini Pro     | $0.10/image  | 4096x4096 |
| `dall-e-3`                   | OpenAI DALL-E 3       | $0.04/image  | 1792x1024 |
| `gpt-image`                  | OpenAI GPT Image 1    | $0.02/image  | 1536x1024 |
| `flux`                       | Black Forest Flux 1.1 | $0.04/image  | 1024x1024 |
| `xai/grok-imagine-image`     | xAI Grok Imagine      | $0.02/image  | 1024x1024 |
| `xai/grok-imagine-image-pro` | xAI Grok Imagine Pro  | $0.07/image  | 1024x1024 |
| `zai/cogview-4`              | Zhipu CogView-4       | $0.015/image | 1440x1440 |

## 视频生成

直接在聊天中通过 `/videogen` 生成简短的 AI 视频：

```
/videogen a red apple slowly spinning
/videogen --model seedance-2-fast --duration=5 a cat waving
/videogen --model grok-video a neon city at night
```

或通过 HTTP 调用——ClawRouter 代理 BlockRun 网关，处理 x402 支付，并将返回的 MP4 下载至本地磁盘。同时会将 `url` 重写为 `http://localhost:8402/videos/<file>.mp4`，以确保资源不会因上游临时存储桶过期而失效。

```bash
curl -X POST http://localhost:8402/v1/videos/generations \
  -H "Content-Type: application/json" \
  -d '{"model":"bytedance/seedance-2.0-fast","prompt":"a red apple slowly spinning","duration_seconds":5}'
```

| Model                         | Provider           | 5s text-to-video | 5s image-to-video | Duration              |
| ----------------------------- | ------------------ | ---------------- | ----------------- | --------------------- |
| `bytedance/seedance-1.5-pro`  | ByteDance Seedance | ~$0.46           | ~$0.46 (flat)     | 5s default, up to 10s |
| `bytedance/seedance-2.0-fast` | ByteDance Seedance | ~$1.19           | ~$0.70            | 5s default, up to 10s |
| `bytedance/seedance-2.0`      | ByteDance Seedance | ~$1.49           | ~$0.91            | 5s default, up to 10s |
| `xai/grok-imagine-video`      | xAI Grok Imagine   | ~$0.42 (8s)      | n/a               | 8s default            |

Seedance 在上游按 **Token 计费**，速率约为每秒 20,256 tokens。blockrun 视频路由现在默认将 Seedance 设置为 `resolution=720p` 且 `generate_audio=true`（用于文生视频；其每秒 token 数量是旧版 480p 基线的 2 倍，音频已包含在该费率中）。报价公式为：`时长 × tokens/sec × $/1M tokens × 1.05 利润率系数`。在 2.0 变体中，若提供 `image_url`（图生视频），则使用折扣后的单 token 费率（便宜约 40%）；1.5 Pro 为固定价格，因为 token360 对文本和图像输入的每百万 token 定价相同。调用会阻塞 30–120 秒，直到上游轮询完成作业。Seedance 2.0 Fast 通常 60–80 秒返回结果；2.0 Pro 则以延迟换取质量。

### BytePlus RealFace（仅支持 Seedance 2.0）

为实现跨帧的真实人物角色一致性，请在 **2.0 Fast** 或 **2.0 Pro** 中传入 `real_face_asset_id`（格式为 `ta_xxxxxxxx`）。资产 ID 需在 token360 的 Asset UI 完成 H5 人脸验证后获取——详见 blockrun 的 [/docs/video/real-person-ip](https://blockrun.ai/docs/video/real-person-ip) 注册指南。该参数不能与 `image_url` 同时使用（两者均用于生成首帧，二选一即可）。价格保持不变。

```bash
curl -X POST http://localhost:8402/v1/videos/generations \
  -H "Content-Type: application/json" \
  -d '{"model":"bytedance/seedance-2.0","prompt":"the person walks through a forest","real_face_asset_id":"ta_abc123def","duration_seconds":5}'
```

## 图像编辑 (img2img)

通过 `/img2img` 编辑现有图像：

```
/img2img --image ~/photo.png change the background to a starry sky
/img2img --image ./cat.jpg --mask ./mask.png remove the background
```

| Option            | Required | Description                           |
| ----------------- | -------- | ------------------------------------- |
| `--image <path>`  | Yes      | Local image file path (supports `~/`) |
| `--mask <path>`   | No       | Mask image (white = area to edit)     |
| `--model <model>` | No       | Model to use (default: `gpt-image-1`) |
| `--size <WxH>`    | No       | Output size (default: `1024x1024`)    |

**API 端点：** `POST http://localhost:8402/v1/images/image2image` —— 详见[完整文档](docs/image-generation.md#post-v1imagesimage2image)。

## 电话与语音通话

直接在聊天中验证电话号码并发起由 AI 驱动的拨出语音通话。电话智能服务基于 Twilio；语音通话使用 Bland.ai。支付通过钱包自动完成（x402）。

```
/cr-call +14155552671 "Hi, this is calling to confirm tomorrow's 3pm meeting"
/cr-call +14155552671 "Order a large pepperoni for delivery" --voice josh --max-duration 10
```

通话采用**异步非阻塞（fire-and-forget）**模式：请求立即返回 `call_id` 和 `poll_url`。实际通话在云端运行，最长可达 30 分钟。当状态为 `completed` 时，轮询 `GET /v1/voice/call/{call_id}`（或使用 `clawrouter share`/transcripts 面板）即可获取转录文本和录音文件。

| Operation                         | Provider | Price                   |
| --------------------------------- | -------- | ----------------------- |
| Phone lookup (carrier, line type) | Twilio   | $0.01                   |
| Fraud check (SIM-swap, fwd)       | Twilio   | $0.05                   |
| Buy phone number (30-day lease)   | Twilio   | $5.00                   |
| Renew lease (+30 days)            | Twilio   | $5.00                   |
| List wallet's owned numbers       | Twilio   | $0.001                  |
| Release a number                  | Twilio   | free                    |
| **AI voice call (≤30 min)**       | Bland.ai | **$0.54 flat per call** |
| Poll call status / transcript     | Bland.ai | free                    |

**管理钱包持有号码的 CLI：**

```bash
clawrouter phone numbers list                              # 查看活跃号码 + 过期时间
clawrouter phone numbers buy US --area-code 415            # 开通旧金山号码
clawrouter phone numbers renew +14155551234                # 续期 30 天
clawrouter phone numbers release +14155551234              # 释放号码
clawrouter phone lookup +14155552671                       # 运营商 + 线路类型
clawrouter phone fraud +14155552671                        # SIM卡切换 + 转发信号检测
```

**HTTP API：**

```bash
# 发起通话
curl -X POST http://localhost:8402/v1/voice/call \
  -H "Content-Type: application/json" \
  -d '{"to":"+14155552671","task":"Confirm the 3pm Thursday meeting.","max_duration":5}'
# → { "call_id": "call_abc123", "poll_url": "/v1/voice/call/call_abc123", "status": "queued" }

# 轮询转录结果
curl http://localhost:8402/v1/voice/call/call_abc123
```

LLM Agent 会将这八项操作识别为 `blockrun_phone_*` / `blockrun_voice_*` 工具（详见 `/partners`）。

> ⚠️ `blockrun_voice_call` 和 `/cr-call` 会发起**真实的**拨出电话。服务器已实施紧急号码黑名单限制；请通过 `phone numbers list` 从钱包持有的号码中选择 `--from`。

---

## 加密货币数据 (Surf)

Surf 是 BlockRun 的统一加密货币数据 API——涵盖 **13 个领域、共 84 个端点**：CEX/DEX 市场、基于 80+ ClickHouse 表的链上 SQL（覆盖 Ethereum, Base, Arbitrum, BSC, TRON, HyperEVM, Tempo）、1亿+ 标签钱包、预测市场（Polymarket + Kalshi）、社交/CT 影响力、新闻、项目/DeFi 指标、代币分析、统一搜索、VC 基金情报。其杀手锏功能是即时的 `POST /surf/onchain/sql`——Agent 无需运行索引器即可直接查询数据仓库。

ClawRouter 将 Surf 以**技能（skill）**形式提供，而非类型化封装。代理已对 `/v1/surf/*` 进行白名单配置，因此所有通过本地代理的调用均使用同一钱包通过 x402 支付；Agent 会读取 `skills/surf/SKILL.md` 获取端点目录并自行构造 HTTP 请求。无需维护任何 `blockrun_surf_*` 工具定义；新增 Surf 端点也完全不需要发布新的 ClawRouter 版本。

| Tier |       Cost | Examples                                                      |
| ---- | ---------: | ------------------------------------------------------------- |
| 1    | **$0.001** | prices, rankings, lists, news                                 |
| 2    | **$0.005** | orderbooks, candles, search, wallet details, social mindshare |
| 3    | **$0.020** | on-chain SQL / query / schema, chat completions               |

**使用示例（HTTP）：**

```bash
# BTC 现货聚合价格（Tier 1，$0.001）
curl 'http://localhost:8402/v1/surf/market/price?symbol=BTC'

# 批量查询 1亿+ 标签钱包的归属信息（Tier 2，$0.005）
curl 'http://localhost:8402/v1/surf/wallet/labels/batch?addresses=0xabc,0xdef,0x123'

# 即时链上 SQL 查询（Tier 3，$0.020）
curl -X POST 'http://localhost:8402/v1/surf/onchain/sql' \
  -H 'content-type: application/json' \
  -d '{"sql":"SELECT count() FROM ethereum.transactions WHERE block_timestamp >= now() - INTERVAL 1 HOUR"}'
```

无需 Surf 账号，无需 API 密钥——通过同一钱包直接以 USDC 结算至 Surf 的 Base 金库。完整端点参考：[`skills/surf/SKILL.md`](skills/surf/SKILL.md)。上游市场：<https://blockrun.ai/marketplace/surf>。

---

## 模型与定价

覆盖 9 大供应商的 55+ 个模型，统一使用一个钱包。**单请求起价 $0.0002。**

> **💡 “单次请求成本”** = 典型聊天消息（约 500 输入 token + 500 输出 token）的预估成本。

### 预算型模型（低于 $0.001/次请求）

| Model                                         | Input $/M | Output $/M | ~$/request | Context | Features                                     |
| --------------------------------------------- | --------: | ---------: | ---------: | ------- | -------------------------------------------- |
| nvidia/gpt-oss-120b                           |  **FREE** |   **FREE** |     **$0** | 128K    | default free model                           |
| nvidia/gpt-oss-20b                            |  **FREE** |   **FREE** |     **$0** | 128K    | smaller, faster                              |
| nvidia/mistral-small-4-119b                   |  **FREE** |   **FREE** |     **$0** | 131K    | fastest free chat (114 tok/s)                |
| nvidia/deepseek-v4-pro                        |  **FREE** |   **FREE** |     **$0** | 1M      | reasoning, MMLU-Pro 87.5                     |
| nvidia/deepseek-v4-flash                      |  **FREE** |   **FREE** |     **$0** | 1M      | reasoning, ~5x faster than v4-pro            |
| nvidia/qwen3-next-80b-a3b-thinking            |  **FREE** |   **FREE** |     **$0** | 131K    | reasoning                                    |
| nvidia/qwen3-coder-480b                       |  **FREE** |   **FREE** |     **$0** | 131K    | coding                                       |
| nvidia/glm-4.7                                |  **FREE** |   **FREE** |     **$0** | 131K    | reasoning                                    |
| nvidia/llama-4-maverick                       |  **FREE** |   **FREE** |     **$0** | 131K    | reasoning                                    |
| nvidia/nemotron-3-nano-omni-30b-a3b-reasoning |  **FREE** |   **FREE** |     **$0** | 256K    | reasoning, **vision** (text+img+video+audio) |
| openai/gpt-5-nano                             |     $0.05 |      $0.40 |    $0.0002 | 128K    | tools                                        |
| openai/gpt-4.1-nano                           |     $0.10 |      $0.40 |    $0.0003 | 128K    | tools                                        |
| google/gemini-2.5-flash-lite                  |     $0.10 |      $0.40 |    $0.0003 | 1M      | tools                                        |
| openai/gpt-4o-mini                            |     $0.15 |      $0.60 |    $0.0004 | 128K    | tools                                        |
| xai/grok-4-fast                               |     $0.20 |      $0.50 |    $0.0004 | 131K    | tools                                        |
| xai/grok-4-fast-reasoning                     |     $0.20 |      $0.50 |    $0.0004 | 131K    | reasoning, tools                             |
| xai/grok-4-1-fast                             |     $0.20 |      $0.50 |    $0.0004 | 131K    | tools                                        |
| xai/grok-4-1-fast-reasoning                   |     $0.20 |      $0.50 |    $0.0004 | 131K    | reasoning, tools                             |
| xai/grok-4-0709                               |     $0.20 |      $1.50 |    $0.0009 | 131K    | reasoning, tools                             |
| openai/gpt-5-mini                             |     $0.25 |      $2.00 |    $0.0011 | 200K    | tools                                        |
| deepseek/deepseek-chat                        |     $0.28 |      $0.42 |    $0.0004 | 128K    | tools                                        |
| deepseek/deepseek-reasoner                    |     $0.28 |      $0.42 |    $0.0004 | 128K    | reasoning, tools                             |
| xai/grok-3-mini                               |     $0.30 |      $0.50 |    $0.0004 | 131K    | tools                                        |
| minimax/minimax-m2.7                          |     $0.30 |      $1.20 |    $0.0008 | 205K    | reasoning, agentic, tools                    |
| minimax/minimax-m2.5                          |     $0.30 |      $1.20 |    $0.0008 | 205K    | reasoning, agentic, tools                    |
| google/gemini-2.5-flash                       |     $0.30 |      $2.50 |    $0.0014 | 1M      | vision, tools                                |
| openai/gpt-4.1-mini                           |     $0.40 |      $1.60 |    $0.0010 | 128K    | tools                                        |
| google/gemini-3-flash-preview                 |     $0.50 |      $3.00 |    $0.0018 | 1M      | vision                                       |
| moonshot/kimi-k2.5                            |     $0.60 |      $3.00 |    $0.0018 | 262K    | reasoning, vision, agentic, tools            |
| moonshot/kimi-k2.6                            |     $0.95 |      $4.00 |    $0.0025 | 262K    | reasoning, vision, agentic, tools            |

### 中端模型（$0.001–$0.01/次请求）

| Model                       | Input $/M | Output $/M | ~$/request | Context | Features                          |
| --------------------------- | --------: | ---------: | ---------: | ------- | --------------------------------- |
| anthropic/claude-haiku-4.5  |     $1.00 |      $5.00 |    $0.0030 | 200K    | vision, agentic, tools            |
| zai/glm-5                   |     $1.00 |      $3.20 |    $0.0021 | 200K    | tools                             |
| openai/o1-mini              |     $1.10 |      $4.40 |    $0.0028 | 128K    | reasoning, tools                  |
| openai/o3-mini              |     $1.10 |      $4.40 |    $0.0028 | 128K    | reasoning, tools                  |
| openai/o4-mini              |     $1.10 |      $4.40 |    $0.0028 | 128K    | reasoning, tools                  |
| zai/glm-5-turbo             |     $1.20 |      $4.00 |    $0.0026 | 200K    | tools                             |
| google/gemini-2.5-pro       |     $1.25 |     $10.00 |    $0.0056 | 1M      | reasoning, vision, tools          |
| openai/gpt-5.2              |     $1.75 |     $14.00 |    $0.0079 | 400K    | reasoning, vision, agentic, tools |
| openai/gpt-5.3              |     $1.75 |     $14.00 |    $0.0079 | 128K    | reasoning, vision, agentic, tools |
| openai/gpt-5.3-codex        |     $1.75 |     $14.00 |    $0.0079 | 400K    | agentic, tools                    |
| openai/gpt-4.1              |     $2.00 |      $8.00 |    $0.0050 | 128K    | vision, tools                     |
| openai/o3                   |     $2.00 |      $8.00 |    $0.0050 | 200K    | reasoning, tools                  |
| google/gemini-3-pro-preview |     $2.00 |     $12.00 |    $0.0070 | 1M      | reasoning, vision, tools          |
| google/gemini-3.1-pro       |     $2.00 |     $12.00 |    $0.0070 | 1M      | reasoning, vision, tools          |
| xai/grok-2-vision           |     $2.00 |     $10.00 |    $0.0060 | 131K    | vision, tools                     |
| openai/gpt-4o               |     $2.50 |     $10.00 |    $0.0063 | 128K    | vision, agentic, tools            |
| openai/gpt-5.4              |     $2.50 |     $15.00 |    $0.0088 | 400K    | reasoning, vision, agentic, tools |

### 高端模型（$0.01+/次请求）

| Model                       | Input $/M | Output $/M | ~$/request | Context | Features                          |
| --------------------------- | --------: | ---------: | ---------: | ------- | --------------------------------- |
| anthropic/claude-sonnet-4.6 |     $3.00 |     $15.00 |    $0.0090 | 200K    | reasoning, vision, agentic, tools |
| xai/grok-3                  |     $3.00 |     $15.00 |    $0.0090 | 131K    | reasoning, tools                  |
| anthropic/claude-opus-4.8   |     $5.00 |     $25.00 |    $0.0150 | 1M      | reasoning, vision, agentic, tools |
| openai/gpt-5.5              |     $5.00 |     $30.00 |    $0.0175 | 1M      | reasoning, vision, agentic, tools |
| openai/o1                   |    $15.00 |     $60.00 |    $0.0375 | 200K    | reasoning, tools                  |
| openai/gpt-5.2-pro          |    $21.00 |    $168.00 |    $0.0945 | 400K    | reasoning, tools                  |
| openai/gpt-5.4-pro          |    $30.00 |    $180.00 |    $0.1050 | 400K    | reasoning, tools                  |

> **免费套餐：** 10 个模型完全免费——`/model free` 默认指向 gpt-oss-120b，或直接选择任意免费模型（例如使用 `/model deepseek-v4-pro` 进行推理、`/model nemotron-omni` 查看视觉内容、`/model qwen-thinking`、`/model deepseek-v4-flash` 获取 1M 上下文、`/model mistral-small`）。
> **最佳性价比：** `gpt-5-nano` 和 `gemini-2.5-flash-lite` 在约 $0.0003/次请求下表现优异。

---

## 支付

无需账号，无需 API 密钥。**支付即身份验证**，通过 [x402](https://x402.org) 实现。

```
Request → 402 (price: $0.003) → wallet signs USDC → retry → response
```

USDC 始终保留在你的钱包中直至花费——非托管模式。签名前，价格会显示在 402 响应头中。

**双链支持：** 可使用 Base (EVM) 或 Solana 上的 **USDC** 进行支付。首次运行时，两个钱包均由同一个 BIP-39 助记词派生。

```bash
/wallet              # 查看余额和地址（双链）
/wallet export       # 导出助记词 + 私钥用于备份
/wallet recover      # 在新设备上通过助记词恢复钱包
/wallet solana       # 切换至 Solana USDC 支付
/wallet base         # 切回 Base (EVM) USDC 支付
/chain solana        # /wallet solana 的别名
/stats               # 查看使用情况和节省金额
/stats clear         # 重置使用统计
/exclude             # 显示已排除的模型
/exclude add <model> # 阻止路由到指定模型（支持别名："grok-4", "free"）
/exclude remove <model> # 解除屏蔽
/exclude clear       # 清除所有排除项
```

**为你的钱包充值：**

- **Base (EVM)：** 向你的 EVM 地址发送 Base 网络上的 USDC
- **Solana：** 向你的 Solana 地址发送 Solana 网络上的 USDC
- **Coinbase/CEX：** 将 USDC 提现至上述任一网络
- **信用卡：** 请联系 [@bc1max on Telegram](https://t.me/bc1max)

---

## 截图演示

<table>
<tr>
<td width="50%" align="center">
<strong>智能路由实战</strong><br><br>
<img src="docs/clawrouter-savings.png" alt="ClawRouter savings" width="400">
</td>
<td width="50%" align="center">
<strong>Telegram 集成</strong><br><br>
<img src="assets/telegram-demo.png" alt="Telegram demo" width="400">
</td>
</tr>
</table>

---

## 配置

基础使用无需任何配置。高级选项如下：

| Variable                    | Default                               | Description             |
| --------------------------- | ------------------------------------- | ----------------------- |
| `BLOCKRUN_WALLET_KEY`       | auto-generated                        | Your wallet private key |
| `BLOCKRUN_PROXY_PORT`       | `8402`                                | Local proxy port        |
| `CLAWROUTER_DISABLED`       | `false`                               | Disable smart routing   |
| `CLAWROUTER_SOLANA_RPC_URL` | `https://api.mainnet-beta.solana.com` | Solana RPC endpoint     |

**完整参考：** [docs/configuration.md](docs/configuration.md)

### 模型排除

阻止路由到特定模型。如果某个模型未遵循你的 Agent 指令，或你想控制成本，此功能非常有用。

```bash
/exclude add nvidia/gpt-oss-120b   # 屏蔽默认免费模型
/exclude add grok-4                # 支持别名 —— 屏蔽所有 grok-4 变体
/exclude add gpt-5.4               # 跳过昂贵模型
/exclude                           # 查看当前排除项
/exclude remove grok-4             # 解除屏蔽
/exclude clear                     # 清除所有排除项
```

排除配置在重启后持久保存（`~/.openclaw/blockrun/exclude-models.json`）。如果某个层级中的所有模型都被排除，安全网机制会忽略该过滤器以确保路由不会中断。

---

## 故障排除

**遇到问题时，请运行诊断工具：**

```bash
npx @blockrun/clawrouter doctor
```

该命令将收集诊断信息并发送至 Claude Sonnet 进行 AI 驱动的分析：

```
🩺 BlockRun Doctor v0.12.24

System
  ✓ OS: darwin arm64
  ✓ Node: v20.11.0

Wallet
  ✓ Address: 0x1234...abcd
  ✓ Balance: $12.50

Network
  ✓ BlockRun API: reachable (142ms)
  ✗ Local proxy: not running on :8402

📤 Sending to Claude Sonnet 4.6 (~$0.003)...

🤖 AI Analysis:
The local proxy isn't running. Run `openclaw gateway restart` to fix.
```

**遇到复杂问题可使用 Opus：**

```bash
npx @blockrun/clawrouter doctor opus
```

**询问具体问题：**

```bash
npx @blockrun/clawrouter doctor "why is my request failing?"
npx @blockrun/clawrouter doctor opus "深度分析我的配置"
```

**费用：** Sonnet 约 $0.003（默认）| Opus 约 $0.01

---

## 开发

```bash
git clone https://github.com/BlockRunAI/ClawRouter.git
cd ClawRouter
npm install
npm run build
npm test
```

---

## 支持

| Channel               | Link                                                               |
| --------------------- | ------------------------------------------------------------------ |
| 📅 Schedule Demo      | [calendly.com/vickyfu9/30min](https://calendly.com/vickyfu9/30min) |
| 💬 Community Telegram | [t.me/blockrunAI](https://t.me/blockrunAI)                         |
| 🐦 X / Twitter        | [x.com/blockrunai](https://x.com/blockrunai)                       |
| 📱 Founder Telegram   | [@bc1max](https://t.me/bc1max)                                     |
| ✉️ Email              | vicky@blockrun.ai                                                  |

---

## BlockRun 生态系统

<table>
<tr>
<td width="50%">

### ⚡ ClawRouter

**专为自主 Agent 打造的 LLM 路由器**

你已在此。55+ 个模型、本地智能路由、x402 USDC 支付——唯一让 Agent 实现独立运行的技术栈。

`curl -fsSL https://blockrun.ai/ClawRouter-update | bash`

</td>
<td width="50%">

### 🤖 [BRCC](https://blockrun.ai/brcc.md)

**BlockRun for Claude Code**

在 Claude Code 中使用 50+ 个模型，无速率限制，无需 Anthropic 账号或手机号验证。按请求使用 USDC 支付——你的钱包即你的身份标识。

`curl -fsSL https://blockrun.ai/brcc-install | bash`

</td>
</tr>
<tr>
<td width="50%">

### 🐍 [ClawRouter-Hermes](https://github.com/BlockRunAI/ClawRouter-Hermes)

**ClawRouter for NousResearch Hermes**

Python 插件，将 ClawRouter 代理封装为 `hermes-agent` 使用。共享 55+ 个模型、Base & Solana 上的 x402 USDC 支付以及原生 Hermes 交互体验。

`pip install hermes-plugin-clawrouter`

</td>
<td width="50%">

<!-- next ecosystem entry goes here -->

</td>
</tr>
</table>

---

## 更多资源

| Resource                                               | Description              |
| ------------------------------------------------------ | ------------------------ |
| [Documentation](https://blockrun.ai/docs)              | Full docs                |
| [Model Pricing](https://blockrun.ai/models)            | All models & prices      |
| [Image Generation & Editing](docs/image-generation.md) | API examples, 5 models   |
| [Routing Profiles](docs/routing-profiles.md)           | ECO/AUTO/PREMIUM details |
| [Architecture](docs/architecture.md)                   | Technical deep dive      |
| [Configuration](docs/configuration.md)                 | Environment variables    |
| [Troubleshooting](docs/troubleshooting.md)             | Common issues            |

### 博客

| Article                                                                                            | Topic                                                   |
| -------------------------------------------------------------------------------------------------- | ------------------------------------------------------- |
| [11 Free AI Models, Zero Cost](docs/11-free-ai-models-zero-cost-blockrun.md)                       | How BlockRun gives developers top-tier LLMs for nothing |
| [ClawRouter Cuts LLM API Costs 500×](docs/clawrouter-cuts-llm-api-costs-500x.md)                   | Deep dive into cost savings                             |
| [ClawRouter vs OpenRouter](docs/clawrouter-vs-openrouter-llm-routing-comparison.md)                | Head-to-head comparison                                 |
| [Smart LLM Router: 14-Dimension Classifier](docs/smart-llm-router-14-dimension-classifier.md)      | How the routing engine works                            |
| [LLM Router Benchmark: 46 Models, Sub-1ms](docs/llm-router-benchmark-46-models-sub-1ms-routing.md) | Performance benchmarks                                  |
| [Anthropic Cost Savings](docs/anthropic-cost-savings.md)                                           | Reducing Claude API spend                               |

---

## 常见问题解答 (FAQ)

### ClawRouter 是什么？

ClawRouter 是一款开源（MIT 许可证）的智能 LLM 路由器，专为自主 AI Agent 打造。它会在本地对每个请求进行 15 个维度的分析，并在不到 1ms 的时间内将其路由到最便宜且具备处理能力的模型上——无需为路由决策发起任何外部 API 调用。

### ClawRouter 能节省多少 LLM 成本？

ClawRouter 的综合平均成本为 $2.05/百万 tokens，对比 Claude Opus 的 $25/百万 = **节省 92%**。实际节省比例取决于你的工作负载——简单查询会路由至免费模型（$0/次请求），复杂任务则分配高端模型。

### ClawRouter 与 OpenRouter 相比如何？

ClawRouter 开源且本地运行。它使用基于钱包的身份验证（无需 API 密钥）和按请求支付的 USDC（无需信用卡或订阅）。OpenRouter 需要账号、API 密钥和信用卡。此外，ClawRouter 具备智能路由功能——自动为每个请求选择最佳模型，而 OpenRouter 需手动选模。

### ClawRouter 与 LiteLLM 相比如何？

两者均开源且支持本地运行。但 ClawRouter 增加了智能路由（自动选模）、钱包身份验证和 USDC 支付。LiteLLM 需要你自带 API 密钥并手动选择模型。

### ClawRouter 兼容哪些 Agent？

ClawRouter 兼容任何发起 OpenAI 兼容 API 调用的工具——只需将请求指向 `http://localhost:8402`。这包括 continue.dev、Cursor、VS Code 扩展、ElizaOS 以及自定义 Agent。它还作为插件与 [OpenClaw](https://openclaw.ai)（一款 AI 编程 Agent）集成，从而启用斜杠命令和使用报告等额外功能。

### ClawRouter 免费吗？

ClawRouter 本身免费且采用 MIT 许可证开源。你仅需为通过它路由的 LLM API 调用付费——其中 10 款由 NVIDIA 托管的模型（`gpt-oss-120b`, `gpt-oss-20b`, `mistral-small-4-119b`, `deepseek-v4-pro`, `deepseek-v4-flash`, `qwen3-next-80b-a3b-thinking`, `qwen3-coder-480b`, `glm-4.7`, `llama-4-maverick`, `nemotron-3-nano-omni-30b-a3b-reasoning`）完全免费。使用 `/model free` 可在它们之间智能路由，或直接按名称选择任意一个。

---

<div align="center">

**MIT 许可证** · [BlockRun](https://blockrun.ai) —— 专为 Agent 打造的 AI 基础设施

⭐ 如果 ClawRouter 为你的 Agent 提供了强大支持，欢迎给仓库点个 Star！

</div>
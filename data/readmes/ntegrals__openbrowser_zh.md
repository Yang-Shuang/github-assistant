<h1 align="center">Open Browser</h1>

<p align="center">
  <b>基于 AI 的 TypeScript 自主网页浏览框架。</b>
</p>

<p align="center">
  <a href="https://github.com/ntegrals/openbrowser/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License"></a>
  <a href="https://github.com/ntegrals/openbrowser"><img src="https://img.shields.io/github/stars/ntegrals/openbrowser?style=social" alt="GitHub stars"></a>
</p>

<img src="./media/header.png" alt="Header"></a>

---

赋予 AI Agent（智能体）一个浏览器。它会点击、输入、导航并提取数据——自主在任何网站上完成任务。基于 Playwright 构建，原生支持 OpenAI、Anthropic 和 Google 模型。

> **自 v1.0 起已可用于生产环境。** 欢迎贡献代码。

## 为什么选择 Open Browser？

- **自主智能体**：用自然语言描述任务，AI 智能体会自动浏览网页完成操作——点击、输入、滚动和提取数据，无需手动编写脚本
- **多模型支持**：通过 Vercel AI SDK 开箱即用支持 OpenAI、Anthropic 和 Google——只需一个参数即可切换模型
- **交互式 REPL**：直接进入实时浏览器会话并交互执行命令——非常适合调试、原型开发和探索性操作
- **沙箱隔离运行**：在资源受限的环境中运行智能体，支持 CPU/内存监控、超时设置和域名限制
- **生产级就绪**：具备停滞检测、成本追踪、会话管理、回放录制及全面的错误处理机制
- **开源免费**：MIT 协议，完全可扩展，支持自带 API 密钥

## 快速开始

```bash
# Install dependencies
bun install

# Set up your API keys
cp .env.example .env
# Edit .env with your API keys

# Run an agent
bun run open-browser run "Find the top story on Hacker News and summarize it"

# Or open a browser interactively
bun run open-browser interactive
```

## 架构设计

Open Browser 是一个包含三个包的 Monorepo（单体仓库）：

| Package                     | Description                                                                |
| --------------------------- | -------------------------------------------------------------------------- |
| **`open-browser`**          | 核心库——智能体逻辑、浏览器控制、DOM 分析、LLM（大语言模型）集成             |
| **`@open-browser/cli`**     | 命令行界面，用于运行智能体和执行浏览器命令                                   |
| **`@open-browser/sandbox`** | 沙箱环境，提供资源限制与监控                                                 |

## CLI 命令

### 运行 AI 智能体

```bash
open-browser run <task> [options]
```

描述你需要完成的任务。其余细节由智能体自行规划。

```bash
# Search and extract information
open-browser run "Find the price of the MacBook Pro on apple.com"

# Fill out forms
open-browser run "Sign up for the newsletter on example.com with test@email.com"

# Multi-step workflows
open-browser run "Go to GitHub, find the open-browser repo, and star it"
```

| Option                       | Description                               |
| ---------------------------- | ----------------------------------------- |
| `-m, --model <model>`        | 使用的模型（默认：`gpt-4o`)          |
| `-p, --provider <provider>`  | 服务提供商：`openai`, `anthropic`, `google` |
| `--headless / --no-headless` | 显示或隐藏浏览器窗口                   |
| `--max-steps <n>`            | 智能体最大执行步数（默认：`25`)           |
| `-v, --verbose`              | 显示详细的步骤信息                   |
| `--no-cost`                  | 隐藏成本追踪信息                        |

### 浏览器命令

```bash
open-browser open <url>              # Open a URL
open-browser click <selector>        # Click an element
open-browser type <selector> <text>  # Type into an input
open-browser screenshot [output]     # Capture a screenshot
open-browser eval <expression>       # Run JavaScript on the page
open-browser extract <goal>          # Extract content as markdown
open-browser state                   # Show current URL, title, and tabs
open-browser sessions                # List active browser sessions
```

### 交互式 REPL

```bash
open-browser interactive
```

进入实时的 `browser>` 提示符，完全掌控浏览器：

```
browser> open https://news.ycombinator.com
browser> extract "top 5 stories with titles and points"
browser> click .morelink
browser> screenshot front-page.png
browser> help
```

## 作为库使用

```typescript
import { Agent, createViewport, createModel } from 'open-browser'

const viewport = await createViewport({ headless: true })
const model = createModel('openai', 'gpt-4o')

const agent = new Agent({
  viewport,
  model,
  task: 'Go to example.com and extract the main heading',
  settings: {
    stepLimit: 50,
    enableScreenshots: true,
  },
})

const result = await agent.run()
console.log(result)
```

### 沙箱隔离运行

在资源限制与监控下运行智能体：

```typescript
import { Sandbox } from '@open-browser/sandbox'

const sandbox = new Sandbox({
  timeout: 300_000, // 5 minute timeout
  maxMemoryMB: 512, // Memory limit
  allowedDomains: ['example.com'],
  stepLimit: 100,
  captureOutput: true,
})

const result = await sandbox.run({
  task: 'Complete the checkout form',
  model: languageModel,
})

console.log(result.metrics) // steps, URLs visited, CPU time
```

## 配置

### 环境变量

```bash
# LLM Provider Keys (at least one required)
OPENAI_API_KEY=sk-...
ANTHROPIC_API_KEY=sk-ant-...
GOOGLE_GENERATIVE_AI_API_KEY=...

# Browser
BROWSER_HEADLESS=true
BROWSER_DISABLE_SECURITY=false

# Recording & Debugging
OPEN_BROWSER_TRACE_PATH=./traces
OPEN_BROWSER_SAVE_RECORDING_PATH=./recordings
```

### 智能体配置

| Setting             | Default  | Description                               |
| ------------------- | -------- | ----------------------------------------- |
| `stepLimit`         | `100`    | 智能体最大迭代次数                  |
| `commandsPerStep`   | `10`     | 每次执行步数可采取的动作数量                    |
| `failureThreshold`  | `5`      | 连续失败多少次后停止      |
| `enableScreenshots` | `true`   | 是否在智能体上下文中包含页面截图 |
| `contextWindowSize` | `128000` | 对话使用的 Token（令牌）预算上限             |
| `allowedUrls`       | `[]`     | 限制导航仅访问指定 URL      |
| `blockedUrls`       | `[]`     | 禁止导航至指定 URL         |

### 视口配置

| Setting            | Default         | Description                                 |
| ------------------ | --------------- | ------------------------------------------- |
| `headless`         | `true`          | 在无头模式下运行浏览器（不显示窗口）          |
| `width` / `height` | `1280` / `1100` | 浏览器窗口尺寸                   |
| `relaxedSecurity`  | `false`         | 禁用浏览器安全特性           |
| `proxy`            | —               | 代理服务器配置                  |
| `cookieFile`       | —               | 用于持久化会话的 Cookie 文件路径 |

## 工作原理

```
                    ┌─────────────┐
  "Book a flight"   │             │
  ───────────────►  │    Agent    │  ◄── LLM (OpenAI / Anthropic / Google)
                    │             │
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │   Commands  │  click, type, scroll, extract, navigate...
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │  Viewport   │  Playwright browser instance
                    └──────┬──────┘
                           │
                    ┌──────▼──────┐
                    │  DOM / Page │  Snapshot, interactive elements, content
                    └─────────────┘
```

1. 你用自然语言描述一个**任务**
2. **智能体（Agent）**将当前页面状态与任务发送给 LLM
3. LLM 决定执行哪些**命令**（点击、输入、导航、提取...）
4. 命令在 **视口（Viewport）**（Playwright 浏览器实例）上执行
5. 智能体观察结果，检测是否停滞，并循环执行直到任务完成

## 模型支持

| Provider      | Example Models                                  | Flag           |
| ------------- | ----------------------------------------------- | -------------- |
| **OpenAI**    | `gpt-4o`, `gpt-4o-mini`, `o1`                   | `-p openai`    |
| **Anthropic** | `claude-sonnet-4-5-20250929`, `claude-opus-4-6` | `-p anthropic` |
| **Google**    | `gemini-2.0-flash`, `gemini-2.5-pro`            | `-p google`    |

## 项目结构

```
packages/
├── core/                    # Core library (open-browser)
│   └── src/
│       ├── agent/           # Agent logic, conversation, stall detection
│       ├── commands/        # Action schemas and executor (25+ commands)
│       ├── viewport/        # Browser control, events, guards
│       ├── page/            # DOM analysis, content extraction
│       ├── model/           # LLM adapter and message formatting
│       ├── metering/        # Cost tracking
│       ├── bridge/          # IPC server/client
│       └── config/          # Configuration types
├── cli/                     # CLI (@open-browser/cli)
│   └── src/
│       ├── commands/        # CLI command implementations
│       └── index.ts         # Entry point
└── sandbox/                 # Sandbox (@open-browser/sandbox)
    └── src/
        └── sandbox.ts       # Resource-limited execution
```

## 开发指南

```bash
# Install dependencies
bun install

# Type check
bun run build

# Run tests
bun run test

# Lint
bun run lint

# Format
bun run format
```

## 贡献代码

欢迎提交 PR！详细规范请参阅 [CONTRIBUTING.md](.github/CONTRIBUTING.md)。

## 许可证

[MIT](LICENSE)
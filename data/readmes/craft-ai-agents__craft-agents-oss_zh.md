# Craft Agents

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![Contributor Covenant](https://img.shields.io/badge/Contributor%20Covenant-2.1-4baaaa.svg)](CODE_OF_CONDUCT.md)

## 工作原理（视频）
要了解 Craft Agents 的功能及工作原理，请观看此视频。

[![Demo Video](https://img.youtube.com/vi/xQouiAIilvU/hqdefault.jpg)](https://www.youtube.com/watch?v=xQouiAIilvU)

[点击此处（或上方图片）在 YouTube 上观看视频 →](https://www.youtube.com/watch?v=xQouiAIilvU)


## 为什么构建 Craft Agents
Craft Agents 是我们（craft.do 团队）开发的一款工具，旨在让你能够高效地与 AI Agent 协作。它支持直观的 multitasking（多任务处理）、无缝连接任意 API 或服务、共享会话，并提供以文档为核心（而非代码）的工作流——全部呈现在美观流畅的界面中。

它并排使用 Claude Agent SDK 和 Pi SDK，在保留我们认可的优秀特性的基础上，优化了期望改进的部分。

它是基于 Agent Native（Agent 原生）软件原则构建的，开箱即用且高度可定制，属于同类产品中的先驱之一。

Craft Agents 以 Apache 2.0 许可证开源——你可以自由修改、更改任何内容，且这完全可行。我们仅使用 Craft Agents（不借助代码编辑器）来开发它本身，因此实际上，任何定制都只需一个 prompt（提示词）。

我们构建 Craft Agents，是因为希望有更好的、更具指导性的（最好是非 CLI 方式）方法来使用世界上最强大的 Agent。我们将基于经验和直觉持续改进它。

<img width="1578" height="894" alt="image" src="https://github.com/user-attachments/assets/3f1f2fe8-7cf6-4487-99ff-76f6c8c0a3fb" />

## 令人惊叹的“开箱即用”功能

**如何连接 Linear、Gmail、Slack？**
告诉 Agent “将 Linear 添加为数据源”。它会查找公共 API 和 MCP 服务器，阅读其文档，配置凭据并设置一切。无需配置文件，也无需引导向导。

[查看我如何刚刚连接 Slack →](https://agents.craft.do/s/DRNQEiy8w2e1v5LPgKl8b)

**我已经准备好了 MCP 的 JSON 配置。**
粘贴即可。其余工作由 Agent 自动完成。

**本地 MCP 呢？**
完全支持。基于 stdio 的 MCP 服务器会在你的机器上作为本地子进程运行。指向一个 npx 命令、Python 脚本或任何本地二进制文件即可，它都能正常工作。

**能处理自定义 API 吗？**
可以。粘贴 OpenAPI 规范、一些端点 URL、文档截图或任何你拥有的内容即可。它能自行解析并引导你完成后续步骤。

**也能连接 API？不只是 MCP？**
Craft Agents 可连接任意服务。我们已将其直连至跳板机后的 PostgreSQL 数据库。Skills（技能）+ Sources（数据源）= 魔法。

**如何导入我的 Claude Code Skills 和 MCP？**
告诉 Agent 你想从 Claude Code 导入 Skills，它会处理迁移工作。

[这里我一次性导入了所有技能 →](https://agents.craft.do/s/gWCFqwhObFWaNJIEJmd6j)

**如何创建新 Skill？**
描述该 Skill 应执行的操作并提供上下文，Agent 会处理其余部分。

**修改后需要重启吗？**
不需要。所有更改即时生效。在对话中途使用 `@` 提及新 Skill 或数据源即可。

**所以我可以直接问它任何问题？**
是的。这正是 Agent Native（Agent 原生）软件的核心思想。你描述需求，它自行规划实现路径。这才是 Token 的正确用法。


## 安装

### 一键安装（推荐）

**macOS / Linux：**
```bash
curl -fsSL https://agents.craft.do/install-app.sh | bash
```

**Windows (PowerShell)：**
```powershell
irm https://agents.craft.do/install-app.ps1 | iex
```

### 从源码构建

```bash
git clone https://github.com/lukilabs/craft-agents-oss.git
cd craft-agents-oss
bun install
bun run electron:start
```

## 功能特性

- **多会话收件箱**：桌面应用，支持会话管理、状态工作流和标记功能
- **类 Claude Code 体验**：流式响应、工具可视化、实时更新
- **多 LLM 连接**：添加多个 AI 提供商，并设置工作区默认值
- **多模型支持**：支持与 Anthropic 并列使用 Google AI Studio、ChatGPT Plus、GitHub Copilot 或 OpenAI API Key 运行会话
- **Craft MCP 集成**：可访问 30+ Craft 文档工具（区块、集合、搜索、任务）
- **数据源（Sources）**：连接 MCP 服务器、REST API（Google、Slack、Microsoft）和本地文件系统
- **权限模式（Permission Modes）**：三级系统（探索/只读、请求编辑、自动），支持自定义规则
- **后台任务**：运行长时间操作并跟踪进度
- **动态状态系统**：可自定义会话工作流状态（待办、进行中、需审核、已完成等）
- **主题系统**：应用级与工作区级级联主题
- **多文件差异对比**：类 VS Code 窗口，用于查看单次交互中的所有文件变更
- **技能（Skills）**：按工作区存储的专用 Agent 指令
- **文件附件**：拖放图片、PDF、Office 文档并自动转换
- **自动化（Automations）**：事件驱动自动化——在标签变更、定时任务、工具调用等场景下创建 Agent 会话

## 快速开始

1. **启动应用**后安装完成的应用程序
2. **选择 API 连接**：使用 Anthropic（API Key 或 Claude Max/Pro）、Google AI Studio、ChatGPT Plus（Codex OAuth）或 GitHub Copilot OAuth
3. **创建工作区**：设置工作区以组织你的会话
4. **连接数据源（可选）**：添加 MCP 服务器、REST API 或本地文件系统
5. **开始对话**：创建会话并与 Claude 交互

## 桌面应用功能

### 会话管理

- **收件箱/归档**：按工作流状态组织会话
- **标记（Flagging）**：标记重要会话以便快速访问
- **状态工作流**：待办 → 进行中 → 需审核 → 已完成
- **会话命名**：AI 自动生成标题或手动命名
- **会话持久化**：完整对话历史保存至磁盘

### 数据源（Sources）

将外部数据源连接到你的工作区：

| 类型 | 示例 |
|------|----------|
| **MCP 服务器** | Craft、Linear、GitHub、Notion、自定义服务器 |
| **REST API** | Google（Gmail、日历、云端硬盘、YouTube、搜索控制台）、Slack、Microsoft |
| **本地文件** | 文件系统、Obsidian 库、Git 仓库 |

### 权限模式（Permission Modes）

| 模式 | 显示名称 | 行为 |
|------|---------|----------|
| `safe` | Explore（探索） | 只读，阻止所有写入操作 |
| `ask` | Ask to Edit（请求编辑） | 提示审批（默认） |
| `allow-all` | Auto（自动） | 自动批准所有命令 |

在聊天界面中使用 **SHIFT+TAB** 循环切换模式。

### 键盘快捷键

| 快捷键 | 操作 |
|----------|--------|
| `Cmd+N` | 新建聊天 |
| `Cmd+1/2/3` | 聚焦侧边栏/列表/聊天区 |
| `Cmd+/` | 快捷键对话框 |
| `SHIFT+TAB` | 循环切换权限模式 |
| `Enter` | 发送消息 |
| `Shift+Enter` | 换行 |

## 远程服务器（无头模式）

Craft Agents 可作为无头服务器在远程机器（如 Linux VPS）上运行，桌面应用作为轻量客户端连接。这让你能够保持长时间运行的会话存活、从多台设备访问它们，并在高性能服务器上执行计算密集型任务。

### 快速开始

在 monorepo 根目录下：

```bash
# Generate a token and start the server
CRAFT_SERVER_TOKEN=$(openssl rand -hex 32) bun run packages/server/src/index.ts
```

服务器启动时会打印连接信息：

```
CRAFT_SERVER_URL=ws://203.0.113.5:9100
CRAFT_SERVER_TOKEN=<generated-token>
```

复制这些值，用于连接桌面应用。

### 连接桌面应用

通过传递服务器 URL 和 Token 以轻量客户端模式启动 Electron 应用：

```bash
CRAFT_SERVER_URL=wss://203.0.113.5:9100 CRAFT_SERVER_TOKEN=<token> bun run electron:start
```

在轻量客户端模式下，桌面应用仅负责渲染界面，所有会话逻辑、工具执行和 LLM 调用均在远程服务器上运行。

### 环境变量

| 变量名 | 是否必需 | 默认值 | 说明 |
|----------|----------|---------|-------------|
| `CRAFT_SERVER_TOKEN` | Yes | — | Bearer token for client authentication（客户端认证的 Bearer Token） |
| `CRAFT_RPC_HOST` | No | `127.0.0.1` | Bind address (`0.0.0.0` for remote access)（绑定地址，远程访问请使用 `0.0.0.0`） |
| `CRAFT_RPC_PORT` | No | `9100` | Bind port（绑定端口） |
| `CRAFT_RPC_TLS_CERT` | No | — | Path to PEM certificate file (enables `wss://`)（PEM 证书文件路径，启用 `wss://`） |
| `CRAFT_RPC_TLS_KEY` | No | — | Path to PEM private key file (required with cert)（PEM 私钥文件路径，需与证书配合使用） |
| `CRAFT_RPC_TLS_CA` | No | — | Path to PEM CA chain file (optional, for client cert verification)（PEM CA 链文件路径，可选，用于客户端证书验证） |
| `CRAFT_DEBUG` | No | `false` | Enable debug logging（启用调试日志） |

### TLS（推荐用于远程访问）

当通过网络暴露服务器时，TLS 会加密 WebSocket 连接（使用 `wss://` 替代 `ws://`）。

**生成自签名证书（开发/测试）：**

```bash
./scripts/generate-dev-cert.sh
# Creates certs/cert.pem and certs/key.pem (valid 365 days)
```

**启动带 TLS 的服务器：**

```bash
CRAFT_SERVER_TOKEN=<token> \
CRAFT_RPC_HOST=0.0.0.0 \
CRAFT_RPC_TLS_CERT=certs/cert.pem \
CRAFT_RPC_TLS_KEY=certs/key.pem \
bun run packages/server/src/index.ts
```

服务器将打印 `CRAFT_SERVER_URL=wss://<your-public-ip>:9100`。

**生产环境**建议使用受信任的 CA 颁发的证书（如 Let's Encrypt），或将服务器置于终止 TLS 的反向代理（nginx、Caddy）之后。

### Docker

```bash
docker run -d \
  -p 9100:9100 \
  -e CRAFT_SERVER_TOKEN=<token> \
  -e CRAFT_RPC_HOST=0.0.0.0 \
  -v craft-data:/root/.craft-agent \
  craft-agents-server
```

要在 Docker 中启用 TLS，请挂载证书并设置环境变量：

```bash
docker run -d \
  -p 9100:9100 \
  -e CRAFT_SERVER_TOKEN=<token> \
  -e CRAFT_RPC_HOST=0.0.0.0 \
  -e CRAFT_RPC_TLS_CERT=/certs/cert.pem \
  -e CRAFT_RPC_TLS_KEY=/certs/key.pem \
  -v ./certs:/certs:ro \
  -v craft-data:/root/.craft-agent \
  craft-agents-server
```

## CLI 客户端

一个通过 WebSocket（`ws://` 或 `wss://`）连接到运行中 Craft Agent 服务器的终端客户端。适用于脚本编写、CI/CD 流水线、服务器验证，或偏好命令行操作时。

### 安装

```bash
# From the monorepo (requires Bun)
bun run apps/cli/src/index.ts --help

# Or add to your PATH
alias craft-cli="bun run $(pwd)/apps/cli/src/index.ts"
```

### 连接

CLI 通过参数标志或环境变量读取连接信息：

```bash
# Via environment (set once)
export CRAFT_SERVER_URL=ws://127.0.0.1:9100
export CRAFT_SERVER_TOKEN=<your-token>

# Or via flags
craft-cli --url ws://127.0.0.1:9100 --token <token> ping
```

对于 TLS 连接（`wss://`），请使用 `--tls-ca <path>` 指定自签名证书。

### 命令

| Command | Description |
|---------|-------------|
| `ping` | Verify connectivity (clientId + latency) |
| `health` | Check credential store health |
| `versions` | Show server runtime versions |
| `workspaces` | List workspaces |
| `sessions` | List sessions in workspace |
| `connections` | List LLM connections |
| `sources` | List configured sources |
| `session create` | Create a session (`--name`, `--mode`) |
| `session messages <id>` | Print session message history |
| `session delete <id>` | Delete a session |
| `send <id> <message>` | Send message and stream AI response |
| `cancel <id>` | Cancel in-progress processing |
| `invoke <channel> [args]` | Raw RPC call with JSON args |
| `listen <channel>` | Subscribe to push events (Ctrl+C to stop) |
| `run <prompt>` | Self-contained: spawn server, run prompt, stream response, exit |
| `--validate-server` | 21-step integration test (auto-spawns server if no `--url`) |

#### run 命令参数

| Flag | Default | Description |
|------|---------|-------------|
| `--workspace-dir <path>` | — | Register a workspace directory before running |
| `--source <slug>` | — | Enable a source (repeatable) |
| `--output-format <fmt>` | `text` | Output format: `text` or `stream-json` |
| `--mode <mode>` | `allow-all` | Permission mode for the session |
| `--no-cleanup` | `false` | Skip session deletion on exit |
| `--server-entry <path>` | — | Custom server entry point |
| `--provider <name>` | `anthropic` | LLM provider (`anthropic`, `openai`, `google`, `openrouter`, `groq`, `mistral`, `xai`, etc.) |
| `--model <id>` | (provider default) | Model ID (e.g., `claude-sonnet-4-5-20250929`, `gpt-4o`, `gemini-2.0-flash`) |
| `--api-key <key>` | — | API key (or `$LLM_API_KEY`, or provider-specific env var) |
| `--base-url <url>` | — | Custom API endpoint for proxies or self-hosted models |

`run` 命令完全独立——它会启动无头服务器、创建会话、发送提示词、流式输出响应并退出。无需单独设置服务器。API Key 的优先级为：`--api-key` > `$LLM_API_KEY` > 特定于提供商的环境变量（如 `$ANTHROPIC_API_KEY`、`$OPENAI_API_KEY`）。

### 示例

```bash
# Quick connectivity check
craft-cli ping

# List sessions (human-readable)
craft-cli sessions

# Send a message and stream the AI response
craft-cli send abc-123 "What files are in the current directory?"

# Pipe input
echo "Summarize this" | craft-cli send abc-123

# JSON output for scripting
craft-cli --json workspaces | jq '.[].name'

# Self-contained run (spawns its own server)
craft-cli run "Summarize the README"
craft-cli run --workspace-dir ./my-project --source github "List open PRs"

# Multi-provider support
craft-cli run --provider openai --model gpt-4o "Summarize this repo"
GOOGLE_API_KEY=... craft-cli run --provider google --model gemini-2.0-flash "Hello"
craft-cli run --provider anthropic --base-url https://openrouter.ai/api/v1 --api-key $OR_KEY "Hello"

# Validate the server (auto-spawns if no --url)
craft-cli --validate-server
craft-cli --validate-server --url ws://127.0.0.1:9100 --token <token>
```

## 架构

```
craft-agent/
├── apps/
│   ├── cli/                   # Terminal client (CLI)
│   └── electron/              # Desktop GUI (primary)
│       └── src/
│           ├── main/          # Electron main process
│           ├── preload/       # Context bridge
│           └── renderer/      # React UI (Vite + shadcn)
└── packages/
    ├── core/                  # Shared types
    └── shared/                # Business logic
        └── src/
            ├── agent/         # CraftAgent, permissions
            ├── auth/          # OAuth, tokens
            ├── config/        # Storage, preferences, themes
            ├── credentials/   # AES-256-GCM encrypted storage
            ├── sessions/      # Session persistence
            ├── sources/       # MCP, API, local sources
            └── statuses/      # Dynamic status system
```

## 开发环境

```bash
# Hot reload development
bun run electron:dev

# Build and run
bun run electron:start

# Type checking
bun run typecheck:all

# Debug logging (writes to ~/Library/Logs/@craft-agent/electron/)
# Logs are automatically enabled in development
```

### 环境变量

OAuth 集成（Slack、Microsoft）需要将凭据打包到构建中。创建 `.env` 文件：

```bash
MICROSOFT_OAUTH_CLIENT_ID=your-client-id
SLACK_OAUTH_CLIENT_ID=your-slack-client-id
SLACK_OAUTH_CLIENT_SECRET=your-slack-client-secret
```

**注意：** Google OAuth 凭据**不会**打包到构建中。用户需通过数据源配置自行提供凭据。详见下方的 [Google OAuth 设置](#google-oauth-setup-gmail-calendar-drive) 部分。

### Google OAuth 设置（Gmail、日历、云端硬盘、YouTube、搜索控制台）

Google 集成需要你自行创建 OAuth 凭据。此为一次性配置。

#### 1. 创建 Google Cloud 项目

1. 前往 [Google Cloud Console](https://console.cloud.google.com)
2. 创建新项目（或选择现有项目）
3. 记录你的 Project ID

#### 2. 启用所需 API

前往 **APIs & Services → Library** 并启用你需要的 API：
- **Gmail API** - for email integration
- **Google Calendar API** - for calendar integration
- **Google Drive API** - for file storage integration

#### 3. 配置 OAuth Consent Screen

1. 前往 **APIs & Services → OAuth consent screen**
2. 选择 **External** user type（除非你拥有 Google Workspace）
3. 填写必填字段：
   - App name: e.g., "My Craft Agent"
   - User support email: your email
   - Developer contact: your email
4. Add scopes (optional - can leave default)
5. Add yourself as a test user (required for External apps in testing mode)
6. Complete the wizard

#### 4. 创建 OAuth Credentials

1. 前往 **APIs & Services → Credentials**
2. Click **Create Credentials → OAuth Client ID**
3. Application type: **Desktop app**
4. Name: e.g., "Craft Agent Desktop"
5. Click **Create**
6. Note the **Client ID** and **Client Secret**

#### 5. 在 Craft Agent 中配置

设置 Google 数据源（Gmail、日历、云端硬盘等）时，将以下字段添加到数据源的 `config.json`：

```json
{
  "api": {
    "googleService": "gmail",
    "googleOAuthClientId": "your-client-id.apps.googleusercontent.com",
    "googleOAuthClientSecret": "your-client-secret"
  }
}
```

或者只需告诉 Agent 你想连接 Gmail/日历/云端硬盘——它会引导你完成凭据输入。

#### 安全须知

- Your OAuth credentials are stored encrypted alongside other source credentials
- Never commit credentials to version control
- For production use, consider getting your OAuth consent screen verified by Google

## 支持的 LLM 提供商

Craft Agents 支持多种连接 LLM 提供商的方式：

### 直连方式

| Provider | Auth | Notes |
|----------|------|-------|
| **Anthropic** | API key or Claude Max/Pro OAuth | Direct Claude connection via the Claude Agent SDK |
| **Google AI Studio** | API key | Gemini models with native Google Search grounding built in |
| **ChatGPT Plus / Pro** | Codex OAuth | Sign in with your ChatGPT subscription — uses OpenAI's Codex models |
| **GitHub Copilot** | OAuth (device code) | One-click authentication with your Copilot subscription |

### 第三方与自托管提供商

通过选择自定义端点，可通过 **Claude / Anthropic API Key** 连接支持更多提供商：

| Provider | Endpoint | Notes |
|----------|----------|-------|
| **OpenRouter** | `https://openrouter.ai/api` | Access Claude, GPT, Llama, Gemini, and hundreds of other models through a single API key. Use `provider/model-name` format (e.g. `anthropic/claude-opus-4.7`). |
| **Vercel AI Gateway** | `https://ai-gateway.vercel.sh` | Route requests through Vercel's AI Gateway with built-in observability and caching. |
| **Ollama** | `http://localhost:11434` | Run open-source models locally. No API key required. |
| **Custom** | Any URL | Any OpenAI-compatible or Anthropic-compatible endpoint. |

### 架构

Craft Agents 使用两个 Agent 后端：

- **Claude** —— 基于 [Claude Agent SDK](https://www.npmjs.com/package/@anthropic-ai/claude-agent-sdk) 构建，原生支持自定义基础 URL 和提供商路由。Anthropic API Key、Claude Max/Pro OAuth 及所有第三方端点均使用此后端。
- **Pi** —— 基于 Pi SDK 构建，负责处理 Google AI Studio、ChatGPT Plus（Codex OAuth）、GitHub Copilot OAuth 和 OpenAI API Key 连接。Pi 连接通过其专属提供商基础设施路由。

## 配置

配置文件存储于 `~/.craft-agent/`：

```
~/.craft-agent/
├── config.json              # Main config (workspaces, LLM connections)
├── credentials.enc          # Encrypted credentials (AES-256-GCM)
├── preferences.json         # User preferences
├── theme.json               # App-level theme
└── workspaces/
    └── {id}/
        ├── config.json      # Workspace settings
        ├── theme.json       # Workspace theme override
        ├── automations.json  # Event-driven automations
        ├── sessions/        # Session data (JSONL)
        ├── sources/         # Connected sources
        ├── skills/          # Custom skills
        └── statuses/        # Status configuration
```

### 自动化（Automations）

自动化功能允许你在事件触发时执行操作，从而实现工作流自动化——例如标签变更、会话启动、工具运行或定时任务。

**直接询问 Agent：**
- "Set up a daily standup briefing every weekday at 9am"
- "Notify me when a session is labelled urgent"
- "Track permission mode changes and summarise them"
- "Every Friday at 5pm, summarise this week's completed tasks"

或在 `~/.craft-agent/workspaces/{id}/automations.json` 中手动配置：

```json
{
  "version": 2,
  "automations": {
    "SchedulerTick": [
      {
        "cron": "0 9 * * 1-5",
        "timezone": "America/New_York",
        "labels": ["Scheduled"],
        "actions": [
          { "type": "prompt", "prompt": "Check @github for new issues assigned to me" }
        ]
      }
    ],
    "LabelAdd": [
      {
        "matcher": "^urgent$",
        "actions": [
          { "type": "prompt", "prompt": "An urgent label was added. Triage the session and summarise what needs attention." }
        ]
      }
    ]
  }
}
```

**提示词操作（Prompt actions）** 会创建一个新的 Agent 会话并传入提示词。支持对数据源和 Skill 使用 `@提及`，且 `$CRAFT_LABEL`、`$CRAFT_SESSION_ID` 等环境变量会自动展开。

**支持的事件：** `LabelAdd`、`LabelRemove`、`PermissionModeChange`、`FlagChange`、`SessionStatusChange`、`SchedulerTick`、`PreToolUse`、`PostToolUse`、`SessionStart`、`SessionEnd` 等。

详见 [自动化文档](https://agents.craft.do/docs/automations/overview)。

## 高级功能

### 大响应处理

长度超过约 60KB 的工具响应会自动使用 Claude Haiku 进行摘要生成，并结合意图感知上下文。系统会在 MCP 工具模式中注入 `_intent` 字段，以保持摘要的聚焦性。

### 深度链接（Deep Linking）

外部应用可通过 `craftagents://` URL 进行导航：

```
craftagents://allSessions                      # All sessions view
craftagents://allSessions/session/session123   # Specific session
craftagents://settings                         # Settings
craftagents://sources/source/github            # Source info
craftagents://action/new-chat                  # Create new session
```

## 技术栈

| Layer | Technology |
|-------|------------|
| Runtime | [Bun](https://bun.sh/) |
| AI | [@anthropic-ai/claude-agent-sdk](https://www.npmjs.com/package/@anthropic-ai/claude-agent-sdk) |
| AI (Pi) | Pi SDK agent server |
| Desktop | [Electron](https://www.electronjs.org/) + React |
| UI | [shadcn/ui](https://ui.shadcn.com/) + Tailwind CSS v4 |
| Build | esbuild (main) + Vite (renderer) |
| Credentials | AES-256-GCM encrypted file storage |

## 故障排除

### 调试模式

要以详细日志模式启动打包后的应用，请使用 `-- --debug`（注意双横线分隔符）：

**macOS：**
```bash
/Applications/Craft\ Agents.app/Contents/MacOS/Craft\ Agents -- --debug
```

**Windows (PowerShell)：**
```powershell
& "$env:LOCALAPPDATA\Programs\@craft-agentelectron\Craft Agents.exe" -- --debug
```

**Linux：**
```bash
./craft-agents -- --debug
```

日志写入位置：
- **macOS：** `~/Library/Logs/@craft-agent/electron/main.log`
- **Windows：** `%APPDATA%\@craft-agent\electron\logs\main.log`
- **Linux：** `~/.config/@craft-agent/electron/logs/main.log`

## 许可证

本项目采用 Apache License 2.0 开源协议——详见 [LICENSE](LICENSE) 文件。

### 第三方许可证

本项目使用了 [Claude Agent SDK](https://www.npmjs.com/package/@anthropic-ai/claude-agent-sdk)，其受 [Anthropic 商业服务条款](https://www.anthropic.com/legal/commercial-terms) 约束。

### 商标

“Craft”和“Craft Agents”是 Craft Docs Ltd. 的注册商标。使用指南详见 [TRADEMARK.md](TRADEMARK.md)。

## 贡献代码

欢迎贡献！请参阅 [CONTRIBUTING.md](CONTRIBUTING.md) 获取指南。

## 安全性

### 本地 MCP 服务器隔离

当启动本地 MCP 服务器（stdio 传输）时，敏感环境变量会被过滤，以防止凭据泄露至子进程。被屏蔽的变量包括：

- `ANTHROPIC_API_KEY`, `CLAUDE_CODE_OAUTH_TOKEN` (app auth)
- `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `AWS_SESSION_TOKEN`
- `GITHUB_TOKEN`, `GH_TOKEN`, `OPENAI_API_KEY`, `GOOGLE_API_KEY`, `STRIPE_SECRET_KEY`, `NPM_TOKEN`

如需向特定 MCP 服务器显式传递环境变量，请在数据源配置中使用 `env` 字段。

如发现安全漏洞，请参阅 [SECURITY.md](SECURITY.md)。
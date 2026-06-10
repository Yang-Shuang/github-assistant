<p align="center">
  <img src="packages/website/public/logo.svg" width="64" height="64" alt="Paseo logo">
</p>

<h1 align="center">Paseo</h1>

<p align="center">
  <a href="https://github.com/getpaseo/paseo/stargazers">
    <img src="https://img.shields.io/github/stars/getpaseo/paseo?style=flat&logo=github" alt="GitHub stars">
  </a>
  <a href="https://github.com/getpaseo/paseo/releases">
    <img src="https://img.shields.io/github/v/release/getpaseo/paseo?style=flat&logo=github" alt="GitHub release">
  </a>
  <a href="https://x.com/moboudra">
    <img src="https://img.shields.io/badge/%40moboudra-555?logo=x" alt="X">
  </a>
  <a href="https://discord.gg/jz8T2uahpH">
    <img src="https://img.shields.io/badge/Discord-555?logo=discord" alt="Discord">
  </a>
  <a href="https://www.reddit.com/r/PaseoAI/">
    <img src="https://img.shields.io/badge/Reddit-555?logo=reddit" alt="Reddit">
  </a>
</p>

<p align="center">一个整合了 Claude Code、Codex、Copilot、OpenCode 和 Pi agent（智能体）的统一界面。</p>

<p align="center">
  <img src="https://paseo.sh/hero-mockup.png" alt="Paseo app screenshot" width="100%">
</p>

<p align="center">
  <img src="https://paseo.sh/mobile-mockup.png" alt="Paseo mobile app" width="100%">
</p>

---

在你的本地机器上并行运行多个 agent，随时随地通过手机或桌面端完成开发并交付代码。

- **自托管（Self-hosted）：** Agent 在你的本地机器上运行，完整保留你的开发环境、工具链、配置和个人技能。
- **多模型支持：** 通过统一界面接入 Claude Code、Codex、Copilot、OpenCode 和 Pi，按需为不同任务选择合适的模型。
- **语音控制：** 在语音模式下口述任务或讨论问题，解放双手。
- **跨设备支持：** 覆盖 iOS、Android、桌面端、网页和 CLI。在电脑开始工作，用手机随时查看进度，或在终端编写脚本自动化流程。
- **隐私优先：** Paseo 不收集任何遥测数据（telemetry）、追踪信息，也不强制要求登录账号。

## Getting Started

Paseo 会运行一个名为 daemon（守护进程）的本地服务器来管理你的编程 agent。桌面端、移动端、网页端和 CLI 等客户端均通过该服务进行连接。

### Prerequisites

你需要至少安装并配置好一个 agent CLI，并完成凭据设置：

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code)
- [Codex](https://github.com/openai/codex)
- [GitHub Copilot](https://github.com/features/copilot/cli/)
- [OpenCode](https://github.com/anomalyco/opencode)
- [Pi](https://pi.dev)

### Desktop app (recommended)

从 [下载页面](https://paseo.sh/download) 或 [GitHub releases 页面](https://github.com/getpaseo/paseo/releases) 获取。打开应用后，daemon 会自动启动，无需额外安装其他组件。

如需通过手机连接，请在设置中扫描显示的二维码。

### CLI / headless

安装 CLI 并启动 Paseo：

```bash
npm install -g @getpaseo/cli
paseo
```

终端将显示一个二维码。你可以通过任意客户端进行连接。该方式特别适用于服务器和远程机器。

完整安装与配置指南请参阅：

- [Docs](https://paseo.sh/docs)
- [Configuration reference](https://paseo.sh/docs/configuration)

## CLI

应用内支持的所有功能，均可通过终端命令行完成。

```bash
paseo run --provider claude/opus-4.6 "implement user authentication"
paseo run --provider codex/gpt-5.4 --worktree feature-x "implement feature X"

paseo ls                           # list running agents
paseo attach abc123                # stream live output
paseo send abc123 "also add tests" # follow-up task

# run on a remote daemon
paseo --host workstation.local:6767 run "run the full test suite"
```

更多详情请参阅 [完整 CLI 参考文档](https://paseo.sh/docs/cli)。

## Skills

Skills（技能）可教会你的 agent 使用 Paseo 来编排其他 agent。

```bash
npx skills add getpaseo/paseo
```

随后在任何 agent 对话中即可调用：

- `/paseo-handoff` — 在不同 agent 之间交接任务。我通常用它与 Claude 进行规划，然后将实现工作交给 Codex。
- `/paseo-loop` — 让 agent 根据明确的验收标准循环执行任务（即 Ralph loops），可选择搭配验证器使用。
- `/paseo-advisor` — 启动单个 agent 作为顾问提供第二意见，而不将实际工作委托给它。
- `/paseo-committee` — 组建由两个观点不同的 agent 组成的“委员会”，用于跳出当前视角、进行根本原因分析并生成计划。

## Development

Monorepo 包结构速览：

- `packages/server`: Paseo daemon（负责 agent 进程编排、WebSocket API 和 MCP server）
- `packages/app`: Expo client（支持 iOS、Android、Web）
- `packages/cli`: `paseo` CLI，用于管理 daemon 和 agent 工作流
- `packages/desktop`: Electron desktop app
- `packages/relay`: Relay package，负责远程连接
- `packages/website`: Marketing site and documentation (`paseo.sh`)

常用命令：

```bash
# run all local dev services
npm run dev

# run individual surfaces
npm run dev:server
npm run dev:app
npm run dev:desktop
npm run dev:website

# build the server stack
npm run build:server

# repo-wide checks
npm run typecheck
```

## Community

- [paseo-relay](https://github.com/zenghongtu/paseo-relay) — 使用 Go 语言实现的自托管 relay 服务

### Self-hosted relay TLS

自托管 relay 默认使用 `ws://`，除非显式启用 TLS。若将 relay 置于 443 端口的 nginx 后方，请通过以下方式启动 daemon：

```bash
PASEO_RELAY_ENDPOINT=127.0.0.1:8080 \
PASEO_RELAY_PUBLIC_ENDPOINT=relay.example.com:443 \
PASEO_RELAY_USE_TLS=true \
paseo daemon start
```

Equivalent config：

```json
{
  "daemon": {
    "relay": {
      "enabled": true,
      "endpoint": "127.0.0.1:8080",
      "publicEndpoint": "relay.example.com:443",
      "useTls": true
    }
  }
}
```

Minimal nginx WebSocket proxy：

```nginx
server {
  listen 443 ssl;
  server_name relay.example.com;

  ssl_certificate /etc/letsencrypt/live/relay.example.com/fullchain.pem;
  ssl_certificate_key /etc/letsencrypt/live/relay.example.com/privkey.pem;

  location /ws {
    proxy_pass http://127.0.0.1:8080;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
    proxy_set_header Host $host;
  }
}
```

---

<p align="center">
  <a href="https://star-history.com/#getpaseo/paseo&Date">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=getpaseo/paseo&type=Date&theme=dark">
      <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/svg?repos=getpaseo/paseo&type=Date">
      <img src="https://api.star-history.com/svg?repos=getpaseo/paseo&type=Date" alt="Star history chart for getpaseo/paseo" width="600" style="max-width: 100%;">
    </picture>
  </a>
</p>

## License

AGPL-3.0
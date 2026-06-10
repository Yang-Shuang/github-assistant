<h1 align="center">Agent Orchestrator — 并行 AI Agent 的编排层</h1>

<p align="center">
<a href="https://github.com/ComposioHQ/agent-orchestrator">
  <img width="800" alt="Agent Orchestrator banner" src="docs/assets/agent_orchestrator_banner.png">
</a>
</p>

<div align="center">

启动并行的 AI 编程 Agent，每个 Agent 拥有独立的 Git Worktree。Agent 自动修复 CI 失败、处理审查意见并提交 PR —— 你只需在一个仪表盘中进行监督。

[![GitHub stars](https://img.shields.io/github/stars/ComposioHQ/agent-orchestrator?style=flat-square)](https://github.com/ComposioHQ/agent-orchestrator/stargazers)
[![npm version](https://img.shields.io/npm/v/%40aoagents%2Fao?style=flat-square)](https://www.npmjs.com/package/@aoagents/ao)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue?style=flat-square)](LICENSE)
[![PRs merged](https://img.shields.io/badge/PRs_merged-61-brightgreen?style=flat-square)](https://github.com/ComposioHQ/agent-orchestrator/pulls?q=is%3Amerged)
[![Tests](https://img.shields.io/badge/test_cases-3%2C288-blue?style=flat-square)](https://github.com/ComposioHQ/agent-orchestrator/releases/tag/metrics-v1)
[![Discord](https://img.shields.io/badge/Discord-Join%20Community-5865F2?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/UZv7JjxbwG)

</div>

---

Agent Orchestrator 管理着在代码库上并行工作的 AI 编程 Agent 集群。每个 Agent 拥有独立的 Git Worktree、分支和 PR。当 CI 失败时，Agent 会自动修复；当审查者留下评论时，Agent 会处理这些反馈。只有需要人类判断时，你才会被介入。

**兼容任意 Agent**（Claude Code、Codex、Aider） · **兼容任意运行时**（tmux、ConPTY/process、Docker） · **兼容任意任务追踪器**（GitHub、Linear）

<div align="center">

## 查看演示效果

<a href="https://x.com/agent_wrapper/status/2026329204405723180">
  <img src="docs/assets/demo-video-tweet.png" alt="Agent Orchestrator demo — AI agents building their own orchestrator" width="560">
</a>
<br><br>
<a href="https://x.com/agent_wrapper/status/2026329204405723180"><img src="docs/assets/btn-watch-demo.png" alt="在 X 上观看演示" height="48"></a>
<br><br><br>
<a href="https://x.com/agent_wrapper/status/2025986105485733945">
  <img src="docs/assets/article-tweet.png" alt="The Self-Improving AI System That Built Itself" width="560">
</a>
<br><br>
<a href="https://x.com/agent_wrapper/status/2025986105485733945"><img src="docs/assets/btn-read-article.png" alt="Read the Full Article on X" height="48"></a>

</div>

## 快速开始

> **前置条件：**[Node.js 20.18.3+](https://nodejs.org)、[Git 2.25+](https://git-scm.com)、[`gh` CLI](https://cli.github.com)，以及：
> - **macOS / Linux：**[tmux](https://github.com/tmux/tmux/wiki/Installing) —— 通过 `brew install tmux` 或 `sudo apt install tmux` 安装。
> - **Windows：**推荐使用 PowerShell 7+。无需安装 tmux —— AO 通过 `runtime-process` 插件使用原生 ConPTY（Windows 默认配置）。如果你安装了 Git Bash 并希望使用它，请设置环境变量 `AO_SHELL=bash`。

### 安装

```bash
npm install -g @aoagents/ao
```

> **夜间构建版**（最新 `main`，每周五至周二发布）：`npm install -g @aoagents/ao@nightly`<br>切换回稳定版：`npm install -g @aoagents/ao@latest`

<details>
<summary>遇到权限拒绝？从源码安装？</summary>

如果 `npm install -g` 因 EACCES 报错，请在命令前加上 `sudo`，或[修复你的 npm 权限](https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally)。

从源码安装（适用于贡献者）：

```bash
git clone https://github.com/ComposioHQ/agent-orchestrator.git
cd agent-orchestrator && bash scripts/setup.sh
```
</details>

### Zsh 补全

从已安装的 CLI 生成补全文件：

```bash
mkdir -p ~/.zsh/completions
ao completion zsh > ~/.zsh/completions/_ao
```

然后确保该目录在运行 `compinit` 前已加入你的 `fpath`：

```zsh
fpath=(~/.zsh/completions $fpath)
autoload -Uz compinit
compinit
```

对于 Oh My Zsh，将生成的文件安装到自定义插件目录，并将 `ao` 添加到插件列表：

```bash
mkdir -p "${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/ao"
ao completion zsh > "${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/ao/_ao"
```

如果你是从源码签出进行开发贡献，也可以为 [`completions/_ao`](completions/_ao) 创建软链接。

### 启动

指向任意代码仓库 —— 一条命令即可完成克隆、配置并启动仪表盘：

```bash
ao start https://github.com/your-org/your-repo
```

或在已有的本地仓库内直接运行：

```bash
cd ~/your-project && ao start
```

到此为止。仪表盘将在 `http://localhost:3000` 打开，编排 Agent 开始管理你的项目。

### 添加更多项目

```bash
ao start ~/path/to/another-repo
```

## 工作原理

1. **你启动它** —— `ao start` 会启动仪表盘并运行一个编排 Agent
2. **编排器生成工作进程** —— 每个 Issue 都会分配到一个独立的 Git Worktree 中的专属 Agent
3. **Agent 自主工作** —— 它们阅读代码、编写测试用例并创建 PR
4. **反应机制处理反馈** —— CI 失败和审查意见会自动路由回对应的 Agent
5. **你进行审查与合并** —— 仅在需要人类判断时才会介入你

编排 Agent 在内部使用 [AO CLI](docs/CLI.md) 来管理会话。你无需学习或使用该 CLI —— 仪表盘和编排器会自动处理一切。

## 配置说明

`ao start` 会自动生成带有合理默认值的 `agent-orchestrator.yaml`。你随后可以编辑该文件来自定义行为：

```yaml
# agent-orchestrator.yaml
$schema: https://raw.githubusercontent.com/ComposioHQ/agent-orchestrator/main/schema/config.schema.json
# Runtime data is auto-derived under ~/.agent-orchestrator/{hash}-{projectId}/
port: 3000

defaults:
  runtime: tmux       # default on macOS / Linux; on Windows the default is `process` (ConPTY)
  agent: claude-code
  workspace: worktree
  notifiers: [desktop]

projects:
  my-app:
    repo: owner/my-app
    path: ~/my-app
    defaultBranch: main
    sessionPrefix: app

reactions:
  ci-failed:
    auto: true
    action: send-to-agent
    retries: 2
  changes-requested:
    auto: true
    action: send-to-agent
    escalateAfter: 30m
  approved-and-green:
    auto: false # flip to true for auto-merge
    action: notify
```

CI 失败 → Agent 获取日志并修复。审查者要求修改 → Agent 处理这些意见。PR 获批且 CI 全绿 → 你会收到合并通知。

请保留 `$schema` 这一行，以便编辑器能够基于 [`schema/config.schema.json`](schema/config.schema.json) 提供自动补全和校验。

完整参考见 [`agent-orchestrator.yaml.example`](agent-orchestrator.yaml.example)，或运行 `ao config-help` 查看完整 Schema。

## 远程访问

运行期间，AO 会保持你的 Mac 处于唤醒状态，因此你可以远程访问仪表盘（例如通过手机上的 Tailscale），而无需担心设备进入睡眠。

**工作原理：**在 macOS 上，AO 会使用 `caffeinate` 自动获取空闲休眠阻止断言。当 AO 退出时，该断言会自动释放。

```yaml
# agent-orchestrator.yaml
$schema: https://raw.githubusercontent.com/ComposioHQ/agent-orchestrator/main/schema/config.schema.json
power:
  preventIdleSleep: true  # Default on macOS; no-op on Linux and Windows
```

如果你希望在 AO 运行时允许系统进入空闲休眠，请将其设置为 `false`。

**合盖限制：**macOS 在硬件层面强制执行合盖睡眠策略 —— 任何用户空间断言都无法覆盖此行为。如果你在合盖出差时需要远程访问，请使用[clamshell mode（外壳模式）](https://support.apple.com/en-us/102505)（需连接外接电源、显示器和输入设备）。

**Linux / Windows：**AO 目前在这两个平台上不持有唤醒断言。在 Linux 上，空闲休眠行为由你的桌面环境或 `systemd-logind` 控制；请直接配置相关设置。如果需要在闲置状态下进行远程访问，请在 Windows 上调整操作系统的电源计划。

## 插件架构

提供七个插件插槽。生命周期管理保留在核心模块中。

| Slot      | Default     | Alternatives             |
| --------- | ----------- | ------------------------ |
| Runtime   | tmux (macOS/Linux) / process (Windows) | process, docker |
| Agent     | claude-code | codex, aider, cursor, opencode, kimicode |
| Workspace | worktree    | clone                    |
| Tracker   | github      | linear, gitlab           |
| SCM       | github      | gitlab                   |
| Notifier  | desktop     | slack, discord, composio, webhook, openclaw |
| Terminal  | iterm2      | web                      |

所有接口均在 [`packages/core/src/types.ts`](packages/core/src/types.ts) 中定义。一个插件只需实现其中一个接口并导出 `PluginModule` 即可。就是这么简单。

## 为什么选择 Agent Orchestrator？

在终端中运行单个 AI Agent 很容易。但在不同的 Issue、分支和 PR 间同时运行 30 个 Agent，则是一个协调难题。

**没有编排时**，你需要手动：创建分支、启动 Agent、检查是否卡住、查看 CI 失败日志、转发审查意见、追踪哪些 PR 已准备好合并、完成后清理环境。

**使用 Agent Orchestrator**，你只需执行 `ao start` 然后离开。系统会自动处理隔离、反馈路由和状态跟踪。你负责审查 PR 并做出决策 —— 其余工作全部自动化。

## 文档说明

| Doc                                      | What it covers                                               |
| ---------------------------------------- | ------------------------------------------------------------ |
| [安装指南](SETUP.md)                  | 详细的安装、配置与故障排除    |
| [CLI 参考手册](docs/CLI.md)             | 所有 `ao` 命令（主要由编排 Agent 调用）    |
| [示例](examples/)                    | 配置模板（GitHub、Linear、多项目、自动合并） |
| [开发指南](docs/DEVELOPMENT.md) | 架构、规范与插件模式                    |
| [贡献指南](CONTRIBUTING.md)          | 如何参与贡献、构建插件及 PR 流程                 |

## 本地开发

```bash
pnpm install && pnpm build    # 安装并构建所有包
pnpm test                      # 运行测试（共 3,288 个用例）
pnpm dev                       # 启动 Web 仪表盘开发服务器
```

代码规范与架构细节请参见 [docs/DEVELOPMENT.md](docs/DEVELOPMENT.md)。

## 参与贡献

欢迎贡献代码。插件系统使得为新的 Agent、运行时、追踪器和通知渠道添加支持变得非常简单。每个插件都是对某个 TypeScript 接口的实现 —— 具体模式请参见 [CONTRIBUTING.md](CONTRIBUTING.md) 和[开发指南](docs/DEVELOPMENT.md)。

## 许可证

MIT
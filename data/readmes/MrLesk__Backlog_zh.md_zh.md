<h1 align="center">Backlog.md</h1>
<p align="center">适用于任意 Git 仓库的 Markdown 原生任务管理器与看板可视化工具</p>

<p align="center">
<code>npm i -g backlog.md</code> 或 <code>bun add -g backlog.md</code> 或 <code>brew install backlog-md</code> 或 <code>nix run github:MrLesk/Backlog.md</code>
</p>

![Backlog demo GIF using: backlog board](./.github/backlog-v1.40.gif)


---

> **Backlog.md** 将任意包含 Git 仓库的文件夹转化为一个**自包含的项目看板**，由纯 Markdown 文件和零配置 CLI 驱动。专为**基于规范的 AI 开发**打造——合理组织你的任务，让 AI Agent 交付可预测的结果。

## Features（功能特性）

* 📝 **Markdown-native tasks（原生 Markdown 任务）** -- 将每个 Issue 管理为纯 `.md` 文件
* 🤖 **AI-Ready（AI 就绪）** -- 兼容 Claude Code、Gemini CLI、Codex、Kiro 及任何支持 MCP 或 CLI 的 AI 助手
* 📊 **Instant terminal Kanban（即时终端看板）** -- `backlog board` 在 Shell 中渲染实时看板
* 🌐 **Modern web interface（现代化 Web 界面）** -- `backlog browser` 启动一个精美的 Web UI 用于可视化任务管理
* 🔍 **Powerful search（强大搜索功能）** -- 使用 `backlog search` 对任务、文档和决策进行模糊搜索
* 📋 **Rich query commands（丰富的查询命令）** -- 轻松查看、列出、过滤或归档任务
* ✅ **Definition of Done defaults（默认“定义完成”清单）** -- 为每个新任务添加可复用的检查清单
* 📤 **Board export（看板导出）** -- `backlog board export` 生成可分享的 Markdown 报告
* 🔒 **100 % private & offline（100% 隐私保护与离线运行）** -- Backlog.md 完全驻留在你的仓库内，所有管理操作均可在本地完成
* 💻 **Cross-platform（跨平台支持）** -- 兼容 macOS、Linux 和 Windows
* 🆓 **MIT-licensed & open-source（MIT 开源许可）** -- 个人与商业用途免费


---

## <img src="./.github/5-minute-tour-256.png" alt="Getting started" width="28" height="28" align="center"> Getting started（快速入门）

```bash
# Install
bun i -g backlog.md
# or: npm i -g backlog.md
# or: brew install backlog-md

# Initialize in any Git repo
backlog init "My Awesome Project"

# Or initialize without Git for local/non-code projects
backlog init "Personal Planning" --no-git
```

初始化向导将询问你如何连接 AI 工具：
- **MCP connector（推荐）** — 自动配置 Claude Code、Codex、Gemini CLI、Kiro 或 Cursor，并为你的 Agent 添加工作流说明。
- **CLI commands** — 创建指令文件（CLAUDE.md, AGENTS.md 等），使 Agent 通过 CLI 使用 Backlog。
- **Skip** — 跳过 AI 配置；仅将 Backlog.md 用作任务管理器。

Backlog 数据存储在项目本地的 backlog 文件夹中（如 `backlog/`、`.backlog/`），或通过 `backlog.config.yml` 配置的项目相对路径。任务文件保持为人类可读的 Markdown 格式（例如 `task-10 - Add core search functionality.md`）。Git 为可选项：使用 `backlog init --no-git` 将创建仅基于文件系统的项目，并禁用跨分支检查、远程操作和自动提交功能。

---

### Working with AI agents（与 AI Agent 协作）

这是推荐用于 Claude Code、Codex、Gemini CLI、Kiro 及类似工具的工作流——遵循**基于规范的 AI 开发**方法。
运行 `backlog init` 并选择 MCP 或 CLI 集成后，请按以下循环操作：

**步骤 1 — 描述你的想法。** 告诉 Agent 你想构建什么，并要求它将工作拆分为带有清晰描述和验收标准的小任务。

**🤖 向你的 AI Agent 提问：**
> I want to add a search feature to the web view that searches tasks, docs, and decisions. Please decompose this into small Backlog.md tasks.

> [!NOTE]
> **审查节点 #1** — 阅读任务描述和验收标准。

**步骤 2 — 一次只处理一个任务。** 每个 Agent 会话仅处理单个任务，每个任务对应一个 PR。良好的任务拆分意味着每次会话均可独立工作而不会产生冲突。确保每个任务足够小，以便在单次对话中完成，从而避免耗尽上下文窗口。

**步骤 3 — 编码前规划。** 让 Agent 进行研究并在任务中编写实施计划。请在实现前立即执行此操作，以确保计划反映代码库的当前状态。

**🤖 向你的 AI Agent 提问：**
> Work on BACK-10 only. Research the codebase and write an implementation plan in the task. Wait for my approval before coding.

> [!NOTE]
> **审查节点 #2** — 阅读计划。方案是否合理？批准它或要求 Agent 修改。

**步骤 4 — 实现与验证。** 让 Agent 执行该任务。

> [!NOTE]
> **审查节点 #3** — 审查代码、运行测试、检查 linting，并验证结果是否符合预期。

如果输出效果不佳：清除计划、笔记和最终总结，优化任务描述与验收标准，并在新的会话中重新运行该任务。

---

### Working without AI agents（不使用 AI Agent）

在终端或浏览器中将 Backlog.md 用作独立的任务管理器。

```bash
# Create and refine tasks
backlog task create "Render markdown as kanban"
backlog task edit BACK-1 -d "Detailed context" --ac "Clear acceptance criteria"

# Track work
backlog task list -s "To Do"
backlog search "kanban"
backlog board

# Work visually in the browser
backlog browser
```

你可以随时在 AI 辅助工作流和手动工作流之间切换——两者均基于相同的 Markdown 任务文件运行。推荐使用 Backlog.md 命令（CLI/MCP/Web）修改任务，而非直接编辑任务文件，以保持字段类型和元数据的一致性。任务可记录相对于项目根目录的已修改文件，后续可通过 `backlog search --modified-file src/path.ts --plain` 查找它们。

**了解更多：** [CLI reference](CLI-INSTRUCTIONS.md) | [Advanced configuration](ADVANCED-CONFIG.md)

---

## <img src="./.github/web-interface-256.png" alt="Web Interface" width="28" height="28" align="center"> Web Interface（Web 界面）

启动现代化、响应式的 Web 界面，用于可视化任务管理：

```bash
# Start the web server (opens browser automatically)
backlog browser

# Custom port
backlog browser --port 8080

# Don't open browser automatically
backlog browser --no-open
```

**Features（功能特性）：**
- 支持拖拽的交互式看板
- 使用丰富表单创建和编辑任务
- 带检查清单的交互式验收标准编辑器
- 所有视图下的实时更新
- 适配桌面端与移动端的响应式设计
- 带确认对话框的任务归档功能
- 无缝 CLI 集成——所有更改均同步至 Markdown 文件

![Web Interface Screenshot](./.github/web.jpeg)

若要将 Web UI 保持为自动启动的本地服务，请参阅 [Running Backlog.md as a Service](backlog/docs/doc-003%20-%20Running-Backlog-Browser-as-a-Service.md)。

---

## 🔧 MCP Integration（Model Context Protocol）集成

将 Backlog.md 与 Claude Code、Codex、Gemini CLI 和 Kiro 等 AI 编程助手连接的最简单方式是通过 MCP 协议。
你可以运行 `backlog init`（即使已初始化过 Backlog.md）来自动配置 MCP 集成，或参考下方的手动步骤。

### Client guides（客户端指南）

<details>
  <summary><strong>Claude Code</strong></summary>

  ```bash
  claude mcp add backlog --scope user -- backlog mcp start
  ```

</details>

<details>
  <summary><strong>Codex</strong></summary>

  ```bash
  codex mcp add backlog backlog mcp start
  ```

</details>

<details>
  <summary><strong>Gemini CLI</strong></summary>

  ```bash
  gemini mcp add backlog -s user backlog mcp start
  ```

</details>

<details>
  <summary><strong>Kiro</strong></summary>

  ```bash
  kiro-cli mcp add --scope global --name backlog --command backlog --args mcp,start
  ```

</details>

在所有位置统一使用共享的服务器名称 `backlog`——MCP 服务端会自动检测当前目录是否已初始化，并在需要时回退至 `backlog://init-required`。

### Manual config（手动配置）

```json
{
  "mcpServers": {
    "backlog": {
      "command": "backlog",
      "args": ["mcp", "start"],
      "env": {
        "BACKLOG_CWD": "/absolute/path/to/your/project"
      }
    }
  }
}
```

如果你的 IDE 无法为 MCP 服务端设置进程工作目录，请如上所示配置 `BACKLOG_CWD`。
如果你的 IDE 支持自定义参数但不支持环境变量，你也可以使用 `["mcp", "start", "--cwd", "/absolute/path/to/your/project"]`。

> [!IMPORTANT]
> 手动添加 MCP 服务端时，应在你的 CLAUDE.md/AGENTS.md 文件中添加一些额外说明，以告知 Agent 关于 Backlog.md 的信息。使用 `backlog init` 时无需此步骤，因为它会自动添加这些指令。Backlog.md 的 Agent 指引位于 [`/src/guidelines/mcp/agent-nudge.md`](/src/guidelines/mcp/agent-nudge.md)。

连接成功后，Agent 可通过资源 `backlog://docs/task-workflow` 读取 Backlog.md 的工作流说明。在你的 AI 工具（Claude Code、Codex、Kiro）中使用 `/mcp` 命令可验证连接是否生效。

---

## <img src="./.github/cli-reference-256.png" alt="CLI Reference" width="28" height="28" align="center"> CLI reference（命令行参考）

完整命令参考——任务管理、搜索、看板、文档、决策等：**[CLI-INSTRUCTIONS.md](CLI-INSTRUCTIONS.md)**

快速示例：`backlog task create`、`backlog task list`、`backlog task edit`、`backlog search`、`backlog board`、`backlog browser`。

完整帮助信息：`backlog --help`

---

## <img src="./.github/configuration-256.png" alt="Configuration" width="28" height="28" align="center"> Configuration（配置）

Backlog.md 按以下层级合并配置（优先级从高到低）：

1. CLI flags
2. Project config file（项目配置文件）:
   - `backlog.config.yml`（若存在）
   - 否则为 `backlog/config.yml` 或 `.backlog/config.yml`
3. Built‑ins（内置默认值）

### Interactive wizard (`backlog config`)

运行无参数的 `backlog config` 可启动完整的交互式向导。这与在 `backlog init` 中选择高级设置时的体验相同，它将引导你完成所有配置项：
- Cross-branch accuracy（跨分支准确性）: `checkActiveBranches`, `remoteOperations`, and `activeBranchDays`.
- Git workflow（Git 工作流）: `autoCommit` and `bypassGitHooks`.
- ID formatting（ID 格式）: enable or size `zeroPaddedIds`.
- Editor integration（编辑器集成）: pick a `defaultEditor` with availability checks.
- Definition of Done defaults（默认“定义完成”清单）: interactively add/remove/reorder/clear project-level `definition_of_done` checklist items.
- Web UI defaults（Web 界面默认值）: choose `defaultPort` and whether `autoOpenBrowser` should run.

跳过向导（在初始化期间回答“No”）将应用 Backlog.md 附带的安全默认值：
- `checkActiveBranches=true`, `remoteOperations=true`, `activeBranchDays=30`.
- `autoCommit=false`, `bypassGitHooks=false`.
- `zeroPaddedIds` disabled.
- `defaultEditor` unset (falls back to your environment).
- `defaultPort=6420`, `autoOpenBrowser=true`.

对于仅基于文件系统的项目，运行 `backlog init --no-git`。Backlog.md 不会执行 `git init`，且保存的配置会强制设置 `checkActiveBranches=false`, `remoteOperations=false`, and `autoCommit=false`，使 CLI、Web 和 MCP 本地文件工作流不依赖 Git 仓库。

每次重新访问 `backlog init` 或重跑 `backlog config` 时，向导会用你当前的值预填充提示项，以便你仅调整变更过的配置。

### Definition of Done defaults（默认“定义完成”清单）

通过 `backlog config`（或在 `backlog init` 高级设置中）、Web UI（Settings → Definition of Done Defaults），或直接编辑项目配置文件来设置全局 DoD 条目：

```yaml
definition_of_done:
  - Tests pass
  - Documentation updated
  - No regressions introduced
```

当项目使用根配置发现机制时，请编辑 `backlog.config.yml` 而非 `backlog/config.yml`。

这些条目默认会添加到每个新任务中。你可以在创建时使用 `--dod` 添加更多条目，或使用 `--no-dod-defaults` 针对特定任务禁用默认值。

完整配置参考（所有选项、命令和详细说明），请参阅 **[ADVANCED-CONFIG.md](ADVANCED-CONFIG.md)**。

---

## 🌐 Community Tools（社区工具）

- **[vscode-backlog-md](https://marketplace.visualstudio.com/items?itemName=ysamlan.vscode-backlog-md)** - VS Code 扩展，提供 Issue 面板、看板视图和编辑功能。（[ysamlan/vscode-backlog-md](https://github.com/ysamlan/vscode-backlog-md)）

---

### License（许可证）

Backlog.md 采用 **MIT License** 发布——可自由使用，仅需注明出处。详见 [LICENSE](LICENSE)。
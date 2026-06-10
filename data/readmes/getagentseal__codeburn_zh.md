<p align="center">
  <img src="https://raw.githubusercontent.com/getagentseal/codeburn/main/assets/providers.png" alt="CodeBurn" width="520" />
</p>

<p align="center"><strong>看清你的 AI 编程 Token 究竟花在了哪里。</strong></p>

<p align="center">                                                                                                                                                                          
    <a href="https://www.npmjs.com/package/codeburn"><img src="https://img.shields.io/npm/v/codeburn.svg" alt="npm version" /></a>
    <a href="https://www.npmjs.com/package/codeburn"><img src="https://img.shields.io/npm/dt/codeburn.svg" alt="total downloads" /></a>                                                       
    <a href="https://github.com/getagentseal/codeburn/blob/main/LICENSE"><img src="https://img.shields.io/npm/l/codeburn.svg" alt="license" /></a>                                            
    <a href="https://github.com/getagentseal/codeburn"><img src="https://img.shields.io/badge/node-%3E%3D20-brightgreen.svg" alt="node version" /></a>                                       
    <a href="https://discord.gg/w2sw8mCqep"><img src="https://img.shields.io/badge/discord-join-5865F2?logo=discord&logoColor=white" alt="Discord" /></a>                                     
    <a href="https://github.com/sponsors/iamtoruk"><img src="https://img.shields.io/badge/sponsor-♥-ea4aaa?logo=github" alt="Sponsor" /></a>                                                  
  </p> 

CodeBurn 追踪 **25 款 AI 编程工具**的 Token 用量、成本与性能。它按任务类型、模型、工具、项目和提供商细分支出，让你清楚看到预算究竟花在了哪里。

所有功能均在本地运行。无需包装器、代理或 API 密钥。CodeBurn 直接从磁盘读取会话数据，并使用 [LiteLLM](https://github.com/BerriAI/litellm) 对每次调用进行定价。

<table>
<tr>
<td align="center"><strong>仪表盘</strong></td>
<td align="center"><strong>菜单栏</strong></td>
</tr>
<tr>
<td><img src="https://raw.githubusercontent.com/getagentseal/codeburn/main/assets/dashboard.jpg" alt="CodeBurn TUI dashboard" width="440" /></td>
<td><img src="https://raw.githubusercontent.com/getagentseal/codeburn/main/assets/menubar-0.9.11.png" alt="CodeBurn macOS menubar" width="440" /></td>
</tr>
<tr>
<td align="center"><strong>优化分析</strong></td>
<td align="center"><strong>模型对比</strong></td>
</tr>
<tr>
<td><img src="https://raw.githubusercontent.com/getagentseal/codeburn/main/assets/optimize.jpg" alt="CodeBurn optimize" width="440" /></td>
<td><img src="https://raw.githubusercontent.com/getagentseal/codeburn/main/assets/compare.jpg" alt="CodeBurn compare" width="440" /></td>
</tr>
</table>

## 环境要求

- Node.js 20+
- 至少安装一款受支持的 AI 编程工具，且磁盘上存在会话数据
- 支持 Cursor 和 OpenCode 时，会自动作为可选依赖安装 `better-sqlite3`

## 安装

```bash
npm install -g codeburn
```

或通过 Homebrew：

```bash
brew install codeburn
```

或直接运行（无需全局安装）：

```bash
npx codeburn
bunx codeburn
dx codeburn
```

## 用法

```bash
codeburn                        # 交互式仪表盘（默认查看最近 7 天）
codeburn today                  # 今日用量
codeburn month                  # 本月用量
codeburn report -p 30days       # 滚动窗口：最近 30 天
codeburn report -p all          # 所有已记录的会话
codeburn report --from 2026-04-01 --to 2026-04-10  # 精确日期范围
codeburn report --format json   # 以 JSON 格式输出完整仪表盘数据
codeburn report --refresh 60    # 每 60s 自动刷新（默认：30s）
codeburn status                 # 紧凑单行显示（今日 + 本月总计）
codeburn status --format json
codeburn export                 # CSV 导出（含今天、7天、30天数据）
codeburn export -f json         # JSON 格式导出
codeburn optimize               # 查找浪费并提供即贴即用修复方案
codeburn optimize -p week       # 仅扫描最近 7 天的范围
codeburn compare                # 并排模型对比
codeburn yield                  # 追踪有效产出 vs 回滚/废弃的支出
codeburn yield -p 30days        # 最近 30 天效能分析
codeburn models                 # 按模型划分的 Token + 成本表（最近 30 天）
codeburn models --by-task       # 将每个模型拆解为按任务类型分行的数据
codeburn models --top 10        # 仅显示费用最高的前 10 个
codeburn models --format markdown      # 输出易于粘贴的 Markdown 表格
codeburn models --task feature         # 过滤至功能开发类工作
codeburn models --provider claude      # 过滤至单一提供商
```

使用方向键可在“今天”、“7天”、“30天”、“本月”和“6个月”之间切换（精确的历史窗口请使用 `--from` / `--to`）。按 `q` 退出，`1`~`5` 为快捷方式，`c` 打开模型对比，`o` 打开优化分析。仪表盘默认每 30 秒自动刷新一次（设置 `--refresh 0` 可禁用）。它还会显示所有项目的平均会话成本以及费用最高的五个会话。

## 支持的提供商

|                                                            | Provider       | Supported | Doc                                               |
|------------------------------------------------------------|----------------|-----------|---------------------------------------------------|
| <img src="assets/providers/claude.jpg" width="28" />       | Claude Code    | Yes       | [claude.md](docs/providers/claude.md)             |
| <img src="assets/providers/claude.jpg" width="28" />       | Claude Desktop | Yes       | [claude.md](docs/providers/claude.md)             |
| <img src="assets/providers/cline.svg" width="28" />        | Cline          | Yes       | [cline.md](docs/providers/cline.md)               |
| <img src="assets/providers/codex.png" width="28" />        | Codex (OpenAI) | Yes       | [codex.md](docs/providers/codex.md)               |
| <img src="assets/providers/cursor.jpg" width="28" />       | Cursor         | Yes       | [cursor.md](docs/providers/cursor.md)             |
| <img src="assets/providers/cursor-agent.jpg" width="28" /> | cursor-agent   | Yes       | [cursor-agent.md](docs/providers/cursor-agent.md) |
| <img src="assets/providers/forge.png" width="28" />        | Forge          | Yes       | [forge.md](docs/providers/forge.md)               |
| <img src="assets/providers/gemini.png" width="28" />       | Gemini CLI     | Yes       | [gemini.md](docs/providers/gemini.md)             |
| <img src="assets/providers/mistral-vibe.svg" width="28" /> | Mistral Vibe   | Yes       | [mistral-vibe.md](docs/providers/mistral-vibe.md) |
| <img src="assets/providers/copilot.jpg" width="28" />      | GitHub Copilot | Yes       | [copilot.md](docs/providers/copilot.md)           |
| <img src="assets/providers/ibm-bob.svg" width="28" />      | IBM Bob        | Yes       | [ibm-bob.md](docs/providers/ibm-bob.md)           |
| <img src="assets/providers/kiro.png" width="28" />         | Kiro           | Yes       | [kiro.md](docs/providers/kiro.md)                 |
| <img src="assets/providers/opencode.png" width="28" />     | OpenCode       | Yes       | [opencode.md](docs/providers/opencode.md)         |
| <img src="assets/providers/openclaw.jpg" width="28" />     | OpenClaw       | Yes       | [openclaw.md](docs/providers/openclaw.md)         |
| <img src="assets/providers/pi.png" width="28" />           | Pi             | Yes       | [pi.md](docs/providers/pi.md)                     |
| <img src="assets/providers/omp.svg" width="28" />          | OMP (Oh My Pi) | Yes       | [omp.md](docs/providers/omp.md)                   |
| <img src="assets/providers/droid.png" width="28" />        | Droid          | Yes       | [droid.md](docs/providers/droid.md)               |
| <img src="assets/providers/roo-code.png" width="28" />     | Roo Code       | Yes       | [roo-code.md](docs/providers/roo-code.md)         |
| <img src="assets/providers/kilo-code.png" width="28" />    | KiloCode       | Yes       | [kilo-code.md](docs/providers/kilo-code.md)       |
| <img src="assets/providers/qwen.png" width="28" />         | Qwen           | Yes       | [qwen.md](docs/providers/qwen.md)                 |
| <img src="assets/providers/kimi.svg" width="28" />         | Kimi Code CLI  | Yes       | [kimi.md](docs/providers/kimi.md)                 |
| <img src="assets/providers/goose.png" width="28" />        | Goose          | Yes       | [goose.md](docs/providers/goose.md)               |
| <img src="assets/providers/antigravity.png" width="28" />  | Antigravity    | Yes       | [antigravity.md](docs/providers/antigravity.md)   |
| <img src="assets/providers/crush.png" width="28" />        | Crush          | Yes       | [crush.md](docs/providers/crush.md)               |
|                                                            | Warp           | Yes       | [warp.md](docs/providers/warp.md)                 |

每个提供商文档均列出了确切的数据位置、存储格式及已知注意事项。Linux 和 Windows 路径会自动检测。如果路径已更改或不正确，请[提交 Issue](https://github.com/getagentseal/codeburn/issues)。

CodeBurn 会自动检测你使用的 AI 编程工具。如果磁盘上存在多个提供商的会话数据，可在仪表盘中按 `p` 进行切换。

使用 `--provider` 参数可将任意命令过滤为单个提供商：`codeburn report --provider claude`、`codeburn today --provider codex`、`codeburn export --provider cursor`。该参数适用于所有命令：`report`、`today`、`month`、`status`、`export`、`optimize`、`compare`、`yield`。

### 提供商说明

**Cursor** 从其本地 SQLite 数据库读取 Token 用量。由于 Cursor 的“Auto”模式会隐藏实际使用的模型，成本将使用 Sonnet 定价进行估算（仪表盘中显示为 "Auto (Sonnet est.)"）。Cursor 视图显示的是 Languages 面板而非 Core Tools/Shell/MCP 面板，因为 Cursor 不记录单个工具调用日志。首次运行大型 Cursor 数据库可能需要最多一分钟；结果会被缓存，后续运行将瞬间完成。

**Gemini CLI** 将会话存储为单个 JSON 文件。每个会话在每个消息中嵌入了真实的 Token 数量（输入、输出、缓存、思考），因此无需估算。Gemini 报告的输入 Token 包含缓存部分；CodeBurn 在定价前会从输入中减去缓存部分，以避免重复计费。

**Antigravity CLI** 在 `agy` 运行时通过一个短生命周期的本地进程暴露精确的用量。运行 `codeburn antigravity-hook install` 安装可选的实时钩子，即使菜单栏的 30 秒刷新错过了该窗口，也能捕获短暂的 CLI 会话。该钩子仅存储脱敏后的用量总计，不记录提示词或本地工作目录路径。使用 `codeburn antigravity-hook uninstall` 移除它；如果 `--force` 替换了现有的 statusLine 命令，卸载时会恢复之前的命令。

**Mistral Vibe** 将会话存储为 `~/.vibe/logs/session/`（或 `$VIBE_HOME/logs/session/`）下的文件夹。CodeBurn 从 `meta.json` 读取累积的提示词/补全总量及模型定价，然后读取 `messages.jsonl` 获取首次用户提示词和助手工具调用。`agents/` 下的子代理会话将作为独立的 Vibe 会话计数。

**Kiro** 将对话存储为 `.chat` JSON 文件。Token 数量根据内容长度估算。底层模型未公开，因此会话标记为 `kiro-auto` 并按 Sonnet 费率计费。

**GitHub Copilot** 从 `~/.copilot/session-state/`（旧版 CLI）和 VS Code/VSCodium `workspaceStorage/*/GitHub.copilot-chat/transcripts/` 读取数据。编辑器转录格式没有明确的 Token 计数；Token 根据内容长度估算，模型通过工具调用 ID 前缀推断。

**OpenClaw** 从 `~/.openclaw/agents/` 读取 JSONL 代理日志，并检查旧版路径（`.clawdbot`, `.moltbot`, `.moldbot`）。

**Warp** 从 Warp 本地的 `warp.sqlite` 读取 Oz 代理会话。Exchange 级别的 Token 归属根据提示词权重归一化到对话总量进行估算，且 `run_command` 块会按时间戳附加到最近的先前 Exchange。

**Forge** 从 `~/.forge/.forge.db` 读取对话。助手用量条目提供提示词、补全和缓存 Token 计数；CodeBurn 为每条带有用量的助手消息生成一次调用记录，并对工具调用进行标准化以用于细分统计。

**Roo Code and KiloCode** 是 Cline 系列的 VS Code 扩展。CodeBurn 从每个任务目录读取 `ui_messages.json`，并从 `api_req_started` 条目中提取 Token 用量。

**Claude with multiple config directories.** 如果你在一个以上的账户或配置文件下运行 Claude Code（例如 `~/.claude-work` and `~/.claude-personal`），请将 `CLAUDE_CONFIG_DIRS` 指向所有这些目录：`CLAUDE_CONFIG_DIRS=~/.claude-work:~/.claude-personal codeburn`。跨所有目录的会话将合并为每项目一行，以便总计反映你所有的 Claude 使用情况。POSIX 系统使用 `:`，Windows 使用 `;`。列表中缺失或无法读取的目录将被跳过。

添加新提供商只需一个文件。示例参见 `src/providers/codex.ts`。

## 功能特性

### 成本追踪 (Cost Tracking)

根据输入、输出、缓存读取、缓存写入和网页搜索的 Token 数量对每次 API 调用进行定价。针对 Claude 的快速模式设有乘数加成。定价数据从 [LiteLLM](https://github.com/BerriAI/litellm) 获取，并在本地缓存 24 小时。所有 Claude 和 GPT 模型均设有硬编码回退机制，以防错误定价。

### 任务分类 (Task Categories)

基于工具使用模式及用户消息关键词划分了 13 个类别。无需调用大模型，完全确定性逻辑。

| Category | What triggers it |
|---|---|
| Coding | Edit, Write tools |
| Debugging | Error/fix keywords + tool usage |
| Feature Dev | "add", "create", "implement" keywords |
| Refactoring | "refactor", "rename", "simplify" |
| Testing | pytest, vitest, jest in Bash |
| Exploration | Read, Grep, WebSearch without edits |
| Planning | EnterPlanMode, TaskCreate tools |
| Delegation | Agent tool spawns |
| Git Ops | git push/commit/merge in Bash |
| Build/Deploy | npm build, docker, pm2 |
| Brainstorming | "brainstorm", "what if", "design" |
| Conversation | No tools, pure text exchange |
| General | Skill tool, uncategorized |

### 细分统计 (Breakdowns)

每日成本图表、按项目细分、按模型（Opus、Sonnet、Haiku、GPT-5、GPT-4o、Gemini、Kiro 等）细分、带一次性成功率的活动细分，以及核心工具、Shell 命令和 MCP 服务器统计。

### 一次性成功率 (One-Shot Rate)

对于涉及代码编辑的类别，CodeBurn 会追踪基于文件感知的重试周期。重试是指中间插入 Shell 命令后重新编辑同一文件（例如：Edit foo.ts -> Bash -> Edit foo.ts）。跨步骤编辑不同文件不算重试。“一次性”列显示未重试即成功的编辑比例。90% 的代码编写成功率意味着 AI 十次中有九次一次成功。Claude、Codex 和 Goose 支持文件级追踪；其他提供商回退到基于工具名称的检测机制。

### 定价 (Pricing)

从 [LiteLLM](https://github.com/BerriAI/litellm) 获取模型价格（在 `~/.cache/codeburn/` 自动缓存 24 小时）。涵盖输入、输出、缓存写入、缓存读取和网页搜索成本。针对 Claude 的快速模式设有乘数加成。所有 Claude 和 GPT-5 模型均设有硬编码回退机制，防止模糊匹配导致错误定价。

### 优化分析 (Optimize)

```bash
codeburn optimize                       # scan the last 30 days
codeburn optimize -p today              # today only
codeburn optimize -p week               # last 7 days
codeburn optimize --provider claude     # restrict to one provider
```

扫描你的会话及 `~/.claude/` 配置中的资源浪费模式：

- Claude 在跨会话中重复读取的文件（相同内容、相同上下文，反复阅读）
- 较低的 Read:Edit 比例（只编辑不阅读会导致重试和 Token 浪费）
- 无效的 Bash 输出（未限制 `BASH_MAX_OUTPUT_LENGTH`，包含大量尾部噪声）
- 闲置的 MCP 服务器仍在每次会话中支付工具 Schema 开销费用
- `~/.claude/` 中定义但从未调用的幽灵代理、技能和斜杠命令
- 臃肿的 `CLAUDE.md` 文件（已计算 `@-import` 展开后的体积）
- 缓存创建开销及垃圾目录读取
- 上下文过载的会话，有效输入/缓存 Token 远超输出量
- 可能低效的高成本会话：无编辑轮次或反复重试，且未观察到 `git`/`gh` 交付命令

每项发现均显示预估的 Token 和美元节省额，并附带即贴即用的修复方案：一行 `CLAUDE.md` 配置、一个环境变量，或用于归档未用项目的 `mv` 命令。发现项按紧急程度排序（影响权重对比实际浪费量），并最终汇总为 A~F 级的系统健康评分。重复运行会将每项发现标记为新发现、改善中或已解决（基于最近 48 小时窗口）。

你也可以从仪表盘内联打开：状态栏出现发现数量时按 `o`，按 `b` 返回。

### 模型对比 (Compare)

```bash
codeburn compare                        # interactive model picker (default: last 6 months)
codeburn compare -p week                # last 7 days
codeburn compare -p today               # today only
codeburn compare --provider claude      # Claude Code sessions only
```

或在仪表盘中按 `c` 进入对比模式。方向键切换时间周期，按 `b` 返回。

| Section | Metric | What it measures |
|---------|--------|-----------------|
| Performance | One-shot rate | Edits that succeed without retries |
| Performance | Retry rate | Average retries per edit turn |
| Performance | Self-correction | Turns where the model corrected its own mistake |
| Efficiency | Cost per call | Average cost per API call |
| Efficiency | Cost per edit | Average cost per edit turn |
| Efficiency | Output tokens per call | Average output tokens per call |
| Efficiency | Cache hit rate | Proportion of input from cache |

同时对比各分类的一次性成功率、代理委派率、规划率、平均每轮工具调用数及快速模式使用情况。

### 产出分析 (Yield)

```bash
codeburn yield                  # last 7 days (default)
codeburn yield -p today         # today only
codeburn yield -p 30days        # last 30 days
codeburn yield -p month         # this calendar month
```

按时间戳将 AI 会话与 Git 提交进行关联：

| Category | Meaning |
|----------|---------|
| Productive | Commits from this session landed in main |
| Reverted | Commits were later reverted |
| Abandoned | No commits near session, or commits never merged |

需要处于 Git 仓库中。请在项目目录下运行。

### 套餐管理 (Plans)

```bash
codeburn plan set claude-max                                  # $200/month
codeburn plan set claude-pro                                  # $20/month
codeburn plan set cursor-pro                                  # $20/month
codeburn plan set custom --monthly-usd 200 --provider codex   # ChatGPT Pro-style custom plan
codeburn plan reset --provider codex                          # remove one provider plan
codeburn plan set none                                        # disable plan view
codeburn plan                                                 # show configured plans
codeburn plan reset                                           # remove plan config
```

追踪 Claude Pro、Claude Max、Cursor Pro 及自定义提供商套餐。套餐按提供商存储，因此你可同时管理 Claude 和 Codex/Cursor 订阅；仪表盘会为每个活跃的提供商套餐显示一条超额使用行。旧的/自定义的 `all` 套餐保持为单一聚合套餐，添加特定提供商套餐时会被替换，避免超额行数重复计算。现有的单套餐配置仍会作为回退机制读取。预设值采用公开声明的套餐价格（截至 2026 年 4 月）；它们不模拟精确的 Token 配额，因为厂商并未公布消费者套餐的具体限制。

### 货币设置 (Currency)

```bash
codeburn currency GBP          # set to British Pounds
codeburn currency AUD          # set to Australian Dollars
codeburn currency JPY          # set to Japanese Yen
codeburn currency              # show current setting
codeburn currency --reset      # back to USD
```

支持任意 [ISO 4217 货币代码](https://en.wikipedia.org/wiki/ISO_4217#List_of_ISO_4217_currency_codes)（共 162 种）。汇率从 [Frankfurter](https://www.frankfurter.app/) 获取（欧洲央行数据，免费且无需 API Key），缓存有效期为 24 小时。配置存储于 `~/.config/codeburn/config.json`。货币设置适用于所有场景：仪表盘、状态栏、菜单栏、CSV/JSON 导出及 JSON API 输出。

### 模型别名 (Model Aliases)

如果部分模型显示 `$0.00`，说明提供商报告的模型名称与 LiteLLM 定价数据中的任何条目不匹配。使用重写模型名称的代理时常见此情况。

```bash
codeburn model-alias "my-proxy-model" "claude-opus-4-6"   # add alias
codeburn model-alias --list                                # show configured aliases
codeburn model-alias --remove "my-proxy-model"             # remove alias
```

别名存储于 `~/.config/codeburn/config.json`，并在定价查询前于运行时生效。目标名称可以是 [LiteLLM 模型列表](https://github.com/BerriAI/litellm/blob/main/model_prices_and_context_window.json) 中的任意项，或回退表中的标准名称（例如 `claude-sonnet-4-6`、`claude-opus-4-5`、`gpt-4o`）。内置别名涵盖已知代理模型名称变体。用户配置的别名优先级高于内置别名。

### 过滤功能 (Filtering)

```bash
codeburn report --project myapp                  # show only projects matching "myapp"
codeburn report --exclude myapp                  # show everything except "myapp"
codeburn report --exclude myapp --exclude tests  # exclude multiple projects
codeburn month --project api --project web       # include multiple projects
codeburn export --project inventory              # export only "inventory" project data
```

支持按提供商、项目名称（不区分大小写的子串匹配）或精确日期范围进行过滤。`--project` 和 `--exclude` 参数适用于所有命令，并可与 `--provider` 组合使用。

```bash
codeburn report --from 2026-04-01 --to 2026-04-10   # explicit window
codeburn report --from 2026-04-01                    # this date through today
codeburn report --to 2026-04-10                      # earliest data through this date
```

单独使用任一参数均有效。日期顺序颠倒或格式错误时会退出并提示明确错误。在 TUI（终端用户界面）中，自定义范围仅设置初始加载；按 `1`~`5` 可切换回预设周期。

### JSON 输出 (JSON Output)

`report`、`today` 和 `month` 支持 `--format json` 以结构化 JSON 格式将完整仪表盘数据输出至 stdout：

```bash
codeburn report --format json             # 7-day JSON report
codeburn today --format json              # today's data as JSON
codeburn month --format json              # this month as JSON
codeburn report -p 30days --format json   # 30-day window
```

JSON 包含所有仪表盘面板数据：概览（成本、调用次数、会话数、缓存命中率 %）、每日细分、项目（含 `avgCostPerSession`）、带 Token 计数的模型、带一次性成功率的活动、核心工具、MCP 服务器及 Shell 命令。可通过管道传递给 `jq` 进行过滤：

```bash
codeburn report --format json | jq '.projects'
codeburn today --format json | jq '.overview.cost'
```

如需更轻量的输出，请使用 `status --format json`（仅今日和本月总计）或文件导出（`export -f json`）。

## 菜单栏 (Menu Bar)

```bash
codeburn menubar
```

单条命令：下载最新的 `.app`，安装至 `~/Applications` 并启动。使用 `--force` 重新运行可强制重装。原生 Swift/SwiftUI 应用位于 `mac/` 目录（构建详情见 `mac/README.md`）。

菜单栏图标显示设置中选定的消费周期（默认为今天；也可选择周、月、6个月）。非今日周期会附加简短后缀如 `$42 / mo`，以保持菜单栏数值清晰。点击可打开弹出面板，包含代理标签页、周期切换器（今天、7天、30天、本月、全部）、趋势、预测、脉冲、统计与套餐洞察、活动与模型细分、优化发现项以及 CSV/JSON 导出功能。每 30 秒刷新一次。

你也可以从终端设置菜单栏状态周期：

```bash
defaults write org.agentseal.codeburn-menubar CodeBurnMenubarPeriod -string month
```

允许的值包括 `today`、`week`、`month` 和 `sixMonths`。更改外部默认值后需重启应用生效。

**紧凑模式 (Compact mode)** 会将菜单栏项收缩以适配文本，并省略小数位（例如显示 `$110` 而非 `$110.20`）：

```bash
defaults write org.agentseal.codeburn-menubar CodeBurnMenubarCompact -bool true
```

重启应用生效。如需恢复默认设置，请运行 `defaults delete org.agentseal.codeburn-menubar CodeBurnMenubarCompact`。

## 解读仪表盘 (Reading the Dashboard)

CodeBurn 提供数据，你负责解读背后的故事。以下是一些值得注意的模式：

| Signal you see | What it might mean |
|---|---|
| Cache hit < 80% | System prompt or context is not stable, or caching not enabled |
| Lots of `Read` calls per session | Agent re-reading same files, missing context |
| Low 1-shot rate (Coding 30%) | Agent struggling with edits, retry loops |
| Opus 4.6 dominating cost on small turns | Overpowered model for simple tasks |
| `dispatch_agent` / `task` heavy | Sub-agent fan-out, expected or excessive |
| No MCP usage shown | Either you don't use MCP servers, or your config is broken |
| Bash dominated by `git status`, `ls` | Agent exploring instead of executing |
| Conversation category dominant | Agent talking instead of doing |

这些仅是参考起点，并非最终定论。单次实验性会话的 60% 缓存命中率是可以接受的。但如果连续数周的工作都维持在 60%，则说明配置存在问题。

## 数据读取机制 (How It Reads Data)

**Claude Code** 将会话转录以 JSONL 格式存储于 `~/.claude/projects/<sanitized-path>/<session-id>.jsonl`。每条助手记录包含模型名称、Token 用量（输入、输出、缓存读取、缓存写入）、tool_use 块及时间戳。

**Codex** 将会话存储于 `~/.codex/sessions/YYYY/MM/DD/rollout-*.jsonl`，其中包含记录单次及累积 Token 用量的 `token_count` 事件，以及用于工具追踪的 `function_call` 条目。

**Cursor** 将会话数据存储在 SQLite 数据库中，路径为 `~/Library/Application Support/Cursor/User/globalStorage/state.vscdb`（macOS）、`~/.config/Cursor/User/globalStorage/state.vscdb`（Linux）或 `%APPDATA%/Cursor/User/globalStorage/state.vscdb`（Windows）。Token 计数位于带有 `bubbleId:` 键前缀的 `cursorDiskKV` 表条目中。解析结果缓存于 `~/.cache/codeburn/cursor-results.json`，并在数据库变更时自动失效。

**OpenCode** 将会话存储在 SQLite 数据库中，路径为 `~/.local/share/opencode/opencode*.db`。CodeBurn 以只读方式查询 `session`、`message` 和 `part` 表，提取 Token 计数与工具用量，并使用 LiteLLM 定价引擎重新计算成本。对于不在我们定价数据中的模型，会回退使用 OpenCode 自身的 cost 字段。子任务会话（`parent_id IS NOT NULL`）将被排除以避免重复计数。支持多通道数据库并遵循 `XDG_DATA_HOME` 规范。

**Warp** 将 Oz 代理数据存储在 `~/Library/Group Containers/2BBY89MBSN.dev.warp/Library/Application Support/dev.warp.Warp-Stable/warp.sqlite`（含 Preview 回退路径）。CodeBurn 读取 `agent_conversations`、`ai_queries` 和 `blocks`，为每个已完成的 Exchange 生成一次调用记录，根据提示词权重相对于对话总量估算 Exchange Token 占比，并将 `run_command` 块归属到最近的先前 Exchange。

**Forge** 将对话存储在 SQLite 中，路径为 `~/.forge/.forge.db`。CodeBurn 以只读方式查询 `conversations`，解析 `context.messages`，从提示词 Token 中减去缓存 Token 用于输入定价，并从助手消息中提取工具调用及 Shell 命令。

**Pi / OMP** 将会话以 JSONL 格式存储于 `~/.pi/agent/sessions/<sanitized-cwd>/*.jsonl`（Pi）和 `~/.omp/agent/sessions/<sanitized-cwd>/*.jsonl`（OMP）。每条助手消息附带 Token 用量（输入、输出、cacheRead、cacheWrite）及内联的 `toolCall` 内容块。CodeBurn 提取 Token 计数，将工具名称标准化为标准集合（如 `bash` 转为 `Bash`，`dispatch_agent` 转为 `Agent`），并从 `toolCall.arguments.command` 中提取 Bash 命令用于 Shell 细分统计。

**Codebuff**（原名 Manicode）将单聊历史以 JSON 格式存储于 `~/.config/manicode/projects/<project>/chats/<chatId>/chat-messages.json`。Codebuff 按积分计费而非 Token，因此 CodeBurn 记录每条已完成的助手消息（通过 `msg.credits`），并按公开按需费率（$0.01/积分）估算成本。当 Codebuff 将调用路由至上游提供商且暂存的 RunState 记录了 Token 级用量（`message.metadata.runState.sessionState.mainAgentState.messageHistory[*].providerOptions`）时，真实 Token 和 LiteLLM 计算的成本将优先采用。Codebuff 原生工具名称（如 `read_files`、`str_replace`、`run_terminal_command`、`spawn_agents` 等）会标准化为规范集合（`Read`、`Edit`、`Bash`、`Agent`）。若存在，会自动遍历 `manicode-dev` 和 `manicode-staging` 通道。支持通过 `CODEBUFF_DATA_DIR` 自定义根目录。

**Gemini CLI** 将会话存储为单个 JSON 文件，路径为 `~/.gemini/tmp/<project>/chats/session-*.json`。每个会话在每个消息中嵌入真实的 Token 数量（输入、输出、缓存、思考）。Gemini 报告的输入 Token 包含缓存部分；CodeBurn 在定价前会从输入中减去缓存部分，以避免重复计费。

**Mistral Vibe** 将会话文件夹存储于 `~/.vibe/logs/session/`。每个文件夹包含记录累积提示词/补全 Token 总量、模型定价、时间戳和工作目录的 `meta.json`，以及记录用户提示词和助手工具调用的 `messages.jsonl`。由于源数据是累计性质的而非按助手轮次划分，CodeBurn 为每个 Vibe 会话生成一条记录。

**OpenClaw** 将代理会话以 JSONL 格式存储于 `~/.openclaw/agents/*.jsonl`。同时检查旧版路径 `.clawdbot`、`.moltbot`、`.moldbot`。Token 用量来自助手消息的 `usage` 块；模型名称取自 `modelId` 或 `message.model` 字段。

**Cline / Roo Code / KiloCode** 属于 Cline 系列编程代理。CodeBurn 从每个任务目录读取 `ui_messages.json`，过滤出 `type: "say"` 且 `say: "api_req_started"` 的条目以提取 Token 计数。Cline 会扫描 VS Code 的 `globalStorage/saoudrizwan.claude-dev` 和 `~/.cline/data`；Roo Code 和 KiloCode 则扫描 VS Code、VS Code Insiders 及 VSCodium 的 `globalStorage` 根目录。

**IBM Bob** 将 IDE 任务历史存储在 IBM Bob 应用数据目录下的 `User/globalStorage/ibm.bob-code/tasks/<task-id>/`。CodeBurn 读取 `ui_messages.json` 获取 API 请求 Token/成本记录，并读取 `api_conversation_history.json` 获取选定模型信息，同时支持正式版（`IBM Bob`）和预览版（`Bob-IDE`）应用数据文件夹。

**Kimi Code CLI** 将会话日志存储于 `$KIMI_SHARE_DIR/sessions/<workdir-hash>/<session-id>/` 或 `~/.kimi/sessions/<workdir-hash>/<session-id>/`。CodeBurn 读取 `wire.jsonl` 中的 `StatusUpdate.token_usage` 记录，将 `input_other`、`input_cache_read`、`input_cache_creation` 和 `output` 映射到标准 Token 列中，并包含每个会话 `subagents/` 文件夹下的子代理会话。

CodeBurn 会对消息进行去重（Claude 按 API 消息 ID，Codex 按累积 Token 交叉核对，Cursor 按对话/时间戳，Gemini 按会话 ID，OpenCode 按会话+消息 ID，Pi/OMP 按 responseId，Codebuff 按聊天文件夹+消息 ID，Kimi 按会话+消息 ID），按条目过滤日期范围，并对每轮交互进行分类。

## 环境变量 (Environment Variables)

| Variable | Description |
|----------|-------------|
| `CLAUDE_CONFIG_DIR` | Override Claude Code data directory (default: `~/.claude`) |
| `CLAUDE_CONFIG_DIRS` | OS-delimited list of Claude data directories to scan together (e.g. `~/.claude-work:~/.claude-personal`). Sessions merge into one row per project. Overrides `CLAUDE_CONFIG_DIR` when set. |
| `CODEX_HOME` | Override Codex data directory (default: `~/.codex`) |
| `CODEBUFF_DATA_DIR` | Override Codebuff data directory (default: `~/.config/manicode`) |
| `FACTORY_DIR` | Override Droid data directory (default: `~/.factory`) |
| `KIMI_SHARE_DIR` | Override Kimi Code CLI share directory (default: `~/.kimi`) |
| `KIMI_MODEL_NAME` | Override Kimi model name when Kimi sessions do not record the model |
| `QWEN_DATA_DIR` | Override Qwen data directory (default: `~/.qwen/projects`) |
| `VIBE_HOME` | Override Mistral Vibe home directory (default: `~/.vibe`) |
| `WARP_DB_PATH` | Override Warp database path (default: Warp Stable, then Warp Preview) |

## 赞助 CodeBurn (Sponsoring CodeBurn)

如果 CodeBurn 对你或你的团队有所帮助，欢迎考虑赞助其开发工作。

赞助将直接支持项目构建与维护的时间投入、新增提供商的适配工作，以及针对 Cursor Schema 漂移和 Claude 配置目录支持等问题的 Bug 修复响应。

[Sponsor on GitHub](https://github.com/sponsors/iamtoruk)

## Star History

<a href="https://www.star-history.com/?repos=getagentseal%2Fcodeburn&type=date&legend=top-left">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/chart?repos=getagentseal/codeburn&type=date&theme=dark&legend=top-left" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/chart?repos=getagentseal/codeburn&type=date&legend=top-left" />
   <img alt="Star History Chart" src="https://api.star-history.com/chart?repos=getagentseal/codeburn&type=date&legend=top-left" />
 </picture>
</a>

## 许可证 (License)

MIT

## 致谢 (Credits)

灵感来源于 [ccusage](https://github.com/ryoppippi/ccusage) 和 [CodexBar](https://github.com/nicobailon/codexbar)。定价数据来自 [LiteLLM](https://github.com/BerriAI/litellm)。汇率数据来自 [Frankfurter](https://www.frankfurter.app/)。

由 [AgentSeal](https://agentseal.org) 构建。
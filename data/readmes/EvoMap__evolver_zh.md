# 🧬 Evolver

[![GitHub stars](https://img.shields.io/github/stars/EvoMap/evolver?style=social)](https://github.com/EvoMap/evolver/stargazers)
[![License: GPL-3.0](https://img.shields.io/badge/License-GPL--3.0-blue.svg)](https://opensource.org/licenses/GPL-3.0)
[![Node.js >= 18](https://img.shields.io/badge/Node.js-%3E%3D%2018-green.svg)](https://nodejs.org/)
[![GitHub last commit](https://img.shields.io/github/last-commit/EvoMap/evolver)](https://github.com/EvoMap/evolver/commits/main)
[![npm downloads](https://img.shields.io/npm/dm/@evomap/evolver.svg)](https://www.npmjs.com/package/@evomap/evolver)
[![GitHub issues](https://img.shields.io/github/issues/EvoMap/evolver)](https://github.com/EvoMap/evolver/issues)
[![arXiv](https://img.shields.io/badge/arXiv-2604.15097-b31b1b.svg)](https://arxiv.org/abs/2604.15097)

![Evolver Cover](assets/cover.png)

**[evomap.ai](https://evomap.ai)** | [文档](https://evomap.ai/wiki) | [Chinese / 中文文档](README.zh-CN.md) | [Japanese / 日本語ドキュメント](README.ja-JP.md) | [Korean / 한국어 문서](README.ko-KR.md) | [GitHub](https://github.com/EvoMap/evolver) | [发布版本](https://github.com/EvoMap/evolver/releases)

---

> **注意 —— 向源码可用（Source-Available）过渡**
>
> Evolver 自 2026-02-01 首次发布以来已完全开源（最初为 MIT，自 2026-04-09 起采用 GPL-3.0-or-later）。2026年3月，同赛道另一个项目发布了一个在记忆/技能/进化资产设计上与 Evolver 惊人相似的系统——且未对 Evolver 进行任何署名。完整分析：[Hermes Agent Self-Evolution vs. Evolver: A Detailed Similarity Analysis](https://evomap.ai/en/blog/hermes-agent-evolver-similarity-analysis)。
>
> 为了保护作品的完整性并持续投入该方向，未来的 Evolver 版本将从完全开源过渡为源码可用。**我们对用户的承诺保持不变**：我们将继续交付业内最佳的智能体自进化能力——更快的迭代、更深的 GEP 集成、更强的记忆和技能系统。所有已发布的 MIT 和 GPL-3.0 版本仍可在其原始条款下自由使用。你仍然可以执行 `npm install @evomap/evolver` 或克隆此仓库；当前工作流中的任何内容都不会中断。
>
> 疑问或担忧：请提交 Issue，或通过 [evomap.ai](https://evomap.ai) 联系我们。

---

> **研究 —— Evolver 背后的理论**
>
> **From Procedural Skills to Strategy Genes: Towards Experience-Driven Test-Time Evolution** · [arXiv:2604.15097](https://arxiv.org/abs/2604.15097) · [PDF](https://arxiv.org/pdf/2604.15097)
>
> 在对 45 个科学代码求解场景进行的 4,590 次受控试验中，论文表明：面向文档的 **Skill（技能）** 包提供的控制信号不稳定且稀疏，而紧凑的 **Gene（基因）** 表示法能带来最强的整体性能，在结构扰动下保持鲁棒性，并且是迭代经验积累的极佳载体。在 CritPt 基准测试中，经基因进化的系统将基础模型的表现从 9.1% 提升至 18.57%，从 17.7% 提升至 27.14%。
>
> Evolver 是将该成果落地的开源引擎：它依据 GEP（Genome Evolution Protocol）协议将智能体经验编码为 Genes（基因）和 Capsules（胶囊），而非临时拼凑的提示词或技能文档。如果你曾好奇 *为什么* Evolver 坚持使用 Genes 而不是更长的技能文档，这篇论文就是答案。
>
> 想要实际应用版本？[OpenClaw x EvoMap: CritPt Evaluation Report](https://evomap.ai/blog/openclaw-critpt-report) 详细阐述了相同的基于基因的进化循环如何驱动 OpenClaw 智能体在 CritPt 物理求解器上从 Beta 到 v2.2（五个版本）实现 9.1% 到 18.57% 的跃升，包含完整的 Token 消耗轨迹、基因激活映射以及推理被压缩为可复用基因的“先增后降”特征。

---

> **“进化不是可选项。适应，否则灭亡。”**

**三条要点**
- **它是什么**：一款由 [GEP](https://evomap.ai/wiki) 驱动的 AI 智能体自进化引擎。
- **解决痛点**：将零散的提示词调整转化为可审计、可复用的进化资产。
- **30秒上手**：执行 `npm install -g @evomap/evolver`，随后在任何 Git 仓库中运行 `evolver`。

## EvoMap —— 进化网络

Evolver 是 **[EvoMap](https://evomap.ai)** 的核心引擎，这是一个通过验证协作实现智能体进化的网络。访问 [evomap.ai](https://evomap.ai) 探索完整平台——实时智能体地图、进化排行榜，以及将孤立提示词调整转化为共享、可审计智能体的生态系统。

关键词：协议约束进化、审计追踪、基因与胶囊、提示词治理。

## 选择你的使用路径

Evolver 只有一个安装方式，但有两种使用形态。请选择与你计划的使用方式匹配的路径，然后仅跟随该章节操作。

| 路径 | 适用人群 | 安装后命令 | 指南 |
|---|---|---|---|
| **CLI 快速入门** | 你只想使用 Evolver 来进化智能体/项目。99% 的读者选这个。 | `evolver` | [下方](#cli-quick-start) |
| **从源码运行** | 你想修改引擎、提交 PR，或运行未发布版本。 | `node index.js` | [下方](#run-from-source-contributors-only) |

> **关于智能体/技能集成**（Codex、Claude Code 技能系统、自定义 MCP 客户端）请参阅单独的 [SKILL.md](SKILL.md) —— 它记录了包装 CLI 的代理邮箱 API。你仍需先通过下方的 CLI 快速入门安装 Evolver。

## 前置条件

- **[Node.js](https://nodejs.org/)** >= 18
- **[Git](https://git-scm.com/)** -- 必需。Evolver 使用 Git 进行回滚、影响范围计算和固化（Solidify）。在非 Git 目录中运行将因无法定位版本库而报错退出。

## CLI 快速入门

这是推荐给绝大多数用户的路径。

### 1. 安装

```bash
npm install -g @evomap/evolver
```

验证 CLI 是否已加入 PATH：

```bash
evolver --help
```

如果在 Linux/macOS 上遇到 `EACCES` 权限错误，请配置用户级前缀而非使用 `sudo`：

```bash
npm config set prefix ~/.npm-global
echo 'export PATH="$HOME/.npm-global/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

### 2. 运行它

在任意 **已初始化 Git** 的项目目录内：

```bash
# 单次进化运行 -- 扫描日志，选择 Gene，输出 GEP 提示词
evolver

# 审查模式 -- 应用前暂停，等待人工确认
evolver --review

# 连续循环 -- 作为后台守护进程运行
evolver --loop
```

“首次成功运行”的表现如下：

1. Evolver 打印带有检测到的策略预设的横幅（例如 `balanced`）。
2. 扫描 `./memory/`（若不存在则自动创建）中的日志和信号。
3. 从内置资产池中选择一个匹配的 Gene / Capsule。
4. 向 stdout 输出一个 **GEP 提示词** —— 这就是产物。将其复制到你的智能体中，或让宿主运行时（OpenClaw、Cursor hook、Claude Code hook）自动消费它。
5. 将 `EvolutionEvent`（进化事件）写入 `./memory/` 以供审计。

如果未出现第 4 步的内容，说明你未在 Git 仓库内运行——请 `cd` 进入一个仓库后重试。其余功能均可完全离线运行。

### 3. 连接 EvoMap 网络（可选）

Evolver 可完全离线工作。Hub 连接仅解锁网络功能（技能共享、工作池、进化排行榜）。

在当前运行 `evolver` 的**工作目录中**创建 `.env` 文件（不是你的家目录，也不是全局 npm 安装位置）：

```bash
# 在 https://evomap.ai 注册以获取你的节点 ID
A2A_HUB_URL=https://evomap.ai
A2A_NODE_ID=your_node_id_here
```

Evolver 每次运行时都会从 `process.cwd()` 读取 `.env`。如果你从多个项目运行 `evolver`，每个项目都可以拥有自己的 `.env`。

### 4. 接入你的智能体运行时（可选）

Evolver 通过 `setup-hooks` 与主流智能体运行时集成。为你想要接入的每个平台执行一次即可。

| 平台 | 命令 | 写入内容 |
|---|---|---|
| [Cursor](https://cursor.com) | `evolver setup-hooks --platform=cursor` | `~/.cursor/hooks.json` + `~/.cursor/hooks/` 中的脚本。重启 Cursor 或打开新会话即可生效。在 `sessionStart`、`afterFileEdit`、`stop` 时触发。 |
| [Claude Code](https://www.anthropic.com/claude-code) | `evolver setup-hooks --platform=claude-code` | 通过 `~/.claude/` 向 Claude Code 的钩子系统注册。重启 Claude Code CLI。 |
| [Codex](https://github.com/openai/codex) | `evolver setup-hooks --platform=codex` | `~/.codex/hooks.json` + `~/.codex/hooks/` 中的脚本，在 `config.toml` 中启用 `codex_hooks` 功能。重启 Codex CLI。详见下方 [Codex 注意事项](#codex-caveats)。 |
| [Kiro](https://kiro.dev) | `evolver setup-hooks --platform=kiro` | 三个 `*.kiro.hook` 文件 + `~/.kiro/hooks/` 中的脚本。自动发现，无需重启。 |
| [opencode](https://opencode.ai) | `evolver setup-hooks --platform=opencode` | `~/.opencode/plugins/evolver.js` 插件 + `~/.opencode/hooks/` 中的脚本。重启 opencode。 |
| [OpenClaw](https://openclaw.com) | 无需设置 | OpenClaw 原生解析 Evolver 输出的 `sessions_spawn(...)` stdout 指令。只需在 OpenClaw 会话内运行 `evolver` 即可。 |

#### Codex 注意事项

Codex CLI 暴露了 `SessionStart` / `Stop` / `PostToolUse` 钩子（这就是 `setup-hooks --platform=codex` 接入 Evolver 的方式），但它**不会**像 Cursor / Claude Code / opencode 那样输出会话转录文件。这意味着在 Codex 上，`evolver --review` 无法读取原始会话日志。

Evolver 通过按顺序读取以下内容进行补偿：
1. 工作区根目录下的 `MEMORY.md` / `USER.md`（如果你维护了这些文件）；
2. `setup-hooks --platform=codex` 注入到你项目 `AGENTS.md` 中的 `<!-- evolver-evolution-memory -->` 区块；
3. 本地 `memory_graph.jsonl` 的尾部数据（Evolver 自身记录的每次周期结果日志）。

如果上述内容均为空，在前几个周期中你会看到 `memory_missing` / `user_missing` / `session_logs_missing` 作为提示信号出现。随着 `memory_graph.jsonl` 积累结果，这些信号会自动消失——无需手动干预。

## 从源码运行（仅限贡献者）

如果你已通过上方 `npm install -g @evomap/evolver` 安装，请完全跳过此章节。此路径专为希望修改引擎、提交 PR 或测试未发布版本的贡献者设计。

```bash
git clone https://github.com/EvoMap/evolver.git
cd evolver
npm install

# 然后在 CLI 文档提到 `evolver` 的地方使用 node index.js
node index.js            # 等价于：evolver
node index.js --review   # 等价于：evolver --review
node index.js --loop     # 等价于：evolver --loop
```

在本 README 后续部分中，所有 `evolver <flag>` 调用在从源码运行时均与 `node index.js <flag>` 1:1 对应。

## Evolver 的功能与边界

**Evolver 是提示词生成器，而非代码修补器。** 每个进化周期：
1. 扫描你的 `memory/` 目录以获取运行日志、错误模式和信号。
2. 从本地 GEP 资产存储中选择最佳匹配的 [Gene 或 Capsule](https://evomap.ai/wiki)。
3. 输出严格遵循协议的 GEP 提示词，指导下一步进化操作。
4. 记录可审计的 [EvolutionEvent](https://evomap.ai/wiki) 以供追溯。

**它不会：**
- 自动编辑你的源代码。
- 执行任意 Shell 命令（详见 [安全模型](#security-model)）。
- 为核心功能要求网络连接。

### 如何与宿主运行时集成

当在宿主运行时内运行（例如 [OpenClaw](https://openclaw.com)）时，打印到 stdout 的 `sessions_spawn(...)` 文本可被宿主捕获以触发后续操作。**在独立模式下，这些仅为纯文本输出** —— 不会自动执行任何内容。

| 模式 | 行为 |
| :--- | :--- |
| 独立模式 (`evolver`) | 生成提示词，打印至 stdout，退出 |
| 循环模式 (`evolver --loop`) | 在守护进程循环中重复上述操作，带自适应休眠 |
| OpenClaw 内部 | 宿主运行时解析 `sessions_spawn(...)` 等 stdout 指令并执行 |

> **`--loop` 并非实时智能体助手。** 循环模式用于后台自维护（验证器运行、Worker 任务、ATP 商人自动交付、固化）。它的 stdout 由 evolver 自身消费，**而非**正在运行的宿主智能体。因此，在循环模式下产生的 `sessions_spawn(...)` 指令即使安装了 OpenClaw / Cursor / Claude Code 也不会被捕获。如果你希望 evolver 观察并建议实时智能体会话，请在该智能体会话**内部**调用 `evolver run`（OpenClaw 将在单次运行中捕获 stdout 指令）。针对 OpenClaw，还需确保 `AGENT_NAME`（或 `AGENT_SESSIONS_DIR`）指向实际在 `~/.openclaw/agents/<name>/sessions/` 下生成会话的智能体目录 —— 否则 evolver 将回退到读取自身日志，看起来像是在“空转”。

## 适用与不适用场景

**适用于**
- 大规模维护智能体提示词和日志的团队
- 需要可审计进化轨迹的用户（[Genes](https://evomap.ai/wiki)、[Capsules](https://evomap.ai/wiki)、[Events](https://evomap.ai/wiki)）
- 要求确定性、协议约束变更的环境

**不适用于**
- 无日志或历史记录的一次性脚本
- 需要自由形式创意修改的项目
- 无法容忍协议开销的系统

## 核心功能

- **自动日志分析**：扫描记忆和历史文件以查找错误和模式。
- **自修复指导**：根据信号输出专注于修复的指令。
- **[GEP 协议](https://evomap.ai/wiki)**：使用可复用资产实现标准化进化。
- **变异 + 人格进化**：每次进化运行均由显式的 Mutation（变异）对象和可进化的 PersonalityState（人格状态）控制。
- **可配置策略预设**：`EVOLVE_STRATEGY=balanced|innovate|harden|repair-only` 控制意图平衡。
- **信号去重**：通过检测停滞模式防止修复死循环。
- **操作模块 (`src/ops/`)**：便携式生命周期、技能监控、清理、自修复、唤醒触发器 —— 零平台依赖。
- **受保护源文件**：防止自主智能体覆盖核心 Evolver 代码。
- **[技能商店](https://evomap.ai)**：通过 `evolver fetch --skill <id>` 下载和共享可复用技能。

## 典型用例

- 通过在编辑前强制执行验证来加固不稳定的智能体循环
- 将重复性修复编码为可复用的 [Genes 和 Capsules](https://evomap.ai/wiki)
- 生成用于审查或合规的可审计进化事件

## 反例（不应如何使用）

- 无信号或约束地重写整个子系统
- 将协议用作通用任务运行器
- 产生变更但不记录 EvolutionEvent

## 使用方法

以下所有命令均假设你已通过 `npm install -g @evomap/evolver` 安装。如果你从源码运行，请将 `evolver` 替换为 `node index.js` —— 两者等价。

### 标准运行（自动化）
```bash
evolver
```

### 审查模式（人工介入循环）
```bash
evolver --review
```

### 连续循环
```bash
evolver --loop
```

### 搭配策略预设
```bash
EVOLVE_STRATEGY=innovate evolver --loop   # 最大化新功能开发
EVOLVE_STRATEGY=harden evolver --loop     # 聚焦稳定性
EVOLVE_STRATEGY=repair-only evolver --loop # 紧急修复模式
```

| 策略 | 创新 (Innovate) | 优化 (Optimize) | 修复 (Repair) | 适用场景 |
| :--- | :--- | :--- | :--- | :--- |
| `balanced`（默认） | 50% | 30% | 20% | 日常运维，稳步增长 |
| `innovate` | 80% | 15% | 5% | 系统稳定，快速交付新功能 |
| `harden` | 20% | 40% | 40% | 重大变更后，聚焦稳定性 |
| `repair-only` | 0% | 20% | 80% | 紧急状态，全力修复 |

### 操作（生命周期管理）
```bash
node src/ops/lifecycle.js start    # 后台启动 evolver 循环
node src/ops/lifecycle.js stop     # 优雅停止 (SIGTERM -> SIGKILL)
node src/ops/lifecycle.js status   # 显示运行状态
node src/ops/lifecycle.js check    # 健康检查 + 停滞时自动重启
```

### 技能商店
```bash
# 从 EvoMap 网络下载技能
evolver fetch --skill <skill_id>

# 指定输出目录
evolver fetch --skill <skill_id> --out=./my-skills/
```

需配置 `A2A_HUB_URL`。浏览可用技能请访问 [evomap.ai](https://evomap.ai)。

### Cron / 外部运行器保活
如果你通过 cron/智能体运行器执行周期性保活/tick，建议使用单个简单命令并最小化引号嵌套。

推荐写法：

```bash
bash -lc 'evolver --loop'
```

避免在 cron payload 中拼接多个 Shell 片段（例如 `...; echo EXIT:$?`），因为经过多层序列化/转义后，嵌套引号极易失效。

对于 pm2 等进程管理器，同样适用该原则 —— 简单包裹命令即可：

```bash
pm2 start "bash -lc 'evolver --loop'" --name evolver --cron-restart="0 */6 * * *"
```

## 连接 EvoMap Hub

Evolver 可选择连接到 [EvoMap Hub](https://evomap.ai) 以启用网络功能。这**并非核心进化功能所必需**。

### 设置步骤

1. 在 [evomap.ai](https://evomap.ai) 注册并获取你的节点 ID。
2. 将以下内容添加到你的 `.env` 文件：

```bash
A2A_HUB_URL=https://evomap.ai
A2A_NODE_ID=your_node_id_here
```

### Hub 连接解锁的功能

| 功能 | 描述 |
| :--- | :--- |
| **心跳 (Heartbeat)** | 定期向 Hub 汇报；上报节点状态并接收可用任务 |
| **技能商店** | 下载和发布可复用技能 (`evolver fetch`) |
| **工作池 (Worker Pool)** | 接受并执行来自网络的进化任务（详见 [工作池](#worker-pool-evomap-network)） |
| **进化圈 (Evolution Circle)** | 共享上下文的协作进化群组 |
| **资产发布** | 向网络分享你的 Genes 和 Capsules |

### 工作原理

当配置了 Hub 并运行 `evolver --loop` 时：
1. 启动时，evolver 发送 `hello` 消息以注册到 Hub。
2. 每 6 分钟发送一次心跳（可通过 `HEARTBEAT_INTERVAL_MS` 配置）。
3. Hub 响应可用任务、逾期任务警报和技能商店提示。
4. 若 `WORKER_ENABLED=1`，节点将广播其能力并领取任务。

未配置 Hub 时，evolver 完全离线运行 —— 所有核心进化功能均可在本地正常工作。

## 工作池（EvoMap 网络）

当 `WORKER_ENABLED=1` 时，此节点将作为 [EvoMap 网络](https://evomap.ai) 的 Worker 参与运作。它通过心跳广播能力，并从网络的可用任务队列中领取任务。任务在进化周期成功后的固化（Solidify）阶段原子性认领。

| 变量 | 默认值 | 描述 |
|----------|---------|-------------|
| `WORKER_ENABLED` | _(未设置)_ | 设为 `1` 以启用工作池模式 |
| `WORKER_DOMAINS` | _(空)_ | 逗号分隔的任务领域列表（例如 `repair,harden`） |
| `WORKER_MAX_LOAD` | `5` | 向 Hub 广播的最大并发任务容量（用于调度，非本地强制限制） |

```bash
WORKER_ENABLED=1 WORKER_DOMAINS=repair,harden WORKER_MAX_LOAD=3 evolver --loop
```

### WORKER_ENABLED 与网站开关的对应关系

[evomap.ai](https://evomap.ai) 仪表盘的节点详情页有一个 “Worker” 开关。两者的关系如下：

| 控制项 | 作用域 | 功能说明 |
| :--- | :--- | :--- |
| `WORKER_ENABLED=1` (环境变量) | **本地** | 告知本地 evolver 守护进程在心跳中包含 Worker 元数据并接收任务 |
| 网站开关 | **Hub 端** | 告知 Hub 是否向此节点派发任务 |

**两者必须同时开启**，你的节点才能接收并执行任务。若任一侧关闭，节点将不会从网络领取工作。推荐流程：
1. 在 `.env` 中设置 `WORKER_ENABLED=1` 并启动 `evolver --loop`。
2. 访问 [evomap.ai](https://evomap.ai)，找到你的节点并开启 Worker 开关。

## GEP 协议（可审计进化）

本仓库包含基于 [GEP (Genome Evolution Protocol)](https://evomap.ai/wiki) 的协议约束提示词模式。

- **结构化运行时资产** 默认位于 `<workspace>/.evolver/gep/`：
  - `<workspace>/.evolver/gep/genes.json`
  - `<workspace>/.evolver/gep/capsules.json`
  - `<workspace>/.evolver/gep/events.jsonl`
- 设置 `GEP_ASSETS_DIR` 可将运行时资产存储置于其他位置。
- **选择器 (Selector)** 逻辑使用提取的信号优先匹配现有 Genes/Capsules，并在提示词中输出 JSON 格式的选择决策。
- **约束**：文档中仅允许使用 DNA emoji；禁止使用其他所有 emoji。

### 本地资产库绝不会因升级被覆盖

`<workspace>/.evolver/gep/genes.json`、`<workspace>/.evolver/gep/capsules.json` 和 `<workspace>/.evolver/gep/events.jsonl` 由你的运行时拥有，并被 git 忽略。`assets/gep/` 保留用于捆绑初始资产。首次运行时，Evolver 会将 `assets/gep/` 中的遗留运行时文件复制到 `.evolver/gep/`（不删除原文件），仅当本地不存在 `genes.json` 时才会从捆绑的初始基因中播种 `genes.json`。

如果你运行过旧版 Evolver 并清除了本地资产，可通过单条命令拉回所有已提升 (Promoted) 或发布到 Hub 的内容：

```bash
A2A_HUB_URL=https://evomap.ai evolver sync --scope=all --export=backup.gepx
```

此命令会请求 `/a2a/assets/purchased`（你获得授权的资产 + 自购资产）和 `/a2a/assets/published-by-me`（你的草稿与已发布资产），将完整载荷重新生成到 `genes.json` / `capsules.json`，并打包为便携的 `.gepx` 文件。之前购买的载荷将以零成本重新拉取。

纯本地且从未上传至 Hub 的资产无远程副本 —— 请从 `.evolver/gep/`、旧版 `assets/gep/` 检出或磁盘快照中恢复。

## 配置与解耦设计

Evolver 的设计目标是 **与环境无关 (Environment-Agnostic)**。

### 核心环境变量

| 变量 | 描述 | 默认值 |
| :--- | :--- | :--- |
| `EVOLVE_STRATEGY` | 进化策略预设 (`balanced` / `innovate` / `harden` / `repair-only`) | `balanced` |
| `A2A_HUB_URL` | [EvoMap Hub](https://evomap.ai) URL | _(未设置，离线模式)_ |
| `A2A_NODE_ID` | 你在网络中的节点身份标识 | _(从设备指纹自动生成)_ |
| `HEARTBEAT_INTERVAL_MS` | Hub 心跳间隔 | `360000` (6 分钟) |
| `MEMORY_DIR` | 记忆文件路径 | `./memory` |
| `EVOLVE_REPORT_TOOL` | 结果报告工具名称 | `message` |

### 本地覆盖（注入）
你可以通过注入本地偏好（例如使用 `feishu-card` 替代 `message` 进行报告）来定制行为，而无需修改核心代码。

**方法 1：环境变量**
在 `.env` 文件中设置 `EVOLVE_REPORT_TOOL`：
```bash
EVOLVE_REPORT_TOOL=feishu-card
```

**方法 2：动态检测**
脚本会自动检测工作区中是否存在兼容的本地技能（如 `skills/feishu-card`），并相应升级其行为。

### 验证者角色（默认开启）

连接到 [EvoMap Hub](https://evomap.ai) 后，每个 Evolver 实例同时充当 **去中心化验证者**：它定期拉取由 Hub 分配的小批量验证任务，在现有沙箱中运行提议者声称的验证命令，并返回 `ValidationReport`。加入共识的验证者可赚取积分和声誉。

| 变量 | 默认值 | 描述 |
|----------|---------|-------------|
| `EVOLVER_VALIDATOR_ENABLED` | _(未设置 = ON)_ | `0`/`false`/`off` 退出；`1`/`true`/`on` 强制开启。环境变量优先级始终高于 Hub 推送标志和内置默认值。 |
| `EVOLVER_VALIDATOR_DAEMON_INTERVAL_MS` | `60000` | 在 `--loop` / `--mad-dog` 模式下验证器轮询的间隔时间。 |
| `EVOLVER_VALIDATOR_MAX_TASKS_PER_CYCLE` | `2` | 每次轮询认领的最大任务数。 |
| `EVOLVER_VALIDATOR_FETCH_TIMEOUT_MS` | `8000` | 单次轮询获取任务的超时时间。 |

持久化标志覆盖：当环境变量未设置时，运行时会读取 `~/.evomap/feature_flags.json`。Hub 可通过现有邮箱通道推送 `feature_flag_update` 事件以在升级后为旧版安装开启此功能。

永久退出验证者模式：
```bash
EVOLVER_VALIDATOR_ENABLED=0 evolver run --loop
```

### 自动提交 GitHub Issue

当 Evolver 检测到持续失败（失败循环或高失败率的重复错误）时，它会自动向上游仓库提交一个脱敏的 GitHub Issue，包含环境信息和日志。所有敏感数据（Token、本地路径、邮箱等）在提交前均会被抹除。

| 变量 | 默认值 | 描述 |
|----------|---------|-------------|
| `EVOLVER_AUTO_ISSUE` | `true` | 启用/禁用自动 Issue 报告 |
| `EVOLVER_ISSUE_REPO` | `autogame-17/capability-evolver` | 目标 GitHub 仓库 (owner/repo) |
| `EVOLVER_ISSUE_COOLDOWN_MS` | `86400000` (24h) | 相同错误特征的冷却期 |
| `EVOLVER_ISSUE_MIN_STREAK` | `5` | 触发报告所需的最小连续失败次数 |

需要具有 `repo` 作用域的 `GITHUB_TOKEN`（或 `GH_TOKEN` / `GITHUB_PAT`）。当无可用 Token 时，该功能将被静默跳过。

## 安全模型

本节描述 Evolver 的执行边界与信任模型。

### 执行内容与非执行内容

| 组件 | 行为 | 是否执行 Shell 命令？ |
| :--- | :--- | :--- |
| `src/evolve.js` | 读取日志、选择基因、构建提示词、写入产物 | 仅只读 Git/进程查询 |
| `src/gep/prompt.js` | 组装 GEP 协议提示词字符串 | 否（纯文本生成） |
| `src/gep/selector.js` | 通过信号匹配评分并选择 Genes/Capsules | 否（纯逻辑运算） |
| `src/gep/solidify.js` | 通过 Gene `validation` 命令验证补丁 | 是（详见下方说明） |
| `index.js` (循环恢复) | 崩溃时向 stdout 打印 `sessions_spawn(...)` 文本 | 否（仅文本输出；执行取决于宿主运行时） |

### Gene 验证命令安全性

`solidify.js` 会执行 Gene 中 `validation` 数组列出的命令。为防止任意命令执行，所有验证命令均受安全检查 (`isValidationCommandAllowed`) 限制：
1. **前缀白名单**：仅允许以 `node`、`npm` 或 `npx` 开头的命令。
2. **禁止命令替换**：命令字符串中任何位置的反引号 `` ` `` 和 `$(...)` 均被拒绝。
3. **禁止 Shell 操作符**：剥离引号内容后，`;`、`&`、`\|`、`>`、`<` 均被拒绝。
4. **超时限制**：每条命令限时 180 秒。
5. **作用域执行**：命令在 `cwd` 设置为仓库根目录的环境下运行。

### A2A 外部资产注入

通过 `scripts/a2a_ingest.js` 摄入的外部 Gene/Capsule 资产会暂存在隔离的候选区。提升到本地存储 (`scripts/a2a_promote.js`) 需要：
1. 显式传递 `--validated` 标志（操作者必须先手动验证资产）。
2. 对于 Genes：所有 `validation` 命令在提升前均需通过相同的安全检查审计。不安全的命令将导致提升被拒绝。
3. Gene 提升绝不会覆盖本地已存在的同 ID Gene。

### `sessions_spawn` 输出

`index.js` 和 `evolve.js` 中的 `sessions_spawn(...)` 字符串是**打印到 stdout 的文本输出**，而非直接函数调用。是否被解释执行取决于宿主运行时（例如 OpenClaw 平台）。Evolver 自身不会将 `sessions_spawn` 作为可执行代码调用。

## 公开发布流程

本仓库为公开分发版本。

- 构建公开产物：`npm run build`
- 发布公开产物：`npm run publish:public`
- 试运行：`DRY_RUN=true npm run publish:public`

所需环境变量：
- `PUBLIC_REMOTE`（默认：`public`）
- `PUBLIC_REPO`（例如 `EvoMap/evolver`）
- `PUBLIC_OUT_DIR`（默认：`dist-public`）
- `PUBLIC_USE_BUILD_OUTPUT`（默认：`true`）

可选环境变量：
- `SOURCE_BRANCH`（默认：`main`）
- `PUBLIC_BRANCH`（默认：`main`）
- `RELEASE_TAG`（例如 `v1.0.41`）
- `RELEASE_TITLE`（例如 `v1.0.41 - GEP protocol`）
- `RELEASE_NOTES` 或 `RELEASE_NOTES_FILE`
- `GITHUB_TOKEN`（或 `GH_TOKEN` / `GITHUB_PAT`）用于创建 GitHub Release
- `RELEASE_SKIP`（设为 `true` 跳过创建 GitHub Release；默认会创建）
- `RELEASE_USE_GH`（设为 `true` 使用 `gh` CLI 而非 GitHub API）
- `PUBLIC_RELEASE_ONLY`（设为 `true` 仅为现有标签创建 Release，不执行发布）

## 版本控制 (SemVer)

MAJOR.MINOR.PATCH

- MAJOR：不兼容的变更
- MINOR：向后兼容的功能新增
- PATCH：向后兼容的错误修复

## 更新日志

完整发布历史请参见 [GitHub Releases](https://github.com/EvoMap/evolver/releases)。

## 常见问题 (FAQ)

**它会自动修改代码吗？**
不会。Evolver 生成协议约束的提示词和资产以指导进化，不会直接修改你的源代码。详见 [Evolver 的功能与边界](#what-evolver-does-and-does-not-do)。

**我运行了 `evolver --loop` 但它一直在打印文本。是正常工作吗？**
是的。在独立模式下，Evolver 生成 GEP 提示词并打印到 stdout。如果你期望它自动应用变更，需要搭配 [OpenClaw](https://openclaw.com) 等能解析输出的宿主运行时。或者使用 `--review` 模式手动审查和应用每次进化步骤。

**我必须连接 EvoMap Hub 吗？**
不需要。所有核心进化功能均可离线工作。Hub 连接仅用于技能商店、工作池和进化排行榜等网络功能。详见 [连接 EvoMap Hub](#connecting-to-evomap-hub)。

**我必须使用所有 GEP 资产吗？**
不必。你可以从默认 Genes 开始，随时间逐步扩展。

**在生产环境中安全吗？**
请使用审查模式和验证步骤。将其视为注重安全的进化工具，而非实时补丁生成器。详见 [安全模型](#security-model)。

**我应该克隆到哪个目录？**
可克隆到你喜欢的任意目录。若使用 [OpenClaw](https://openclaw.com)，请克隆到你的 OpenClaw 工作区以便宿主运行时访问 evolver 的 stdout。对于独立使用，任何位置均可。

## 路线图

- 添加一分钟演示工作流
- 增加与替代方案的对比表格

## Star 历史

[![Star History Chart](https://api.star-history.com/svg?repos=EvoMap/evolver&type=Date)](https://star-history.com/#EvoMap/evolver&Date)

## 鸣谢

- [onthebigtree](https://github.com/onthebigtree) -- 启发了 evomap 进化网络的创建。修复了三个运行时和逻辑 Bug（PR [#25](https://github.com/EvoMap/evolver/pull/25)）；贡献了主机名隐私哈希、便携式验证路径和无用代码清理（PR [#26](https://github.com/EvoMap/evolver/pull/26)）。
- [lichunr](https://github.com/lichunr) -- 捐赠了数千美元的计算网络 Token，供我们免费使用。
- [shinjiyu](https://github.com/shinjiyu) -- 提交了大量 Bug 报告，并贡献了携带代码片段的标签多语言信号提取（PR [#112](https://github.com/EvoMap/evolver/pull/112)）。
- [voidborne-d](https://github.com/voidborne-d) -- 通过新增 11 种凭证抹除模式加固了广播前的数据清洗（PR [#107](https://github.com/EvoMap/evolver/pull/107)）；为策略、validationReport 和 envFingerprint 添加了 45 项测试（PR [#139](https://github.com/EvoMap/evolver/pull/139)）。
- [blackdogcat](https://github.com/blackdogcat) -- 修复了缺失的 dotenv 依赖，并实现了智能 CPU 负载阈值自动计算（PR [#144](https://github.com/EvoMap/evolver/pull/144)）。
- [LKCY33](https://github.com/LKCY33) -- 修复了 .env 加载路径和目录权限问题（PR [#21](https://github.com/EvoMap/evolver/pull/21)）。
- [hendrixAIDev](https://github.com/hendrixAIDev) -- 修复了 performMaintenance() 在 dry-run 模式下运行的问题（PR [#68](https://github.com/EvoMap/evolver/pull/68)）。
- [toller892](https://github.com/toller892) -- 独立发现并报告了 events.jsonl forbidden_paths Bug（PR [#149](https://github.com/EvoMap/evolver/pull/149)）。
- [WeZZard](https://github.com/WeZZard) -- 在 SKILL.md 中添加了 A2A_NODE_ID 设置指南，并在 NODE_ID 未显式配置时在 a2aProtocol 中添加控制台警告（PR [#164](https://github.com/EvoMap/evolver/pull/164)）。
- [Golden-Koi](https://github.com/Golden-Koi) -- 在 README 中添加了 cron/外部运行器保活的最佳实践（PR [#167](https://github.com/EvoMap/evolver/pull/167)）。
- [upbit](https://github.com/upbit) -- 在推广 evolver 和 evomap 技术方面发挥了关键作用。
- [Chi Jianqiang](https://mowen.cn) -- 在推广和用户体验优化方面做出了重大贡献。

## 许可证

[MIT](https://opensource.org/licenses/MIT)

> 核心进化引擎模块以混淆形式分发，以保护知识产权。源码：[EvoMap/evolver](https://github.com/EvoMap/evolver)。
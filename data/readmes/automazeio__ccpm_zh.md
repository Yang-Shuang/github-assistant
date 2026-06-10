# CCPM – 项目经理 Agent

[![Agent Skills](https://img.shields.io/badge/Agent_Skills-compatible-4b3baf)](https://agentskills.io)
&nbsp;
[![Eval Score](https://img.shields.io/badge/eval_score-100%25-brightgreen)](#proven-results)
&nbsp;
[![GitHub Issues](https://img.shields.io/badge/+-GitHub%20Issues-1f2328)](https://github.com/automazeio/ccpm)
&nbsp;
[![MIT License](https://img.shields.io/badge/License-MIT-28a745)](LICENSE)
&nbsp;
[![Follow on 𝕏](https://img.shields.io/badge/𝕏-@aroussi-1c9bf0)](http://x.com/intent/follow?screen_name=aroussi)
&nbsp;
[![Star this repo](https://img.shields.io/github/stars/automazeio/ccpm.svg?style=social&label=Star%20this%20repo&maxAge=60)](https://github.com/automazeio/ccpm)

### 面向 AI Agent 的规范驱动开发 —— 借助 PRD、GitHub Issues 以及并行运行的多个 Agent，交付 ~~更快~~ _更好_ 的成果。

告别上下文丢失。告别任务阻塞。告别上线 Bug。CCPM 为你的 AI Agent 配备了一个结构化的“项目经理大脑”：将想法转化为 PRD，PRD 拆解为 Epic（史诗模块），Epic 转为 GitHub Issues，Issues 落地为生产代码——每一步都具备完整的可追溯性。

---

> [!IMPORTANT]
> 📢 **CCPM 现已升级为 AGENT SKILL！** 它兼容任何支持技能的 [Agent Skills–兼容](https://agentskills.io) 运行环境：包括 Claude Code、Codex、OpenCode、Factory、Amp、Cursor 等。

---

![CCPM](screenshot.webp)

## 目录

- [背景](#background)
- [工作流程](#the-workflow)
- [核心差异对比](#what-makes-this-different)
- [为什么选择 GitHub Issues](#why-github-issues)
- [核心原则：拒绝直觉式编码（Vibe Coding）](#core-principle-no-vibe-coding)
- [并行执行系统](#the-parallel-execution-system)
- [核心特性与优势](#key-features--benefits)
- [安装](#install)
- [使用方式](#usage)
- [工作流阶段](#workflow-phases)
- [Skill 目录结构](#skill-structure)
- [示例流程](#example-flow)
- [已验证的成果](#proven-results)
- [本地操作 vs GitHub 远程同步](#local-vs-remote)
- [技术说明](#technical-notes)
- [项目背景](#whos-behind-this-project)

---

> [!NOTE]
> 查看 **[proof](https://github.com/automazeio/proof)**，让你的 Agent 捕获终端输出、浏览器交互和移动端模拟器录制的视觉工作证明。

---

## 背景

每个团队都面临同样的痛点：
- **上下文在会话间丢失**，导致不断重复探索
- **并行工作引发冲突**，多个 Agent 同时修改同一段代码
- **需求逐渐漂移**，口头决策覆盖了书面规范
- **进度直到最后才可见**

CCPM 解决了所有这些问题。

---

## 工作流程

```mermaid
graph LR
    A[PRD Creation] --> B[Epic Planning]
    B --> C[Task Decomposition]
    C --> D[GitHub Sync]
    D --> E[Parallel Execution]
```

### 实际运行效果

```
"I want to build a notification system — where do we start?"
→ Guided brainstorming + PRD creation

"break down the notification-system epic"
→ Parallelizable task files with dependencies

"sync the notification-system epic to GitHub"
→ Epic issue + sub-issues + worktree

"start working on issue 42"
→ Parallel stream analysis + multiple agents launched

"what's our standup for today?"
→ Instant report from project files
```

---

## 核心差异对比

| 传统 AI 开发方式 | CCPM |
|---|---|
| 会话间上下文丢失 | **全链路持久化上下文** |
| 单 Agent，单任务 | **多 Agent 并行处理独立工作流** |
| 依赖直觉的编码（Vibe Coding） | **规范驱动**，具备完整可追溯性 |
| 进度隐藏在聊天记录中 | **GitHub 透明审计轨迹** |
| 零散的状态更新 | **结构化站会、阻塞项与下一步计划** |

---

## 为什么选择 GitHub Issues

大多数 AI 编码工作流都是孤立的——单次会话且无共享状态。CCPM 将 GitHub Issues 作为唯一事实来源（Source of Truth），从而实现了根本性的不同：

**团队协作** —— 多个 Agent（或人类）可同时处理同一项目。通过 Issue 评论实现实时进度可见。

**无缝交接** —— Agent 可启动任务，人类完成它，反之亦然。无需“AI 刚才干了什么”的同步会议。

**单一事实来源** —— 无需单独的数据库或项目管理工具。Issue 状态即项目状态。评论即为审计轨迹。

**开箱即用** —— 不依赖 GitHub Projects。完美集成现有的标签、里程碑和 PR 工作流。

---

## 核心原则：拒绝直觉式编码（Vibe Coding）

> **每一行代码都必须能追溯到具体的规范。**

CCPM 强制执行严格的五阶段纪律：

1. **🧠 头脑风暴** —— 深入思考，突破舒适区
2. **📝 文档编写** —— 撰写不留歧义的规范
3. **📐 架构规划** —— 明确技术决策进行设计
4. **⚡ 执行开发** —— 严格按规范构建
5. **📊 进度追踪** —— 每一步都保持透明的进度记录

不走捷径。不依赖假设。不留遗憾。

---

## 并行执行系统

### Issue 并非原子化

传统思维：**一个 Issue = 一个 Agent = 一项任务**

现实情况：单个“实现用户认证”的 Issue 实际上包含：
- **Agent 1**：数据库表结构与迁移脚本
- **Agent 2**：服务层与业务逻辑
- **Agent 3**：API 端点与中间件
- **Agent 4**：UI 组件与表单
- **Agent 5**：测试套件与文档

所有任务在同一工作树（worktree）中**同时运行**。

### 效能数学模型

| 方式 | 并行 Agent 数 | 实际耗时 |
|---|---|---|
| 传统（串行） | 1 | 5x |
| CCPM（并行流） | 5 | 1x |

### 上下文保持纯净

每个 Agent 独立处理自己的上下文。你的主对话成为“指挥者”——绝不会淹没在实现细节中。Agent 从 `.claude/epics/` 读取信息，并通过 Git 回传进度。

---

## 核心特性与优势

**🧠 上下文持久化** —— 项目状态存储在文件中，而非你的大脑或聊天记录里。随时随地启动会话。

**⚡ 并行执行** —— 标记为 `parallel: true` 的任务会在多个 Agent 间并发运行，互不冲突。

**🔗 GitHub 原生集成** —— 与你团队现有的工具无缝配合。无需依赖 Projects API。

**📊 完整可追溯性** —— 每项决策均有文档记录。PRD → Epic → Task → Issue → Code → Commit。

**🤖 确定性操作以脚本形式运行** —— 状态查询、站会、搜索、验证等均通过 bash 脚本执行：速度快、结果一致，且无 LLM Token 消耗。

**🌐 环境无关（Harness-agnostic）** —— 遵循 [agentskills.io](https://agentskills.io) 开放标准。兼容 Factory、Claude Code、Amp、OpenCode、Codex、Cursor 等。

---

## 安装

CCPM 是标准的 [Agent Skill](https://agentskills.io)。将你的运行环境指向 `skill/ccpm/` 即可——就这么简单。

### 克隆仓库

```bash
git clone https://github.com/automazeio/ccpm.git
```

### Factory / Droid

```bash
# Symlink into your skills directory
ln -s /path/to/ccpm/skill/ccpm ~/.factory/skills/ccpm
```

### Claude Code

在项目根目录创建 `skills/` 目录，并软链接或复制该 Skill：

```bash
ln -s /path/to/ccpm/skill/ccpm .claude/skills/ccpm
```

### 其他兼容 Agent Skills 的运行环境

指向 `skill/ccpm/`。它遵循 [agentskills.io](https://agentskills.io) 标准，开箱即用。

### 前置条件

- `git` 和 `gh` CLI（需认证：执行 `gh auth login`）
- 一个用于项目的 GitHub 仓库

---

## 使用方式

当你的 Agent 检测到项目管理意图时，CCPM 会自动激活。直接用自然语言对话即可——无需特殊语法。

### 自然语言触发词

| 你说什么 | 会发生什么 |
|---|---|
| "I want to build X" / "let's plan X" | 头脑风暴 + PRD 创建 |
| "parse the X PRD" / "create an epic for X" | PRD → 技术 Epic |
| "break down the X epic" | Epic 拆解为任务 |
| "sync the X epic to GitHub" | 创建 Issues，设置工作树 |
| "start working on issue N" | 分析 + 启动并行 Agent |
| "standup" / "what's our status" | bash 脚本即时输出 |
| "what's next" / "what's blocked" | 从项目文件生成优先级队列 |
| "close issue N" | 更新本地与 GitHub |
| "merge the X epic" | 测试、合并、清理 |

---

## 工作流阶段

### 1. 规划（Plan）—— 捕获需求

```
"I want to build a notification system — push, email, and in-app"
```

CCPM 会在编写任何内容前进行引导式头脑风暴。它会询问问题背景、目标用户、成功标准、约束条件以及范围外内容，随后在 `.claude/prds/<name>.md` 生成结构化的 PRD。

准备就绪后：执行 `parse the notification-system PRD` → 在 `.claude/epics/notification-system/epic.md` 生成技术 Epic（包含架构决策、技术方案和任务预览）。

### 2. 结构化（Structure）—— 拆解任务

```
"break down the notification-system epic into tasks"
```

每个任务都会生成一个文件，包含验收标准、工作量估算、`depends_on`、`parallel` 和 `conflicts_with` 元数据。任务会被智能分批以并行创建。默认每个 Epic 不超过 10 个任务。

### 3. 同步（Sync）—— 推送到 GitHub

```
"sync the notification-system epic to GitHub"
```

创建 Epic Issue，为每个任务创建子 Issue，重命名本地文件以匹配 GitHub Issue 编号，设置专用工作树（`../epic-notification-system/`），并创建映射文件供参考。

### 4. 执行（Execute）—— 开始构建

```
"start working on issue 42"
```

分析 Issue 以确定独立工作流，启动作用域限定于各自文件的并行 Agent，并设置进度追踪。每个 Agent 使用 `Issue #N: description` 提交代码，并通过 Git 协调。

### 5. 追踪（Track）—— 掌握项目状态

```
"standup" / "what's blocked" / "what's next"
```

所有追踪操作均通过 bash 脚本运行——即时输出，无 LLM 开销。脚本会扫描 `.claude/epics/` 并报告进行中、下一步以及阻塞项。

---

## Skill 目录结构

```
skill/ccpm/
├── SKILL.md                  # Entry point — detects intent, routes to reference
└── references/
    ├── plan.md               # PRD writing + parsing to epic
    ├── structure.md          # Epic decomposition into tasks
    ├── sync.md               # GitHub sync, progress comments, close, merge
    ├── execute.md            # Issue analysis + parallel agent launch
    ├── track.md              # Status, standup, search, next, blocked
    ├── conventions.md        # File formats, frontmatter schemas, git rules
    └── scripts/              # Bash scripts for deterministic operations
        ├── status.sh
        ├── standup.sh
        ├── epic-list.sh
        ├── search.sh
        └── ...               # 14 scripts total
```

你的项目文件位于项目根目录的 `.claude/` 下：

```
.claude/
├── prds/                     # Product requirement documents
├── epics/
│   └── <feature>/
│       ├── epic.md           # Technical epic
│       ├── <N>.md            # Task files (named by GitHub issue number after sync)
│       ├── <N>-analysis.md   # Parallel work stream analysis
│       └── updates/          # Agent progress tracking
└── (archived epics)
```

文件是唯一的真相来源——纯 Markdown 格式，直接存放在仓库中，无需外部服务。

---

## 示例流程

```
You: "I want to build a payment integration with Stripe — subscriptions and one-time charges"

CCPM: Asks 5 clarifying questions about scope, users, success criteria...

You: [answers]

CCPM: ✅ PRD created: .claude/prds/payment-integration.md
      Ready to create the technical epic?

You: "yes, parse it"

CCPM: ✅ Epic created: .claude/epics/payment-integration/epic.md
      8 task categories identified. Ready to decompose?

You: "break it down"

CCPM: ✅ Created 7 tasks — 5 parallel, 2 sequential
      Ready to push to GitHub?

You: "sync it"

CCPM: ✅ Epic #1234 created
      ✅ 7 sub-issues created (#1235–#1241)
      ✅ Worktree: ../epic-payment-integration/

You: "start working on issue 1235"

CCPM: Analyzed 3 parallel streams:
      Stream A: Stripe client setup ✓ Started
      Stream B: Webhook handler ✓ Started
      Stream C: Database models ⏸ Waiting on A

You: "what's our standup?"

CCPM: [runs standup.sh instantly]
      📅 Daily Standup — 2026-03-18
      🔄 In Progress: Issue #1235 (payment-integration) — 60%
      ⏭️ Next: Issue #1236 — Subscription billing logic
      📊 Tasks: 2 in progress, 5 open, 0 closed
```

---

## 已验证的成果

采用该系统的团队反馈：
- **上下文切换耗时减少 89%**
- **并行任务数从 1 个提升至 5–8 个**
- **Bug 率降低 75%** —— 得益于编码前详细的任务拆解
- **功能交付速度提升最高达 3 倍**

### 基准测试

在对比 CCPM Agent 与基线（无 Skill）的结构化评估中：

| 场景 | 启用 CCPM | 未启用 |
|---|---|---|
| PRD 创建（先头脑风暴，路径正确） | ✅ 4/4 | ❌ 2/4 |
| Issue 执行（分析 + worktree 检查） | ✅ 4/4 | ❌ 0/4 |
| 站会（运行脚本，真实数据） | ✅ 3/3 | ❌ 1/3 |
| **总计** | **100%** | **27.7%** |

---

## 本地操作 vs GitHub 远程同步

| 操作 | 本地 | GitHub |
|---|---|---|
| PRD 创建 | ✅ | — |
| 实现规划 | ✅ | — |
| 任务拆解 | ✅ | ✅（同步时） |
| 执行开发 | ✅ | — |
| 进度更新 | ✅ | ✅（同步时） |
| 最终交付物 | — | ✅ |

---

## 技术说明

**GitHub 集成** —— 使用 `gh-sub-issue` 扩展实现正确的父子层级关系。若未安装则回退至任务列表。安装命令：`gh extension install yahsan2/gh-sub-issue`

**文件命名规则** —— 拆解阶段任务以 `001.md`、`002.md` 开头。GitHub 同步后，重命名为 `{issue-id}.md`（例如 `1234.md`）。Issue #1234 对应文件 `1234.md`。

**架构决策** —— 有意避开 GitHub Projects API 的复杂性。所有操作优先在本地文件执行以保证速度。GitHub 同步为显式且受控的操作。工作树（Worktrees）提供干净的 Git 隔离以支持并行开发。

**寻找 v1 版本？** —— 原始的 `/pm:*` Claude Code 斜杠命令系统已保留在 [`v1` 分支](https://github.com/automazeio/ccpm/tree/v1)。

---

## 项目背景

CCPM 由 [Automaze](https://automaze.io) 开发，**专为注重交付的开发者打造**。

如果 CCPM 帮助你的团队交付了更优质的软件：

- ⭐ **[Star this repository](https://github.com/automazeio/ccpm)** 以表示支持
- 🐦 **[Follow @aroussi on X](https://x.com/aroussi)** 获取更新与技巧

---

> [!TIP]
> **Ship faster with Automaze.** We partner with founders to bring their vision to life, scale their business, and optimize for success.
> **[Visit Automaze to book a call ›](https://automaze.io)**

---

![Star History Chart](https://api.star-history.com/svg?repos=automazeio/ccpm)
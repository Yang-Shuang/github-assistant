<p align="center">
  <img src="harness_banner.png" alt="Harness Banner" width="600">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Version-1.2.0-brightgreen.svg" alt="Version">
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-Apache_2.0-blue.svg" alt="License"></a>
  <img src="https://img.shields.io/badge/Claude_Code-Plugin-purple.svg" alt="Claude Code Plugin">
  <img src="https://img.shields.io/badge/Patterns-6_Architectures-orange.svg" alt="6 Architecture Patterns">
  <img src="https://img.shields.io/badge/Mode-Agent_Teams-green.svg" alt="Agent Teams">
  <a href="https://github.com/revfactory/harness/stargazers"><img src="https://img.shields.io/github/stars/revfactory/harness?style=social" alt="GitHub Stars"></a>
</p>

<p align="center">
  <a href="#category--where-harness-sits"><img src="https://img.shields.io/badge/Layer-L3%20Meta--Factory-orange" alt="Layer"></a>
  <a href="#category--where-harness-sits"><img src="https://img.shields.io/badge/Sub--layer-Team--Architecture%20Factory-teal" alt="Sub-layer"></a>
  <a href="#"><img src="https://img.shields.io/badge/README-EN%20%7C%20KO%20%7C%20JA-lightgrey" alt="i18n"></a>
</p>

# Harness —— Claude Code 的团队架构工厂

**英文** | [한국어](README_KO.md) | [日本語](README_JA.md)

> **Harness 是专为 Claude Code 打造的团队架构工厂。** 只需输入 **“build a harness for this project”**（英文）、**“하네스 구성해줘”**（韩文）或 **“ハーネスを構成して”**（日文），该插件即可将你的领域描述转化为一个智能体（Agent）团队及其使用的技能——这些均从六种预定义的团队架构模式中选取。

## 概述

Harness 利用 Claude Code 的智能体团队系统，将复杂任务分解为多个协调运作的专业智能体团队。只需说“build a harness for this project”，它便会自动生成针对你所在领域的智能体定义（`.claude/agents/`）和技能文件（`.claude/skills/`）。

## 定位 —— Harness 所处的层级

Harness 位于 Claude Code 生态系统的 **L3 元工厂（Meta-Factory）** 层级——这是一个用于生成其他 Harness 的层级，而非被生成的对象。在 L3 内部，我们专注于一个特定的子层：**团队架构工厂（Team-Architecture Factory）**。

| Layer | What it does | Neighbors we coexist with |
|-------|--------------|---------------------------|
| **L3 — Meta-Factory / Team-Architecture Factory** (us) | Domain sentence → agent team + skills, via 6 pre-defined team patterns | — |
| L3 — Meta-Factory / Runtime-Configuration Factory | Deterministic, repeatable runtime configurations | [coleam00/Archon](https://github.com/coleam00/Archon) |
| L3 — Meta-Factory / Codex Runtime Port | Same concept, Codex runtime | [SaehwanPark/meta-harness](https://github.com/SaehwanPark/meta-harness) |
| L2 — Cross-Harness Workflow | Standardize skills/rules/hooks across multiple harnesses | [affaan-m/ECC](https://github.com/affaan-m/everything-claude-code) |

> Archon generates deterministic runtime configurations. Harness generates team architectures (pipeline, fan-out/fan-in, expert pool, producer-reviewer, supervisor, hierarchical delegation) plus the skills agents use. Different sub-layers of the same L3. Pick Archon for runtime determinism, Harness for team architecture, or combine them.

## ⭐ Star 历史

<a href="https://www.star-history.com/?repos=revfactory%2Fharness&type=date&legend=top-left">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/chart?repos=revfactory/harness&type=date&theme=dark&legend=top-left" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/chart?repos=revfactory/harness&type=date&legend=top-left" />
   <img alt="Star History Chart" src="https://api.star-history.com/chart?repos=revfactory/harness&type=date&legend=top-left" />
 </picture>
</a>


## 核心特性

- **智能体团队设计（Agent Team Design）** — 6 种架构模式：Pipeline、Fan-out/Fan-in、Expert Pool、Producer-Reviewer、Supervisor，以及 Hierarchical Delegation
- **技能生成（Skill Generation）** — 自动生成功能，采用渐进式披露（Progressive Disclosure）机制以实现高效的上下文管理
- **编排协调（Orchestration）** — 支持智能体间数据传递、错误处理及团队协作协议
- **验证测试（Validation）** — 提供触发器校验、Dry-run 试运行，以及“带技能/不带技能”对比测试


## 工作流程

```
Phase 1: Domain Analysis
    ↓
Phase 2: Team Architecture Design (Agent Teams vs Subagents)
    ↓
Phase 3: Agent Definition Generation (.claude/agents/)
    ↓
Phase 4: Skill Generation (.claude/skills/)
    ↓
Phase 5: Integration & Orchestration
    ↓
Phase 6: Validation & Testing
```

## 安装指南

### 通过插件市场安装

#### 添加市场源
```shell
/plugin marketplace add revfactory/harness
```

#### 安装插件
```shell
/plugin install harness@harness-marketplace
```

### 直接安装为全局技能

```shell
# Copy the skills directory to ~/.claude/skills/harness/
cp -r skills/harness ~/.claude/skills/harness
```

## 插件目录结构

```
harness/
├── .claude-plugin/
│   └── plugin.json                 # Plugin manifest
├── skills/
│   └── harness/
│       ├── SKILL.md                # Main skill definition (6-Phase workflow)
│       └── references/
│           ├── agent-design-patterns.md   # 6 architectural patterns
│           ├── orchestrator-template.md   # Team/subagent orchestrator templates
│           ├── team-examples.md           # 5 real-world team configurations
│           ├── skill-writing-guide.md     # Skill authoring guide
│           ├── skill-testing-guide.md     # Testing & evaluation methodology
│           └── qa-agent-guide.md          # QA agent integration guide
└── README.md
```

## 使用方法

在 Claude Code 中通过以下提示词触发：

```
Build a harness for this project
Design an agent team for this domain
Set up a harness
```

### 执行模式

| Mode | Description | Recommended For |
|------|-------------|-----------------|
| **Agent Teams** (default) | TeamCreate + SendMessage + TaskCreate | 2+ agents requiring collaboration |
| **Subagents** | Direct Agent tool invocation | One-off tasks, no inter-agent communication needed |

<p align="center">
  <img src="harness_team.png" alt="Harness Agent Team" width="500">
</p>

### 架构模式

| Pattern | Description |
|---------|-------------|
| Pipeline | Sequential dependent tasks |
| Fan-out/Fan-in | Parallel independent tasks |
| Expert Pool | Context-dependent selective invocation |
| Producer-Reviewer | Generation followed by quality review |
| Supervisor | Central agent with dynamic task distribution |
| Hierarchical Delegation | Top-down recursive delegation |

## 输出文件

Harness 生成的文件结构：

```
your-project/
├── .claude/
│   ├── agents/          # Agent definition files
│   │   ├── analyst.md
│   │   ├── builder.md
│   │   └── qa.md
│   └── skills/          # Skill files
│       ├── analyze/
│       │   └── SKILL.md
│       └── build/
│           ├── SKILL.md
│           └── references/
```

## 应用场景 —— 试试这些提示词

安装 Harness 后，将以下任意提示词复制到 Claude Code：

**深度研究（Deep Research）**
```
Build a harness for deep research. I need an agent team that can investigate
any topic from multiple angles — web search, academic sources, community
sentiment — then cross-validate findings and produce a comprehensive report.
```

**网站开发（Website Development）**
```
Build a harness for full-stack website development. The team should handle
design, frontend (React/Next.js), backend (API), and QA testing in a
coordinated pipeline from wireframe to deployment.
```

**条漫/漫画制作（Webtoon / Comic Production）**
```
Build a harness for webtoon episode production. I need agents for story
writing, character design prompts, panel layout planning, and dialogue
editing. They should review each other's work for style consistency.
```

**YouTube 内容策划（YouTube Content Planning）**
```
Build a harness for YouTube content creation. The team should research
trending topics, write scripts, optimize titles/tags for SEO, and plan
thumbnail concepts — all coordinated by a supervisor agent.
```

**代码审查与重构（Code Review & Refactoring）**
```
Build a harness for comprehensive code review. I want parallel agents
checking architecture, security vulnerabilities, performance bottlenecks,
and code style — then merging all findings into a single report.
```

**技术文档生成（Technical Documentation）**
```
Build a harness that generates API documentation from this codebase.
Agents should analyze endpoints, write descriptions, generate usage
examples, and review for completeness.
```

**数据管道设计（Data Pipeline Design）**
```
Build a harness for designing data pipelines. I need agents for schema
design, ETL logic, data validation rules, and monitoring setup that
delegate sub-tasks hierarchically.
```

**营销活动策划（Marketing Campaign）**
```
Build a harness for marketing campaign creation. The team should research
the target market, write ad copy, design visual concepts, and set up
A/B test plans with iterative quality review.
```

## 生态共存 —— Harness 与周边项目

Harness 并非孤身一人。在 Claude Code / 智能体框架生态中，以下项目位于相邻层级；每个项目均采用“X 是……，Harness 是……”的对照形式进行说明，方便你按需选择或组合使用。

| Repo | Their position | Relationship to Harness |
|------|----------------|-------------------------|
| [coleam00/Archon](https://github.com/coleam00/Archon) | "harness builder" — deterministic, repeatable runtime configurations | **同属 L3，相邻子层。** Archon 是运行时配置工厂（Runtime-Configuration Factory），Harness 是团队架构工厂（Team-Architecture Factory）。若需运行时的确定性选 Archon，若需团队架构设计选 Harness，或结合使用。 |
| [SaehwanPark/meta-harness](https://github.com/SaehwanPark/meta-harness) | Codex port of the same concept | **同属 L3，运行时不同。** 在 Claude Code 上使用 Harness，在 Codex 上使用 meta-harness。 |
| [affaan-m/ECC](https://github.com/affaan-m/everything-claude-code) | "Agent harness performance & workflow layer" (sits on top of existing harnesses) | **不同层级。** ECC 是跨 Harness 的标准化层；Harness 是生成 Harness 的工厂。可串行组合使用。 |
| [wshobson/agents](https://github.com/wshobson/agents) | Subagent / skill catalog (182 agents, 149 skills) | **工厂 ↔ 零部件供应。** wshobson 是素材库；Harness 负责团队设计。可将 wshobson 的条目作为组件吸收进 Harness 生成的团队中。 |
| [LangGraph](https://langchain-ai.github.io/langgraph/) | State-graph orchestration, LLM-agnostic | **不同赛道。** LangGraph 适用于长周期、支持状态恢复的编排；Harness 专注于快速构建原生的 Claude Code 团队架构。 |

## 基于 Harness 构建的项目

### Harness 100

**[revfactory/harness-100](https://github.com/revfactory/harness-100)** —— 覆盖 10 个领域的 100 套生产级智能体团队 Harness，提供英文和韩文版本（共 200 个包）。每个 Harness 均内置 4-5 个专业智能体、编排技能及领域专属技能——全部由本插件生成。包含 1,808 个 Markdown 文件，涵盖内容创作、软件开发、数据/AI、商业战略、教育、法律、健康等领域。

### 研究：Harness 有效性 A/B 测试

**[revfactory/claude-code-harness](https://github.com/revfactory/claude-code-harness)** —— 一项针对 15 项软件工程任务的对照实验，旨在衡量结构化预配置对大语言模型（LLM）代码智能体输出质量的影响。

| Metric | Without Harness | With Harness | Improvement |
|--------|:-:|:-:|:-:|
| Average Quality Score | 49.5 | 79.3 | **+60%** |
| Win Rate | — | — | **100%** (15/15) |
| Output Variance | — | — | **-32%** |

**核心发现**：效果随任务复杂度提升而增强——任务越难，提升越大（基础级 +23.8%，进阶级 +29.6%，专家级 +36.2%）。

**统一引用话术**：平均质量提升 +60%（49.5 → 79.3），胜率 15/15，方差降低 -32%（样本量 n=15，作者实测 A/B 测试，第三方复现进行中）。

> Full paper: *Hwang, M. (2026). Harness: Structured Pre-Configuration for Enhancing LLM Code Agent Output Quality.*

## 环境要求

- [已启用智能体团队（Agent Teams enabled）](https://code.claude.com/docs/en/agent-teams)：`CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1`

## 常见问题 (FAQ)

<details>
<summary><b>Q1. “+60%”是否夸大其词？</b></summary>

**A.** +60% 的数据来源于**作者实测的 A/B 测试（n=15，共 15 项任务，在姊妹仓库 `claude-code-harness` 上测量）**。本仓库中每次引用该数据时，均会在同一句话内附带说明“样本量 n=15，作者实测，第三方复现进行中”。对于是否采用的决策，建议你进行为期 2-4 周的内测并记录实际数据。

**参考依据：**
- 作者 A/B 测试：[revfactory/claude-code-harness](https://github.com/revfactory/claude-code-harness)
- 论文：*Hwang, M. (2026). Harness: Structured Pre-Configuration for Enhancing LLM Code Agent Output Quality*
</details>

<details>
<summary><b>Q2. 为什么叫“Harness 工厂”而不是“Harness 构建器”？这是否与 Archon 存在竞争？</b></summary>

**A.** Archon 生成确定性的运行时配置——它是**运行时配置工厂（Runtime-Configuration Factory）**。Harness 生成智能体团队架构（团队结构、消息协议、审查关卡）——它是**团队架构工厂（Team-Architecture Factory）**。它们同属 L3 元工厂下的相邻子层，服务于不同需求。若需运行时的确定性选 Archon，若需团队架构模式选 Harness，或结合使用（用 Harness 设计架构 → 用 Archon 部署运行时）。

**参考依据：**
- Archon 官方定义：[clawfit docs/reference-levels.md](https://github.com/hongsw/clawfit/blob/main/docs/reference-levels.md)
- 子层声明：见上方 **定位 —— Harness 所处的层级** 章节
- Archon 仓库：[github.com/coleam00/Archon](https://github.com/coleam00/Archon)
</details>

<details>
<summary><b>Q3. “仅限 Claude Code”是否过于局限？那 Gemini/Codex 怎么办？</b></summary>

**A.** 目前官方支持的唯一运行时是 Claude Code。相同概念在 Codex 上的移植版——[SaehwanPark/meta-harness](https://github.com/SaehwanPark/meta-harness)——已公开，Codex 团队可先行使用。Harness 选择了“Claude Code 原生、深度集成”而非“多运行时、浅层兼容”；与兄弟仓库（meta-harness, harness-init, OpenRig）的跨运行时协作已列入开发路线图。

**参考依据：**
- Codex 移植版：[github.com/SaehwanPark/meta-harness](https://github.com/SaehwanPark/meta-harness)
- 跨运行时脚手架工具：[github.com/Gizele1/harness-init](https://github.com/Gizele1/harness-init)
</details>

## 开源协议

Apache 2.0
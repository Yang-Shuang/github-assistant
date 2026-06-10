<p align="center">
  <a href="README.md"><img alt="English" src="https://img.shields.io/badge/EN-English-blue?style=flat-square"></a>
  <a href="docs-readme/zh-CN/README.md"><img alt="简体中文" src="https://img.shields.io/badge/ZH-简体中文-red?style=flat-square"></a>
  <a href="docs-readme/zh-TW/README.md"><img alt="繁體中文" src="https://img.shields.io/badge/ZH--TW-繁體中文-orange?style=flat-square"></a>
  <a href="docs-readme/ja-JP/README.md"><img alt="日本語" src="https://img.shields.io/badge/JA-日本語-green?style=flat-square"></a>
  <a href="docs-readme/ko-KR/README.md"><img alt="한국어" src="https://img.shields.io/badge/KO-한국어-blueviolet?style=flat-square"></a>
  <a href="docs-readme/es-ES/README.md"><img alt="Español" src="https://img.shields.io/badge/ES-Español-yellow?style=flat-square"></a>
  <a href="docs-readme/fr-FR/README.md"><img alt="Français" src="https://img.shields.io/badge/FR-Français-007EC6?style=flat-square"></a>
  <a href="docs-readme/ru-RU/README.md"><img alt="Русский" src="https://img.shields.io/badge/RU-Русский-informational?style=flat-square"></a>
  <a href="docs-readme/de-DE/README.md"><img alt="Deutsch" src="https://img.shields.io/badge/DE-Deutsch-2EA043?style=flat-square"></a>
  <a href="docs-readme/ar-SA/README.md"><img alt="العربية" src="https://img.shields.io/badge/AR-العربية-success?style=flat-square"></a>
  <a href="docs-readme/vi-VN/README.md"><img alt="Tiếng Việt" src="https://img.shields.io/badge/VI-Tiếng_Việt-cc6699?style=flat-square"></a>
  <a href="docs-readme/uz-UZ/README.md"><img alt="Oʻzbekcha" src="https://img.shields.io/badge/UZ-Oʻzbekcha-1A8BBA?style=flat-square"></a>
  <a href="docs-readme/tr-TR/README.md"><img alt="Türkçe" src="https://img.shields.io/badge/TR-Türkçe-E30A17?style=flat-square"></a>
</p>

<h1 align="center">Learn Harness Engineering</h1>

<p align="center"><strong>一门基于项目的课程，专注于构建让 AI 编程智能体可靠运行的环境、状态管理、验证与控制机制。</strong></p>

<p align="center">
  <img src="https://img.shields.io/badge/Lectures-12-blue?style=flat-square" alt="12 Lectures">
  <img src="https://img.shields.io/badge/Projects-6-green?style=flat-square" alt="6 Projects">
  <img src="https://img.shields.io/badge/Languages-13-yellow?style=flat-square" alt="13 Languages">
  <img src="https://img.shields.io/badge/License-MIT-lightgrey?style=flat-square" alt="MIT License">
</p>

> **地球图标** 本课程提供 **13种语言** 版本：英文、简体中文、繁体中文、日语、韩语、西班牙语、法语、俄语、德语、阿拉伯语、越南语、乌兹别克语、土耳其语。请通过上方的徽章选择你的语言。

Learn Harness Engineering 是一门专注于 AI 编程智能体工程的课程。我们深入研究并综合了业界最先进的 Harness（编排）工程理论与最佳实践。核心参考资料包括：

- [OpenAI: Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/)
- [Anthropic: Effective harnesses for long-running agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)
- [Anthropic: Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps)
- [Awesome Harness Engineering](https://github.com/walkinglabs/awesome-harness-engineering)

> **快速开始？** [`skills/harness-creator/`](./skills/harness-creator/) 技能可帮助你在几分钟内为你的项目搭建生产级 Harness（AGENTS.md、功能列表、init.sh、验证工作流）。

---

## Table of Contents

- [✨ Visual Preview](#visual-preview)
- [What Harness Engineering Actually Means](#what-harness-engineering-actually-means)
- [Quick Start: Improve Your Agent Today](#quick-start-improve-your-agent-today)
- [Capstone Project: A Real App](#capstone-project-a-real-app)
- [Learning Path](#learning-path)
- [Syllabus](#syllabus)
- [Skills](#skills)
- [Other Courses](#other-courses)

---

## ✨ Visual Preview

### 🏠 Course Homepage
> 全面的课程大纲与核心哲学介绍，提供清晰的入门路径。

![Course homepage preview](./docs/public/screenshots/readme/en-home.png)

### 📖 Immersive Lectures
> 深入探讨真实痛点与动手项目（如 Project 01），打造沉浸式学习体验。

![Course lecture preview](./docs/public/screenshots/readme/en-lecture-01.png)

### 🗂️ Ready-to-Use Resource Library
> 专为解决多轮 AI 智能体开发中的常见陷阱而设计的模板和参考配置，例如上下文丢失和过早完成任务。

![Resource library preview](./docs/public/screenshots/readme/en-resources.png)

## PDF Coursebooks

该仓库现已包含课程内容的 PDF 构建流水线。

- Run `npm run pdf:build` 可在本地生成当前配置的 PDF 课件。
- Output files are written to `artifacts/pdfs/`.
- Run `npm run screenshots:readme` if you want to refresh the README preview images.
- GitHub Actions workflow [`release-course-pdfs.yml`](./.github/workflows/release-course-pdfs.yml) can build the PDFs and publish them to GitHub Releases.

---

## The Model Is Smart, The Harness Makes It Reliable

有一个大多数人都是吃尽苦头才明白的残酷真相：**如果你没有为模型构建合适的环境，世界上最强大的模型在面对真实工程任务时依然会失败。**

你可能已经亲眼见过这种情况。你把一个任务交给 Claude 或 GPT。它一开始表现不错——读取文件、编写代码，看起来很高效。然后出了问题。它跳过了某个步骤。它破坏了一个测试。它说“做完了”，但实际上什么都跑不通。你花在做清理上的时间比你自己写还多。

这不是模型的问题。这是 Harness（编排）的问题。

证据很明确。Anthropic 进行了一项受控实验：使用相同的模型（Opus 4.5）、相同的提示词（prompt，“build a 2D retro game editor”）。没有 Harness，它在 20 分钟内花费了 9 美元，产出了一些无法运行的东西。有了完整的 Harness（规划器 + 生成器 + 评估器），它在 6 小时内花费了 200 美元，构建了一个真正能玩的游戏。模型没变。Harness 变了。

OpenAI 也报告了类似情况：在配置良好的 Harness 仓库中，相同的模型从“不可靠”变为“可靠”。这不是边际改进——而是质的飞跃。

**本课程将教你如何构建那样的环境。**

```text
                    THE HARNESS PATTERN
                    ====================

    You --> give task --> Agent reads harness files --> Agent executes
                                                        |
                                              harness governs every step:
                                              |
                                              +--> Instructions: what to do, in what order
                                              +--> Scope:        one feature at a time, no overreach
                                              +--> State:        progress log, feature list, git history
                                              +--> Verification: tests, lint, type-check, smoke runs
                                              +--> Lifecycle:    init at start, clean state at end
                                              |
                                              v
                                         Agent stops only when
                                         verification passes
```

---

## What Harness Engineering Actually Means

Harness（编排）工程旨在为模型构建一个完整的工作环境，使其产生可靠的结果。它不是关于编写更好的提示词（prompt），而是设计模型运行的系统架构。

一个 Harness 包含五个子系统：

```text
    ┌────────────────────────────────────────────────────────────────┐
    │                          THE HARNESS                           │
    │                                                                │
    │   ┌──────────────┐  ┌──────────────┐  ┌────────────────────┐   │
    │   │ Instructions │  │    State     │  │   Verification     │   │
    │   │              │  │              │  │                    │   │
    │   │ AGENTS.md    │  │ progress.md  │  │ tests + lint       │   │
    │   │ CLAUDE.md    │  │ feature_list │  │ type-check         │   │
    │   │ feature_list │  │ git log      │  │ smoke runs         │   │
    │   │ docs/        │  │ session hand │  │ e2e pipeline       │   │
    │   └──────────────┘  └──────────────┘  └────────────────────┘   │
    │                                                                │
    │   ┌──────────────┐  ┌──────────────────────────────────────┐   │
    │   │    Scope     │  │         Session Lifecycle            │   │
    │   │              │  │                                      │   │
    │   │ one feature  │  │ init.sh at start                     │   │
    │   │ at a time    │  │ clean-state checklist at end         │   │
    │   │ definition   │  │ handoff note for next session        │   │
    │   │ of done      │  │ commit only when safe to resume      │   │
    │   └──────────────┘  └──────────────────────────────────────┘   │
    │                                                                │
    └────────────────────────────────────────────────────────────────┘

    The MODEL decides what code to write.
    The HARNESS governs when, where, and how it writes it.
    The harness doesn't make the model smarter.
    It makes the model's output reliable.
```

每个子系统各司其职：

- **Instructions（指令）**——告诉智能体该做什么、按什么顺序做，以及开始前需要阅读什么。不是单个巨型文件；而是一种渐进式披露结构，智能体按需导航。
- **State（状态）**——跟踪已完成、进行中以及下一步的内容。持久化到磁盘，以便下一次会话能无缝衔接上一次的工作进度。
- **Verification（验证）**——只有通过的测试套件才算作证据。智能体无法在没有可运行证明的情况下宣布胜利。
- **Scope（范围）**——限制智能体一次只处理一个功能。不越界、不半途而废地做三件事、不重写功能列表来掩盖未完成的工作。
- **Session Lifecycle（会话生命周期）**——开始时初始化，结束时清理。为下一次会话留下干净的重启路径。

---

## Why This Course Exists

问题不是“模型能写代码吗？”它们当然可以。真正的问题是：**在没有人类持续监督的情况下，它们能否在真实仓库中、跨多次会话可靠地完成真实的工程任务？**

目前的答案是：没有 Harness 就不行。

```text
    WITHOUT HARNESS                            WITH HARNESS
    ==============                             ============

    Session 1: agent writes code               Session 1: agent reads instructions
               agent breaks tests                         agent runs init.sh
               agent says "done"                          agent works on one feature
               you fix it manually                        agent verifies before claiming done
                                                          agent updates progress log
    Session 2: agent starts fresh                         agent commits clean state
               agent has no memory
               of what happened before         Session 2: agent reads progress log
               agent re-does work                         agent picks up exactly where it left off
               or does something else entirely            agent continues the unfinished feature
               you fix it again                           you review, not rescue

    Result: you spend more time                Result: agent does the work,
            cleaning up than if you                    you verify the result
            did it yourself
```

本课程真正关注的核心问题是：

- 哪些 Harness（编排）设计能提高任务完成率？
- 哪些设计能减少返工和错误完成的情况？
- 哪些机制能让长时运行的任务稳步推进？
- 哪些结构能在多次智能体运行后保持系统的可维护性？

---

## Course Curriculum & Documentation

如需完整课程内容，请访问 **[Documentation Website](https://walkinglabs.github.io/learn-harness-engineering/)**。

课程分为三个部分：

1. **Lectures（讲座）**：12 个概念单元，讲解 Harness 工程背后的理论。
2. **Projects（项目）**：6 个动手实践项目，从零开始构建智能体工作区。
3. **Resource Library（资源库）**：开箱即用的模板（AGENTS.md、feature_list.json、init.sh 等），供你直接用于自己的仓库。

---

## Quick Start: Improve Your Agent Today

你不需要读完所有 12 个讲座才能开始获得收益。如果你已经在真实项目中使用编程智能体，以下是立即改进它的方法。

核心思路很简单：与其只写提示词（prompt），不如给智能体一套结构化文件，定义该做什么、已完成什么以及如何验证工作成果。这些文件位于你的仓库内，因此每次会话都从相同的状态开始。

```text
    YOUR PROJECT ROOT
    ├── AGENTS.md              <-- the agent's operating manual
    ├── CLAUDE.md              <-- (alternative, if using Claude Code)
    ├── init.sh                <-- runs install + verify + start
    ├── feature_list.json      <-- what features exist, which are done
    ├── claude-progress.md     <-- what happened each session
    └── src/                   <-- your actual code
```

从 [Resource Library](https://walkinglabs.github.io/learn-harness-engineering/en/resources/) 获取启动模板，放入你的项目中。就这么简单。四个文件，你的智能体会话稳定性将已经比仅依赖提示词高出很多。

---

## Capstone Project: A Real App

所有六个课程项目都围绕同一个产品展开：**一款基于 Electron 的个人知识库桌面应用**。

```text
    ┌──────────────────────────────────────────────────────┐
    │             Knowledge Base Desktop App               │
    │                                                      │
    │  ┌──────────────┐  ┌──────────────────────────────┐  │
    │  │ Document List│  │       Q&A Panel              │  │
    │  │              │  │                              │  │
    │  │ doc-001.md   │  │  Q: What is harness eng?     │  │
    │  │ doc-002.md   │  │  A: The environment built    │  │
    │  │ doc-003.md   │  │     around an agent model... │  │
    │  │ ...          │  │     [citation: doc-002.md]   │  │
    │  └──────────────┘  └──────────────────────────────┘  │
    │                                                      │
    │  ┌─────────────────────────────────────────────────┐ │
    │  │ Status Bar: 42 docs | 38 indexed | last sync 3m │ │
    │  └─────────────────────────────────────────────────┘ │
    └──────────────────────────────────────────────────────┘

    Core features:
    ├── Import local documents
    ├── Manage a document library
    ├── Process and index documents
    ├── Run AI-powered Q&A over imported content
    └── Return grounded answers with citations
```

选择这个项目是因为它兼具强烈的实用价值、足够的真实产品复杂度，以及观察 Harness（编排）改进前后效果的绝佳场景。

每个课程项目的启动/解决方案目录，都是该演进阶段完整的 Electron 应用副本。P(N+1) 的启动项目基于 P(N) 的解决方案生成——随着你的 Harness 技能提升，应用也会同步进化。

---

## Learning Path

课程设计为按顺序完成。每个阶段都建立在前一阶段的基础上。

```text
    Phase 1: SEE THE PROBLEM              Phase 2: STRUCTURE THE REPO
    ========================              ==========================

    L01  Strong models ≠ reliable         L03  Repository as single
         execution                              source of truth
    L02  What harness actually means
                                          L04  Split instructions across
         |                                     files, not one giant file
         v
    P01  Prompt-only vs.                       |
         rules-first comparison                v
                                               P02  Agent-readable workspace


    Phase 3: CONNECT SESSIONS             Phase 4: FEEDBACK & SCOPE
    ==========================            =========================

    L05  Keep context alive               L07  Draw clear task boundaries
         across sessions
                                          L08  Feature lists as harness
    L06  Initialize before every               primitives
         agent session
                                               |
         |                                     v
         v                                     P04  Runtime feedback to 
    P03  Multi-session continuity                   correct agent behavior


    Phase 5: VERIFICATION                 Phase 6: PUT IT ALL TOGETHER
    =====================                 ============================

    L09  Stop agents from                 L11  Make agent's runtime
         declaring victory early               observable

    L10  Full-pipeline run =              L12  Clean handoff at end of 
         real verification                      every session

         |                                     |
         v                                     v
    P05  Agent verifies its own work      P06  Build a complete harness
                                               (capstone project)
```

如果你是兼职学习，每个阶段大约需要一周时间。如果想加快进度，第 1–3 阶段可以在一个长周末内完成。

---

## Syllabus

### Lectures — 12 conceptual units, each answering one core question

*Read the full text for each lecture on the [Documentation Website](https://walkinglabs.github.io/learn-harness-engineering/).*

| Session | Question | Core Idea |
|---------|----------|-----------|
| [L01](./docs/en/lectures/lecture-01-why-capable-agents-still-fail/index.md) | Why do strong models still fail on real tasks? | The capability gap between benchmarks and real engineering |
| [L02](./docs/en/lectures/lecture-02-what-a-harness-actually-is/index.md) | What does "harness" actually mean? | Five subsystems: instructions, state, verification, scope, lifecycle |
| [L03](./docs/en/lectures/lecture-03-why-the-repository-must-become-the-system-of-record/index.md) | Why must the repo be the single source of truth? | If the agent can't see it, it doesn't exist |
| [L04](./docs/en/lectures/lecture-04-why-one-giant-instruction-file-fails/index.md) | Why does one giant instruction file fail? | Progressive disclosure: give a map, not an encyclopedia |
| [L05](./docs/en/lectures/lecture-05-why-long-running-tasks-lose-continuity/index.md) | Why do long-running tasks lose continuity? | Persist progress to disk; pick up where you left off |
| [L06](./docs/en/lectures/lecture-06-why-initialization-needs-its-own-phase/index.md) | Why does initialization need its own phase? | Verify the environment is healthy before the agent starts work |
| [L07](./docs/en/lectures/lecture-07-why-agents-overreach-and-under-finish/index.md) | Why do agents overreach and under-finish? | One feature at a time; explicit definition of done |
| [L08](./docs/en/lectures/lecture-08-why-feature-lists-are-harness-primitives/index.md) | Why are feature lists harness primitives? | Machine-readable scope boundaries the agent can't ignore |
| [L09](./docs/en/lectures/lecture-09-why-agents-declare-victory-too-early/index.md) | Why do agents declare victory too early? | Verification gaps: confidence ≠ correctness |
| [L10](./docs/en/lectures/lecture-10-why-end-to-end-testing-changes-results/index.md) | Why does end-to-end testing change results? | Only a full-pipeline run counts as real verification |
| [L11](./docs/en/lectures/lecture-11-why-observability-belongs-inside-the-harness/index.md) | Why does observability belong inside the harness? | If you can't see what the agent did, you can't fix what it broke |
| [L12](./docs/en/lectures/lecture-12-why-every-session-must-leave-a-clean-state/index.md) | Why must every session leave a clean state? | The next session's success depends on this session's cleanup |

### Projects — 6 hands-on projects applying lecture methods to the same Electron app

| Project | What You Do | Harness Mechanism |
|---------|------------|-------------------|
| [P01](./docs/en/projects/project-01-baseline-vs-minimal-harness/index.md) | Run the same task twice: prompt-only vs. rules-first | Minimal harness: AGENTS.md + init.sh + feature_list.json |
| [P02](./docs/en/projects/project-02-agent-readable-workspace/index.md) | Restructure the repo so the agent can read it | Agent-readable workspace + persistent state files |
| [P03](./docs/en/projects/project-03-multi-session-continuity/index.md) | Make the agent pick up from where it left off | Progress log + session handoff + multi-session continuity |
| [P04](./docs/en/projects/project-04-incremental-indexing/index.md) | Stop the agent from doing too much or too little | Runtime feedback + scope control + incremental indexing |
| [P05](./docs/en/projects/project-05-grounded-qa-verification/index.md) | Make the agent verify its own work | Self-verification + grounded Q&A + evidence-based completion |
| [P06](./docs/en/projects/project-06-runtime-observability-and-debugging/index.md) | Build a complete harness from scratch (capstone) | Full harness: all mechanisms + observability + ablation study |

```text
    PROJECT EVOLUTION
    =================

    P01  Prompt-only vs. rules-first       You see the problem
     |
     v
    P02  Agent-readable workspace          You restructure the repo
     |
     v
    P03  Multi-session continuity          You connect sessions
     |
     v
    P04  Runtime feedback & scope          You add feedback loops
     |
     v
    P05  Self-verification                 You make the agent check itself
     |
     v
    P06  Complete harness (capstone)       You build the full system

    Each project's solution becomes the next project's starter.
    The app evolves. Your harness skills grow with it.
```

### Resource Library

- [English](https://walkinglabs.github.io/learn-harness-engineering/en/resources/) — 模板、清单和方法参考
- [简体中文](https://walkinglabs.github.io/learn-harness-engineering/zh/resources/) — 中文模板、清单和方法参考
- [繁體中文](https://walkinglabs.github.io/learn-harness-engineering/zh-TW/resources/) — 繁體中文範本、清單和方法參考
- [日本語](https://walkinglabs.github.io/learn-harness-engineering/ja/resources/) — テンプレート、チェックリスト、方法リファレンス
- [한국어](https://walkinglabs.github.io/learn-harness-engineering/ko/resources/) — 템플릿, 체크리스트, 방법 참고 자료
- [Español](https://walkinglabs.github.io/learn-harness-engineering/es/resources/) — plantillas, listas de verificación y referencias
- [Français](https://walkinglabs.github.io/learn-harness-engineering/fr/resources/) — modèles, listes de contrôle et références
- [Русский](https://walkinglabs.github.io/learn-harness-engineering/ru/resources/) — шаблоны, чек-листы и справочники
- [Deutsch](https://walkinglabs.github.io/learn-harness-engineering/de/resources/) — Vorlagen, Checklisten und Referenzen
- [العربية](https://walkinglabs.github.io/learn-harness-engineering/ar/resources/) — قوالب، قوائم تحقق ومراجع
- [Tiếng Việt](https://walkinglabs.github.io/learn-harness-engineering/vi/resources/) — mẫu, danh sách kiểm tra và tài liệu tham khảo
- [Oʻzbekcha](https://walkinglabs.github.io/learn-harness-engineering/uz/resources/) — andozalar, tekshiruv roʻyxatlari va maʼlumotnomalar
- [Türkçe](https://walkinglabs.github.io/learn-harness-engineering/tr/resources/) — şablonlar, kontrol listeleri ve referanslar

---

## The Agent Session Lifecycle

本课程的核心思想之一：**智能体的会话应遵循结构化的生命周期，而非毫无章法地运行。** 具体流程如下：

```text
    AGENT SESSION LIFECYCLE
    ======================

    ┌──────────────────────────────────────────────────────────────────┐
    │  START                                                           │
    │                                                                  │
    │  1. Agent reads AGENTS.md / CLAUDE.md                            │
    │  2. Agent runs init.sh (install, verify, health check)           │
    │  3. Agent reads claude-progress.md (what happened last time)     │
    │  4. Agent reads feature_list.json (what's done, what's next)     │
    │  5. Agent checks git log (recent changes)                        │
    │                                                                  │
    │  SELECT                                                          │
    │                                                                  │
    │  6. Agent picks exactly ONE unfinished feature                   │
    │  7. Agent works only on that feature                             │
    │                                                                  │
    │  EXECUTE                                                         │
    │                                                                  │
    │  8. Agent implements the feature                                 │
    │  9. Agent runs verification (tests, lint, type-check)            │
    │  10. If verification fails: fix and re-run                       │
    │  11. If verification passes: record evidence                     │
    │                                                                  │
    │  WRAP UP                                                         │
    │                                                                  │
    │  12. Agent updates claude-progress.md                            │
    │  13. Agent updates feature_list.json                             │
    │  14. Agent records what's still broken or unverified             │
    │  15. Agent commits (only when safe to resume)                    │
    │  16. Agent leaves clean restart path for next session            │
    │                                                                  │
    └──────────────────────────────────────────────────────────────────┘

    The harness governs every transition in this lifecycle.
    The model decides what code to write at each step.
    Without the harness, step 9 becomes "agent says it looks fine."
    With the harness, step 9 is "tests pass, lint is clean, types check."
```

---

## Who This Is For

本课程适合：

- 已在使用编程智能体的工程师，希望获得更好的稳定性和质量
- 研究人员或构建者，希望系统性地理解 Harness（编排）设计
- 技术负责人，需要了解环境设计如何影响智能体性能

本课程不适合：

- 寻找零代码 AI 入门指南的人
- 只关注提示词且无意构建实际实现的人
- 不愿让智能体在真实仓库中工作的学习者

---

## Requirements

这是一门需要你真正运行编程智能体的课程。

你至少需要以下工具之一：

- Claude Code
- Codex
- 其他支持文件编辑、命令执行和多步任务的 IDE 或 CLI 编程智能体

课程假设你能做到：

- 打开本地仓库
- 允许智能体编辑文件
- 允许智能体运行命令
- 检查输出并重新运行任务

如果你没有这类工具，仍可阅读课程内容，但无法按预期完成项目。

---

## Local Preview

本仓库使用 VitePress 作为文档查看器。

```sh
npm install
npm run docs:dev        # Dev server with hot reload
npm run docs:build      # Production build
npm run docs:preview    # Preview built site
```

然后在浏览器中打开 VitePress 输出的本地地址即可。

---

## Prerequisites

必需：

- 熟悉终端、git 和本地开发环境
- 能够使用至少一种常见应用栈进行代码读写
- 具备基础软件调试经验（阅读日志、测试和运行时行为）
- 有足够时间投入以实践为主的课程学习

加分项（非必需）：

- 有 Electron、桌面应用或本地优先工具的开发经验
- 具备测试、日志记录或软件架构背景
- 曾接触过 Codex、Claude Code 等类似编程智能体

---

## Core References

主要参考：

- [OpenAI: Harness engineering: leveraging Codex in an agent-first world](https://openai.com/index/harness-engineering/)
- [Anthropic: Effective harnesses for long-running agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents)
- [Anthropic: Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps)
- [OpenAI: Unrolling the Codex agent loop](https://openai.com/index/unrolling-the-codex-agent-loop/)
- [Anthropic: Demystifying evals for AI agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents)
- [LangChain: Improving Deep Agents with harness engineering](https://www.langchain.com/blog/improving-deep-agents-with-harness-engineering)
- [Thoughtworks / Martin Fowler: Harness engineering for coding agent users](https://martinfowler.com/articles/harness-engineering.html)
- [Cursor: Continually improving our agent harness](https://cursor.com/blog/continually-improving-agent-harness)

完整的分层参考文献列表请参见 [`docs/en/resources/reference/`](./docs/en/resources/reference/index.md)。

---

## Repository Structure

```text
learn-harness-engineering/
├── docs/                          # VitePress documentation site
│   ├── lectures/                  # 12 lectures (index.md + code/ examples)
│   │   ├── lecture-01-*/
│   │   └── ... (12 total)
│   ├── projects/                  # 6 project descriptions
│   │   ├── project-01-*/
│   │   └── ... (6 total)
│   └── resources/                 # Multilingual templates & references (13 languages)
│       ├── en/
│       └── ... (13 total)
├── projects/
│   ├── shared/                    # Shared Electron + TypeScript + React foundation
│   └── project-NN/                # Per-project starter/ and solution/ directories
├── skills/                        # Reusable AI agent skills
│   └── harness-creator/           # Harness engineering skill
├── package.json                   # VitePress + dev tooling
└── CLAUDE.md                      # Claude Code instructions for this repo
```

---

## How the Course Is Organized

- 每个讲座聚焦一个核心问题
- 课程包含 6 个项目
- 每个项目都要求智能体执行真实工作
- 每个项目均对比弱 Harness（编排）与强 Harness 的结果差异
- 重点在于可衡量的效果差异，而非编写了多少文档

---

## Skills

本仓库还包含可复用的 AI 智能体技能，你可以直接安装到 IDE 或智能体工作区中。

- [**harness-creator**](./skills/harness-creator/): A skill that helps you scaffold a production-grade harness for your own project in minutes.

---

## Other Courses

我们的团队还开发了其他课程！欢迎查看：

[![Hands-on Modern RL](https://img.shields.io/badge/HANDS--ON_MODERN_RL-0052cc?style=for-the-badge)](https://github.com/walkinglabs/hands-on-modern-rl)

**《动手学现代强化学习（Modern RL）》**: An open-source, hands-on curriculum bridging the gap from basic RL concepts to LLM alignment, RLVR, and advanced Agentic systems.

[![Modern LLM Notebook](https://img.shields.io/badge/MODERN_LLM_NOTEBOOK-0052cc?style=for-the-badge)](https://github.com/walkinglabs/modern-llm-notebook)

**《现代大语言模型笔记（Modern LLM Notebook）》**: A hands-on course for building modern LLMs from scratch in PyTorch, with 23 runnable Jupyter Notebooks covering tokenizers, attention, MoE, RLHF, inference, evaluation, and distillation.

---

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=walkinglabs/learn-harness-engineering&type=date&legend=top-left)](https://www.star-history.com/#walkinglabs/learn-harness-engineering&type=date&legend=top-left)

---

## Acknowledgments

本课程受 [learn-claude-code](https://github.com/shareAI-lab/learn-claude-code) 启发并借鉴了其理念——这是一份从零构建智能体的渐进式指南，从单一循环到隔离的自主执行。
# claude-obsidian：为 Obsidian + Claude Code 打造的自组织 AI 第二大脑

<p align="center">
  <img src="wiki/meta/claude-obsidian-gif-cover-16x9.gif" alt="claude-obsidian: persistent compounding wiki vault for Claude Code and Obsidian" width="100%" />
</p>

[![GitHub stars](https://img.shields.io/github/stars/AgriciDaniel/claude-obsidian?style=flat&color=e8734a)](https://github.com/AgriciDaniel/claude-obsidian/stargazers)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Release](https://img.shields.io/github/v/release/AgriciDaniel/claude-obsidian?color=blue)](https://github.com/AgriciDaniel/claude-obsidian/releases/latest)
[![CI](https://github.com/AgriciDaniel/claude-obsidian/actions/workflows/test.yml/badge.svg)](https://github.com/AgriciDaniel/claude-obsidian/actions/workflows/test.yml)
[![Claude Code](https://img.shields.io/badge/Claude_Code-plugin-8B5CF6)](https://code.claude.com/docs/en/discover-plugins)
[![Obsidian](https://img.shields.io/badge/Obsidian-v1.9.10%2B-7c3aed)](https://obsidian.md)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-Compatible-blue)](https://agentskills.io)
[![Community](https://img.shields.io/badge/AI%20Marketing%20Hub-Pro%20community-purple)](https://www.skool.com/ai-marketing-hub-pro)
[![Blog Post](https://img.shields.io/badge/Deep_Dive-Blog_Post-22c55e)](https://agricidaniel.com/blog/claude-obsidian-ai-second-brain)

Claude 与 Obsidian 的知识伴侣及自组织 AI 第二大脑。一个持续运行的 AI 笔记助手，构建并维护一个持久化、知识复利增长的 Wiki 知识库（Wiki Vault）。你添加的每个来源都会被整合。你提出的任何问题都会基于已阅读的所有内容进行回答。知识像利息一样复利增长。

面向 AI 笔记、个人知识管理（PKM）、第二大脑工作流以及私有 Notion 替代方案的开源 Obsidian AI 插件。**15 个 Claude Code 技能**，支持多智能体协作，具备多写者安全机制（v1.7+），提供一等公民的方法论模式（LYT / PARA / Zettelkasten / Generic，v1.8 起）以及十原则思维框架（v1.9）。基于 [Andrej Karpathy 的 LLM Wiki 模式](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)。

> **两种获取该技能的方式。** 选择适合你工作流的一种。
>
> - 🌐 **公共开源版本**（最新版：`v1.9.2`，推荐）：在 [Daniel Agrici 的 GitHub](https://github.com/AgriciDaniel/claude-obsidian) 上免费发布的 MIT 许可版本。向所有人开放，无需会员资格。包含所有功能：v1.7 复合知识库（Compound Vault）、v1.8 方法论模式以及 v1.9 思维框架和审计加固。
> - ⚡ **AI Marketing Hub Pro**：相同的 MIT 许可核心代码，外加开发中功能的抢先体验（在公开发布之前）、直接协作支持及 [Pro 社区](https://www.skool.com/ai-marketing-hub-pro)。Pro 成员从 [AI Marketing Hub](https://github.com/AI-Marketing-Hub) 组织镜像安装（见下方选项 2 的说明）。

> ✨ **v1.7“复合知识库”重构**：以 Obsidian CLI 为默认传输层，混合检索机制（基于 [Anthropic 2024年9月研究](https://www.anthropic.com/news/contextual-retrieval) 的上下文前缀 + BM25 + 余弦重排），针对潜在多写者数据损坏漏洞的文件级建议锁（advisory locking），以及与 [kepano/obsidian-skills](https://github.com/kepano/obsidian-skills) 的底物对齐。完整指南：[docs/compound-vault-guide.md](docs/compound-vault-guide.md)。可选 [DragonScale Memory](docs/dragonscale-guide.md) 扩展（日志折叠、确定性页面地址、语义分块校验、边界优先自动研究）。

---

## 目录

- [它做什么](#what-it-does)
- [为什么选择 claude-obsidian？](#why-claude-obsidian)
- [快速开始](#quick-start)
- [命令](#commands)
  - [`/wiki`：设置、生成结构、继续操作](#wiki-setup-scaffold-continue)
  - [`/autoresearch`：自主研究循环](#autoresearch-autonomous-research-loop)
  - [`/canvas`：可视化层](#canvas-visual-layer)
  - [`/think`：十原则思维循环](#think-10-principle-thinking-loop)
- [方法论模式 (v1.8+)](#methodology-modes-v18)
- [知识库使用场景 (v1.0+)](#vault-use-cases-v10)
- [跨项目知识库](#cross-project-knowledge-base)
- [创建的内容](#what-gets-created)
- [架构设计](#architecture)
- [MCP 设置 (可选)](#mcp-setup-optional)
- [插件](#plugins)
- [CSS 片段（由 setup-vault.sh 自动启用）](#css-snippets-auto-enabled-by-setup-vaultsh)
- [Banner 插件](#banner-plugin)
- [文件结构](#file-structure)
- [AutoResearch 配置](#autoresearch-programmd)
- [种子知识库目录](#seed-vault)
- [配套插件：claude-canvas](#companion-claude-canvas)
- [常见问题](#faq)
- [环境要求](#requirements)
- [卸载](#uninstall)
- [贡献指南](#contributing)
- [相关项目](#related-projects)
- [社区交流](#community)
- [许可证](#license)

---

## 它做什么

### [YouTube 演示](https://www.youtube.com/watch?v=a2hgayvr-H4)

<p align="center">
  <img src="wiki/meta/welcome-canvas.gif" alt="claude-obsidian welcome canvas: visual demo of the wiki vault workflow" width="96%" />
</p>

你放入来源。Claude 读取它们，提取实体和概念，更新交叉引用，并将所有内容归档到结构化的 Obsidian 知识库中。每次导入都会让 Wiki 更加丰富。

你提出问题。Claude 读取热缓存（hot cache，近期上下文），扫描索引，深入相关页面，并综合生成答案。它引用的是具体的 Wiki 页面，而非训练数据。

你进行校验（lint）。Claude 查找孤立文件、死链、过时声明和缺失的交叉引用。你的 Wiki 无需手动清理即可保持健康状态。

每次会话结束时，Claude 都会更新热缓存。下次会话将直接从完整的近期上下文开始，无需回顾总结。

<p align="center">
  <img src="wiki/meta/image-example-graph-view.png" alt="Obsidian graph view showing the claude-obsidian knowledge graph with color-coded nodes for concepts, entities, and sources" width="48%" />
  <img src="wiki/meta/image-example-wiki-map-view.png" alt="Wiki Map canvas: visual hub linking domain pages, concepts, and entities" width="48%" />
</p>

---

## 为什么选择 claude-obsidian？

大多数 Obsidian AI 插件只是聊天界面，用于回答你现有笔记中的问题。claude-obsidian 是一个知识引擎，它自主创建、组织、维护和演进你的笔记。

| 能力 | claude-obsidian | Smart Connections | Copilot |
|---|---|---|---|
| **自动整理笔记** | ✅ 创建实体、概念、交叉引用 | ❌ | ❌ |
| **矛盾标记** | ✅ `[!contradiction]` 提示框并附来源 | ❌ | ❌ |
| **会话记忆** | ✅ 热缓存在对话间持久化 | ❌ | ❌ |
| **知识库维护** | ✅ 8类校验（孤立文件、死链、缺失内容） | ❌ | ❌ |
| **自主研究** | ✅ 3轮网络研究并填补空白 | ❌ | ❌ |
| **方法论模式** | ✅ LYT / PARA / Zettelkasten / Generic（一等支持） | ❌ | ❌ |
| **思维框架** | ✅ 10原则循环作为可调用技能 | ❌ | ❌ |
| **多模型支持** | ✅ Claude, Gemini, Codex, Cursor, Windsurf | ❌ 仅 Claude | ✅ 多模型 |
| **可视化画布** | ✅ 通过 [claude-canvas](https://github.com/AgriciDaniel/claude-canvas) | ❌ | ❌ |
| **多写者安全** | ✅ 文件级建议锁（v1.7+） | ❌ | ❌ |
| **带引用的查询** | ✅ 引用具体 Wiki 页面 | ✅ 引用相似笔记 | ✅ 引用笔记 |
| **批量导入** | ✅ 并行智能体处理多个来源 | ❌ | ❌ |
| **开源** | ✅ MIT | ✅ MIT | ⚠️ 免费增值 |

> 📖 **深入解析：** [我将 Obsidian 变成了自组织的 AI 大脑](https://agricidaniel.com/blog/claude-obsidian-ai-second-brain)。完整拆解包含数据可视化、市场背景及工作流演示。

---

## 快速开始

> ℹ️ 以下命令将安装来自 `AgriciDaniel/claude-obsidian` 的**公共开源版本**（推荐，无需会员资格）。希望抢先体验开发中功能的 **AI Marketing Hub Pro 成员**可将 `AgriciDaniel/claude-obsidian` 替换为 `AI-Marketing-Hub/claude-obsidian`（选项 2 也会替换插件标识符；详见该选项下方的说明）。

### 选项 1：克隆为知识库目录（推荐，完整设置仅需 2 分钟）

```bash
git clone https://github.com/AgriciDaniel/claude-obsidian
cd claude-obsidian
bash bin/setup-vault.sh
```

在 Obsidian 中打开该文件夹：**管理知识库目录 → 以文件夹形式打开知识库目录 → 选择 `claude-obsidian/`**。

在同一文件夹中打开 Claude Code。输入 `/wiki`。

> ℹ️ `setup-vault.sh` 会配置 `graph.json`（过滤器+颜色）、`app.json`（排除插件目录）和 `appearance.json`（启用 CSS）。在首次打开 Obsidian 前运行一次即可开箱即用地获得完整预配置的图谱视图、配色方案和 Wiki 结构。

---

### 选项 2：作为 Claude Code 插件安装

插件安装分为两步。首先添加市场目录，然后从中安装插件。

> ℹ️ **你正在安装哪个版本？**
>
> - **公共版（推荐，无需会员）：** 以下命令将安装来自 [`AgriciDaniel/claude-obsidian`](https://github.com/AgriciDaniel/claude-obsidian) 的免费 MIT 许可版本。无需注册。
> - **AI Marketing Hub Pro 成员？** 如需抢先体验开发中功能，请将 `AgriciDaniel/claude-obsidian` 替换为 `AI-Marketing-Hub/claude-obsidian`，并将插件标识符 `claude-obsidian@agricidaniel-claude-obsidian` 替换为 `claude-obsidian@ai-marketing-hub-claude-obsidian`。组织镜像需要具有访问 `AI-Marketing-Hub` 组织权限的已认证 `gh auth login`（或 GitHub PAT）。如果 `/plugin marketplace add` 返回 404，说明你的账号尚未加入该组织。请在 [Skool 社区](https://www.skool.com/ai-marketing-hub-pro) 私信以获取邀请。

```bash
# Step 1: add the marketplace
claude plugin marketplace add AgriciDaniel/claude-obsidian

# Step 2: install the plugin
claude plugin install claude-obsidian@agricidaniel-claude-obsidian
```

在任何 Claude Code 会话中：输入 `/wiki`。Claude 将引导你完成知识库设置。

检查是否安装成功：

```bash
claude plugin list
```

---

### 选项 3：添加到现有知识库目录

将 `WIKI.md` 复制到你的知识库根目录。粘贴到 Claude：

```
Read WIKI.md in this project. Then:
1. Check if Obsidian is installed. If not, install it.
2. Check if the Local REST API plugin is running on port 27124.
3. Configure the MCP server.
4. Ask me ONE question: "What is this vault for?"
Then scaffold the full wiki structure.
```

---

## 命令

| 你说 | Claude 执行 |
|---------|------------|
| `/wiki` | 检查设置、生成结构或继续上次的操作 |
| `ingest [file]` | 读取来源，创建 8-15 个 Wiki 页面，更新索引和日志 |
| `ingest all of these` | 批量处理多个来源，然后建立交叉引用 |
| `what do you know about X?` | 读取索引，深入相关页面，综合生成答案 |
| `/save` | 将当前对话归档为 Wiki 笔记 |
| `/save [name]` | 使用指定标题保存（跳过命名提问） |
| `/autoresearch [topic]` | 运行自主研究循环：搜索、获取、综合、归档 |
| `/canvas` | 打开或创建可视化画布，列出区域和节点 |
| `/canvas add image [path]` | 将图片（URL 或本地路径）添加到画布并自动布局 |
| `/canvas add text [content]` | 向画布添加 Markdown 文本卡片 |
| `/canvas add pdf [path]` | 将 PDF 文档作为渲染预览节点添加 |
| `/canvas add note [page]` | 将 Wiki 页面固定为画布上的链接卡片 |
| `/canvas zone [name]` | 向画布添加新的标签区域以组织视觉内容 |
| `/canvas from banana` | 捕获最近生成的图片到画布上 |
| `/think [problem]` | 将十原则思维循环应用于非平凡问题 |
| `lint the wiki` | 健康检查：孤立文件、死链、缺失内容及建议 |
| `update hot cache` | 使用最新的上下文摘要刷新 hot.md |

> ✨ **想要更多？** [claude-canvas](https://github.com/AgriciDaniel/claude-canvas) 提供 12 种模板、6 种布局算法、AI 图像生成、演示文稿及完整画布编排。同时安装两者，它们互为补充。

### `/wiki`：设置、生成结构、继续操作

首次运行设置将引导你完成以下步骤：

1. 检查是否已安装 Obsidian
2. 检查 Local REST API 插件（如需使用 MCP 传输）
3. 询问“这个知识库是用于什么的？”（仅一个问题，驱动后续结构生成）
4. 根据所选 [方法论模式](#methodology-modes-v18) 和 [知识库使用场景](#vault-use-cases-v10) 生成目录结构
5. 初始化 `hot.md`、`index.md`、`log.md`、`wiki/meta/dashboard.base`
6. 建议首次导入来源

在后续运行中，`/wiki` 会从中断处继续。它会检查知识库健康状态，提示过时声明，并显示 `hot.md` 中的近期活动。

### `/autoresearch`：自主研究循环

可配置程序位于 [`skills/autoresearch/references/program.md`](skills/autoresearch/references/program.md)：

- 最大轮次（默认 3）
- 每次会话最大页面数（默认 15）
- 来源偏好规则（学术、官方文档、新闻）
- 置信度评分 + 领域约束

循环流程：

1. **第 1 轮，广泛搜索**：分解为 3-5 个角度，每个角度运行 2-3 次查询，获取每个角度的前 2-3 条结果
2. **第 2 轮，填补空白**：针对矛盾和缺失内容的定向搜索
3. **第 3 轮，综合检查**（可选）：如果仍有重大空白，再进行一次检索
4. **归档**：生成综合页面 + 来源页面 + 实体页面 + 概念页面，全部建立交叉引用

应用 URL 验证和内容清理，遵循 [`skills/autoresearch/SKILL.md`](skills/autoresearch/SKILL.md) 中 `## Web egress hygiene (v1.8.2+)` 策略：拒绝 `file://` / `javascript:` / RFC1918 主机，剥离 `<script>` 和 wiki 链接注入尝试，限制获取内容体不超过 50KB。

### `/canvas`：可视化层

向 Obsidian 画布添加图片、PDF、笔记和 AI 生成图像。支持区域管理用于分组。自动布局可避免节点重叠。

```
/canvas                       # open or create the canvas
/canvas add image <path>      # add an image with auto-layout
/canvas add pdf <path>        # render PDF as preview node
/canvas add note <wiki-page>  # pin a wiki page as a linked card
/canvas zone <name>           # add a labeled zone
/canvas from banana           # capture recent banana-generated images
```

符合 JSON Canvas 1.0 规范（[`skills/canvas/references/canvas-spec.md`](skills/canvas/references/canvas-spec.md)）。完整编排功能（12 种模板、6 种布局算法、演示文稿）在配套插件 [claude-canvas](https://github.com/AgriciDaniel/claude-canvas) 中提供。

### `/think`：十原则思维循环

将 OBSERVE-OBSERVE-LISTEN-THINK-CONNECT-CONNECT-FEEL-ACCEPT-CREATE-GROW 框架应用于任何非平凡问题（架构决策、审计、事后复盘、模糊的用户需求）。

```
/think <problem statement>
```

该框架通过提示引导 Claude 经历 10 个阶段。当问题的新颖性和不可逆性足以证明需要严谨对待时使用。完整框架见 [`skills/think/SKILL.md`](skills/think/SKILL.md)。其他所有技能均附有“如何思考”附录，将框架映射到其具体工作中。[v1.8.0 推送前审计](docs/audits/v1.8.0-pre-push-audit-2026-05-18.md) 以此框架作为方法论主线。

---

## 方法论模式 (v1.8+)

四种组织哲学，通过 `bash bin/setup-mode.sh` 选择启用。`wiki-mode` 技能（v1.8+）读取 `.vault-meta/mode.json` 并据此路由新页面。默认为 `generic`（v1.7 行为，不强制任何特定结构）。

| 模式 | 哲学理念 | 归档约定 |
|------|-----------|---------|
| **Generic** (默认) | 无预设偏好。保留 v1.7 行为。 | `wiki/sources/`, `wiki/entities/`, `wiki/concepts/`, `wiki/sessions/` |
| **LYT** (Linking Your Thinking) | 笔记之间相互链接，文件夹不作为导航基础。MOC（地图之心智）是核心导航原语。 | `wiki/mocs/<topic>-moc.md` + `wiki/notes/<atomic-note>.md` |
| **PARA** (Tiago Forte) | 按可操作性组织（项目、领域、资源、归档）。 | `wiki/projects/`, `wiki/areas/`, `wiki/resources/`, `wiki/archives/` |
| **Zettelkasten** (Luhmann slip-box) | 原子化笔记、唯一 ID、密集双向链接，不使用文件夹。 | `wiki/<YYYYMMDDHHMMSSffffff>-<slug>.md`（扁平结构，带时间戳） |

切换模式**不会**自动迁移现有文件。完整指南：[`docs/methodology-modes-guide.md`](docs/methodology-modes-guide.md)。

---

## 知识库使用场景 (v1.0+)

这些描述你的知识库是用于**什么**。它们与方法论模式（描述**如何**组织）可组合使用。

| 使用场景 | 适用情况 |
|----------|-------------|
| **A：网站** | 站点地图、内容审计、SEO Wiki |
| **B：GitHub** | 代码库映射、架构 Wiki |
| **C：商业** | 项目 Wiki、竞争情报 |
| **D：个人** | 第二大脑、目标管理、日记综合 |
| **E：研究** | 论文、概念、学位论文 |
| **F：书籍/课程** | 章节追踪器、课程笔记 |

使用场景可以组合。一个按 PARA 组织的企业+研究知识库是有效的组合。

---

## 跨项目知识库

将任何 Claude Code 项目指向此知识库目录。添加到该项目的 `CLAUDE.md`：

```markdown
## Wiki Knowledge Base
Path: ~/path/to/vault

When you need context not already in this project:
1. Read wiki/hot.md first (recent context cache)
2. If not enough, read wiki/index.md
3. If you need domain details, read the relevant domain sub-index
4. Only then drill into specific wiki pages

Do NOT read the wiki for general coding questions or tasks unrelated to [domain].
```

你的执行助理、编码项目和内容工作流都将共享同一个知识库。

---

## 创建的内容

典型的初始结构将生成：

- 适用于你选择的使用场景 + 方法论模式的文件夹结构
- `wiki/index.md`：主目录索引
- `wiki/log.md`：追加式操作日志
- `wiki/hot.md`：近期上下文缓存
- `wiki/overview.md`：执行摘要
- `wiki/meta/dashboard.base`：Bases 仪表盘（原生，Obsidian 内置）
- `wiki/meta/dashboard.md`：遗留 Dataview 仪表盘（可选回退方案）
- `_templates/`：每种笔记类型的 Obsidian Templater 模板
- `.obsidian/snippets/vault-colors.css`：按类型着色的文件浏览器
- 知识库 `CLAUDE.md`：自动加载的项目指令

---

## 架构设计

三张图表解释了该插件的核心设计选择。

### 知识库目录工作流

来源文件存入 `.raw/`。`/wiki-ingest` 智能体读取每个来源，提取实体和概念，按当前启用的方法论模式将其归档到相应的 `wiki/` 子文件夹中，并更新索引、日志和热缓存。查询请求按此顺序依次读取热缓存 → 索引 → 页面，以保持较低的 Token 消耗。

<p align="center">
  <img src="assets/diagrams/vault-flow.svg" alt="Architecture diagram: sources flow into the wiki-ingest agent, which produces entity, concept, and source pages. The index and hot cache are updated. The wiki-query interface reads the cache, index, and pages to synthesize cited answers." width="100%" />
</p>

### 多写者安全机制 (v1.7+)

如果用户批量导入多个来源，并行处理的子智能体可能会同时目标指向同一个 Wiki 页面。`scripts/wiki-lock.sh` 提供文件级建议锁：一个写者获取锁后，另一个会等待并在下一轮重试。PostToolUse 自动提交钩子在暂存前检查锁列表，在写入进行时推迟提交操作。

<p align="center">
  <img src="assets/diagrams/multi-writer-locking.svg" alt="Architecture diagram: two parallel writers attempt to acquire a lock on the same wiki page via wiki-lock.sh. One writer is granted, writes the page, and releases the lock. The other writer logs the skip and retries on the next pass. No corruption, no half-written pages." width="100%" />
</p>

### 混合检索机制 (v1.7+，可选启用)

`/wiki-retrieve` 技能内置了一个基于 [Anthropic 2024年9月上下文检索研究](https://www.anthropic.com/news/contextual-retrieval) 的三层检索管道。BM25 是始终开启的稀疏层。上下文前缀（contextual-prefix）层需用户同意（`--allow-egress`）才能将页面内容发送至 Anthropic API 以生成前缀。余弦重排（cosine rerank）默认使用本地 ollama 模型。v1.7 的 50 次查询基准测试显示，相比 v1.6 基线，Top-1 准确率提升 32 个百分点，错误率降低 41%。

<p align="center">
  <img src="assets/diagrams/hybrid-retrieval.svg" alt="Architecture diagram: user query feeds both BM25 sparse search and an optional contextual-prefix Anthropic API call. Both feed a cosine rerank via local ollama embeddings. The output is a ranked list of candidates with --explain traceability for every score." width="100%" />
</p>

> ℹ️ 使用 `bash bin/setup-retrieve.sh` 配置该管道。它将构建 BM25 索引、请求出站权限同意，并验证 ollama 连接。该管道具备优雅降级能力：如果任何一层不可用，其余层仍会返回有效结果。

---

## MCP 设置 (可选)

MCP 允许 Claude 直接读写知识库笔记，无需复制粘贴。

**选项 A（基于 REST API）：**

1. 在 Obsidian 中安装 Local REST API 插件
2. 复制你的 API 密钥
3. 运行：

```bash
claude mcp add-json obsidian-vault '{
  "type": "stdio",
  "command": "uvx",
  "args": ["mcp-obsidian"],
  "env": {
    "OBSIDIAN_API_KEY": "your-key",
    "OBSIDIAN_HOST": "127.0.0.1",
    "OBSIDIAN_PORT": "27124",
    "NODE_TLS_REJECT_UNAUTHORIZED": "0"
  }
}' --scope user
```

**选项 B（基于文件系统，无需插件）：**

```bash
claude mcp add-json obsidian-vault '{
  "type": "stdio",
  "command": "npx",
  "args": ["-y", "@bitbonsai/mcpvault@latest", "/path/to/your/vault"]
}' --scope user
```

> ℹ️ 两种传输方式均由 `scripts/detect-transport.sh` 自动检测。结果保存在 `.vault-meta/transport.json` 中。如需手动指定，请编辑该文件并设置 `"manual_override": true`（v1.8.2+ 支持此配置）。

---

## 插件

### 核心插件（Obsidian 内置，无需安装）

| 插件 | 用途 |
|--------|---------|
| **Bases** | 驱动 `wiki/meta/dashboard.base`：原生数据库视图。自 Obsidian v1.9.10（2025年8月）起可用。替代 Dataview 作为主仪表盘。 |
| **Properties** | Visual frontmatter editor -> 可视化 Frontmatter 编辑器 |
| **Backlinks**, **Outline**, **Graph view** | Standard navigation -> 标准导航功能 |

### 预装社区插件（随知识库目录附带）

在 **设置 → 社区插件 → 启用** 中开启：

| 插件 | 用途 | 备注 |
|--------|---------|-------|
| **Calendar** | 右侧边栏日历，显示字数统计 + 任务圆点 | 预装 |
| **Thino** | 快速备忘录捕获面板 | 预装 |
| **Excalidraw** | 自由绘图画布，支持图片标注 | 预装* |
| **Banners** | 通过 `banner:` frontmatter 实现 Notion 风格页眉图 | 预装 |

\* Excalidraw `main.js`（8MB）由 `setup-vault.sh` 自动下载。不纳入 Git 版本控制。

### 需从社区插件安装（未预装）

| 插件 | 用途 |
|--------|---------|
| **Templater** | 自动从 `_templates/` 填充 frontmatter |
| **Obsidian Git** | 每 15 分钟自动提交知识库目录 |
| **Dataview** *(可选，遗留)* | 仅用于遗留的 `wiki/meta/dashboard.md` 查询。主仪表盘现已使用 Bases。 |

同时安装 **[Obsidian Web Clipper](https://obsidian.md/clipper)** 浏览器扩展。一键将网页发送至 `.raw/`。

---

## CSS 片段（由 setup-vault.sh 自动启用）

知识库目录附带三个片段，并会自动启用：

| 片段 | 效果 |
|---------|--------|
| `vault-colors` | 在文件浏览器中按类型对 `wiki/` 文件夹着色（蓝色=概念，绿色=来源，紫色=实体） |
| `ITS-Dataview-Cards` | 将 Dataview `TABLE` 查询转换为可视化卡片网格：配合 `.cards` 类使用 ` ```dataviewjs ` |
| `ITS-Image-Adjustments` | 精细控制笔记中的图片尺寸：在任何图片嵌入后追加 `\|100` |

---

## Banner 插件

添加到任意 Wiki 页面的 frontmatter：

```yaml
banner: "_attachments/images/your-image.png"
banner_icon: "🧠"
```

该页面将在 Obsidian 中渲染全宽页眉图。非常适合枢纽页面和概览页使用。

---

## 文件结构

```
claude-obsidian/
├── .claude-plugin/
│   ├── plugin.json              # manifest
│   └── marketplace.json         # distribution
├── skills/                       # 15 Claude Code skills (v1.9.2)
│   ├── wiki/                    # orchestrator + references
│   ├── wiki-ingest/             # source ingestion
│   ├── wiki-query/              # answer questions from the vault
│   ├── wiki-lint/               # vault health check
│   ├── wiki-cli/                # Obsidian CLI transport (v1.7+)
│   ├── wiki-retrieve/           # hybrid retrieval (v1.7+, opt-in)
│   ├── wiki-mode/               # methodology modes router (v1.8+)
│   ├── wiki-fold/               # log rollup (DragonScale opt-in)
│   ├── save/                    # /save: file conversations to wiki
│   ├── autoresearch/            # autonomous research loop
│   ├── canvas/                  # visual layer (images, PDFs, notes)
│   ├── defuddle/                # web extraction wrapper
│   ├── obsidian-bases/          # Bases schema reference
│   ├── obsidian-markdown/       # OFM syntax reference
│   └── think/                   # 10-principle thinking framework (v1.9+)
├── agents/
│   ├── verifier.md              # pre-commit audit agent (v1.7.1+)
│   ├── wiki-ingest.md           # parallel batch ingestion agent
│   └── wiki-lint.md             # health check agent
├── commands/                     # slash command entry points
├── hooks/
│   └── hooks.json               # SessionStart + Stop + PostToolUse hooks
├── scripts/                      # 12 helper scripts (transport, locking, retrieval, etc.)
├── tests/                        # 9 hermetic test suites (~1240 assertions, make test)
├── bin/                          # 5 setup scripts (setup-vault, setup-retrieve, setup-mode, etc.)
├── _templates/                   # Obsidian Templater templates
├── wiki/                         # seeded vault content (demo)
│   ├── canvases/                # welcome.canvas + main.canvas
│   ├── concepts/                # seeded: LLM Wiki Pattern, Hot Cache, Compounding Knowledge
│   ├── entities/                # seeded: Andrej Karpathy
│   ├── sources/                 # populated by your first ingest
│   └── meta/
│       ├── dashboard.base       # Bases dashboard (primary)
│       └── dashboard.md         # Legacy Dataview dashboard (optional)
├── docs/                         # guides + audits + release notes
├── .raw/                         # source documents (hidden in Obsidian)
├── .obsidian/snippets/           # vault-colors.css (3-color scheme)
├── WIKI.md                       # full schema reference
├── CLAUDE.md                     # project instructions
└── README.md                     # this file
```

---

## AutoResearch：program.md

`/autoresearch` 命令支持自定义配置。编辑 [`skills/autoresearch/references/program.md`](skills/autoresearch/references/program.md) 以控制：

- 优先使用的来源类型（学术、官方文档、新闻）
- 置信度评分规则
- 最大轮次和每次会话最大页面数
- 领域特定约束

默认程序适用于通用研究。可根据你的领域进行覆盖。医学研究人员可添加“优先使用 PubMed”，商业分析师可添加“聚焦市场数据和财报文件”。

---

## 种子知识库目录

本仓库附带一个预置种子的知识库目录。在 Obsidian 中打开你将看到：

- `wiki/concepts/`：LLM Wiki Pattern, Hot Cache, Compounding Knowledge
- `wiki/entities/`：Andrej Karpathy
- `wiki/sources/`：首次导入前为空
- `wiki/meta/dashboard.base`：Bases 仪表盘（适用于任意 Obsidian v1.9.10+）
- `wiki/meta/dashboard.md`：遗留 Dataview 仪表盘（可选回退方案）

图谱视图将显示由 5 个页面组成的连接集群。这是导入一次来源后的 Wiki 状态。添加更多来源后，知识网络将持续扩展。

<p align="center">
  <img src="wiki/meta/wiki-graph-grow.gif" alt="Animated GIF: claude-obsidian knowledge graph growing from a few seeded pages to a dense web of cross-referenced concepts after multiple ingests" width="48%" />
  <img src="wiki/meta/workflow-loop.gif" alt="Animated GIF: claude-obsidian workflow loop showing ingest, query, lint, save, and hot-cache refresh cycle" width="48%" />
</p>

---

## 配套插件：claude-canvas

针对可视化层，[claude-canvas](https://github.com/AgriciDaniel/claude-canvas) 提供 AI 编排的画布创建功能：支持知识图谱、演示文稿、流程图和情绪板，内置 12 种模板与 6 种布局算法。可自动检测 claude-obsidian 知识库目录。

```bash
claude plugin install AgriciDaniel/claude-canvas
```

---

## 常见问题

**什么是最好的 AI 第二大脑应用？**
最好的 AI 第二大脑应确保数据归属权在你手中。claude-obsidian 将所有内容存储为你拥有的纯 Markdown 文件（无数据库、无锁定、无需订阅），并让 Claude 读取、链接并将它们组织成一个关联的知识图谱。完全免费且开源（MIT）。

**如何用 AI 构建第二大脑？**
将任意来源放入知识库目录。Claude 会读取它，提取实体和概念，链接到你已有的内容，并归档到结构化的 Obsidian 知识库中。你提出问题；它基于已读所有内容回答，并引用具体页面。每次会话后，知识库都会变得更丰富、连接更紧密。

**如何将 Claude 与 Obsidian 结合使用以构建第二大脑？**
只需两行命令：`git clone https://github.com/AgriciDaniel/claude-obsidian`，然后 `cd claude-obsidian && bash bin/setup-vault.sh`。将该文件夹作为 Obsidian 知识库目录打开，在同一文件夹中打开 Claude Code，并输入 `/wiki`。完整步骤见 [快速开始](#quick-start)。

**有适合私有、AI 驱动的知识库的 Notion 替代品吗？**
有。claude-obsidian 是一个开源、本地优先的替代方案：你的笔记是存放在你自己磁盘上的纯 Markdown，而非托管数据库，且 AI 会为你自动整理它们。无厂商锁定，无月费。

**它是否支持跨设备自动同步？**
不支持开箱即用。知识库目录只是一个包含 Markdown 文件的普通文件夹。可搭配 Obsidian Sync、Obsidian Git 或任何文件同步工具（Syncthing、iCloud、Dropbox）实现跨设备同步。

**多人可以安全地编辑同一个知识库目录吗？**
可以（v1.7+）。通过 [`scripts/wiki-lock.sh`](scripts/wiki-lock.sh) 实现的文件级建议锁可防止并发写入导致页面损坏。并行导入子智能体在写入前会获取锁。过期锁会在 60 秒后自动清理。

**`hot.md` 和 `index.md` 有什么区别？**
`hot.md` 是近期上下文缓存（约 500 词，每次会话刷新）。`index.md` 是整个知识库目录中所有页面的主索引。Claude 优先读取 `hot.md`，然后是 `index.md`，最后深入具体页面。这种双层设计可保持重复查询时的 Token 消耗较低。

**我可以在不使用 Claude Code 的情况下使用它吗？**
该技能兼容 Agent Skills（实验性支持 OpenAI Codex CLI、Cursor、Windsurf、Gemini CLI、Goose）。目前仅在 Claude Code 上经过生产环境验证。跨主机安装路径遵循各主机的惯例，但技能发现机制可能有所不同。

**如何从 Dataview 迁移到 Bases？**
两者同时附带。`wiki/meta/dashboard.base` 为主仪表盘；`wiki/meta/dashboard.md` 为遗留的 Dataview 回退方案。在 Obsidian 中任选其一即可，另一者无影响。Bases 需要 Obsidian v1.9.10+（2025年8月）。

**方法论模式（LYT/PARA/Zettelkasten）与知识库使用场景（网站/GitHub/商业）有什么区别？**
方法论模式（v1.8+）控制页面的组织**方式**：文件夹结构 + 文件名约定。知识库使用场景（v1.0+）描述知识库的用途**内容类型**。两者可组合使用。例如，采用 PARA 方法论的企业知识库是有效的配置。

**这会将我的笔记发送到 Anthropic 吗？**
默认不会。可选的 `/wiki-retrieve` 技能包含 API 出口（`contextual-prefix.py`），但受 `--allow-egress` 同意标志限制。未启用该标志时，检索完全在本地进行（BM25 + 可选 ollama 重排）。`/autoresearch` 的网络出口也遵循相同的可选原则。

**公共版本与 AI Marketing Hub Pro 有什么区别？**
两者共享相同的 MIT 许可核心代码，位于 [`AgriciDaniel/claude-obsidian`](https://github.com/AgriciDaniel/claude-obsidian)，这也是推荐给所有人使用的安装源。AI Marketing Hub Pro 成员可抢先体验在此公开发布前处于开发阶段的功能，并获得直接协作支持与社区服务。核心功能中没有任何仅限付费版本的内容。

**什么是 DragonScale Memory？**
一个可选的启用扩展（`bash bin/setup-dragonscale.sh`），提供四种记忆机制：日志折叠（历史条目汇总）、确定性页面地址（基于计数器的唯一 ID）、语义分块校验（通过 ollama 验证内容边界）和边界优先自动研究（优先研究知识库的“前沿”）。非正常使用必需。完整指南：[`docs/dragonscale-guide.md`](docs/dragonscale-guide.md)。

---

## 环境要求

| 组件 | 最低版本 | 备注 |
|-----------|---------|-------|
| Claude Code | 最新版 | https://claude.com/claude-code |
| Obsidian | v1.9.10+（支持 Bases） | https://obsidian.md。v1.6+ 可使用 Dataview 回退方案。 |
| Python | 3.10+ | 用于可选的检索管道和测试套件 |
| Bash | 4.0+（或 zsh） | 用于设置脚本 |
| Git | 任意版本 | 通过 Obsidian Git 插件实现知识库目录自动提交 |

**可选组件：**

- **ollama**（用于 `/wiki-retrieve` 的本地重排）
- **defuddle-cli**（用于 `/defuddle` 的干净网页提取）
- **Anthropic API key**（用于 `/wiki-retrieve` 上下文前缀层，通过 `--allow-egress` 启用）
- **Local REST API plugin**（用于 REST-API MCP 传输方式）

---

## 卸载

插件安装：

```bash
claude plugin uninstall claude-obsidian@agricidaniel-claude-obsidian
claude plugin marketplace remove AgriciDaniel/claude-obsidian
```

克隆安装（删除文件夹）：

```bash
rm -rf /path/to/claude-obsidian
```

你的知识库内容（位于 `wiki/` 下）为纯 Markdown，卸载后不受影响。若要在不卸载的情况下清除运行时状态，请在仓库根目录运行 `make clean-test-state`。

---

## 贡献指南

欢迎提交 PR。请先阅读：

- [`CONTRIBUTING.md`](CONTRIBUTING.md)：工作流、六步自我审查清单、提交规范、隔离测试要求
- [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md)：Contributor Covenant v2.1
- [`SECURITY.md`](SECURITY.md)：负责任的安全披露政策
- [`CHANGELOG.md`](CHANGELOG.md)：版本历史（最新版：v1.9.2）

问题与 PR 模板位于 [`.github/`](.github/)。CI 会在每次 PR 时运行 `make test`、SKILL.md frontmatter 验证及插件清单 JSON 有效性检查。[`agents/verifier.md`](agents/verifier.md) 中的预提交验证智能体会对暂存区差异应用六步审查 + 智能体内核机制。

---

## 相关项目

- 🎨 [**claude-canvas**](https://github.com/AgriciDaniel/claude-canvas): visual canvas orchestration（12 种模板、6 种布局算法、AI 图像生成）。本插件的配套工具。
- 📊 [**claude-ads**](https://github.com/AgriciDaniel/claude-ads): multi-platform paid advertising audit（涵盖 Google、Meta、LinkedIn、TikTok、Microsoft、Apple、Amazon Ads 的 250+ 项检查）。
- 🔍 [**claude-seo**](https://github.com/AgriciDaniel/claude-seo): technical SEO + GEO audit suite. -> **claude-seo**：技术 SEO + GEO 审计套件。
- 🧠 [**best-practices**](https://github.com/AgriciDaniel/best-practices): composable engineering kernel. Source for the six-cut + agent kernel that `agents/verifier.md` enforces. -> **best-practices**：可组合的工程内核。`agents/verifier.md` 强制执行的六步审查 + 智能体内核的来源。

---

## 社区交流

- 📝 [**Blog post**](https://agricidaniel.com/blog/claude-obsidian-ai-second-brain): deep dive with competitor analysis, data charts, and workflow demos -> **博客文章**：深入解析，含竞品分析、数据图表和工作流演示
- 💬 [**AI Marketing Hub**](https://www.skool.com/ai-marketing-hub): 2,800+ members, free community -> **AI Marketing Hub**：2800+ 成员，免费社区
- ⚡ [**AI Marketing Hub Pro**](https://www.skool.com/ai-marketing-hub-pro): early access to in-development features and direct collaboration -> **AI Marketing Hub Pro**：抢先体验开发中功能及直接协作支持
- 🎬 [**YouTube**](https://www.youtube.com/@AgriciDaniel): tutorials and demos -> **YouTube 频道**：教程与演示
- 🔧 [**All open-source tools**](https://github.com/AgriciDaniel): claude-seo, claude-ads, claude-blog, and more -> **所有开源工具**：claude-seo、claude-ads、claude-blog 等

---

## 许可证

MIT 许可证。完整文本见 [LICENSE](LICENSE)。个人与商业用途免费。欢迎署名，但非强制要求。

---

## Star 历史

<a href="https://star-history.com/#AgriciDaniel/claude-obsidian&Date">
  <img src="https://api.star-history.com/svg?repos=AgriciDaniel/claude-obsidian&type=Date" alt="Star history chart for AgriciDaniel/claude-obsidian on GitHub" width="640" />
</a>

---

*基于 [Andrej Karpathy 的 LLM Wiki 模式](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)。由 [Agrici Daniel](https://agricidaniel.com/about) 构建。知识复利是思考者所能建立的最高杠杆习惯。*
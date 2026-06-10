[英文](README.md) | [中文](README.zh.md)

# fireworks-tech-graph

> **别再手动画图了。** 用英文或中文描述你的系统 —— 几秒钟即可生成出版级质量的 SVG + PNG 技术图表。

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Claude Code Skill](https://img.shields.io/badge/Claude%20Code-Skill-blue)](https://claude.ai/code)
[![7 Visual Styles](https://img.shields.io/badge/Styles-7-purple)]()
[![14 Diagram Types](https://img.shields.io/badge/Diagram%20Types-14-green)]()
[![UML Support](https://img.shields.io/badge/UML-Full%20Support-orange)]()

---

## 概述

`fireworks-tech-graph` 将自然语言描述转化为精美的 SVG 图表，并通过 `cairosvg`（推荐）导出为高分辨率 PNG，同时提供 `rsvg-convert` 和 `puppeteer` 作为备选方案。内置 **7 种视觉风格**，深度集成 AI/Agent 领域模式（RAG、Agentic Search、Mem0、Multi-Agent、Tool Call 流程），并完整支持全部 14 种 UML 图表类型。

```
User: "Generate a Mem0 memory architecture diagram, dark style"
  → Skill classifies: Memory Architecture Diagram, Style 2
  → Generates SVG with swim lanes, cylinders, semantic arrows
  → Exports 1920px PNG
  → Reports: mem0-architecture.svg / mem0-architecture.png
```

---

## 合作说明

本项目也是更广泛能力的一个验证示例：将模糊的 AI/开发工具工作流转化为受约束、可复用的系统，具备校验机制、文档支持、导出路径以及面向产品的打磨细节。

如果你正在构建 Agent 基础设施、AI IDE、内部 Copilot、开发者工具、技术文档系统或落地型 AI 工作流产品，我开放有限范围的付费冲刺（sprint）、设计合作伙伴项目以及创始工程师对话机会。

- Founder-facing profile: https://bradzhang.dev/en
- Commercial case study: https://bradzhang.dev/en/case-studies/fireworks-tech-graph
- Work with me: https://bradzhang.dev/en/work-with-me

---

## 效果展示

> 所有示例均通过 `cairosvg` 导出为 1920px 宽度（2× Retina）。PNG 是无损格式，非常适合技术图表 —— 边缘锐利，文本和线条无 JPEG 压缩伪影。

### Style 1 — Flat Icon
*Mem0 Memory Architecture — white background, semantic arrows, layered memory system*
![Style 1 — Flat Icon](assets/samples/sample-style1-flat.png)

### Style 2 — Dark Terminal
*Tool Call Flow — dark background, neon accents, monospace font*
![Style 2 — Dark Terminal](assets/samples/sample-style2-dark.png)

### Style 3 — Blueprint
*Microservices Architecture — deep blue background, grid lines, cyan strokes*
![Style 3 — Blueprint](assets/samples/sample-style3-blueprint.png)

### Style 4 — Notion Clean
*Agent Memory Types — minimal white, single accent color*
![Style 4 — Notion Clean](assets/samples/sample-style4-notion.png)

### Style 5 — Glassmorphism
*Multi-Agent Collaboration — dark gradient background, frosted glass cards*
![Style 5 — Glassmorphism](assets/samples/sample-style5-glass.png)

### Style 6 — Claude Official
*System Architecture — warm cream background (#f8f6f3), Anthropic brand colors, clean professional aesthetic*
![Style 6 — Claude Official](assets/samples/sample-style6-claude.png)

### Style 7 — OpenAI Official
*API Integration Flow — pure white background, OpenAI brand palette, modern minimalist design*
![Style 7 — OpenAI Official](assets/samples/sample-style7-openai.png)

---

## 稳定 Prompt 模板

当你希望模型输出尽可能贴近仓库中经过回归测试的最佳结果时，可使用以下 Prompt：

### Style 1 — Flat Icon
```text
Draw a Mem0 memory architecture diagram in style 1 (Flat Icon).
Use four horizontal sections: Input Layer, Memory Manager, Storage Layer, Output / Retrieval.
Include User, AI App / Agent, LLM, mem0 Client, Memory Manager, Vector Store, Graph DB, Key-Value Store, History Store, Context Builder, Ranked Results, Personalized Response.
Use semantic arrows for read, write, control, and data flow. Keep the layout clean and product-doc friendly.
```

### Style 2 — Dark Terminal
```text
Draw a tool call flow diagram in style 2 (Dark Terminal).
Show User query, Retrieve chunks, Generate answer, Knowledge base, Agent, Terminal, Source documents, and Grounded answer.
Use terminal chrome, neon accents, monospace typography, and semantic arrows for retrieval, synthesis, and embedding update.
```

### Style 3 — Blueprint
```text
Draw a microservices architecture diagram in style 3 (Blueprint).
Create numbered engineering sections like 01 // EDGE, 02 // APPLICATION SERVICES, 03 // DATA + EVENT INFRA, 04 // OBSERVABILITY.
Include Client Apps, API Gateway, Auth / Policy, three services, Event Router, Postgres, Redis Cache, Warehouse, and Metrics / Traces.
Use blueprint grid, cyan strokes, and a bottom-right title block.
```

### Style 4 — Notion Clean
```text
Draw an agent memory types diagram in style 4 (Notion Clean).
Compare Sensory Memory, Working Memory, Episodic Memory, Semantic Memory, and Procedural Memory around a central Agent core.
Use a minimal white layout, neutral borders, one accent color for arrows, and short storage tags for each memory type.
```

### Style 5 — Glassmorphism
```text
Draw a multi-agent collaboration diagram in style 5 (Glassmorphism).
Use three sections: Mission Control, Specialist Agents, and Synthesis.
Include User brief, Coordinator Agent, Research Agent, Coding Agent, Review Agent, Shared Memory, Synthesis Engine, and Final response.
Use frosted cards, soft glow, and semantic arrows for delegation, shared memory writes, and synthesis output.
```

### Style 6 — Claude Official
```text
Draw a system architecture diagram in style 6 (Claude Official).
Use left-side layer labels: Interface Layer, Core Layer, Foundation Layer.
Include Client Surface, Gateway, Task Planner, Model Runtime, Policy Guardrails, Memory Store, Tool Runtime, Observability, and Registry.
Use warm cream background, restrained brand-like palette, generous whitespace, and a bottom-right legend.
```

### Style 7 — OpenAI Official
```text
Draw an API integration flow diagram in style 7 (OpenAI Official).
Use three sections: Entry, Model + Tools, and Delivery.
Include Application, OpenAI SDK Layer, Prompt Builder, Model Runtime, Tool Calls, Response Formatter, Observability, and Release Control.
Keep the look minimal, white, precise, and modern with clean green-accented arrows.
```

---

## 核心特性

- **7 visual styles** — from clean white docs to dark neon to frosted glass to official brand styles -> **7 种视觉风格** —— 从简洁白底文档、深色霓虹风、毛玻璃效果到官方品牌风格
- **Executable style system** — style guides are encoded into the generator, not only documented in markdown -> **可执行的样式系统** —— 样式指南直接编码至生成器中，而非仅停留在 Markdown 文档里
- **14 diagram types** — Full UML support (Class, Component, Deployment, Package, Composite Structure, Object, Use Case, Activity, State Machine, Sequence, Communication, Timing, Interaction Overview, ER Diagram) plus AI/Agent domain diagrams -> **14 种图表类型** —— 完整支持 UML（类图、组件图等），并涵盖 AI/Agent 领域专属图表
- **AI/Agent domain patterns** — RAG, Agentic Search, Mem0, Multi-Agent, Tool Call, and more built-in -> **内置 AI/Agent 领域模式** —— 预置 RAG、Agentic Search、Mem0、Multi-Agent、Tool Call 等常见架构
- **Semantic shape vocabulary** — LLM = double-border rect, Agent = hexagon, Vector Store = ringed cylinder -> **语义化图形词汇** —— LLM 用双边框矩形表示，Agent 用六边形，向量库用带环圆柱体
- **Semantic arrow system** — color + dash pattern encode meaning (write vs read vs async vs loop) -> **语义化箭头系统** —— 颜色与虚线样式编码具体含义（写入/读取/异步/循环）
- **Product icons** — 40+ products with brand colors: OpenAI, Anthropic, Pinecone, Weaviate, Kafka, PostgreSQL… -> **产品图标库** —— 收录 40+ 主流产品的品牌色图标：OpenAI、Anthropic、Pinecone、Weaviate、Kafka、PostgreSQL…
- **Swim lane grouping** — automatic layer labeling for complex architectures -> **泳道分组（Swim lane）** —— 自动为复杂架构添加分层标签
- **SVG + PNG output** — SVG for editing, 1920px PNG for embedding -> **SVG + PNG 双格式输出** —— SVG 便于二次编辑，1920px PNG 适合直接嵌入文档
- **Renderer-friendly** — pure inline SVG, no external font fetching; renders cleanly in cairosvg, rsvg-convert, and headless Chrome -> **渲染器友好** —— 纯内联 SVG，不依赖外部字体拉取；在 cairosvg、rsvg-convert 和无头 Chrome 中均能干净渲染

---

## 安装

```bash
npx skills add yizhiyanhua-ai/fireworks-tech-graph
```

该 Skill 从 GitHub 仓库进行安装。npm 包页面为公开的分发地址：

```text
https://www.npmjs.com/package/@yizhiyanhua-ai/fireworks-tech-graph
```

请勿在 `skills add` 命令中使用 npm 包名，因为 CLI 会将安装源解析为 GitHub/本地路径。

## 更新

```bash
npx skills add yizhiyanhua-ai/fireworks-tech-graph --force -g -y
```

重新执行 `add --force` 即可拉取该 Skill 的最新版本。

或直接克隆：

```bash
git clone https://github.com/yizhiyanhua-ai/fireworks-tech-graph.git ~/.claude/skills/fireworks-tech-graph
```

---

## 环境要求

请选择 **一种** PNG 渲染器（推荐 cairosvg）：

```bash
# Recommended: cairosvg (best CSS support)
pip install cairosvg

# Fallback: rsvg-convert (system package; may drop CSS / <foreignObject>)
brew install librsvg                   # macOS
sudo apt install librsvg2-bin          # Ubuntu/Debian

# Highest fidelity: puppeteer (real Chromium; heavy)
npm install puppeteer

# Verify (any one is enough)
python3 -c "import cairosvg; print(cairosvg.__version__)"
rsvg-convert --version
```

| Renderer | Quality | Install Cost | Use When |
|----------|---------|--------------|----------|
| **cairosvg** | ✅ Good | Single `pip install` | Default — best balance |
| rsvg-convert | ⚠️ Fair | System package | No Python available, simple flat diagrams |
| puppeteer | ✅✅ Best | Node + ~150MB Chromium | Browser-generated SVG (D3, Mermaid) or pixel-perfect required |

---

## 为什么不直接用 Mermaid 或 draw.io？

| | Mermaid | draw.io | **fireworks-tech-graph** |
|--|---------|---------|--------------------------|
| Natural language input | ✗ | ✗ | ✅ |
| AI/Agent domain patterns | ✗ | ✗ | ✅ |
| Multiple visual styles | ✗ | manual | ✅ 5 built-in |
| High-res PNG export | ✗ | manual | ✅ auto 1920px |
| Semantic arrow colors | ✗ | manual | ✅ auto |
| No online tool needed | ✅ | ✗ | ✅ |

Mermaid 非常适合在 Markdown 中快速生成内联图表。draw.io 擅长手动精细调整。`fireworks-tech-graph` 专注于**描述系统并即时获得精美图表**，无需编写 DSL 语法或点击操作 GUI。

---

## 使用指南

### Trigger phrases
The skill auto-triggers on:

```
generate diagram / draw diagram / create chart / visualize
architecture diagram / flowchart / sequence diagram / data flow
```

### Basic usage

```
Draw a RAG pipeline flowchart
```

```
Generate an Agentic Search architecture diagram
```

### Specify style

```
Draw a microservices architecture diagram, style 2 (dark terminal)
```

```
Draw a multi-agent collaboration diagram --style glassmorphism
```

### Specify output path

```
Generate a Mem0 architecture diagram, output to ~/Desktop/
```

```
Create a tool call flow diagram --output /tmp/diagrams/
```

---

## 场景化 Prompt 示例

### AI/Agent Systems

```
Compare Agentic RAG vs standard RAG in a feature matrix, Notion clean style
```
→ Comparison matrix: RAG vs Agentic RAG, covering retrieval strategy, agent loop, tool use

```
Generate a Mem0 memory architecture diagram with vector store, graph DB, KV store, and memory manager
```
→ Memory Architecture with swim lanes: Input → Memory Manager → Storage tiers → Retrieval

```
Draw a Multi-Agent diagram: Orchestrator dispatches 3 SubAgents (search / compute / code execution), results aggregated
```
→ Agent Architecture with hexagons, tool layers, and result aggregation

```
Visualize the Tool Call execution flow: LLM → Tool Selector → Execution → Parser → back to LLM
```
→ Flowchart with decision loop showing tool invocation cycle

```
Draw the 5 agent memory types: Sensory, Working, Episodic, Semantic, Procedural
```
→ Mind map or layered architecture showing memory tiers from sensory to procedural

### Infrastructure & Cloud

```
Draw a microservices architecture: Client → API Gateway → [User Service / Order Service / Payment Service] → PostgreSQL + Redis
```
→ Architecture diagram with horizontal layers, swim lanes per service cluster

```
Generate a data pipeline diagram: Kafka → Spark processing → write to S3 → Athena query
```
→ Data flow diagram with labeled arrows (stream / batch / query)

```
Draw a Kubernetes deployment: Ingress → Service → [Pod × 3] → ConfigMap + PersistentVolume
```
→ Architecture with dashed containers per namespace, solid arrows for traffic flow

### API & Sequence Flows

```
Draw an OAuth2 authorization code flow sequence diagram: User → Client → Auth Server → Resource Server
```
→ Sequence diagram with vertical lifelines and activation boxes

```
Draw the ChatGPT Plugin call sequence diagram
```
→ Sequence: User → ChatGPT → Plugin Manifest → API → Response chain

### Decision & Process Flows

```
Draw a pre-launch QA flowchart for an AI app: Code Review → Security Scan → Performance Test → Manual Approval → Deploy
```
→ Flowchart with diamond decision nodes and parallel branches

```
Generate a feature comparison matrix: RAG vs Fine-tuning vs Prompt Engineering
```
→ Comparison matrix with checked/unchecked cells across cost, latency, accuracy, flexibility

### Concept Maps

```
Visualize the LLM application tech stack: from foundation model to SDK to app framework to deployment
```
→ Layered architecture or mind map from model layer to product layer

```
Draw an AI Agent capability map: Perception / Memory / Reasoning / Action / Learning
```
→ Mind map with central "AI Agent" node and 5 radial branches

---

## 样式说明

| # | Name | Background | Font | Best For |
|---|------|-----------|------|----------|
| 1 | **Flat Icon** *(default)* | `#ffffff` | Helvetica | Blogs, slides, docs |
| 2 | **Dark Terminal** | `#0f0f1a` | SF Mono / Fira Code | GitHub README, dev articles |
| 3 | **Blueprint** | `#0a1628` | Courier New | Architecture docs, engineering |
| 4 | **Notion Clean** | `#ffffff` | system-ui | Notion, Confluence, wikis |
| 5 | **Glassmorphism** | `#0d1117` gradient | Inter | Product sites, keynotes |
| 6 | **Claude Official** | `#f8f6f3` | system-ui | Anthropic-style diagrams, warm aesthetic |
| 7 | **OpenAI Official** | `#ffffff` | system-ui | OpenAI-style diagrams, clean modern look |

每种样式均在 `references/` 目录下配有专属参考文件，包含精确的颜色值、SVG 模板与规范。生成器还会读取具备样式感知能力的结构字段（如 `containers`、语义化的 `nodes[].kind`、`arrows[].flow` 及显式端口锚点），以确保示例级布局能够更稳定地复现。

用于精细化调整的实用配置字段：
- `style_overrides` to nudge title alignment or palette tokens without forking a full style -> **微调标题对齐或调色板**，无需 fork 完整样式文件
- `containers[].header_prefix` / `containers[].header_text` for blueprint-style numbered section headers such as `01 // EDGE` -> **蓝图风格编号章节头**（如 `01 // EDGE`）
- `containers[].side_label` for Claude-style left layer labels -> **左侧分层标签**（Claude 风格）
- `window_controls`, `meta_left`, `meta_center`, `meta_right` for terminal / document chrome -> **终端/文档装饰元素控制**
- `blueprint_title_block` for engineering title boxes in style 3 -> **工程标题框**（Style 3 专用）

### 样式选择指南

**For UML Diagrams:**
- **Class/Component/Package**: Style 1 (Flat Icon) or Style 4 (Notion Clean) — clear structure, easy to read -> **类图/组件图/包图**：推荐 Style 1 或 Style 4 —— 结构清晰，易于阅读
- **Sequence/Timing**: Style 2 (Dark Terminal) — monospace fonts help with alignment -> **时序图/时间图**：推荐 Style 2 —— 等宽字体有助于对齐
- **State Machine/Activity**: Style 3 (Blueprint) — engineering aesthetic fits process flows -> **状态机/活动图**：推荐 Style 3 —— 工程美学契合流程走向
- **Use Case/Interview**: Style 1 (Flat Icon) — colorful, accessible -> **用例图**：推荐 Style 1 —— 色彩丰富，直观易懂

**For AI/Agent Diagrams:**
- **RAG/Agentic Search**: Style 2 (Dark Terminal) or Style 5 (Glassmorphism) — tech-forward aesthetic -> **RAG/Agentic Search**：推荐 Style 2 或 Style 5 —— 科技感强
- **Memory Architecture**: Style 3 (Blueprint) — emphasizes layered storage tiers -> **记忆架构**：推荐 Style 3 —— 突出分层存储结构
- **Multi-Agent**: Style 5 (Glassmorphism) — frosted cards distinguish agent boundaries -> **多 Agent 协作**：推荐 Style 5 —— 毛玻璃卡片清晰区分 Agent 边界

**For Documentation:**
- **Internal docs**: Style 4 (Notion Clean) — minimal, wiki-friendly -> **内部文档**：Style 4（极简，适合 Wiki）
- **Blog posts**: Style 1 (Flat Icon) — colorful, engaging -> **博客文章**：Style 1（色彩丰富，吸引眼球）
- **GitHub README**: Style 2 (Dark Terminal) — matches dark theme -> **GitHub README**：Style 2（契合深色主题）
- **Presentations**: Style 5 (Glassmorphism) or Style 6 (Claude Official) — polished -> **演示文稿**：Style 5 或 Style 6（精致专业）

**Brand-Specific:**
- **Anthropic/Claude projects**: Style 6 (Claude Official) — warm cream background, brand colors -> **Anthropic/Claude 项目**：Style 6 —— 暖白背景，品牌色匹配
- **OpenAI projects**: Style 7 (OpenAI Official) — clean white, OpenAI palette -> **OpenAI 项目**：Style 7 —— 纯白底色，官方调色板

---

## 图表类型

| Type | Description | Key Layout Rule |
|------|-------------|-----------------|
| **Architecture** | Services, components, cloud infra | Horizontal layers top→bottom |
| **Data Flow** | What data moves where | Label every arrow with data type |
| **Flowchart** | Decisions, process steps | Diamond = decision, top→bottom |
| **Agent Architecture** | LLM + tools + memory | 5-layer model: Input/Agent/Memory/Tool/Output |
| **Memory Architecture** | Mem0, MemGPT-style | Separate read/write paths, memory tiers |
| **Sequence** | API call chains, time-ordered | Vertical lifelines, horizontal messages |
| **Comparison** | Feature matrix, side-by-side | Column = system, row = attribute |
| **Mind Map** | Concept maps, radial | Central node, bezier branches |

### UML Diagram Support (14 Types)

| UML Type | Description | Best Style |
|----------|-------------|------------|
| **Class Diagram** | Classes, attributes, methods, relationships | Style 1, 4 |
| **Component Diagram** | Software components and dependencies | Style 1, 3 |
| **Deployment Diagram** | Hardware nodes and software deployment | Style 3 |
| **Package Diagram** | Package organization and dependencies | Style 1, 4 |
| **Composite Structure** | Internal structure of classes/components | Style 1, 3 |
| **Object Diagram** | Object instances and relationships | Style 1, 4 |
| **Use Case Diagram** | Actors, use cases, system boundaries | Style 1 |
| **Activity Diagram** | Workflows, parallel processes | Style 3 |
| **State Machine** | State transitions and events | Style 2, 3 |
| **Sequence Diagram** | Message exchanges over time | Style 2 |
| **Communication Diagram** | Object interactions and messages | Style 1, 2 |
| **Timing Diagram** | State changes over time | Style 2 |
| **Interaction Overview** | High-level interaction flow | Style 1, 2 |
| **ER Diagram** | Entity-relationship data models | Style 1, 3 |

---

## AI/Agent 领域模式

内置模式知识库：

```
RAG Pipeline         → Query → Embed → VectorSearch → Retrieve → LLM → Response
Agentic RAG          → adds Agent loop + Tool use
Agentic Search       → Query → Planner → [Search/Calc/Code] → Synthesizer
Mem0 Memory Layer    → Input → Memory Manager → [VectorDB + GraphDB] → Context
Agent Memory Types   → Sensory → Working → Episodic → Semantic → Procedural
Multi-Agent          → Orchestrator → [SubAgent×N] → Aggregator → Output
Tool Call Flow       → LLM → Tool Selector → Execution → Parser → LLM (loop)
```

---

## 图形语义对照

Shapes encode semantic meaning consistently across all styles:

| Concept | Shape |
|---------|-------|
| User / Human | Circle + body |
| LLM / Model | Rounded rect, double border, ⚡ |
| Agent / Orchestrator | Hexagon |
| Memory (short-term) | Dashed-border rounded rect |
| Memory (long-term) | Solid cylinder |
| Vector Store | Cylinder with inner rings |
| Graph DB | 3-circle cluster |
| Tool / Function | Rect with ⚙ |
| API / Gateway | Hexagon (single border) |
| Queue / Stream | Horizontal pipe/tube |
| Document / File | Folded-corner rect |
| Browser / UI | Rect with 3-dot titlebar |
| Decision | Diamond |
| External Service | Dashed-border rect |

---

## 箭头语义规范

| Flow Type | Stroke | Dash | Meaning |
|-----------|--------|------|---------|
| Primary data flow | 2px solid | — | Main request/response |
| Control / trigger | 1.5px solid | — | System A triggers B |
| Memory read | 1.5px solid | — | Retrieve from store |
| Memory write | 1.5px | `5,3` | Write/store operation |
| Async / event | 1.5px | `4,2` | Non-blocking |
| Feedback / loop | 1.5px curved | — | Iterative reasoning |

---

## 项目结构

```
fireworks-tech-graph/
├── SKILL.md                      # Main skill — diagram types, layout rules, shape vocab
├── README.md                     # This file (English)
├── README.zh.md                  # Chinese version
├── references/
│   ├── style-1-flat-icon.md      # White background, colored accents
│   ├── style-2-dark-terminal.md  # Dark bg, neon accents, monospace
│   ├── style-3-blueprint.md      # Blueprint grid, cyan lines
│   ├── style-4-notion-clean.md   # Minimal, white, single arrow color
│   ├── style-5-glassmorphism.md  # Dark gradient, frosted glass cards
│   ├── style-6-claude-official.md # Warm cream background, Anthropic brand
│   ├── style-7-openai.md      # Clean white, OpenAI brand palette
│   └── icons.md                  # 40+ product icons + semantic shapes
├── agents/
│   └── openai.yaml              # Agent metadata for compatible runtimes
├── fixtures/
│   ├── mem0-style1.json         # Style 1 regression fixture
│   ├── tool-call-style2.json    # Style 2 regression fixture
│   └── ...                      # Additional sample-grade fixtures per style
├── scripts/
│   ├── generate-diagram.sh       # Validate SVG + export PNG
│   ├── generate-from-template.py # Create starter SVGs from templates
│   ├── validate-svg.sh           # Validate SVG syntax
│   └── test-all-styles.sh        # Batch test all styles
├── assets/
│   └── samples/                  # Showcase diagram PNGs
├── templates/
│   ├── architecture.svg         # Architecture starter template
│   ├── data-flow.svg            # Data-flow starter template
│   └── ...                      # Additional diagram templates
└── agentloop-core.svg           # Included sample SVG
```

---

## 产品图标覆盖范围

**AI/ML:** OpenAI, Anthropic/Claude, Google Gemini, Meta LLaMA, Mistral, Cohere, Groq, Hugging Face

**AI Frameworks:** Mem0, LangChain, LlamaIndex, LangGraph, CrewAI, AutoGen, DSPy, Haystack

**Vector DBs:** Pinecone, Weaviate, Qdrant, Chroma, Milvus, pgvector, Faiss

**Databases:** PostgreSQL, MySQL, MongoDB, Redis, Elasticsearch, Neo4j, Cassandra

**Messaging:** Kafka, RabbitMQ, NATS, Pulsar

**Cloud:** AWS, GCP, Azure, Cloudflare, Vercel, Docker, Kubernetes

**Observability:** Grafana, Prometheus, Datadog, LangSmith, Langfuse, Arize

---

## 常见问题排查

| Symptom | Cause | Fix |
|---------|-------|-----|
| PNG is blank or all-black | `@import url()` in SVG — neither cairosvg nor rsvg-convert can fetch external fonts | Remove `@import`, use system font stack |
| PNG not generated | No renderer installed | `pip install cairosvg` (recommended), or `brew install librsvg` / `apt install librsvg2-bin` |
| Borders or text missing in PNG | Using `rsvg-convert` on SVG with CSS / `<foreignObject>` | Switch to `cairosvg` (`pip install cairosvg`) — much better CSS support |
| Diagram cut off at bottom | ViewBox height too short | Increase `height` in `viewBox="0 0 960 <height>"` |
| Text overflowing boxes | Labels too long | Add `text-anchor="middle"` + `<clipPath>` or shorten label |
| Icons not rendering | External CDN URL | Use inline SVG paths from `references/icons.md` |
| Browser-generated SVG renders incorrectly | cairosvg / rsvg can't replay all CSS/JS-injected styles | Use the puppeteer script in `SKILL.md` for 100% fidelity |

---

## License

MIT © 2025 fireworks-tech-graph contributors
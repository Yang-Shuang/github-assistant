# AI 核心项目：AI 工程进阶之路
## 第一阶段 RAG 系统：arXiv 论文策展人

<div align="center">
  <h3>面向学习者的生产级 RAG（检索增强生成）系统构建之旅</h3>
  <p>通过动手实践，从零开始掌握现代 AI 系统的构建方法</p>
  <p>掌握最热门的 AI 工程技能：<strong>RAG（检索增强生成）</strong></p>
</div>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.12+-blue.svg" alt="Python Version">
  <img src="https://img.shields.io/badge/FastAPI-0.115+-green.svg" alt="FastAPI">
  <img src="https://img.shields.io/badge/OpenSearch-2.19-orange.svg" alt="OpenSearch">
  <img src="https://img.shields.io/badge/Docker-Compose-blue.svg" alt="Docker">
  <img src="https://img.shields.io/badge/Status-Week%207%20Advanced%20Features-brightgreen.svg" alt="Status">
</p>

</br>

<p align="center">
  <a href="#-about-this-course">
    <img src="static/mother_of_ai_project_rag_architecture.gif" alt="RAG Architecture" width="700">
  </a>
</p>

## 📖 课程简介

这是一个**以学习者为中心的项目**。你将构建一个完整的科研助手系统，该系统能够自动获取学术论文、理解其内容，并使用先进的 RAG 技术回答你的研究问题。

**arXiv 论文策展人**将教你如何使用行业最佳实践构建**生产级 RAG 系统**。与直接跳入向量搜索的教程不同，我们遵循**专业路径**：先掌握关键词检索基础，再结合向量实现混合检索。

> **🎯 专业做法的区别：** 我们像成功的企业一样构建 RAG 系统——以扎实的检索基础为核心，辅以 AI 增强，而非忽视检索基础的“AI 优先”方案。

完成本课程后，你将拥有自己的 AI 科研助手，并具备为任何领域构建生产级 RAG 系统的深厚技术能力。

### **🎓 你将构建的内容**

- **第 1 周：** Docker、FastAPI、PostgreSQL、OpenSearch 和 Airflow 的完整基础设施
- **第 2 周：** 自动从 arXiv 获取并解析学术论文的数据管道  
- **第 3 周：** 带过滤和相关性评分的生产级 BM25 关键词搜索
- **第 4 周：** 智能分块 + 结合关键词与语义理解的混合检索
- **第 5 周：** 完整的 RAG 流水线，支持本地 LLM、流式响应及 Gradio 界面
- **第 6 周：** 基于 Langfuse 追踪和 Redis 缓存的生产级监控与性能优化
- **第 7 周：** **基于 LangGraph 的 Agent（智能体）RAG 系统及 Telegram Bot 移动端接入**

---

## 🏗️ 系统架构演进

### 第 7 周：Agent RAG & Telegram Bot 集成
<div align="center">
  <img src="static/week7_telegram_and_agentic_ai.png" alt="Week 7 Telegram and Agentic AI Architecture" width="800">
  <p><em>展示 Telegram Bot 与 Agent RAG 系统集成的完整第 7 周架构</em></p>
</div>

### LangGraph Agent RAG 工作流
<div align="center">
  <img src="static/langgraph-mermaid.png" alt="LangGraph Agentic RAG Flow" width="800">
  <p><em>详细展示决策节点、文档评分和自适应检索的 LangGraph 工作流</em></p>
</div>


**第 7 周代码讲解 + 博客：** [Agentic RAG with LangGraph and Telegram](https://jamwithai.substack.com/p/agentic-rag-with-langgraph-and-telegram) 

**第 7 周核心创新点：**
- **智能决策**：Agent（智能体）评估并自适应调整检索策略
- **文档评分**：基于语义评估的自动相关性打分
- **查询重写**：在结果不足时自适应优化查询语句
- **安全护栏（Guardrails）**：检测超范围问题，防止幻觉生成
- **移动端访问**：通过 Telegram Bot 实现跨设备对话式 AI
- **透明度**：完整追踪推理步骤，便于调试与建立信任

---

## 🚀 快速开始

### **📋 前置要求**
- **Docker Desktop**（需包含 Docker Compose）  
- **Python 3.12+**
- **UV 包管理器**（[安装指南](https://docs.astral.sh/uv/getting-started/installation/)）
- **8GB+ RAM** 和 **20GB+ 可用磁盘空间**

### **⚡ 开始使用**

```bash
# 1. Clone and setup
git clone <repository-url>
cd arxiv-paper-curator

# 2. Configure environment (IMPORTANT!)
cp .env.example .env
# The .env file contains all necessary configuration for OpenSearch, 
# arXiv API, and service connections. Defaults work out of the box.
# You need to add Jina embeddings free api key and langfuse keys (check the blogs)

# 3. Install dependencies
uv sync

# 4. Start all services
docker compose up --build -d

# 5. Verify everything works
curl http://localhost:8000/api/v1/health
```

### **📚 每周学习路径**

| Week | Topic | Blog Post | Code Release |
|------|-------|-----------|--------------|
| **Week 0** | The Mother of AI project - 6 phases | [The Mother of AI project](https://jamwithai.substack.com/p/the-mother-of-ai-project) | - |
| **Week 1** | Infrastructure Foundation | [The Infrastructure That Powers RAG Systems](https://jamwithai.substack.com/p/the-infrastructure-that-powers-rag) | [week1.0](https://github.com/jamwithai/arxiv-paper-curator/releases/tag/week1.0) |
| **Week 2** | Data Ingestion Pipeline | [Building Data Ingestion Pipelines for RAG](https://jamwithai.substack.com/p/bringing-your-rag-system-to-life) | [week2.0](https://github.com/jamwithai/arxiv-paper-curator/releases/tag/week2.0) |
| **Week 3** | OpenSearch ingestion & BM25 retrieval | [The Search Foundation Every RAG System Needs](https://jamwithai.substack.com/p/the-search-foundation-every-rag-system) | [week3.0](https://github.com/jamwithai/arxiv-paper-curator/releases/tag/week3.0) |
| **Week 4** | **Chunking & Hybrid Search** | [The Chunking Strategy That Makes Hybrid Search Work](https://jamwithai.substack.com/p/chunking-strategies-and-hybrid-rag) | [week4.0](https://github.com/jamwithai/arxiv-paper-curator/releases/tag/week4.0) |
| **Week 5** | **Complete RAG system** | [The Complete RAG System](https://jamwithai.substack.com/p/the-complete-rag-system) | [week5.0](https://github.com/jamwithai/arxiv-paper-curator/releases/tag/week5.0) |
| **Week 6** | **Production monitoring & caching** | [Production-ready RAG: Monitoring & Caching](https://jamwithai.substack.com/p/production-ready-rag-monitoring-and) | [week6.0](https://github.com/jamwithai/arxiv-paper-curator/releases/tag/week6.0) |
| **Week 7** | **Agentic RAG & Telegram Bot** | [Agentic RAG with LangGraph and Telegram](https://jamwithai.substack.com/p/agentic-rag-with-langgraph-and-telegram) | [week7.0](https://github.com/jamwithai/arxiv-paper-curator/releases/tag/week7.0) |

**📥 克隆特定周期的代码：**
```bash
# Clone a specific week's code
git clone --branch <WEEK_TAG> https://github.com/jamwithai/arxiv-paper-curator
cd arxiv-paper-curator
uv sync
docker compose down -v
docker compose up --build -d

# Replace <WEEK_TAG> with: week1.0, week2.0, etc.
```

### **📊 访问你的服务**

| Service | URL | Purpose |
|---------|-----|---------|
| **API Documentation** | http://localhost:8000/docs | Interactive API testing |
| **Gradio RAG Interface** | http://localhost:7861 | User-friendly chat interface |
| **Langfuse Dashboard** | http://localhost:3000 | RAG pipeline monitoring & tracing |
| **Airflow Dashboard** | http://localhost:8080 | Workflow management |
| **OpenSearch Dashboards** | http://localhost:5601 | Hybrid search engine UI |

#### **注意**: 请在 `airflow/simple_auth_manager_passwords.json.generated` 中查看 Airflow 的用户名和密码
---

## 📚 Week 1：基础设施基础 ✅

**从这里开始！** 掌握支撑现代 RAG 系统的基础设施。

### **🎯 学习目标**
- 使用 Docker Compose 完成完整基础设施搭建
- FastAPI 开发（含自动文档生成与健康检查）
- PostgreSQL 数据库配置与管理
- OpenSearch 混合搜索引擎设置
- Ollama 本地 LLM 服务配置
- 服务编排与健康监控
- 配备代码质量工具的专业开发环境

### **🏗️ 架构概览**

<p align="center">
  <img src="static/week1_infra_setup.png" alt="Week 1 Infrastructure Setup" width="800">
</p>

**基础设施组件：**
- **FastAPI**：支持异步的 REST API（端口 8000）  
- **PostgreSQL 16**：论文元数据存储（端口 5432）
- **OpenSearch 2.19**：带控制面板的搜索引擎（端口 9200、5601）
- **Apache Airflow 3.0**：工作流编排（端口 8080）
- **Ollama**：本地 LLM 服务器（端口 11434）

### **📓 设置指南**

```bash
# Launch the Week 1 notebook
uv run jupyter notebook notebooks/week1/week1_setup.ipynb
```

**完成指南：** 跟随 [Week 1 notebook](notebooks/week1/week1_setup.ipynb) 进行动手实践与验证步骤。

### **📖 深入阅读**
**博客文章：** [The Infrastructure That Powers RAG Systems](https://jamwithai.substack.com/p/the-infrastructure-that-powers-rag) - 详细讲解与生产环境洞察

---

## 📚 Week 2：数据摄入管道 ✅

**基于第 1 周基础设施：** 学习如何自动获取、处理并存储学术论文。

### **🎯 学习目标**
- arXiv API 集成（含速率限制与重试机制）
- 使用 Docling 解析科学 PDF 文档
- Apache Airflow 自动化数据摄入管道
- 元数据提取与存储工作流
- 完整的论文处理流程：从 API 到数据库

### **🏗️ 架构概览**

<p align="center">
  <img src="static/week2_data_ingestion_flow.png" alt="Week 2 Data Ingestion Architecture" width="800">
</p>

**数据管道组件：**
- **MetadataFetcher**：🎯 主协调器，统筹整个管道流程
- **ArxivClient**：带速率限制与重试机制的论文获取客户端
- **PDFParserService**：基于 Docling 的科学文档处理服务  
- **Airflow DAGs**：自动化每日论文摄入工作流
- **PostgreSQL Storage**：结构化论文元数据与内容存储

### **📓 实现指南**

```bash
# Launch the Week 2 notebook  
uv run jupyter notebook notebooks/week2/week2_arxiv_integration.ipynb
```

**完成指南：** 跟随 [Week 2 notebook](notebooks/week2/week2_arxiv_integration.ipynb) 进行动手实现与验证步骤。

### **📖 深入阅读**
**博客文章：** [Building Data Ingestion Pipelines for RAG](https://jamwithai.substack.com/p/bringing-your-rag-system-to-life) - arXiv API 集成与 PDF 处理详解

---

## 📚 Week 3：关键词检索优先——关键基础

**基于第 1-2 周基础：** 实现专业 RAG 系统所依赖的关键词检索基础。

### **🎯 学习目标**
- 为什么关键词检索对 RAG 系统至关重要（先打基础的方法论）
- OpenSearch 索引管理、映射配置与搜索优化
- BM25 算法及高效关键词检索背后的数学原理
- 使用查询 DSL 构建带过滤和权重提升的复杂搜索查询
- 通过搜索分析衡量相关性与性能
- 真实企业采用的生产级模式

### **🏗️ 架构概览**

<p align="center">
  <img src="static/week3_opensearch_flow.png" alt="Week 3 OpenSearch Flow Architecture" width="800">
</p>

**搜索基础设施组件：**
- **OpenSearch Service**：`src/services/opensearch/` - 专业级搜索服务实现
- **Search API**：`src/routers/search.py` - 带 BM25 评分的搜索 API 端点
- **学习资料**：`notebooks/week3/` - 完整的 OpenSearch 集成指南
- **质量指标**：精确率、召回率与相关性评分

### **📓 设置指南**

```bash
# Launch the Week 3 notebook
uv run jupyter notebook notebooks/week3/week3_opensearch.ipynb
```

**完成指南：** 跟随 [Week 3 notebook](notebooks/week3/week3_opensearch.ipynb) 进行 OpenSearch 设置与 BM25 搜索实现的动手实践。

### **📖 深入阅读**
**博客文章：** [The Search Foundation Every RAG System Needs](https://jamwithai.substack.com/p/the-search-foundation-every-rag-system) - 完整的 BM25 实现与 OpenSearch 集成指南

---

## 📚 Week 4：分块与混合检索——语义层

**基于第 3 周基础：** 添加让搜索真正智能化的语义层。

### **🎯 学习目标**
- 基于章节的智能文档分段（Chunking）
- 生产级 Embedding 生成（含 Jina AI 集成与降级策略）
- 混合检索精通：使用 RRF 融合算法结合关键词与语义检索
- 统一 API 设计：单端点支持多种搜索模式
- 性能分析与不同搜索方案的权衡对比

### **🏗️ 架构概览**

<p align="center">
  <img src="static/week4_hybrid_opensearch.png" alt="Week 4 Hybrid Search Architecture" width="800">
</p>

**混合检索基础设施组件：**
- **Text Chunker**：`src/services/indexing/text_chunker.py` - 感知章节结构并支持重叠策略的分块器
- **Embeddings Service**：`src/services/embeddings/` - 生产级 Embedding 管道（集成 Jina AI）
- **Hybrid Search API**：`src/routers/hybrid_search.py` - 统一搜索 API，支持所有模式
- **学习资料**：`notebooks/week4/` - 完整的混合检索实现指南

### **📓 设置指南**

```bash
# Launch the Week 4 notebook
uv run jupyter notebook notebooks/week4/week4_hybrid_search.ipynb
```

**完成指南：** 跟随 [Week 4 notebook](notebooks/week4/week4_hybrid_search.ipynb) 进行动手实现与验证步骤。

### **📖 深入阅读**
**博客文章：** [The Chunking Strategy That Makes Hybrid Search Work](https://jamwithai.substack.com/p/chunking-strategies-and-hybrid-rag) - 生产级分块策略与 RRF 融合实现详解

---

## 📚 Week 5：集成 LLM 的完整 RAG 流水线

**基于第 4 周混合检索：** 添加将搜索转化为智能对话的 LLM 层。

### **🎯 学习目标**
- 通过 Ollama 集成本地 LLM，保障数据隐私
- 性能优化：提示词减少 80%（速度提升 6 倍）
- 基于 Server-Sent Events (SSE) 的流式响应实现
- 双端点 API 设计：标准接口与流式接口并存
- 交互式 Gradio 界面，支持高级参数控制

### **🏗️ 架构概览**

<p align="center">
  <img src="static/week5_complete_rag.png" alt="Week 5 Complete RAG System Architecture" width="900">
</p>

**完整 RAG 基础设施组件：**
- **RAG Endpoints**：`src/routers/ask.py` - 双端点（`/api/v1/ask` + `/api/v1/stream`）
- **Ollama Service**：`src/services/ollama/` - LLM 客户端与优化提示词
- **System Prompt**：`src/services/ollama/prompts/rag_system.txt` - 针对学术论文优化的系统提示词
- **Gradio Interface**：`src/gradio_app.py` - 支持流式响应的交互式 Web UI
- **Launcher Script**：`gradio_launcher.py` - 便捷启动脚本（运行于端口 7861）

### **📓 设置指南**

```bash
# Launch the Week 5 notebook
uv run jupyter notebook notebooks/week5/week5_complete_rag_system.ipynb

# Launch Gradio interface
uv run python gradio_launcher.py
# Open http://localhost:7861
```

**完成指南：** 跟随 [Week 5 notebook](notebooks/week5/week5_complete_rag_system.ipynb) 进行 LLM 集成与 RAG 流水线实现的动手实践。

### **📖 深入阅读**
**博客文章：** [The Complete RAG System](https://jamwithai.substack.com/p/the-complete-rag-system) - 完整 RAG 系统架构、本地 LLM 集成与优化技巧详解

---

## 📚 Week 6：生产级监控与缓存

**基于第 5 周完整 RAG 系统：** 添加可观测性、性能优化与生产级监控。

### **🎯 学习目标**
- Langfuse 集成实现端到端 RAG 流水线追踪
- Redis 缓存策略（智能缓存键设计与 TTL 管理）
- 实时仪表盘监控延迟与成本
- 生产环境下的可观测性与优化模式
- 成本分析与 LLM 使用优化（缓存加速 150-400 倍）

### **🏗️ 架构概览**

<p align="center">
  <img src="static/week6_monitoring_and_caching.png" alt="Week 6 Monitoring & Caching Architecture" width="900">
</p>

**生产基础设施组件：**
- **Langfuse Service**：`src/services/langfuse/` - 完整追踪集成与 RAG 专属指标
- **Cache Service**：`src/services/cache/` - Redis 客户端（精确匹配缓存与优雅降级）
- **Updated Endpoints**：`src/routers/ask.py` - 集成追踪与缓存中间件的端点
- **Docker Config**：`docker-compose.yml` - 新增 Redis 服务与 Langfuse 本地实例配置
- **学习资料**：`notebooks/week6/` - 完整的监控与缓存实现指南

### **📓 设置指南**

```bash
# Launch the Week 6 notebook
uv run jupyter notebook notebooks/week6/week6_cache_testing.ipynb
```

**完成指南：** 跟随 [Week 6 notebook](notebooks/week6/week6_cache_testing.ipynb) 进行 Langfuse 追踪与 Redis 缓存实现的动手实践。

### **📖 深入阅读**
**博客文章：** [Production-ready RAG: Monitoring & Caching](https://jamwithai.substack.com/p/production-ready-rag-monitoring-and) - 生产级 RAG 监控与缓存最佳实践

---

## 📚 Week 7：基于 LangGraph 的 Agent RAG 与 Telegram Bot

**基于第 6 周生产系统：** 添加智能推理、多步决策，并集成 Telegram Bot 实现移动端优先的 AI 交互。

### **🎯 学习目标**
- LangGraph 工作流：基于状态的 Agent（智能体）编排与决策节点设计
- Guardrail 实现：查询验证与领域边界检测
- 文档评分：语义相关性评估
- 查询重写：自动优化查询语句以提升检索效果
- 自适应检索：多轮尝试检索与智能降级策略
- Telegram Bot 集成：异步操作与异常处理机制
- 推理透明度：暴露 Agent 决策过程，便于调试与建立信任

### **🏗️ 架构概览**

<p align="center">
  <img src="static/week7_telegram_and_agentic_ai.png" alt="Week 7 Agentic RAG & Telegram Architecture" width="900">
</p>

**Agent RAG 基础设施组件：**
- **Agent Nodes**：`src/services/agents/nodes/` - Guardrail、retrieve、grade、rewrite、generate 节点
- **Workflow Orchestration**：`src/services/agents/agentic_rag.py` - LangGraph 工作流协调器
- **Telegram Bot**：`src/services/telegram/` - 命令处理器与消息处理逻辑
- **Agentic Endpoint**：`src/routers/agentic_ask.py` - Agent RAG API 端点
- **学习资料**：`notebooks/week7/` - 第 7 周学习材料与示例

### **📓 设置指南**

```bash
# Launch the Week 7 notebook
uv run jupyter notebook notebooks/week7/week7_agentic_rag.ipynb
```

**完成指南：** 跟随 [Week 7 notebook](notebooks/week7/week7_agentic_rag.ipynb) 进行 LangGraph Agent RAG 与 Telegram Bot 实现的动手实践。

### **📖 深入阅读**
**博客文章：** [Agentic RAG with LangGraph and Telegram](https://jamwithai.substack.com/p/agentic-rag-with-langgraph-and-telegram) - 构建具备决策能力、自适应检索与移动端访问的智能 Agent

---

## ⚙️ 配置说明

**设置步骤：**
```bash
cp .env.example .env
# Edit .env for your environment
```

**关键变量：**
- `JINA_API_KEY` - 第 4 周及之后必需（用于混合检索与 Embedding）
- `TELEGRAM__BOT_TOKEN` - 第 7 周必需（Telegram Bot 集成）
- `LANGFUSE__PUBLIC_KEY` & `LANGFUSE__SECRET_KEY` - 第 6 周可选（监控追踪）

**完整配置：** 查看 [.env.example](.env.example) 获取所有可用选项与详细文档。

---

## 🔧 参考与开发指南

### **🛠️ 技术栈**

| Service | Purpose | Status |
|---------|---------|--------|
| **FastAPI** | REST API with automatic docs | ✅ Ready |
| **PostgreSQL 16** | Paper metadata and content storage | ✅ Ready |
| **OpenSearch 2.19** | Hybrid search engine (BM25 + Vector) | ✅ Ready |
| **Apache Airflow 3.0** | Workflow automation | ✅ Ready |
| **Jina AI** | Embedding generation (Week 4) | ✅ Ready |
| **Ollama** | Local LLM serving (Week 5) | ✅ Ready |
| **Redis** | High-performance caching (Week 6) | ✅ Ready |
| **Langfuse** | RAG pipeline observability (Week 6) | ✅ Ready |

**开发工具：** UV, Ruff, MyPy, Pytest, Docker Compose

### **🏗️ 项目结构**

```
arxiv-paper-curator/
├── src/                    # Main application code
│   ├── routers/            # API endpoints (search, ask, papers)
│   ├── services/           # Business logic (opensearch, ollama, agents, cache)
│   ├── models/             # Database models (SQLAlchemy)
│   ├── schemas/            # Pydantic validation schemas
│   └── config.py           # Environment configuration
├── notebooks/              # Weekly learning materials (week1-7)
├── airflow/                # Workflow orchestration (DAGs)
├── tests/                  # Test suite
└── compose.yml             # Docker service orchestration
```

### **📡 API 端点参考**

| Endpoint | Method | Description | Week |
|----------|--------|-------------|------|
| `/health` | GET | Service health check | Week 1 |
| `/api/v1/papers` | GET | List stored papers | Week 2 |
| `/api/v1/papers/{id}` | GET | Get specific paper | Week 2 |
| `/api/v1/search` | POST | BM25 keyword search | Week 3 |
| `/api/v1/hybrid-search/` | POST | Hybrid search (BM25 + Vector) | **Week 4** |

**API 文档：** 访问 http://localhost:8000/docs 查看交互式 API 浏览器

### **🔧 常用命令**

#### **使用 Makefile（推荐）**
```bash
# View all available commands
make help

# Quick workflow
make start         # Start all services
make health        # Check all services health
make test          # Run tests
make stop          # Stop services
```

#### **所有可用命令**
| Command | Description |
|---------|-------------|
| `make start` | Start all services |
| `make stop` | Stop all services |
| `make restart` | Restart all services |
| `make status` | Show service status |
| `make logs` | Show service logs |
| `make health` | Check all services health |
| `make setup` | Install Python dependencies |
| `make format` | Format code |
| `make lint` | Lint and type check |
| `make test` | Run tests |
| `make test-cov` | Run tests with coverage |
| `make clean` | Clean up everything |

#### **直接命令（备选）**
```bash
# If you prefer using commands directly
docker compose up --build -d    # Start services
docker compose ps               # Check status
docker compose logs            # View logs
uv run pytest                 # Run tests
```

### **🎓 目标受众**
| Who | Why |
|-----|-----|
| **AI/ML Engineers** | Learn production RAG architecture beyond tutorials |
| **Software Engineers** | Build end-to-end AI applications with best practices |
| **Data Scientists** | Implement production AI systems using modern tools |

---

## 🛠️ 故障排除

**常见问题：**
- **服务无法启动？** 等待 2-3 分钟，检查 `docker compose logs`
- **端口冲突？** 停止占用 8000、8080、5432、9200 端口的其他服务
- **内存不足？** 增加 Docker Desktop 的内存分配限制

**获取帮助：**
- 查看完整的第 1 周 notebook 故障排除章节
- 检查服务日志：`docker compose logs [service-name]`
- 完全重置环境：`docker compose down --volumes && docker compose up --build -d`

---

## 💰 成本说明

**本课程完全免费！** 你只需为可选服务支付少量费用：
- **本地开发：** $0（所有组件均在本地运行）
- **可选云端 API：** ~$2-5（若选择外部 LLM 云服务）

---

<div align="center">
  <h3>🎉 准备好开始你的 AI 工程之旅了吗？</h3>
  <p><strong>从第 1 周设置 notebook 开始，构建你的第一个生产级 RAG 系统！</strong></p>
  
  <p><em>专为希望掌握现代 AI 工程的学习者打造</em></p>
  <p><strong>Built with love by <a href="https://www.linkedin.com/in/shirin-khosravi-jam/">Shirin Khosravi Jam</a> & <a href="https://www.linkedin.com/in/shantanuladhwe/">Shantanu Ladhwe</a></strong></p>
</div>

---

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=jamwithai/production-agentic-rag-course&type=Date)](https://star-history.com/#jamwithai/production-agentic-rag-course&Date)

---

## 📄 许可证

MIT License - see [LICENSE](LICENSE) file for details.
<img width="1217" alt="Screenshot 2025-03-27 at 6 35 02 AM" src="https://github.com/user-attachments/assets/10b530a6-527f-4335-b2e4-ceaa9fc1219f" />

<h3 align="center">
最先进的 AI 检索系统。

具备 RESTful API 的 Agent 化检索增强生成（Retrieval-Augmented Generation, RAG）。
</h3>

<div align="center">
   <div>
      <a href="https://r2r-docs.sciphi.ai/"><strong>Docs</strong></a> ·
      <a href="https://github.com/SciPhi-AI/R2R/issues/new?assignees=&labels=&projects=&template=bug_report.md&title="><strong>Report Bug</strong></a> ·
      <a href="https://github.com/SciPhi-AI/R2R/issues/new?assignees=&labels=&projects=&template=feature_request.md&title="><strong>Feature Request</strong></a> ·
      <a href="https://discord.gg/p6KqD2kjtB"><strong>Discord</strong></a>
   </div>
   <br />
   <p align="center">
    <a href="https://r2r-docs.sciphi.ai"><img src="https://img.shields.io/badge/docs.sciphi.ai-3F16E4" alt="Docs"></a>
    <a href="https://discord.gg/p6KqD2kjtB"><img src="https://img.shields.io/discord/1120774652915105934?style=social&logo=discord" alt="Discord"></a>
    <a href="https://github.com/SciPhi-AI"><img src="https://img.shields.io/github/stars/SciPhi-AI/R2R" alt="Github Stars"></a>
    <a href="https://github.com/SciPhi-AI/R2R/pulse"><img src="https://img.shields.io/github/commit-activity/w/SciPhi-AI/R2R" alt="Commits-per-week"></a>
    <a href="https://opensource.org/licenses/MIT"><img src="https://img.shields.io/badge/License-MIT-purple.svg" alt="License: MIT"></a>
  </p>
</div>

# 关于 (About)
R2R 是一款先进的 AI 检索系统，支持检索增强生成（Retrieval-Augmented Generation, RAG），并具备开箱即用的生产级功能。围绕 RESTful API 构建，R2R 提供多模态内容摄入、混合搜索、知识图谱以及全面的文档管理功能。

R2R 还包含一个 **深度研究 API（Deep Research API）**，这是一个多步推理系统，能够从你的知识库和/或互联网中获取相关数据，为复杂查询提供更丰富、更具上下文感知能力的回答。

# 使用示例 (Usage)

```python
# Basic search
results = client.retrieval.search(query="What is DeepSeek R1?")

# RAG with citations
response = client.retrieval.rag(query="What is DeepSeek R1?")

# Deep Research RAG Agent
response = client.retrieval.agent(
  message={"role":"user", "content": "What does deepseek r1 imply? Think about market, societal implications, and more."},
  rag_generation_config={
    "model": "anthropic/claude-3-7-sonnet-20250219",
    "extended_thinking": True,
    "thinking_budget": 4096,
    "temperature": 1,
    "top_p": None,
    "max_tokens_to_sample": 16000,
  },
)
```



## 快速开始 (Getting Started)
```bash
# Quick install and run in light mode
pip install r2r
export OPENAI_API_KEY=sk-...
python -m r2r.serve

# Or run in full mode with Docker
# git clone git@github.com:SciPhi-AI/R2R.git && cd R2R
# export R2R_CONFIG_NAME=full OPENAI_API_KEY=sk-...
# docker compose -f compose.full.yaml --profile postgres up -d
```

有关详细的自托管说明，请参阅[自托管文档](https://r2r-docs.sciphi.ai/self-hosting/installation/overview)。

## 演示 (Demo)
https://github.com/user-attachments/assets/173f7a1f-7c0b-4055-b667-e2cdcf70128b

## 使用 API (Using the API)

### 1. 安装 SDK 与配置

```bash
# Install SDK
pip install r2r  # Python
# or
npm i r2r-js    # JavaScript
```

### 2. 客户端初始化

```python
from r2r import R2RClient
client = R2RClient(base_url="http://localhost:7272")
```

```javascript
const { r2rClient } = require('r2r-js');
const client = new r2rClient("http://localhost:7272");
```

### 3. 文档操作

```python
# Ingest sample or your own document
client.documents.create(file_path="/path/to/file")

# List documents
client.documents.list()
```


## 核心功能 (Key Features)

- **📁 多模态内容摄入**：支持解析 `.txt`、`.pdf`、`.json`、`.png`、`.mp3` 等多种格式
- **🔍 混合搜索**：结合语义与关键词搜索，采用互反秩融合（Reciprocal Rank Fusion）算法
- **🔗 知识图谱**：自动提取实体及关系
- **🤖 Agent 化 RAG**：检索与推理 Agent 深度集成
- **🔐 用户与权限管理**：完整的身份认证与数据集合（Collection）管理系统

## 社区与贡献指南 (Community & Contributing)

- [加入我们的 Discord](https://discord.gg/p6KqD2kjtB) 获取支持与交流讨论
- 提交[功能请求](https://github.com/SciPhi-AI/R2R/issues/new?assignees=&labels=&projects=&template=feature_request.md&title=)或[问题报告](https://github.com/SciPhi-AI/R2R/issues/new?assignees=&labels=&projects=&template=bug_report.md&title=)
- 欢迎提交 PR，用于新增功能、改进优化或完善文档

### 贡献者 (Our Contributors)
<a href="https://github.com/SciPhi-AI/R2R/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=SciPhi-AI/R2R" />
</a>
<h1 align="center">Databend</h1>
<h3 align="center">面向 AI Agent 的企业级数据仓库</h3>
<p align="center">支持大规模数据分析、向量搜索与全文检索——结合灵活的 Agent 编排机制与安全 Python UDF 沙箱。专为大型企业 AI 工作负载打造。</p>

<div align="center">

<a href="https://databend.com/">☁️ 试用云服务</a> •
<a href="#-quick-start">🚀 快速开始</a> •
<a href="https://docs.databend.com/">📖 文档</a> •
<a href="https://link.databend.com/join-slack">💬 Slack 社区</a>

<br><br>

<a href="https://github.com/databendlabs/databend/actions/workflows/release.yml">
<img src="https://img.shields.io/github/actions/workflow/status/datafuselabs/databend/release.yml?branch=main" alt="CI Status" />
</a>
<img src="https://img.shields.io/badge/Platform-Linux%2C%20macOS%2C%20ARM-green.svg?style=flat" alt="Platform" />

</div>

<br>

<img src="https://github.com/user-attachments/assets/4c288d5c-9365-44f7-8cde-b2c7ebe15622" alt="databend" width="100%" />

## 💡 为什么选择 Databend？

Databend 是一款基于 Rust 构建的开源企业级数据仓库。

**核心能力**：数据分析、向量搜索、全文检索、自动 Schema 演进——全部集成于单一引擎中。

**Agent 就绪（Agent-Ready）**：提供沙箱化 UDF 用于 Agent 逻辑执行，SQL 负责编排，事务保障可靠性，分支功能支持在生产数据上进行安全实验。

| | |
| :--- | :--- |
| **📊 核心引擎**<br>数据分析、向量搜索、全文检索、自动 Schema 演进、事务处理。 | **🤖 Agent 就绪**<br>沙箱 UDF + SQL 编排。在您的企业数据上构建并运行 AI Agent。 |
| **🏢 企业级规模**<br>弹性计算，云原生架构。支持 S3/Azure/GCS 存储。 | **🌿 分支功能**<br>类 Git 的数据版本管理。Agent 可安全地在生产数据快照上运行。 |

![Databend Architecture](https://github.com/user-attachments/assets/288dea8d-0243-4c45-8d18-d4d402b08075)

## ⚡ 快速开始

### 1. 云服务（推荐）
[在 Databend Cloud 上免费试用](https://docs.databend.com/guides/cloud/) —— 60秒即可投入生产环境使用。

### 2. 本地开发（Python）
适用于开发与测试。需要 Python 3.12 或 3.13，以及 `databend-driver` 0.34.0 或更高版本：

```bash
pip install "databend-driver[local]>=0.34.0"
```

```python
from databend_driver import connect

conn = connect("databend+local:///./local-state")
print(conn.query_row("SELECT 'Hello, Databend!'").values())
```

### 3. Docker
在本地运行完整的数据仓库：

```bash
docker run -p 8000:8000 datafuselabs/databend
```

## 🤖 Agent-Ready（Agent 就绪）架构

Databend 的 **沙箱 UDF** 通过三层架构实现灵活的 Agent 编排：

- **控制平面（Control Plane）**：资源调度、权限验证、沙箱生命周期管理
- **执行平面（Execution Plane，Databend）**：SQL 编排，通过 Arrow Flight 发起请求
- **计算平面（Compute Plane，Sandbox Workers）**：隔离的沙箱环境，运行您的 Agent 逻辑

```sql
-- Define your agent logic
CREATE FUNCTION my_agent(input STRING) RETURNS STRING
LANGUAGE python HANDLER = 'run'
AS $$
def run(input):
    # Your agent logic: LLM calls, tool use, reasoning...
    return response
$$;

-- Orchestrate agents with SQL
SELECT my_agent(question) FROM tasks;
```

## 🚀 应用场景

- **AI Agent**：沙箱 UDF + SQL 编排 + 分支功能，实现安全可靠的运行环境
- **数据分析与 BI（商业智能）**：大规模 SQL 分析 —— [了解更多](https://docs.databend.com/guides/query/sql-analytics)
- **搜索与 RAG（检索增强生成）**：向量搜索 + 全文检索 —— [了解更多](https://docs.databend.com/guides/query/vector-db)

## 🤝 社区与支持

- [📖 文档中心](https://docs.databend.com/)
- [💬 加入 Slack](https://link.databend.com/join-slack)
- [🐛 Issue 跟踪器](https://github.com/databendlabs/databend/issues)
- [🗺️ 产品路线图](https://github.com/databendlabs/databend/issues/14167)

**贡献者将永久收录于 `system.contributors` 表中 🏆**

## 📄 许可证

[Apache 2.0](licenses/Apache-2.0.txt) + [Elastic 2.0](licenses/Elastic.txt) | [许可协议常见问题解答（FAQ）](https://docs.databend.com/guides/products/dee/license)

---

<div align="center">
<strong>企业级数据仓库，专为 Agent 就绪</strong><br>
<a href="https://databend.com">🌐 官方网站</a> •
<a href="https://x.com/DatabendLabs">🐦 Twitter</a>
</div>
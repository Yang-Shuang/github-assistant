<p align="center">
    <img height="200" src="docs/images/pgai_logo.png#gh-dark-mode-only" alt="pgai"/>
    <img height="200" src="docs/images/pgai_white.png#gh-light-mode-only" alt="pgai"/>
</p>

<div align=center>

<h3>使用 PostgreSQL 为你的 RAG 与 Agentic（智能体）应用赋能</h3>

<div>
  <a href="https://github.com/timescale/pgai/tree/main/docs"><strong>文档</strong></a> ·
  <a href="https://discord.gg/KRdHVXAmkp"><strong>加入 pgai Discord！</strong></a> ·
  <a href="https://tsdb.co/gh-pgai-signup"><strong>免费试用 Timescale！</strong></a> ·
  <a href="https://github.com/timescale/pgai/releases"><strong>更新日志</strong></a>
</div>
</div>
<br/>

<h1> 截至 2026 年 2 月，本项目已停止维护与支持。 </h1>

一个 Python 库，将 PostgreSQL 转变为用于 RAG 和 Agentic 应用的健壮、生产级检索引擎。

- 🔄 **自动创建并同步向量嵌入（embeddings）**：从 PostgreSQL 数据和 S3 文档中自动生成，数据变更时嵌入也会自动更新。
- 🤖 **[语义目录（Semantic Catalog）](/docs/semantic_catalog/README.md)：通过 AI 实现自然语言转 SQL**。自动生成数据库描述，为 Agentic 应用提供文本到 SQL 的转换能力。 
- 🔍 基于 pgvector 和 pgvectorscale 的强大向量与语义搜索功能。
- 🛡️ 开箱即用的生产级就绪：支持批量处理以高效生成嵌入，内置对模型故障、速率限制和延迟突发的处理机制。
- 🐘 兼容任意 PostgreSQL 数据库，包括 Timescale Cloud、Amazon RDS、Supabase 等。


**基础架构**：
该系统由你编写的应用程序、PostgreSQL 数据库以及无状态的 vectorizer（向量生成器）工作进程组成。应用程序定义 vectorizer 配置，用于将来自 PostgreSQL 或 S3 等源的数据转换为嵌入。工作进程读取该配置，处理数据队列以生成嵌入和分块文本，并将结果写回。随后，应用程序通过查询这些数据来驱动 RAG 和语义搜索。

该架构的核心优势在于其韧性：应用程序进行的数据修改与嵌入过程解耦，确保嵌入服务的故障不会影响核心数据操作。
    
<div align=center>
<img height="400" src="docs/images/pgai_architecture.png" alt="Pgai Architecture: application, database, vectorizer worker">


</div>

### 安装 

首先，安装 pgai 包。

```bash
pip install pgai
```              

接着，安装 pgai 数据库组件。你可以通过终端使用 CLI，或在 Python 应用代码中使用 pgai Python 包来完成此操作。
```
# from the cli
pgai install -d <database-url>

# or from the python package, often done as part of your application setup
import pgai
pgai.install(DB_URL)
```

如果你未使用 Timescale Cloud，还需运行 pgai vectorizer 工作进程。通过以下方式安装其依赖项：
```bash
pip install "pgai[vectorizer-worker]"
```

如果你使用的是 [语义目录（Semantic Catalog）](/docs/semantic_catalog/README.md)，还需运行：

```bash
pip install "pgai[semantic-catalog]"
```


# 快速入门

本快速入门演示了 pgai Vectorizer（向量生成器）如何通过自动创建和同步嵌入，实现基于 PostgreSQL 数据的语义搜索与 RAG。

**寻找文本转 SQL（Text-to-SQL）功能？** 请查看 [语义目录快速入门](/docs/semantic_catalog/README.md)，了解如何将自然语言问题转换为 SQL 查询。

pgai Vectorizer 的关键“秘诀”在于其声明式的嵌入生成方法。只需定义你的管道（pipeline），让 Vectorizer 处理保持嵌入同步的运维复杂性，即使嵌入端点不可靠也能应对自如。你可以按如下方式定义一个简单的管道：

```sql
CREATE TABLE IF NOT EXISTS wiki (
    id INTEGER PRIMARY KEY GENERATED ALWAYS AS IDENTITY,
    url TEXT NOT NULL,
    title TEXT NOT NULL,
    text TEXT NOT NULL
)

SELECT ai.create_vectorizer(
     'wiki'::regclass,
     loading => ai.loading_column(column_name=>'text'),
     destination => ai.destination_table(target_table=>'wiki_embedding_storage'),
     embedding => ai.embedding_openai(model=>'text-embedding-ada-002', dimensions=>'1536')
    )
```

Vectorizer 将自动为 `wiki` 表中的所有行创建嵌入，更重要的是，它会随着底层数据的变更保持嵌入同步。**你可以将其视为在 `wiki` 表上声明了一个索引**，只不过不是数据库为你管理索引数据结构，而是 Vectorizer 负责管理嵌入。 

## 运行快速入门示例

**前置条件：**
- 一个 PostgreSQL 数据库（[Docker 安装指南](https://docs.timescale.com/self-hosted/latest/install/installation-docker/)）。
- 一个 OpenAI API 密钥（快速入门中使用 OpenAI 进行嵌入，但你也可以使用 [多个提供商](#supported-embedding-models)）。

创建包含以下内容的 `.env` 文件：

```
OPENAI_API_KEY=<your-openai-api-key>
DB_URL=<your-database-url>
```

你可以从快速入门示例中下载完整的 [Python 代码](examples/quickstart/main.py) 和 [requirements.txt](examples/quickstart/requirements.txt)，并在与 `.env` 文件相同的目录下运行它。

<details>
<summary>点击此处查看用于运行快速入门的 Bash 脚本</summary>

```bash
curl -O https://raw.githubusercontent.com/timescale/pgai/main/examples/quickstart/main.py
curl -O https://raw.githubusercontent.com/timescale/pgai/main/examples/quickstart/requirements.txt
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
python main.py
```
</details>
示例输出：

<details>
<summary>点击查看示例输出</summary>

```
Search results 1:
[WikiSearchResult(id=7,
                  url='https://en.wikipedia.org/wiki/Aristotle',
                  title='Aristotle',
                  text='Aristotle (;  Aristotélēs, ; 384–322\xa0BC) was an '
                       'Ancient Greek philosopher and polymath. His writings '
                       'cover a broad range of subjects spanning the natural '
                       'sciences, philosophy, linguistics, economics, '
                       'politics, psychology and the arts. As the founder of '
                       'the Peripatetic school of philosophy in the Lyceum in '
                       'Athens, he began the wider Aristotelian tradition that '
                       'followed, which set the groundwork for the development '
                       'of modern science.\n'
                       '\n'
                       "Little is known about Aristotle's life. He was born in "
                       'the city of Stagira in northern Greece during the '
                       'Classical period. His father, Nicomachus, died when '
                       'Aristotle was a child, and he was brought up by a '
                       "guardian. At 17 or 18 he joined Plato's Academy in "
                       'Athens and remained there till the age of 37 (). '
                       'Shortly after Plato died, Aristotle left Athens and, '
                       'at the request of Philip II of Macedon, tutored his '
                       'son Alexander the Great beginning in 343 BC. He '
                       'established a library in the Lyceum which helped him '
                       'to produce many of his hundreds of books on papyru',
                  chunk='Aristotle (;  Aristotélēs, ; 384–322\xa0BC) was an '
                        'Ancient Greek philosopher and polymath. His writings '
                        'cover a broad range of subjects spanning the natural '
                        'sciences, philosophy, linguistics, economics, '
                        'politics, psychology and the arts. As the founder of '
                        'the Peripatetic school of philosophy in the Lyceum in '
                        'Athens, he began the wider Aristotelian tradition '
                        'that followed, which set the groundwork for the '
                        'development of modern science.',
                  distance=0.22242502364217387)]
Search results 2:
[WikiSearchResult(id=41,
                  url='https://en.wikipedia.org/wiki/pgai',
                  title='pgai',
                  text='pgai is a Python library that turns PostgreSQL into '
                       'the retrieval engine behind robust, production-ready '
                       'RAG and Agentic applications. It does this by '
                       'automatically creating vector embeddings for your data '
                       'based on the vectorizer you define.',
                  chunk='pgai is a Python library that turns PostgreSQL into '
                        'the retrieval engine behind robust, production-ready '
                        'RAG and Agentic applications. It does this by '
                        'automatically creating vector embeddings for your '
                        'data based on the vectorizer you define.',
                  distance=0.13639101792546204)]
RAG response:
The main thing pgai does right now is generating vector embeddings for data in PostgreSQL databases based on the vectorizer defined by the user, enabling the creation of robust RAG and Agentic applications.
```
</details>


## 代码详解

### 安装 pgai 数据库组件

pgai 需要在数据库中安装一些目录表和函数。这通过 `pgai.install` 函数完成，它会将必要的组件安装到数据库的 `ai` 模式中。

```python
pgai.install(DB_URL)
```

### 创建 Vectorizer（向量生成器）

此步骤定义 Vectorizer，告知系统如何从 `wiki` 表的 `text` 列创建嵌入。Vectorizer 会创建一个名为 `wiki_embedding` 的视图，供我们后续查询嵌入数据（如下文所示）。

```python
async def create_vectorizer(conn: psycopg.AsyncConnection):
    async with conn.cursor() as cur:    
        await cur.execute("""
            SELECT ai.create_vectorizer(
                'wiki'::regclass,
                if_not_exists => true,
                loading => ai.loading_column(column_name=>'text'),
                embedding => ai.embedding_openai(model=>'text-embedding-ada-002', dimensions=>'1536'),
                destination => ai.destination_table(view_name=>'wiki_embedding')
            )
        """)   
    await conn.commit()
```

### 运行 Vectorizer 工作进程


在本示例中，我们仅运行一次 Vectorizer 工作进程以创建现有数据的嵌入。

```python
worker = Worker(DB_URL, once=True)
worker.run()
```

在实际应用中，我们不会每次需要生成嵌入时都手动调用工作进程。相反，我们会让它在后台持续运行，轮询 Vectorizer 获取任务。 

你可以在应用中、通过 CLI 或使用 Docker 在后台运行该工作进程。更多详情请参阅 [Vectorizer 工作进程文档](/docs/vectorizer/worker.md)。


### 使用语义搜索检索 Wiki 文章

这是 PostgreSQL 中标准的 pgvector 语义搜索。查询针对由 Vectorizer 创建的 `wiki_embedding` 视图执行，该视图包含 `wiki` 表的所有列以及 `embedding` 列和分块文本。此函数同时返回 `wiki` 表的完整 `text` 列以及与查询最相关的较小文本片段。


```python
@dataclass
class WikiSearchResult:
    id: int
    url: str
    title: str
    text: str
    chunk: str
    distance: float

async def _find_relevant_chunks(client: AsyncOpenAI, query: str, limit: int = 1) -> List[WikiSearchResult]:
    # Generate embedding for the query using OpenAI's API
    response = await client.embeddings.create(
        model="text-embedding-ada-002",
        input=query,
        encoding_format="float",
    )
    
    embedding = np.array(response.data[0].embedding)
    
    # Query the database for the most similar chunks using pgvector's cosine distance operator (<=>)
    async with pool.connection() as conn:
        async with conn.cursor(row_factory=class_row(WikiSearchResult)) as cur:
            await cur.execute("""
                SELECT w.id, w.url, w.title, w.text, w.chunk, w.embedding <=> %s as distance
                FROM wiki_embedding w
                ORDER BY distance
                LIMIT %s
            """, (embedding, limit))
            
            return await cur.fetchall()
```

### 向 Wiki 表插入新文章

这段代码的亮点在于它**没有做**什么。这只是一个向 `wiki` 表插入新文章的简单操作。我们无需为生成嵌入做任何额外处理，Vectorizer 工作进程会自动随着数据变更更新嵌入。

```python
def insert_article_about_pgai(conn: psycopg.AsyncConnection):
    async with conn.cursor(row_factory=class_row(WikiSearchResult)) as cur:
        await cur.execute("""
            INSERT INTO wiki (url, title, text) VALUES
            ('https://en.wikipedia.org/wiki/pgai', 'pgai', 'pgai is a Python library that turns PostgreSQL into the retrieval engine behind robust, production-ready RAG and Agentic applications. It does this by automatically creating vector embeddings for your data based on the vectorizer you define.')
        """)
    await conn.commit() 
```

### 使用大语言模型（LLM）执行 RAG

此代码利用 LLM 执行 RAG。它使用上文定义的 `_find_relevant_chunks` 函数从 `wiki` 表中查找最相关的文本片段，然后调用 LLM 生成回复。

```python
    query = "What is the main thing pgai does right now?"
    relevant_chunks = await _find_relevant_chunks(client, query)
    context = "\n\n".join(
        f"{chunk.title}:\n{chunk.text}" 
        for chunk in relevant_chunks
    )
    prompt = f"""Question: {query}

Please use the following context to provide an accurate response:   

{context}

Answer:"""

    response = await client.chat.completions.create({
        model: "gpt-4o-mini",
        messages: [{ role: "user", content: prompt }],
    })
    print("RAG response:")
    print(response.choices[0].message.content)
```

## 后续步骤


### 更多 RAG 与向量化示例  
- [FastAPI + psycopg 快速入门](/examples/simple_fastapi_app/README.md)
- [Vectorizer 概述](/docs/vectorizer/overview.md) 与 [工作进程文档](/docs/vectorizer/worker.md)
- [Vectorizer API 参考](/docs/vectorizer/api-reference.md)

### 基于语义目录的文本转 SQL（Text-to-SQL）
- **[语义目录快速入门](/docs/semantic_catalog/README.md)**：了解如何使用语义目录将自然语言转换为 Agentic 应用的 SQL。


# 功能特性 

我们的 pgai Python 库让你能够直接使用由数据生成的嵌入：

* 使用 [Vectorizer（向量生成器）](/docs/vectorizer/overview.md) 自动创建并同步数据的向量嵌入。
* [加载数据](/docs/vectorizer/api-reference.md#loading-configuration)：支持从表的列、文件、S3 存储桶等来源读取。
* 为同一数据使用不同模型和参数创建多个嵌入，便于测试与实验。
* [自定义](#a-configurable-vectorizer-pipeline) 你的嵌入管道如何解析、分块、格式化并生成数据嵌入。

你可以使用向量嵌入来：
- 使用 pgvector [执行语义搜索](/docs/vectorizer/overview.md#query-an-embedding)。
- 实现检索增强生成（Retrieval Augmented Generation, RAG）
- 使用与 pgvector 互补的 [pgvectorscale](https://github.com/timescale/pgvectorscale)，在大规模向量负载下执行高性能、低成本的 ANN（近似最近邻）搜索。


**基于语义目录的文本转 SQL（Text-to-SQL）**：将自然语言转换为精准的 SQL 查询。语义目录会自动生成数据库描述，支持人工审核与优化这些描述，并存储 SQL 示例和业务事实。这使得 LLM 能够理解你的数据模式和上下文。更多详情请见 [语义目录文档](/docs/semantic_catalog/README.md)。

我们还提供了一个 [PostgreSQL 扩展](/projects/extension/README.md)，支持直接从 SQL 调用大语言模型。这对于分类、摘要和数据增强等现有数据处理场景非常有用。

## 可配置的 Vectorizer 管道

Vectorizer 旨在具备灵活性与可定制性。每个 Vectorizer 定义了一个从数据生成嵌入的管道（pipeline）。该管道由一系列按顺序应用于数据的组件组成：

- **[加载（Loading）](/docs/vectorizer/api-reference.md#loading-configuration)**：首先定义要嵌入的数据源。可以是直接存储在源表列中的数据，也可以是源表列中引用的指向文件、S3 存储桶等的 URI。
- **[解析（Parsing）](/docs/vectorizer/api-reference.md#parsing-configuration)**：如果数据是非文本文档（如 PDF、HTML 或 Markdown 文件），则定义其解析方式。
- **[分块（Chunking）](/docs/vectorizer/api-reference.md#chunking-configuration)**：接着定义文本数据如何被分割成块。
- **[格式化（Formatting）](/docs/vectorizer/api-reference.md#formatting-configuration)**：然后，为每个数据块定义发送前进行嵌入的格式。例如，你可以将文档标题作为该数据块的第一行添加进去。
- **[生成嵌入（Embedding）](/docs/vectorizer/api-reference.md#embedding-configuration)**：最后，指定用于生成嵌入的大语言模型提供商、模型及参数。

## 支持的嵌入模型

以下模型支持用于生成嵌入：

- [Ollama](/docs/vectorizer/api-reference.md#aiembedding_ollama)
- [OpenAI](/docs/vectorizer/api-reference.md#aiembedding_openai)
- [Voyage AI](/docs/vectorizer/api-reference.md#aiembedding_voyageai)
- [Cohere](/docs/vectorizer/api-reference.md#aiembedding_litellm)
- [Huggingface](/docs/vectorizer/api-reference.md#aiembedding_litellm)
- [Mistral](/docs/vectorizer/api-reference.md#aiembedding_litellm)
- [Azure OpenAI](/docs/vectorizer/api-reference.md#aiembedding_litellm)
- [AWS Bedrock](/docs/vectorizer/api-reference.md#aiembedding_litellm)
- [Vertex AI](/docs/vectorizer/api-reference.md#aiembedding_litellm)

## 关键在于错误处理

仅仅创建向量嵌入是简单直接的。真正的挑战在于大语言模型（LLM）有时不太稳定，且端点会出现间歇性故障或性能下降。正确处理故障的关键在于：你的核心数据修改操作（INSERT、UPDATE、DELETE）不应依赖于嵌入操作。否则，一旦端点变慢或失败，你的应用就会中断，用户体验将大打折扣。

通常，你需要实现自定义的 MLOps 管道来妥善处理端点故障。这通常涉及 Kafka 等消息队列系统、专用工作进程以及其他用于处理队列和重试失败请求的基础设施。这是一项繁重且容易出错的工作。

使用 pgai，你可以跳过所有这些繁琐工作并专注于构建应用，因为 Vectorizer 会替你管理嵌入。我们内置了队列和重试逻辑来处理你可能遇到的各种故障模式。由于这些工作在后台执行，核心数据修改操作不依赖于嵌入操作。这也是为什么 pgai 开箱即用且具备生产级就绪能力的原因。

许多专用向量数据库会为你生成嵌入。然而，当嵌入端点宕机或性能下降时，它们通常会失败，并将错误处理和重试的负担重新推回给你。

 
# 资源链接
## 设计初衷
- [Vector Databases Are the Wrong Abstraction](https://www.timescale.com/blog/vector-databases-are-the-wrong-abstraction/)
- [pgai: Giving PostgreSQL Developers AI Engineering Superpowers](http://www.timescale.com/blog/pgai-giving-postgresql-developers-ai-engineering-superpowers)

## 快速入门指南
- [语义目录（文本转 SQL）](/docs/semantic_catalog/README.md)：了解如何使用语义目录提升 Agentic 应用的自然语言到 SQL 转换效果。
- [上方的 Vectorizer 快速入门](#quick-start)
- [OpenAI 快速入门](/docs/vectorizer/quick-start-openai.md)
- [VoyageAI 快速入门](/docs/vectorizer/quick-start-voyage.md)

## pgai Vectorizer 教程
- [如何在 PostgreSQL 中通过一条 SQL 查询自动创建和更新嵌入](https://www.timescale.com/blog/how-to-automatically-create-update-embeddings-in-postgresql/)
- [视频] [一行 SQL 实现向量嵌入的自动生成与同步](https://www.youtube.com/watch?v=ZoC2XYol6Zk)
- [哪种 OpenAI 嵌入模型最适合你的 Pgvector RAG 应用？](https://www.timescale.com/blog/which-openai-embedding-model-is-best/)
- [哪种 RAG 分块与格式化策略最适合你的 Pgvector 应用？](https://www.timescale.com/blog/which-rag-chunking-and-formatting-strategy-is-best/)
- [使用开源工具解析所有数据：Unstructured 和 Pgai](https://www.timescale.com/blog/parsing-all-the-data-with-open-source-tools-unstructured-and-pgai/)


## 贡献指南
我们欢迎对 pgai 做出贡献！更多信息请参阅[贡献指南](/CONTRIBUTING.md)。


## 参与社区

pgai 仍处于早期阶段。现在是帮助塑造项目方向的绝佳时机；我们目前正在确定优先级。请查看我们正在规划的功能[列表](https://github.com/timescale/pgai/issues)。欢迎随时评论、补充功能列表，或加入讨论区交流。

要开始参与，请查阅[如何贡献](./CONTRIBUTING.md)以及[如何搭建开发/测试环境](./DEVELOPMENT.md)。

## 关于 Timescale 

Timescale 是一家 PostgreSQL 数据库公司。了解更多请访问 [timescale.com](https://www.timescale.com)。

Timescale Cloud 是一款高性能、面向开发者、云原生的平台，为最具挑战性的 AI、时间序列、分析和事件处理负载提供 PostgreSQL 服务。Timescale Cloud 非常适合生产级应用，并提供高可用性、流式备份、平滑升级、角色与权限管理以及卓越的安全保障。

[pgai-plpython]: https://github.com/postgres-ai/postgres-howtos/blob/main/0047_how_to_install_postgres_16_with_plpython3u.md
[asdf-postgres]: https://github.com/smashedtoatoms/asdf-postgres
[asdf]: https://github.com/asdf-vm/asdf
[python3]: https://www.python.org/downloads/
[pip]: https://pip.pypa.io/en/stable/installation/#supported-methods
[plpython3u]: https://www.postgresql.org/docs/current/plpython.html
[pgvector]: https://github.com/pgvector/pgvector
[pgvector-install]: https://github.com/pgvector/pgvector?tab=readme-ov-file#installation
[python-virtual-environment]: https://packaging.python.org/en/latest/tutorials/installing-packages/#creating-and-using-virtual-environments
[create-a-new-service]: https://console.cloud.timescale.com/dashboard/create_services
[just]: https://github.com/casey/just
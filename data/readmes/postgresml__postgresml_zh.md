<div align="center">
   <picture>
     <source media="(prefers-color-scheme: dark)" srcset="https://github.com/user-attachments/assets/5d5510da-6014-4cf3-849f-566050e053da">
     <source media="(prefers-color-scheme: light)" srcset="https://github.com/user-attachments/assets/aea1c38a-15bf-4270-8365-3d5e6311f5fc">
     <img alt="Logo" src="" width="520">
   </picture>
</div>

<p align="center">
   <p align="center"><b>用于机器学习（ML）/人工智能（AI）应用的 Postgres + GPU。</b></p>
</p>

<p align="center">
| <a href="https://postgresml.org/docs/"><b>文档</b></a> | <a href="https://postgresml.org/blog"><b>博客</b></a> | <a href="https://discord.gg/DmyJP3qJ7U"><b>Discord 社区</b></a> |
|---|---|---|
</p>

---
**为什么要在 Postgres 中进行机器学习（ML）和人工智能（AI）？**

ML 与 AI 系统的数据天然比模型更大、更动态。将模型移至数据库，而不是不断将数据移向模型，在效率、可管理性和可靠性上都更高。</b></p>
</p>

- [快速入门](#getting-started)
    - [PostgresML 云托管服务](#postgresml-cloud)
    - [自行部署](#self-hosted)
    - [生态系统](#ecosystem)
- [大语言模型（LLM）](#large-language-models)
    - [Hugging Face 集成](#hugging-face)
    - [OpenAI 及其他提供商](#openai)
- [检索增强生成（RAG）](#rag)
    - [分块（Chunk）](#chunk)
    - [向量化/嵌入（Embed）](#embed)
    - [排序（Rank）](#rank)
    - [转换/生成（Transform）](#transform)
- [机器学习](#machine-learning)

## 架构设计

<div align="center">
   <picture>
     <source media="(prefers-color-scheme: dark)" srcset="https://github.com/user-attachments/assets/e27f8bda-1fe6-49f8-b9d8-ef563e0150e5">
     <source media="(prefers-color-scheme: light)" srcset="https://github.com/user-attachments/assets/09bbed94-b73f-447b-95d9-2d4a7727c3aa">
     <img alt="Logo" src="" width="784">
   </picture>
</div>

<div align="center">
<b>PostgresML 是一个强大的 PostgreSQL 扩展，在数据库内无缝整合了数据存储与机器学习推理功能。</b>通过集成这些功能，PostgresML 消除了对独立系统和数据迁移的需求，让你能够直接在数据所在处执行 ML/AI 操作。
</div>

## 核心特性一览

- **数据库内 ML/AI**：直接在 PostgreSQL 中运行机器学习和人工智能操作
- **GPU 加速**：利用 GPU 算力实现更快的计算和模型推理
- **大语言模型（LLM）**：集成并使用来自 Hugging Face 的最新 LLM
- **RAG 管道**：内置用于文本分块、向量化、排序和转换的函数
- **向量搜索**：通过集成 `pgvector` 实现高效的相似度搜索
- **丰富的机器学习算法**：提供 47 种以上的分类与回归算法
- **高性能**：推理速度比基于 HTTP 的模型服务快 8 到 40 倍
- **高可扩展性**：支持每秒数百万次事务处理及水平扩展
- **自然语言处理（NLP）任务**：提供广泛的语言处理能力
- **安全性**：模型与数据共存，增强数据隐私保护
- **无缝集成**：兼容现有 PostgreSQL 工具及客户端库

# 快速入门

使用 PostgresML 的唯一前提条件是拥有一个已安装我们开源 `pgml` 扩展的 PostgreSQL 数据库。

## PostgresML 云托管服务

我们的无服务器云服务是最简单且推荐的入门方式。

[注册免费的 PostgresML 账户](https://postgresml.org/signup)。你将在几秒内获得一个免费数据库，并可访问 GPU 及前沿的 LLM。

## 自行部署

如果你不想使用我们的云服务，可以选择自行部署。

```
docker run \
    -it \
    -v postgresml_data:/var/lib/postgresql \
    -p 5433:5432 \
    -p 8000:8000 \
    ghcr.io/postgresml/postgresml:2.10.0 \
    sudo -u postgresml psql -d postgresml
```

更多详情，请参阅我们的 [Docker 快速入门](https://postgresml.org/docs/open-source/pgml/developers/quick-start-with-docker) 文档。

## 生态系统

我们还有许多专为与 PostgresML 协同工作而设计的工具和库。请记住，PostgresML 是一个运行在 PostgreSQL 内部的扩展，因此你可以使用 `psql` 连接，并使用你喜爱的任何工具及客户端库（如 [psycopg](https://www.psycopg.org/psycopg3/)）来连接并执行查询。

<b>PostgresML 专用客户端库：</b>
- [Korvus](https://github.com/postgresml/korvus) - Korvus 是一款支持 Python、JavaScript、Rust 和 C 的搜索 SDK，能在单次数据库查询中统一整个 RAG 管道。
- [postgresml-django](https://github.com/postgresml/postgresml-django) - postgresml-django 是一款将 PostgresML 与 Django ORM 集成的 Python 模块。

<b>推荐的 PostgreSQL 连接池：</b>
- [pgcat](https://github.com/postgresml/pgcat) - pgcat 是一款支持分片、负载均衡和故障转移的 PostgreSQL 连接池工具。

# 大语言模型（LLM）

PostgresML 将模型直接带到你的数据处，消除了昂贵且耗时的数据传输需求。这种方法显著提升了 AI 驱动应用的性能、安全性和可扩展性。

通过在数据库内运行模型，PostgresML 实现了：

- 降低延迟并提升查询性能
- 增强数据隐私与安全
- 简化基础设施管理
- 与现有数据库操作无缝集成

## Hugging Face 集成

PostgresML 支持在 Hugging Face [模型库](https://huggingface.co/models)中提供的多种前沿深度学习架构。此集成让你能够：

- 访问数千个预训练模型
- 利用尖端 NLP、计算机视觉及其他 AI 模型
- 轻松尝试不同的架构

## OpenAI 及其他提供商

尽管基于云的 LLM 提供商提供了强大的功能，但从数据库内部发起 API 调用可能会引入延迟、安全风险及潜在的合规问题。目前，PostgresML 不直接支持与 OpenAI 等远程 LLM 提供商的集成。

# 检索增强生成（RAG）

PostgresML 将你的 PostgreSQL 数据库转变为用于检索增强生成（RAG）应用的强大向量数据库。它利用 `pgvector` 实现嵌入的高效存储与检索。

我们的 RAG 实现基于四个核心 SQL 函数：

1. [分块（Chunk）](#chunk)：将文本拆分为可管理的片段
2. [向量化/嵌入（Embed）](#embed)：使用预训练模型从文本生成向量嵌入
3. [排序（Rank）](#rank)：在嵌入上执行相似度搜索
4. [转换/生成（Transform）](#transform)：应用语言模型进行文本生成或转换

有关在 PostgresML 中使用 RAG 的更多信息，请参阅我们的 [统一 RAG](https://postgresml.org/docs/open-source/pgml/guides/unified-rag) 指南。

## 分块（Chunk）

`pgml.chunk` 函数使用指定的分块器对文档进行切分。这通常在向量化之前执行。

```postgresql
pgml.chunk(
    splitter TEXT,    -- splitter name
    text TEXT,        -- text to embed
    kwargs JSON       -- optional arguments (see below)
)
```

详见 [pgml.chunk 文档](https://postgresml.org/docs/open-source/pgml/api/pgml.chunk)。

## 向量化/嵌入（Embed）

`pgml.embed` 函数使用数据库内模型从文本生成嵌入。

```postgresql
pgml.embed(
    transformer TEXT,
    "text" TEXT,
    kwargs JSONB
)
```
详见 [pgml.embed 文档](https://postgresml.org/docs/open-source/pgml/api/pgml.embed)。

## 排序（Rank）

`pgml.rank` 函数使用交叉编码器（Cross-Encoders）对句子对进行评分。

这通常在搜索时用作重排序步骤。

```postgresl
pgml.rank(
    transformer TEXT,
    query TEXT,
    documents TEXT[],
    kwargs JSONB
)
```

文档即将发布。

## 转换/生成（Transform）

`pgml.transform` 函数可用于生成文本。

```postgresql
SELECT pgml.transform(
    task   => TEXT OR JSONB,     -- Pipeline initializer arguments
    inputs => TEXT[] OR BYTEA[], -- inputs for inference
    args   => JSONB              -- (optional) arguments to the pipeline.
)
```

详见 [pgml.transform 文档](https://postgresml.org/docs/open-source/pgml/api/pgml.transform)。

请参阅我们的 [文本生成指南](https://postgresml.org/docs/open-source/pgml/guides/llms/text-generation) 了解如何生成文本。

# 机器学习

<b>核心亮点：</b>
- [47 种以上的分类与回归算法](https://postgresml.org/docs/open-source/pgml/api/pgml.train)
- [推理速度比基于 HTTP 的模型服务快 8 到 40 倍](https://postgresml.org/blog/postgresml-is-8x-faster-than-python-http-microservices)
- [每秒处理数百万次事务](https://postgresml.org/blog/scaling-postgresml-to-one-million-requests-per-second)
- [水平可扩展性](https://postgresml.org/docs/open-source/pgcat/)

**训练分类模型**

*训练*
```postgresql
SELECT * FROM pgml.train(
    'Handwritten Digit Image Classifier',
    algorithm => 'xgboost',
    'classification',
    'pgml.digits',
    'target'
);
```

*推理*
```postgresql
SELECT pgml.predict(
    'My Classification Project',
    ARRAY[0.1, 2.0, 5.0]
) AS prediction;
```

## NLP（自然语言处理）

`pgml.transform` 函数暴露了多种可用的 NLP 任务。

可用任务包括：
- [文本分类](https://postgresml.org/docs/open-source/pgml/guides/llms/text-classification)
- [零样本分类](https://postgresml.org/docs/open-source/pgml/guides/llms/zero-shot-classification)
- [词元分类](https://postgresml.org/docs/open-source/pgml/guides/llms/token-classification)
- [翻译](https://postgresml.org/docs/open-source/pgml/guides/llms/translation)
- [摘要生成](https://postgresml.org/docs/open-source/pgml/guides/llms/summarization)
- [问答](https://postgresml.org/docs/open-source/pgml/guides/llms/question-answering)
- [文本生成](https://postgresml.org/docs/open-source/pgml/guides/llms/text-generation)
- [文到文生成](https://postgresml.org/docs/open-source/pgml/guides/llms/text-to-text-generation)
- [掩码填充](https://postgresml.org/docs/open-source/pgml/guides/llms/fill-mask)
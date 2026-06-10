# PaperQA2

<!-- pyml disable-num-lines 6 line-length -->

[![GitHub](https://img.shields.io/badge/GitHub-black?logo=github&logoColor=white)](https://github.com/Future-House/paper-qa)
[![PyPI version](https://badge.fury.io/py/paper-qa.svg)](https://badge.fury.io/py/paper-qa)
[![tests](https://github.com/Future-House/paper-qa/actions/workflows/tests.yml/badge.svg)](https://github.com/Future-House/paper-qa)
![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)
![PyPI Python Versions](https://img.shields.io/pypi/pyversions/paper-qa)

PaperQA2 是一个用于对 PDF、文本文件、Microsoft Office 文档和源代码文件进行高精度检索增强生成（RAG）的包，重点面向科学文献领域。请参阅我们 [最近的 2024 年论文](https://paper.wikicrow.ai)，查看 PaperQA2 在问答、摘要生成和矛盾检测等科学任务中超越人类表现的表现示例。

<!--TOC-->

---

**目录**

- [快速入门](#quickstart)
  - [输出示例](#example-output)
- [什么是 PaperQA2](#what-is-paperqa2)
  - [PaperQA2 vs PaperQA](#paperqa2-vs-paperqa)
  - [PaperQA2 于 2025 年 12 月采用日历版本控制](#paperqa2-goes-calver-in-december-2025)
  - [第 5 版（即 PaperQA2）的新特性](#whats-new-in-version-5-aka-paperqa2)
  - [2025 年 12 月更新内容](#whats-new-in-december-2025)
  - [PaperQA2 算法](#paperqa2-algorithm)
- [安装](#installation)
- [CLI 使用](#cli-usage)
  - [内置配置](#bundled-settings)
  - [速率限制](#rate-limits)
- [库（Library）使用](#library-usage)
  - [智能体添加/查询文档](#agentic-addingquerying-documents)
  - [手动（无智能体）添加/查询文档](#manual-no-agent-addingquerying-documents)
  - [异步操作](#async)
  - [选择模型](#choosing-model)
    - [本地托管](#locally-hosted)
  - [嵌入模型](#embedding-model)
    - [指定嵌入模型](#specifying-the-embedding-model)
    - [本地嵌入模型（Sentence Transformers）](#local-embedding-models-sentence-transformers)
  - [调整来源数量](#adjusting-number-of-sources)
  - [使用代码或 HTML](#using-code-or-html)
  - [多模态支持](#multimodal-support)
  - [使用外部数据库/向量数据库及缓存](#using-external-dbvector-db-and-caching)
  - [创建索引](#creating-index)
    - [清单文件（Manifest Files）](#manifest-files)
  - [复用索引](#reusing-index)
  - [直接使用客户端](#using-clients-directly)
- [配置速查表](#settings-cheatsheet)
- [如何获取论文？](#where-do-i-get-papers)
- [回调（Callbacks）](#callbacks)
  - [缓存嵌入向量](#caching-embeddings)
- [自定义提示词（Prompts）](#customizing-prompts)
  - [前置与后置提示词](#pre-and-post-prompts)
- [常见问题解答](#faq)
  - [为什么我的结果与论文中的不同？](#how-come-i-get-different-results-than-your-papers)
  - [这与 LlamaIndex 或 LangChain 有何区别？](#how-is-this-different-from-llamaindex-or-langchain)
  - [我可以保存或加载吗？](#can-i-save-or-load)
- [复现（Reproduction）](#reproduction)
- [引用（Citation）](#citation)

---

<!--TOC-->

## 快速入门

在本示例中，我们获取一个包含研究论文 PDF 的文件夹，自动提取其元数据（包括带有撤稿检查的引用计数），然后将 PDF 解析并缓存为全文搜索索引，最后由大语言模型（LLM）智能体回答用户问题。

```bash
pip install paper-qa
mkdir my_papers
curl -o my_papers/PaperQA2.pdf https://arxiv.org/pdf/2409.13740
cd my_papers
pqa ask 'What is PaperQA2?'
```

### 输出示例

问：是否有人设计过使用蛋白质或 DNA 进行计算的神经网络？

> 多个来源支持“已设计出用于计算 DNA 的神经网络”这一说法。
> Qian、Winfree 和 Bruck 的研究展示了利用 DNA 链置换级联反应构建神经网络组件（如人工神经元和联想记忆）的方法，并使用基于 DNA 的系统实现了这些组件（Qian2011Neural pages 1-2, Qian2011Neural pages 15-16, Qian2011Neural pages 54-56）。
> 该研究包括实现了一个 3 位 XOR 门和一个四神经元 Hopfield 联想记忆，展示了 DNA 在神经网络计算中的潜力。
> 此外，将深度学习技术应用于基因组学（涉及使用 DNA 序列进行计算）的研究也已得到充分记录。
> 已有研究应用卷积神经网络（CNNs）来预测转录因子结合和 DNA 可及性等基因组特征（Eraslan2019Deep pages 4-5, Eraslon2019Deep pages 5-6）。
> 这些模型以 DNA 序列作为输入数据，有效地利用神经网络进行 DNA 计算。
> 虽然提供的摘录未明确提及基于蛋白质的神经网络计算，但它们强调了神经网络在蛋白质序列相关任务中的应用，例如预测 DNA-蛋白质结合（Zeng2016Convolutional pages 1-2）。
> 然而，主要重点仍在于基于 DNA 的计算。

## 什么是 PaperQA2

PaperQA2 专为处理科学论文的最优智能体 RAG 模型而设计。其主要特性包括：

- 提供简洁的接口，获取带有文中引用的可靠答案。
- 采用最先进的实现方式，在嵌入向量和 LLM 重排序及上下文摘要（RCS）中融入文档元数据感知能力。
- 支持智能体 RAG，语言智能体可迭代优化查询与答案。
- 自动从多个提供商获取论文元数据的冗余请求，包括引用和期刊质量数据。
- 提供可用的本地 PDF/文本文件仓库全文搜索引擎。
- 提供健壮的自定义接口，默认支持所有 [LiteLLM][LiteLLM providers] 模型。

[LiteLLM providers]: https://docs.litellm.ai/docs/providers
[LiteLLM general docs]: https://docs.litellm.ai/docs/

默认情况下，它使用 [OpenAI embeddings](https://platform.openai.com/docs/guides/embeddings) 和 [models](https://platform.openai.com/docs/models)，配合 Numpy 向量数据库进行文档嵌入与搜索。不过，你也可以轻松切换其他闭源、开源模型或嵌入方式（详见下文）。

PaperQA2 依赖一些优秀的库/API，使我们的仓库得以实现。按任意顺序排列如下：

1. [Semantic Scholar](https://www.semanticscholar.org/)
2. [Crossref](https://www.crossref.org/)
3. [Unpaywall](https://unpaywall.org/)
4. [Pydantic](https://docs.pydantic.dev/latest/)
5. [tantivy](https://github.com/quickwit-oss/tantivy)
6. [LiteLLM][LiteLLM general docs]
7. [pybtex](https://pybtex.org/)

### PaperQA2 vs PaperQA

我们一直在进行底层架构升级，并主要遵循 [SemVer（语义化版本控制）](https://semver.org/) 规范，直到 [2025 年 12 月](#paperqa2-goes-calver-in-december-2025)。这意味着我们在每次破坏性更新时都会递增主版本号。这也使当前的主版本号达到了 v5。那么为什么现在仓库改名为 PaperQA2？
我们想强调，我们在 [许多重要指标](https://paper.wikicrow.ai) 上已经超越了人类表现。因此，我们任意将第 5 版及之后的版本称为 PaperQA2，之前的版本称为 PaperQA1，以表明性能发生了显著变化。我们知道 FutureHouse 在命名和计数方面存在挑战，所以我们保留随时将其名称任意更改为 PaperCrow 的权利。

### PaperQA2 于 2025 年 12 月采用日历版本控制

2025 年 12 月之前，我们使用 [语义化版本控制](https://semver.org/)。这最终导致了两种混淆：

1. **开发者困惑**：我们应该基于配置项还是底层系统能力来执行主版本号递增？如果 bug 修复需要破坏智能体行为怎么办？
2. **交流术语混乱**：应该使用我们出版物中的术语（例如 [PaperQA1](https://arxiv.org/abs/2312.07559)、[PaperQA2](https://arxiv.org/abs/2409.13740)）还是本仓库/包的 Git 标签（如 v5）？当有人说“PaperQA”时，他们指的是哪个版本？

为解决这些混淆，我们在 2025 年 12 月转向了 [日历版本控制](https://calver.org/)。由于 CalVer 与日期绑定且属于 [ZeroVer](https://0ver.org/) 范畴，我们基本取消了跨版本的向后兼容性保证，从而减轻了开发者的维护负担。它解决了“交流术语”问题，因为 Git 标签现在与出版物术语截然不同（例如 PaperQA2 vs `v2025.12.17`）。当有人说“PaperQA”时，仅指代该系统本身，而非特定版本的智能体行为快照。当有人说“PaperQA2”时，将指代 `paper-qa>=5`，这同时适用于 SemVer 标签 `v5.0.0` 和新的 CalVer 标签 `v2025.12.17`。

此次切换对第 5 版的 SemVer 向后兼容，因为年份 2025 严格大于主版本号 5。

### 第 5 版（即 PaperQA2）的新特性

第 5 版新增：

- CLI `pqa`
- 智能体工作流，调用工具进行论文搜索、证据收集和答案生成
- 从 `Docs` 对象中移除了大量状态管理逻辑
- 迁移至 LiteLLM，以兼容多种 LLM 提供商，并集中管理速率限制与成本追踪
- 内置一组已知良好的超参数配置（详见 [此处](#bundled-settings)）

注意：从早期 `PaperQA` 版本 pickle 序列化保存的 `Docs` 对象与第 5 版不兼容，需要重新构建。此外，我们的最低 Python 版本已提升至 Python 3.11。

### 2025 年 12 月更新内容

自 `5.29.1` 版本以来的四个月里，我们进行了大量更新：

- **新模态支持**：表格、图片、非英语语言、数学公式
- **更多且更优的解析器**
  - 两种新的 _基于模型的_ PDF 解析器：[Docling](packages/paper-qa-docling) 和 [Nvidia nemotron-parse](packages/paper-qa-nemotron)
  - 所有 PDF 解析器现在均可解析图片和表格、报告页码，并支持 DPI 设置
  - 新增 Microsoft Office 数据类型解析器
- **多模态上下文摘要**
  - 在创建过程中，媒体对象也会传递给 `summary_llm`
  - 使用 `enrichment_llm` 提示词增强媒体对象的嵌入空间
- **更简单且高性能的 HTTP 栈**
  - 从 `aiohttp` 和 `httpx` 整合为仅使用 `httpx`
  - 集成 [`httpx-aiohttp`](https://github.com/karpetrosyan/httpx-aiohttp) 以提升性能
- **简化了 `Context` 相关性计算**，并移除了部分假设前提
- **多项小功能改进**：例如在 JSON 无效时重试 `Context` 创建、兼容 2025 年秋季的前沿 LLMs、优化提示词模板
- **修复元数据处理问题**：通过 Semantic Scholar 和 OpenAlex 处理元数据（例如错误推断正文与补充材料具有相同文档 ID）
- **完成过去一年积累的弃用项清理**

### PaperQA2 算法

要理解 PaperQA2，我们先从底层算法的组成部分开始。PaperQA2 的默认工作流程如下：

| 阶段                   | PaperQA2 操作                                                                        |
| ---------------------- | ------------------------------------------------------------------------------------ |
| **1. 论文搜索**        | - 通过 LLM 生成的关键词查询获取候选论文                                              |
|                        | - 分块、嵌入并将候选论文添加到状态                                                   |
| **2. 收集证据**        | - 将查询转换为向量                                                                   |
|                        | - 对当前状态中的前 _k_ 个文档分块进行排名                                            |
|                        | - 结合当前查询上下文，为每个分块创建评分摘要                                         |
|                        | - 使用 LLM 重新排序并选择最相关的摘要                                                |
| **3. 生成答案**        | - 将最佳摘要放入提示词中并结合上下文                                                 |
|                        | - 根据提示词生成最终答案                                                             |

智能体可以按任意顺序调用这些工具。例如，LLM 智能体可能会执行窄搜索和宽搜索，或者在“收集证据”步骤与“生成答案”步骤中使用不同的措辞。

## 安装

对于非开发环境部署，请从 [PyPI](https://pypi.org/project/paper-qa/) 安装 PaperQA2（即第 5 版）。注意：第 5 版需要 Python 3.11+。

```bash
pip install paper-qa>=5
```

对于开发环境部署，请参阅 [CONTRIBUTING.md](CONTRIBUTING.md) 文件。

PaperQA2 依赖 LLM 运行，因此你需要设置相应的 [API key 环境变量][LiteLLM providers]（即 `export OPENAI_API_KEY=sk-...`），或搭建开源 LLM 服务器（例如使用 [llamafile](https://github.com/Mozilla-Ocho/llamafile)）。任何兼容 LiteLLM 的模型均可配置为 PaperQA2 使用。

如果你需要索引大量论文（100+篇），建议同时获取 [Crossref](https://www.crossref.org/documentation/metadata-plus/metadata-plus-keys/) 和 [Semantic Scholar](https://www.semanticscholar.org/product/api#api-key) 的 API key，这将帮助你避免触发这些元数据服务的公共速率限制。可通过导出 `CROSSREF_API_KEY` 和 `SEMANTIC_SCHOLAR_API_KEY` 环境变量来配置。

## CLI 使用

通过 CLI 测试 PaperQA2 是最快的方式。首先导航至包含论文的目录并使用 `pqa` cli：

```bash
pqa ask 'What is PaperQA2?'
```

你将看到 PaperQA2 索引你的本地 PDF 文件，收集每个文件的必要元数据（使用 [Crossref](https://www.crossref.org/) 和 [Semantic Scholar](https://www.semanticscholar.org/)），在该索引上进行搜索，然后将文件拆分为分块证据上下文、进行排名，并最终生成答案。下次查询该目录时，你的索引已经构建完成（除非检测到差异，如新增论文），因此会跳过索引和分块步骤。

所有历史答案均已索引进存储，你可以通过 `search` 子命令查询查看，或在你的 `PQA_HOME` 目录中直接访问，默认路径为 `~/.pqa/`。

```bash
pqa -i 'answers' search 'ranking and contextual summarization'
```

PaperQA2 高度可配置。在命令行运行时，`pqa --help` 会显示所有选项及简短说明。例如，要使用更高的温度运行：

```bash
pqa --temperature 0.5 ask 'What is PaperQA2?'
```

你可以使用 `pqa view` 查看所有设置。另一个有用的功能是切换其他模板化配置——例如 `fast` 是一种加快回答速度的配置，你可以通过 `pqa -s fast view` 查看它。

也许你想保存一些新配置？可以使用以下命令完成：

```bash
pqa -s my_new_settings --temperature 0.5 --llm foo-bar-5 save
```

然后即可通过以下方式调用：

```bash
pqa -s my_new_settings ask 'What is PaperQA2?'
```

如果你运行 `pqa` 且命令需要新建索引（例如更改了默认的 chunk_size），系统会自动为你创建新索引。

```bash
pqa --parsing.chunk_size 5000 ask 'What is PaperQA2?'
```

你也可以使用 `pqa` 结合 LLM 进行全文搜索。例如，让我们为目录保存一个索引并命名：

```bash
pqa -i nanomaterials index
```

现在我可以搜索关于热电材料（thermoelectrics）的论文：

```bash
pqa -i nanomaterials search thermoelectrics
```

或者使用常规的 `ask` 命令：

```bash
pqa -i nanomaterials ask 'Are there nm scale features in thermoelectric materials?'
```

CLI 和模块均基于过往性能和我们出版物预置了配置，可按如下方式调用：

```bash
pqa --settings <setting name> \
    ask 'Are there nm scale features in thermoelectric materials?'
```

### 内置配置

在 [`src/paperqa/configs`](src/paperqa/configs) 中，我们打包了已知有用的配置：

| 设置名称       | 描述                                                                                                     |
| -------------- | -------------------------------------------------------------------------------------------------------- |
| high_quality   | 高性能但相对昂贵（因 `evidence_k` = 15）的查询，使用 `ToolSelector` 智能体。                             |
| fast           | 快速且低成本获取答案的配置。                                                                             |
| wikicrow       | 模拟我们 WikiCrow 出版物中使用的维基百科文章写作流程的配置。                                             |
| contracrow     | 用于发现论文矛盾的配置，你的查询应为一个需要被标记为矛盾（或非矛盾）的声明。                             |
| debug          | 仅用于调试的配置，不适用于任何实际应用场景。                                                             |
| tier1_limits   | 匹配 OpenAI 各等级速率限制的配置，可使用 `tier<1-5>_limits` 指定具体等级。                               |

### 速率限制

如果你遇到了速率限制（例如使用 OpenAI Tier 1 计划），可以将限制配置到 PaperQA2 中。针对每个 OpenAI 等级，都提供了预置的限制配置。

```bash
pqa --settings 'tier1_limits' ask 'What is PaperQA2?'
```

这将限制你的系统使用 [tier1_limits](src/paperqa/configs/tier1_limits.json)，并减缓查询速度以适应限制。

你也可以通过匹配 [limits](https://limits.readthedocs.io/en/stable/quickstart.html#rate-limit-string-notation) 模块规范的任意速率限制字符串手动指定：

```bash
pqa --summary_llm_config '{"rate_limit": {"gpt-4o-2024-11-20": "30000 per 1 minute"}}' \
    ask 'What is PaperQA2?'
```

或者在命令式调用时添加到 `Settings` 对象中：

```python
from paperqa import Settings, ask

answer_response = ask(
    "What is PaperQA2?",
    settings=Settings(
        llm_config={"rate_limit": {"gpt-4o-2024-11-20": "30000 per 1 minute"}},
        summary_llm_config={"rate_limit": {"gpt-4o-2024-11-20": "30000 per 1 minute"}},
    ),
)
```

## 库（Library）使用

你可以通过 Python 直接访问 PaperQA2 的完整工作流：

```python
from paperqa import Settings, ask

answer_response = ask(
    "What is PaperQA2?",
    settings=Settings(temperature=0.5, paper_directory="my_papers"),
)
```

请参阅我们的 [安装文档](#installation) 了解如何从 PyPI 安装包。

### 智能体添加/查询文档

答案对象包含以下属性：`formatted_answer`、`answer`（仅答案）、`question`，以及 `context`（用于生成答案的段落摘要）。
`ask` 会使用 `SearchPapers` 工具，该工具会查询本地文件索引。你可以通过 `Settings` 对象指定此位置：

```python
from paperqa import Settings, ask

answer_response = ask(
    "What is PaperQA2?",
    settings=Settings(
        temperature=0.5, agent={"index": {"paper_directory": "my_papers"}}
    ),
)
```

`ask` 只是真实入口的便捷封装。如果你希望运行并发异步任务，可以直接访问该入口：

```python
from paperqa import Settings, agent_query

answer_response = await agent_query(
    query="What is PaperQA2?",
    settings=Settings(
        temperature=0.5, agent={"index": {"paper_directory": "my_papers"}}
    ),
)
```

默认智能体将使用基于 LLM 的智能体，但你也可以指定 `"fake"` 智能体以使用硬编码的调用路径 `search -> gather evidence -> answer`，从而减少 token 消耗。

### 手动（无智能体）添加/查询文档

通常通过智能体执行时，智能体会调用搜索工具，在后台将文档添加到 `Docs` 对象中。不过，如果你偏好精细控制，可以直接与 `Docs` 对象交互。

注意：手动添加和查询 `Docs` 不会影响性能。它只是移除了智能体自动选择要添加文档的自动化流程。

```python
from paperqa import Docs, Settings

# 有效扩展名包括 .pdf, .txt, .md, .html, .docx, .xlsx, .pptx，以及代码文件（如 .py, .ts, .yaml）
doc_paths = ("myfile.pdf", "myotherfile.pdf")

# 通过添加一批文档准备 Docs 对象
docs = Docs()
for doc_path in doc_paths:
    await docs.aadd(doc_path)

# 设置我们查询 Docs 对象的期望方式
settings = Settings()
settings.llm = "claude-3-5-sonnet-20240620"
settings.answer.answer_max_sources = 3

# 查询 Docs 对象获取答案
session = await docs.aquery("What is PaperQA2?", settings=settings)
print(session)
```

### 异步操作

PaperQA2 专为异步使用而设计。同步 API 仅是异步版本的封装。以下是方法及其 `async` 等价项：

| Sync                | Async                |
| ------------------- | -------------------- |
| `Docs.add`          | `Docs.aadd`          |
| `Docs.add_file`     | `Docs.aadd_file`     |
| `Docs.add_url`      | `Docs.aadd_url`      |
| `Docs.get_evidence` | `Docs.aget_evidence` |
| `Docs.query`        | `Docs.aquery`        |

同步版本仅在循环中调用异步版本。大多数现代 Python 环境原生支持 `async`（包括 Jupyter Notebook！）。因此你可以在 Jupyter Notebook 中这样写：

```python
import asyncio
from paperqa import Docs


async def main() -> None:
    docs = Docs()
    # 有效扩展名包括 .pdf, .txt, .md, .html, .docx, .xlsx, .pptx，以及代码文件（如 .py, .ts, .yaml）
    for doc in ("myfile.pdf", "myotherfile.pdf"):
        await docs.aadd(doc)

    session = await docs.aquery("What is PaperQA2?")
    print(session)


asyncio.run(main())
```

### 选择模型

默认情况下，PaperQA2 对 `summary_llm`、`llm` 和 `agent_llm` 使用 OpenAI 的 `gpt-4o-2024-11-20` 模型。请参阅 [配置速查表](#settings-cheatsheet) 获取这些设置的更多信息。PaperQA2 默认还使用 OpenAI 的 `text-embedding-3-small` 模型作为 `embedding` 设置。如果你没有 OpenAI API key，可以使用其他嵌入模型。关于嵌入模型的更多信息可在 [“嵌入模型”部分](#embedding-model) 找到。

我们使用 [`lmi`](https://github.com/Future-House/ldp/tree/main/packages/lmi) 包作为 LLM 接口，该包底层通过 `litellm` 支持多种 LLM 提供商。你可以轻松调整以使用 `litellm` 支持的任意模型：

```python
from paperqa import Settings, ask

answer_response = ask(
    "What is PaperQA2?",
    settings=Settings(
        llm="gpt-4o-mini", summary_llm="gpt-4o-mini", agent={"index": {"paper_directory": "my_papers"}}
    ),
)
```

要使用 Claude，请确保设置了 `ANTHROPIC_API_KEY` 环境变量。在此示例中，我们还使用了不同的嵌入模型。请确保运行 `pip install paper-qa[local]` 以使用本地嵌入模型。

```python
from paperqa import Settings, ask
from paperqa.settings import AgentSettings

answer_response = ask(
    "What is PaperQA2?",
    settings=Settings(
        llm="claude-3-5-sonnet-20240620",
        summary_llm="claude-3-5-sonnet-20240620",
        agent=AgentSettings(agent_llm="claude-3-5-sonnet-20240620"),
        # 参见：https://huggingface.co/sentence-transformers/multi-qa-MiniLM-L6-cos-v1
        embedding="st-multi-qa-MiniLM-L6-cos-v1",
    ),
)
```

或使用 Gemini，通过 Google AI Studio 设置 `GEMINI_API_KEY`：

```python
from paperqa import Settings, ask
from paperqa.settings import AgentSettings

answer_response = ask(
    "What is PaperQA2?",
    settings=Settings(
        llm="gemini/gemini-2.0-flash",
        summary_llm="gemini/gemini-2.0-flash",
        agent=AgentSettings(agent_llm="gemini/gemini-2.0-flash"),
        embedding="gemini/text-embedding-004",
    ),
)
```

#### 本地托管

你可以使用 llama.cpp 作为 LLM。请注意，你应该使用相对较大的模型，因为 PaperQA2 需要遵循大量指令。7B 以下的模型无法获得良好性能。

最简单的配置方式是下载一个 [llama file](https://github.com/Mozilla-Ocho/llamafile) 并使用 `-cb -np 4 -a my-llm-model --embedding` 参数执行，这将启用连续批处理和嵌入功能。

```python
from paperqa import Settings, ask

local_llm_config = dict(
    model_list=[
        dict(
            model_name="my_llm_model",
            litellm_params=dict(
                model="my-llm-model",
                api_base="http://localhost:8080/v1",
                api_key="sk-no-key-required",
                temperature=0.1,
                frequency_penalty=1.5,
                max_tokens=512,
            ),
        )
    ]
)

answer_response = ask(
    "What is PaperQA2?",
    settings=Settings(
        llm="my-llm-model",
        llm_config=local_llm_config,
        summary_llm="my-llm-model",
        summary_llm_config=local_llm_config,
    ),
)
```

使用 `ollama` 托管的模型也受支持。要运行以下示例，请确保你已通过 ollama 下载了 llama3.2 和 mxbai-embed-large。

```python
from paperqa import Settings, ask

local_llm_config = {
    "model_list": [
        {
            "model_name": "ollama/llama3.2",
            "litellm_params": {
                "model": "ollama/llama3.2",
                "api_base": "http://localhost:11434",
            },
        }
    ]
}

answer_response = ask(
    "What is PaperQA2?",
    settings=Settings(
        llm="ollama/llama3.2",
        llm_config=local_llm_config,
        summary_llm="ollama/llama3.2",
        summary_llm_config=local_llm_config,
        embedding="ollama/mxbai-embed-large",
    ),
)
```

### 嵌入模型

嵌入向量用于检索 k 个文本（k 通过 `Settings.answer.evidence_k` 指定）以进行重排序和上下文摘要。如果你不想使用嵌入，而是直接获取所有分块，可通过 `Settings.answer.evidence_retrieval` 设置禁用“证据检索”。

PaperQA2 默认使用 OpenAI (`text-embedding-3-small`) 嵌入向量，但对向量存储和嵌入选择提供了灵活选项。

#### 指定嵌入模型

指定嵌入模型的最简单方式是通过 `Settings.embedding`：

```python
from paperqa import Settings, ask

answer_response = ask(
    "What is PaperQA2?",
    settings=Settings(embedding="text-embedding-3-large"),
)
```

`embedding` 接受 litellm 支持的任何嵌入模型名称。PaperQA2 还支持 `"hybrid-<model_name>"`（即 `"hybrid-text-embedding-3-small"`）的混合嵌入输入，以使用稀疏关键词（基于 token 取模嵌入）和密集向量嵌入，其中密集模型名可使用任意 litellm 模型。使用 `"sparse"` 可仅启用稀疏关键词嵌入。

嵌入模型用于创建 PaperQA2 全文嵌入向量的索引（`texts_index` 参数）。你可以在将新论文添加到 `Docs` 对象时指定嵌入模型：

```python
from paperqa import Docs, Settings

docs = Docs()
for doc in ("myfile.pdf", "myotherfile.pdf"):
    await docs.aadd(doc, settings=Settings(embedding="text-embedding-large-3"))
```

注意 PaperQA2 使用 Numpy 作为密集向量存储。其设计通过初始关键词搜索，将每个答案所需的分块数量减少到相对较小的范围（< 1k）。因此，`NumpyVectorStore` 是一个良好的起点，它是一个简单的内存存储，无索引结构。但如果需要超出内存的向量存储，你可以通过 `QdrantVectorStore` 类使用外部向量数据库如 [Qdrant](https://qdrant.tech/)。

混合嵌入可自定义：

```python
from paperqa import (
    Docs,
    HybridEmbeddingModel,
    SparseEmbeddingModel,
    LiteLLMEmbeddingModel,
)


model = HybridEmbeddingModel(
    models=[LiteLLMEmbeddingModel(), SparseEmbeddingModel(ndim=1024)]
)
docs = Docs()
for doc in ("myfile.pdf", "myotherfile.pdf"):
    await docs.aadd(doc, embedding_model=model)
```

稀疏嵌入（关键词）模型默认具有 256 维，但可通过 `ndim` 参数指定。

#### 本地嵌入模型（Sentence Transformers）

如果你安装了 `sentence-transformers`，可以使用 `SentenceTransformerEmbeddingModel` 模型，这是一个 [本地嵌入库](https://sbert.net/)，支持 HuggingFace 模型等。你可以通过添加 `local` extras 来安装它。

```sh
pip install paper-qa[local]
```

然后在嵌入模型名前加上 `st-` 前缀：

```python
from paperqa import Settings, ask

answer_response = ask(
    "What is PaperQA2?",
    settings=Settings(embedding="st-multi-qa-MiniLM-L6-cos-v1"),
)
```

或使用混合模型：

```python
from paperqa import Settings, ask

answer_response = ask(
    "What is PaperQA2?",
    settings=Settings(embedding="hybrid-st-multi-qa-MiniLM-L6-cos-v1"),
)
```

### 调整来源数量

你可以调整来源（文本段落）的数量以减少 token 消耗或增加上下文。`k` 指的是最相关且多样化（可能来自不同来源）的前 k 个段落。每个段落都会发送给 LLM 进行摘要生成，或判断其是否不相关。在此步骤之后，会应用 `max_sources` 限制，以确保最终答案能放入 LLM 的上下文窗口中。因此，`k` > `max_sources`，且 `max_sources` 是最终答案使用的来源数量。

```python
from paperqa import Settings

settings = Settings()
settings.answer.answer_max_sources = 3
settings.answer.evidence_k = 5

await docs.aquery(
    "What is PaperQA2?",
    settings=settings,
)
```

### 使用代码或 HTML

你不需要仅依赖论文——你可以使用代码或原始 HTML。注意该工具专注于回答问题，因此在编写代码方面表现不佳。需要注意的是，该工具无法从代码中推断引用关系，因此你需要自行提供。

```python
import glob
import os
from paperqa import Docs

source_files = glob.glob("**/*.js")

docs = Docs()
for f in source_files:
    # 此处假设文件名在代码中具有唯一性
    await docs.aadd(
        f, citation="File " + os.path.basename(f), docname=os.path.basename(f)
    )
session = await docs.aquery("Where is the search bar in the header defined?")
print(session)
```

### 多模态支持

多模态支持主要围绕：

- 独立图片
- PDF 中的图片或表格

`Docs` 对象通过 `ParsedMedia` 对象存储媒体。在对文档进行分块时，媒体不会在分块边界处拆分，因此可能 2+ 个分块对应同一个媒体。这意味着在 PaperQA 内部，每个分块的 `ParsedMedia` 与分块之间存在一对多关系。

根据源文档的不同，同一张图片可能出现多次（例如 PDF 的每页边距都包含一个 Logo）。因此，客户端应将媒体数据库视为与分块存在多对多关系。

由于 PaperQA 的证据收集过程以基于文本的检索为中心，可能存在相关图片或表格未被检索到的情况，因为其关联的正文内容不相关。具体而言，假设论文中的图片带有简短说明，且放置在相关正文讨论的一页之后。为解决此问题，PaperQA 支持在文档读取时进行媒体增强。基本上，在读入 PDF 后，`parsing.enrichment_llm` 会接收 `parsing.enrichment_prompt` 及相邻文本，为每张图/表生成合成说明。这些合成说明用于调整每个文本分块的嵌入向量，但与实际源文本保持分离。这样证据收集即可获取相关图片/表格，同时避免 LLM 生成的说明污染上下文摘要。

如果你希望支持多模态 PDF 读取但不想要增强（因为会在读取时增加一次 LLM 提示调用），可通过将 `parsing.multimodal` 设置为 `ON_WITHOUT_ENRICHMENT` 来禁用增强功能。

在为给定分块（一个 `Text`）创建上下文摘要时，摘要 LLM 会同时接收分块的文本及其关联的媒体，但输出的上下文摘要本身仍保持纯文本格式。

如果你愿意，将提示词 `paperqa.prompts.summary_json_multimodal_system_prompt` 指定给设置项 `prompt.summary_json_system`，将在任何上下文摘要中包含 `used_images` 标志，以标记是否使用了图片。

### 使用外部数据库/向量数据库及缓存

你可能希望将解析后的文本和嵌入向量缓存到外部数据库或文件中。然后你可以直接从中构建 Docs 对象：

```python
from paperqa import Docs, Doc, Text

docs = Docs()

for ... in my_docs:
    doc = Doc(docname=..., citation=..., dockey=..., citation=...)
    texts = [Text(text=..., name=..., doc=doc) for ... in my_texts]
    docs.add_texts(texts, doc)
```

### 创建索引

默认情况下，索引将放置在 [主目录][home dir] 中。这可以通过 `PQA_HOME` 环境变量控制。

索引通过读取 `IndexSettings.paper_directory` 中的文件构建。默认情况下，我们递归读取论文子目录，除非使用 `IndexSettings.recurse_subdirectories` 禁用。论文目录本身不会被修改，仅作为只读来源。

[home dir]: https://docs.python.org/3/library/pathlib.html#pathlib.Path.home

#### 清单文件（Manifest Files）

索引过程会尝试通过基于 LLM 的文本处理推断论文的标题和 DOI 等元数据。你可以使用“清单”文件避免此不确定性，该文件是一个包含 `DocDetails` 字段的 CSV（顺序无关紧要）。例如：

- `file_location`: 论文 PDF 在索引目录内的相对路径
- `doi`: 论文的 DOI
- `title`: 论文标题

通过提供这些信息，我们可以确保查询 Crossref 等元数据提供商的结果准确无误。

为简化清单创建过程，提供了辅助类方法 `Doc.to_csv`，在 `DocDetails` 上调用时也有效。

### 复用索引

本地搜索索引基于当前 `Settings` 对象的哈希值构建。因此请确保正确指定了 `IndexSettings` 对象中的 `paper_directory`。通常建议：

1. 预先根据论文文件夹构建索引（可能需要几分钟）
2. 复用该索引执行多次查询

```python
import os

from paperqa import Settings
from paperqa.agents.main import agent_query
from paperqa.agents.search import get_directory_index


async def amain(folder_of_papers: str | os.PathLike) -> None:
    settings = Settings(agent={"index": {"paper_directory": folder_of_papers}})

    # 1. 构建索引。未指定时会自动生成索引名称
    built_index = await get_directory_index(settings=settings)
    print(settings.get_index_name())  # 显示自动生成的索引名称
    print(await built_index.index_files)  # 显示索引内容

    # 2. 可多次使用 settings 配合 ask 进行查询
    answer_response_1 = await agent_query(
        query="What is a cool retrieval augmented generation technique?",
        settings=settings,
    )
    answer_response_2 = await agent_query(
        query="What is PaperQA2?",
        settings=settings,
    )
```

### 直接使用客户端

PaperQA2 最强大的功能之一是其能够整合多个元数据源的数据。例如，[Unpaywall](https://unpaywall.org/) 可提供开放获取状态/直接 PDF 链接，[Crossref](https://www.crossref.org/) 可提供 bibtex，[Semantic Scholar](https://www.semanticscholar.org/) 可提供引用许可信息。以下是简短演示：

```python
from paperqa.clients import DocMetadataClient, ALL_CLIENTS

client = DocMetadataClient(metadata_clients=ALL_CLIENTS)
details = await client.query(title="Augmenting language models with chemistry tools")

print(details.formatted_citation)
# Andres M. Bran, Sam Cox, Oliver Schilter, Carlo Baldassari,
# Andrew D. White, and Philippe Schwaller.
#  Augmenting large language models with chemistry tools. Nature Machine Intelligence,
# 6:525-535, May 2024. URL: https://doi.org/10.1038/s42256-024-00832-8,
# doi:10.1038/s42256-024-00832-8.
# This article has 243 citations and is from a domain leading peer-reviewed journal.

print(details.citation_count)
# 243

print(details.license)
# cc-by

print(details.pdf_url)
# https://www.nature.com/articles/s42256-024-00832-8.pdf
```

`client.query` 旨在检查标题的精确匹配。它具有一定的容错性（如大小写、漏词）。不过标题可能存在重复——因此你还可以添加作者进行消歧。或者直接提供 DOI `client.query(doi="10.1038/s42256-024-00832-8")`。

如果你在大规模下执行此操作，可能不希望使用 `ALL_CLIENTS`（省略该参数即可），并且可以指定所需的具体字段以加速查询。例如：

```python
details = await client.query(
    title="Augmenting large language models with chemistry tools",
    authors=["Andres M. Bran", "Sam Cox"],
    fields=["title", "doi"],
)
```

这将比第一次查询返回得快得多，且我们能确保作者匹配无误。

## 配置速查表

| Setting                                      | Default                                | Description                                                                                                                   |
| -------------------------------------------- | -------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `llm`                                        | `"gpt-4o-2024-11-20"`                  | 用于通用任务的 LLM，包括元数据推断（见 Docs.aadd）和答案生成（见 Docs.aquery 及 gen_answer 工具）。                           |
| `llm_config`                                 | `None`                                 | `llm` 的可选配置。                                                                                                          |
| `summary_llm`                                | `"gpt-4o-2024-11-20"`                  | 用于创建上下文摘要的 LLM（见 Docs.aget_evidence 及 gather_evidence 工具）。                                                 |
| `summary_llm_config`                         | `None`                                 | `summary_llm` 的可选配置。                                                                                                    |
| `embedding`                                  | `"text-embedding-3-small"`             | 添加论文时对文本分块进行嵌入的模型。                                                                                            |
| `embedding_config`                           | `None`                                 | `embedding` 的可选配置。                                                                                                      |
| `temperature`                                | `0.0`                                  | LLM 的温度参数。                                                                                                              |
| `batch_size`                                 | `1`                                    | 调用 LLM 时的批处理大小。                                                                                                     |
| `texts_index_mmr_lambda`                     | `1.0`                                  | 文本索引中 MMR（最大边际相关性）的 Lambda 值。                                                                                |
| `verbosity`                                  | `0`                                    | 日志记录整数级别（0-3）。3 = 记录所有 LLM/嵌入调用。                                                                         |
| `custom_context_serializer`                  | `None`                                 | 自定义异步函数（见类型签名）以覆盖默认答案上下文序列化逻辑。                                                                  |
| `answer.evidence_k`                          | `10`                                   | 要检索的证据数量。                                                                                                            |
| `answer.evidence_retrieval`                  | `True`                                 | 使用检索 vs 处理所有文档。                                                                                                    |
| `answer.evidence_summary_length`             | `"about 100 words"`                    | 证据摘要的长度。                                                                                                              |
| `answer.evidence_skip_summary`               | `False`                                | 是否跳过摘要生成。                                                                                                            |
| `answer.evidence_text_only_fallback`         | `False`                                | 是否允许上下文创建在无媒体时重试。                                                                                            |
| `answer.answer_max_sources`                  | `5`                                    | 答案的最大来源数量。                                                                                                          |
| `answer.max_answer_attempts`                 | `None`                                 | 生成答案的最大尝试次数。                                                                                                      |
| `answer.answer_length`                       | `"about 200 words, but can be longer"` | 最终答案的长度。                                                                                                              |
| `answer.max_concurrent_requests`             | `4`                                    | 向 LLM 发送的最大并发请求数。                                                                                                 |
| `answer.answer_filter_extra_background`      | `False`                                | 是否引用模型提供的背景信息。                                                                                                  |
| `answer.get_evidence_if_no_contexts`         | `True`                                 | 允许惰性证据收集。                                                                                                            |
| `answer.group_contexts_by_question`          | `False`                                | 在最终上下文提示词中按底层 `gather_evidence` 问题分组最终上下文。                                                             |
| `answer.evidence_relevance_score_cutoff`     | `1`                                    | 纳入答案上下文的证据相关性分数阈值（包含）。                                                                                  |
| `answer.skip_evidence_citation_strip`        | `False`                                | 跳过从 `gather_evidence` 上下文中移除引用。                                                                                   |
| `parsing.page_size_limit`                    | `1,280,000`                            | 每页字符限制。                                                                                                                |
| `parsing.use_doc_details`                    | `True`                                 | 是否获取文档的元数据详情。                                                                                                    |
| `parsing.reader_config`                      | `dict`                                 | 文档读取器的可选关键字参数。                                                                                                  |
| `parsing.multimodal`                         | `True`                                 | 控制从适用文档中解析文本和媒体，以及可能使用文本描述对其进行增强。                                                            |
| `parsing.defer_embedding`                    | `False`                                | 是否将嵌入推迟到摘要生成阶段。                                                                                                |
| `parsing.parse_pdf`                          | `paperqa_pypdf.parse_pdf_to_pages`     | 解析 PDF 文件的函数。                                                                                                         |
| `parsing.configure_pdf_parser`               | No-op                                  | 用于配置 `parse_pdf` 内 PDF 解析器的可调用对象，适用于启用日志记录等行为。                                                    |
| `parsing.doc_filters`                        | `None`                                 | 允许文档的可选过滤器。                                                                                                        |
| `parsing.use_human_readable_clinical_trials` | `False`                                | 将临床试验 JSON 解析为可读文本。                                                                                              |
| `parsing.enrichment_llm`                     | `"gpt-4o-2024-11-20"`                  | 用于媒体增强的 LLM。                                                                                                          |
| `parsing.enrichment_llm_config`              | `None`                                 | `enrichment_llm` 的可选配置。                                                                                                 |
| `parsing.enrichment_page_radius`             | `1`                                    | 增强功能中上下文文本的页面半径。                                                                                              |
| `parsing.enrichment_prompt`                  | `image_enrichment_prompt_template`     | 用于增强媒体的提示词模板。                                                                                                    |
| `parsing.citation_prompt`                    | `citation_prompt`                      | 从预览单个分块创建引用的提示词。                                                                                              |
| `parsing.structured_citation_prompt`         | `structured_citation_prompt`           | 从预览单个分块创建引用（JSON 格式）的提示词。                                                                                 |
| `parsing.disable_doc_valid_check`            | `False`                                | 禁用检查文档是否像文本（是否正确解析）的标志。                                                                                |
| `prompts.summary`                            | `summary_prompt`                       | 文本摘要模板，必须包含与 `summary_prompt` 匹配的变量。                                                                        |
| `prompts.qa`                                 | `qa_prompt`                            | QA 模板，必须包含与 `qa_prompt` 匹配的变量。                                                                                  |
| `prompts.select`                             | `select_paper_prompt`                  | 论文选择模板，必须包含与 `select_paper_prompt` 匹配的变量。                                                                   |
| `prompts.pre`                                | `None`                                 | 可选前置提示词，仅使用原始问题进行模板化，用于在 QA 提示词前附加信息。                                                        |
| `prompts.post`                               | `None`                                 | 可选后置处理提示词，可访问 PQASession 字段。                                                                                  |
| `prompts.system`                             | `default_system_prompt`                | 模型的系统提示词。                                                                                                            |
| `prompts.use_json`                           | `True`                                 | 是否使用 JSON 格式。                                                                                                          |
| `prompts.summary_json`                       | `summary_json_prompt`                  | 特定于 JSON 的摘要提示词。                                                                                                    |
| `prompts.summary_json_system`                | `summary_json_system_prompt`           | JSON 摘要的系统提示词。                                                                                                       |
| `prompts.context_outer`                      | `CONTEXT_OUTER_PROMPT`                 | 生成答案时如何格式化所有上下文的提示词。                                                                                      |
| `prompts.context_inner`                      | `CONTEXT_INNER_PROMPT`                 | 生成答案时如何格式化单个上下文的提示词。必须包含 'name' 和 'text' 变量。                                                      |
| `prompts.answer_iteration_prompt`            | `answer_iteration_prompt_template`     | 注入现有历史答案以允许迭代的提示词。默认不注入任何历史答案。                                                                  |
| `agent.agent_llm`                            | `"gpt-4o-2024-11-20"`                  | 智能体内负责工具选择的 LLM。                                                                                                  |
| `agent.agent_llm_config`                     | `None`                                 | `agent_llm` 的可选配置。                                                                                                      |
| `agent.agent_type`                           | `"ToolSelector"`                       | 要使用的智能体类型。                                                                                                          |
| `agent.agent_config`                         | `None`                                 | AGENT 构造函数的可选关键字参数。                                                                                              |
| `agent.agent_system_prompt`                  | `env_system_prompt`                    | 可选系统提示消息。                                                                                                            |
| `agent.agent_prompt`                         | `env_reset_prompt`                     | 智能体提示词。                                                                                                                |
| `agent.return_paper_metadata`                | `False`                                | 是否在搜索工具结果中包含论文标题/年份。                                                                                        |
| `agent.search_count`                         | `8`                                    | 搜索计数。                                                                                                                    |
| `agent.timeout`                              | `500.0`                                | 智能体执行超时时间（秒）。                                                                                                    |
| `agent.tool_names`                           | `None`                                 | 提供给智能体的工具的可选覆盖项。                                                                                              |
| `agent.max_timesteps`                        | `None`                                 | 环境步数的可选上限。                                                                                                          |
| `agent.agent_evidence_n`                     | `1`                                    | 收集证据后展示给智能体的排名前 n 的证据。                                                                                     |
| `agent.rebuild_index`                        | `True`                                 | 在智能体运行器开始时重建索引的标志。                                                                                            |
| `agent.callbacks`                            | `{}`                                   | 与环境状态一起调用的可调用对象命名列表。                                                                                        |
| `agent.index.name`                           | `None`                                 | 索引的可选名称。                                                                                                              |
| `agent.index.paper_directory`                | `Current working directory`            | 包含待索引论文的目录。                                                                                                        |
| `agent.index.manifest_file`                  | `None`                                 | 包含文档属性的清单 CSV 路径。                                                                                                 |
| `agent.index.index_directory`                | `pqa_directory("indexes")`             | 存储 PQA 索引的目录。                                                                                                         |
| `agent.index.use_absolute_paper_directory`   | `False`                                | 是否使用绝对论文目录路径。                                                                                                    |
| `agent.index.recurse_subdirectories`         | `True`                                 | 索引时是否递归进入子目录。                                                                                                    |
| `agent.index.concurrency`                    | `5`                                    | 并发文件系统读取数。                                                                                                          |
| `agent.index.sync_with_paper_directory`      | `True`                                 | 加载时是否将索引与论文目录同步。                                                                                              |
| `agent.index.batch_size`                     | `1`                                    | 提交到索引前处理的文件数量。                                                                                                  |
| `agent.index.files_filter`                   | `lambda f: f.suffix in {...}`          | 标记论文目录中待索文件的过滤器函数。                                                                                            |

## 如何获取论文？

这是个非常好的问题！最好的方法通常是下载你认为有助于回答你问题的论文的 PDF，然后从这里开始。

详见 [关于 Zotero、OpenReview 和解析的文档](docs/tutorials/where_do_I_get_papers.md)

## 回调（Callbacks）

若要在每次 LLM 补全的分块上执行函数，你需要提供一个可在每个分块上调用的函数。例如，若要获得打字机视图的输出效果，可以这样做：

```python
from paperqa import Docs


def typewriter(chunk: str) -> None:
    print(chunk, end="")


docs = Docs()

# 添加一些文档...

await docs.aquery("What is PaperQA2?", callbacks=[typewriter])
```

### 缓存嵌入向量

通常，无论使用何种向量存储，pickle 序列化 `Docs` 时都会自动缓存嵌入向量。因此只要保存了底层的 `Docs` 对象，你就可以避免重新嵌入文档。

## 自定义提示词（Prompts）

你可以通过设置来自定义任意提示词。

```python
from paperqa import Docs, Settings

my_qa_prompt = (
    "Answer the question '{question}'\n"
    "Use the context below if helpful. "
    "You can cite the context using the key like (pqac-abcd1234). "
    "If there is insufficient context, write a poem "
    "about how you cannot answer.\n\n"
    "Context: {context}"
)

docs = Docs()
settings = Settings()
settings.prompts.qa = my_qa_prompt
await docs.aquery("What is PaperQA2?", settings=settings)
```

### 前置与后置提示词

遵循上述语法，你还可以包含在查询执行后和查询执行前运行的提示词。例如，你可以利用此功能对答案进行批判性评估。

## 常见问题解答

### 为什么我的结果与论文中的不同？

FutureHouse 内部有一套略有不同的工具集。我们正在尝试将其中一些（如引用遍历）整合到本仓库中。然而，我们拥有访问研究论文的 API 和许可证，无法公开共享。此外，在我们研究论文的实验中，我们并非从已知的 PDF 开始。我们的智能体必须通过在所有论文中进行关键词搜索来识别它们，而不仅仅是子集。我们正在逐步对齐这两个版本的 PaperQA，但直到出现免费开源的论文获取方式（即使是仅开源论文）之前，你都需要自行提供 PDF。

### 这与 LlamaIndex 或 LangChain 有何区别？

[LangChain](https://github.com/langchain-ai/langchain)
和 [LlamaIndex](https://github.com/run-llama/llama_index)
都是用于开发 LLM 应用的框架，提供了针对智能体工作流和检索增强生成（RAG）的抽象。

随着时间推移，PaperQA 团队逐渐选择保持与框架无关（framework-agnostic），将 LLM 驱动外包给 [LiteLLM][LiteLLM general docs]，除 Pydantic 外不使用任何其他框架来处理工具。PaperQA 专注于科学论文及其元数据。

PaperQA 可以使用 LlamaIndex 或 LangChain 重新实现。例如，我们的 `GatherEvidence` 工具可以重新实现在带有基于 LLM 的重排序和上下文摘要的检索器中。LlamaIndex 中的树状响应方法也有类似工作。

### 我可以保存或加载吗？

`Docs` 类支持 pickle 序列化和反序列化。如果你想保存文档的嵌入向量以便后续加载，这将非常有用。

```python
import pickle

# save
with open("my_docs.pkl", "wb") as f:
    pickle.dump(docs, f)

# load
with open("my_docs.pkl", "rb") as f:
    docs = pickle.load(f)
```

## 复现（Reproduction）

在 [docs/2024-10-16_litqa2-splits.json5](docs/2024-10-16_litqa2-splits.json5) 中包含了训练、评估和测试拆分所使用的题目 ID，以及用于构建拆分索引的论文 DOI。

- **训练集与验证集**：题目 ID 来自 [LAB-Bench's LitQA2 question IDs](https://github.com/Future-House/LAB-Bench/blob/main/LitQA2/litqa-v2-public.jsonl)。
- **测试集**：题目 ID 来自 [aviary-paper-data's LitQA2 question IDs](https://huggingface.co/datasets/futurehouse/aviary-paper-data)。

有多篇论文在逐步构建 PaperQA，详见下方 [引用](#citation) 部分。要复现结果：

- `skarlinski2024language`：训练集和验证集适用。测试集仍保持隐藏。
- `narayanan2024aviarytraininglanguageagents`：训练集、验证集和测试集均适用。

关于如何使用 LitQA 进行评估的示例，请参阅 [aviary.litqa](https://github.com/Future-House/aviary/tree/main/packages/litqa#running-litqa)。

## 引用（Citation）

如果你使用了本软件，请阅读并引用以下论文：

```bibtex
@article{narayanan2024aviarytraininglanguageagents,
      title = {Aviary: training language agents on challenging scientific tasks},
      author = {
      Siddharth Narayanan and
 James D. Braza and
 Ryan-Rhys Griffiths and
 Manu Ponnapati and
 Albert Bou and
 Jon Laurent and
 Ori Kabeli and
 Geemi Wellawatte and
 Sam Cox and
 Samuel G. Rodriques and
 Andrew D. White},
      journal = {arXiv preprent arXiv:2412.21154},
      year = {2024},
      url = {https://doi.org/10.48550/arXiv:2412.21154},
}
```

```bibtex
@article{skarlinski2024language,
    title = {Language agents achieve superhuman synthesis of scientific knowledge},
    author = {
    Michael D. Skarlinski and
 Sam Cox and
 Jon M. Laurent and
 James D. Braza and
 Michaela Hinks and
 Michael J. Hammerling and
 Manvitha Ponnapati and
 Samuel G. Rodriques and
 Andrew D. White},
    journal = {arXiv preprent arXiv:2409.13740},
    year = {2024},
    url = {https://doi.org/10.48550/arXiv:2409.13740}
}
```

```bibtex
@article{lala2023paperqa,
    title = {PaperQA: Retrieval-Augmented Generative Agent for Scientific Research},
    author = {
    Jakub Lála and
 Odhran O'Donoghue and
 Aleksandar Shtedritski and
 Sam Cox and
 Samuel G. Rodriques and
 Andrew D. White},
    journal = {arXiv preprint arXiv:2312.07559},
    year = {2023},
    url = {https://doi.org/10.48550/arXiv:2312.07559}
}
```
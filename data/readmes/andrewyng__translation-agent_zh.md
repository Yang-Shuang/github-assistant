# Translation Agent：基于反思机制的智能体翻译工作流

这是一个用于机器翻译的 Python 演示项目，展示了基于反思（reflection）机制的智能体工作流。主要步骤如下：
1. 提示 LLM 将文本从 `source_language` 翻译为 `target_language`；
2. 让 LLM 对译文进行反思，提出建设性的改进建议；
3. 根据这些建议优化译文。

## 可定制性

通过将大语言模型（LLM）作为翻译引擎的核心，该系统具有高度的可控性。例如，与传统的机器翻译（MT）系统相比，通过调整提示词（prompt），使用此工作流可以更轻松地实现：
- 修改输出风格，如正式或非正式。
- 指定如何处理习语及专有名词、技术术语和缩写。例如，在提示词中包含术语表（glossary）可以让你确保特定术语（如 open source、H100 或 GPU）的翻译保持一致。
- 指定语言的具体地区用法或特定方言，以服务于目标受众。例如，拉丁美洲的西班牙语与西班牙的西班牙语不同；加拿大的法语也与法国的法语有所差异。

**本项目并非成熟软件**，它只是 Andrew 过去几个月在周末折腾翻译的产物，同时感谢合作者（Joaquin Dominguez、Nedelina Teneva、John Santerre）协助重构代码。

根据我们在传统翻译数据集上使用 BLEU 分数进行的评估，该工作流的表现有时可与主流商业产品相媲美，但有时也会稍逊一筹。不过，我们也偶尔通过此方法获得了极佳的结果（优于商业产品）。我们认为这仅仅是智能体翻译的起点，也是翻译领域一个极具潜力的方向，仍有巨大的优化空间。因此我们开源此演示项目，旨在鼓励更多的讨论、实验、研究与开源贡献。

如果智能体翻译能生成比传统架构（例如端到端 Transformer，输入文本直接输出译文）更好的结果——尽管这类架构通常运行更快/成本更低——它还将提供一种自动生成训练数据（平行语料库）的机制，可用于进一步训练和优化传统算法。（另请参阅《The Batch》中关于使用 LLM 生成训练数据的[这篇文章](https://www.deeplearning.ai/the-batch/building-models-that-learn-from-themselves/)。）

非常欢迎就如何改进本项目提出意见与建议！

## 快速开始

要使用 `translation-agent`，请按照以下步骤操作：

### 安装：
- 安装需要使用 Poetry 包管理器。[Poetry 安装指南](https://python-poetry.org/docs/#installation)。根据你的运行环境，可能适用以下命令：

```bash
pip install poetry
```

- 运行工作流需要包含 `OPENAI_API_KEY` 的 `.env` 文件。可参考 `.env.sample` 文件作为示例。
```bash
git clone https://github.com/andrewyng/translation-agent.git
cd translation-agent
poetry install
poetry shell # activates virtual environment
```

### 使用：

```python
import translation_agent as ta
source_lang, target_lang, country = "English", "Spanish", "Mexico"
translation = ta.translate(source_lang, target_lang, source_text, country)
```
可参考 `examples/example_script.py` 中的示例脚本进行尝试。

## 许可证

Translation Agent 基于 **MIT 许可证** 发布。你可以自由出于商业或非商业用途使用、修改和分发本代码。

## 扩展思路

以下是我们尚未有时间进行实验，但希望开源社区能继续探索的方向：
- **尝试其他大语言模型。** 我们主要使用 `gpt-4-turbo` 进行了原型开发。非常欢迎其他人尝试不同的 LLM 及其他超参数组合，观察它们在特定语言对上的表现差异。
- **术语表构建。** 如何高效地构建一个术语表（glossary）——或许借助 LLM ——来确保我们最关注的核心术语保持一致的翻译？例如，许多企业使用互联网上鲜见的专业术语，LLM 可能并不熟悉；此外，许多术语存在多种译法。例如，西班牙语中的“open source”可译为“Código abierto”或“Fuente abierta”，两者皆可，但在同一文档中最好选定一种并坚持使用。
- **术语表的使用与实现。** 给定一个术语表后，如何将其最优地嵌入到提示词（prompt）中？
- **不同语言的评估。** 该系统在不同语言下的表现有何差异？是否存在针对特定源语言或目标语言的优化调整？（注：对于 MT 系统已接近的高性能水平，我们不确定 BLEU 是否仍是最佳指标。）此外，其在低资源语言上的表现也有待进一步研究。
- **错误分析。** 我们发现，指定语言及国家/地区（例如“墨西哥口语西班牙语”）在我们的应用中效果相当不错。当前方法在哪些地方仍有不足？我们也特别关注其在专业领域（如法律、医学）或特殊文本类型（如电影字幕）上的表现，以深入了解其局限性。
- **更优的评估体系。** 最后，我们认为开发更好的评估指标/体系（evals）是一个重大且重要的研究课题。与其他生成自由文本的 LLM 应用类似，当前的评估指标似乎仍显不足。例如，我们发现即使在某些文档中，我们的智能体工作流能更好地捕捉上下文和术语，使得人工评分员更偏好其译文而非当前商业产品，但在句子级别的评估（使用 [FLORES](https://github.com/facebookresearch/flores) 数据集）中，该智能体系统的 BLEU 分数反而更低。我们能否设计出更好的指标（例如利用 LLM 评估译文？），以在文档层面捕捉更能反映人类偏好的翻译质量？

## 相关研究

目前已有少数学术团队开始关注基于大语言模型及智能体的翻译技术。我们认为该领域仍处于早期发展阶段！
- *ChatGPT MT: Competitive for High- (but not Low-) Resource Languages*, Robinson et al. (2023), https://arxiv.org/pdf/2309.07423
- *How to Design Translation Prompts for ChatGPT: An Empirical Study*, Gao et al. (2023), https://arxiv.org/pdf/2304.02182v2
- *Beyond Human Translation: Harnessing Multi-Agent Collaboration for Translating Ultra-Long Literary Texts*, Wu et al. (2024),  https://arxiv.org/pdf/2405.11804
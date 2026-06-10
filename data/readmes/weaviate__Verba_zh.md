# Verba

## The Golden RAGtriever - 社区版 ✨

[![Weaviate](https://img.shields.io/static/v1?label=powered%20by&message=Weaviate%20%E2%9D%A4&color=green&style=flat-square)](https://weaviate.io/)
[![PyPi downloads](https://static.pepy.tech/personalized-badge/goldenverba?period=total&units=international_system&left_color=grey&right_color=orange&left_text=pip%20downloads)](https://pypi.org/project/goldenverba/) [![Docker support](https://img.shields.io/badge/Docker_support-%E2%9C%93-4c1?style=flat-square&logo=docker&logoColor=white)](https://docs.docker.com/get-started/) [![Demo](https://img.shields.io/badge/Check%20out%20the%20demo!-yellow?&style=flat-square&logo=react&logoColor=white)](https://verba.weaviate.io/)

欢迎来到 Verba：黄金检索增强生成器（The Golden RAGtriever），这是一款由社区驱动的应用程序，旨在开箱即用地提供一个端到端、流程简化且用户友好的界面用于检索增强生成（RAG）。只需几步简单操作，你就可以轻松探索数据集并提取洞察，既可以在本地使用 Ollama 和 Huggingface，也可以通过 Anthropic、Cohere 和 OpenAI 等 LLM 提供商。本项目由社区构建并为社区服务，请注意它可能不会像其他 Weaviate 生产级应用那样以同等紧迫性进行维护。欢迎随时为项目做出贡献，帮助我们让 Verba 变得更好！<3

```
pip install goldenverba
```

![Demo of Verba](https://github.com/weaviate/Verba/blob/2.0.0/img/verba.gif)

- [Verba](#verba)
  - [🎯 什么是 Verba？](#what-is-verba)
  - [✨ 功能特性](#feature-lists)
- [✨ 快速上手 Verba](#getting-started-with-verba)
- [🔑 API 密钥与环境变量](#api-keys-and-environment-variables)
  - [Weaviate](#weaviate)
  - [Ollama](#ollama)
  - [Unstructured](#unstructured)
  - [AssemblyAI](#assemblyai)
  - [OpenAI](#openai)
  - [HuggingFace](#huggingface)
  - [Groq](#groq)
  - [Novita AI](#novitaai)
- [快速入门：通过 pip 部署](#how-to-deploy-with-pip)
- [快速入门：从源码构建](#how-to-build-from-source)
- [快速入门：使用 Docker 部署](#how-to-install-verba-with-docker)
- [💾 Verba 操作指南](#️verba-walkthrough)
- [💖 开源贡献](#open-source-contribution)
- [🚩 已知问题](#known-issues)
- [❔ 常见问题解答 (FAQ)](#faq)

## 🎯 什么是 Verba？

Verba 是一款完全可定制的个人助手，利用 [检索增强生成（RAG）](https://weaviate.io/rag#:~:text=RAG%20with%20Weaviate,accuracy%20of%20AI%2Dgenerated%20content.) 来查询和交互你的数据，**支持本地运行或通过云端部署**。它可以解答关于你文档的疑问、交叉引用多个数据点，或从现有知识库中获取洞察。Verba 将最先进的 RAG 技术与 Weaviate 的上下文感知数据库相结合。你可以根据具体使用场景，选择不同的 RAG 框架、数据类型、分块与检索技术以及 LLM 提供商。

## 开源精神

**Weaviate** 很荣幸为社区提供这款开源项目。尽管我们力求尽快解决问题，但请理解它可能不会像生产级软件那样保持同等严格的维护标准。我们欢迎并鼓励社区贡献代码，以帮助项目平稳运行。感谢大家积极协助修复开放问题！

### 在这里观看我们的最新 Verba 视频：

[![VIDEO LINK](https://github.com/weaviate/Verba/blob/main/img/thumbnail.png)](https://www.youtube.com/watch?v=2VCy-YjRRhA&t=40s&ab_channel=Weaviate%E2%80%A2VectorDatabase)

## 功能特性列表

| 🤖 模型支持                  | 已实现 | 说明                                             |
| --------------------------------- | ----------- | ------------------------------------------------------- |
| Ollama (例如 Llama3)              | ✅          | 由 Ollama 驱动的本地嵌入与生成模型 |
| HuggingFace (例如 MiniLMEmbedder) | ✅          | 由 Huggingface 驱动的本地嵌入模型           |
| Cohere (例如 Command R+)          | ✅          | Cohere 提供的嵌入与生成模型               |
| Anthropic (例如 Claude Sonnet)   | ✅          | Anthropic 提供的嵌入与生成模型           |
| OpenAI (例如 GPT4)                | ✅          | OpenAI 提供的嵌入与生成模型                |
| Groq (例如 Llama3)                | ✅          | Groq 提供的生成模型（LPU 推理）               |
| Novita AI (例如 Llama3.3)         | ✅          | Novita AI 提供的生成模型                          |
| Upstage (例如 Solar)              | ✅          | Upstage 提供的嵌入与生成模型              |

| 🤖 向量嵌入（Embedding）支持 | 已实现 | 说明                              |
| -------------------- | ----------- | ---------------------------------------- |
| Weaviate             | ✅          | 由 Weaviate 驱动的嵌入模型     |
| Ollama               | ✅          | 由 Ollama 驱动的本地嵌入模型 |
| SentenceTransformers | ✅          | 由 Huggingface 驱动的嵌入模型  |
| Cohere               | ✅          | Cohere 提供的嵌入模型               |
| VoyageAI             | ✅          | VoyageAI 提供的嵌入模型             |
| OpenAI               | ✅          | OpenAI 提供的嵌入模型               |
| Upstage              | ✅          | Upstage 提供的嵌入模型              |

| 📁 数据支持                                          | 已实现 | 说明                                    |
| -------------------------------------------------------- | ----------- | ---------------------------------------------- |
| [UnstructuredIO](https://docs.unstructured.io/welcome)   | ✅          | 通过 Unstructured 导入数据               |
| [Firecrawl](https://www.firecrawl.dev/)                  | ✅          | 通过 Firecrawl 抓取和爬取 URL         |
| [UpstageDocumentParse](https://upstage.ai/)              | ✅          | 通过 Upstage Document AI 解析文档    |
| PDF 导入                                            | ✅          | 将 PDF 导入 Verba                          |
| GitHub & GitLab                                          | ✅          | 从 Github 和 GitLab 导入文件            |
| CSV/XLSX 导入                                       | ✅          | 将表格数据导入 Verba                   |
| .DOCX                                                    | ✅          | 导入 `.docx` 文件                             |
| 多模态 (使用 [AssemblyAI](https://assemblyai.com)) | ✅          | 通过 AssemblyAI 导入并转录音频             |

| ✨ RAG 功能特性         | 状态     | 说明                                                               |
| ----------------------- | --------------- | ------------------------------------------------------------------------- |
| 混合搜索           | ✅              | 语义搜索与关键词搜索相结合                              |
| 自动补全建议 | ✅              | Verba 提供自动补全功能                                             |
| 过滤               | ✅              | 在执行 RAG 前应用过滤器（例如文档、文档类型等） |
| 自定义元数据   | ✅              | 自由控制元数据                                                |
| 异步导入         | ✅              | 异步导入数据以加快处理速度                        |
| 高级查询       | 计划中 ⏱️      | 基于 LLM 评估的任务委派                                   |
| 重排序               | 计划中 ⏱️      | 根据上下文对结果进行重排以提升效果                      |
| RAG 评估          | 计划中 ⏱️      | 用于评估 RAG 管道的界面                                    |
| Agent 式 RAG             | 不在规划范围内 ❌ | Agent 式 RAG 管道                                                     |
| Graph RAG               | 不在规划范围内 ❌ | 基于图的 RAG 管道                                                 |

| 🗡️ 分块（Chunking）技术 | 已实现 | 说明                                             |
| ---------------------- | ----------- | ------------------------------------------------------- |
| Token                  | ✅          | 按 Token 分块，由 [spaCy](https://spacy.io/) 驱动    |
| Sentence               | ✅          | 按句子分块，由 [spaCy](https://spacy.io/) 驱动 |
| Semantic               | ✅          | 基于语义相似度进行分块和分组         |
| Recursive              | ✅          | 根据规则递归地对数据进行分块                   |
| HTML                   | ✅          | 对 HTML 文件进行分块                                        |
| Markdown               | ✅          | 对 Markdown 文件进行分块                                    |
| Code                   | ✅          | 对代码文件进行分块                                        |
| JSON                   | ✅          | 对 JSON 文件进行分块                                        |

| 🆒 额外亮点            | 状态     | 说明                                             |
| ------------------------ | --------------- | ------------------------------------------------------- |
| Docker 支持           | ✅              | Verba 可通过 Docker 部署                          |
| 可定制前端    | ✅              | Verba 的前端完全可通过配置进行自定义 |
| 向量查看器            | ✅              | 以 3D 形式可视化你的数据                               |
| 多用户协作 | 不在规划范围内 ❌ | Verba 中的多用户协作                       |

| 🤝 RAG 库支持 | 已实现 | 说明                        |
| ---------------- | ----------- | ---------------------------------- |
| LangChain        | ✅          | 实现 LangChain RAG 管道  |
| Haystack         | 计划中 ⏱️  | 实现 Haystack RAG 管道   |
| LlamaIndex       | 计划中 ⏱️  | 实现 LlamaIndex RAG 管道 |

> 缺少某项功能？欢迎创建新的 Issue 或 Discussion，分享你的想法！

![Showcase of Verba](https://github.com/weaviate/Verba/blob/2.0.0/img/verba_screen.png)

---

# 🚀 快速上手 Verba

Verba 提供三种部署方式：

- 通过 pip 安装

```
pip install goldenverba
```

- 从源码构建

```
git clone https://github.com/weaviate/Verba

pip install -e .
```

- 使用 Docker 进行部署

**前置要求**：如果你不使用 Docker，请确保你的系统已安装 `Python >=3.10.0,<3.13.0`。

```
git clone https://github.com/weaviate/Verba

docker compose --env-file <your-env-file> up -d --build
```

如果你对 Python 和虚拟环境不熟悉，请阅读 [python 教程指南](./PYTHON_TUTORIAL.md)。

# 🔑 API 密钥与环境变量

你可以在 Verba 前端界面中设置所有 API 密钥，但为了简化你的操作，我们也可以准备一个 `.env` 文件，Verba 会自动从中读取密钥。在你打算启动 Verba 的目录下创建一个 `.env` 文件。你可以在 [goldenverba](./goldenverba/.env.example) 目录中找到 `.env.example` 示例文件。

> 请确保仅设置你计划使用的环境变量，缺失或值不正确的环境变量可能会导致错误。

以下是你可能需要的 API 密钥和环境变量的完整列表：

| 环境变量   | 值                                                      | 说明                                                                                                                   |
| ---------------------- | ---------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| WEAVIATE_URL_VERBA     | 托管的 Weaviate 集群地址                        | 连接你的 [WCS](https://console.weaviate.cloud/) 集群                                                                |
| WEAVIATE_API_KEY_VERBA | 托管的 Weaviate 集群 API 凭证            | 连接你的 [WCS](https://console.weaviate.cloud/) 集群                                                                |
| ANTHROPIC_API_KEY      | Anthropic API 密钥                                     | 获取 [Anthropic](https://www.anthropic.com/) 模型访问权限                                                                  |
| OPENAI_API_KEY         | OpenAI API 密钥                                            | 获取 [OpenAI](https://openai.com/) 模型访问权限                                                                            |
| OPENAI_EMBED_API_KEY         | OpenAI API 密钥                                            | 为向量嵌入使用不同的端点                                                                            |
| OPENAI_BASE_URL        | OpenAI 实例地址                                     | 模型                                                                                                                        |
| OPENAI_EMBED_BASE_URL         | OpenAI 实例地址                                     | 为向量嵌入使用不同的端点                                                                                                                        |
| OPENAI_MODEL        | 选择 OpenAI 作为生成器时要使用的模型名称                                    | 默认值：返回的列表中的第一个模型                                                                                                                        |
| OPENAI_EMBED_MODEL        | 选择 OpenAI 作为嵌入器时要使用的 OpenAI 向量嵌入模型名称                                    | 默认值：`text-embedding-3-small`                                                                                                                        |
| OPENAI_CUSTOM_EMBED        | `true` \| `false`                                    | 允许 Verba 识别自定义向量嵌入模型名称（不仅限于 OpenAI 官方模型）                                                                            |
| COHERE_API_KEY         | API 密钥                                               | 获取 [Cohere](https://cohere.com/) 模型访问权限                                                                            |
| GROQ_API_KEY           | Groq API 密钥                                          | 获取 [Groq](https://groq.com/) 模型访问权限                                                                                |
| NOVITA_API_KEY         | Novita AI API 密钥                                        | 获取 [Novita AI](https://novita.ai?utm_source=github_verba&utm_medium=github_readme&utm_campaign=github_link) 模型访问权限 |
| OLLAMA_URL             | Ollama 实例地址（例如 http://localhost:11434 ) | 获取 [Ollama](https://ollama.com/) 模型访问权限                                                                            |
| UNSTRUCTURED_API_KEY   | API 密钥                                               | 获取 [Unstructured](https://docs.unstructured.io/welcome) 数据导入权限                                             |
| UNSTRUCTURED_API_URL   | Unstructured 实例地址                               | 获取 [Unstructured](https://docs.unstructured.io/welcome) 数据导入权限                                             |
| ASSEMBLYAI_API_KEY     | API 密钥                                               | 获取 [AssemblyAI](https://assemblyai.com) 数据导入权限                                                             |
| GITHUB_TOKEN           | GitHub Token                                          | 通过 GitHub 获取数据导入权限                                                                                       |
| GITLAB_TOKEN           | GitLab Token                                          | 通过 GitLab 获取数据导入权限                                                                                       |
| FIRECRAWL_API_KEY      | Firecrawl API 密钥                                     | 通过 Firecrawl 获取数据导入权限                                                                                    |
| VOYAGE_API_KEY         | VoyageAI API 密钥                                      | 通过 VoyageAI 获取向量嵌入模型访问权限                                                                                   |
| EMBEDDING_SERVICE_URL  | 你的向量嵌入服务实例地址                     | 通过 [Weaviate Embedding Service](https://weaviate.io/developers/wcs/embeddings) 获取向量嵌入模型访问权限                |
| EMBEDDING_SERVICE_KEY  | 你的向量嵌入服务密钥                                 | 通过 [Weaviate Embedding Service](https://weaviate.io/developers/wcs/embeddings) 获取向量嵌入模型访问权限                |
| UPSTAGE_API_KEY        | Upstage API 密钥                                       | 获取 [Upstage](https://upstage.ai/) 模型访问权限                                                                           |
| UPSTAGE_BASE_URL       | Upstage 实例地址                                    | 模型                                                                                                                        |
| DEFAULT_DEPLOYMENT     | Local, Weaviate, Custom, Docker                            | 设置默认部署模式                                                                                               |
| SYSYEM_MESSAGE_PROMPT     | Prompt 文本值                            | 默认值以 "You are Verba, a chatbot for..." 开头                                                                                               |
| OLLAMA_MODEL           | Ollama 模型                                          | 设置要使用的默认 Ollama 模型                                                                                           |
| OLLAMA_EMBED_MODEL     | Ollama 向量嵌入模型                                | 设置要使用的默认 Ollama 向量嵌入模型                                                                                 |

![API Keys in Verba](https://github.com/weaviate/Verba/blob/2.0.0/img/api_screen.png)

## Weaviate

Verba 根据你的需求提供连接 Weaviate 实例的灵活方式。你有三种选择：

1. **本地部署**：使用内置（Embedded）Weaviate，它在你的设备上本地运行（Windows 除外，请选择 Docker/云部署）
2. **Docker 部署**：当你运行 Verba 的 Dockerfile 时选择此项。
3. **云部署**：使用托管在 WCD 上的现有 Weaviate 实例来运行 Verba

**💻 Weaviate 内置模式（Embedded）**
内置 Weaviate 是一种部署模型，它从你的应用代码中启动 Weaviate 实例，而不是依赖独立的服务器安装。当你在 `本地部署` 模式下运行 Verba 时，它会在后台设置并管理内置 Weaviate。请注意，Weaviate 内置模式在 Windows 上不受支持，且目前处于实验阶段，可能会引发意外错误。我们建议使用 Docker 部署或云部署。你可以在此处了解更多关于 Weaviate 内置模式的信息 [here](https://weaviate.io/developers/weaviate/installation/embedded)。

**🌩️ Weaviate 云部署（WCD）**

如果你偏好云端解决方案，Weaviate Cloud (WCD) 提供可扩展的托管环境。请按照 [Weaviate 集群设置指南](https://weaviate.io/developers/wcs/guides/create-instance) 了解如何设置云集群并获取 API 密钥。

**🐳 Docker 部署**
另一种本地替代方案是使用 Docker 部署 Weaviate。更多详情，请参阅下方的 [使用 Docker 安装 Verba](#how-to-install-verba-with-docker) 章节。

![Deployment in Verba](https://github.com/weaviate/Verba/blob/2.0.0/img/verba_deployment.png)

**⚙️ 自定义 Weaviate 部署**

如果你自行托管 Weaviate，可以在 Verba 中使用 `Custom`（自定义）部署选项。这将允许你指定自己的 Weaviate 实例的 URL、端口和 API 密钥。

## Ollama

Verba 支持 Ollama 模型。请在你的设备上下载并安装 Ollama (https://ollama.com/download)。确保使用 `ollama run <model>` 安装了你所偏好的 LLM。

已测试 `llama3`、`llama3:70b` 和 `mistral`。较大的模型通常表现更好，但需要更多的计算资源。

> 请确保 Ollama 服务器在后台运行，并且不要使用不同的 ollama 模型导入文档，因为它们的向量维度可能不同，从而导致错误

你可以通过运行以下命令进行验证：

```
ollama run llama3
```

## Unstructured

Verba 支持通过 Unstructured IO 导入文档（例如纯文本、.pdf、.csv 等）。要使用此功能，你需要设置 `UNSTRUCTURED_API_KEY` 和 `UNSTRUCTURED_API_URL` 环境变量。你可以从 [Unstructured](https://unstructured.io/) 获取。

> `UNSTRUCTURED_API_URL` 默认设置为 `https://api.unstructuredapp.io/general/v0/general`

## AssemblyAI

Verba 支持通过 AssemblyAI 导入文档（音频文件或视频文件中的音频）。要使用此功能，你需要设置 `ASSEMBLYAI_API_KEY` 环境变量。你可以从 [AssemblyAI](https://assemblyai.com) 获取。

## OpenAI

Verba 支持 OpenAI 模型，如 Ada、GPT3 和 GPT4。要使用它们，你需要指定 `OPENAI_API_KEY` 环境变量。你可以从 [OpenAI](https://openai.com/) 获取。

你也可以添加 `OPENAI_BASE_URL` 来使用代理服务器，例如 LiteLLM (https://github.com/BerriAI/litellm)：

```
OPENAI_BASE_URL=YOUR-OPENAI_BASE_URL
```
### OpenAI 向量嵌入（Embedding）

若要为向量嵌入指定不同的端点，请设置 `OPENAI_EMBED_API_KEY` 和 `OPENAI_EMBED_BASE_URL` 环境变量。

如果你使用自定义的 OpenAI 服务器进行嵌入处理，请确保设置 `OPENAI_CUSTOM_EMBED=true`。这将允许 Verba 识别自定义的向量嵌入模型名称（而不仅仅是默认的 OpenAI 模型）。

## HuggingFace

如果你想使用 HuggingFace 功能，请确保安装正确的 Verba 包。它将安装使用本地向量嵌入模型所需的依赖包。请注意，启动时 Verba 会自动下载并安装向量嵌入模型。

```bash
pip install goldenverba[huggingface]

or

pip install `.[huggingface]`
```

> 如果你使用的是 Docker，请相应地修改 `Dockerfile`。目前无法直接从 Docker Hub 拉取镜像后安装自定义 Verba 版本，你需要从源码构建 Docker 部署并提前修改 `Dockerfile`。

## Groq

要使用 Groq LPU 作为生成引擎，你需要从 [Groq](https://console.groq.com/keys) 获取 API 密钥。

> 虽然你可以在 Verba 启动后通过图形界面提供该密钥，但建议在启动应用程序前将其指定为 `GROQ_API_KEY` 环境变量。  
> 这将允许你在最新的可用模型列表中选择生成模型。

## Novita

要使用 Novita AI 作为生成引擎，你需要从 [Novita AI](https://novita.ai/settings/key-management?utm_source=github_verba&utm_medium=github_readme&utm_campaign=github_link) 获取 API 密钥。

# 🛠️ 通过 pip 部署

`Python >=3.10.0`

1. （非常重要）**初始化新的 Python 虚拟环境**

```
python3 -m virtualenv venv
source venv/bin/activate
```

2. **安装 Verba**

```
pip install goldenverba
```

3. **启动 Verba**

```
verba start
```

> 你可以通过参数指定 `--port` 和 `--host`

4. **访问 Verba**

```
访问 localhost:8000
```

5. （可选）**创建 `.env` 文件并添加环境变量**

# 🛠️ 从源码构建

1. **克隆 Verba 仓库**

```
git clone https://github.com/weaviate/Verba.git
```

2. **初始化新的 Python 虚拟环境**

```
python3 -m virtualenv venv
source venv/bin/activate
```

3. **安装 Verba**

```
pip install -e .
```

4. **启动 Verba**

```
verba start
```

> 你可以通过参数指定 `--port` 和 `--host`

5. **访问 Verba**

```
访问 localhost:8000
```

6. （可选）**创建 `.env` 文件并添加环境变量**

# 🐳 使用 Docker 安装 Verba

Docker 是一套平台即服务（PaaS）产品，它利用操作系统级别的虚拟化技术来分发以容器为单位的软件。要开始通过 Docker 部署 Verba，请按照以下步骤操作。如需更详细的 Docker 使用说明，请参阅 [Docker 教程](https://docker-curriculum.com/)。

你可以使用 `docker pull semitechnologies/verba` 拉取最新的 Verba Docker 镜像。请注意，直接从 Docker Hub 拉取仅能安装不包含额外包（如 `HuggingFace`）的默认版 Verba。如果你想同时使用 Docker 和 `HuggingFace`，请按照以下步骤操作。

若要自行构建镜像，你可以克隆 Verba 仓库并在 Verba 目录下运行 `docker build -t verba .`。

0. **克隆 Verba 仓库**
   确保你的系统已安装 Git。然后打开终端或命令提示符，运行以下命令克隆 Verba 仓库：

```
git clone https://github.com/weaviate/Verba.git
```

1. **设置必要的环境变量**
   请确保在 `.env` 文件中设置了所需的环境变量。你可以在 [API 密钥部分](#api-keys) 了解如何配置它们。

2. **调整 docker-compose 文件**
   你可以使用 `docker-compose.yml` 为 `verba` 服务添加必要的环境变量，也可以调整 Weaviate Docker 设置以启用身份验证或更改数据库实例的其他参数。你可以在我们的 [docker-compose 文档](https://weaviate.io/developers/weaviate/installation/docker-compose) 中了解更多关于 Weaviate 配置的信息。你也可以取消注释 `ollama` 服务以便在同一 docker compose 中使用 Ollama。

> 请确保仅添加你真正需要使用的环境变量。

3. **使用 Docker 部署**
   安装好 Docker 并克隆 Verba 仓库后，在终端或命令提示符中导航到包含 Docker Compose 文件的目录。运行以下命令以后台模式启动 Verba 应用：

```bash

docker compose up -d

```

```bash

docker compose --env-file goldenverba/.env up -d --build

```

该命令将下载必要的 Docker 镜像，创建容器并启动 Verba。
请记住，使用此方法必须先在系统上安装 Docker。如需安装说明和更多详细信息，请访问官方 Docker 文档。

4. **访问 Verba**

- 你可以在 `localhost:8080` 访问你的本地 Weaviate 实例

- 你可以在 `localhost:8000` 访问 Verba 前端界面

如果你希望 Docker 实例安装特定版本的 Verba，可以编辑 `Dockerfile` 并更改安装行。

```
RUN pip install -e '.'
```

## 💾 Verba 操作指南

### 选择部署方式

你看到的第一个界面是部署设置页。你可以在此选择 `Local`（本地）、`Docker`、`Weaviate Cloud`（云）或 `Custom`（自定义）部署模式。`Local` 模式在底层使用 Weaviate Embedded，它会在后台初始化一个 Weaviate 实例。`Docker` 模式使用运行在同一 Docker 网络中的独立 Weaviate 实例。`Weaviate Cloud` 模式使用托管在 WCS 上的实例。`Custom` 模式允许你指定自己的 Weaviate 实例 URL、端口和 API 密钥。

你也可以通过设置 `DEFAULT_DEPLOYMENT` 环境变量为 `Local`、`Docker`、`Weaviate` 或 `Custom` 来跳过此步骤。

### 导入数据

首先需要添加你的数据。你可以点击 `Import Data`（导入数据），然后选择 `Add Files`、`Add Directory` 或 `Add URL` 选项卡来添加文件。在这里你可以添加所有想要导入的文件。
随后可通过选中文件并点击 `Overview` 或 `Configure` 选项卡，对每个文件进行单独配置。
![Demo of Verba](https://github.com/weaviate/Verba/blob/2.0.0/img/verba_data.png)

### 查询数据

导入数据后，你可以使用 `Chat`（聊天）页面提出相关问题。系统将返回与你的问题语义相关的文本块，并由你选择的模型生成答案。你可以在 `Config`（配置）选项卡中配置 RAG 管道。

![Demo of Verba](https://github.com/weaviate/Verba/blob/2.0.0/img/verba_rag.png)

## 💖 开源贡献

我们非常欢迎你的贡献！如果你有任何想法、反馈，或发现了问题与 Bug，请随时提交 Issue 和 PR！在贡献之前，请先阅读 [贡献指南](./CONTRIBUTING.md)。如需任何帮助，请访问我们的 [Weaviate 社区论坛](https://forum.weaviate.io/)。

### 项目架构

你可以在 [技术文档](./TECHNICAL.md) 和 [前端文档](./FRONTEND.md) 中了解更多关于 Verba 的架构与实现细节。建议在贡献代码前查阅这些文档。

## 🚩 已知问题

- **Weaviate Embedded（内置模式）** 目前在 Windows 上尚不可用
  - 将在未来版本中修复，在此之前请使用 Docker 或 WCS 部署

## ❔ 常见问题解答 (FAQ)

- **我可以使用 Weaviate 实例中的历史数据吗？**

  - 目前不行。Verba 要求数据以特定格式存在才能正常工作。截至目前，只能通过 Verba UI 导入数据来实现此功能。

- **Verba 支持多语言吗？**

  - 这取决于你选择的向量嵌入和生成模型是否支持多语言数据处理。

- **我可以在 Verba Docker 中使用自己的 Ollama Server 吗？**

  - 可以！请确保 URL 设置为：`OLLAMA_URL=http://host.docker.internal:11434`
  - 如果你在 Linux 上运行，可能需要获取 Ollama 服务器的 IP 网关地址：`OLLAMA_URL="http://YOUR-IP-OF-OLLAMA:11434"`

- **如何清除 Weaviate Embedded（内置模式）的存储？**

  - 你将在以下路径找到已存储的数据：`~/.local/share/weaviate`

- **如何指定端口？**

  - 你可以使用 `verba start --port 9000 --host 0.0.0.0` 命令来指定端口和主机。

- **多个用户可以同时使用 Verba 吗？支持基于角色的访问控制（RBAC）吗？**

  - Verba 目前专为单用户设计并优化。短期内暂无计划支持多用户或基于角色的访问控制。

- **Verba 是否提供可供外部调用的 API 端点？**

  - 目前没有。Verba 尚未提供任何用于与应用程序交互的实用 API 端点。当前的 FastAPI 设置已针对前端和后端之间的内部通信进行了优化，不建议将其用作外部 API 端点。团队有计划添加用户友好的...（原文截断）

- **如何连接自定义 OpenAI Server？**

  - 在 `.env` 文件中设置你的自定义 OpenAI API 密钥和 URL，这将允许 Verba 启动并从你的自定义 OpenAI Server 获取模型列表。`OPENAI_BASE_URL` 默认设置为 `https://api.openai.com/v1`。
  - 你还可以通过配置 `OPENAI_EMBED_API_KEY` 和 `OPENAI_EMBED_BASE_URL` 环境变量，并设置 `OPENAI_CUSTOM_EMBED=true` 来为向量嵌入指定不同的端点。更多详情见 [OpenAI 向量嵌入](#openai-embeddings)。

- **如何向 Verba 上传自定义 JSON 文件？**
  - 目前 Verba 不支持自定义 JSON 结构。相反，整个 JSON 内容将被直接转储到 Verba 文档的 content 字段中。你可以在技术文档 [此处](./TECHNICAL.md) 了解更多关于 Verba JSON 结构的信息。
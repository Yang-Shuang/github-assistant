![DeepSearcher](./assets/pic/logo.png)

<div align="center">
  
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![DeepWiki](https://img.shields.io/badge/DeepWiki-AI%20Docs-orange.svg)](https://deepwiki.com/zilliztech/deep-searcher)
[![Twitter](https://img.shields.io/twitter/url/https/twitter.com/zilliz_universe.svg?style=social&label=Follow%20%40Zilliz)](https://twitter.com/zilliz_universe)
<a href="https://discord.gg/mK3R95yE5"><img height="20" src="https://img.shields.io/badge/Discord-%235865F2.svg?style=for-the-badge&logo=discord&logoColor=white" alt="discord"/></a>

</div>

---

DeepSearcher 结合了前沿的大语言模型（LLM）（如 OpenAI o3、Qwen3、DeepSeek、Grok 4、Claude 4 Sonnet、Llama 4、QwQ 等）与向量数据库（如 Milvus、Zilliz Cloud 等），能够基于私有数据进行检索、评估与推理，提供高准确度的答案和全面的报告。本项目适用于企业知识管理、智能问答系统及信息检索等场景。

![Architecture](./assets/pic/deep-searcher-arch.png)

## 🚀 核心特性

- **私有数据检索**：在确保数据安全的前提下，最大化利用企业内部数据。必要时可整合在线内容以获取更精准的答案。
- **向量数据库管理**：支持 Milvus 等向量数据库，允许进行数据分区以实现高效检索。
- **灵活的嵌入模型选项**：兼容多种 Embedding（文本嵌入）模型，便于按需选择。
- **多模型支持**：支持 DeepSeek、OpenAI 等主流大语言模型进行智能问答与内容生成。
- **文档加载器**：支持本地文件加载，网页爬取功能正在开发中。

---

## 🎉 演示效果
![demo](./assets/pic/demo.gif)


## 📖 快速开始

### 安装
你可以通过以下任一方式安装 DeepSearcher：

#### 方式一：使用 pip
创建并激活虚拟环境（推荐使用 Python 3.10）。
```bash
python -m venv .venv
source .venv/bin/activate
```
安装 DeepSearcher
```bash
pip install deepsearcher
```

如需可选依赖，例如 Ollama：
```bash
pip install "deepsearcher[ollama]"
```

#### 方式二：开发模式安装
我们推荐使用 [uv](https://github.com/astral-sh/uv) 进行更快、更可靠的安装。请按照[官方安装指南](https://docs.astral.sh/uv/getting-started/installation/)完成安装。

克隆仓库并进入项目目录：
```shell
git clone https://github.com/zilliztech/deep-searcher.git && cd deep-searcher
```
同步并安装依赖项：
```shell
uv sync
source .venv/bin/activate
```

有关更详细的开发环境配置及可选依赖安装说明，请参阅 [CONTRIBUTING.md](CONTRIBUTING.md#development-environment-setup-with-uv)。

### 快速入门示例

运行此快速入门示例前，请确保在环境变量中配置了 `OPENAI_API_KEY`。如果你在配置中更换了其他大语言模型（LLM），请提前准备好对应的 API Key。

```python
from deepsearcher.configuration import Configuration, init_config
from deepsearcher.online_query import query

config = Configuration()

# 在此自定义你的配置，
# 更多配置说明请参阅下方的“详细配置”部分。
config.set_provider_config("llm", "OpenAI", {"model": "o1-mini"})
config.set_provider_config("embedding", "OpenAIEmbedding", {"model": "text-embedding-ada-002"})
init_config(config = config)

# 加载你的本地数据
from deepsearcher.offline_loading import load_from_local_files
load_from_local_files(paths_or_directory=your_local_path)

# （可选）从网页爬取（需要配置 `FIRECRAWL_API_KEY` 环境变量）
from deepsearcher.offline_loading import load_from_website
load_from_website(urls=website_url)

# 查询
result = query("Write a report about xxx.") # 在此输入你的问题
```

### 详细配置说明：
#### LLM（大语言模型）配置

<pre><code>config.set_provider_config("llm", "(LLMName)", "(Arguments dict)")</code></pre>
<p>"LLMName" 可以是以下之一：["DeepSeek", "OpenAI", "XAI", "SiliconFlow", "Aliyun", "PPIO", "TogetherAI", "Gemini", "Ollama", "Novita", "Jiekou.AI"]</p>
<p>"Arguments dict" 是一个包含该 LLM 类所需参数的字典。</p>

<details>
  <summary>示例（OpenAI）</summary>
    <p>请确保已准备好环境变量 <code>OPENAI_API_KEY</code>。</p>
    <pre><code>config.set_provider_config("llm", "OpenAI", {"model": "o1-mini"})</code></pre>
    <p>关于 OpenAI 模型的更多详情：https://platform.openai.com/docs/models </p>
</details>

<details>
  <summary>示例（阿里云百炼的 Qwen3）</summary>
    <p>请确保已准备好环境变量 <code>DASHSCOPE_API_KEY</code>。</p>
    <pre><code>config.set_provider_config("llm", "Aliyun", {"model": "qwen-plus-latest"})</code></pre>
    <p>关于阿里云百炼模型的更多详情：https://bailian.console.aliyun.com </p>
</details>


<details>
  <summary>示例（OpenRouter 的 Qwen3）</summary>
    <pre><code>config.set_provider_config("llm", "OpenAI", {"model": "qwen/qwen3-235b-a22b:free", "base_url": "https://openrouter.ai/api/v1", "api_key": "OPENROUTER_API_KEY"})</code></pre>
    <p>关于 OpenRouter 模型的更多详情：https://openrouter.ai/qwen/qwen3-235b-a22b:free </p>
</details>


<details>
  <summary>示例（DeepSeek 官方）</summary>
    <p>请确保已准备好环境变量 <code>DEEPSEEK_API_KEY</code>。</p>
    <pre><code>config.set_provider_config("llm", "DeepSeek", {"model": "deepseek-reasoner"})</code></pre>
    <p>关于 DeepSeek 的更多详情：https://api-docs.deepseek.com/ </p>
</details>

<details>
  <summary>示例（SiliconFlow 的 DeepSeek）</summary>
    <p>请确保已准备好环境变量 <code>SILICONFLOW_API_KEY</code>。</p>
    <pre><code>config.set_provider_config("llm", "SiliconFlow", {"model": "deepseek-ai/DeepSeek-R1"})</code></pre>
    <p>关于 SiliconFlow 的更多详情：https://docs.siliconflow.cn/quickstart </p>
</details>

<details>
  <summary>示例（TogetherAI 的 DeepSeek）</summary>
    <p>请确保已准备好环境变量 <code>TOGETHER_API_KEY</code>。</p>
    对于 deepseek R1：
    <pre><code>config.set_provider_config("llm", "TogetherAI", {"model": "deepseek-ai/DeepSeek-R1"})</code></pre>
    对于 Llama 4：
    <pre><code>config.set_provider_config("llm", "TogetherAI", {"model": "meta-llama/Llama-4-Scout-17B-16E-Instruct"})</code></pre>
    <p>运行前你需要安装 together，请执行：<code>pip install together</code>。关于 TogetherAI 的更多详情：https://www.together.ai/ </p>
</details>

<details>
  <summary>示例（XAI Grok）</summary>
    <p>请确保已准备好环境变量 <code>XAI_API_KEY</code>。</p>
    <pre><code>config.set_provider_config("llm", "XAI", {"model": "grok-4-0709"})</code></pre>
    <p>关于 XAI Grok 的更多详情：https://docs.x.ai/docs/overview#featured-models </p>
</details>

<details>
  <summary>示例（Claude）</summary>
    <p>请确保已准备好环境变量 <code>ANTHROPIC_API_KEY</code>。</p>
    <pre><code>config.set_provider_config("llm", "Anthropic", {"model": "claude-sonnet-4-0"})</code></pre>
    <p>关于 Anthropic Claude 的更多详情：https://docs.anthropic.com/en/home </p>
</details>

<details>
  <summary>示例（Google Gemini）</summary>
    <p>请确保已准备好环境变量 <code>GEMINI_API_KEY</code>。</p>
    <pre><code>config.set_provider_config('llm', 'Gemini', { 'model': 'gemini-2.0-flash' })</code></pre>
    <p>运行前你需要安装 gemini，请执行：<code>pip install google-genai</code>。关于 Gemini 的更多详情：https://ai.google.dev/gemini-api/docs </p>
</details>

<details>
  <summary>示例（PPIO 的 DeepSeek）</summary>
    <p>请确保已准备好环境变量 <code>PPIO_API_KEY</code>。你可以在此处创建 API Key：<a href="https://ppinfra.com/settings/key-management?utm_source=github_deep-searcher">点击这里</a>。</p>
    <pre><code>config.set_provider_config("llm", "PPIO", {"model": "deepseek/deepseek-r1-turbo"})</code></pre>
    <p>关于 PPIO 的更多详情：https://ppinfra.com/docs/get-started/quickstart.html?utm_source=github_deep-searcher </p>
</details>

<details>
  <summary>示例（Jiekou.AI 的 Claude Sonnet 4.5）</summary>
    <p>请确保已准备好环境变量 <code>JIEKOU_API_KEY</code>。你可以在此处创建 API Key：<a href="https://jiekou.ai/settings/key-management?utm_source=github_deep-searcher">点击这里</a>。</p>
    <pre><code>config.set_provider_config("llm", "JiekouAI", {"model": "claude-sonnet-4-5-20250929"})</code></pre>
    <p>关于 Jiekou.AI 的更多详情：https://docs.jiekou.ai/docs/support/quickstart?utm_source=github_deep-searcher </p>
</details>

<details>
  <summary>示例（Ollama）</summary>
  <p>请按照<a href="https://github.com/jmorganca/ollama">这些说明</a>设置并运行本地 Ollama 实例：</p>
  <p><a href="https://ollama.ai/download">下载</a>并将 Ollama 安装到支持的平台（包括 Windows Subsystem for Linux / WSL）。</p>
  <p>通过<a href="https://ollama.ai/library">模型库</a>查看可用模型列表。</p>
  <p>通过 <code>ollama pull &lt;name-of-model&gt;</code> 获取可用的 LLM 模型。</p>
  <p>示例：<code>ollama pull qwen3</code></p>
  <p>要直接从命令行与模型对话，请使用 <code>ollama run &lt;name-of-model&gt;</code>。</p>
  <p>默认情况下，Ollama 提供 REST API 用于在 <a href="http://localhost:11434">http://localhost:11434</a> 上运行和管理模型。</p>
    <pre><code>config.set_provider_config("llm", "Ollama", {"model": "qwen3"})</code></pre>
</details>

<details>
  <summary>示例（火山引擎 Volcengine）</summary>
    <p>请确保已准备好环境变量 <code>VOLCENGINE_API_KEY</code>。你可以在此处创建 API Key：<a href="https://console.volcengine.com/ark/region:ark+cn-beijing/apiKey">点击这里</a>。</p>
    <pre><code>config.set_provider_config("llm", "Volcengine", {"model": "deepseek-r1-250120"})</code></pre>
    <p>关于 Volcengine 的更多详情：https://www.volcengine.com/docs/82379/1099455?utm_source=github_deep-searcher </p>
</details>

<details>
  <summary>示例（GLM）</summary>
    <p>请确保已准备好环境变量 <code>GLM_API_KEY</code>。</p>
    <pre><code>config.set_provider_config("llm", "GLM", {"model": "glm-4-plus"})</code></pre>
    <p>运行前你需要安装 zhipuai，请执行：<code>pip install zhipuai</code>。关于 GLM 的更多详情：https://bigmodel.cn/dev/welcome </p>
</details>

<details>
  <summary>示例（Amazon Bedrock）</summary>
    <p>请确保已准备好环境变量 <code>AWS_ACCESS_KEY_ID</code> 和 <code>AWS_SECRET_ACCESS_KEY</code>。</p>
    <pre><code>config.set_provider_config("llm", "Bedrock", {"model": "us.deepseek.r1-v1:0"})</code></pre>
    <p>运行前你需要安装 boto3，请执行：<code>pip install boto3</code>。关于 Amazon Bedrock 的更多详情：https://docs.aws.amazon.com/bedrock/ </p>
</details>

<details>
  <summary>示例（IBM watsonx.ai）</summary>
    <p>请确保已准备好环境变量 <code>WATSONX_APIKEY</code>、<code>WATSONX_URL</code> 和 <code>WATSONX_PROJECT_ID</code>。</p>
    <pre><code>config.set_provider_config("llm", "watsonx", {"model": "us.deepseek.r1-v1:0"})</code></pre>
    <p>运行前你需要安装 ibm-watsonx-ai，请执行：<code>pip install ibm-watsonx-ai</code>。关于 IBM watsonx.ai 的更多详情：https://www.ibm.com/products/watsonx-ai/foundation-models </p>
</details>


#### 嵌入模型（Embedding）配置
<pre><code>config.set_provider_config("embedding", "(EmbeddingModelName)", "(Arguments dict)")</code></pre>
<p>"EmbeddingModelName" 可以是以下之一：["MilvusEmbedding", "OpenAIEmbedding", "VoyageEmbedding", "SiliconflowEmbedding", "PPIOEmbedding", "NovitaEmbedding", "JiekouAIEmbedding"]</p>
<p>"Arguments dict" 是一个包含该嵌入模型类所需参数的字典。</p>

<details>
  <summary>示例（OpenAI embedding）</summary>
    <p>请确保已准备好环境变量 <code>OPENAI_API_KEY</code>。</p>
    <pre><code>config.set_provider_config("embedding", "OpenAIEmbedding", {"model": "text-embedding-3-small"})</code></pre>
    <p>关于 OpenAI 模型的更多详情：https://platform.openai.com/docs/guides/embeddings/use-cases </p>
</details>

<details>
  <summary>示例（OpenAI embedding Azure）</summary>
    <p>请确保已准备好环境变量 <code>OPENAI_API_KEY</code>。</p>
    <pre><code>config.set_provider_config("embedding", "OpenAIEmbedding", {
    "model": "text-embedding-ada-002",
    "azure_endpoint": "https://<youraifoundry>.openai.azure.com/",
    "api_version": "2023-05-15"
})</code></pre>
</details>

<details>
  <summary>示例（Pymilvus 内置嵌入模型）</summary>
    <p>使用 Pymilvus 的内置嵌入模型，你可以将模型名称设置为 <code>"default"</code>、<code>"BAAI/bge-base-en-v1.5"</code>、<code>"BAAI/bge-large-en-v1.5"</code>、<code>"jina-embeddings-v3"</code> 等。<br/>
    详见 [milvus_embedding.py](deepsearcher/embedding/milvus_embedding.py)。  </p>
    <pre><code>config.set_provider_config("embedding", "MilvusEmbedding", {"model": "BAAI/bge-base-en-v1.5"})</code></pre>
    <pre><code>config.set_provider_config("embedding", "MilvusEmbedding", {"model": "jina-embeddings-v3"})</code></pre>
    <p>对于 Jina 的嵌入模型，你需要配置<code>JINAAI_API_KEY</code>。</p>
    <p>运行前你需要安装 pymilvus model，请执行：<code>pip install pymilvus.model</code>。关于 Pymilvus 的更多详情：https://milvus.io/docs/embeddings.md </p>

</details>

<details>
  <summary>示例（VoyageAI embedding）</summary>
    <p>请确保已准备好环境变量 <code>VOYAGE_API_KEY</code>。</p>
    <pre><code>config.set_provider_config("embedding", "VoyageEmbedding", {"model": "voyage-3"})</code></pre>
    <p>运行前你需要安装 voyageai，请执行：<code>pip install voyageai</code>。关于 VoyageAI 的更多详情：https://docs.voyageai.com/embeddings/ </p>
</details>

<details>
  <summary>示例（Amazon Bedrock embedding）</summary>
  <pre><code>config.set_provider_config("embedding", "BedrockEmbedding", {"model": "amazon.titan-embed-text-v2:0"})</code></pre>
    <p>运行前你需要安装 boto3，请执行：<code>pip install boto3</code>。关于 Amazon Bedrock 的更多详情：https://docs.aws.amazon.com/bedrock/ </p>
</details>

<details>
  <summary>示例（Novita AI embedding）</summary>
    <p>请确保已准备好环境变量 <code>NOVITA_API_KEY</code>。</p>
    <pre><code>config.set_provider_config("embedding", "NovitaEmbedding", {"model": "baai/bge-m3"})</code></pre>
    <p>关于 Novita AI 的更多详情：https://novita.ai/docs/api-reference/model-apis-llm-create-embeddings?utm_source=github_deep-searcher&utm_medium=github_readme&utm_campaign=link </p>
</details>

<details>
  <summary>示例（Siliconflow embedding）</summary>
    <p>请确保已准备好环境变量 <code>SILICONFLOW_API_KEY</code>。</p>
    <pre><code>config.set_provider_config("embedding", "SiliconflowEmbedding", {"model": "BAAI/bge-m3"})</code></pre>
    <p>关于 Siliconflow 的更多详情：https://docs.siliconflow.cn/en/api-reference/embeddings/create-embeddings </p>
</details>

<details>
  <summary>示例（Volcengine embedding）</summary>
    <p>请确保已准备好环境变量 <code>VOLCENGINE_API_KEY</code>。</p>
    <pre><code>config.set_provider_config("embedding", "VolcengineEmbedding", {"model": "doubao-embedding-text-240515"})</code></pre>
    <p>关于 Volcengine 的更多详情：https://www.volcengine.com/docs/82379/1302003 </p>
</details>

<details>
  <summary>示例（GLM embedding）</summary>
    <p>请确保已准备好环境变量 <code>GLM_API_KEY</code>。</p>
    <pre><code>config.set_provider_config("embedding", "GLMEmbedding", {"model": "embedding-3"})</code></pre>
    <p>运行前你需要安装 zhipuai，请执行：<code>pip install zhipuai</code>。关于 GLM 的更多详情：https://bigmodel.cn/dev/welcome </p>
</details>

<details>
  <summary>示例（Google Gemini embedding）</summary>
    <p>请确保已准备好环境变量 <code>GEMINI_API_KEY</code>。</p>
    <pre><code>config.set_provider_config("embedding", "GeminiEmbedding", {"model": "text-embedding-004"})</code></pre>
    <p>运行前你需要安装 gemini，请执行：<code>pip install google-genai</code>。关于 Gemini 的更多详情：https://ai.google.dev/gemini-api/docs </p>
</details>

<details>
  <summary>示例（Ollama embedding）</summary>
    <pre><code>config.set_provider_config("embedding", "OllamaEmbedding", {"model": "bge-m3"})</code></pre>
    <p>运行前你需要安装 ollama，请执行：<code>pip install ollama</code>。关于 Ollama Python SDK 的更多详情：https://github.com/ollama/ollama-python </p>
</details>

<details>
  <summary>示例（PPIO embedding）</summary>
    <p>请确保已准备好环境变量 <code>PPIO_API_KEY</code>。</p>
    <pre><code>config.set_provider_config("embedding", "PPIOEmbedding", {"model": "baai/bge-m3"})</code></pre>
    <p>关于 PPIO 的更多详情：https://ppinfra.com/docs/get-started/quickstart.html?utm_source=github_deep-searcher </p>
</details>

<details>
  <summary>示例（Jiekou.AI embedding）</summary>
    <p>请确保已准备好环境变量 <code>JIEKOU_API_KEY</code>。</p>
    <pre><code>config.set_provider_config("embedding", "JiekouAIEmbedding", {"model": "qwen/qwen3-embedding-8b"})</code></pre>
    <p>关于 Jiekou.AI 的更多详情：https://docs.jiekou.ai/docs/support/quickstart?utm_source=github_deep-searcher </p>
</details>

<details>
  <summary>示例（FastEmbed embedding）</summary>
    <pre><code>config.set_provider_config("embedding", "FastEmbedEmbedding", {"model": "intfloat/multilingual-e5-large"})</code></pre>
    <p>运行前你需要安装 fastembed，请执行：<code>pip install fastembed</code>。关于 fastembed 的更多详情：https://github.com/qdrant/fastembed </p>
</details>


<details>
  <summary>示例（IBM watsonx.ai embedding）</summary>
    <p>请确保已准备好环境变量 <code>WATSONX_APIKEY</code>、<code>WATSONX_URL</code> 和 <code>WATSONX_PROJECT_ID</code>。</p>
    <pre><code>config.set_provider_config("embedding", "WatsonXEmbedding", {"model": "ibm/slate-125m-english-rtrvr-v2"})</code></pre>
    <pre><code>config.set_provider_config("embedding", "WatsonXEmbedding", {"model": "sentence-transformers/all-minilm-l6-v2"})</code></pre>
    <p>运行前你需要安装 ibm-watsonx-ai，请执行：<code>pip install ibm-watsonx-ai</code>。关于 IBM watsonx.ai 的更多详情：https://www.ibm.com/products/watsonx-ai/foundation-models </p>
</details>

#### 向量数据库配置
<pre><code>config.set_provider_config("vector_db", "(VectorDBName)", "(Arguments dict)")</code></pre>
<p>"VectorDBName" 可以是以下之一：["Milvus"]（正在开发中）</p>
<p>"Arguments dict" 是一个包含该向量数据库类所需参数的字典。</p>

<details>
  <summary>示例（Milvus）</summary>
    <pre><code>config.set_provider_config("vector_db", "Milvus", {"uri": "./milvus.db", "token": ""})</code></pre>
    <p>关于 Milvus 配置的更多详情：</p>
    <ul>
        <li>
            将 <code>uri</code> 设置为本地文件（例如 <code>./milvus.db</code>）是最便捷的方法，因为它会自动利用 <a href="https://milvus.io/docs/milvus_lite.md" target="_blank">Milvus Lite</a> 将所有数据存储在该文件中。
        </li>
    </ul>
    <ul>
      <li>
          如果你拥有大规模数据集，可以使用 <a href="https://milvus.io/docs/quickstart.md" target="_blank">Docker 或 Kubernetes</a> 搭建性能更强的 Milvus 服务器。在此配置下，使用服务器 URI（例如 <code>http://localhost:19530</code>）作为你的 <code>uri</code>。你也可以使用 Milvus 支持的任何其他连接参数，如 <code>host</code>、<code>user</code>、<code>password</code> 或 <code>secure</code>。
        </li>
    </ul>
    <ul>
        <li>
            如果你想使用 <a href="https://zilliz.com/cloud" target="_blank">Zilliz Cloud</a>（Milvus 的全托管云服务），请根据 Zilliz Cloud 中的<a href="https://docs.zilliz.com/docs/on-zilliz-cloud-console#free-cluster-details" 
            target="_blank">公共端点和 API Key</a>调整 <code>uri</code> 和 <code>token</code>。
        </li>
    </ul>

</details>

<details>
  <summary>示例（AZURE AI Search）</summary>
    <pre><code>config.set_provider_config("vector_db", "AzureSearch", {
    "endpoint": "https://<yourazureaisearch>.search.windows.net",
    "index_name": "<yourindex>",
    "api_key": "<yourkey>",
    "vector_field": ""
})</code></pre>
    <p>关于配置的更多详情：</p>

</details>

#### 文件加载器（File Loader）配置
<pre><code>config.set_provider_config("file_loader", "(FileLoaderName)", "(Arguments dict)")</code></pre>
<p>"FileLoaderName" 可以是以下之一：["PDFLoader", "TextLoader", "UnstructuredLoader"]</p>
<p>"Arguments dict" 是一个包含该文件加载器类所需参数的字典。</p>

<details>
  <summary>示例（Unstructured）</summary>
    <p>你可以通过两种方式配置 Unstructured：</p>
    <ul>
      <li>使用 API：设置环境变量 <code>UNSTRUCTURED_API_KEY</code> 和 <code>UNSTRUCTURED_API_URL</code></li>
      <li>不使用 API：直接不设置这些环境变量，即可使用本地处理模式</li>
    </ul>
    <pre><code>config.set_provider_config("file_loader", "UnstructuredLoader", {})</code></pre>
    <ul>
      <li>当前支持的文件类型：["pdf"]（正在开发中）</li>
      <li>安装要求：
        <ul>
          <li>安装 ingest pipeline：<code>pip install unstructured-ingest</code></li>
          <li>所有文档格式：<code>pip install "unstructured[all-docs]"</code></li>
          <li>特定格式（例如仅 PDF）：<code>pip install "unstructured[pdf]"</code></li>
        </ul>
      </li>
      <li>更多信息：
        <ul>
          <li>Unstructured 文档：<a href="https://docs.unstructured.io/ingestion/overview">https://docs.unstructured.io/ingestion/overview</a></li>
          <li>安装指南：<a href="https://docs.unstructured.io/open-source/installation/full-installation">https://docs.unstructured.io/open-source/installation/full-installation</a></li>
        </ul>
      </li>
    </ul>
</details>

<details>
  <summary>示例（Docling）</summary>
    <pre><code>config.set_provider_config("file_loader", "DoclingLoader", {})</code></pre>
    <p>当前支持的文件类型：请参阅 Docling 文档：https://docling-project.github.io/docling/usage/supported_formats/#supported-output-formats </p>
    <p>运行前你需要安装 docling，请执行：<code>pip install docling</code>。关于 Docling 的更多详情：https://docling-project.github.io/docling/ </p>
</details>

#### 网页爬虫（Web Crawler）配置
<pre><code>config.set_provider_config("web_crawler", "(WebCrawlerName)", "(Arguments dict)")</code></pre>
<p>"WebCrawlerName" 可以是以下之一：["FireCrawlCrawler", "Crawl4AICrawler", "JinaCrawler"]</p>
<p>"Arguments dict" 是一个包含该网页爬虫类所需参数的字典。</p>

<details>
  <summary>示例（FireCrawl）</summary>
    <p>请确保已准备好环境变量 <code>FIRECRAWL_API_KEY</code>。</p>
    <pre><code>config.set_provider_config("web_crawler", "FireCrawlCrawler", {})</code></pre>
    <p>关于 FireCrawl 的更多详情：https://docs.firecrawl.dev/introduction </p>
</details>

<details>
  <summary>示例（Crawl4AI）</summary>
    <p>请确保已在你的环境中运行过 <code>crawl4ai-setup</code>。</p>
    <pre><code>config.set_provider_config("web_crawler", "Crawl4AICrawler", {"browser_config": {"headless": True, "verbose": True}})</code></pre>
    <p>运行前你需要安装 crawl4ai，请执行：<code>pip install crawl4ai</code>。关于 Crawl4AI 的更多详情：https://docs.crawl4ai.com/ </p>
</details>

<details>
  <summary>示例（Jina Reader）</summary>
    <p>请确保已准备好环境变量 <code>JINA_API_TOKEN</code> 或 <code>JINAAI_API_KEY</code>。</p>
    <pre><code>config.set_provider_config("web_crawler", "JinaCrawler", {})</code></pre>
    <p>关于 Jina Reader 的更多详情：https://jina.ai/reader/ </p>
</details>

<details>
  <summary>示例（Docling）</summary>
    <pre><code>config.set_provider_config("web_crawler", "DoclingCrawler", {})</code></pre>
    <p>当前支持的文件类型：请参阅 Docling 文档：https://docling-project.github.io/docling/usage/supported_formats/#supported-output-formats </p>
    <p>运行前你需要安装 docling，请执行：<code>pip install docling</code>。关于 Docling 的更多详情：https://docling-project.github.io/docling/ </p>
</details>


### Python CLI 模式
#### 数据加载 (load)
```shell
deepsearcher load "your_local_path_or_url"
# 加载到指定集合中
deepsearcher load "your_local_path_or_url" --collection_name "your_collection_name" --collection_desc "your_collection_description"
```
从本地文件加载示例：
```shell
deepsearcher load "/path/to/your/local/file.pdf"
# 或一次性加载多个文件
deepsearcher load "/path/to/your/local/file1.pdf" "/path/to/your/local/file2.md"
```
从 URL 加载示例（*请在环境变量中设置 `FIRECRAWL_API_KEY`，详见 [FireCrawl](https://docs.firecrawl.dev/introduction)*）：

```shell
deepsearcher load "https://www.wikiwand.com/en/articles/DeepSeek"
```

#### 数据查询 (query)
```shell
deepsearcher query "Write a report about xxx."
```

更多帮助信息
```shell
deepsearcher --help
```
如需查看特定子命令的详细信息，可使用 `deepsearcher [subcommand] --help`。
```shell
deepsearcher load --help
deepsearcher query --help
```

### 部署服务

#### 配置模块

你可以通过修改 [config.yaml](./config.yaml) 来配置所有参数，从而使用默认模块快速搭建系统。例如，在 YAML 文件的 `llm` 部分设置你的 `OPENAI_API_KEY`。

#### 启动服务
主脚本将启动一个默认的 FastAPI 服务（地址为 `localhost:8000`）。

```shell
$ python main.py
```

#### 通过浏览器访问

你可以在浏览器中打开 URL `http://localhost:8000/docs` 访问 Web 服务。点击“尝试运行”（Try it out）按钮，即可填写参数并直接与 API 进行交互。


---

## ❓ 常见问题 (Q&A)

**问题 1**：为什么无法解析大语言模型（LLM）的输出格式？/ 如何选择 LLM？

**解答 1**：小型 LLM 难以遵循提示词生成符合要求的响应，这通常会导致输出格式解析失败。建议优先使用大型推理模型，例如 deepseek-r1-671b、OpenAI o-series、Claude 4 Sonnet 等作为你的 LLM。 

---

**问题 2**： 
`OSError: We couldn't connect to 'https://huggingface.co' to load this file, couldn't find it in the cached files and it looks like GPTCache/paraphrase-albert-small-v2 is not the path to a directory containing a file named config.json.`
请检查你的网络连接，或参阅离线模式运行指南：`https://huggingface.co/docs/transformers/installation#offline-mode`.

**解答 2**：这通常是由于无法访问 Hugging Face 导致的，可能是网络或权限问题。你可以尝试以下两种方法：
1. 如果是网络问题，请设置代理，尝试添加以下环境变量。
```bash
export HF_ENDPOINT=https://hf-mirror.com
```
2. 如果是权限问题，请设置个人令牌，尝试添加以下环境变量。
```bash
export HUGGING_FACE_HUB_TOKEN=xxxx
```

---

**问题 3**：DeepSearcher 无法在 Jupyter Notebook 中运行。

**解答 3**：安装 `nest_asyncio`，并将以下代码块放在你的 Jupyter Notebook 开头。

```
pip install nest_asyncio
```

```
import nest_asyncio
nest_asyncio.apply()
```

---

## 🔧 模块支持

### 🔹 嵌入模型（Embedding）
- [开源嵌入模型](https://milvus.io/docs/embeddings.md)
- [OpenAI](https://platform.openai.com/docs/guides/embeddings/use-cases)（需配置 `OPENAI_API_KEY` 环境变量）
- [VoyageAI](https://docs.voyageai.com/embeddings/)（需配置 `VOYAGE_API_KEY` 环境变量）
- [Amazon Bedrock](https://docs.aws.amazon.com/bedrock/)（需配置 `AWS_ACCESS_KEY_ID` 和 `AWS_SECRET_ACCESS_KEY` 环境变量）
- [FastEmbed](https://qdrant.github.io/fastembed/)
- [PPIO](https://ppinfra.com/model-api/product/llm-api?utm_source=github_deep-searcher)（需配置 `PPIO_API_KEY` 环境变量）
- [Novita AI](https://novita.ai/docs/api-reference/model-apis-llm-create-embeddings?utm_source=github_deep-searcher&utm_medium=github_readme&utm_campaign=link)（需配置 `NOVITA_API_KEY` 环境变量）
- [IBM watsonx.ai](https://www.ibm.com/products/watsonx-ai/foundation-models#ibmembedding)（需配置 `WATSONX_APIKEY`、`WATSONX_URL`、`WATSONX_PROJECT_ID` 环境变量）
- [Jiekou.AI](https://jiekou.ai/?utm_source=github_deep-searcher)（需配置 `JIEKOU_API_KEY` 环境变量）

### 🔹 大语言模型（LLM）支持
- [OpenAI](https://platform.openai.com/docs/models)（需配置 `OPENAI_API_KEY` 环境变量）
- [DeepSeek](https://api-docs.deepseek.com/)（需配置 `DEEPSEEK_API_KEY` 环境变量）
- [XAI Grok](https://x.ai/api)（需配置 `XAI_API_KEY` 环境变量）
- [Anthropic Claude](https://docs.anthropic.com/en/home)（需配置 `ANTHROPIC_API_KEY` 环境变量）
- [SiliconFlow 推理服务](https://docs.siliconflow.cn/en/userguide/introduction)（需配置 `SILICONFLOW_API_KEY` 环境变量）
- [PPIO](https://ppinfra.com/model-api/product/llm-api?utm_source=github_deep-searcher)（需配置 `PPIO_API_KEY` 环境变量）
- [TogetherAI 推理服务](https://docs.together.ai/docs/introduction)（需配置 `TOGETHER_API_KEY` 环境变量）
- [Google Gemini](https://ai.google.dev/gemini-api/docs)（需配置 `GEMINI_API_KEY` 环境变量）
- [SambaNova Cloud 推理服务](https://docs.together.ai/docs/introduction)（需配置 `SAMBANOVA_API_KEY` 环境变量）
- [Ollama](https://ollama.com/)
- [Novita AI](https://novita.ai/docs/guides/introduction?utm_source=github_deep-searcher&utm_medium=github_readme&utm_campaign=link)（需配置 `NOVITA_API_KEY` 环境变量）
- [IBM watsonx.ai](https://www.ibm.com/products/watsonx-ai/foundation-models#ibmfm)（需配置 `WATSONX_APIKEY`、`WATSONX_URL`、`WATSONX_PROJECT_ID` 环境变量）
- [Jiekou.AI](https://jiekou.ai/?utm_source=github_deep-searcher)（需配置 `JIEKOU_API_KEY` 环境变量）

### 🔹 文档加载器
- 本地文件
  - PDF（含 txt/md）加载器
  - [Unstructured](https://unstructured.io/)（正在开发中，需配置 `UNSTRUCTURED_API_KEY` 和 `UNSTRUCTURED_URL` 环境变量）
- 网页爬虫
  - [FireCrawl](https://docs.firecrawl.dev/introduction)（需配置 `FIRECRAWL_API_KEY` 环境变量）
  - [Jina Reader](https://jina.ai/reader/)（需配置 `JINA_API_TOKEN` 环境变量）
  - [Crawl4AI](https://docs.crawl4ai.com/)（首次运行请执行命令 `crawl4ai-setup`）

### 🔹 向量数据库支持
- [Milvus](https://milvus.io/) 和 [Zilliz Cloud](https://www.zilliz.com/)（全托管 Milvus 服务）
- [Qdrant](https://qdrant.tech/)

---
## 📊 模型评估 
详见 [Evaluation](./evaluation) 目录。

---
## 📌 未来计划
- 增强网页爬取功能
- 支持更多向量数据库（如 FAISS...）
- 增加对其他大语言模型的支持
- 提供 RESTful API 接口（**已完成**）

我们欢迎你的贡献！请 Star & Fork 本项目，与我们一起打造更强大的 DeepSearcher！🎯
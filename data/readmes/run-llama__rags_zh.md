# RAGs



https://github.com/run-llama/rags/assets/4858925/a6204550-b3d1-4cde-b308-8d944e5d3058



RAGs 是一个基于 Streamlit 的应用，让你能够使用自然语言从数据源创建 RAG（检索增强生成）流水线。

你可以执行以下操作：
1. 描述你的任务（例如“加载这个网页”）以及你希望从 RAG 系统中获取的参数（例如“我想检索 X 数量的文档”）。
2. 进入配置视图，查看/修改生成的参数（如 top-k、摘要生成等），按需调整。
3. 通过提问向基于数据的 RAG agent（智能体）发起查询。

本项目灵感来源于 OpenAI 推出的 [GPTs](https://openai.com/blog/introducing-gpts)。

## Installation and Setup 

克隆该项目，进入 `rags` 项目文件夹。我们建议为依赖项创建虚拟环境（`python3 -m venv .venv`）。

```
poetry install --with dev
```

默认情况下，我们使用 OpenAI 作为构建器智能体（builder agent）和生成的 RAG 智能体的后端。
在项目主目录添加 `.streamlit/secrets.toml` 文件。

然后填入以下内容：
```
openai_key = "<openai_key>"
```


接着从“主页”文件运行该应用。

```

streamlit run 1_🏠_Home.py

```

**注意**：如果你升级了 RAGs 版本并在启动时遇到问题，可能需要删除用户主目录（home directory）下的 `cache` 文件夹（不同版本间存储的数据结构可能引入了破坏性更新）。

## Detailed Overview

该应用包含以下部分，分别对应上述步骤。

### 1. 🏠 Home Page
这是你通过指令“构建器智能体”来搭建 RAG 流水线的区域。通常，设置一个 RAG 流水线需要以下组件：
1. Describe the dataset. Currently we support either **a single local file** or a **web page**. We're open to suggestions here! 
   描述数据集。目前我们支持**单个本地文件**或**网页**。非常欢迎提出其他建议！ 
2. Describe the task. Concretely this description will be used to initialize the "system prompt" of the LLM powering the RAG pipeline.
   描述任务。具体来说，该描述将用于初始化驱动 RAG 流水线的 LLM（大语言模型）的“系统提示词”。
3. Define the typical parameters for a RAG setup. See the below section for the list of parameters.
   定义 RAG 设置的典型参数。参数列表见下文。

### 2. ⚙️ RAG Config

此部分包含由上一节“构建器智能体”生成的 RAG 参数。在这里，你可以通过界面查看生成的参数，并拥有完全的自由度按需手动编辑或修改它们。

当前支持的参数如下：
- System Prompt（系统提示词）
- Include Summarization: whether to also add a summarization tool (instead of only doing top-k retrieval.) -> 包含摘要生成：是否添加摘要工具（而非仅进行 top-k 检索）。
- Top-K
- Chunk Size（分块大小）
- Embed Model（嵌入模型）
- LLM 

如果你手动修改了参数，可以按下“Update Agent”按钮以应用更改。

```{tip}
If you don't see the `Update Agent` button, that's because you haven't created the agent yet. Please go to the previous "Home" page and complete the setup process.
```
{tip} 如果你没有看到 `Update Agent` 按钮，是因为你尚未创建该智能体。请前往之前的“主页”完成设置流程。{/tip>

我们随时可以添加更多参数以使功能更“高级” 🛠️，但这作为起点已经足够好了。

### 3. Generated RAG Agent

Once your RAG agent is created, you have access to this page.
创建好你的 RAG 智能体后，即可访问此页面。

This is a standard chatbot interface where you can query the RAG agent and it will answer questions over your data.
这是一个标准的聊天机器人界面，你可以向 RAG 智能体提问，它将基于你的数据回答问题。

It will be able to pick the right RAG tools (either top-k vector search or optionally summarization) in order to fulfill the query.
它能够自动选择最合适的 RAG 工具（如 top-k 向量搜索或可选的摘要生成）来响应查询请求。


## Supported LLMs and Embeddings

### Builder Agent

By default the builder agent uses OpenAI. This is defined in the `core/builder_config.py` file.
默认情况下，构建器智能体使用 OpenAI。这一定义位于 `core/builder_config.py` 文件中。

You can customize this to whatever LLM you want (an example is provided for Anthropic).
你可以根据需要将其自定义为任意 LLM（已提供 Anthropic 的示例）。

Note that GPT-4 variants will give the most reliable results in terms of actually constructing an agent (we couldn't get Claude to work).
请注意，在实际构建智能体方面，GPT-4 系列模型能提供最可靠的结果（我们曾尝试让 Claude 工作但未能成功）。

### Generated RAG Agent

You can set the configuration either through natural language or manually for both the embedding model and LLM.
你可以使用自然语言或手动设置嵌入模型和 LLM 的配置。

- **LLM**: We support the following LLMs, but you need to explicitly specify the ID to the builder agent.
    - OpenAI: ID is "openai:<model_name>" e.g. "openai:gpt-4-1106-preview" -> **LLM**：我们支持以下模型，但需要向构建器智能体显式指定其 ID。
        - OpenAI：ID 格式为 `openai:<model_name>`，例如 `"openai:gpt-4-1106-preview"`
        - Anthropic：ID 格式为 `anthropic:<model_name>`，例如 `"anthropic:claude-2"`
        - Replicate：ID 格式为 `replicate:<model_name>`
        - HuggingFace：ID 格式为 `local:<model_name>`，例如 `"local:BAAI/bge-small-en"`
- **Embeddings**: Supports text-embedding-ada-002 by default, but also supports Hugging Face models. To use a hugging face model simply prepend with local, e.g. local:BAAI/bge-small-en.
    - **嵌入模型**：默认支持 `text-embedding-ada-002`，同时也支持 Hugging Face 模型。使用 Hugging Face 模型时只需在名称前加上 `local:` 即可，例如 `local:BAAI/bge-small-en`。


## Resources

Running into issues? Please file a GitHub issue or join our [Discord](https://discord.gg/dGcwcsnxhU).
遇到问题？请提交 GitHub Issue 或加入我们的 [Discord](https://discord.gg/dGcwcsnxhU)。

This app was built with [LlamaIndex Python](https://github.com/run-llama/llama_index).
本应用基于 [LlamaIndex Python](https://github.com/run-llama/llama_index) 构建。

See our launch blog post [here](https://blog.llamaindex.ai/introducing-rags-your-personalized-chatgpt-experience-over-your-data-2b9d140769b1).
查看我们的发布博客文章 [此处](https://blog.llamaindex.ai/introducing-rags-your-personalized-chatgpt-experience-over-your-data-2b9d140769b1)。
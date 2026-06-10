<a name="readme-top"></a>

<div align="center">
  <img src="./assets/AutoAgent_logo.svg" alt="Logo" width="200">
  <h1 align="center">AutoAgent: Fully-Automated & Zero-Code</br> LLM Agent Framework </h1>
</div>




<div align="center">
  <a href="https://autoagent-ai.github.io"><img src="https://img.shields.io/badge/Project-Page-blue?style=for-the-badge&color=FFE165&logo=homepage&logoColor=white" alt="Credits"></a>
  <a href="https://join.slack.com/t/metachain-workspace/shared_invite/zt-2zibtmutw-v7xOJObBf9jE2w3x7nctFQ"><img src="https://img.shields.io/badge/Slack-Join%20Us-red?logo=slack&logoColor=white&style=for-the-badge" alt="Join our Slack community"></a>
  <a href="https://discord.gg/jQdXyDB"><img src="https://img.shields.io/badge/Discord-Join%20Us-purple?logo=discord&logoColor=white&style=for-the-badge" alt="Join our Discord community"></a>
  <!-- <a href="https://github.com/HKUDS/AutoAgent/blob/main/assets/autoagent-wechat.jpg"><img src="https://img.shields.io/badge/Wechat-Join%20Us-green?logo=wechat&logoColor=white&style=for-the-badge" alt="Join our Wechat community"></a> -->
  <a href="./Communication.md"><img src="https://img.shields.io/badge/💬Feishu-Group-07c160?style=for-the-badge&logoColor=white&labelColor=1a1a2e"></a>
  <a href="./Communication.md"><img src="https://img.shields.io/badge/WeChat-Group-07c160?style=for-the-badge&logo=wechat&logoColor=white&labelColor=1a1a2e"></a>
  
  <br/>
  <a href="https://autoagent-ai.github.io/docs"><img src="https://img.shields.io/badge/Documentation-000?logo=googledocs&logoColor=FFE165&style=for-the-badge" alt="Check out the documentation"></a>
  <a href="https://arxiv.org/abs/2502.05957"><img src="https://img.shields.io/badge/Paper%20on%20Arxiv-000?logoColor=FFE165&logo=arxiv&style=for-the-badge" alt="Paper"></a>
  <a href="https://gaia-benchmark-leaderboard.hf.space/"><img src="https://img.shields.io/badge/GAIA%20Benchmark-000?logoColor=FFE165&logo=huggingface&style=for-the-badge" alt="Evaluation Benchmark Score"></a>
  <hr>
</div>

<div align="center">
<a href="https://trendshift.io/repositories/13954" target="_blank"><img src="https://trendshift.io/api/badge/repositories/13954" alt="HKUDS%2FAutoAgent | Trendshift" style="width: 250px; height: 55px;" width="250" height="55"/></a>
</div>

欢迎来到 AutoAgent！AutoAgent 是一个**全自动**且高度**自我演进**的框架，使用户能够仅通过**自然语言**创建和部署 LLM Agent（大语言模型智能体）。 

## ✨AutoAgent 核心特性

* 💬 **自然语言驱动的智能体构建** 
</br>纯粹通过自然对话自动构建和编排协作式智能体系统，无需手动编写代码或进行技术配置。

* 🚀 **零代码框架**
</br>降低 AI 开发门槛，让任何人无论是否有编程经验，都能仅使用自然语言来创建和定制自己的智能体、工具和流程。

* ⚡ **自我管理工作流生成**
</br>根据高层任务描述动态创建、优化和调整智能体工作流，即使用户无法完全指定实现细节也能正常工作。

* 🔧 **智能资源编排**
</br>通过迭代式自我改进实现对代码生成的控制，用于创建工具、智能体和流程，支持单智能体创建和多智能体工作流生成。

* 🎯 **自博弈智能体定制** 
</br>通过迭代式自我改进实现对代码生成的控制，用于创建工具、智能体和流程，支持单智能体创建和多智能体工作流生成。

🚀 解锁 LLM Agent 的未来。立即尝试 🔥AutoAgent🔥！

<div align="center">
  <!-- <img src="./assets/AutoAgentnew-intro.pdf" alt="Logo" width="100%"> -->
  <figure>
    <img src="./assets/autoagent-intro.svg" alt="Logo" style="max-width: 100%; height: auto;">
    <figcaption><em>AutoAgent 快速概览。</em></figcaption>
  </figure>
</div>



## 🔥 更新动态

<div class="scrollable">
    <ul>
      <li><strong>[2025, Feb 17]</strong>: &nbsp;🎉🎉我们已更新并发布 AutoAgent v0.2.0（原名为 MetaChain）。详细变更包括：1) 修复了不同 LLM 提供商的 bug；2) 根据 issue 添加了在容器环境中自动安装 AutoAgent 的功能；3) 为 CLI 模式增加了更多易用的命令。4) 将项目更名为 AutoAgent 以便于理解。</li>
      <li><strong>[2025, Feb 10]</strong>: &nbsp;🎉🎉我们发布了 <b>MetaChain！</b>，包括框架、评估代码和 CLI 模式！详情请查看我们的 <a href="https://arxiv.org/abs/2502.05957">论文</a>。</li>
    </ul>
</div>
<span id='table-of-contents'/>

## 📑 目录

* <a href='#features'>✨ 核心特性</a>
* <a href='#news'>🔥 更新动态</a>
* <a href='#how-to-use'>🔍 如何使用 AutoAgent</a>
  * <a href='#user-mode'>1. `user mode`（深度研究智能体）</a>
  * <a href='#agent-editor'>2. `agent editor`（无流程的智能体创建）</a>
  * <a href='#workflow-editor'>3. `workflow editor`（带流程的智能体创建）</a>
* <a href='#quick-start'>⚡ 快速入门</a>
  * <a href='#installation'>安装</a>
  * <a href='#api-keys-setup'>API Key 配置</a>
  * <a href='#start-with-cli-mode'>通过 CLI 模式启动</a>
* <a href='#todo'>☑️ 待办事项</a>
* <a href='#reproduce'>🔬 如何复现论文结果</a>
* <a href='#documentation'>📖 文档</a>
* <a href='#community'>🤝 加入社区</a>
* <a href='#acknowledgements'>🙏 致谢</a>
* <a href='#cite'>🌟 引用</a>

<span id='how-to-use'/>

## 🔍 如何使用 AutoAgent

<span id='user-mode'/>

### 1. `user mode`（深度研究智能体）

AutoAgent 提供了一个开箱即用的多智能体系统，可在启动页通过用户模式访问。该系统旨在作为全面的 AI 研究助手，用于信息检索、复杂分析任务和综合报告生成。

- 🚀 **高性能**：使用 Claude 3.5 即可媲美 Deep Research（原基于 OpenAI o3 模型）。
- 🔄 **模型灵活性**：兼容任何 LLM（包括 Deepseek-R1、Grok、Gemini 等）
- 💰 **高性价比**：Deep Research 订阅费为每月 $200，本框架为其开源替代方案
- 🎯 **用户友好**：易于部署的 CLI 界面，实现无缝交互
- 📁 **文件支持**：支持文件上传以增强数据交互

<div align="center">
  <video width="80%" controls>
    <source src="./assets/video_v1_compressed.mp4" type="video/mp4">
  </video>
  <p><em>🎥 Deep Research（即 User Mode）</em></p>
</div>



<span id='agent-editor'/>

### 2. `agent editor`（无流程的智能体创建）

AutoAgent 最独特的功能是其自然语言定制能力。与其他智能体框架不同，AutoAgent 允许你仅使用自然语言来创建工具、智能体和流程。只需选择 `agent editor` 或 `workflow editor` 模式即可开始通过对话构建智能体的旅程。

你可以按照下图所示使用 `agent editor`。

<table>
<tr align="center">
    <td width="33%">
        <img src="./assets/agent_editor/1-requirement.png" alt="requirement" width="100%"/>
        <br>
        <em>输入你想创建的智能体类型。</em>
    </td>
    <td width="33%">
        <img src="./assets/agent_editor/2-profiling.png" alt="profiling" width="100%"/>
        <br>
        <em>自动化智能体画像生成。</em>
    </td>
    <td width="33%">
        <img src="./assets/agent_editor/3-profiles.png" alt="profiles" width="100%"/>
        <br>
        <em>输出智能体配置信息。</em>
    </td>
</tr>
</table>
<table>
<tr align="center">
    <td width="33%">
        <img src="./assets/agent_editor/4-tools.png" alt="tools" width="100%"/>
        <br>
        <em>创建所需工具。</em>
    </td>
    <td width="33%">
        <img src="./assets/agent_editor/5-task.png" alt="task" width="100%"/>
        <br>
        <em>输入你想用该智能体完成的任务。（可选）</em>
    </td>
    <td width="33%">
        <img src="./assets/agent_editor/6-output-next.png" alt="output" width="100%"/>
        <br>
        <em>创建所需智能体并进入下一步。</em>
    </td>
</tr>
</table>

<span id='workflow-editor'/>

### 3. `workflow editor`（带流程的智能体创建）

你也可以使用 `workflow editor` 模式通过自然语言描述来创建工作流，如下图所示。（提示：此模式暂时不支持工具创建。）

<table>
<tr align="center">
    <td width="33%">
        <img src="./assets/workflow_editor/1-requirement.png" alt="requirement" width="100%"/>
        <br>
        <em>输入你想创建工作流的类型。</em>
    </td>
    <td width="33%">
        <img src="./assets/workflow_editor/2-profiling.png" alt="profiling" width="100%"/>
        <br>
        <em>自动化工作流画像生成。</em>
    </td>
    <td width="33%">
        <img src="./assets/workflow_editor/3-profiles.png" alt="profiles" width="100%"/>
        <br>
        <em>输出工作流配置信息。</em>
    </td>
</tr>
</table>
<table>
<tr align="center">
    <td width="33%">
        <img src="./assets/workflow_editor/4-task.png" alt="task" width="66%"/>
        <br>
        <em>输入你想用该工作流完成的任务。（可选）</em>
    </td>
    <td width="33%">
        <img src="./assets/workflow_editor/5-output-next.png" alt="output" width="66%"/>
        <br>
        <em>创建所需工作流并进入下一步。</em>
    </td>
</tr>
</table>

<span id='quick-start'/>

## ⚡ 快速入门

<span id='installation'/>

### 安装

#### AutoAgent 安装

```bash
git clone https://github.com/HKUDS/AutoAgent.git
cd AutoAgent
pip install -e .
```

#### Docker 安装

我们使用 Docker 对智能体交互环境进行容器化封装，因此请先安装 [Docker](https://www.docker.com/)。你无需手动拉取预构建镜像，因为我们已让 Auto-Deep-Research **根据你的机器架构自动拉取相应的预构建镜像**。

<span id='api-keys-setup'/>

### API Key 配置

创建一个环境变量文件（例如 `.env.template`），并设置你要使用的 LLM 的 API Key。并非所有 LLM 的 API Key 都是必需的，按需填写即可。

```bash
# Required Github Tokens of your own
GITHUB_AI_TOKEN=

# Optional API Keys
OPENAI_API_KEY=
DEEPSEEK_API_KEY=
ANTHROPIC_API_KEY=
GEMINI_API_KEY=
HUGGINGFACE_API_KEY=
GROQ_API_KEY=
XAI_API_KEY=
```

<span id='start-with-cli-mode'/>

### 通过 CLI 模式启动

> [🚨 **更新**: ] 我们已更新更易于使用的命令来启动 CLI 模式，并修复了不同 LLM 提供商的 bug。你可以按照以下步骤使用不同的 LLM 提供商以极少的配置启动 CLI 模式。

#### 命令选项：

运行 `auto main` 可启动 AutoAgent 的全部功能，包括 `user mode`、`agent editor` 和 `workflow editor`。此外，你也可以运行 `auto deep-research` 来启动更轻量级的 `user mode`，类似于 [Auto-Deep-Research](https://github.com/HKUDS/Auto-Deep-Research) 项目。该命令的部分配置如下所示： 

- `--container_name`: Docker 容器名称（默认: 'deepresearch'）
- `--port`: 容器端口（默认: 12346）
- `COMPLETION_MODEL`: 指定要使用的 LLM 模型，请遵循 [Litellm](https://github.com/BerriAI/litellm) 的命名规范来设置模型名称。（默认: `claude-3-5-sonnet-20241022`）
- `DEBUG`: 启用调试模式以获取详细日志（默认: False）
- `API_BASE_URL`: LLM 提供商的基础 URL（默认: None）
- `FN_CALL`: 启用函数调用（默认: None）。大多数情况下你可以忽略此选项，因为我们已根据模型名称设置了默认值。
- `git_clone`: 将 AutoAgent 仓库克隆到本地环境（仅支持与 `auto main` 命令配合使用，默认: True）
- `test_pull_name`: 测试分支/PR 的名称。（仅支持与 `auto main` 命令配合使用，默认: 'autoagent_mirror'）

#### 关于 `git_clone` 和 `test_pull_name` 的更多说明 

在 `agent editor` 和 `workflow editor` 模式中，我们需要将 AutoAgent 仓库的镜像克隆到本地智能体交互环境中，并让我们的 **AutoAgent** 自动更新自身（例如创建新工具、智能体和流程）。因此，如果你想使用这两种模式，应将 `git_clone` 设置为 True，并将 `test_pull_name` 设置为 'autoagent_mirror' 或其他分支。

#### 使用不同 LLM 提供商运行 `auto main`

接下来我将展示如何使用 `auto main` 命令配合不同的 LLM 提供商来启动 AutoAgent 的全部功能。如果你想使用 `auto deep-research` 命令，可参考 [Auto-Deep-Research](https://github.com/HKUDS/Auto-Deep-Research) 项目获取更多信息。

##### Anthropic

* 在 `.env` 文件中设置 `ANTHROPIC_API_KEY`。

```bash
ANTHROPIC_API_KEY=your_anthropic_api_key
```

* 运行以下命令启动框架：

```bash
auto main # default model is claude-3-5-sonnet-20241022
```

##### OpenAI

* 在 `.env` 文件中设置 `OPENAI_API_KEY`。

```bash
OPENAI_API_KEY=your_openai_api_key
```

* 运行以下命令启动框架：

```bash
COMPLETION_MODEL=gpt-4o auto main
```

##### Mistral

* 在 `.env` 文件中设置 `MISTRAL_API_KEY`。

```bash
MISTRAL_API_KEY=your_mistral_api_key
```

* 运行以下命令启动框架：

```bash
COMPLETION_MODEL=mistral/mistral-large-2407 auto main
```

##### Gemini - Google AI Studio

* 在 `.env` 文件中设置 `GEMINI_API_KEY`。

```bash
GEMINI_API_KEY=your_gemini_api_key
```

* 运行以下命令启动框架：

```bash
COMPLETION_MODEL=gemini/gemini-2.0-flash auto main
```

##### Huggingface

* 在 `.env` 文件中设置 `HUGGINGFACE_API_KEY`。

```bash
HUGGINGFACE_API_KEY=your_huggingface_api_key
```

* 运行以下命令启动框架：

```bash
COMPLETION_MODEL=huggingface/meta-llama/Llama-3.3-70B-Instruct auto main
```

##### Groq

* 在 `.env` 文件中设置 `GROQ_API_KEY`。

```bash
GROQ_API_KEY=your_groq_api_key
```

* 运行以下命令启动框架：

```bash
COMPLETION_MODEL=groq/deepseek-r1-distill-llama-70b auto main
```

##### OpenAI-Compatible Endpoints (e.g., Grok)

* 在 `.env` 文件中设置 `OPENAI_API_KEY`。

```bash
OPENAI_API_KEY=your_api_key_for_openai_compatible_endpoints
```

* 运行以下命令启动框架：

```bash
COMPLETION_MODEL=openai/grok-2-latest API_BASE_URL=https://api.x.ai/v1 auto main
```

##### OpenRouter (e.g., DeepSeek-R1)

我们建议暂时使用 OpenRouter 作为 DeepSeek-R1 的 LLM 提供商。因为官方 API 目前无法高效使用。

* 在 `.env` 文件中设置 `OPENROUTER_API_KEY`。

```bash
OPENROUTER_API_KEY=your_openrouter_api_key
```

* 运行以下命令启动框架：

```bash
COMPLETION_MODEL=openrouter/deepseek/deepseek-r1 auto main
```

##### DeepSeek

* 在 `.env` 文件中设置 `DEEPSEEK_API_KEY`。

```bash
DEEPSEEK_API_KEY=your_deepseek_api_key
```

* 运行以下命令启动框架：

```bash
COMPLETION_MODEL=deepseek/deepseek-chat auto main
```


启动 CLI 模式后，你将看到 AutoAgent 的启动页面： 

<div align="center">
  <!-- <img src="./assets/AutoAgentnew-intro.pdf" alt="Logo" width="100%"> -->
  <figure>
    <img src="./assets/cover.png" alt="Logo" style="max-width: 100%; height: auto;">
    <figcaption><em>AutoAgent 启动页面。</em></figcaption>
  </figure>
</div>

### 使用技巧

#### 将浏览器 Cookie 导入浏览器环境

你可以将浏览器 Cookie 导入到浏览器环境中，以便智能体更好地访问某些特定网站。更多详情请参考 [cookies](./AutoAgent/environment/cookie_json/README.md) 文件夹。

#### 为第三方工具平台添加你自己的 API Key

如果你想从第三方工具平台（如 RapidAPI）创建工具，你需要先在平台上订阅所需工具，然后通过运行 [process_tool_docs.py](./process_tool_docs.py) 添加你自己的 API Key。 

```bash
python process_tool_docs.py
```

更多功能即将推出！🚀 **Web GUI（图形用户界面）** 正在开发中。



<span id='todo'/>

## ☑️ 待办事项

AutoAgent 正在持续演进！以下是接下来的计划：

- 📊 **更多基准测试**：扩展对 **SWE-bench**、**WebArena** 等平台的评估
- 🖥️ **GUI 智能体**：支持具有 GUI 交互功能的 *Computer-Use*（计算机使用）智能体
- 🔧 **工具平台**：集成更多平台，如 **Composio**
- 🏗️ **代码沙盒**：支持更多环境，如 **E2B**
- 🎨 **网页界面**：开发全面的 GUI 以提升用户体验

有想法或建议？欢迎提交 Issue！敬请期待更多精彩更新！🚀

<span id='reproduce'/>

## 🔬 如何复现论文结果

### GAIA Benchmark
对于 GAIA 基准测试，你可以运行以下命令进行推理。

```bash
cd path/to/AutoAgent && sh evaluation/gaia/scripts/run_infer.sh
```

进行评估时，可运行以下命令。

```bash
cd path/to/AutoAgent && python evaluation/gaia/get_score.py
```

### Agentic-RAG

对于 Agentic-RAG 任务，你可以运行以下命令进行推理。

第一步：访问[此页面](https://huggingface.co/datasets/yixuantt/MultiHopRAG)并下载数据集，将其保存到你的数据路径中。

第二步：运行以下命令进行推理。

```bash
cd path/to/AutoAgent && sh evaluation/multihoprag/scripts/run_rag.sh
```

第三步：结果将保存在 `evaluation/multihoprag/result.json` 中。

<span id='documentation'/>

## 📖 文档

更详细的文档即将推出 🚀，我们将同步更新到[官方文档](https://AutoAgent-ai.github.io/docs)页面。

<span id='community'/>

## 🤝 加入社区

我们希望为 AutoAgent 建立一个社区，并欢迎所有人加入。你可以通过以下方式参与我们的社区：

- [加入我们的 Slack 工作区](https://join.slack.com/t/AutoAgent-workspace/shared_invite/zt-2zibtmutw-v7xOJObBf9jE2w3x7nctFQ) - 在这里我们讨论研究、架构和未来开发。
- [加入我们的 Discord 服务器](https://discord.gg/z68KRvwB) - 这是一个社区运营的服务器，用于一般性讨论、提问和反馈。 
- [查看或提交 GitHub Issue](https://github.com/HKUDS/AutoAgent/issues) - 了解我们正在处理的问题，或提出你自己的想法。

<span id='acknowledgements'/>



## Misc

<div align="center">

[![Stargazers repo roster for @HKUDS/AutoAgent](https://reporoster.com/stars/HKUDS/AutoAgent)](https://github.com/HKUDS/AutoAgent/stargazers)

[![Forkers repo roster for @HKUDS/AutoAgent](https://reporoster.com/forks/HKUDS/AutoAgent)](https://github.com/HKUDS/AutoAgent/network/members)

[![Star History Chart](https://api.star-history.com/svg?repos=HKUDS/AutoAgent&type=Date)](https://star-history.com/#HKUDS/AutoAgent&Date)

</div>

## 🙏 致谢

罗马非一日建成。AutoAgent 站在巨人的肩膀上，我们深深感激此前优秀的开源工作。我们的框架架构灵感来源于 [OpenAI Swarm](https://github.com/openai/swarm)，而用户模式的三智能体设计受益于 [Magentic-one](https://github.com/microsoft/autogen/tree/main/python/packages/autogen-magentic-one) 的见解。我们还从 [OpenHands](https://github.com/All-Hands-AI/OpenHands) 学习了文档结构，并从许多其他优秀项目中借鉴了智能体与环境交互的设计方案等。我们对这些对塑造 AutoAgent 起到关键作用的开创性工作表示诚挚的感谢与敬意。


<span id='cite'/>

## 🌟 引用

```tex
@misc{AutoAgent,
      title={{AutoAgent: A Fully-Automated and Zero-Code Framework for LLM Agents}},
      author={Jiabin Tang, Tianyu Fan, Chao Huang},
      year={2025},
      eprint={202502.05957},
      archivePrefix={arXiv},
      primaryClass={cs.AI},
      url={https://arxiv.org/abs/2502.05957},
}
```
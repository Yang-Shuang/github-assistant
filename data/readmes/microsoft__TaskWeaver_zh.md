<h1 align="center">
    <img src="./.asset/logo.color.svg" width="45" /> TaskWeaver
</h1>

<div align="center">

![Python Version](https://img.shields.io/badge/Python-3776AB?&logo=python&logoColor=white-blue&label=3.10%20%7C%203.11)&ensp;
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)&ensp;
![Welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)

</div>

TaskWeaver 是一个**代码优先（Code-First）**的智能体框架，用于无缝规划并执行数据分析任务。该创新框架通过代码片段解析用户请求，并以有状态的方式高效协调多种函数形式的插件来执行数据分析任务。

与许多仅以文本形式记录与大语言模型（LLM）对话历史的智能体框架不同，TaskWeaver 同时保留了**对话历史**和**代码执行历史**，包括内存中的数据。该特性增强了智能体框架的*表达能力（Expressiveness）*，使其非常适合处理如高维表格数据等复杂数据结构。

<h1 align="center">
    <img src="./.asset/taskweaver_arch.png"/> 
</h1>


## 🆕 更新动态
- 📅2025-03-13：Planner（规划）角色现已支持视觉输入。详情请查看[视觉输入文档](https://microsoft.github.io/TaskWeaver/blog/vision)。👀
- 📅2025-01-16：TaskWeaver 新增了名为 [Recepta](https://microsoft.github.io/TaskWeaver/blog/reasoning) 的实验性角色，以增强其推理能力。🧠
- 📅2024-12-23：TaskWeaver 已集成 [AgentOps](https://microsoft.github.io/TaskWeaver/docs/observability)，以提供更佳的观测与监控功能。🔍
- 📅2024-09-13：我们引入了共享内存（Shared Memory）用于存储 TaskWeaver 中各角色间共享的信息。详情请查看[内存文档](https://microsoft.github.io/TaskWeaver/docs/memory)。🧠
- 📅2024-09-13：我们增强了经验（Experience）功能，支持静态与动态经验选择。详情请查看[经验文档](https://microsoft.github.io/TaskWeaver/blog/experience)。📚 
- 📅2024-07-02：我们优化了 TaskWeaver，以支持本地部署的非超大语言模型。详情请查看[此文章](https://microsoft.github.io/TaskWeaver/blog/local_llm)。🔗
- 📅2024-05-07：文档中新增了两篇博客文章，分别介绍[评估 LLM 智能体](https://microsoft.github.io/TaskWeaver/blog/evaluation)和[为 TaskWeaver 添加新角色](https://microsoft.github.io/TaskWeaver/blog/role)。📝
- 📅2024-03-28：TaskWeaver 现已提供一体化 Docker 镜像，为用户提供便捷的一站式体验。详情请查看[Docker 文档](https://microsoft.github.io/TaskWeaver/docs/usage/docker)。🐳
- 📅2024-03-27：代码执行默认切换为 `container`（容器）模式。详情请查看[代码执行文档](https://microsoft.github.io/TaskWeaver/docs/code_execution)。🐳
<!-- - 📅2024-03-07: TaskWeaver now supports configuration of different LLMs for various components, such as the Planner and CodeInterpreter. Please check the [multi-llm](https://microsoft.github.io/TaskWeaver/docs/llms/multi-llm) for more details.🔗 -->
<!-- - 📅2024-03-04: TaskWeaver now supports a [container](https://microsoft.github.io/TaskWeaver/docs/code_execution) mode, which provides a more secure environment for code execution.🐳 -->
<!-- - 📅2024-02-28: TaskWeaver now offers a [CLI-only](https://microsoft.github.io/TaskWeaver/docs/advanced/cli_only) mode, enabling users to interact seamlessly with the Command Line Interface (CLI) using natural language.📟 -->
<!-- - 📅2024-02-01: TaskWeaver now has a plugin [document_retriever](https://github.com/microsoft/TaskWeaver/blob/main/project/plugins/README.md#document_retriever) for RAG based on a knowledge base.📚 -->
<!-- - 📅2024-01-30: TaskWeaver introduces a new plugin-only mode that securely generates calls to specified plugins without producing extraneous code.🪡 --> 
<!-- - 📅2024-01-23: TaskWeaver can now be personalized by transforming your chat histories into enduring [experiences](https://microsoft.github.io/TaskWeaver/docs/customization/experience) 🎉 -->
<!-- - 📅2024-01-17: TaskWeaver now has a plugin [vision_web_explorer](https://github.com/microsoft/TaskWeaver/blob/main/project/plugins/README.md#vision_web_explorer) that can open a web browser and explore websites.🌐 -->
<!-- - 📅2024-01-15: TaskWeaver now supports Streaming♒ in both UI and command line.✌️ -->
<!-- - 📅2024-01-01: Welcome join TaskWeaver [Discord](https://discord.gg/Z56MXmZgMb). -->
<!-- - 📅2023-12-21: TaskWeaver now supports a number of LLMs, such as LiteLLM, Ollama, Gemini, and QWen🎈.) -->
<!-- - 📅2023-12-21: TaskWeaver Website is now [available]&#40;https://microsoft.github.io/TaskWeaver/&#41; with more documentations.) -->
<!-- - 📅2023-12-12: A simple UI demo is available in playground/UI folder, try it [here](https://microsoft.github.io/TaskWeaver/docs/usage/webui)! -->
- ......
- 📅2023-11-30：TaskWeaver 在 GitHub 正式发布🎈。  


## 💥 核心特性

- [x] **复杂任务规划** - TaskWeaver 具备任务分解与进度跟踪功能，专为解决复杂任务而设计。
- [x] **反思执行（Reflective Execution）** - TaskWeaver 支持反思执行机制，允许智能体对执行过程进行回顾并做出调整。
- [x] **丰富的数据结构** - 在 Python 中，你可以直接使用 DataFrame 等丰富数据结构进行开发，而无需处理字符串。
- [x] **自定义算法** - TaskWeaver 允许你将自有算法封装为插件并进行编排调用。
- [x] **融入领域知识** - TaskWeaver 设计易于集成特定领域的专业知识，以提升系统的可靠性。
- [x] **有状态执行** - TaskWeaver 支持生成代码的有状态执行，确保一致且流畅的用户体验。
- [x] **代码验证（Code Verification）** - 在执行前会对生成的代码进行校验，检测潜在问题并提供修复建议。
- [x] **易于使用** - 提供示例插件、案例和教程，助你快速上手。TaskWeaver 开箱即用，安装后即可直接运行。
- [x] **易于调试** - 提供详细且透明的日志，帮助你全面了解整个流程（包括 LLM 提示词、代码生成与执行过程），便于调试。
- [x] **安全考量** - 支持基础会话管理以隔离不同用户的数据。代码执行被分离到独立进程中，避免相互干扰。
- [x] **易于扩展** - 可通过定义多个智能体角色和插件轻松扩展功能，以应对更复杂的任务需求。

## 📚 寻求社区贡献

仍有大量功能与改进空间。受限于团队资源，我们无法逐一实现或推进速度较慢。我们非常期待你的贡献，共同完善 TaskWeaver。
- [ ] 易用且易维护的 UX/UI
- [ ] 提示词模板管理支持
- [ ] 更优的插件交互体验，例如显示运行进度、中途停止插件执行及运行前用户确认等
- [ ] 与大语言模型（LLM）的异步交互支持
- [ ] 远程代码执行支持


## ✨ 快速开始

### 🛠️ 步骤 1：安装
TaskWeaver 需要 **Python >= 3.10**。可通过以下命令安装：
```bash
# [optional to create conda environment]
# conda create -n taskweaver python=3.10
# conda activate taskweaver

# clone the repository
git clone https://github.com/microsoft/TaskWeaver.git
cd TaskWeaver
# install the requirements
pip install -r requirements.txt
```

如需安装早期版本，可访问[Release 页面](https://github.com/microsoft/TaskWeaver/releases)，找到对应标签（例如 `v0.0.1`）并通过以下命令安装： 
```
pip install git+https://github.com/microsoft/TaskWeaver@<TAG>
```

### 🖊️ 步骤 2：配置大语言模型
运行 TaskWeaver 前，需提供你的 LLM 配置。以 OpenAI 为例，可将 `taskweaver_config.json` 文件配置如下。 

#### OpenAI
```json
{
  "llm.api_key": "the api key",
  "llm.model": "the model name, e.g., gpt-4"
}
```

💡 TaskWeaver 还支持其他 LLM 及高级配置，详情请查阅[官方文档](https://microsoft.github.io/TaskWeaver/docs/overview)。 

### 🚩 步骤 3：启动 TaskWeaver

💡 TaskWeaver 默认已切换至 `container`（容器）模式执行代码，这意味着代码将在容器中运行。你可能需要安装 Docker 并处理容器内的依赖项。详情请查看[代码执行文档](https://microsoft.github.io/TaskWeaver/docs/code_execution)。

#### ⌨️ 命令行界面（CLI）
```bash
# assume you are in the cloned TaskWeaver folder
python -m taskweaver -p ./project/
```
这将启动 TaskWeaver 进程，你可通过命令行界面与其交互。一切正常后，你将看到如下提示：

```
=========================================================
 _____         _     _       __
|_   _|_ _ ___| | _ | |     / /__  ____ __   _____  _____
  | |/ _` / __| |/ /| | /| / / _ \/ __ `/ | / / _ \/ ___/
  | | (_| \__ \   < | |/ |/ /  __/ /_/ /| |/ /  __/ /
  |_|\__,_|___/_|\_\|__/|__/\___/\__,_/ |___/\___/_/
=========================================================
TaskWeaver: I am TaskWeaver, an AI assistant. To get started, could you please enter your request?
Human: ___
```

#### 或 💻 WebUI 
TaskWeaver 也支持用于演示的 WebUI，详情请参考[WebUI 文档](https://microsoft.github.io/TaskWeaver/docs/usage/webui)。

#### 或 📋 作为库导入（Library）
TaskWeaver 可作为库导入以集成到你现有的项目中，更多信息请查阅[文档](https://microsoft.github.io/TaskWeaver/docs/usage/library)



## 📖 文档
更多文档请访问 [TaskWeaver 官网](https://microsoft.github.io/TaskWeaver)。


### ❓获取帮助 
* ❔GitHub Issues（**推荐**）
* [💬 Discord](https://discord.gg/Z56MXmZgMb) 用于讨论交流
* 其他事宜请联系 taskweaver@microsoft.com

---


## 🎬 演示案例

本演示基于[WebUI](https://microsoft.github.io/TaskWeaver/docs/usage/webui)制作，更适合展示生成的图像等产物。这些演示同样可在命令行界面中运行。 

#### 1️⃣📉 案例 1：从数据库拉取数据并应用异常检测算法
在本例中，我们将向你展示如何使用 TaskWeaver 从数据库中提取数据并应用异常检测算法。

[Anomaly Detection](https://github.com/microsoft/TaskWeaver/assets/7489260/248b9a0c-d504-4708-8c2e-e004689ee8c6)

若要运行此示例，需在 `project/plugins/sql_pull_data.yaml` 文件中配置 `sql_pull_data` 插件。你需要提供以下信息：
```yaml
api_type: azure or openai
api_base: ...
api_key: ...
api_version: ...
deployment_name: ...
sqlite_db_path: sqlite:///../../../sample_data/anomaly_detection.db
```
`sql_pull_data` 是一个用于从数据库提取数据的插件。它以自然语言请求作为输入，并返回一个 DataFrame。

该插件基于 [Langchain](https://www.langchain.com/) 实现。若要运行此示例，需安装 Langchain 包：
```bash
pip install langchain
pip install tabulate
```

#### 2️⃣🏦 案例 2：预测 QQQ 未来 7 天的价格
在本例中，我们将向你展示如何使用 TaskWeaver 预测 QQQ（纳斯达克100指数ETF）在未来 7 天的价格走势。 

[Nasdaq 100 Index Price Forecasting](https://github.com/microsoft/TaskWeaver/assets/7489260/1361ed83-16c3-4056-98fc-e0496ecab015)

若要运行此示例，请确保已安装以下两个依赖：
```bash
pip install yfinance
pip install statsmodels
```

更多案例请参考我们的[论文](http://export.arxiv.org/abs/2311.17541)。 

> 💡 TaskWeaver 的规划基于大语言模型（LLM）。因此，若要复现示例，执行流程可能与视频中显示的不同。例如在第二个演示中，助手可能会询问用户应使用哪种预测算法。通常，更具体的提示词有助于模型生成更好的规划与代码。


## 📚 引用
我们的论文详见[此处](http://export.arxiv.org/abs/2311.17541)。若在你的研究中使用 TaskWeaver，请引用我们的论文：
```
@article{taskweaver,
  title={TaskWeaver: A Code-First Agent Framework},
  author={Bo Qiao, Liqun Li, Xu Zhang, Shilin He, Yu Kang, Chaoyun Zhang, Fangkai Yang, Hang Dong, Jue Zhang, Lu Wang, Minghua Ma, Pu Zhao, Si Qin, Xiaoting Qin, Chao Du, Yong Xu, Qingwei Lin, Saravan Rajmohan, Dongmei Zhang},
  journal={arXiv preprint arXiv:2311.17541},
  year={2023}
}
```


## 商标信息

本项目可能包含项目、产品或服务的商标或徽标。对微软商标或徽标的授权使用须遵守并遵循[《微软商标与品牌指南》](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general)。对本项目的修改版本中使用微软商标或徽标不得引起混淆或暗示微软赞助。任何第三方商标或徽标的使用均受该第三方政策约束。

## 免责声明
本仓库中推荐的模型仅为示例，旨在结合[《TaskWeaver: A Code-First Agent Framework》](https://export.arxiv.org/abs/2311.17541)论文探索智能体系统的潜力。用户可根据自身需求替换本仓库中的模型。使用本仓库推荐模型时，需分别遵守这些模型的许可协议。对于因用户使用本仓库而导致的任何第三方权利侵权问题，微软不承担任何责任。用户同意就因本仓库产生的任何索赔，为微软进行抗辩、赔偿并使微软免受损害（包括所有损失、费用及律师费）。若任何人认为本仓库侵犯了其权利，请通知项目所有者邮箱。
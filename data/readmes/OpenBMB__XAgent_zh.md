<div align= "center">
    <h1> <img src="assets/readme/xagent_logo.png" height=40 align="texttop">XAgent</h1>
</div>

<div align="center">

[![Twitter](https://img.shields.io/twitter/follow/XAgent?style=social)](https://twitter.com/XAgentTeam) [![Discord](https://img.shields.io/badge/XAgent-Discord-purple?style=flat)](https://discord.gg/zncs5aQkWZ) [![License: Apache 2.0](https://img.shields.io/badge/License-Apache_2-0-green.svg)](https://opensource.org/license/apache-2-0/) ![Welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)

</div>

<p align="center">
    <a>English</a> •
    <a href="README_ZH.md">中文</a> •
    <a href="README_JA.md">日本語</a>
</p>

<p align="center">
  <a href="#quickstart">教程</a> •
  <a href="https://www.youtube.com/watch?v=QGkpd-tsFPA">演示</a> •
  <a href="https://blog.x-agent.net/blog/xagent/">博客</a> •
  <a href="https://xagent-doc.readthedocs.io/en/latest/">文档</a> •
  <a href="#Citation">引用文献</a>
</p>


## 📖 简介

XAgent 是一个开源的、由大语言模型（LLM）驱动的实验性自主智能体，能够自动解决各类任务。它被设计为一种通用型智能体，可应用于广泛的任务场景。目前 XAgent 仍处于早期阶段，我们正在持续努力改进它。

🏆 我们的目标是打造一个能够解决任何给定任务的超级智能体！

我们欢迎各种形式的合作，包括全职、兼职等职位。如果你对智能体前沿技术感兴趣，并希望加入我们共同实现真正的自主智能体，请通过 xagentteam@gmail.com 联系我们。

<div align="center">
    <img src="assets/readme/overview.png" alt="Overview of Xagent" width="700"/>
    <br/>
    <figcaption>XAgent 概览。</figcaption>
</div>

### <img src="assets/readme/xagent_logo.png" height=30 align="texttop"> XAgent

XAgent 具备以下核心特性：
- **自主性（Autonomy）**：XAgent 无需人工参与即可自动解决各类任务。
- **安全性（Safety）**：XAgent 被设计为安全运行，所有操作均在 Docker 容器内隔离执行。请放心使用！
- **可扩展性（Extensibility）**：XAgent 具备优秀的扩展能力。你可以轻松添加新工具以增强智能体的能力，甚至引入新的智能体！
- **图形界面（GUI）**：XAgent 提供了友好的图形用户界面供用户与智能体交互。你也可以通过命令行界面与之交互。
- **人机协作**：XAgent 能够与你协同完成任务。它不仅具备在解决复杂任务过程中遵循你指导的能力，还能在遇到挑战时主动寻求你的帮助。

XAgent 由三个核心部分组成：
- **🤖 调度器（Dispatcher）**：负责动态实例化并将任务分发至不同的智能体。它支持我们添加新智能体并持续提升其能力。
- **🧐 规划器（Planner）**：负责生成和修正任务计划。它将任务拆解为子任务并为每个子任务设定里程碑，使智能体能够逐步解决问题。
- **🦾 执行者（Actor）**：负责采取具体行动以实现目标并完成任务。执行者利用多种工具解决子任务，同时也能与人协作完成工作。

<div align="center">
    <img src="assets/readme/workflow.png" alt="Workflow of Xagent" width="700"/>
    <br/>
    <figcaption>XAgent 工作流程。</figcaption>
</div>

### 🧰 ToolServer

ToolServer 是为 XAgent 提供强大且安全工具的服务器。它是一个 Docker 容器，为 XAgent 的运行提供隔离的安全环境。
目前，ToolServer 提供以下工具：
- **📝 文件编辑器（File Editor）**：提供文本编辑功能，用于编写、读取和修改文件。
- **📘 Python 笔记本（Python Notebook）**：提供交互式 Python 运行环境，可执行代码以验证想法、绘制图表等。
- **🌏 网页浏览器（Web Browser）**：提供网页浏览功能，用于搜索和访问互联网资源。
- **🖥️ Shell 终端（Shell）**：提供 bash shell 工具，可执行任意 shell 命令，包括安装程序和托管服务。
- **🧩 Rapid API 接口（Rapid API）**：提供从 Rapid API 检索并调用外部 API 的工具，为 XAgent 提供了丰富的能力扩展。有关 Rapid API 集合的更多信息，请参阅 [ToolBench](https://github.com/OpenBMB/ToolBench)。
你也可以轻松向 ToolServer 添加新工具，以进一步增强 XAgent 的能力。

<div><a id="Quickstart"></a></div>

## ✨ 快速开始

### 🛠️ 构建与配置 ToolServer

ToolServer 是执行 XAgent 操作的场所。它是一个 Docker 容器，为 XAgent 的运行提供安全环境。
因此，你需要先安装 `docker` 和 `docker-compose`。 
然后，请参照以下任一方式构建 ToolServer 镜像：

#### 从 Docker Hub 拉取镜像：

```bash
docker compose up
```

#### 从本地源码构建镜像：

```bash
docker compose build
docker compose up
```
这将构建 ToolServer 镜像并启动其容器。若希望后台运行容器，请使用 `docker compose up -d`。
有关 ToolServer 的详细信息，请参阅[此处](ToolServer/README.md)。

若 ToolServer 更新，需重新拉取或构建镜像：
```bash
docker compose pull
```
或
```bash
docker compose build
```

### 🎮 配置并运行 XAgent

完成 ToolServer 的配置后，即可开始运行 XAgent。
- 安装依赖（需 Python >= 3.10）
```bash
pip install -r requirements.txt
```

- 配置 XAgent

1. 运行前，请在 `assets/config.yml` 中完成 XAgent 的基础配置。 
2. `assets/config.yml` 中至少需提供一项 OpenAI API Key，用于访问 OpenAI 服务。我们强烈建议使用 `gpt-4-32k` 运行 XAgent；对于大多数简单任务，使用 `gpt-4` 也可以。无论如何，至少需提供一个 `gpt-3.5-turbo-16k` API Key 作为备用模型。由于上下文长度限制，我们未测试也不推荐使用 `gpt-3.5-turbo` 运行 XAgent；请勿尝试使用该模型。
3. 若想更改 `XAgentServer` 的配置文件路径，需修改 `.env` 文件中的 `CONFIG_FILE` 值并重启 Docker 容器。


- 运行 XAgent
```bash
python run.py --task "put your task here" --config-file "assets/config.yml"
```
1. 可使用参数 `--upload-files` 选择要提交给 XAgent 的初始文件。

2. XAgent 的本地工作区位于 `local_workspace`，运行过程中生成的所有文件均可在此找到。 

3. 执行结束后，为方便查看，`ToolServerNode` 中的整个 `workspace` 目录将被复制到 `running_records`。

4. 此外，在 `running_records` 中可查看所有中间步骤信息，例如任务状态、LLM 的输入输出对、使用的工具等。

5. 你可通过在配置文件中设置 `record_dir`（默认为 `Null`）来加载记录，从而复现之前的运行。该记录是绑定至 XAgent 代码版本级的系统级录制文件，所有运行配置、查询请求、代码执行状态（含错误信息）及服务器行为均会被详细记录。

6. 记录中已移除所有敏感信息（包括 API Key），因此你可安全地与他人分享。近期我们将推出更细粒度的共享选项，以突出展示人类在运行过程中的贡献。

   

- 通过图形界面运行 XAgent
容器 `XAgent-Server` 已内置 Nginx，且 Web 服务监听端口为 `5173`。
你可通过浏览器访问 `http://localhost:5173`，使用 Web UI 与 XAgent 进行交互。
默认用户名和密码分别为 `guest` 和 `xagent`。
有关 GUI 演示的详细信息，请参阅[此处](XAgentServer/README.md)。

<div><a id="Demo"></a></div>

## 🎬 演示案例

在此，我们展示一些由 XAgent 解决任务的案例：
你可以在 [XAgent 官网](https://www.x-agent.net/) 查看实时演示。此外，此处也提供了视频演示及使用 XAgent 的案例展示：
![Demo](assets/readme/demo.gif)

### 案例 1. 数据分析：双循环机制的有效性验证

我们以协助用户进行复杂数据分析的案例开篇。在此案例中，用户向 XAgent 提交了 `iris.zip` 文件以寻求数据分析帮助。XAgent 迅速将任务拆解为四个子任务：(1) 数据检查与理解；(2) 验证系统 Python 环境中相关数据分析库的可用性；(3) 编写用于数据处理与分析的代码；(4) 基于代码执行结果编制分析报告。
以下是由 XAgent 绘制的图表：
![Data Statics by XAgent](assets/readme/statistics.png)


### 案例 2. 推荐系统：人机交互新范式

凭借主动寻求人类协助并协同解决问题的独特能力，XAgent 不断重新定义人机合作的边界。如下方截图所示，一位用户寻求 XAgent 推荐适合朋友聚会的优质餐厅，但未提供具体细节。XAgent 识别到信息不足后，调用了 `AskForHumanHelp`（请求人工帮助）工具，提示人类介入以获取用户的偏好地点、预算限制、口味喜好及饮食禁忌。获得这些宝贵反馈后，XAgent 无缝生成了个性化的餐厅推荐，为用户及其朋友确保了满意且贴心的体验。

![Illustration of Ask for Human Help of XAgent](assets/readme/ask_for_human_help.png)

### 案例 3. 模型训练：高级工具使用者

XAgent 不仅能处理日常任务，在模型训练等复杂工作中也是不可或缺的好帮手。在此场景中，用户希望分析影评并评估特定电影的大众情绪。为此，XAgent 迅速启动流程：下载 IMDB 数据集以训练前沿的 BERT 模型（见下方截图），充分利用深度学习的力量。借助该训练好的 BERT 模型，XAgent 能够精准解析影评中的细微差别，并就公众对各类电影的看法提供具有洞察力的预测。

![bert_1](assets/readme/bert_1.png)
![bert_2](assets/readme/bert_2.png)
![bert_3](assets/readme/bert_3.png)

### 📊 评估结果

我们采用人类偏好评估来检验 XAgent 的性能表现。我们准备了[超过 50 个真实世界复杂任务](assets/tasks.yml)用于评估，涵盖五大类：搜索与报告、编码与开发、数据分析、数学计算及生活助手。
我们将 XAgent 的结果与 [AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) 进行对比，结果显示 XAgent 在总体表现上优于 AutoGPT。 
所有运行记录可参考[此处链接](https://drive.google.com/drive/folders/1I-j6FZDyMRrLTpZ64jeN89emA77AbNfc?usp=drive_link)。

![HumanPrefer](assets/readme/agent_comparison.png)

数据显示，XAgent 在人类偏好指标上较 AutoGPT 有显著提升。

我们还在以下基准测试中对 XAgent 进行了评估：
![Benchmarks](assets/readme/eval_on_dataset.png)


<div><a id="Blog"></a></div>

## 🖌️ 博客

我们的官方博客位于[此处](https://blog.x-agent.net/)！

<div><a id="Citation"></a></div>

## 🌟 贡献者

衷心感谢所有为项目做出贡献的伙伴。你们的努力使该项目不断成长与繁荣。无论大小，每一份贡献都弥足珍贵。

![Contributors](https://contrib.rocks/image?repo=OpenBMB/XAgent)

## 🌟 Star 增长历史

[![Star History Chart](https://api.star-history.com/svg?repos=openbmb/xagent&type=Date)](https://star-history.com/##openbmb/xagent&Date)

## 引用文献

如果你觉得我们的仓库对你有帮助，请考虑引用以下文献：
```angular2
@misc{xagent2023,
      title={XAgent: An Autonomous Agent for Complex Task Solving}, 
      author={XAgent Team},
      year={2023},
}
```
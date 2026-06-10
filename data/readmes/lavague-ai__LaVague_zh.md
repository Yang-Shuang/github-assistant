<p align="center">

  <a href="https://github.com/lavague-ai/LaVague/stargazers"><img src="https://img.shields.io/github/stars/lavague-ai/LaVague.svg?style=for-the-badge" alt="Stargazers"></a>

  <a href="https://github.com/lavague-ai/LaVague/issues"><img src="https://img.shields.io/github/issues/lavague-ai/LaVague.svg?style=for-the-badge" alt="Issues"></a>

  <a href="https://github.com/lavague-ai/LaVague/network/members"><img src="https://img.shields.io/github/forks/lavague-ai/LaVague.svg?style=for-the-badge" alt="Forks"></a>

  <a href="https://github.com/lavague-ai/LaVague/graphs/contributors"><img src="https://img.shields.io/github/contributors/lavague-ai/LaVague.svg?style=for-the-badge" alt="Contributors"></a>

</p>

</br>



<div align="center">

  <img src="docs/assets/logo.png" width=140px: alt="LaVague Logo">

  <h1>欢迎使用 LaVague</h1>



<h4 align="center">

 <a href="https://discord.gg/SDxn9KpqX9" target="_blank">

    <img src="https://img.shields.io/badge/Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white" height='35px' alt="Join our Discord server!">

  </a>

  <a href="https://docs.lavague.ai/en/latest/"><img src="https://img.shields.io/badge/📄-docs-000000?style=for-the-badge&colorA=09c&colorB=555" height='35px' alt="Docs"></a>

</h4>

  <p>用于开发 AI 网页代理（Web Agent）的大型动作模型框架

</p>

<h1></h1>

</div>



## LaVague：面向开发者的网页代理框架



LaVague 是一个开源框架，专为希望为终端用户创建 AI 网页代理以自动化流程的开发者设计。



我们的网页代理可以接收一个目标（例如“打印 Hugging Face Diffusers 库的安装步骤”），并生成和执行实现该目标所需的动作。



LaVague 代理由以下部分组成：



- **世界模型（World Model）**：接收目标和当前状态（即当前网页），并输出适当的指令集。

- **动作引擎（Action Engine）**：将这些指令“编译”为可执行的动作代码，例如 Selenium 或 Playwright，并执行它们。





### LaVague QA：专为测试工程师打造的工具

**🌊 基于 LaVague 构建**



LaVague QA 是一款面向测试工程师的专用工具，充分利用了我们的框架优势。 



它允许你将 Gherkin 规范转化为易于集成的测试用例，从而实现自动化测试编写。LaVague QA 在幕后利用 LaVague 框架，使网页测试效率提升 10 倍。



如需详细信息和设置指南，请访问 [LaVague QA 文档](https://docs.lavague.ai/en/latest/docs/lavague-qa/quick-tour/)。



## 🚀 快速开始



### Demo（演示）



以下示例展示了 LaVague 如何通过多步操作实现“前往 PEFT 的快速入门指南”这一目标：



<p align="center">

  <img src="./docs/assets/demo_agent_hf.gif" alt="Demo for agent">

</p>



### 动手实践 



你可以通过以下步骤完成此操作：



1. 使用以下命令安装 LaVague：



```bash

pip install lavague

```

2. 使用我们的框架构建网页代理并实现目标：



```python

from lavague.core import  WorldModel, ActionEngine

from lavague.core.agents import WebAgent

from lavague.drivers.selenium import SeleniumDriver



selenium_driver = SeleniumDriver(headless=False)

world_model = WorldModel()

action_engine = ActionEngine(selenium_driver)

agent = WebAgent(world_model, action_engine)

agent.get("https://huggingface.co/docs")

agent.run("Go on the quicktour of PEFT")



# Launch Gradio Agent Demo

agent.demo("Go on the quicktour of PEFT")

```



有关此示例及如何使用 LaVague 的更多信息，请参阅我们的[快速入门指南](https://docs.lavague.ai/en/latest/docs/get-started/quick-tour/)。



> 注意，这些示例默认使用 OpenAI API 配置。你需要在本地环境中设置有效的 `OPENAI_API_KEY` 环境变量，否则无法运行。



如需查看 LaVague 在 Google Colab 中的端到端示例，请参阅我们的[快速入门笔记本](https://colab.research.google.com/github/lavague-ai/lavague/blob/main/docs/docs/get-started/quick-tour-notebook/quick-tour.ipynb)



## 核心功能



- ✅ [内置上下文（Contexts）](https://docs.lavague.ai/en/latest/docs/get-started/customization/)（即配置项）

- ✅ [可自定义的配置](https://docs.lavague.ai/en/latest/docs/get-started/customization/)

- ✅ 用于测试和基准评估 LaVague 性能的[测试运行器](https://docs.lavague.ai/en/latest/docs/get-started/testing/)

- ✅ 用于估算 Token 使用量和成本的 [Token 计数器](https://docs.lavague.ai/en/latest/docs/get-started/token-usage/)

- ✅ [日志工具](https://docs.lavague.ai/en/latest/docs/get-started/customization/)

- ✅ 可选的交互式 [Gradio 界面](https://docs.lavague.ai/en/latest/docs/get-started/gradio/)

- ✅ [调试工具](https://docs.lavague.ai/en/latest/docs/get-started/customization/)

- ✅ [Chrome 浏览器扩展](https://docs.lavague.ai/en/latest/docs/get-started/docs-chrome/)



## 支持的驱动（Drivers）



我们支持三种驱动选项：



- Selenium Webdriver

- Playwright webdriver

- Chrome 扩展驱动



请注意，并非所有驱动都支持全部代理功能：



| Feature                  | Selenium  | Playwright       | Chrome Extension                     |

|--------------------------|-----------|------------------|--------------------------------------|

| 无头代理（Headless agents）    | ✅ | ⏳ | N/A |

| 处理 iframe     | ✅ | ✅ | ❌ |

| 打开多个标签页  | ✅ | ⏳ | ✅  |

| 高亮元素 | ✅ | ✅  | ✅ |





✅ 支持  

⏳ 即将推出  

❌ 不支持 



## 🔎 技术支持



如果你在启动 LaVague 时遇到任何问题，可以通过以下方式获取帮助：



- 查看我们的[故障排除指南](https://docs.lavague.ai/en/latest/docs/get-started/troubleshoot/)，其中列出了常见问题的信息与解决方案。

- 在 [GitHub Issues](https://github.com/lavague-ai/LaVague/issues) 中提交问题并描述你的具体情况

- 在我们的 [Discord](https://discord.gg/SDxn9KpqX9") 服务器的 '#support' 频道留言



## 🙋 贡献指南



我们非常欢迎你在构建稳健可靠的网页自动化大型动作模型的过程中提供帮助与支持。



为避免多人重复开发同一功能导致无法合并代码的情况，我们制定了以下贡献流程：



1) 📢 我们通过 [`GitHub Issues`](https://github.com/lavague-ai/LaVague/issues) 规划任务：建议优先查看带有 [`help-wanted`](https:/github.com/lavague-ai/LaVague/labels/help%20wanted) 和 [`good first issue`](https://github.com/lavague-ai/LaVague/labels/good%20first%20issue) 标签的 Issue

2) 🙋‍♀️ 如果你有兴趣负责其中某项任务，请在该 Issue 下留言！ 

3) 🤝 我们将与你沟通，并为你分配带有 [`community assigned`](https://github.com/lavague-ai/LaVague/labels/community-assigned) 标签的任务 

4) 💬 随后我们将随时为你提供关于该任务的讨论与支持

5) ⬆️ 请将你的工作成果以 PR（Pull Request）形式提交

6) ✅ 我们将审查并合并你的代码，或提出修改建议/反馈



更多详细信息请查阅我们的[`贡献指南`](https://docs.lavague.ai/en/latest/docs/contributing/contributing/)。



## 🗺️ 路线图



如需了解项目待办事项的最新进展，请访问[此处](https://github.com/orgs/lavague-ai/projects/1/views/2)。



## 💰 运行代理的成本是多少？



LaVague 在底层使用 LLM（默认使用 OpenAI 的 `gpt4-o`，但完全可自定义）。



这些 LLM 调用的成本取决于： 

- 为特定代理选择的模型

- 目标的复杂程度

- 你正在交互的网站。 



请参阅我们的[专用文档（Token 计数与成本估算）](https://docs.lavague.ai/en/latest/docs/get-started/token-usage/)，了解如何追踪所有 Token 并估算运行代理的成本。



## 📈 数据收集

我们希望构建一个数据集，供 AI 社区用于开发更优秀的网页大型动作模型（Large Action Models）。你可以在我们的 [BigAction HuggingFace 页面](https://huggingface.co/BigAction) 查看我们目前为社区构建的数据集。

因此，LaVague 默认收集以下用户遥测数据：

- LaVague 安装版本
- 每次网页动作步骤生成的代码/动作列表
- 历史动作记录
- “观测”（用于检查当前页面的方法）
- 使用的 LLM（例如 GPT4）
- 使用的多模态 LLM（例如 GPT4）
- 随机生成的匿名用户 ID
- 你使用的是 CLI 命令（如 lavague-qa）、Gradio 演示还是直接调用我们的库。
- 设定的目标（Objective）
- 代理的思考链（Chain of thoughts）
- 页面上的交互区域（边界框坐标）
- 浏览器视口尺寸
- 当前步骤编号
- 生成的指令及当前使用的引擎
- Token 成本与使用情况
- 执行动作的 URL
- 动作是否失败或成功
- 指定的额外用户数据
- 错误信息（如适用）
- 源节点（从网页检索以执行此操作的 HTML 代码块）

**请注意，切勿在目标设定和额外用户数据中包含任何个人信息。如果你打算在目标/额外数据中涉及个人信息，强烈建议关闭遥测功能。**



### 🚫 关闭所有遥测数据



如果你想关闭所有遥测功能，请将 `LAVAGUE_TELEMETRY` 环境变量设置为 `"NONE"`。



关于如何设置你的 `LAVAGUE_TELEMTRY` 环境变量，请参阅我们的指南 [此处](https://docs.lavague.ai/en/latest/docs/get-started/FAQs/#how-can-i-set-environment-variables)。
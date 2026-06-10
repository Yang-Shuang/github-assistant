# 将你的 $20 Cursor 升级为类 Devin AI 助手

本仓库提供了所需的一切，助你为 Cursor/Windsurf IDE 或 GitHub Copilot 注入**高级**智能体（Agentic AI）能力——类似于 Devin 的 $25/任务定价（根据官方文档计算：Core 计划中为 $2.25/ACU，复杂度在 5-12.5 ACU 之间），但成本仅为其中的一小部分。只需不到一分钟，你将获得：

* 自动规划与自我进化，让你的 AI “先思考后行动”，并从错误中学习
* 扩展工具调用能力，包括网页浏览、搜索引擎查询以及由大语言模型（LLM）驱动的文本/图像分析
* [实验性] 多智能体协作：由 o1 负责规划，普通 Claude/GPT-4o 负责执行。

## 为什么这很重要

Devin 令人印象深刻之处在于，它表现得像一名实习生：自己编写计划、在执行过程中更新计划，甚至根据你的反馈进行自我进化。但你无需承担 Devin $25/任务的费用也能获得大部分功能。只需自定义 `.cursorrules` 文件并搭配几个 Python 脚本，你就能在 Cursor 内部解锁同样的高级特性。

## 核心亮点

1.	轻松配置
   
   提供两种入门方式：

   **选项 1：使用 Cookiecutter（推荐）**
   ```bash
   # Install cookiecutter if you haven't
   pip install cookiecutter

   # Create a new project
   cookiecutter gh:grapeot/devin.cursorrules --checkout template
   ```

   **选项 2：手动配置**
   将 `tools` 文件夹及以下配置文件复制到你的项目根目录：Windsurf 用户需要同时包含 `.windsurfrules` 和 `scratchpad.md` 文件。Cursor 用户仅需 `.cursorrules` 文件。GitHub Copilot 用户需使用 `.github/copilot-instructions.md` 文件。

2.	规划器-执行者多智能体架构（实验性）

   我们的新 [多智能体分支](https://github.com/grapeot/devin.cursorrules/tree/multi-agent) 引入了一个高级规划器（由 o1 驱动），负责协调复杂任务；以及一个执行者（由 Claude/GPT 驱动），负责逐步落实具体操作。这种双智能体架构大幅提升了方案质量、交叉验证能力和迭代速度。

3.	扩展工具集

   包含：
   
   * 网页抓取（基于 Playwright）
   * 搜索引擎集成（DuckDuckGo）
   * 大语言模型（LLM）驱动的分析

   AI 会自动决定如何以及何时调用这些工具（就像 Devin 一样）。

   注意：对于截图验证功能，首次使用时将自动安装 Playwright 浏览器。

4.	自我进化

   每当你对 AI 进行纠正时，它都能更新 `.cursorrules` 中的“经验教训”。随着时间的推移，它会积累特定项目的知识，并在每次迭代中变得越来越聪明。这使得 AI 成为一个可指导且值得投入的合作伙伴。
	
## 使用方法

如需详细了解如何在 Cursor 中配置和使用 devin.cursorrules，请查阅我们的[分步教程](step_by_step_tutorial.md)。该指南涵盖了从初始环境设置、配置 devin.cursorrules 到使用增强功能的全部内容。

1.	选择你的配置方式：
   - **Cookiecutter（推荐）**：运行命令后按提示操作即可
   - **手动**：从本仓库复制所需文件

2.	配置你的环境：
   - 设置 API Key（可选）

3.	开始以完全智能体化的方式探索高级任务——例如数据收集、快速构建原型或交叉引用外部资源。

## 想要了解更多细节？

查看我们的[博客文章](https://yage.ai/cursor-to-devin-en.html)，了解我们如何在一小时内将每月 $20 的成本转化为 $25/任务级别的 AI 能力。文章详细阐述了流程规划、自我进化以及全自动工作流背后的设计理念。你还会看到 Devin、Cursor 和 Windsurf 的对比评测，以及从零开始搭建整套环境的分步教程。

许可证：MIT
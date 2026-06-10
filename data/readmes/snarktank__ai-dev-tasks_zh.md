# AI Dev Tasks

欢迎使用 **AI Dev Tasks**！本仓库提供了一系列 Markdown 文件，旨在通过 AI 驱动的 IDE 和 CLI 工具大幅提升你的功能开发工作流。这些工具可与任何 AI 编程助手（包括 [Amp](https://ampcode.com)、Claude Code、Windsurf 等）配合使用。借助这些结构化的提示词（prompt），你可以系统性地推进功能构建，从构思到实现，并内置验证检查点。

别再与冗长庞大的 AI 请求搏斗了，开始一步步引导你的 AI 协作者吧！

## 核心思路

使用 AI 构建复杂功能有时感觉像个“黑盒”。本工作流旨在通过以下方式为该过程带来结构化、清晰度和可控性：

1. **明确范围：** 利用产品需求文档（Product Requirement Document, PRD）清晰地勾勒出需要构建的内容。
2. **详细规划：** 将 PRD 拆解为细致、可执行的任务列表。
3. **迭代实现：** 引导 AI 每次只处理一个任务，以便你审查并批准每一项更改。

这种结构化方法有助于确保 AI 保持在正确的轨道上运行，使问题调试更加容易，并让你对生成的代码更有信心。

## 工作流：从构思到实现的功能

以下是使用本仓库中 `.md` 文件的分步流程：

### 1. 创建产品需求文档（PRD）

首先，为你的功能搭建蓝图。PRD 能明确你要构建什么、为谁而建以及为什么而建。

你可以直接在所选的 AI 工具中创建一个轻量级 PRD：

1. 确保你能访问本仓库中的 `create-prd.md` 文件。
2. 在你的 AI 工具中，发起 PRD 创建流程：

    ```text
    Use @create-prd.md
    Here's the feature I want to build: [Describe your feature in detail]
    Reference these files to help you: [Optional: @file1.py @file2.ts]
    ```


    ![Example of initiating PRD creation](https://pbs.twimg.com/media/Go6DDlyX0AAS7JE?format=jpg&name=large)

### 2. 从 PRD 生成任务列表

草稿完成你的 PRD（例如 `MyFeature-PRD.md`）后，下一步是为你的人工智能开发者生成一份详细的分步实施计划。

1. 确保你能访问 `generate-tasks.md`。
2. 在你的 AI 工具中，使用 PRD 来创建任务：

    ```text
    Now take @MyFeature-PRD.md and create tasks using @generate-tasks.md
    ```
    *（注：请将 `@MyFeature-PRD.md` 替换为你在第 1 步中生成的实际 PRD 文件名。）*

    ![Example of generating tasks from PRD](https://pbs.twimg.com/media/Go6FITbWkAA-RCT?format=jpg&name=medium)

### 3. 查看任务列表

现在你将拥有一个结构良好的任务列表，通常包含任务和子任务，随时准备让 AI 开始工作。这为实施提供了清晰的路径图。

![Example of a generated task list](https://pbs.twimg.com/media/Go6GNuOWsAEcSDm?format=jpg&name=medium)

### 4. 指示 AI 逐步处理任务（并标记完成）

为确保有条不紊的进度并便于验证，请指示 AI 每次只按子任务顺序处理任务列表。

1. 在你的 AI 工具中，告诉 AI 从第一个任务（例如 `1.1`）开始：

    ```text
    Please start on task 1.1 from the generated task list.
    ```

    AI 将尝试执行该任务，随后提示你进行审查。

    ![Example of starting on a task](https://pbs.twimg.com/media/Go6I41KWcAAAlHc?format=jpg&name=medium)

### 5. 进度推进

AI 将继续处理列表中剩余的任务。

![Example of a progressing task list with completed items](https://pbs.twimg.com/media/Go6KrXZWkAA_UuX?format=jpg&name=medium)

虽然并非总是完美无缺，但此方法已被证明是借助 AI 构建较大功能时非常可靠的途径。

### 视频演示

如果你想看实际操作效果，我曾在 [Claire Vo 的 “How I AI” 播客](https://www.youtube.com/watch?v=fD4ktSkNCw4) 上进行了演示。

[![Demonstration of AI Dev Tasks on How I AI Podcast](https://img.youtube.com/vi/fD4ktSkNCw4/maxresdefault.jpg)](https://www.youtube.com/watch?v=fD4ktSkNCw4).

## 本仓库文件说明

* **`create-prd.md`**：引导 AI 为你的功能生成产品需求文档。
* **`generate-tasks.md`**：接收 PRD Markdown 文件作为输入，并帮助 AI 将其拆解为详细的分步实施任务列表。

## 优势

* **结构化开发：** 强制执行从构思到代码的清晰流程。
* **分步验证：** 允许你在每个小步骤中审查并批准 AI 生成的代码，确保质量与可控性。
* **管理复杂性：** 将大型功能拆解为更小、更易消化的任务供 AI 处理，降低其迷失方向或生成过于复杂/错误代码的概率。
* **提升可靠性：** 与单一的大提示词相比，为利用 AI 进行重大开发工作提供了更可靠的方法。
* **清晰的进度追踪：** 提供已完成任务的可视化展示，便于直观了解已完成的工作量及下一步计划。

## 使用方法

1. **克隆或下载：** 将这些 `.md` 文件获取到你的项目中，或放置于你的 AI 工具可访问的集中位置。
   ```bash
   git clone https://github.com/snarktank/ai-dev-tasks.git
   ```
2. **遵循工作流：** 按照上述工作流的描述，在你的 AI 助手中有系统地使用这些 `.md` 文件。
3. **适配与迭代：**
    * 欢迎修改 `.md` 文件中的提示词（prompt），以更好地适应你的特定需求或编码风格。
    * 如果 AI 在处理某个任务时遇到困难，可尝试重新表述初始功能描述，或将任务进一步拆分。

## 成功技巧

* **保持具体明确：** 你提供的上下文和清晰指令越多（无论是初始功能描述还是后续澄清），AI 的输出效果就会越好。
* **正确标记文件：** 生成任务时，务必准确标注 PRD 文件名（例如 `@MyFeature-PRD.md`）。
* **耐心与迭代：** AI 是强大的工具，但并非魔法。请做好引导、纠正和迭代的准备。本工作流正是为了简化这一迭代过程而设计的。

## 贡献指南

有改进这些 `.md` 文件的想法，或有新文件适合此工作流？欢迎贡献！

请随时：

* 提交 Issue（问题）以讨论更改或建议新功能。
* 提交 Pull Request（PR）带来你的改进。

---

祝你享受 AI 辅助开发的乐趣！
<h1 align="center">Copilot for Obsidian</h1>

<h2 align="center">
你第二大脑的终极 AI 助手
</h2>

<p align="center">
  <img src="https://img.shields.io/github/v/release/logancyang/obsidian-copilot?style=for-the-badge&sort=semver" alt="GitHub release (latest SemVer)">
  <img src="https://img.shields.io/badge/dynamic/json?logo=obsidian&color=%23483699&label=downloads&query=%24%5B%22copilot%22%5D.downloads&url=https%3A%2F%2Fraw.githubusercontent.com%2Fobsidianmd%2Fobsidian-releases%2Fmaster%2Fcommunity-plugin-stats.json&style=for-the-badge" alt="Obsidian Downloads">
</p>

<p align="center">
  <a href="https://www.obsidiancopilot.com/en/docs">文档</a> |
  <a href="https://www.youtube.com/@loganhallucinates">YouTube</a> |
  <a href="https://github.com/logancyang/obsidian-copilot/issues/new?template=bug_report.md">报告问题</a> |
  <a href="https://github.com/logancyang/obsidian-copilot/issues/new?template=feature_request.md">请求功能</a>
</p>

<p align="center">
  <a href="https://example.com](https://obsidian.md/blog/2024-goty-winners/">
    <img src="./images/reward-banner.svg" alt="Reward Banner" width="400"/>
  </a>
</p>

## The What

_Copilot for Obsidian_ 是你在 Vault（知识库）内的 AI 助手，支持基于聊天的知识库搜索、网页和 YouTube 内容解析、强大的上下文处理，以及在 Obsidian 高度可定制工作区中不断扩展的 Agent（智能体）能力——同时确保你的数据始终由**你**掌控。

## The Why

如今的 AI 巨头希望**将你困住**：你的数据存放在他们的服务器上，提示词被锁定在他们的模型中，高昂的迁移成本让你不得不持续付费。一旦他们调整定价、关闭功能或封禁账号，你积累的一切都将付诸东流。

我们正致力于构建相反的理念。我们的目标是打造一种无厂商锁定、可自由迁移的 Agent（智能体）体验。**数据始终属于你。** 使用任何你喜欢的 LLM（大语言模型）。想象一下，当一款全新模型发布时，你可以直接在自己的硬件上运行它，而它已经了解你的情况（长期记忆），知道如何执行你过去定义过的_相同的命令和工具_（仅作为 Markdown 文件存储），并成为真正由你_拥有_的思维伙伴与助手。这是与你共同成长的 AI，而不是让你成为订阅制“人质”的服务。

这是我们坚信的未来。如果你认同这一愿景，请支持本项目！

## Key Features

- **🔒 Your data is 100% yours**: Local search and storage, and full control of your data if you use self-hosted models.
  -> **🔒 数据 100% 属于你**：本地搜索与存储，若使用自托管模型则完全掌控你的数据。
- **🧠 Bring Your Own Model**: Tap any OpenAI-compatible or local model to uncover insights, spark connections, and create content.
  -> **🧠 自带模型（BYOM）**：接入任意兼容 OpenAI 的接口或本地模型，挖掘洞察、激发灵感并生成内容。
- **🖼️ Multimedia understanding**: Drop in webpages, YouTube videos, images, PDFs, EPUBS, or real-time web search for quick insights.
  -> **🖼️ 多媒体理解**：拖入网页、YouTube 视频、图片、PDF、EPUB，或使用实时网络搜索，快速获取洞察。
- **🔍 Smart Vault Search**: Search your vault with chat, no setup required. Embeddings are optional. Copilot delivers results right away.
  -> **🔍 智能知识库搜索**：通过聊天即可搜索你的知识库，无需额外配置。向量嵌入（Embeddings）为可选项，Copilot 即刻返回结果。
- **✍️ Composer and Quick Commands**: Interact with your writing with chat, apply changes with 1 click.
  -> **✍️ 编辑器与快捷命令**：通过聊天与你的笔记交互，一键应用更改。
- **🗂️ Project Mode**: Create AI-ready context based on folders and tags. Think NotebookLM but inside your vault!
  -> **🗂️ 项目模式**：基于文件夹和标签创建适用于 AI 的上下文。就像把 NotebookLM 搬进了你的知识库！
- **🤖 Agent Mode (Plus)**: Unlock an autonomous agent with built-in tool calling. No commands needed. Copilot automatically triggers vault, web searches or any other relevant tool when relevant.
  -> **🤖 Agent（智能体）模式（Plus）**：解锁内置工具调用的自主 Agent。无需手动输入命令，Copilot 会在相关场景自动触发知识库搜索、网络搜索或其他适用工具。

<p align="center">
  <em>Copilot's Agent can call the proper tools on its own upon your request.</em>
</p>
<p align="center">
  <img src="./images/product-ui-screenshot.png" alt="Product UI screenshot" width="800"/>
</p>

## Table of Contents

- [核心定位](#the-what)
- [设计初衷](#the-why)
- [关键特性](#key-features)
- [Copilot v4：重塑 Agent 模式 🚀](#copilot-v4-agent-mode-reimagined-)
- [用户好评 ❤️](#why-people-love-it-️)
- [快速上手](#get-started)
  - [安装 Obsidian Copilot](#install-obsidian-copilot)
  - [配置 API 密钥](#set-api-keys)
- [使用指南](#usage)
  - [免费用户](#free-user)
    - [**聊天模式：引用笔记并与 Copilot 探讨想法**](#chat-mode-reference-notes-and-discuss-ideas-with-copilot)
    - [**知识库问答模式：与整个知识库对话**](#vault-qa-mode-chat-with-your-entire-vault)
    - [Copilot 命令面板](#copilots-command-palette)
    - [**相关笔记：基于语义相似度和链接的笔记推荐**](#relevant-notes-notes-suggestions-based-on-semantic-similarity-and-links)
  - [Copilot Plus/支持者](#copilot-plusbeliever)
    - [**获取特定时间窗口的精准洞察**](#get-precision-insights-from-a-specific-time-window)
    - [**Agent（智能体）模式：自主工具调用**](#agent-mode-autonomous-tool-calling)
    - [**理解笔记中的图片**](#understand-images-in-your-notes)
    - [**一条提示词，全源解析——PDF、视频与网页即时摘要**](#one-prompt-every-sourceinstant-summaries-from-pdfs-videos-and-web)
- [**需要帮助？**](#need-help?)
- [**常见问题（FAQ）**](#faq)
- [**🙏 鸣谢**](#-thank-you)
- [**Copilot Plus 披露声明**](#copilot-plus-disclosure)
- [**作者团队**](#authors)

## Copilot v4: Agent Mode, Reimagined 🚀

这是我们迄今为止最大的飞跃。**Copilot v4** 允许你在知识库内原生运行目前最强大的编程 Agent —— **opencode**、**Claude Code** 或 **Codex**，专为知识工作优化，完全由你掌控。自带你的 Agent，将每条笔记保存在本地设备上，让它为你规划、搜索并在你的“第二大脑”中采取行动。无厂商锁定，无需妥协。

**加入支持者计划，即刻体验 Copilot v4 的魔力！**

👉 **[探索 Copilot v4 →](https://www.obsidiancopilot.com/v4)**

## Why People Love It ❤️

- *"Copilot is the missing link that turns Obsidian into a true second brain. I use it to draft investment memos with text, code, and visuals—all in one place. It’s the first tool that truly unifies how I search, process, organize, and retrieve knowledge without ever leaving Obsidian. With AI-powered search, organization, and reasoning built into my notes, it unlocks insights I’d otherwise miss. My workflow is faster, deeper, and more connected than ever—I can’t imagine working without it."* 
  -> “Copilot 是缺失的那一环，它将 Obsidian 真正变成了第二大脑。我用它来撰写包含文本、代码和视觉元素的投资备忘录——全部集中在一个地方。它是第一款真正统一了我搜索、处理、组织和检索知识方式的工具，且无需离开 Obsidian。AI 驱动的搜索、组织与推理功能内置于我的笔记中，解锁了以往容易遗漏的洞察。我的工作流变得更快、更深、更紧密相连——我无法想象没有它该如何工作。” - @jasonzhangb, 投资者兼研究分析师
- *"Since discovering Copilot, my writing process has been completely transformed. Conversing with my own articles and thoughts is the most refreshing experience I’ve had in decades.”* 
  -> “自发现 Copilot 以来，我的写作流程发生了彻底转变。与我自己的文章和思想进行对话，是我几十年来体验过最耳目一新的事情。” - Mat QV, 作家
- *"Copilot has transformed our family—not just as a productivity assistant, but as a therapist. I introduced it to my non‑technical wife, Mania, who was stressed about our daughter’s upcoming exam; within an hour, she gained clarity on her mindset and next steps, finding calm and confidence."* 
  -> “Copilot 改变了我们的家庭——它不仅是生产力助手，更像一位心理治疗师。我将它介绍给我非技术背景的妻 MANIA，她正为女儿即将到来的考试感到焦虑；短短一小时内，她就理清了思路并明确了下一步行动，重获平静与自信。” - @screenfluent, 一位贴心的丈夫

## Get Started

### Install Obsidian Copilot

1. Open **Obsidian → Settings → Community plugins**.
   -> 打开 **Obsidian → 设置 → 社区插件**。
2. Turn off **Safe mode** (if enabled).
   -> 关闭**安全模式**（如果已启用）。
3. Click **Browse**, search for **“Copilot for Obsidian”**.
   -> 点击**浏览**，搜索“Copilot for Obsidian”。
4. Click **Install**, then **Enable**.
   -> 点击**安装**，然后**启用**。

### Set API Keys

**Free User**

1. Go to **Obsidian → Settings → Copilot → Basic** and click **Set Keys**.
   -> 前往 **Obsidian → 设置 → Copilot → 基础**，点击**配置密钥**。
2. Choose your AI provider(s) (e.g., **OpenRouter, Gemini, OpenAI, Anthropic, Cohere**) and paste your API key(s). **OpenRouter is recommended.**
   -> 选择你的 AI 提供商（如 **OpenRouter、Gemini、OpenAI、Anthropic、Cohere**）并粘贴 API 密钥。**推荐使用 OpenRouter。**

**Copilot Plus/Believer**

1. Copy your license key at your [dashboard](https://www.obsidiancopilot.com/en/dashboard). _Don’t forget to join our wonderful Discord community!_
   -> 在[控制面板](https://www.obsidiancopilot.com/en/dashboard)复制你的许可证密钥。_别忘了加入我们的 Discord 社区！_
2. Go to **Obsidian → Settings → Copilot → Basic** and paste the key into in the **Copilot Plus** card.
   -> 前往 **Obsidian → 设置 → Copilot → 基础**，将密钥粘贴到 **Copilot Plus** 卡片中。

## Usage

### Free User

#### **Chat Mode: reference notes and discuss ideas with Copilot**

Use `@` to add context and chat with your note.
-> 使用 `@` 添加上下文，与你的笔记进行对话。

<p align="center">
    <img src="./images/Add-Context.png" alt="Chat Mode" width="700">
</p>

Ask Copilot:
> _Summarize [[Q3 Retrospective]] and identify the top 3 action items for Q4 based on the notes in {01-Projects}._
-> 向 Copilot 提问：
> _总结 [[Q3 Retrospective]] 的内容，并根据 {01-Projects} 中的笔记列出 Q4 的三大行动项。_

<p align="center">
    <img src="./images/Chat-Mode.png" alt="Chat Mode" width="700">
</p>

#### **Vault QA Mode: chat with your entire vault**

Ask Copilot:
> _What are the recurring themes in my research regarding the intersection of AI and SaaS?_
-> 向 Copilot 提问：
> _在我的研究中，关于人工智能（AI）与软件即服务（SaaS）交叉领域的反复出现的主题有哪些？_

<p align="center">
    <img src="./images/Vault-Mode.png" alt="Vault Mode" width="700">
</p>

#### Copilot's Command Palette

Copilot's Command Palette puts powerful AI capabilities at your fingertips. Access all commands in chat window via `/` or via right-click menu on selected text.
-> Copilot 的命令面板将强大的 AI 功能触手可及。在聊天窗口中通过 `/` 或选中文字后的右键菜单访问所有命令。

**Add selection to chat context**
Select text and add it to context. Recommend shortcut: `ctrl/cmd + L`
-> **将选区添加到聊天上下文**：选中文本并将其加入上下文。推荐快捷键：`ctrl/cmd + L`

<p align="center">
    <img src="./images/Add-Selection-to-Context.png" alt="Add Selection to Context" width="700">
</p>

**Quick Command**
Select text and apply action without opening chat. Recommend shortcut: `ctrl/cmd + K`
-> **快捷命令**：选中文本并直接执行操作，无需打开聊天窗口。推荐快捷键：`ctrl/cmd + K`

<p align="center">
    <img src="./images/Quick-Command.png" alt="Quick Command" width="700">
</p>

**Edit and Apply with One Click**
Select text and edit with one RIGHT click.
-> **一键编辑与应用**：选中文本并通过右键单击进行编辑。

<p align="center">
    <img src="./images/One-Click-Commands.png" alt="One-Click Commands" width="700">
</p>

**Create your Command**
Create commands and workflows in `Settings → Copilot → Command → Add Cmd`.
-> **创建你的命令**：在 `设置 → Copilot → 命令 → 添加命令` 中创建命令和工作流。

<p align="center">
    <img src="./images/Create-Command.png" alt="Create Command" width="700">
</p>

**Command Palette in Chat**
Type `/` to use Command Palette in chat window.
-> **聊天中的命令面板**：在聊天窗口中输入 `/` 即可使用命令面板。

<p align="center">
    <img src="./images/Prompt-Palette.png" alt="Prompt Palette" width="700">
</p>

#### **Relevant Notes: notes suggestions based on semantic similarity and links**

Appears automatically when there's useful related content and links. Use it to quickly reference past research, ideas, or decisions—no need to search or switch tabs.
-> 当存在有用的相关内容和链接时自动显示。用于快速查阅过往研究、想法或决策——无需搜索或切换标签页。

<p align="center">
    <img src="./images/Relevant-Notes.png" alt="Relevant Notes" width="700">
</p>

### Copilot Plus/Believer

Copilot Plus brings powerful AI agentic capabilities, context-aware actions and seamless tool integration—built to elevate your knowledge work in Obsidian.
-> Copilot Plus 带来强大的 AI Agent（智能体）能力、上下文感知操作与无缝工具集成，旨在提升你在 Obsidian 中的知识工作效率。

#### **Get Precision Insights From a Specific Time Window**

In agent mode, ask copilot:
> _What did I do last week?_
-> 在 Agent 模式下向 Copilot 提问：
> _我上周做了什么？_

<p align="center">
    <img src="./images/Time-Based-Queries.png" alt="Time-Based Queries" width="700">
</p>

#### **Agent Mode: Autonomous Tool Calling**

Copilot's agent automatically calls the right tools—no manual commands needed. Just ask, and it searches the web, queries your vault, and combines insights seamlessly.
Ask Copilot in agent mode:
> _Research web and my vault and draft a note on AI SaaS onboarding best practices._
-> Copilot 的 Agent 会自动调用合适的工具——无需手动输入命令。只需提问，它便会自动搜索网络、查询你的知识库并无缝整合洞察。
在 Agent 模式下向 Copilot 提问：
> _调研网络和我的知识库，起草一篇关于 AI SaaS 用户入职最佳实践的笔记。_

<p align="center">
    <img src="./images/Agent-Mode.png" alt="Agent Mode" width="700">
</p>

#### **Understand Images in Your Notes**

Copilot can analyze images embedded in your notes—from wireframes and diagrams to screenshots and photos. Get detailed feedback, suggestions, and insights based on visual content.
Ask Copilot to analyze your wireframes:
> _Analyze the wireframe in [[UX Design - Mobile App Wireframes]] and suggest improvements for the navigation flow._
-> Copilot 可分析嵌入你笔记中的图像——从线框图、图表到截图和照片。基于视觉内容获取详细的反馈、建议与洞察。
请 Copilot 分析你的线框图：
> _分析 [[UX Design - Mobile App Wireframes]] 中的线框图，并为导航流程提出改进建议。_

<p align="center">
    <img src="./images/Note-Image.png" alt="Image Understanding" width="700">
</p>

#### **One Prompt, Every Source—Instant Summaries from PDFs, Videos, and Web**

In agent mode, ask Copilot
> \*Compare the information about [Agent Memory] from this youtube video: [URL], this PDF [file], and @web[search results]. Start with your conclusion in bullet points in your response*
-> 在 Agent 模式下向 Copilot 提问：
> _对比以下来源中关于 [Agent Memory] 的信息：YouTube 视频 [链接]、PDF [文件]，以及 @web[搜索结果]。请在回复中以要点形式先给出你的结论。*_

<p align="center">
    <img src="./images/One-Prompt-Every-Source.png" alt="One Prompt, Every Source" width="700">
</p>

## **Need Help?**

- Check the [documentation](https://www.obsidiancopilot.com/en/docs) for setup guides, how-tos, and advanced features.
  -> 查阅[文档](https://www.obsidiancopilot.com/en/docs)获取设置指南、使用教程和高级功能说明。
- Watch [Youtube](https://www.youtube.com/@loganhallucinates) for walkthroughs.
  -> 观看 [YouTube](https://www.youtube.com/@loganhallucinates) 视频教程。
- If you're experiencing a bug or have a feature idea, please follow the steps below to help us help you faster:
  -> 如果遇到 Bug 或有新功能想法，请按以下步骤操作以帮助我们更快协助你：
  - 🐛 Bug Report Checklist
    - ☑️Use the [bug report template](https://github.com/logancyang/obsidian-copilot/issues/new?template=bug_report.md) when reporting an issue
      -> 提交问题时使用[问题报告模板](https://github.com/logancyang/obsidian-copilot/issues/new?template=bug_report.md)
    - ☑️Enable Debug Mode in Copilot Settings → Advanced for more detailed logs
      -> 在 `Copilot 设置 → 高级` 中启用调试模式以获取更详细的日志
    - ☑️Open the dev console to collect error messages: Mac: Cmd + Option + I / Windows: Ctrl + Shift + I
      -> 打开开发者控制台收集错误信息：Mac: `Cmd + Option + I` / Windows: `Ctrl + Shift + I`
    - ☑️Turn off all other plugins, keeping only Copilot enabled
      -> 关闭所有其他插件，仅保留 Copilot 启用
    - ☑️Attach relevant console logs to your report
      -> 将相关的控制台日志附加到你的报告中
    - ☑️Submit your bug report [here](https://github.com/logancyang/obsidian-copilot/issues/new?template=bug_report.md)
      -> 在此提交你的 Bug 报告[这里](https://github.com/logancyang/obsidian-copilot/issues/new?template=bug_report.md)
  - 💡 Feature Request Checklist
    - ☑️Use the [feature request template](https://github.com/logancyang/obsidian-copilot/issues/new?template=feature_request.md) for requesting a new feature
      -> 请求新功能时使用[功能请求模板](https://github.com/logancyang/obsidian-copilot/issues/new?template=feature_request.md)
    - ☑️Clearly describe the feature, why it matters, and how it would help
      -> 清晰描述该功能、其重要性以及它将如何提供帮助
    - ☑️Submit your feature request [here](https://github.com/logancyang/obsidian-copilot/issues/new?template=feature_request.md)
      -> 在此提交你的功能请求[这里](https://github.com/logancyang/obsidian-copilot/issues/new?template=feature_request.md)

## **FAQ**

<details>
  <summary><strong>Why isn’t Vault search finding my notes?</strong></summary>
If you're using the Vault QA mode (or the tool <code>@vault</code> in Plus), try the following:
- Ensure you have a working embedding model from your AI model's provider (e.g. OpenAI). Watch this video: [AI Model Setup (API Key)](https://www.youtube.com/watch?v=mzMbiamzOqM)
- Ensure your Copilot indexing is up-to-date. Watch this video: [Vault Mode](https://www.youtube.com/watch?v=hBLMWE8WRFU)
- If issues persist, run <strong>Force Re-Index</strong> or use <strong>List Indexed Files</strong> from the Command Palette to inspect what's included in the index.
- ⚠️ <strong>Don’t switch embedding models after indexing</strong>—it can break the results.
</details>

<details>
  <summary><strong>为什么知识库搜索找不到我的笔记？</strong></summary>
如果你正在使用 Vault QA 模式（或 Plus 中的 <code>@vault</code> 工具），请尝试以下操作：
- 确保你的 AI 模型提供商处已配置可用的嵌入模型（例如 OpenAI）。观看此视频：[AI 模型设置 (API Key)](https://www.youtube.com/watch?v=mzMbiamzOqM)
- 确保 Copilot 索引是最新的。观看此视频：[知识库模式](https://www.youtube.com/watch?v=hBLMWE8WRFU)
- 如果问题仍然存在，请运行 <strong>强制重新索引</strong> 或使用命令面板中的 <strong>列出已索引文件</strong> 检查索引中包含的内容。
- ⚠️ <strong>不要在建立索引后切换嵌入模型</strong>——这会导致结果异常。
</details>

<details>
  <summary><strong>Why is my AI model returning error code 429: ‘Insufficient Quota’?</strong></summary>
Most likely this is happening because you haven’t configured billing with your chosen model provider—or you’ve hit your monthly quota. For example, OpenAI typically caps individual accounts at $120/month. To resolve:
- ▶️ Watch the “AI Model Setup” video: [AI Model Setup (API Key)](https://www.youtube.com/watch?v=mzMbiamzOqM)
- 🔍 Verify your billing settings in your OpenAI dashboard
- 💳 Add a payment method if one isn’t already on file
- 📊 Check your usage dashboard for any quota or limit warnings
If you’re using a different provider, please refer to their documentation and billing policies for the equivalent steps.
</details>

<details>
  <summary><strong>为什么我的 AI 模型返回错误代码 429：“配额不足”（Insufficient Quota）？</strong></summary>
这通常是因为你尚未在所选的模型提供商处配置计费信息，或者已用完当月额度。例如，OpenAI 通常对单个账户每月限额为 $120。解决方法如下：
- ▶️ 观看“AI 模型设置”视频：[AI 模型设置 (API Key)](https://www.youtube.com/watch?v=mzMbiamzOqM)
- 🔍 在 OpenAI 控制面板中核实你的计费设置
- 💳 如果尚未绑定，请添加支付方式
- 📊 查看使用量仪表板，检查是否有任何配额或限额警告
如果你使用的是其他提供商，请参阅其文档和计费政策以执行相应步骤。
</details>

<details>
  <summary><strong>Why am I getting a token limit error?</strong></summary>
Please refer to your model provider’s documentation for the context window size.
⚠️ If you set a large <strong>max token limit</strong> in your Copilot settings, you may encounter this error.
- <strong>Max tokens</strong> refers to <em>completion tokens</em>, not input tokens.
- A higher output token limit means less room for input!
🧠 Behind-the-scenes prompts for Copilot commands also consume tokens, so:
- Keep your message length short
- Set a reasonable max token value to avoid hitting the cap
💡 For QA with unlimited context, switch to the <strong>Vault QA</strong> mode in the dropdown (Copilot v2.1.0+ required).
</details>

<details>
  <summary><strong>为什么会遇到令牌限制错误？</strong></summary>
请参阅你的模型提供商文档以了解上下文窗口大小。
⚠️ 如果你在 Copilot 设置中设置了较大的 <strong>最大令牌数（max token limit）</strong>，可能会遇到此错误。
- <strong>Max tokens（最大令牌数）</strong>指的是 <em>输出/补全令牌</em>，而非输入令牌。
- 更高的输出令牌限额意味着留给输入的“空间”更少！
🧠 Copilot 命令的后台提示词也会消耗令牌，因此：
- 尽量保持消息简短
- 设置合理的最大令牌值以避免触及上限
💡 如需无上下文限制的问答功能，请在下拉菜单中切换到 <strong>Vault QA（知识库问答）</strong>模式（需 Copilot v2.1.0+）。
</details>

## **🙏 Thank You**

If you share the vision of building the most powerful AI agent for our second brain, consider [sponsoring this project](https://github.com/sponsors/logancyang) or buying me a coffee. Help spread the word by sharing Copilot for Obsidian on Twitter/X, Reddit, or your favorite platform!
-> 如果你也认同打造第二大脑最强 AI Agent 的愿景，请考虑[赞助本项目](https://github.com/sponsors/logancyang)或请我喝杯咖啡。通过在 Twitter/X、Reddit 或其他你喜欢的平台分享 Copilot for Obsidian 来帮助我们传播！

<p align="center">
  <img src="https://camo.githubusercontent.com/7b8f7343bfc6e3c65c7901846637b603fd812f1a5f768d8b0572558bde859eb9/68747470733a2f2f63646e2e6275796d6561636f666665652e636f6d2f627574746f6e732f76322f64656661756c742d79656c6c6f772e706e67" alt="BuyMeACoffee" width="200">
</p>

**Acknowledgments**
-> **鸣谢**

Special thanks to our top sponsors: @mikelaaron, @pedramamini, @Arlorean, @dashinja, @azagore, @MTGMAD, @gpythomas, @emaynard, @scmarinelli, @borthwick, @adamhill, @gluecode, @rusi, @timgrote, @JiaruiYu-Consilium, @ddocta, @AMOz1, @chchwy, @pborenstein, @GitTom, @kazukgw, @mjluser1, @joesfer, @rwaal, @turnoutnow-harpreet, @dreznicek, @xrise-informatik, @jeremygentles, @ZhengRui, @bfoujols, @jsmith0475, @pagiaddlemon, @sebbyyyywebbyyy, @royschwartz2, @vikram11, @amiable-dev, @khalidhalim, @DrJsPBs, @chishaku, @Andrea18500, @shayonpal, @rhm2k, @snorcup, @JohnBub, @obstinatelark, @jonashaefele, @vishnu2kmohan
-> 特别感谢我们的顶级赞助商：@mikelaaron, @pedramamini, @Arlorean, @dashinja, @azagore, @MTGMAD, @gpythomas, @emaynard, @scmarinelli, @borthwick, @adamhill, @gluecode, @rusi, @timgrote, @JiaruiYu-Consilium, @ddocta, @AMOz1, @chchwy, @pborenstein, @GitTom, @kazukgw, @mjluser1, @joesfer, @rwaal, @turnoutnow-harpreet, @dreznicek, @xrise-informatik, @jeremygentles, @ZhengRui, @bfoujols, @jsmith0475, @pagiaddlemon, @sebbyyyywebbyyy, @royschwartz2, @vikram11, @amiable-dev, @khalidhalim, @DrJsPBs, @chishaku, @Andrea18500, @shayonpal, @rhm2k, @snorcup, @JohnBub, @obstinatelark, @jonashaefele, @vishnu2kmohan

## **Copilot Plus Disclosure**

Copilot Plus is a premium product of Brevilabs LLC and it is not affiliated with Obsidian. It offers a powerful agentic AI integration into Obsidian. Please check out our website [obsidiancopilot.com](https://www.obsidiancopilot.com/) for more details!
- An account and payment are required for full access.
  -> Copilot Plus 是 Brevilabs LLC 的付费产品，与 Obsidian 官方无关。它提供强大的 AI Agent（智能体）集成体验至 Obsidian。请访问我们的官网 [obsidiancopilot.com](https://www.obsidiancopilot.com/) 了解详情！
- An account and payment are required for full access. -> 需要账户和付费才能获取完整功能。
- Copilot Plus requires network use to facilitate the AI agent. -> Copilot Plus 需要联网以支持 AI Agent 运行。
- **Privacy & Data Handling**:
  - **Free tier**: Your messages and notes are sent only to your configured LLM provider (OpenAI, Anthropic, Google, etc.). Nothing goes to Brevilabs servers.
    -> **隐私与数据处理**：
      - **免费层**：你的消息和笔记仅发送至你配置的 LLM 提供商（如 OpenAI、Anthropic、Google 等）。数据不会上传至 Brevilabs 服务器。
      - **Plus 层**：消息发送至你配置的 LLM 提供商。文件转换（PDF、DOCX、EPUB、图片等）仅在通过 `@` 命令显式触发相关功能时，由 Brevilabs 服务器进行处理。
      - **处理与保留**：我们仅为交付你所请求的功能而临时处理你的数据，随后立即丢弃。处理后不会在我们的服务器上保留任何消息内容、上传文件或文档。
      - **用户 ID**：随机生成的 UUID 会随 Plus API 请求发送，仅用于服务交付（防止许可证滥用、限流），不用于用户追踪、画像或数据分析。
- Please see the privacy policy on the website for more details. -> 详情请参阅官网上的隐私政策。
- The frontend code of Copilot plugin is fully open-source. However, the backend code facilitating the AI agents is close-sourced and proprietary. -> Copilot 插件的前端代码完全开源。然而，支持 AI Agent 的后端代码为闭源专有软件。
- We offer a full refund if you are not satisfied with the product within 14 days of your purchase, no questions asked. -> 如果您在购买后 14 天内对产品不满意，我们提供无条件全额退款。

## **Authors**

Brevilabs Team | Email: logan@brevilabs.com | X/Twitter: [@logancyang](https://twitter.com/logancyang)
-> Brevilabs 团队 | 邮箱：logan@brevilabs.com | X/Twitter：[@logancyang](https://twitter.com/logancyang)
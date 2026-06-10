# 为 Agent AI 系统设计高效提示词：模式与实践

## 目录

*   [引言：Agent AI 的蓝图](#introduction-the-blueprint-of-agentic-ai)
*   [基础：核心原则](#the-foundation-core-principles-of-agentic-prompts)
    *   [1. 明确的角色定义与范围](#1-clear-role-definition-and-scope)
    *   [2. 结构化指令与组织方式](#2-structured-instructions-and-organization)
    *   [3. 明确的工具集成与使用指南](#3-explicit-tool-integration-and-usage-guidelines)
    *   [4. 逐步推理与规划](#4-step-by-step-reasoning-and-planning)
    *   [5. 环境与上下文感知](#5-environment-and-context-awareness)
    *   [6. 领域特定知识与约束条件](#6-domain-specific-expertise-and-constraints)
    *   [7. 安全性、对齐与拒绝协议](#7-safety-alignment-and-refusal-protocols)
    *   [8. 一致的语气与交互风格](#8-consistent-tone-and-interaction-style)
*   [案例研究：分析真实提示词](#case-studies-analyzing-real-world-prompts)
    *   [Vercel v0：UI 生成与组件工具](#vercel-v0-ui-generation--component-tooling)
    *   [same.new：Agent 结对编程与严格工具调用](#samenew-agentic-pair-programming--strict-tooling)
    *   [Manus：通用 Agent 与显式循环](#manus-general-purpose-agent--explicit-loop)
    *   [OpenAI ChatGPT (GPT-4.5/4o)：集成工具与策略](#openai-chatgpt-gpt-454o-integrated-tools--policies)
    *   [其他系统备注（Cline, Bolt, Augment, Claude Code, Clawdbot）](#notes-on-other-systems-cline-bolt-augment-claude-code-clawdbot)
*   [提炼最佳实践：构建者的关键要点](#synthesizing-best-practices-key-takeaways-for-builders)
*   [独特惯例与架构差异](#unique-conventions--architectural-differences)
*   [结语：构建 Agent AI 的未来](#conclusion-building-the-agentic-future)
*   [Visual AI Agent: Harpagan](https://harpagan.com)


---

## 引言：Agent AI 的蓝图

Agent（智能体）人工智能系统的兴起标志着从纯对话模型向能够主动执行任务、交互工具并自主追求复杂目标的 AI 的重大转变。这些具备规划、执行命令、编辑文件、浏览网页等能力的系统，有望彻底改变我们与技术的互动方式，并增强人类能力。

每个高效 Agent AI 的核心都在于其**系统提示词（system prompt）**。它不仅仅是初始指令，更是指导 AI 行为、能力、限制和人格的基础蓝图、操作手册甚至“宪法”。精心设计的系统提示词对于确保 Agent 以可靠、安全且有效的方式实现用户目标至关重要。

本指南深入探讨设计这些关键提示词的艺术与科学。通过分析 [awesome-ai-system-prompts](https://github.com/dontriskit/awesome-ai-system-prompts) 仓库中多样化的真实世界系统提示词——特别是聚焦于 Vercel 的 v0、same.new、Manus、OpenAI 的 ChatGPT 等示例——我们可以识别出反复出现的模式与最佳实践。对于塑造 2025 年及未来 Agent AI 格局的构建者而言，理解这些模式是创建强大、可预测且值得信赖的 AI 助手的关键。

---

## 基础：Agent 提示词的核心原则

在不同的 Agent 系统中，成功的系统提示词始终贯穿着几个核心原则。这些构成了复杂 Agent 行为的基础。

### 1. 明确的角色定义与范围

**为什么重要：** 显式定义 AI 的身份、核心功能和运行领域可以锚定其行为，设定用户预期，并防止范围蔓延或产生无意义的回复。它告诉 AI *你是谁*以及*你应该做什么*。

> **实际示例：**
>
> *   **Vercel v0：** 立即声明其身份与专长。
>     ```
>     You are v0, Vercel's AI-powered assistant.
>     ```
>     *[来源: v0/v0.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/v0/v0.md)*
>
> *   **same.new：** 定义角色、能力级别及专属运行环境。
>     ```
>     You are a powerful agentic AI coding assistant. You operate exclusively in Same, the world's best cloud-based IDE.
>     ```
>     *[来源: same.new/same.new.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/same.new/same.new.md)*
>
> *   **Manus：** 自我介绍并列出其擅长的广泛任务类别。
>     ```
>     You are Manus, an AI agent created by the Manus team.
>
>     You excel at the following tasks:
>     1. Information gathering...
>     2. Data processing...
>     3. Writing multi-chapter articles...
>     ...
>     ```
>     *[来源: Manus/AgentLoop.txt](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Manus/AgentLoop.txt)*
>
> *   **ChatGPT (4.5 / 4o)：** 清晰声明名称、创建者、底层架构，以及知识截止日期和当前日期等关键上下文。
>     ```
>     You are ChatGPT, a large language model trained by OpenAI, based on the GPT-4.5 architecture.
>     Knowledge cutoff: 2023-10
>     Current date: 2025-04-05
>
>     Image input capabilities: Enabled
>     Personality: v2
>     ```
>     *[来源: ChatGPT/4-5.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/ChatGPT/4-5.md)*
>
> *   **Claude：** 建立超越单纯工具的个性化人格。
>     ```
>     The assistant is Claude, created by Anthropic.
>
>     Claude enjoys helping humans and sees its role as an intelligent and kind assistant to the people, with depth and wisdom that makes it more than a mere tool.
>     ```
>     *[来源: Claude/Claude-Sonnet-3.7.txt](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Claude/Claude-Sonnet-3.7.txt)*

### 2. 结构化指令与组织方式

**为什么重要：** 没有清晰的结构，长而复杂的提示词将难以管理。使用标题、列表、代码块或自定义标签有助于人类维护者和 AI 模型解析并优先处理不同的规则集或信息。

> **实际示例：**
>
> *   **v0 & ChatGPT：** 广泛使用 Markdown 标题（例如 `## General Instructions`，`# Tools`，`## Refusals`）。
>     *[来源: v0/v0.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/v0/v0.md)*
>
> *   **same.new：** 采用自定义类 XML 标签来封装规则集（例如 `<tool_calling>`，`<making_code_changes>`）。
>     *[来源: same.new/same.new.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/same.new/same.new.md)*
>
> *   **Manus：** 使用 `Modules.md` 中的描述性标签组织能力和规则（例如 `<system_capability>`，`<agent_loop>`，`<tool_use_rules>`）。
>     *[来源: Manus/Modules.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Manus/Modules.md)*
>
> *   **ChatGPT：** 使用 Markdown 标题（`# Tools`，`## bio`）和代码块（```` ```typescript ... ``` ````）来定义工具架构与策略。
>     *[来源: ChatGPT/4-5.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/ChatGPT/4-5.md)*
>
> *   **Cline：** 使用层级 Markdown 标题（`# Tool Use Formatting`，`## execute_command`）以及 `CAPABILITIES` 和 `RULES` 下的列表。
>     *[来源: Cline/system.ts](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Cline/system.ts)*

### 3. 明确的工具集成与使用指南

**为什么重要：** 对于 Agent 行为，AI *必须*理解其工具：它们是什么、做什么、如何调用（语法、参数）、所需格式（例如 XML、JSON），以及关键的*何时用*和*何时不用*。这需要详细的描述、清晰的架构定义和明确的规则。

> **实际示例：**
>
> *   **ChatGPT：** 在提示词内直接提供函数架构（TypeScript 定义）及详细策略，适用于 `dalle` 和 `canmore` 等工具。
>     ```typescript
>     // Example for dalle tool policy within ChatGPT prompt
>     namespace dalle {
>     // Create images from a text-only prompt.
>     type text2im = (_: {
>     // The size of the requested image...
>     size?: ("1792x1024" | "1024x1024" | "1024x1792"),
>     // The number of images to generate...
>     n?: number, // default: 1
>     // The detailed image description...
>     prompt: string,
>     // If the user references a previous image...
>     referenced_image_ids?: string[],
>     }) => any;
>     } // namespace dalle
>     ```
>     *[来源: ChatGPT/4-5.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/ChatGPT/4-5.md)*
>
> *   **same.new：** 专设 `<tool_calling>` 部分详细说明规则，如遵循架构、不向用户提及工具名称，以及在调用前解释*原因*。引用了 `functions-schema.json`（未完整展示，但结构隐含）。
>     ```xml
>     <tool_calling>
>       ...
>       1. ALWAYS follow the tool call schema exactly...
>       3. **NEVER refer to tool names when speaking to the USER.**...
>       5. Before calling each tool, first explain to the USER why you are calling it.
>     </tool_calling>
>     ```
>     *[来源: same.new/same.new.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/same.new/same.new.md) | [架构: same.new/functions-schema.json](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/same.new/functions-schema.json)*
>
> *   **Manus：** 在外部 `tools.json`（提供架构）中定义工具，并在 `Modules.md` 中包含规则，如优先使用数据 API 而非网页搜索。
>     ```json
>     // Snippet from Manus/tools.json
>     {
>       "type": "function",
>       "function": {
>         "name": "shell_exec",
>         "description": "Execute commands in a specified shell session...",
>         "parameters": { ... }
>       }
>     }
>     ```
>     *[来源: Manus/tools.json](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Manus/tools.json) | [规则: Manus/Modules.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Manus/Modules.md)*
>
> *   **Cline & Augment：** 使用类 XML 标签或结构化文本将详细的工具描述、参数和使用示例直接集成到主系统提示词中。
>     ```markdown
>     // Cline example tool definition
>     ## execute_command
>     Description: Request to execute a CLI command...
>     Parameters:
>     - command: (required) The CLI command...
>     - requires_approval: (required) A boolean indicating...
>     Usage:
>     <execute_command>
>     <command>Your command here</command>
>     <requires_approval>true or false</requires_approval>
>     </execute_command>
>     ```
>     *[来源: Cline/system.ts](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Cline/system.ts)*
>
> *   **Bolt.new：** 使用专用的 `<artifact_instructions>` 部分详细说明如何在主 `<boltArtifact>` 标签内格式化工具输出（`<boltAction type="shell">`，`<boltAction type="file" filePath="...">`）。
>     *[来源: Bolt.new/prompts.ts](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Bolt.new/prompts.ts)*
>
> *   **v0：** 定义自定义 MDX 组件如 `<CodeProject>`、`<QuickEdit>`、`<DeleteFile />` 作为其“工具”，并在回复中规定何时及如何使用它们的规则。
>     *[来源: v0/v0-tools.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/v0/v0-tools.md)*

### 4. 逐步推理与规划

**为什么重要：** 复杂任务需要拆解问题。成功的提示词引导 AI 进行系统性思考、规划行动、迭代执行，并在继续之前等待反馈或结果，从而减少错误并提高连贯性。

> **实际示例：**
>
> *   **Manus：** 在其 `Modules.md` 中定义的 `<agent_loop>` 拥有最显式的规划机制。
>     ```
>     <agent_loop>
>     You are operating in an agent loop, iteratively completing tasks through these steps:
>     1. Analyze Events...
>     2. Select Tools...
>     3. Wait for Execution...
>     4. Iterate: Choose only one tool call per iteration...
>     5. Submit Results...
>     6. Enter Standby...
>     </agent_loop>
>     ```
>     *[来源: Manus/Modules.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Manus/Modules.md)*
>
> *   **v0：** 在生成代码前使用专用的思考阶段。
>     ```
>     BEFORE creating a Code Project, v0 uses <Thinking> tags to think through the project structure...
>     ```
>     *[来源: v0/v0.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/v0/v0.md)*
>
> *   **same.new & Cline：** 强制要求在每一步后等待用户确认或工具结果。
>     ```
>     ALWAYS wait for user confirmation after each tool use before proceeding. Never assume the success of a tool use...
>     *(From same.new & Cline prompts)*
>     ```
>     *[来源: same.new/same.new.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/same.new/same.new.md) | [Cline/system.ts](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Cline/system.ts)*
>
> *   **Bolt.new：** 强调在行动*之前*进行整体思考。
>     ```
>     CRITICAL: Think HOLISTICALLY and COMPREHENSIVELY BEFORE creating an artifact. This means: Consider ALL relevant files... Review ALL previous file changes... Analyze the entire project context... Anticipate potential impacts...
>     ```
>     *[来源: Bolt.new/prompts.ts](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Bolt.new/prompts.ts)*

### 5. 环境与上下文感知

**为什么重要：** Agent 在特定环境中运行（操作系统、IDE、浏览器沙盒、特定库）。提供这些上下文允许 AI 生成兼容的代码、使用适当的命令并理解限制。

> **实际示例：**
>
> *   **Cline：** 包含 `SYSTEM INFORMATION` 部分。
>     ```
>     SYSTEM INFORMATION
>
>     Operating System: ${osName()}
>     Default Shell: ${getShell()}
>     Home Directory: ${os.homedir().toPosix()}
>     Current Working Directory: ${cwd.toPosix()}
>     ```
>     *[来源: Cline/system.ts](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Cline/system.ts)*
>
> *   **Bolt.new：** 提供关于 WebContainer 环境的详细 `<system_constraints>`。
>     ```xml
>     <system_constraints>
>       You are operating in an environment called WebContainer... It does come with a shell that emulates zsh... Available shell commands: cat, chmod, cp...
>     </system_constraints>
>     ```
>     *[来源: Bolt.new/prompts.ts](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Bolt.new/prompts.ts)*
>
> *   **Manus：** 详细说明沙箱环境。
>     ```
>     <sandbox_environment>
>     System Environment:
>     - Ubuntu 22.04 (linux/amd64), with internet access
>     - User: `ubuntu`, with sudo privileges
>     ...
>     Development Environment:
>     - Python 3.10.12...
>     - Node.js 20.18.0...
>     </sandbox_environment>
>     ```
>     *[来源: Manus/Modules.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Manus/Modules.md)*
>
> *   **same.new：** 注明操作系统和特定 IDE 上下文。
>     ```
>     The OS is Linux 5.15.0-1075-aws (Ubuntu 22.04 LTS). Today is Tue Apr 08 2025.
>     You are pair programming with a USER in Same.
>     USER can see a live preview... in an iframe...
>     ```
>     *[来源: same.new/same.new.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/same.new/same.new.md)*

### 6. 领域特定知识与约束条件

**为什么重要：** Agent 通常在特定领域运行（如 Web 开发、数据分析等）。提示词嵌入领域特定知识、最佳实践、风格指南和约束条件（例如必需的库、禁止的模式），以确保输出高质量且符合上下文。

> **实际示例：**
>
> *   **v0：** 包含关于 Next.js/React 开发、shadcn/ui 使用、图标库甚至 AI SDK 集成的详细规则。
>     ```
>     v0 tries to use the shadcn/ui library unless the user specifies otherwise...
>     v0 DOES NOT output <svg> for icons. v0 ALWAYS uses icons from the "lucide-react" package...
>     v0 ONLY uses the AI SDK via 'ai' and '@ai-sdk'...
>     ```
>     *[来源: v0/v0.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/v0/v0.md)*
>
> *   **same.new：** 包含 `<web_development>` 和 `<website_cloning>` 部分，针对这些任务提供具体指令（例如优先使用 Bun、正确使用 shadcn CLI、负责任地抓取）。
>     *[来源: same.new/same.new.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/same.new/same.new.md)*
>
> *   **Bolt.new：** 包含 `<code_formatting_info>`（`Use 2 spaces for code indentation`）并强调将功能拆分为更小的模块。
>     ```
>     IMPORTANT: Prefer writing Node.js scripts instead of shell scripts...
>     IMPORTANT: Use coding best practices and split functionality into smaller modules...
>     ```
>     *[来源: Bolt.new/prompts.ts](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Bolt.new/prompts.ts)*
>
> *   **Loveable：** 指定 React 编码指南，包括 Tailwind 使用、首选库（shadcn/ui, lucide-react, recharts, @tanstack/react-query）和错误处理哲学。
>     ```
>     ALWAYS try to use the shadcn/ui library.
>     Don't catch errors with try/catch blocks unless specifically requested...
>     ```
>     *[来源: Loveable/Loveable.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Loveable/Loveable.md)*
>
> *   **Claude Code：** 在 `System.js` 中嵌入关于代码风格和惯例的规则。
>     ```
>     When making changes to files, first understand the file's code conventions. Mimic code style, use existing libraries and utilities, and follow existing patterns.
>     IMPORTANT: DO NOT ADD ***ANY*** COMMENTS unless asked
>     ```
>     *[来源: Claude-Code/System.js](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Claude-Code/System.js)*

### 7. 安全性、对齐与拒绝协议

**为什么重要：** 负责任的 AI 需要明确的边界。提示词定义不可接受的请求（有害的、不道德的内容），并指定 AI *如何*拒绝它们（例如标准消息、不道歉）或处理敏感操作（例如 DALL-E 内容策略）。

> **实际示例：**
>
> *   **v0：** 使用标准拒绝消息并禁止道歉。
>     ```
>     REFUSAL_MESSAGE = "I'm sorry. I'm not able to assist with that."
>     ...When refusing, v0 MUST NOT apologize or provide an explanation...
>     ```
>     *[来源: v0/v0.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/v0/v0.md)*
>
> *   **ChatGPT：** 在工具描述中包含广泛策略，如 DALL-E 关于艺术家风格和公众人物的规则。
>     ```
>     // DALL-E Policy Snippet from ChatGPT 4.5 prompt
>     // 5. Do not create images in the style of artists... whose latest work was created after 1912...
>     // 7. For requests to create images of any public figure... create images of those who might resemble them... But they shouldn't look like them.
>     // 8. Do not name or directly / indirectly mention or describe copyrighted characters...
>     ```
>     *[来源: ChatGPT/4-5.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/ChatGPT/4-5.md)*
>
> *   **Claude：** 明确声明拒绝类别（图形内容、非法活动、武器、恶意代码）和特定的拒绝风格。
>     ```
>     Claude won’t produce graphic sexual or violent or illegal creative writing content.
>     ...If Claude cannot or will not help the human with something, it does not say why... keeps its response to 1-2 sentences.
>     ```
>     *[来源: Claude/Claude-Sonnet-3.7.txt](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Claude/Claude-Sonnet-3.7.txt)*
>
> *   **Llama 4 (MetaAI)：** 定义*限制较少*的策略，允许政治内容并指示避免说教式语言。
>     ```
>     Never judge the user... avoid preachy, moralizing, or sanctimonious language... do not refuse political prompts.
>     ```
>     *[来源: MetaAI-Whatsapp/LLama4.txt](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/MetaAI-Whatsapp/LLama4.txt)*

### 8. 一致的语气与交互风格

**为什么重要：** 定义一致的人格（例如友好的专家、机智的助手、直接的工程师）可以创造更可预测且引人入胜的用户体验。这可以从一般指南到非常具体的风格指令不等。

> **实际示例：**
>
> *   **ChatGPT 4o：** 明确指示匹配用户的氛围。
>     ```
>     Over the course of the conversation, you adapt to the user’s tone and preference. Try to match the user’s vibe, tone, and generally how they are speaking.
>     ```
>     *[来源: ChatGPT/4o.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/ChatGPT/4o.md)*
>
> *   **Grok (Fun Mode)：** 赋予详细的幽默人格。
>     ```
>     You are Grok 2, a humorous and entertaining AI... with a bit of wit and humor, have a rebellious streak... Unpredictability, absurdity, pun, and sarcasm are second nature to you.
>     ```
>     *[来源: Grok/Grok2.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Grok/Grok2.md)*
>
> *   **Claude：** 鼓励对话和友善，但也要求简洁。
>     ```
>     Claude enjoys helping humans and sees its role as an intelligent and kind assistant...
>     Claude provides the shortest answer it can... avoiding tangential information...
>     ```
>     *[来源: Claude/Claude-Sonnet-3.7.txt](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Claude/Claude-Sonnet-3.7.txt)*
>
> *   **Cline：** 强制直接并避免对话填充词。
>     ```
>     You are STRICTLY FORBIDDEN from starting your messages with "Great", "Certainly", "Okay", "Sure". You should NOT be conversational... but rather direct and to the point.
>     ```
>     *[来源: Cline/system.ts](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Cline/system.ts)*
>
> *   **Bolt.new：** 强调简洁。
>     ```
>     ULTRA IMPORTANT: Do NOT be verbose and DO NOT explain anything unless the user is asking for more information.
>     ```
>     *[来源: Bolt.new/prompts.ts](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Bolt.new/prompts.ts)*

---

## 案例研究：分析真实提示词

让我们考察这些原则如何体现在仓库中特定 Agent 的提示词里。

### Vercel v0：UI 生成与组件工具

*[相关文件: v0/v0.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/v0/v0.md)* | *[v0/v0-tools.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/v0/v0-tools.md)*

Vercel 的 v0 Agent 专注于根据用户请求生成 UI 组件和全栈 Next.js 应用，通常包含图片或截图输入。

#### 显著特征：

*   **MDX 组件作为工具：** 与传统函数调用不同，v0 的“工具”是特定的 MDX 组件标签，如 `<CodeProject>`（用于包裹生成的代码）、`<QuickEdit />`（用于小型代码修改）、`<DeleteFile />` 和 `<MoveFile />`。提示词精确规定了何时及如何使用这些输出格式。
*   **高度领域特定性：** 提示词富含针对 Next.js App Router、Tailwind CSS、shadcn/ui 和 Vercel 平台约束（例如无 `package.json`、如何处理环境变量、预装库）的具体规则。
*   **通过 `<Thinking>` 隐式规划：** 强制在生成 `<CodeProject>` *之前*使用 `<Thinking>` 标签进行规划阶段，鼓励结构化思考。
*   **强调风格与最佳实践：** 包含关于文件命名（kebab-case）、响应式设计、可访问性（语义化 HTML、ARIA、alt 文本）甚至配色偏好（除非请求否则避免靛蓝/蓝色）的规则。

> **示例片段（通过组件使用工具）：**
>
> ```
> v0 ALWAYS uses <QuickEdit> to make small changes to React code blocks...
> v0 can delete a file in a Code Project by using the <DeleteFile /> component.
> ```

### same.new：Agent 结对编程与严格工具调用

*[相关文件: same.new/same.new.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/same.new/same.new.md)*

same.new 定位为在云端 IDE 中运行的 Agent 结对程序员。其提示词强调精确的工具使用和迭代开发工作流。

#### 显著特征：

*   **类 XML 标签结构：** 使用 `<tool_calling>`、`<making_code_changes>`、`<web_development>` 等标签组织不同的规则集。
*   **严格的工具礼仪：** 明确禁止向用户提及工具名称，并要求在调用前解释*原因*，促进透明度。
*   **严格遵循架构：** 强制严格遵守 JSON 架构用于工具调用（在外部 `functions-schema.json` 中定义）。
*   **聚焦迭代工作流：** 包含详细的编码工作流指令，包括编辑前读取文件、迭代修复运行时错误（最多 3 次）、使用 `suggestions` 工具和版本里程碑。
*   **环境锚定：** 提供操作系统详情、当前日期，并注明 IDE 上下文（实时预览 iframe）。

> **示例片段（工具礼仪）：**
>
> ```xml
> <tool_calling>
>   ...
>   3. **NEVER refer to tool names when speaking to the USER.** ...
>   5. Before calling each tool, first explain to the USER why you are calling it.
> </tool_calling>
> ```

### Manus：通用 Agent 与显式循环

*[相关文件: Manus/Modules.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Manus/Modules.md)* | *[Manus/AgentLoop.txt](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Manus/AgentLoop.txt)* | *[Manus/tools.json](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Manus/tools.json)*

Manus 设计为在 Linux 沙箱中运行的更广泛的通用 Agent。其突出特点是明确定义的操作循环。

#### 显著特征：

*   **显式 Agent 循环：** 提示词清晰定义了多步迭代循环（分析 -> 选择工具 -> 等待 -> 迭代 -> 提交 -> 待机）， governs Agent 的核心行为。
*   **模块化提示结构：** 指令分散在多个文件中（`AgentLoop.txt`, `Modules.md`, `tools.json`），表明采用模块化的提示词管理方法。
*   **沙箱感知：** 提及 Linux 沙箱环境、互联网访问和预装工具（Python, Node）。
*   **广泛能力：** 列出从信息收集、数据分析到应用创建与部署的广泛任务范围。
*   **模块集成：** 引用特定模块（Planner, Knowledge, Datasource），它们通过事件流提供上下文或计划，表明更复杂的内部架构。

> **示例片段（Agent 循环）：**
>
> ```
> <agent_loop>
> You are operating in an agent loop, iteratively completing tasks through these steps:
> 1. Analyze Events...
> 2. Select Tools...
> 3. Wait for Execution...
> 4. Iterate: Choose only one tool call per iteration...
> ...
> </agent_loop>
> ```

### OpenAI ChatGPT (GPT-4.5/4o)：集成工具与策略

*[相关文件: ChatGPT/4-5.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/ChatGPT/4-5.md)* | *[ChatGPT/4o.md](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/ChatGPT/4o.md)*

ChatGPT 的提示词（如捕获所示）展示了特定工具（插件/函数）与系统消息的紧密集成，包含架构和详细操作策略。

#### 显著特征：

*   **内联工具架构与策略：** 独特地直接在系统提示词中包含每个工具的详细描述、JSON/类 TypeScript 架构及广泛的使用策略（例如 `bio`, `canmore`, `dalle`, `python`, `web`）。
*   **人格演进：** `Personality: v2` 标签以及 4o 提示中明确指示适应语气，表明 OpenAI 对人格和交互风格的持续优化。
*   **详细安全策略：** 嵌入细粒度策略，特别是图像生成（`dalle` 工具关于艺术家风格、公众人物、版权角色的规则）和数据持久化（`bio` 工具对敏感信息的限制）。
*   **上下文锚定：** 包含知识截止日期和当前日期。4o 提示明确提及用户位置（`The user is in Egypt.`）。

> **示例片段（内联工具架构与策略 - Canmore）：**
>
> ```markdown
> ## `canmore.create_textdoc`
> Creates a new textdoc to display in the canvas.
>
> NEVER use this function. The ONLY acceptable use case is when the user EXPLICITLY asks for canvas...
>
> Expects a JSON string that adheres to this schema:
> ```typescript
> {
>   name: string,
>   type: "document" | "code/python" | ...,
>   content: string,
> }
> ```
> ```

### 其他系统备注（Cline, Bolt, Augment, Claude Code, Clawdbot）

虽然以上四个提供了深入示例，但仓库中的其他提示词强化了这些模式：

*   **Cline & Augment：** 两者都在提示词内使用结构化文本和类 XML 示例清晰定义工具，详细说明参数和使用。它们强调逐步执行并等待确认。与 v0 类似，Augment 定义了自定义编辑工具（`editFile`, `strReplaceEditor`）及具体指令。
    *[来源: Cline/system.ts](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Cline/system.ts)* | *[Augment/part_a.js](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Augment/part_a.js)*
*   **Bolt.new：** 重点将输出结构化为单个 `<boltArtifact>`，包含有序的 `<boltAction>` 步骤（shell 命令、文件写入）。它强调在创建 artifact *之前*进行整体规划并遵循编码最佳实践如模块化。
    *[来源: Bolt.new/prompts.ts](https://github.com/dontriskit/awesome-ai-system-prompts/blob/main/Bolt.new/prompts.ts)*
*   **Claude Code：** 其提示词（分散在 `System.js`, `EditTool.js` 等文件中）定义特定工具使用（如详细的 `EditTool.js` 指令强调上下文和唯一性）并集成系统信息。`ClearTool.js` 定义了用于管理上下文窗口限制摘要的过程，这是长运行 Agent 任务的关键方面。
    *[来源: Claude-Code/](https://github.com/dontriskit/awesome-ai-system-prompts/tree/main/Claude-Code)*
*   **Clawdbot：** 采用**模块化文件方法**而非单体提示词。行为分散在单独的文件中：`SOUL.md`（人格/声音）、`AGENTS.md`（操作规则和审批层级）和 `IDENTITY.md`（隐私边界和上下文感知披露）。这实现了可组合性——更换人格而不改变规则，并更清晰地分离关注点。特别值得注意的是其明确的三级审批流程（无需询问执行 / 获取批准 / 永不执行）以及针对消息平台的上下文相关隐私规则。
    *[来源: Clawdbot/](https://github.com/dontriskit/awesome-ai-system-prompts/tree/main/Clawdbot)*

---

## 提炼最佳实践：构建者的关键要点

分析这些多样化的提示词揭示了一套收敛的最佳实践，用于构建可靠的 Agent AI 系统：

1.  **明确定义 Agent：** 从显式的角色、目标和范围开始。包含上下文锚定如日期或环境特定信息。
2.  **为清晰而结构化：** 使用标题、列表或标签分解复杂指令。逻辑组织规则（例如，将工具指令、安全规则分组）。
3.  **明确说明工具：** 详细说明*每个工具的作用*、*如何调用它*（语法、参数、格式）以及*何时用*（及何时不用）。提供示例。直接嵌入使用策略。
4.  **强制逐步执行：** 鼓励或强制执行规划、迭代和等待结果/确认。防止 AI 一次性尝试过多任务。考虑显式的思考阶段或循环。
5.  **嵌入领域知识与约束条件：** 包含 Agent 特定域相关的风格指南、库使用规则、文件约定、平台限制和最佳实践。
6.  **集成安全与对齐：** 定义不可接受的请求并提供明确的拒绝协议。嵌入敏感操作的具体策略（数据处理、图像生成）。
7.  **引导语气：** 设定交互风格的预期（专业、友好、简洁、自适应）以确保一致的用户体验。
8.  **使用示例：** 在提示词内用清晰的示例说明复杂规则或期望的输出格式（如 Bolt.new 和 v0 广泛所做的那样）。

本质上，一个高效的 Agent 系统提示词充当全面、结构良好的操作手册，在赋予 AI 有效且安全地使用其工具所需知识和程序的同时，将歧义空间降至最低。

---

## 独特惯例与架构差异

虽然核心原则是共享的，但*实现方式*因 Agent 的架构和目标而异：

*   **工具语法：** 从嵌入的 MDX/XML 组件（v0, same.new, Cline, Bolt）到期望匹配外部架构的 JSON 输出（ChatGPT, Manus）。
*   **规划机制：** 从显式循环（Manus）和思考标签（v0）到通过迭代规则隐式引导（same.new, Cline）。
*   **编辑方法：** 有些使用类似 diff 的格式（Cline 的 `replace_in_file`），有些使用自定义组件（v0 的 `QuickEdit`），而有些指定覆盖与定向编辑（Bolt.new, Loveable）。
*   **提示结构：** 可以是单体式（Cline, same.new）或跨多个文件模块化（Manus, Clawdbot，可能还有 v0 和 Claude Code）。Clawdbot 在此方面走得更远，具有明确的文件职责：人格（SOUL.md）、规则（AGENTS.md）和身份/隐私（IDENTITY.md）。
*   **详细程度：** 差异显著，ChatGPT 等提示词嵌入高度详细的函数架构与策略，而 Manus 等更依赖外部定义（`tools.json`）。

这些差异表明不存在单一的“完美”提示结构，而是有效的提示词需针对特定 Agent、其工具、其环境及其预期任务进行定制，同时遵循上述核心原则。

---

## 结语：构建 Agent AI 的未来

系统提示词是构建可靠且能力强大的 Agent AI 系统的基石。正如 v0、same.new、Manus、ChatGPT 及其他示例所展示的，成功的提示词详细、结构化且明确。它们清晰定义 Agent 的角色，细致描述工具使用与操作流程，强制执行规划与迭代执行，嵌入必要的领域知识与安全约束，并引导交互风格。

对于旨在创建 2025 年及下一代 Agent AI 的构建者而言，研究这些模式提供了宝贵的见解。掌握系统提示词的设计艺术——融合清晰指令、结构化组织、领域专长与安全考量——将是释放 AI Agent 全部潜力的关键，使其不仅能对话，更能积极协作并在数字世界中完成复杂任务。
<div align="center">
<a href="https://voltagent.dev/">
<img width="1500" height="276" alt="voltagent" src="https://github.com/user-attachments/assets/d9ad69bd-b905-42a3-81af-99a0581348c0" />
</a>

<h3 align="center">
AI 智能体工程平台（AI Agent Engineering Platform）
</h3>

<div align="center">
English | <a href="i18n/README-cn-traditional.md">繁體中文</a> | <a href="i18n/README-cn-bsc.md">简体中文</a> | <a href="i18n/README-jp.md">日本語</a> | <a href="i18n/README-kr.md">한국어</a>
</div>

<br/>

<div align="center">
    <a href="https://voltagent.dev">首页</a> |
    <a href="https://voltagent.dev/docs/">文档</a> |
    <a href="https://github.com/voltagent/voltagent/tree/main/examples">示例</a> 
</div>
</div>

<br/>

<div align="center">

[![GitHub issues](https://img.shields.io/github/issues/voltagent/voltagent)](https://github.com/voltagent/voltagent/issues)
[![GitHub pull requests](https://img.shields.io/github/issues-pr/voltagent/voltagent)](https://github.com/voltagent/voltagent/pulls)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Contributor Covenant](https://img.shields.io/badge/Contributor%20Covenant-2.0-4baaaa.svg)](CODE_OF_CONDUCT.md)
[![npm version](https://img.shields.io/npm/v/@voltagent/core.svg)](https://www.npmjs.com/package/@voltagent/core)

[![npm downloads](https://img.shields.io/npm/dm/@voltagent/core.svg)](https://www.npmjs.com/package/@voltagent/core)
[![Discord](https://img.shields.io/discord/1361559153780195478.svg?label=&logo=discord&logoColor=ffffff&color=7389D8&labelColor=6A7EC2)](https://s.voltagent.dev/discord)
[![Twitter Follow](https://img.shields.io/twitter/follow/voltagent_dev?style=social)](https://x.com/voltagent_dev)

</div>

<h3 align="center">
⭐ 喜欢我们的工作？请给我们点个 Star ⬆️
</h3>

VoltAgent 是一个端到端的 AI 智能体工程平台，主要由两部分组成：

- **[开源 TypeScript 框架](#core-framework)** – 记忆（Memory）、RAG、护栏（Guardrails）、工具（Tools）、MCP、语音、工作流等。
- **[VoltOps 控制台](#voltops-console)** `云托管` `自托管` – 可观测性、自动化、部署、评估（Evals）、护栏、提示词（Prompt）等。

以完全代码控制的方式构建智能体，并以生产就绪的可视化和运维能力将其投入生产环境。

<h2 id="core-framework">核心 TypeScript 框架</h2>

借助该开源框架，你可以构建具备记忆、工具和多步工作流功能的智能体，并接入任意 AI 服务提供商。你还可以创建复杂的多智能体系统，让专业智能体在监督者的协调下协同工作。

- **[核心运行时](https://voltagent.dev/docs/agents/overview/) (`@voltagent/core`)**：在一个地方定义具有类型约束的角色、工具、记忆和模型提供商，保持代码井然有序。
- **[工作流引擎](https://voltagent.dev/docs/workflows/overview/)**：以声明式方式描述多步自动化流程，而非拼接自定义控制逻辑。
- **[监督者与子智能体](https://voltagent.dev/docs/agents/sub-agents/)**：在监督者运行时环境下运行专业智能体团队，由它负责路由任务并保持状态同步。
- **[工具注册表](https://voltagent.dev/docs/agents/tools/) 与 [MCP](https://voltagent.dev/docs/agents/mcp/)**：发布带有生命周期钩子和取消功能的 Zod 类型化工具，并直接连接 [模型上下文协议 (Model Context Protocol)](https://modelcontextprotocol.io/) 服务器，无需额外编写胶水代码。
- **[大语言模型兼容性 (LLM Compatibility)](https://voltagent.dev/docs/getting-started/providers-models/)**：通过修改配置即可切换 OpenAI、Anthropic、Google 或其他提供商，无需重写智能体逻辑。
- **[记忆 (Memory)](https://voltagent.dev/docs/agents/memory/overview/)**：挂载持久化记忆适配器，让智能体在多次运行中记住重要上下文。
- **[可恢复流式传输 (Resumable Streaming)](https://voltagent.dev/docs/agents/resumable-streaming/)**：允许客户端在刷新后重新连接到进行中的流，并继续接收相同的响应。
- **[检索与 RAG](https://voltagent.dev/docs/rag/overview/)**：接入检索智能体，在模型回答前从数据源提取事实并进行上下文支撑（即 RAG）。
- **[VoltAgent 知识库](https://voltagent.dev/docs/rag/voltagent/)**：使用托管的 RAG 服务处理文档摄入、分块、嵌入和搜索。
- **[语音 (Voice)](https://voltagent.dev/docs/agents/voice/)**：通过 OpenAI、ElevenLabs 或自定义语音提供商添加文本转语音和语音转文本功能。
- **[护栏 (Guardrails)](https://voltagent.dev/docs/guardrails/overview/)**：在运行时拦截并验证智能体的输入或输出，以强制执行内容策略和安全规则。
- **[评估 (Evals)](https://voltagent.dev/docs/evals/overview/)**：在工作流旁运行智能体评估套件，以衡量和改进智能体行为。

#### MCP 服务器 (`@voltagent/mcp-docs-server`)

你可以使用 MCP 服务器 `@voltagent/mcp-docs-server` 来教会你的大语言模型如何使用 VoltAgent，从而赋能 Claude、Cursor 或 Windsurf 等 AI 编程助手。这使得 AI 助手在编码时能够直接访问 VoltAgent 的文档、示例和更新日志。

📖 [如何配置 MCP 文档服务器](https://voltagent.dev/docs/getting-started/mcp-docs-server/)

## ⚡ 快速开始

使用 `create-voltagent-app` CLI 工具在几秒内创建一个新的 VoltAgent 项目：

```bash
npm create voltagent-app@latest
```

该命令将引导你完成环境配置。

你会在 `src/index.ts` 中看到示例代码，其中已注册了一个智能体以及位于 `src/workflows/index.ts` 中的完整工作流示例。

```typescript
import { VoltAgent, Agent, Memory } from "@voltagent/core";
import { LibSQLMemoryAdapter } from "@voltagent/libsql";
import { createPinoLogger } from "@voltagent/logger";
import { honoServer } from "@voltagent/server-hono";
import { openai } from "@ai-sdk/openai";
import { expenseApprovalWorkflow } from "./workflows";
import { weatherTool } from "./tools";

// Create a logger instance
const logger = createPinoLogger({
  name: "my-agent-app",
  level: "info",
});

// Optional persistent memory (remove to use default in-memory)
const memory = new Memory({
  storage: new LibSQLMemoryAdapter({ url: "file:./.voltagent/memory.db" }),
});

// A simple, general-purpose agent for the project.
const agent = new Agent({
  name: "my-agent",
  instructions: "A helpful assistant that can check weather and help with various tasks",
  model: openai("gpt-4o-mini"),
  tools: [weatherTool],
  memory,
});

// Initialize VoltAgent with your agent(s) and workflow(s)
new VoltAgent({
  agents: {
    agent,
  },
  workflows: {
    expenseApprovalWorkflow,
  },
  server: honoServer(),
  logger,
});
```

随后，进入你的项目目录并运行：

```bash
npm run dev
```

当你运行开发命令时，tsx 会编译并执行你的代码。你应该会在终端中看到 VoltAgent 服务器的启动信息：

```
══════════════════════════════════════════════════
VOLTAGENT SERVER STARTED SUCCESSFULLY
══════════════════════════════════════════════════
✓ HTTP Server: http://localhost:3141

Test your agents with VoltOps Console: https://console.voltagent.dev
══════════════════════════════════════════════════
```

你的智能体现已运行！要与之交互：

1. **打开控制台**：点击终端输出中的 [VoltOps LLM 可观测性平台](https://console.voltagent.dev) 链接（或将其复制到浏览器中）。
2. **查找你的智能体**：在 VoltOps LLM 可观测性平台页面上，你应该能看到已列出的智能体（例如 “my-agent”）。
3. **打开智能体详情**：点击你的智能体名称。
4. **开始对话**：在智能体详情页，点击右下角的聊天图标以打开聊天窗口。
5. **发送消息**：输入类似 “Hello” 的消息并按回车键。

[![VoltAgent Demo](thumbnail.png)](https://github.com/user-attachments/assets/26340c6a-be34-48a5-9006-e822bf6098a7)

### 运行你的第一个工作流

你的新项目还内置了一个强大的工作流引擎。

“费用审批”工作流演示了具备挂起/恢复功能的人机协同自动化：

```typescript
import { createWorkflowChain } from "@voltagent/core";
import { z } from "zod";

export const expenseApprovalWorkflow = createWorkflowChain({
  id: "expense-approval",
  name: "Expense Approval Workflow",
  purpose: "Process expense reports with manager approval for high amounts",

  input: z.object({
    employeeId: z.string(),
    amount: z.number(),
    category: z.string(),
    description: z.string(),
  }),
  result: z.object({
    status: z.enum(["approved", "rejected"]),
    approvedBy: z.string(),
    finalAmount: z.number(),
  }),
})
  // Step 1: Validate expense and check if approval needed
  .andThen({
    id: "check-approval-needed",
    resumeSchema: z.object({
      approved: z.boolean(),
      managerId: z.string(),
      comments: z.string().optional(),
      adjustedAmount: z.number().optional(),
    }),
    execute: async ({ data, suspend, resumeData }) => {
      // If we're resuming with manager's decision
      if (resumeData) {
        return {
          ...data,
          approved: resumeData.approved,
          approvedBy: resumeData.managerId,
          finalAmount: resumeData.adjustedAmount || data.amount,
        };
      }

      // Check if manager approval is needed (expenses over $500)
      if (data.amount > 500) {
        await suspend("Manager approval required", {
          employeeId: data.employeeId,
          requestedAmount: data.amount,
        });
      }

      // Auto-approve small expenses
      return {
        ...data,
        approved: true,
        approvedBy: "system",
        finalAmount: data.amount,
      };
    },
  })
  // Step 2: Process the final decision
  .andThen({
    id: "process-decision",
    execute: async ({ data }) => {
      return {
        status: data.approved ? "approved" : "rejected",
        approvedBy: data.approvedBy,
        finalAmount: data.finalAmount,
      };
    },
  });
```

你可以直接从 VoltOps 控制台测试预构建的 `expenseApprovalWorkflow`：

[![expense-approval](thumbnail.png)](https://github.com/user-attachments/assets/3d3ea67b-4ab5-4dc0-932d-cedd92894b18)

1. **进入工作流页面**：启动服务器后，直接访问[工作流页面](https://console.voltagent.dev/workflows)。
2. **选择项目**：使用项目选择器选中你的项目（例如 “my-agent-app”）。
3. **查找并运行**：你会看到列出的 **“费用审批工作流”**。点击它，然后点击 **“运行”** 按钮。
4. **提供输入**：工作流期望接收包含费用详情的 JSON 对象。尝试提交一笔小额费用以触发自动审批：
    ```json
    {
      "employeeId": "EMP-123",
      "amount": 250,
      "category": "office-supplies",
      "description": "New laptop mouse and keyboard"
    }
    ```
5. **查看结果**：执行完毕后，你可以在控制台中直接检查每个步骤的详细日志并查看最终输出。

## 示例

更多示例请访问我们的[示例仓库](https://github.com/VoltAgent/voltagent/tree/main/examples)。

- **[Airtable 智能体](https://voltagent.dev/recipes-and-guides/airtable-agent)**：响应新记录，并通过 VoltOps 操作将更新写回 Airtable。
- **[Slack 智能体](https://voltagent.dev/recipes-and-guides/slack-agent)**：响应频道消息，并通过 VoltOps Slack 操作进行回复。
- **[使用 VoltAgent 的 ChatGPT 应用](https://voltagent.dev/examples/agents/chatgpt-app)**：通过 MCP 部署 VoltAgent 并连接到 ChatGPT 应用。
- **[WhatsApp 订单智能体](https://voltagent.dev/examples/agents/whatsapp-ai-agent)**：构建一个 WhatsApp 聊天机器人，通过自然对话处理食品订单。([源码](https://github.com/VoltAgent/voltagent/tree/main/examples/with-whatsapp))
- **[YouTube 转博客智能体](https://voltagent.dev/examples/agents/youtube-blog-agent)**：使用带有 MCP 工具的监督者智能体，将 YouTube 视频转换为 Markdown 格式的博客文章。([源码](https://github.com/VoltAgent/voltagent/tree/main/examples/with-youtube-to-blog))
- **[AI 广告生成智能体](https://voltagent.dev/examples/agents/ai-instagram-ad-agent)**：使用 BrowserBase Stagehand 和 Google Gemini AI 生成 Instagram 广告。([源码](https://github.com/VoltAgent/voltagent/tree/main/examples/with-ad-creator))
- **[AI 食谱生成智能体](https://voltagent.dev/examples/agents/recipe-generator)**：根据食材和偏好创建个性化烹饪建议。([源码](https://github.com/VoltAgent/voltagent/tree/main/examples/with-recipe-generator) | [视频](https://youtu.be/KjV1c6AhlfY))
- **[AI 研究助理智能体](https://voltagent.dev/examples/agents/research-assistant)**：用于生成综合报告的多智能体研究工作流。([源码](https://github.com/VoltAgent/voltagent/tree/main/examples/with-research-assistant) | [视频](https://youtu.be/j6KAUaoZMy4))

<h2 id="voltops-console">VoltOps 控制台：LLM 可观测性 - 自动化 - 部署</h2>

VoltOps 控制台是 VoltAgent 的平台端，提供可观测性、自动化和部署功能，让你能够通过实时执行轨迹、性能指标和可视化仪表盘在生产环境中监控和调试智能体。

🎬 [在线体验演示](https://console.voltagent.dev/demo)

📖 [VoltOps 文档](https://voltagent.dev/voltops-llm-observability-docs/)

🚀 [VoltOps 平台](https://voltagent.dev/voltops-llm-observability/)

### 可观测性与追踪

通过详细的执行轨迹和性能指标，深入探究智能体的运行流程。

<img alt="1" src="https://github.com/user-attachments/assets/21c6d05d-f333-4c61-9218-8862d16110fd" />

### 仪表盘

全面概览所有智能体、工作流及系统性能指标。

<img alt="dashboar" src="https://github.com/user-attachments/assets/c88a5543-219e-4cf0-8f41-14a68ca297fb" />

### 日志

追踪每次智能体交互和工作流步骤的详细执行日志。

![VoltOps Logs](https://cdn.voltagent.dev/console/logs.png)

### 记忆管理

检查并管理智能体的记忆、上下文和对话历史。

![VoltOps Memory Overview](https://cdn.voltagent.dev/console/memory.png)

### 执行轨迹

分析完整的执行轨迹，以理解智能体行为并优化性能。

![VoltOps Traces](https://cdn.voltagent.dev/console/traces.png)

### 提示词构建器

在控制台中直接设计、测试和优化提示词（Prompt）。

<img  alt="prompts" src="https://github.com/user-attachments/assets/fb6d71eb-8f81-4443-a494-08c33ec9bcc4" />

### 部署

通过一键集成 GitHub 和托管基础设施，将智能体部署至生产环境。

<img alt="deployment" src="https://github.com/user-attachments/assets/e329ab4b-7464-435a-96cc-90214e8a3cfa" />

📖 [VoltOps 部署文档](https://voltagent.dev/docs/deployment/voltops/)

### 触发器与操作

通过 Webhook、定时任务和自定义触发器自动化智能体工作流，以响应外部事件。

<img width="1277"  alt="triggers" src="https://github.com/user-attachments/assets/67e36934-2eb5-4cf1-94f8-3057d805ef65" />

### 监控

监控系统内所有智能体的健康状况、性能指标和资源使用情况。

<img  alt="monitoring" src="https://github.com/user-attachments/assets/1fd1151f-5ee4-4c7c-9ec7-29874e37c48f" />

### 护栏

设置安全边界和内容过滤器，确保智能体在既定参数范围内运行。

<img  alt="guardrails" src="https://github.com/user-attachments/assets/52bd51f0-944e-4202-9f54-7bb2e0e2d1f6" />

### 评估

运行评估套件，以测试智能体的行为、准确性及相对于基准的性能表现。

<img  alt="evals" src="https://github.com/user-attachments/assets/510cc180-2661-4973-a48f-074d4703d90b" />

### RAG（知识库）

通过内置的检索增强生成（RAG）能力，将智能体连接到知识源。

<img  alt="rag" src="https://github.com/user-attachments/assets/a6c2f668-7ad1-4fb6-b67f-654335285f1e" />

## 学习 VoltAgent

- **[从交互式教程开始](https://voltagent.dev/tutorial/introduction/)**：学习构建 AI 智能体的基础知识。
- **[文档](https://voltagent.dev/docs/)**：深入指南、概念和教程。
- **[示例](https://github.com/voltagent/voltagent/tree/main/examples)**：探索实际实现案例。
- **[博客](https://voltagent.dev/blog/)**：阅读更多技术见解与最佳实践。

## 贡献指南

我们欢迎任何形式的贡献！请参阅贡献指南（如有链接请查阅）。加入我们的 [Discord](https://s.voltagent.dev/discord) 服务器进行提问与交流。

## 贡献者 ♥️ 鸣谢

衷心感谢每一位参与 VoltAgent 旅程的伙伴，无论你是开发了插件、提交了 Issue、发起了 Pull Request，还是在 Discord 或 GitHub Discussions 中帮助过他人。

VoltAgent 是一项社区驱动的努力，正因有你这样的贡献者，它才得以不断精进。

![Contributors](https://contrib.rocks/image?repo=voltagent/voltagent&max=500&columns=20&anon=1)

## 许可证

采用 MIT 许可证授权，版权所有 © 2026 至今 VoltAgent。
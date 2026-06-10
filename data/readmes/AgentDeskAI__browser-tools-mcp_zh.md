⚠️ 本项目已不再维护，请使用其他替代方案。

# BrowserTools MCP

> 让你的 AI 工具在感知能力和浏览器交互方面提升 10 倍

该应用是一款强大的浏览器监控与交互工具，通过 Anthropic 的模型上下文协议（Model Context Protocol, MCP），使基于 AI 的应用程序能够通过 Chrome 扩展捕获并分析浏览器数据。

请参阅我们的[文档](https://browsertools.agentdesk.ai/)以获取完整的安装、快速入门及贡献指南。

## Roadmap

请在此查看我们的项目路线图：[Github Roadmap / Project Board](https://github.com/orgs/AgentDeskAI/projects/1/views/1)

## Updates

v1.2.0 已发布！以下是本次更新的简要说明：
- 你现在可以在 DevTools 面板中启用“允许自动粘贴到 Cursor”。截图将自动粘贴到 Cursor 中（请确保在 Cursor 中将焦点/点击切换到 Agent 输入框，否则将无法生效！）
- 通过 Lighthouse 集成了一套 SEO、性能、可访问性及最佳实践分析工具
- 新增针对 Next.js 的专用提示词，用于优化 Next.js 应用的 SEO
- 新增“调试器模式（Debugger Mode）”工具，按特定顺序执行所有调试工具，并附带提升推理能力的提示词
- 新增“审计模式（Audit Mode）”工具，按特定顺序执行所有审计工具
- 修复了 Windows 系统的连接问题
- 优化了 BrowserTools 服务器、扩展与 MCP 服务器之间的网络通信，新增主机/端口自动发现、自动重连及优雅关闭机制
- 增加了通过 `Ctrl+C` 更便捷地退出 BrowserTools 服务器的功能

## Quickstart Guide

运行此 MCP 工具需要三个组件：

1. 从以下链接安装我们的 Chrome 扩展：[v1.2.0 BrowserToolsMCP Chrome Extension](https://github.com/AgentDeskAI/browser-tools-mcp/releases/download/v1.2.0/BrowserTools-1.2.0-extension.zip)
2. 在你的 IDE 中通过以下命令安装 MCP 服务器：`npx @agentdeskai/browser-tools-mcp@latest`
3. 打开一个新的终端并运行此命令：`npx @agentdeskai/browser-tools-server@latest`

* 不同 IDE 的配置方式各异，但上述命令通常是一个良好的起点；请查阅你所用 IDE 的官方文档以完成正确的配置。

⚠️ **重要提示** — 你需要安装两个服务器：
- `browser-tools-server`（本地 Node.js 中间件服务器，用于收集日志）
以及
- `browser-tools-mcp`（安装到 IDE 中的 MCP 服务器，负责与扩展及 `browser-tools-server` 通信）

`npx @agentdeskai/browser-tools-mcp@latest` 是你要填入 IDE 的命令
`npx @agentdeskai/browser-tools-server@latest` 是在新终端窗口中运行的命令

完成上述三个步骤后，打开 Chrome 开发者工具（DevTools），然后进入 BrowserToolsMCP 面板。

如果仍有问题，请尝试以下步骤：
- 完全退出/关闭浏览器。不仅仅是关闭窗口，而是彻底结束所有 Chrome 进程。 
- 重启本地 Node.js 服务器（`browser-tools-server`）
- 确保只打开一个 Chrome 开发者工具面板实例

完成上述操作后通常即可正常使用。如果问题依旧，请随时反馈给我，我可以提供进一步排查日志和信息的步骤！

如有任何疑问或问题，欢迎提交 Issue！如果你有改进建议，也欢迎提出 Feature Request（添加 enhancement 标签），或直接通过 [@tedx_ai on X](https://x.com/tedx_ai) 联系我。

## Full Update Notes:

像 Cursor 这样的编程 AI 代理可以无缝地对当前页面执行这些审计。借助 Puppeteer 和 Lighthouse npm 库，BrowserTools MCP 现在能够：

- 评估页面是否符合 WCAG（Web 内容无障碍指南）标准
- 识别性能瓶颈
- 标记页内 SEO 问题
- 检查是否遵循 Web 开发最佳实践
- 审查 Next.js 相关的特定 SEO 问题

……且无需离开你的 IDE 🎉

---

## 🔑 Key Additions

| Audit Type         | Description                                                                                                                              |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------- |
| **Accessibility**  | WCAG 合规检查，包括色彩对比度、缺失的替代文本（alt text）、键盘导航陷阱、ARIA 属性等。                        |
| **Performance**    | 基于 Lighthouse 的分析，检测渲染阻塞资源、过大的 DOM 树、未优化的图片及其他影响页面速度的因素。 |
| **SEO**            | 评估页内 SEO 因素（如元数据、标题标签和链接结构），并提供提升搜索可见性的改进建议。      |
| **Best Practices** | 检查 Web 开发中的通用最佳实践。                                                                                    |
| **NextJS Audit**   | 注入专用提示词以执行 Next.js 专项审计。                                                                                         |
| **Audit Mode**     | 按顺序运行所有审计工具。                                                                                                   |
| **Debugger Mode**  | 按顺序运行所有调试工具。                                                                                                  |

---

## 🛠️ Using Audit Tools

### ✅ **Before You Start**

请确保你已具备：

- 浏览器中有一个**活动标签页（Active Tab）**
- 已启用 **BrowserTools 扩展**

### ▶️ **Running Audits**

**Headless Browser Automation**:  
Puppeteer 会自动启动一个无头 Chrome 实例来加载页面并收集审计数据，即使对于单页应用（SPA）或通过 JavaScript 动态加载的内容也能确保结果准确。

最后一次调用审计后，该无头浏览器实例将保持活动状态 **60 秒**，以便高效处理连续的审计请求。

**Structured Results**:  
每次审计均以结构化的 JSON 格式返回结果，包含总体评分和详细问题列表。这使得兼容 MCP 的客户端能够轻松解析发现内容并呈现可操作的见解。

MCP 服务器提供了在当前页面上执行审计的工具。以下是一些触发这些工具的示例查询：

#### Accessibility Audit (`runAccessibilityAudit`)

确保页面符合 WCAG 等无障碍标准。

> **Example Queries:**
>
> - "Are there any accessibility issues on this page?"
> - "Run an accessibility audit."
> - "Check if this page meets WCAG standards."

#### Performance Audit (`runPerformanceAudit`)

识别性能瓶颈和加载问题。

> **Example Queries:**
>
> - "Why is this page loading so slowly?"
> - "Check the performance of this page."
> - "Run a performance audit."

#### SEO Audit (`runSEOAudit`)

评估页面针对搜索引擎的优化程度。

> **Example Queries:**
>
> - "How can I improve SEO for this page?"
> - "Run an SEO audit."
> - "Check SEO on this page."

#### Best Practices Audit (`runBestPracticesAudit`)

检查 Web 开发中的通用最佳实践。

> **Example Queries:**
>
> - "Run a best practices audit."
> - "Check best practices on this page."
> - "Are there any best practices issues on this page?"

#### Audit Mode (`runAuditMode`)

按特定顺序运行所有审计。如果检测到框架，将自动执行 Next.js 专项审计。

> **Example Queries:**
>
> - "Run audit mode."
> - "Enter audit mode."

#### NextJS Audits (`runNextJSAudit`)

检查 Next.js 应用的最佳实践与 SEO 改进项。

> **Example Queries:**
>
> - "Run a NextJS audit."
> - "Run a NextJS audit, I'm using app router."
> - "Run a NextJS audit, I'm using page router."

#### Debugger Mode (`runDebuggerMode`)

按特定顺序运行所有调试工具。

> **Example Queries:**
>
> - "Enter debugger mode."

## Architecture

系统包含三个核心组件，均用于捕获和分析浏览器数据：

1. **Chrome Extension**: 一个浏览器扩展程序，负责捕获截图、控制台日志、网络活动及 DOM 元素。
2. **Node Server**: 作为中介服务器，促进 Chrome 扩展与任意 MCP 服务器实例之间的通信。
3. **MCP Server**: 基于模型上下文协议的服务器，为 AI 客户端提供标准化的浏览器交互工具。

```
┌─────────────┐     ┌──────────────┐     ┌───────────────┐     ┌─────────────┐
│  MCP Client │ ──► │  MCP Server  │ ──► │  Node Server  │ ──► │   Chrome    │
│  (e.g.      │ ◄── │  (Protocol   │ ◄── │ (Middleware)  │ ◄── │  Extension  │
│   Cursor)   │     │   Handler)   │     │               │     │             │
└─────────────┘     └──────────────┘     └───────────────┘     └─────────────┘
```

模型上下文协议（Model Context Protocol, MCP）是 Anthropic AI 模型支持的一项能力，允许你为任何兼容的客户端创建自定义工具。Claude Desktop、Cursor、Cline 或 Zed 等 MCP 客户端可以运行一个 MCP 服务器，该服务器会“教授”这些客户端如何使用新工具。

这些工具可以调用外部 API，但在我们的架构中，**所有日志均本地存储**在你的设备上，且绝不会发送到任何第三方服务或 API。BrowserTools MCP 会运行一个本地的 Node.js API 服务器实例，负责与 BrowserTools Chrome 扩展进行通信。

BrowserTools MCP 服务器的所有使用者均通过同一个 Node.js API 和 Chrome 扩展进行交互。

#### Chrome Extension
- 监控 XHR 请求/响应及控制台日志
- 追踪选中的 DOM 元素
- 将所有日志和当前选中元素发送至 BrowserTools 连接器（Connector）
- 连接 WebSocket 服务器以捕获/发送截图
- 允许用户配置 Token/截断限制及截图文件夹路径

#### Node Server
- 充当 Chrome 扩展与 MCP 服务器之间的中间件
- 接收来自 Chrome 扩展的日志和当前选中元素
- 处理来自 MCP 服务器的请求，以捕获日志、截图或当前元素
- 向 Chrome 扩展发送 WebSocket 命令以截取屏幕截图
- 智能截断日志中的字符串和重复对象数量，以避免触发 Token 限制
- 移除 Cookie 及敏感请求头，防止将其发送给 MCP 客户端中的大语言模型（LLM）

#### MCP Server
- 实现模型上下文协议
- 为 AI 客户端提供标准化交互工具
- 兼容多种 MCP 客户端（Cursor、Cline、Zed、Claude Desktop 等）

## Installation

详细安装步骤请参阅我们的官方文档：

- [BrowserTools MCP Docs](https://browsertools.agentdesk.ai/)

## Usage

安装并配置完成后，该系统允许任何兼容的 MCP 客户端执行以下操作：

- 监控浏览器控制台输出
- 捕获网络流量
- 截取屏幕截图
- 分析选中的 DOM 元素
- 清除存储在 MCP 服务器中的日志
- 执行可访问性、性能、SEO 及最佳实践审计

## Compatibility

- 兼容任何支持 MCP 协议的客户端
- 主要面向 Cursor IDE 集成进行优化设计
- 同时支持其他 AI 编辑器及 MCP 客户端
# GitMCP

<p align="center">
  <img width="884" alt="image" src="https://github.com/user-attachments/assets/2bf3e3df-556c-49c6-ab7b-36c279d53bba" />
</p>

<p align="center">
  <a href="#%F0%9F%A4%B4-%E4%BB%80%E4%B9%88%E6%98%AF-gitmcp">什么是 GitMCP</a> •
  <a href="#%E2%9C%A8-%E6%A0%B8%E5%BF%83%E5%8A%9F%E8%83%BD">核心功能</a> •
  <a href="#%F0%9F%9A%80-%E5%BF%AB%E9%80%9F%E5%BC%80%E5%A7%8B">快速开始</a> •
  <a href="#%E2%8C%99-%E5%B7%A5%E4%BD%9C%E5%8E%9F%E7%90%86">工作原理</a> •
  <a href="#-badge">徽章（Badge）</a> •
  <a href="#-examples">使用示例</a> •
  <a href="#-faq">常见问题</a> •
  <a href="#-privacy">隐私保护</a> •
  <a href="#-contributing">参与贡献</a> •
  <a href="#-license">许可证</a>
</p>
<div align="center">

[![GitMCP](https://img.shields.io/endpoint?url=https://gitmcp.io/badge/idosal/git-mcp)](https://gitmcp.io/idosal/git-mcp)
[![Twitter Follow](https://img.shields.io/twitter/follow/idosal1?style=social)](https://twitter.com/idosal1)
[![Twitter Follow](https://img.shields.io/twitter/follow/liadyosef?style=social)](https://twitter.com/liadyosef)
</div>

<div align="center">
  <a href="https://www.pulsemcp.com/servers/idosal-git-mcp"><img src="https://www.pulsemcp.com/badge/top-pick/idosal-git-mcp" width="400" alt="Pulse MCP Badge"></a>
</div>

## 🤔 什么是 GitMCP？
**告别“氛围感幻觉”，开启精准编码！**

[GitMCP](https://gitmcp.io) 是一款免费、开源的远程 [模型上下文协议（Model Context Protocol, MCP）](https://docs.anthropic.com/en/docs/agents-and-tools/mcp) 服务器，它能将 **任何** GitHub 项目（仓库或 GitHub Pages 站点）转化为文档中心。它使 Cursor 等 AI 工具能够访问最新的文档和代码，即使大语言模型（LLM）从未接触过这些内容，从而无缝消除代码幻觉问题。

GitMCP 支持 **两种模式**：

*   **特定仓库模式 (`gitmcp.io/{owner}/{repo}` 或 `{owner}.gitmcp.io/{repo}`)：** 当你主要使用少数几个库时推荐使用此模式。这能确保你的 AI 助手始终定位到正确的项目，通过防止访问非目标仓库来提升安全性和相关性。
*   **通用服务器模式 (`gitmcp.io/docs`)：** 当你需要频繁切换不同仓库时使用此模式以获得最大灵活性。AI 助手会在每次请求前提示你（或根据上下文自动判断）要访问哪个仓库。请注意，该模式依赖每次都能准确识别目标仓库。

**使用 GitMCP 可以带来以下优势：**

*   AI 助手能够直接从源码获取 *最新* 的文档和代码。
*   获得准确的 API 使用说明和可靠的代码示例。
*   即使面对冷门、新兴或快速迭代的库，也能高效工作。
*   显著减少幻觉问题，大幅提升代码正确性。

例如，以下并排对比展示了在 Cursor 中创建 [three.js](https://github.com/mrdoob/three.js) 场景时，使用相同一次性提示词（one-shot prompt）的结果：

https://github.com/user-attachments/assets/fbf1b4a7-f9f0-4c0e-831c-4d64faae2c45

## ✨ 核心功能

- 😎 **任意 GitHub 项目的最新文档**：让你的 AI 助手无缝访问 GitHub 项目的文档和代码。内置的智能搜索功能可精准定位 AI 所需内容，同时避免消耗过多 Token！
- 🧠 **彻底告别幻觉**：借助 GitMCP，你的 AI 助手能够针对你的问题提供准确且相关的解答。
- ☁️ **零配置部署**：GitMCP 运行在云端。只需将你选定的 GitMCP URL 添加为 IDE 中的 MCP 服务器即可——无需下载、安装、注册或进行任何修改。
- 💬 **内置聊天窗口**：通过我们的网页端聊天功能，直接与仓库文档对话，快速上手！
- ✅ **开放、免费且私密**：GitMCP 开源且完全免费使用。它不收集个人信息，也不存储查询记录。你甚至可以进行自托管（Self-host）部署！

<video src="https://github.com/user-attachments/assets/2c3afaf9-6c08-436e-9efd-db8710554430"></video>

## 🚀 快速开始

使用 GitMCP 非常简单！只需按照以下步骤操作：

### 步骤 1：选择服务器类型

根据你的连接目标，选择以下 URL 格式之一：

- GitHub 仓库：`gitmcp.io/{owner}/{repo}`
- GitHub Pages 站点：`{owner}.gitmcp.io/{repo}`
- 支持任意仓库的通用工具（动态）：`gitmcp.io/docs`

将 `{owner}` 替换为 GitHub 用户名或组织名称，将 `{repo}` 替换为仓库名称。

为方便起见，你也可以在首页使用转换工具，将 GitHub URL 自动格式化为 MCP URL！

### 步骤 2：连接你的 AI 助手

从下方选择你的 AI 助手，并按照配置说明操作：

#### 连接 Cursor

更新 `~/.cursor/mcp.json` 中的 Cursor 配置文件：
   ```json
   {
     "mcpServers": {
       "gitmcp": {
         "url": "https://gitmcp.io/{owner}/{repo}"
       }
     }
   }
   ```

#### 连接 Claude Desktop

1. 在 Claude Desktop 中，进入 Settings > Developer > Edit Config
2. 将配置替换为：
   ```json
   {
     "mcpServers": {
       "gitmcp": {
         "command": "npx",
         "args": [
           "mcp-remote",
           "https://gitmcp.io/{owner}/{repo}"
         ]
       }
     }
   }
   ```

#### 连接 Windsurf

更新 `~/.codeium/windsurf/mcp_config.json` 中的 Windsurf 配置文件：
   ```json
   {
     "mcpServers": {
       "gitmcp": {
         "serverUrl": "https://gitmcp.io/{owner}/{repo}"
       }
     }
   }
   ```

#### 连接 VS Code

更新 `.vscode/mcp.json` 中的 VS Code 配置文件：
   ```json
   {
     "servers": {
       "gitmcp": {
         "type": "sse",
         "url": "https://gitmcp.io/{owner}/{repo}"
       }
     }
   }
   ```

#### 连接 Cline

更新 `~/Library/Application Support/Code/User/globalStorage/saoudrizwan.claude-dev/settings/cline_mcp_settings.json` 中的 Cline 配置文件：
   ```json
   {
     "mcpServers": {
       "gitmcp": {
         "url": "https://gitmcp.io/{owner}/{repo}",
         "disabled": false,
         "autoApprove": []
       }
     }
   }
   ```

#### 连接 Highlight AI

1. 打开 Highlight AI，点击侧边栏的插件图标（@ 符号）
2. 在侧边栏顶部点击 **Installed Plugins**
3. 选择 **Custom Plugin**
4. 点击 **Add a plugin using a custom SSE URL**

插件名称：`gitmcp`
SSE URL：`https://gitmcp.io/{owner}/{repo}`

有关向 Highlight AI 添加自定义 MCP 服务器的更多详情，请参阅 [官方文档](https://docs.highlightai.com/plugins/custom)。

#### 连接 Augment Code

1. 打开 Augment Code 设置
2. 导航至 MCP 部分
3. 使用以下信息添加新的 MCP 服务器：

MCP 服务器名称：`git-mcp Docs`

使用此命令：
```bash
npx mcp-remote https://gitmcp.io/{owner}/{repo}
```

或使用以下配置：
```json
{
  "mcpServers": {
    "git-mcp Docs": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "https://gitmcp.io/{owner}/{repo}"
      ]
    }
  }
}
```

#### 连接 Msty AI
1. 打开 Msty Studio
2. 进入 Tools > Import Tools from JSON Clipboard
3. 粘贴以下配置：

```json
{
  "mcpServers": {
    "git-mcp Docs": {
      "command": "npx",
      "args": [
        "mcp-remote",
        "https://gitmcp.io/{owner}/{repo}"
      ]
    }
  }
}
```

有关在 Augment Code 中配置 MCP 服务器的更多详情，请访问 [Augment Code 官方文档](https://docs.augmentcode.com/setup-augment/mcp)。

> **注意：** 请记得将 `{owner}` 和 `{repo}` 替换为实际的 GitHub 用户名/组织名及仓库名称。你也可以使用动态端点 `https://gitmcp.io/docs`，让你的 AI 按需访问任意仓库。

## ⚙ 工作原理

GitMCP 通过模型上下文协议（MCP）——一种允许 AI 工具从外部源请求额外信息的标准协议——将你的 AI 助手与 GitHub 仓库连接起来。

使用 GitMCP 时发生的过程：

1. **你向 AI 助手提供 GitMCP URL**（例如 `gitmcp.io/microsoft/typescript`）。GitMCP 会暴露文档获取、智能搜索、代码搜索等工具接口。
2. **针对文档/代码相关问题提示 AI 助手**。
3. **你的 AI 发送请求** 到 GitMCP 以使用其工具（需经你批准）。
4. **GitMCP 执行 AI 的请求** 并返回所需数据。
5. **你的 AI 接收信息** 并生成更准确、有据可依的回复，彻底消除幻觉。

### 支持的文档格式

GitMCP 目前按优先级支持以下文档：
1. [llms.txt](https://llmstxt.org)
2. 项目文档的 AI 优化版本
3. `README.md`/根目录文件

## 💡 使用示例

以下是如何结合不同 AI 助手和仓库使用 GitMCP 的示例：

### 示例 1：在 Windsurf 中使用特定仓库

对于 GitHub 仓库 `https://github.com/microsoft/playwright-mcp`，将 `https://gitmcp.io/microsoft/playwright-mcp` 添加为 Windsurf 的 MCP 服务器。

**向 Claude 发送提示词：**
> "How do I use the Playwright MCP"

Windsurf 将从 GitMCP 拉取相关文档以正确实现记忆功能。

### 示例 2：在 Cursor 中使用 GitHub Pages 站点

对于 GitHub Pages 站点 `langchain-ai.github.io/langgraph`，将 `https://langchain-ai.gitmcp.io/langgraph` 添加为 Cursor 的 MCP 服务器。

**向 Cursor 发送提示词：**
> "Add memory to my LangGraph agent"

Cursor 将从 GitMCP 拉取相关文档和代码以正确实现记忆功能。

### 示例 3：在 Claude Desktop 中使用动态端点

你无需指定特定仓库。通用的 `gitmcp.io/docs` 端点允许 AI 随时自主选择 GitHub 项目！

**向任意 AI 助手发送提示词：**
> "I want to learn about the OpenAI Whisper speech recognition model. Explain how it works."

Claude 将从 GitMCP 拉取数据并回答问题。

## 🛠️ 提供工具

GitMCP 为 AI 助手提供了多个实用工具，帮助它们访问、理解及查询 GitHub 仓库。

### `fetch_<repo-name>_documentation`

此工具用于获取 GitHub 仓库的主要文档。它通过检索相关文档（例如 `llms.txt`）来实现。这能让 AI 对项目的全貌有一个良好的概览。

**适用场景：** 关于项目用途、功能或入门指南的通用问题

### `search_<repo-name>_documentation`

此工具允许 AI 通过提供具体查询词来搜索仓库文档。它不会加载全部文档（可能非常庞大），而是使用智能搜索仅定位相关内容部分。

**适用场景：** 针对项目中特定功能、函数或概念的详细问题

### `fetch_url_content`

此工具帮助 AI 获取文档中提及的链接内容。它会检索这些链接的内容并将其转换为 AI 易于阅读的格式。

**适用场景：** 当文档引用了有助于解答你问题的外部信息时

### `search_<repo-name>_code`

此工具使用 GitHub 的代码搜索功能在仓库实际代码中进行查找。它帮助 AI 定位具体的代码示例或实现细节。

**适用场景：** 当你需要查看某功能的实现方式，或获取文档未涵盖的技术细节时

> **注意：** 当使用动态端点（`gitmcp.io/docs`）时，这些工具的名称略有不同（分别为 `fetch_generic_documentation`、`search_generic_code` 和 `search_generic_documentation`），且需要提供额外的信息以指定要访问的仓库。

## 📊 徽章（Badge）

GitMCP 为你的仓库 README 提供了专属徽章。它允许用户通过 IDE 或浏览器（使用内置聊天功能）快速访问你的文档。同时，它还能展示你的文档通过 GitMCP 被访问的次数。

示例 (`idosal/git-mcp`)：[![GitMCP](https://img.shields.io/endpoint?url=https://gitmcp.io/badge/idosal/git-mcp)](https://gitmcp.io/idosal/git-mcp)

### 将徽章添加到你的仓库

在你的 `README.md` 中添加以下内容：

```markdown
[![GitMCP](https://img.shields.io/endpoint?url=https://gitmcp.io/badge/OWNER/REPO)](https://gitmcp.io/OWNER/REPO)
```

将 `OWNER` 替换为你的 GitHub 用户名或组织名，将 `REPO` 替换为你的仓库名称。

### 浏览量统计规则

每次针对该特定仓库的工具调用都会使计数加一。

### 自定义徽章样式

你可以通过参数自定义徽章的外观：

| 参数 | 说明 | 默认值 | 示例 |
|-----------|-------------|---------|---------|
| `color` | 徽章数值的颜色 | `aquamarine` | `?color=green` |
| `label` | 徽章标签文本 | `GitMCP` | `Documentation`

如需帮助，请随时联系我们！

## ❓ 常见问题 (FAQ)

### 什么是模型上下文协议（Model Context Protocol）？

[模型上下文协议](https://modelcontextprotocol.io/introduction) 是一项标准协议，允许 AI 助手以结构化方式向外部源请求和接收额外上下文信息，从而增强其理解能力和表现。

### GitMCP 兼容所有 AI 助手吗？

是的，GitMCP 与任何支持模型上下文协议的 AI 助手兼容，包括 Cursor、VS Code、Claude 等工具。

### GitMCP 兼容所有 GitHub 项目吗？

完全没问题！GitMCP 适用于任何公开的 GitHub 仓库，无需进行任何修改。它会优先读取 `llms.txt` 文件；如果该文件不可用，则回退到 `README.md` 或其他页面。未来的更新计划支持更多文档格式，甚至动态生成内容。

### GitMCP 需要付费吗？

不需要，GitMCP 是面向社区的免费服务，没有任何费用。

## 🔒 隐私保护

GitMCP 高度重视用户隐私。该服务无需身份验证即可访问，因此不获取或存储任何个人可识别信息（PII）。此外，它也不会存储 AI 助手发送的任何查询记录。而且，由于 GitMCP 是开源项目，你可以在自己的环境中独立部署。

GitMCP 仅访问已公开可用的内容，且仅在用户主动查询时进行访问。GitMCP 不会自动爬取仓库。在访问任何 GitHub Pages 站点之前，代码会检查 `robots.txt` 规则并遵循站点所有者设置的指令，允许他们选择退出（opt-out）。请注意，GitMCP 不会永久存储关于 GitHub 项目或其内容的数据。

## 👥 参与贡献

我们欢迎任何形式的贡献、反馈和想法！请查阅我们的 [贡献指南](https://github.com/idosal/git-mcp/blob/main/.github/CONTRIBUTING.md)。

### 本地开发环境搭建

1. **克隆仓库**
   ```bash
   git clone https://github.com/idosal/git-mcp.git
   cd git-mcp
   ```

2. **安装依赖**
   ```bash
   pnpm install
   ```

3. **本地运行进行开发**
   ```bash
   npm run dev
   # 或
   pnpm dev
   ```

#### 使用 MCP Inspector 进行测试

1. 安装 MCP Inspector 工具：
   ```bash
   npx @modelcontextprotocol/inspector
   ```

2. 在 Inspector 界面中：
   - 将传输类型（Transport Type）设置为 `SSE`
   - 输入你的 GitMCP URL（例如 `http://localhost:5173/docs`）
   - 点击 "Connect"

## 📄 许可证

本项目采用 [Apache License 2.0](LICENSE) 许可。

## 免责声明

GitMCP 按“原样”提供，不提供任何形式的明示或暗示担保。虽然我们致力于确保服务的可靠性和安全性，但不对因其使用而产生的任何损害或问题承担责任。通过 GitMCP 访问的 GitHub 项目受其各自所有者的条款和条件约束。GitMCP 与 GitHub 或任何提及的 AI 工具均无隶属关系。

## ⭐ Star History

[![Star History Chart](https://api.star-history.com/svg?repos=idosal/git-mcp&type=Timeline)](https://www.star-history.com/#idosal/git-mcp&Timeline)
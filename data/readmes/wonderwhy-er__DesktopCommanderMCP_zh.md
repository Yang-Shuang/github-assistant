# Desktop Commander MCP
### 使用 AI 搜索、更新、管理文件并运行终端命令

[![npm downloads](https://img.shields.io/npm/dw/@wonderwhy-er/desktop-commander)](https://www.npmjs.com/package/@wonderwhy-er/desktop-commander)
[![AgentAudit Verified](https://agentaudit.dev/api/badge/desktop-commander)](https://agentaudit.dev/skills/desktop-commander)
[![Trust Score](https://archestra.ai/mcp-catalog/api/badge/quality/wonderwhy-er/DesktopCommanderMCP)](https://archestra.ai/mcp-catalog/wonderwhy-er__desktopcommandermcp)
[![smithery badge](https://smithery.ai/badge/@wonderwhy-er/desktop-commander)](https://smithery.ai/server/@wonderwhy-er/desktop-commander)
[![Buy Me A Coffee](https://img.shields.io/badge/Buy%20Me%20A%20Coffee-support-yellow.svg)](https://www.buymeacoffee.com/wonderwhyer)


[![Discord](https://img.shields.io/badge/Join%20Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/kQ27sNnZr7)


处理代码和文本，运行进程并自动化任务，超越其他 AI 编辑器——同时使用宿主客户端订阅而非 API Token 费用。

<a href="https://glama.ai/mcp/servers/zempur9oh4">
  <img width="380" height="200" src="https://glama.ai/mcp/servers/zempur9oh4/badge" alt="Desktop Commander MCP" />
</a>

## 👋 我们正在招聘 — 来和我们一起构建：https://desktopcommander.app/careers/

## 🖥️ 试用 Desktop Commander 应用（Beta）

**想要更好的体验？** Desktop Commander 应用提供了 MCP 服务器具备的所有功能，并额外支持：

- **使用任意 AI 模型** —— Claude、GPT-4.5、Gemini 2.5 或你偏好的任何模型
- **实时查看文件更改** —— AI 编辑文件时提供可视化预览
- **添加自定义 MCP 和上下文** —— 使用你自己的工具进行扩展，无需配置文件
- **即将推出** —— 技能系统、语音输入、后台定时任务等更多功能

**👉 [下载应用](https://desktopcommander.app/#download)**（支持 macOS 和 Windows）

> 下方的 MCP 服务器在 Claude Desktop 和其他 MCP 客户端中依然运行良好——本应用专为追求专属、精致体验的用户设计。

## 目录
- [功能特性](#features)
- [安装指南](#how-to-install)
- [快速上手](#getting-started)
- [使用方法](#usage)
- [文件预览界面与 Markdown 编辑器](#file-preview-ui--markdown-editor)
- [处理长时间运行的命令](#handling-long-running-commands)
- [开发计划与待办事项](#roadmap)
- [赞助商与支持者](#support-desktop-commander)
- [官方网站](#website)
- [媒体报道](#media)
- [用户评价](#testimonials)
- [常见问题解答](#frequently-asked-questions)
- [贡献指南](#contributing)
- [许可证](#license)

将你的所有 AI 开发工具集中于一处。Desktop Commander 将所有开发工具整合到一个聊天窗口中。通过模型上下文协议（Model Context Protocol, MCP）在本地计算机上执行长时间运行的终端命令并管理进程。基于 [MCP Filesystem Server](https://github.com/modelcontextprotocol/servers/tree/main/src/filesystem) 构建，提供额外的搜索替换与文件编辑功能。

## 功能特性

- **远程 AI 控制** - 通过 [Remote MCP](https://mcp.desktopcommander.app) 从 ChatGPT、Claude Web 及其他 AI 服务中使用 Desktop Commander
- **文件预览界面** - 在 Claude Desktop 中提供可视化文件预览，支持渲染 Markdown、内联图片、可展开内容、内置 Markdown 编辑器以及快捷“在文件夹中打开”功能
- **增强的终端命令与交互式进程控制**
- **内存中执行代码（Python、Node.js、R）而无需保存文件**
- **即时数据分析** - 只需要求分析 CSV/JSON/Excel 文件即可开始
- **原生 Excel 文件支持** - 无需外部工具即可读取、写入、编辑和搜索 Excel 文件（.xlsx, .xls, .xlsm）
- **PDF 支持** - 通过文本提取读取 PDF，从 Markdown 创建新 PDF，修改现有 PDF
- **DOCX 支持** - 使用精准 XML 编辑和 Markdown 到 DOCX 转换功能来读取、创建、编辑和搜索 Word 文档（.docx）
- **与运行中的进程交互（SSH、数据库、开发服务器）**
- 执行终端命令并流式输出结果
- 支持命令超时设置和后台执行
- 进程管理（列出和终止进程）
- 长时间运行命令的会话管理
- **进程输出分页** - 通过偏移量/长度控制读取终端输出，防止上下文溢出
- 服务器配置管理：
  - 获取/设置配置值
  - 一次性更新多项设置
  - 无需重启服务器即可动态更改配置
- 完整的文件系统操作：
  - 读写文件（文本、Excel、PDF、DOCX）
  - 创建/列出目录
  - **递归目录列表** - 支持可配置深度和上下文溢出保护，适用于大型文件夹
  - 移动文件或目录
  - 搜索文件和内容（包括 Excel 内容）
  - 获取文件元数据
  - **负偏移量文件读取**：使用负偏移值从文件末尾开始读取（类似 Unix tail 命令）
- 代码编辑功能：
  - 针对小范围更改的精准文本替换
  - 针对重大更改的全文件重写
  - 支持多文件操作
  - 基于模式的替换
  - 基于 vscode-ripgrep 的文件夹递归代码或文本搜索
- 全面的审计日志（Audit Logging）：
  - 所有工具调用均自动记录日志
  - 支持日志轮转，限制大小为 10MB
  - 详细的 timestamp（时间戳）和参数记录
- 安全加固：
  - 防止文件操作中的符号链接遍历攻击
  - 命令黑名单及防绕过保护
  - [Docker 隔离](#option-6-docker-installation--auto-updates-no-nodejs-required) 实现完全沙盒化运行
  - 详见 [SECURITY.md](SECURITY.md)

## 安装指南

### 在 Claude Desktop 中安装

Desktop Commander 为 Claude Desktop 提供多种安装方式。

> **📋 更新与卸载信息：** 选项 1、2、3、4 和 6 支持自动更新。选项 5 需要手动更新。详见下方说明。

<details>
<summary><b>选项 1：通过 npx 安装 ⭐ 自动更新（需 Node.js）</b></summary>

只需在终端中运行：
```
npx @wonderwhy-er/desktop-commander@latest setup
```

调试模式（允许 Node.js 调试器连接）：
```
npx @wonderwhy-er/desktop-commander@latest setup --debug
```

**安装过程中的命令行选项：**
- `--debug`：启用 Node.js 调试器的调试模式
- `--no-onboarding`：禁用新用户引导提示

如果 Claude 正在运行，请重启。

**✅ 自动更新：** 是 - 重启 Claude 时自动更新  
**🔄 手动更新：** 再次运行安装命令  
**🗑️ 卸载：** 运行 `npx @wonderwhy-er/desktop-commander@latest remove`

</details>

<details>
<summary><b>选项 2：使用 bash 脚本安装器（macOS） ⭐ 自动更新（按需安装 Node.js）</b></summary>

```
curl -fsSL https://raw.githubusercontent.com/wonderwhy-er/DesktopCommanderMCP/refs/heads/main/install.sh | bash
```
该脚本会自动处理所有依赖项和配置。

**✅ 自动更新：** 是  
**🔄 手动更新：** 重新运行上方的 bash 安装器命令  
**🗑️ 卸载：** 运行 `npx @wonderwhy-er/desktop-commander@latest remove`

</details>

<details>
<summary><b>选项 3：通过 Smithery 安装 ⭐ 自动更新（需 Node.js）</b></summary>

1. **访问：** https://smithery.ai/server/@wonderwhy-er/desktop-commander
2. **登录 Smithery**（如尚未登录）
3. **在右侧选择你的客户端**（Claude Desktop）
4. **使用显示提供的密钥进行安装**
5. **重启 Claude Desktop**

**✅ 自动更新：** 是 - 重启 Claude 时自动更新  
**🔄 手动更新：** 访问 Smithery 页面并重新安装  

</details>

<details>
<summary><b>选项 4：手动添加到 claude_desktop_config ⭐ 自动更新（需 Node.js）</b></summary>

将此条目添加到你的 claude_desktop_config.json：

- Mac: `~/Library/Application Support/Claude/claude_desktop_config.json`
- Windows: `%APPDATA%\Claude\claude_desktop_config.json`
- Linux: `~/.config/Claude/claude_desktop_config.json`

```json
{
  "mcpServers": {
    "desktop-commander": {
      "command": "npx",
      "args": [
        "-y",
        "@wonderwhy-er/desktop-commander@latest"
      ]
    }
  }
}
```
如果 Claude 正在运行，请重启。

**✅ 自动更新：** 是 - 重启 Claude 时自动更新  
**🔄 手动更新：** 再次运行安装命令  
**🗑️ 卸载：** 运行 `npx @wonderwhy-er/desktop-commander@latest remove` 或从你的 claude_desktop_config.json 中移除该条目

</details>

<details>
<summary><b>选项 5：本地检出 ❌ 手动更新（需 Node.js）</b></summary>

```bash
git clone https://github.com/wonderwhy-er/DesktopCommanderMCP.git
cd DesktopCommanderMCP
npm run setup
```
如果 Claude 正在运行，请重启。

setup 命令将安装依赖项、构建服务器并配置 Claude 桌面应用。

**❌ 自动更新：** 否 - 需要手动 git 更新  
**🔄 手动更新：** `cd DesktopCommanderMCP && git pull && npm run setup`  
**🗑️ 卸载：** 运行 `npx @wonderwhy-er/desktop-commander@latest remove` 或移除克隆的目录和 Claude 配置中的 MCP 服务器条目

</details>

<details>
<summary><b>选项 6：Docker 安装 🐳 ⭐ 自动更新（无需 Node.js）</b></summary>

非常适合需要隔离环境或未安装 Node.js 的用户。在沙盒化的 Docker 容器中运行，并带有持久化工作目录。

**前置条件：** 已安装并正在运行的 [Docker Desktop](https://www.docker.com/products/docker-desktop/)，以及 Claude Desktop 应用。

**macOS/Linux：**
```bash
bash <(curl -fsSL https://raw.githubusercontent.com/wonderwhy-er/DesktopCommanderMCP/refs/heads/main/install-docker.sh)
```

**Windows PowerShell：**
```powershell
iex ((New-Object System.Net.WebClient).DownloadString('https://raw.githubusercontent.com/wonderwhy-er/DesktopCommanderMCP/refs/heads/main/install-docker.ps1'))
```

安装程序将检查 Docker、拉取镜像、提示挂载文件夹，并配置 Claude Desktop。

**Docker 持久化：** 你的工具、配置、工作文件和包缓存都会在重启后保留。

<details>
<summary>手动 Docker 配置</summary>

**基础设置（无文件访问）：**
```json
{
  "mcpServers": {
    "desktop-commander-in-docker": {
      "command": "docker",
      "args": ["run", "-i", "--rm", "mcp/desktop-commander:latest"]
    }
  }
}
```

**带文件夹挂载：**
```json
{
  "mcpServers": {
    "desktop-commander-in-docker": {
      "command": "docker",
      "args": [
        "run", "-i", "--rm",
        "-v", "/Users/username/Desktop:/mnt/desktop",
        "-v", "/Users/username/Documents:/mnt/documents",
        "mcp/desktop-commander:latest"
      ]
    }
  }
}
```

**高级文件夹挂载：**
```json
{
  "mcpServers": {
    "desktop-commander-in-docker": {
      "command": "docker",
      "args": [
        "run", "-i", "--rm",
        "-v", "dc-system:/usr",
        "-v", "dc-home:/root", 
        "-v", "dc-workspace:/workspace",
        "-v", "dc-packages:/var",
        "-v", "/Users/username/Projects:/mnt/Projects",
        "-v", "/Users/username/Downloads:/mnt/Downloads",
        "mcp/desktop-commander:latest"
      ]
    }
  }
}
```

</details>

<details>
<summary>Docker 管理命令</summary>

**macOS/Linux：**
```bash
# 检查状态
bash <(curl -fsSL https://raw.githubusercontent.com/wonderwhy-er/DesktopCommanderMCP/refs/heads/main/install-docker.sh) --status

# 重置所有持久化数据
bash <(curl -fsSL https://raw.githubusercontent.com/wonderwhy-er/DesktopCommanderMCP/refs/heads/main/install-docker.sh) --reset
```

**Windows PowerShell：**
```powershell
# 检查状态
$script = (New-Object System.Net.WebClient).DownloadString('https://raw.githubusercontent.com/wonderwhy-er/DesktopCommanderMCP/refs/heads/main/install-docker.ps1'); & ([ScriptBlock]::Create("$script")) -Status

# 重置所有数据
$script = (New-Object System.Net.WebClient).DownloadString('https://raw.githubusercontent.com/wonderwhy-er/DesktopCommanderMCP/refs/heads/main/install-docker.ps1'); & ([ScriptBlock]::Create("$script")) -Reset

# 显示帮助
$script = (New-Object System.Net.WebClient).DownloadString('https://raw.githubusercontent.com/wonderwhy-er/DesktopCommanderMCP/refs/heads/main/install-docker.ps1'); & ([ScriptBlock]::Create("$script")) -Help
```

**故障排除：** 从头开始重置并重新安装：
```bash
bash <(curl -fsSL https://raw.githubusercontent.com/wonderwhy-er/DesktopCommanderMCP/refs/heads/main/install-docker.sh) --reset && bash <(curl -fsSL https://raw.githubusercontent.com/wonderwhy-er/DesktopCommanderMCP/refs/heads/main/install-docker.sh)
```

</details>

**✅ 自动更新：** 是 - `latest` 标签会自动获取新版本  
**🔄 手动更新：** `docker pull mcp/desktop-commander:latest` 然后重启 Claude  

</details>

### 在其他客户端中安装

Desktop Commander 可与任何兼容 MCP 的客户端配合使用。标准 JSON 配置如下：

```json
{
  "mcpServers": {
    "desktop-commander": {
      "command": "npx",
      "args": ["-y", "@wonderwhy-er/desktop-commander@latest"]
    }
  }
}
```

将此添加到你的客户端 MCP 配置文件，位置如下：

<details>
<summary><b>C</b></summary><br>

[![Install MCP Server](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/en-US/install-mcp?name=desktop-commander&config=eyJjb21tYW5kIjoibnB4IiwiYXJncyI6WyIteSIsIkB3b25kZXJ3aHktZXIvZGVza3RvcC1jb21tYW5kZXJAbGF0ZXN0Il19)

[View MCP Server in Directory](https://cursor.directory/mcp/desktop-commander-mcp)

或手动添加到 `~/.cursor/mcp.json`（全局）或项目文件夹中的 `.cursor/mcp.json`（项目特定）。

详见 [Cursor MCP 文档](https://docs.cursor.com/context/model-context-protocol)。

</details>

<details>
<summary><b>Windsurf</b></summary>

添加到 `~/.codeium/windsurf/mcp_config.json`。详见 [Windsurf MCP 文档](https://docs.windsurf.com/windsurf/cascade/mcp)。

</details>

<details>
<summary><b>VS Code / GitHub Copilot</b></summary>

添加到项目中的 `.vscode/mcp.json` 或 VS Code 用户设置（JSON）中。确保 Chat > MCP 下已启用 MCP。支持 Agent 模式。

详见 [VS Code MCP 文档](https://code.visualstudio.com/docs/copilot/chat/mcp-servers)。

</details>

<details>
<summary><b>Cline</b></summary>

通过 VS Code 中的 Cline 扩展设置进行配置。打开 Cline 侧边栏，点击 MCP Servers 图标，并添加上方的 JSON 配置。详见 [Cline MCP 文档](https://docs.cline.bot/mcp/configuring-mcp-servers)。

</details>

<details>
<summary><b>Roo Code</b></summary>

添加到你的 Roo Code MCP 配置文件。详见 [Roo Code MCP 文档](https://docs.roocode.com/features/mcp/using-mcp-in-roo)。

</details>

<details>
<summary><b>Claude Code</b></summary>

```sh
claude mcp add --scope user desktop-commander -- npx -y @wonderwhy-er/desktop-commander@latest
```

移除 `--scope user` 仅在当前项目中安装。详见 [Claude Code MCP 文档](https://docs.anthropic.com/en/docs/claude-code/mcp)。

</details>

<details>
<summary><b>Trae</b></summary>

使用“手动添加”功能并粘贴上方的 JSON 配置。详见 [Trae MCP 文档](https://docs.trae.ai/ide/model-context-protocol?_lang=en)。

</details>

<details>
<summary><b>Kiro</b></summary>

导航至 `Kiro` > `MCP Servers`，点击 `+ Add`，并粘贴上方的 JSON 配置。详见 [Kiro MCP 文档](https://kiro.dev/docs/mcp/configuration/)。

</details>

<details>
<summary><b>Codex (OpenAI)</b></summary>

Codex 使用 TOML 配置。运行以下命令添加 Desktop Commander：

```sh
codex mcp add desktop-commander -- npx -y @wonderwhy-er/desktop-commander@latest
```

或手动添加到 `~/.codex/config.toml`：

```toml
[mcp_servers.desktop-commander]
command = "npx"
args = ["-y", "@wonderwhy-er/desktop-commander@latest"]
```

详见 [Codex MCP 文档](https://developers.openai.com/codex/mcp/)。

</details>

<details>
<summary><b>JetBrains (AI Assistant)</b></summary>

在 JetBrains IDE 中，前往 **Settings → Tools → AI Assistant → Model Context Protocol (MCP)**，点击 `+` Add，选择 **As JSON**，并粘贴上方的 JSON 配置。详见 [JetBrains MCP 文档](https://www.jetbrains.com/help/ai-assistant/configure-an-mcp-server.html)。

</details>

<details>
<summary><b>Gemini CLI</b></summary>

添加到 `~/.gemini/settings.json`：

```json
{
  "mcpServers": {
    "desktop-commander": {
      "command": "npx",
      "args": ["-y", "@wonderwhy-er/desktop-commander@latest"]
    }
  }
}
```

详见 [Gemini CLI 文档](https://github.com/google-gemini/gemini-cli)。

</details>

<details>
<summary><b>Augment Code</b></summary>

按 `Cmd/Ctrl+Shift+P`，打开 Augment 面板，并添加一个名为 `desktop-commander` 的新 MCP 服务器，配置为上方的 JSON。详见 [Augment Code MCP 文档](https://docs.augmentcode.com/setup-augment/mcp)。

</details>

<details>
<summary><b>Qwen Code</b></summary>

运行以下命令添加 Desktop Commander：

```sh
qwen mcp add desktop-commander -- npx -y @wonderwhy-er/desktop-commander@latest
```

或添加到 `.qwen/settings.json`（项目）或 `~/.qwen/settings.json`（全局）。详见 [Qwen Code MCP 文档](https://qwenlm.github.io/qwen-code-docs/en/developers/tools/mcp-server/)。

</details>

<details>
<summary><b>ChatGPT / Claude Web (Remote MCP)</b></summary>

通过 Remote MCP 从 **ChatGPT**、**Claude web** 及其他 AI 服务中使用 Desktop Commander —— 无需桌面应用。

**👉 [在 mcp.desktopcommander.app 开始使用](https://mcp.desktopcommander.app)**

工作原理：
1. 你在计算机上运行轻量级的 **Remote Device**
2. 它安全地连接到云端 Remote MCP 服务
3. 你的 AI 通过云端向你的设备发送命令
4. 命令在本地执行，结果返回给 AI
5. **你始终保持控制权** —— 随时使用 `Ctrl+C` 停止

### 安全性

- ✅ 仅在你启动时运行
- ✅ 命令在你的用户权限下执行
- ✅ 安全的 OAuth 认证和加密通信通道

</details>

## 更新与卸载 Desktop Commander

### 自动更新（选项 1、2、3、4 & 6）
**选项 1 (npx)、选项 2 (bash 安装器)、3 (Smithery)、4 (手动配置) 和 6 (Docker)** 会在你每次重启 Claude 时自动更新至最新版本。无需任何手动干预。

### 手动更新（选项 5）
- **选项 5 (本地检出):** `cd DesktopCommanderMCP && git pull && npm run setup`

### 卸载 Desktop Commander
#### 🤖 自动卸载（推荐）

完全移除 Desktop Commander 的最简单方法：

```bash
npx @wonderwhy-er/desktop-commander@latest remove
```

此自动卸载程序将：
- ✅ 从 Claude 的 MCP 服务器配置中移除 Desktop Commander
- ✅ 在更改前备份你的 Claude 配置
- ✅ 提供完整包移除的指导
- ✅ 如果出现问题可从备份恢复

#### 🔧 手动卸载

如果自动卸载失败或你更喜欢手动移除：

##### 从 Claude 配置中移除

1. **找到你的 Claude Desktop 配置文件：**
  - **macOS:** `~/Library/Application Support/Claude/claude_desktop_config.json`
  - **Windows:** `%APPDATA%\Claude\claude_desktop_config.json`
  - **Linux:** `~/.config/Claude/claude_desktop_config.json`

2. **编辑配置文件：**
  - 在文本编辑器中打开文件
  - 找到并移除 `"mcpServers"` 部分中的 `"desktop-commander"` 条目
  - 保存文件

  **示例 - 移除此部分：**
  ```json
  {
      "desktop-commander": {
        "command": "npx",
        "args": ["@wonderwhy-er/desktop-commander@latest"]
      }
  }
  ```

关闭并重启 Claude Desktop 以完成移除。

#### 🆘 故障排除

**如果自动卸载失败：**
- 使用手动卸载作为备选方案

**如果在卸载后 Claude 无法启动：**
- 恢复卸载程序创建的备份配置文件
- 或手动修复 claude_desktop_config.json 中的 JSON 语法

**需要帮助？**
- 加入我们的 Discord 社区：https://discord.com/invite/kQ27sNnZr7

## 快速上手

安装 Desktop Commander 并重启 Claude Desktop 后，你就可以大幅提升 Claude 的使用体验了！

### 🚀 新用户引导

Desktop Commander 包含智能引导功能，帮助你探索可能性的边界：

**对于新用户：** 当你刚开始使用（成功执行少于 10 条命令）时，Claude 会在你成功使用 Desktop Commander 后自动提供实用的入门指导和教程。

**随时请求帮助：** 你可以随时通过以下方式询问引导协助：
- *"帮我开始使用 Desktop Commander"*
- *"展示我 Desktop Commander 示例"* 
- *"Desktop Commander 能做什么？"*

随后 Claude 将向你展示适合初学者的教程和示例，包括：
- 📁 自动整理你的下载文件夹
- 📊 使用 Python 分析 CSV/Excel 文件
- ⚙️ 设置 GitHub Actions CI/CD
- 🔍 探索和理解代码库
- 🤖 运行交互式开发环境

## 使用方法

该服务器提供一系列全面的工具，分为几个类别：

### 可用工具

| 分类 | 工具 | 描述 |
|----------|------|-------------|
| **配置** | `get_config` | 获取完整的服务器配置为 JSON（包含 blockedCommands, defaultShell, allowedDirectories, fileReadLineLimit, fileWriteLineLimit, telemetryEnabled） |
| | `set_config_value` | 通过键设置特定配置值。可用设置：<br>• `blockedCommands`: 无法执行的 shell 命令数组<br>• `defaultShell`: 用于命令的 Shell（例如，bash, zsh, powershell）<br>• `allowedDirectories`: 服务器可访问的文件系统路径数组以进行文件操作（⚠️ 终端命令仍可访问这些目录之外的文件）<br>• `fileReadLineLimit`: 一次读取的最大行数（默认：1000）<br>• `fileWriteLineLimit`: 一次写入的最大行数（默认：50）<br>• `telemetryEnabled`: 启用/禁用遥测数据收集（布尔值） |
| **终端** | `start_process` | 启动程序并智能检测何时准备好接收输入 |
| | `interact_with_process` | 向运行中的程序发送命令并获取响应 |
| | `read_process_output` | 读取运行中进程的输出 |
| | `force_terminate` | 强制终止正在运行的终端会话 |
| | `list_sessions` | 列出所有活动的终端会话 |
| | `list_processes` | 列出所有正在运行的进程的详细信息 |
| | `kill_process` | 通过 PID 终止运行中的进程 |
| **文件系统** | `read_file` | 从本地文件系统、URL、Excel 文件（.xlsx, .xls, .xlsm）和 PDF 中读取内容，支持基于行/页的分页 |
| | `read_multiple_files` | 同时读取多个文件 |
| | `write_file` | 写入文件内容，支持重写或追加模式。支持 Excel 文件（JSON 二维数组格式）。对于 PDF，请使用 `write_pdf` |
| | `write_pdf` | 从 Markdown 创建新 PDF 文件或修改现有 PDF（插入/删除页面）。支持 HTML/CSS 样式和 SVG 图形 |
| | `create_directory` | 创建新目录或确保其存在 |
| | `list_directory` | 获取文件和目录的详细递归列表（支持 depth 参数，默认 depth=2） |
| | `move_file` | 移动或重命名文件和目录 |
| | `start_search` | 开始按文件名或内容模式流式搜索文件（搜索文本文件和 Excel 内容） |
| | `get_more_search_results` | 获取活动搜索的分页结果，支持偏移量 |
| | `stop_search` | 优雅地停止活动搜索 |
| | `list_searches` | 列出所有活动搜索会话 |
| | `get_file_info` | 检索文件或目录的详细元数据（包含 Excel 文件的 sheet 信息） |
| **文本编辑** | `edit_block` | 对文本文件应用精准文本替换，或对 Excel 文件进行基于范围的单元格更新 |
| **分析** | `get_usage_stats` | 获取你自己的使用情况统计信息 |
| | `get_recent_tool_calls` | 获取最近的工具调用历史记录（含参数和输出），用于调试和上下文恢复 |
| | `give_feedback_to_desktop_commander` | 在浏览器中打开反馈表单，向 Desktop Commander 团队提供反馈 |

### 快速示例

**数据分析：**
```
"分析 sales.csv 并显示顶级客户" → Claude 在内存中运行 Python 代码
```

**远程访问：**
```
"SSH 到我的服务器并检查磁盘空间" → Claude 维持 SSH 会话
```

**开发：**
```
"启动 Node.js 并测试此 API" → Claude 运行交互式 Node 会话
```

### 工具使用示例

搜索/替换块格式：
```
filepath.ext
<<<<<<< SEARCH
content to find
=======
new content
>>>>>>> REPLACE
```

示例：
```
src/main.js
<<<<<<< SEARCH
console.log("old message");
=======
console.log("new message");
>>>>>>> REPLACE
```

### 增强的编辑块功能

`edit_block` 工具包含多项增强功能以提高可靠性：

1. **改进的提示词**：工具描述现在强调进行多次小而专注的编辑，而非一次大型更改
2. **模糊搜索回退**：当精确匹配失败时，它会执行模糊搜索并提供详细反馈
3. **字符级差异显示**：使用 `{-已删除-}{+已添加+}` 格式准确显示差异内容
4. **多实例支持**：可通过 `expected_replacements` 参数替换多个实例
5. **全面日志记录**：所有模糊搜索均记录用于分析和调试

当搜索失败时，你将看到关于找到的最接近匹配的详细信息，包括相似度百分比、执行时间和字符差异。所有这些细节都会自动记录，以便后续使用模糊搜索日志工具进行分析。

### Docker 支持

### 🐳 隔离环境用法

Desktop Commander 可在 Docker 容器中运行，以**与你的宿主机系统完全隔离**，为你的计算机提供**零风险**。这非常适合测试、开发或当你需要完全沙盒化时。

### 安装说明

1. **为 Windows/Mac 安装 Docker**
   - 从 [docker.com](https://www.docker.com/products/docker-desktop/) 下载并安装 Docker Desktop

2. **获取 Desktop Commander Docker 配置**
   - 访问：https://hub.docker.com/mcp/server/desktop-commander/manual
   - **选项 A：** 使用提供的终端命令进行自动设置
   - **选项 B：** 点击“Standalone”获取配置 JSON 并手动添加到你的 Claude Desktop 配置中
 ![docker-config.png](screenshots/docker-config.png)

3. **挂载本机文件夹（即将推出）**
   - 说明如何将本地目录挂载到 Docker 容器中的指南将很快提供
   - 这将允许你在保持完全隔离的同时操作文件

### Docker 用法的优势
- **与宿主机系统完全隔离**
- **跨不同机器的一致性环境**
- **易于清理** - 完成后只需移除容器即可
- **非常适合测试新功能或配置**

## URL 支持
- `read_file` 现在可以获取本地文件和 URL 的内容
- 示例：使用 `isUrl: true` 参数的 `read_file` 从网络资源读取
- 处理来自远程源的文本和图片内容
- 图片（本地或来自 URL）在 Claude 的界面中以视觉形式显示，而非作为纯文本
- Claude 可以看到并分析实际图片内容
- URL 请求默认超时时间为 30 秒

## 文件预览界面与 Markdown 编辑器

Desktop Commander 在 Claude Desktop 中包含一个丰富的文件预览组件，可在 AI 处理文件时以可视化方式渲染。

### 支持的文件类型
- **Markdown** — 带有内置编辑器的渲染预览
- **图片** — 内联显示（PNG, JPEG, GIF, WebP 等）
- **代码文件** — 语法高亮的源码视图
- **HTML** — 渲染预览，可切换至源码视图
- **目录** — 交互式树形结构，支持展开/折叠和懒加载
- **PDF, Excel, DOCX** — 原生内容提取与显示

### Markdown 编辑器

在 Claude Desktop 中查看 `.md` 文件时，你可以直接在预览面板内编辑——无需打开单独的应用程序。

**使用方法：**
1. 要求 Claude 读取或创建 markdown 文件
2. 使用 **⤢ Expand** 按钮将文件预览展开至全屏
3. 编辑器在全屏模式下自动激活
4. 使用实时预览切换、复制、撤销和保存控件编辑内容
5. 更改会自动保存到磁盘；折叠后返回内联视图

**编辑器功能：**
- 实时 **编辑/预览切换** — 在原始 markdown 和渲染输出之间切换
- **自动保存** 至磁盘并显示保存状态指示器
- **撤销** 支持以恢复未保存的更改
- **复制** 按钮可获取完整 markdown 源码
- **在编辑器中打开** — 直接从面板启动默认 markdown 应用
- 部分文件感知 —— 当文件仅被部分读取时，加载并合并周围行
- 文本选择上下文 —— 在预览模式下选中文本，AI 可引用你的选择

### 目录浏览器

当 Claude 运行 `list_directory` 时，结果会在预览面板内以交互式文件树形式打开——而不仅仅是原始文本输出。

**功能：**
- **可展开的树形结构** — 文件夹点击即可展开和折叠；顶层内容立即显示
- **懒加载** —— 子文件夹按需加载以保持初始视图快速
- **大型目录处理** —— 包含大量项目的目录会显示 `⚠ click to load all` 按钮，避免界面过载
- **在 Finder/资源管理器中打开** —— 每个文件夹都有一个快捷打开按钮以在你的文件管理器中显示它
- **点击预览** —— 点击树中的任意文件可直接在文件预览面板中打开它
- **返回导航** —— 从树形结构中打开文件后，← Back 按钮可带你返回目录视图

### 其他预览功能
- **展开/折叠** — 在紧凑摘要行和完整面板之间切换
- **在文件夹中打开** - 一键在 Finder/资源管理器中显示文件
- **加载更多行** —— 增量加载部分读取窗口上方或下方的内容
- **文本选择** —— 在任何预览中高亮显示文本；AI 可以看到并引用你的选择

## 模糊搜索日志分析（npm 脚本）

模糊搜索日志系统包含方便的 npm 脚本，用于在 MCP 环境之外分析日志：

```bash
# 查看最近的模糊搜索日志
npm run logs:view -- --count 20

# 分析模式和性能
npm run logs:analyze -- --threshold 0.8

# 将日志导出为 CSV 或 JSON
npm run logs:export -- --format json --output analysis.json

# 清除所有日志（带确认提示）
npm run logs:clear
```

有关这些脚本的详细文档，请参阅 [scripts/README.md](scripts/README.md)。

## 模糊搜索日志

Desktop Commander 在 `edit_block` 工具中包含了全面的模糊搜索操作日志记录。当未找到精确匹配时，系统将执行模糊搜索并记录详细信息以供分析。

### 记录的内容

每次模糊搜索操作都会记录：
- **搜索文本与找到的文本**：你寻找的文本与实际找到的文本对比
- **相似度分数**：匹配的接近程度（0-100%）
- **执行时间**：搜索耗时多久
- **字符差异**：显示确切差异的详细 diff
- **文件元数据**：扩展名、搜索/找到文本长度
- **字符编码**：导致差异的具体字符代码

### 日志位置

日志自动保存至：
- **macOS/Linux**: `~/.claude-server-commander-logs/fuzzy-search.log`
- **Windows**: `%USERPROFILE%\.claude-server-commander-logs\fuzzy-search.log`

### 你将获得的信息

模糊搜索日志可帮助你了解：
1. **精确匹配失败的原因**：常见问题如空格差异、换行符或字符编码问题
2. **性能模式**：搜索复杂度如何影响执行时间
3. **文件类型问题**：哪些文件扩展名经常出现匹配问题
4. **字符编码问题**：导致 diff 的具体字符代码

## 审计日志（Audit Logging）

Desktop Commander 现在包含了所有工具调用的全面日志记录：

### 记录的内容
- 每次工具调用都会记录 timestamp、工具名称和参数（为隐私进行脱敏处理）
- 当日志达到 10MB 时会自动轮转

### 日志位置
日志保存至：
- **macOS/Linux**: `~/.claude-server-commander/claude_tool_call.log`
- **Windows**: `%USERPROFILE%\.claude-server-commander\claude_tool_call.log`

此审计追踪有助于调试、安全监控以及了解 Claude 如何与你的系统交互。

## 处理长时间运行的命令

对于可能需要较长时间的命令：

1. `execute_command` 在超时后返回初始输出结果
2. 命令继续在后台运行
3. 使用带有 PID 的 `read_output` 获取新输出
4. 如需停止，请使用 `force_terminate`

## 配置管理

### ⚠️ 重要安全警告

> **有关全面的安全信息和漏洞报告**：请参阅 [SECURITY.md](SECURITY.md)

1. **已知的安全限制**：目录限制和命令阻止可通过各种方法绕过，包括符号链接、命令替换、绝对路径或代码执行
2. **始终在单独的聊天窗口中更改配置**，与你实际工作的地方分开。如果你遇到文件系统访问限制，Claude 有时会尝试修改配置设置（如 `allowedDirectories`）。
3. **`allowedDirectories` 设置目前仅限制文件操作**，不限制终端命令。终端命令仍可访问允许目录之外的文件。
4. **用于生产环境安全**：请使用 [Docker 安装](#option-6-docker-installation-🐳-⭐-自动更新无需-nodejs)，它提供与宿主机系统的完全隔离。

### 配置工具

你可以使用提供的工具管理服务器配置：

```javascript
// 获取完整配置
get_config({})

// 设置特定配置值
set_config_value({ "key": "defaultShell", "value": "/bin/zsh" })

// 通过单独的调用设置多个配置值
set_config_value({ "key": "defaultShell", "value": "/bin/bash" })
set_config_value({ "key": "allowedDirectories", "value": ["/Users/username/projects"] })
```

配置保存在服务器的 `config.json` 文件中，并在服务器重启之间保持持久化。

#### 理解 `fileWriteLineLimit`（文件写入行数限制）

`fileWriteLineLimit` 设置控制单次 `write_file` 操作可写入的行数（默认：50 行）。此限制出于以下几个重要原因存在：

**为何存在此限制：**
- **AI 在 Token 使用上较为浪费**：与其对文件进行两次小范围编辑，AI 可能会决定重写整个文件。我们试图迫使 AI 以较小的更改进行操作，因为这能节省时间和 Token
- **Claude UX 消息限制**：单条消息内有限制，而点击“继续”实际上并不起作用。我们在此尝试让 AI 以小分块工作，这样当你达到该限制时，多个分块已成功执行，且这些工作不会丢失——只需从最后一个分块重新开始即可

**设置此限制：**
```javascript
// 如果你愿意可以设置为数千
set_config_value({ "key": "fileWriteLineLimit", "value": 1000 })

// 或保持较小值以强制更高效的执行行为
set_config_value({ "key": "fileWriteLineLimit", "value": 25 })
```

**最大值**：你可以设置为数千——技术上没有限制。

**最佳实践：**
- 保持默认值（50）以鼓励高效的 AI 行为并避免 Token 浪费
- 当超过限制时，系统会自动建议分块处理
- 更小的分块意味着当 Claude 达到消息限制时损失的工作更少

### 最佳实践

1. **为配置更改创建专用聊天窗口**：在一个聊天中完成所有配置更改，然后在新聊天中开始实际工作。
2. **谨慎使用空的 `allowedDirectories`**：将其设置为空数组（`[]`）将授予对整个文件系统的文件操作访问权限。
3. **使用具体路径**：不要使用 `/` 这样宽泛的路径，而是指定你想要访问的确切目录。
4. **更改后始终验证配置**：使用 `get_config({})` 确认你的更改已正确应用。

## 命令行选项

Desktop Commander 支持多个命令行选项来自定义行为：

### 禁用引导提示（Onboarding）

默认情况下，Desktop Commander 会向新用户（工具调用少于 10 次的用户）显示有用的引导提示。你可以禁用此行为：

```bash
# 为此会话禁用引导提示
node dist/index.js --no-onboarding

# 或使用 npm 脚本
npm run start:no-onboarding

# 对于 npx 安装，修改你的 claude_desktop_config.json：
{
  "mcpServers": {
    "desktop-commander": {
      "command": "npx",
      "args": [
        "-y",
        "@wonderwhy-er/desktop-commander@latest",
        "--no-onboarding"
      ]
    }
  }
}
```

**引导提示自动禁用的情况：**
- 当 MCP 客户端名称设置为 "desktop-commander" 时
- 使用 `--no-onboarding` 标志时
- 用户已使用过引导提示或进行了 10+ 次工具调用后

**调试信息：**
服务器将记录引导提示何时被禁用：`"Onboarding disabled via --no-onboarding flag"`

## 使用不同的 Shell

你可以指定用于命令执行的 Shell：

```javascript
// 使用默认 Shell（bash 或系统默认）
execute_command({ "command": "echo $SHELL" })

// 专门使用 zsh
execute_command({ "command": "echo $SHELL", "shell": "/bin/zsh" })

// 专门使用 bash
execute_command({ "command": "echo $SHELL", "shell": "/bin/bash" })
```

这允许你使用 Shell 特定功能或在命令之间保持一致的环境。

## 调试指南

如果你需要调试服务器，可以以调试模式安装它：

```bash
# 使用 npx
npx @wonderwhy-er/desktop-commander@latest setup --debug

# 或如果本地已安装
npm run setup:debug
```

这将：
1. 配置 Claude 使用单独的 "desktop-commander" 服务器
2. 启用带有 `--inspect-brk=9229` 标志的 Node.js 调试器协议
3. 在启动时暂停执行，直到调试器连接
4. 启用额外的调试环境变量

要连接调试器：
- 在 Chrome 中，访问 `chrome://inspect` 并查找 Node.js 实例
- 在 VS Code 中，使用 "Attach to Node Process" 调试配置
- 其他 IDE/工具可能有类似的 Node.js 调试“附加”选项

重要调试说明：
- 服务器将在启动时暂停（由于 `--inspect-brk` 标志），直到调试器连接
- 如果在调试期间未看到活动，请确保你已连接到正确的 Node.js 进程
- 可能运行着多个 Node 进程；请连接到端口 9229 上的那个
- 调试服务器在 Claude 的 MCP 服务器列表中标识为 "desktop-commander-debug"

故障排除：
- 如果 Claude 在使用调试服务器时超时，可能是你的调试器未正确连接
- 当正确连接时，进程将在命中第一个断点后继续执行
- 连接后你可以在 IDE 中添加额外的断点

## 模型上下文协议（MCP）集成

本项目扩展了 MCP Filesystem Server 以启用：
- Claude Desktop 中的本地服务器支持
- 完整的系统命令执行
- 进程管理
- 文件操作
- 带有搜索/替换块的代码编辑

作为探索 Claude MCPs 的一部分创建：https://youtube.com/live/TlbjFDbl5Us

## 支持 Desktop Commander

<div align="center">
  <h3>📢 支持此项目</h3>
  <p><strong>Desktop Commander MCP 是免费且开源的，但需要你的支持才能蓬勃发展！</strong></p>
  
  <div style="background-color: #f8f9fa; padding: 15px; border-radius: 10px; margin: 20px 0; border: 2px solid #007bff;">
    <p>我们的理念很简单：如果你没有成功，我们不想让你为此付费。但如果 Desktop Commander 对你的成功有所贡献，请考虑为它提供支持。</p>
    <p><strong>支持方式：</strong></p>
    <ul style="list-style-type: none; padding: 0;">
      <li>🌟 <a href="https://github.com/sponsors/wonderwhy-er"><strong>GitHub Sponsors</strong></a> - 定期支持</li>
      <li>☕ <a href="https://www.buymeacoffee.com/wonderwhyer"><strong>Buy Me A Coffee</strong></a> - 一次性贡献</li>
      <li>💖 <a href="https://www.patreon.com/c/EduardsRuzga"><strong>Patreon</strong></a> - 成为赞助人并每月支持我们</li>
      <li>⭐ <a href="https://github.com/wonderwhy-er/DesktopCommanderMCP"><strong>在 GitHub 上 Star</strong></a> - 帮助他人发现此项目</li>
    </ul>
  </div>
</div>


### ❤️ 支持者名人堂

慷慨的支持者在此展示。感谢你让这个项目成为可能！

<div align="center">
<table>
  <tr>
    <td align="center">
      <a href="https://github.com/jonrichards">
        <img src="https://github.com/jonrichards.png" width="100px;" alt="Jon Richards"/>
        <br />
        <sub><b>Jon Richards</b></sub>
      </a>
    </td>
    <td align="center">
      <a href="https://github.com/stepanic">
        <img src="https://github.com/stepanic.png" width="100px;" alt="Matija Stepanic"/>
        <br />
        <sub><b>Matija Stepanic</b></sub>
      </a>
    </td>
  </tr>
</table>
</div>

<details>
  <summary><strong>为何你的支持至关重要</strong></summary>
  <p>你的支持使我们能够：</p>
  <ul>
    <li>继续积极开发和维护</li>
    <li>添加新功能和集成</li>
    <li>提高跨平台的兼容性</li>
    <li>提供更好的文档和示例</li>
    <li>围绕项目构建更强大的社区</li>
  </ul>
</details>

## 官方网站

访问我们的官方网站 [https://desktopcommander.app/](https://desktopcommander.app/) 获取最新信息、文档和更新。

## 媒体报道

通过以下资源了解更多关于此项目的信息：

### 文章
[Claude with MCPs replaced Cursor & Windsurf. How did that happen?](https://wonderwhy-er.medium.com/claude-with-mcps-replaced-cursor-windsurf-how-did-that-happen-c1d1e2795e96) - 深入探讨 Claude 与模型上下文协议能力如何改变开发者工作流。

### 视频
[Claude Desktop Commander Video Tutorial](https://www.youtube.com/watch?v=ly3bed99Dy8) - 观看如何设置和有效使用 Commander。

### AnalyticsIndiaMag 报道
[![analyticsindiamag.png](testemonials%2Fanalyticsindiamag.png)
This Developer Ditched Windsurf, Cursor Using Claude with MCPs](https://analyticsindiamag.com/ai-features/this-developer-ditched-windsurf-cursor-using-claude-with-mcps/)

### 社区
加入我们的 [Discord 服务器](https://discord.gg/kQ27sNnZr7) 获取帮助、分享反馈并与其他用户建立联系。

## 用户评价

[![It's a life saver! I paid Claude + Cursor currently which I always feel it's kind of duplicated. This solves the problem ultimately. I am so happy. Thanks so much. Plus today Claude has added the web search support. With this MCP + Internet search, it writes the code with the latest updates. It's so good when Cursor doesn't work sometimes or all the fast requests are used.](https://raw.githubusercontent.com/wonderwhy-er/ClaudeComputerCommander/main/testemonials/img.png) https://www.youtube.com/watch?v=ly3bed99Dy8&lc=UgyyBt6_ShdDX_rIOad4AaABAg
](https://www.youtube.com/watch?v=ly3bed99Dy8&lc=UgyyBt6_ShdDX_rIOad4AaABAg
)

[![This is the first comment I've ever left on a youtube video, THANK YOU! I've been struggling to update an old Flutter app in Cursor from an old pre null-safety version to a current version and implemented null-safety using Claude 3.7. I got most of the way but had critical BLE errors that I spent days trying to resolve with no luck. I tried Augment Code but it didn't get it either. I implemented your MCP in Claude desktop and was able to compare the old and new codebase fully, accounting for the updates in the code, and fix the issues in a couple of hours. A word of advice to people trying this, be sure to stage changes and commit when appropriate to be able to undo unwanted changes. Amazing!](https://raw.githubusercontent.com/wonderwhy-er/ClaudeComputerCommander/main/testemonials/img_1.png)
https://www.youtube.com/watch?v=ly3bed99Dy8&lc=UgztdHvDMqTb9jiqnf54AaABAg](https://www.youtube.com/watch?v=ly3bed99Dy8&lc=UgztdHvDMqTb9jiqnf54AaABAg
)

[![Great! I just used Windsurf, bought license a week ago, for upgrading old fullstack socket project and it works many times good or ok but also many times runs away in cascade and have to revert all changes losing hundereds of cascade tokens. In just a week down to less than 100 tokens and do not want to buy only 300 tokens for 10$. This Claude MCP ,bought claude Pro finally needed but wanted very good reason to also have next to ChatGPT, and now can code as much as I want not worrying about token cost.
Also this is much more than code editing it is much more thank you for great video!](https://raw.githubusercontent.com/wonderwhy-er/ClaudeComputerCommander/main/testemonials/img_2.png)
https://www.youtube.com/watch?v=ly3bed99Dy8&lc=UgyQFTmYLJ4VBwIlmql4AaABAg](https://www.youtube.com/watch?v=ly3bed99Dy8&lc=UgyQFTmYLJ4VBwIlmql4AaABAg)

[![it is a great tool, thank you, I like using it, as it gives claude an ability to do surgical edits, making it more like a human developer.](https://raw.githubusercontent.com/wonderwhy-er/ClaudeComputerCommander/main/testemonials/img_3.png)
https://www.youtube.com/watch?v=ly3bed99Dy8&lc=Ugy4-exy166_Ma7TH-h4AaABAg](https://www.youtube.com/watch?v=ly3bed99Dy8&lc=Ugy4-exy166_Ma7TH-h4AaABAg)

[![You sir are my hero. You've pretty much summed up and described my experiences of late, much better than I could have. Cursor and Windsurf both had me frustrated to the point where I was almost yelling at my computer screen. Out of whimsy, I thought to myself why not just ask Claude directly, and haven't looked back since.
Claude first to keep my sanity in check, then if necessary, engage with other IDEs, frameworks, etc. I thought I was the only one, glad to see I'm not lol.
33
1](https://raw.githubusercontent.com/wonderwhy-er/ClaudeComputerCommander/main/testemonials/img_4.png)
https://medium.com/@pharmx/you-sir-are-my-hero-62cff5836a3e](https://medium.com/@pharmx/you-sir-are-my-hero-62cff5836a3e)

如果你发现这个项目有用，请考虑在 GitHub 上给它一个 ⭐ Star！这有助于他人发现该项目并鼓励进一步开发。

我们欢迎社区的贡献！无论你是发现了 Bug、有功能请求还是想贡献代码，以下是你提供帮助的方式：

- **发现了 Bug？** 在 [github.com/wonderwhy-er/DesktopCommanderMCP/issues](https://github.com/wonderwhy-er/DesktopCommanderMCP/issues) 提交问题
- **有新想法？** 在 issues 部分提交功能请求
- **想贡献代码？** Fork 仓库，创建分支并提交 Pull Request
- **有疑问或讨论？** 在 GitHub Discussions 标签页发起讨论

所有大小贡献都备受感激！

如果你发现此工具对你的工作流非常有价值，请考虑 [支持该项目](https://www.buymeacoffee.com/wonderwhyer)。

## 常见问题解答（FAQ）

以下是常见问题的答案。如需更全面的 FAQ，请参阅我们的[详细 FAQ 文档](FAQ.md)。

### Desktop Commander 是什么？
它是一个 MCP 工具，使 Claude Desktop 能够访问你的文件系统和终端，将 Claude 转变为用于编码、自动化、代码库探索等方面的多功能助手。

### 这与 Cursor/Windsurf 有何不同？
与专注于 IDE 的工具不同，Claude Desktop Commander 提供以解决方案为中心的方法，可与整个操作系统配合使用，而不仅限于编码环境内。Claude 会完整读取文件而非分块处理，可同时跨多个项目工作，并一次性执行更改而无需频繁审查。

### 我需要支付 API 费用吗？
不需要。此工具与 Claude Desktop 的标准 Pro 订阅（$20/月）配合使用，而非通过 API 调用，因此除了订阅费外不会产生额外费用。

### Desktop Commander 会自动更新吗？
是的，当通过 npx 或 Smithery 安装时，Desktop Commander 会在你重启 Claude 时自动更新至最新版本。无需手动更新流程。

### 最常见的用例有哪些？
- 探索和理解复杂的代码库
- 生成图表和文档
- 自动化跨系统的任务
- 同时处理多个项目
- 进行精确控制的精准代码更改

### 我在安装或使用工具时遇到问题，去哪里寻求帮助？
加入我们的 [Discord 服务器](https://discord.gg/kQ27sNnZr7) 获取社区支持，查看 [GitHub issues](https://github.com/wonderwhy-er/DesktopCommanderMCP/issues) 了解已知问题，或查阅[完整 FAQ](FAQ.md) 获取故障排除技巧。你也可以访问我们的[网站 FAQ 部分](https://desktopcommander.app#faq) 获得更友好的体验。如果你遇到新问题，请考虑[提交 GitHub issue](https://github.com/wonderwhy-er/DesktopCommanderMCP/issues/new)，并附上你问题的详细信息。

### 我如何报告安全漏洞？
请在 [GitHub Issue](https://github.com/wonderwhy-er/DesktopCommanderMCP/issues) 中创建包含你所发现任何安全漏洞详细信息的条目。请参阅我们的[安全政策](SECURITY.md)获取负责任披露的完整指南。

## 数据收集与隐私（Data Collection & Privacy）

Desktop Commander 会收集有限的、伪匿名的遥测数据以改进工具。我们不收集文件内容、文件路径或命令参数。

**退出选项：** 要求 Claude “禁用 Desktop Commander 遥测”或在你的配置中设置 `"telemetryEnabled": false`。

完整详情请参阅我们的[隐私政策](PRIVACY.md)。

## 验证（Verifications）
[![Verified on MseeP](https://mseep.ai/badge.svg)](https://mseep.ai/app/25ff7a06-58bc-40b8-bd79-ebb715140f1a)

## 许可证（License）

MIT
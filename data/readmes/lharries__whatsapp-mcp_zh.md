# WhatsApp MCP 服务器

这是一个用于 WhatsApp 的模型上下文协议（Model Context Protocol, MCP）服务器。

借助它，你可以搜索和阅读你的个人 WhatsApp 消息（包括图片、视频、文档和音频消息），搜索联系人并向个人或群组发送消息。你还可以发送媒体文件，包括图片、视频、文档和音频消息。

它通过 WhatsApp Web 多设备 API（使用 [whatsmeow](https://github.com/tulir/whatsmeow) 库）直接连接到你的 **个人 WhatsApp 账号**。所有消息均本地存储在 SQLite 数据库中，仅当代理（agent）通过工具访问时才会发送给大语言模型（LLM，如 Claude）。

以下是连接至 Claude 后可实现的效果示例。

![WhatsApp MCP](./example-use.png)

> 想要获取本项目及其他我参与项目的更新，[在此输入你的邮箱](https://docs.google.com/forms/d/1rTF9wMBTN0vPfzWuQa2BjfGKdKIpTbyeKxhPMcEzgyI/preview)

> *注意：* 与许多 MCP 服务器一样，WhatsApp MCP 也存在[致命三元组（the lethal trifecta）](https://simonwillison.net/2025/Jun/16/the-lethal-trifecta/)的风险。这意味着项目注入可能导致私有数据泄露。

## 安装

### 前置条件

- Go
- Python 3.6+
- Anthropic Claude Desktop 应用（或 Cursor）
- UV（Python 包管理器），安装命令：`curl -LsSf https://astral.sh/uv/install.sh | sh`
- FFmpeg（*可选*） - 仅用于处理音频消息。如果你希望发送可播放的 WhatsApp 语音消息，文件必须是 `.ogg` Opus 格式。安装 FFmpeg 后，MCP 服务器会自动将非 Opus 格式的音频文件进行转换。若未安装 FFmpeg，你仍可使用 `send_file` 工具发送原始音频文件。

### 步骤

1. **克隆本仓库**

   ```bash
   git clone https://github.com/lharries/whatsapp-mcp.git
   cd whatsapp-mcp
   ```

2. **运行 WhatsApp 桥接程序**

   进入 `whatsapp-bridge` 目录并运行该 Go 应用程序：

   ```bash
   cd whatsapp-bridge
   go run main.go
   ```

   首次运行时，系统会提示你扫描二维码。请使用手机上的 WhatsApp 应用扫描该二维码完成验证。

   大约 20 天后，你可能需要重新进行身份验证。

3. **连接至 MCP 服务器**

   复制下方的 JSON 配置，并将 `{{PATH}}` 替换为实际路径：

   ```json
   {
     "mcpServers": {
       "whatsapp": {
         "command": "{{PATH_TO_UV}}", // Run `which uv` and place the output here
         "args": [
           "--directory",
           "{{PATH_TO_SRC}}/whatsapp-mcp/whatsapp-mcp-server", // cd into the repo, run `pwd` and enter the output here + "/whatsapp-mcp-server"
           "run",
           "main.py"
         ]
       }
     }
   }
   ```

   对于 **Claude**，将此文件保存为 `claude_desktop_config.json`，路径位于你的 Claude Desktop 配置目录：

   ```
   ~/Library/Application Support/Claude/claude_desktop_config.json
   ```

   对于 **Cursor**，将此文件保存为 `mcp.json`，路径位于你的 Cursor 配置目录：

   ```
   ~/.cursor/mcp.json
   ```

4. **重启 Claude Desktop / Cursor**

   打开 Claude Desktop，你现在应该能看到 WhatsApp 作为可用集成项。

   或者重启 Cursor。

### Windows 兼容性

如果你在 Windows 上运行此项目，请注意 `go-sqlite3` 需要**启用 CGO** 才能正确编译和运行。默认情况下，Windows 上的 **CGO 是禁用的**，因此你需要手动启用它并安装 C 编译器。

#### 配置步骤：

1. **安装 C 编译器**  
   推荐使用 [MSYS2](https://www.msys2.org/) 为 Windows 安装 C 编译器。安装 MSYS2 后，请确保将 `ucrt64\bin` 文件夹添加到你的系统 `PATH` 环境变量中。  
   → 详细步骤指南可[在此查看](https://code.visualstudio.com/docs/cpp/config-mingw)。

2. **启用 CGO 并运行程序**

   ```bash
   cd whatsapp-bridge
   go env -w CGO_ENABLED=1
   go run main.go
   ```

若未进行此设置，你可能会遇到类似以下错误：

> `Binary was compiled with 'CGO_ENABLED=0', go-sqlite3 requires cgo to work.`

## 架构概览

该应用由两个主要组件组成：

1. **Go WhatsApp 桥接程序**（`whatsapp-bridge/`）：一个连接至 WhatsApp Web API 的 Go 应用程序，负责通过二维码进行身份验证，并将消息历史记录存储在 SQLite 中。它充当了 WhatsApp 与 MCP 服务器之间的桥梁。

2. **Python MCP 服务器**（`whatsapp-mcp-server/`）：一个实现模型上下文协议（Model Context Protocol, MCP）的 Python 服务，为 Claude 提供标准化工具，用于与 WhatsApp 数据交互以及发送/接收消息。

### 数据存储

- 所有消息历史记录均存储在 `whatsapp-bridge/store/` 目录下的 SQLite 数据库中
- 数据库维护着聊天和消息相关的表结构
- 消息已建立索引，便于高效搜索与检索

## 使用方法

连接成功后，你可以通过 Claude 与你的 WhatsApp 联系人进行交互，在 WhatsApp 对话中利用 Claude 的 AI 能力。

### MCP 工具

Claude 可访问以下工具以与 WhatsApp 交互：

- **search_contacts**：按名称或电话号码搜索联系人
- **list_messages**：检索消息（支持可选过滤和上下文）
- **list_chats**：列出可用聊天及元数据
- **get_chat**：获取特定聊天的信息
- **get_direct_chat_by_contact**：查找与特定联系人的单聊会话
- **get_contact_chats**：列出涉及特定联系人的所有会话
- **get_last_interaction**：获取与某联系人的最近一次消息交互
- **get_message_context**：检索特定消息的上下文内容
- **send_message**：向指定的电话号码或群组 JID 发送 WhatsApp 消息
- **send_file**：向指定接收者发送文件（图片、视频、原始音频、文档）
- **send_audio_message**：将音频文件作为 WhatsApp 语音消息发送（需为 .ogg opus 格式，或已安装 ffmpeg）
- **download_media**：下载 WhatsApp 消息中的媒体文件并返回本地路径

### 媒体处理功能

MCP 服务器支持发送和接收多种类型的媒体文件：

#### 发送媒体

你可以向 WhatsApp 联系人发送各类媒体：

- **图片、视频、文档**：使用 `send_file` 工具分享任何支持的媒体类型。
- **语音消息**：使用 `send_audio_message` 工具将音频文件作为可播放的 WhatsApp 语音消息发送。
  - 为确保最佳兼容性，音频文件建议使用 `.ogg` Opus 格式。
  - 安装 FFmpeg 后，系统会自动将其他音频格式（MP3、WAV 等）转换为所需格式。
  - 未安装 FFmpeg 时，你仍可使用 `send_file` 工具发送原始音频文件，但它们不会显示为可播放的语音消息。

#### 下载媒体

默认情况下，本地数据库仅存储媒体文件的元数据。消息会提示已发送媒体。要访问这些媒体文件，你需要使用 `download_media` 工具，传入 `message_id` 和 `chat_jid`（在打印包含媒体的消息时会显示）。该工具会下载媒体并返回文件路径，随后可打开或传递给其他工具。

## 技术细节

1. Claude 向 Python MCP 服务器发送请求
2. MCP 服务器向 Go 桥接程序查询 WhatsApp 数据或直接访问 SQLite 数据库
3. Go 程序调用 WhatsApp API 并保持 SQLite 数据库实时更新
4. 数据沿链路反向传递回 Claude
5. 发送消息时，请求流向为：Claude → MCP 服务器 → Go 桥接程序 → WhatsApp

## 故障排除

- 如果运行 `uv` 时遇到权限问题，可能需要将其添加到系统 PATH，或使用可执行文件的完整路径。
- 确保 Go 应用程序和 Python 服务器均处于运行状态，集成才能正常工作。

### 身份验证问题

- **二维码未显示**：若二维码不出现，请尝试重启身份验证脚本。若问题持续，检查你的终端是否支持渲染二维码。
- **WhatsApp 已登录**：如果你的会话已激活，Go 桥接程序会自动重新连接而无需显示二维码。
- **设备数量已达上限**：WhatsApp 限制了关联设备的数量。若达到上限，你需要在手机端的 WhatsApp 中移除一个现有设备（设置 > 已关联的设备）。
- **消息未加载**：初始验证后，可能需要几分钟才能加载完你的历史记录，尤其是当聊天较多时。
- **WhatsApp 不同步**：如果你的 WhatsApp 消息与桥接程序出现同步异常，请删除两个数据库文件（`whatsapp-bridge/store/messages.db` 和 `whatsapp-bridge/store/whatsapp.db`）并重启桥接程序以重新验证。

如需更多 Claude Desktop 集成排错指南，请参阅 [MCP 官方文档](https://modelcontextprotocol.io/quickstart/server#claude-for-desktop-integration-issues)。该文档包含检查日志和解决常见问题的实用技巧。
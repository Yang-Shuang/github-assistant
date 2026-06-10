<img src="assets/banner.png" alt="XcodeBuild MCP" width="600"/>

一个基于模型上下文协议（Model Context Protocol, MCP）的服务器与命令行工具（CLI），为在 iOS 和 macOS 项目中使用智能体提供相关工具。

[![CI](https://github.com/getsentry/XcodeBuildMCP/actions/workflows/ci.yml/badge.svg)](https://github.com/getsentry/XcodeBuildMCP/actions/workflows/ci.yml)
[![npm version](https://badge.fury.io/js/xcodebuildmcp.svg)](https://badge.fury.io/js/xcodebuildmcp) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) [![Node.js](https://img.shields.io/badge/node->=18.x-brightgreen.svg)](https://nodejs.org/) [![Xcode 16](https://img.shields.io/badge/Xcode-16-blue.svg)](https://developer.apple.com/xcode/) [![macOS](https://img.shields.io/badge/platform-macOS-lightgrey.svg)](https://www.apple.com/macos/) [![MCP](https://img.shields.io/badge/MCP-Compatible-green.svg)](https://modelcontextprotocol.io/) [![Ask DeepWiki](https://deepwiki.com/badge.svg)](https://deepwiki.com/getsentry/XcodeBuildMCP) [![AgentAudit Security](https://img.shields.io/badge/AgentAudit-Safe-brightgreen?logo=data:image/svg%2Bxml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI+PHBhdGggZmlsbD0id2hpdGUiIGQ9Ik0xMiAxTDMgNXY2YzAgNS41NSAzLjg0IDEwLjc0IDkgMTIgNS4xNi0xLjI2IDktNi40NSA5LTEyVjVsLTktNHoiLz48L3N2Zz4=)](https://www.agentaudit.dev/skills/xcodebuildmcp)

## 安装

XcodeBuildMCP 以单一包的形式发布，包含两种模式：**命令行工具（CLI）**用于直接在终端使用，以及 **MCP 服务器**供 AI 编程智能体调用。无论采用哪种安装方式，你都会同时获得这两项功能。

### 方式 A — Homebrew

```bash
brew tap getsentry/xcodebuildmcp
brew install xcodebuildmcp
```

### 方式 B — npm（Node.js 18+）

```bash
npm install -g xcodebuildmcp@latest
```

验证安装是否成功：
```bash
xcodebuildmcp --help
```

### 连接你的 MCP 客户端

你可以在官方文档页面 [MCP Clients](https://xcodebuildmcp.com/docs/clients) 中找到适用于 Cursor、Claude Code 和 Codex 的开箱即用配置片段。大多数客户端也支持通过 `npx -y xcodebuildmcp@latest mcp` 按需运行 MCP 服务器，无需全局安装。

## 系统要求

- macOS 14.5 或更高版本
- Xcode 16.x 或更高版本
- Node.js 18.x 或更高版本（通过 Homebrew 安装时不需要）

## 智能体技能

XcodeBuildMCP 现已包含两个可选的 agent 技能：

- **MCP Skill**：向智能体注入如何使用 MCP 服务器工具的上下文指引（使用 MCP 服务器时可选）。
- **CLI Skill**：向智能体注入如何操作命令行工具的指引（使用 CLI 时推荐启用）。


通过全局安装进行初始化：

```bash
xcodebuildmcp init
```

或通过 npx 直接运行，无需全局安装：

```bash
npx -y xcodebuildmcp@latest init
```

有关安装技能的更多信息，请参阅 [Agent Skills](https://xcodebuildmcp.com/docs/skills)。

## 注意事项

- XcodeBuildMCP 会请求 `xcodebuild` 跳过宏验证，以避免在使用 Swift Macros 的项目构建时出现错误。
- 设备调试工具需要在 Xcode 中配置代码签名。详见 [Device Code Signing](https://xcodebuildmcp.com/docs/device-signing)。

## 隐私说明

XcodeBuildMCP 仅使用 Sentry 收集内部运行时错误遥测数据。如需了解详情或选择退出，请参阅 [Privacy & Telemetry](https://xcodebuildmcp.com/docs/privacy)。

## 命令行工具 (CLI)

XcodeBuildMCP 提供统一的命令行界面。`mcp` 子命令用于启动 MCP 服务器，其余所有命令均可直接在终端中调用工具：

```bash
# Install globally
npm install -g xcodebuildmcp@latest

# Start the MCP server (for MCP clients)
xcodebuildmcp mcp

# List available tools
xcodebuildmcp tools

# Build for simulator
xcodebuildmcp simulator build --scheme MyApp --project-path ./MyApp.xcodeproj
```

检查更新与就地升级：

```bash
xcodebuildmcp upgrade --check
xcodebuildmcp upgrade --yes
```

该 CLI 使用基于工作区的守护进程来处理有状态操作（如日志捕获、调试等），并在需要时自动启动。完整文档请参阅 [CLI guide](https://xcodebuildmcp.com/docs/cli)。

## 相关文档

- Installation: [https://xcodebuildmcp.com/docs/installation](https://xcodebuildmcp.com/docs/installation)
- Setup: [https://xcodebuildmcp.com/docs/setup](https://xcodebuildmcp.com/docs/setup)
- MCP clients: [https://xcodebuildmcp.com/docs/clients](https://xcodebuildmcp.com/docs/clients)
- CLI usage: [https://xcodebuildmcp.com/docs/cli](https://xcodebuildmcp.com/docs/cli)
- Configuration and options: [https://xcodebuildmcp.com/docs/configuration](https://xcodebuildmcp.com/docs/configuration)
- Tools reference: [https://xcodebuildmcp.com/docs/tools](https://xcodebuildmcp.com/docs/tools)
- Troubleshooting: [https://xcodebuildmcp.com/docs/troubleshooting](https://xcodebuildmcp.com/docs/troubleshooting)
- Privacy: [https://xcodebuildmcp.com/docs/privacy](https://xcodebuildmcp.com/docs/privacy)
- Skills: [https://xcodebuildmcp.com/docs/skills](https://xcodebuildmcp.com/docs/skills)
- Contributing: [https://xcodebuildmcp.com/docs/contributing](https://xcodebuildmcp.com/docs/contributing)

## 开源许可

本项目采用 MIT 许可证授权 - 详见 [LICENSE](LICENSE) 文件。
第三方许可声明详见 [THIRD_PARTY_LICENSES](THIRD_PARTY_LICENSES) 文件。
npm 包归属信息详见 [THIRD_PARTY_PACKAGE_LICENSES.md](THIRD_PARTY_PACKAGE_LICENSES.md) 文件。
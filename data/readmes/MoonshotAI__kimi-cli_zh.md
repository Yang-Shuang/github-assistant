# Kimi Code CLI

[![Commit Activity](https://img.shields.io/github/commit-activity/w/MoonshotAI/kimi-cli)](https://github.com/MoonshotAI/kimi-cli/graphs/commit-activity)
[![Checks](https://img.shields.io/github/check-runs/MoonshotAI/kimi-cli/main)](https://github.com/MoonshotAI/kimi-cli/actions)
[![Version](https://img.shields.io/pypi/v/kimi-cli)](https://pypi.org/project/kimi-cli/)
[![Downloads](https://img.shields.io/pypi/dw/kimi-cli)](https://pypistats.org/packages/kimi-cli)
[![Ask DeepWiki](https://deepwiki.com/badge.svg)](https://deepwiki.com/MoonshotAI/kimi-cli)

[Kimi Code](https://www.kimi.com/code/) | [Documentation](https://moonshotai.github.io/kimi-cli/en/) | [文档](https://moonshotai.github.io/kimi-cli/zh/)

> [!IMPORTANT]
> **Kimi Code CLI 正在演变为 [Kimi Code](https://github.com/MoonshotAI/kimi-code)** —— 来自同一团队的全新终端 AI Agent。安装 Kimi Code 会自动迁移你的配置和会话记录。本项目将逐步停止维护；文档及现有安装包仍可供使用。

Kimi Code CLI 是一款在终端运行的 AI Agent，帮助你完成软件开发任务与终端操作。它可以读取和编辑代码、执行 Shell 命令、搜索并获取网页内容，并在运行过程中自主规划与调整操作。

## 快速开始

请参阅 [快速开始](https://moonshotai.github.io/kimi-cli/en/guides/getting-started.html) 了解如何安装并开始使用 Kimi Code CLI。

## 核心功能

### Shell 命令行模式

Kimi Code CLI 不仅是一个编程 Agent，也是一个 Shell。你可以按 `Ctrl-X` 切换到 Shell 命令行模式。在此模式下，无需离开 Kimi Code CLI 即可直接运行 Shell 命令。

![](./docs/media/shell-mode.gif)

> [!NOTE]
> 目前尚不支持 `cd` 等内置 Shell 命令。

### VS Code 扩展

你可以通过 [Kimi Code VS Code Extension](https://marketplace.visualstudio.com/items?itemName=moonshot-ai.kimi-code) 将 Kimi Code CLI 与 [Visual Studio Code](https://code.visualstudio.com/) 集成。

![VS Code Extension](./docs/media/vscode.png)

### 通过 ACP（Agent Client Protocol）实现 IDE 集成

Kimi Code CLI 开箱即用地支持 [Agent Client Protocol]。你可以将其与任何兼容 ACP 的编辑器或 IDE 配合使用。

[Agent Client Protocol]: https://github.com/agentclientprotocol/agent-client-protocol

要在 ACP 客户端中使用 Kimi Code CLI，请确保先在终端运行 Kimi Code CLI 并发送 `/login` 完成登录。随后，你可以配置你的 ACP 客户端以命令 `kimi acp` 启动 Kimi Code CLI 作为 ACP Agent 服务器。

例如，若要在 [Zed](https://zed.dev/) 或 [JetBrains](https://blog.jetbrains.com/ai/2025/12/bring-your-own-ai-agent-to-jetbrains-ides/) 中使用 Kimi Code CLI，请将以下配置添加到你的 `~/.config/zed/settings.json` 或 `~/.jetbrains/acp.json` 文件中：

```json
{
  "agent_servers": {
    "Kimi Code CLI": {
      "type": "custom",
      "command": "kimi",
      "args": ["acp"],
      "env": {}
    }
  }
}
```

随后即可在 IDE 的 Agent 面板中创建 Kimi Code CLI 会话线程。

![](./docs/media/acp-integration.gif)

### Zsh 集成

你可以将 Kimi Code CLI 与 Zsh 结合使用，为你的 Shell 体验注入 AI Agent 能力。

通过以下方式安装 [zsh-kimi-cli](https://github.com/MoonshotAI/zsh-kimi-cli) 插件：

```sh
git clone https://github.com/MoonshotAI/zsh-kimi-cli.git \
  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/kimi-cli
```

> [!NOTE]
> 如果你使用的是 Oh My Zsh 以外的插件管理器，可能需要参考该插件的 README 获取安装说明。

然后在 `~/.zshrc` 中的 Zsh 插件列表里添加 `kimi-cli`：

```sh
plugins=(... kimi-cli)
```

重启 Zsh 后，按 `Ctrl-X` 即可切换到 Agent 模式。

### MCP（Model Context Protocol）支持

Kimi Code CLI 支持 MCP（Model Context Protocol）工具。

**`kimi mcp` 子命令组**

你可以使用 `kimi mcp` 子命令组来管理 MCP 服务器。例如：

```sh
# Add streamable HTTP server:
kimi mcp add --transport http context7 https://mcp.context7.com/mcp --header "CONTEXT7_API_KEY: ctx7sk-your-key"

# Add streamable HTTP server with OAuth authorization:
kimi mcp add --transport http --auth oauth linear https://mcp.linear.app/mcp

# Add stdio server:
kimi mcp add --transport stdio chrome-devtools -- npx chrome-devtools-mcp@latest

# List added MCP servers:
kimi mcp list

# Remove an MCP server:
kimi mcp remove chrome-devtools

# Authorize an MCP server:
kimi mcp auth linear
```

**临时（Ad-hoc）MCP 配置**

Kimi Code CLI 还支持通过 CLI 选项进行临时的 MCP 服务器配置。

假设你有一个符合标准 MCP 格式的配置文件，内容如下：

```json
{
  "mcpServers": {
    "context7": {
      "url": "https://mcp.context7.com/mcp",
      "headers": {
        "CONTEXT7_API_KEY": "YOUR_API_KEY"
      }
    },
    "chrome-devtools": {
      "command": "npx",
      "args": ["-y", "chrome-devtools-mcp@latest"]
    }
  }
}
```

使用 `--mcp-config-file` 选项运行 `kimi`，即可连接到指定的 MCP 服务器：

```sh
kimi --mcp-config-file /path/to/mcp.json
```

### 更多功能

更多功能请参阅[文档](https://moonshotai.github.io/kimi-cli/en/)。

## 开发指南

要参与 Kimi Code CLI 的开发，请运行：

```sh
git clone https://github.com/MoonshotAI/kimi-cli.git
cd kimi-cli

make prepare  # prepare the development environment
```

随后即可开始开发工作。

完成修改后，可参考以下命令：

```sh
uv run kimi  # run Kimi Code CLI

make format  # format code
make check  # run linting and type checking
make test  # run tests
make test-kimi-cli  # run Kimi Code CLI tests only
make test-kosong  # run kosong tests only
make test-pykaos  # run pykaos tests only
make build-web  # build the web UI and sync it into the package (requires Node.js/npm)
make build  # build python packages
make build-bin  # build standalone binary
make help  # show all make targets
```

注意：`make build` 和 `make build-bin` 会自动运行 `make build-web` 以嵌入 Web UI。
<!-- panvimdoc-ignore-start -->

<p align="center">
<a href="https://codecompanion.olimorris.dev"><img src="https://github.com/user-attachments/assets/64da6a69-a54d-4799-b034-59d9efd27b76" alt="CodeCompanion.nvim" /></a>
</p>

<p align="center">
<a href="https://github.com/olimorris/codecompanion.nvim/stargazers"><img src="https://img.shields.io/github/stars/olimorris/codecompanion.nvim?color=c678dd&logoColor=e06c75&style=for-the-badge"></a>
<a href="https://github.com/olimorris/codecompanion.nvim/actions/workflows/ci.yml"><img src="https://img.shields.io/github/actions/workflow/status/olimorris/codecompanion.nvim/ci.yml?branch=main&label=tests&style=for-the-badge"></a>
<a href="https://github.com/olimorris/codecompanion.nvim/releases"><img src="https://img.shields.io/github/v/release/olimorris/codecompanion.nvim?style=for-the-badge"></a>
</p>

<p align="center">一个用于与大型语言模型（LLM）和 AI Agent 进行编程的 Neovim AI 编码助手。内置支持 <a href="https://agentclientprotocol.com">Agent Client Protocol（ACP）</a>、<a href="https://codecompanion.olimorris.dev/model-context-protocol">Model Context Protocol（MCP）</a>，以及 <a href="https://docs.anthropic.com/en/docs/claude-code/overview">Claude Code</a> 和 <a href="https://openai.com/codex">Codex</a> 等 Agent。</p>

<p align="center">新功能公告请始终查看 <a href="https://github.com/olimorris/codecompanion.nvim/discussions/categories/announcements">此处</a></p>

## :purple_heart: Sponsors

感谢以下赞助者：

<p align="center">
<!-- sponsors --><a href="https://github.com/unicell"><img src="https:&#x2F;&#x2F;github.com&#x2F;unicell.png" width="60px" alt="User avatar: Qiu Yu" /></a><a href="https://github.com/jfgordon2"><img src="https:&#x2F;&#x2F;github.com&#x2F;jfgordon2.png" width="60px" alt="User avatar: Jeff Gordon" /></a><a href="https://github.com/JuanCrg90"><img src="https:&#x2F;&#x2F;github.com&#x2F;JuanCrg90.png" width="60px" alt="User avatar: Juan Carlos Ruiz" /></a><a href="https://github.com/Alexander-Garcia"><img src="https:&#x2F;&#x2F;github.com&#x2F;Alexander-Garcia.png" width="60px" alt="User avatar: Alexander Garcia" /></a><a href="https://github.com/LumenYoung"><img src="https:&#x2F;&#x2F;github.com&#x2F;LumenYoung.png" width="60px" alt="User avatar: Lumen Yang" /></a><a href="https://github.com/alzwded"><img src="https:&#x2F;&#x2F;github.com&#x2F;alzwded.png" width="60px" alt="User avatar: Vlad Meșco" /></a><a href="https://github.com/JPFrancoia"><img src="https:&#x2F;&#x2F;github.com&#x2F;JPFrancoia.png" width="60px" alt="User avatar: JPFrancoia" /></a><a href="https://github.com/pixlmint"><img src="https:&#x2F;&#x2F;github.com&#x2F;pixlmint.png" width="60px" alt="User avatar: Christian Gröber" /></a><a href="https://github.com/itskyedo"><img src="https:&#x2F;&#x2F;github.com&#x2F;itskyedo.png" width="60px" alt="User avatar: Kyedo" /></a><a href="https://github.com/jsit"><img src="https:&#x2F;&#x2F;github.com&#x2F;jsit.png" width="60px" alt="User avatar: Jay Sitter" /></a><a href="https://github.com/harrisoncramer"><img src="https:&#x2F;&#x2F;github.com&#x2F;harrisoncramer.png" width="60px" alt="User avatar: Harrison (Harry) Cramer" /></a><!-- sponsors -->
</p>

<p align="center">如果 <i>你</i> 热爱 CodeCompanion 并将其融入工作流中，欢迎考虑 <a href="https://github.com/sponsors/olimorris">赞助我</a></p>

<!-- panvimdoc-ignore-end -->

## :sparkles: Features

- :speech_balloon: [Copilot Chat](https://github.com/features/copilot) 与 [Zed AI](https://zed.dev/blog/zed-ai) 在 Neovim 中的融合体验
- :zap: 将 Neovim 与 CLI 环境下的 LLM 及 Agent 无缝集成
- :electric_plug: 支持 Anthropic、Copilot、GitHub Models、DeepSeek、Gemini、Mistral AI、Novita、Ollama、OpenAI、Azure OpenAI、HuggingFace 和 xAI 的 LLM（或[自行接入](https://codecompanion.olimorris.dev/extending/adapters.html)）
- :robot: 支持 [Agent Client Protocol（ACP）](https://agentclientprotocol.com/overview/introduction)，允许使用 [Augment Code](https://docs.augmentcode.com/cli/overview)、Docker 的 [Cagent](https://github.com/docker/cagent)、[Claude Code](https://docs.anthropic.com/en/docs/claude-code/overview)、[Codex](https://openai.com/codex)、[Copilot CLI](https://github.com/features/copilot/cli)、[Gemini CLI](https://github.com/google-gemini/gemini-cli)、[Goose](https://block.github.io/goose/)、[Cursor CLI](https://cursor.com/docs/cli/overview)、[Kimi CLI](https://github.com/MoonshotAI/kimi-cli)、[Kiro](https://kiro.dev/docs/cli/)、[Mistral Vibe](https://github.com/mistralai/mistral-vibe) 和 [OpenCode](https://opencode.ai) 等 Agent 进行编程
- :heart_hands: 用户贡献并维护的 [adapters（适配器）](https://codecompanion.olimorris.dev/configuration/adapters-http#community-adapters)
- :battery: 支持 [Model Context Protocol（MCP）](https://codecompanion.olimorris.dev/model-context-protocol#model-context-protocol-mcp-support)
- :rocket: [行内转换（Inline transformations）](https://codecompanion.olimorris.dev/usage/inline.html)、代码生成与重构
- :art: 提供 [编辑器上下文（Editor Context）](https://codecompanion.olimorris.dev/usage/chat-buffer/editor-context.html)、[斜杠命令（Slash Commands）](https://codecompanion.olimorris.dev/usage/chat-buffer/slash-commands.html)、[Agent/工具（Agents/Tools）](https://codecompanion.olimorris.dev/usage/chat-buffer/agents-tools) 和 [工作流（Workflows）](https://codecompanion.olimorris.dev/usage/workflows.html)，以优化 LLM 输出效果
- :brain: 支持类如 `CLAUDE.md`、`.cursor/rules` 及自定义的 [rules（规则）文件](https://codecompanion.olimorris.dev/usage/chat-buffer/rules.html)
- :sparkles: 内置 [提示词库（prompt library）](https://codecompanion.olimorris.dev/usage/action-palette.html)，涵盖 LSP 错误建议与代码解释等常见任务
- :building_construction: 支持创建自定义的 [提示词（prompts）](https://codecompanion.olimorris.dev/configuration/prompt-library.html#creating-prompts)、编辑器上下文和斜杠命令
- :books: 支持同时打开多个对话窗口
- :art: 支持将视觉与图片作为输入内容
- :muscle: 采用异步执行机制，性能卓越

<!-- panvimdoc-ignore-start -->

## :camera_flash: In Action

<div align="center">
  <p>
    <h3><a href="https://github.com/user-attachments/assets/aa109f1d-0ec9-4f08-bd9a-df99da03b9a4">聊天缓冲区（Chat Buffer）</a></h3>
    <video controls muted src="https://github.com/user-attachments/assets/3cc83544-2690-49b5-8be6-51e671db52ef"></video>
  </p>
  <p>
    <h3><a href="https://github.com/user-attachments/assets/362b7cfd-e794-4d9c-9a74-90d5e2a87a32">工具 + Agent 工作流</a></h3>
    <video controls muted src="https://github.com/user-attachments/assets/59efa262-e768-4f36-9901-9d02b018fcf0"></video>
  </p>
  <p>
    <h3><a href="https://github.com/user-attachments/assets/dcddcb85-cba0-4017-9723-6e6b7f080fee">行内交互</a></h3>
    <video controls muted src="https://github.com/user-attachments/assets/11a42705-d9de-4eb5-a9ab-c8a2772fb4d4"></video>
  </p>
</div>

<!-- panvimdoc-ignore-end -->

## :rocket: Getting Started

关于 CodeCompanion（安装、配置与使用）的所有内容，请参阅[官方文档](https://codecompanion.olimorris.dev)。

## :toolbox: Troubleshooting

在提交 [Issue](https://github.com/olimorris/codecompanion.nvim/issues) 之前，你可以尝试以下步骤进行故障排查：

**检查健康状态（Checkhealth）**

运行 `:checkhealth codecompanion` 并确认所有依赖项均已正确安装。同时记下日志文件的路径。

**开启日志记录**

更新你的配置文件，并开启调试日志：

```lua
-- lazy.nvim
{
  "olimorris/codecompanion.nvim",
  dependencies = {
    "nvim-lua/plenary.nvim",
    "nvim-treesitter/nvim-treesitter",
  },
  opts = {
    -- NOTE: The log_level is in `opts.opts`
    opts = {
      log_level = "DEBUG", -- or "TRACE"
    },
  },
},

-- Other package managers
require("codecompanion").setup({
  opts = {
    log_level = "DEBUG", -- or "TRACE"
  }
})
```

并根据 `checkhealth` 命令返回的路径查看日志文件。

**使用 `minimal.lua` 文件测试**

在 Neovim 插件中提交的绝大多数问题都与用户自身的配置有关。因此，我在用户提交 Issue 时总是要求他们提供一个 `minimal.lua` 文件。这可以排除因用户自定义配置导致的问题，并让我能够复现该问题。

为此，我在仓库中提供了一个 [minimal.lua](https://github.com/olimorris/codecompanion.nvim/blob/main/minimal.lua) 文件供你在遇到问题时测试。只需复制该文件、编辑后运行 `nvim --clean -u minimal.lua` 即可。

<!-- panvimdoc-ignore-start -->

## :gift: Contributing

我欢迎社区贡献，但具体是否采纳由我决定。在提交 Pull Request（PR）之前，建议先开启 Discussion 交流想法，并请务必阅读 [CONTRIBUTING.md](CONTRIBUTING.md) 指南。

## :clap: Acknowledgements

- [Steven Arcangeli](https://github.com/stevearc)：对聊天缓冲区（chat buffer）的精妙设计以及早期的反馈建议
- [Wtf.nvim](https://github.com/piersolenski/wtf.nvim)：提供的 LSP 助手操作功能
- [CopilotChat.nvim](https://github.com/CopilotC-Nvim/CopilotChat.nvim)：在聊天缓冲区渲染与可用性方面的启发
- [Aerial.nvim](https://github.com/stevearc/aerial.nvim)：Tree-sitter 解析功能，启发了符号斜杠命令（symbols Slash Command）的实现
- [Saghen](https://github.com/Saghen)：基于 [blink.cmp](https://github.com/Saghen/blink.cmp) 的优秀文档设计灵感，以及持续为项目提交的 PR
- [Catwell](https://github.com/catwell)：提供的队列（queue）实现灵感，我借此用于堆叠 Agent 和工具
- [bassamsdata](https://github.com/bassamsdata)：出色的 `insert_edit_into_file` 工具（名单很长）以及对本项目持续的贡献
- [ravitemer](https://github.com/ravitemer)：提供的优秀扩展 API
- [Davidyz](https://github.com/Davidyz)：持续且卓越的贡献，让 CodeCompanion 得以不断演进
- [Conrad Irwin](https://github.com/conradirwin)、[Agus Zubiaga](https://github.com/agu-z) 和来自 [Zed Industries](https://github.com/zed-industries) 的 Morgan Krey：感谢他们在实现 [ACP](https://agentclientprotocol.com) 过程中提供的支持
- [Sidekick.nvim](https://github.com/folke/sidekick.nvim)：在 Diff 显示与终端输入方面的设计灵感

<!-- panvimdoc-ignore-end -->
<!-- HEADER -->
<div align="center">

<br>
<!-- LOGO -->
<img src="https://github.com/user-attachments/assets/aced1e8e-e6be-485a-9015-b822d01ab064" alt="Awesome Opencode" />
<br><br>

<!-- TITLE -->
<h1>Awesome OpenCode</h1>

<!-- BADGES -->
<p>
<a href="https://github.com/sindresorhus/awesome"><img src="https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg" height="28" alt="Awesome" /></a>
&nbsp;&nbsp;
<a href="https://github.com/anomalyco/opencode"><img src="https://img.shields.io/github/stars/anomalyco/opencode?style=social" height="28" alt="Opencode Stars" /></a>
</p>

<br>

<!-- DESCRIPTION -->
<h3>一份为 <a href="https://opencode.ai/">OpenCode</a> 精心整理的插件、主题、Agent 和资源列表。</h3>
<h3>由 <a href="https://github.com/anomalyco">Anomaly</a> 团队打造的终端 AI 编程 Agent。</h3>

<br>

[**官方**](#official) • [**插件**](#plugins) • [**主题**](#themes) • [**Agent**](#agents) • [**项目**](#projects) • [**资源**](#resources)

<br>
<hr>

</div>

<!-- CONTENT -->

<div id="official"></div>

<h3>⭐️ 官方仓库</h3>

| Project | Stars | Description |
| :--- | :--- | :--- |
| **[opencode](https://github.com/anomalyco/opencode)** | ![Stars](https://badgen.net/github/stars/anomalyco/opencode) | OpenCode 官方 AI 编程 Agent。 |
| **[opencode-sdk-js](https://github.com/anomalyco/opencode-sdk-js)** | ![Stars](https://badgen.net/github/stars/anomalyco/opencode-sdk-js) | OpenCode 官方 JavaScript/TypeScript SDK。 |
| **[opencode-sdk-go](https://github.com/anomalyco/opencode-sdk-go)** | ![Stars](https://badgen.net/github/stars/anomalyco/opencode-sdk-go) | OpenCode 官方 Go SDK。 |
| **[opencode-sdk-python](https://github.com/anomalyco/opencode-sdk-python)** | ![Stars](https://badgen.net/github/stars/anomalyco/opencode-sdk-python) | OpenCode 官方 Python SDK。 |

<br>

<div id="plugins"></div>

<details open>
<summary><strong>🧩 插件</strong></summary>
<br>

<details>
  <summary><b>Agent Identity</b> <img src="https://badgen.net/github/stars/gotgenes/opencode-agent-identity" height="14"/> - <i>用于多 Agent 会话的 Agent 自我身份识别与逐条消息归属标注</i></summary>
  <blockquote>
    两个提升 Agent 身份感知能力的插件。AgentSelfIdentityPlugin 将一行提示注入系统 Prompt，使模型知晓当前运行的 Agent 身份。AgentAttributionToolPlugin 通过 SDK 暴露一个工具，用于查询逐条消息的 Agent 归属信息，适用于需要审查多 Agent 会话的场景。
    <br><br>
    <a href="https://github.com/gotgenes/opencode-agent-identity">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Agent Memory</b> <img src="https://badgen.net/github/stars/joshuadavidthomas/opencode-agent-memory" height="14"/> - <i>受 Letta 启发的记忆机制</i></summary>
  <blockquote>
    为 Agent 提供持久化、可自我编辑的记忆块，灵感来源于 Letta Agent。
    <br><br>
    <a href="https://github.com/joshuadavidthomas/opencode-agent-memory">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Agent Skills (JDT)</b> <img src="https://badgen.net/github/stars/joshuadavidthomas/opencode-agent-skills" height="14"/> - <i>动态技能加载器</i></summary>
  <blockquote>
    动态技能加载器，可从项目目录、用户目录和插件目录中自动发现并加载技能。
    <br><br>
    <a href="https://github.com/joshuadavidthomas/opencode-agent-skills">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Antigravity Auth</b> <img src="https://badgen.net/github/stars/NoeFabris/opencode-antigravity-auth" height="14"/> - <i>Google Antigravity 模型支持</i></summary>
  <blockquote>
    通过 Google Antigravity IDE 认证免费使用 Gemini 和 Anthropic 模型。
    <br><br>
    <a href="https://github.com/NoeFabris/opencode-antigravity-auth">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Antigravity Multi-Auth</b> <img src="https://badgen.net/github/stars/theblazehen/opencode-antigravity-multi-auth" height="14"/> - <i>多 Google 账号支持</i></summary>
  <blockquote>
    opencode-antigravity-auth 的分支版本，支持同时使用多个 Google 账号，并在触发速率限制时自动轮换。
    <br><br>
    <a href="https://github.com/theblazehen/opencode-antigravity-multi-auth">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Background</b> <img src="https://badgen.net/github/stars/zenobi-us/opencode-background" height="14"/> - <i>后台进程管理</i></summary>
  <blockquote>
    OpenCode 的后台进程管理插件。
    <br><br>
    <a href="https://github.com/zenobi-us/opencode-background">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Background Agents</b> <img src="https://badgen.net/github/stars/kdcokenny/opencode-background-agents" height="14"/> - <i>异步 Agent 委托</i></summary>
  <blockquote>
    Claude Code 风格的后台 Agent，支持异步委托与上下文持久化。
    <br><br>
    <a href="https://github.com/kdcokenny/opencode-background-agents">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Beads Plugin</b> <img src="https://badgen.net/github/stars/joshuadavidthomas/opencode-beads" height="14"/> - <i>Beads 问题追踪器集成</i></summary>
  <blockquote>
    集成 Steve Yegge 的 beads 问题追踪器，提供 /bd-* 命令支持。
    <br><br>
    <a href="https://github.com/joshuadavidthomas/opencode-beads">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>CC Safety Net</b> <img src="https://badgen.net/github/stars/kenryu42/claude-code-safety-net" height="14"/> - <i>安全网：拦截破坏性操作</i></summary>
  <blockquote>
    Claude Code 插件，充当安全网角色，在执行前拦截破坏性的 git 和文件系统命令。
    <br><br>
    <a href="https://github.com/kenryu42/claude-code-safety-net">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Context Analysis</b> <img src="https://badgen.net/github/stars/IgorWarzocha/Opencode-Context-Analysis-Plugin" height="14"/> - <i>Token 使用分析</i></summary>
  <blockquote>
    OpenCode 插件，为你的 AI 会话提供详细的 Token 用量分析。
    <br><br>
    <a href="https://github.com/IgorWarzocha/Opencode-Context-Analysis-Plugin">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Devcontainers</b> <img src="https://badgen.net/github/stars/athal7/opencode-devcontainers" height="14"/> - <i>多分支 devcontainer 支持</i></summary>
  <blockquote>
    支持运行多个 devcontainer 实例的插件，自动分配端口并实现基于分支的隔离。
    <br><br>
    <a href="https://github.com/athal7/opencode-devcontainers">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Direnv</b> <img src="https://badgen.net/github/stars/simonwjackson/opencode-direnv" height="14"/> - <i>加载 direnv 环境变量</i></summary>
  <blockquote>
    在会话启动时自动加载 direnv 环境变量。非常适合搭配 Nix flakes 使用。
    <br><br>
    <a href="https://github.com/simonwjackson/opencode-direnv">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Dynamic Context Pruning</b> <img src="https://badgen.net/github/stars/Tarquinen/opencode-dynamic-context-pruning" height="14"/> - <i>优化 Token 使用量</i></summary>
  <blockquote>
    通过修剪对话上下文中过期的工具输出结果，优化 Token 使用的插件。
    <br><br>
    <a href="https://github.com/Tarquinen/opencode-dynamic-context-pruning">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Envsitter Guard</b> <img src="https://badgen.net/github/stars/boxpositron/envsitter-guard" height="14"/> - <i>防止 .env 文件泄露</i></summary>
  <blockquote>
    OpenCode 插件，阻止 Agent/工具读取或编辑敏感的 .env* 文件，同时允许通过 EnvSitter 进行安全检查（仅显示键名与确定性指纹，绝不暴露具体值）。
    <br><br>
    <a href="https://github.com/boxpositron/envsitter-guard">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Froggy</b> <img src="https://badgen.net/github/stars/smartfrog/opencode-froggy" height="14"/> - <i>Hooks 与专用 Agent</i></summary>
  <blockquote>
    提供 Claude Code 风格的 Hooks、专用 Agent 以及 gitingest 等工具的插件。
    <br><br>
    <a href="https://github.com/smartfrog/opencode-froggy">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Gemini Auth</b> <img src="https://badgen.net/github/stars/jenslys/opencode-gemini-auth" height="14"/> - <i>Google 账号认证</i></summary>
  <blockquote>
    为你的 Google 账号进行 OpenCode CLI 认证，以便使用现有的 Gemini 订阅计划。
    <br><br>
    <a href="https://github.com/jenslys/opencode-gemini-auth">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Google AI Search</b> <img src="https://badgen.net/github/stars/IgorWarzocha/Opencode-Google-AI-Search-Plugin" height="14"/> - <i>查询 Google AI Mode (SGE)</i></summary>
  <blockquote>
    OpenCode 插件，提供原生工具以调用 Google AI Mode (SGE) 进行搜索查询。
    <br><br>
    <a href="https://github.com/IgorWarzocha/Opencode-Google-AI-Search-Plugin">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Handoff</b> <img src="https://badgen.net/github/stars/joshuadavidthomas/opencode-handoff" height="14"/> - <i>会话交接提示词</i></summary>
  <blockquote>
    生成聚焦的交接提示词，以便在新会话中继续之前的工作。
    <br><br>
    <a href="https://github.com/joshuadavidthomas/opencode-handoff">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Kilo Gateway Auth</b> <img src="https://badgen.net/github/stars/JungHoonGhae/opencode-kilo-auth" height="14"/> - <i>Kilo Gateway 提供商支持</i></summary>
  <blockquote>
    为 OpenCode 添加 Kilo Gateway 提供商支持。
    <br><br>
    <a href="https://github.com/JungHoonGhae/opencode-kilo-auth">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Micode</b> <img src="https://badgen.net/github/stars/vtemian/micode" height="14"/> - <i>头脑风暴-规划-实施工作流</i></summary>
  <blockquote>
    结构化工作流，具备会话连续性、子 Agent 编排、git worktree 隔离以及 AST 感知工具等功能。
    <br><br>
    <a href="https://github.com/vtemian/micode">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Model Announcer</b> <img src="https://badgen.net/github/stars/ramarivera/opencode-model-announcer" height="14"/> - <i>模型自我认知</i></summary>
  <blockquote>
    自动将当前模型名称注入聊天上下文，使 LLM 具备自我认知能力。
    <br><br>
    <a href="https://github.com/ramarivera/opencode-model-announcer">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Morph Fast Apply</b> <img src="https://badgen.net/github/stars/JRedeker/opencode-morph-fast-apply" height="14"/> - <i>10,500+ tokens/sec 代码编辑</i></summary>
  <blockquote>
    集成 Morph 的 Fast Apply API，通过延迟编辑标记和统一 diff 输出实现更快的代码编辑。
    <br><br>
    <a href="https://github.com/JRedeker/opencode-morph-fast-apply">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Oh My Opencode</b> <img src="https://badgen.net/github/stars/code-yeongyu/oh-my-opencode" height="14"/> - <i>Agent 与预置工具集</i></summary>
  <blockquote>
    后台 Agent、预置工具（LSP/AST/MCP）、精选 Agent 以及兼容 Claude Code 的层。
    <br><br>
    <a href="https://github.com/code-yeongyu/oh-my-opencode">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Oh My Opencode Slim</b> <img src="https://badgen.net/github/stars/alvinunreal/oh-my-opencode-slim" height="14"/> - <i>轻量级 Agent 编排，降低 Token 消耗</i></summary>
  <blockquote>
    oh-my-opencode 的精简分支，专注于核心 Agent 编排。包含专用子 Agent（Explorer、Oracle、Librarian、Designer 等）、后台任务管理、LSP/AST 工具、用于实时查看 Agent 状态的 tmux 集成以及 MCP Server。经过优化，显著降低 Token 消耗。
    <br><br>
    <a href="https://github.com/alvinunreal/oh-my-opencode-slim">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Omniroute Auth</b> <img src="https://badgen.net/github/stars/Alph4d0g/opencode-omniroute-auth" height="14"/> - <i>Omniroute 认证提供商</i></summary>
  <blockquote>
    连接并自动从你的 Omniroute 实例获取模型。
    <br><br>
    <a href="https://github.com/Alph4d0g/opencode-omniroute-auth">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>open-plan-annotator</b> <img src="https://badgen.net/github/stars/ndom91/open-plan-annotator" height="14"/> - <i>像编辑 Google Docs 一样批注 LLM 规划！</i></summary>
  <blockquote>
    一个完全本地化的 Agent 编程插件，拦截 plan 模式并在浏览器中打开注释 UI。选中文本以删除线、替换、插入或添加评论——随后批准规划或请求修改。
    <br><br>
    <a href="https://github.com/ndom91/open-plan-annotator">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>OpenAI Codex Auth</b> <img src="https://badgen.net/github/stars/numman-ali/opencode-openai-codex-auth" height="14"/> - <i>ChatGPT Plus/Pro OAuth</i></summary>
  <blockquote>
    该插件使 opencode 能够通过 ChatGPT Plus/Pro OAuth 认证使用 OpenAI 的 Codex 后端。
    <br><br>
    <a href="https://github.com/numman-ali/opencode-openai-codex-auth">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>OpenCode Agent Tmux</b> <img src="https://badgen.net/github/stars/AnganSamadder/opencode-agent-tmux" height="14"/> - <i>OpenCode Agent 实时 tmux 面板（自动启动、流式输出与清理）</i></summary>
  <blockquote>
    为 OpenCode 打造的智能 tmux 集成，自动创建面板以流式输出 Agent 结果，支持灵活的布局和多端口设置，并在会话结束时自动清理。
    <br><br>
    <a href="https://github.com/AnganSamadder/opencode-agent-tmux">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Opencode Canvas</b> <img src="https://badgen.net/github/stars/mailshieldai/opencode-canvas" height="14"/> - <i>tmux 分屏中的交互式终端画布</i></summary>
  <blockquote>
    在 tmux 分屏中提供交互式终端画布（日历、文档、航班预订等）。claude-canvas 的 OpenCode 移植版。
    <br><br>
    <a href="https://github.com/mailshieldai/opencode-canvas">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Opencode Ignore</b> <img src="https://badgen.net/github/stars/lgladysz/opencode-ignore" height="14"/> - <i>基于模式忽略文件/目录</i></summary>
  <blockquote>
    根据匹配模式忽略特定目录或文件的插件。
    <br><br>
    <a href="https://github.com/lgladysz/opencode-ignore">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Opencode Mem</b> <img src="https://badgen.net/github/stars/tickernelz/opencode-mem" height="14"/> - <i>基于向量数据库的持久化记忆</i></summary>
  <blockquote>
    面向 AI 编程 Agent 的持久化记忆系统，利用本地向量数据库技术实现跨会话的长期上下文保留。具备双级记忆作用域、Web 界面、自动捕获机制及多提供商 AI 支持。
    <br><br>
    <a href="https://github.com/tickernelz/opencode-mem">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Opencode Notify</b> <img src="https://badgen.net/github/stars/kdcokenny/opencode-notify" height="14"/> - <i>原生操作系统通知</i></summary>
  <blockquote>
    OpenCode 的原生 OS 通知插件，让你随时知晓任务完成状态。
    <br><br>
    <a href="https://github.com/kdcokenny/opencode-notify">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>OpenCode ntfy.sh</b> <img src="https://badgen.net/github/stars/lannuttia/opencode-ntfy.sh" height="14"/> - <i>推送通知：随时随地掌握进展</i></summary>
  <blockquote>
    通过 ntfy.sh 添加推送通知功能的 OpenCode 插件。
    <br><br>
    <a href="https://github.com/lannuttia/opencode-ntfy.sh">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Opencode Quota</b> <img src="https://badgen.net/github/stars/slkiser/opencode-quota" height="14"/> - <i>配额提示与 Token 追踪</i></summary>
  <blockquote>
    通过自动 Toast 提示和斜杠命令，跨不同提供商追踪配额与 Token 使用情况。
    <br><br>
    <a href="https://github.com/slkiser/opencode-quota">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Opencode Roadmap</b> <img src="https://badgen.net/github/stars/IgorWarzocha/Opencode-Roadmap" height="14"/> - <i>战略规划</i></summary>
  <blockquote>
    战略路线图规划与多 Agent 协调插件。提供项目级规划能力。
    <br><br>
    <a href="https://github.com/IgorWarzocha/Opencode-Roadmap">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Opencode Sessions</b> <img src="https://badgen.net/github/stars/malhashemi/opencode-sessions" height="14"/> - <i>会话管理</i></summary>
  <blockquote>
    支持多 Agent 协作的 OpenCode 会话管理插件。
    <br><br>
    <a href="https://github.com/malhashemi/opencode-sessions">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Opencode Skills</b> <img src="https://badgen.net/github/stars/malhashemi/opencode-skills" height="14"/> - <i>管理与组织能力</i></summary>
  <blockquote>
    用于管理和组织 opencode 技能与能力的插件。
    <br><br>
    <a href="https://github.com/malhashemi/opencode-skills">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Opencode Snippets</b> <img src="https://badgen.net/github/stars/JosXa/opencode-snippets" height="14"/> - <i>即时内联文本扩展</i></summary>
  <blockquote>
    为 OpenCode 提供即时内联文本扩展功能。在消息中任意位置输入 #snippet 即可触发转换。通过可组合、支持 Shell 的片段将 DRY 原则引入 Prompt 工程。
    <br><br>
    <a href="https://github.com/JosXa/opencode-snippets">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Opencode Synced</b> <img src="https://badgen.net/github/stars/iHildy/opencode-synced" height="14"/> - <i>跨设备同步配置</i></summary>
  <blockquote>
    支持在不同机器间同步全局 opencode 配置的插件，提供公开/私有可见性选项。
    <br><br>
    <a href="https://github.com/iHildy/opencode-synced">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Opencode Workspace</b> <img src="https://badgen.net/github/stars/kdcokenny/opencode-workspace" height="14"/> - <i>多 Agent 编排</i></summary>
  <blockquote>
    捆绑式多 Agent 编排框架，一次安装包含 16 个组件。
    <br><br>
    <a href="https://github.com/kdcokenny/opencode-workspace">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Opencode Worktree</b> <img src="https://badgen.net/github/stars/kdcokenny/opencode-worktree" height="14"/> - <i>零摩擦 git worktrees</i></summary>
  <blockquote>
    为 OpenCode 打造的零摩擦 git worktrees。自动启动终端、同步文件，并在退出时清理环境。
    <br><br>
    <a href="https://github.com/kdcokenny/opencode-worktree">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>opencode-mystatus</b> <img src="https://badgen.net/github/stars/vbgate/opencode-mystatus" height="14"/> - <i>查看 AI 订阅配额</i></summary>
  <blockquote>
    一条命令查看所有 AI 订阅配额。支持 OpenAI（Plus/Pro/Codex 等）、智谱 AI、Google Antigravity 等。
    <br><br>
    <a href="https://github.com/vbgate/opencode-mystatus">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>opencode-plugin-otel</b> <img src="https://badgen.net/github/stars/DEVtheOPS/opencode-plugin-otel" height="14"/> - <i>OpenTelemetry 遥测导出器，镜像 Claude Code 监控信号</i></summary>
  <blockquote>
    通过 OTLP/gRPC 将 metrics、logs 和 traces 从 opencode 会话导出至任何兼容 OpenTelemetry 的后端（Datadog、Honeycomb、Grafana Cloud 等）。对会话生命周期、Token 用量、成本、工具执行时长及 git commit 进行插桩——完全镜像 Claude Code 的监控信号。
    <br><br>
    <a href="https://github.com/DEVtheOPS/opencode-plugin-otel">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>opencode-snip</b> <img src="https://badgen.net/github/stars/VincentHardouin/opencode-snip" height="14"/> - <i>OpenCode 插件：通过 snip 前缀 Shell 命令，减少 60-90% LLM Token 消耗</i></summary>
  <blockquote>
    自动为支持的 Shell 命令（git、go、cargo、npm、docker 等）添加 snip 前缀，在输出进入 LLM 上下文窗口前进行过滤。
    <br><br>
    <a href="https://github.com/VincentHardouin/opencode-snip">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>OpenHax Codex</b> <img src="https://badgen.net/github/stars/open-hax/codex" height="14"/> - <i>OAuth 认证</i></summary>
  <blockquote>
    面向个人编程助手的 OAuth 认证插件，支持 ChatGPT Plus/Pro 订阅。
    <br><br>
    <a href="https://github.com/open-hax/codex">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Openskills</b> <img src="https://badgen.net/github/stars/numman-ali/openskills" height="14"/> - <i>替代型技能管理器</i></summary>
  <blockquote>
    功能增强的 opencode 替代技能管理插件。
    <br><br>
    <a href="https://github.com/numman-ali/openskills">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>OpenSpec</b> <img src="https://badgen.net/github/stars/Octane0411/opencode-plugin-openspec" height="14"/> - <i>为 OpenSpec 添加架构规划与规范 Agent</i></summary>
  <blockquote>
    集成 OpenSpec 的 OpenCode 插件，提供专门用于软件架构规划与规范的专用 Agent。
    <br><br>
    <a href="https://github.com/Octane0411/opencode-plugin-openspec">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Optimal Model Temps</b> <img src="https://badgen.net/github/stars/Lyapsus/opencode-optimal-model-temps" height="14"/> - <i>最佳采样温度推荐</i></summary>
  <blockquote>
    极简插件，引导特定模型使用其偏好的采样温度。
    <br><br>
    <a href="https://github.com/Lyapsus/opencode-optimal-model-temps">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Pilot</b> <img src="https://badgen.net/github/stars/athal7/opencode-pilot" height="14"/> - <i>自动化守护进程</i></summary>
  <blockquote>
    自动轮询 GitHub Issues 和 Linear Tickets 以获取任务的自动化守护进程。
    <br><br>
    <a href="https://github.com/athal7/opencode-pilot">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Plannotator</b> <img src="https://badgen.net/github/stars/backnotprop/plannotator" height="14"/> - <i>交互式规划审查 UI</i></summary>
  <blockquote>
    支持可视化批注、私密/离线分享以及 Obsidian/Bear 集成的规划审查 UI。
    <br><br>
    <a href="https://github.com/backnotprop/plannotator">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Plugin Template</b> <img src="https://badgen.net/github/stars/zenobi-us/opencode-plugin-template" height="14"/> - <i>CICD 插件构建环境</i></summary>
  <blockquote>
    专注于提供 CICD 设置，包含生成脚本、release please、bun publish、npm trusted publishing 及 mise tasks。
    <br><br>
    <a href="https://github.com/zenobi-us/opencode-plugin-template">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Pocket Universe</b> <img src="https://badgen.net/github/stars/spoons-and-mirrors/pocket-universe" height="14"/> - <i>为主 Agent 打造的子 Agent 驱动微型宇宙</i></summary>
  <blockquote>
    异步 Agent 功能强大但编排往往棘手；它们采用 fire-and-forget 模式，容易遗留任务、丢失上下文并浪费时间和 Token。该插件扩展了原生 opencode 子 Agent 范式，提供闭环、高容错的异步 Agent，阻塞主线程执行。内置三个工具，构建强大的并行子 Agent 通信与协调系统。
    <br><br>
    <a href="https://github.com/spoons-and-mirrors/pocket-universe">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Ralph Wiggum</b> <img src="https://badgen.net/github/stars/Th0rgal/opencode-ralph-wiggum" height="14"/> - <i>自我修正 Agent 循环</i></summary>
  <blockquote>
    基于 Ralph Wiggum 技术的迭代 AI 开发循环，支持具备自我修正能力的 Agent。
    <br><br>
    <a href="https://github.com/Th0rgal/opencode-ralph-wiggum">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Ring a Bell Example</b> - <i>简易终端提示音插件</i></summary>
  <blockquote>
    一个简单的插件，在请求完成后响铃一次。
    <br><br>
    <a href="https://gist.github.com/ahosker/267f375a65378bcb9a867fd9a195db1e">🔗 <b>查看 Gist</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Shell Strategy</b> <img src="https://badgen.net/github/stars/JRedeker/opencode-shell-strategy" height="14"/> - <i>避免交互式 Shell 卡死</i></summary>
  <blockquote>
    指令文件，教导 LLM 如何避免在非 TTY 环境中执行导致挂起的交互式 Shell 命令。
    <br><br>
    <a href="https://github.com/JRedeker/opencode-shell-strategy">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Simple Memory</b> <img src="https://badgen.net/github/stars/cnicolov/opencode-plugin-simple-memory" height="14"/> - <i>基于 Git 的记忆管理</i></summary>
  <blockquote>
    简易插件，用于在 git 仓库内管理记忆，支持团队提交与审查。
    <br><br>
    <a href="https://github.com/cnicolov/opencode-plugin-simple-memory">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Smart Title</b> <img src="https://badgen.net/github/stars/Tarquinen/opencode-smart-title" height="14"/> - <i>自动生成会话标题</i></summary>
  <blockquote>
    利用 AI 自动生成有意义的会话标题。
    <br><br>
    <a href="https://github.com/Tarquinen/opencode-smart-title">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Smart Voice Notify</b> <img src="https://badgen.net/github/stars/MasuRii/opencode-smart-voice-notify" height="14"/> - <i>智能语音通知</i></summary>
  <blockquote>
    集成多 TTS 引擎（ElevenLabs、Edge TTS、SAPI）的智能语音通知插件，配备智能提醒系统。
    <br><br>
    <a href="https://github.com/MasuRii/opencode-smart-voice-notify">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Subtask2</b> <img src="https://badgen.net/github/stars/spoons-and-mirrors/subtask2" height="14"/> - <i>编排系统</i></summary>
  <blockquote>
    将 opencode /commands 扩展为功能强大的编排系统，提供细粒度的流程控制。
    <br><br>
    <a href="https://github.com/spoons-and-mirrors/subtask2">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Swarm Plugin</b> <img src="https://badgen.net/github/stars/joelhooks/opencode-swarm-plugin" height="14"/> - <i>群体智能</i></summary>
  <blockquote>
    支持基于群体智能的 Agent 协调机制的 opencode 插件。
    <br><br>
    <a href="https://github.com/joelhooks/opencode-swarm-plugin">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Tokenscope</b> <img src="https://badgen.net/github/stars/ramtinJ95/opencode-tokenscope" height="14"/> - <i>Token 分析与成本追踪</i></summary>
  <blockquote>
    Tokenscope，为 opencode 会话提供全面的 Token 用量分析与成本追踪工具。
    <br><br>
    <a href="https://github.com/ramtinJ95/opencode-tokenscope">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>UNMOJI</b> - <i>剥离输出中的 Emoji</i></summary>
  <blockquote>
    一个简单的插件，用于从 OpenCode Agent 的输出中移除所有 Emoji。
    <br><br>
    <a href="https://codeberg.org/bastiangx/opencode-unmoji">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Vibe Coding Slack Notifier</b> <img src="https://badgen.net/github/stars/Wangmerlyn/vibe-coding-slack-notifier" height="14"/> - <i>Slack DM 通知：OpenCode 任务完成提醒</i></summary>
  <blockquote>
    兼容 OpenCode 的 Slack 通知插件及工具包，适用于 Codex、OpenCode、Claude Code 和 Gemini 工作流。
    <br><br>
    <a href="https://github.com/Wangmerlyn/vibe-coding-slack-notifier">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>WakaTime</b> <img src="https://badgen.net/github/stars/angristan/opencode-wakatime" height="14"/> - <i>WakaTime 集成</i></summary>
  <blockquote>
    用于追踪 opencode 会话中编程活动的 WakaTime 集成插件。
    <br><br>
    <a href="https://github.com/angristan/opencode-wakatime">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Warcraft Notifications</b> <img src="https://badgen.net/github/stars/pantheon-org/opencode-warcraft-notifications" height="14"/> - <i>趣味音效通知</i></summary>
  <blockquote>
    为 opencode 完成提醒提供魔兽争霸风格音效的通知插件。
    <br><br>
    <a href="https://github.com/pantheon-org/opencode-warcraft-notifications">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>With Context MCP</b> <img src="https://badgen.net/github/stars/boxpositron/with-context-mcp" height="14"/> - <i>项目专属 Markdown 笔记</i></summary>
  <blockquote>
    MCP Server，用于管理项目专属的 Markdown 笔记，支持模板、批量编辑和忽略模式。
    <br><br>
    <a href="https://github.com/boxpositron/with-context-mcp">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Xquik</b> <img src="https://badgen.net/github/stars/Xquik-dev/x-twitter-scraper" height="14"/> - <i>X/Twitter 数据技能与 MCP Server</i></summary>
  <blockquote>
    X/Twitter 数据技能 —— 包含 MCP Server、REST API 及 20 个提取工具。兼容 Claude Code、Cursor、Codex 等 40+ Agent。
    <br><br>
    <a href="https://github.com/Xquik-dev/x-twitter-scraper">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Zellij Namer</b> <img src="https://badgen.net/github/stars/24601/opencode-zellij-namer" height="14"/> - <i>自动重命名 Zellij 会话</i></summary>
  <blockquote>
    使你的 Zellij 会话名称与当前工作保持同步。
    <br><br>
    <a href="https://github.com/24601/opencode-zellij-namer">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<br>
<a href="https://github.com/awesome-opencode/awesome-opencode/blob/main/contributing.md"><b>➕ 通过 PR 添加插件</b></a>
</details>

<br>

<div id="themes"></div>

<details>
<summary><strong>🎨 主题</strong></summary>
<br>

<details>
  <summary><b>Ayu Dark</b> <img src="https://badgen.net/github/stars/postrednik/opencode-ayu-theme" height="14"/> - <i>流行 Ayu Dark 配色移植版，搭配金色黄色高亮</i></summary>
  <blockquote>
    流行 Ayu Dark 配色的移植版，采用金色黄色作为强调色。
    <br><br>
    <a href="https://github.com/postrednik/opencode-ayu-theme">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Lavi</b> <img src="https://badgen.net/github/stars/b0o/lavi" height="14"/> - <i>适用于 OpenCode 及 15+ 其他应用的柔和甜美配色方案</i></summary>
  <blockquote>
    专为 OpenCode 打造的柔和暗黑主题，富含紫色调并精心调配了语法与 Diff 颜色。属于 Lavi 配色家族的一部分，同时为 Neovim、Alacritty、Ghostty、Kitty、Wezterm、Zellij 等工具提供配套主题，支持 Nix flake 和 home-manager。
    <br><br>
    <a href="https://github.com/b0o/lavi/tree/main/contrib/opencode">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Moonlight</b> <img src="https://badgen.net/github/stars/brunogabriel/opencode-moonlight-theme" height="14"/> - <i>基于流行 moonlight-vscode-theme 的月光主题</i></summary>
  <blockquote>
    一款专为 OpenCode 设计的月光配色主题，源自 atomiks 广受欢迎的 moonlight-vscode-theme。采用受月光美学启发的深色冷色调调色板。
    <br><br>
    <a href="https://github.com/brunogabriel/opencode-moonlight-theme">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Poimandres Theme</b> <img src="https://badgen.net/github/stars/ajaxdude/opencode-ai-poimandres-theme" height="14"/> - <i>Poimantres 主题</i></summary>
  <blockquote>
    OpenCode 的 Poimantres 主题移植版。
    <br><br>
    <a href="https://github.com/ajaxdude/opencode-ai-poimandres-theme">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<br>
<a href="https://github.com/awesome-opencode/awesome-opencode/blob/main/contributing.md"><b>➕ 通过 PR 添加主题</b></a>
</details>

<br>

<div id="agents"></div>

<details>
<summary><strong>🤖 Agent</strong></summary>
<br>

<details>
  <summary><b>Agentic</b> <img src="https://badgen.net/github/stars/Cluster444/agentic" height="14"/> - <i>模块化 AI Agent</i></summary>
  <blockquote>
    面向结构化软件开发、支持模块化的 AI Agent 与命令集，专为 OpenCode 打造。
    <br><br>
    <a href="https://github.com/Cluster444/agentic">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Claude Subagents</b> <img src="https://badgen.net/github/stars/VoltAgent/awesome-claude-code-subagents" height="14"/> - <i>Claude Code 子 Agent</i></summary>
  <blockquote>
    生产级 Claude Code 子 Agent 的综合参考仓库。
    <br><br>
    <a href="https://github.com/VoltAgent/awesome-claude-code-subagents">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Opencode Agents</b> <img src="https://badgen.net/github/stars/darrenhinde/opencode-agents" height="14"/> - <i>增强型工作流</i></summary>
  <blockquote>
    一套包含配置、Prompt、Agent 和插件的 OpenCode 组合，用于提升开发工作流效率。
    <br><br>
    <a href="https://github.com/darrenhinde/opencode-agents">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Redstone</b> <img src="https://badgen.net/github/stars/BackGwa/Redstone" height="14"/> - <i>AI 生成的 Minecraft 插件</i></summary>
  <blockquote>
    一个简化 Minecraft 插件开发与部署的 OpenCode Agent。
    <br><br>
    <a href="https://github.com/BackGwa/Redstone">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<br>
<a href="https://github.com/awesome-opencode/awesome-opencode/blob/main/contributing.md"><b>➕ 通过 PR 添加 Agent</b></a>
</details>

<br>

<div id="projects"></div>

<details>
<summary><strong>🛠 项目</strong></summary>
<br>

<details>
  <summary><b>Agent of Empires</b> <img src="https://badgen.net/github/stars/njbrake/agent-of-empires" height="14"/> - <i>OpenCode 多会话 TUI</i></summary>
  <blockquote>
    用于在 tmux 中管理多个 OpenCode 会话的终端 UI，集成 git worktree 与 Docker 沙箱隔离功能。
    <br><br>
    <a href="https://github.com/njbrake/agent-of-empires">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Beads</b> <img src="https://badgen.net/github/stars/steveyegge/beads" height="14"/> - <i>项目任务管理系统</i></summary>
  <blockquote>
    Steve Yegge 的项目/任务管理系统（附带 beads_viewer UI），专为 Agent 设计。
    <br><br>
    <a href="https://github.com/steveyegge/beads">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>CLI Proxy API</b> <img src="https://badgen.net/github/stars/router-for-me/CLIProxyAPI" height="14"/> - <i>多模型代理网关</i></summary>
  <blockquote>
    提供兼容多个模型 CLI 的 API 接口代理服务。
    <br><br>
    <a href="https://github.com/router-for-me/CLIProxyAPI">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Codex Proxy Server</b> <img src="https://badgen.net/github/stars/unluckyjori/Codex-Proxy-Server" height="14"/> - <i>本地 API 代理</i></summary>
  <blockquote>
    为 Codex/ChatGPT 类模型提供本地 API 代理服务的服务器。
    <br><br>
    <a href="https://github.com/unluckyjori/Codex-Proxy-Server">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Cupcake</b> <img src="https://badgen.net/github/stars/eqtylab/cupcake" height="14"/> - <i>策略执行层</i></summary>
  <blockquote>
    基于 OPA/Rego 构建的 AI 编程 Agent 原生策略层，内置 OpenCode 插件支持。
    <br><br>
    <a href="https://github.com/eqtylab/cupcake">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Gemini CLI to API</b> <img src="https://badgen.net/github/stars/gzzhongqi/geminicli2api" height="14"/> - <i>Gemini 代理服务</i></summary>
  <blockquote>
    将 Gemini CLI 工具转换为兼容 OpenAI 端点的代理服务器。
    <br><br>
    <a href="https://github.com/gzzhongqi/geminicli2api">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>GolemBot</b> <img src="https://badgen.net/github/stars/0xranx/golembot" height="14"/> - <i>统一多编码 Agent CLI 的 AI 助手框架</i></summary>
  <blockquote>
    将 Claude Code、Cursor、OpenCode 和 Codex 封装至单一 API，内置 Skill 系统、IM 频道适配器（飞书/Slack/Telegram/Discord）、集群模式及交互式引导向导。
    <br><br>
    <a href="https://github.com/0xranx/golembot">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Handy</b> <img src="https://badgen.net/github/stars/cjpais/Handy" height="14"/> - <i>语音转文本 (Speech to Text)</i></summary>
  <blockquote>
    简单易用的开源语音转文本工具。
    <br><br>
    <a href="https://github.com/cjpais/Handy">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>hcom</b> <img src="https://badgen.net/github/stars/aannoo/hcom" height="14"/> - <i>让 AI Agent 跨终端互发消息、监控与派生</i></summary>
  <blockquote>
    允许 Claude Code、Gemini CLI、Codex CLI 和 OpenCode Agent 在不同终端中互相通信，检测文件编辑冲突、读取日志、查看终端屏幕、订阅活动以及派生/分叉/恢复 Agent。提供原生插件支持的一等 OpenCode 集成。内置 TUI 仪表盘、跨设备中继、Python API 及多 Agent 工作流脚本。pip 可安装，MIT 开源协议。
    <br><br>
    <a href="https://github.com/aannoo/hcom">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Kimaki</b> <img src="https://badgen.net/github/stars/remorses/kimaki" height="14"/> - <i>Discord 机器人控制器</i></summary>
  <blockquote>
    一款 Discord 机器人，支持通过 Discord 控制任意电脑上的 OpenCode 会话。
    <br><br>
    <a href="https://github.com/remorses/kimaki/">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>MCP Voice Interface</b> <img src="https://badgen.net/github/stars/shantur/mcp-voice-interface" height="14"/> - <i>语音与 AI 助手对话</i></summary>
  <blockquote>
    通过 Web 浏览器使用语音与 AI 助手进行交互。兼容 Claude Desktop 和 OpenCode。
    <br><br>
    <a href="https://github.com/shantur/mcp-voice-interface">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>OC Context (occtx)</b> <img src="https://badgen.net/github/stars/hungthai1401/occtx" height="14"/> - <i>快速切换上下文</i></summary>
  <blockquote>
    用于在 OpenCode 不同上下文间快速切换的命令行工具。
    <br><br>
    <a href="https://github.com/hungthai1401/occtx">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>OC Manager</b> <img src="https://badgen.net/github/stars/kcrommett/oc-manager" height="14"/> - <i>元数据 TUI</i></summary>
  <blockquote>
    终端 UI，用于检查、过滤和清理磁盘上存储的 OpenCode 元数据。
    <br><br>
    <a href="https://github.com/kcrommett/oc-manager">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>OC Monitor Share</b> <img src="https://badgen.net/github/stars/Shlomob/ocmonitor-share" height="14"/> - <i>CLI 监控工具</i></summary>
  <blockquote>
    一款 CLI 工具，用于监控和分析 OpenCode AI 编程使用情况。
    <br><br>
    <a href="https://github.com/Shlomob/ocmonitor-share">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Octto</b> <img src="https://badgen.net/github/stars/vtemian/octto" height="14"/> - <i>AI 头脑风暴交互式浏览器 UI</i></summary>
  <blockquote>
    支持多问题表单、并行探索分支及可视化反馈的 AI 头脑风暴交互式 Web UI。
    <br><br>
    <a href="https://github.com/vtemian/octto">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>OCX</b> <img src="https://badgen.net/github/stars/kdcokenny/ocx" height="14"/> - <i>OpenCode 包管理器</i></summary>
  <blockquote>
    缺失的 OpenCode 扩展包管理器——采用 ShadCN 模型并内置 Ghost Mode。
    <br><br>
    <a href="https://github.com/kdcokenny/ocx">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Open Agent</b> <img src="https://badgen.net/github/stars/Th0rgal/openagent" height="14"/> - <i>自托管控制平面</i></summary>
  <blockquote>
    面向 OpenCode Agent 的自托管控制平面，配备隔离的 Linux 工作区（systemd-nspawn）、基于 Git 的 Library 配置及多平台仪表盘（Next.js Web、SwiftUI iOS）。
    <br><br>
    <a href="https://github.com/Th0rgal/openagent">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Open Dispatch</b> <img src="https://badgen.net/github/stars/bobum/open-dispatch" height="14"/> - <i>通过 Slack 或 Microsoft Teams 控制 OpenCode</i></summary>
  <blockquote>
    连接聊天平台与 AI 编程助手的桥接应用。在桌面端启动会话，在手机端引导执行。支持通过 OpenCode 集成对接 75+ AI 提供商，具备会话持久化与智能消息路由功能。
    <br><br>
    <a href="https://github.com/bobum/open-dispatch">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>OpenChamber</b> <img src="https://badgen.net/github/stars/btriapitsyn/openchamber" height="14"/> - <i>OpenCode GUI</i></summary>
  <blockquote>
    由社区制作的 OpenCode Web 和桌面界面，提供 VS Code 扩展、多会话管理及 git worktree 管理功能。
    <br><br>
    <a href="https://github.com/btriapitsyn/openchamber">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Opencode DDEV</b> <img src="https://badgen.net/github/stars/JUVOJustin/opencode-ddev" height="14"/> - <i>DDEV 容器封装器</i></summary>
  <blockquote>
    将 Bash 命令封装至 DDEV 容器中执行（基于 Docker 的 PHP 开发环境）。
    <br><br>
    <a href="https://github.com/JUVOJustin/opencode-ddev">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Opencode Neovim</b> <img src="https://badgen.net/github/stars/NickvanDyke/opencode.nvim" height="14"/> - <i>Neovim 插件</i></summary>
  <blockquote>
    使编辑器感知 Prompt 更加便捷的 Neovim 插件。
    <br><br>
    <a href="https://github.com/NickvanDyke/opencode.nvim">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Opencode Session Manager</b> <img src="https://badgen.net/github/stars/GNITOAHC/opencode-session" height="14"/> - <i>会话查看器与管理工具</i></summary>
  <blockquote>
    用于查看和管理 OpenCode 会话，并自动检测可删除的孤立会话的工具。
    <br><br>
    <a href="https://github.com/GNITOAHC/opencode-session">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Opencode Sessions</b> <img src="https://badgen.net/github/stars/malhashemi/opencode-sessions" height="14"/> - <i>会话追踪器</i></summary>
  <blockquote>
    用于跟踪和组织 OpenCode 编程会话的管理工具。
    <br><br>
    <a href="https://github.com/malhashemi/opencode-sessions">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Opencode Skills</b> <img src="https://badgen.net/github/stars/malhashemi/opencode-skills" height="14"/> - <i>技能管理系统</i></summary>
  <blockquote>
    用于组织与追踪 OpenCode 能力的技能管理系统。
    <br><br>
    <a href="https://github.com/malhashemi/opencode-skills">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Opencode Telegram Bot</b> <img src="https://badgen.net/github/stars/grinev/opencode-telegram-bot" height="14"/> - <i>OpenCode CLI 的 Telegram 机器人客户端</i></summary>
  <blockquote>
    在本地机器上运行 AI 编程任务，并通过手机进行远程监控与控制。
    <br><br>
    <a href="https://github.com/grinev/opencode-telegram-bot">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Opencode Web</b> <img src="https://badgen.net/github/stars/kcrommett/opencode-web" height="14"/> - <i>浏览器端访问支持</i></summary>
  <blockquote>
    OpenCode 的 Web 界面，提供基于浏览器的 AI 编程 Agent 访问方式。
    <br><br>
    <a href="https://github.com/kcrommett/opencode-web">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>OpenSpec</b> <img src="https://badgen.net/github/stars/Fission-AI/OpenSpec" height="14"/> - <i>规范驱动开发</i></summary>
  <blockquote>
    面向 OpenCode 的规范驱动开发框架——结构化规范管理方案。
    <br><br>
    <a href="https://github.com/Fission-AI/OpenSpec">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>OpenWork</b> <img src="https://badgen.net/github/stars/different-ai/openwork" height="14"/> - <i>OpenCode 工作流桌面 GUI</i></summary>
  <blockquote>
    基于 OpenCode 构建的 Claude Cowork 开源替代方案。提供精美的桌面 UI，支持会话、技能、插件和模板管理。
    <br><br>
    <a href="https://github.com/different-ai/openwork">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Qwen Code OAI Proxy</b> <img src="https://badgen.net/github/stars/aptdnfapt/qwen-code-oai-proxy" height="14"/> - <i>Qwen 模型代理网关</i></summary>
  <blockquote>
    面向 Qwen 模型的 OpenAI 兼容代理服务。
    <br><br>
    <a href="https://github.com/aptdnfapt/qwen-code-oai-proxy">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Tokscale</b> <img src="https://badgen.net/github/stars/junhoyeo/tokscale" height="14"/> - <i>Token 用量追踪 CLI</i></summary>
  <blockquote>
    用于追踪 OpenCode 及其他编程 Agent（Claude Code、Codex、Gemini CLI、Cursor IDE）Token 用量的 CLI 工具。
    <br><br>
    <a href="https://github.com/junhoyeo/tokscale">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Universal LLM API Proxy</b> <img src="https://badgen.net/github/stars/Mirrowel/LLM-API-Key-Proxy" height="14"/> - <i>通用多模型代理与库——由 Opencode 社区共创</i></summary>
  <blockquote>
    通用 LLM 网关：一个 API，接入所有大语言模型。提供 OpenAI/Anthropic 兼容端点、多提供商翻译及智能负载均衡。支持任何自定义 OpenAI/Anthropic 基础 URL 的应用——无需修改现有工具代码。对 Antigravity/Gemini CLI 的支持最为完善。可部署至任意环境。<a href='https://discord.com/channels/1391832426048651334/1449788759917858959'>OpenCode Discord 讨论</a>
    <br><br>
    <a href="https://github.com/Mirrowel/LLM-API-Key-Proxy">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Vibe Kanban</b> <img src="https://badgen.net/github/stars/BloopAI/vibe-kanban" height="14"/> - <i>并行管理 AI 任务</i></summary>
  <blockquote>
    用于并行管理与编排 AI 编程 Agent 的看板工具。
    <br><br>
    <a href="https://github.com/BloopAI/vibe-kanban">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<br>
<a href="https://github.com/awesome-opencode/awesome-opencode/blob/main/contributing.md"><b>➕ 通过 PR 添加项目</b></a>
</details>

<br>

<div id="resources"></div>

<details>
<summary><strong>📚 资源</strong></summary>
<br>

<details>
  <summary><b>Debug Log to Text File</b> - <i>故障排查指南</i></summary>
  <blockquote>
    如何将 OpenCode 调试日志输出到文本文件以供故障排查。
    <br><br>
    <a href="https://github.com/awesome-opencode/awesome-opencode/discussions/19">🔗 <b>查看讨论</b></a>
  </blockquote>
</details>

<details>
  <summary><b>GoTTY</b> <img src="https://badgen.net/github/stars/sorenisanerd/gotty" height="14"/> - <i>将 CLI 转换为 Web 应用</i></summary>
  <blockquote>
    一款简单的命令行工具，可将你的 CLI 工具（如 OpenCode）直接转换为 Web 应用程序。
    <br><br>
    <a href="https://github.com/sorenisanerd/gotty">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<details>
  <summary><b>Opencode Config Starter</b> <img src="https://badgen.net/github/stars/jjmartres/opencode" height="14"/> - <i>灵活的配置起点</i></summary>
  <blockquote>
    一套功能强大的自定义 OpenCode 配置模板，内置 Agent、命令、规则、技能及预配置的 MCP Server。
    <br><br>
    <a href="https://github.com/jjmartres/opencode">🔗 <b>查看仓库</b></a>
  </blockquote>
</details>

<br>
<a href="https://github.com/awesome-opencode/awesome-opencode/blob/main/contributing.md"><b>➕ 通过 PR 添加资源</b></a>
</details>

<br><br>

<div align="center">
<h3>🤝 贡献指南</h3>
发现了 Awesome OpenCode 项目？ <br>
<a href="https://github.com/awesome-opencode/awesome-opencode/blob/main/contributing.md"><b>提交 Pull Request</b></a> 将其添加到列表中！
<br><br>
<sub>遵循 <a href="https://creativecommons.org/publicdomain/zero/1.0/">CC0 1.0 Universal</a> 协议发布。</sub>
</div>
<h1 align="center">
    <a href="https://github.com/pixel-agents-hq/pixel-agents/discussions">
        <img src="webview-ui/public/banner.png" alt="Pixel Agents">
    </a>
</h1>

<h2 align="center" style="padding-bottom: 20px;">
  AI Agent 构建实际成果的游戏化界面
</h2>

<div align="center" style="margin-top: 25px;">

[![version](https://img.shields.io/endpoint?url=https%3A%2F%2Fgist.githubusercontent.com%2Fpablodelucca%2F3cd28398fa4a2c0a636e1d51d41aee39%2Fraw%2Fversion.json)](https://github.com/pixel-agents-hq/pixel-agents/releases)
[![marketplaces](https://img.shields.io/endpoint?url=https%3A%2F%2Fgist.githubusercontent.com%2Fpablodelucca%2F3cd28398fa4a2c0a636e1d51d41aee39%2Fraw%2Finstalls.json)](https://marketplace.visualstudio.com/items?itemName=pablodelucca.pixel-agents)
[![stars](https://img.shields.io/github/stars/pixel-agents-hq/pixel-agents?logo=github&color=0183ff&style=flat)](https://github.com/pixel-agents-hq/pixel-agents/stargazers)
[![license](https://img.shields.io/github/license/pixel-agents-hq/pixel-agents?color=0183ff&style=flat)](https://github.com/pixel-agents-hq/pixel-agents/blob/main/LICENSE)
[![good first issues](https://img.shields.io/github/issues/pixel-agents-hq/pixel-agents/good%20first%20issue?color=7057ff&label=good%20first%20issues)](https://github.com/pixel-agents-hq/pixel-agents/issues?q=is%3Aopen+is%3Aissue+label%3A%22good+first+issue%22)

</div>

<div align="center">
<a href="https://marketplace.visualstudio.com/items?itemName=pablodelucca.pixel-agents">🛒 VS Code 应用市场</a> • <a href="https://github.com/pixel-agents-hq/pixel-agents/discussions">💬 讨论区</a> • <a href="https://github.com/pixel-agents-hq/pixel-agents/issues">🐛 问题反馈</a> • <a href="CONTRIBUTING.md">🤝 贡献指南</a> • <a href="CHANGELOG.md">📋 更新日志</a>
</div>

<br/>

Pixel Agent 将多 Agent AI 系统转化为你可以直观查看和管理的形态。每个 Agent 都会化身像素风办公室中的角色，它们会在办公室里走动、坐在办公桌前，并通过视觉动画实时反映其工作状态——编写代码时表现为打字，搜索文件时表现为阅读，需要你的介入时则处于等待状态。

目前它作为 VS Code 扩展与 Claude Code 配合使用。但我们的愿景是打造一个完全独立于 Agent 和平台的界面，用于编排任意 AI Agent，并可部署在任何地方。

这是免费 VS Code 扩展 **Pixel Agents** 的源代码——你可以从 [VS Code 应用市场](https://marketplace.visualstudio.com/items?itemName=pablodelucca.pixel-agents) 或 [Open VSX](https://open-vsx.org/extension/pablodelucca/pixel-agents) 安装，安装包内已包含完整的家具素材库。

![Pixel Agents screenshot](webview-ui/public/Screenshot.jpg)

## Features（功能特性）

- **一 Agent 一角色** —— 每个 Claude Code 终端都会生成一个专属的动画角色
- **实时活动追踪** —— 角色的动画会根据 Agent 的实际操作（编写、阅读、运行命令）动态变化
- **办公室布局编辑器** —— 使用内置编辑器设计地板、墙壁和家具来打造你的专属空间
- **对话气泡** —— Agent 等待输入或需要权限时显示可视化提示
- **声音通知** —— Agent 完成一轮操作后可选播放提示音
- **子 Agent 可视化** —— Task 工具生成的子 Agent 会作为独立角色出现，并与父级关联
- **布局持久化** —— 你的办公室设计会被保存并在多个 VS Code 窗口间同步共享
- **外部资源目录** —— 可从本机任意文件夹加载自定义或第三方家具素材包
- **多样化角色** —— 提供 6 款风格各异的角色。这些角色基于 [JIK-A-4, Metro City](https://jik-a-4.itch.io/metrocity-free-topdown-character-pack) 的精美作品制作。

<p align="center">
  <img src="webview-ui/public/characters.png" alt="Pixel Agents characters" width="320" height="72" style="image-rendering: pixelated;">
</p>

## Requirements（环境要求）

- VS Code 1.105.0 或更高版本
- [Claude Code CLI](https://docs.anthropic.com/en/docs/claude-code) 已安装并配置完成
- **平台支持**：Windows、Linux 和 macOS

## Getting Started（快速上手）

如果你只想使用 Pixel Agent，最简单的方式是下载该 [VS Code 扩展](https://marketplace.visualstudio.com/items?itemName=pablodelucca.pixel-agents)。如果你想体验源码、进行开发或参与贡献，请继续：

### Install from source（从源码安装）

```bash
git clone https://github.com/pixel-agents-hq/pixel-agents.git
cd pixel-agents
npm install
cd webview-ui && npm install && cd ..
npm run build
```

然后在 VS Code 中按 **F5** 启动扩展调试主机（Extension Development Host）。

### Usage（使用指南）

1. 打开 **Pixel Agent** 面板（它将出现在底部面板区域，与终端并列）
2. 点击 **+ Agent** 启动新的 Claude Code 终端及其对应角色。右键点击可选择使用 `--dangerously-skip-permissions` 参数启动（将跳过所有工具权限审批提示）
3. 开始与 Claude 一起编码——观察角色的实时反应
4. 点击角色进行选中，然后点击座位即可重新分配位置
5. 点击 **Layout** 打开办公室编辑器并自定义你的空间

## Layout Editor（布局编辑器）

内置编辑器让你可以设计自己的办公室：

- **Floor（地板）** —— 支持完整的 HSB 色彩控制
- **Walls（墙壁）** —— 自动平铺的墙壁，支持自定义颜色
- **Tools（工具栏）** —— 选择、绘制、擦除、放置、吸管取色、拾取
- **Undo/Redo（撤销/重做）** —— 支持 50 步操作，快捷键为 Ctrl+Z / Ctrl+Y
- **Export/Import（导出/导入）** —— 通过设置面板将布局保存或分享为 JSON 文件

网格最大可扩展至 64×64 格。点击当前网格外的虚线边框即可扩大范围。

### Office Assets（办公室资源）

所有办公室资源（家具、地板、墙壁）现已**完全开源**，并包含在本仓库的 `webview-ui/public/assets/` 目录下。无需额外购买或导入——开箱即用。

每件家具都位于 `assets/furniture/` 下的独立文件夹中，并附带一个 `manifest.json` 文件用于声明其精灵图（sprites）、旋转组、状态组（开/关）及动画帧。地板瓷砖为 `assets/floors/` 中的单个 PNG 图片，墙壁贴图集则位于 `assets/walls/`。这种模块化结构让你无需修改任何代码即可轻松添加、移除或自定义资源。

要添加新家具，请在 `webview-ui/public/assets/furniture/` 中创建文件夹并放入你的 PNG 精灵图及 `manifest.json`，然后重新构建。资源管理器（`scripts/asset-manager.html`）提供了可视化界面用于创建和编辑清单文件。

若要使用外部目录中的家具，请打开设置并选择 **Add Asset Directory**。完整清单格式及第三方素材包使用方法详见 [docs/external-assets.md](docs/external-assets.md)。

角色设计基于 [JIK-A-4, Metro City](https://jik-a-4.itch.io/metrocity-free-topdown-character-pack) 的杰出作品。

## How It Works（工作原理）

Pixel Agent 会监听 Claude Code 的 JSONL 记录文件，以追踪每个 Agent 的操作状态。当 Agent 调用工具（如编写文件或运行命令）时，扩展会检测到该行为并相应更新角色动画。无需对 Claude Code 进行任何修改——它仅采用纯观测模式工作。

Webview 运行着一个轻量级游戏循环，包含 Canvas 渲染、BFS 寻路算法以及角色状态机（空闲 → 行走 → 打字/阅读）。在整数缩放级别下，所有画面均保持像素级精准。

## Tech Stack（技术栈）

- **Extension（扩展核心）**：TypeScript、VS Code Webview API、esbuild
- **Webview（前端界面）**：React 19、TypeScript、Vite、Canvas 2D

## Known Limitations（已知限制）

- **Agent-terminal sync（Agent 与终端同步问题）** —— Agent 与 Claude Code 终端实例的连接机制并非绝对稳定，偶尔会出现不同步的情况。特别是在快速打开/关闭终端或跨会话恢复时更为明显。
- **Heuristic-based status detection（基于启发式的状态检测）** —— Claude Code 的 JSONL 记录格式并未提供明确的信号来指示 Agent 何时在等待用户输入或已完成一轮操作。当前的检测逻辑依赖于启发式规则（如空闲计时器、回合时长事件），因此容易产生误判——Agent 可能会短暂显示错误的状态，或漏掉某些状态切换。
- **Linux/macOS tip** —— 如果你在不打开文件夹的情况下启动 VS Code（例如直接运行 `code` 命令），Agent 将会从你的主目录开始工作。此功能完全受支持；只需注意，你的 Claude 会话记录将被保存在 `~/.claude/projects/` 下，并以你的主目录作为项目根路径进行追踪。

## Troubleshooting（故障排查）

如果你的 Agent 卡在空闲状态或无法生成：

1. **Debug View** —— 在 Pixel Agent 面板中点击齿轮图标（设置），然后开启 **Debug View**。该模式会显示每个 Agent 的连接诊断信息：JSONL 文件状态、已解析行数、最新数据时间戳及文件路径。若看到 "JSONL not found"，说明扩展无法定位到会话文件。
2. **Debug Console** —— 若你正在从源码运行（通过 F5 启动扩展调试主机），请打开 VS Code 的 **View > Debug Console**。搜索 `[Pixel Agents]` 查看详细日志：项目目录解析、JSONL 轮询状态、路径编码不匹配问题以及无法识别的 JSONL 记录类型。

## Where This Is Going（未来规划）

我们的长期愿景是打造一个管理 AI Agent 如同玩《模拟人生》般直观的界面，但产出的却是实实在在的成果。

- **Agents as characters** —— 你可以直观地查看、分配、监控和重定向每个 Agent，它们拥有可见的角色定位（设计师、程序员、撰稿人、审核员）、属性面板、上下文使用情况及可用工具。
- **Desks as directories** —— 将 Agent 拖拽至办公桌上，即可将其分配给特定项目或工作目录。
- **An office as a project** —— 墙上设有看板（Kanban Board），空闲的 Agent 可自主领取任务。
- **Deep inspection** —— 点击任意 Agent 可查看其使用的模型、代码分支、系统提示词及完整工作历史。支持中断对话、直接沟通或重新分配任务。
- **Token health bars** —— 将速率限制和上下文窗口大小可视化游戏内的属性数值。
- **Fully customizable** —— 支持上传自定义角色精灵图、主题及办公室资源。未来甚至可能突破像素风，迈向 3D 或虚拟现实体验。

为实现这一愿景，架构必须在各个层面保持模块化：

- **Platform-agnostic（跨平台无关）** —— 目前是 VS Code 扩展，未来将支持 Electron 桌面应用、Web 应用或其他任何宿主环境。
- **Agent-agnostic（跨 Agent 无关）** —— 目前适配 Claude Code，但架构设计为通过可组合适配器支持 Codex、OpenCode、Gemini、Cursor、Copilot 等其他工具。
- **Theme-agnostic（主题/皮肤无关）** —— 允许社区成员贡献自定义资源、角色皮肤及界面主题。

我们目前正在积极开发实现这一目标的核心模块与适配器架构。如果你对此感兴趣并希望深入交流，欢迎前往我们的 [Discussions Section](https://github.com/pixel-agents-hq/pixel-agents/discussions)。

## Community & Contributing（社区与贡献）

使用 **[Issues](https://github.com/pixel-agents-hq/pixel-agents/issues)** 提交 Bug 或功能请求。加入 **[Discussions](https://github.com/pixel-agents-hq/pixel-agents/discussions)** 进行交流与提问。

贡献指南详见 [CONTRIBUTING.md](CONTRIBUTING.md)。
参与贡献前请阅读我们的 [Code of Conduct](CODE_OF_CONDUCT.md)。

## Supporting the Project（支持该项目）

如果你觉得 Pixel Agent 有用，欢迎考虑支持其开发：

<a href="https://github.com/sponsors/pablodelucca">
  <img src="https://img.shields.io/badge/Sponsor-GitHub-ea4aaa?logo=github" alt="GitHub Sponsors">
</a>
<a href="https://ko-fi.com/pablodelucca">
  <img src="https://img.shields.io/badge/Support-Ko--fi-ff5e5b?logo=ko-fi" alt="Ko-fi">
</a>

## Star History（⭐ 星标历史）

[![Star History Chart](https://api.star-history.com/svg?repos=pixel-agents-hq/pixel-agents&type=Date)](https://www.star-history.com/?repos=pixel-agents-hq%2Fpixel-agents&type=date&legend=bottom-right)

## License（📜 开源许可）

This project is licensed under the [MIT License](LICENSE).
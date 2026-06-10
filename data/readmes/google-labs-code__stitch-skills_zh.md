# Stitch 设计技能

一套面向 [Google Stitch](https://stitch.withgoogle.com) 的 Agent（智能体）技能与插件集合，遵循 [Agent Skills](https://agentskills.io) 开放标准。兼容 Codex、Antigravity、Gemini CLI、Claude Code 和 Cursor 等编码 Agent。

## 快速开始

### 1. 安装插件（推荐）
全局配置完整 Stitch 插件套件的最快方式。

#### Codex

在 Codex 中，将此仓库添加为插件市场：

| 字段 | 值 |
|---|---|
| Source | `https://github.com/google-labs-code/stitch-skills` |
| Git ref | `main` |
| Sparse paths | 留空，或使用下方路径以缩小检出范围 |

可选的稀疏检出路径：

```text
.agents/plugins
plugins/stitch-design
plugins/stitch-build
plugins/stitch-utilities
```

请勿使用 `plugins/codex`；该路径在此仓库中不存在。

等效的 Codex CLI 命令如下：

```bash
codex plugin marketplace add google-labs-code/stitch-skills --ref main \
  --sparse .agents/plugins \
  --sparse plugins/stitch-design \
  --sparse plugins/stitch-build \
  --sparse plugins/stitch-utilities
```

添加市场后，从 `Stitch Skills` 市场中安装你所需的插件：

- `stitch-design`
- `stitch-build`
- `stitch-utilities`

#### Claude Code

```bash
npx plugins add google-labs-code/stitch-skills --scope project --target claude-code
```

### 2. 按需安装技能
仅选择你需要的特定技能。

> [!IMPORTANT]
> Stitch Design Skills 通常存在相互依赖关系。若选择按需安装技能，请确保包含所有必需的依赖项。

```bash
npx skills add google-labs-code/stitch-skills
```

你可以运行以下命令查看插件和技能的帮助文档：

```bash
npx plugins --help

npx skills --help
```

## 前置条件

这些技能要求你的 Agent 环境中已配置并运行 **Stitch MCP** 服务器。请确保你已按照 [Stitch MCP 设置说明](https://stitch.withgoogle.com/docs/mcp/setup/) 完成服务器注册，并正确设置了相关环境变量与凭据。

## 可用插件

### Design (`stitch-design`)

在 Stitch 中创建、管理和优化设计的核心工作流。

| Skill | Description | Prompt Example |
|---|---|---|
| [stitch::code-to-design](plugins/stitch-design/skills/code-to-design/) | 通过提取 HTML、应用设计系统并上传，将前端代码（React、Vue 等）转换为 Stitch 设计 | *"Upload the frontend code at `/path/to/dashboard` into a Stitch project named 'Dashboard-Migration-2026'."* |
| [stitch::generate-design](plugins/stitch-design/skills/generate-design/) | 根据文本或图片生成新界面，编辑现有界面，并创建设计变体 | · *"Make a browse tab for a mobile app for romance and date night ideas."*<br>· *"Edit the login screen to add a 'Remember Me' checkbox and change the button color to blue."*<br>· *"Generate 3 design variants of the home screen with dark mode and high-density layouts."* |
| [stitch::manage-design-system](plugins/stitch-design/skills/manage-design-system/) | 管理 Stitch 中的设计系统——上传 `DESIGN.md` 并将主题应用到界面 | *"Upload our design system from `.stitch/DESIGN.md` and apply it to all screens."* |
| [stitch::extract-design-md](plugins/stitch-design/skills/extract-design-md/) | 直接从前端源代码中提取完整的 `DESIGN.md` | *"Scan `/src` and extract the design system into `.stitch/DESIGN.md`."* |
| [stitch::extract-static-html](plugins/stitch-design/skills/extract-static-html/) | 从运行的 Web 应用中提取独立静态 HTML，内联 CSS 和图片资源 | *"Extract a static HTML snapshot of `http://localhost:3000/profile`."* |
| [stitch::upload-to-stitch](plugins/stitch-design/skills/upload-to-stitch/) | 将本地资源（图片、原型图、HTML）上传至 Stitch 项目 | *"Upload `.stitch/landing_page.html` to Stitch project `projects/987654321`."* |

---

### Build (`stitch-build`)

从 Stitch 设计生成代码、集成框架及编译资源。

| Skill | Description | Prompt Example |
|---|---|---|
| [react-components](plugins/stitch-build/skills/react-components/) | 将 Stitch 界面转换为 React 组件系统，支持自动验证与设计 Token（令牌）一致性检查 | *"Convert all screens in Stitch project `projects/123` to React components."* |
| [remotion](plugins/stitch-build/skills/remotion/) | 使用 Remotion 从 Stitch 项目中生成演示视频，包含平滑过渡与缩放效果 | *"Generate a walkthrough video of the Stitch project `projects/456`."* |
| [shadcn-ui](plugins/stitch-build/skills/shadcn-ui/) | 提供集成与开发基于 shadcn/ui 组件的应用程序的专家级指导 | *"Set up shadcn/ui and build a data table with sorting and filtering."* |

---

### Utilities (`stitch-utilities`)

辅助工具，用于优化提示词、生成设计规范及强制执行设计标准。

| Skill | Description | Prompt Example |
|---|---|---|
| [design-md](plugins/stitch-utilities/skills/design-md/) | 分析 Stitch 项目并以语义化语言生成全面的 `DESIGN.md` 文件 | *"Analyze Stitch project `projects/123` and generate a DESIGN.md."* |
| [enhance-prompt](plugins/stitch-utilities/skills/enhance-prompt/) | 将模糊的 UI 创意转化为经过打磨、针对 Stitch 优化的提示词，并融入 UI/UX 关键词 | *"Enhance this prompt: 'make a settings page'."* |
| [stitch-loop](plugins/stitch-utilities/skills/stitch-loop/) | 通过单条提示词生成完整的多页网站，并附带自动验证功能 | *"Build a 5-page portfolio website with Stitch."* |
| [taste-design](plugins/stitch-utilities/skills/taste-design/) | 生成 `DESIGN.md` 文件，强制执行高端、非模板化的 UI 标准 | *"Generate a premium DESIGN.md with strict typography and calibrated colors."* |

## 仓库结构

```text
plugins/
├── stitch-design/          — Core design workflow plugin
│   ├── plugin.json
│   └── skills/
│       ├── code-to-design/
│       ├── generate-design/
│       ├── manage-design-system/
│       ├── extract-design-md/
│       ├── extract-static-html/
│       └── upload-to-stitch/
├── stitch-build/           — Code generation & build plugin
│   ├── plugin.json
│   └── skills/
│       ├── react-components/
│       ├── remotion/
│       └── shadcn-ui/
└── stitch-utilities/       — Design utilities & assistants plugin
    ├── plugin.json
    └── skills/
        ├── design-md/
        ├── enhance-prompt/
        ├── stitch-loop/
        └── taste-design/
```

每项技能均遵循 Agent Skills 开放标准：

```text
skills/<skill-name>/
├── SKILL.md           — The "Mission Control" for the agent
├── scripts/           — Executable enforcers (Validation & Networking)
├── resources/         — The knowledge base (Checklists & Style Guides)
└── examples/          — The "Gold Standard" syntactically valid references
```

## 添加新技能

所有新增技能均需遵循上述文件结构，以实现 Agent Skills 开放标准。

### 推荐的新技能方向
* **验证类**：将 Stitch HTML 转换为其他 UI 框架并校验语法的技能。
* **数据解耦**：将静态设计内容转换为外部模拟数据文件的技能。
* **生成设计**：根据给定数据集在 Stitch 中生成新设计界面的技能。

本项目并非 Google 官方支持的产品。该项目不符合 [Google 开源软件漏洞奖励计划](https://bughunters.google.com/open-source-security) 的资格。
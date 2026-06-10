<p>
  <img src="banner.png" alt="visual-explainer" width="1100">
</p>

# visual-explainer

**一项 Agent 技能，将复杂的终端输出转换为你真正想阅读的样式化 HTML 页面。**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](LICENSE)

让你的 Agent 解释系统架构、审查代码差异（diff），或将需求与计划进行对比。它不再使用 ASCII 艺术和字符绘制表格，而是生成一个独立的 HTML 页面并在你的浏览器中打开。

```
> draw a diagram of our authentication flow
> /diff-review
> /plan-review ~/docs/refactor-plan.md
```

https://github.com/user-attachments/assets/55ebc81b-8732-40f6-a4b1-7c3781aa96ec

## 为什么

当你要求生成图表时，每个编程 Agent 默认都会使用 ASCII 艺术。框线字符、等宽字体对齐技巧、文本箭头。这在简单场景下还行，但一旦超过三个框的流程图，就会变成一团无法阅读的乱码。

表格更糟。让 Agent 将 15 个需求与计划进行对比，你会看到一堵由管道符和连字符组成的墙，在终端里换行错乱。数据虽然在那里，但阅读体验极其痛苦。

该技能解决了这些问题。提供专业的排版、深色/浅色主题、支持缩放和平移的交互式 Mermaid 图表。无需构建步骤，除浏览器外无其他依赖。

## Install

| 运行环境 (Harness) | 支持方式 | 安装路径与行为 |
|---|---|---|
| Claude Code | Marketplace plugin | 保留市场插件结构，源码位于 `plugins/visual-explainer/` |
| Pi | Package metadata plus installer | `package.json` 声明了该技能与提示词；`install-pi.sh` 将其安装至 `~/.pi/agent/skills/visual-explainer` 和 `~/.pi/agent/prompts/` |
| Codex CLI | Native skill path plus optional prompts | 复制至 `~/.codex/skills/visual-explainer`；若你的 Codex 版本支持，可选提示词放入 `~/.codex/prompts/` |
| OpenCode/opencode | Observed skill/command paths | 复制至 `~/.config/opencode/skill/visual-explainer`；可选命令放入 `~/.config/opencode/command/` |
| Cursor | Rules-based guidance | 添加提供的 `.mdc` 规则文件；Cursor 不视为原生 Agent Skills 支持 |
| OpenClaw | Lightweight AGENTS/rules guidance | 使用提供的 AGENTS 指引，并配合标准技能目录 |

**Claude Code (marketplace):**
```shell
/plugin marketplace add nicobailon/visual-explainer
/plugin install visual-explainer@visual-explainer-marketplace
```

注意：Claude Code 插件将命令命名空间为 `/visual-explainer:command-name`。

**Pi:**
```bash
pi install git:github.com/nicobailon/visual-explainer
```

或从本地检出版本安装：
```bash
git clone --depth 1 https://github.com/nicobailon/visual-explainer.git
pi install ./visual-explainer
```

包清单声明了标准技能与命令模板：

```json
"pi": {
  "skills": ["./plugins/visual-explainer"],
  "prompts": ["./plugins/visual-explainer/commands"]
}
```

如果你之前使用过旧的 `curl`/手动安装器，请在使用 `pi install` 前删除已复制的文件；否则 Pi 会报告技能与提示词冲突，因为用户级副本会覆盖包资源：

```bash
rm -rf ~/.pi/agent/skills/visual-explainer
rm -f ~/.pi/agent/prompts/{diff-review,fact-check,generate-slides,generate-visual-plan,generate-web-diagram,plan-review,project-recap,share-page}.md
```

如果你更倾向于直接复制文件而非使用包管理，旧版安装器仍然可用：

```bash
curl -fsSL https://raw.githubusercontent.com/nicobailon/visual-explainer/main/install-pi.sh | bash
```

**Codex CLI:**
```bash
git clone --depth 1 https://github.com/nicobailon/visual-explainer.git /tmp/visual-explainer

mkdir -p ~/.codex/skills ~/.codex/prompts
cp -R /tmp/visual-explainer/plugins/visual-explainer ~/.codex/skills/visual-explainer

# Optional, only if your Codex build supports prompt templates:
cp /tmp/visual-explainer/plugins/visual-explainer/commands/*.md ~/.codex/prompts/

rm -rf /tmp/visual-explainer
```

通过调用 `$visual-explainer` 或让 Codex 使用 `visual-explainer` 技能来启动。如果已安装并支持提示词，可使用 `/prompts:diff-review`、`/prompts:plan-review` 等命令。

**OpenCode/opencode:**
```bash
git clone --depth 1 https://github.com/nicobailon/visual-explainer.git /tmp/visual-explainer

mkdir -p ~/.config/opencode/skill ~/.config/opencode/command
cp -R /tmp/visual-explainer/plugins/visual-explainer ~/.config/opencode/skill/visual-explainer

# Optional command templates:
cp /tmp/visual-explainer/plugins/visual-explainer/commands/*.md ~/.config/opencode/command/

rm -rf /tmp/visual-explainer
```

通过让 OpenCode 使用 `visual-explainer` 技能来激活它。命令模板的行为取决于已安装的 OpenCode/opencode 版本。

**Cursor:**

将 `configs/cursor/visual-explainer.mdc` 添加到你的 Cursor 规则中，或将其内容复制到项目规则界面。这是基于规则的指引，用于引导 Cursor 使用标准技能；它不声称支持原生 Agent Skills。

**OpenClaw：**

使用 `configs/openclaw/AGENTS.md` 作为轻量级项目指引，并复制或引用 `plugins/visual-explainer/` 作为标准技能来源。未包含原生 OpenClaw 插件适配器。

## Commands

| Command | What it does |
|---------|-------------|
| `/generate-web-diagram` | Generate an HTML diagram for any topic |
| `/generate-visual-plan` | Generate a visual implementation plan for a feature or extension |
| `/generate-slides` | Generate a magazine-quality slide deck |
| `/diff-review` | Visual diff review with architecture comparison and code review |
| `/plan-review` | Compare a plan against the codebase with risk assessment |
| `/project-recap` | Mental model snapshot for context-switching back to a project |
| `/fact-check` | Verify accuracy of a document against actual code |
| `/share-page` | Deploy an HTML page to Vercel and get a live URL |

当 Agent 准备在终端输出复杂表格（超过 4 行或 3 列）时，它也会自动介入——直接渲染为 HTML 页面。

## Slide Deck Mode

任何生成可滚动页面的命令均支持 `--slides` 参数，用于改为生成幻灯片：

```
/diff-review --slides
/project-recap --slides 2w
```

https://github.com/user-attachments/assets/342d3558-5fcf-4fb2-bc03-f0dd5b9e35dc

## How It Works

```
.claude-plugin/
├── plugin.json           ← marketplace identity
└── marketplace.json      ← plugin catalog
plugins/
└── visual-explainer/
    ├── .claude-plugin/
    │   └── plugin.json   ← plugin manifest
    ├── SKILL.md           ← workflow + design principles
    ├── commands/          ← slash commands
    ├── references/        ← agent reads before generating
    │   ├── css-patterns.md   (layouts, animations, theming)
    │   ├── libraries.md      (Mermaid, Chart.js, fonts)
    │   ├── responsive-nav.md (sticky TOC for multi-section pages)
    │   └── slide-patterns.md (slide engine, transitions, presets)
    ├── templates/         ← reference templates with different palettes
    │   ├── architecture.html
    │   ├── mermaid-flowchart.html
    │   ├── data-table.html
    │   └── slide-deck.html
    └── scripts/
        └── share.sh       ← deploy HTML to Vercel for sharing
```

**输出路径：** `~/.agent/diagrams/filename.html` → 自动在浏览器中打开

该技能会自动路由到合适的渲染方案：流程图与图表使用 Mermaid，架构概览使用 CSS Grid，数据展示使用 HTML 表格，仪表盘使用 Chart.js。

## Limitations

- 生成的 HTML 具备可移植性与独立性，但自动打开功能取决于运行环境、浏览器访问权限及沙盒规则。
- 除非用户指定其他路径，否则所有运行环境均将可视化输出写入 `~/.agent/diagrams/`。
- 切换操作系统主题后，Mermaid SVG 图表需刷新页面才能生效。
- `/share-page` 依赖 `plugins/visual-explainer/scripts/share.sh`，该脚本期望在标准 Pi 技能路径中找到兼容 Pi 的 `vercel-deploy` 技能。其他运行环境仍可生成并打开页面，但分享功能可能需单独安装此依赖。
- 实际效果因模型能力而异。

## Credits

灵感借鉴自 [Anthropic 的 frontend-design skill](https://github.com/anthropics/skills) 与 [interface-design](https://github.com/Dammyjay93/interface-design)。

## License

MIT
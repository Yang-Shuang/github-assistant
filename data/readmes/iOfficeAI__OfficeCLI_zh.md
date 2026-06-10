# OfficeCLI

> **OfficeCLI 是全球首款且最佳的专为 AI Agent（智能体）设计的办公套件。**

**只需一行代码，即可让任何 AI Agent 完全掌控 Word、Excel 和 PowerPoint。**

开源。单文件二进制程序。无需安装 Office。无外部依赖。随处可用。

**内置面向 Agent 的渲染引擎** —— Agent 可以“看到”自己创建的内容，无需安装 Office。将 `.docx` / `.xlsx` / `.pptx` 渲染为 HTML 或 PNG，在二进制程序运行的任何地方完成 *渲染 → 查看 → 修复* 闭环。

[![GitHub Release](https://img.shields.io/github/v/release/iOfficeAI/OfficeCLI)](https://github.com/iOfficeAI/OfficeCLI/releases)
[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)

**English** | [中文](README_zh.md) | [日本語](README_ja.md) | [한국어](README_ko.md)

<p align="center">
  <strong>💬 社区：</strong> <a href="https://discord.gg/2QAwJn7Egx" target="_blank">Discord</a>
</p>

<p align="center">
  <img src="assets/ppt-process.webp" alt="OfficeCLI 在 AionUi 上创建 PowerPoint 演示文稿" width="100%">
</p>

<p align="center"><em>使用 OfficeCLI 在 <a href="https://github.com/iOfficeAI/AionUi">AionUi</a> 上的 PPT 创建流程</em></p>

<p align="center"><strong>PowerPoint 演示文稿</strong></p>

<table>
<tr>
<td width="33%"><img src="assets/designwhatmovesyou.gif" alt="OfficeCLI 设计类演示文稿 (PowerPoint)"></td>
<td width="33%"><img src="assets/horizon.gif" alt="OfficeCLI 商业类演示文稿 (PowerPoint)"></td>
<td width="33%"><img src="assets/efforless.gif" alt="OfficeCLI 科技类演示文稿 (PowerPoint)"></td>
</tr>
<tr>
<td width="33%"><img src="assets/blackhole.gif" alt="OfficeCLI 太空主题演示文稿 (PowerPoint)"></td>
<td width="33%"><img src="assets/first-ppt-aionui.gif" alt="OfficeCLI 游戏类演示文稿 (PowerPoint)"></td>
<td width="33%"><img src="assets/shiba.gif" alt="OfficeCLI 创意类演示文稿 (PowerPoint)"></td>
</tr>
</table>

<p align="center">—</p>
<p align="center"><strong>Word 文档</strong></p>

<table>
<tr>
<td width="33%"><img src="assets/showcase/word1.gif" alt="OfficeCLI 学术论文 (Word)"></td>
<td width="33%"><img src="assets/showcase/word2.gif" alt="OfficeCLI 项目提案 (Word)"></td>
<td width="33%"><img src="assets/showcase/word3.gif" alt="OfficeCLI 年度报告 (Word)"></td>
</tr>
</table>

<p align="center">—</p>
<p align="center"><strong>Excel 电子表格</strong></p>

<table>
<tr>
<td width="33%"><img src="assets/showcase/excel1.gif" alt="OfficeCLI 预算追踪器 (Excel)"></td>
<td width="33%"><img src="assets/showcase/excel2.gif" alt="OfficeCLI 成绩记录表 (Excel)"></td>
<td width="33%"><img src="assets/showcase/excel3.gif" alt="OfficeCLI 销售数据看板 (Excel)"></td>
</tr>
</table>

<p align="center"><em>上述所有文档均由 AI Agent 使用 OfficeCLI 完全创建 —— 无模板，无手动编辑。</em></p>

## 面向 AI Agent —— 一行代码上手

将此粘贴到 AI Agent 的对话框中 —— 它将读取技能文件并自动安装所有内容：

```
curl -fsSL https://officecli.ai/SKILL.md
```

搞定。该技能文件会教导 Agent 如何安装二进制程序并使用所有命令。

## 面向人类用户

**选项 A —— 图形界面（GUI）：**安装 [**AionUi**](https://github.com/iOfficeAI/AionUi) —— 一款桌面应用，让你通过自然语言创建和编辑 Office 文档，底层由 OfficeCLI 驱动。只需描述你的需求，AionUi 即可处理其余一切。

**选项 B —— 命令行（CLI）：**从 [GitHub Releases](https://github.com/iOfficeAI/OfficeCLI/releases) 下载对应平台的二进制程序，然后运行：

```bash
officecli install
```

这会将二进制程序复制到你的 `PATH` 环境变量中，并将 **officecli skill** 安装到你检测到的每一个 AI 编程 Agent（如 Claude Code、Cursor、Windsurf、GitHub Copilot 等）中。你的 Agent 即可立即代表你创建、读取和编辑 Office 文档，无需额外配置。

## 面向开发者 —— 30 秒内实时预览

```bash
# 1. Install (macOS / Linux)
curl -fsSL https://raw.githubusercontent.com/iOfficeAI/OfficeCLI/main/install.sh | bash
# Windows (PowerShell): irm https://raw.githubusercontent.com/iOfficeAI/OfficeCLI/main/install.ps1 | iex

# 2. Create a blank PowerPoint
officecli create deck.pptx

# 3. Start live preview — opens http://localhost:26315 in your browser
officecli watch deck.pptx

# 4. Open another terminal, add a slide — watch the browser update instantly
officecli add deck.pptx / --type slide --prop title="Hello, World!"
```

搞定。你运行的每一个 `add`、`set` 或 `remove` 命令都会实时刷新预览。尽情尝试吧 —— 浏览器就是你的实时反馈环。

## 快速开始

```bash
# Create a presentation and add content
officecli create deck.pptx
officecli add deck.pptx / --type slide --prop title="Q4 Report" --prop background=1A1A2E
officecli add deck.pptx '/slide[1]' --type shape \
  --prop text="Revenue grew 25%" --prop x=2cm --prop y=5cm \
  --prop font=Arial --prop size=24 --prop color=FFFFFF

# View as outline
officecli view deck.pptx outline
# → Slide 1: Q4 Report
# →   Shape 1 [TextBox]: Revenue grew 25%

# View as HTML — opens a rendered preview in your browser, no server needed
officecli view deck.pptx html

# Get structured JSON for any element
officecli get deck.pptx '/slide[1]/shape[1]' --json
```

```json
{
  "tag": "shape",
  "path": "/slide[1]/shape[1]",
  "attributes": {
    "name": "TextBox 1",
    "text": "Revenue grew 25%",
    "x": "720000",
    "y": "1800000"
  }
}
```

## 为什么选择 OfficeCLI？

过去需要 50 行 Python 和 3 个独立库才能实现的功能：

```python
from pptx import Presentation
from pptx.util import Inches, Pt
prs = Presentation()
slide = prs.slides.add_slide(prs.slide_layouts[0])
title = slide.shapes.title
title.text = "Q4 Report"
# ... 45 more lines ...
prs.save('deck.pptx')
```

现在只需一条命令：

```bash
officecli add deck.pptx / --type slide --prop title="Q4 Report"
```

**OfficeCLI 能做什么：**

- **创建（Create）** 文档 —— 空白或带内容均可从头生成
- **读取（Read）** 文本、结构、样式、公式 —— 以纯文本或结构化 JSON 形式输出
- **分析（Analyze）** 格式问题、样式不一致及结构缺陷
- **修改（Modify）** 任意元素 —— 文本、字体、颜色、布局、公式、图表、图片
- **重组（Reorganize）** 内容 —— 跨文档添加、删除、移动、复制元素

| Format | Read | Modify | Create |
|--------|------|--------|--------|
| Word (.docx) | ✅ | ✅ | ✅ |
| Excel (.xlsx) | ✅ | ✅ | ✅ |
| PowerPoint (.pptx) | ✅ | ✅ | ✅ |

**Word** —— 完整 [i18n & RTL（右向左）支持](https://github.com/iOfficeAI/OfficeCLI/wiki/i18n)（按脚本分区的字体槽位、按脚本的 BCP-47 语言标签 `lang.latin/ea/cs`、复杂脚本粗体/斜体/字号、`direction=rtl` 级联作用于段落/运行/章节/表格/样式/页眉/页脚/文档默认值、`rtlGutter` + `pgBorders` 简写、针对印地语/阿拉伯语/泰语/CJK 的区域设置感知页码），[段落](https://github.com/iOfficeAI/OfficeCLI/wiki/word-paragraph)、[运行（Runs）](https://github.com/iOfficeAI/OfficeCLI/wiki/word-run)、[表格](https://github.com/iOfficeAI/OfficeCLI/wiki/word-table)、[样式](https://github.com/iOfficeAI/OfficeCLI/wiki/word-style)、[页眉/页脚](https://github.com/iOfficeAI/OfficeCLI/wiki/word-header-footer)、[图片](https://github.com/iOfficeAI/OfficeCLI/wiki/word-picture)（PNG/JPG/GIF/SVG）、[公式](https://github.com/iOfficeAI/OfficeCLI/wiki/word-equation)、[批注](https://github.com/iOfficeAI/OfficeCLI/wiki/word-comment)、[脚注](https://github.com/iOfficeAI/OfficeCLI/wiki/word-footnote)、[水印](https://github.com/iOfficeAI/OfficeCLI/wiki/word-watermark)、[书签](https://github.com/iOfficeAI/OfficeCLI/wiki/word-bookmark)、[目录（TOC）](https://github.com/iOfficeAI/OfficeCLI/wiki/word-toc)、[图表](https://github.com/iOfficeAI/OfficeCLI/wiki/word-chart)、[超链接](https://github.com/iOfficeAI/OfficeCLI/wiki/word-hyperlink)、[章节](https://github.com/iOfficeAI/OfficeCLI/wiki/word-section)、[表单字段](https://github.com/iOfficeAI/OfficeCLI/wiki/word-formfield)、[内容控件（SDT）](https://github.com/iOfficeAI/OfficeCLI/wiki/word-sdt)、[域（Fields）](https://github.com/iOfficeAI/OfficeCLI/wiki/word-field)（22 种零参数类型 + MERGEFIELD / REF / PAGEREF / SEQ / STYLEREF / DOCPROPERTY / IF）、[OLE 对象](https://github.com/iOfficeAI/OfficeCLI/wiki/word-ole)、[文档属性](https://github.com/iOfficeAI/OfficeCLI/wiki/word-document)

**Excel** —— [单元格](https://github.com/iOfficeAI/OfficeCLI/wiki/excel-cell)（添加时支持拼音指南 / 假名注音）、公式（150+ 内置函数，写入时自动求值、动态数组函数自动前缀 `_xlfn.`）、[工作表](https://github.com/iOfficeAI/OfficeCLI/wiki/excel-sheet)（可见/隐藏/极隐、打印边距、printTitleRows/Cols、RTL `sheetView`、级联感知的工作表重命名）、[表格](https://github.com/iOfficeAI/OfficeCLI/wiki/excel-table)、[排序](https://github.com/iOfficeAI/OfficeCLI/wiki/excel-sort)（工作表 / 范围、多键值、侧车感知）、[条件格式](https://github.com/iOfficeAI/OfficeCLI/wiki/excel-conditionalformatting)、[图表](https://github.com/iOfficeAI/OfficeCLI/wiki/excel-chart)（含箱须图、[帕累托图](https://github.com/iOfficeAI/OfficeCLI/wiki/excel-chart-add) 支持自动排序 + 累计百分比、对数坐标轴）、[数据透视表](https://github.com/iOfficeAI/OfficeCLI/wiki/excel-pivottable)（多字段、日期分组、showDataAs、排序、总计/小计、紧凑/大纲/表格布局、重复项目标签、空行、计算字段）、[切片器](https://github.com/iOfficeAI/OfficeCLI/wiki/excel-slicer)、[命名范围](https://github.com/iOfficeAI/OfficeCLI/wiki/excel-namedrange)、[数据验证](https://github.com/iOfficeAI/OfficeCLI/wiki/excel-validation)、[图片](https://github.com/iOfficeAI/OfficeCLI/wiki/excel-picture)（PNG/JPG/GIF/SVG 含双表示回退）、[迷你图](https://github.com/iOfficeAI/OfficeCLI/wiki/excel-sparkline)、[批注](https://github.com/iOfficeAI/OfficeCLI/wiki/excel-comment)（RTL）、[自动筛选](https://github.com/iOfficeAI/OfficeCLI/wiki/excel-autofilter)、[形状](https://github.com/iOfficeAI/OfficeCLI/wiki/excel-shape)、[OLE 对象](https://github.com/iOfficeAI/OfficeCLI/wiki/excel-ole)、CSV/TSV 导入、`$Sheet:A1` 单元格寻址

**PowerPoint** —— [幻灯片](https://github.com/iOfficeAI/OfficeCLI/wiki/ppt-slide)（页眉/页脚/日期/幻灯片编号开关、隐藏）、[形状](https://github.com/iOfficeAI/OfficeCLI/wiki/ppt-shape)（图案填充、模糊效果、超链接提示 + 幻灯片跳转链接）、[图片](https://github.com/iOfficeAI/OfficeCLI/wiki/ppt-picture)（PNG/JPG/GIF/SVG，填充模式：拉伸/适应/覆盖/平铺，亮度/对比度/发光/阴影）、[表格](https://github.com/iOfficeAI/OfficeCLI/wiki/ppt-table)、[图表](https://github.com/iOfficeAI/OfficeCLI/wiki/ppt-chart)、[动画](https://github.com/iOfficeAI/OfficeCLI/wiki/ppt-slide)、[平滑切换（Morph Transitions）](https://github.com/iOfficeAI/OfficeCLI/wiki/ppt-morph-check)、[3D 模型 (.glb)](https://github.com/iOfficeAI/OfficeCLI/wiki/ppt-3dmodel)、[幻灯片缩放](https://github.com/iOfficeAI/OfficeCLI/wiki/ppt-zoom)、[公式](https://github.com/iOfficeAI/OfficeCLI/wiki/ppt-equation)、[主题](https://github.com/iOfficeAI/OfficeCLI/wiki/ppt-theme)、[连接线](https://github.com/iOfficeAI/OfficeCLI/wiki/ppt-connector)、[视频/音频](https://github.com/iOfficeAI/OfficeCLI/wiki/ppt-video)、[组合](https://github.com/iOfficeAI/OfficeCLI/wiki/ppt-group)、[备注](https://github.com/iOfficeAI/OfficeCLI/wiki/ppt-notes)（RTL、语言）、[批注](https://github.com/iOfficeAI/OfficeCLI/wiki/ppt-comment)（RTL）、[OLE 对象](https://github.com/iOfficeAI/OfficeCLI/wiki/ppt-ole)、[占位符](https://github.com/iOfficeAI/OfficeCLI/wiki/ppt-placeholder)（按 phType 添加/设置）

## 使用场景

**面向开发者：**
- 从数据库或 API 自动生成报告
- 批量处理文档（批量查找替换、样式更新）
- 在 CI/CD 环境中构建文档流水线（根据测试结果生成文档）
- Docker / 容器化环境中的无头 Office 自动化

**面向 AI Agent：**
- 根据用户提示生成演示文稿（见上方示例）
- 从文档中提取结构化数据至 JSON
- 交付前验证并检查文档质量

**面向团队：**
- 克隆文档模板并用数据填充
- CI/CD 流水线中的自动化文档校验

## 安装

以单个自包含二进制文件分发。内置 .NET 运行时 —— 无需额外安装，无运行时管理负担。

**一键安装：**

```bash
# macOS / Linux
curl -fsSL https://raw.githubusercontent.com/iOfficeAI/OfficeCLI/main/install.sh | bash

# Windows (PowerShell)
irm https://raw.githubusercontent.com/iOfficeAI/OfficeCLI/main/install.ps1 | iex
```

**或手动下载** 自 [GitHub Releases](https://github.com/iOfficeAI/OfficeCLI/releases)：

| Platform | Binary |
|----------|--------|
| macOS Apple Silicon | `officecli-mac-arm64` |
| macOS Intel | `officecli-mac-x64` |
| Linux x64 | `officecli-linux-x64` |
| Linux ARM64 | `officecli-linux-arm64` |
| Windows x64 | `officecli-win-x64.exe` |
| Windows ARM64 | `officecli-win-arm64.exe` |

验证安装：`officecli --version`

**或从下载的二进制文件自行安装（或直接运行裸命令 `officecli` 触发自动安装）：**

```bash
officecli install    # explicit
officecli            # bare invocation also triggers install
```

后台会自动检查更新。可通过 `officecli config autoUpdate false` 禁用，或通过 `OFFICECLI_SKIP_UPDATE=1` 跳过单次执行。配置文件位于 `~/.officecli/config.json`。

## 核心功能

### 内置引擎与生成原语

OfficeCLI 完全自包含。以下功能均内置于二进制程序中 —— **无需 Office**。

#### 渲染引擎

从零构建的面向 Agent 的渲染引擎直接打包在二进制文件中，覆盖形状、图表（趋势线、误差条、瀑布图、蜡烛图、迷你图）、公式（OMML → MathJax 兼容）、通过 Three.js 加载的 3D `.glb` 模型、平滑切换、幻灯片缩放及形状效果。页面级 PNG 截图通过将渲染后的 HTML 管道传输至无头浏览器生成。提供三种模式：

- **`view html`** —— 独立 HTML 文件，资源内联。在任何浏览器中打开即可。
- **`view screenshot`** —— 逐页 PNG，多模态 Agent 可直接读取。
- **`watch`** —— 本地 HTTP 服务器，支持自动刷新预览；每次 `add` / `set` / `remove` 都会即时更新浏览器。Excel watch 模式支持内联单元格编辑和拖拽重定位图表。

```bash
officecli view deck.pptx html -o /tmp/deck.html
officecli view deck.pptx screenshot -o /tmp/deck.png # add --page 1-N for more slides
officecli watch deck.pptx                            # http://localhost:26315
```

> 若无可视化能力，生成幻灯片的 Agent 就如同盲人摸象 —— 它能读取 DOM，但无法判断标题是否溢出或两个形状是否重叠。由于渲染引擎内置于二进制程序中，*渲染 → 查看 → 修复* 闭环可在 CI、Docker、无显示器的服务器上运行 —— 只要二进制程序能跑的地方就能用。

#### 公式与数据透视表引擎

150+ 内置 Excel 函数在写入时自动求值 —— 输入 `=SUM(A1:A2)`，调用 `get` 获取单元格，值已经就绪。无需往返 Office 进行重新计算。涵盖动态数组函数（`FILTER` / `UNIQUE` / `SORT` / `SEQUENCE` 带自动 `_xlfn.` 前缀）、`VLOOKUP` / `INDEX` / `MATCH`、日期与文本函数等 140+ 更多功能。

此外，通过一条命令即可从源范围生成原生 OOXML 数据透视表 —— 支持多字段行/列/筛选器、10 种聚合方式、`showDataAs` 模式、日期分组、计算字段、Top-N、布局等。透视缓存 + 定义直接写入 OOXML，Excel 打开文件时聚合结果已填充完毕：

```bash
officecli add sales.xlsx '/Sheet1' --type pivottable \
  --prop source='Data!A1:E10000' --prop rows='Region,Category' \
  --prop cols=Quarter --prop values='Revenue:sum,Units:avg' \
  --prop showDataAs=percentOfTotal
```

#### 模板合并 —— 一次设计，批量填充

`merge` 将 `.docx` / `.xlsx` / `.pptx` 中的 `{{key}}` 占位符替换为 JSON 数据 —— 跨段落、表格单元格、形状、页眉、页脚和图表标题。Agent 一次性完成布局设计（昂贵）；生产代码批量填充 N 次（廉价、确定性高、零 Token 消耗）。避免了 Agent 从头重新生成每份报告并导致 N 种不一致布局的失败模式。

```bash
officecli merge invoice-template.docx out-001.docx '{"client":"Acme","total":"$5,200"}'
officecli merge q4-template.pptx q4-acme.pptx data.json
```

#### 双向序列化（Round-trip dump）—— 从现有文档中学习

`dump` 将任意 `.docx` —— 整个文档 **或任何子树**（单个段落、表格、样式部分、编号、主题或设置） —— 序列化为可重放的批处理 JSON；`batch` 负责回放。给定一个用户希望模仿的样本，Agent 读取结构化规范而非原始 OOXML XML，进行修改后再回放。打通了“我有一个现有模板”和“给我生成 100 个变体”之间的桥梁。

```bash
officecli dump existing.docx -o blueprint.json                  # whole document
officecli dump existing.docx /body/tbl[1] -o table.json         # any subtree
officecli batch new.docx --input blueprint.json
```

### 驻留模式与批处理

对于多步骤工作流，驻留模式（Resident Mode）可将文档保留在内存中。批处理模式可在一次打开/保存周期内执行多个操作。

```bash
# Resident mode — near-zero latency via named pipes
officecli open report.docx
officecli set report.docx /body/p[1]/r[1] --prop bold=true
officecli set report.docx /body/p[2]/r[1] --prop color=FF0000
officecli close report.docx

# Batch mode — atomic multi-command execution (stops on first error by default)
echo '[{"command":"set","path":"/slide[1]/shape[1]","props":{"text":"Hello"}},
      {"command":"set","path":"/slide[1]/shape[2]","props":{"fill":"FF0000"}}]' \
  | officecli batch deck.pptx --json

# Inline batch with --commands (no stdin needed)
officecli batch deck.pptx --commands '[{"op":"set","path":"/slide[1]/shape[1]","props":{"text":"Hi"}}]'

# Use --force to continue past errors
officecli batch deck.pptx --input updates.json --force --json
```

### 三层架构

从简单开始，仅在需要时深入。

| Layer | Purpose | Commands |
|-------|---------|----------|
| **L1: Read** | 内容的语义视图 | `view` (text, annotated, outline, stats, issues, html, svg, screenshot) |
| **L2: DOM** | 结构化元素操作 | `get`, `query`, `set`, `add`, `remove`, `move`, `swap` |
| **L3: Raw XML** | 直接 XPath 访问 —— 通用回退方案 | `raw`, `raw-set`, `add-part`, `validate` |

```bash
# L1 — high-level views
officecli view report.docx annotated
officecli view budget.xlsx text --cols A,B,C --max-lines 50

# L2 — element-level operations
officecli query report.docx "run:contains(TODO)"
officecli add budget.xlsx / --type sheet --prop name="Q2 Report"
officecli move report.docx /body/p[5] --to /body --index 1

# L3 — raw XML when L2 isn't enough
officecli raw deck.pptx '/slide[1]'
officecli raw-set report.docx document \
  --xpath "//w:p[1]" --action append \
  --xml '<w:r><w:t>Injected text</w:t></w:r>'
```

## AI 集成

### MCP 服务器

内置 [MCP](https://modelcontextprotocol.io) 服务器 —— 一条命令注册：

```bash
officecli mcp claude       # Claude Code
officecli mcp cursor       # Cursor
officecli mcp vscode       # VS Code / Copilot
officecli mcp lmstudio     # LM Studio
officecli mcp list         # Check registration status
```

通过 JSON-RPC 将所有文档操作暴露为工具 —— 无需 Shell 访问权限。

### 直接 CLI 集成

分两步让你的 AI Agent 与 OfficeCLI 协同工作：

1. **安装二进制程序** —— 一条命令（见 [Installation](#installation)）
2. **完成。** OfficeCLI 会自动检测你的 AI 工具（通过检查已知配置目录），并自动安装其技能文件。你的 Agent 即可立即创建、读取和修改任意 Office 文档。

<details>
<summary><strong>手动设置（可选）</strong></summary>

如果自动安装未覆盖你的环境，可手动安装技能文件：

**直接将 SKILL.md 喂给 Agent：**

```bash
curl -fsSL https://officecli.ai/SKILL.md
```

**作为 Claude Code 的本地技能安装：**

```bash
curl -fsSL https://officecli.ai/SKILL.md -o ~/.claude/skills/officecli.md
```

**其他 Agent：** 将 `SKILL.md` 的内容包含在你的 Agent 系统提示词或工具描述中。

</details>

### 为什么你的 Agent 能在 OfficeCLI 上如鱼得水

- **确定性 JSON 输出** —— 每条命令均支持 `--json`，且 Schema 一致。无需正则解析，无需抓取 stdout。
- **基于路径的寻址（Path-based addressing）** —— 每个元素都有稳定路径（`/slide[1]/shape[2]`）。Agent 可在不理解 XML 命名空间的情况下导航文档。（OfficeCLI 语法：1-based 索引、元素本地名称 —— 非 XPath。）
- **渐进式复杂度（L1 → L2 → L3）** —— Agent 从只读视图开始，升级到 DOM 操作，仅在必要时回退到原始 XML。最大限度降低 Token 消耗。
- **自愈工作流** —— `validate`、`view issues` 及结构化错误码（`not_found`、`invalid_value`、`unsupported_property`）会返回建议与有效范围。Agent 可自我修正，无需人工干预。
- **内置面向 Agent 的渲染引擎** —— `view html` / `view screenshot` / `watch` 原生输出 HTML 和 PNG。无需 Office。Agent 可以“看到”自己的输出并修复布局问题，即使在 CI / Docker / 无头环境中亦然。
- **内置公式与数据透视表引擎** —— 150+ Excel 函数写入时自动求值；一条命令即可从源范围生成原生 OOXML 数据透视表。Agent 可立即读取计算结果和已交付的聚合数据，无需往返 Office。
- **模板合并** —— Agent 一次性设计布局，下游代码批量填充 `{{key}}` 占位符 N 次。避免从头重新生成每份报告而浪费 Token。
- **双向序列化（Round-trip dump）** —— `dump` 将任意 `.docx` 转换为可重放的批处理 JSON。Agent 通过读取结构化规范而非原始 OOXML XML 向人类编写的样本学习。
- **内置帮助** —— 当不确定属性名或值格式时，Agent 会运行 `officecli <format> set <element>` 而非盲目猜测。
- **自动安装** —— OfficeCLI 检测你的 AI 工具链（Claude Code、Cursor、VS Code 等）并自动配置自身。无需手动设置技能文件。

### 内置帮助

不要猜属性名 —— 深入查看帮助文档：

```bash
officecli pptx set              # All settable elements and properties
officecli pptx set shape        # Detail for one element type
officecli pptx set shape.fill   # One property: format and examples
officecli docx query            # Selector reference: attributes, :contains, :has(), etc.
```

运行 `officecli --help` 获取完整概览。

### JSON 输出 Schema

所有命令均支持 `--json`。通用响应结构如下：

**单个元素（`get --json`）：**

```json
{"tag": "shape", "path": "/slide[1]/shape[1]", "attributes": {"name": "TextBox 1", "text": "Hello"}}
```

**元素列表（`query --json`）：**

```json
[
  {"tag": "paragraph", "path": "/body/p[1]", "attributes": {"style": "Heading1", "text": "Title"}},
  {"tag": "paragraph", "path": "/body/p[5]", "attributes": {"style": "Heading1", "text": "Summary"}}
]
```

**错误（Errors）** 返回非零退出码，并附带结构化错误对象，包含错误代码、建议及可用有效值：

```json
{
  "success": false,
  "error": {
    "error": "Slide 50 not found (total: 8)",
    "code": "not_found",
    "suggestion": "Valid Slide index range: 1-8"
  }
}
```

错误代码：`not_found`、`invalid_value`、`unsupported_property`、`invalid_path`、`unsupported_type`、`missing_property`、`file_not_found`、`file_locked`、`invalid_selector`。属性名支持自动纠错 —— 拼写错误的属性会返回最接近匹配的建议值。

**错误恢复（Error Recovery）** —— Agent 通过检查可用元素自我修正：

```bash
# Agent tries an invalid path
officecli get report.docx /body/p[99] --json
# Returns: {"success": false, "error": {"error": "...", "code": "not_found", "suggestion": "..."}}

# Agent self-corrects by checking available elements
officecli get report.docx /body --depth 1 --json
# Returns the list of available children, agent picks the right path
```

**变更确认（Mutation confirmations）（`set`, `add`, `remove`, `move`, `create` 配合 `--json`）：**

```json
{"success": true, "path": "/slide[1]/shape[1]"}
```

详见 `officecli --help` 获取退出码和错误格式的完整说明。

## 对比

| | OfficeCLI | Microsoft Office | LibreOffice | python-docx / openpyxl |
|---|---|---|---|---|
| 开源且免费 | ✓ (Apache 2.0) | ✗ (付费许可) | ✓ | ✓ |
| AI 原生 CLI + JSON | ✓ | ✗ | ✗ | ✗ |
| 零安装（单文件二进制） | ✓ | ✗ | ✗ | ✗ (Python + pip) |
| 任意语言调用 | ✓ (CLI) | ✗ (COM/Add-in) | ✗ (UNO API) | Python only |
| 基于路径的元素访问 | ✓ | ✗ | ✗ | ✗ |
| 原始 XML 回退方案 | ✓ | ✗ | ✗ | Partial |
| 内置面向 Agent 的渲染引擎 | ✓ | ✗ | ✗ | ✗ |
| 无头 HTML/PNG 输出 | ✓ | ✗ | Partial | ✗ |
| 跨格式模板合并 (`{{key}}`) | ✓ | ✗ | ✗ | ✗ |
| 双向序列化 → 批处理 JSON | ✓ | ✗ | ✗ | ✗ |
| 实时预览（编辑时自动刷新） | ✓ | ✗ | ✗ | ✗ |
| 无头 / CI 环境支持 | ✓ | ✗ | Partial | ✓ |
| 跨平台 | ✓ | Windows/Mac | ✓ | ✓ |
| Word + Excel + PowerPoint | ✓ | ✓ | ✓ | Separate libs |

## 命令参考

| Command | Description |
|---------|-------------|
| [`create`](https://github.com/iOfficeAI/OfficeCLI/wiki/command-create) | 创建空白 .docx, .xlsx, 或 .pptx（根据扩展名自动识别类型） |
| [`view`](https://github.com/iOfficeAI/OfficeCLI/wiki/command-view) | 查看内容（模式：`outline`, `text`, `annotated`, `stats` (`--page-count`), `issues`, `html`, `svg`, `screenshot`, `pdf` (通过导出器插件), `forms` (通过格式处理器插件)）。docx 支持 `--render auto\|native\|html`. |
| [`load_skill`](https://github.com/iOfficeAI/OfficeCLI/wiki/command-skills) | 打印专用技能的嵌入式 SKILL.md 内容（无需安装） |
| [`get`](https://github.com/iOfficeAI/OfficeCLI/wiki/command-get) | 获取元素及其子节点 (`--depth N`, `--json`) |
| [`query`](https://github.com/iOfficeAI/OfficeCLI/wiki/command-query) | CSS 风格查询 (`[attr=value]`, `:contains()`, `:has()` 等) |
| [`set`](https://github.com/iOfficeAI/OfficeCLI/wiki/command-set) | 修改元素属性 |
| [`add`](https://github.com/iOfficeAI/OfficeCLI/wiki/command-add) | 添加元素（或通过 `--from <path>` 克隆） |
| [`remove`](https://github.com/iOfficeAI/OfficeCLI/wiki/command-remove) | 删除元素 |
| [`move`](https://github.com/iOfficeAI/OfficeCLI/wiki/command-move) | 移动元素 (`--to <parent>`, `--index N`, `--after <path>`, `--before <path>`) |
| [`swap`](https://github.com/iOfficeAI/OfficeCLI/wiki/command-swap) | 交换两个元素 |
| [`validate`](https://github.com/iOfficeAI/OfficeCLI/wiki/command-validate) | 基于 OpenXML Schema 验证 |
| `view <file> issues` | 枚举文档问题（文本溢出、缺少替代文本、公式错误等） |
| [`batch`](https://github.com/iOfficeAI/OfficeCLI/wiki/command-batch) | 单次打开/保存周期内执行多项操作（支持 stdin, `--input`, 或 `--commands`; 默认遇错停止，`--force` 继续） |
| [`dump`](https://github.com/iOfficeAI/OfficeCLI/wiki/command-dump) | 将 `.docx` 或 `.pptx` 序列化为可重放的批处理 JSON（通过 `batch` 双向回放）；接受子树路径 |
| [`refresh`](https://github.com/iOfficeAI/OfficeCLI/wiki/command-refresh) | 重新计算目录页码 / `PAGE` / 交叉引用 (`.docx`; Windows 下调用 Word 后端，无头环境回退至 HTML) |
| [`plugins`](https://github.com/iOfficeAI/OfficeCLI/wiki/command-plugins) | 列出 / 检查 / 校验已安装插件（通过 dump-reader / exporter / format-handler 类型扩展支持 `.doc`, `.hwpx`, `.pdf` 导出） |
| [`merge`](https://github.com/iOfficeAI/OfficeCLI/wiki/command-merge) | 模板合并 —— 将 `{{key}}` 占位符替换为 JSON 数据 |
| [`watch`](https://github.com/iOfficeAI/OfficeCLI/wiki/command-watch) | 浏览器内实时 HTML 预览，支持自动刷新 |
| [`mcp`](https://github.com/iOfficeAI/OfficeCLI/wiki/command-mcp) | 启动 MCP 服务器以集成 AI 工具 |
| [`raw`](https://github.com/iOfficeAI/OfficeCLI/wiki/command-raw) | 查看文档部分的原始 XML |
| [`raw-set`](https://github.com/iOfficeAI/OfficeCLI/wiki/command-raw) | 通过 XPath 修改原始 XML |
| `add-part` | 添加新的文档部分（页眉、图表等） |
| [`open`](https://github.com/iOfficeAI/OfficeCLI/wiki/command-open) | 启动驻留模式（将文档保留在内存中） |
| `close` | 保存并关闭驻留模式 |
| [`install`](https://github.com/iOfficeAI/OfficeCLI/wiki/command-install) | 安装二进制程序 + 技能文件 + MCP (`all`, `claude`, `cursor` 等) |
| `config` | 获取或设置配置 |
| `<format> <command>` | [内置帮助](https://github.com/iOfficeAI/OfficeCLI/wiki/command-reference) (例如 `officecli pptx set shape`) |

## 端到端工作流示例

典型的自愈 Agent 工作流：创建演示文稿、填充内容、验证并修复问题 —— 全程无需人工干预。

```bash
# 1. Create
officecli create report.pptx

# 2. Add content
officecli add report.pptx / --type slide --prop title="Q4 Results"
officecli add report.pptx '/slide[1]' --type shape \
  --prop text="Revenue: $4.2M" --prop x=2cm --prop y=5cm --prop size=28
officecli add report.pptx / --type slide --prop title="Details"
officecli add report.pptx '/slide[2]' --type shape \
  --prop text="Growth driven by new markets" --prop x=2cm --prop y=5cm

# 3. Verify
officecli view report.pptx outline
officecli validate report.pptx

# 4. Fix any issues found
officecli view report.pptx issues --json
# Address issues based on output, e.g.:
officecli set report.pptx '/slide[1]/shape[1]' --prop font=Arial
```

### 单位与颜色

所有尺寸和颜色属性均接受灵活的输入格式：

| Type | Accepted formats | Examples |
|------|-----------------|----------|
| **Dimensions** | cm, in, pt, px, or raw EMU | `2cm`, `1in`, `72pt`, `96px`, `914400` |
| **Colors** | Hex, named, RGB, theme | `#FF0000`, `FF0000`, `red`, `rgb(255,0,0)`, `accent1` |
| **Font sizes** | Bare number or pt-suffixed | `14`, `14pt`, `10.5pt` |
| **Spacing** | pt, cm, in, or multiplier | `12pt`, `0.5cm`, `1.5x`, `150%` |

## 常见模式

```bash
# Replace all Heading1 text in a Word doc
officecli query report.docx "paragraph[style=Heading1]" --json | ...
officecli set report.docx /body/p[1]/r[1] --prop text="New Title"

# Export all slide content as JSON
officecli get deck.pptx / --depth 2 --json

# Bulk-update Excel cells
officecli batch budget.xlsx --input updates.json --json

# Import CSV data into an Excel sheet
officecli add budget.xlsx / --type sheet --prop name="Q1 Data" --prop csv=sales.csv

# Template merge for batch reports
officecli merge invoice-template.docx invoice-001.docx '{"client":"Acme","total":"$5,200"}'

# Check document quality before delivery
officecli validate report.docx && officecli view report.docx issues --json
```

**从 Python 调用** —— 封装一次，每次调用均返回解析后的 JSON：

```python
import json, subprocess

def cli(*args):
    return json.loads(subprocess.check_output(["officecli", *args, "--json"], text=True))

cli("create", "deck.pptx")
cli("add", "deck.pptx", "/", "--type", "slide", "--prop", "title=Q4 Report")
slide = cli("get", "deck.pptx", "/slide[1]")
print(slide["attributes"]["text"])
```

## 文档

[Wiki](https://github.com/iOfficeAI/OfficeCLI/wiki) 包含每个命令、元素类型和属性的详细指南：

- **按格式：** [Word](https://github.com/iOfficeAI/OfficeCLI/wiki/word-reference) | [Excel](https://github.com/iOfficeAI/OfficeCLI/wiki/excel-reference) | [PowerPoint](https://github.com/iOfficeAI/OfficeCLI/wiki/powerpoint-reference)
- **工作流：** [端到端示例](https://github.com/iOfficeAI/OfficeCLI/wiki/workflows) —— Word 报告、Excel 看板、PowerPoint 演示文稿、批量修改、驻留模式
- **故障排除：** [常见错误与解决方案](https://github.com/iOfficeAI/OfficeCLI/wiki/troubleshooting)
- **AI Agent 指南：** [导航 Wiki 的决策树](https://github.com/iOfficeAI/OfficeCLI/wiki/agent-guide)

## 从源码构建

仅需 [.NET 10 SDK](https://dotnet.microsoft.com/download) 用于编译。输出结果为自包含的原生二进制程序 —— .NET 已嵌入二进制文件中，运行时无需安装。

```bash
./build.sh
```

## 许可证

[Apache License 2.0](LICENSE)

欢迎在 [GitHub Issues](https://github.com/iOfficeAI/OfficeCLI/issues) 提交 Bug 报告与贡献代码。

---

如果你发现 OfficeCLI 有用，请 [给它在 GitHub 上点个 Star](https://github.com/iOfficeAI/OfficeCLI) —— 这有助于更多人发现该项目。

[OfficeCLI.AI](https://OfficeCLI.AI) | [GitHub](https://github.com/iOfficeAI/OfficeCLI)

<!--
yaml-frontmatter:
  name: officecli
  version: see GitHub Releases
  description: The standard CLI for AI agents to create, read, and modify Office documents
  formats: [docx, xlsx, pptx]
  platforms: [macos, linux, windows]
  license: Apache-2.0
  keywords: [office, cli, ai-agent, automation, docx, xlsx, pptx, openxml, document-generation, mcp-server, word, excel, powerpoint]
  ai-agent-compatible: true
  mcp-server: true
  skill-file: SKILL.md

  install-command-unix: curl -fsSL https://raw.githubusercontent.com/iOfficeAI/OfficeCLI/main/install.sh | bash
  install-command-windows: irm https://raw.githubusercontent.com/iOfficeAI/OfficeCLI/main/install.ps1 | iex
-->

<!-- LLM/agent discovery metadata
tool: officecli
type: cli
canonical: the standard CLI for AI-driven Office document manipulation
formats: docx, xlsx, pptx
capabilities: create, read, modify, validate, batch, resident-mode, mcp-server, live-preview, auto-install
output: json, text, annotated
platforms: macos, linux, windows
license: Apache-2.0
keywords: office, cli, ai-agent, automation, docx, xlsx, pptx, openxml, document-generation, mcp-server, word, excel, powerpoint, ai-tools, command-line, structured-output
ai-agent-compatible: true
mcp-server: true
skill-file: SKILL.md
skill-file-lines: 403
alternatives: python-docx, openpyxl, python-pptx, libreoffice --headless
install-command-unix: curl -fsSL https://raw.githubusercontent.com/iOfficeAI/OfficeCLI/main/install.sh | bash
install-command-windows: irm https://raw.githubusercontent.com/iOfficeAI/OfficeCLI/main/install.ps1 | iex
-->
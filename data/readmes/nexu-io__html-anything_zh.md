# HTML Anything

<p align="center"><sub>来自 <a href="https://github.com/nexu-io/open-design"><b>Open Design</b></a> 团队 —— <b>40k★ · 200+ 贡献者</b>，生产级项目且迭代迅速。html-anything 是面向 Agent 时代的专注型 HTML 编辑器；如果你喜欢它，<a href="https://github.com/nexu-io/open-design">Open Design</a> 将是同一团队规模化交付的阵地。</sub></p>

<p align="center"><b>在线预览：</b> <a href="https://open-design.ai/html-anything/"><b>open-design.ai/html-anything/</b></a> —— 在克隆代码前，先浏览概览、交付形式（surface modes）与展示案例。</p>

> **Markdown 是草稿，HTML 才是人类阅读的内容。你的本地 Agent 负责编写它。** 这是一款 AI Agent 驱动的 HTML 编辑器 —— 在 Agent 时代，你不再需要手动编辑文档，因此输出格式应当符合读者的实际阅读需求：HTML。采用本地优先架构，零 API Key，直接复用你已登录的 CLI 会话 —— **8 款编程 Agent CLI** 会自动检测你的 `PATH`（Claude Code · Cursor Agent · Codex · Gemini CLI · GitHub Copilot CLI · OpenCode · Qwen Coder · Aider），由 **75 个可组合的技能模板** 驱动，覆盖 **9 种交付形式**（杂志文章 · 主题演讲幻灯片 · 简历 · 海报 · 小红书卡片 · Twitter/X 推文卡片 · Web 原型 · 数据报告 · Hyperframes 视频）。支持一键导出到微信 / X / 知乎，或直接下载 `.html` / `.png`。

<p align="center">
  <img src="docs/assets/banner.png" alt="HTML Anything —— 你的本地 AI Agent HTML 编辑器" width="100%" />
</p>

<p align="center">
  <a href="LICENSE"><img alt="License" src="https://img.shields.io/badge/license-Apache%202.0-blue.svg?style=flat-square" /></a>
  <a href="#supported-coding-agents"><img alt="Agents" src="https://img.shields.io/badge/agents-8%20CLIs-black?style=flat-square" /></a>
  <a href="#skills"><img alt="Skills" src="https://img.shields.io/badge/skills-75-orange?style=flat-square" /></a>
  <a href="#export-targets"><img alt="Export" src="https://img.shields.io/badge/export-WeChat%20%C2%B7%20X%20%C2%B7%20Zhihu%20%C2%B7%20PNG-9b59b6?style=flat-square" /></a>
  <a href="#quickstart"><img alt="Quickstart" src="https://img.shields.io/badge/quickstart-30%20seconds-green?style=flat-square" /></a>
  <a href="#architecture"><img alt="No API key" src="https://img.shields.io/badge/no-API%20key%20required-ff6b35?style=flat-square" /></a>
</p>

<!-- This project is built on top of nexu-io/open-design — the badges below link to its community channels on purpose. -->
<p align="center">
  <a href="https://discord.gg/keeVPMrueT"><img alt="Discord (html-anything)" src="https://img.shields.io/badge/discord-html--anything-5865f2?style=flat-square&logo=discord&logoColor=white" /></a>
  <a href="https://x.com/nexudotio"><img alt="Follow @nexudotio on X" src="https://img.shields.io/badge/follow-%40nexudotio-000000?style=flat-square&logo=x&logoColor=white" /></a>
  <a href="https://github.com/nexu-io/open-design/releases/latest"><img alt="open-design release" src="https://img.shields.io/github/v/release/nexu-io/open-design?style=flat-square&label=release&color=8e44ad" /></a>
  <a href="https://github.com/nexu-io/open-design/graphs/commit-activity"><img alt="open-design commits / month" src="https://img.shields.io/github/commit-activity/m/nexu-io/open-design?style=flat-square&label=commits%2Fmonth&color=f39c12" /></a>
  <a href="#showcase"><img alt="Design systems" src="https://img.shields.io/badge/design%20systems-9-1abc9c?style=flat-square" /></a>
  <a href="https://github.com/nexu-io/open-design"><img alt="Built on open-design" src="https://img.shields.io/badge/built%20on-nexu--io%2Fopen--design-ff7043?style=flat-square&logo=github&logoColor=white" /></a>
</p>

<p align="center"><b>English</b> · <a href="README.zh-CN.md">简体中文</a></p>

---

## 案例展示

选择器中“精选（Featured）”分组顶部展示的八个技能 —— 按 `SKILL.md` 元数据中的 `recommended:` 值排序（数值越低排名越高）。每个技能都附带一个真实的 `example.html`，你可直接从仓库打开预览，无需任何认证或配置。

<table>
<tr>
<td width="50%" valign="top">
<a href="next/src/lib/templates/skills/deck-guizang-editorial/"><img src="docs/screenshots/skills/deck-guizang-editorial.png" alt="deck-guizang-editorial" /></a><br/>
<sub><b><a href="next/src/lib/templates/skills/deck-guizang-editorial/"><code>deck-guizang-editorial</code></a></b> · <i>幻灯片（deck）</i> · <code>recommended: 1</code><br/>杂志 × 电子墨水风格编辑排版幻灯片，灵感源自 <a href="https://github.com/op7418/guizang-ppt-skill"><code>op7418/guizang-ppt-skill</code></a> —— 10 种固定布局 × 5 套配色（墨色 / 靛蓝瓷 / 森林墨 / 牛皮纸 / 沙丘）。阅读体验如同印刷艺术杂志，而非普通幻灯片。</sub>
</td>
<td width="50%" valign="top">
<a href="next/src/lib/templates/skills/deck-swiss-international/"><img src="docs/screenshots/skills/deck-swiss-international.png" alt="deck-swiss-international" /></a><br/>
<sub><b><a href="next/src/lib/templates/skills/deck-swiss-international/"><code>deck-swiss-international</code></a></b> · <i>幻灯片（deck）</i> · <code>recommended: 2</code><br/>瑞士国际风格幻灯片 —— 16 列网格 + 高饱和度强调色（克莱因蓝 / 柠檬黄 / 薄荷绿 / 安全橙），覆盖 22 种固定布局。冷峻、理性、机构感极强。打开的瞬间就能看出“这是设计师做的”。</sub>
</td>
</tr>
<tr>
<td width="50%" valign="top">
<a href="next/src/lib/templates/skills/doc-kami-parchment/"><img src="docs/screenshots/skills/doc-kami-parchment.png" alt="doc-kami-parchment" /></a><br/>
<sub><b><a href="next/src/lib/templates/skills/doc-kami-parchment/"><code>doc-kami-parchment</code></a></b> · <i>文档（doc）</i> · <code>recommended: 3</code><br/>暖色调羊皮纸风格编辑文档，灵感源自 <a href="https://github.com/tw93/kami"><code>tw93/kami</code></a>。<code>#f5f4ed</code> 底色 + 墨蓝强调色 + 单衬线字体 —— 相比纯白 Markdown，为长篇论文、报告和单页文档提供更舒适的阅读表面。</sub>
</td>
<td width="50%" valign="top">
<a href="next/src/lib/templates/skills/magazine-poster/"><img src="docs/screenshots/skills/magazine-poster.png" alt="magazine-poster" /></a><br/>
<sub><b><a href="next/src/lib/templates/skills/magazine-poster/"><code>magazine-poster</code></a></b> · <i>海报（poster）</i> · <code>recommended: 4</code><br/>新闻报纸周日特刊海报 —— 超大号衬线标题、双栏正文、六个编号章节、点阵图案奶油底色。阅读体验如同印刷版大报，而非网页。</sub>
</td>
</tr>
<tr>
<td width="50%" valign="top">
<a href="next/src/lib/templates/skills/video-hyperframes/"><img src="docs/screenshots/skills/video-hyperframes.png" alt="video-hyperframes" /></a><br/>
<sub><b><a href="next/src/lib/templates/skills/video-hyperframes/"><code>video-hyperframes</code></a></b> · <i>帧 / 视频（frame / video）</i> · <code>recommended: 5</code><br/>Hyperframes / Remotion 兼容的分镜脚本 —— 6–10 个连续的 <code>1920×1080</code> 帧，包含隐藏的时间轴 + 转场标记和自动播放脚本。直接交给 <a href="https://github.com/heygen-com/hyperframes"><code>heygen-com/hyperframes</code></a> 或 Remotion 渲染 <code>.mp4</code>。</sub>
</td>
<td width="50%" valign="top">
<a href="next/src/lib/templates/skills/frame-glitch-title/"><img src="docs/screenshots/skills/frame-glitch-title.png" alt="frame-glitch-title" /></a><br/>
<sub><b><a href="next/src/lib/templates/skills/frame-glitch-title/"><code>frame-glitch-title</code></a></b> · <i>帧（frame）</i> · <code>recommended: 6</code><br/>故障艺术标题帧 —— 青/洋红色差偏移、CRT 扫描线、损坏数据副标题、角落 ASCII 噪点。赛博朋克主视觉卡片或视频转场素材。</sub>
</td>
</tr>
<tr>
<td width="50%" valign="top">
<a href="next/src/lib/templates/skills/vfx-text-cursor/"><img src="docs/screenshots/skills/vfx-text-cursor.png" alt="vfx-text-cursor" /></a><br/>
<sub><b><a href="next/src/lib/templates/skills/vfx-text-cursor/"><code>vfx-text-cursor</code></a></b> · <i>VFX 特效</i> · <code>recommended: 7</code><br/>VFX 文字光标开场动画 —— 光标在画布上“打字”，每个字符带出亮粉色 × 青色的色差拖尾和定向光泄漏。填入一段引言，即可生成电影级开场帧。</sub>
</td>
<td width="50%" valign="top">
<a href="next/src/lib/templates/skills/frame-logo-outro/"><img src="docs/screenshots/skills/frame-logo-outro.png" alt="frame-logo-outro" /></a><br/>
<sub><b><a href="next/src/lib/templates/skills/frame-logo-outro/"><code>frame-logo-outro</code></a></b> · <i>帧（frame）</i> · <code>recommended: 8</code><br/>品牌 Logo 片尾帧 —— Logo 逐块组装并带有辉光泛光效果，标语上浮，CTA（行动号召）显现。适用于产品发布或品牌宣传片的结尾卡片。</sub>
</td>
</tr>
</table>

完整技能目录（按模式分类）见下方的 [Skills](#skills)。

## 为什么会有这个项目

Anthropic 的 [Claude Code 团队宣布](https://x.com/trq212/status/2052809885763747935)他们已停止使用 Markdown 编写内部文档 —— 现在直接交付 HTML。理由很简单：

| Markdown | HTML |
|---|---|
| 对作者友好 | 对读者友好 |
| 排版受限于渲染器 | 排版由你掌控 |
| 截图发推文效果很差 | 天生就是设计好的图片样式 |
| 需重新排版才能适配微信/知乎/Newsletter | 一键转换格式 |

**HTML 才是人类阅读的最终形态，Markdown 只是写作过程中的中间态。**

但“编写 HTML”过去意味着写 CSS、选字体比例、对齐网格、做响应式适配 —— 大多数用户不会，设计师懒得折腾，作者也没耐心。所以我们做了这个：按下 ⌘+Enter 后，你的 **本地 AI Agent** 会在几秒内将任意输入（Markdown / CSV / Excel / JSON / SQL / 原始笔记）转换为 **可直接交付的单文件 HTML**，然后一键发送到微信 / X / 知乎或任何地方。“开箱即用”是标准 —— 生成结束时，产物就是观众实际看到的样子。没有“我稍后微调一下”的返工环节。

我们站在四个开源项目的肩膀上：

- [**`nexu-io/open-design`**](https://github.com/nexu-io/open-design) —— Agent 检测层、设计系统模型与 `SKILL.md` 协议。`next/src/lib/agents/` 和 `next/src/lib/templates/skills/*` 直接镜像了该架构。
- [**`mdnice/markdown-nice`**](https://github.com/mdnice/markdown-nice) —— 证明了将 CSS 内联后粘贴到微信和知乎无需逐平台手动修复。
- [**`gcui-art/markdown-to-image`**](https://github.com/gcui-art/markdown-to-image) —— iframe → 高 DPI PNG 导出路径。
- [**`alchaincyf/huashu-md-html`**](https://github.com/alchaincyf/huashu-md-html) —— 反 AI 水化（anti-AI-slop）规范，映射为每个 `SKILL.md` 内部的硬约束（CJK 优先字体栈、8 px 基线网格、对比度 ≥ 4.5、必须使用真实数据规则）。

## 核心特性一览

| | 你将获得什么 |
|---|---|
| **编程 Agent CLI（8款）** | Claude Code · Cursor Agent · OpenAI Codex · Gemini CLI · GitHub Copilot CLI · OpenCode · Qwen Coder · Aider —— 启动时扫描 `PATH`（包括 `~/.local/bin`、`~/.bun/bin`、`/opt/homebrew/bin`、`~/.npm-global/bin` —— GUI 启动的 Node 进程通常会遗漏这些目录），通过顶部栏选择器切换。 |
| **零 API Key** | 复用你已通过 `claude login` · `cursor login` · `gemini auth` 登录的会话。现有订阅直接干活，边际成本为 **$0**。 |
| **75 个技能模板** | `prototype`（Web / SaaS 落地页 / 仪表盘 / 数据报告）· `deck`（20 款主题演讲技能，含瑞士国际、贵藏编辑、小红书 pastel、Hermes Cyber、Replit、杂志 Web…）· `frame`（10 个 Hyperframes 视频帧 —— 液态主视觉、NYT 数据图、便签流程图、故障标题、电影光泄漏、macOS 通知、Logo 片尾…）· `social`（X / 小红书 / Spotify / Reddit 卡片）· `office`（PM 规范 · 工程手册 · 财务报告 · HR 入职 · 发票 · OKR · 周报 · 会议纪要 · 看板）· `doc`（Kami 暖羊皮纸编辑排版）· `mockup`（3D 设备样机）· `vfx`（文字光标特效）。 |
| **9 种交付形式** | 📖 杂志文章 · 🎬 主题演讲幻灯片 · 📄 简历 · 🖼️ 海报 · 📱 小红书卡片 · 🐦 推文卡片 · 🛠️ Web 原型 · 📊 数据报告 · 🎞️ Hyperframes 视频。每种形式包含多个可选技能。 |
| **一键导出** | `juice` 内联 CSS → 微信粘贴零重排 · `modern-screenshot` 渲染 iframe 为 2× PNG → `ClipboardItem` → 直接拖入推文编辑器 · `<mjx-container>` → `data-eeimg` 占位符 → 知乎公式自动渲染 · 独立 `.html` 下载 · 高 DPI `.png` 下载。 |
| **流式渲染** | `POST /api/convert` 基于 SSE。Agent 的 stdout JSON-line 流解析为文本增量 → Server-Sent Events → 客户端追加 → iframe `srcdoc` 实时更新。等待 AI 生成就像看着它在终端里实时打字。 |
| **沙箱预览** | `<iframe sandbox="allow-scripts allow-same-origin">`。用户生成的 HTML 在隔离的 origin 中运行 —— Tailwind CDN / Google Fonts / 内联脚本可用，但 Cookie 和 localStorage 与宿主机隔离。 |
| **格式自动检测** | 编辑器接受 Markdown / CSV / TSV / JSON / SQL / 纯文本。`papaparse` + `xlsx` 在浏览器端解析表格数据 —— 绝不上传任何内容。 |
| **可部署至** | 本地（`pnpm -F @html-anything/next dev`）· Vercel Web 层（Agent 始终驻留你的电脑）。 |
| **许可证** | Apache-2.0 |

## 演示

<table>
<tr>
<td width="50%">
<img src="docs/screenshots/01-entry-view.png" alt="01 · 入口视图" /><br/>
<sub><b>入口视图</b> —— 顶部栏显示已安装的 CLI，左侧为编辑器，中间为模板 + 设计系统选择器，右侧为实时 iframe 预览。同一界面可生成杂志、幻灯片、海报、Web 原型和 Hyperframes 分镜脚本。</sub>
</td>
<td width="50%">
<img src="docs/screenshots/02-template-picker.png" alt="02 · 75 个技能，支持搜索与筛选" /><br/>
<sub><b>75 个模板，支持搜索与筛选</b> —— 按模式（prototype / deck / frame / social / office / doc）× 场景（design / marketing / engineering / product / personal）选择。每个技能都附带一个 <code>example.html</code>，你可直接从仓库打开预览 Agent 的产出效果。</sub>
</td>
</tr>
<tr>
<td width="50%">
<img src="docs/screenshots/03-streaming.png" alt="03 · SSE 流式传输" /><br/>
<sub><b>SSE 流式传输</b> —— Agent stdout JSON-line 解析文本增量，实时追加至 iframe <code>srcdoc</code>。你看着页面逐行渲染。不喜欢当前走向？随时中断并重新提示 —— 不会浪费整次生成。</sub>
</td>
<td width="50%">
<img src="docs/screenshots/04-export.png" alt="04 · 一键导出" /><br/>
<sub><b>一键导出</b> —— 微信（juice 内联 CSS）· X / 微博 / 小红书（modern-screenshot → 2× PNG → <code>ClipboardItem</code>）· 知乎（LaTeX 图片占位符）· 下载 <code>.html</code> · 下载 <code>.png</code>。直接粘贴，无需二次手动排版。</sub>
</td>
</tr>
<tr>
<td width="50%">
<img src="docs/screenshots/05-deck-mode.png" alt="05 · 幻灯片模式" /><br/>
<sub><b>幻灯片模式</b> —— 20 款主题演讲技能，包括瑞士国际（Helvetica 网格极简主义）、贵藏编辑（杂志墨色）、Open Slide Canvas（1920×1080 Agent 原生）、杂志 Web、小红书 pastel、Hermes Cyber、Replit 风格。←/→ 切换幻灯片，支持演讲者备注与 PDF 导出。</sub>
</td>
<td width="50%">
<img src="docs/screenshots/06-hyperframes.png" alt="06 · Hyperframes 视频帧" /><br/>
<sub><b>Hyperframes 分镜脚本</b> —— 10 个动态帧脚本（液态主视觉、NYT 数据图、便签流程图、故障标题、电影光泄漏、macOS 通知、品牌 Logo 片尾、文字光标 VFX、3D 设备样机…）符合 <a href="https://github.com/heygen-com/hyperframes">heygen-com/hyperframes</a> 规范；直接交给 Remotion 渲染 <code>.mp4</code>。</sub>
</td>
</tr>
</table>

## 快速开始

```bash
git clone https://github.com/nexu-io/html-anything
cd html-anything
pnpm install
pnpm -F @html-anything/next dev
# → http://localhost:3000
```

打开浏览器 → 顶部栏自动检测你已登录的编程 Agent CLI → 选择模板 → 粘贴内容 → ⌘+Enter。

**无需配置 API Key。** 直接复用你已登录的会话（Claude / Cursor / Codex / Gemini / Copilot 订阅均可直接使用）。

## 工作区结构

本仓库是一个轻量级 pnpm 工作区：

- `next/` 是完整的 Next.js 应用 (`@html-anything/next`)。
- `e2e/` 是浏览器测试包 (`@html-anything/e2e`)，也是 Playwright 用例的唯一真实数据源。
- 根目录管理 CI、文档和 `scripts/guard.ts`；根 `package.json` 故意不代理应用或测试命令。

从仓库根目录运行包命令：

```bash
pnpm exec tsx scripts/guard.ts
pnpm -F @html-anything/next dev
pnpm -F @html-anything/next typecheck
pnpm -F @html-anything/next test
pnpm -F @html-anything/next build
pnpm -F @html-anything/e2e typecheck
pnpm -F @html-anything/e2e test
```

## 支持的编程 Agent

启动时我们扫描 `PATH`（包括 `~/.local/bin`、`~/.bun/bin`、`/opt/homebrew/bin`、`~/.npm-global/bin` —— GUI 启动的 Node 通常遗漏这些目录）并展示所有识别到的 CLI：

| Agent | 检测二进制文件 | 调用方式 |
|---|---|---|
| **Claude Code** | `claude` | `claude -p --output-format stream-json` |
| **OpenAI Codex** | `codex` | `codex exec --json --sandbox workspace-write` |
| **Cursor Agent** | `cursor-agent` | `cursor-agent --print --output-format stream-json --force --trust` |
| **Gemini CLI** | `gemini` | `gemini --output-format stream-json --yolo` |
| **GitHub Copilot CLI** | `copilot` | `copilot --allow-all-tools --output-format json` |
| **OpenCode** | `opencode-cli` / `opencode` | `opencode run --format json --dangerously-skip-permissions -` |
| **Qwen Coder** | `qwen` | `qwen --yolo -` |
| **Aider** | `aider` | `aider --no-pretty --no-stream --yes-always --message-file -` |

> 检测策略与每个 CLI 的适配器结构直接借鉴自 [`nexu-io/open-design`](https://github.com/nexu-io/open-design) 和 [`multica-ai/multica`](https://github.com/multica-ai/multica)：一个特权进程启动 CLI，JSON-line 为通信协议，每个 CLI 在 [`next/src/lib/agents/argv.ts`](next/src/lib/agents/argv.ts) 中拥有独立的轻量级适配器。

如果你已在终端完成 `claude login` / `cursor login` / `gemini auth`，HTML Anything 会直接复用该会话。**无需提供第二份 API Key。**

## Skills

**位于 [`next/src/lib/templates/skills/`](next/src/lib/templates/skills/) 下的 **75 个技能**，每个均为一个遵循 Claude Code [`SKILL.md`](https://docs.anthropic.com/en/docs/claude-code/skills) 规范的文件夹，并扩展了元数据（`mode` · `scenario` · `surface` · `preview` · `design_system`）。

选择器使用的两个维度：

- **模式（mode）** —— `prototype`（Web / SaaS 落地页 / 仪表盘 / 数据报告 / 简历 / 文档）· `deck`（20 个横向滑动演示文稿）· `frame`（10 个 Hyperframes 动态帧）· `social`（4 种社交卡片格式）· `office`（PM / 工程 / 财务 / HR / 运营文档形式）。
- **场景（scenario）** —— `design` · `marketing` · `engineering` · `product` · `finance` · `hr` · `sale` · `personal`。用于在选择器中对技能进行分组。

### Web 原型与营销页（prototype 模式）

| Skill | 最佳适用场景 | 输出格式 |
|---|---|---|
| [`prototype-web`](next/src/lib/templates/skills/prototype-web/) | 通用 Web 原型（默认） | 单页 HTML，1440×900 桌面端 |
| [`saas-landing`](next/src/lib/templates/skills/saas-landing/) | SaaS 落地页 | Hero / 功能 / 定价 / CTA |
| [`waitlist-page`](next/src/lib/templates/skills/waitlist-page/) | 候补名单 / 早鸟访问页 | 极简表单 + 社交证明 |
| [`pricing-page`](next/src/lib/templates/skills/pricing-page/) | 定价页 | 多阶梯对比表格 |
| [`dashboard`](next/src/lib/templates/skills/dashboard/) | 管理后台 / 分析控制台 | 侧边栏 + 高密度数据布局 |
| [`docs-page`](next/src/lib/templates/skills/docs-page/) | 技术文档 | 3 列文档布局 |
| [`blog-post`](next/src/lib/templates/skills/blog-post/) | 长篇博客文章 | 编辑排版风格 |
| [`mobile-app`](next/src/lib/templates/skills/mobile-app/) | iOS / Android 原型 | iPhone 15 Pro 外框 |
| [`mobile-onboarding`](next/src/lib/templates/skills/mobile-onboarding/) | App 引导流程 | 启动页 · 价值主张 · 登录三件套 |
| [`gamified-app`](next/src/lib/templates/skills/gamified-app/) | 游戏化应用 | 任务 · XP · 等级三件套 |
| [`dating-web`](next/src/lib/templates/skills/dating-web/) | 社交 / 匹配仪表盘 | 左侧栏 · KPI · 30 日趋势图 |
| [`magazine-poster`](next/src/lib/templates/skills/magazine-poster/) | 单页杂志海报 | 1080×1920 |
| [`poster-hero`](next/src/lib/templates/skills/poster-hero/) | 营销海报 | 单页展示型海报 |
| [`web-proto-editorial`](next/src/lib/templates/skills/web-proto-editorial/) | 编辑风格 Web | 衬线显示字体 + 网格系统 |
| [`web-proto-brutalist`](next/src/lib/templates/skills/web-proto-brutalist/) | 粗野主义 Web | 硬边缘、黑白配色、反网格 |
| [`web-proto-soft`](next/src/lib/templates/skills/web-proto-soft/) | 柔和 / 暖色调 Web | 柔光阴影、圆角、温暖调色板 |
| [`article-magazine`](next/src/lib/templates/skills/article-magazine/) | 长篇杂志文章 | A4 / 长页排版 |
| [`digital-eguide`](next/src/lib/templates/skills/digital-eguide/) | 数字电子书指南 | 封面 + 章节跨页 |
| [`resume-modern`](next/src/lib/templates/skills/resume-modern/) | 极简简历 | A4 210×297mm |
| [`email-marketing`](next/src/lib/templates/skills/email-marketing/) | 品牌产品发布邮件 | 居中单列，表格回退兼容 |
| [`wireframe-sketch`](next/src/lib/templates/skills/wireframe-sketch/) | 手绘线框图 | 早期构思阶段 |

### 幻灯片（deck 模式，共 20 个技能）

| Skill | 最佳适用场景 |
|---|---|
| [`deck-swiss-international`](next/src/lib/templates/skills/deck-swiss-international/) | 瑞士国际风格幻灯片 |
| [`deck-guizang-editorial`](next/src/lib/templates/skills/deck-guizang-editorial/) | 杂志墨色编辑排版（源自 [op7418/guizang-ppt-skill](https://github.com/op7418/guizang-ppt-skill)） |
| [`deck-open-slide-canvas`](next/src/lib/templates/skills/deck-open-slide-canvas/) | 1920×1080 Agent 原生画布（源自 [1weiho/open-slide](https://github.com/1weiho/open-slide)） |
| [`deck-magazine-web`](next/src/lib/templates/skills/deck-magazine-web/) | 杂志风格 Web 幻灯片 |
| [`deck-hermes-cyber`](next/src/lib/templates/skills/deck-hermes-cyber/) | Hermes Cyber 霓虹奢华风 |
| [`deck-replit`](next/src/lib/templates/skills/deck-replit/) | Replit 风格产品演示 |
| [`deck-xhs-pastel`](next/src/lib/templates/skills/deck-xhs-pastel/) | 小红书 pastel 风格幻灯片 |
| [`deck-xhs-white`](next/src/lib/templates/skills/deck-xhs-white/) | 小红书纯白风格幻灯片 |
| [`deck-xhs-post`](next/src/lib/templates/skills/deck-xhs-post/) | 小红书单篇笔记幻灯片 |
| [`deck-tech-sharing`](next/src/lib/templates/skills/deck-tech-sharing/) | 技术分享幻灯片 |
| [`deck-product-launch`](next/src/lib/templates/skills/deck-product-launch/) | 产品发布会事件幻灯片 |
| [`deck-pitch`](next/src/lib/templates/skills/deck-pitch/) | 融资路演 |
| [`deck-blueprint`](next/src/lib/templates/skills/deck-blueprint/) | 蓝图 / 路线图 |
| [`deck-presenter-mode`](next/src/lib/templates/skills/deck-presenter-mode/) | 演讲者备注感知模式 |
| [`deck-course-module`](next/src/lib/templates/skills/deck-course-module/) | 课程模块幻灯片 |
| [`deck-dir-key-nav`](next/src/lib/templates/skills/deck-dir-key-nav/) | 方向键深度浏览导航 |
| [`deck-graphify-dark`](next/src/lib/templates/skills/deck-graphify-dark/) | 暗色、数据图表密集型幻灯片 |
| [`deck-obsidian-claude`](next/src/lib/templates/skills/deck-obsidian-claude/) | Obsidian / Claude 风格笔记 |
| [`deck-safety-alert`](next/src/lib/templates/skills/deck-safety-alert/) | 事件通报 / 安全简报 |
| [`deck-simple`](next/src/lib/templates/skills/deck-simple/) | 极简横向滑动幻灯片 |

### Hyperframes 视频帧、VFX 特效与设备样机（frame / vfx / mockup，共 12 个技能）

| Skill | 最佳适用场景 |
|---|---|
| [`frame-liquid-bg-hero`](next/src/lib/templates/skills/frame-liquid-bg-hero/) | 液态背景主视觉 |
| [`frame-data-chart-nyt`](next/src/lib/templates/skills/frame-data-chart-nyt/) | NYT 风格数据图表 |
| [`frame-flowchart-sticky`](next/src/lib/templates/skills/frame-flowchart-sticky/) | 便签流程图 |
| [`frame-glitch-title`](next/src/lib/templates/skills/frame-glitch-title/) | 故障艺术标题卡 |
| [`frame-light-leak-cinema`](next/src/lib/templates/skills/frame-light-leak-cinema/) | 电影光泄漏效果 |
| [`frame-macos-notification`](next/src/lib/templates/skills/frame-macos-notification/) | macOS 通知弹窗 |
| [`frame-logo-outro`](next/src/lib/templates/skills/frame-logo-outro/) | 品牌 Logo 片尾 |
| [`motion-frames`](next/src/lib/templates/skills/motion-frames/) | 通用动态设计帧 |
| [`video-hyperframes`](next/src/lib/templates/skills/video-hyperframes/) | Hyperframes 分镜脚本架构 |
| [`sprite-animation`](next/src/lib/templates/skills/sprite-animation/) | 像素 / 8-bit 动画 |
| [`vfx-text-cursor`](next/src/lib/templates/skills/vfx-text-cursor/) | 文字光标 VFX |
| [`mockup-device-3d`](next/src/lib/templates/skills/mockup-device-3d/) | 3D 设备外框样机 |

> 分镜脚本符合 [`heygen-com/hyperframes`](https://github.com/heygen-com/hyperframes) 规范，并直接交付给 [`remotion-dev/remotion`](https://github.com/remotion-dev/remotion) 渲染 `.mp4`。

### 社交分享卡片（social 模式）

| Skill | 最佳适用场景 |
|---|---|
| [`social-x-post-card`](next/src/lib/templates/skills/social-x-post-card/) | X / Twitter 引用卡（1600×900） |
| [`social-spotify-card`](next/src/lib/templates/skills/social-spotify-card/) | Spotify-Wrapped 风格卡片 |
| [`social-reddit-card`](next/src/lib/templates/skills/social-reddit-card/) | Reddit 帖子卡片 |
| [`social-carousel`](next/src/lib/templates/skills/social-carousel/) | 3 张一组 1080×1080 轮播图 |
| [`card-xiaohongshu`](next/src/lib/templates/skills/card-xiaohongshu/) | 小红书图文卡片 |
| [`card-twitter`](next/src/lib/templates/skills/card-twitter/) | Twitter 引用语录卡 |
| [`social-media-dashboard`](next/src/lib/templates/skills/social-media-dashboard/) | 社媒运营仪表盘 |
| [`social-media-matrix`](next/src/lib/templates/skills/social-media-matrix/) | 多平台内容矩阵 |

### 办公与运营文档（office / doc 模式）

| Skill | 场景 | 最佳适用场景 |
|---|---|---|
| [`doc-kami-parchment`](next/src/lib/templates/skills/doc-kami-parchment/) | personal | 暖羊皮纸编辑排版（源自 [tw93/kami](https://github.com/tw93/kami)） |
| [`pm-spec`](next/src/lib/templates/skills/pm-spec/) | product | PM 需求文档 + 决策日志 |
| [`team-okrs`](next/src/lib/templates/skills/team-okrs/) | product | OKR 评分表 |
| [`meeting-notes`](next/src/lib/templates/skills/meeting-notes/) | operation | 会议决策日志 |
| [`weekly-update`](next/src/lib/templates/skills/weekly-update/) | operation | 团队周度同步 |
| [`kanban-board`](next/src/lib/templates/skills/kanban-board/) | operation | 看板快照 |
| [`eng-runbook`](next/src/lib/templates/skills/eng-runbook/) | engineering | 故障应急手册 |
| [`finance-report`](next/src/lib/templates/skills/finance-report/) | finance | 高管财务摘要 |
| [`invoice`](next/src/lib/templates/skills/invoice/) | finance | 单页发票 |
| [`hr-onboarding`](next/src/lib/templates/skills/hr-onboarding/) | hr | 岗位入职计划 |
| [`data-report`](next/src/lib/templates/skills/data-report/) | finance / product | CSV/Excel → 可视化数据报告 |
| [`live-dashboard`](next/src/lib/templates/skills/live-dashboard/) | operation | 实时数据仪表盘 |
| [`flowai-team-dashboard`](next/src/lib/templates/skills/flowai-team-dashboard/) | operation | 团队工作流看板 |
| [`ppt-keynote`](next/src/lib/templates/skills/ppt-keynote/) | personal | 通用 Keynote 风格幻灯片 |

**新增一个技能只需添加一个文件夹。** 复制相似技能，编辑其 `SKILL.md` 元数据，重启 `pnpm -F @html-anything/next dev`，选择器即可显示。参见 [`CONTRIBUTING.md`](CONTRIBUTING.md) 了解合并 PR 的技能标准。

## 六大核心理念

### 1 · 我们不内置 Agent。你的已经足够好。

启动时浏览器调用 `/api/agents`。服务端扫描 `PATH` —— 包括 GUI 启动的 Node 通常遗漏的目录（`~/.local/bin`、`~/.bun/bin`、`/opt/homebrew/bin`、`~/.npm-global/bin`）并展示检测到的 CLI。每个 CLI 在 [`next/src/lib/agents/argv.ts`](next/src/lib/agents/argv.ts) 中仅有一个适配器（argv + stdin 协议 + 流解析器）。整套检测模型直接借鉴自 [`nexu-io/open-design`](https://github.com/nexu-io/open-design) 和 [`multica-ai/multica`]：一个特权进程启动 CLI，JSON-line 为通信协议。

### 2 · 技能是文件夹，而非插件。

遵循 Claude Code 的 [`SKILL.md` 规范](https://docs.anthropic.com/en/docs/claude-code/skills) —— `SKILL.md` + `assets/` + `references/` + `example.html`。将文件夹放入 [`next/src/lib/templates/skills/`](next/src/lib/templates/skills/)，重启 `pnpm -F @html-anything/next dev`，选择器即可显示。`deck-guizang-editorial` 直接源自 [`op7418/guizang-ppt-skill`](https://github.com/op7418/guizang-ppt-skill)，保留原始 LICENSE 与作者署名。

### 3 · 硬约束防止模型自由发挥（避免 AI 水化）。

每个模板均硬编码了以下规则：

- **CJK 优先字体栈** —— `Noto Sans/Serif SC` / source-han 用于中文，`Inter` / `Manrope` 用于拉丁字符。
- **8 px 基线网格** —— 所有间距、行高、字号均为 8 的倍数。
- **圆角 · 柔光阴影 · 禁用纯黑/纯白** —— 视觉去套路化。
- **色彩对比度 ≥ 4.5**，每个交互元素均具备真实的 `:focus` 状态。
- **必须使用用户真实数据**，严禁 lorem ipsum 占位符。

该规范借鉴自 [`alchaincyf/huashu-design`](https://github.com/alchaincyf/huashu-design) 的 Junior-Designer 模式 + 反 AI 水化检查清单。约束条件写入 Prompt —— 每个 `SKILL.md` 均包含这些规则。

### 4 · 流式渲染 = 看着 AI “作画”。

`POST /api/convert` 基于 SSE。Agent 的 stdout 为逐行 JSON；服务端提取文本增量并以 SSE 事件形式重发；客户端追加至 iframe 的 `srcdoc`。整体体验等同于在终端中实时观看 Agent 打字，只是产物是 HTML 而非 Markdown。**随时中断** —— 你无需为不想要的完整生成结果付费或等待。

### 5 · 一键导出 = 零二次排版。

- **微信公众号（WeChat MP）** —— `juice` 内联 CSS + `data-tool` 标记 → 粘贴至编辑器，样式端到端保留。
- **X / 微博 / 小红书** —— `modern-screenshot` 将 iframe 渲染为 2× PNG → `ClipboardItem` → 直接拖入编辑器。
- **知乎（Zhihu）** —— 同上逻辑，并将 `<mjx-container>` 替换为 `data-eeimg` LaTeX 图片占位符（知乎不支持实时渲染 KaTeX —— 数学公式必须为图片）。
- **下载 `.html`** / **下载 `.png`** —— 自包含单文件，随处可分享。

机制灵感源自 [`mdnice/markdown-nice`](https://github.com/mdnice/markdown-nice) 和 [`gcui-art/markdown-to-image`](https://github.com/gcui-art/markdown-to-image)。

### 6 · 沙箱 iframe = 安全且隔离。

用户生成的 HTML 始终在 `<iframe sandbox="allow-scripts allow-same-origin">` 内部渲染。第三方脚本（Tailwind CDN、Google Fonts、自定义动画）仍可执行，但 Cookie 和 localStorage 保留在 iframe 自身的 origin 中 —— 宿主页面无污染风险。打开开发者工具仅显示 iframe DOM，调试体验与独立 HTML 文件一致。

## 架构

```
┌─────────────────────── Browser (Next.js 16) ──────────────────────┐
│  Editor / upload · top-bar agent picker · template picker · iframe │
└─────────────┬──────────────────────────────────┬──────────────────┘
              │ ⌘+Enter                            │
              ▼                                    ▼
     ┌─────────────────────┐            ┌──────────────────────┐
     │  GET /api/agents    │            │  POST /api/convert   │
     │  scan PATH, list    │            │  SSE — spawn CLI     │
     │  installed CLIs     │            │  pipe stdin / stdout │
     └─────────────────────┘            └──────────┬───────────┘
                                                   │ spawn + stdin pipe
                                                   ▼
                                ┌────────────────────────────────────┐
                                │  Your local coding-agent CLI       │
                                │  claude / codex / cursor-agent /   │
                                │  gemini / copilot / opencode /     │
                                │  qwen / aider                      │
                                │  → reuses your existing session    │
                                └────────────────────────────────────┘
                                                   │
                                                   ▼
                                stdout JSON-line ──► SSE event
                                                   │
                                                   ▼
                              iframe srcdoc append (live)
                                                   │
                              ⌘+C copy → ClipboardItem
                              ⌘+S download → .html / .png
```

| Layer | Stack |
|---|---|
| Frontend | Next.js 16 App Router + Turbopack · React 19 · Tailwind v4 · zustand state |
| Server routes | `GET /api/agents` (detection) · `POST /api/convert` (SSE streaming spawn) |
| Agent transport | `child_process.spawn` · one stdin/stdout adapter per CLI ([`next/src/lib/agents/argv.ts`](next/src/lib/agents/argv.ts)) |
| Browser-side processing | `juice` (CSS inlining) · `modern-screenshot` (PNG export) · `xlsx` / `papaparse` (spreadsheet parsing) · `marked` + `highlight.js` (Markdown-compatible input) · `dompurify` (XSS defense) |
| Preview sandbox | `iframe[sandbox="allow-scripts allow-same-origin"]` + `srcdoc` |
| Export targets | `.html` standalone · `.png` high-DPI · `ClipboardItem` (text/html + image/png) · WeChat-compatible inlined CSS |
| Deploy | Local `pnpm -F @html-anything/next dev` · Vercel one-click for the web layer (agent stays local) |

## 导出目标

| Platform | Implementation | Paste behavior |
|---|---|---|
| **WeChat MP** | `juice` inlines CSS + `data-tool` markers | Paste into editor, zero re-formatting |
| **Zhihu** | Same as WeChat + `<mjx-container>` → `data-eeimg` LaTeX image placeholder | Equations render after upload |
| **X / Weibo / Xiaohongshu** | `modern-screenshot` → 2× PNG → `ClipboardItem` | Drop straight into the composer |
| **Download `.html`** | Single-file, inlined assets | Open anywhere with a browser |
| **Download `.png`** | High-DPI screenshot | Share anywhere |

## Roadmap

- [ ] **Multi-template compare preview** — generate four candidates of the same brief, pick the best one
- [ ] **Hyperframes → mp4** — one-click hand-off of frame scripts to Remotion for real video output
- [ ] **Shared design systems** — interop with [`nexu-io/open-design`](https://github.com/nexu-io/open-design) `DESIGN.md` assets
- [ ] **Template marketplace** — community-contributed prompts & examples
- [ ] **Browser extension** — select on any page → convert to HTML template
- [ ] **History / version diff / IndexedDB archive**
- [ ] **More export targets** — WeChat Channels · Douyin captions · Notion · Linear · Telegraph

## Status

Early but real. The closed loop — **detect agent → pick skill → SSE stream → sandboxed iframe preview → one-click export** — runs end-to-end against all 8 CLIs listed above. The skill library and the `SKILL.md` hard-constraints are where most of the leverage lives, and both are stable. The picker UX, design-system metadata, and the multi-template compare flow ship daily. If something looks broken on your machine, open an issue with the agent CLI you were using and the input — those are the bug reports that move things forward fastest.

| Surface | State |
|---|---|
| Agent detection (8 CLIs) | ✅ stable |
| Skill registry + picker (75 skills) | ✅ stable |
| SSE streaming render | ✅ stable |
| Sandboxed iframe preview | ✅ stable |
| One-click WeChat / X / Zhihu / `.html` / `.png` export | ✅ stable |
| CSV / Excel / JSON / SQL format auto-detect | ✅ stable |
| Multi-template compare (generate 4, pick 1) | 🛠 in progress |
| Hyperframes → `.mp4` one-click handoff to Remotion | 🛠 in progress |
| Browser extension (select on any page → convert) | ⏳ planned |
| History / version diff / IndexedDB archive | ⏳ planned |
| Skill marketplace (`install <github-repo>`) | ⏳ planned |

## Security

The Next API surface is the local-only side of the app — `/api/convert` spawns the user's coding-agent CLI with maximally permissive flags, `/api/deploy` writes credentialed config to disk. Both are intended for a single operator on a single machine. To prevent a malicious page from DNS-rebinding `attacker.example` to `127.0.0.1` and POSTing into those routes through the user's browser, every `/api/*` request is gated on a Host-header allowlist in [`next/src/middleware.ts`](next/src/middleware.ts).

| Setting | When to use |
|---|---|
| **Default (no env vars set)** | The common case — `next dev` / `next start` on your own machine. `127.0.0.1`, `localhost`, and `::1` Host headers (any port) are accepted. Everything else gets a 403 `{ "error": "Host not allowed" }`. |
| **`HTML_ANYTHING_ALLOWED_HOSTS=daemon.mirage.local,html-anything.lan`** | LAN / mDNS setup — you're reaching the app from another device on the same network and the browser dials a non-loopback hostname. Comma-separated; port-insensitive; case-insensitive. The default loopback set is still accepted on top of this. |
| **`HTML_ANYTHING_ALLOW_ANY_HOST=1`** | Reverse-proxy mode — Caddy / nginx / Cloudflare Tunnel is terminating the public hostname and forwarding to the app. The proxy is now responsible for Host policy. Loudly insecure if you set this without a trusted proxy in front, so it is not the default. |

Set the env var in whatever environment file your launcher reads (e.g. `next/.env.local`). The middleware is pinned to the Node runtime (`export const runtime = "nodejs"` in [`next/src/middleware.ts`](next/src/middleware.ts)) so `process.env` is read per-request — Edge middleware can inline `process.env.*` at build time, which would silently break operator overrides set after `next build`. The validation is unit-tested in [`next/src/lib/security/host-validation.test.ts`](next/src/lib/security/host-validation.test.ts) and the loopback-still-works dev path is exercised in the Playwright spec at [`e2e/ui/host-validation.spec.ts`](e2e/ui/host-validation.spec.ts).

## Contributing

Issues, PRs, new skills, new agent adapters, new export targets, and translations are all welcome. The highest-leverage contributions are usually **one folder, one Markdown file, or one PR-sized adapter** — small surface area, big leverage. Pick the slot that matches what you want to add:

- **Add a skill** — drop a folder into [`next/src/lib/templates/skills/`](next/src/lib/templates/skills/) with `SKILL.md` + `example.html` (+ optional `assets/` and `references/`). The picker auto-discovers it after `pnpm -F @html-anything/next dev` restart. The `SKILL.md` frontmatter has to set `mode` · `scenario` · `surface` · `preview` · `design_system` — copy a neighbour and edit.
- **Wire up a new coding-agent CLI** — one entry in [`next/src/lib/agents/argv.ts`](next/src/lib/agents/argv.ts) covering: detection binary, argv builder, stdin/stdout protocol, stream parser. Detection is exercised by [`next/src/app/api/agents/`](next/src/app/api/agents/) and the spawn loop by [`next/src/app/api/convert/`](next/src/app/api/convert/).
- **Add an export target** — drop a module under [`next/src/lib/export/`](next/src/lib/export/) (next to `wechat.ts` / `image.ts` / `clipboard.ts`) and add the button to the export menu. WeChat Channels · Douyin captions · Notion · Linear · Telegraph · RSS are all open.
- **Sharpen a `SKILL.md`** — strengthen the hard-constraints (CJK font stack, 8 px baseline, contrast ≥ 4.5, must-use-real-data), add a 5-dimensional self-critique, swap in a better palette. Anti-AI-slop discipline is the most underrated PR shape we accept.
- **Translations & docs** — [`README.zh-CN.md`](README.zh-CN.md) and [`CONTRIBUTING.zh-CN.md`](CONTRIBUTING.zh-CN.md) are kept in parallel with the English files; please update both.

Full walkthrough, bar-for-merging, code style, and what we **don't** accept → [`CONTRIBUTING.md`](CONTRIBUTING.md) ([简体中文](CONTRIBUTING.zh-CN.md)).

## References & lineage

Every external project this repo borrows from — what we take from each, and where it lands in the tree.

| Project | Role here |
|---|---|
| [**`nexu-io/open-design`**](https://github.com/nexu-io/open-design) | The agent-detection layer, the `DESIGN.md` design-system schema, and the `SKILL.md` skill protocol. [`next/src/lib/agents/argv.ts`](next/src/lib/agents/argv.ts) and [`next/src/lib/templates/skills/`](next/src/lib/templates/skills/) mirror this architecture verbatim. |
| [**`multica-ai/multica`**](https://github.com/multica-ai/multica) | Daemon-and-runtime architecture: one privileged process spawns CLIs, JSON-line is the wire protocol, every CLI gets a thin per-adapter shape. |
| [**`alchaincyf/huashu-design`**](https://github.com/alchaincyf/huashu-design) | Anti-AI-slop discipline — Junior-Designer mode, 5-step brand-asset protocol, contrast-≥-4.5 / 8 px baseline-grid / must-use-real-data rules. Hard-coded into every [`SKILL.md`](next/src/lib/templates/skills/) frontmatter. |
| [`alchaincyf/huashu-md-html`](https://github.com/alchaincyf/huashu-md-html) | Proof that end-to-end WeChat / Zhihu paste-compatibility is solvable. Reference for [`next/src/lib/export/wechat.ts`](next/src/lib/export/wechat.ts). |
| [`mdnice/markdown-nice`](https://github.com/mdnice/markdown-nice) | `juice`-inlined-CSS pipeline → WeChat / Zhihu paste with zero re-formatting. Drives [`next/src/lib/export/wechat.ts`](next/src/lib/export/wechat.ts). |
| [`mdnice/markdown-resume`](https://github.com/mdnice/markdown-resume) | A4-formatted résumé inspiration → [`resume-modern`](next/src/lib/templates/skills/resume-modern/). |
| [`gcui-art/markdown-to-image`](https://github.com/gcui-art/markdown-to-image) | iframe → high-DPI PNG export, replicated with `modern-screenshot` in [`next/src/lib/export/image.ts`](next/src/lib/export/image.ts). |
| [**`op7418/guizang-ppt-skill`**](https://github.com/op7418/guizang-ppt-skill) | Magazine-ink editorial deck integrated verbatim as [`deck-guizang-editorial`](next/src/lib/templates/skills/deck-guizang-editorial/) and the Swiss variant [`deck-swiss-international`](next/src/lib/templates/skills/deck-swiss-international/). Original LICENSE + authorship preserved. |
| [**`tw93/kami`**](https://github.com/tw93/kami) | Warm-parchment monochrome editorial document system → [`doc-kami-parchment`](next/src/lib/templates/skills/doc-kami-parchment/). |
| [**`1weiho/open-slide`**](https://github.com/1weiho/open-slide) | 1920×1080 agent-native canvas convention → [`deck-open-slide-canvas`](next/src/lib/templates/skills/deck-open-slide-canvas/). |
| [`heygen-com/hyperframes`](https://github.com/heygen-com/hyperframes) | Frame-script schema for the entire `frame-*` / `vfx-*` / `mockup-*` / `social-*` family. Output hands straight off to Remotion to render `.mp4`. |
| [`remotion-dev/remotion`](https://github.com/remotion-dev/remotion) | Target renderer for Hyperframes frame scripts. |
| [`jimliu/baoyu-skills`](https://github.com/jimliu/baoyu-skills) | Practical skills collection — reference catalog for picker categorization. |

Each bundled upstream skill retains its original LICENSE and authorship inside its own `next/src/lib/templates/skills/<skill>/` folder.

## Stay in the loop

Follow [**@nexudotio**](https://x.com/nexudotio) on X for release notes, new skills, and the occasional behind-the-scenes thread on what's shipping next. The [HTML Anything Discord channel](https://discord.gg/keeVPMrueT) is where demos, template requests, export/debugging questions, and bigger community conversations happen — run by the upstream `open-design` team.

## Contributors

Thanks to everyone who has filed an issue, opened a PR, or added a skill / agent adapter / export target. Every real contribution counts, and the wall below is the easiest way to say so out loud.

<a href="https://github.com/nexu-io/html-anything/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=nexu-io/html-anything" alt="HTML Anything contributors" />
</a>

If you've shipped your first PR — welcome. The [`good-first-issue` / `help-wanted`](https://github.com/nexu-io/html-anything/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22%2C%22help+wanted%22) labels are the entry point.

## Star History

<a href="https://star-history.com/#nexu-io/html-anything&Date">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=nexu-io/html-anything&type=Date&theme=dark" />
    <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/svg?repos=nexu-io/html-anything&type=Date" />
    <img alt="HTML Anything star history" src="https://api.star-history.com/svg?repos=nexu-io/html-anything&type=Date" />
  </picture>
</a>

If the curve bends up, that's the signal we look for. ★ this repo to push it.

## License

Apache-2.0 © 2026 HTML Anything contributors. See [`LICENSE`](LICENSE).

Bundled work retains its original license and authorship attribution — see the per-skill `LICENSE` / `README.md` inside each `next/src/lib/templates/skills/<skill>/` folder for what it inherits from upstream.
<div align="center">

# Garden Skills

**精心策划的、可直接投入生产的 [Agent Skills（智能体技能）](https://support.claude.com/en/articles/12512176-what-are-skills) 集合，适用于 Claude Code、Cursor、Codex 及其他 AI 编程智能体。**

<a id="skills-gallery"></a>

<table>
<tr>
<td width="50%" valign="top">
<a href="#web-video-presentation"><img src="https://cdn.jsdelivr.net/gh/ConardLi/assets@main/imgs/web-video-presentation-skill.webp" alt="Web Video Presentation Skill" width="100%"></a>
<br/><a href="#web-video-presentation"><strong>web-video-presentation</strong></a>
<br/><sub>Web 视频 / 演示</sub>
</td>
<td width="50%" valign="top">
<a href="#web-design-engineer"><img src="https://cdn.jsdelivr.net/gh/ConardLi/assets@main/imgs/web-design-skill.webp" alt="Web Design Skill" width="100%"></a>
<br/><a href="#web-design-engineer"><strong>web-design-engineer</strong></a>
<br/><sub>设计 / 前端开发</sub>
</td>
</tr>
<tr>
<td width="50%" valign="top">
<a href="#gpt-image-2"><img src="https://cdn.jsdelivr.net/gh/ConardLi/assets@main/imgs/gpt-image-2-skill.webp" alt="GPT Image 2 Skill" width="100%"></a>
<br/><a href="#gpt-image-2"><strong>gpt-image-2</strong></a>
<br/><sub>图像生成 / 提示词工程</sub>
</td>
<td width="50%" valign="top">
<a href="#kb-retriever"><img src="https://cdn.jsdelivr.net/gh/ConardLi/assets@main/imgs/kb-retriever-skill.webp" alt="KB Retriever Skill" width="100%"></a>
<br/><a href="#kb-retriever"><strong>kb-retriever</strong></a>
<br/><sub>本地知识检索</sub>
</td>
</tr>
</table>

[![License: MIT](https://img.shields.io/github/license/ConardLi/garden-skills?style=flat-square&color=blue)](./LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/ConardLi/garden-skills?style=flat-square)](https://github.com/ConardLi/garden-skills/stargazers)
[![PRs welcome](https://img.shields.io/badge/PRs-welcome-brightgreen?style=flat-square)](#contributing)
[![Skills count](https://img.shields.io/badge/skills-4-orange?style=flat-square)](#skills-gallery)
[![Spec](https://img.shields.io/badge/spec-SKILL.md-black?style=flat-square)](https://agentskills.io)

[English](./README.md) · [中文文档](./README.zh-CN.md) · [日本語](./README.ja-JP.md)

</div>

---

## 目录

| 安装 | 使用 | 贡献 |
|---|---|---|
| [安装](#install)<br>[`skills` CLI（命令行工具）](#option-a--skills-cli-npx)<br>[Claude Code 插件市场](#option-b--claude-code-plugin-marketplace)<br>[GitHub Release 锁定的 `.zip`](#option-c--pinned-zip-from-releases)<br>[手动复制](#option-d--manual-copy-into-your-project)<br>[Git 子模块](#option-e--git-submodule) | [兼容性](#compatibility)<br>什么是技能？（What is a Skill?）| [参与贡献](#contributing)<br>[鸣谢](#acknowledgments)<br>[许可证](#license) |

---

### [`web-video-presentation`](./skills/web-video-presentation)

![Web Video Presentation Skill](https://cdn.jsdelivr.net/gh/ConardLi/assets@main/imgs/web-video-presentation-skill.webp)

**类别：** Web 视频 / 演示工程  
**适用场景：** 将脚本、文章、课程、产品演示和演讲转化为支持点击交互的 16:9 网页版幻灯片，并可直接录屏生成电影级视频。

`web-video-presentation` 构建可直接用于录屏的 Vite + React + TypeScript 幻灯片项目，其交互方式类似专业视频制作工作台。工作流将原始文章自动转化为配音脚本，将脚本节拍映射为全屏场景，在关键节点暂停等待确认，并可在视觉大纲获批后选择性地合成配音音频。

亮点：

- 固定 1920×1080 舞台尺寸，自适应视口缩放以确保录屏画面稳定
- 点击/键盘驱动的 `(章节, 步骤)` 光标控制，每个视觉步骤严格对应一个配音节拍
- 强制协作检查点：脚本、主题、大纲、实现模式及可选音频均需人工确认后方可继续
- 隐藏式悬停进度控件，确保录屏时界面保持整洁无干扰
- 基于 **23 套内置主题**的 Token 架构，每套均具备独特设计语言——涵盖编辑排版、终端风格、工程风、瑞士国际主义等
- **可插拔 TTS（文本转语音）** —— 厂商无关的音频运行器；内置 **两套提供商** (MiniMax `mmx-cli` + OpenAI TTS via curl)，并提供 ElevenLabs / edge-tts / Azure / Google Cloud / macOS `say` 的接口契约与即贴即用代码片段
- 预置包含可复用舞台组件和录屏指南的 Vite + React + TypeScript 项目脚手架

<table>
<tr>
<td align="center" width="25%"><a href="./skills/web-video-presentation/README.md#theme-gallery"><img src="https://cdn.jsdelivr.net/gh/ConardLi/assets@main/imgs/web-video/creative-voltage.webp" alt="creative-voltage preview" /></a><br /><sub><code>creative-voltage</code><br />创意演讲</sub></td>
<td align="center" width="25%"><a href="./skills/web-video-presentation/README.md#theme-gallery"><img src="https://cdn.jsdelivr.net/gh/ConardLi/assets@main/imgs/web-video/blueprint.webp" alt="blueprint preview" /></a><br /><sub><code>blueprint</code><br />技术架构</sub></td>
<td align="center" width="25%"><a href="./skills/web-video-presentation/README.md#theme-gallery"><img src="https://cdn.jsdelivr.net/gh/ConardLi/assets@main/imgs/web-video/swiss-ikb.webp" alt="swiss-ikb preview" /></a><br /><sub><code>swiss-ikb</code><br />数据报告</sub></td>
<td align="center" width="25%"><a href="./skills/web-video-presentation/README.md#theme-gallery"><img src="https://cdn.jsdelivr.net/gh/ConardLi/assets@main/imgs/web-video/chalk-garden.webp" alt="chalk-garden preview" /></a><br /><sub><code>chalk-garden</code><br />科普讲解</sub></td>
</tr>
</table>

<a href="./skills/web-video-presentation/README.md#theme-gallery"><img src="https://cdn.jsdelivr.net/gh/ConardLi/assets@main/imgs/web-video/gallery.webp" alt="Theme gallery — 23 built-in themes for web-video-presentation" /></a>

<sub>↑ 一览全部 23 套主题 —— <a href="./skills/web-video-presentation/README.md#theme-gallery"><b>打开完整画廊</b></a> 查看实时 16:9 预览、设计语言说明及适用场景标签。</sub>

链接：[README](./skills/web-video-presentation/README.md) · [SKILL.md](./skills/web-video-presentation/SKILL.md) · <!-- DOWNLOAD:web-video-presentation:start -->[下载 v1.2.1 .zip](https://github.com/ConardLi/garden-skills/releases/download/web-video-presentation-v1.2.1/web-video-presentation-1.2.1.zip)<!-- DOWNLOAD:web-video-presentation:end -->

---

### [`web-design-engineer`](./skills/web-design-engineer)

![Web Design Skill](https://cdn.jsdelivr.net/gh/ConardLi/assets@main/imgs/web-design-skill.webp)

**类别：** 设计 / 前端开发  
**适用场景：** 网页、落地页（Landing Page）、仪表盘、交互原型、HTML 幻灯片、动画、UI 样机、数据可视化及设计系统探索。

`web-design-engineer` 将 AI 生成的网页作品从“仅能运行”提升为经过精心打磨、具有明确设计意图且视觉印象深刻的优质前端代码。它将智能体视为设计工程师：先理解产品上下文，再声明设计规范，展示早期 v0 版本，构建完整体验，最后验证结果。

亮点：

- 定义六步设计工作流：需求分析 → 上下文理解 → 设计规范声明 → v0 原型 → 全量开发 → 结果验证
- 通过反套路（Anti-Cliché）黑名单和更强的视觉判断力，突破通用 AI UI 模式
- 内置 **设计方向顾问（六大差异化流派）+ 25 套锚定风格配方**（Linear / Aesop / Pentagram / Bloomberg / Stripe Press / Mid-Century 等），每份配方均附带具体的调色板、排版规范、标志性手法及反模式，可直接粘贴至设计规范声明中
- 覆盖 HTML / CSS / JavaScript / React 原型开发，提供响应式布局、动效与交互打磨指南
- 包含内联 React + Babel、CSS Token、`oklch()` 色彩系统、容器查询及减少动态效果处理的实用实现规范
- 提供高级模式参考：设备外框、幻灯片引擎、动画时间轴、仪表盘及其他可复用网页组件

<table>
<tr>
<td align="center" width="25%"><a href="./skills/web-design-engineer/README.md#style-recipe-gallery"><img src="https://cdn.jsdelivr.net/gh/ConardLi/assets@main/imgs/web-design/aesop.webp" alt="aesop preview" /></a><br /><sub><code>aesop</code><br />药房风格页面</sub></td>
<td align="center" width="25%"><a href="./skills/web-design-engineer/README.md#style-recipe-gallery"><img src="https://cdn.jsdelivr.net/gh/ConardLi/assets@main/imgs/web-design/muji-kenya-hara.webp" alt="muji-kenya-hara preview" /></a><br /><sub><code>muji-kenya-hara</code><br />产品目录册</sub></td>
<td align="center" width="25%"><a href="./skills/web-design-engineer/README.md#style-recipe-gallery"><img src="https://cdn.jsdelivr.net/gh/ConardLi/assets@main/imgs/web-design/monocle-magazine.webp" alt="monocle-magazine preview" /></a><br /><sub><code>monocle-magazine</code><br />杂志内容页</sub></td>
<td align="center" width="25%"><a href="./skills/web-design-engineer/README.md#style-recipe-gallery"><img src="https://cdn.jsdelivr.net/gh/ConardLi/assets@main/imgs/web-design/stripe-press.webp" alt="stripe-press preview" /></a><br /><sub><code>stripe-press</code><br />图书详情页</sub></td>
</tr>
<tr>
<td align="center" width="25%"><a href="./skills/web-design-engineer/README.md#style-recipe-gallery"><img src="https://cdn.jsdelivr.net/gh/ConardLi/assets@main/imgs/web-design/bloomberg-terminal.webp" alt="bloomberg-terminal preview" /></a><br /><sub><code>bloomberg-terminal</code><br />交易仪表盘</sub></td>
<td align="center" width="25%"><a href="./skills/web-design-engineer/README.md#style-recipe-gallery"><img src="https://cdn.jsdelivr.net/gh/ConardLi/assets@main/imgs/web-design/linear.webp" alt="linear preview" /></a><br /><sub><code>linear</code><br />开发者工具落地页</sub></td>
<td align="center" width="25%"><a href="./skills/web-design-engineer/README.md#style-recipe-gallery"><img src="https://cdn.jsdelivr.net/gh/ConardLi/assets@main/imgs/web-design/vercel-mesh.webp" alt="vercel-mesh preview" /></a><br /><sub><code>vercel-mesh</code><br />部署首屏大图</sub></td>
<td align="center" width="25%"><a href="./skills/web-design-engineer/README.md#style-recipe-gallery"><img src="https://cdn.jsdelivr.net/gh/ConardLi/assets@main/imgs/web-design/tufte-dataink.webp" alt="tufte-dataink preview" /></a><br /><sub><code>tufte-dataink</code><br />数据叙事图表</sub></td>
</tr>
<tr>
<td align="center" width="25%"><a href="./skills/web-design-engineer/README.md#style-recipe-gallery"><img src="https://cdn.jsdelivr.net/gh/ConardLi/assets@main/imgs/web-design/mid-century-modern.webp" alt="mid-century-modern preview" /></a><br /><sub><code>mid-century-modern</code><br />海报致敬风</sub></td>
<td align="center" width="25%"><a href="./skills/web-design-engineer/README.md#style-recipe-gallery"><img src="https://cdn.jsdelivr.net/gh/ConardLi/assets@main/imgs/web-design/y2k-retrofuturism.webp" alt="y2k-retrofuturism preview" /></a><br /><sub><code>y2k-retrofuturism</code><br />Y2K 门户风</sub></td>
<td align="center" width="25%"><a href="./skills/web-design-engineer/README.md#style-recipe-gallery"><img src="https://cdn.jsdelivr.net/gh/ConardLi/assets@main/imgs/web-design/bloomberg-businessweek-turley.webp" alt="bloomberg-businessweek-turley preview" /></a><br /><sub><code>businessweek-turley</code><br />编辑封面设计</sub></td>
<td align="center" width="25%"><a href="./skills/web-design-engineer/README.md#style-recipe-gallery"><img src="https://cdn.jsdelivr.net/gh/ConardLi/assets@main/imgs/web-design/active-theory.webp" alt="active-theory preview" /></a><br /><sub><code>active-theory</code><br />电影级发布页</sub></td>
</tr>
</table>

<sub>↑ 展示 25 套风格配方中的 12 款 —— <a href="./skills/web-design-engineer/README.md#style-recipe-gallery"><b>打开完整画廊</b></a> 查看全部工作流（药房页面、交易终端、杂志封面、Y2K 门户、复古海报等），附带标志性手法与适用场景标签。</sub>

链接：[README](./skills/web-design-engineer/README.md) · [SKILL.md](./skills/web-design-engineer/SKILL.md) · [Website](./website/web-design-website) · [Demo](./demo/web-design-demo) · <!-- DOWNLOAD:web-design-engineer:start -->[下载 v1.2.1 .zip](https://github.com/ConardLi/garden-skills/releases/download/web-design-engineer-v1.2.1/web-design-engineer-1.2.1.zip)<!-- DOWNLOAD:web-design-engineer:end -->

---

### [`gpt-image-2`](./skills/gpt-image-2)

![GPT Image 2 Skill](https://cdn.jsdelivr.net/gh/ConardLi/assets@main/imgs/gpt-image-2-skill.webp)

**类别：** 图像生成 / 提示词工程  
**适用场景：** 海报、UI 样机、产品视觉图、信息图表、学术插图、技术架构图、漫画、头像、故事板、品牌看板及图像编辑工作流。

`gpt-image-2` 是专注于 GPT Image 2 及兼容 OpenAI 的图像 API 的生成技能。它设计用于适配不同智能体环境：完全本地的 Garden 生成、宿主原生图像工具委托，或在无图像工具时的纯提示词顾问模式。

亮点：

- 支持三种运行模式：**A 模式（Garden 本地）**、**B 模式（宿主原生委托）**、**C 模式（仅提示词顾问）**
- 每项任务启动时自动检测模式，避免静默选择错误的执行路径
- 在 `references/` 下提供 18 类视觉分类与 79 个结构化提示词模板
- 通过专用工作流和脚本覆盖图像生成与编辑全流程
- 在 Garden 模式下将提示词与生成结果保存至 `garden-gpt-image-2/`，便于复用、审查与版本管理

#### 精选实战案例

<table>
  <tr>
    <td width="25%" align="center">
      <a href="https://gpt-image2.mmh1.top/#/case/editing-workflows%2Fbackground-replacement%2F1"><img src="https://cdn.jsdelivr.net/gh/ConardLi/gpt-image-2-101@main/public/case/editing-workflows/background-replacement/1-thumb.webp" alt="Background replacement case" width="100%"></a><br/>
      <strong><code>background-replacement</code></strong><br/>
      <sub>肖像编辑配合时代广场重打光。</sub>
    </td>
    <td width="25%" align="center">
      <a href="https://gpt-image2.mmh1.top/#/case/ui-mockups%2Fchat-interface-scene%2F3"><img src="https://cdn.jsdelivr.net/gh/ConardLi/gpt-image-2-101@main/public/case/ui-mockups/chat-interface-scene/3-thumb.webp" alt="AI assistant UI mockup case" width="100%"></a><br/>
      <strong><code>chat-interface-scene</code></strong><br/>
      <sub>Claude 风格助手产品截图。</sub>
    </td>
    <td width="25%" align="center">
      <a href="https://gpt-image2.mmh1.top/#/case/ui-mockups%2Flive-commerce-ui%2F1"><img src="https://cdn.jsdelivr.net/gh/ConardLi/gpt-image-2-101@main/public/case/ui-mockups/live-commerce-ui/1-thumb.webp" alt="Live commerce UI case" width="100%"></a><br/>
      <strong><code>live-commerce-ui</code></strong><br/>
      <sub>明星直播带货界面。</sub>
    </td>
    <td width="25%" align="center">
      <a href="https://gpt-image2.mmh1.top/#/case/ui-mockups%2Fproduct-card-overlay%2F1"><img src="https://cdn.jsdelivr.net/gh/ConardLi/gpt-image-2-101@main/public/case/ui-mockups/product-card-overlay/1-thumb.webp" alt="Product card overlay case" width="100%"></a><br/>
      <strong><code>product-card-overlay</code></strong><br/>
      <sub>护肤品类落地页首屏大图。</sub>
    </td>
  </tr>
  <tr>
    <td width="25%" align="center">
      <a href="https://gpt-image2.mmh1.top/#/case/infographics%2Fbento-grid-infographic%2F1"><img src="https://cdn.jsdelivr.net/gh/ConardLi/gpt-image-2-101@main/public/case/infographics/bento-grid-infographic/1-thumb.webp" alt="Bento grid infographic case" width="100%"></a><br/>
      <strong><code>bento-grid-infographic</code></strong><br/>
      <sub>iPhone 16 Pro 高信息密度解析图。</sub>
    </td>
    <td width="25%" align="center">
      <a href="https://gpt-image2.mmh1.top/#/case/technical-diagrams%2Fsystem-architecture%2F1"><img src="https://cdn.jsdelivr.net/gh/ConardLi/gpt-image-2-101@main/public/case/technical-diagrams/system-architecture/1-thumb.webp" alt="System architecture diagram case" width="100%"></a><br/>
      <strong><code>system-architecture</code></strong><br/>
      <sub>多租户 AI SaaS 生产环境架构图。</sub>
    </td>
    <td width="25%" align="center">
      <a href="https://gpt-image2.mmh1.top/#/case/slides-and-visual-docs%2Fdense-explainer-slides%2F2"><img src="https://cdn.jsdelivr.net/gh/ConardLi/gpt-image-2-101@main/public/case/slides-and-visual-docs/dense-explainer-slides/2-thumb.webp" alt="Dense explainer slide case" width="100%"></a><br/>
      <strong><code>dense-explainer-slides</code></strong><br/>
      <sub>一页纸讲清 AI Agent 机制。</sub>
    </td>
    <td width="25%" align="center">
      <a href="https://gpt-image2.mmh1.top/#/case/maps%2Ffood-map%2F1"><img src="https://cdn.jsdelivr.net/gh/ConardLi/gpt-image-2-101@main/public/case/maps/food-map/1-thumb.webp" alt="Food map case" width="100%"></a><br/>
      <strong><code>food-map</code></strong><br/>
      <sub>城市漫步编辑精选美食指南。</sub>
    </td>
  </tr>
  <tr>
    <td width="25%" align="center">
      <a href="https://gpt-image2.mmh1.top/#/case/product-visuals%2Fexploded-view-poster%2F2"><img src="https://cdn.jsdelivr.net/gh/ConardLi/gpt-image-2-101@main/public/case/product-visuals/exploded-view-poster/2-thumb.webp" alt="Exploded product poster case" width="100%"></a><br/>
      <strong><code>exploded-view-poster</code></strong><br/>
      <sub>Vision Pro 2 光学与算力拆解。</sub>
    </td>
    <td width="25%" align="center">
      <a href="https://gpt-image2.mmh1.top/#/case/academic-figures%2Fneural-network-architecture%2F2"><img src="https://cdn.jsdelivr.net/gh/ConardLi/gpt-image-2-101@main/public/case/academic-figures/neural-network-architecture/2-thumb.webp" alt="Neural network architecture case" width="100%"></a><br/>
      <strong><code>neural-network-architecture</code></strong><br/>
      <sub>论文用 ViT-B/16 模型插图。</sub>
    </td>
    <td width="25%" align="center">
      <a href="https://gpt-image2.mmh1.top/#/case/branding-and-packaging%2Fcosmetic-packaging%2F1"><img src="https://cdn.jsdelivr.net/gh/ConardLi/gpt-image-2-101@main/public/case/branding-and-packaging/cosmetic-packaging/1-thumb.webp" alt="Cosmetic packaging case" width="100%"></a><br/>
      <strong><code>cosmetic-packaging</code></strong><br/>
      <sub>高端护肤礼盒构图。</sub>
    </td>
    <td width="25%" align="center">
      <a href="https://gpt-image2.mmh1.top/#/case/storyboards-and-sequences%2Fanime-key-visual%2F1"><img src="https://cdn.jsdelivr.net/gh/ConardLi/gpt-image-2-101@main/public/case/storyboards-and-sequences/anime-key-visual/1-thumb.webp" alt="Anime key visual case" width="100%"></a><br/>
      <strong><code>anime-key-visual</code></strong><br/>
      <sub>游戏发布主视觉，含安全裁剪布局。</sub>
    </td>
  </tr>
</table>

<sub>↑ 从 160+ 公开案例库中精选的 12 款 —— <a href="./skills/gpt-image-2/README.md#case-gallery"><b>打开技能画廊</b></a> 查看更多模板，或浏览 <a href="https://gpt-image2.mmh1.top/#/case">在线网站</a>。</sub>

链接：[README](./skills/gpt-image-2/README.md) · [SKILL.md](./skills/gpt-image-2/SKILL.md) · [Website](./website/gpt-image2-website) · <!-- DOWNLOAD:gpt-image-2:start -->[下载 v1.0.3 .zip](https://github.com/ConardLi/garden-skills/releases/download/gpt-image-2-v1.0.3/gpt-image-2-1.0.3.zip)<!-- DOWNLOAD:gpt-image-2:end -->

---

### [`kb-retriever`](./skills/kb-retriever)

![Kb Retriever Skill](https://cdn.jsdelivr.net/gh/ConardLi/assets@main/imgs/kb-retriever-skill.webp)

**类别：** 检索 / 本地知识库  
**适用场景：** 基于本地 `knowledge/` 目录回答问题、搜索结构化文档，并从 Markdown、文本、PDF 和 Excel 文件中提取证据，同时避免撑爆智能体上下文。

`kb-retriever` 是一个以谨慎、渐进式搜索为核心的本地知识库检索工具。它不会一次性加载整个文件，而是通过层级索引文件导航、缩小候选范围、正确处理复杂文件格式，并附带来源引用进行回答。

亮点：

- 使用分层 `data_structure.md` 文件在搜索内容前快速定位知识库结构
- 对 PDF 和 Excel 文件强制执行 **“先学习后处理”** 规则，提取或分析前先调用内置参考文档
- 结合精确关键词搜索、本地窗口读取、同义词扩展与迭代优化
- 将检索限制在最多 5 轮搜索，确保探索过程可控且高效
- 内置 `grep`、`pdftotext`、`pdfplumber` 和 `pandas` 工作流，支持带来源引用的答案格式化

链接：[README](./skills/kb-retriever/README.md) · [SKILL.md](./skills/kb-retriever/SKILL.md) · <!-- DOWNLOAD:kb-retriever:start -->[下载 v1.0.0 .zip](https://github.com/ConardLi/garden-skills/releases/download/kb-retriever-v1.0.0/kb-retriever-1.0.0.zip)<!-- DOWNLOAD:kb-retriever:end -->

---

## 安装

提供五种支持的安装路径。请根据你的技术栈选择最合适的一种：

| # | 方式 | 适用场景 | 是否锁定版本？ |
|---|---|---|---|
| A | [`skills` CLI (`npx skills add`)](#option-a--skills-cli-npx) | 任意智能体，一键安装，按需选择技能 | ✅ 通过标签 URL |
| B | [Claude Code 插件市场](#option-b--claude-code-plugin-marketplace) | 希望订阅捆绑插件包的 Claude Code 用户 | ✅ 通过市场版本 |
| C | [GitHub Release 锁定的 `.zip`](#option-c--pinned-zip-from-releases) | CI / 离线环境 / 可复现安装 | ✅✅（不可变） |
| D | [`git clone` 后手动复制](#option-d--manual-copy-into-your-project) | 本地 Fork 或修改技能本身 | ❌（跟随 `main`） |
| E | [Git 子模块](#option-e--git-submodule) | 引入大型项目并追踪上游更新 | ✅ 通过子模块 SHA |

> 上述每个技能部分在“Links”行中均提供了 **下载 v<版本> .zip** 链接，指向当前锁定的发布制品。这些 URL 会在每次发布时由 [`scripts/release/update-readme.mjs`](./scripts/release/update-readme.mjs) 自动重写，因此始终指向最新的不可变版本。

### Option A · `skills` CLI (npx)

最快的跨智能体安装路径。使用标准的 [`npx skills` CLI](https://www.npmjs.com/package/skills)，它会自动检测你的智能体（Claude Code、Cursor、Codex 等）并将技能放入正确的目录。

```bash
# 安装全部四个技能（最新版）
npx skills add ConardLi/garden-skills

# 仅安装单个技能（最新版）
npx skills add ConardLi/garden-skills -s web-design-engineer

# 全局安装 (~/.skills) 而非按项目安装 (./.skills)
npx skills add ConardLi/garden-skills -s gpt-image-2 --global

# 指定目标智能体
npx skills add ConardLi/garden-skills -s kb-retriever -a claude-code
```

> **默认使用 `main` 分支的最新提交。** 这通常是你的首选——CLI 会直接从源码树中跟踪每个技能最新发布的 `SKILL.md`。

**需要锁定版本？（用于 CI / 生产环境）** 请使用带标签范围的 `tree/` URL——它指向发布构建时的确切提交：

```bash
# 将单个技能锁定至特定发行版
npx skills add ConardLi/garden-skills/tree/web-design-engineer-v1.0.0/skills/web-design-engineer
```

每个技能的当前锁定 `.zip` URL 也显示在上述“Links”行中（即 `Download v<version> .zip` 链接）。

常用子命令：

```bash
npx skills list                 # 查看已安装的技能
npx skills find web-design      # 搜索注册表中的技能
npx skills update               # 更新所有技能
npx skills remove kb-retriever  # 卸载指定技能
```

### Option B · Claude Code plugin marketplace

如果你使用 [Claude Code](https://docs.anthropic.com/en/docs/claude-code)，可以订阅插件市场并安装捆绑了一个或多个技能的插件包：

```bash
/plugin marketplace add ConardLi/garden-skills
/plugin install presentation-skills@garden-skills
/plugin install web-design-skills@garden-skills
/plugin install knowledge-base-skills@garden-skills
/plugin install image-generation-skills@garden-skills
```

插件包声明位于 [`.claude-plugin/marketplace.json`](./.claude-plugin/marketplace.json)：

| 插件包 | 包含的技能 |
|---|---|
| `presentation-skills` | `web-video-presentation` |
| `web-design-skills` | `web-design-engineer` |
| `knowledge-base-skills` | `kb-retriever` |
| `image-generation-skills` | `gpt-image-2` |

### Option C · Pinned `.zip` from Releases

每次正式发行都会将不可变的 `.zip`（附带 SHA-256 校验和）发布到 [GitHub Releases](https://github.com/ConardLi/garden-skills/releases)。当你需要确保文件字节绝对稳定时，可在 CI、Dockerfile 或离线安装脚本中锁定此版本。

```bash
# 将 <skill> 和 <version> 替换为你需要的版本。
SKILL=web-design-engineer
VERSION=1.0.0

curl -fsSL -o "${SKILL}.zip" \
  "https://github.com/ConardLi/garden-skills/releases/download/${SKILL}-v${VERSION}/${SKILL}-${VERSION}.zip"

# 验证校验和（强烈建议用于无人值守安装）
curl -fsSL -o "${SKILL}.zip.sha256" \
  "https://github.com/ConardLi/garden-skills/releases/download/${SKILL}-v${VERSION}/${SKILL}-${VERSION}.zip.sha256"
shasum -a 256 -c "${SKILL}.zip.sha256"

# 将文件夹解压至智能体的技能目录
unzip -q "${SKILL}.zip" -d .claude/skills/   # 或 .agents/skills/, .codex/skills/, ...
```

同时提供“始终最新版”浮动 URL——适用于一次性安装：

```bash
https://github.com/ConardLi/garden-skills/releases/latest/download/<skill>-<version>.zip
```

> **每个技能的锁定 URL 均列于本 README 中** —— 见上方各技能“Links”条目下的下载行。它们由发布流水线自动保持同步。

### Option D · Manual copy into your project

克隆仓库并复制你需要的技能文件夹。如果你打算 Fork 该技能或对其进行修改，此方式非常便捷。

```bash
git clone https://github.com/ConardLi/garden-skills.git
cp -r garden-skills/skills/web-design-engineer  your-project/.claude/skills/
# Cursor / 通用智能体：
cp -r garden-skills/skills/web-design-engineer  your-project/.agents/skills/
```

智能体在下次扫描工作区时将自动发现该技能。

### Option E · Git submodule

适用于将技能引入大型项目并希望追踪上游更新：

```bash
git submodule add https://github.com/ConardLi/garden-skills.git vendor/garden-skills
ln -s ../../vendor/garden-skills/skills/web-design-engineer .claude/skills/web-design-engineer
```

锁定至发布标签以确保可复现性：

```bash
cd vendor/garden-skills
git checkout web-design-engineer-v1.0.0
```

---

## 兼容性

| 智能体 / 运行环境 | 技能目录位置 | 状态 |
|---|---|---|
| **Claude Code** | `.claude/skills/<name>/` 或通过插件市场安装 | ✅ 已测试 |
| **Claude.ai** (网页版) | 设置 → 功能 → 技能 | ✅ 已测试 |
| **Cursor** | `.agents/skills/<name>/` | ✅ 已测试 |
| **Codex CLI** | `.codex/skills/<name>/` | ✅ 已测试 |
| **Gemini CLI** | 扩展清单 (extension manifest) | ✅ 已测试 |
| **OpenCode** | `.opencode/skills/<name>/` | ✅ 已测试 |

> `SKILL.md` 格式在设计上即可跨平台移植——如果你的智能体支持技能，只需将文件夹复制到它扫描的目录中即可生效。欢迎通过 PR 扩展此兼容矩阵。

---

## 什么是技能？（What is a Skill?）

**技能（Skill）** 是一个智能体可按需加载的独立文件夹。它本质上只是一个 `SKILL.md`（包含 YAML 前置元数据与指令），可选地附带参考文档、脚本和资源文件：

```text
<skill-name>/
├── SKILL.md      ← 必需：何时使用 + 如何使用
├── README.md     ← 面向人类的说明文档
├── references/   ← 可选：智能体按需加载的扩展文档
├── scripts/      ← 可选：确定性可执行辅助脚本
└── assets/       ← 可选：模板、字体、图标等资源
```

智能体将根据前置元数据中的 `description`（描述）字段决定是否激活该技能——因此，描述是你与智能体之间的契约。完整规范请参阅 [agentskills.io](https://agentskills.io) 和 [Anthropic 的参考仓库](https://github.com/anthropics/skills)。

---

## 参与贡献（Contributing）

欢迎提交 Bug 报告、新技能以及工具链改进。

面向维护者的文档——包括仓库结构、发布流程、版本规则、CI 工作流及故障排查——均位于 [**`CONTRIBUTING.md`**](./CONTRIBUTING.md) ([中文](./CONTRIBUTING.zh-CN.md))。若计划添加技能或发布新版本，请优先阅读该文档。

快速上手指南：

```bash
git clone https://github.com/ConardLi/garden-skills.git
cd garden-skills
npm run list      # 显示所有技能及清单状态
npm run validate  # 执行与 CI 相同的检查
```

---

## 鸣谢（Acknowledgments）

本集合得益于以下项目/团队的支持：

- **[Anthropic](https://www.anthropic.com)**：提供 [Agent Skills 规范](https://agentskills.io) 及 [`anthropics/skills`](https://github.com/anthropics/skills) 参考仓库。
- **[Claude Design](https://www.anthropic.com/news/claude-design-anthropic-labs)**：启发 `web-design-engineer` 的系统提示词。原版已保留在 [`dist/prompt/claude-design-system-prompt.md`](./dist/prompt/claude-design-system-prompt.md) 供参考。
- 更广泛的开源技能社区——详见 [`travisvn/awesome-claude-skills`](https://github.com/travisvn/awesome-claude-skills) 与 [`obra/superpowers`](https://github.com/obra/superpowers) 以探索更多内容。

---

## 许可证（License）

[MIT](./LICENSE) © [ConardLi](https://github.com/ConardLi)
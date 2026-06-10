# Open CoDesign

**简体中文**: [README.zh-CN.md](./README.zh-CN.md)

> 你的提示词。你的模型。你的电脑。
>
> 将提示词转化为精美的成品——在本地、开源地进行，并使用你已付费的任何模型。

[官网](https://opencoworkai.github.io/open-codesign/) · [快速入门](#quickstart) · [更新日志](https://github.com/OpenCoworkAI/open-codesign/releases) · [变更说明](./CHANGELOG.md) · [讨论区](https://github.com/OpenCoworkAI/open-codesign/discussions) · [文档](https://opencoworkai.github.io/open-codesign/quickstart) · [贡献指南](./CONTRIBUTING.md) · [安全政策](./SECURITY.md)

**开源替代品：** [Claude Design](https://opencoworkai.github.io/open-codesign/claude-design-alternative) · [v0 by Vercel](https://opencoworkai.github.io/open-codesign/v0-alternative) · [Lovable](https://opencoworkai.github.io/open-codesign/lovable-alternative) · [Bolt.new](https://opencoworkai.github.io/open-codesign/bolt-alternative) · [Figma AI](https://opencoworkai.github.io/open-codesign/figma-ai-alternative)

<p align="center">
  <img src="https://raw.githubusercontent.com/OpenCoworkAI/open-codesign/main/website/public/screenshots/product-hero.png" alt="Open CoDesign — prompt on the left, live artifact on the right" width="1000" />
</p>

<p align="center">
  <a href="https://github.com/OpenCoworkAI/open-codesign/releases"><img alt="GitHub release" src="https://img.shields.io/github/v/release/OpenCoworkAI/open-codesign?label=release&color=c96442" /></a>
  <a href="LICENSE"><img alt="License" src="https://img.shields.io/badge/license-MIT-blue" /></a>
  <a href="https://github.com/OpenCoworkAI/open-codesign/actions"><img alt="CI" src="https://img.shields.io/github/actions/workflow/status/OpenCoworkAI/open-codesign/ci.yml?label=CI" /></a>
  <a href="https://github.com/OpenCoworkAI/open-codesign/stargazers"><img alt="Stars" src="https://img.shields.io/github/stars/OpenCoworkAI/open-codesign?style=social" /></a>
  <a href="#community"><img alt="WeChat Group" src="https://img.shields.io/badge/WeChat-Group-07C160?logo=wechat&logoColor=white" /></a>
</p>

<p align="center">
  <a href="https://github.com/OpenCoworkAI/open-codesign/commits/main"><img alt="Last commit" src="https://img.shields.io/github/last-commit/OpenCoworkAI/open-codesign?label=last%20commit&color=40b4a1" /></a>
  <a href="https://github.com/OpenCoworkAI/open-codesign/pulse"><img alt="Commit activity" src="https://img.shields.io/github/commit-activity/m/OpenCoworkAI/open-codesign?label=commits%2Fmonth" /></a>
  <a href="https://github.com/OpenCoworkAI/open-codesign/graphs/contributors"><img alt="Contributors" src="https://img.shields.io/github/contributors/OpenCoworkAI/open-codesign" /></a>
  <a href="https://github.com/OpenCoworkAI/open-codesign/releases"><img alt="Downloads" src="https://img.shields.io/github/downloads/OpenCoworkAI/open-codesign/total?label=downloads&color=6c5ce7" /></a>
</p>

<p align="center">
  <sub><code>claude-code</code> · <code>claude-design-alternative</code> · <code>v0-alternative</code> · <code>bolt-alternative</code> · <code>lovable-alternative</code> · <code>figma-alternative</code> · <code>ai-design</code> · <code>design-to-code</code> · <code>prompt-to-design</code> · <code>ai-prototyping</code> · <code>desktop-design-tool</code> · <code>byok</code> · <code>local-first</code> · <code>multi-model</code> · <code>electron</code></sub>
</p>

---

## 更新日志

- **v0.2.0** *(2026-05-09)* —— 智能体设计（Agentic Design）：基于工作区的会话 · 权限控制的本地工具 · 文件面板升级 · 提供商诊断 · 安全加固 · `DESIGN.md` 设计规范
- **v0.1.4** *(2026-04-23)* —— AI 图像生成 · 支持 ChatGPT Plus / Codex 订阅 · CLIProxyAPI 一键导入 · API 配置加固
- **v0.1.3** *(2026-04-21)* —— 修复 Gemini `models/` 前缀问题 · 修复 OpenAI 兼容中继的“需要 instructions”提示 · 第三方中继 SSE 截断提示
- **v0.1.2** *(2026-04-21)* —— 发布流水线 · Homebrew / winget / Scoop 打包清单

[完整发行历史 →](https://github.com/OpenCoworkAI/open-codesign/releases) · [变更日志 →](./CHANGELOG.md)

---

## 项目简介

使用你已有的模型，在本地将提示词转化为精美的原型、演示文稿或营销素材。

**Open CoDesign 是 Claude Design 的开源替代品** —— 专为那些希望体验 AI 原生设计工具速度，但不愿被订阅制绑定、不愿依赖纯云端工作流、或不想局限于单一提供商的用户打造。这是一款采用 MIT 许可证的桌面应用，从第一天起就坚持本地优先（local-first），支持自带密钥（BYOK）接入任意模型（Claude、GPT、Gemini、DeepSeek、Kimi、GLM、Ollama 或任何 OpenAI 兼容端点），并可直接通过 ChatGPT Plus / Pro / Team 订阅登录使用 Codex 模型。一键导入现有的 Claude Code 或 Codex 提供商配置，或直接一键登录 ChatGPT，90 秒内即可开始使用。

---

## 效果演示

从空白提示词到成品，智能体会进行规划、编写、自检，并交付包含悬停状态（hover states）、标签页和空状态的完整成果：

![Generate a design from scratch](https://raw.githubusercontent.com/OpenCoworkAI/open-codesign/main/website/public/demos/generate-from-scratch.gif)

---

## 为什么值得 Star

- **在本地电脑运行** —— 无需强制使用云端工作区
- **兼容你的模型** —— 支持 Claude、GPT、Gemini、Ollama、OpenRouter 等
- **导出真实文件** —— HTML、PDF、PPTX、ZIP、Markdown
- **过程透明可见** —— 实时显示智能体活动与工具调用，支持中途中断

---

## 为什么选择 Open CoDesign？

开源、原生桌面应用，专为不愿将设计工作流绑定到单一模型或单一云服务的用户打造。

| | **Open CoDesign** | Claude Design | v0 by Vercel | Lovable |
|:---|:---:|:---:|:---:|:---:|
| 开源协议 | ✅ MIT | ❌ 闭源 | ❌ 闭源 | ❌ 闭源 |
| 原生桌面应用 | ✅ Electron | ❌ 仅网页 | ❌ 仅网页 | ❌ 仅网页 |
| 自带密钥（BYOK） | ✅ 任意提供商 | ❌ 仅限 Anthropic | ❌ 仅限 Vercel | ⚠️ 有限支持 |
| 本地/离线运行 | ✅ 完全本地应用 | ❌ 云端 | ❌ 云端 | ❌ 云端 |
| 支持模型 | ✅ 20+（Claude、GPT、Gemini、Ollama…） | 仅限 Claude | GPT-4o | 多 LLM |
| 版本历史 | ✅ 本地会话 + 工作区文件 | ❌ | ❌ | ❌ |
| 数据隐私 | ✅ 设备端应用状态 | ❌ 云端处理 | ❌ 云端 | ❌ 云端 |
| 可编辑导出 | ✅ HTML、PDF、PPTX、ZIP、Markdown | ⚠️ 有限支持 | ⚠️ 有限支持 | ⚠️ 有限支持 |
| 价格 | ✅ 应用免费，仅收取提供商/订阅费用 | 💳 需订阅 | 💳 需订阅 | 💳 需订阅 |

---

## 核心亮点

<table>
  <tr>
    <td width="50%">
      <a href="https://raw.githubusercontent.com/OpenCoworkAI/open-codesign/main/website/public/screenshots/comment-mode.png">
        <img src="https://raw.githubusercontent.com/OpenCoworkAI/open-codesign/main/website/public/screenshots/comment-mode.png" alt="Click any element, leave a pin, let the model rewrite that region" />
      </a>
      <p><b>仅评论，不重输。</b><br/>点击任意元素、添加标记，让模型仅重写该区域。</p>
    </td>
    <td width="50%">
      <a href="https://raw.githubusercontent.com/OpenCoworkAI/open-codesign/main/website/public/screenshots/tweaks-sliders.png">
        <img src="https://raw.githubusercontent.com/OpenCoworkAI/open-codesign/main/website/public/screenshots/tweaks-sliders.png" alt="AI-emitted tweaks panel with color pickers and RGB inputs" />
      </a>
      <p><b>AI 调节滑块。</b><br/>模型会提示值得调整的参数，让你无需重新输入完整提示词即可微调颜色、间距和排版。</p>
    </td>
  </tr>
  <tr>
    <td width="50%">
      <a href="https://raw.githubusercontent.com/OpenCoworkAI/open-codesign/main/website/public/screenshots/hub-your-designs.png">
        <img src="https://raw.githubusercontent.com/OpenCoworkAI/open-codesign/main/website/public/screenshots/hub-your-designs.png" alt="Your Designs hub, filled with real generated artifacts" />
      </a>
      <p><b>每次迭代均保留。</b><br/>设计稿保存在本地，可即时切换查看最近的版本。</p>
    </td>
    <td width="50%">
      <a href="https://raw.githubusercontent.com/OpenCoworkAI/open-codesign/main/website/public/screenshots/agent-panel.png">
        <img src="https://raw.githubusercontent.com/OpenCoworkAI/open-codesign/main/website/public/screenshots/agent-panel.png" alt="Live agent panel showing todos and streaming tool calls" />
      </a>
      <p><b>实时观察智能体工作。</b><br/>待办事项、工具调用和实时进度全程可见且支持中断。</p>
    </td>
  </tr>
</table>

---

## 快速入门

**首个成果生成时间：**约 3 分钟

**所需条件：**一个 API Key、ChatGPT 订阅登录或本地 Ollama

**运行环境：**macOS 12+（Monterey 及更高版本）、Windows 10+、Linux（glibc ≥ 2.31）

### 1. 安装

**包管理器**（推荐）：

```bash
# macOS
brew install --cask opencoworkai/tap/open-codesign

# Windows — Scoop
scoop bucket add opencoworkai https://github.com/OpenCoworkAI/scoop-bucket
scoop install opencoworkai/open-codesign
```

**或直接下载** [v0.2.0 GitHub 发行版](https://github.com/OpenCoworkAI/open-codesign/releases/tag/v0.2.0)中的文件：

| 平台 | 文件 |
|---|---|
| macOS (Apple Silicon) | `open-codesign-*-arm64.dmg` |
| macOS (Intel) | `open-codesign-*-x64.dmg` |
| Windows (x64) | `open-codesign-*-x64-setup.exe` |
| Windows (ARM64) | `open-codesign-*-arm64-setup.exe` |
| Linux (x64, AppImage) | `open-codesign-*-x64.AppImage` |
| Linux (x64, Debian/Ubuntu) | `open-codesign-*-x64.deb` |
| Linux (x64, Fedora/RHEL) | `open-codesign-*-x64.rpm` |

每个发行版均附带 `SHA256SUMS.txt` 和 CycloneDX SBOM（`*-sbom.cdx.json`），方便你验证下载文件的完整性。

<details>
<summary><b>更多包管理器</b></summary>

| 管理器 | 命令 | 状态 |
|---|---|---|
| Homebrew Cask (macOS) | `brew install --cask opencoworkai/tap/open-codesign` | 🟢 已上线 |
| Scoop (Windows) | `scoop bucket add opencoworkai https://github.com/OpenCoworkAI/scoop-bucket && scoop install opencoworkai/open-codesign` | 🟢 已上线 |
| winget (Windows) | `winget install OpenCoworkAI.OpenCoDesign` | 🟡 PR 已提交；等待微软审核 |
| Flathub (Linux) | `flatpak install flathub ai.opencowork.codesign` | ⏸ 暂缓；需签名构建 + AppStream 元数据 |
| Snap (Linux) | `snap install --dangerous open-codesign-*.snap` | 🟡 随发行版附带尽力支持；尚未接入 Snap Store 发布流程 |

每次稳定版本推送后，CI 会将 SHAs 同步回 `packaging/` 目录。当仓库密钥配置完成后，会自动发布下游 Homebrew/Scoop 更新。首次 winget 提交正在审核中；微软接受该包后，后续的 winget 升级可从发布工作流自动完成。每个 `packaging/*/README.md` 均记录了其对应的分发渠道。
</details>

> **未签名安装程序说明：**安装程序尚未进行公证或 Authenticode 签名。在 **macOS Sequoia 15+** 上，右键→打开不再能绕过 Gatekeeper，且系统设置中的“仍要打开”选项通常也会失败。可靠的单行命令：
>
> ```sh
> xattr -cr "/Applications/Open CoDesign.app"
> ```
>
> 然后正常双击运行。（旧版 0.1.x 构建安装为 `/Applications/open-codesign.app`。）在 **Windows** 上：SmartScreen 安全筛选器 → 更多信息 → 仍要运行。
>
> 需要验证过的构建版本？请从源码编译——详见 [CONTRIBUTING.md](./CONTRIBUTING.md)。

### 2. 添加提供商

首次启动时，Open CoDesign 会打开设置页面。选择与你现有模型使用方式匹配的路径：

- **ChatGPT 订阅** —— 通过 ChatGPT 登录即可使用 Codex 模型，无需粘贴 API Key。
- **API Key** —— 粘贴 Anthropic（`sk-ant-...`）、OpenAI（`sk-...`）、Google Gemini、OpenRouter、SiliconFlow、DeepSeek 或其他支持提供商的密钥。
- **本地/无密钥** —— 使用 Ollama 或经过 IP 白名单认证的 OpenAI 兼容网关。

凭证信息保存在 `~/.config/open-codesign/config.toml` 及应用配置目录下的 ChatGPT OAuth Token 存储中。除非你选择的模型路由明确要求，否则数据不会离开你的设备。

### 3. 输入你的第一个提示词

从 **15 个内置演示**中选择一个——落地页、仪表盘、推介幻灯片、定价页、移动应用、聊天界面、活动日历、博客文章、收据/发票、作品集、设置面板等，或描述你自己的需求。沙盒原型将在数秒内生成。

---

## 无缝迁移你的技术栈

已在使用 Claude Code 或 Codex？API Key 提供商配置可一键导入，无需复制粘贴或重新输入设置。如果你通过 ChatGPT 订阅登录使用 Codex，可直接在设置中登录：

![Import from Claude Code or Codex in one click](https://raw.githubusercontent.com/OpenCoworkAI/open-codesign/main/website/public/demos/claude-code-import.gif)

---

## 内置设计品味

通用 AI 工具往往产出千篇一律的结果。Open CoDesign 内置了 **12 个设计技能模块**——演示文稿、仪表盘、落地页、SVG 图表、毛玻璃效果、排版字体、首屏海报（Hero）、定价页、页脚、聊天界面、数据表格和日历——并配备内置的“品味层”，引导模型采用考究的排版、有目的的留白和有意义的配色。

每次生成均可调用所有技能模块。在模型编写任何一行 CSS 之前，它会先根据需求匹配合适的技能，并推演布局意图、设计规范一致性与对比度，从而为你选择的任意模型带来更高质量的设计表现。

在任何项目中添加 `SKILL.md`，即可教会模型你的个人品味/偏好。

---

## 功能一览

### 模型与提供商
- **统一提供商架构** —— 支持 Anthropic、OpenAI、Gemini、DeepSeek、OpenRouter、SiliconFlow、本地 Ollama，或任何 OpenAI 兼容中继；支持无密钥（IP 白名单）代理
- **一键导入与登录** —— 无缝迁移 Claude Code / Codex API Key 提供商配置，或通过 ChatGPT 订阅登录使用 Codex 模型
- **动态模型选择器** —— 各提供商直接暴露真实模型目录，而非硬编码的短名单

### 生成与编辑
- **提示词 → HTML 或 JSX/React 组件**原型，在沙盒 iframe 中渲染（内置 React 18 + Babel）
- **15 个内置演示 + 12 个设计技能模块** —— 针对常见设计需求的开箱即用起点
- **实时智能体面板** —— 观看模型编辑文件时工具调用的实时流
- **AI 图像生成** —— 可选地通过 OpenAI、OpenRouter 或已登录的 ChatGPT 订阅生成首屏海报、产品图、背景和插图等位图素材
- **AI 生成调节滑块** —— 模型输出值得调整的参数（颜色、间距、字体）
- **评论模式** —— 点击预览中的任意元素添加标记和备注，让模型仅重写该区域
- **生成取消** —— 中途停止且不丢失之前的交互记录

### 预览与工作流
- **手机/平板/桌面预览** —— 真实的响应式框架，一键切换
- **文件面板** —— 导出前检查多文件成果（HTML、CSS、JS）
- **即时设计切换** —— 最近五个设计稿的预览 iframe 保持活跃，确保中心枢纽与工作区及侧边栏导航零延迟切换
- **连接诊断面板** —— 一键测试任意提供商，提供可操作的错误提示
- **单次生成 Token 计数器** —— 在侧边栏精确查看每次运行的 Token 消耗量
- **四标签页设置** —— 模型、外观、存储与高级选项
- **亮色/暗色主题**，支持 **英文/简体中文 UI** 实时切换

### 导出与打包
- **五种导出格式** —— HTML（内联 CSS）、PDF（本地 Chrome）、PPTX、ZIP、Markdown
- **GitHub 发布流水线** —— 未签名的 DMG（macOS）、EXE（Windows）、AppImage（Linux）。代码签名与可选自动更新功能将在 v0.5 版本上线

---

## 路线图

当前版本：v0.2.0。本次发布主题为**智能体设计（Agentic Design）**。

### 现已发布 —— v0.2.0

v0.2 将 Open CoDesign 从单次生成工具转变为拥有真实工作区的本地设计智能体：

- **以会话形式管理设计** —— 每个设计均为一个 `pi` 会话，包含 JSONL 历史记录与磁盘上的工作区文件夹
- **权限控制的智能体循环** —— `pi` 内置了读、写、编辑、bash、grep、find 和 ls 命令，受 Open CoDesign 权限 UI 管控
- **按需调用的设计工具** —— `` `ask`, `scaffold`, `skill`, `preview`, `gen_image`, `tweaks`, `todos`, and `done` ``
- **以 `DESIGN.md` 作为共享记忆** —— 品牌标识与设计规范决策变为可编辑文件，而非依赖模型上下文记忆
- **v0.1 迁移路径** —— 现有的 SQLite 设计数据将自动迁移至工作区与会话历史中

### 上一版本 —— v0.1.4

- **AI 图像生成** —— 通过 OpenAI 或 OpenRouter 的图像模型可选地生成位图素材
- **ChatGPT Plus / Codex 订阅登录** —— 为不愿粘贴 API Key 的用户提供一键 OAuth 登录
- **CLIProxyAPI 一键导入** —— 自动检测运行的本地代理并将其接入设置
- **API 配置加固** —— 提供更清晰的中继诊断（超时、SSE 截断、缺少 `/models`、不兼容的 Messages API）

### 后续规划 —— v0.2.x 及更远

- 渲染器打磨：针对新的 `ask`、`preview`、调节滑块与进程管理界面
- 成本透明化：生成前预估 + 每周预算（单次 Token 计数已上线）
- 版本快照与并排对比
- 三风格并行探索
- 代码库转设计规范（Token 提取）
- 代码签名（Apple ID + Authenticode）+ 可选自动更新 —— v0.5
- Figma 图层导出 —— 1.0 之后

有不同的优先级想法？[提交 Issue](https://github.com/OpenCoworkAI/open-codesign/issues/new/choose) 或为现有 Issue 👍——我们会仔细阅读。

---

## Star 历史

<p align="center">
  <a href="https://star-history.com/#OpenCoworkAI/open-codesign&Date">
    <img
      alt="Star History Chart"
      src="https://api.star-history.com/image?repos=OpenCoworkAI/open-codesign&type=Date"
      width="720"
    />
  </a>
</p>

---

## 技术栈

- Electron + React 19 + Vite 6 + Tailwind v4
- `@mariozechner/pi-ai` and `pi-coding-agent`（模型/提供商及智能体循环基础组件）
- `electron-builder`

## 报告问题

发现 Bug 或有功能建议？

1. **搜索** [现有 Issue](https://github.com/OpenCoworkAI/open-codesign/issues)。
2. **生成诊断包** —— 设置 → 存储 → 导出诊断（API Key 和提示词会自动脱敏）。
3. **提交新 Issue** —— 使用我们的 [Bug 报告](https://github.com/OpenCoworkAI/open-codesign/issues/new?template=bug_report.yml) 或 [功能建议](https://github.com/OpenCoworkAI/open-codesign/issues/new?template=feature_request.yml) 模板。
4. 安全漏洞请参见 [SECURITY.md](./SECURITY.md)。

## OpenCoworkAI 更多项目

如果你喜欢 Open CoDesign，可能也会对我们早期的项目 [Open Cowork](https://github.com/OpenCoworkAI/open-cowork) 感兴趣。这是一款面向 Windows 和 macOS 的开源 AI 智能体桌面应用，支持一键安装、多模型兼容、沙盒隔离与内置技能。

## 社区

Open CoDesign 首发于 [LINUX DO](https://linux.do/) 社区——感谢所有早期反馈与讨论的伙伴。

- **[GitHub Discussions](https://github.com/OpenCoworkAI/open-codesign/discussions)** —— 在 [Show & Tell](https://github.com/OpenCoworkAI/open-codesign/discussions/categories/show-and-tell) 分享你的设计，在 [Q&A](https://github.com/OpenCoworkAI/open-codesign/discussions/categories/q-a) 提问，或在 [Ideas](https://github.com/OpenCoworkAI/open-codesign/discussions/categories/ideas) 提出功能建议。
- **[LINUX DO](https://linux.do/)** —— 中文讨论、使用技巧与反馈（主要社区）。
- **GitHub Issues** —— [Bug 报告与可复现问题](https://github.com/OpenCoworkAI/open-codesign/issues)。

### 微信群

面向中文用户，我们维护了一个微信群用于产品更新、使用答疑与社区交流。

<p align="center">
  <img
    src="https://raw.githubusercontent.com/OpenCoworkAI/open-codesign/main/website/public/community/wechat-group.jpg"
    alt="Open CoDesign WeChat group QR code"
    width="260"
  />
</p>

> ⚠️ 微信群二维码每 7 天轮换，当前有效期至 **5月16日**。若已过期，请在 [GitHub Issue](https://github.com/OpenCoworkAI/open-codesign/issues) 留言，我们将刷新仓库内的图片。

详见中文文档：[README.zh-CN.md#社群](./README.zh-CN.md#%E7%A4%BE%E7%BE%A4)。

## 贡献指南

请阅读 [CONTRIBUTING.md](./CONTRIBUTING.md)。提交代码前请先开启 Issue，并在发起 PR 前运行 `pnpm lint && pnpm typecheck && pnpm test`。

## 许可证

MIT —— 可自由 Fork、发布与销售。第三方声明保留在 [NOTICE](./NOTICE) 中。

## 引用本项目

如果你在论文、文章或产品对比中引用了 Open CoDesign，请按以下格式标注仓库：

```bibtex
@misc{open_codesign_github,
  author       = {OpenCoworkAI Contributors},
  title        = {Open CoDesign: An Open-Source Desktop AI Design Tool},
  year         = {2026},
  howpublished = {\url{https://github.com/OpenCoworkAI/open-codesign}},
  note         = {GitHub repository}
}
````

或使用根目录下的机器可读文件 `CITATION.cff`。
<p align="center">
  <img src="src/assets/logo.svg" width="128" height="128" alt="ClawX Logo" />
</p>

<h1 align="center">ClawX</h1>

<p align="center">
  <strong>OpenClaw AI 代理的桌面界面</strong>
</p>

<p align="center">
  <a href="#features">功能特性</a> •
  <a href="#why-clawx">为何选择 ClawX</a> •
  <a href="#getting-started">快速开始</a> •
  <a href="#architecture">架构设计</a> •
  <a href="#development">开发指南</a> •
  <a href="#contributing">贡献代码</a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/platform-MacOS%20%7C%20Windows%20%7C%20Linux-blue" alt="Platform" />
  <img src="https://img.shields.io/badge/electron-40+-47848F?logo=electron" alt="Electron" />
  <img src="https://img.shields.io/badge/react-19-61DAFB?logo=react" alt="React" />
  <a href="https://discord.com/invite/84Kex3GGAh" target="_blank">
  <img src="https://img.shields.io/discord/1399603591471435907?logo=discord&labelColor=%20%235462eb&logoColor=%20%23f5f5f5&color=%20%235462eb" alt="chat on Discord" />
  </a>
  <img src="https://img.shields.io/github/downloads/ValueCell-ai/ClawX/total?color=%23027DEB" alt="Downloads" />
  <img src="https://img.shields.io/badge/license-MIT-green" alt="License" />
</p>

<p align="center">
  English | <a href="README.zh-CN.md">简体中文</a> | <a href="README.ja-JP.md">日本語</a> | <a href="README.ru-RU.md">Русский</a>
</p>

---

## 概述

**ClawX** 在强大的 AI 代理与日常用户之间架起桥梁。基于 [OpenClaw](https://github.com/OpenClaw) 构建，它将命令行 AI 编排转化为直观、美观的桌面体验——无需终端。

无论你是想自动化工作流、管理 AI 驱动的消息通道，还是调度智能任务，ClawX 都能为你提供高效驾驭 AI 代理所需的界面。

ClawX 预置了最佳实践的模型提供商配置，并原生支持 Windows 及多语言设置。当然，你也可以通过 **Settings → Advanced → Developer Mode**（设置 → 高级 → 开发者模式）微调高级配置。

<p align="center"><strong style="font-size:1.1em; text-decoration: underline;">如需完整企业版、专属技术支持或针对你业务场景的定制部署指导，请通过 <a href="mailto:public@valuecell.ai">public@valuecell.ai</a> 联系我们。</strong></p>

---
## 截图

<p align="center">
  <img src="resources/screenshot/en/chat.png" style="width: 100%; height: auto;">
</p>

<p align="center">
  <img src="resources/screenshot/en/cron.png" style="width: 100%; height: auto;">
</p>

<p align="center">
  <img src="resources/screenshot/en/skills.png" style="width: 100%; height: auto;">
</p>

<p align="center">
  <img src="resources/screenshot/en/channels.png" style="width: 100%; height: auto;">
</p>

<p align="center">
  <img src="resources/screenshot/en/models.png" style="width: 100%; height: auto;">
</p>

<p align="center">
  <img src="resources/screenshot/en/settings.png" style="width: 100%; height: auto;">
</p>

---

## 为何选择 ClawX

构建 AI 代理无需精通命令行。ClawX 秉持一个简单的设计理念：**强大的技术理应拥有尊重你时间的界面。**

| 挑战 | ClawX 解决方案 |
|-----------|----------------|
| 复杂的 CLI 配置 | 一键安装，附带引导式设置向导 |
| 配置文件管理 | 可视化设置与实时校验 |
| 进程管理 | 自动化的 Gateway（网关）生命周期管理 |
| 应用更新 | 启动时检查更新，下载或安装前弹出提示 |
| 多模型提供商接入 | 统一的提供商配置面板 |
| 技能/插件安装 | 本地优先的技能管理，可选扩展提供的企业级市场 |

### OpenClaw 内核

ClawX 直接基于官方 **OpenClaw** 核心构建。无需单独安装，我们将运行时环境嵌入应用内，提供开箱即用的完整体验。

我们承诺与上游 OpenClaw 项目保持严格同步，确保你始终能获取官方发布带来的最新功能、稳定性改进及生态兼容性。

启用开发者模式后，侧边栏还会提供原生的 Dreams（梦境）页面，用于查看 OpenClaw 记忆、检查梦境日记以及执行基础维护操作。当需要更深度的诊断时，完整的上游 OpenClaw Dreams UI 仍可从该页面访问。

---

## 功能特性

### 🎯 零配置门槛
通过直观的图形界面完成从安装到首次 AI 交互的全部设置。无需终端命令、YAML 文件或环境变量配置。

### 💬 智能聊天界面
通过现代化的聊天体验与 AI 代理交流。支持多对话上下文、消息历史、Markdown 富文本渲染（含 GitHub 风格表格及 KaTeX 驱动的 LaTeX 数学公式：`$inline$`、`$$block$$`、`\(inline\)`、`\[block\]`），以及在主输入框中直接 `@agent` 路由以实现多代理协作。从输入框插入的技能会显示为 `/skill-name` 标签；点击标签可打开预览侧边栏并阅读该技能的 `SKILL.md`。当使用 `@agent` 指定其他代理时，ClawX 会直接切换至该代理的对话上下文，而非通过默认代理中转。各代理的工作空间默认保持独立，更强的隔离性取决于 OpenClaw 的沙箱设置。每个代理也可覆盖其自身的 `provider/model`（提供商/模型）运行时配置；未覆盖的代理将继续继承全局默认模型。

### 📡 多通道管理
同时配置和监控多个 AI 消息通道。各通道独立运行，让你为不同任务部署专用代理。每个通道现已支持多账号、按账号绑定代理，并可直接在“通道”页面切换通道的默认账号。对于自定义通道账号 ID，ClawX 会强制执行 OpenClaw 兼容的标准格式（`[a-z0-9_-]`，小写，最长 64 字符，必须以字母/数字开头）以防止路由错配。此外，ClawX 还内置了腾讯官方个人微信通道插件，你可直接在“通道”页面通过应用内扫码流程绑定微信。

### ⏰ 定时任务自动化
调度 AI 任务自动运行。定义触发条件、设置间隔时间，让 AI 代理全天候工作而无需手动干预。“定时任务”页面现已允许你在任务表单中直接配置外部投递功能，提供独立的发送账号和接收目标选择器。对于受支持的通道，系统会自动从通道目录或已知会话历史中发现接收目标，你不再需要手动编辑 `jobs.json`。

### 🧩 可扩展技能系统
通过预置技能扩展你的 AI 代理。“技能”页面采用本地优先架构：它会扫描托管/工作区内的技能目录，允许你在不依赖 Gateway（网关）的情况下启用或禁用技能，并在企业版中可选地提供扩展市场。ClawX 还内置了完整的文档处理技能（`pdf`, `xlsx`, `docx`, `pptx`），在启动时自动部署到托管技能目录（默认 `~/.openclaw/skills`），并在首次安装时默认启用。其他内置技能（`find-skills`, `self-improving-agent`, `tavily-search`）也默认启用；若缺少必要的 API 密钥，OpenClaw 会在运行时提示配置错误。“技能”页面现在可显示来自多个 OpenClaw 来源（托管目录、工作区及额外技能目录）的技能，并展示每个技能的真实路径以便直接打开文件夹。对于内置的 OpenClaw 技能，社区构建版现仅发布和暴露 `skill-creator`；非白名单内的内置技能会在开发和打包启动时被物理裁剪，且残留的旧 `openclaw.json` 条目也会被清理。

内置搜索技能的环境变量：
- `TAVILY_API_KEY` 用于 `tavily-search`（上游技能运行时可能也支持 OAuth）
- `find-skills` 和 `self-improving-agent` 无需 API 密钥

### 🔐 安全的提供商集成
安全连接至多个 AI 提供商（OpenAI、Anthropic 等），凭据将加密存储于系统原生钥匙串中。OpenAI 支持 API Key 及浏览器 OAuth（Codex 订阅）登录方式。在开发者模式下，专用的“图像生成”页面支持独立的 OpenAI 兼容图像生成端点（Base URL、API Key 和模型名称如 `gpt-image-2`），使图像生成可调用专用 `/v1/images/generations` 服务，而聊天继续使用常规 OpenAI 提供商。对于使用 OpenAI 兼容网关的**自定义**提供商，你可以在 **Settings → AI Providers → Edit Provider**（设置 → AI 提供商 → 编辑提供商）中设置自定义 `User-Agent` 以适配对兼容性敏感的服务端点。当兼容网关因非认证原因拒绝 `/models` 请求时，ClawX 会在 API Key 验证期间自动降级使用轻量级的 `/chat/completions` 或 `/responses` 探针。

### 🌙 自适应主题
支持亮色、暗色及跟随系统主题。ClawX 会自动适应你的偏好设置。

### 🚀 启动项控制
在 **Settings → General**（设置 → 常规）中，可启用 **Launch at system startup**（开机自启），使 ClawX 在登录后自动运行。

### 🔔 更新提示
ClawX 可在启动时自动检查新版本。发现更新时会弹出应用内提示；仅在你确认操作后才会下载和安装。

---

## 快速开始

### 系统要求

- **操作系统**：macOS 11+、Windows 10+ 或 Linux（Ubuntu 20.04+）
- **内存**：最低 4GB RAM（推荐 8GB）
- **存储空间**：至少 1GB 可用磁盘空间

### 安装方式

#### 预构建版本（推荐）

从 [Releases](https://github.com/ValueCell-ai/ClawX/releases) 页面下载对应平台的最新版本。

#### 从源码编译

```bash
# Clone the repository
git clone https://github.com/ValueCell-ai/ClawX.git
cd ClawX

# Initialize the project
pnpm run init

# Start in development mode
pnpm dev
```
### 首次启动

首次启动 ClawX 时，**设置向导**将引导你完成以下步骤：

1. **Language & Region（语言与区域）** – 配置首选区域设置
2. **AI Provider（AI 提供商）** – 添加带有 API Key 或 OAuth（支持浏览器/设备登录的提供商）的提供商
3. **Skill Bundles（技能包）** – 选择适用于常见场景的预配置技能
4. **Verification（验证）** – 进入主界面前测试你的配置

向导会在支持时自动预选系统语言，否则回退至英文。

> **Moonshot（Kimi）注意事项**：ClawX 默认保持 Kimi 网页搜索功能开启。  
> 配置 Moonshot 后，ClawX 还会将 Kimi 网页搜索同步至国内端点 (`https://api.moonshot.cn/v1`) 的 OpenClaw 配置中。

### 代理设置

ClawX 内置了代理设置，适用于需要通过本地代理客户端访问互联网的 Electron、OpenClaw Gateway（网关）或 Telegram 等通道环境。

打开 **Settings → Gateway → Proxy**（设置 → 网关 → 代理）并配置：

- **Proxy Server（代理服务器）**：所有请求的默认代理
- **Bypass Rules（绕过规则）**：需直连的主机，以分号、逗号或换行分隔
- 在**开发者模式**下，可覆盖以下设置：
  - **HTTP Proxy**
  - **HTTPS Proxy**
  - **ALL_PROXY / SOCKS**

推荐的本地配置示例：

```text
Proxy Server: http://127.0.0.1:7890
```
注意事项：

- 仅填写 `host:port` 格式的值将被视为 HTTP。
- 若高级代理字段留空，ClawX 将回退使用 `Proxy Server`。
- 保存代理设置会立即重新应用 Electron 网络配置并自动重启 Gateway（网关）。
- 启用 Telegram 时，ClawX 还会将代理同步至 OpenClaw 的 Telegram 通道配置中。
- 若当前 ClawX 代理已禁用，Gateway（网关）重启时会保留现有的 Telegram 通道代理设置。
- 如需明确清除 OpenClaw 配置中的 Telegram 通道代理，请在禁用代理的情况下保存设置。
- 在 **Settings → Advanced → Developer**（设置 → 高级 → 开发者）中，可运行 **OpenClaw Doctor** 执行 `openclaw doctor --json`，无需离开应用即可查看诊断输出。
- 在打包的 Windows 版本中，内置的 `openclaw` CLI/TUI 将通过随附的 `node.exe` 入口点运行，以保持终端输入行为稳定。

---

## 架构设计

ClawX 采用带有统一 Host API（主机 API）层的**双进程架构**。渲染器通过单一的客户端抽象层进行通信，而 Electron Main（主进程）负责协议选择与进程生命周期管理：

```
┌──────────────────────────────────────────────────────────────────┐
│                        ClawX Desktop App                         │
│                                                                  │
│  ┌────────────────────────────────────────────────────────────┐  │
│  │              Electron Main Process                         │  │
│  │  • Window & application lifecycle management               │  │
│  │  • Gateway process supervision                             │  │
│  │  • System integration (tray, notifications, keychain)      │  │
│  │  • Auto-update orchestration                               │  │
│  └────────────────────────────────────────────────────────────┘  │
│                              │                                   │
│                              │ IPC (authoritative control plane) │
│                              ▼                                   │
│  ┌────────────────────────────────────────────────────────────┐  │
│  │              React Renderer Process                        │  │
│  │  • Modern component-based UI (React 19)                    │  │
│  │  • State management with Zustand                           │  │
│  │  • Unified host-api/api-client calls                       │  │
│  │  • Rich Markdown rendering                                 │  │
│  └────────────────────────────────────────────────────────────┘  │
└──────────────────────────────┬───────────────────────────────────┘
                               │
                               │ Main-owned transport strategy
                               │ (WS first, HTTP then IPC fallback)
                               ▼
┌──────────────────────────────────────────────────────────────────┐
│                Host API & Main Process Proxies                   │
│                                                                  │
│  • hostapi:fetch (Main proxy, avoids CORS in dev/prod)           │
│  • gateway:httpProxy (Renderer never calls Gateway HTTP direct)  │
│  • Unified error mapping & retry/backoff                         │
└──────────────────────────────┬───────────────────────────────────┘
                               │
                               │ WS / HTTP / IPC fallback
                               ▼
┌──────────────────────────────────────────────────────────────────┐
│                     OpenClaw Gateway                             │
│                                                                  │
│  • AI agent runtime and orchestration                            │
│  • Message channel management                                    │
│  • Skill/plugin execution environment                            │
│  • Provider abstraction layer                                    │
└──────────────────────────────────────────────────────────────────┘
```
### 设计原则

- **进程隔离**：AI 运行时运行在独立进程中，确保即使在重度计算时 UI 依然保持响应
- **前端调用单点入口**：渲染器请求统一经过 host-api/api-client；协议细节隐藏在稳定的接口之后
- **主进程传输控制**：Electron Main 负责管理 WS/HTTP 的使用，并在必要时降级至 IPC 以保障可靠性
- **优雅恢复**：内置的重连、超时与退避逻辑可自动处理临时性故障
- **安全存储**：API Key 及敏感数据采用操作系统原生的安全存储机制
- **设计即防 CORS**：本地 HTTP 访问由主进程代理，彻底避免渲染器端的跨域问题

### 进程模型与网关排错

- ClawX 是 Electron 应用，因此**一个应用实例在操作系统中通常表现为多个进程**（主进程、渲染器、Zygote、Utility）。这是正常现象。
- 单实例保护采用 Electron 锁机制，并辅以本地进程文件锁，防止在桌面 IPC/会话总线不稳定的环境中重复启动应用。
- 滚动升级期间，新旧版本混合时保护行为可能不对称。为确保最佳可靠性，建议将所有桌面客户端升级至同一版本。
- OpenClaw Gateway（网关）监听器应保持**单主拥有**：仅允许一个进程监听 `127.0.0.1:18789`。
- 网关就绪状态基于 OpenClaw 核心信号（如 `system-presence`、`health`、`status`）；内存、Dreams（梦境）或通道故障将显示为能力降级，而非全局网关失败。
- 验证当前监听进程：
  - macOS/Linux: `lsof -nP -iTCP:18789 -sTCP:LISTEN`
  - Windows (PowerShell): `Get-NetTCPConnection -LocalPort 18789 -State Listen`
- 点击窗口关闭按钮（`X`）会将 ClawX 最小化至系统托盘；这并**不**代表完全退出应用。请使用托盘菜单中的 **Quit ClawX** 实现彻底关闭。

---

## 使用场景

### 🤖 个人 AI 助手
配置通用型 AI 代理，通过简洁的桌面界面回答问题、起草邮件、总结文档并处理日常事务。

### 📊 自动化监控
设置定时任务监控新闻源、追踪价格或监视特定事件。结果将推送至你偏好的通知通道。

### 💻 开发者效能
将 AI 集成至开发工作流。使用代理审查代码、生成文档或自动化重复性编码任务。

### 🔄 工作流自动化
串联多个技能创建复杂的自动化流水线。处理数据、转换内容并触发操作——全部通过可视化界面编排。

---

## 开发指南

### 环境准备

- **Node.js**：22+（推荐 LTS 版本）
- **包管理器**：pnpm 9+（推荐）或 npm
- **Linux (Ubuntu/Debian)**：运行 Electron 前需安装以下系统依赖库：
  ```bash
  sudo apt-get install -y libnss3 libgtk-3-0 libxss1 libxtst6 libatspi2.0-0 libnotify4 xdg-utils
  ```
  在 Ubuntu 24.04+ 上，部分软件包使用 `t64` 后缀；执行上述命令后，`apt` 会自动选择正确的变体。

### 项目结构

```ClawX/
├── electron/                 # Electron Main Process
│   ├── api/                 # Main-side API router and handlers
│   │   └── routes/          # RPC/HTTP proxy route modules
│   ├── services/            # Provider, secrets and runtime services
│   │   ├── providers/       # Provider/account model sync logic
│   │   └── secrets/         # OS keychain and secret storage
│   ├── shared/              # Shared provider schemas/constants
│   │   └── providers/
│   ├── main/                # App entry, windows, IPC registration
│   ├── gateway/             # OpenClaw Gateway process manager
│   ├── preload/             # Secure IPC bridge
│   └── utils/               # Utilities (storage, auth, paths)
├── src/                      # React Renderer Process
│   ├── lib/                 # Unified frontend API + error model
│   ├── stores/              # Zustand stores (settings/chat/gateway)
│   ├── components/          # Reusable UI components
│   ├── pages/               # Setup/Dashboard/Chat/Channels/Skills/Cron/Settings
│   ├── i18n/                # Localization resources
│   └── types/               # TypeScript type definitions
├── tests/
│   ├── e2e/                 # Playwright Electron end-to-end smoke tests
│   └── unit/                # Vitest unit/integration-like tests
├── resources/                # Static assets (icons/images)
└── scripts/                  # Build and utility scripts
```
### 可用命令

```bash
# Development
pnpm run init             # Install dependencies + download bundled binaries (uv, agent-browser)
pnpm dev                  # Start with hot reload (auto-prepares bundled skills if missing)

# Quality
pnpm lint                 # Run ESLint
pnpm typecheck            # TypeScript validation

# Testing
pnpm test                 # Run unit tests
pnpm run test:e2e         # Run Electron E2E smoke tests with Playwright
pnpm run test:e2e:headed  # Run Electron E2E tests with a visible window
pnpm run comms:replay     # Compute communication replay metrics
pnpm run comms:baseline   # Refresh communication baseline snapshot
pnpm run comms:compare    # Compare replay metrics against baseline thresholds

# Build & Package
pnpm run build:vite       # Build frontend only
pnpm build                # Full production build (with packaging assets)
pnpm package              # Package for current platform (includes bundled preinstalled skills)
pnpm package:mac          # Package for macOS
pnpm package:win          # Package for Windows
pnpm package:linux        # Package for Linux
```

在无头 Linux 环境下，需在显示服务器（如 `xvfb-run`）下运行 Electron 测试：`xvfb-run -a pnpm run test:e2e`。

### 通信回归检查

当 PR 修改了通信路径（网关事件、聊天运行时收发流程、通道投递或传输降级）时，请运行：

```bash
pnpm run comms:replay
pnpm run comms:compare
```

CI 中的 `comms-regression` 会强制执行所需场景与阈值检查。

### Electron E2E 测试

Playwright Electron 套件直接从 `dist/` 和 `dist-electron/` 启动打包后的渲染器与主进程，因此无需手动先运行 `pnpm dev`。

`pnpm run test:e2e` 会自动：

- 使用 `pnpm run build:vite` 构建渲染器与 Electron 包
- 以隔离的 E2E 模式启动 Electron，并设置临时 `HOME` 目录
- 使用临时的 ClawX `userData` 目录
- 跳过启动阶段的重量级副作用（如网关自启、内置技能安装、托盘创建及 CLI 自动安装）

前两个基准测试用例覆盖：

- 全新配置下首次启动设置向导的可见性
- 跳过初始设置并导航至 Electron 应用内的“模型”页面

后续新增的 Electron 流程请置于 `tests/e2e/` 目录下，并复用 `tests/e2e/fixtures/electron.ts` 中的共享 Fixture。

### 技术栈

| 层级 | 技术选型 |
|-------|------------|
| 运行时 | Electron 40+ |
| UI 框架 | React 19 + TypeScript |
| 样式方案 | Tailwind CSS + shadcn/ui |
| 状态管理 | Zustand |
| 构建工具 | Vite + electron-builder |
| 测试框架 | Vitest + Playwright |
| 动画库 | Framer Motion |
| 图标库 | Lucide React |

---

## 贡献代码

我们欢迎社区贡献！无论是 Bug 修复、新功能开发、文档改进还是翻译——每一份贡献都将助力 ClawX 变得更好。

### 如何参与贡献

1. **Fork（克隆）**本仓库
2. **创建**功能分支（`git checkout -b feature/amazing-feature`）
3. **提交**你的更改，并附带清晰的提交信息
4. **推送**至你的分支
5. **创建**Pull Request（PR）

### 贡献指南

- 遵循现有代码规范（ESLint + Prettier）
- 为新功能编写测试用例
- 按需更新文档
- 保持提交原子化且描述清晰

---

## 致谢

ClawX 的诞生得益于以下优秀的开源项目：

- [OpenClaw](https://github.com/OpenClaw) – AI 代理运行时核心
- [Electron](https://www.electronjs.org/) – 跨平台桌面框架
- [React](https://react.dev/) – UI 组件库
- [shadcn/ui](https://ui.shadcn.com/) – 精美设计的组件
- [Zustand](https://github.com/pmndrs/zustand) – 轻量级状态管理

---

## 社区加入

加入我们的社区，与其他用户交流、获取支持并分享你的使用体验。

| 企业微信 | 飞书群组 | Discord |
| :---: | :---: | :---: |
| <img src="src/assets/community/wecom-qr.png" width="150" alt="WeChat QR Code" /> | <img src="src/assets/community/feishu-qr.png" width="150" alt="Feishu QR Code" /> | <img src="src/assets/community/20260212-185822.png" width="150" alt="Discord QR Code" /> |

### ClawX 合作伙伴计划 🚀

我们正在推出 ClawX 合作伙伴计划，寻找能帮助我们向更多客户介绍 ClawX 的合作伙伴，尤其是那些有定制化 AI 代理或自动化需求的客户。

合作伙伴负责连接潜在用户与项目，ClawX 团队则提供全面的技术支持、定制开发与集成服务。

如果你的客户对 AI 工具或自动化感兴趣，我们非常期待与你合作。

欢迎私信或通过邮件 [public@valuecell.ai](mailto:public@valuecell.ai) 联系我们了解详情。

---

## Star History

<p align="center">
  <img src="https://api.star-history.com/svg?repos=ValueCell-ai/ClawX&type=Date" alt="Star History Chart" />
</p>

---

## 许可证

ClawX 基于 [MIT 许可证](LICENSE) 发布。你可自由使用、修改和分发本软件。

---

<p align="center">
  <sub>Built with ❤️ by the ValueCell Team</sub>
</p>
<p align="center">
  <strong>Hermes Web UI</strong>
  <a href="./README_zh.md">中文</a>
</p>

<p align="center">
  为 <a href="https://github.com/NousResearch/hermes-agent">Hermes Agent</a> 打造的完整功能桌面应用与 Web 仪表盘。<br/>
  管理 AI 对话会话、监控用量与成本、配置平台通道、<br/>
  调度定时任务、浏览技能库 —— 全部通过简洁响应式的 Web 界面完成。
</p>

<p align="center">
  <a href="https://github.com/EKKOLearnAI/hermes-web-ui/releases/latest">下载 Hermes Studio 桌面版</a>
  ·
  <code>npm install -g hermes-web-ui && hermes-web-ui start</code>
</p>

<p align="center">
  <img src="https://github.com/EKKOLearnAI/hermes-web-ui/blob/main/packages/client/src/assets/image1.png" alt="Hermes Web UI Demo" width="680"/>
</p>

<p align="center">
  <img src="https://github.com/EKKOLearnAI/hermes-web-ui/blob/main/packages/client/src/assets/image2.png" alt="Hermes Web UI Demo" width="680"/>
</p>

<p align="center">
  <a href="https://www.npmjs.com/package/hermes-web-ui"><img src="https://img.shields.io/npm/v/hermes-web-ui?style=flat-square&color=blue" alt="npm version"/></a>
  <a href="https://github.com/EKKOLearnAI/hermes-web-ui/blob/main/LICENSE"><img src="https://img.shields.io/npm/l/hermes-web-ui?style=flat-square" alt="license"/></a>
  <a href="https://github.com/EKKOLearnAI/hermes-web-ui/stargazers"><img src="https://img.shields.io/github/stars/EKKOLearnAI/hermes-web-ui?style=flat-square" alt="stars"/></a>
</p>

---

## 功能特性

### AI 对话聊天

- 通过 Socket.IO `/chat-run` 实现实时聊天流式传输；对话运行经由 Hermes Agent 桥接器执行
- 多会话管理 —— 创建、重命名、删除及切换会话
- **自建会话数据库** —— Web UI 使用本地 SQLite 存储；Hermes `state.db` 仅作为历史 API 的只读数据源
- 按来源（Telegram、Discord、Slack 等）分组会话，支持折叠式手风琴面板
- 活跃会话指示器 —— 实时会话置顶并显示旋转加载图标
- 按最新消息时间排序会话
- Markdown 渲染，支持语法高亮与代码复制
- 工具调用详情展开（参数/结果）
- 基于配置文件的文件上传
- 支持文件下载 —— 可通过解析路径下载已上传的文件及 Agent 生成的文件，支持本地、Docker、SSH 和 Singularity 后端
- 会话搜索 —— 使用 `Ctrl+K` 在 Web UI 本地会话数据库中搜索；只读的 Hermes 历史会话不包含在内
- 配置文件感知模型选择器 —— 通过已授权的 Hermes 配置文件发现登录账户可用的模型
- 按会话显示模型标识及上下文 Token 用量

### 平台通道

在单个页面统一配置 **8 个平台**：

| Platform      | Features                                                               |
| ------------- | ---------------------------------------------------------------------- |
| Telegram      | Bot Token、@提及控制、表情回应、自由回复对话                             |
| Discord       | Bot Token、@提及、自动创建线程、表情回应、频道允许/忽略列表              |
| Slack         | Bot Token、@提及控制、Bot 消息处理                                     |
| WhatsApp      | 启用/禁用、@提及控制、提及模式                                         |
| Matrix        | 访问 Token、Homeserver、自动创建线程、私聊 @提及线程                     |
| Feishu (Lark) | 应用 ID/密钥、@提及控制                                                |
| WeChat        | 二维码登录（浏览器扫码，自动保存凭证）                                 |
| WeCom         | Bot ID/密钥                                                            |

- 凭证管理写入至 `~/.hermes/.env`
- 通道行为设置写入至 `~/.hermes/config.yaml`
- 按平台检测已配置/未配置状态

### 用量分析

- Token 总用量明细（输入/输出）
- 会话数量及日均统计
- 预估成本追踪与缓存命中率
- 模型使用分布图
- 近 30 天每日趋势（柱状图 + 数据表）

### 定时任务

- 创建、编辑、暂停、恢复及删除 Cron 任务
- 支持立即触发执行
- Cron 表达式快捷预设

### 模型管理

- 从凭证池（`~/.hermes/auth.json`）自动发现模型
- 通过各提供商端点获取可用模型（`/v1/models`）
- 添加、更新及删除提供商（内置预设与自定义 OpenAI 兼容接口）
- 支持 OpenAI Codex 与 Nous Portal OAuth 登录
- 自动检测非 v1 API 版本的提供商 URL（如 `/v4`）
- 按提供商对模型进行分组，支持切换默认模型

### 多配置文件管理

- 创建、重命名、删除及切换 Hermes 配置文件
- 克隆现有配置文件或从归档文件（`.tar.gz`）导入
- 导出配置文件用于备份或共享
- 配置、缓存、上传、会话、任务、用量、记忆库、技能、插件、提供商及模型可见性均按配置文件隔离管理
- 账户绑定配置文件访问权限：超级管理员可管理所有配置文件；普通管理员仅可查看和使用分配给其账户的配置文件

### 文件浏览器

- 浏览远程后端上的文件（本地、Docker、SSH、Singularity）
- 支持上传、下载、重命名、复制、移动及删除文件
- 上传文件存储于所选/请求的 Hermes 配置文件下，同时保持基于路径的下载功能以支持 Agent 生成在上传目录外的产物
- 创建目录
- 查看文件内容并支持语法高亮

### 群聊

- 多 Agent 聊天室，通过 Socket.IO 实现实时消息通信
- @提及路由 —— @指定 Agent 触发上下文回复
- 上下文压缩 —— 历史记录超出 Token 阈值时自动进行对话摘要总结
- 打字状态与回复进度指示器
- 支持聊天室创建、删除及邀请码管理
- Agent 管理 —— 按独立配置文件向房间添加/移除 Agent
- SQLite 消息持久化存储
- 移动端响应式布局，侧边栏支持折叠

### 技能与记忆库

- 浏览并搜索已安装的技能
- 查看技能详情及关联文件
- 用户笔记与配置文件管理

### 日志

- 查看 Agent/服务器/错误日志
- 支持按日志级别、日志文件及关键词筛选
- 结构化日志解析，HTTP 访问日志高亮显示

### 身份认证

- 基于 Token 的认证（首次运行自动生成或通过 `AUTH_TOKEN` 环境变量设置）
- 用户名/密码登录，支持在设置中管理账户
- 默认初始凭证为 `admin` / `123456`；登录后将提示用户修改默认用户名和密码
- 超级管理员可管理用户及配置文件绑定关系；普通管理员仅可管理自己的账户信息

CLI maintenance commands:

```bash
# Delete persisted login IP lock records
hermes-web-ui clear-login-locks

# Delete login locks and restart the running Web UI process
hermes-web-ui clear-login-locks --restart

# Create or reset the default super administrator login to admin / 123456
hermes-web-ui reset-default-login
```

`clear-login-locks` removes `${HERMES_WEB_UI_HOME:-~/.hermes-web-ui}/.login-lock.json`. If the server is running, restart it to clear in-memory lock state. `reset-default-login` updates the Web UI account database; if an `admin` user already exists, its password is reset to `123456` and the account is enabled as a super administrator.

### 设置

- 显示（流式传输、紧凑模式、推理过程、成本展示）
- Agent（最大轮次、超时时间、工具调用强制启用）
- 记忆库（启用/禁用、字符限制）
- 会话重置（空闲超时、定时重置）
- 隐私（个人身份信息 PII 脱敏）
- 模型设置（默认模型与提供商）
- 配置文件与提供商配置

### Web 终端

- 集成终端，基于 `node-pty` 和 `@xterm/xterm` 驱动
- 支持多会话 —— 创建、切换及关闭终端会话
- 通过 WebSocket 实现实时键盘输入与 PTY 输出流式传输
- 支持窗口尺寸调整

---

## 快速开始

### 桌面应用（推荐）

从 [GitHub Releases](https://github.com/EKKOLearnAI/hermes-web-ui/releases/latest) 下载最新的 **Hermes Studio** 桌面安装程序。

桌面版已发布 macOS、Windows 和 Linux 构建版本，并提供相应的架构资源文件。桌面应用内置了 Web UI 运行时环境，并将 Hermes Agent 数据存储在原生路径中：

- Windows：%LOCALAPPDATA%\hermes（回退至 %APPDATA%\hermes）
- macOS/Linux：`~/.hermes`

桌面包装器将自身的 Web UI 状态独立存储于 `~/.hermes-web-ui`，除非设置了 `HERMES_WEB_UI_HOME`。

### npm

```bash
npm install -g hermes-web-ui
hermes-web-ui start
```

访问 **http://localhost:8648**

### Docker Compose

单容器部署，内置集成 Hermes Agent：

```bash
# Use pre-built image (Recommended)
WEBUI_IMAGE=ekkoye8888/hermes-web-ui docker compose up -d

# Or build from source
docker compose up -d --build

docker compose logs -f hermes-webui
```

访问 **http://localhost:6060**

- 持久化 Hermes 数据存储在 `./hermes_data`
- Web UI 认证 Token 存储在 `./hermes_data/hermes-web-ui/.token`
- 首次启用认证运行时，Token 将打印至容器日志中
- 所有运行时设置均通过 `docker-compose.yml` 中的环境变量驱动

详细说明与故障排查请参阅 [`docs/docker.md`](./docs/docker.md)。

### Hermes Agent 运行时自动发现

当 Web UI 启动后端聊天功能时，优先查找包含 `run_agent.py` 的源码目录（如 `~/.hermes/hermes-agent`）。若未找到源码目录，则回退至已安装 `hermes` 命令所使用的 Python 环境，最后尝试系统 Python。此机制同时支持源码部署与包管理安装（如 `pip install hermes-agent`）。

## Web UI 环境变量

这些变量用于配置 Hermes Web UI、本地 Hermes 运行时集成以及开发/预览辅助功能。提供商 API Key 和 Hermes Agent 设置通常通过 Hermes 配置文件管理；此处提供的环境变量为进程级覆盖选项。

| Variable | Default | Description |
| --- | --- | --- |
| `PORT` | `8648` | Web UI 监听端口。 |
| `BIND_HOST` | `0.0.0.0` | Web UI 绑定主机地址。IPv6 请显式设置为 `::`。 |
| `HERMES_WEB_UI_HOME` | `~/.hermes-web-ui` | Web UI 数据主目录，用于存放认证 Token、凭证、日志、数据库及默认上传文件。同时支持兼容别名 `HERMES_WEBUI_STATE_DIR`。 |
| `HERMES_WEBUI_STATE_DIR` | unset | `HERMES_WEB_UI_HOME` 的兼容别名。 |
| `UPLOAD_DIR` | `$HERMES_WEB_UI_HOME/upload` | 上传根目录覆盖路径。文件将按配置文件隔离的子目录存储。 |
| `CORS_ORIGINS` | `*` | Koa CORS 跨域来源设置。 |
| `AUTH_TOKEN` | auto-generated | 显式 Bearer Token。若未设置，Web UI 将在 `HERMES_WEB_UI_HOME` 下自动生成。 |
| `AUTH_JWT_SECRET` | `AUTH_TOKEN` | 用户名/密码会话的 JWT 签名密钥覆盖值。 |
| `PROFILE` | `default` | 启动/默认 Hermes 配置文件。运行时请求将使用前端选择且当前账户已授权的配置文件。 |
| `LOG_LEVEL` | `info` | 服务器日志级别。 |
| `BRIDGE_LOG_LEVEL` | `$LOG_LEVEL` or `info` | 桥接器日志级别。 |
| `MAX_DOWNLOAD_SIZE` | `200MB` | 最大文件下载大小限制。 |
| `MAX_EDIT_SIZE` | `10MB` | 可编辑文件大小上限。 |
| `WORKSPACE_BASE` | `/opt/data/workspace` | 工作区浏览的基础目录。 |
| `HERMES_HOME` | platform default | Hermes 数据主路径。Windows 使用 `%LOCALAPPDATA%\hermes`；macOS/Linux 使用 `~/.hermes`。 |
| `HERMES_BIN` | `hermes` | 自定义 Hermes CLI 可执行文件路径。 |
| `HERMES_AGENT_ROOT` | auto-discovered | 包含 `run_agent.py` 的 Hermes Agent 源码目录。 |
| `HERMES_AGENT_BRIDGE_PYTHON` | auto-discovered | 用于启动 Agent 桥接器的 Python 解释器路径。 |
| `HERMES_AGENT_BRIDGE_UV` | auto-discovered | 可用时用于启动 Agent 桥接器的 `uv` 可执行文件路径。 |
| `UV` | auto-discovered | 备用 `uv` 可执行文件路径。 |
| `PYTHON` | auto-discovered | Agent 桥接器备用的 Python 可执行文件路径。 |
| `HERMES_AGENT_BRIDGE_ENDPOINT` | platform default | Agent 桥接器代理端点。Windows 默认为 `tcp://127.0.0.1:18765`；macOS/Linux 默认为 `ipc:///tmp/hermes-agent-bridge.sock`。 |
| `HERMES_AGENT_BRIDGE_TIMEOUT_MS` | `120000` | Node.js 请求桥接代理的超时时间（毫秒）。 |
| `HERMES_AGENT_BRIDGE_CONNECT_RETRY_MS` | `5000` | 连接桥接 Socket 的重试间隔窗口（毫秒）。 |
| `HERMES_AGENT_BRIDGE_STARTUP_TIMEOUT_MS` | `120000` | 等待 Python 桥接器就绪的超时时间（毫秒）。 |
| `HERMES_AGENT_BRIDGE_AUTO_RESTART` | enabled | 异常退出后自动重启桥接代理。设置为 `0`、`false`、`no` 或 `off` 可禁用。 |
| `HERMES_AGENT_BRIDGE_RESTART_DELAY_MS` | `1000` | 桥接器自动重启退避的基础延迟（毫秒）。 |
| `HERMES_AGENT_BRIDGE_PLATFORM` | `cli` | 传递给 Hermes Agent 的平台标识。 |
| `HERMES_AGENT_BRIDGE_WORKER_TRANSPORT` | platform default | 配置文件工作进程传输协议。设置为 `tcp` 使用回环 TCP，或 `ipc`/`unix` 使用 Unix 域套接字；默认 Windows 为 TCP，macOS/Linux 为 IPC。 |
| `HERMES_AGENT_BRIDGE_WORKER_PORT_BASE` | `18780` | TCP 工作进程端点的基准端口。 |
| `HERMES_BRIDGE_PROVIDER` | profile/default | 桥接运行时的提供商覆盖配置。 |
| `HERMES_BRIDGE_TOOLSETS` | profile/default | 桥接运行时的工具集覆盖配置。 |
| `HERMES_BRIDGE_MAX_TURNS` | profile/default | 桥接运行的最大轮次覆盖配置。 |
| `HERMES_BRIDGE_SUPPRESS_PLATFORM_HINT` | `cli` | 控制传递给 Hermes Agent 的桥接平台提示抑制行为。 |
| `HERMES_OPENROUTER_APP_REFERER` | `https://hermes-studio.ai` | 桥接运行时发送的 OpenRouter 归属 Referer。 |
| `HERMES_OPENROUTER_APP_TITLE` | `Hermes Web UI` | 桥接运行时发送的 OpenRouter 归属标题。 |
| `HERMES_OPENROUTER_APP_CATEGORIES` | `cli-agent,personal-agent` | 桥接运行时发送的 OpenRouter 归属分类。 |
| `HERMES_WEB_UI_MANAGED_GATEWAY` | platform/runtime dependent | 强制使用托管的传统网关进程处理机制。设置为 `1`、`true`、`yes` 或 `on` 可启用。 |
| `HERMES_WEB_UI_STOP_GATEWAYS_ON_SHUTDOWN` | enabled in production | 控制 Web UI 关闭时是否同时停止托管的网关进程。设置为 `0` 或 `false` 可分离独立运行。 |
| `GATEWAY_HOST` | `127.0.0.1` | 写入配置文件以兼容传统网关的默认网关主机地址。 |
| `HERMES_WEB_UI_PREVIEW_REPO` | package repository | 版本预览功能使用的 GitHub 仓库。 |
| `HERMES_WEB_UI_PREVIEW_AGENT_BRIDGE_TRANSPORT` | platform default | 版本预览代理传输协议。在 macOS/Linux 上设置为 `tcp` 可使用回环 TCP；若未设置，则遵循 `HERMES_AGENT_BRIDGE_WORKER_TRANSPORT=tcp`。 |
| `HERMES_WEB_UI_PREVIEW_AGENT_BRIDGE_ENDPOINT` | isolated preview endpoint | 直接覆盖版本预览的代理端点。 |
| `HERMES_WEB_UI_BACKEND_PORT` | `8648` | Vite 开发代理使用的后端端口。 |
| `HERMES_WEB_UI_FRONTEND_PORT` | `8649` | 前端 Vite 开发服务器端口。 |

### CLI 命令

| Command                           | Description                        |
| --------------------------------- | ---------------------------------- |
| `hermes-web-ui start`             | 后台启动（守护进程模式）           |
| `hermes-web-ui start --port 9000` | 在指定端口启动                     |
| `hermes-web-ui stop`              | 停止后台进程                       |
| `hermes-web-ui restart`           | 重启后台进程                       |
| `hermes-web-ui status`            | 检查运行状态                       |
| `hermes-web-ui update`            | 更新至最新版本并重启               |
| `hermes-web-ui upgrade`           | `update` 的别名                    |
| `hermes-web-ui -v`                | 显示版本号                         |
| `hermes-web-ui -h`                | 显示帮助信息                       |

`update` / `upgrade` 会先尝试执行 `npm cache clean --force`，随后运行 `npm install -g hermes-web-ui@latest` 并重启。缓存清理为尽力操作；若失败，更新器将继续执行安装流程。

### 自动配置

启动时 BFF 服务器将自动：

- 初始化 Web UI 数据目录、本地数据库及内置技能库
- 启动 `/chat-run` 所需的 Hermes Agent 桥接器
- 成功启动后自动打开浏览器

---

## 开发指南

```bash
git clone https://github.com/EKKOLearnAI/hermes-web-ui.git
cd hermes-web-ui
npm install
npm run dev
```

- Frontend: http://localhost:8649
- BFF Server: http://localhost:8647

```bash
npm run build   # outputs to dist/
```

See [DEVELOPMENT.md](./DEVELOPMENT.md) for project development guidelines.

## 架构设计

```
Browser → BFF (Koa, :8648) → Socket.IO /chat-run
                ↓
        Hermes agent bridge → Hermes Agent runtime
                ↓
           Hermes CLI / profiles
           profile config.yaml    (channel/provider behavior)
           profile auth.json      (credential pool)
           Tencent iLink API      (WeChat QR login)
```

前端采用**多 Agent 扩展架构**设计 —— 所有与 Hermes 相关的代码均命名空间化至 `hermes/` 目录下（包含 API、组件、视图、状态管理），便于在此基础上无缝添加新的 Agent 集成。

BFF 层负责处理 Socket.IO 聊天流式传输、Hermes Agent 桥接器、基于配置文件的文件上传与基于路径的下载（支持多后端：本地/Docker/SSH/Singularity）、会话增删改查、账户与配置文件级管理、配置/凭证管理、微信二维码登录、模型发现、技能/记忆库管理、日志读取及静态文件服务。

## 技术栈

**前端：** Vue 3 + TypeScript + Vite + Naive UI + Pinia + Vue Router + vue-i18n + SCSS + markdown-it + highlight.js

**后端：** Koa 2（BFF 服务器）+ node-pty（Web 终端）

## Star 历史

[![Star History Chart](https://api.star-history.com/svg?repos=EKKOLearnAI/hermes-web-ui&type=Date)](https://star-history.com/#EKKOLearnAI/hermes-web-ui&Date)

<!-- If the chart above doesn't load, visit https://star-history.com/#EKKOLearnAI/hermes-web-ui -->

## 许可证

[BSL-1.1](./LICENSE)
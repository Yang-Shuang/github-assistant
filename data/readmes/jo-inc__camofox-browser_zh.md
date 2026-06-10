<div align="center">
  <img src="fox.png" alt="camofox-browser" width="200" />
  <h1>camofox-browser</h1>
  <p><strong>基于 Camoufox 的 AI Agent 反检测浏览器服务器</strong></p>
  <p>
    <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="License: MIT" /></a>
    <a href="https://github.com/jo-inc/camofox-browser/stargazers"><img src="https://img.shields.io/github/stars/jo-inc/camofox-browser" alt="GitHub stars" /></a>
    <a href="https://www.npmjs.com/package/camofox-browser"><img src="https://img.shields.io/npm/v/camofox-browser" alt="npm version" /></a>
    <a href="https://github.com/jo-inc/camofox-browser/commits"><img src="https://img.shields.io/github/last-commit/jo-inc/camofox-browser" alt="GitHub last commit" /></a>
  </p>
  <p>
    站在巨人的肩膀上：<a href="https://camoufox.com">Camoufox</a> —— 一款在 C++ 层面实现指纹伪造的 Firefox 分支浏览器。
  </p>
</div>

<br/>

> <a href="https://askjo.ai?ref=camofox"><img src="jo-logo.png" alt="Jo" width="80" height="80" align="left" /></a>
>
> 由 <a href="https://askjo.ai?ref=camofox"><strong>个人 AI Agent jo 的开发团队</strong></a> 打造。jo 一半运行在你的 Mac 上，另一半运行在专为你搭建的云端机器中——完全零维护。支持 macOS、Telegram、WhatsApp 和邮件。<a href="https://askjo.ai?ref=camofox">免费试用 Beta 版 -></a>

<br/>

```bash
git clone https://github.com/jo-inc/camofox-browser && cd camofox-browser
npm install && npm start
# -> http://localhost:9377
```

---

## Why

AI Agent 需要浏览真实的网页。但使用 Playwright 容易被封禁，无头 Chrome 会被采集指纹，而隐身插件本身反而会成为指纹特征。

Camoufox 在 **C++ 实现层面** 对 Firefox 进行底层修补 —— `navigator.hardwareConcurrency`、WebGL 渲染器、AudioContext、屏幕几何信息、WebRTC 等，均在 JavaScript 执行前完成伪造。没有垫片（shims），没有包装层，不留痕迹。

本项目将该引擎封装为专为 Agent 设计的 REST API：提供无障碍快照（而非臃肿的原始 HTML）、稳定的元素引用以便点击，以及常用网站的搜索宏。

## Features

- **C++ 级反检测** - 绕过 Google、Cloudflare 及绝大多数机器人检测机制
- **元素引用（Element Refs）** - 提供稳定的 `e1`、`e2`、`e3` 标识符，确保可靠交互
- **节省 Token** - 无障碍快照体积比原始 HTML 小约 90%
- **全平台运行** - 延迟启动浏览器 + 空闲自动关闭，闲置时内存仅占 ~40MB。专为与其他服务共享服务器设计——树莓派、$5 VPS 或共享基础设施均可胜任。
- **会话隔离（Session Isolation）** - 每个用户独立的 Cookie/存储数据
- **Cookie 导入** - 支持注入 Netscape 格式的 Cookie 文件以实现已登录状态浏览
- **代理与地理位置（Proxy + GeoIP）** - 通过住宅代理路由流量，并自动匹配对应的语言区域/时区
- **结构化日志** - 输出带请求 ID 的 JSON 格式日志行，便于生产环境可观测性监控
- **YouTube 字幕提取** - 通过 yt-dlp 从任意 YouTube 视频提取字幕，无需 API Key
- **搜索宏（Search Macros）** - `@google_search`、`@youtube_search`、`@amazon_search`、`@reddit_subreddit` 等 13 种常用站点快捷指令
- **快照截图** - 可在无障碍快照旁附带 Base64 格式的 PNG 截图
- **大页面处理** - 自动截断长快照，支持基于偏移量的分页
- **下载捕获** - 拦截浏览器下载文件并通过 API 获取（可选内联 Base64）
- **DOM 图片提取** - 列出 `<img>` `src`/`alt`，并可选择返回内联 Data URL
- **随处部署** - Docker、Fly.io、Railway
- **VNC 交互式登录** - 通过 noVNC 可视化登录网站，并导出存储状态供 Agent 复用
- **OpenAPI 文档** - 自动生成规范文件至 [`/openapi.json`](http://localhost:9377/openapi.json)，并提供交互式文档界面 [`/docs`](http://localhost:9377/docs)
- **结构化提取（Structured Extract）** - `POST /tabs/:tabId/extract`，通过 JSON Schema 的 `x-ref` 将属性映射到快照元素引用
- **会话追踪（Session Tracing）** - 可选按会话捕获 Playwright 追踪记录（含截图、DOM 快照、网络请求），并提供 API 端点用于列表查看、下载和删除追踪压缩包
- **遥测数据（Telemetry）** - 自动通过 GitHub Issues 上报[匿名化的崩溃/挂起遥测数据](lib/reporter.js#L28-L290)。用于识别导致故障的网站及常见失败模式。私有域名经 HMAC 哈希处理，路径和参数被剥离，Token/IP 已脱敏。可通过设置 `CAMOFOX_CRASH_REPORT_ENABLED=false` 关闭上报。

## Optional Dependencies

| Dependency | Purpose | Install |
|-----------|---------|---------|
| [yt-dlp](https://github.com/yt-dlp/yt-dlp) | YouTube 字幕提取（快速路径） | `pip install yt-dlp` 或 `brew install yt-dlp` |

Docker 镜像已内置 yt-dlp。若用于本地开发，请安装该依赖以启用 `/youtube/transcript` 端点。未安装时，该端点将回退至较慢的基于浏览器的方法。

## Quick Start

### OpenClaw Plugin

```bash
openclaw plugins install @askjo/camofox-browser
```

**Tools:** `camofox_create_tab`  |  `camofox_snapshot`  |  `camofox_click`  |  `camofox_type`  |  `camofox_navigate`  |  `camofox_scroll`  |  `camofox_screenshot`  |  `camofox_close_tab`  |  `camofox_list_tabs`  |  `camofox_import_cookies`

### Standalone

通过 npm 运行：

```bash
npx @askjo/camofox-browser
```

或从源码运行：

```bash
git clone https://github.com/jo-inc/camofox-browser
cd camofox-browser
npm install
npm start  # downloads Camoufox on first run (~300MB)
```

默认端口为 `9377`。所有可选配置请参见[环境变量](#environment-variables)。

> **注意：**安装后脚本（postinstall）会在拉取 Camoufox 二进制文件前自行清除 `PLAYWRIGHT_SKIP_BROWSER_DOWNLOAD` 变量。若不进行此覆盖，已导出的 `PLAYWRIGHT_SKIP_BROWSER_DOWNLOAD=1`（通常在 Playwright 配置为使用系统 Chrome 时常见）会静默跳过下载，导致服务器运行时崩溃。
>
> **外部 Camoufox 可执行文件：**在运行 `npm install` 及启动服务前设置 `CAMOUFOX_EXECUTABLE=/path/to/camoufox-bin`，即可跳过内置下载并直接调用该可执行文件。兼容别名包括 `CAMOUFOX_EXECUTABLE_PATH` 和 `CAMOFOX_EXECUTABLE_PATH`。适用于 NixOS 路径（如 `/nix/store/.../camoufox-bin`）；该可执行文件必须来自包含 `properties.json`、`version.json` 和 `fontconfig/` 的 Camoufox 发行包。
>
> **离线或自定义二进制管理：**若已拥有 Camoufox 发行包，建议优先使用 `CAMOUFOX_EXECUTABLE`。否则可通过 `npm install --ignore-scripts`（跳过所有依赖的生命周期脚本，最粗暴的方式）或更精准地通过 `npm install --omit=optional` 配合手动执行 `npx camoufox-js fetch` 来禁用自动拉取。注意：`PLAYWRIGHT_SKIP_BROWSER_DOWNLOAD=1 npm install` 已不再跳过 Camoufox 下载（postinstall 会在本地清理该环境变量）；如需跳过，请使用 `--ignore-scripts` 或设置 `CAMOUFOX_EXECUTABLE`。

### Docker

内置的 `Makefile` 会自动检测你的 CPU 架构，并在 Docker 构建外部预下载 Camoufox 和 yt-dlp 二进制文件，因此重新构建速度极快（约 30s vs ~3min）。

```bash
# Build and start (auto-detects arch: aarch64 on M1/M2, x86_64 on Intel)
make up

# Stop and remove the container
make down

# Force a clean rebuild (e.g. after upgrading VERSION/RELEASE)
make reset

# Just download binaries (without building)
make fetch

# Override arch or version explicitly
make up ARCH=x86_64
make up VERSION=135.0.1 RELEASE=beta.24
```

#### Windows

在 Windows 上不可用 `make`。请改用内置的 `build.ps1` PowerShell 脚本：

```powershell
# Build and start
.\build.ps1 up

# Stop and remove the container
.\build.ps1 down

# Build image only
.\build.ps1 build

# Force a clean rebuild
.\build.ps1 reset

# Download binaries only (without building)
.\build.ps1 fetch

# Override architecture
.\build.ps1 up -Arch x86_64
.\build.ps1 up -Arch aarch64
```

> **注意：**推荐使用 PowerShell 7+（`pwsh`），但 `powershell.exe`（Windows PowerShell 5.1）也可正常工作。该脚本要求安装带有 WSL2 后端的 Docker Desktop for Windows。
>
> **换行符注意：**本项目包含一个 `.gitattributes` 文件，强制 `.sh` 脚本使用 Unix（`LF`）换行符。如果你已克隆仓库并在 `docker build` 期间遇到 `sh: not found` 或 `set: Illegal option -` 错误，请运行：
> ```powershell
> Get-ChildItem -Recurse *.sh | ForEach-Object { (Get-Content $_) -join "`n" + "`n" | Set-Content $_ -NoNewline }
> ```
> 这将把脚本转换为 LF 换行符。得益于 `.gitattributes`，未来克隆将自动处理此问题。

> **警告：请勿直接运行 `docker build`。** Dockerfile 使用绑定挂载从 `dist/` 拉取预下载的二进制文件。请始终使用 `make up`（或先执行 `make fetch` 再执行 `make build`）——它会先下载二进制文件。

### Fly.io

对于 Fly.io 或其他远程 CI，你需要一个在构建时下载二进制文件的 Dockerfile（而非使用绑定挂载）。

### Railway

已内置 `railway.toml`。该配置使用 `Dockerfile.ci`（在构建时下载二进制文件），并自动将 Railway 的 `PORT` 环境变量映射为 `CAMOFOX_PORT`。

```bash
# Install Railway CLI, then:
railway link
railway up
```

通过 Railway Dashboard 或 CLI 设置密钥：
```bash
railway variables set CAMOFOX_API_KEY="your-generated-key"
```

## Usage

### Cookie Import

将浏览器中的 Cookie 导入 Camoufox，以跳过 LinkedIn、Amazon 等网站的交互式登录。

#### Setup

**1. 生成密钥：**

```bash
# macOS / Linux
openssl rand -hex 32
```

**2. 在启动 OpenClaw 前设置环境变量：**

```bash
export CAMOFOX_API_KEY="your-generated-key"
openclaw start
```

该密钥同时用于插件（验证请求）和服务端（校验签名）。两者运行在同一环境中，只需设置一次。

> **为何使用环境变量？** 该密钥属于敏感信息。`openclaw.json` 中的插件配置以明文存储，因此不适合存放密钥。请在 Shell 配置文件、systemd 单元文件、Docker 环境变量或 Fly.io Secrets 中设置 `CAMOFOX_API_KEY`。

> **默认禁用 Cookie 导入。** 若未设置 `CAMOFOX_API_KEY`，服务端将拒绝所有 Cookie 请求并返回 403。

**3. 从浏览器导出 Cookie：**

安装支持导出 Netscape 格式 Cookie 文件的浏览器扩展（例如 Chrome/Firefox 的 "cookies.txt"）。导出你需要登录的网站对应的 Cookie。

**4. 放置 Cookie 文件：**

```bash
mkdir -p ~/.camofox/cookies
cp ~/Downloads/linkedin_cookies.txt ~/.camofox/cookies/linkedin.txt
```

默认目录为 `~/.camofox/cookies/`。可通过 `CAMOFOX_COOKIES_DIR` 覆盖。

**5. 让 Agent 导入：**

> Import my LinkedIn cookies from linkedin.txt

Agent 会调用 `camofox_import_cookies` -> 读取文件 -> 携带 Bearer Token POST 至服务端 -> Cookie 注入浏览器会话。后续对 linkedin.com 的 `camofox_create_tab` 请求将自动保持已登录状态。

#### How it works

```
~/.camofox/cookies/linkedin.txt          (Netscape format, on disk)
        |
        v
camofox_import_cookies tool              (parses file, filters by domain)
        |
        v  POST /sessions/:userId/cookies
        |  Authorization: Bearer <CAMOFOX_API_KEY>
        |  Body: { cookies: [Playwright cookie objects] }
        v
camofox server                           (validates, sanitizes, injects)
        |
        v  context.addCookies(...)
        |
Camoufox browser session                 (authenticated browsing)
```

- `cookiesPath` 相对于 Cookie 目录解析——禁止越权路径遍历
- 单次请求最多导入 500 个 Cookie，文件体积限制为 5MB
- Cookie 对象会经过清理，仅保留 Playwright 允许的字段

### Session Persistence

默认情况下，camofox 会将每个用户的 Cookie 和 localStorage 持久化至 `~/.camofox/profiles/`。会话状态会随浏览器重启而保留——只需登录一次（通过 Cookie 或 VNC），后续会话将自动恢复已认证状态。

```
~/.camofox/
|-- cookies/          # Bootstrap cookie files (Netscape format)
\-- profiles/         # Persisted session state (auto-managed)
    \-- <hashed-userId>/
        \-- storage_state.json
```

可通过 `CAMOFOX_PROFILE_DIR` 覆盖目录，或在持久化插件配置中设置 `"profileDir"`。若要禁用持久化，请在 `camofox.config.json` 中设置 `"persistence": { "enabled": false }`。

### Session Tracing

捕获会话中每一步操作的 Playwright 追踪记录：页面截图、DOM 快照、网络请求及控制台输出。输出为单个 `.zip` 文件，可直接在 Playwright 内置的 Trace Viewer 中打开查看。

在打开第一个标签页时传入 `trace: true` 即可按会话开启追踪：

```bash
curl -X POST http://localhost:9377/tabs \
  -H 'Content-Type: application/json' \
  -d '{"userId":"agent1","sessionKey":"task1","url":"https://example.com","trace":true}'
```

会话关闭时会写入追踪文件。关闭会话以刷新数据，随后即可查看、下载和删除：

```bash
# Close the session to flush the trace
curl -X DELETE http://localhost:9377/sessions/agent1

# List trace files
curl http://localhost:9377/sessions/agent1/traces
# {"traces":[{"filename":"trace-2026-04-18T04-05-00-...zip","sizeBytes":42810,"createdAt":...}]}

# Download (Content-Type: application/zip)
curl http://localhost:9377/sessions/agent1/traces/trace-2026-04-18T04-05-00-abc.zip > session.zip

# View it in Playwright's Trace Viewer
npx playwright show-trace session.zip

# Delete
curl -X DELETE http://localhost:9377/sessions/agent1/traces/trace-2026-04-18T04-05-00-abc.zip
```

**为何使用追踪而非视频？** Camoufox 基于 Firefox，而 Playwright 的 `recordVideo` 仅支持 Chromium。追踪功能在 Firefox 上同样有效，且提供的信息比视频更丰富（包含网络、DOM、控制台及截图）。

无法对已存在的会话动态切换追踪开关。如需修改该选项，请先调用 `DELETE /sessions/:userId` 关闭会话。

存储默认位于 `~/.camofox/traces/<hashed-userId>/`，并在服务端启动时自动清理：
- `CAMOFOX_TRACES_DIR` - 基础目录（默认: `~/.camofox/traces`）
- `CAMOFOX_TRACES_MAX_BYTES` - 单个追踪文件最大体积，超出将在下次启动时被移除（默认: 50MB）
- `CAMOFOX_TRACES_TTL_HOURS` - 超过此时长的追踪记录将在下次启动时被清理（默认: 24）

#### Standalone server usage

```bash
curl -X POST http://localhost:9377/sessions/agent1/cookies \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer YOUR_CAMOFOX_API_KEY' \
  -d '{"cookies":[{"name":"foo","value":"bar","domain":"example.com","path":"/","expires":-1,"httpOnly":false,"secure":false}]}'
```

#### Docker / Fly.io / Railway

```bash
docker run -p 9377:9377 \
  -e CAMOFOX_API_KEY="your-generated-key" \
  -v ~/.camofox/cookies:/home/node/.camofox/cookies:ro \
  camofox-browser
```

对于 Fly.io：
```bash
fly secrets set CAMOFOX_API_KEY="your-generated-key"
```

对于 Railway：
```bash
railway variables set CAMOFOX_API_KEY="your-generated-key"
```

### Proxy + GeoIP

通过代理路由所有浏览器流量，并利用 Camoufox 内置的 GeoIP 功能自动匹配语言区域、时区及地理位置。

**基础代理（单端点）：**

```bash
export PROXY_HOST=166.88.179.132
export PROXY_PORT=46040
export PROXY_USERNAME=myuser
export PROXY_PASSWORD=mypass
npm start
```

**回连代理（旋转固定会话）：** 适用于提供单一网关端点并支持基于会话的固定 IP 的服务商，如 Decodo、Bright Data 或 Oxylabs：

```bash
export PROXY_STRATEGY=backconnect
export PROXY_BACKCONNECT_HOST=gate.provider.com
export PROXY_BACKCONNECT_PORT=7000
export PROXY_USERNAME=myuser
export PROXY_PASSWORD=mypass
npm start
```

每个浏览器上下文都会分配一个独立的固定会话，从而确保不同用户获得不同的 IP 地址。遇到代理错误或被 Google 拦截时，会话会自动轮换。

或在 Docker 中：

```bash
docker run -p 9377:9377 \
  -e PROXY_HOST=166.88.179.132 \
  -e PROXY_PORT=46040 \
  -e PROXY_USERNAME=myuser \
  -e PROXY_PASSWORD=mypass \
  camofox-browser
```

配置代理后：
- 所有流量均通过代理路由
- Camoufox 的 GeoIP 会自动将 `locale`、`timezone` 和 `geolocation` 设置为与代理出口 IP 匹配的值
- 浏览器指纹（语言、时区、坐标）将与代理位置保持一致
- 未配置代理时，默认使用 `en-US`、`America/Los_Angeles` 及旧金山坐标

### Telemetry

浏览器自动化的失败模式往往难以预测——Cloudflare 人机验证、网站改版导致选择器失效、重定向循环、弹窗风暴或渲染器崩溃。故障范围广泛且模式多样。若无遥测数据，唯一的反馈就是“它没起作用”。

遥测数据为我们提供结构化的故障信息：*哪些网站会失败*、*如何失败*以及*发生频率*，从而帮助我们优先修复真正影响用户的问题模式。当出现以下情况时，系统会自动提交 GitHub Issue：
- **未捕获异常（Uncaught exceptions）** 导致进程崩溃
- **事件循环阻塞** 超过 5 秒（通过看门狗检测）
- **挫败感模式（Frustration patterns）** —— 同一标签页连续失败 3+ 次（超时、上下文失效、导航中止）

每次上报均包含故障类型、堆栈跟踪、标签页健康指标（HTTP 状态分布、控制台错误、请求失败数、重定向深度）及目标网址——所有数据均已匿名化。

#### How it works

遥测数据发送至轻量级 Cloudflare Worker 端点 [`https://camofox-telemetry.askjo.workers.dev`](https://camofox-telemetry.askjo.workers.dev/health)。该端点将 GitHub App 凭证作为环境变量密钥存储——**本包内不携带任何密钥**。

```
lib/reporter.js (client, no secrets)
    |  anonymize -> POST https://camofox-telemetry.askjo.workers.dev/report
    v
Cloudflare Worker (holds GitHub App key)
    |  validate -> rate-limit -> dedup -> create GitHub Issue
    v
GitHub Issue created
```

端点源代码位于本仓库 [`workers/crash-reporter/index.ts`](workers/crash-reporter/index.ts)。

#### Verification

你不必盲目信任——可自行验证当前运行代码：

```bash
# 1. 询问端点正在运行的代码
curl https://camofox-telemetry.askjo.workers.dev/source
# -> { "commit": "abc1234", "sha256": "e3b0c44...", "source": "https://github.com/..." }

# 2. 将 sha256 与本仓库源码进行比对
sha256sum workers/crash-reporter/index.ts

# 3. 检查 commit 是否与 CI 部署版本一致
#    https://github.com/jo-inc/camofox-browser/actions/workflows/telemetry-deploy.yml
git log --oneline workers/crash-reporter/index.ts | head -1
```

若哈希值不匹配，说明端点运行了与仓库不同的代码。部署工作流 ([`.github/workflows/telemetry-deploy.yml`](.github/workflows/telemetry-deploy.yml)) 会在部署时注入 commit 和源码哈希——每次部署均可在 [GitHub Actions](https://github.com/jo-inc/camofox-browser/actions/workflows/telemetry-deploy.yml) 中审计。

或直接跳过验证：设置 `CAMOFOX_CRASH_REPORT_ENABLED=false` 可禁用所有遥测，或通过 `CAMOFOX_CRASH_REPORT_URL` 指向[你自己的端点](#self-hosted-telemetry-endpoint)。

#### Privacy

所有上报数据在离开进程前均会经过严格匿名化处理（[`lib/reporter.js` L28-290](lib/reporter.js#L28-L290)）：
- **URLs** —— 知名公共域名（Google、Amazon、Reddit、Cloudflare 等）将原样显示以便定位问题网站。私有/未知域名将被替换为稳定的 HMAC 哈希值（`site-a1b2c3d4`）——跨报告保持一致性以供关联，但不可逆推回原始域名。路径段变为 `*/*/*`（仅保留深度）。查询参数变为 `?[3]`（仅保留数量）。绝不包含任何键、值或路径内容。
- **文件路径** -> 剥离至仅文件名 (`<path>/server.js`)
- **Tokens, secrets, API keys** -> `<token>`
- **IPs, emails, env vars** -> 已脱敏
- **Docker/Fly machine IDs** -> `<id>`
- **标签页健康指标** —— 纯计数（崩溃次数、错误数、状态码分布）。不包含页面内容、URL 或用户数据。

重复 Issue 将通过堆栈签名检测，并添加 `+1` 评论而非创建新 Issue。

```bash
# Disable telemetry
export CAMOFOX_CRASH_REPORT_ENABLED=false

# Point to your own endpoint (see below)
export CAMOFOX_CRASH_REPORT_URL=https://your-endpoint.example.com/report

# Adjust rate limit (default: 10 per hour)
export CAMOFOX_CRASH_REPORT_RATE_LIMIT=5
```

#### Self-hosted telemetry endpoint

若要在你自己的 GitHub 仓库中上报遥测数据（而非 `jo-inc/camofox-browser`）：

1. **创建 GitHub App** —— [Settings -> Developer settings -> GitHub Apps -> New](https://github.com/settings/apps/new)
   - Permissions: **Repository -> Issues -> Read & Write**
   - Uncheck **Webhook -> Active** (not needed)
   - Click **Generate a key** -- 下载 `.pem` 文件
   - Install the app on your target repo (Install App -> select repo)
   - Note your **App ID** (number on the app's General page) and **Installation ID** (from the URL after installing: `github.com/settings/installations/{id}`)

2. **部署端点** —— 克隆本仓库并部署 Worker：
   ```bash
   cd workers/crash-reporter
   # Edit wrangler.toml: set account_id to your Cloudflare account ID
   npx wrangler deploy
   ```
   该 Worker 是单个 TypeScript 文件，零 npm 依赖。它同样可在 Deno、Bun 或任何支持 Web Crypto API 的运行时中运行。

3. **设置 Worker Secrets：**
   ```bash
   cd workers/crash-reporter
   echo "YOUR_APP_ID" | npx wrangler secret put GH_APP_ID
   echo "YOUR_INSTALL_ID" | npx wrangler secret put GH_INSTALL_ID
   # Key must be PKCS#8 DER base64 (not raw PEM)
   openssl pkcs8 -topk8 -inform PEM -outform DER -nocrypt -in your-app.pem | \
     base64 | tr -d '\n' | npx wrangler secret put GH_PRIVATE_KEY
   # File issues in your repo
   echo "your-org/your-repo" | npx wrangler secret put GH_REPO
   ```

4. **将 camofox-browser 指向你的端点：**
   ```bash
   export CAMOFOX_CRASH_REPORT_URL=https://your-worker.your-subdomain.workers.dev/report
   ```

5. **验证：**
   ```bash
   curl https://your-worker.your-subdomain.workers.dev/health
   # -> {"status":"ok"}
   ```

### Structured Logging

所有日志输出均为 JSON 格式（每行一个对象），便于日志聚合工具解析：

```json
{"ts":"2026-02-11T23:45:01.234Z","level":"info","msg":"req","reqId":"a1b2c3d4","method":"POST","path":"/tabs","userId":"agent1"}
{"ts":"2026-02-11T23:45:01.567Z","level":"info","msg":"res","reqId":"a1b2c3d4","status":200,"ms":333}
```

健康检查请求（`/health`）不会记录在请求日志中，以减少噪音。

### Basic Browsing

```bash
# Create a tab
curl -X POST http://localhost:9377/tabs \
  -H 'Content-Type: application/json' \
  -d '{"userId": "agent1", "sessionKey": "task1", "url": "https://example.com"}'

# Get accessibility snapshot with element refs
curl "http://localhost:9377/tabs/TAB_ID/snapshot?userId=agent1"
# -> { "snapshot": "[button e1] Submit  [link e2] Learn more", ... }

# Click by ref
curl -X POST http://localhost:9377/tabs/TAB_ID/click \
  -H 'Content-Type: application/json' \
  -d '{"userId": "agent1", "ref": "e1"}'

# Type into an element
curl -X POST http://localhost:9377/tabs/TAB_ID/type \
  -H 'Content-Type: application/json' \
  -d '{"userId": "agent1", "ref": "e2", "text": "hello", "pressEnter": true}'

# Navigate with a search macro
curl -X POST http://localhost:9377/tabs/TAB_ID/navigate \
  -H 'Content-Type: application/json' \
  -d '{"userId": "agent1", "macro": "@google_search", "query": "best coffee beans"}'
```

## API

### Tab Lifecycle

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/tabs` | Create tab with initial URL |
| `GET` | `/tabs?userId=X` | List open tabs |
| `GET` | `/tabs/:id/stats` | Tab stats (tool calls, visited URLs) |
| `DELETE` | `/tabs/:id` | Close tab |
| `DELETE` | `/tabs/group/:groupId` | Close all tabs in a group |
| `DELETE` | `/sessions/:userId` | Close all tabs for a user |

### Page Interaction

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/tabs/:id/snapshot` | Accessibility snapshot with element refs. Query params: `includeScreenshot=true` (add base64 PNG), `offset=N` (paginate large snapshots) |
| `POST` | `/tabs/:id/click` | Click element by ref or CSS selector |
| `POST` | `/tabs/:id/type` | Type text into element |
| `POST` | `/tabs/:id/press` | Press a keyboard key |
| `POST` | `/tabs/:id/scroll` | Scroll page (up/down/left/right) |
| `POST` | `/tabs/:id/navigate` | Navigate to URL or search macro |
| `POST` | `/tabs/:id/wait` | Wait for selector or timeout |
| `GET` | `/tabs/:id/links` | Extract all links on page |
| `GET` | `/tabs/:id/images` | List `<img>` elements. Query params: `includeData=true` (return inline data URLs), `maxBytes=N`, `limit=N` |
| `GET` | `/tabs/:id/downloads` | List captured downloads. Query params: `includeData=true` (base64 file data), `consume=true` (clear after read), `maxBytes=N` |
| `GET` | `/tabs/:id/screenshot` | Take screenshot |
| `POST` | `/tabs/:id/back` | Go back |
| `POST` | `/tabs/:id/forward` | Go forward |
| `POST` | `/tabs/:id/refresh` | Refresh page |

### YouTube Transcript

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/youtube/transcript` | Extract captions from a YouTube video |

```bash
curl -X POST http://localhost:9377/youtube/transcript \
  -H 'Content-Type: application/json' \
  -d '{"url": "https://www.youtube.com/watch?v=dQw4w9WgXcQ", "languages": ["en"]}'
# -> { "status": "ok", "transcript": "[00:18] [music] We're no strangers to love [music]\n...", "video_title": "...", "total_words": 548 }
```

Uses [yt-dlp](https://github.com/yt-dlp/yt-dlp) when available (fast, no browser needed). Falls back to a browser-based intercept method if yt-dlp is not installed -- this is slower and less reliable due to YouTube ad pre-rolls.

### Server

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/health` | Health check |
| `POST` | `/start` | Start browser engine |
| `POST` | `/stop` | Stop browser engine |

### Sessions

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/sessions/:userId/cookies` | Add cookies to a user session (Playwright cookie objects) |
| `GET` | `/sessions/:userId/storage_state` | Export cookies + localStorage ([VNC plugin](plugins/vnc/)) |

## Search Macros

`@google_search`  |  `@youtube_search`  |  `@amazon_search`  |  `@reddit_search`  |  `@reddit_subreddit`  |  `@wikipedia_search`  |  `@twitter_search`  |  `@yelp_search`  |  `@spotify_search`  |  `@netflix_search`  |  `@linkedin_search`  |  `@instagram_search`  |  `@tiktok_search`  |  `@twitch_search`

Reddit macros return JSON directly (no HTML parsing needed):
- `@reddit_search` - search all of Reddit, returns JSON with 25 results
- `@reddit_subreddit` - browse a subreddit (e.g., query `"programming"` -> `/r/programming.json`)

## Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `CAMOFOX_PORT` | Server port | `9377` |
| `PORT` | Server port (fallback, for platforms like Fly.io, Railway) | `9377` |
| `CAMOFOX_API_KEY` | Enable cookie import endpoint (disabled if unset) | - |
| `CAMOFOX_ADMIN_KEY` | Required for `POST /stop` | - |
| `CAMOFOX_ACCESS_KEY` | If set, all routes (except `/health`, cookie import, and `/stop`) require `Authorization: Bearer <key>`. Lets you safely expose the server beyond loopback. | - |
| `CAMOUFOX_EXECUTABLE` | External Camoufox executable to use instead of downloading/launching the bundled cache. Must point to a Camoufox bundle with sibling resources. | - |
| `CAMOUFOX_EXECUTABLE_PATH` | Compatibility alias for `CAMOUFOX_EXECUTABLE` | - |
| `CAMOFOX_EXECUTABLE_PATH` | Compatibility alias for `CAMOUFOX_EXECUTABLE` | - |
| `CAMOFOX_COOKIES_DIR` | Directory for cookie files | `~/.camofox/cookies` |
| `CAMOFOX_PROFILE_DIR` | Directory for persisted session profiles | `~/.camofox/profiles` |
| `CAMOFOX_TRACES_DIR` | Directory for session trace zips | `~/.camofox/traces` |
| `CAMOFOX_TRACES_MAX_BYTES` | Max size per trace, removed on next startup if exceeded | `52428800` (50MB) |
| `CAMOFOX_TRACES_TTL_HOURS` | Traces older than this are swept on startup | `24` |
| `MAX_SESSIONS` | Max concurrent browser sessions | `50` |
| `MAX_TABS_PER_SESSION` | Max tabs per session | `10` |
| `SESSION_TIMEOUT_MS` | Session inactivity timeout | `1800000` (30min) |
| `BROWSER_IDLE_TIMEOUT_MS` | Kill browser when idle (0 = never) | `300000` (5min) |
| `HANDLER_TIMEOUT_MS` | Max time for any handler | `30000` (30s) |
| `MAX_CONCURRENT_PER_USER` | Concurrent request cap per user | `3` |
| `MAX_OLD_SPACE_SIZE` | Node.js V8 heap limit (MB) | `128` |
| `PROXY_STRATEGY` | Proxy mode: `backconnect` (rotating sticky sessions) or blank (single endpoint) | - |
| `PROXY_PROVIDER` | Provider name for session format (e.g. `decodo`) | `decodo` |
| `PROXY_HOST` | Proxy hostname or IP (simple mode) | - |
| `PROXY_PORT` | Proxy port (simple mode) | - |
| `PROXY_USERNAME` | Proxy auth username | - |
| `PROXY_PASSWORD` | Proxy auth password | - |
| `PROXY_BACKCONNECT_HOST` | Backconnect gateway hostname | - |
| `PROXY_BACKCONNECT_PORT` | Backconnect gateway port | `7000` |
| `PROXY_COUNTRY` | Target country for proxy geo-targeting | - |
| `PROXY_STATE` | Target state/region for proxy geo-targeting | - |
| `TAB_INACTIVITY_MS` | Close tabs idle longer than this | `300000` (5min) |
| `CAMOFOX_CRASH_REPORT_ENABLED` | Enable anonymized crash/hang telemetry (`false` to disable) | `true` |
| `CAMOFOX_CRASH_REPORT_URL` | Telemetry endpoint ([self-hosted endpoint](#self-hosted-telemetry-endpoint)) | `https://camofox-telemetry.askjo.workers.dev/report` |
| `CAMOFOX_CRASH_REPORT_REPO` | GitHub repo for telemetry issues | `jo-inc/camofox-browser` |
| `CAMOFOX_CRASH_REPORT_RATE_LIMIT` | Max telemetry reports per hour | `10` |
| `ENABLE_VNC` | Enable VNC plugin for interactive browser access (`1`) | - |
| `VNC_PASSWORD` | Password for VNC access (recommended in production) | - |
| `NOVNC_PORT` | noVNC web UI port | `6080` |

## Architecture

```
Browser Instance (Camoufox)
\-- User Session (BrowserContext) - isolated cookies/storage
    |-- Tab Group (sessionKey: "conv1")
    |   |-- Tab (google.com)
    |   \-- Tab (github.com)
    \-- Tab Group (sessionKey: "conv2")
        \-- Tab (amazon.com)
```

会话在闲置 30 分钟后自动过期。浏览器引擎本身在无活跃会话 5 分钟后关闭，并在下次请求时重新启动。

当会话达到标签页上限时，系统会自动回收最旧或最少使用的标签页，而非返回错误——确保长期运行的 Agent 会话不会遇到死胡同。

## Security Model

本节面向用户及自动化安全审查人员，详细说明 camofox-browser 的安全边界。

### Code isolation

所有 `process.env` 读取均集中管理于 `lib/config.js`。所有 `child_process` 调用位于 `lib/launcher.js`（服务端子进程）和 `plugins/youtube/youtube.js`（yt-dlp）。主文件 `server.js` 包含路由处理器，但零 `process.env` 读取及零 `child_process` 引用。没有任何单个文件同时混合了环境凭证访问与网络发送功能。

### No embedded secrets

本包不携带任何凭据、私钥、API Token 或签名密钥。所有密钥均通过环境变量（`CAMOFOX_API_KEY`, `CAMOFOX_ACCESS_KEY`）在运行时提供，或由 Cloudflare Worker 环境变量管理（遥测端点的 GitHub App 密钥）。

### Cookie import is disabled by default

Cookie 导入端点（`POST /sessions/:userId/cookies`）受 `CAMOFOX_API_KEY` 保护。若未设置该环境变量，服务端将拒绝所有 Cookie 请求并返回 HTTP 403。Cookie 文件从沙箱目录（`~/.camofox/cookies/`）读取，并具备路径遍历防护——尝试越权访问将被拦截。单次请求最多导入 500 个 Cookie，文件体积限制为 5MB。

### Access control

`CAMOFOX_ACCESS_KEY` 提供全局 Bearer Token 认证（覆盖所有路由，除 `/health`）。设置后，每个请求必须包含 `Authorization: Bearer <key>`。推荐用于任何非本地部署场景。

### Binary download

Camoufox 浏览器引擎（约 300MB）在 `npm install` 阶段由 [`camoufox-js`](https://www.npmjs.com/package/camoufox-js) 下载，该 npm 包由 [Camoufox 项目](https://camoufox.com) 维护。它从[官方 GitHub Releases](https://github.com/nicedayzhu/camoufox/releases) 拉取文件，完整性校验由 `camoufox-js` 处理。无自定义下载 URL、无短链接、无裸 IP 直连。

### Telemetry

匿名化的崩溃/挂起遥测数据发送至 Cloudflare Worker 端点。端点源码[位于本仓库](workers/crash-reporter/index.ts)且可审计。验证方式：向端点发送 `GET /source` 将返回已部署的 commit hash 和 sha256，便于与仓库比对。上报器（[`lib/reporter.js` L28-290](lib/reporter.js#L28-L290)）执行严格匿名化：私有域名经 HMAC 哈希处理（不可逆），路径被剥离，Token/IP/邮箱已脱敏。绝不发送页面内容、Cookie 或用户数据。可通过 `CAMOFOX_CRASH_REPORT_ENABLED=false` 关闭，或使用 `CAMOFOX_CRASH_REPORT_URL` 指向你自己的端点。

### Session persistence

持久化插件将 Cookie 和 localStorage 保存至 `~/.camofox/profiles/<hashed-userId>/`，确保已登录会话随浏览器重启而保留。UserIds 经哈希处理用于目录命名。可通过在 `camofox.config.json` 中移除 plugins 数组里的 `persistence` 来禁用。

### Network access

出站连接仅指向：(1) Agent 导航的 URL（核心功能），(2) 遥测端点（已匿名化，支持关闭）。入站连接：localhost:9377 上的 REST API（默认），可选通过 `CAMOFOX_ACCESS_KEY` 保护。

### Subprocess usage

可能生成两个子进程：(1) Camoufox 浏览器引擎（核心功能，`lib/launcher.js`），(2) yt-dlp 用于 YouTube 字幕提取（可选，`plugins/youtube/youtube.js`）。两者均隔离在独立文件中，与路由处理器分离。

## Testing

```bash
npm test              # all tests
npm run test:e2e      # e2e tests only
npm run test:live     # live site tests (Google, macros)
npm run test:debug    # with server output
```

## npm

```bash
npm install @askjo/camofox-browser
```

## Credits

- [Camoufox](https://camoufox.com) - Firefox-based browser with C++ anti-detection
- [Donate to Camoufox's original creator daijro](https://camoufox.com/about/)
- [OpenClaw](https://openclaw.ai) - Open-source AI agent framework

## Crypto Scam Warning

随着本项目受到关注，一些可疑人员开始利用名为 “Camofox” 的加密货币代币进行欺诈活动。**Camofox 并非加密项目，也永远不会是。** 任何使用 Camoufox/Camofox 名称的代币、币种或 NFT 均与我们无关。

## License

MIT
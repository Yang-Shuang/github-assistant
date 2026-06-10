# Open Agents

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?project-name=open-agents&repository-name=open-agents&repository-url=https%3A%2F%2Fgithub.com%2Fvercel-labs%2Fopen-agents&demo-title=Open+Agents&demo-description=Open-source+reference+app+for+building+and+running+background+coding+agents+on+Vercel.&demo-url=https%3A%2F%2Fopen-agents.dev%2F&env=POSTGRES_URL%2CBETTER_AUTH_SECRET%2CNEXT_PUBLIC_VERCEL_APP_CLIENT_ID%2CVERCEL_APP_CLIENT_SECRET%2CNEXT_PUBLIC_GITHUB_CLIENT_ID%2CGITHUB_CLIENT_SECRET%2CGITHUB_APP_ID%2CGITHUB_APP_PRIVATE_KEY%2CNEXT_PUBLIC_GITHUB_APP_SLUG%2CGITHUB_WEBHOOK_SECRET&envDescription=Neon+can+provide+POSTGRES_URL+automatically.+Generate+BETTER_AUTH_SECRET+yourself%2C+then+add+your+Vercel+OAuth+and+GitHub+App+credentials+for+a+full+deployment.&products=%255B%257B%2522type%2522%253A%2522integration%2522%252C%2522protocol%2522%253A%2522storage%2522%252C%2522productSlug%2522%253A%2522neon%2522%252C%2522integrationSlug%2522%253A%2522neon%2522%257D%252C%257B%2522type%2522%253A%2522integration%2522%252C%2522protocol%2522%253A%2522storage%2522%252C%2522productSlug%2522%253A%2522upstash-kv%2522%252C%2522integrationSlug%2522%253A%2522upstash%2522%257D%255D&skippable-integrations=1)

Open Agents 是一个开源参考应用，用于在 Vercel 上构建和运行后台编码智能体。它包含 Web 界面、智能体运行时（agent runtime）、沙箱编排以及 GitHub 集成，让你无需连接本地电脑即可从提示词直接生成代码变更。

该仓库旨在供你 Fork 并进行二次开发/适配，而非作为黑盒直接使用。

## 核心架构

Open Agents 采用三层系统架构：

```text
Web -> Agent workflow -> Sandbox VM
```

- Web 应用负责处理身份验证、会话管理、聊天及流式界面。
- 智能体在 Vercel 上以持久化工作流的形式运行。
- 沙箱提供执行环境：包括文件系统、Shell、Git、开发服务器及预览端口。

### 核心架构决策：智能体与沙箱分离

智能体并不运行在虚拟机（VM）内部。它在沙箱外部运行，并通过文件读取、编辑、搜索和 Shell 命令等工具与沙箱进行交互。

这种分离是该项目的核心设计目标：

- 智能体执行不绑定于单次请求的生命周期
- 沙箱生命周期可独立休眠与恢复
- 模型/服务商的选择与沙箱实现可独立演进
- 虚拟机仅保持为纯粹的执行环境，而非控制平面

## 当前功能

- 基于聊天的编码智能体，支持文件、搜索、Shell、任务、技能及网页浏览工具
- 基于 Workflow SDK 的持久化多步执行，支持流式输出与中断取消
- 隔离的 Vercel 沙箱，支持基于快照的恢复
- 在沙箱内完成代码库克隆及分支操作
- 可选功能：运行成功后自动提交（commit）、推送（push）并创建 Pull Request (PR)
- 通过只读链接分享会话
- 可选语音输入，集成 ElevenLabs 转录服务

## 运行时说明

以下细节对于理解当前实现至关重要：

- 聊天请求会启动工作流运行，而非内联执行智能体。
- 每次智能体交互可跨越多个持久化的工作流步骤继续执行。
- 活跃的运行任务可通过重新连接到现有工作流的流来恢复。
- 沙箱暴露端口 `3000`、`5173`、`4321` 和 `8000`，可选择使用配置的基础快照，并在闲置后自动休眠。
- 支持自动提交与自动创建 PR，但属于偏好设置功能，默认并非始终开启。

## 环境变量

完整列表请参阅 `apps/web/.env.example`。摘要如下：

### 基础运行时

```env
POSTGRES_URL=
BETTER_AUTH_SECRET=
```

### 登录必需（Vercel OAuth）

```env
NEXT_PUBLIC_VERCEL_APP_CLIENT_ID=
VERCEL_APP_CLIENT_SECRET=
```

### 访问 GitHub 仓库、推送及创建 PR 必需

```env
NEXT_PUBLIC_GITHUB_CLIENT_ID=
GITHUB_CLIENT_SECRET=
GITHUB_APP_ID=
GITHUB_APP_PRIVATE_KEY=
NEXT_PUBLIC_GITHUB_APP_SLUG=
GITHUB_WEBHOOK_SECRET=
```

### 可选配置

```env
REDIS_URL=
KV_URL=
OPEN_AGENTS_RESOURCE_PROFILE=
VERCEL_PROJECT_PRODUCTION_URL=
NEXT_PUBLIC_VERCEL_PROJECT_PRODUCTION_URL=
VERCEL_SANDBOX_BASE_SNAPSHOT_ID=
ELEVENLABS_API_KEY=
```

- `REDIS_URL` / `KV_URL`：技能元数据缓存（未配置时回退至内存缓存）。
- `OPEN_AGENTS_RESOURCE_PROFILE`：可选的部署资源规格。设置为 `hobby` 可使用兼容 Hobby 套餐的聊天与沙箱资源默认值；留空则使用标准行为。
- `VERCEL_PROJECT_PRODUCTION_URL` / `NEXT_PUBLIC_VERCEL_PROJECT_PRODUCTION_URL`：用于元数据及部分回调行为的正式生产环境域名。
- `VERCEL_SANDBOX_BASE_SNAPSHOT_ID`：新沙箱的基础快照（可选）。若未设置，沙箱将从 Vercel 标准运行时启动。请使用在你自己的 Vercel 作用域内创建或可访问的快照。
- `ELEVENLABS_API_KEY`：语音转录服务密钥。

## 在 Vercel 部署你自己的副本

1. Fork（派生）该仓库。
2. 将仓库导入 Vercel。若使用上方的部署按钮，Neon Postgres 数据库将自动配置。
3. 生成用于会话签名的密钥：

   ```bash
   openssl rand -base64 32   # BETTER_AUTH_SECRET
   ```

4. 在 Vercel 项目设置中添加环境变量：

   ```env
   POSTGRES_URL=
   BETTER_AUTH_SECRET=
   ```

5. 首次部署以获取稳定的生产环境域名。
6. 创建 Vercel OAuth 应用，回调地址设为：

   ```text
   https://YOUR_DOMAIN/api/auth/callback/vercel
   ```

7. 添加这些环境变量并重新部署：

   ```env
   NEXT_PUBLIC_VERCEL_APP_CLIENT_ID=
   VERCEL_APP_CLIENT_SECRET=
   ```

8. 如需完整支持 GitHub 的编码智能体流程，请创建 GitHub App：
   - 首页 URL：`https://YOUR_DOMAIN`
   - 回调地址：`https://YOUR_DOMAIN/api/auth/callback/github`
   - 设置页面：`https://YOUR_DOMAIN/api/github/app/callback`

   在 GitHub App 设置中：
   - 使用应用的 Client ID 和 Client Secret 分别配置 `NEXT_PUBLIC_GITHUB_CLIENT_ID` 与 `GITHUB_CLIENT_SECRET`
   - 若需完美支持组织安装，请将应用设为公开

9. 添加 GitHub App 相关环境变量并重新部署。
10. （可选）添加 Redis/KV、设置 `OPEN_AGENTS_RESOURCE_PROFILE=hobby` 以启用 Hobby 兼容的资源默认值、配置正式生产域名变量，以及自定义 `VERCEL_SANDBOX_BASE_SNAPSHOT_ID`（若希望新沙箱从预配置镜像启动）。

## 本地环境搭建

1. 安装依赖：

   ```bash
   bun install
   ```

2. 创建本地环境变量文件：

   ```bash
   cp apps/web/.env.example apps/web/.env
   ```

3. 在 `apps/web/.env` 中填写所需值。
4. 启动应用：

   ```bash
   bun run web
   ```

若已关联 Vercel 项目，可通过 `vc env pull` 将环境变量拉取至本地。

## OAuth 与集成配置

### Vercel OAuth

身份验证由 [Better Auth](https://www.better-auth.com/) 处理，支持 Vercel 和 GitHub 作为第三方登录提供商。所有认证路由均通过 `/api/auth/[...all]` 捕获所有路由统一提供。

创建 Vercel OAuth 应用并使用以下回调地址：

```text
https://YOUR_DOMAIN/api/auth/callback/vercel
```

本地开发时使用：

```text
http://localhost:3000/api/auth/callback/vercel
```

随后设置：

```env
NEXT_PUBLIC_VERCEL_APP_CLIENT_ID=...
VERCEL_APP_CLIENT_SECRET=...
```

### GitHub App

你无需单独创建 GitHub OAuth 应用。Open Agents 直接使用 GitHub App 的 OAuth 凭据作为 Better Auth 的第三方登录提供商，并利用其安装令牌访问代码库。

为基于安装的仓库访问权限创建 GitHub App 并配置：

- 首页 URL：`https://YOUR_DOMAIN`
- 回调地址：`https://YOUR_DOMAIN/api/auth/callback/github`
- 设置页面：`https://YOUR_DOMAIN/api/github/app/callback`
- 若需完美支持组织安装，请将应用设为公开

本地开发时，首页 URL 使用 `http://localhost:3000`，回调地址使用 `http://localhost:3000/api/auth/callback/github`，设置页面使用 `http://localhost:3000/api/github/app/callback`。

随后设置：

```env
NEXT_PUBLIC_GITHUB_CLIENT_ID=...   # GitHub App Client ID
GITHUB_CLIENT_SECRET=...           # GitHub App Client Secret
GITHUB_APP_ID=...
GITHUB_APP_PRIVATE_KEY=...
NEXT_PUBLIC_GITHUB_APP_SLUG=...
GITHUB_WEBHOOK_SECRET=...
```

`GITHUB_APP_PRIVATE_KEY` 可存储为转义换行的 PEM 内容，或 Base64 编码的 PEM 字符串。

## 常用命令

```bash
bun run web                # run dev server
bun run check              # lint + format check
bun run fix                # lint + format fix
bun run typecheck          # typecheck all packages
bun run ci                 # full CI: check, typecheck, tests, migration check
bun run sandbox:snapshot-base  # refresh sandbox base snapshot
```

## 仓库结构

```text
apps/web         Next.js app, workflows, auth, chat UI
packages/agent   agent implementation, tools, subagents, skills
packages/sandbox sandbox abstraction and Vercel sandbox integration
packages/shared  shared utilities
```
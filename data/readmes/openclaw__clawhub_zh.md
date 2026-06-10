<p align="center">
  <img src="public/clawd-logo.png" alt="ClawHub" width="120">
</p>

![ClawHub banner](docs/assets/readme-banner.jpg)

<h1 align="center">ClawHub</h1>

<p align="center">
  <a href="https://github.com/openclaw/clawhub/actions/workflows/ci.yml?branch=main"><img src="https://img.shields.io/github/actions/workflow/status/openclaw/clawhub/ci.yml?branch=main&style=for-the-badge" alt="CI status"></a>
  <a href="https://discord.gg/clawd"><img src="https://img.shields.io/discord/1456350064065904867?label=Discord&logo=discord&logoColor=white&color=5865F2&style=for-the-badge" alt="Discord"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge" alt="MIT License"></a>
</p>

ClawHub 是 **OpenClaw 的公开技能注册中心**：用于发布、版本管理和搜索基于文本的智能体技能（包含 `SKILL.md` 及支持文件）。
它专为快速浏览和 CLI 友好的 API 而设计，并集成了内容审核钩子与向量搜索功能。
此外，它还原生暴露了 **OpenClaw 软件包目录**，用于管理代码插件和捆绑插件。

<p align="center">
  <a href="https://clawhub.ai">ClawHub</a> ·
  <a href="VISION.md">Vision</a> ·
  <a href="docs/clawhub.md">Docs</a> ·
  <a href="CONTRIBUTING.md">Contributing</a> ·
  <a href="https://discord.gg/clawd">Discord</a>
</p>

## 你可以用它做什么

- 浏览技能并渲染其 `SKILL.md`。
- 发布带有更新日志和标签（包括 `latest`）的新技能版本。
- 重命名已拥有的技能，且不会破坏旧链接或安装记录。
- 将重复的自有技能合并为一个标准 slug。
- 浏览灵魂（Souls）并渲染其 `SOUL.md`。
- 发布带有更新日志和标签的新灵魂版本。
- 通过嵌入向量索引进行搜索，替代脆弱的关键词匹配。
- 收藏与评论；管理员/审核员可策展并审批技能。
- 锁定本地技能安装，防止更新或强制重新安装覆盖已锁定的副本。
- 浏览带有家族/信任度/能力元数据的 OpenClaw 软件包。
- 通过 `/packages` API 和 CLI 流程发布原生代码插件与捆绑插件。

## 工作原理（高层概述）

- Web 应用：TanStack Start（基于 React、Vite/Nitro）。
- 后端：Convex（数据库 + 文件存储 + HTTP 操作）+ Convex Auth（GitHub OAuth 认证）。
- 搜索功能：OpenAI 嵌入模型（`text-embedding-3-small`）+ Convex 向量搜索。
- API 模式与路由：`packages/schema`（`clawhub-schema`）。

## CLI 命令行工具

常用 CLI 操作流程：

- 认证：`clawhub login`, `clawhub whoami`
- 远程/无头模式认证：`clawhub login --device`
- 发现与浏览：`clawhub search ...`, `clawhub explore`
- 浏览统一目录（技能 + 插件）：`clawhub package explore`, `clawhub package inspect <name>`
- 管理本地安装：`clawhub install <slug>`, `clawhub pin <slug>`, `clawhub unpin <slug>`, `clawhub uninstall <slug>`, `clawhub list`, `clawhub update --all`
- 仅查看不安装：`clawhub inspect <slug>`
- 发布/同步技能：`clawhub skill publish <path>`, `clawhub sync`
- 发布插件：`clawhub package publish <source>`
- 代码插件清单必须包含 `openclaw.compat.pluginApi` 和 `openclaw.build.openclawVersion`；最小示例见 [`docs/cli.md`](docs/cli.md)。
- 规范化自有技能：`clawhub skill rename <slug> <new-slug>`, `clawhub skill merge <source> <target>`

文档：[`docs/quickstart.md`](docs/quickstart.md), [`docs/cli.md`](docs/cli.md)。

### 清理与删除权限

- `clawhub uninstall <slug>` 仅移除你本机上的本地安装。
- 已上传至注册表的技能采用软删除/恢复机制（`clawhub delete <slug>` / `clawhub undelete <slug>` 或对应的 API）。
- 仅技能或软件包所有者、发布者所有者/管理员、审核员和管理员可执行软删除与恢复操作。
- 软件包使用 `clawhub package delete <name>` / `clawhub package undelete <name>`。
- 硬删除仅限管理员操作（通过管理工具或封禁流程执行）。
- 所有者重命名会将旧 slug 保留为跳转别名。
- 所有者合并会隐藏源技能列表，并将旧 slug 重定向至标准目标。

## 遥测数据收集

当你以登录状态运行 `clawhub sync` 时，ClawHub 会收集极少量的**安装遥测数据**（用于统计安装量）。
可通过以下方式禁用：

```bash
export CLAWHUB_DISABLE_TELEMETRY=1
```

详细说明见 [`docs/telemetry.md`](docs/telemetry.md)。

## 项目目录结构

- `src/` —— TanStack Start 应用（路由、组件、样式）。
- `convex/` —— 模式定义 + 查询/变更/操作逻辑 + HTTP API 路由。
- `packages/schema/` —— CLI 与 Web 应用共享的 API 类型与路由。
- [`docs/`](docs/README.md) —— 面向用户、发布者、API 客户端及部署运维人员的可发布公开文档。
- [`specs/`](specs/README.md) —— 产品规格、计划、回归测试说明与设计历史。
- [`specs/spec.md`](specs/spec.md) —— 产品与实现规格（维护者推荐阅读）。

## 本地开发环境

前置依赖：[Bun](https://bun.sh/)（Convex 通过 `bunx` 运行，无需全局安装）。分离式工作树路径还需安装 [Worktrunk](https://github.com/max-sixty/worktrunk)（即 `wt`）。

```bash
bun install
cp .env.local.example .env.local
# edit .env.local — see CONTRIBUTING.md for local Convex values

# terminal A: local Convex backend
bunx convex dev

# terminal B: web app (port 3000)
bun run dev

# detached/Codex worktree preview
bun run setup:worktree
bun run dev:worktree
wt --yes url

# seed local QA fixtures and the public corpus
bun run seed:dev
```

`bun run seed:dev` 会等待本地 Convex 服务启动，运行开发环境测试数据填充脚本，并刷新全局统计信息。这些测试数据由 `@local` 账户拥有，在修改测试数据或模式后安全地重新运行是安全的。如需重置/手动命令及完整设置指南（环境变量、GitHub OAuth、JWT 密钥、数据库初始化），请参阅 [CONTRIBUTING.md](CONTRIBUTING.md)。

## 环境变量

- `VITE_CONVEX_URL`: Convex 部署地址（`https://<deployment>.convex.cloud`）。
- `VITE_CONVEX_SITE_URL`: Convex 站点地址（`https://<deployment>.convex.site`）。
- `VITE_SOULHUB_SITE_URL`: SoulHub 站点地址。
- `VITE_SOULHUB_HOST`: SoulHub 主机匹配规则。
- `VITE_SITE_MODE`: SSR 构建的可选覆盖参数（`skills` 或 `souls`）。
- `CONVEX_SITE_URL`: 同 `VITE_CONVEX_SITE_URL`（用于认证与 Cookie）。
- `SITE_URL`: 应用访问地址（本地环境为 `http://localhost:3000`）。
- `AUTH_GITHUB_ID` / `AUTH_GITHUB_SECRET`: GitHub OAuth 应用凭证。
- `JWT_PRIVATE_KEY` / `JWKS`: Convex 认证密钥。
- `OPENAI_API_KEY`: 用于搜索与索引的 OpenAI API 密钥。

## Nix 插件（nixmode 技能）

ClawHub 允许在 `SKILL.md` 的 Frontmatter 中声明 nix-clawdbot 插件路径，以便注册表识别应安装哪个 Nix 软件包捆绑。Nix 插件不同于常规技能包：它将技能包、CLI 二进制文件及其配置标志/依赖项打包在一起。

添加到 `SKILL.md`：

```yaml
---
name: peekaboo
description: Capture and automate macOS UI with the Peekaboo CLI.
metadata:
  {
    "clawdbot":
      {
        "nix":
          {
            "plugin": "github:clawdbot/nix-steipete-tools?dir=tools/peekaboo",
            "systems": ["aarch64-darwin"],
          },
      },
  }
---
```

通过 nix-clawdbot 安装：

```nix
programs.clawdbot.plugins = [
  { source = "github:clawdbot/nix-steipete-tools?dir=tools/peekaboo"; }
];
```

你还可声明配置要求及示例片段：

```yaml
---
name: padel
description: Check padel court availability and manage bookings via Playtomic.
metadata:
  {
    "clawdbot":
      {
        "config":
          {
            "requiredEnv": ["PADEL_AUTH_FILE"],
            "stateDirs": [".config/padel"],
            "example": "config = { env = { PADEL_AUTH_FILE = \\\"/run/agenix/padel-auth\\\"; }; };",
          },
      },
  }
---
```

为显示 CLI 帮助信息（推荐用于 Nix 插件），请包含 `cli --help` 输出：

```yaml
---
name: padel
description: Check padel court availability and manage bookings via Playtomic.
metadata: { "clawdbot": { "cliHelp": "padel --help\\nUsage: padel [command]\\n" } }
---
```

推荐使用 `metadata.clawdbot`，但也接受 `metadata.clawdis` 和 `metadata.openclaw` 作为别名。

## 技能元数据

技能通过 `SKILL.md` 的 Frontmatter 声明其运行时依赖（环境变量、二进制文件、安装规范）。ClawHub 的安全分析模块会将这些声明与实际行为进行比对；中等风险审查结果将保持可见，而“可疑”过滤器仅保留给高风险或恶意行为。

完整参考文档：[`docs/skill-format.md`](docs/skill-format.md#frontmatter-metadata)

快速示例：

```yaml
---
name: my-skill
description: Does a thing with an API.
metadata:
  openclaw:
    requires:
      env:
        - MY_API_KEY
      bins:
        - curl
    primaryEnv: MY_API_KEY
---
```

## 可用脚本

```bash
bun run dev
bun run build
bun run test
bun run coverage
bun run lint
```
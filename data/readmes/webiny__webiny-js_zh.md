<p align="center">
  <img src="./docs/static/webiny-logo.svg" width="350">
</p>

<p align="center">
  面向企业级部署的 AI 可编程内容管理系统（CMS），托管于 AWS
</p>

<p align="center">
    <a href="https://github.com/webiny/webiny-js/actions"><img src="https://img.shields.io/github/actions/workflow/status/webiny/webiny-js/push.yml" alt="Build Status"></a>
    <a href="https://www.npmjs.com/package/@webiny/cli"><img src="https://img.shields.io/npm/dt/@webiny/cli.svg" alt="Total Downloads"></a>
    <a href="https://github.com/webiny/webiny-js/releases"><img src="https://img.shields.io/github/v/release/webiny/webiny-js" alt="Latest Release"></a>
    <a href="https://github.com/webiny/webiny-js/blob/master/LICENSE"><img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License"></a>
</p>

# About Webiny

开源内容平台。基于 AWS Serverless 架构自托管部署。采用 TypeScript 框架构建，你可以通过代码进行扩展，而非通过 UI 配置的黑盒产品。

运行在你自己的 AWS 账户内的 Lambda、DynamoDB、S3 和 CloudFront 之上。自动扩缩容，无需管理服务器。基础设施通过 IaC（基础设施即代码）工具 Pulumi，仅需一条 `deploy` 命令即可完成预配。

已被多个团队投入生产环境使用，管理着数亿条内容记录、PB 级资产以及数千名编辑者——其中包括亚马逊、阿联酋航空、财富 500 强企业、政府机构，以及在自有产品中白标 Webiny 的 SaaS 平台。

[Documentation](https://www.webiny.com/docs) · [Learn Webiny Course](https://www.webiny.com/learn) · [Community Slack](https://www.webiny.com/slack)

---

## What's Inside

![Webiny Headless CMS](<https://www.webiny.com/_next/image?url=https%3A%2F%2Fd3ifp5fffz13jc.cloudfront.net%2Ffiles%2F6970b24992482400025a77b4%2FCMSModel(3).png%3Foriginal&w=3840&q=75>)

**Headless CMS（无头 CMS）** —— 自定义内容模型、GraphQL API、字段级权限、多语言支持、版本控制。模型可通过管理后台 UI 定义，或通过框架在代码中定义。

![Webiny Website Builder](https://www.webiny.com/_next/image?url=https%3A%2F%2Fd3ifp5fffz13jc.cloudfront.net%2Ffiles%2F6971fe95a148300002b2bffb%2FWebsiteBuilder-Featureimage.png%3Foriginal&w=3840&q=75)

**Website Builder（网站构建器）** —— 提供可视化拖拽页面编辑器及 Next.js SDK。通过你自己的前端服务渲染页面（支持 Vercel、CloudFront 等任意部署位置）。使用 React 组件创建自定义页面元素。

![Webiny Website Builder](https://www.webiny.com/_next/image?url=%2Fimages%2Fapp-showcase%2Ffile-manager.png&w=3840&q=75)
**File Manager（文件管理器）** —— 数字资产管理，支持 CDN 分发、文件夹结构、标签分类与搜索。已深度集成至 CMS 和网站构建器中。

**Publishing Workflows（发布工作流）** —— 支持多步骤内容审批，包含草稿状态、审核人分配、定时发布及审计日志追踪。

**Multi-Tenancy（多租户）** —— 从单次部署中实现原生的租户隔离（数据、用户、资产、权限）。单个实例可托管数千个租户。租户通过 GraphQL API 以编程方式创建和管理。支持层级化租户结构（如 Root → Brand → Market，Root → Client → Site 等）。

**Webiny Framework（框架）** —— 基于 TypeScript，提供生命周期钩子、依赖注入、GraphQL Schema 扩展、管理后台 UI 扩展点及基础设施扩展能力。这是核心所在——正是它让 Webiny 成为可编程平台，而不仅仅是可配置产品。

---

## Architecture

```
┌─────────────────────────────────────────────────────┐
│                    Your AWS Account                  │
│                                                      │
│  ┌──────────┐  ┌──────────┐  ┌─────┐  ┌──────────┐ │
│  │  Lambda   │  │ DynamoDB │  │ S3  │  │CloudFront│ │
│  │ (API +   │  │ (Content │  │(Assets)│ │  (CDN)  │ │
│  │  business │  │  storage) │  │     │  │          │ │
│  │  logic)   │  │          │  │     │  │          │ │
│  └──────────┘  └──────────┘  └─────┘  └──────────┘ │
│                                                      │
│  Optional: OpenSearch (full-text search at scale)    │
│  Optional: VPC deployment, multi-AZ, custom config   │
│                                                      │
│  All provisioned automatically via Pulumi IaC         │
└─────────────────────────────────────────────────────┘
```

**Stack（技术栈）：** TypeScript、React、GraphQL、Node.js、Pulumi、AWS Serverless 服务。

**What you control（你完全掌控）：** 一切。IaC 模板均为开源。你可以修改 Lambda 内存、添加 CloudWatch 告警、更改 VPC 配置或添加自定义 AWS 资源——基础设施由你主导。

**What you don't manage（你无需管理）：** 服务器、补丁更新、扩缩容、容量规划。这正是 Serverless（无服务器）架构的意义所在。

---

## Quick Start

**Prerequisites（前置条件）：** Node.js 22+、Yarn，以及具备编程访问权限的 AWS 账户。

```bash
npx create-webiny-project my-project
cd my-project
yarn webiny deploy
```

首次部署需要 5–15 分钟（用于 AWS 资源预配）。完成后你将获得管理后台地址。创建首个管理员账号即可登录使用。

**Local development（本地开发）：**

```bash
yarn webiny watch admin  # React dev server on localhost:3001
yarn webiny watch api    # Local Lambda execution environment
```

**New team member onboarding（新团队成员接入）：**

```bash
git clone <your-repo>
yarn
# Ready to develop
```

---

## AI-Assisted Development

![Webiny - MCP AI Assisted Development](https://image.mux.com/VAFZGdrkqL6HskOokDtEBkDnHUstqzTgkwgps59nEtE/animated.gif?width=640)

Webiny 内置了 **MCP Server（模型上下文协议服务器）** 和 **AI Skills（AI 技能包）**，可为 AI 编程代理（如 Claude Code、Cursor、Kiro 等）提供关于平台架构、扩展点及设计模式的深度上下文信息。

这意味着你可以让 AI 代理帮你完成以下任务：

- Create content models with specific field types and validation
- Build lifecycle hooks that trigger on content events
- Extend the GraphQL API with custom queries and business logic
- Scaffold admin UI extensions with React components
- Wire integrations with external systems via lifecycle events
- Set up multi-tenant configurations programmatically

AI 生成的代码将严格遵循 Webiny 的实际开发规范，因为 MCP Server 为其提供了框架的真实知识体系——而非泛泛的猜测。

**Why this works better on Webiny than most platforms（为何在 Webiny 上效果优于大多数平台）：** 该框架采用强类型设计，并具备明确的扩展点。AI 生成的代码要么符合类型系统规范，否则无法通过编译。不存在让 AI 盲目猜测的模糊插件 API。类型定义强制保证了代码的正确性。

**Getting started with the MCP server（MCP Server 入门指南）：**

```bash
# The MCP server runs locally inside your Webiny project
# Connect it to your AI coding tool of choice
# See docs for tool-specific setup instructions
```

→ [AI-Assisted Development Guide](https://www.webiny.com/docs/build-with-ai/ai-assisted-development)

---

## Extending Webiny

所有自定义操作均在 `extensions/` 文件夹中进行，并在 `webiny.config.tsx` 中注册。共有四种扩展类型：

**API Extensions（API 扩展）** —— 自定义 GraphQL Schema、解析器、生命周期钩子及业务逻辑。

```typescript
// extensions/NotifyOnPublish.ts — Example: send Slack notification when content is published
class NotifyOnPublish implements CmsLifecycleHook.Interface {
  constructor(private slackService: SlackService.Interface) {}

  async afterPublish(params: AfterPublishParams): Promise<void> {
    await this.slackService.notify(`Content published: ${params.entry.title}`);
  }
}
```

**Admin Extensions（管理后台扩展）** —— 自定义 UI 组件、白标品牌定制、新视图页面、租户专属主题。基于标准 React——使用你熟悉的任何开发模式与库即可。

**Infrastructure Extensions（基础设施扩展）** —— 通过 Pulumi 修改 AWS 资源。可添加 Lambda 函数、S3 存储桶、CloudWatch 告警，或更改现有资源配置。

**CLI Extensions（CLI 扩展）** —— 自定义命令，用于部署工作流、数据迁移及代码生成器。

→ [Extensions Guide](https://www.webiny.com/docs/core-concepts/extensions)

---

## When to Use Webiny

- You need a self-hosted CMS and don't want to run servers
- You need multi-tenancy as a first-class primitive, not a workaround
- You want to extend the CMS with real code (TypeScript), not just configuration
- You need to embed a CMS inside your own product (white-label)
- Data ownership and compliance requirements rule out SaaS CMS
- You want AI agents to be able to build on your content platform effectively
- You're on AWS (or planning to be)

## When Not to Use Webiny

**Be honest with yourself about these（诚实地评估以下场景）：**

- **Simple sites or blogs.** Webiny is built for complex projects. If you need a blog with 10 pages, use something simpler.
- **Not on AWS.** Webiny only runs on AWS. No GCP, no Azure, no on-prem. If that's a dealbreaker, it's a dealbreaker.
- **No TypeScript/React skills on the team.** The entire extension model is TypeScript and React. If your team works in a different stack and doesn't want to adopt these, Webiny won't be a good fit.
- **You want a no-code, plug-and-play SaaS CMS.** Webiny is a platform for developers to build on. If you want zero development involvement, this isn't it.

---

## Licensing

**Community Edition（社区版）** —— MIT 开源协议。永久免费。包含 Headless CMS、Website Builder、File Manager。

**Business Edition（商业版）** —— 商业许可证，起价 $79/月。新增基于角色的访问控制（RBAC）、多租户、发布工作流。

**Enterprise Edition（企业版）** —— 定制定价。新增单点登录（SSO）、审计日志、团队管理、优先技术支持及托管部署选项。

所有版本均包含：无限量的内容条目、页面、资产、API 调用次数、角色和工作流。无按席位收费的陷阱，不对 API 调用量进行计量限制。

→ [Pricing Details](https://www.webiny.com/pricing)

---

## Project Structure

```
my-webiny-project/
  extensions/          # Your custom code lives here
  public/              # Admin app static assets
  webiny.config.tsx    # Project configuration (React components, type-safe)
  package.json
  tsconfig.json
```

仅包含一个 `package.json` 和一个 `tsconfig.json`。`webiny.config.tsx` 中的配置采用 React 组件编写，以提供类型安全与 IDE 自动补全支持。

---

## Key Commands

```bash
npx create-webiny-project <name>    # Create new project
yarn webiny deploy                   # Deploy to AWS
yarn webiny deploy core api          # Deploy specific apps
yarn webiny watch admin              # Local admin dev server
yarn webiny watch api                # Local Lambda dev environment
yarn webiny info                     # Show endpoints and URLs
yarn webiny destroy                  # Tear down all AWS resources
```

---

## Resources

- **[Learn Webiny Course](https://www.webiny.com/learn)** —— 涵盖架构设计、扩展开发、部署流程及 AI 辅助开发的系统化课程
- **[Documentation](https://www.webiny.com/docs)** —— 完整参考手册
- **[Community Slack](https://www.webiny.com/slack)** —— 开发者交流频道
- **[Website Builder Next.js Starter](https://github.com/webiny/website-builder-nextjs)** —— 使用 Next.js 渲染 Webiny 页面的 starter kit

---

## Contributing

我们欢迎社区贡献。请参阅 [CONTRIBUTING.md](docs/CONTRIBUTING.md) 了解贡献指南。

在提交 PR 之前，请先查看现有 Issue 或发起讨论——这有助于我们提供更精准的指导，并避免重复工作。
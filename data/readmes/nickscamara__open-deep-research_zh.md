# Open Deep Research

这是一个开源版本的 OpenAI Deep Research 实验项目。该方法不使用经过微调的 o3 模型，而是结合推理模型与 [Firecrawl 的 extract + search 功能](https://firecrawl.dev/) 对网页进行深度研究。

你可以在[这里](https://x.com/nickscamara_/status/1886459999905521912)查看演示

![Open Deep Research Hero](public/open-hero.png)

## 功能特性

- [Firecrawl](https://firecrawl.dev) 搜索与数据提取（Search + Extract）
  - 通过搜索接口为 AI 提供实时数据
  - 通过提取功能从多个网站获取结构化数据
- [Next.js](https://nextjs.org) App Router（应用路由）
  - 高级路由配置，实现无缝导航与高性能体验
  - 采用 React 服务器组件（RSCs）和服务器操作（Server Actions），支持服务端渲染并提升性能
- [AI SDK](https://sdk.vercel.ai/docs)
  - 提供统一 API，用于通过大语言模型（LLM）生成文本、结构化对象及工具调用
  - 内置 Hooks，便于构建动态聊天界面与生成式用户交互
  - 支持 OpenAI（默认）、Anthropic、Cohere 及其他模型提供商
- [shadcn/ui](https://ui.shadcn.com)
  - 使用 [Tailwind CSS](https://tailwindcss.com) 进行样式设计
  - 基于 [Radix UI](https://radix-ui.com) 的组件基础库，兼顾无障碍访问与灵活性
- 数据持久化
  - 使用由 Neon 驱动的 [Vercel Postgres](https://vercel.com/storage/postgres) 保存聊天记录与用户数据
  - 使用 [Vercel Blob](https://vercel.com/storage/blob) 实现高效文件存储
- [NextAuth.js](https://github.com/nextauthjs/next-auth)
  - 提供简洁安全的身份验证功能

## 模型提供商

本模板默认使用 OpenAI `gpt-4o`。借助 [AI SDK](https://sdk.vercel.ai/docs)，你只需几行代码即可将大语言模型提供商切换为 [OpenAI](https://openai.com)、[Anthropic](https://anthropic.com)、[Cohere](https://cohere.com/) 以及[更多其他选项](https://sdk.vercel.ai/providers/ai-sdk-providers)。

本仓库兼容 [OpenRouter](https://openrouter.ai/) 和 [OpenAI](https://openai.com/)。若要使用 OpenRouter，你需要配置 `OPENROUTER_API_KEY` 环境变量。

## 函数最大运行时长

默认情况下，函数超时时间设置为 300 秒（5 分钟）。如果你使用的是 Vercel 的 Hobby 套餐，需将其降低至 60 秒。你可以通过修改 `.env` 文件中的 `MAX_DURATION` 环境变量来调整此设置：

```bash
MAX_DURATION=60
```

点击[这里](https://vercel.com/docs/functions/configuring-functions/duration#duration-limits)了解更多。

## 自行部署

你可以通过一键操作将你自己的 Next.js AI 聊天机器人版本部署到 Vercel：

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2Fnickscamara%2Fopen-deep-research&env=AUTH_SECRET,OPENAI_API_KEY,OPENROUTER_API_KEY,FIRECRAWL_API_KEY,BLOB_READ_WRITE_TOKEN,POSTGRES_URL,UPSTASH_REDIS_REST_URL,UPSTASH_REDIS_REST_TOKEN,REASONING_MODEL,BYPASS_JSON_VALIDATION,TOGETHER_API_KEY,MAX_DURATION&envDescription=Learn%20more%20about%20how%20to%20get%20the%20API%20Keys%20for%20the%20application&envLink=https%3A%2F%2Fgithub.com%2Fvercel%2Fai-chatbot%2Fblob%2Fmain%2F.env.example&demo-title=AI%20Chatbot&demo-description=An%20Open-Source%20AI%20Chatbot%20Template%20Built%20With%20Next.js%20and%20the%20AI%20SDK%20by%20Vercel.&demo-url=https%3A%2F%2Fchat.vercel.ai&stores=[{%22type%22:%22postgres%22},{%22type%22:%22blob%22}])

## 本地运行

运行 Next.js AI 聊天机器人需要配置 [.env.example](.env.example) 中定义的环境变量。推荐使用 [Vercel 环境变量](https://vercel.com/docs/projects/environment-variables)，但仅使用 `.env` 文件也完全足够。

> 注意：请勿提交你的 `.env` 文件，否则将泄露密钥，导致他人可控制你各类 OpenAI 及身份验证提供商的账户。

1. 安装 Vercel CLI：`npm i -g vercel`
2. 将本地实例与 Vercel 和 GitHub 账户关联（会创建 `.vercel` 目录）：`vercel link`
3. 拉取环境变量配置：`vercel env pull`

# 1. 首先安装所有依赖项
```bash
pnpm install
```

# 2. 然后运行数据库迁移
```bash
pnpm db:migrate
```

# 3. 启动应用
```bash
pnpm dev
```

现在你的应用模板应该已在 [localhost:3000](http://localhost:3000/) 上运行。


# 模型依赖项

如果你想使用非默认的其他模型，需要安装该模型对应的依赖项。


TogetherAI 的 Deepseek：
```bash
pnpm add @ai-sdk/togetherai
```

注意：存在最大速率限制（Rate Limit） https://docs.together.ai/docs/rate-limits

## 推理模型配置

该应用使用独立的模型来处理推理任务（如研究分析与结构化输出）。你可通过 `REASONING_MODEL` 环境变量进行配置。

### 可用选项

| Provider | Models | Notes |
|----------|--------|-------|
| OpenAI | `gpt-4o`, `o1`, `o3-mini` | Native JSON schema support |
| TogetherAI | `deepseek-ai/DeepSeek-R1` | Requires `BYPASS_JSON_VALIDATION=true` |

### 重要说明

- 仅部分 OpenAI 模型（gpt-4o、o1、o3-mini）原生支持结构化 JSON 输出
- 其他模型（如 deepseek-reasoner）也可使用，但可能需要禁用 JSON Schema 验证
- 当使用不支持 JSON Schema 的模型时：
  - 在 `.env` 文件中设置 `BYPASS_JSON_VALIDATION=true`
  - 这将允许非 OpenAI 模型用于推理任务
  - 注意：若无 JSON 验证，模型响应可能缺乏结构化格式
- 该推理模型用于需要结构化思维与分析的任务，例如：
  - 研究分析
  - 文档建议生成
  - 数据提取
  - 结构化响应输出
- 若未指定 `REASONING_MODEL`，默认将使用 `o1-mini`
- 若指定的模型无效，系统将自动回退至 `o1-mini`

### 使用方法

将其添加到你的 `.env` 文件中：
```bash
# Choose one of: deepseek-reasoner, deepseek-ai/DeepSeek-R1
REASONING_MODEL=deepseek-ai/DeepSeek-R1

# Required when using models that don't support JSON schema (like deepseek-reasoner)
BYPASS_JSON_VALIDATION=true
```

当应用需要结构化输出或复杂分析时，会自动调用该推理模型。这与用户在常规聊天中选择的模型无关。
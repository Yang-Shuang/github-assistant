<a href="https://www.llamacoder.io">
  <img alt="Llama Coder" src="./public/og-image.png">
  <h1 align="center">Llama Coder</h1>
</a>

<p align="center">
  一个开源的 Claude Artifacts——通过一条提示词即可生成小型应用。由 Together.ai 上的 Llama 3 驱动。
</p>

## Tech stack

- [Llama 3.1 405B](https://ai.meta.com/blog/meta-llama-3-1/) from Meta for the LLM：使用来自 Meta 的 [Llama 3.1 405B](https://ai.meta.com/blog/meta-llama-3-1/) 作为大语言模型（LLM）
- [Together AI](https://togetherai.link/?utm_source=llamacoder&utm_medium=referral&utm_campaign=example-app) for LLM inference：使用 [Together AI](https://togetherai.link/?utm_source=llamacoder&utm_medium=referral&utm_campaign=example-app) 进行 LLM 推理服务
- [Sandpack](https://sandpack.codesandbox.io/) for the code sandbox：使用 [Sandpack](https://sandpack.codesandbox.io/) 作为代码沙盒环境
- Next.js app router with Tailwind：基于 Next.js 应用路由与 Tailwind CSS 构建
- Helicone for observability：使用 Helicone 实现可观测性（Observability）监控
- Plausible for website analytics：使用 Plausible 进行网站数据分析

## Cloning & running

1. Clone the repo: `git clone https://github.com/Nutlope/llamacoder` → 克隆仓库：`git clone https://github.com/Nutlope/llamacoder`
2. Create a `.env` file and add your API keys: → 创建 `.env` 文件并添加你的 API 密钥：
   - **[Together AI API key](https://dub.sh/together-ai/?utm_source=example-app\&utm_medium=llamacoder\&utm_campaign=llamacoder-app-signup)**: `TOGETHER_API_KEY=<your_together_ai_api_key>` → **[Together AI API 密钥](https://dub.sh/together-ai/?utm_source=example-app\&utm_medium=llamacoder\&utm_campaign=llamacoder-app-signup)**：`TOGETHER_API_KEY=<你的 Together AI API 密钥>`
   - **[CSB API key](https://codesandbox.io/signin)**: `CSB_API_KEY=<your_csb_api_key>` → **[CSB API 密钥](https://codesandbox.io/signin)**：`CSB_API_KEY=<你的 CSB API 密钥>`
   - **Database URL**: Use [Neon](https://neon.tech) to set up your PostgreSQL database and add the Prisma connection string: `DATABASE_URL=<your_database_url>` → **数据库连接地址**：使用 [Neon](https://neon.tech) 搭建你的 PostgreSQL 数据库，并添加 Prisma 连接字符串：`DATABASE_URL=<你的数据库连接地址>`
3. Run `npm install` and `npm run dev` to install dependencies and run locally → 运行 `npm install` 和 `npm run dev` 安装依赖并在本地启动项目

## Contributing

For contributing to the repo, please see the [contributing guide](./CONTRIBUTING.md) → 如需为本仓库做出贡献，请参阅[贡献指南](./CONTRIBUTING.md)。
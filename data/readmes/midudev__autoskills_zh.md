<div align="center">

<a href="https://autoskills.sh">
<img src="https://autoskills.sh/og.jpg" alt="autoskills" />
</a>

# autoskills

**一条命令。你的完整 AI 技能栈，已就绪。**

[autoskills.sh](https://autoskills.sh)

</div>

扫描项目、检测技术栈，并自动安装精选的 AI Agent（智能体）技能。

```bash
npx autoskills
```

## 工作原理

1. 在项目根目录运行 `npx autoskills`
2. 扫描你的 `package.json`、Gradle 文件及配置文件以检测技术栈
3. 从经过审核的 autoskills 注册表中匹配并选择最合适的 AI Agent 技能
4. 仅下载选中的技能文件，并在本地写入前进行验证

就是这样。无需任何配置。

## 安全模型

`autoskills` 不会在运行时直接从随机的上游仓库拉取内容。

维护者会将技能同步至仓库本地的 autoskills 注册表中，扫描提示词注入（prompt-injection）和供应链风险，并在清单中记录 SHA-256 哈希值。当你运行 `autoskills` 时，CLI 仅从该精选注册表下载项目所需的技能，根据清单验证每个文件，并写入包含安装来源与包哈希的 `skills-lock.json` 条目。

这既保持了安装包体积小巧，又避免了在安装过程中从第三方技能源进行实时下载。

## 选项

```
-y, --yes       Skip confirmation prompt
--dry-run       Show what would be installed without installing
-h, --help      Show help message
```

## 支持的技术栈

专为现代前端、后端、移动端、云端及媒体技术栈设计。

- **框架与 UI：** React, Next.js, Vue, Nuxt, Svelte, Angular, Astro, Tailwind CSS, shadcn/ui, GSAP, Three.js
- **语言与运行时环境：** TypeScript, Node.js, Go, Bun, Deno, Dart
- **后端与 API：** Express, Hono, NestJS, Spring Boot
- **移动端与桌面端：** Expo, React Native, Flutter, SwiftUI, Android, Kotlin Multiplatform, Tauri, Electron
- **数据与存储：** Supabase, Neon, Prisma, Drizzle ORM, Zod, React Hook Form
- **认证与计费：** Better Auth, Clerk, Stripe
- **测试：** Vitest, Playwright
- **云端与基础设施：** Vercel, Vercel AI SDK, Cloudflare, Durable Objects, Cloudflare Agents, Cloudflare AI, AWS, Azure, Terraform
- **开发工具：** Turborepo, Vite, oxlint
- **媒体与 AI：** Remotion, ElevenLabs

## 环境要求

Node.js >= 22

## 许可证

[CC BY-NC 4.0](./LICENSE) — [midudev](https://midu.dev)
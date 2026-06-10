# Claude Code 基础设施展示

**一套经过生产环境验证的 Claude Code 基础设施参考库。**

源于 6 个月管理复杂 TypeScript 微服务项目的实战经验，本展示提供了那些解决了“技能无法自动激活”问题并将 Claude Code 扩展至企业级开发的模式与系统。

> **这不是一个可直接运行的应用程序**——它是一套参考库。按需复制到你自己的项目中即可。

---

## 内容概览

**适用于以下场景的生产级基础设施：**
- ✅ 通过 Hook（钩子）实现**技能自动激活**
- ✅ **模块化技能模式**（遵循 500 行规则与渐进式披露）
- ✅ 针对复杂任务的**专用 Agent（智能体）**
- ✅ 可抵御上下文重置的**开发文档系统**
- ✅ 基于通用博客领域的**完整示例**

**构建耗时：** 6 个月迭代打磨  
**集成到项目所需时间：** 15-30 分钟

---

## 快速开始 - 选择你的路径

### 🤖 使用 Claude Code 进行集成？

**Claude：** 阅读 [`CLAUDE_INTEGRATION_GUIDE.md`](CLAUDE_INTEGRATION_GUIDE.md) 获取专为 AI 辅助设置量身定制的分步集成指南。

### 🎯 我想要技能自动激活功能

**突破性特性：** 真正在你需要时自动激活的技能。

**你需要准备：**
1. 技能激活 Hooks（共 2 个文件）
2. 一两个与你工作相关的技能
3. 15 分钟时间

**👉 [设置指南：.claude/hooks/README.md](.claude/hooks/README.md)**

### 📚 我只想添加一个技能

浏览 [技能目录](.claude/skills/) 并复制你需要的内容。

**当前提供：**
- `backend-dev-guidelines`（后端开发规范） - Node.js/Express/TypeScript 模式
- `frontend-dev-guidelines`（前端开发规范） - React/TypeScript/MUI v7 模式
- `skill-developer`（技能开发者） - 用于创建技能的元技能
- `route-tester`（路由测试器） - 测试需认证的 API 路由
- `error-tracking`（错误追踪） - Sentry 集成模式

**👉 [技能指南：.claude/skills/README.md](.claude/skills/README.md)**

### 🤖 我想要专用 Agent（智能体）

10 个经过生产验证的 Agent，用于处理复杂任务：
- 代码架构审查
- 重构辅助
- 文档生成
- 错误调试
- 以及更多……

**👉 [Agent 指南：.claude/agents/README.md](.claude/agents/README.md)**

---

## 核心差异

### 自动激活的突破

**痛点：** Claude Code 的技能通常闲置在那里，你必须手动记住去调用它们。

**解决方案：** `UserPromptSubmit` Hook（钩子），具备以下功能：
- 分析你的提示词
- 检查文件上下文
- 自动推荐相关技能
- 通过 `skill-rules.json` 配置实现工作流

**效果：** 技能在你需要时激活，而不是靠你记起来才去用。

### 经过生产验证的模式

这些不是理论示例——它们提取自：
- ✅ 6 个生产环境中的微服务
- ✅ 超过 50,000 行 TypeScript 代码
- ✅ 包含复杂数据网格的 React 前端
- ✅ 复杂的业务流程引擎
- ✅ 每天使用 Claude Code 长达 6 个月

这些模式行之有效，因为它们解决了真实场景中的问题。

### 模块化技能（500 行规则）

大型技能容易触及上下文长度限制。解决方案如下：

```
skill-name/
  SKILL.md                  # <500 lines, high-level guide
  resources/
    topic-1.md              # <500 lines each
    topic-2.md
    topic-3.md
```

**渐进式披露：** Claude 首先加载主技能文件，仅在需要时才按需加载资源文件。

---

## 仓库结构

```
.claude/
├── skills/                 # 5 个生产级技能
│   ├── backend-dev-guidelines/  (12 个资源文件)
│   ├── frontend-dev-guidelines/ (11 个资源文件)
│   ├── skill-developer/         (7 个资源文件)
│   ├── route-tester/
│   ├── error-tracking/
│   └── skill-rules.json    # 技能激活配置
├── hooks/                  # 6 个自动化 Hook
│   ├── skill-activation-prompt.*  (核心必需)
│   ├── post-tool-use-tracker.sh   (核心必需)
│   ├── tsc-check.sh        (可选，需自定义)
│   └── trigger-build-resolver.sh  (可选)
├── agents/                 # 10 个专用 Agent
│   ├── code-architecture-reviewer.md
│   ├── refactor-planner.md
│   ├── frontend-error-fixer.md
│   └── ... 其余 7 个
└── commands/               # 3 个斜杠命令
    ├── dev-docs.md
    └── ...

dev/
└── active/                 # 开发文档模式示例
    └── public-infrastructure-repo/
```

---

## 组件目录

### 🎨 技能（共 5 个）

| 技能 | 行数 | 用途 | 最佳适用场景 |
|-------|-------|---------|----------|
| [**skill-developer**](.claude/skills/skill-developer/) | 426 | 创建与管理技能 | 元开发（Meta-development） |
| [**backend-dev-guidelines**](.claude/skills/backend-dev-guidelines/) | 304 | Express/Prisma/Sentry 模式 | 后端 API |
| [**frontend-dev-guidelines**](.claude/skills/frontend-dev-guidelines/) | 398 | React/MUI v7/TypeScript | React 前端 |
| [**route-tester**](.claude/skills/route-tester/) | 389 | 测试需认证的路由 | API 测试 |
| [**error-tracking**](.claude/skills/error-tracking/) | ~250 | Sentry 集成 | 错误监控 |

**所有技能均遵循模块化模式**——主文件 + 资源文件，实现渐进式披露。

**👉 [如何集成技能 →](.claude/skills/README.md)**

### 🪝 Hooks（钩子，共 6 个）

| Hook | 类型 | 是否必需？ | 定制需求 |
|------|------|-----------|----------|
| skill-activation-prompt | UserPromptSubmit | ✅ 是 | ✅ 无需定制 |
| post-tool-use-tracker | PostToolUse | ✅ 是 | ✅ 无需定制 |
| tsc-check | Stop | ⚠️ 可选 | ⚠️ 较重 - 仅限 Monorepo |
| trigger-build-resolver | Stop | ⚠️ 可选 | ⚠️ 较重 - 仅限 Monorepo |
| error-handling-reminder | Stop | ⚠️ 可选 | ⚠️ 中等 |
| stop-build-check-enhanced | Stop | ⚠️ 可选 | ⚠️ 中等 |

**建议从两个核心 Hook 开始使用**——它们可启用技能自动激活，且开箱即用。

**👉 [Hook 设置指南 →](.claude/hooks/README.md)**

### 🤖 Agent（智能体，共 10 个）

**独立运行 - 直接复制即可使用！**

| Agent | 用途 |
|-------|---------|
| code-architecture-reviewer | 审查代码的架构一致性 |
| code-refactor-master | 规划并执行重构 |
| documentation-architect | 生成全面的技术文档 |
| frontend-error-fixer | 调试前端错误 |
| plan-reviewer | 评审开发计划 |
| refactor-planner | 制定重构策略 |
| web-research-specialist | 在线调研技术问题 |
| auth-route-tester | 测试需认证的接口 |
| auth-route-debugger | 调试认证相关问题 |
| auto-error-resolver | 自动修复 TypeScript 错误 |

**👉 [Agent 工作机制 →](.claude/agents/README.md)**

### 💬 斜杠命令（共 3 个）

| 命令 | 用途 |
|---------|---------|
| `/dev-docs` | 创建结构化的开发文档 |
| `/dev-docs-update` | 在上下文重置前更新文档 |
| `/route-research-for-testing` | 调研用于测试的路由模式 |

---

## 核心概念

### Hook + skill-rules.json = 自动激活机制

**工作原理：**
1. `skill-activation-prompt` Hook 会在每次用户输入提示词时触发
2. 检查 **skill-rules.json** 中的触发模式
3. 自动推荐相关技能
4. 仅在需要时加载技能

**这解决了 Claude Code 技能的头号痛点：** 它们无法自行激活。

### 渐进式披露（500 行规则）

**问题：** 大型技能容易触及上下文限制  
**解决方案：** 模块化结构
- 主 `SKILL.md`（<500 行，包含概览与导航）
- 资源文件（每个 <500 行，用于深度解析）
- Claude 按需逐步加载

**示例：** `backend-dev-guidelines` 包含 12 个资源文件，涵盖路由、控制器、服务层、仓储层、测试等。

### 开发文档模式

**问题：** 上下文重置会导致项目信息丢失  
**解决方案：** 三文件结构
- `[任务名]-plan.md`（战略规划）
- `[任务名]-context.md`（关键决策与相关文件）
- `[任务名]-tasks.md`（清单格式）

**配合使用：** 通过 `/dev-docs` 斜杠命令自动生成这些文件。

---

## ⚠️ 重要提示：开箱即用的限制

### `settings.json`
内置的 `settings.json` 仅为**示例**：
- Stop 类 Hook 引用了特定的 Monorepo（多包仓库）结构
- 服务名称（如 blog-api 等）仅为示例
- 你的环境中可能不存在对应的 MCP Server

**使用方法：**
1. 仅提取 `UserPromptSubmit` 和 `PostToolUse` Hook
2. 自定义或跳过 Stop 类 Hook
3. 根据你的环境更新 MCP Server 列表

### 博客领域示例
技能使用了通用的博客示例（文章/评论/用户）：
- 这些仅为**教学示例**，并非硬性要求
- 该模式适用于任何领域（电商、SaaS 等）
- 请根据你的业务逻辑调整模式

### Hook 目录结构
部分 Hook 期望特定的目录结构：
- `tsc-check.sh` 需要服务级目录
- 请根据你的项目布局进行定制

---

## 集成工作流

**推荐步骤：**

### 阶段一：技能激活（约 15 分钟）
1. 复制 `skill-activation-prompt` Hook
2. 复制 `post-tool-use-tracker` Hook
3. 更新 `settings.json`
4. 安装 Hook 依赖项

### 阶段二：添加首个技能（约 10 分钟）
1. 选择一个与你工作相关的技能
2. 复制该技能的目录
3. 创建或更新 `skill-rules.json`
4. 自定义路径匹配模式

### 阶段三：测试与迭代（约 5 分钟）
1. 编辑文件 - 观察技能是否自动激活
2. 提问 - 观察技能是否被推荐
3. 按需添加更多技能

### 阶段四：可选增强功能
- 添加你常用的 Agent
- 添加斜杠命令
- 自定义 Stop Hook（高级）

---

## 获取帮助

### 面向用户
**集成遇到问题？**
1. 查阅 [CLAUDE_INTEGRATION_GUIDE.md](CLAUDE_INTEGRATION_GUIDE.md)
2. 询问 Claude：“为什么 [技能名] 没有激活？”
3. 提交 Issue 时附上你的项目结构

### 面向 Claude Code（AI）
协助用户集成时：
1. **优先阅读 `CLAUDE_INTEGRATION_GUIDE.md`**
2. 询问对方的项目结构
3. 按需定制，不要盲目复制
4. 集成完成后进行验证

---

## 解决的核心问题

### 使用此基础设施前

❌ 技能无法自动激活  
❌ 必须手动记住该调用哪个技能  
❌ 大型技能容易触及上下文限制  
❌ 上下文重置会导致项目信息丢失  
❌ 开发过程缺乏一致性规范  
❌ 每次都需要手动调用 Agent  

### 使用此基础设施后

✅ 技能会根据上下文主动推荐  
✅ Hook 在恰当时机触发技能  
✅ 模块化设计使技能始终处于上下文限制内  
✅ 开发文档可在重置间持久化知识  
✅ 通过护栏机制保持规范一致性  
✅ Agent 大幅简化复杂任务处理  

---

## 社区反馈

**觉得有用？**

- ⭐ Star 本仓库
- 🐛 提交 Issue 或建议改进
- 💬 分享你自己的技能/Hook/Agent
- 📝 贡献你所在领域的示例

**背景说明：**  
该基础设施的详细实践曾发布于 Reddit 帖子 ["Claude Code is a Beast – Tips from 6 Months of Hardcore Use"](https://www.reddit.com/r/ClaudeAI/comments/1oivjvm/claude_code_is_a_beast_tips_from_6_months_of/)。在收到数百次请求后，我创建了本展示库，以帮助社区更好地落地这些模式。

---

## 许可证

MIT License - 可自由用于你的项目（商业或个人均可）。

---

## 快速链接

- 📖 [Claude 集成指南](CLAUDE_INTEGRATION_GUIDE.md) - 适用于 AI 辅助设置
- 🎨 [技能文档](.claude/skills/README.md)
- 🪝 [Hook 设置](.claude/hooks/README.md)
- 🤖 [Agent 指南](.claude/agents/README.md)
- 📝 [开发文档模式](dev/README.md)

**从这里开始：** 复制两个核心 Hook，添加一个技能，体验自动激活的魔法。
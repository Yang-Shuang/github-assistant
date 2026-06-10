# Claude Code 项目配置示例

> 大多数软件工程师都严重低估了当前大语言模型（LLM）智能体的强大能力，尤其是像 Claude Code 这样的工具。

配置好 Claude Code 后，你可以让它指向你的代码库，学习你的开发规范，吸收最佳实践，并不断打磨优化，直到它基本上像一个功能超群的队友在运作。**真正的关键在于构建一套可复用的“[技能（Skills）](#skills---domain-knowledge)”以及几个用于日常任务的“[智能体（Agents）](#agents---specialized-assistants)”。**

### 实际应用场景

**自定义 UI 库？** 我们有一个 [解释如何精确使用它的技能](.claude/skills/core-components/SKILL.md)。[测试编写规范](.claude/skills/testing-patterns/SKILL.md)、[GraphQL 结构规范](.claude/skills/graphql-schema/SKILL.md)等也是如此，基本上涵盖了我们在仓库中希望一切按标准执行的方式。因此当 Claude 生成代码时，开箱即用就能匹配我们的模式和标准。

**自动化质量门禁？** 我们使用 [hooks（钩子）](.claude/settings.json) 来自动格式化代码、在测试文件变更时运行测试、进行 TypeScript 类型检查，甚至 [阻止对 main 分支的编辑](.claude/settings.md)。Claude Code 还创建了大量 ESLint 自动化配置，包括自定义规则和 lint 检查，能在提交审查前拦截问题。

**深度代码审查？** 我们有一个 [代码审查智能体（agent）](.claude/agents/code-reviewer.md)，在代码变更后由 Claude 自动运行。它遵循一份详细的检查清单，涵盖 TypeScript 严格模式、错误处理、加载状态、变更模式等。当 PR 提交时，我们会通过一个 [GitHub Action](.github/workflows/pr-claude-code-review.yml) 自动执行完整的 PR 审查。

**定时维护？** 我们配置了 GitHub workflow 智能体按计划运行：
- [每月文档同步](.github/workflows/scheduled-claude-code-docs-sync.yml) - 读取过去一个月的提交记录，确保文档仍保持一致
- [每周代码质量检查](.github/workflows/scheduled-claude-code-quality.yml) - 随机审查目录并自动修复问题
- [双周依赖审计](.github/workflows/scheduled-claude-code-dependency-audit.yml) - 安全更新依赖并进行测试验证

**智能技能推荐？** 我们构建了一个 [技能评估系统](#skill-evaluation-hooks)，它会分析每条提示词，并根据关键词、文件路径和意图模式自动建议 Claude 激活哪些技能。

大量的维护和质检工作就这样实现了自动化。运行起来极其顺畅。

**JIRA/Linear 集成？** 我们通过 [MCP 服务器](.mcp.json)将 Claude Code 连接到工单系统。现在 Claude 可以读取工单、理解需求、实现功能、更新工单状态，甚至在开发过程中发现 bug 时创建新工单。[`/ticket` 命令](.claude/commands/ticket.md) 处理整个工作流——从阅读验收标准到将 PR 关联回工单。

我们甚至用 Claude Code 进行工单分类。它会读取工单、深入代码库，并留下一条评论说明它认为应该做什么。这样当工程师接手时，基本上已经完成了半程工作。

**这里的“低垂果实”实在太多了，说实话，我简直不敢相信大家还没全面采用。**

---

## 目录

- [目录结构](#directory-structure)
- [快速开始](#quick-start)
- [配置参考](#configuration-reference)
  - [CLAUDE.md - 项目记忆](#claudemd---project-memory)
  - [settings.json - Hooks（钩子）与环境](#settingsjson---hooks--environment)
  - [MCP Servers - 外部集成](#mcp-servers---external-integrations)
  - [LSP Servers - 实时代码智能](#lsp-servers---real-time-code-intelligence)
  - [技能评估 Hooks（钩子）](#skill-evaluation-hooks)
  - [Skills（技能）- 领域知识](#skills---domain-knowledge)
  - [Agents（智能体）- 专用助手](#agents---specialized-assistants)
  - [Commands（命令）- 斜杠命令](#commands---slash-commands)
- [GitHub Actions Workflows（工作流）](#github-actions-workflows)
- [最佳实践](#best-practices)
- [本仓库中的示例](#examples-in-this-repository)

---

## 目录结构

```
your-project/
├── CLAUDE.md                      # Project memory (alternative location)
├── .mcp.json                      # MCP server configuration (JIRA, GitHub, etc.)
├── .claude/
│   ├── settings.json              # Hooks, environment, permissions
│   ├── settings.local.json        # Personal overrides (gitignored)
│   ├── settings.md                # Human-readable hook documentation
│   ├── .gitignore                 # Ignore local/personal files
│   │
│   ├── agents/                    # Custom AI agents
│   │   └── code-reviewer.md       # Proactive code review agent
│   │
│   ├── commands/                  # Slash commands (/command-name)
│   │   ├── onboard.md             # Deep task exploration
│   │   ├── pr-review.md           # PR review workflow
│   │   └── ...
│   │
│   ├── hooks/                     # Hook scripts
│   │   ├── skill-eval.sh          # Skill matching on prompt submit
│   │   ├── skill-eval.js          # Node.js skill matching engine
│   │   └── skill-rules.json       # Pattern matching configuration
│   │
│   ├── skills/                    # Domain knowledge documents
│   │   ├── README.md              # Skills overview
│   │   ├── testing-patterns/
│   │   │   └── SKILL.md
│   │   ├── graphql-schema/
│   │   │   └── SKILL.md
│   │   └── ...
│   │
│   └── rules/                     # Modular instructions (optional)
│       ├── code-style.md
│       └── security.md
│
└── .github/
    └── workflows/
        ├── pr-claude-code-review.yml           # Auto PR review
        ├── scheduled-claude-code-docs-sync.yml # Monthly docs sync
        ├── scheduled-claude-code-quality.yml   # Weekly quality review
        └── scheduled-claude-code-dependency-audit.yml
```

---

## 快速开始

### 1. 创建 `.claude` 目录

```bash
mkdir -p .claude/{agents,commands,hooks,skills}
```

### 2. 添加 CLAUDE.md 文件

在项目根目录创建 `CLAUDE.md`，填入项目的关键信息。完整示例见 [CLAUDE.md](CLAUDE.md)。

```markdown
# Project Name

## Quick Facts
- **Stack**: React, TypeScript, Node.js
- **Test Command**: `npm run test`
- **Lint Command**: `npm run lint`

## Key Directories
- `src/components/` - React components
- `src/api/` - API layer
- `tests/` - Test files

## Code Style
- TypeScript strict mode
- Prefer interfaces over types
- No `any` - use `unknown`
```

### 3. 添加包含 hooks（钩子）的 settings.json

创建 `.claude/settings.json`。完整示例见 [settings.json](.claude/settings.json)，包含自动格式化、测试等配置。

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "[ \"$(git branch --show-current)\" != \"main\" ] || { echo '{\"block\": true, \"message\": \"Cannot edit on main branch\"}' >&2; exit 2; }",
            "timeout": 5
          }
        ]
      }
    ]
  }
}
```

### 4. 添加你的第一个技能

创建 `.claude/skills/testing-patterns/SKILL.md`。完整示例见 [testing-patterns/SKILL.md](.claude/skills/testing-patterns/SKILL.md)。

```markdown
---
name: testing-patterns
description: Jest testing patterns for this project. Use when writing tests, creating mocks, or following TDD workflow.
---

# Testing Patterns

## Test Structure
- Use `describe` blocks for grouping
- Use `it` for individual tests
- Follow AAA pattern: Arrange, Act, Assert

## Mocking
- Use factory functions: `getMockUser(overrides)`
- Mock external dependencies, not internal modules
```

> **提示：** `description` 字段至关重要——Claude 会用它来决定何时应用该技能。请包含用户自然提及的关键词。

---

## 配置参考

### CLAUDE.md - 项目记忆

CLAUDE.md 是 Claude 的持久化记忆，会在会话开始时自动加载。

**位置（按优先级排序）：**
1. `.claude/CLAUDE.md`（项目级，位于 .claude 文件夹内）
2. `./CLAUDE.md`（项目根目录）
3. `~/.claude/CLAUDE.md`（用户级，适用于所有项目）

**建议包含的内容：**
- 技术栈与架构概览
- 关键命令（测试、构建、Lint、部署）
- 代码风格规范
- 重要目录及其用途
- 核心规则与约束

**📄 示例：** [CLAUDE.md](CLAUDE.md)

---

### settings.json - Hooks & Environment

用于配置 hooks（钩子）、环境变量和权限的主配置文件。

**位置：** `.claude/settings.json`

**📄 示例：** [settings.json](.claude/settings.json) | [人类可读文档](.claude/settings.md)

#### Hooks（钩子）事件

| Event | When It Fires | Use Case |
|-------|---------------|----------|
| `PreToolUse` | Before tool execution | Block edits on main, validate commands |
| `PostToolUse` | After tool completes | Auto-format, run tests, lint |
| `UserPromptSubmit` | User submits prompt | Add context, suggest skills |
| `Stop` | Agent finishes | Decide if Claude should continue |

#### Hooks（钩子）响应格式

```json
{
  "block": true,           // Block the action (PreToolUse only)
  "message": "Reason",     // Message to show user
  "feedback": "Info",      // Non-blocking feedback
  "suppressOutput": true,  // Hide command output
  "continue": false        // Whether to continue
}
```

#### 退出码
- `0` - Success
- `2` - Blocking error (PreToolUse only, blocks the tool)
- Other - Non-blocking error

---

### MCP Servers - External Integrations

MCP（模型上下文协议）服务器允许 Claude Code 连接到 JIRA、GitHub、Slack、数据库等外部工具。这是实现“读取工单、实现功能并更新状态”等工作流的关键。

**位置：** `.mcp.json`（项目根目录，提交至 Git 以便团队共享）

**📄 示例：** [.mcp.json](.mcp.json)

#### MCP 工作原理

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   Claude Code   │────▶│   MCP Server    │────▶│  External API   │
│                 │◀────│  (local bridge) │◀────│  (JIRA, GitHub) │
└─────────────────┘     └─────────────────┘     └─────────────────┘
```

MCP 服务器在本地运行，为 Claude 提供与外部服务交互的工具。配置 JIRA MCP 服务器后，Claude 将获得如 `jira_get_issue`、`jira_update_issue`、`jira_create_issue` 等工具。

#### .mcp.json 格式

```json
{
  "mcpServers": {
    "server-name": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@anthropic/mcp-server-name"],
      "env": {
        "API_KEY": "${API_KEY}"
      }
    }
  }
}
```

**字段说明：**

| Field | Required | Description |
|-------|----------|-------------|
| `type` | Yes | Server type: `stdio` (local process) or `http` (remote) |
| `command` | For stdio | Executable to run (e.g., `npx`, `python`) |
| `args` | No | Command-line arguments |
| `env` | No | Environment variables (supports `${VAR}` expansion) |
| `url` | For http | Remote server URL |
| `headers` | For http | HTTP headers for authentication |

#### 示例：JIRA 集成

```json
{
  "mcpServers": {
    "jira": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@anthropic/mcp-jira"],
      "env": {
        "JIRA_HOST": "${JIRA_HOST}",
        "JIRA_EMAIL": "${JIRA_EMAIL}",
        "JIRA_API_TOKEN": "${JIRA_API_TOKEN}"
      }
    }
  }
}
```

**此配置可实现：**
- Read ticket details, acceptance criteria, and comments
- Update ticket status (To Do → In Progress → In Review)
- Add comments with progress updates
- Create new tickets for bugs found during development
- Link PRs to tickets

**使用 [`/ticket` 命令](.claude/commands/ticket.md) 的工作流示例：**
```
You: /ticket PROJ-123

Claude:
1. Fetching PROJ-123 from JIRA...
   "Add user profile avatar upload"

2. Reading acceptance criteria...
   - Upload button on profile page
   - Support JPG/PNG up to 5MB
   - Show loading state

3. Searching codebase for related files...
   Found: src/screens/Profile/ProfileScreen.tsx

4. Creating branch: cw/PROJ-123-avatar-upload

5. [Implements feature...]

6. Updating JIRA status to "In Review"
   Adding comment: "PR #456 ready for review"

7. Creating PR linked to PROJ-123...
```

#### 常见 MCP 服务器配置

**问题追踪：**
```json
{
  "jira": {
    "type": "stdio",
    "command": "npx",
    "args": ["-y", "@anthropic/mcp-jira"],
    "env": {
      "JIRA_HOST": "${JIRA_HOST}",
      "JIRA_EMAIL": "${JIRA_EMAIL}",
      "JIRA_API_TOKEN": "${JIRA_API_TOKEN}"
    }
  },
  "linear": {
    "type": "stdio",
    "command": "npx",
    "args": ["-y", "@anthropic/mcp-linear"],
    "env": { "LINEAR_API_KEY": "${LINEAR_API_KEY}" }
  }
}
```

**代码与 DevOps：**
```json
{
  "github": {
    "type": "stdio",
    "command": "npx",
    "args": ["-y", "@anthropic/mcp-github"],
    "env": { "GITHUB_TOKEN": "${GITHUB_TOKEN}" }
  },
  "sentry": {
    "type": "stdio",
    "command": "npx",
    "args": ["-y", "@anthropic/mcp-sentry"],
    "env": {
      "SENTRY_AUTH_TOKEN": "${SENTRY_AUTH_TOKEN}",
      "SENTRY_ORG": "${SENTRY_ORG}"
    }
  }
}
```

**通信协作：**
```json
{
  "slack": {
    "type": "stdio",
    "command": "npx",
    "args": ["-y", "@anthropic/mcp-slack"],
    "env": {
      "SLACK_BOT_TOKEN": "${SLACK_BOT_TOKEN}",
      "SLACK_TEAM_ID": "${SLACK_TEAM_ID}"
    }
  }
}
```

**数据库：**
```json
{
  "postgres": {
    "type": "stdio",
    "command": "npx",
    "args": ["-y", "@anthropic/mcp-postgres"],
    "env": { "DATABASE_URL": "${DATABASE_URL}" }
  }
}
```

#### 环境变量

MCP 配置支持变量展开：
- `${VAR}` - Expands to environment variable (fails if not set)
- `${VAR:-default}` - Uses default if VAR is not set

在 Shell 配置文件或 `.env` 文件中设置这些变量（切勿提交密钥！）：
```bash
export JIRA_HOST="https://yourcompany.atlassian.net"
export JIRA_EMAIL="you@company.com"
export JIRA_API_TOKEN="your-api-token"
```

#### MCP 相关配置

在 `settings.json` 中，你可以自动批准 MCP 服务器：

```json
{
  "enableAllProjectMcpServers": true
}
```

或仅批准特定服务器：
```json
{
  "enabledMcpjsonServers": ["jira", "github", "slack"]
}
```

---

### LSP Servers - Real-Time Code Intelligence

LSP（语言服务器协议）让 Claude 能够实时理解你的代码——包括类型信息、错误提示、自动补全和导航。Claude 不再只是读取文本，而是能像你的 IDE 一样“看到”你的代码。

**为什么重要：** 当你编辑 TypeScript 时，Claude 会立即察觉是否引入了类型错误。引用函数时，它能直接跳转到定义处。这将大幅提升代码生成质量。

#### 启用 LSP

LSP 支持通过 `settings.json` 中的插件启用：

```json
{
  "enabledPlugins": {
    "typescript-lsp@claude-plugins-official": true,
    "pyright-lsp@claude-plugins-official": true
  }
}
```

#### Claude 从 LSP 获取的能力

| Feature | Description |
|---------|-------------|
| **Diagnostics** | Real-time errors and warnings after every edit |
| **Type Information** | Hover info, function signatures, type definitions |
| **Code Navigation** | Go to definition, find references |
| **Completions** | Context-aware symbol suggestions |

#### 可用的 LSP 插件

| Plugin | Language | Install Binary First |
|--------|----------|---------------------|
| `typescript-lsp` | TypeScript/JavaScript | `npm install -g typescript-language-server typescript` |
| `pyright-lsp` | Python | `pip install pyright` |
| `rust-lsp` | Rust | `rustup component add rust-analyzer` |

#### 自定义 LSP 配置

对于高级设置，创建 `.lsp.json`：

```json
{
  "typescript": {
    "command": "typescript-language-server",
    "args": ["--stdio"],
    "extensionToLanguage": {
      ".ts": "typescript",
      ".tsx": "typescriptreact"
    },
    "initializationOptions": {
      "preferences": {
        "quotePreference": "single"
      }
    }
  }
}
```

#### 故障排除

如果 LSP 无法正常工作：

1. **检查二进制文件是否已安装：**
   ```bash
   which typescript-language_server  # Should return a path
   ```

2. **启用调试日志：**
   ```bash
   claude --enable-lsp-logging
   ```

3. **检查插件状态：**
   ```bash
   claude /plugin  # View Errors tab
   ```

---

### Skill Evaluation Hooks

我们最强大的自动化功能之一是**技能评估系统**。它会在每次提交提示词时运行，并智能建议 Claude 激活哪些技能。

**📄 相关文件：** [skill-eval.sh](.claude/hooks/skill-eval.sh) | [skill-eval.js](.claude/hooks/skill-eval.js) | [skill-rules.json](.claude/hooks/skill-rules.json)

#### 工作原理

当你提交提示词时，`UserPromptSubmit` 钩子会触发我们的技能评估引擎：

1. **提示词分析** - 引擎会分析你的提示词中的：
   - **Keywords（关键词）**：简单单词匹配（如 `test`、`form`、`graphql`、`bug`）
   - **Patterns（模式）**：正则表达式匹配（如 `\btest(?:s|ing)?\b`、`\.stories\.`）
   - **File Paths（文件路径）**：提取提及的文件（如 `src/components/Button.tsx`）
   - **Intent（意图）**：检测你的目标操作（如 `create.*test`、`fix.*bug`）

2. **目录映射** - 将文件路径映射到相关技能：
   ```json
   {
     "src/components/core": "core-components",
     "src/graphql": "graphql-schema",
     ".github/workflows": "github-actions",
     "src/hooks": "react-ui-patterns"
   }
   ```

3. **置信度评分** - 每种触发类型都有对应的分值：
   ```json
   {
     "keyword": 2,
     "keywordPattern": 3,
     "pathPattern": 4,
     "directoryMatch": 5,
     "intentPattern": 4
   }
   ```

4. **技能推荐** - 超过置信度阈值的技能会附带原因进行推荐：
   ```
   SKILL ACTIVATION REQUIRED

   Detected file paths: src/components/UserForm.tsx

   Matched skills (ranked by relevance):
   1. formik-patterns (HIGH confidence)
      Matched: keyword "form", path "src/components/UserForm.tsx"
   2. react-ui-patterns (MEDIUM confidence)
      Matched: directory mapping, keyword "component"
   ```

#### 配置说明

技能定义在 [skill-rules.json](.claude/hooks/skill-rules.json) 中：

```json
{
  "testing-patterns": {
    "description": "Jest testing patterns and TDD workflow",
    "priority": 9,
    "triggers": {
      "keywords": ["test", "jest", "spec", "tdd", "mock"],
      "keywordPatterns": ["\\btest(?:s|ing)?\\b", "\\bspec\\b"],
      "pathPatterns": ["**/*.test.ts", "**/*.test.tsx"],
      "intentPatterns": [
        "(?:write|add|create|fix).*(?:test|spec)",
        "(?:test|spec).*(?:for|of|the)"
      ]
    },
    "excludePatterns": ["e2e", "maestro", "end-to-end"]
  }
}
```

#### 添加到你的项目

1. 将钩子文件复制到你的项目中：
   ```bash
   cp -r .claude/hooks/ your-project/.claude/hooks/
   ```

2. 在 `settings.json` 中添加该钩子：
   ```json
   {
     "hooks": {
       "UserPromptSubmit": [
         {
           "hooks": [
             {
               "type": "command",
               "command": "\"$CLAUDE_PROJECT_DIR\"/.claude/hooks/skill-eval.sh",
               "timeout": 5
             }
           ]
         }
       ]
     }
   }
   ```

3. 根据你的项目技能和触发条件自定义 [skill-rules.json](.claude/hooks/skill-rules.json)。

---

### Skills - Domain Knowledge

Skills（技能）是 Markdown 文档，用于向 Claude 传授项目特定的模式和规范。

**位置：** `.claude/skills/{skill-name}/SKILL.md`

**📄 示例：**
- [testing-patterns](.claude/skills/testing-patterns/SKILL.md) - TDD、工厂函数与 Mocking
- [systematic-debugging](.claude/skills/systematic-debugging/SKILL.md) - Four-phase debugging methodology
- [react-ui-patterns](.claude/skills/react-ui-patterns/SKILL.md) - Loading states, error handling
- [graphql-schema](.claude/skills/graphql-schema/SKILL.md) - Queries, mutations, codegen
- [core-components](.claude/skills/core-components/SKILL.md) - Design system, tokens
- [formik-patterns](.claude/skills/formik-patterns/SKILL.md) - Form handling, validation

#### SKILL.md 前置字段（Frontmatter）

| Field | Required | Max Length | Description |
|-------|----------|------------|-------------|
| `name` | **Yes** | 64 chars | Lowercase letters, numbers, and hyphens only. Should match directory name. |
| `description` | **Yes** | 1024 chars | What the skill does and when to use it. Claude uses this to decide when to apply the skill. |
| `allowed-tools` | No | - | Comma-separated list of tools Claude can use (e.g., `Read, Grep, Bash(npm:*)`). |
| `model` | No | - | Specific model to use (e.g., `claude-sonnet-4-20250514`). |

#### SKILL.md 格式

```markdown
---
name: skill-name
description: What this skill does and when to use it. Include keywords users would mention.
allowed-tools: Read, Grep, Glob
model: claude-sonnet-4-20250514
---

# Skill Title

## When to Use
- Trigger condition 1
- Trigger condition 2

## Core Patterns

### Pattern Name
```typescript
// Example code
```

## Anti-Patterns

### What NOT to Do
```typescript
// Bad example
```

## Integration
- Related skill: `other-skill`
```

#### 技能编写最佳实践

1. **保持内容聚焦** - 控制在 500 行以内；详细文档请放入独立的引用文件中
2. **编写丰富的触发描述** - Claude 会通过语义匹配来判断何时应用技能，因此描述中需包含相关关键词
3. **提供示例** - 展示正误代码模式
4. **引用其他技能** - 说明各技能如何协同工作
5. **使用精确文件名** - 必须命名为 `SKILL.md`（区分大小写）

---

### Agents - Specialized Assistants

Agents（智能体）是具备特定目标和独立提示词的 AI 助手。

**位置：** `.claude/agents/{agent-name}.md`

**📄 示例：**
- [code-reviewer.md](.claude/agents/code-reviewer.md) - Comprehensive code review with checklist
- [github-workflow.md](.claude/agents/github-workflow.md) - Git commits, branches, PRs

#### 智能体格式

```markdown
---
name: code-reviewer
description: Reviews code for quality, security, and conventions. Use after writing or modifying code.
model: opus
---

# Agent System Prompt

You are a senior code reviewer...

## Your Process
1. Run `git diff` to see changes
2. Apply review checklist
3. Provide feedback

## Checklist
- [ ] No TypeScript `any`
- [ ] Error handling present
- [ ] Tests included
```

#### 智能体配置字段

| Field | Required | Description |
|-------|----------|-------------|
| `name` | Yes | Lowercase with hyphens |
| `description` | Yes | When/why to use (max 1024 chars) |
| `model` | No | `sonnet`, `opus`, or `haiku` |
| `tools` | No | Comma-separated tool list |

---

### Commands - Slash Commands

通过 `/command-name` 调用的自定义命令。

**位置：** `.claude/commands/{command-name}.md`

**📄 示例：**
- [onboard.md](.claude/commands/onboard.md) - Deep task exploration
- [pr-review.md](.claude/commands/pr-review.md) - PR review workflow
- [pr-summary.md](.claude/commands/pr-summary.md) - Generate PR description
- [code-quality.md](.claude/commands/code-quality.md) - Quality checks
- [docs-sync.md](.claude/commands/docs-sync.md) - Documentation alignment

#### 命令格式

```markdown
---
description: Brief description shown in command list
allowed-tools: Bash(git:*), Read, Grep
---

# Command Instructions

Your task is to: $ARGUMENTS

## Steps
1. Do this first
2. Then do this
```

#### 变量说明

- `$ARGUMENTS` - All arguments as single string
- `$1`, `$2`, `$3` - Individual positional arguments

#### 内联 Bash

```markdown
Current branch: !`git branch --show-current`
Recent commits: !`git log --oneline -5`
```

---

## GitHub Actions Workflows

使用 Claude Code 自动化代码审查、质量检查与维护工作。

**📄 示例：**
- [pr-claude-code-review.yml](.github/workflows/pr-claude-code-review.yml) - Auto PR review
- [scheduled-claude-code-docs-sync.yml](.github/workflows/scheduled-claude-code-docs-sync.yml) - Monthly docs sync
- [scheduled-claude-code-quality.yml](.github/workflows/scheduled-claude-code-quality.yml) - Weekly quality review
- [scheduled-claude-code-dependency-audit.yml](.github/workflows/scheduled-claude-code-dependency-audit.yml) - Biweekly dependency updates

### PR 代码审查

自动审查 PR，并响应 `@claude` 提及。

```yaml
name: PR - Claude Code Review
on:
  pull_request:
    types: [opened, synchronize, reopened]
  issue_comment:
    types: [created]

jobs:
  review:
    if: |
      github.event_name == 'pull_request' ||
      (github.event_name == 'issue_comment' &&
       github.event.issue.pull_request &&
       contains(github.event.comment.body, '@claude'))
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - uses: anthropics/claude-code-action@beta
        with:
          anthropic_api_key: ${{ secrets.ANTHROPIC_API_KEY }}
          model: claude-opus-4-5-20251101
          prompt: |
            Review this PR using .claude/agents/code-reviewer.md standards.
            Run `git diff origin/main...HEAD` to see changes.
```

### 定时工作流

| Workflow | Schedule | Purpose |
|----------|----------|---------|
| [Code Quality](.github/workflows/scheduled-claude-code-quality.yml) | Weekly (Sunday) | Reviews random directories, auto-fixes issues |
| [Docs Sync](.github/workflows/scheduled-claude-code-docs-sync.yml) | Monthly (1st) | Ensures docs align with code changes |
| [Dependency Audit](.github/workflows/scheduled-claude-code-dependency-audit.yml) | Biweekly (1st & 15th) | Safe dependency updates with testing |

### 必要设置

将 `ANTHROPIC_API_KEY` 添加到仓库密钥中：
- Settings → Secrets and variables → Actions → New repository secret

### 成本预估

| Workflow | Frequency | Est. Cost |
|----------|-----------|-----------|
| PR Review | Per PR | ~$0.05 - $0.50 |
| Docs Sync | Monthly | ~$0.50 - $2.00 |
| Dependency Audit | Biweekly | ~$0.20 - $1.00 |
| Code Quality | Weekly | ~$1.00 - $5.00 |

**预计每月总计：** ~$10 - $50（取决于 PR 数量）

---

## Best Practices

### 1. 从 CLAUDE.md 开始

你的 `CLAUDE.md` 是基础。请包含：
- 技术栈概览
- 关键命令
- 核心规则
- 目录结构

### 2. 逐步构建技能

不要试图一次性记录所有内容：
1. 从最常用的模式开始
2. 随着痛点出现逐步添加技能
3. 每个技能专注单一领域

### 3. 使用 Hooks（钩子）实现自动化

让钩子处理重复性任务：
- 保存时自动格式化
- 测试文件变更时运行测试
- Schema 变更时重新生成类型定义
- 阻止对受保护分支的编辑

### 4. 为复杂工作流创建智能体（Agents）

智能体非常适合用于：
- 代码审查（配合团队检查清单）
- PR 的创建与管理
- 调试工作流
- 任务上手引导

### 5. 善用 GitHub Actions

自动化维护流程：
- 每次 PR 审查
- 每周质量巡检
- 每月文档对齐
- 依赖更新

### 6. 对配置进行版本控制

提交除以下文件外的所有内容：
- `settings.local.json`（个人偏好设置）
- `CLAUDE.local.md`（个人笔记）
- 用户专属凭证

---

## Examples in This Repository

| File | Description |
|------|-------------|
| [CLAUDE.md](CLAUDE.md) | Example project memory file |
| [.claude/settings.json](.claude/settings.json) | Full hooks configuration |
| [.claude/settings.md](.claude/settings.md) | Human-readable hooks documentation |
| [.mcp.json](.mcp.json) | MCP server configuration (JIRA, GitHub, Slack, etc.) |
| **Agents** | |
| [.claude/agents/code-reviewer.md](.claude/agents/code-reviewer.md) | Comprehensive code review agent |
| [.claude/agents/github-workflow.md](.claude/agents/github-workflow.md) | Git workflow agent |
| **Commands** | |
| [.claude/commands/onboard.md](.claude/commands/onboard.md) | Deep task exploration |
| [.claude/commands/ticket.md](.claude/commands/ticket.md) | **JIRA/Linear ticket workflow (read → implement → update)** |
| [.claude/commands/pr-review.md](.claude/commands/pr-review.md) | PR review workflow |
| [.claude/commands/pr-summary.md](.claude/commands/pr-summary.md) | Generate PR summary |
| [.claude/commands/code-quality.md](.claude/commands/code-quality.md) | Quality checks |
| [.claude/commands/docs-sync.md](.claude/commands/docs-sync.md) | Documentation sync |
| **Hooks** | |
| [.claude/hooks/skill-eval.sh](.claude/hooks/skill-eval.sh) | Skill evaluation wrapper |
| [.claude/hooks/skill-eval.js](.claude/hooks/skill-eval.js) | Node.js skill matching engine |
| [.claude/hooks/skill-rules.json](.claude/hooks/skill-rules.json) | Pattern matching rules |
| **Skills** | |
| [.claude/skills/testing-patterns/SKILL.md](.claude/skills/testing-patterns/SKILL.md) | TDD, factory functions, mocking |
| [.claude/skills/systematic-debugging/SKILL.md](.claude/skills/systematic-debugging/SKILL.md) | Four-phase debugging |
| [.claude/skills/react-ui-patterns/SKILL.md](.claude/skills/react-ui-patterns/SKILL.md) | Loading/error/empty states |
| [.claude/skills/graphql-schema/SKILL.md](.claude/skills/graphql-schema/SKILL.md) | Queries, mutations, codegen |
| [.claude/skills/core-components/SKILL.md](.claude/skills/core-components/SKILL.md) | Design system, tokens |
| [.claude/skills/formik-patterns/SKILL.md](.claude/skills/formik-patterns/SKILL.md) | Form handling, validation |
| **GitHub Workflows** | |
| [.github/workflows/pr-claude-code-review.yml](.github/workflows/pr-claude-code-review.yml) | Auto PR review |
| [.github/workflows/scheduled-claude-code-docs-sync.yml](.github/workflows/scheduled-claude-code-docs-sync.yml) | Monthly docs sync |
| [.github/workflows/scheduled-claude-code-quality.yml](.github/workflows/scheduled-claude-code-quality.yml) | Weekly quality review |
| [.github/workflows/scheduled-claude-code-dependency-audit.yml](.github/workflows/scheduled-claude-code-dependency-audit.yml) | Biweekly dependency audit |

---

## Learn More

- [Claude Code Documentation](https://docs.anthropic.com/en/docs/claude-code)
- [Claude Code Action](https://github.com/anthropics/claude-code-action) - GitHub Action
- [Anthropic API](https://docs.anthropic.com/en/api)

---

## License

MIT - Use this as a template for your own projects.
# Ralph for Claude Code

[![CI](https://github.com/frankbria/ralph-claude-code/actions/workflows/test.yml/badge.svg)](https://github.com/frankbria/ralph-claude-code/actions/workflows/test.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
![Version](https://img.shields.io/badge/version-0.11.5-blue)
![Tests](https://img.shields.io/badge/tests-784%20passing-green)
[![GitHub Issues](https://img.shields.io/github/issues/frankbria/ralph-claude-code)](https://github.com/frankbria/ralph-claude-code/issues)
[![Mentioned in Awesome Claude Code](https://awesome.re/mentioned-badge.svg)](https://github.com/hesreallyhim/awesome-claude-code)
[![Follow on X](https://img.shields.io/twitter/follow/FrankBria18044?style=social)](https://x.com/FrankBria18044)

> **具备智能退出检测与速率限制功能的自主 AI 开发循环**

Ralph 是 Geoffrey Huntley 提出的 [Ralph Wiggum](https://ghuntley.com/ralph/) 技术在 Claude Code 上的实现版本。它支持持续的自主开发周期，让 Claude Code 迭代优化你的项目直至完成，并内置了防止无限循环和 API 过度调用的安全机制（rate limiting）。

**一次安装，随处使用** - Ralph 会成为全局命令，在任何目录下均可调用。

## 项目状态

**版本**：v0.11.5 - 活跃开发中
**核心功能**：已实现并经过测试
**测试覆盖率**：784 项测试，通过率 100%

### 当前可用功能
- 具备智能退出检测的自主开发循环
- **双条件退出门控（Dual-condition exit gate）**：需同时满足完成指标与显式 `EXIT_SIGNAL`
- 按小时重置的速率限制（默认 100 次调用/小时，可配置）
- 具备高级错误检测功能的熔断器（Circuit breaker，防止循环失控）
- 支持语义理解与两级错误过滤的响应分析器
- **支持 JSON 输出格式，并自动降级为文本解析**
- **会话连续性：通过 `--resume` 标志保留上下文（防止会话劫持）**
- **会话过期机制：支持可配置的超时时间（默认：24 小时）**
- **现代 CLI 标志：`--output-format`、`--allowed-tools`、`--no-continue`**
- **通过 `ralph-enable` 向导实现交互式项目启用**
- **支持 `.ralphrc` 配置文件进行项目设置**
- **通过 `--live` 标志实现实时流式输出，直观查看 Claude Code 运行状态**
- **日志轮转：`ralph.log` 在达到 10MB 时自动轮转，保留 4 个归档文件**
- **干跑模式（Dry-run mode, `--dry-run`）：模拟循环执行而不实际调用 API**
- **指标追踪：通过 `ralph-stats` 分析命令记录每次循环的 JSON Lines 格式指标**
- **桌面通知（`--notify`）：针对关键循环事件发送通知（支持 macOS/Linux/终端响铃）**
- **自动 Git 备份分支（`--backup`），并支持通过 `--rollback` 恢复**
- 多行错误匹配，精准检测卡死循环
- 处理 Claude 5 小时 API 使用限制，并提供用户提示
- 集成 tmux 实现实时监控
- PRD（产品需求文档）导入功能
- **基于 GitHub Actions 的 CI/CD 流水线**
- **专用卸载脚本，实现干净移除**

### 近期更新

**v0.11.5 - 社区缺陷修复**（最新版）
- 修复 API 限制误报：超时退出码 124 不再被错误识别为 5 小时 API 限制 (#183)
- 三层 API 限制检测机制：超时守卫 → 结构化 JSON（`rate_limit_event`）→ 过滤文本降级
- 无人值守模式：API 限制提示现在会在超时时自动等待，而非直接退出
- 修复 bash 3.x 兼容性问题：将 `${,,}` 小写替换替换为符合 POSIX 标准的 `tr` 命令 (#187)
- 新增 8 项 API 限制检测测试（总计 548 → 566 项）

**v0.11.4 - 缺陷修复与兼容性改进**
- 修复进度检测：循环内的 Git 提交现在会被计入进度 (#141)
- 修复复选框正则表达式：日期条目 `[2026-01-29]` 不再被误判为复选框 (#144)
- 修复会话劫持问题：改用 `--resume <session_id>` 替代 `--continue` (#151)
- 修复 EXIT_SIGNAL 覆盖问题：当 `STATUS: COMPLETE` 且 `EXIT_SIGNAL: false` 时，现在会正确继续执行 (#146)
- 修复 ralph-import 无限挂起问题（新增 `--print` 标志以支持非交互模式）
- 修复 ralph-import 绝对路径处理逻辑
- 修复 macOS (Homebrew coreutils) 下的跨平台日期命令兼容性问题
- 新增通过环境变量配置熔断器阈值的功能 (#99)
- 新增对非零 `base-index` 配置的 tmux 支持
- 新增 13 项回归测试，覆盖进度检测与复选框正则表达式

**v0.11.3 - 实时流式输出与 Beads 修复**
- 新增通过 `--live` 标志实现的实时流式输出模式，直观查看 Claude Code 运行状态 (#125)
- 修复使用正确 `bd list` 参数导入 beads 任务的问题 (#150)
- 应用 CodeRabbit 审查建议：修正驼峰命名变量、尊重状态降级逻辑及添加 jq 守卫检查
- 新增 12 项测试，覆盖实时流式输出与 beads 导入改进

**v0.11.2 - 安装权限修复**
- 修复问题 #136：`ralph-setup` 现在会创建具有统一工具权限的 `.ralphrc` 文件
- 更新默认 `ALLOWED_TOOLS`，新增 `Edit`、`Bash(npm *)` 和 `Bash(pytest)`
- `ralph-setup` 与 `ralph-enable` 现在均生成一致的 `.ralphrc` 配置
- 监控程序现在会将所有 CLI 参数转发至内部 Ralph 循环 (#126)
- 新增 16 项测试，覆盖权限管理与参数转发

**v0.11.1 - 完成指标修复**
- 修复 JSON 输出模式下恰好执行 5 次循环后过早退出的问题
- `completion_indicators` 现在仅在 `EXIT_SIGNAL: true` 时累积计数
- 行为与文档中描述的双条件退出门控逻辑保持一致

**v0.11.0 - Ralph 启用向导**
- 新增交互式 `ralph-enable` 向导，用于在现有项目中启用 Ralph
- 五阶段向导流程：环境检测 → 任务源选择 → 配置设置 → 文件生成 → 验证检查
- 自动检测项目类型（TypeScript、Python、Rust、Go）及框架（Next.js、FastAPI、Django）
- 支持从 beads、GitHub Issues 或 PRD 文档导入任务
- 新增非交互版 `ralph-enable-ci`，适用于 CI/自动化流程
- 新增核心库组件：`enable_core.sh`、`wizard_utils.sh`、`task_sources.sh`

**v0.10.1 - 缺陷修复与监控路径修正**
- 修复 `ralph_monitor.sh` 硬编码路径，兼容 v0.10.0
- 修复 JSON 格式下的 EXIT_SIGNAL 解析逻辑
- 新增安全熔断器（连续出现 5 次完成指标时强制退出）
- 修复缩进 Markdown 的复选框解析问题

**v0.10.0 - `.ralph/` 子目录结构（破坏性更新）**
- **破坏性变更**：所有 Ralph 专属文件已移至 `.ralph/` 子文件夹
- 项目根目录保持整洁：仅保留 `src/`、`README.md` 及用户自定义文件
- 新增 `ralph-migrate` 命令，用于升级现有项目

<details>
<summary>早期版本 (v0.9.x)</summary>

**v0.9.9 - EXIT_SIGNAL 门控与卸载脚本**
- 修复过早退出缺陷：完成指标现在需要 Claude 显式输出 `EXIT_SIGNAL: true`
- 新增专用 `uninstall.sh` 脚本，实现干净移除 Ralph

**v0.9.8 - PRD 导入的现代 CLI**
- 现代化改造 `ralph_import.sh`，改用 Claude Code CLI JSON 输出格式
- 增强错误处理，采用结构化 JSON 错误消息

**v0.9.7 - 会话生命周期管理**
- 完整的会话生命周期管理，支持自动重置触发机制
- 新增 `--reset-session` CLI 标志用于手动重置会话

**v0.9.6 - JSON 输出与会话管理**
- 扩展 `parse_json_response()` 以支持 Claude Code CLI JSON 格式
- 新增会话管理函数

**v0.9.5 - v0.9.0** - PRD 导入测试、项目设置测试、安装测试、提示词文件修复、现代 CLI 命令、熔断器增强

</details>

### 进行中
- 扩展测试覆盖率
- [自动徽章更新](#138)

**v1.0 时间线**：最终打磨进行中 | [完整路线图](IMPLEMENTATION_PLAN.md) | **欢迎贡献！**

## 功能特性

- **自主开发循环（Autonomous Development Loop）** - 持续执行 Claude Code，处理你的项目需求
- **智能退出检测（Intelligent Exit Detection）** - 双条件检查机制，需同时满足完成指标与显式 EXIT_SIGNAL
- **会话连续性（Session Continuity）** - 跨循环迭代保留上下文，支持自动会话管理
- **会话过期（Session Expiration）** - 可配置超时时间（默认：24 小时），支持自动重置会话
- **速率限制（Rate Limiting）** - 内置 API 调用管理，支持按小时限额与倒计时提示
- **5 小时 API 使用限制处理** - 三层检测机制（超时守卫、JSON 解析、过滤文本）配合无人值守模式自动等待
- **实时监控（Live Monitoring）** - 实时仪表盘显示循环状态、进度与日志
- **任务管理（Task Management）** - 结构化方法，支持优先级任务列表与进度追踪
- **项目模板（Project Templates）** - 快速为新项目设置最佳实践结构
- **交互式项目设置** - `ralph-enable` 向导用于现有项目并导入任务
- **配置文件（Configuration Files）** - `.ralphrc` 管理项目特定设置与工具权限
- **全面日志记录（Comprehensive Logging）** - 带时间戳的详细执行日志与状态追踪
- **可配置超时（Configurable Timeouts）** - 为 Claude Code 操作设置执行超时（1-120 分钟）
- **详细进度模式（Verbose Progress Mode）** - 可选的执行期间详细进度更新
- **响应分析器（Response Analyzer）** - AI 驱动的 Claude Code 响应语义理解与分析
- **熔断器（Circuit Breaker）** - 高级错误检测，支持两级过滤、多行错误匹配与自动恢复
- **CI/CD 集成** - GitHub Actions 工作流与自动化测试
- **干净卸载（Clean Uninstall）** - 专用卸载脚本实现完全移除
- **实时流式输出（Live Streaming Output）** - 通过 `--live` 标志实时查看 Claude Code 执行过程

## 快速入门

Ralph 分为两个阶段：**一次性安装**与**按项目设置**。

```
INSTALL ONCE              USE MANY TIMES
+-----------------+          +----------------------+
| ./install.sh    |    ->    | ralph-setup project1 |
|                 |          | ralph-enable         |
| Adds global     |          | ralph-import prd.md  |
| commands        |          | ...                  |
+-----------------+          +----------------------
```

### 阶段 1：安装 Ralph（仅需一次）

在系统中全局安装 Ralph：

```bash
git clone https://github.com/frankbria/ralph-claude-code.git
cd ralph-claude-code
./install.sh
```

这会将 `ralph`、`ralph-monitor`、`ralph-setup`、`ralph-import`、`ralph-migrate`、`ralph-enable` 和 `ralph-enable-ci` 命令添加到你的 PATH。

> **注意**：你只需在每台系统上执行一次此操作。安装完成后，如需清理可删除已克隆的仓库。

### 阶段 2：初始化项目（按项目进行）

#### 选项 A：在现有项目中启用 Ralph（推荐）
```bash
cd my-existing-project

# 交互式向导 - 自动检测项目类型并导入任务
ralph-enable

# 或指定特定任务源
ralph-enable --from beads
ralph-enable --from github --label "sprint-1"
ralph-enable --from prd ./docs/requirements.md

# 启动自主开发
ralph --monitor
```

#### 选项 B：导入现有 PRD/规范文档
```bash
# 将现有 PRD/规范转换为 Ralph 格式
ralph-import my-requirements.md my-project
cd my-project

# 审查并调整生成的文件：
# - .ralph/PROMPT.md (Ralph 指令)
# - .ralph/fix_plan.md (任务优先级)
# - .ralph/specs/requirements.md (技术规范)

# 启动自主开发
ralph --monitor
```

#### 选项 C：从零创建新项目
```bash
# 创建空白 Ralph 项目
ralph-setup my-awesome-project
cd my-awesome-project

# 手动配置你的项目需求
# 在 .ralph/PROMPT.md 中编辑你的项目目标
# 在 .ralph/specs/ 中编写详细技术规范
# 在 .ralph/fix_plan.md 中设置初始优先级

# 启动自主开发
ralph --monitor
```

### 持续使用（安装完成后）

一旦 Ralph 已安装且项目初始化完成：

```bash
# 导航至任意 Ralph 项目并运行：
ralph --monitor              # 集成 tmux 监控（推荐）

# 或使用独立终端：
ralph                        # 终端 1：Ralph 循环
ralph-monitor               # 终端 2：实时监控仪表盘
```

### 卸载 Ralph

要从系统中完全移除 Ralph：

```bash
# 运行卸载脚本
./uninstall.sh

# 或如果你已删除仓库，可下载并运行：
curl -sL https://raw.githubusercontent.com/frankbria/ralph-claude-code/main/uninstall.sh | bash
```

## 理解 Ralph 文件结构

运行 `ralph-enable` 或 `ralph-import` 后，你将获得一个包含多个文件的 `.ralph/` 目录。以下是各文件的作用及建议操作：

| 文件 | 是否自动生成？ | 建议操作 |
|------|-----------------|---------------|
| `.ralph/PROMPT.md` | 是（智能默认值） | **审查并自定义**项目目标与原则 |
| `.ralph/fix_plan.md` | 是（可导入任务） | **添加/修改**具体实施任务 |
| `.ralph/AGENT.md` | 是（自动检测构建命令） | 极少需要编辑（由 Ralph 自动维护） |
| `.ralph/specs/` | 空目录 | 当 PROMPT.md 不够详细时添加文件 |
| `.ralph/specs/stdlib/` | 空目录 | 添加可复用的模式与规范 |
| `.ralphrc` | 是（感知项目环境） | 极少需要编辑（默认值已足够合理） |

### 关键文件关联关系

```
PROMPT.md (高层目标)
    ↓
specs/ (详细需求，按需使用)
    ↓
fix_plan.md (Ralph 执行的具体任务)
    ↓
AGENT.md (构建/测试命令 - 自动维护)
```

### 何时使用 specs/
- **简单项目**：通常只需 PROMPT.md + fix_plan.md
- **复杂功能**：添加 `specs/feature-name.md` 以提供详细需求
- **团队规范**：添加 `specs/stdlib/convention-name.md` 定义可复用模式

详见 [用户指南](docs/user-guide/) 与 [examples/](examples/) 目录中的实际项目配置示例。

## 工作原理

Ralph 基于一个简单但强大的循环机制运行：

1. **读取指令** - 加载包含你项目需求的 `PROMPT.md`
2. **执行 Claude Code** - 在当前上下文与优先级下运行 Claude Code
3. **追踪进度** - 更新任务列表并记录执行结果
4. **评估完成状态** - 检查退出条件与项目完成信号
5. **循环继续** - 持续执行直至项目完成或达到限制

### 智能退出检测

Ralph 采用**双条件检查机制**，防止在高效迭代期间过早退出：

**退出需同时满足两个条件：**
1. `completion_indicators >= 2`（基于自然语言模式的启发式检测）
2. Claude 在 RALPH_STATUS 块中显式输出 `EXIT_SIGNAL: true`

**示例行为：**
```
Loop 5: Claude 输出 "Phase complete, moving to next feature"
        → completion_indicators: 3 (模式匹配置信度高)
        → EXIT_SIGNAL: false (Claude 表示仍需工作)
        → 结果：CONTINUE（尊重 Claude 的显式意图）

Loop 8: Claude 输出 "All tasks complete, project ready"
        → completion_indicators: 4
        → EXIT_SIGNAL: true (Claude 确认完成)
        → 结果：EXIT with "project_complete"
```

**其他退出条件：**
- `.ralph/fix_plan.md` 中所有任务标记为已完成
- Claude Code 连续多次输出 "done" 信号
- 测试类循环过多（表明功能已完备）
- Claude API 5 小时使用限制达到（提示用户等待或退出）

## 在现有项目中启用 Ralph

`ralph-enable` 命令提供交互式向导，用于向现有项目添加 Ralph：

```bash
cd my-existing-project
ralph-enable
```

**向导流程：**
1. **检测环境** - 识别项目类型（TypeScript、Python 等）及框架
2. **选择任务源** - 从 beads、GitHub Issues 或 PRD 文档中选择
3. **配置设置** - 设置工具权限与循环参数
4. **生成文件** - 创建 `.ralph/` 目录与 `.ralphrc` 配置文件
5. **验证安装** - 确认所有文件已正确创建

**非交互模式（适用于 CI/自动化）：**
```bash
ralph-enable-ci                              # 使用合理默认值
ralph-enable-ci --from github               # 从 GitHub Issues 导入
ralph-enable-ci --project-type typescript   # 覆盖自动检测类型
ralph-enable-ci --json                      # 机器可读输出格式
```

## 导入现有需求

Ralph 可利用 Claude Code 将现有的 PRD、规范或需求文档转换为标准的 Ralph 格式。

### 支持的格式
- **Markdown** (.md) - 产品需求、技术规范
- **文本文件** (.txt) - 纯文本需求
- **JSON** (.json) - 结构化需求数据
- **Word 文档** (.docx) - 业务需求
- **PDFs** (.pdf) - 设计文档、规范说明
- **任意基于文本的格式** - Ralph 将智能解析内容

### 使用示例

```bash
# 转换 Markdown PRD
ralph-import product-requirements.md my-app

# 转换文本规范
ralph-import requirements.txt webapp

# 转换 JSON API 规范
ralph-import api-spec.json backend-service

# 让 Ralph 自动根据文件名命名项目
ralph-import design-doc.pdf
```

### 生成内容说明

Ralph-import 会创建完整的项目结构，包含：

- **.ralph/PROMPT.md** - 转换为 Ralph 开发指令
- **.ralph/fix_plan.md** - 将需求拆解为优先级任务列表
- **.ralph/specs/requirements.md** - 从文档中提取的技术规范
- **.ralphrc** - 包含工具权限的项目配置文件
- **标准 Ralph 结构** - `.ralph/` 下的所有必要目录与模板文件

转换过程具备智能性，在保留你原始需求的同时使其可被自主开发流程直接执行。

## 配置管理

### 项目配置 (.ralphrc)

每个 Ralph 项目均可拥有独立的 `.ralphrc` 配置文件：

```bash
# .ralphrc - Ralph 项目配置
PROJECT_NAME="my-project"
PROJECT_TYPE="typescript"

# Claude Code CLI 命令（自动检测，如需覆盖请取消注释）
CLAUDE_CODE_CMD="claude"
# CLAUDE_CODE_CMD="npx @anthropic-ai/claude-code"  # 备选：使用 npx

# Shell init 文件 — 在运行 claude 前 source（适用于 zsh/fish 用户，
# 其 PATH 或环境变量仅在 shell 的初始化文件中设置）
#RALPH_SHELL_INIT_FILE="~/.zshrc"

# 循环设置
MAX_CALLS_PER_HOUR=100
CLAUDE_TIMEOUT_MINUTES=15
CLAUDE_OUTPUT_FORMAT="json"
# 每小时 Token 预算（0 = 禁用）。单次 Claude 调用可能消耗 100k+ tokens。
#MAX_TOKENS_PER_HOUR=500000

# 工具权限
ALLOWED_TOOLS="Write,Read,Edit,Bash(git *),Bash(npm *),Bash(pytest)"

# 会话管理
SESSION_CONTINUITY=true
SESSION_EXPIRY_HOURS=24

# 熔断器阈值
CB_NO_PROGRESS_THRESHOLD=3
CB_SAME_ERROR_THRESHOLD=5
```

### 速率限制与熔断器

Ralph 内置智能速率限制与熔断器功能：

```bash
# 默认：每小时 100 次调用
ralph --calls 50

# 配合集成监控使用
ralph --monitor --calls 50

# 查看当前使用情况（显示本小时已用调用次数与 Token）
ralph --status
```

速率限制支持两个独立限额 — 均按小时重置：

| 设置项 | 默认值 | 说明 |
|---------|---------|-------------|
| `MAX_CALLS_PER_HOUR` | `100` | 每小时最大 Claude 调用次数 |
| `MAX_TOKENS_PER_HOUR` | `0`（已禁用） | 每小时累计最大 Token 数 |

Token 追踪会从每次 Claude 响应中提取 `input_tokens + output_tokens`。单次调用可能消耗 100k+ tokens，因此 `MAX_TOKENS_PER_HOUR` 提供了仅靠 `MAX_CALLS_PER_HOUR` 无法实现的成本管控能力。

熔断器会自动：
- 使用高级两级过滤检测 API 错误与速率限制问题
- 在连续 3 次循环无进展或 5 次循环出现相同错误时触发（OPEN）
- 消除包含 "error" 字段的 JSON 误报
- 通过多行错误匹配精准检测卡死循环
- 以半开状态（HALF_OPEN）逐步恢复
- **冷却期后自动恢复**（默认：30 分钟）— OPEN → HALF_OPEN → CLOSED
- 提供详细的错误追踪与带状态历史的日志记录

**自动恢复选项：**
```bash
# 默认：等待 30 分钟后尝试自动恢复
CB_COOLDOWN_MINUTES=30     # 在 .ralphrc 中设置（0 = 立即执行）

# 启动时自动重置（适用于完全无人值守运行）
ralph --auto-reset-circuit
# 或在 .ralphrc 中设置：CB_AUTO_RESET=true
```

### Claude 5 小时 API 使用限制

当达到 Claude 的 5 小时用量上限时，Ralph 会：
1. 通过三层验证机制检测限制（超时守卫 → 结构化 JSON → 过滤文本降级）
2. 提示你选择操作：
   - **选项 1**：等待 60 分钟让限制重置（带倒计时器）
   - **选项 2**：优雅退出
3. **无人值守模式**：在提示超时（30秒）后自动等待，而非直接退出
4. 防止因回显文件内容提及 "5-hour limit" 导致的误报

### 自定义提示词

```bash
# 使用自定义提示词文件
ralph --prompt my_custom_instructions.md

# 配合集成监控使用
ralph --monitor --prompt my_custom_instructions.md
```

### 执行超时设置

```bash
# 设置 Claude Code 执行超时时间（默认：15 分钟）
ralph --timeout 30  # 复杂任务设置为 30 分钟超时

# 配合监控与自定义超时使用
ralph --monitor --timeout 60  # 60 分钟超时

# 快速迭代设置短超时
ralph --verbose --timeout 5  # 5 分钟超时并显示进度
```

### 详细模式（Verbose Mode）

```bash
# 启用执行期间的详细进度更新
ralph --verbose

# 与其他选项组合使用
ralph --monitor --verbose --timeout 30
```

### 实时流式输出

```bash
# 启用 Claude Code 执行的实时可见性
ralph --live

# 配合监控获得最佳体验
ralph --monitor --live

# 实时输出将写入 .ralph/live.log
tail -f .ralph/live.log  # 在另一终端中查看
```

流式模式会在 Claude Code 工作时实时显示其输出，让你直观了解每次循环迭代中的实际进展。

### 会话连续性

Ralph 跨循环迭代维持会话上下文，以提升连贯性：

```bash
# 默认启用会话连续性（通过 --continue 标志）
ralph --monitor                 # 使用会话连续性

# 从头开始，不保留会话上下文
ralph --no-continue             # 孤立执行各次循环

# 手动重置会话（清除上下文）
ralph --reset-session           # 清空当前会话

# 查看会话状态
cat .ralph/.ralph_session              # 查看当前会话文件
cat .ralph/.ralph_session_history      # 查看会话切换历史
```

**会话自动重置触发条件：**
- 熔断器触发（检测到停滞）
- 手动中断（Ctrl+C / SIGINT）
- 项目完成（优雅退出）
- 手动重置熔断器（`--reset-circuit`）
- 会话过期（默认：24 小时）

会话状态持久化至 `.ralph/.ralph_session`，支持可配置过期时间（默认：24 小时）。最近 50 次会话切换记录将写入 `.ralph/.ralph_session_history` 供调试使用。

### 退出阈值

可在 `~/.ralph/ralph_loop.sh` 中修改以下变量：

**退出检测阈值：**
```bash
MAX_CONSECUTIVE_TEST_LOOPS=3     # 连续 3 次纯测试循环后退出
MAX_CONSECUTIVE_DONE_SIGNALS=2   # 连续 2 个 "done" 信号后退出
TEST_PERCENTAGE_THRESHOLD=30     # 若超过 30% 的循环为纯测试则标记警告
```

**熔断器阈值：**
```bash
CB_NO_PROGRESS_THRESHOLD=3       # 连续 3 次无文件变更后触发 OPEN
CB_SAME_ERROR_THRESHOLD=5        # 连续 5 次重复错误后触发 OPEN
CB_OUTPUT_DECLINE_THRESHOLD=70   # 输出质量下降超过 70% 时触发 OPEN
CB_COOLDOWN_MINUTES=30           # OPEN → HALF_OPEN 自动恢复前的冷却分钟数
CB_AUTO_RESET=false              # true = 启动时重置为 CLOSED（跳过冷却期）
```

**完成指标与 EXIT_SIGNAL 门控逻辑：**

| completion_indicators | EXIT_SIGNAL | 结果 |
|-----------------------|-------------|--------|
| >= 2 | `true` | **退出** ("project_complete") |
| >= 2 | `false` | **继续** (Claude 仍在工作中) |
| >= 2 | missing | **继续** (默认视为 false) |
| < 2 | `true` | **继续** (未达阈值要求) |

## 项目结构

Ralph 为每个项目创建标准化目录结构，配置信息存放于 `.ralph/` 子文件夹中：

```
my-project/
├── .ralph/                 # Ralph 配置与状态（隐藏文件夹）
│   ├── PROMPT.md           # Ralph 的主要开发指令
│   ├── fix_plan.md        # 优先级任务列表
│   ├── AGENT.md           # 构建与运行说明
│   ├── specs/              # 项目规范与需求
│   │   └── stdlib/         # 标准库规范
│   ├── examples/           # 使用示例与测试用例
│   ├── logs/               # Ralph 执行日志
│   └── docs/generated/     # 自动生成文档
├── .ralphrc                # Ralph 配置文件（工具权限、设置）
└── src/                    # 源代码实现（位于项目根目录）
```

> **迁移说明**：若你拥有使用旧扁平结构的现有 Ralph 项目，请运行 `ralph-migrate` 自动将文件迁移至 `.ralph/` 子文件夹。

## 最佳实践

### 编写高效提示词（Prompts）
1. **明确具体** - 清晰的需求能带来更好的结果
2. **设定优先级** - 使用 `.ralph/fix_plan.md` 引导 Ralph 的关注重点
3. **划定边界** - 明确定义范围与排除项
4. **提供示例** - 展示预期的输入/输出格式

### 项目规范建议
- 将详细需求放置于 `.ralph/specs/`
- 使用 `.ralph/fix_plan.md` 进行优先级任务追踪
- 保持 `.ralph/AGENT.md` 与构建说明同步更新
- 记录关键决策与架构设计

### 进度监控指南
- 使用 `ralph-monitor` 获取实时状态更新
- 查看 `.ralph/logs/` 中的日志以获取详细执行历史
- 监控 `.ralph/status.json` 实现程序化访问
- 留意退出条件信号

## 系统要求

- **Bash 4.0+** - 用于脚本执行
- **Claude Code CLI** - `npm install -g @anthropic-ai/claude-code`（或使用 npx — 在 `.ralphrc` 中设置 `CLAUDE_CODE_CMD`）
- **tmux** - 终端复用器，用于集成监控（推荐）
- **jq** - JSON 处理工具，用于状态追踪
- **Git** - 版本控制（项目初始化为 git 仓库）
- **GNU coreutils** - 提供 `timeout` 命令（执行超时功能）
  - Linux：大多数发行版预装
  - macOS：通过 `brew install coreutils` 安装（提供 `gtimeout`）
- **标准 Unix 工具** - grep、date 等

### 测试要求（开发环境）

详见 [TESTING.md](TESTING.md) 获取完整测试指南。

若需运行测试套件：

```bash
# 安装 BATS 测试框架
npm install -g bats bats-support bats-assert

# 运行单元 + 集成测试（771 项测试）
npm test

# 运行端到端测试（13 项；完整 ralph_loop.sh 子进程执行）
npm run test:e2e

# 运行特定测试套件
bats tests/unit/test_rate_limiting.bats
bats tests/unit/test_exit_detection.bats
bats tests/unit/test_json_parsing.bats
bats tests/unit/test_cli_modern.bats
bats tests/unit/test_cli_parsing.bats
bats tests/unit/test_session_continuity.bats
bats tests/unit/test_enable_core.bats
bats tests/unit/test_task_sources.bats
bats tests/unit/test_ralph_enable.bats
bats tests/unit/test_wizard_utils.bats
bats tests/unit/test_circuit_breaker_recovery.bats
bats tests/integration/test_loop_execution.bats
bats tests/integration/test_prd_import.bats
bats tests/integration/test_project_setup.bats
bats tests/integration/test_installation.bats

# 运行错误检测与熔断器测试
./tests/test_error_detection.sh
./tests/test_stuck_loop_detection.sh
```

当前测试状态：
- **784 项测试**，覆盖 34 个测试文件
- **100% 通过率**（784/784 通过）
- 全面的单元、集成与端到端测试
- 针对 JSON 解析、CLI 标志、熔断器、EXIT_SIGNAL 行为、启用向导及安装工作流的专项测试
- 真正的 E2E 套件以子进程形式运行 ralph_loop.sh，对接模拟 Claude CLI（`tests/e2e/`）

> **覆盖率说明**：使用 kcov 测量 Bash 代码覆盖率在追踪子进程执行时存在根本性限制。测试通过率（100%）即为质量门禁标准。详见 [bats-core#15](https://github.com/bats-core/bats-core/issues/15)。

### 安装 tmux

```bash
# Ubuntu/Debian
sudo apt-get install tmux

# macOS
brew install tmux

# CentOS/RHEL
sudo yum install tmux
```

### 安装 GNU coreutils (macOS)

Ralph 使用 `timeout` 命令实现执行超时。在 macOS 上，你需要安装 GNU coreutils：

```bash
# 安装 coreutils（提供 gtimeout）
brew install coreutils

# 验证安装
gtimeout --version
```

Ralph 会自动检测并使用 macOS 上的 `gtimeout`。安装后无需额外配置。

## 监控与调试

### 实时仪表盘

```bash
# 集成 tmux 监控（推荐）
ralph --monitor

# 在独立终端中手动监控
ralph-monitor
```

实时显示：
- 当前循环计数与状态
- API 调用使用情况 vs. 限额
- 最近日志条目
- 速率限制倒计时

**tmux 控制键：**
- `Ctrl+B` 然后按 `D` - 分离会话（Ralph 继续运行）
- `Ctrl+B` 然后按 `←/→` - 切换面板
- `tmux list-sessions` - 查看活跃会话
- `tmux attach -t <session-name>` - 重新附加至会话

### 状态检查

```bash
# JSON 格式输出状态
ralph --status

# 手动检查日志
tail -f .ralph/logs/ralph.log
```

### 常见问题排查

- **Ralph 在首次循环时静默退出** - Claude Code CLI 可能未安装或不在 PATH 中。Ralph 会在启动时验证命令并显示安装指引。若使用 npx，请在 `.ralphrc` 中添加 `CLAUDE_CODE_CMD="npx @anthropic-ai/claude-code"`
- **速率限制** - Ralph 会自动等待并显示倒计时
- **5 小时 API 限制** - Ralph 会检测并提示用户操作（等待或退出）
- **卡死循环** - 检查 `fix_plan.md` 中是否存在模糊或冲突的任务
- **过早退出** - 若 Ralph 停止过早，请审查退出阈值设置
- **提前退出** - 检查 Claude 是否设置了 `EXIT_SIGNAL: false`（Ralph 现已尊重此设置）
- **执行超时** - 复杂操作请增加 `--timeout` 数值
- **依赖缺失** - 确保已安装 Claude Code CLI 与 tmux
- **tmux 会话丢失** - 使用 `tmux list-sessions` 和 `tmux attach` 重新连接
- **会话过期** - 默认 24 小时后会话失效；使用 `--reset-session` 重新开始
- **timeout: command not found (macOS)** - 安装 GNU coreutils：`brew install coreutils`
- **权限拒绝（Permission Denied）** - 当 Claude Code 被拒绝执行命令时，Ralph 会暂停：
  1. 编辑 `.ralphrc` 并更新 `ALLOWED_TOOLS` 以包含所需工具
  2. 常见模式：`Bash(npm *)`、`Bash(git *)`、`Bash(pytest)`
  3. 更新 `.ralphrc` 后运行 `ralph --reset-session`
  4. 使用 `ralph --monitor` 重新启动

## 贡献指南

Ralph 正在积极寻找贡献者！我们正朝着 v1.0.0 迈进，目标明确且路线图详尽。

**详见 [CONTRIBUTING.md](CONTRIBUTING.md) 获取完整贡献者指南**，内容包括：
- 入门指引与环境设置说明
- 开发工作流与提交规范
- 代码风格准则
- 测试要求（必须保持 100% 通过率）
- Pull Request 流程与代码审查规范
- 质量标准与检查清单

### 快速开始

```bash
# Fork 并克隆仓库
git clone https://github.com/YOUR_USERNAME/ralph-claude-code.git
cd ralph-claude-code

# 安装依赖并运行测试
npm install
npm test && npm run test:e2e  # 所有 784 项测试必须通过
```

### 优先贡献领域

1. **测试实现** - 协助扩展测试覆盖率
2. **功能开发** - 认领 [开放 Issue](https://github.com/frankbria/ralph-claude-code/issues)
3. **文档编写** - 教程、故障排查指南、示例项目
4. **真实场景测试** - 实际使用 Ralph，报告 Bug，分享反馈

**每一份贡献都至关重要** - 从修正拼写错误到实现核心功能！

## 许可证

本项目采用 MIT License 开源协议 - 详见 [LICENSE](LICENSE) 文件。

## 致谢

- 灵感来源于 Geoffrey Huntley 创建的 [Ralph 技术](https://ghuntley.com/ralph/)
- 专为 Anthropic 的 [Claude Code](https://claude.ai/code) 构建
- 感谢社区反馈与贡献者

## 相关项目

- [Claude Code](https://claude.ai/code) - 驱动 Ralph 运行的 AI 编程助手
- [Aider](https://github.com/paul-gauthier/aider) - Ralph 原始技术的初始实现版本

---

## 命令参考

### 安装命令（仅需运行一次）
```bash
./install.sh              # 全局安装 Ralph
./uninstall.sh            # 从系统移除 Ralph（专用脚本）
./install.sh uninstall    # 备选：从系统移除 Ralph
./install.sh --help       # 显示安装帮助信息
ralph-migrate             # 将现有项目迁移至 .ralph/ 结构
```

### Ralph 循环选项
```bash
ralph [OPTIONS]
  -h, --help              Show help message
  -c, --calls NUM         Set max calls per hour (default: 100)
  -p, --prompt FILE       Set prompt file (default: .ralph/PROMPT.md)
  -s, --status            Show current status and exit
  -m, --monitor           Start with tmux session and live monitor
  -v, --verbose           Show detailed progress updates during execution
  -l, --live              Enable live streaming output (real-time Claude Code visibility)
  -t, --timeout MIN       Set Claude Code execution timeout in minutes (1-120, default: 15)
  --dry-run               Simulate loop execution without making actual Claude API calls
  -n, --notify            Enable desktop notifications for key events
  -b, --backup            Enable automatic git backup branch before each loop (requires git)
  --rollback [BRANCH]     Roll back to a backup branch (lists available branches if none given)
  --show-tool-args        Show tool arguments (commands, file paths) in live streaming output
  --output-format FORMAT  Set output format: json (default) or text
  --allowed-tools TOOLS   Set allowed Claude tools (default: granular git subcommands + npm/pytest)
  --no-continue           Disable session continuity (start fresh each loop)
  --session-expiry HOURS  Set session expiration time in hours (default: 24)
  --reset-circuit         Reset the circuit breaker
  --circuit-status        Show circuit breaker status
  --auto-reset-circuit    Auto-reset circuit breaker on startup (bypasses cooldown)
  --reset-session         Reset session state manually
```

> **完整参考**：每个标志均附有详细文档、使用示例及 `.ralphrc` 配置模式，详见 [docs/CLI_OPTIONS.md](docs/CLI_OPTIONS.md)。

### 项目命令（按项目进行）
```bash
ralph-setup project-name     # 创建新 Ralph 项目
ralph-enable                 # 在现有项目中启用 Ralph（交互式）
ralph-enable-ci              # 在现有项目中启用 Ralph（非交互模式）
ralph-import prd.md project  # 将 PRD/规范转换为 Ralph 项目格式
ralph --monitor              # 启动集成监控
ralph --status               # 检查当前循环状态
ralph --verbose              # 启用详细进度更新
ralph --timeout 30           # 设置 30 分钟执行超时
ralph --calls 50             # 限制每小时最多 50 次 API 调用
ralph --reset-session        # 手动重置会话状态
ralph --live                 # 启用实时流式输出
ralph --dry-run              # 模拟循环而不实际调用 API
ralph --notify               # 关键事件桌面通知
ralph --backup               # 每次循环前自动创建 Git 备份分支
ralph-stats                  # 汇总 .ralph/logs/metrics.jsonl 中的指标数据
ralph-monitor                # 手动监控仪表盘
```

### tmux 会话管理
```bash
tmux list-sessions        # 查看活跃的 Ralph 会话
tmux attach -t <name>     # 重新附加至已分离的会话
# Ctrl+B then D           # 分离会话（保持后台运行）
```

---

## 开发路线图

Ralph 处于活跃开发阶段，具备清晰的 v1.0.0 演进路径。详见 [IMPLEMENTATION_PLAN.md](IMPLEMENTATION_PLAN.md) 获取完整路线图。

### 当前状态：v0.11.5

**已交付功能：**
- 核心循环功能与智能退出检测
- **双条件退出门控（完成指标 + EXIT_SIGNAL）**
- 速率限制（100 次调用/小时）与熔断器模式
- 支持语义理解的响应分析器
- **784 项全面测试**（100% 通过率）
- **实时流式输出模式**，直观查看 Claude Code 运行状态
- **日志轮转、干跑模式、指标追踪（`ralph-stats`）、桌面通知及 Git 备份/回滚功能**
- tmux 集成与实时监控
- PRD 导入功能与现代 CLI JSON 解析支持
- 安装系统与项目模板
- 现代 CLI 命令与 JSON 输出支持
- CI/CD 流水线（GitHub Actions）
- **交互式 `ralph-enable` 向导（适用于现有项目）**
- **`.ralphrc` 配置文件支持**
- 会话生命周期管理与自动重置触发机制
- 可配置超时的会话过期功能
- 专用卸载脚本

**测试覆盖：**
- **34 个测试文件共 784 项测试** — 单元、集成与端到端（100% 通过率）
- 详见 [TESTING.md](TESTING.md) 获取各套件明细及运行方式

### v1.0.0 演进路径

**已完成里程碑**：安装/设置工作流测试、tmux 集成测试、监控仪表盘测试、端到端全循环测试、日志轮转、干跑模式、指标追踪（`ralph-stats`）、桌面通知及 Git 备份/回滚。

**剩余事项**
- 最终文档梳理与发布准备
- CI 工作流供应链加固 ([#275](https://github.com/frankbria/ralph-claude-code/issues/275))
- 基于 [开放 Issue](https://github.com/frankbria/ralph-claude-code/issues) 积压项的真实场景反馈收集

详见 [IMPLEMENTATION_STATUS.md](IMPLEMENTATION_STATUS.md) 获取详细进度追踪。

### 如何贡献
Ralph 正在寻找贡献者！详见 [CONTRIBUTING.md](CONTRIBUTING.md) 获取完整指南。优先领域：
1. **测试实现** - 协助扩展测试覆盖率（[查看计划](IMPLEMENTATION_PLAN.md)）
2. **功能开发** - 认领 [开放 Issue](https://github.com/frankbria/ralph-claude-code/issues)
3. **文档编写** - 使用示例、教程、故障排查指南
4. **Bug 报告** - 真实场景使用反馈与边界案例

---

**准备好让 AI 构建你的项目了吗？** 运行 `./install.sh`，交由 Ralph 接管后续流程！

## ⭐ Star 历史

[![Star History Chart](https://api.star-history.com/svg?repos=frankbria/ralph-claude-code&type=date&legend=top-left)](https://www.star-history.com/#frankbria/ralph-claude-code&type=date&legend=top-left)
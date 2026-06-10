<div align="center">

# NotebookLM Claude Code Skill

**让 [Claude Code](https://github.com/anthropics/claude-code) 直接与 NotebookLM 对话，仅基于你上传的文档提供有来源依据的答案**

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![Claude Code Skill](https://img.shields.io/badge/Claude%20Code-Skill-purple.svg)](https://www.anthropic.com/news/skills)
[![Based on](https://img.shields.io/badge/Based%20on-NotebookLM%20MCP-green.svg)](https://github.com/PleasePrompto/notebooklm-mcp)
[![GitHub](https://img.shields.io/github/stars/PleasePrompto/notebooklm-skill?style=social)](https://github.com/PleasePrompto/notebooklm-skill)

> 使用此技能直接从 Claude Code 查询你的 Google NotebookLM 笔记本库，获取由 Gemini 提供的、有据可查且附带引用的答案。支持浏览器自动化（Browser Automation）、库管理和持久化认证。大幅减少幻觉——答案仅源自你上传的文档。

[安装](#installation) • [快速入门](#quick-start) • [为何选择 NotebookLM](#why-notebooklm-not-local-rag) • [工作原理](#how-it-works) • [MCP 替代方案](https://github.com/PleasePrompto/notebooklm-mcp)

</div>

---

## ⚠️ 重要提示：仅限本地 Claude Code

**此技能仅适用于本地安装的 [Claude Code](https://github.com/anthropics/claude-code)，不适用于网页版 UI。**

网页版 UI 在沙盒中运行技能，且无网络访问权限，而本技能需要联网进行浏览器自动化。你必须在本地机器上使用 [Claude Code](https://github.com/anthropics/claude-code)。

---

## 痛点问题

当你告诉 [Claude Code](https://github.com/anthropics/claude-code) “搜索我的本地文档”时，会发生以下情况：
- **大量消耗 Token**：搜索文档意味着反复读取多个文件
- **检索不准确**：仅进行关键词匹配，会遗漏上下文及文档间的关联
- **产生幻觉**：找不到内容时，它会编造听起来合理的 API 或代码
- **手动复制粘贴**：不断在 NotebookLM 浏览器和编辑器之间切换

## 解决方案

这个 Claude Code 技能让 [Claude Code](https://github.com/anthropics/claude-code) 能够直接与 [**NotebookLM**](https://notebooklm.google/) —— Google 基于 Gemini 2.5 打造的**有来源依据的知识库**——进行对话，从而仅从你上传的文档中生成智能、综合的答案。

```
你的任务 → Claude 向 NotebookLM 提问 → Gemini 综合答案 → Claude 编写正确代码
```

**告别繁琐的复制粘贴流程**：Claude 直接提问并直接在 CLI 中接收答案。它通过自动追问建立深度理解，获取具体的实现细节、边界情况和最佳实践。

---

## 为何选择 NotebookLM，而非本地 RAG？

| 方案 | Token 消耗 | 配置时间 | 幻觉情况 | 答案质量 |
|----------|------------|------------|----------------|----------------|
| **直接喂文档给 Claude** | 🔴 极高（反复读取多文件） | 即时 | 有 - 会自行填补空白 | 检索效果不稳定 |
| **网页搜索** | 🟡 中等 | 即时 | 高 - 来源不可靠 | 时好时坏 |
| **本地 RAG** | 🟡 中高 | 数小时（需配置嵌入、分块） | 中等 - 存在检索盲区 | 高度依赖配置 |
| **NotebookLM Skill** | 🟢 极低 | 5 分钟 | **极低** - 仅基于来源依据 | 专家级综合解答 |

### NotebookLM 的优势何在？

1. **Gemini 预处理**：上传一次文档，即可瞬间获取专家级知识
2. **自然语言问答（Natural language Q&A）**：不仅是检索——而是真正的理解与综合
3. **多源关联分析**：跨 50+ 份文档连接信息
4. **附带引用来源**：每个答案均包含参考文献指引
5. **无需基础设施**：无需向量数据库、嵌入模型或分块策略

---

## 安装

### 史上最简单的安装方式：

```bash
# 1. 创建技能目录（若不存在）
mkdir -p ~/.claude/skills

# 2. 克隆此仓库
cd ~/.claude/skills
git clone https://github.com/PleasePrompto/notebooklm-skill notebooklm

# 3. 完成！打开 Claude Code 并输入：
"What are my skills?"
```

首次使用时，它会自动执行以下操作：
- 创建隔离的 Python 环境 (`.venv`)
- 安装所有依赖项，包括 **Google Chrome**
- 使用 Chrome（而非 Chromium）设置浏览器自动化以确保最高可靠性
- 所有内容均保留在技能文件夹内

**注意：** 配置采用真实 Chrome 而非 Chromium，以实现跨平台兼容性、一致的浏览器指纹特征以及针对 Google 服务更好的反检测能力。

---

## 快速入门

### 1. 检查你的技能

在 Claude Code 中输入：
```
"What skills do I have?"
```

Claude 将列出你可用的技能，其中包括 NotebookLM。

### 2. 进行 Google 认证（一次性）

```
"Set up NotebookLM authentication"
```
*打开一个 Chrome 窗口 → 使用你的 Google 账号登录*

### 3. 创建知识库

前往 [notebooklm.google.com](https://notebooklm.google.com) → 创建笔记本 (Create notebook) → 上传你的文档：
- 📄 PDF、Google Docs、markdown 文件
- 🔗 网站链接、GitHub 仓库
- 🎥 YouTube 视频
- 📚 每个笔记本可添加多个来源

分享设置：**⚙️ Share → Anyone with link → Copy**（复制链接）

### 4. 添加到你的库中

**选项 A：让 Claude 自动识别（智能添加）**
```
"Query this notebook about its content and add it to my library: [your-link]"
```
Claude 将自动查询笔记本以发现其内容，然后使用适当的元数据将其添加。

**选项 B：手动添加**
```
"Add this NotebookLM to my library: [your-link]"
```
Claude 会询问名称和主题标签，随后保存以供日后使用。

### 5. 开始研究

```
"What does my React docs say about hooks?"
```

Claude 会自动选择正确的笔记本并直接从 NotebookLM 获取答案。

---

## 工作原理

这是一个 **Claude Code Skill**——一个包含指令和脚本的本地文件夹，供 Claude Code 在需要时调用。与 [MCP Server 版本](https://github.com/PleasePrompto/notebooklm-mcp)不同，它直接在 Claude Code 中运行，无需额外的服务器。

### 与 MCP Server 的主要区别

| 特性 | 本技能 (Skill) | MCP Server |
|---------|------------|------------|
| **协议** | Claude Skills | Model Context Protocol (MCP) |
| **安装方式** | 克隆至 `~/.claude/skills` | `claude mcp add ...` |
| **会话模式** | 每次提问打开全新浏览器 | 持久化聊天会话 |
| **兼容性** | 仅限 Claude Code（本地） | Claude Code、Codex、Cursor 等 |
| **开发语言** | Python | TypeScript |
| **分发方式** | Git clone | npm package |

### 架构结构

```
~/.claude/skills/notebooklm/
├── SKILL.md              # 给 Claude 的指令说明
├── scripts/              # Python 自动化脚本
│   ├── ask_question.py   # 查询 NotebookLM
│   ├── notebook_manager.py # 库管理功能
│   └── auth_manager.py   # Google 认证管理
├── .venv/                # 隔离的 Python 环境（自动创建）
└── data/                 # 本地笔记本库数据
```

当你提及 NotebookLM 或发送笔记本链接时，Claude 会：
1. 加载技能指令说明
2. 运行相应的 Python 脚本
3. 打开浏览器并提出你的问题
4. 将答案直接返回给你
5. 利用该知识协助你完成任务

---

## 核心功能

### **基于来源的回复**
NotebookLM 通过仅根据你上传的文档回答问题来显著减少幻觉。如果找不到相关信息，它会表明不确定性而非编造内容。

### **直接集成**
无需在浏览器和编辑器之间复制粘贴。Claude 通过编程方式提问并接收答案。

### **智能库管理**
保存带有标签和描述的 NotebookLM 链接。Claude 会自动为你的任务选择正确的笔记本。

### **自动认证**
一次性 Google 登录，之后跨会话保持认证状态。

### **完全独立运行**
所有内容均在技能文件夹内与隔离的 Python 环境中运行。无需全局安装。

### **拟人化自动化**
采用真实的打字速度和交互模式，避免被检测为机器人操作。

---

## 常用指令

| 你输入的内容 | 执行的操作 |
|--------------|--------------|
| *"Set up NotebookLM authentication"* | 打开 Chrome 进行 Google 登录 |
| *"Add [link] to my NotebookLM library"* | 保存笔记本及元数据 |
| *"Show my NotebookLM notebooks"* | 列出所有已保存的笔记本 |
| *"Ask my API docs about [topic]"* | 查询相关笔记本 |
| *"Use the React notebook"* | 设置当前活动笔记本 |
| *"Clear NotebookLM data"* | 重置状态（保留库数据） |

---

## 实际案例

### 示例 1：维修手册查询

**用户提问**：“查看我的铃木 GSR 600 维修手册，查找刹车油类型、发动机机油规格和后轴扭矩。”

**Claude 自动执行：**
- 完成 NotebookLM 认证
- 针对各项参数提出全面问题
- 当提示“还需要了解其他信息吗？”时进行追问
- 提供准确参数：DOT 4 刹车油、SAE 10W-40 机油、后轴扭矩 100 N·m

![NotebookLM Chat Example](images/example_notebookchat.png)

### 示例 2：无幻觉构建工作流

**你**：“我需要为 Gmail 垃圾邮件过滤构建一个 n8n 工作流。使用我的 n8n 笔记本。”

**Claude 的内部流程：**
```
→ 加载 NotebookLM 技能
→ 激活 n8n 笔记本
→ 提出全面问题并进行追问
→ 综合多次查询结果生成完整答案
```

**结果**：首次尝试即可生成可用工作流，无需调试幻觉产生的 API。

---

## 技术细节

### 核心技术
- **Patchright**：基于 Playwright 的浏览器自动化库
- **Python**：本技能的实现语言
- **反检测技术**：拟人化的打字速度和交互模式

注：MCP Server 使用相同的 Patchright 库，但通过 TypeScript/npm 生态实现。

### 依赖项
- **patchright==1.55.2**：浏览器自动化
- **python-dotenv==1.0.0**：环境变量配置
首次使用时自动安装至 `.venv`

### 数据存储

所有数据均本地存储于技能目录内：

```
~/.claude/skills/notebooklm/data/
├── library.json       - 你的笔记本库及元数据
├── auth_info.json     - 认证状态信息
└── browser_state/     - 浏览器 Cookie 与会话数据
```

**重要安全提示：**
- `data/` 目录包含敏感的认证数据和私人笔记本
已通过 `.gitignore` 自动排除在 Git 版本控制之外
- **切勿**手动提交或分享 `data/` 目录的内容

### 会话模型

与 MCP Server 不同，本技能采用**无状态模型**：
- 每次提问都会打开全新的浏览器窗口
- 提出问题并获取答案
- 附加一个追问提示，鼓励 Claude 提出更多问题
- 立即关闭浏览器

这意味着：
- 无持久化的聊天上下文
- 每次提问相互独立
- 但你的笔记本库会持续保存
- **追问机制**：每个答案末尾均包含“还需要了解其他信息吗？”，以提示 Claude 进行全面的后续提问

对于多步骤研究，Claude 会在需要时自动提出追问。

---

## 限制说明

### 技能相关限制
- **仅限本地 Claude Code** —— 在网页版 UI 中无法使用（沙盒限制）
- **无会话持久化** —— 每次提问相互独立
- **无追问上下文** —— 无法引用“上一个答案”

### NotebookLM 平台限制
- **频率限制** —— 免费套餐有每日查询次数限制
- **需手动上传** —— 你必须先将文档上传至 NotebookLM
- **需公开分享** —— 笔记本必须设置为链接可访问

---

## 常见问题 (FAQ)

**为何在 Claude 网页版 UI 中无法使用？**
网页版 UI 在沙盒中运行技能，且无网络访问权限。浏览器自动化需要联网才能访问 NotebookLM。

**这与 MCP Server 有什么区别？**
本技能是一个更轻量级的 Python 实现，直接作为 Claude Skill 运行。MCP Server 功能更丰富，支持持久化会话，并兼容多种工具（Codex、Cursor 等）。

**我可以同时使用此技能和 MCP Server 吗？**
可以！它们适用于不同场景。若需快速集成 Claude Code，请使用本技能；若需持久化会话或多工具支持，请选用 MCP Server。

**如果 Chrome 崩溃了怎么办？**
运行指令：`"Clear NotebookLM browser data"` 后重试即可。

**我的 Google 账号安全吗？**
Chrome 在本地机器上运行。你的凭证绝不会离开本机。如果你担心安全问题，建议使用一个专用的 Google 账号进行自动化操作。

---

## 故障排除

### 提示找不到技能
```bash
# 确认路径是否正确
ls ~/.claude/skills/notebooklm/
# 应显示：SKILL.md, scripts/, 等文件
```

### 认证问题
输入指令：`"Reset NotebookLM authentication"`

### 浏览器崩溃
输入指令：`"Clear NotebookLM browser data"`

### 依赖项异常
```bash
# 如需手动重装
cd ~/.claude/skills/notebooklm
rm -rf .venv
python -m venv .venv
source .venv/bin/activate  # Windows 用户使用 .venv\Scripts\activate
pip install -r requirements.txt
```

---

## 免责声明

本工具通过自动化浏览器交互来提升你在 NotebookLM 中的工作效率。但在此提供几点温馨提示：

**关于浏览器自动化：**
虽然我已内置拟人化功能（真实打字速度、自然延迟、鼠标轨迹）以使操作更贴近人类行为，但我无法保证 Google 不会检测或标记自动化使用。建议你为自动化操作创建一个专用的 Google 账号，而非主账号——这类似于网页爬虫：通常没问题，但谨慎起见总没错！

**关于 CLI 工具与 AI Agent：**
Claude Code、Codex 等基于 AI 的 CLI 助手功能强大，但也可能出错。请谨慎使用并保持警惕：
- 提交或部署前务必审查变更内容
- 先在安全环境中进行测试
- 定期备份重要工作成果
- 请记住：AI Agent 是辅助工具，而非全知全能的神谕

我开发此工具是因为受够了在 NotebookLM 和编辑器之间反复复制粘贴的繁琐流程。分享它是希望它也能帮到你，但我无法对可能出现的任何问题、数据丢失或账号异常承担责任。请根据你的判断自行使用。

当然，如果你遇到问题或有疑问，欢迎在 GitHub 上提交 Issue。我很乐意协助排查！

---

## 致谢

本技能灵感来源于我的 [**NotebookLM MCP Server**](https://github.com/PleasePrompto/notebooklm-mcp)，并提供了一种作为 Claude Code Skill 的替代实现方案：
- 两者均使用 Patchright 进行浏览器自动化（MCP 版为 TypeScript，Skill 版为 Python）
- Skill 版本直接在 Claude Code 中运行，无需 MCP 协议
- 无状态设计专为技能架构优化

如果你需要：
- **持久化会话** → 请使用 [MCP Server](https://github.com/PleasePrompto/notebooklm-mcp)
- **多工具支持**（Codex、Cursor）→ 请使用 [MCP Server](https://github.com/PleasePrompto/notebooklm-mcp)
- **快速 Claude Code 集成** → 请直接使用本技能

---

## 总结

**不使用此技能**：浏览器打开 NotebookLM → 复制答案 → 粘贴到 Claude → 复制下一个问题 → 返回浏览器...

**使用此技能后**：Claude 直接研究 → 瞬间获取答案 → 编写正确代码

停止繁琐的复制粘贴。直接在 Claude Code 中获取准确、有据可查的答案。

```bash
# 30 秒快速开始
cd ~/.claude/skills
git clone https://github.com/PleasePrompto/notebooklm-skill notebooklm
# 打开 Claude Code: "What are my skills?"
```

---

<div align="center">

基于我的 [NotebookLM MCP Server](https://github.com/PleasePrompto/notebooklm-mcp) 适配开发的 Claude Code Skill

专为在 Claude Code 中直接进行有来源依据的文档研究而设计

</div>
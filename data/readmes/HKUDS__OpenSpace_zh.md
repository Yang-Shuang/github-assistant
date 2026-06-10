<div align="center">

<picture>
    <img src="assets/logo.png" width="320px" style="border: none; box-shadow: none;" alt="OpenSpace Logo">
</picture>

## ✨ OpenSpace：让你的智能体更聪明、低成本、自我进化 ✨

| 🔋 **Token 使用量减少 46%** | **💰 6 小时内赚取 $11K** | 🧬 **技能自我进化** | 🌐 **智能体经验共享** |

[![Agents](https://img.shields.io/badge/Agents-Claude_Code%20%7C%20Codex%20%7C%20OpenClaw%20%7C%20nanobot%20%7C%20...-99C9BF.svg)](https://modelcontextprotocol.io/)
[![Python](https://img.shields.io/badge/Python-3.12+-FCE7D6.svg)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-C1E5F5.svg)](https://opensource.org/licenses/MIT/)
[![Feishu](https://img.shields.io/badge/Feishu-Group-E9DBFC?style=flat&logo=larksuite&logoColor=white)](./COMMUNICATION.md)
[![WeChat](https://img.shields.io/badge/WeChat-Group-C5EAB4?style=flat&logo=wechat&logoColor=white)](./COMMUNICATION.md)
[![中文文档](https://img.shields.io/badge/文档-中文版-F5C6C6?style=flat)](./README_CN.md)

**一条命令让所有 AI 智能体实现进化**：OpenClaw、nanobot、Claude Code、Codex、Cursor 等。

<img src="assets/cli-typing.gif" width="500px" alt="openspace --query your task">

</div>

---

## 📢 更新日志

- **2026-04-16** 📊 **进化候选项生命周期追踪** —— 技能库现在记录处理进化建议的时间（`evolution_processed_at`），清晰区分待处理候选项与已处理项。
- **2026-04-12** 🍎 **macOS 平台加固** —— 将 `atomacos` 与核心 macOS 导入解耦，使截图、窗口控制和录制功能可独立运行。
- **2026-04-10** 🎯 **CAPTURED（捕获）技能**现在持久化保存到宿主智能体的专属技能目录，而非默认注册表路径。云技能上传现支持正确的私有可见性设置。
- **2026-04-09** 💬 多通道**通信网关**。OpenSpace 现可接收并回复来自外部平台的消息。内置 WhatsApp（Baileys 桥接 + QR 码认证）和飞书（HTTP Webhook）适配器，支持会话管理、附件缓存及基于白名单的访问控制。详见 [`openspace/config/README.md`](openspace/config/README.md)。
- **2026-04-07** 🌐 OpenSpace MCP 现支持独立的 **SSE** 和 **streamable HTTP** 启动模式，使远程主机更易于通过 HTTP（而非 stdio）连接，从而避开受限于 stdio 的 MCP 服务器超时瓶颈。详见 [宿主集成指南](openspace/host_skills/README.md)。
- **2026-04-06** 🛠️ 修复了底层执行、MCP 服务、技能进化及持久化方面的多项运行时问题，提升了长工作流的执行稳定性与恢复能力。
- **2026-04-05** 🧭 优化了 LLM 凭据解析：集中加载 `.env`，改进宿主配置自动检测，并使原生提供商的环境变量处理更加一致。
- **2026-04-03** 🚀 发布 **v0.1.0** —— 技能质量监控：从高质量技能中提取的结构化模式现每日评估新提交内容。云搜索更快、更相关。社区内正自然涌现生产级垂直技能集群。前端现已支持中文 (zh) 国际化。
- **2026-04-02** ⚡ 云搜索升级，提升相关度并降低延迟。
- **2026-03-31** 🛡️ 安全加固：增强了对路径遍历攻击的防御（针对 zip 解压和 `import_skill`）。CLI 现遵循 `OPENSPACE_MODEL` 和 `OPENSPACE_LLM_*` 环境变量；兼容 MiniMax；修复工作流 ID 冲突问题。
- **2026-03-29** 🔒 将 `litellm` 锁定在 `<1.82.7`，以规避 PYSEC-2026-2 供应链攻击。
- **2026-03-28** 🔧 幂等技能注册 —— `register_skill_dir` 现对已注册技能返回现有的 `SkillMeta`。更新了 OpenClaw 设置文档。
- **2026-03-27** 🪟 修复了 Windows 上的 stdio 死锁问题；通过词干匹配改进了进化器确认解析。
- **2026-03-26** 🌱 每次调用时动态重新扫描技能目录，提供轻量级本地技能搜索，并精简了文档。
- **2026-03-25** 🎉 OpenSpace 现已开源！

---

## 当前 AI 智能体存在的问题

今天的 AI 智能体 —— [OpenClaw](https://github.com/openclaw/openclaw)、[nanobot](https://github.com/HKUDS/nanobot)、[Claude Code](https://docs.anthropic.com/en/docs/claude-code)、[Codex](https://github.com/openai/codex)、[Cursor](https://cursor.com) 等 —— 功能强大，但存在一个致命弱点：它们从未从真实世界中**学习**、**适应**和**进化**——更不用说彼此之间进行**共享**。
- **❌ 海量 Token 浪费** - 如何复用成功的任务模式，而不是每次从头推理并消耗大量 Token？
- **❌ 重复的高昂失败** - 如何在智能体间共享解决方案，避免重复昂贵的探索与试错？
- **❌ 技能质量差且不可靠** - 如何随着工具和 API 的演进保持技能可靠性——同时确保社区贡献的技能符合严格的质量标准？

## 🎯 OpenSpace 是什么？

**🚀 🚀 一个自我进化的引擎，让每次任务都使每个智能体变得更聪明、更省钱。**

https://github.com/user-attachments/assets/c50f70ab-f6db-47bf-9498-3210c0f0abae

OpenSpace 作为插件接入任意智能体（以技能形式），并通过三大超能力驱动其进化：

### 🧬 自我进化
自动学习并改进自身的技能
- ✅ **AUTO-FIX** —— 技能出错时，瞬间自动修复
- ✅ **AUTO-IMPROVE** —— 成功模式转化为更优的技能版本
- ✅ **AUTO-LEARN** —— 捕获实际使用中的高效工作流
- ✅ **质量监控** —— 追踪所有任务中技能的性能、错误率及执行成功率。

**持续进化的技能——将每次失败转化为改进，将每次成功转化为优化。**

### 🌐 群体智能共享
将单个智能体汇聚为共享大脑
- ✅ **共享进化**：一个智能体的提升成为所有智能体的升级
- ✅ **网络效应**：更多智能体 → 更丰富的数据 → 每个智能体进化更快
- ✅ **轻松共享** —— 一条简单命令即可上传和下载已进化的技能
- ✅ **访问控制** —— 为每项技能选择公开、私有或仅团队可见

**一个智能体学习，所有智能体受益——实现规模化群体智能。**

### 💰 Token 效率提升
更聪明的智能体，大幅降低成本
- ✅ **停止重复劳动** → 复用成功方案，而非每次从零开始
- ✅ **任务成本递减** → 随着技能优化，类似工作消耗越来越少
- ✅ **仅做微小更新** —— 修复问题所在，无需推倒重来
- ✅ **真实节省**：在真实任务中性能提升 4.2 倍，Token 使用量减少 46%，带来可衡量的经济价值（[GDPVal](#-benchmark-gdpval)）

做更多事，花更少的钱——真正为你长期省钱的智能体。

---

### 核心差异

**❌ 现有智能体**
- 技能随工具演进而无声退化
- 失败模式重复且无学习机制
- 知识困于单个智能体内

**✅ OpenSpace 赋能的智能体**
- 多层监控发现问题并自动触发修复
- 成功工作流转化为可复用、可共享的技能
- 当一个智能体学到有用知识时，所有智能体瞬间同步

### 📊 OpenSpace：将你的智能体变成赚钱的协作者

**🎯 值得关注的真实世界成果**
在涵盖 6 个行业的 50 项专业任务（**📈 [GDPVal 经济基准](#-benchmark-gdpval)**）上，OpenSpace 智能体使用相同的底层 LLM（Qwen 3.5-Plus），其收益比基线（[ClawWork](https://github.com/HKUDS/ClawWork)）智能体高出 **4.2 倍**。同时通过技能进化削减了 46% 的高昂 Token 消耗。

<div align="center">
<img src="assets/benchmark_kpi.png" width="100%" alt="GDPVal Benchmark — Key Results" />
</div>

**💼 这些均为真实业务场景**
- 根据复杂的工会合同构建薪资计算器
- 从 15 份零散 PDF 文档准备税务申报
- 起草关于加州隐私法规的法律备忘录
- 创建合规表格与工程规范

**📈 全领域持续获胜**
- 合规工作：收益提升 18.5%
- 工程项目：性能表现提升 8.7%
- 专业文档：所需 Token 减少 56%
- 所有类别均有改善，无一例外

<div align="center">
<img src="assets/benchmark_task_showcase.png" width="100%" alt="GDPVal Benchmark — Task Showcase by Category" />
</div>

**OpenSpace 不仅让智能体更聪明** —— 它让它们具备经济可行性。真实工作、真实收入、可衡量的结果。

## OpenSpace 在自主系统开发中的应用案例

**🖥️ [我的每日监控面板](showcase/README.md)** —— OpenSpace 赋能你的智能体完成大规模系统开发。这个拥有 20+ 个实时仪表板面板的个人行为监控系统完全由智能体构建——60+ 项技能从零进化而来，展示了自主端到端软件开发能力。

<div align="center">
<img src="assets/my_daily_monitor_dark.png" width="100%" alt="My Daily Monitor – Dark Mode" />
</div>

---

## 📋 目录

- [⚡ 快速开始](#-quick-start)
  - [🤖 路径 A：为你的智能体接入](#-path-a-for-your-agent)
  - [👤 路径 B：作为你的协作者直接使用](#-path-b-as-your-co-worker)
  - [📊 本地仪表盘](#-local-dashboard)
- [📈 基准测试：GDPVal](#-benchmark-gdpval)
- [📊 案例展示：我的每日监控面板](#-showcase-my-daily-monitor)
- [🏗️ 架构设计](#️-framework)
  - [🧬 自我进化引擎](#-self-evolution-engine)
  - [🌐 云技能社区](#-cloud-skill-community)
- [🔧 高级配置](#-advanced-configuration)
- [📖 代码结构](#-code-structure)
- [🔗 相关项目](#-related-projects)

---

## ⚡ 快速开始

🌐 **只想体验一下？** 前往 **[open-space.cloud](https://open-space.cloud)** 浏览社区技能与进化谱系 —— 无需安装。

```bash
git clone https://github.com/HKUDS/OpenSpace.git && cd OpenSpace
pip install -e .
openspace-mcp --help   # verify installation
```

> [!TIP]
> **克隆速度慢？** `assets/` 文件夹（约 50 MB 的图片）导致默认克隆体积较大。使用以下轻量级替代方案跳过它：
> ```bash
> git clone --filter=blob:none --sparse https://github.com/HKUDS/OpenSpace.git
> cd OpenSpace
> git sparse-checkout set --no-cone '/*' '!/assets/'
> pip install -e .
> ```

**选择你的路径：**
- **[路径 A](#-path-a-for-your-agent)** —— 为智能体接入 OpenSpace
- **[路径 B](#-path-b-as-your-co-worker)** —— 将 OpenSpace 作为 AI 协作者直接使用

### 🤖 路径 A：为你的智能体接入

适用于支持技能（`SKILL.md`）的任何智能体 —— [Claude Code](https://docs.anthropic.com/en/docs/claude-code)、[Codex](https://github.com/openai/codex)、[OpenClaw](https://github.com/openclaw/openclaw)、[nanobot](https://github.com/HKUDS/nanobot) 等。

**① 将 OpenSpace 添加到你的智能体的 MCP 配置中：**

```json
{
  "mcpServers": {
    "openspace": {
      "command": "openspace-mcp",
      "toolTimeout": 600,
      "env": {
        "OPENSPACE_HOST_SKILL_DIRS": "/path/to/your/agent/skills",
        "OPENSPACE_WORKSPACE": "/path/to/OpenSpace",
        "OPENSPACE_API_KEY": "sk-xxx (optional, for cloud)"
      }
    }
  }
}
```

> [!TIP]
> 凭据（API Key、模型）会从你的智能体配置中**自动检测**，通常无需手动设置。

> [!NOTE]
> OpenSpace 支持 3 种启动模式：
> - **stdio**：在宿主配置中保留 `command: "openspace-mcp"`。
> - **SSE**：启动 `openspace-mcp --transport sse --host 127.0.0.1 --port 8080`。
> - **streamable HTTP**：启动 `openspace-mcp --transport streamable-http --host 127.0.0.1 --port 8081`。
>
> 常用远程端点：
> - SSE 端点：`http://127.0.0.1:8080/sse`
> - streamable HTTP 端点：`http://127.0.0.1:8081/mcp`
>
> `stdio` 是最简单的选项。HTTP 模式将 OpenSpace 作为独立服务器运行，但**宿主特定的注册语法**和**宿主侧超时设置**仍然适用。

**② 将技能复制到你智能体的技能目录中：**

```bash
cp -r OpenSpace/openspace/host_skills/delegate-task/ /path/to/your/agent/skills/
cp -r OpenSpace/openspace/host_skills/skill-discovery/ /path/to/your/agent/skills/
```

完成。这两项技能会教导你的智能体何时以及如何使用 OpenSpace —— 无需额外提示词。现在你的智能体可以自我进化技能、执行复杂任务，并访问云技能社区。你也可以添加自己的自定义技能——详见 [`openspace/skills/README.md`](openspace/skills/README.md)。

> [!NOTE]
> **云社区（可选）：** 在 **[open-space.cloud](https://open-space.cloud)** 注册获取 `OPENSPACE_API_KEY`，然后添加到上方的 `env` 块中。没有它，所有本地功能（任务执行、进化、本地技能搜索）均可正常运行。

📖 各智能体配置指南（OpenClaw / nanobot）、全部环境变量及高级设置：[`openspace/host_skills/README.md`](openspace/host_skills/README.md)

### 👤 路径 B：作为你的协作者直接使用

将 OpenSpace 直接用于编程、搜索、工具调用等——内置自我进化技能与云社区。

> [!NOTE]
> 创建 `.env` 文件填入你的 LLM API Key，并可选添加 `OPENSPACE_API_KEY` 以访问云社区（参考 [`openspace/.env.example`](openspace/.env.example)）。

```bash
# Interactive mode
openspace

# Execute task
openspace --model "anthropic/claude-sonnet-4-5" --query "Create a monitoring dashboard for my Docker containers"
```

添加你的自定义技能：[`openspace/skills/README.md`](openspace/skills/README.md)。

**云 CLI** —— 通过命令行管理技能：

```bash
openspace-download-skill <skill_id>         # download a skill from the cloud
openspace-upload-skill /path/to/skill/dir   # upload a skill to the cloud
```

<details>
<summary><b>Python API</b></summary>

```python
import asyncio
from openspace import OpenSpace

async def main():
    async with OpenSpace() as cs:
        result = await cs.execute("Analyze GitHub trending repos and create a report")
        print(result["response"])

        for skill in result.get("evolved_skills", []):
            print(f"  Evolved: {skill['name']} ({skill['origin']})")

asyncio.run(main())
```

</details>

### 📊 本地仪表盘

查看你的技能如何进化——浏览技能、追踪谱系、对比差异。

> 需要 **Node.js ≥ 20**。

```bash
# Terminal 1. Start backend API
openspace-dashboard --port 7788

# Terminal 2: Start frontend dev server
cd frontend
npm install        # only needed once
npm run dev    
```

📖 **前端设置指南**：[`frontend/README.md`](frontend/README.md)

<div align="center">
<table>
<tr>
<td width="50%"><img src="assets/frontend_1.gif" width="100%" alt="Skill Classes" /></td>
<td width="50%"><img src="assets/frontend_2.gif" width="100%" alt="Cloud Skill Records" /></td>
</tr>
<tr>
<td align="center"><sub>Skill Classes — Browse, Search & Sort</sub></td>
<td align="center"><sub>Cloud — Browse & Discover Skill Records</sub></td>
</tr>
<tr>
<td width="50%"><img src="assets/frontend_3.gif" width="100%" alt="Version Lineage" /></td>
<td width="50%"><img src="assets/frontend_4.gif" width="100%" alt="Workflow Sessions" /></td>
</tr>
<tr>
<td align="center"><sub>Version Lineage — Skill Evolution Graph</sub></td>
<td align="center"><sub>Workflow Sessions — Execution History & Metrics</sub></td>
</tr>
</table>
</div>

---

## 📈 基准测试：GDPVal

我们在 [GDPVal](https://huggingface.co/datasets/openai/gdpval) 上评估 OpenSpace —— 涵盖 44 种职业、220 项真实世界专业任务。采用与 [ClawWork](https://github.com/HKUDS/ClawWork) 相同的评估协议，使用一致的生产力工具及基于 LLM 的评分机制。我们的两阶段设计（冷启动 → 热重跑）展示了累积技能如何随时间降低 Token 消耗。

公平基准测试：OpenSpace 以 Qwen 3.5-Plus 作为底层 LLM —— 与 ClawWork 基线智能体完全一致 —— 确保性能差异纯粹源于技能进化，而非模型能力本身。

真实经济价值：任务涵盖从构建薪资计算器到准备税务申报再到起草法律备忘录——这些生成实际 GDP 的真实专业工作，同时评估质量与成本效率。

<div align="center">
<img src="assets/benchmark_income.png" width="100%" alt="GDPVal Benchmark — Income Comparison" />
</div>

- **收益高出 4.2 倍** vs ClawWork（相同底层 LLM Qwen 3.5-Plus）
- **价值捕获率 72.8%** —— 在 $15,764 的任务总价值中赚取 $11,484，超越所有智能体
- **平均质量得分 70.8%** —— 比最佳 ClawWork 智能体（40.8%）高出 30 个百分点
- **第二阶段 Token 使用量较第一阶段降低 45.9%** —— 以更低的成本取得更好结果

<div align="center">
<img src="assets/benchmark_quality_tokens.png" width="100%" alt="GDPVal Benchmark — Quality & Token Efficiency" />
</div>

### OpenSpace 能处理哪些真实世界任务？

50 项 GDPVal 任务涵盖 6 个实际工作类别。 
- **第一阶段（冷启动）**：顺序执行全部 50 项任务——随着每项任务完成，技能累积在共享数据库中。
- **第二阶段（热重跑）**：使用第一阶段积累的全部进化技能数据库，重新执行相同的 50 项任务。

收益捕获率 = 实际赚取金额 ÷ 任务最大可能价值

<div align="center">
<img src="assets/benchmark_task_showcase.png" width="100%" alt="GDPVal Benchmark — Task Showcase by Category" />
</div>

## 🎯 进化产生最大影响的领域及原因：

| 类别 | 收益变化 | Token 变化 | 原因 |
|---|---|---|---|
| **📝 文档与信函** (7) | 71→74% (+3.3pp) | −56% | 打磨正式输出——加州隐私法备忘录、监控调查报告、抚养费案件报告。`document-gen-fallback` 技能族历经 13 次迭代，使结构生成与错误恢复近乎自动化。 |
| **📋 合规与表单** (11) | 51→70% (+18.5pp) | −51% | 结构化 PDF——基于 15 份源文档的税务申报、药房合规检查表、临床交接模板。PDF 技能链（检查逻辑 → reportlab 排版 → 验证）进化一次，所有表单任务即可复用完整流水线。 |
| **🎬 媒体制作** (3) | 53→58% (+5.8pp) | −46% | Python 与 ffmpeg 处理音视频——基于鼓点参考生成 bossa-nova 纯音乐、从 5 轨音频编辑贝斯干音、从 13 个源视频制作 CGI 展示 reel。进化技能编码了可用的 ffmpeg 参数与编解码器回退方案，消除了沙盒试错成本。 |
| **🛠️ 工程** (4) | 70→78% (+8.7pp) | −43% | 多交付物技术项目——Web3 全栈（Solidity + React + 测试）、CNC 工作单元安全系统（报告 + 布局 + 硬件表）、航空航天 CFD 报告。协调技能可跨这些多样化任务通用迁移。 |
| **📊 电子表格** (15) | 63→70% (+7.3pp) | −37% | 功能性 .xlsx 工具——基于工会合同的薪资计算器、基于历史数据的销售预测、含竞品基准的定价模型。跨领域共享相同的电子表格模式（公式、合并单元格、数据验证）。 |
| **📈 战略与分析** (10) | 88→89% (+1.0pp) | −32% | 战略建议——供应商谈判策略、非营利项目评估、$3 亿交易台的能源交易分析。本身质量已最高（88%）；节省源于复用文档结构与多文件编排逻辑。 |

### 进化产出了什么？（165 项技能）

在 50 项第一阶段任务中，OpenSpace 自主进化了 **165 项技能**。核心突破在于：这些不仅仅是领域知识——它们是**鲁棒的执行模式**与**质量保证工作流**。智能体学会了如何在不完美的真实环境中可靠地交付结果。

**关键发现**：大多数技能聚焦于工具可靠性与错误恢复，而非特定任务知识。

<div align="center">
<img src="assets/benchmark_skill_taxonomy.png" width="100%" alt="GDPVal Benchmark — Evolved Skill Taxonomy" />
</div>

| 目的 | 数量 | 教会智能体什么 |
|---|---|---|
| **文件格式 I/O** | 44 | PDF 提取回退、DOCX 解析、Excel 合并单元格处理、PPTX 创建。32/44 *捕获自真实失败*——每一项都是已解决的生产级 Bug。 |
| **执行恢复** | 29 | 分层回退：沙盒失败 → Shell → 文件写入后运行 → heredoc。28/29 *捕获自实际崩溃*。使一切其他功能可靠的基石。 |
| **文档生成** | 26 | 端到端文档流水线。`document-gen-fallback` 从 1 个导入技能进化为 **13 个衍生版本**——迭代最深的技能族。 |
| **质量保证** | 23 | 写入后验证：检查 Excel 行数、验证 PDF 页码、校对电子表格公式。解释 P2 质量为何提升——智能体*会验证*，而不仅是生成。 |
| **任务编排** | 17 | 多文件追踪、ZIP 打包、零迭代失败检测。跨多种交付物类型通用的元技能。 |
| **领域工作流** | 13 | SOAP 笔记、音频制作（基于 1 个模板进化出 **4 代**）、视频流水线。数量较少但每个领域内部进化极深。 |
| **Web 与研究** | 11 | SSL/代理调试、搜索回退、重 JS 页面处理。包含 2 项*已修复*技能——网络访问 inherently 不稳定。 |

**复现实验、分析工具与结果**：[`gdpval_bench/README.md`](gdpval_bench/README.md)

---

## 📊 案例展示：我的每日监控面板

> **零人工编写代码。** 60+ 项技能从零进化，构建出完全可用的实时仪表盘。

**My Daily Monitor** 是一个全天候运行的仪表盘，流式传输进程、服务器、新闻、市场、邮件与日程——内置 AI 智能体。

<div align="center">
<img src="assets/my_daily_monitor_light.png" width="90%" alt="My Daily Monitor – Light Mode" />
</div>

### OpenSpace 如何从零构建它（From Zero）

| 阶段 | 发生了什么 | 技能数量 |
|-------|--------------|--------|
| 🌱 **种子期** | 分析开源 [WorldMonitor](https://github.com/koala73/worldmonitor)，提取参考模式 | 6 项初始技能 |
| 🏗️ **搭建期** | 生成项目结构、Vite 配置、TypeScript 设置 | +8 项技能 |
| 🎨 **构建期** | 创建 20+ 个面板，含数据服务、API 路由、网格布局 | +25 项技能 |
| 🔧 **修复期** | 自动修复破损的 TypeScript、API 不匹配、CSS 冲突 | +12 次 FIX 进化 |
| 🧬 **进化期** | 衍生增强模式，合并互补技能 | +15 项 DERIVED 技能 |
| 📦 **捕获期** | 从成功执行中提取可复用模式 | +8 项 CAPTURED 技能 |

### 📈 技能进化图谱

<div align="center">
<img src="assets/my_daily_monitor_evograph.png" width="90%" alt="Skill Evolution Graph" />
</div>

> 每个节点都是 OpenSpace 学习、提取或优化的技能。完整的进化历史已在 [`showcase/.openspace/openspace.db`](showcase/.openspace/openspace.db) 中开源——在任何 SQLite 浏览器中加载即可探索谱系、差异与质量指标。

**完整详情**：[`showcase/README.md`](showcase/README.md)

---

## 🏗️ OpenSpace 的架构设计

<div align="center">
<img src="assets/framework.png" width="90%" alt="OpenSpace Framework" />
</div>

### 🧬 自我进化引擎

OpenSpace 的核心。技能不是静态文件——而是能够自动选择、应用、监控、分析和进化的“活体”实体。

#### 🔄 自主且持续进化

- **全生命周期管理**：从发现到应用到进化——全程无需人工干预。无论是否存在匹配技能，OpenSpace 均可完成任务。

**三种进化模式**：
- 🔧 FIX —— 就地修复破损或过时指令。同一技能的新版本。
- 🚀 DERIVED —— 基于父级技能创建增强或专用版本。新建技能目录，与父级共存。
- ✨ CAPTURED —— 从成功执行中提取新颖的可复用模式。全新技能，无父级依赖。

**三个独立触发器**：多层防线对抗技能退化——成功与失败执行均驱动进化。
- **📈 执行后分析** —— 每项任务完成后运行。分析完整录制并建议 FIX/DERIVED/CAPTURED。
- **⚠️ 工具退化** —— 当工具成功率下降时，质量监控器找出所有依赖技能并批量进化。
- **📊 指标监控** —— 定期扫描技能健康指标（应用率、完成率、回退率）并对表现不佳者进行进化。

#### 📊 全栈质量监控
多层追踪：质量监控覆盖整个执行堆栈——从高层工作流到单个工具调用：
- **🎯 技能** —— 应用率、完成率、有效率、回退率
- **🔨 工具调用** —— 成功率、延迟、标记问题
- **⚡ 代码执行** —— 执行状态、错误模式

**级联进化**：当任何组件退化时——无论是技能工作流还是单个工具调用——进化会自动触发所有上游依赖技能，保持系统整体一致性。

#### 🔧 智能且安全的进化
**🤖 自主进化**：每次进化都会探索代码库、发现根本原因并自主决定修复方案——在做出更改前收集真实证据，而非盲目生成。

**⚡ 基于差异与节省 Token**：生成最小化、针对性的 diff 而非完整重写，失败时自动重试。每个版本均存储在版本 DAG 中，具备完整的谱系追踪能力。

**🛡️ 内置安全护栏**：
- 确认机制减少误触发
- 防循环机制防止进化失控
- 安全检查标记危险模式（提示词注入、凭据外泄）
- 进化技能在替换前需经过验证

**🌐 协作技能社区**
一个智能体共享进化技能的注册中心。当一个智能体进化出改进时，所有连接的智能体均可发现、导入并在此基础上构建——将个体进步转化为集体智慧。

- **🔐 灵活共享**：公开分享、组内分享或保持私有。智能搜索帮你找到所需内容并自动导入。每次进化均带谱系追踪与完整 diff。
- **☁️ 协作平台**：open-space.cloud —— 注册获取 API Key，浏览社区技能，管理你的群组。

---

## 🔧 高级配置

对于大多数用户，[快速开始](#-quick-start) 已足够使用。如需高级选项（环境变量、执行模式、安全策略等），请查阅 [`openspace/config/README.md`](openspace/config/README.md)。

---

<a id="-code-structure"></a>
<details>
<summary><b>📖 Code Structure</b></summary>

> **Legend**: ⚡ Core modules &nbsp;|&nbsp; 🧬 Skill evolution &nbsp;|&nbsp; 🌐 Cloud &nbsp;|&nbsp; 🔧 Supporting modules

```
OpenSpace/
├── openspace/
│   ├── tool_layer.py                     # OpenSpace main class & OpenSpaceConfig
│   ├── mcp_server.py                     # MCP Server (4 tools for your agent)
│   ├── __main__.py                       # CLI entry point (python -m openspace)
│   ├── dashboard_server.py               # Web dashboard API server
│   │
│   ├── ⚡ agents/                         # Agent System
│   │   ├── base.py                       # Base agent class
│   │   └── grounding_agent.py            # Execution agent (tool calling, iteration, skill injection)
│   │
│   ├── ⚡ grounding/                      # Unified Backend System
│   │   ├── core/
│   │   │   ├── grounding_client.py       # Unified interface across all backends
│   │   │   ├── search_tools.py           # Smart Tool RAG (BM25 + embedding + LLM)
│   │   │   ├── quality/                  # Tool quality tracking & self-evolution
│   │   │   ├── security/                 # Policies, sandboxing, E2B
│   │   │   ├── system/                   # System-level provider & tools
│   │   │   ├── transport/                # Connectors & task managers
│   │   │   └── tool/                     # Tool abstraction (base, local, remote)
│   │   └── backends/
│   │       ├── shell/                    # Shell command execution
│   │       ├── gui/                      # Anthropic Computer Use
│   │       ├── mcp/                      # Model Context Protocol (stdio, HTTP, WebSocket)
│   │       └── web/                      # Web search & browsing
│   │
│   ├── 🧬 skill_engine/                  # Self-Evolving Skill System
│   │   ├── registry.py                   # Discovery, BM25+embedding pre-filter, LLM selection
│   │   ├── analyzer.py                   # Post-execution analysis (agent loop + tool access)
│   │   ├── evolver.py                    # FIX / DERIVED / CAPTURED evolution (3 triggers)
│   │   ├── patch.py                      # Multi-file FULL / DIFF / PATCH application
│   │   ├── store.py                      # SQLite persistence, version DAG, quality metrics
│   │   ├── skill_ranker.py               # BM25 + embedding hybrid ranking
│   │   ├── retrieve_tool.py              # Skill retrieval tool for agents
│   │   ├── fuzzy_match.py                # Fuzzy matching for skill discovery
│   │   ├── conversation_formatter.py     # Format execution history for analysis
│   │   ├── skill_utils.py                # Shared skill utilities
│   │   └── types.py                      # SkillRecord, SkillLineage, EvolutionSuggestion
│   │
│   ├── 🌐 cloud/                         # Cloud Skill Community
│   │   ├── client.py                     # HTTP client (upload, download, search)
│   │   ├── search.py                     # Hybrid search engine
│   │   ├── embedding.py                  # Embedding generation for skill search
│   │   ├── auth.py                       # API key management
│   │   └── cli/                          # CLI tools (download_skill, upload_skill)
│   │
│   ├── 💬 communication/                  # Multi-Channel Communication Gateway
│   │   ├── gateway.py                    # Message routing, session management, reply dispatch
│   │   ├── adapters/                     # Platform adapters (WhatsApp, Feishu)
│   │   ├── bridges/                      # Non-Python runtimes (WhatsApp Baileys bridge)
│   │   ├── config.py                     # Communication config loader
│   │   ├── session_store.py              # Per-channel session persistence
│   │   └── types.py                      # ChannelMessage, ChannelSource, SendResult
│   │
│   ├── 🔧 platform/                      # Platform abstraction (system info, screenshots)
│   ├── 🔧 host_detection/                # Auto-detect nanobot / openclaw credentials
│   ├── 🔧 host_skills/                   # SKILL.md definitions for agent integration
│   │   ├── delegate-task/SKILL.md        # Teaches agent: execute, fix, upload
│   │   └── skill-discovery/SKILL.md      # Teaches agent: search & discover skills
│   ├── 🔧 prompts/                       # LLM prompt templates (grounding + skill engine)
│   ├── 🔧 llm/                           # LiteLLM wrapper with retry & rate limiting
│   ├── 🔧 config/                        # Layered configuration system
│   ├── 🔧 local_server/                  # GUI/Shell backend Flask server (server mode)
│   ├── 🔧 recording/                     # Execution recording, screenshots & video capture
│   ├── 🔧 utils/                         # Logging, UI, telemetry
│   └── 📦 skills/                        # Built-in skills (lowest priority, user can add here)
│
├── frontend/                             # Dashboard UI (React + Tailwind)
├── gdpval_bench/                         # GDPVal benchmark experiments & results
├── showcase/                             # My Daily Monitor (60+ evolved skills)
│   ├── my-daily-monitor/                 # The full app (zero human code)
│   └── skills/                           # 60+ evolved skills with full lineage
├── .openspace/                           # Runtime: embedding cache + skill DB
└── logs/                                 # Execution logs & recordings
```

</details>

---

## 🔗 相关项目

OpenSpace 基于以下开源项目构建。我们衷心感谢其作者与贡献者：

- **[AnyTool](https://github.com/HKUDS/AnyTool)** —— 即插即用的通用工具调用层，适配任意 AI 智能体
- **[ClawWork](https://github.com/HKUDS/ClawWork)** - 将 AI 助手转化为真正的 AI 协作者
- **[WorldMonitor](https://github.com/koala73/worldmonitor)** - 实时全球情报仪表盘

---

<div align="center">

## ⭐ Star 历史

如果 OpenSpace 对你有帮助，请考虑给我们点个 Star！⭐

<div align="center">
  <a href="https://star-history.com/#HKUDS/OpenSpace&Date">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=HKUDS/OpenSpace&type=Date&theme=dark" />
      <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/svg?repos=HKUDS/OpenSpace&type=Date" />
      <img alt="Star History Chart" src="https://api.star-history.com/svg?repos=HKUDS/OpenSpace&type=Date" />
    </picture>
  </a>
</div>

**🧬 让你的智能体自我进化 · 🌐 共同成长社区 · 💰 更少 Token，更聪明智能体**

</div>

---

<p align="center">
  <em> ❤️ 感谢访问 ✨ OpenSpace!</em><br><br>
  <img src="https://visitor-badge.laobi.icu/badge?page_id=HKUDS.OpenSpace&style=for-the-badge&color=00d4ff"
  alt="Views">
</p>
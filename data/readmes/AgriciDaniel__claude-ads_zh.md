<p align="center">
  <img src="assets/banner.svg" alt="Claude Ads: Paid Advertising Audit Skill for Claude Code. Animated terminal-style banner with breathing gradient logo, scanning command palette, and pulsing status indicators" width="100%">
</p>

# Claude Ads：Claude Code 付费广告审计技能

手动审计单个 Google Ads 账户需要高级 PPC 专家花费 4-6 小时。**Claude Ads 仅需 10-15 分钟即可完成同等审计**，基于 0-100 加权评分系统给出分数，并输出针对 Google、Meta、YouTube、LinkedIn、TikTok、Microsoft、Apple 和 Amazon Ads 的优先级行动清单。专为 **PPC 代理商、企业内部营销人员及自由广告顾问** 打造。本地运行，确定性执行，采用 MIT 许可证。

[![Agent Skill](https://img.shields.io/badge/Agent%20Skills-Compatible-blue)](https://agentskills.io)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Version](https://img.shields.io/github/v/release/AgriciDaniel/claude-ads?label=public%20release)](https://github.com/AgriciDaniel/claude-ads/releases)
[![CI](https://img.shields.io/github/actions/workflow/status/AgriciDaniel/claude-ads/ci.yml?branch=main&label=public%20CI)](https://github.com/AgriciDaniel/claude-ads/actions)
[![Community](https://img.shields.io/badge/AI%20Marketing%20Hub-Pro%20community-purple)](https://www.skool.com/ai-marketing-hub-pro)
[![GitHub org](https://img.shields.io/badge/AI%20Marketing%20Hub-GitHub-181717?logo=github&logoColor=white)](https://github.com/AI-Marketing-Hub)

**宿主支持：**
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Verified-brightgreen)](https://claude.ai/claude-code)
[![Codex CLI](https://img.shields.io/badge/Codex%20CLI-Experimental-yellow)](https://github.com/openai/codex)
[![Cursor](https://img.shields.io/badge/Cursor-Experimental-yellow)](https://cursor.sh)
[![Windsurf](https://img.shields.io/badge/Windsurf-Experimental-yellow)](https://codeium.com/windsurf)
[![Gemini CLI](https://img.shields.io/badge/Gemini%20CLI-Experimental-yellow)](https://github.com/google-gemini/gemini-cli)
[![Goose](https://img.shields.io/badge/Goose-Experimental-yellow)](https://block.github.io/goose/)

> **最后更新：** 2026-05-18 · **版本：** v1.7.1 · [CHANGELOG](CHANGELOG.md) · [博客：完整广告审计拆解](https://agricidaniel.com/blog/claude-code-ad-agency)

> **本技能提供两个版本。**
> - 🌐 **公共开源版** → [`AgriciDaniel/claude-ads`](https://github.com/AgriciDaniel/claude-ads)：MIT 许可，公开发布，无需会员。适合追求稳定且希望下载使用的用户。
> - 🔒 **社区私有镜像版** → [`AI-Marketing-Hub/claude-ads`](https://github.com/AI-Marketing-Hub/claude-ads)：抢先体验即将推出的功能，并与 [AI Marketing Hub Pro](https://www.skool.com/ai-marketing-hub-pro) 社区直接协作。需要会员资格。

## 适用人群

- **管理 5+ 个广告账户的 PPC 代理商**：将每季度一次的审计改为每周一次。预算与时间投入不变。
- **跨 4+ 平台投放的企业内部营销人员**：在高管评审前增加一轮“第二双眼睛”检查。不受个人偏好影响，客观评估各平台表现。
- **自由 PPC 顾问**：通过 10 分钟审计快速锚定客户首日的服务范围。在你花费一小时做诊断之前，先赢得合作机会。

## v1.7.0（Wave 2）新增内容

- **3 个新子技能**：`/ads amazon`（Sponsored Products/Brands/Display、ACOS/TACOS）、`/ads attribution`（AdAttributionKit + GA4 + Consent Mode V2）、`/ads tracking`（sGTM + CAPI Gateway + 去重 + 哈希处理）。
- **41 项 pytest 评估套件**位于 `tests/`：路由快照、双向 209 项检查目录覆盖、评分算法确定性验证、SSRF 回归测试。每次提交均在 CI 中自动运行。
- **跨宿主安装矩阵**：`install.sh` / `install.ps1 --target=<host>`，内置白名单校验（支持 Claude Code、Codex CLI、Cursor、Windsurf、Gemini CLI、Goose）。
- **深度平台重写**：`/ads google` 适配 AI Max 时代（`ai_max_setting.enable_ai_max`、AI Brief、FUE、品牌排除设置）；`/ads meta` 适配 Andromeda + GEM + Lattice 时代，新增 Entity-ID 聚类检测。
- **10 项原则思维框架**：每项审计、规划与创意输出均遵循统一的认知纪律。详见 [`ads/references/thinking-framework.md`](ads/references/thinking-framework.md)。

完整发布说明：[CHANGELOG.md](CHANGELOG.md)。

## Demo

<p align="center">
  <img src="assets/demo.gif" alt="Claude Ads in action: /ads audit dispatching 6 parallel subagents, returning Ads Health Score with platform breakdown and prioritized action plan" width="100%">
</p>

### 示例输出

`/ads audit` 的实际返回结果（为简洁起见已截断）：

```json
{
  "ads_health_score": 73,
  "grade": "C",
  "audit_date": "2026-05-18",
  "platforms": {
    "google_ads": { "score": 78, "grade": "B", "checks_run": 80, "critical": 2, "high": 5 },
    "meta_ads":   { "score": 64, "grade": "C", "checks_run": 50, "critical": 4, "high": 7 },
    "linkedin":   { "score": 81, "grade": "B", "checks_run": 27, "critical": 0, "high": 3 }
  },
  "top_findings": [
    {
      "id": "M-AND-01",
      "severity": "critical",
      "platform": "meta",
      "title": "Andromeda creative similarity > 60%: retrieval suppression risk",
      "impact": "Estimated 20-35% reach loss; 4 ad sets affected",
      "action": "Replace 7 near-duplicate creatives with concept-diverse variants",
      "owner": "creative",
      "eta_days": 7
    },
    {
      "id": "G-AIM-03",
      "severity": "high",
      "platform": "google",
      "title": "AI Max enabled without negative keyword discipline",
      "impact": "Wasted spend ~$1,400/mo on irrelevant queries",
      "action": "Build negative list from 30d search term report",
      "owner": "search",
      "eta_days": 2
    }
  ],
  "quick_wins": [
    "Enable Consent Mode V2 (Privacy Sandbox compatible, ~1 hr)",
    "Pause 3 ad groups failing 3x Kill Rule (saves ~$420/mo)"
  ]
}
```

此外还提供 PDF 版本（使用 `/ads report`），包含健康度仪表盘、平台对比图表及零重叠排版的客户交付文档。

## 目录

- [安装方式：为 Claude Code 添加 Claude Ads 的三种方法](#installation-3-ways-to-add-claude-ads)
- [快速开始](#quick-start)
- [命令列表](#commands)
- [功能特性：250+ 审计检查覆盖范围](#features-what-250-audit-checks-cover)
- [与手动/代理商/商业工具对比](#compared-to-manual--agency--commercial-tools)
- [使用场景](#use-cases)
- [评估套件：严谨验证](#eval-harness-verified-rigor)
- [架构设计](#architecture)
- [工作原理：如何分析你的广告](#how-it-analyzes-your-ads)
- [常见问题](#faq)
- [环境要求](#requirements)
- [卸载](#uninstall)
- [路线图](#roadmap)
- [项目信息](#project-info)
- [相关项目](#related-projects)
- [维护者](#maintainer)
- [许可证](#license)

## 安装方式：为 Claude Code 添加 Claude Ads 的三种方法

> ℹ️ **提供两种安装路径——请选择符合你权限的版本。**
>
> 以下命令默认指向**社区私有镜像版** `AI-Marketing-Hub/claude-ads`（Pro 会员抢先体验）。若要使用**公共发布版** `AgriciDaniel/claude-ads`（MIT 许可，无需会员），请将所有命令中的 `AI-Marketing-Hub/claude-ads` 替换为 `AgriciDaniel/claude-ads`，并将插件标识符 `claude-ads@ai-marketing-hub-claude-ads` 替换为 `claude-ads@agricidaniel-claude-ads`。
>
> Pro 会员：需要执行 `gh auth login`（或提供 PAT）并拥有 `AI-Marketing-Hub` 组织的访问权限。若 `/plugin marketplace add` 返回 404，请在 [Skool 社区](https://www.skool.com/ai-marketing-hub-pro) 私聊管理员添加权限。

### 1. 插件安装（Claude Code，推荐）

```shell
/plugin marketplace add AI-Marketing-Hub/claude-ads
/plugin install claude-ads@ai-marketing-hub-claude-ads
```

将 claude-ads 注册为原生插件，支持自动更新、命名空间隔离与版本追踪。

### 2. 一键安装（Unix/macOS/Linux）

```bash
curl -fsSL https://raw.githubusercontent.com/AI-Marketing-Hub/claude-ads/main/install.sh | bash
```

### 3. 一键安装（Windows PowerShell）

```powershell
irm https://raw.githubusercontent.com/AI-Marketing-Hub/claude-ads/main/install.ps1 | iex
```

### 4. 跨宿主安装（Codex CLI / Cursor / Windsurf / Gemini CLI / Goose）

```bash
# Unix/macOS/Linux
bash install.sh --target=codex      # OpenAI Codex CLI       (实验性)
bash install.sh --target=cursor     # Cursor IDE              (实验性)
bash install.sh --target=windsurf   # Windsurf IDE            (实验性)
bash install.sh --target=gemini     # Gemini CLI              (实验性)
bash install.sh --target=goose      # Goose CLI               (实验性)
```

```powershell
# Windows PowerShell
.\install.ps1 -Target codex
.\install.ps1 -Target cursor
.\install.ps1 -Target windsurf
.\install.ps1 -Target gemini
.\install.ps1 -Target goose
```

**各宿主安装路径对照表：**

| Target     | 技能根目录                                     | Agent 根目录                                | Python 依赖 |
|------------|-------------------------------------------------|--------------------------------------------|-------------|
| `claude`   | `~/.claude/skills`                              | `~/.claude/agents`                         | ✓           |
| `codex`    | `~/.codex/skills`                               | `~/.codex/agents`                          | ✓           |
| `cursor`   | `~/.cursor/extensions/claude-ads/skills`        | `~/.cursor/extensions/claude-ads/agents`   | 跳过        |
| `windsurf` | `~/.windsurf/skills`                            | `~/.windsurf/agents`                       | 跳过        |
| `gemini`   | `~/.gemini/extensions/claude-ads/skills`        | `~/.gemini/extensions/claude-ads/agents`   | 跳过        |
| `goose`    | `~/.config/goose/skills`                        | `~/.config/goose/agents`                   | 跳过        |

**路径覆盖：**

```bash
bash install.sh --target=claude --skill-dir=~/custom/skills --agent-dir=~/custom/agents
```

目标宿主与覆盖路径均经过严格白名单校验：无 Shell 注入、无参数歧义、无 `..` 穿越、无 UNC 路径。

> ⚠ **实验性宿主：** 仅 Claude Code 已通过端到端验证。其他宿主安装路径遵循各平台官方约定；技能发现机制与子技能路由可能有所不同。若某目标需要调整，请提交包含复现步骤的 Issue。

### 手动安装

```bash
git clone https://github.com/AI-Marketing-Hub/claude-ads.git
cd claude-ads
./install.sh                # Unix/macOS/Linux，默认 target=claude
./install.sh --target=codex # 任意跨宿主目标
```

```powershell
.\install.ps1                # Windows PowerShell，默认 Target=claude
.\install.ps1 -Target codex
```

<p align="center">
  <img src="assets/diagrams/20-install-methods.svg" alt="Installation Methods Comparison" width="100%">
</p>

## 快速开始

```bash
# 启动 Claude Code
claude

# 运行全平台审计
/ads audit

# 单平台深度分析
/ads google
/ads meta
/ads linkedin

# 按业务类型制定战略计划
/ads plan saas
/ads plan ecommerce
/ads plan local-service

# 跨平台创意质量审计
/ads creative

# 预算与出价策略审查
/ads budget
```

<p align="center">
  <img src="assets/diagrams/06-how-it-works.svg" alt="How It Works: 5-Step Process" width="100%">
</p>

## 命令列表

| 命令 | 说明 |
|---------|-------------|
| `/ads audit` | 全平台并行审计，自动委派子 Agent 执行 |
| `/ads google` | Google Ads 深度分析（Search、PMax、AI Max、Display、YouTube、Demand Gen） |
| `/ads meta` | Meta Ads 深度分析（FB、IG、Threads、Advantage+、Andromeda + GEM + Lattice） |
| `/ads youtube` | YouTube Ads 专项分析（Skippable、Shorts、Demand Gen、CTV） |
| `/ads linkedin` | LinkedIn Ads 深度分析（B2B、Lead Gen、TLA、ABM） |
| `/ads tiktok` | TikTok Ads 深度分析（Creative、Shop、Smart+、post-USDS） |
| `/ads microsoft` | Microsoft/Bing Ads 深度分析（Copilot、导入校验） |
| `/ads apple` | Apple Ads 深度分析（CPPs、Maximize Conversions、AdAttributionKit、TAP） |
| `/ads amazon` | Amazon Ads 深度分析（Sponsored Products / Brands / Display、ACOS / TACOS）· *Wave 2* |
| `/ads attribution` | 跨平台归因审计（AdAttributionKit、GA4、Consent Mode V2、MMP）· *Wave 2* |
| `/ads tracking` | 服务端追踪管道审计（sGTM、CAPI Gateway、去重、哈希处理）· *Wave 2* |
| `/ads creative` | 跨平台创意质量审计与疲劳度检测 |
| `/ads landing` | 广告落地页质量评估 |
| `/ads budget` | 预算分配与出价策略审查 |
| `/ads plan <type>` | 行业模板战略广告计划 |
| `/ads competitor` | 全平台竞品广告情报分析 |
| `/ads math` | PPC 财务计算器（CPA、ROAS、盈亏平衡点、预算预测、LTV:CAC） |
| `/ads test` | A/B 测试设计（假设框架、显著性、样本量、周期） |
| `/ads report` | 生成 PDF 审计报告用于客户交付 |
| `/ads dna <url>` | 从官网提取品牌 DNA → `brand-profile.json` |
| `/ads create` | 生成广告创意概念 + 文案简报 → `campaign-brief.md` |
| `/ads generate` | 根据简报生成 AI 广告图 → `ad-assets/` |
| `/ads photoshoot` | 5 种风格产品摄影（Studio、Floating、Ingredient、In Use、Lifestyle） |

### `/ads audit`
**全平台并行审计**

启动 6 个并行子 Agent：
- **audit-google**：80 项检查，覆盖 Search、PMax、AI Max、Demand Gen、CTV、YouTube
- **audit-meta**：50 项检查，覆盖 Pixel/CAPI、Andromeda 创意多样性、账户结构、受众定向
- **audit-creative**：跨平台创意质量评估（含 Andromeda Entity-ID 与 Symphony 感知）
- **audit-tracking**：转化追踪 + 隐私基础设施（Consent Mode V2、CAPI、Events API、AdAttributionKit）
- **audit-budget**：LinkedIn、TikTok、Microsoft 的预算与出价策略
- **audit-compliance**：全平台合规性、设置检查与性能基准对比

生成统一的 **广告健康度评分（0-100）** 及优先级行动清单。

> **Wave 2 独立子技能。** `/ads audit` 并行委派上述 6 个 Agent。Amazon、归因与服务端追踪为独立子技能（`/ads amazon`、`/ads attribution`、`/ads tracking`）；请直接调用它们。Wave 3 将为其添加配套的审计 Agent。

<p align="center">
  <img src="assets/diagrams/02-pipeline-A.svg" alt="Audit pipeline: stage-by-stage execution from data intake through parallel sub-agent dispatch to scored report output" width="100%">
</p>

<p align="center">
  <img src="assets/diagrams/19-audit-lifecycle.svg" alt="Audit Lifecycle" width="100%">
</p>

### `/ads plan <business-type>`
**战略广告规划**

内置行业模板，涵盖平台组合、账户架构、创意策略、定向设置、预算指南与 KPI 目标。

**支持的业务类型：**
- `saas`：试用/演示导向，Google + LinkedIn 为主
- `ecommerce`：Shopping/PMax，ROAS 导向，季节性投放
- `local-service`：Google Search + LSA，通话追踪，地理半径定向
- `b2b-enterprise`：LinkedIn ABM，长销售周期，漏斗指标管理
- `info-products`：Meta + YouTube，网络研讨会/VSL 转化漏斗
- `mobile-app`：Meta + Google UAC，需集成 MMP，关注 LTV:CPI
- `real-estate`：特殊广告类别（住房），买家/卖家投放组合
- `healthcare`：HIPAA 合规、LegitScript 认证、受限定向策略
- `finance`：特殊广告类别（信贷）、强制披露声明
- `agency`：多客户管理、标准化报告框架
- `generic`：通用模板，含平台选择问卷

<p align="center">
  <img src="assets/diagrams/08-industry-templates.svg" alt="Industry Templates" width="100%">
</p>

### `/ads math` 与 `/ads test`

<p align="center">
  <img src="assets/diagrams/18-ppc-calculators.svg" alt="PPC Calculators" width="48%">
  <img src="assets/diagrams/17-ab-testing.svg" alt="A/B Test Design" width="48%">
</p>

### `/ads report`

面向客户交付的 PDF 审计报告：健康度仪表盘、平台对比图表、通过/失败分布图、格式化表格、零重叠排版布局。

<p align="center">
  <img src="assets/diagrams/16-pdf-pipeline.svg" alt="PDF Report Pipeline" width="100%">
</p>

## 功能特性：250+ 审计检查覆盖范围

每项检查的实际作用：精准捕捉导致预算浪费的平台特定盲区。例如 Meta 的 Andromeda 创意相似度抑制机制、Google AI Max 中的否定关键词纪律缺失、Andromeda 感知的创意多样性评分、Apple 的 AdAttributionKit 可配置窗口期漏洞、Amazon 的 ACOS/TACOS 目标与利润率错配，以及落地页缺少 Consent Mode V2（隐性收入流失）。这些正是手动审计容易遗漏的项目——分析师往往还在检查 *过去* 重要的指标，而非平台在 2026 年已变更的规则。

### 各平台覆盖明细

| 平台 | 检查项数 | 核心领域 |
|----------|--------|-----------|
| Google Ads | 80 | Search、PMax、AI Max（`ai_max_setting`、AI Brief、FUE）、Demand Gen、CTV、YouTube |
| Meta Ads | 50 | Pixel/CAPI、Andromeda + GEM + Lattice、Entity-ID 聚类、ASC/AAC、账户结构、受众定向 |
| LinkedIn Ads | 27 | B2B 定向、TLA、Lead Gen、CRM 集成 |
| TikTok Ads | 28 | 创意优先、Smart+、GMV Max、搜索广告、Events API（post-USDS） |
| Microsoft Ads | 24 | Google 导入安全校验、Copilot、CTV、LinkedIn 定向、视频投放 |
| Apple Ads | 35+ | 账户结构、CPPs、Maximize Conversions、AdAttributionKit |
| Amazon Ads | 30+\* | Sponsored Products / Brands / Display、ACOS / TACOS、搜索词挖掘 |
| 跨平台 | 3 | 隐私基础设施、创意多样性、更新频率 |
| 归因 + 服务端 | 25+\* | AdAttributionKit、GA4、Consent Mode V2、sGTM、CAPI Gateway、哈希质量 |

> \* **已验证 vs 预估。** Google（80）、Meta（50）、LinkedIn（27）、TikTok（28）与 Microsoft（24）的共 209 项检查已通过 `tests/fixtures/check-catalog.yaml` 双向校验；若数据漂移将直接导致 CI 失败。Apple、Amazon、跨平台及归因+服务端为各 SKILL.md 文件中的内联阈值；对应审计参考文件与目录条目将在 Wave 3 上线。

<p align="center">
  <img src="assets/diagrams/15-platform-grid.svg" alt="Platform Coverage Grid" width="100%">
</p>

<p align="center">
  <img src="assets/diagrams/04-platform-checks.svg" alt="Platform Check Distribution" width="100%">
</p>

### 广告健康度评分（0-100）

加权评分算法，含严重性乘数：

| 等级 | 分数段 | 需采取的行动 |
|-------|-------|-----------------|
| A | 90-100 | 仅需微调优化 |
| B | 75-89 | 存在部分改进空间 |
| C | 60-74 | 明显问题需优先处理 |
| D | 40-59 | 存在严重问题 |
| F | <40 | 需紧急干预 |

<p align="center">
  <img src="assets/diagrams/04-scoring-weights-B.svg" alt="Scoring weight breakdown: donut chart showing the 9 audit categories that compose the 100-point Ads Health Score, with per-platform legend" width="100%">
</p>

### 行业自动识别

通过广告账户信号（商品 Feed、转化事件、平台组合、定向模式）自动检测业务类型，并加载行业专属基准与模板。

### 质量门禁（Quality Gates）

审计过程中强制执行的核心规则：
- Google 投放中，绝不推荐脱离智能出价（Smart Bidding）的广泛匹配（Broad Match）
- **3x Kill Rule**：CPA > 目标值 3 倍时立即标记并暂停
- 预算充足性校验：Meta ≥5x CPA/广告组，TikTok ≥50x CPA/广告系列
- 学习期保护：活跃学习阶段禁止修改设置
- 合规检查：自动识别特殊广告类别（住房/信贷/金融）
- **隐私基础设施门禁**：在给出优化建议前，强制验证追踪栈（Consent Mode V2、CAPI、Events API、AdAttributionKit）
- **Andromeda 创意多样性**：标记 Meta 账户中 <10 个真正差异化的创意素材

<p align="center">
  <img src="assets/diagrams/05-quality-gates.svg" alt="Quality Gates" width="100%">
</p>

### 创意管道（Creative Pipeline）

AI 驱动的创意生成工作流，含 4 个专用 Agent（`/ads dna` → `/ads create` → `/ads generate` → `/ads photoshoot`）。

<p align="center">
  <img src="assets/diagrams/14-creative-pipeline.svg" alt="Creative Pipeline" width="100%">
</p>

### 参考数据（Reference Data）

内置 26 份参考文件，涵盖 2026 年最新基准、出价决策树、平台规范、合规要求、转化追踪指南、MCP 集成说明与平台覆盖备注。

### 10 项原则思维框架

每项审计、规划与创意输出均遵循统一的认知纪律：**OBSERVE × 2 / LISTEN / THINK / CONNECT × 2 / FEEL / ACCEPT / CREATE / GROW**。将每项原则映射到具体的广告工作行为，标注跳过该原则的反模式信号，并明确其主导的工作流阶段。这决定了你是输出一堆红色预警清单，还是交付一份真正的战略方案。定义于 [`ads/references/thinking-framework.md`](ads/references/thinking-framework.md)。

### 数据处理与隐私（Data handling & privacy）

完全在本地通过 Claude Code 运行。不会向外部服务器发送任何广告账户数据。使用 MCP 服务器获取实时 API 访问时，数据仅在您的设备与平台 API 之间直接流转。所有分析均在本地完成。

<p align="center">
  <img src="assets/diagrams/12-privacy-flow.svg" alt="Privacy and Data Flow" width="100%">
</p>

## 与手动审计 / 代理商 / 商业工具对比

| | 手动审计 | 代理商合作 | 商业 PPC 审计工具 | **Claude Ads** |
|---|---|---|---|---|
| **单次耗时** | 4-6 小时（高级 PPC） | 1-2 周交付周期 | 5-30 分钟 | **10-15 分钟** |
| **成本** | 高（按工时计费） | $2k-$10k+ / 项目 | $99-$799/月订阅 | **免费技能 + Claude Code 订阅费** |
| **可重复性** | 不同分析师结果不一致 | 跨账户表现不稳定 | 是 | **是，确定性执行 + 可脚本化** |
| **输出格式** | 冗长 PDF 报告 | 品牌定制 PPT | Web 仪表盘、导出文件 | **JSON + PDF，本地文件直出** |
| **自定义基准** | 手动维护 | 手动配置 | 厂商固定不可改 | **直接编辑本地 SKILL.md** |
| **数据是否离开设备？** | 否（你的表格） | 是（发送给代理商） | 是（上传至供应商） | **否，完全本地化** |
| **锁定风险** | 无 | 高 | 高（数据迁移成本高） | **无（MIT 开源，文件归你）** |
| **Andromeda / AI Max / AdAttributionKit 感知能力** | 依赖分析师经验 | 依赖代理商资深程度 | 滞后（通常落后 6-12 个月） | **原生支持 Andromeda (Oct 2025)、AI Max (May 2025)、AdAttributionKit + WWDC25 可配置窗口期、Consent Mode V2** |

> 成本基准说明：手动审计按行业高级 PPC 顾问标准工时计算；代理商合作基于常见发现/审计交付范围估算；商业工具订阅参考 PPC 审计品类中端定价。你的实际数字可能有所不同。

## 使用场景

**管理 12 个客户账户的代理商负责人。** 用每周一下午的 `/ads audit` 替代每季度一次的“深度审计”仪式。向客户发送健康度评分邮件的时间从 4 小时缩短至 12 分钟；覆盖频率从季度提升至周度，且无需额外计费工时。

**50 人规模 SaaS 公司的企业内部营销人员。** 在季度业务评审（QBR）前 24 小时运行 `/ads audit`。提前拦截平台 UI 隐藏的隐患（转化目标断裂、ASC 预算饥饿、缺失 Andromeda 创意多样性），避免 CMO 在董事会面前质问“为什么 CAC 涨了？”

**自由 PPC 顾问接手新客户。** 在首次需求沟通会上直接运行 `/ads audit`。用真实的 0-100 分数与 3 项高优关键发现锚定服务范围，而非模糊的“我看看情况再回复你”。价值证明发生在提案之前，签约率显著提升。

## 评估套件：严谨验证

**41 项测试，全部通过，每次提交均触发 CI。** `tests/` 目录下的 Pytest 套件包含：

- **路由快照**：每个文档化触发词精准路由至对应子技能（拦截描述回归缺陷）
- **检查目录覆盖**：`tests/fixtures/check-catalog.yaml`（209 个 ID）与所有审计参考文件双向校验；无孤立 ID，无未跟踪行
- **评分算法验证**：重新实现加权评分逻辑；断言连续 10 次运行结果一致且严重性权重正确
- **SSRF 回归测试集**：27 项 IPv4/IPv6 黑名单用例、非 HTTP 协议拦截、DNS 失败关闭策略、凭证脱敏

这在 Claude Code 技能中较为罕见。使项目可端到端审计，防止发布版本出现“宣传 vs 实际”的偏差。

## 架构设计

<p align="center">
  <img src="assets/diagrams/01-architecture-B.svg" alt="System architecture: left-to-right pipeline from /ads audit invocation through orchestrator routing, sub-skill execution, and report synthesis" width="100%">
</p>

<p align="center">
  <img src="assets/diagrams/03-sub-skill-map-B.svg" alt="Sub-skill ecosystem: 22 modules organized as concentric rings, platform sub-skills inner, cross-cut and strategy and creative sub-skills outer" width="100%">
</p>

```
~/.claude/skills/ads/              # 主编排器
~/.claude/skills/ads/references/   # 26 份 RAG 参考文件
~/.claude/skills/ads-*/            # 22 个子技能（含 ads-math、ads-test、ads-amazon、ads-attribution、ads-server-side-tracking）
~/.claude/skills/ads-plan/assets/  # 12 份行业模板
~/.claude/agents/                  # 10 个 Agent（6 审计 + 4 创意）
~/.claude/skills/ads/tests/        # 41 项 pytest 评估套件（Wave 2）
```

### 工作原理

1. **编排器**（`/ads`）将命令路由至专业子技能
2. **子技能**提供深度单领域分析与结构化输出
3. **Agent** 在全量审计中并行运行以最大化速度
4. **参考文件**按需加载（RAG 模式）；每次分析仅调用所需内容
5. **模板**提供行业专属战略框架

## 工作原理：如何分析你的广告

**Claude Ads 依赖你提供的数据工作**：导出文件、截图或从广告平台仪表盘粘贴的指标。它不会自动连接任何广告平台 API。

**要获取准确且针对账户的建议：**
1. 导出你的账户数据（建议最近 30 天）
2. 运行对应命令：`/ads google`、`/ads audit` 等
3. Claude 会先询问你的行业与预算背景；提供这些信息可匹配更精准的基准
4. 在提示时粘贴或分享你的数据

<p align="center">
  <img src="assets/diagrams/07-data-flow.svg" alt="Data Flow" width="100%">
</p>

### 实时数据集成（可选）

若需直接 API 访问而无需手动导出，可将 Claude Ads 与 MCP 服务器配合使用。详见 [`ads/references/mcp-integration.md`](ads/references/mcp-integration.md)：
- **Google Ads**：[mcp-google-ads](https://github.com/cohnen/mcp-google-ads)，29 个 GAQL 工具支持实时 API 访问
- **Meta Ads**：[Adspirer MCP](https://www.adspirer.com)（商业版）；自托管方案 = 封装 Meta Marketing API 并将 JSON 喂入标准数据收集流
- **LinkedIn Ads**：[GrowthSpree MCP](https://www.growthspreeofficial.com) 或 [Adzviser MCP](https://adzviser.com)

<p align="center">
  <img src="assets/diagrams/10-mcp-integration.svg" alt="MCP Integration" width="100%">
</p>

## FAQ

<details>
<summary><b>Claude Ads 能自动登录我的广告管理后台吗？</b></summary>

不能。Claude Ads 分析你提供的数据（导出文件、截图或粘贴指标）。它不会自动连接广告平台。如需 Google Ads API 实时访问，请参阅 [实时数据集成](#live-data-integration-optional) 部分使用 MCP。
</details>

<details>
<summary><b>它是用真实账户数据还是通用基准？</b></summary>

两者结合。你的账户数据驱动审计结果；行业基准（基于覆盖数千广告活动的研究）提供对比底线与上限。基准为平均值，实际表现因行业、预算级别与账户成熟度而异。建议首次使用时明确告知行业与月预算，以获取最相关的对比参考。
</details>

<details>
<summary><b>广告投放或广告系列创建仍需手动操作吗？</b></summary>

是的。Claude Ads 是审计与战略工具。它负责发现问题、推荐修复方案并制定广告计划，但创建、修改或投放广告仍需在你的广告平台中手动完成。
</details>

<details>
<summary><b>为什么有些建议似乎不适合我的账户规模？</b></summary>

$500/月 与 $50k/月 的账户在基准与最佳实践上差异显著。请提前告知预算：“我在 Google Ads 投放本地 Plumbing 业务，月预算 $2k”，比直接冷启动 `/ads google` 效果好得多。
</details>

<details>
<summary><b>是否支持 [某平台] 广告？</b></summary>

当前支持：Google、Meta（Facebook/Instagram）、YouTube、LinkedIn、TikTok、Microsoft/Bing、Apple 与 Amazon。其他平台（Reddit、CTV/OTT、Pinterest、Snapchat）的投放策略已收录于 `ads/references/additional-platforms.md`，供战略规划参考。
</details>

<details>
<summary><b>如何对 ROAS、CPA、ACOS、TACOS、LTV:CAC 等财务 KPI 进行评分？</b></summary>

使用 `/ads math` 调用财务计算器（含 CPA、ROAS、CPL、盈亏平衡分析、展现份额机会评估、预算预测、LTV:CAC 比率、MER）。全量审计（`/ads audit`）会自动将你上报的 ROAS / CPA / CPL 与 `ads/references/benchmarks.md` 加载的行业专属目标进行基准对比。针对 Amazon，`/ads amazon` 会将 ACOS 和 TACOS 与品类基准对比，并标记 TACOS 超出贡献利润率的商品。
</details>

<details>
<summary><b>维护与支持承诺是怎样的？</b></summary>

单一维护者（见 [维护者](#maintainer)）。Bug 报告通过 GitHub Issue 提交，公共仓库 48 小时内响应；Pro 社区成员可通过 [Skool 社区](https://www.skool.com/ai-marketing-hub-pro) 获得更快支持。功能请求无 SLA，统一纳入公开路线图管理。CI 会在每次提交时运行完整评估套件，确保回归缺陷在发布前被拦截。
</details>

<details>
<summary><b>我的数据会离开本地设备吗？</b></summary>

不会。该技能完全在 Claude Code 本地运行。若你选择接入实时 MCP（如 mcp-google-ads），数据仅在您的设备与平台 API 之间直接流转，绝不会经过 claude-ads 基础设施（实际上也没有）。
</details>

<details>
<summary><b>这与商业 PPC 审计工具有什么区别？</b></summary>

三点核心差异：(1) 本地优先，数据不上传至任何第三方；(2) MIT 开源可分叉：你可直接修改审计检查逻辑；(3) 紧跟 2026 年平台变更（Andromeda、AI Max、AdAttributionKit），而商业工具通常滞后 6-12 个月。
</details>

<details>
<summary><b>代理商能否将此用于客户服务？</b></summary>

可以。MIT 许可允许商用。通过 `/ads report` 模板可白标化 PDF 报告。`/ads plan agency` 模板专为多客户管理设计。社区私有镜像版（AI-Marketing-Hub）比公共发布早一步向 Pro 会员开放。
</details>

## 环境要求

- Claude Code CLI
- Python 3.10+ 与 Playwright（可选，用于实时落地页分析）
- reportlab（可选，用于通过 `/ads report` 生成 PDF）

## 卸载

### Unix/macOS/Linux

```bash
curl -fsSL https://raw.githubusercontent.com/AI-Marketing-Hub/claude-ads/main/uninstall.sh | bash
```

### Windows PowerShell

```powershell
irm https://raw.githubusercontent.com/AI-Marketing-Hub/claude-ads/main/uninstall.ps1 | iex
```

## 路线图

<p align="center">
  <img src="assets/diagrams/05-roadmap-A.svg" alt="Wave roadmap: 12-month timeline from v1.5 stable through v1.7.x Wave 2 to v1.8.0 visual system and v2.0 multi-tenant" width="100%">
</p>

从 v1.5 稳定版至 Wave 2（v1.7.x，当前版本）再到 Wave 3（v1.8.0+，私有仓库活跃开发中）的 12 个月交付节奏。各版本详细更新见 [CHANGELOG.md](CHANGELOG.md)。

## 项目信息

- [CHANGELOG](CHANGELOG.md)：发布历史与完整 Wave 2 说明（v1.7.0 + v1.7.1）
- [CONTRIBUTING](CONTRIBUTING.md)：Bug 报告、功能请求、子技能模板、测试规范
- [CODE OF CONDUCT](CODE_OF_CONDUCT.md)：Contributor Covenant 行为准则
- [SECURITY](SECURITY.md)：漏洞披露机制、出站网络目标表、错误信息脱敏
- [SUPPORT](SUPPORT.md)：求助渠道

## 相关项目

- [Claude SEO](https://github.com/AgriciDaniel/claude-seo)：面向 Claude Code 的综合 SEO 分析技能

> 寻找另一个版本？请查看本 README 顶部的 **[本技能提供两个版本。](#claude-ads-paid-advertising-audit-skill-for-claude-code)** 说明区块。

## 维护者

由 **[Agrici Daniel](https://agricidaniel.com/about)**（AI 工作流架构师）独立开发，欢迎通过 [Pro Skool 社区](https://www.skool.com/ai-marketing-hub-pro) 参与贡献。

- [博客](https://agricidaniel.com/blog)：AI 营销自动化深度解析
- [AI Marketing Hub (免费)](https://www.skool.com/ai-marketing-hub)：开放社区
- [AI Marketing Hub Pro](https://www.skool.com/ai-marketing-hub-pro)：Pro 社区，抢先体验本技能
- [YouTube](https://www.youtube.com/@AgriciDaniel)：教程与演示视频
- [所有开源工具](https://github.com/AgriciDaniel)：公共主页

## Star 历史

<a href="https://star-history.com/#AgriciDaniel/claude-ads&Date">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=AgriciDaniel/claude-ads&type=Date&theme=dark" />
    <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/svg?repos=AgriciDaniel/claude-ads&type=Date" />
    <img alt="Star history of AgriciDaniel/claude-ads on GitHub" src="https://api.star-history.com/svg?repos=AgriciDaniel/claude-ads&type=Date" />
  </picture>
</a>

如果 Claude Ads 为你节省了时间，在 [公共仓库](https://github.com/AgriciDaniel/claude-ads) 点个 Star 是最简单的感谢方式（也能帮助更多 PPC 从业者发现它）。

## 许可证

MIT。详见 [LICENSE](LICENSE)。
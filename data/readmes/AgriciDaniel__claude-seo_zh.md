![Claude SEO 终端横幅：动画 CRT 命令面板，包含 /seo audit、/seo schema、/seo geo，系统行显示 25 个子技能、271 项测试、8 个 MCP 服务器](assets/banner.svg)

# Claude SEO：Claude Code 的 SEO 分析技能

**Claude SEO 是 [Claude Code](https://claude.ai/claude-code) 的一款开源 SEO 分析插件。** 它在技术 SEO、内容质量（E-E-A-T）、Schema.org 标记、AI 搜索优化（GEO）、本地 SEO、电商和国际化 SEO 等领域并行运行 25 个子技能和 18 个专家代理。每次审计都会生成一份优先级行动清单，其中包含基于 Google 官方原始指南的、可证伪的建议。

[![CI](https://github.com/AgriciDaniel/claude-seo/actions/workflows/ci.yml/badge.svg)](https://github.com/AgriciDaniel/claude-seo/actions/workflows/ci.yml)
[![Claude Code Skill](https://img.shields.io/badge/Claude%20Code-Skill-blue)](https://claude.ai/claude-code)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Version](https://img.shields.io/github/v/release/AgriciDaniel/claude-seo)](https://github.com/AgriciDaniel/claude-seo/releases)
[![Tests](https://img.shields.io/badge/tests-271%20passing-brightgreen)](tests/)
[![Community](https://img.shields.io/badge/AI%20Marketing%20Hub-Pro%20community-purple)](https://www.skool.com/ai-marketing-hub-pro)

> **两个版本。**
> - 🌐 **公共开源版** → [`AgriciDaniel/claude-seo`](https://github.com/AgriciDaniel/claude-seo)：MIT 协议，公开发布，无需会员资格。如果你想要稳定且可下载的发行版，请使用此版本。
> - 🔒 **社区私有镜像** → [`AI-Marketing-Hub/claude-seo`](https://github.com/AI-Marketing-Hub/claude-seo)：抢先体验即将推出的功能，并与 [AI Marketing Hub Pro](https://www.skool.com/ai-marketing-hub-pro) 社区直接协作。需要会员资格。

### 为什么选择 Claude SEO

- **AI 搜索优先。** 对齐 [Google AI 优化指南](https://developers.google.com/search/docs/fundamentals/ai-optimization-guide)。基于问题的可引用性评分、llms.txt 上的原始来源证据、用于 AI 生成产品图的 IPTC `TrainedAlgorithmicMedia`，以及按 [web.dev](https://web.dev/) 标准进行的代理友好型页面检查。
- **并行执行。** 完整网站审计可同时启动最多 15 个专家代理。站点级审计可在几分钟内完成，而非数小时。
- **可证伪，非营销宣传。** 每条建议都附带其依赖的第一性原理观察、与其他建议的依赖关系、明确的“我们如何知道它失败了？”检查项，以及一个领先指标。详见 [Methodology](#methodology)。

> 使用 Codex 而非 Claude Code？请使用 [Codex SEO](https://github.com/AgriciDaniel/codex-seo)，它是面向 Codex 的移植版本，支持 TOML agent、插件打包、确定性运行器，并提供相同的 SEO 工作流界面。

## 适用人群

- **运营 5+ 个客户站点的 SEO 机构。** 用每周自动运行的审计取代季度深度审计。团队产能不变，审计频率提升 4 倍，每条建议都附带客户端可自行验证的可证伪性检查。
- **SaaS / 出版商 / 电商公司的内部 SEO 负责人。** 在高管评审前提供“第二双眼睛”。捕获 GSC（Google Search Console）和 Lighthouse 隐藏的问题：标记废弃、AI 引用缺口、过期域名遗产风险、寄生 SEO 暴露面、机器翻译漂移。
- **自由职业 SEO 顾问。** 通过 15 分钟审计和真实的 0-100 分数锚定首日客户范围。在花费一小时撰写提案之前，用具体的价值证明赢得项目合作。

![Claude SEO /seo 命令演示（Claude Code 终端）](screenshots/seo-command-demo.gif)

运行完整审计，观察并行代理如何向站点各部分发散：

![Claude SEO /seo audit 演示：并行子代理生成优先级行动清单](screenshots/seo-audit-demo.gif)

[在 YouTube 观看完整演示](https://www.youtube.com/watch?v=COMnNlUakQk)

## 目录

- [适用人群](#who-this-is-for)
- [安装](#installation)
- [快速开始](#quick-start)
- [命令](#commands)
- [功能特性](#features)
- [与手动/机构/商业工具对比](#compared-to-manual--agency--commercial-tools)
- [使用场景](#use-cases)
- [示例输出](#sample-output)
- [架构](#architecture)
- [方法论](#methodology)
- [v2 新增内容](#whats-new-in-v2)
- [局限性](#limitations)
- [环境要求](#requirements)
- [卸载](#uninstall)
- [扩展插件](#extensions)
- [生态系统](#ecosystem)
- [文档](#documentation)
- [常见问题 (FAQ)](#faq)
- [社区贡献者](#community-contributors)
- [许可证](#license)
- [参与贡献](#contributing)
- [作者](#author)

## 安装

> ℹ️ **你正在安装哪个版本？**
>
> - **公共开源版（默认）。** 以下命令将从 [`AgriciDaniel/claude-seo`](https://github.com/AgriciDaniel/claude-seo) 安装 —— MIT 协议，公开发布，无需会员资格。
> - **AI Marketing Hub Pro 会员？** 改用社区版本抢先体验：将 `AgriciDaniel/claude-seo` 替换为 `AI-Marketing-Hub/claude-seo`，并将插件标识符 `claude-seo@agricidaniel-claude-seo` 替换为 `claude-seo@ai-marketing-hub-claude-seo`。需要具有 `AI-Marketing-Hub` 组织访问权限的 `gh auth login`（或 PAT）。如果 `/plugin marketplace add` 返回 404，请在 [Skool 社区](https://www.skool.com/ai-marketing-hub-pro) 私聊以获取添加权限。

### 插件安装（Claude Code 1.0.33+）

最快的路径。一次性市场添加，然后安装插件：

```bash
/plugin marketplace add AgriciDaniel/claude-seo
/plugin install claude-seo@agricidaniel-claude-seo
```

### 手动安装（Unix / macOS / Linux）

```bash
git clone --depth 1 https://github.com/AgriciDaniel/claude-seo.git
bash claude-seo/install.sh
```

<details>
<summary>一键命令（curl，先审查再运行）</summary>

```bash
curl -fsSL https://raw.githubusercontent.com/AgriciDaniel/claude-seo/main/install.sh > install.sh
cat install.sh        # 运行前请审查内容
bash install.sh
rm install.sh
```

</details>

### Windows（PowerShell）

```powershell
git clone --depth 1 https://github.com/AgriciDaniel/claude-seo.git
powershell -ExecutionPolicy Bypass -File claude-seo\install.ps1
```

> **为什么使用 `git clone` 而不是 `irm | iex`？** Claude Code 自身的安全护栏将 `irm ... | iex` 标记为供应链风险：下载并执行未经验证的远程代码。`git clone` 方式允许你在运行前检查 `claude-seo\install.ps1`。

## 快速开始

```bash
# 启动 Claude Code
claude

# 完整网站审计：并行子代理生成优先级行动清单
/seo audit https://example.com

# 深度单页分析：页面元素、内容质量、标记
/seo page https://example.com/about

# Schema.org 标记审计：检测、验证、生成
/seo schema https://example.com

# AI 搜索优化：段落可引用性 + 原始来源对齐建议
/seo geo https://example.com

# 使用行业模板生成站点地图
/seo sitemap generate
```

## 命令

![Claude SEO 子技能生态系统：25 个模块分为 8 类（审计、内容、标记、技术、AI搜索、本地+地图、电商+国际、扩展），围绕中央编排器排列](assets/diagrams/03-sub-skill-map-B.svg)

编排器和 25 个子技能共提供 27 个用户可调用命令。完整参考见 [docs/COMMANDS.md](docs/COMMANDS.md)。

| 命令 | 描述 |
|---------|-------------|
| `/seo audit <url>` | 完整网站审计，并行子代理委派 |
| `/seo page <url>` | 深度单页分析 |
| `/seo technical <url>` | 跨 9 个类别的技术 SEO 审计 |
| `/seo content <url>` | E-E-A-T 和内容质量分析 |
| `/seo schema <url>` | 检测、验证和生成 Schema.org 标记 |
| `/seo geo <url>` | AI 摘要 / 生成式引擎优化（GEO） |
| `/seo sitemap <url \| generate>` | 分析或生成 XML 站点地图 |
| `/seo images <url>` | 图片优化分析 |
| `/seo plan <type>` | SEO 战略规划（saas、local、ecommerce、publisher、agency） |
| `/seo programmatic <url>` | 程序化 SEO 分析与规划 |
| `/seo competitor-pages <url>` | 竞争对手对比页面生成 |
| `/seo local <url>` | 本地 SEO 分析（GBP、引用、评论、地图包） |
| `/seo maps [command]` | 地图情报（地理网格、GBP 审计、评论、竞争对手） |
| `/seo hreflang <url>` | Hreflang / i18n SEO 审计与生成 |
| `/seo google [command]` | Google SEO API（GSC、PageSpeed、CrUX、Indexing、GA4、PDF 报告） |
| `/seo backlinks <url>` | 反向链接档案分析（Moz、Bing、Common Crawl） |
| `/seo cluster <keyword>` | 基于 SERP 的语义聚类 |
| `/seo sxo <url>` | 搜索体验优化（页面类型、用户故事、人物画像） |
| `/seo drift baseline \| compare \| history <url>` | 使用 SQLite 快照进行 SEO 漂移监控 |
| `/seo ecommerce <url>` | 电商 SEO 与市场情报 |
| `/seo flow [stage]` | FLOW 框架提示词（CC BY 4.0，证据驱动） |
| `/seo firecrawl [command] <url>` | 全站点爬取（扩展插件） |
| `/seo dataforseo [command]` | 实时 SEO 数据（扩展插件） |
| `/seo image-gen [use-case]` | AI 图片生成用于 SEO 素材（扩展插件） |

## 功能特性

### Claude SEO 检查哪些 Core Web Vitals？

Claude SEO 测量当前的三项核心网页指标：**LCP**（最大内容绘制，目标低于 2.5s）、**INP**（交互到下一次绘制，目标低于 200ms）和 **CLS**（累积布局偏移，目标低于 0.1）。[INP 于 2024 年 3 月 12 日取代了 FID](https://web.dev/articles/inp)；FID 已于 2024 年 9 月 9 日从所有 Chrome 工具（CrUX API、PageSpeed Insights、Lighthouse）中移除，Claude SEO 从未引用过 FID。现场数据在可用时来自 Chrome 用户体验报告（CrUX）；实验室数据则通过 PageSpeed Insights 回退到 Lighthouse。可通过 `/seo google` CrUX 集成将 LCP 分解为子部分（TTFB、加载延迟、加载时长、渲染延迟）以定位瓶颈。移动端和桌面端分别测量。CrUX History（25 周趋势）包含在 Tier 0 免费凭证集中。

### Claude SEO 如何评估 E-E-A-T？

E-E-A-T（经验、专业度、权威性、可信度）依据《搜索质量评定员指南》进行评估，该指南于 2025 年 9 月最新更新，YMYL（Your Money Your Life）已扩展至涵盖政治和社会话题。经验信号：原创研究、案例研究、一手照片。专业度：作者资质和主题深度。权威性：外部引用和品牌提及。可信度是四项中权重最高的：联系信息、安全 HTTPS、透明更正、日期戳。在评分子因素之前，Claude SEO 会应用 Google 自身的 Who / How / Why 启发式规则（出自 [helpful-content guide](https://developers.google.com/search/docs/fundamentals/creating-helpful-content)）。如果生成式 AI 内容符合搜索基本标准则没问题；当用于规模化低价值页面时才会被视为垃圾，`seo-content humanize` 和 `seo-content verify` 正是为此设计。

### Claude SEO 支持哪些 Schema.org 类型？

JSON-LD 是首选格式（Google 官方声明的偏好）。Claude SEO 检测、验证并生成以下活跃类型：Organization、LocalBusiness、Article、BlogPosting、NewsArticle、Product、ProductGroup、Offer、Review、AggregateRating、BreadcrumbList、WebSite、WebPage、Person、ProfilePage、ContactPage、VideoObject、ImageObject、Event、JobPosting、Course、DiscussionForumPosting、Reservation、OrderAction，以及视频和专用类型（BroadcastEvent、Clip、SeekToAction、SoftwareSourceCode）。受限：FAQ（自 2023 年 8 月起仅限政府和医疗权威站点）。已废弃且从不推荐：HowTo（富媒体结果于 2023 年 9 月移除）、SpecialAnnouncement（2025 年 7 月）、ClaimReview、VehicleListing、EstimatedSalary、LearningVideo、CourseInfo carousel（均于 2025 年 6 月退役）。替代指南：[skills/seo-schema/references/deprecated-types-2024-2026.md](skills/seo-schema/references/deprecated-types-2024-2026.md)。

### Claude SEO 如何针对 AI 搜索进行优化？

对齐 [Google AI 优化指南](https://developers.google.com/search/docs/fundamentals/ai-optimization-guide)，该指南指出 "AEO" 和 "GEO" 是 SEO 的重新包装标签。AI 摘要和 AI 模式基于与经典搜索相同的排名系统；页面必须被索引并具备片段展示资格才能出现在任何 AI 功能中。Claude SEO 对段落可引用性（最优为 134-167 字的自包含答案块）、基于问题的标题层级、归属密度、结构化数据覆盖度，以及跨 Wikipedia、Reddit、YouTube 和 LinkedIn 的实体存在进行评分。`seo-geo` 技能包含针对三个流行误解的证据驱动重构：llms.txt 目前并非引用杠杆（[原始来源证据](skills/seo-geo/references/llmstxt-evidence.md)）、无需内容分块，且 AI 特定关键词重写不必要，因为同义词理解已足够。

### Claude SEO 集成了哪些 Google SEO API？

采用 4 级凭证系统，让你从零密钥开始，按需添加数据。每个层级都在其级别上提供实际价值：

| 层级 | 凭证 | 解锁的 API |
|------|------|------|
| 0 | API key | PageSpeed Insights、CrUX、CrUX History（25 周趋势） |
| 1 | + OAuth 或服务账号 | + Search Console（查询、URL 检查、站点地图状态）、Indexing API |
| 2 | + GA4 属性配置 | + GA4 自然流量、顶级着陆页、设备/国家细分 |
| 3 | + Ads 开发者令牌 | + Keyword Planner 搜索量和竞争数据 |

PDF 报告通过 [WeasyPrint](https://weasyprint.org/)（A4 布局）生成，图表使用 matplotlib 以 200 DPI 渲染。运行 `/seo google setup` 获取凭证向导。所有凭证保存在 `~/.config/claude-seo/` 下，权限为 `0o600`；不会提交到仓库中。

### Claude SEO 如何处理本地 SEO？

三层架构。**Google Business Profile (GBP) 信号**：类别、营业时间、照片、帖子、产品、属性。**NAP（名称、地址、电话）一致性**：跨引用匹配主要目录，并标记偏差。**评论情报**：评分趋势、情感分析、回复覆盖率。对于多地点企业，Claude SEO 强制执行 30 页警告阈值和 50 页硬性停止以防止门页违规（可配置）。`/seo maps` 工作流添加地理网格排名跟踪、GBP 档案审计和竞争对手半径映射。本地标记生成覆盖 `LocalBusiness` 的所有必需和推荐属性（地理坐标、营业时间、areaServed）。Phase F (v2) 添加了 GBP 废弃检查器，检测退役的聊天字段引用和 `.business.site` URL。

## 与手动/机构/商业工具对比

| | 手动审计 | 机构合作 | 商业 SEO 审计工具 | **Claude SEO** |
|---|---|---|---|---|
| **每次审计耗时** | 4-8 小时（高级 SEO） | 1-3 周交付周期 | 10-45 分钟爬取+报告 | **10-15 分钟** |
| **成本** | 高（计费工时） | $2k-$15k+ 项目 | $99-$999/月订阅 | **免费技能 + Claude Code 订阅** |
| **可重复性** | 分析师之间不一致 | 合作之间不一致 | 是 | **是，确定性 + 可脚本化** |
| **输出格式** | 发现堆砌 PDF | 品牌幻灯片 | Web 仪表板、CSV 导出 | **Markdown + PDF + JSON，本地文件** |
| **自定义基准** | 分析师手动设置 | 机构特定框架 | 厂商固定 | **编辑本地 SKILL.md** |
| **数据离开机器？** | 否（你的表格） | 是（发送给机构） | 是（上传至厂商） | **默认完全本地化** |
| **锁定风险** | 无 | 高 | 高（数据退出摩擦） | **无。MIT，文件归你。** |
| **AI 搜索意识** | 依赖分析师能力 | 依赖机构资深程度 | 滞后（通常落后 6-12 个月） | **Google AI Optimization Guide (May 2026)、Sept 2025 QRG、INP-not-FID、GEO/AEO=SEO 重构、llms.txt 证据驱动立场** |
| **每项发现的可证伪性** | 无 | 无 | 无 | **有。每条建议附带“我们如何知道它失败了？”检查 + 领先指标** |

> 成本基准：手动审计假设高级 SEO 顾问按典型机构计费费率；机构合作基于常见的发现/审计交付范围；商业工具订阅反映 SEO 审计类别（Ahrefs、Semrush、Sitebulb、Screaming Frog）的公开中级定价。你的实际数字可能有所不同。

## 使用场景

**运营 10 个客户站点的 SEO 机构负责人。** 用每周周一早晨的 `/seo audit` 取代季度“深度审计”仪式。交付客户健康评分邮件的时间从 4 小时降至 12 分钟；覆盖范围从季度变为周度，且不增加计费工时。漂移基线捕获审计间的回归问题，使客户对话从“看看这个快照”转变为“这是本周的变化”。

**50 人 SaaS 公司的内部 SEO 负责人。** 在每次季度业务评审前 24 小时运行 `/seo audit`。捕获平台 UI 埋藏的项目（程序化页面上的损坏规范链、Google 2025 年 6 月退役潮后的标记废弃、侵蚀 SERP 到 AI 摘要采样的 AI 引用缺口、收购博客资产的过期域名遗产），在 CMO 向董事会质问自然流量下降前解决问题。

**自由职业 SEO 顾问为新客户入职。** 在发现通话中运行 `/seo audit`。用真实的 0-100 分数、3 个优先关键发现和每条建议的可证伪性检查来锚定合作范围，而不是模糊的“我会看看并回复你”。因为价值证明发生在通话期间而非提案之后，从而签下更多长期合同。

## 示例输出

Claude SEO 以真实的 Markdown 报告作为主要交付物。以下是 `/seo schema https://rankenstein.pro/about` 审计的前 ~50 行原文。插件实际生成的结构、标题和评分格式如下。

<details>
<summary><code>SCHEMA-REPORT.md</code>: 真实审计的前 50 行</summary>

```markdown
# Schema Markup Report: rankenstein.pro/about

**URL:** https://rankenstein.pro/about
**Date:** 2026-02-09
**Format Detected:** JSON-LD (3 blocks) | No Microdata | No RDFa

---

## Summary

| Metric | Value |
|--------|-------|
| **JSON-LD Blocks** | 3 |
| **Schema Types** | Organization, WebSite, SoftwareApplication |
| **Critical Issues** | 2 |
| **Warnings** | 5 |
| **Passed Checks** | 18 |
| **Overall Grade** | B+ (solid foundation, actionable gaps) |

---

## Existing Schema Validation

### 1. Organization (`@id: #organization`)

| Property | Value | Status | Notes |
|----------|-------|--------|-------|
| `@context` | https://schema.org | Valid | |
| `@type` | Organization | Valid | Active type |
| `@id` | https://rankenstein.pro#organization | Good | Enables cross-referencing |
| `name` | Rankenstein | Valid | |
| `description` | Present, 200+ chars | Good | Descriptive and keyword-rich |
| `url` | https://rankenstein.pro | Valid | Absolute URL |
| `logo` | ImageObject with @id, url, width, height, caption | Excellent | Well-structured |
| `foundingDate` | "2024" | Imprecise | Year-only accepted but ISO 8601 preferred |
| `areaServed` | "Worldwide" | Text | Works but `GeoShape` is more semantic |
| `contactPoint` | email + contactType | Valid | Consider adding `telephone` |
| `founder` | 1 Person (Daniel Agrici) | Incomplete | Page describes two co-founders; second missing |
| `sameAs` | 5 social profiles | Good | GitHub, X, LinkedIn, YouTube, Reddit |
| `knowsAbout` | 6 topics | Good | Relevant topical signals |

**Critical Issue:** The `founder` property only includes Daniel Agrici. Benjamin Samar (Co-Founder & Technical Director) is displayed on the page but absent from the schema. This creates a content-schema mismatch that can confuse search engines.
```

</details>

其他审计输出遵循相同结构：`FULL-AUDIT-REPORT.md`（总览审计）、`GEO-ANALYSIS.md`（AI 搜索就绪度）、`LOCAL-SEO-ANALYSIS.md`（GBP 和引用），以及通过 WeasyPrint + matplotlib 生成的生产级 PDF（封面、目录、执行摘要、数据部分、建议、方法论，完整站点审计约 32 页 A4）。

## 架构

![Claude SEO 系统架构：/seo audit 进入编排器，发散至 25 个子技能和 6 个并行审计代理，通过评分引擎收敛为优先级报告](assets/diagrams/01-architecture-B.svg)

该插件遵循 [Agent Skills 标准](https://docs.claude.com/en/docs/claude-code/skills)，采用三层架构（指令、编排、执行）。技能和代理从 `skills/seo-*/` 和 `agents/seo-*.md` 自动发现。编排器（`skills/seo/SKILL.md`）处理行业检测（SaaS、本地、电商、出版商、机构）、最多同时调度 15 个子代理，并通过 [10 原则框架](#methodology)进行综合后输出行动清单。完整架构：[docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)。

![Claude SEO 审计流水线：从 /seo audit 输入到站点爬取、并行代理调度、分数收集再到报告输出的线性流程](assets/diagrams/02-pipeline-A.svg)

## 方法论

![Claude SEO 10 原则思维框架：径向轮盘，包含 PERCEIVE（感知）、ANALYZE（分析）、VALIDATE（验证）、ACT（行动）四个阶段及按象限排列的 10 项原则](assets/diagrams/04-framework-B.svg)

每次审计遵循分为四个阶段的 10 项原则。每条发出的建议携带四个字段：其依赖的第一性原理观察、与其他建议的依赖关系、“我们如何知道它失败了？”检查项，以及用于监控的领先指标。

| 阶段 | 原则 | 作用 |
|---|---|---|
| **PERCEIVE（感知）** | OBSERVE (外部) · OBSERVE (内部) · LISTEN | 收集原始信号；审计自身假设；读取 SERP、品牌声音和社区的实际反馈 |
| **ANALYZE（分析）** | THINK · CONNECT (横向) · CONNECT (系统) | 还原至第一性原理；发现跨技能的非明显关联；排序为依赖图 |
| **VALIDATE（验证）** | FEEL · ACCEPT | 针对 UX、品牌声音、操作员容量进行压力测试；暴露可证伪性 |
| **ACT（行动）** | CREATE · GROW | 交付产物；设置下一轮审计的反馈循环 |

完整方法论：[skills/seo/references/thinking-framework.md](skills/seo/references/thinking-framework.md)。

## v2 新增内容

v2.0.0 是该插件历史上最大的版本。六个构建阶段，全部上线：

- **Phase A: 全量无头渲染。** 共享 `scripts/render_page.py`（Playwright Chromium + [trafilatura](https://github.com/adbar/trafilatura) + [htmldate](https://github.com/adbar/htmldate)）。每个审计子代理通过 `--render auto` 获得 SPA 感知抓取（自动检测 Next.js、React、Vue、Nuxt、Astro islands）。修复了限制 v1.x 的 SPA 局限。
- **Phase B: QRG 对齐的内容质量门控。** 填充物检测器和 AI 模式人性化模块基于 QRG §4.6.5 和 §4.6.6，含主张验证扫描器、通过 WHOIS 检查过期域名遗产、原始来源 Google 更新日志。
- **Phase C: 技术和 CWV 深度。** CrUX LCP 子部分（TTFB、加载延迟、加载时长、渲染延迟）、Speculation Rules 和 bfcache 检测、IndexNow 提交器用于 Bing / Yandex / Seznam / Naver、Unlighthouse 多页 Lighthouse 包装器。
- **Phase D: Schema 完整性。** 四个显式生成器（Reservation、OrderAction、DiscussionForumPosting、ProfilePage）、电商标记验证器（`hasMerchantReturnPolicy`、`shippingDetails`、MemberProgram、EU `energyEfficiencyClass`、ProductGroup 变体）、双验证器（Rich Results Test + Schema Markup Validator）。
- **Phase E: AI 搜索重构与 5 个新 MCP 扩展。** Ahrefs、SE Ranking（AI 声量份额）、Profound（LLM 引用追踪器）、Bing Webmaster + IndexNow、Unlighthouse。另含按 Google 2024 年 11 月 [网站声誉滥用政策](https://developers.google.com/search/blog/2024/11/site-reputation-abuse-update)的寄生 SEO 风险扫描器。
- **Phase F: 本地、国际化与隐私打磨。** GBP 废弃检查器（聊天字段、`.business.site` URL、Q&A）、DMA 同意模式 v2 点击诊断、按 2025 年 1 月 QRG 的机器翻译 QA 标记。

测试覆盖率：248 → 271（较 v1.9.9 基线增长 5.4 倍）。83 项 SSRF 和 DNS 重绑定绕过测试关闭了完整的混淆 IPv4、FQDN 尾部点、重定向重绑定绕过类。完整迁移说明和破坏性变更：[docs/MIGRATION-v1-to-v2.md](docs/MIGRATION-v1-to-v2.md)。

![Claude SEO 路线图：从 v1.7.0 Google API 到 v2.0.0 AI 搜索与 10 原则框架（当前）再到 v3.0.0 audit-as-code 的水平时间轴](assets/diagrams/05-roadmap-A.svg)

## 局限性

值得提前说明的两个真实边界。

**重度客户端渲染时机。** Phase A 的无头渲染器开箱处理大多数 SPA（`--render auto` 检测空 `<div id="root">` 外壳并切换至 Playwright）。仍会产生噪音发现的边缘情况：与折叠后滚动位置绑定的渲染页面、用户交互后抓取关键内容的页面（模态框打开、标签点击）、易受竞态条件影响的第三方组件挂载。针对这些，手动触发 `seo-visual` 子代理并将其 Playwright 快照与原始 HTML 子代理的发现进行对比是推荐的工作流。

**本地化但无数据增强。** 免费层级不调用任何外部 API，输出零网络请求。添加 Google API 凭证（Tier 0 至 3）可解锁真实现场数据和实时索引状态；否则 Core Web Vitals 仅为实验室估算，索引状态从页面级信号推断。添加 MCP 扩展（Ahrefs、DataForSEO、SE Ranking、Profound）同样会解锁竞争和 AI 引用数据，但需要各自的账户凭证。

## 环境要求

- Python 3.10+
- Claude Code CLI
- 可选：Playwright Chromium（由 `install.sh` 自动安装）用于 SPA 渲染和截图
- 可选：Google API 凭证以获取增强的 CWV / GSC / GA4 数据（见 `/seo google setup`）

## 卸载

```bash
git clone --depth 1 https://github.com/AgriciDaniel/claude-seo.git
bash claude-seo/uninstall.sh
```

<details>
<summary>一键命令（curl）</summary>

```bash
curl -fsSL https://raw.githubusercontent.com/AgriciDaniel/claude-seo/main/uninstall.sh | bash
```

</details>

## 扩展插件

可选的 MCP 服务器为审计流水线添加实时数据。Claude SEO 提供 8 个服务器的扩展；插件核心无需任何扩展即可工作。

### DataForSEO

实时 SERP 数据、关键词研究、反向链接、页面内分析、内容分析、商业列表、AI 可见性检查和 LLM 引用追踪。跨 9 个 API 模块的 22 条命令。

```bash
./extensions/dataforseo/install.sh   # 需要 DataForSEO 账户
/seo dataforseo serp best coffee shops
/seo dataforseo ai-mentions your brand
```

完整 DataForSEO 文档：[extensions/dataforseo/README.md](extensions/dataforseo/README.md)。

### Firecrawl

通过 [Firecrawl](https://www.firecrawl.dev/) MCP 服务器进行全站点爬取和 URL 发现。

```bash
./extensions/firecrawl/install.sh
/seo firecrawl crawl https://example.com
```

完整 Firecrawl 文档：[extensions/firecrawl/README.md](extensions/firecrawl/README.md)。

### Banana: AI 图片生成

通过 [Claude Banana](https://github.com/AgriciDaniel/banana-claude) Creative Director 流水线进行 SEO 图片生成（OG 预览、博客头图、产品照片、信息图）。

```bash
./extensions/banana/install.sh
/seo image-gen og "Professional SaaS dashboard"
```

完整 Banana 文档：[extensions/banana/README.md](extensions/banana/README.md)。

### Ahrefs, SE Ranking, Profound, Bing Webmaster, Unlighthouse (v2 新增)

Phase E 添加的五个扩展：

- **Ahrefs：** 官方 `@ahrefs/mcp` 服务器，含反向链接和自然数据
- **SE Ranking：** ChatGPT、Gemini、Perplexity、AI Overviews、AI Mode 跨平台的 AI 声量份额
- **Profound：** 带时间序列数据的 LLM 引用追踪器
- **Bing Webmaster：** Bing Webmaster Tools + IndexNow 统一接口
- **Unlighthouse：** MIT 许可的多页 Lighthouse 运行器

设置指南：[docs/MCP-INTEGRATION.md](docs/MCP-INTEGRATION.md)。

## 生态系统

Claude SEO 是一组可良好互操作的 Claude Code 技能家族的一部分：

| 技能 | 功能 | 连接方式 |
|-------|-------------|-----------------|
| [Claude SEO](https://github.com/AgriciDaniel/claude-seo) | SEO 分析、审计、标记、GEO | 核心。分析站点并生成行动清单。 |
| [Claude Blog](https://github.com/AgriciDaniel/claude-blog) | 博客撰写、优化、评分 | 伴侣。根据 SEO 发现撰写优化的内容。 |
| [Claude Banana](https://github.com/AgriciDaniel/banana-claude) | 通过 Gemini 进行 AI 图片生成 | 共享。为 SEO 素材和博客文章生成图片。 |
| [Codex SEO](https://github.com/AgriciDaniel/codex-seo) | Codex 优先的 SEO 技能套件 | 移植版。适配 Codex 技能、TOML agent、确定性运行器的相同 SEO 系统。 |
| [AI Marketing Claude](https://github.com/zubair-trabzada/ai-marketing-claude) | 文案、邮件、社交、广告、漏斗、CRO | 社区。基于 SEO 发现的审计后营销行动。 |
| [FLOW](https://github.com/AgriciDaniel/flow) | 证据驱动的 SEO 框架（41 个 AI 提示词，CC BY 4.0） | 知识库。驱动 `seo-flow` 提示词。 |

**工作流示例：**

1. `/seo audit https://example.com`: 识别内容缺口和技术问题
2. `/seo backlinks https://example.com`: 分析链接档案和竞争对手差距
3. `/seo geo https://example.com/blog/post`: 评分 AI 引用就绪度
4. `/blog write "target keyword"`: 创建 SEO 优化博客文章（Claude Blog）
5. `/seo image-gen hero "blog topic"`: 生成头图（Banana 扩展）

## 文档

- [安装指南](docs/INSTALLATION.md)
- [命令参考](docs/COMMANDS.md): 27 条命令详解
- [架构](docs/ARCHITECTURE.md): 三层设计、自动发现、并行调度
- [迁移 v1 → v2](docs/MIGRATION-v1-to-v2.md): 破坏性变更、六阶段工作流
- [MCP 集成](docs/MCP-INTEGRATION.md): 全部 8 个服务器的扩展设置
- [故障排除](docs/TROUBLESHOOTING.md)
- [贡献者](CONTRIBUTORS.md): 社区致谢

## FAQ

### Claude SEO 是什么？

Claude SEO 是 [Claude Code](https://claude.ai/claude-code) 的开源 SEO 分析插件。它在技术 SEO、内容质量（E-E-A-T）、Schema.org 标记、AI 搜索优化（GEO）、本地 SEO、电商和国际化 SEO 等领域并行运行 25 个子技能和 18 个专家代理。审计生成优先级行动清单，其中每条建议都附带其依赖的第一性原理观察、与其他建议的依赖关系、“我们如何知道它失败了？”检查项，以及一个领先指标。该插件采用 MIT 许可，零专有跟踪，若跳过可选的 Google API 和 MCP 扩展增强则可完全离线工作。对齐 [Google AI 优化指南](https://developers.google.com/search/docs/fundamentals/ai-optimization-guide) 及 2025 年 9 月《质量评定员指南》。

### Claude SEO 与 Screaming Frog 或 Ahrefs Site Audit 有何不同？

不同的作用域，不同的权衡。**Screaming Frog** 在链接图级别爬取更深更快；它是专为爬虫设计的工具，Claude SEO 并不试图取代它。**Ahrefs Site Audit** 带来专有的反向链接索引和链接情报；Claude SEO 通过其 MCP 扩展与 Ahrefs 集成而非竞争。Claude SEO 的优势在于：对话式 LLM 原生工作流、建议可证伪性（每项发现附带明确的失败模式检查）、开源 MIT 许可且零域名定价、对齐 Google 原始指南的 AI 搜索优化，以及基于原始来源的标记废弃追踪。用 Screaming Frog 或 Ahrefs 发挥它们的最强项；当你需要 LLM 驱动的整合、对话式迭代和 AI 搜索优先审计（与你的其他 Claude Code 工作流在同一环境）时，使用 Claude SEO。

### Claude SEO 是否支持单页应用（Next.js, React, Vue）？

支持。v2 的 Phase A 上线了共享无头渲染器（`scripts/render_page.py`），后端为 Playwright Chromium。每个抓取子代理均支持 `--render auto`（默认值），可自动检测 SPA 特征（空 `<div id="root">` 外壳、单 bundle 脚本、水合标记）并切换至渲染抓取。设置 `--render always` 强制渲染，或 `--render never` 仅获取原始 HTML。内容提取使用 [trafilatura](https://github.com/adbar/trafilatura) 进行样板代码移除。发布日期来自 [htmldate](https://github.com/adbar/htmldate)。已知细节：带有滚动绑定水合或交互后内容抓取的页面仍会产生噪音发现；详见 [局限性](#limitations) 部分中针对这些边缘情况的 `seo-visual` 交叉检查工作流建议。

### Claude SEO 使用哪些 Google API，它们是必需的吗？

均非必需。Claude SEO 在零 API 密钥下完全可用。4 级凭证系统让你逐步升级：Tier 0（仅 API key）解锁 PageSpeed Insights、CrUX 和 CrUX History（25 周趋势数据）。Tier 1（+ OAuth 或服务账号）添加 Search Console，含查询、URL 检查、站点地图状态和 Indexing API。Tier 2（+ GA4 属性配置）添加自然流量、顶级着陆页和设备/国家细分。Tier 3（+ Ads 开发者令牌）添加 Keyword Planner 搜索量和竞争数据。凭证设置向导通过 `/seo google setup` 运行。所有凭证保存在 `~/.config/claude-seo/` 下，文件权限为 `0o600`；不会提交到仓库中，且除 Google 自身端点外不传输任何数据。

### Claude SEO 免费吗？

是的。MIT 许可，完全开源，无按域名定价，无遥测数据，插件本身不施加 API 配额限制。核心插件和全部 25 个子技能无需任何付费服务即可工作。部分可选 MCP 扩展包装了付费服务（DataForSEO、Ahrefs、Profound、SE Ranking），需自带账户凭证；使用为可选项，无它们插件仍可完全运行。Google API（PageSpeed Insights、Search Console、Indexing、GA4）由 Google 免费提供，受正常账户配额限制且需你自己的凭证。如果你想要商业支持或超出开源插件的企业级功能，这不属于本项目范围。

### Claude SEO 在 AI 搜索方面与传统 SEO 工具有何不同？

大多数 SEO 工具将 AI 搜索视为独立的优化学科。Claude SEO 遵循 [Google 的官方立场](https://developers.google.com/search/docs/fundamentals/ai-optimization-guide)，即 AEO 和 GEO 是 SEO 的重新包装标签。AI 摘要和 AI 模式基于与经典搜索相同的排名系统；资格门槛为常规索引。Claude SEO 对段落可引用性（134-167 字自包含答案块）、基于问题的标题层级、归属密度，以及跨 Wikipedia、Reddit、YouTube 和 LinkedIn 的实体存在进行评分。它明确驳斥三个网红误解：将 llms.txt 作为引用杠杆、为 AI 分块内容、AI 特定关键词重写。对于电商站点，Claude SEO 按 Google Merchant Center 政策审计 AI 生成产品图上的 IPTC `TrainedAlgorithmicMedia` 要求。

## 社区贡献者

v1.9.0 包含来自 [AI Marketing Hub](https://www.skool.com/ai-marketing-hub) Pro Hub Challenge 的贡献：

| 贡献者 | 贡献内容 |
|------------|-------------|
| **Lutfiya Miller**（冠军） | Semantic Cluster Engine → `seo-cluster` |
| **Florian Schmitz** | SXO Skill → `seo-sxo` |
| **Dan Colta** | SEO Drift Monitor → `seo-drift` |
| **Chris Muller** | 多语言 SEO → `seo-hreflang` 增强 |
| **Matej Marjanovic** | 电商 + DataForSEO 成本配置 → `seo-ecommerce` + 成本护栏 |

完整详情及原始仓库链接见 [CONTRIBUTORS.md](CONTRIBUTORS.md)。

## 许可证

MIT License。详见 [LICENSE](LICENSE)。

## 参与贡献

欢迎贡献。请在提交 PR 前阅读 [CONTRIBUTING.md](CONTRIBUTING.md)。项目强制执行每 PR 审计门禁，涵盖清单一致性（14 项断言）、测试套件（271 项通过）以及合并至 `main` 前的 8 维度安全审查。

---

## 作者

由 **[Agrici Daniel](https://agricidaniel.com/about)** 构建，AI 工作流架构师。单一维护者，欢迎通过 [Pro Skool community](https://www.skool.com/ai-marketing-hub-pro) 参与社区贡献。背景涵盖营销自动化、AI 辅助内容工作流及 Claude Code 开源工具链。

- [博客](https://agricidaniel.com/blog): AI 营销自动化深度解析
- [AI Marketing Hub (免费)](https://www.skool.com/ai-marketing-hub): 开放社区
- [AI Marketing Hub Pro](https://www.skool.com/ai-marketing-hub-pro): Pro 社区，抢先体验本技能
- [YouTube](https://www.youtube.com/@AgriciDaniel): 教程与演示
- [GitHub](https://github.com/AgriciDaniel): 全部开源工具
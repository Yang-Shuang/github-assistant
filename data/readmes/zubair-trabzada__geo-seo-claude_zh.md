<p align="center">
  <img src="assets/banner.svg" alt="GEO-SEO Claude Code 技能" width="900"/>
</p>

<p align="center">
  <strong>GEO优先，SEO辅助。</strong> 在保持传统SEO基础的同时，针对AI搜索引擎<br/>
  （ChatGPT、Claude、Perplexity、Gemini、Google AI概览）优化网站。
</p>

<p align="center">
  AI搜索正在取代传统搜索。本工具针对流量流向进行优化，而非过去的位置。
</p>

---

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=zubair-trabzada/geo-seo-claude&type=Date)](https://www.star-history.com/#zubair-trabzada/geo-seo-claude&Date)

---

## 为什么 GEO 很重要（2026）

| 指标 | 数值/说明 |
|--------|-------|
| GEO服务市场规模 | $8.5亿+（预计2031年达$73亿） |
| AI引荐流量增长 | 同比增长 +527% |
| AI流量转化率对比自然搜索 | 高出 4.4倍 |
| Gartner预测：到2028年搜索流量下降 | -50% |
| 对AI而言，品牌提及与反向链接的相关性 | 强3倍 |
| 投资GEO的营销人员比例 | 仅 23% |

---

## 快速开始

### 一键安装（macOS/Linux）

```bash
curl -fsSL https://raw.githubusercontent.com/zubair-trabzada/geo-seo-claude/main/install.sh | bash
```

### 手动安装

```bash
git clone https://github.com/zubair-trabzada/geo-seo-claude.git
cd geo-seo-claude
./install.sh
```

### Windows（Git Bash）

需要 [Windows版 Git](https://git-scm.com/downloads)，其中包含 Git Bash。

```bash
# Option 1: One-command install (run from Git Bash, not PowerShell/CMD)
curl -fsSL https://raw.githubusercontent.com/zubair-trabzada/geo-seo-claude/main/install-win.sh | bash

# Option 2: Manual install
git clone https://github.com/zubair-trabzada/geo-seo-claude.git
cd geo-seo-claude
./install-win.sh
```

> **注意：** 右键文件夹并选择“在此打开 Git Bash”，或打开 Git Bash 后导航至该目录。请勿使用 PowerShell 或命令提示符（CMD）。

### 环境要求

- Python 3.8+（Debian/Ubuntu 还需安装 `python3-venv`）
- Claude Code CLI
- Git
- 可选：[`uv`](https://docs.astral.sh/uv/) — 若已存在，安装程序将使用它来加速依赖安装
- 可选：Playwright（用于截图）

### 独立环境安装

Python 依赖项会安装在独立的虚拟环境中 `~/.claude/skills/geo/.venv/`。你的系统 Python **不会**受到影响，卸载该技能时会一并删除该虚拟环境及所有相关文件。

技能和代理文件直接引用了该虚拟环境，因此无论你的 `PATH` 中 `python3` 指向何处，工具均可正常运行。

---

## 命令

打开 Claude Code 并使用以下命令：

| Command | What It Does |
|---------|-------------|
| `/geo audit <url>` | 完整GEO + SEO审计，并行子代理运行 |
| `/geo quick <url>` | 60秒GEO可见性快照 |
| `/geo citability <url>` | 评估内容对AI引用的准备度 |
| `/geo crawlers <url>` | 检查AI爬虫访问权限（robots.txt） |
| `/geo llmstxt <url>` | 分析或生成 llms.txt |
| `/geo brands <url>` | 扫描AI引用平台上的品牌提及 |
| `/geo platforms <url>` | 平台专属优化建议 |
| `/geo schema <url>` | 结构化数据分析与生成 |
| `/geo technical <url>` | 技术SEO审计 |
| `/geo content <url>` | 内容质量与E-E-A-T评估 |
| `/geo report <url>` | 生成面向客户的GEO报告 |
| `/geo report-pdf` | 生成包含图表与可视化的专业PDF报告 |

---

## 架构

```
geo-seo-claude/
├── geo/                          # Main skill orchestrator
│   └── SKILL.md                  # Primary skill file with commands & routing
├── skills/                       # 13 specialized sub-skills
│   ├── geo-audit/                # Full audit orchestration & scoring
│   ├── geo-citability/           # AI citation readiness scoring
│   ├── geo-crawlers/             # AI crawler access analysis
│   ├── geo-llmstxt/              # llms.txt standard analysis & generation
│   ├── geo-brand-mentions/       # Brand presence on AI-cited platforms
│   ├── geo-platform-optimizer/   # Platform-specific AI search optimization
│   ├── geo-schema/               # Structured data for AI discoverability
│   ├── geo-technical/            # Technical SEO foundations
│   ├── geo-content/              # Content quality & E-E-A-T
│   ├── geo-report/               # Client-ready markdown report generation
│   ├── geo-report-pdf/           # Professional PDF report with charts
│   ├── geo-prospect/             # CRM-lite prospect pipeline management
│   ├── geo-proposal/             # Auto-generate client proposals
│   └── geo-compare/              # Monthly delta tracking & progress reports
├── agents/                       # 5 parallel subagents
│   ├── geo-ai-visibility.md      # GEO audit, citability, crawlers, brands
│   ├── geo-platform-analysis.md  # Platform-specific optimization
│   ├── geo-technical.md          # Technical SEO analysis
│   ├── geo-content.md            # Content & E-E-A-T analysis
│   └── geo-schema.md             # Schema markup analysis
├── scripts/                      # Python utilities
│   ├── fetch_page.py             # Page fetching & parsing
│   ├── citability_scorer.py      # AI citability scoring engine
│   ├── brand_scanner.py          # Brand mention detection
│   ├── llmstxt_generator.py      # llms.txt validation & generation
│   └── generate_pdf_report.py    # PDF report generator (ReportLab)
├── schema/                       # JSON-LD templates
│   ├── organization.json         # Organization schema (with sameAs)
│   ├── local-business.json       # LocalBusiness schema
│   ├── article-author.json       # Article + Person schema (E-E-A-T)
│   ├── software-saas.json        # SoftwareApplication schema
│   ├── product-ecommerce.json    # Product schema with offers
│   └── website-searchaction.json # WebSite + SearchAction schema
├── install.sh                    # One-command installer
├── uninstall.sh                  # Uninstaller
├── requirements.txt              # Python dependencies
└── README.md                     # This file
```

---

## 数据存储

CRM和报告功能模块（`/geo prospect`、`/geo proposal`、`/geo compare`）将运行时数据存储于Claude Code目录之外：

```
~/.geo-prospects/
├── prospects.json              # Client/prospect pipeline data
├── proposals/                  # Generated proposal documents
│   └── <domain>-proposal-<date>.md
└── reports/                    # Monthly delta reports
    └── <domain>-monthly-<YYYY-MM>.md
```

该目录**不会**被卸载程序删除——若不再需要你的潜在客户数据，请手动将其删除。

---

## 工作原理

### 完整审计流程

当你运行 `/geo audit https://example.com` 时：

1. **发现阶段** — 抓取首页、识别业务类型、爬取站点地图
2. **并行分析** — 同时启动5个子代理：
   - AI可见性（引用准备度、爬虫权限、llms.txt、品牌提及）
   - 平台分析（ChatGPT、Perplexity、Google AIO 就绪情况）
   - 技术SEO（Core Web Vitals、SSR、安全性、移动端适配）
   - 内容质量（E-E-A-T、可读性、时效性）
   - Schema标记（检测、验证、生成）
3. **综合评估** — 聚合各项得分，生成综合GEO评分（0-100）
4. **报告输出** — 输出优先级行动清单及快速见效建议

### 评分方法论

| 类别 | 权重 |
|----------|--------|
| AI引用准备度与可见性 | 25% |
| 品牌权威信号 | 20% |
| 内容质量与E-E-A-T | 20% |
| 技术基础 | 15% |
| 结构化数据 | 10% |
| 平台优化 | 10% |

---

## 核心功能

### 引用就绪度评分 (Citability Scoring)
分析内容块对AI引用的准备情况。最适合被AI引用的段落长度为134-167词，需结构完整、事实丰富且直接回答问题。

### AI爬虫分析
检查 robots.txt 是否允许14+种AI爬虫（GPTBot、ClaudeBot、PerplexityBot等）访问，并提供具体的放行/拦截建议。

### 品牌提及扫描
对AI而言，品牌提及与可见性的相关性是反向链接的3倍。该功能会扫描 YouTube、Reddit、Wikipedia、LinkedIn 及7+其他平台。

### 平台专属优化
针对同一查询，仅有11%的网站能同时被 ChatGPT 和 Google AI概览 引用。本工具提供按平台定制的建议。

### llms.txt 文件生成
自动生成新兴的 `llms.txt` 标准文件，帮助AI爬虫理解你的网站结构。

### 面向客户的报告 (Client-Ready Reports)
生成专业的 Markdown 或 PDF 格式GEO报告。PDF报告包含评分仪表盘、柱状图、平台就绪度可视化、颜色编码表格及优先级行动清单——开箱即用，可直接交付客户。

---

## 使用场景

- **GEO代理机构** — 执行客户审计并生成交付物
- **营销团队** — 监控并提升AI搜索可见性
- **内容创作者** — 优化内容以适配AI引用
- **本地企业** — 让AI助手更容易发现你
- **SaaS公司** — 提升跨平台实体识别能力
- **电商企业** — 针对AI购物推荐优化商品页

---

## 卸载

```bash
./uninstall.sh
```

或手动删除：
```bash
rm -rf ~/.claude/skills/geo ~/.claude/skills/geo-* ~/.claude/agents/geo-*.md
```

---

## 如何将其转化为业务？

该工具免费。学习如何从中盈利，正是社区发挥作用的地方。

**[加入AI工作坊社区 →](https://skool.com/aiworkshop)**

你将获得：
- **视频操作指南** — 逐步设置、运行审计、解读结果
- **客户获取手册** — 如何寻找潜在客户、推介GEO服务并促成交易
- **实时办公时间** — 带上你的审计结果，获取直接指导
- **GEO代理定价与模板** — 提案文档、冷启动外呼话术、入职工作流

GEO代理机构月费在$2K–$12K之间。本工具负责执行审计。社区教你如何进行销售。

---





## 许可证

MIT 许可证

---

## 贡献指南

欢迎提交贡献！

---

专为AI搜索时代打造。
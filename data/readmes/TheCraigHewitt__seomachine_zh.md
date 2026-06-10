# SEO Machine

一个专为创建面向任何企业的长篇幅、SEO 优化博客内容而设计的 Claude Code 工作区。该系统帮助你研究、撰写、分析和优化能够排名靠前并服务于目标受众的内容。

## 概述

SEO Machine 基于 Claude Code 构建，提供：
- **自定义命令**：`/research`、`/write`、`/rewrite`、`/analyze-existing`、`/optimize`、`/performance-review`、`/publish-draft`、`/article`、`/priorities`，以及专门的研究和落地页（landing page）相关命令
- **专用 Agent**：Content Analyzer、SEO Optimizer、Meta Creator、Internal Linker、Keyword Mapper、Editor、Performance Analysis、Headline Generator、CRO Analyst、Landing Page Optimizer
- **营销技能**：26 项用于文案撰写、转化率优化（CRO）、A/B 测试、邮件序列、定价策略等的营销技能
- **高级 SEO 分析**：搜索意图检测、关键词密度与聚类、内容长度对比、可读性评分、SEO 质量评级（0-100）
- **数据集成**：Google Analytics 4 (GA4)、Google Search Console (GSC)、DataForSEO，提供实时性能洞察
- **上下文驱动**：品牌语调、风格指南、SEO 规范及示例将指导所有内容生成
- **工作流组织**：为主题（topics）、研究资料、草稿和已发布内容提供结构化的目录

## 快速开始

### 前置条件
- [Claude Code](https://claude.com/claude-code) 已安装
- Anthropic API 账户

### 安装步骤

1. 克隆本仓库：
```bash
git clone https://github.com/TheCraigHewitt/seomachine.git
cd seomachine
```

2. 为分析模块安装 Python 依赖项：
```bash
pip install -r data_sources/requirements.txt
```

此命令将安装：
- Google Analytics/Search Console 集成模块
- DataForSEO API 客户端
- NLP 库（nltk, textstat）
- 机器学习工具（scikit-learn）
- 网页抓取工具（beautifulsoup4）

3. 在 Claude Code 中打开项目：
```bash
claude-code .
```

4. **自定义上下文文件**（重要！）：

   所有上下文文件均以模板形式提供。请填入你公司的相关信息：

   - `context/brand-voice.md` - 定义你的品牌语调与核心信息 *(参考 examples/castos/ 中的示例)*
   - `context/writing-examples.md` - 添加 3-5 篇来自你站点的优秀博客文章作为范例
   - `context/features.md` - 列出产品/服务的功能与优势
   - `context/internal-links-map.md` - 映射用于内部链接的关键页面
   - `context/style-guide.md` - 填写你的排版与风格偏好
   - `context/target-keywords.md` - 添加关键词研究与主题聚类数据
   - `context/competitor-analysis.md` - 添加竞争对手分析与洞察
   - `context/seo-guidelines.md` - 审查并调整 SEO 要求

   **快速上手**：查看 `examples/castos/`，了解一个播客托管 SaaS 公司如何完整填写所有上下文文件的真实案例。

## 工作流

### 创建新内容

#### 1. 从研究开始
```
/research [topic]
```

**作用**：
- 执行关键词研究
- 分析前 10 名竞争对手
- 识别内容缺口（Content Gaps）
- 生成综合研究报告
- 保存至 `/research/` 目录

**示例**：
```
/research content marketing strategies for B2B SaaS
```

#### 2. 撰写文章
```
/write [topic or research brief]
```

**作用**：
- 创建 2000-3000+ 词的 SEO 优化长文
- 保持 `context/brand-voice.md` 中定义的品牌语调
- 自然融入关键词
- 包含内部链接与外部权威链接
- 提供元数据元素（标题、描述、关键词）
- 自动触发优化 Agent
- 保存至 `/drafts/` 目录

**示例**：
```
/write content marketing strategies for B2B SaaS
```

**Agent 自动执行**：
撰写完成后，以下 Agent 将自动分析内容：
- **SEO Optimizer**：页内 SEO 优化建议
- **Meta Creator**：多组元标题/描述选项
- **Internal Linker**：具体的内部链接建议
- **Keyword Mapper**：关键词布局与密度分析

#### 3. 最终优化
```
/optimize [article file]
```

**作用**：
- 全面 SEO 审计
- 验证所有元素是否符合要求
- 提供最终润色建议
- 生成发布就绪度评分
- 输出优化报告

**示例**：
```
/optimize drafts/content-marketing-strategies-2025-10-29.md
```

### 更新现有内容

#### 1. 分析现有文章
```
/analyze-existing [URL or file path]
```

**作用**：
- 抓取并分析当前内容
- 评估 SEO 表现
- 识别过时信息
- 评估竞争定位
- 提供内容健康度评分（0-100）
- 推荐更新优先级与范围
- 将分析报告保存至 `/research/` 目录

**示例**：
```
/analyze-existing https://yoursite.com/blog/marketing-guide
/analyze-existing published/marketing-guide-2024-01-15.md
```

#### 2. 重写/更新内容
```
/rewrite [topic or analysis file]
```

**作用**：
- 根据分析结果更新内容
- 刷新统计数据与案例
- 提升 SEO 优化程度
- 补充缺失的新章节
- 保留原稿中有效的部分
- 记录所有修改痕迹
- 保存至 `/rewrites/` 目录

**示例**：
```
/rewrite marketing guide
```

## 命令参考

### `/research [topic]`
针对新内容执行全面的关键词与竞品研究。

**输出**：研究报告位于 `/research/brief-[topic]-[date].md`

**包含**：
- 核心词与长尾词
- 竞争对手分析（前 10 名）
- 内容缺口与机会点
- 推荐大纲结构
- 内部链接策略
- 元数据元素预览

---

### `/write [topic]`
创建长篇幅 SEO 优化文章（2000-3000+ 词）。

**输出**：文章位于 `/drafts/[topic]-[date].md`

**包含**：
- 完整文章结构（H1/H2/H3）
- SEO 优化正文
- 内部与外部链接
- 元数据元素（标题、描述、关键词）
- SEO 检查清单

**自动触发**：
- SEO Optimizer Agent
- Meta Creator Agent
- Internal Linker Agent
- Keyword Mapper Agent

---

### `/rewrite [topic]`
更新并改进现有内容。

**输出**：更新后的文章位于 `/rewrites/[topic]-rewrite-[date].md`

**包含**：
- 重写/更新的内容正文
- 修改摘要
- 前后对比表
- 更新的 SEO 元素

---

### `/analyze-existing [URL or file]`
分析现有博客文章以发现优化机会。

**输出**：分析报告位于 `/research/analysis-[topic]-[date].md`

**包含**：
- 内容健康度评分（0-100）
- 快速改进项（Quick Wins）
- 战略性改进建议
- 重写优先级与范围评估
- 用于重写的研究简报

---

### `/optimize [file]`
发布前的最终 SEO 优化检查。

**输出**：优化报告位于 `/drafts/optimization-report-[topic]-[date].md`

**包含**：
- SEO 评分（0-100）
- 高优先级修复项
- 快速改进项
- 元数据元素选项
- 链接增强建议
- 发布就绪度评估

---

### `/publish-draft [file]`
通过 REST API 将文章发布至 WordPress，并同步 Yoast SEO 元数据。

---

### `/article [topic]`
简化的文章创建工作流。

---

### `/priorities`
基于分析数据的优先级矩阵，用于识别影响力最大的内容任务。

---

### `/scrub [file]`
移除 AI 生成内容的痕迹与模式（如破折号、填充词、机械句式）。

---

### 研究类命令

| Command | Description |
|---------|-------------|
| `/research-serp [keyword]` | 针对目标关键词的 SERP 分析 |
| `/research-gaps` | 竞争对手内容缺口分析 |
| `/research-trending` | 热门趋势机会挖掘 |
| `/research-performance` | 基于性能数据的内容优先级排序 |
| `/research-topics` | 主题聚类研究 |

---

### 落地页（Landing Page）命令

| Command | Description |
|---------|-------------|
| `/landing-write [topic]` | 创建转化率优化的落地页 |
| `/landing-audit [file]` | 审计落地页的 CRO 问题 |
| `/landing-research [topic]` | 研究竞争对手与定位策略 |
| `/landing-competitor [URL]` | 深度分析竞品落地页 |
| `/landing-publish [file]` | 将落地页发布至 WordPress |

## Agent（智能体）

自动分析内容并提供专业建议的专用 Agent。

### Content Analyzer (NEW!)
**用途**：基于数据的全面内容分析，使用 5 个专项模块

**分析维度**：
- 搜索意图分类（信息型/导航型/交易型/商业型）
- 关键词密度与聚类及主题检测
- 与顶级 SERP 竞争对手的内容长度对比
- 可读性评分（Flesch Reading Ease、Flesch-Kincaid Grade Level）
- SEO 质量评级（0-100 分，含分类明细）
- 关键词堆砌风险检测
- 被动语态比例与句子复杂度分析
- 按章节划分的关键词分布热力图

**输出**：
- 包含发布就绪度评估的执行摘要
- 优先级行动计划（关键/高优/优化级）
- 竞争定位分析
- 各分析维度的详细建议
- 用于改进的具体指标与基准数据

**底层驱动**：
- `search_intent_analyzer.py` - 搜索意图检测
- `keyword_analyzer.py` - 关键词密度、聚类、LSI 关键词
- `content_length_comparator.py` - SERP 竞品分析
- `readability_scorer.py` - 多维度可读性指标
- `seo_quality_rater.py` - 综合 SEO 评分

---

### SEO Optimizer
**用途**：页内 SEO 分析与优化建议

**分析维度**：
- 关键词优化与密度分布
- 内容结构与标题层级
- 内部链接与外部链接
- 元数据元素（Meta Elements）
- 可读性与用户体验
- 精选摘要（Featured Snippet）机会点

**输出**：SEO 评分（0-100）及具体改进建议

---

### Meta Creator
**用途**：生成高转化率的元标题与描述

**生成内容**：
- 5 组元标题变体（50-60 字符）
- 5 组元描述变体（150-160 字符）
- A/B 测试建议
- SERP 预览效果
- 转化导向的文案

**输出**：多选项对比，附带推荐意见与理由

---

### Internal Linker
**用途**：战略性内部链接建议

**提供内容**：
- 3-5 条具体内部链接建议
- 精确插入位置
- 锚文本（Anchor Text）推荐
- 用户路径映射
- SEO 影响预测

**参考文件**：`context/internal-links-map.md`

---

### Keyword Mapper
**用途**：关键词布局与整合分析

**分析维度**：
- 关键词密度与分布情况
- 关键位置检查清单
- 自然语言融合质量
- LSI（语义相关）关键词覆盖率
- 关键词内耗（Cannibalization）风险

**输出**：分布图、缺口分析、具体修改建议

---

### Editor
**用途**：将技术准确的内容转化为拟人化、引人入胜的文章

**分析维度**：
- 语调与个性特征
- 案例的具体程度
- 可读性与行文流畅度
- 机械感 vs 人类表达模式
- 互动性与故事性

**提供内容**：
- 人性化评分（0-100）
- 关键修改项及前后对比
- 句式模式分析
- 注入个性的具体重写建议
- 可读性改进方案

**输出**：编辑报告，明确如何使内容更贴近人类写作风格

---

### Performance
**用途**：基于真实数据的优先级排序与内容策略指导

**分析维度**：
- Google Analytics 流量与趋势
- Google Search Console 排名与 CTR
- DataForSEO 竞争数据
- 快速机会点（排名第 11-20 位）
- 衰退中内容识别
- 低 CTR 优化机会
- 热门趋势话题

**提供内容**：
- 任务优先级队列
- 机会评分（0-100）
- 影响力与工作量预估
- 按周推进的路径图
- 成功指标定义

**输出**：包含可执行优先级的综合性能报告

---

### Headline Generator
**用途**：生成高转化率标题变体及 A/B 测试建议

**提供内容**：
- 10+ 条基于成熟公式的标题变体
- 转化潜力评分
- A/B 测试策略
- 针对特定受众的标题选项

---

### CRO Analyst
**用途**：落地页转化率优化（CRO）分析

**分析维度**：
- 首屏（Above-the-fold）有效性
- CTA 质量与分布
- 信任信号（Trust Signals） presence
- 摩擦点识别
- 页面结构评估

---

### Landing Page Optimizer
**用途**：落地页综合优化建议

**提供内容**：
- CRO 评分（0-100）及分类明细
- 首屏、CTA、信任信号、结构与 SEO 分析
- A/B 测试推荐方案
- 优先级行动清单

## 营销技能

SEO Machine 内置 26 项可通过斜杠命令调用的营销技能：

| Category | Skills |
|----------|--------|
| **文案撰写（Copywriting）** | `/copywriting`、`/copy-editing` |
| **转化率优化（CRO）** | `/page-cro`、`/form-cro`、`/signup-flow-cro`、`/onboarding-cro`、`/popup-cro`、`/paywall-upgrade-cro` |
| **策略规划** | `/content-strategy`、`/pricing-strategy`、`/launch-strategy`、`/marketing-ideas` |
| **渠道运营** | `/email-sequence`、`/social-content`、`/paid-ads` |
| **SEO 专项** | `/seo-audit`、`/schema-markup`、`/programmatic-seo`、`/competitor-alternatives` |
| **数据分析** | `/analytics-tracking`、`/ab-test-setup` |
| **其他** | `/referral-program`、`/free-tool-strategy`、`/marketing-psychology` |

## 数据来源

### 分析工具集成

SEO Machine 接入实时数据源以指导内容策略：

**Google Analytics 4 (GA4)**：
- 流量与互动指标
- 转化追踪
- 趋势分析
- 流量来源拆解

**Google Search Console (GSC)**：
- 关键词排名与位置
- 展示量（Impressions）与点击数
- CTR 分析
- 查询表现评估

**DataForSEO**：
- 竞争排名数据
- SERP 特征提取
- 核心指标监控
- 竞品缺口分析

### 高级 SEO 分析模块 (NEW!)

SEO Machine 内置 5 个专用 Python 模块，用于深度内容分析：

**Search Intent Analyzer (`search_intent_analyzer.py`)**：
- 将查询分类为信息型、导航型、交易型或商业意图
- 分析 SERP 特征与内容模式
- 提供置信度评分与内容匹配建议

**Keyword Analyzer (`keyword_analyzer.py`)**：
- 计算精确的关键词密度与分布
- 检测堆砌风险并发出警告
- 使用 TF-IDF 和 K-means 进行主题聚类
- 生成按章节划分的分布热力图
- 识别 LSI（语义相关）关键词

**SEO Quality Rater (`seo_quality_rater.py`)**：
- 对照 SEO 最佳实践对内容评级（0-100 分）
- 分类明细：内容、关键词、元数据、结构、链接、可读性
- 识别关键问题、警告与建议项
- 判定发布就绪状态

**Content Length Comparator (`content_length_comparator.py`)**：
- 抓取并分析前 10-20 名 SERP 竞品的字数统计
- 计算中位数、75% 分位及最优长度建议
- 展示竞争定位与目标差距
- 提供数据驱动的扩写建议

**Readability Scorer (`readability_scorer.py`)**：
- Flesch Reading Ease 与 Flesch-Kincaid Grade Level
- 句子与段落结构分析
- 被动语态检测与比例计算
- 复杂词汇识别
- 过渡词使用分析
- 综合可读性评分（0-100）

所有模块均可直接在 Python 中调用，或通过 Content Analyzer Agent 间接使用。

### CRO 分析模块

6 个用于落地页转化优化的 Python 模块：

- `above_fold_analyzer.py` - 首屏内容分析（标题、价值主张、CTA、信任背书）
- `cta_analyzer.py` - CTA 有效性评分（质量、分布、目标对齐度）
- `trust_signal_analyzer.py` - 信任信号检测（评价、社会证明、风险逆转承诺）
- `landing_page_scorer.py` - 落地页综合评分（0-100，含分类明细）
- `landing_performance.py` - 通过 GA4/GSC 追踪落地页表现
- `cro_checker.py` - CRO 最佳实践检查清单验证

### 其他分析模块

- `opportunity_scorer.py` - 8 维机会评分模型（用于内容优先级排序）
- `content_scorer.py` - 5 维度内容质量评分（人性化、具体性、结构、SEO、可读性）
- `engagement_analyzer.py` - 内容互动模式分析
- `competitor_gap_analyzer.py` - 竞品内容缺口识别
- `article_planner.py` - 数据驱动的文章规划
- `section_writer.py` - 章节级内容指导
- `social_research_aggregator.py` - 社交媒体研究聚合

### Python 研究脚本

从仓库根目录运行：

```bash
# 内容研究
python3 research_quick_wins.py
python3 research_competitor_gaps.py
python3 research_performance_matrix.py
python3 research_priorities_comprehensive.py
python3 research_serp_analysis.py
python3 research_topic_clusters.py
python3 research_trending.py

# SEO 分析（需配置 config/competitors.json）
python3 seo_baseline_analysis.py
python3 seo_bofu_rankings.py
python3 seo_competitor_analysis.py

# 测试 API 连通性
python3 test_dataforseo.py
```

**注意**：SEO 分析脚本会从 `config/competitors.json` 加载竞争对手列表与关键词。复制 `config/competitors.example.json` 并根据你的业务进行自定义配置。

### WordPress 集成

发布功能通过 WordPress REST API 实现，配合自定义的 MU-plugin 暴露 Yoast SEO 字段。

**设置步骤**：
1. 将 `wordpress/seo-machine-yoast-rest.php` 安装为 WordPress 站点的 MU-plugin
2. 将 `wordpress/functions-snippet.php` 添加到主题的 functions.php
3. 在 `.env` 中配置 WordPress 凭据：
   ```
   WP_URL=https://yoursite.com
   WP_USERNAME=your_username
   WP_APP_PASSWORD=your_application_password
   ```

详细设置说明请参阅 `wordpress/README.md`。

分析工具集成说明请参阅 `data_sources/README.md`。

## 目录结构

```
seomachine/
├── .claude/
│   ├── commands/          # 自定义工作流命令
│   │   ├── analyze-existing.md
│   │   ├── research.md
│   │   ├── write.md
│   │   ├── rewrite.md
│   │   ├── optimize.md
│   │   ├── scrub.md
│   │   ├── performance-review.md
│   │   ├── publish-draft.md
│   │   ├── article.md
│   │   ├── priorities.md
│   │   ├── research-serp.md
│   │   ├── research-gaps.md
│   │   ├── research-trending.md
│   │   ├── research-performance.md
│   │   ├── research-topics.md
│   │   ├── landing-write.md
│   │   ├── landing-audit.md
│   │   ├── landing-research.md
│   │   ├── landing-competitor.md
│   │   └── landing-publish.md
│   ├── agents/            # 专用分析 Agent
│   │   ├── content-analyzer.md
│   │   ├── seo-optimizer.md
│   │   ├── meta-creator.md
│   │   ├── internal-linker.md
│   │   ├── keyword-mapper.md
│   │   ├── editor.md
│   │   ├── performance.md
│   │   ├── headline-generator.md
│   │   ├── cro-analyst.md
│   │   └── landing-page-optimizer.md
│   └── skills/            # 26 项营销技能
├── data_sources/          # 分析工具集成
│   ├── modules/           # Python 分析模块
│   │   ├── google_analytics.py
│   │   ├── google_search_console.py
│   │   ├── dataforseo.py
│   │   ├── data_aggregator.py
│   │   ├── search_intent_analyzer.py
│   │   ├── keyword_analyzer.py
│   │   ├── seo_quality_rater.py
│   │   ├── content_length_comparator.py
│   │   ├── readability_scorer.py
│   │   ├── opportunity_scorer.py
│   │   ├── content_scorer.py
│   │   ├── engagement_analyzer.py
│   │   ├── social_research_aggregator.py
│   │   ├── competitor_gap_analyzer.py
│   │   ├── article_planner.py
│   │   ├── section_writer.py
│   │   ├── wordpress_publisher.py
│   │   ├── above_fold_analyzer.py
│   │   ├── cro_checker.py
│   │   ├── cta_analyzer.py
│   │   ├── landing_page_scorer.py
│   │   ├── landing_performance.py
│   │   └── trust_signal_analyzer.py
│   ├── config/            # API 凭据（未提交至 Git）
│   ├── utils/             # 辅助函数
│   ├── cache/             # 缓存的 API 响应
│   └── README.md          # 设置说明
├── config/                # 配置文件
│   └── competitors.example.json  # 竞品配置模板
├── context/               # 上下文与规范文件
│   ├── brand-voice.md
│   ├── writing-examples.md
│   ├── style-guide.md
│   ├── seo-guidelines.md
│   ├── target-keywords.md
│   ├── internal-links-map.md
│   ├── competitor-analysis.md
│   └── cro-best-practices.md
├── wordpress/             # WordPress 集成
│   ├── seo-machine-yoast-rest.php
│   ├── functions-snippet.php
│   └── README.md
├── topics/                # 原始主题创意
├── research/              # 研究简报与分析报告
├── drafts/                # 进行中的草稿文章
├── review-required/       # 待审核文章
├── published/             # 准备发布的终稿
├── rewrites/              # 已更新的历史内容
├── landing-pages/         # 落地页内容
├── audits/                # 审计报告
└── README.md              # 本文件
```

## 上下文文件（重要！）

内容质量取决于正确配置的上下文文件：

### `context/brand-voice.md`
定义你的品牌语调、语气与核心信息框架。

**必须包含**：
- 语调支柱（Voice Pillars）
- 按内容类型划分的语气指南
- 核心品牌信息
- 写作风格规范
- 术语偏好

**用途**：确保所有内容符合你的品牌调性

---

### `context/writing-examples.md`
包含你站点的 3-5 篇优秀博客文章范例。

**必须包含**：
- 完整文章正文
- 每篇范文的亮点说明
- 语调与结构的关键要点

**用途**：通过示例教会 AI 你的专属写作风格

---

### `context/style-guide.md`
编辑规范与排版标准。

**必须包含**：
- 语法与标点规则
- 大小写惯例
- 格式标准
- 首选术语表

**用途**：确保所有内容保持一致性

---

### `context/seo-guidelines.md`
SEO 最佳实践与硬性要求。

**包含内容**：
- 字数长度要求
- 关键词优化规则
- 元数据元素标准
- 链接策略指南
- 可读性指标要求

**用途**：确保所有内容符合 SEO 标准

---

### `context/target-keywords.md`
按主题聚类组织的关键词研究数据。

**必须包含**：
- 各聚类的核心词（Pillar Keywords）
- 子话题关键词（Cluster Keywords）
- 长尾词变体
- 搜索意图分类
- 当前排名情况

**用途**：指导新内容的关键词布局

---

### `context/internal-links-map.md`
用于内部链接的站点关键页面目录。

**必须包含**：
- 产品页与功能介绍页
- 核心支柱内容（Pillar Content）URL
- 高流量博客文章列表
- 主题聚类映射关系
- 推荐锚文本

**用途**：使每篇文章都能实现战略性内部链接

---

### `context/competitor-analysis.md`
竞争情报与内容缺口分析。

**必须包含**：
- 主要竞争对手名单
- 他们的内容策略
- 关键词缺口
- 差异化机会点

**用途**：指导内容策略制定与竞争定位

## 内容质量标准

每篇文章必须符合以下要求：

### 内容质量
- [ ] 最低 2,000 词（推荐 2,500-3,000+ 词）
- [ ] 相比竞品提供独特价值
- [ ] 事实准确且信息时效性强
- [ ] 为目标受众提供可执行建议
- [ ] 保持品牌语调一致

### SEO 规范
- [ ] 核心关键词密度 1-2%
- [ ] 关键词出现在 H1、前 100 词及 2-3 个 H2 中
- [ ] 包含 3-5 条带描述性锚文本的内部链接
- [ ] 包含 2-3 条外部权威来源链接
- [ ] 元标题长度 50-60 字符
- [ ] 元描述长度 150-160 字符
- [ ] 严格遵循 H1>H2>H3 层级结构

### 可读性要求
- [ ] 阅读难度相当于 8-10 年级水平
- [ ] 平均句长 15-20 词
- [ ] 段落长度 2-4 句话
- [ ] 每 300-400 词设置小标题
- [ ] 合理使用列表与排版提升扫读体验

### 结构完整性
- [ ] 吸引人的开头（钩子、痛点、承诺）
- [ ] 逻辑清晰的章节流转
- [ ] 明确的结尾与 CTA（行动号召）
- [ ] 包含案例与数据支撑

## 最佳实践

### 撰写前准备
1. **先研究**：务必在 `/write` 之前运行 `/research`
2. **查阅上下文**：阅读 `brand-voice.md` 及相关 `writing-examples.md`
3. **核对关键词**：确认 `target-keywords.md` 中的目标词
4. **规划内部链接**：查看 `internal-links-map.md` 寻找链接机会

### 撰写过程中
1. **遵循简报**：以研究报告作为大纲基础
2. **自然融入关键词**：切勿生硬堆砌
3. **持续提供价值**：每个章节都应包含可执行洞察
4. **使用真实案例**：加入你所在行业的实际场景与用例
5. **注明出处**：为统计数据与数据源添加链接

### 撰写完成后
1. **审查 Agent 输出**：仔细阅读所有 Agent 的建议报告
2. **落实改进项**：优先解决高优先级问题后再进行优化
3. **执行最终优化**：使用 `/optimize` 进行最后润色
4. **模拟读者审阅**：以目标读者的视角通读全文
5. **核对检查清单**：确认所有标准均已达标

### 内容重写时
1. **先分析**：运行 `/analyze-existing` 明确更新范围
2. **确定策略**：是轻度刷新还是全面重写？
3. **保留有效部分**：维持原稿中表现良好的章节
4. **聚焦缺口**：补充竞品内容中的缺失信息
5. **全面更新**：统计数据、案例、截图与链接均需同步更新

## 工作流示例

### 示例 1：从零创建新内容

```
# 步骤 1：添加主题创意
# 在 topics/ 目录中创建文件并记录初步想法

# 步骤 2：研究该主题
/research content marketing strategies

# 步骤 3：审阅研究报告
# 阅读 research/brief-content-marketing-strategies-[date].md

# 步骤 4：撰写文章
/write content marketing strategies

# 步骤 5：审查 Agent 反馈
# 阅读 drafts/ 目录下所有 Agent 报告

# 步骤 6：进行修改
# 根据 Agent 建议编辑文章

# 步骤 7：最终优化
/optimize drafts/content-marketing-strategies-[date].md

# 步骤 8：发布至 WordPress（可选）
/publish-draft drafts/content-marketing-strategies-[date].md
```

### 示例 2：更新现有内容

```
# 步骤 1：分析现有文章
/analyze-existing https://yoursite.com/blog/product-comparison

# 步骤 2：审阅分析报告
# 阅读 research/analysis-product-comparison-2025-10-29.md
# 检查内容健康度评分与优先级等级

# 步骤 3：重写内容
/rewrite product comparison

# 步骤 4：审查修改结果
# 阅读 rewrites/product-comparison-rewrite-2025-10-29.md
# 查看修改摘要

# 步骤 5：优化
/optimize rewrites/product-comparison-rewrite-2025-10-29.md

# 步骤 6：发布
# 准备就绪后移至 published/ 目录
```

### 示例 3：批量内容审计

```
# 分析多篇现有文章以优先排序更新任务
/analyze-existing https://yoursite.com/blog/post-1
/analyze-existing https://yoursite.com/blog/post-2
/analyze-existing https://yoursite.com/blog/post-3

# 审阅内容健康度评分
# 按以下标准优先安排重写：
# - 最低分文章
# - 最高流量潜力
# - 战略重要性
```

## 技巧与提示

### 最大化内容质量
- **研读范例**：每次撰写前仔细阅读 `writing-examples.md`
- **引用数据**：始终包含最新统计数据并注明来源
- **保持具体**：“提升 40%”优于“显著改善”
- **用实例说话**：使用你所在行业的真实案例与场景
- **解答疑问**：针对研究中提取的“People Also Ask”问题进行回答

### SEO 优化技巧
- **关键词前置**：确保核心词出现在前 100 词内
- **自然融合**：大声朗读内容，若关键词显得生硬则重写
- **多样化锚文本**：避免所有内部链接使用相同的锚文本
- **战略性链接**：优先链接至支柱内容与相关聚类文章
- **定期更新**：每 6-12 个月刷新高表现内容

### 工作流提效
- **批量研究**：单次会话中研究多个主题
- **遵循结构**：使用 `/write` 命令提供的标准文章结构
- **优先处理高优项**：先修复关键问题，再优化细节
- **善用 Agent**：让 Agent 负责分析，你专注于写作与策略
- **建立模板库**：保存常用段落以便复用

### 避免常见错误
- ❌ 跳过研究阶段直接撰写
- ❌ 忽视品牌语调规范
- ❌ 生硬堆砌关键词
- ❌ 忘记添加内部链接
- ❌ 引用数据却不注明出处
- ❌ 未经优化直接发布
- ❌ 抄袭竞品内容而非打造差异化

## 维护计划

### 每周
- 将新主题创意添加至 `/topics/`
- 更新 `target-keywords.md` 中的新关键词机会
- 检查 `internal-links-map.md` 中的死链

### 每月
- 审阅已发布内容的表现数据
- 若出现更优范例，更新 `writing-examples.md`
- 将新发布内容添加至 `internal-links-map.md`
- 在 `competitor-analysis.md` 中追踪竞品动态

### 每季度
- 全面审查上下文文件
- 根据算法更新调整 SEO 规范
- 刷新综合竞争对手分析
- 审阅并更新 `target-keywords.md` 中的主题聚类

## 故障排除

### “内容读起来不像我的品牌”
- **解决方案**：在 `context/brand-voice.md` 中添加更具体的指导说明
- **解决方案**：为 `context/writing-examples.md` 补充更多样化的范例
- **解决方案**：使用 `/write` 命令时直接引用具体范例文件

### “关键词密度过高或过低”
- **解决方案**：查阅 `seo-guidelines.md` 中的目标密度（1-2%）
- **解决方案**：运行 `/optimize` 获取具体的关键词布局建议
- **解决方案**：使用 Keyword Mapper Agent 进行分布分析

### “内部链接不相关”
- **解决方案**：更新 `context/internal-links-map.md` 中的当前页面列表
- **解决方案**：按主题聚类组织，便于 Agent 匹配
- **解决方案**：为每个页面提供更详细的覆盖范围说明

### “文章与竞品过于相似”
- **解决方案**：在 `competitor-analysis.md` 中补充差异化机会点
- **解决方案**：将你的独特优势添加至 `brand-voice.md` 和 `features.md`
- **解决方案**：在 `/research` 命令中明确引用具体的差异化角度

## 支持与贡献

### 获取帮助
- 仔细阅读本 README
- 确认上下文文件已正确配置
- 查阅 [Claude Code 官方文档](https://docs.claude.com/claude-code)

### 参与贡献
- 通过 GitHub Issues 报告问题
- 提出命令或 Agent 的改进建议
- 分享成功的工作流或实用技巧

## 许可证

[添加你的许可证信息]

## 致谢

本项目基于 Anthropic 的 [Claude Code](https://claude.com/claude-code) 构建。

最初为 Castos 开发，现作为开源工具开放给所有企业，用于简化长篇幅 SEO 内容的创建流程。

## 示例与社区

**查看实际运行效果**：访问 `examples/castos/`，了解一家播客托管 SaaS 公司如何使用 SEO Machine 的真实案例。

**欢迎贡献**：发现 Bug？有功能需求？想分享你所在行业的自定义范例？我们非常欢迎你的贡献与 Pull Request！

---

**准备好开始创作了吗？**

1. 配置你的上下文文件（以模板为指南）
2. 运行 `/research [your topic]`
3. 审阅研究报告
4. 运行 `/write [your topic]`
5. 发布精彩内容！

祝你写作顺利！ 📝
# Trafilatura：在网络上发现与提取文本数据

<br/>

<img alt="Trafilatura Logo" src="https://raw.githubusercontent.com/adbar/trafilatura/master/docs/trafilatura-logo.png" align="center" width="60%"/>

<br/>

[![Python package](https://img.shields.io/pypi/v/trafilatura.svg)](https://pypi.python.org/pypi/trafilatura)
[![Python versions](https://img.shields.io/pypi/pyversions/trafilatura.svg)](https://pypi.python.org/pypi/trafilatura)
[![Documentation Status](https://readthedocs.org/projects/trafilatura/badge/?version=latest)](http://trafilatura.readthedocs.org/en/latest/?badge=latest)
[![Code Coverage](https://img.shields.io/codecov/c/github/adbar/trafilatura.svg)](https://codecov.io/gh/adbar/trafilatura)
[![Downloads](https://static.pepy.tech/badge/trafilatura/month)](https://pepy.tech/project/trafilatura)
[![Reference DOI: 10.18653/v1/2021.acl-demo.15](https://img.shields.io/badge/DOI-10.18653%2Fv1%2F2021.acl--demo.15-blue)](https://aclanthology.org/2021.acl-demo.15/)

<br/>

<img alt="Demo as GIF image" src="https://raw.githubusercontent.com/adbar/trafilatura/master/docs/trafilatura-demo.gif" align="center" width="80%"/>

<br/>


## 简介

Trafilatura 是一款前沿的 **Python 包与命令行工具**，旨在**收集网络文本并简化将原始 HTML 转换为结构化、有意义数据的过程**。它内置了所有必要的发现与文本处理组件，用于执行主文本、元数据和评论的**网页爬取、下载、抓取和提取**。该项目致力于保持**便捷与模块化**：无需依赖数据库，输出结果可轻松转换为常用格式。

从海量 HTML 内容中提取核心部分，可以有效缓解许多与文本质量相关的问题。通过**聚焦实际内容**、**避免页眉和页脚等重复元素产生的噪声**，并利用精选信息使**数据与元数据更具意义**。该提取器在限制噪声（精度）与保留所有有效部分（召回率）之间取得了良好平衡。它具备**高鲁棒性且运行速度合理**。

Trafilatura 已被**广泛使用**，并被 HuggingFace、IBM、微软研究院等公司，以及艾伦人工智能研究所（Allen Institute）、斯坦福大学、东京工业大学和慕尼黑大学等机构集成。


### 功能特性

- 高级网络爬取与文本发现：
   - 支持站点地图（TXT、XML）和订阅源（ATOM、JSON、RSS）
   - 智能爬取与 URL 管理（过滤与去重）

- 在线与离线输入的并行处理：
   - 实时 URL、高效且符合爬虫礼仪的下载队列处理
   - 已下载的 HTML 文件及解析后的 HTML 树结构

- 关键元素的鲁棒性与可配置提取：
   - 主文本（通用模式与经典算法，如 jusText 和 readability）
   - 元数据（标题、作者、日期、站点名称、分类与标签）
   - 格式与结构：段落、标题、列表、引用、代码、换行符及行内文本格式化
   - 可选元素：评论、链接、图片、表格

- 多种输出格式：
   - TXT 和 Markdown
   - CSV
   - JSON
   - HTML、XML 和 [XML-TEI](https://tei-c.org/)

- 可选附加功能：
   - 提取内容的语言检测
   - 速度优化

- 由开源社区支持，持续积极维护：
   - 定期更新、功能新增与性能优化
   - 完善的文档体系


### 评估与替代方案

Trafilatura 在文本提取基准测试中持续优于其他开源库，展现了其在提取网络内容方面的高效性与准确性。该提取器力求在限制噪声与保留所有有效部分之间取得平衡。

更多信息请参阅[基准测试章节](https://trafilatura.readthedocs.io/en/latest/evaluation.html)和[评估说明文档](https://github.com/adbar/trafilatura/blob/master/tests/README.rst)，以使用最新数据与依赖包运行评估。


#### 其他权威评估：

- 在 ScrapingHub 的 [文章提取基准测试](https://github.com/scrapinghub/article-extraction-benchmark) 中被评为最高效的开源库
- 根据 Lejeune & Barbaresi (2020) 的研究《[Bien choisir son outil d'extraction de contenu à partir du Web](https://hal.archives-ouvertes.fr/hal-02768510v3/document)》，被评为综合最佳工具
- 在 Bevendorff 等人 (2023) 的论文《[An Empirical Comparison of Web Content Extraction Algorithms](https://webis.de/downloads/publications/papers/bevendorff_2023b.pdf)》中，以 ROUGE-LSum 平均 F1 页面得分被评为最佳单一工具


## 使用方式与文档

[Trafilatura 入门指南](https://trafilatura.readthedocs.io/en/latest/quickstart.html) 简单直观。如需更多信息与详细指南，请访问[Trafilatura 官方文档](https://trafilatura.readthedocs.io/)：

- [安装说明](https://trafilatura.readthedocs.io/en/latest/installation.html)
- 使用方式：
  [命令行](https://trafilatura.readthedocs.io/en/latest/usage-cli.html)、
  [Python](https://trafilatura.readthedocs.io/en/latest/usage-python.html)、
  [R 语言](https://trafilatura.readthedocs.io/en/latest/usage-r.html)
- [核心 Python 函数](https://trafilatura.readthedocs.io/en/latest/corefunctions.html)
- 交互式 Python Notebook：[Trafilatura 概览](docs/Trafilatura_Overview.ipynb)
- [教程与用例](https://trafilatura.readthedocs.io/en/latest/tutorials.html)

多语言视频教程合集：

- [网页抓取教程与操作指南](https://www.youtube.com/watch?v=8GkiOM17t0Q&list=PL-pKWbySIRGMgxXQOtGIz1-nbfYLvqrci)


## 许可证

本软件包遵循 [Apache 2.0 许可证](https://www.apache.org/licenses/LICENSE-2.0.html)。

v1.8.0 之前的版本采用 GPLv3+ 许可证。


### 贡献指南

欢迎任何形式的贡献。请访问[贡献说明页](https://github.com/adbar/trafilatura/blob/master/CONTRIBUTING.md)获取更多信息。Bug 报告请提交至[专属 Issue 页面](https://github.com/adbar/trafilatura/issues)。

衷心感谢所有[贡献者](https://github.com/adbar/trafilatura/graphs/contributors)，是你们完善了文档、提交了 Bug 报告、新功能与修复！


## 项目背景

该项目最初是语言学与自然语言处理（NLP）交叉领域的一项博士研究课题。这项专业知识在多年的发展中为 Trafilatura 的架构塑造起到了关键作用。它最初由柏林-勃兰登堡科学院（DWDS 与 ZDL 部门）启动，旨在创建用于学术研究的文本数据库。该软件包目前仍在持续维护中，但其未来发展依赖于社区支持。

**如果你重视本软件或你的产品依赖于此，请考虑赞助该项目并为其代码库贡献力量。** 你在 [GitHub](https://github.com/sponsors/adbar) 或 [ko-fi.com](https://ko-fi.com/adbarbaresi) 上的支持将有助于维护与提升这款广受欢迎的软件包。

*Trafilatura* 是意大利语，意为“拉丝”，象征着精炼与转换的过程。它也是制作意大利面成型的方式。

### 作者

如需咨询、合作或反馈，请通过软件仓库或[联系页面](https://adrien.barbaresi.eu/)联系我们。也可关注社交媒体获取最新动态。

-   Barbaresi, A. [Trafilatura: A Web Scraping Library and Command-Line Tool for Text Discovery and Extraction](https://aclanthology.org/2021.acl-demo.15/), Proceedings of ACL/IJCNLP 2021: System Demonstrations, 2021, p. 122-131.
-   Barbaresi, A. "[Generic Web Content Extraction with Open-Source Software](https://hal.archives-ouvertes.fr/hal-02447264/document)", Proceedings of KONVENS 2019, Kaleidoscope Abstracts, 2019.
-   Barbaresi, A. "[Efficient construction of metadata-enhanced web corpora](https://hal.archives-ouvertes.fr/hal-01371704v2/document)", Proceedings of the [10th Web as Corpus Workshop (WAC-X)](https://www.sigwac.org.uk/wiki/WAC-X), 2016.


### 引用 Trafilatura

Trafilatura 在学术界被广泛使用，主要用于数据采集。引用方式如下：

[![Reference DOI: 10.18653/v1/2021.acl-demo.15](https://img.shields.io/badge/DOI-10.18653%2Fv1%2F2021.acl--demo.15-blue)](https://aclanthology.org/2021.acl-demo.15/)
[![Zenodo archive DOI: 10.5281/zenodo.3460969](https://zenodo.org/badge/DOI/10.5281/zenodo.3460969.svg)](https://doi.org/10.5281/zenodo.3460969)

``` shell
@inproceedings{barbaresi-2021-trafilatura,
  title = {{Trafilatura: A Web Scraping Library and Command-Line Tool for Text Discovery and Extraction}},
  author = "Barbaresi, Adrien",
  booktitle = "Proceedings of the Joint Conference of the 59th Annual Meeting of the Association for Computational Linguistics and the 11th International Joint Conference on Natural Language Processing: System Demonstrations",
  pages = "122--131",
  publisher = "Association for Computational Linguistics",
  url = "https://aclanthology.org/2021.acl-demo.15",
  year = 2021,
}
```


### 软件生态

联合开发的插件与附加软件包也为网络数据提取与分析领域做出了贡献：

<img alt="Software ecosystem" src="https://raw.githubusercontent.com/adbar/htmldate/master/docs/software-ecosystem.png" align="center" width="65%"/>

相关文章可查阅 [Bits of Language 博客](https://adrien.barbaresi.eu/blog/tag/trafilatura.html)。

令人印象深刻，你已阅读至页面末尾：感谢你的关注！
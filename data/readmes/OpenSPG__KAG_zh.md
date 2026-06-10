# KAG：知识增强生成

<div align="center">
<a href="https://spg.openkg.cn/en-US">
<img src="./_static/images/OpenSPG-1.png" width="520" alt="openspg logo">
</a>
</div>

<p align="center">
  <a href="./README.md">English</a> |
  <a href="./README_cn.md">简体中文</a> |
  <a href="./README_ja.md">日本語版ドキュメント</a>
</p>

<p align="center">
    <a href='https://arxiv.org/pdf/2409.13731'><img src='https://img.shields.io/badge/arXiv-2409.13731-b31b1b'></a>
    <a href="https://github.com/OpenSPG/KAG/releases/latest">
        <img src="https://img.shields.io/github/v/release/OpenSPG/KAG?color=blue&label=Latest%20Release" alt="Latest Release">
    </a>
    <a href="https://openspg.yuque.com/ndx6g9/docs_en">
        <img src="https://img.shields.io/badge/User%20Guide-1e8b93?logo=readthedocs&logoColor=f5f5f5" alt="User Guide">
    </a>
    <a href="https://github.com/OpenSPG/KAG/blob/main/LICENSE">
        <img height="21" src="https://img.shields.io/badge/License-Apache--2.0-ffffff?labelColor=d4eaf7&color=2e6cc4" alt="license">
    </a>
    <a href="https://deepwiki.com/Like0x/KAG"><img src="https://deepwiki.com/badge.svg" alt="Ask DeepWiki"></a>
</p>
<p align="center">
   <a href="https://discord.gg/PURG77zhQ7">
        <img src="https://img.shields.io/discord/1329648479709958236?style=for-the-badge&logo=discord&label=Discord" alt="Discord">
   </a>
</p>

# 1. KAG 是什么？

KAG 是一个基于 [OpenSPG](https://github.com/OpenSPG/openspg) 引擎和大语言模型（LLM）的逻辑推理与问答框架，用于构建垂直领域知识库的逻辑推理和问答解决方案。KAG 能有效克服传统 RAG 向量相似度计算的歧义问题，以及 GraphRAG 因 OpenIE 引入的噪声问题。KAG 支持逻辑推理和多跳事实问答等，性能显著优于当前的 SOTA（State of the Art）方法。

KAG 的目标是在专业领域构建知识增强的 LLM 服务框架，支持逻辑推理、事实问答等。KAG 充分融合了知识库（KG）的逻辑与事实特征。其核心特性包括：

- 知识与文本块（Chunk）互索引结构，以整合更完整的上下文信息
- 基于概念语义推理的知识对齐机制，缓解 OpenIE 引入的噪声问题
- 受模式（Schema）约束的知识构建，支持领域专家知识的表示与构建
- 逻辑形式引导的混合推理与检索，支持逻辑推理和多跳问答

⭐️ 给本仓库点星（Star），以获取最新功能与改进的更新！第一时间接收新版本通知！🌟

![Star KAG](./_static/images/star-kag.gif)

# 2. 核心特性

## 2.1 知识表示

在私有知识库场景下，非结构化数据、结构化信息及业务专家经验往往共存。KAG 参考 DIKW（数据-信息-知识-智慧）层次模型，将 SPG 升级为对 LLM 更友好的版本。 

针对新闻、事件、日志和书籍等非结构化数据，交易、统计和审批等结构化数据，以及业务经验和领域知识规则，KAG 采用版面分析、知识抽取、属性归一化和语义对齐等技术，将原始业务数据和专家规则整合为统一的企业业务知识图谱。

![KAG Diagram](./_static/images/kag-diag.jpg)

这使得 KAG 能够在同一知识类型（如实体类型、事件类型）上，同时兼容无模式约束的信息抽取和有模式约束的专业知识构建，并支持图谱结构与原始文本块之间的交叉索引表示。 

这种互索引表示有助于基于图结构的倒排索引构建，并推动了逻辑形式的统一表示与推理。

## 2.2 逻辑形式引导的混合推理

![Logical Form Solver](./_static/images/kag-lf-solver.png)

KAG 提出了一种逻辑形式引导的混合求解与推理引擎。 

该引擎包含三种类型的算子：规划（planning）、推理（reasoning）和检索（retrieval），将自然语言问题转化为结合语言与符号的求解过程。 

在此过程中，每一步均可使用不同的算子（如精确匹配检索、文本检索、数值计算或语义推理），从而实现四种不同求解过程的融合：检索、知识图谱推理、语言推理和数值计算。

# 3. 更新日志

## 3.1 最新更新
* 2025.06.27：发布 KAG 0.8.0 版本 
  * 扩展两种模式：私有知识库（含结构化与非结构化数据）和公网知识库，支持通过 MCP 协议集成 LBS、WebSearch 等公开数据源。
  * 增强私有知识库索引能力，内置大纲（Outline）、摘要（Summary）、知识单元（KnowledgeUnit）、原子查询（AtomicQuery）、文本块（Chunk）和表格（Table）等基础索引类型。
  * 解耦知识库与应用：知识库负责管理私有数据（结构化与非结构化）与公开数据；应用可关联多个知识库，并根据构建时建立的索引类型自动适配相应的检索器进行数据召回。
  * 全面拥抱 MCP 协议，支持在 Agent 工作流中通过 MCP 协议调用 KAG 推理问答能力。
  * 完成 KAG-Thinker 模型适配。通过在广度问题分解、深度方案推导、知识边界判定及抗噪检索等方面的优化，在多轮迭代思考框架指导下，提升了框架的推理范式稳定性与逻辑严谨性。 
* 2025.04.17：发布 KAG 0.7 版本 
  * 首先，重构了 KAG-Solver 框架。新增静态与迭代两种任务规划模式，并在推理阶段实现了更严谨的知识分层机制。 
  * 其次，优化产品体验：在推理阶段引入“简单模式”和“深度推理”双模式，支持流式输出、自动渲染图索引，并将生成内容链接至原始出处。 
  * 在 KAG 仓库顶层新增 `open_benchmark` 目录，对比相同基础模型下的各类 RAG 方法，达到 SOTA（State of the Art）效果。 
  * 引入“轻量构建”模式，知识构建 Token 成本降低 89%。
* 2025.01.07：支持领域知识注入、领域 Schema 自定义、QFS 任务支持、可视化查询分析，开启抽取模式下的 Schema 约束等。
* 2024.11.21：支持 Word 文档上传、模型调用并发设置、用户体验优化等。
* 2024.10.25：KAG 初始版本发布

## 3.2 未来规划

我们将持续关注并提升大模型利用外部知识库的能力。目标是实现大模型与符号知识的双向增强与无缝融合，提高专业场景下推理与问答的事实准确性、严谨性和一致性。同时将持续发布更新，拓展能力边界，推动在垂直领域的落地应用。

# 4. 快速开始

## 4.1 基于产品（面向普通用户）

### 4.1.1 引擎与依赖镜像安装

* **推荐系统版本：**

  ```text
  macOS User：macOS Monterey 12.6 or later
  Linux User：CentOS 7 / Ubuntu 20.04 or later
  Windows User：Windows 10 LTSC 2021 or later
  ```

* **软件要求：**

  ```text
  macOS / Linux User：Docker，Docker Compose
  Windows User：WSL 2 / Hyper-V，Docker，Docker Compose
  ```

使用以下命令下载 docker-compose.yml 文件，并通过 Docker Compose 启动服务。

```bash
# set the HOME environment variable (only Windows users need to execute this command)
# set HOME=%USERPROFILE%

curl -sSL https://raw.githubusercontent.com/OpenSPG/openspg/refs/heads/master/dev/release/docker-compose-west.yml -o docker-compose-west.yml
docker compose -f docker-compose-west.yml up -d
```

### 4.1.2 使用产品

在浏览器中访问 KAG 产品的默认地址：<http://127.0.0.1:8887>
```text
Default Username: openspg
Default password: openspg@kag
```
详细使用说明请参阅 [KAG 使用指南（产品模式）](https://openspg.yuque.com/ndx6g9/cwh47i/rs7gr8g4s538b1n7#rtOlA)。

## 4.2 基于工具包（面向开发者）

### 4.2.1 引擎与依赖镜像安装

请参考 3.1 节完成引擎与依赖镜像的安装。

### 4.2.2 安装 KAG


**macOS / Linux 开发者**

```text
# Create conda env: conda create -n kag-demo python=3.10 && conda activate kag-demo

# Clone code: git clone https://github.com/OpenSPG/KAG.git

# Install KAG: cd KAG && pip install -e .
```

**Windows 开发者**

```text
# Install the official Python 3.10 or later, install Git.

# Create and activate Python venv: py -m venv kag-demo && kag-demo\Scripts\activate

# Clone code: git clone https://github.com/OpenSPG/KAG.git

# Install KAG: cd KAG && pip install -e .
```

### 4.2.3 使用工具包

详细工具包使用说明请参阅 [KAG 使用指南（开发者模式）](https://openspg.yuque.com/ndx6g9/cwh47i/rs7gr8g4s538b1n7#cikso)。随后，你可以利用内置组件复现内置数据集的性能结果，并将这些组件应用于新的业务场景。

# 5. 技术架构

![KAG technical architecture](./_static/images/kag-arch.png)

KAG 框架包含三个部分：kg-builder、kg-solver 和 kag-model。本次发布仅涉及前两部分，kag-model 将在未来逐步开源。

kg-builder 实现了面向大语言模型（LLM）友好的知识表示。基于 DIKW（数据、信息、知识、智慧）的层次结构，它升级了 SPG 的知识表示能力，在同一知识类型（如实体类型和事件类型）上兼容无模式约束的信息抽取与有模式约束的专业知识构建；同时支持图谱结构与原始文本块之间的互索引表示，为推理问答阶段的高效检索提供支撑。

kg-solver 采用逻辑符号引导的混合求解与推理引擎，包含规划、推理和检索三种类型的算子，将自然语言问题转化为结合语言与符号的求解过程。在此过程中，每一步均可使用不同的算子（如精确匹配检索、文本检索、数值计算或语义推理），从而实现四种不同求解过程的融合：检索、知识图谱推理、语言推理和数值计算。

# 6. 社区与支持

**GitHub**：<https://github.com/OpenSPG/KAG>

**官网**：<https://openspg.github.io/v2/docs_en>

## Discord <a href="https://discord.gg/PURG77zhQ7"> <img src="https://img.shields.io/discord/1329648479709958236?style=for-the-badge&logo=discord&label=Discord" alt="Discord"></a>

加入我们的 [Discord](https://discord.gg/PURG77zhQ7) 社区。

## 微信

关注 OpenSPG 官方公众号，获取关于 OpenSPG 和 KAG 的技术文章与产品更新。

<img src="./_static/images/openspg-qr.png" alt="Contact Us: OpenSPG QR-code" width="200">

扫描下方二维码加入我们的微信交流群。 

<img src="./_static/images/robot-qr.JPG" alt="Join WeChat group" width="200">


# 7. KAG、RAG 与 GraphRAG 的区别

**KAG 介绍与应用**：<https://github.com/orgs/OpenSPG/discussions/52>

# 8. 引用

如果你使用了本软件，请按以下格式引用：

* [KAG: Boosting LLMs in Professional Domains via Knowledge Augmented Generation](https://arxiv.org/abs/2409.13731)

* KGFabric: A Scalable Knowledge Graph Warehouse for Enterprise Data Interconnection

```bibtex
@article{liang2024kag,
  title={KAG: Boosting LLMs in Professional Domains via Knowledge Augmented Generation},
  author={Liang, Lei and Sun, Mengshu and Gui, Zhengke and Zhu, Zhongshu and Jiang, Zhouyu and Zhong, Ling and Zhao, Peilong and Bo, Zhongpu and Yang, Jin and others},
  journal={arXiv preprint arXiv:2409.13731},
  year={2024}
}

@article{yikgfabric,
  title={KGFabric: A Scalable Knowledge Graph Warehouse for Enterprise Data Interconnection},
  author={Yi, Peng and Liang, Lei and Da Zhang, Yong Chen and Zhu, Jinye and Liu, Xiangyu and Tang, Kun and Chen, Jialin and Lin, Hao and Qiu, Leijie and Zhou, Jun}
}
```

# License

[Apache License 2.0](LICENSE)

# KAG 核心团队
Lei Liang, Mengshu Sun, Zhengke Gui, Zhongshu Zhu, Zhouyu Jiang, Ling Zhong, Peilong Zhao, Zhongpu Bo, Jin Yang, Huaidong Xiong, Lin Yuan, Jun Xu, Zaoyang Wang, Zhiqiang Zhang, Wen Zhang, Huajun Chen, Wenguang Chen, Jun Zhou, Haofen Wang
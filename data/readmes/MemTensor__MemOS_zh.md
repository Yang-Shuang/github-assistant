<div align="center">
  <a href="https://memos.openmem.net/">
    <img src="https://statics.memtensor.com.cn/memos/memos-banner.gif" alt="MemOS Banner">
  </a>

  <h1 align="center">
    <img src="https://statics.memtensor.com.cn/logo/memos_color_m.png" alt="MemOS Logo" width="48"/>&nbsp;
    MemOS 2.0&ensp;Stardust（星尘）

  </h1>

<p align="center">
  <br>
  <a href="https://memos-docs.openmem.net/home/overview/"><img src="https://img.shields.io/badge/Docs-Get--Start-002FA7?labelColor=gray&style=for-the-badge&logo=googledocs&logoColor=white" alt="Docs"></a>
  <a href="https://arxiv.org/abs/2507.03724"><img src="https://img.shields.io/badge/ArXiv-2507.03724-B31B1B?labelColor=gray&style=for-the-badge&logo=arxiv&logoColor=white" alt="ArXiv"></a>
  <a href="https://x.com/MemOS_dev"><img src="https://img.shields.io/badge/Follow-MemOS-000000?labelColor=gray&style=for-the-badge&logo=x&logoColor=white" alt="X"></a>
  <a href="https://discord.gg/Txbx3gebZR"><img src="https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fdiscord.com%2Fapi%2Fv10%2Finvites%2FTxbx3gebZR%3Fwith_counts%3Dtrue&query=%24.approximate_presence_count&suffix=%20online&label=Discord&color=404EED&labelColor=gray&style=for-the-badge&logo=discord&logoColor=white" alt="Discord"></a>
  <a href="https://github.com/IAAR-Shanghai/Awesome-AI-Memory"><img src="https://img.shields.io/badge/Resources-Awesome--AI--Memory-8A2BE2?labelColor=gray&style=for-the-badge&logo=awesomelists&logoColor=white" alt="Resources"></a>
</p>

<p align="center">
  <strong>🎯 相比 OpenAI Memory，准确率提升 43.70%</strong><br/>
  <strong>🏆 顶级长程记忆能力与个性化支持</strong><br/>
  <strong>💰 节省 35.24% 的记忆 Token 消耗</strong><br/>
  <sub>LoCoMo 75.80 • LongMemEval +40.43% • PrefEval-10 +2568% • PersonaMem +40.75%</sub>
  <!-- <a href="https://memos.openmem.net/">
    <img src="https://statics.memtensor.com.cn/memos/github_api_free_banner.gif" alt="MemOS Free API Banner">
  </a> -->

</p>

</div>

<!-- Get Free API: [Try API](https://memos-dashboard.openmem.net/quickstart/?source=github) -->

<!-- --- -->

<!-- <br> -->

## 🧠 MemOS 插件：为 AI Agent 提供持久化记忆能力 ✨

<div align="center">
  
<img width="1660" height="664" alt="MemOS Plugin Banner" src="https://github.com/user-attachments/assets/9d15dde2-196e-4f71-a364-dd5a33062117" />

你的 Lobster（🦞）和 Hermes Agent 现在拥有了**最佳**的记忆系统——选择 ***云端服务*** 或 ***本地自托管*** 即可快速开始 🏃🏻

| 🔌 插件 | <div align="center"> 💡 核心特性 </div> | 🧩 资源链接 |
| :----: | :--- | :---: |
| 🧠 [**memos-local-plugin 2.0**](https://github.com/hijzy/MemOS/tree/main/apps/memos-local-plugin) | <ul><li>为 **Hermes Agent** 和 **OpenClaw** 提供以本地为核心的单一记忆内核。</li><li>具备自我演进的记忆能力：L1 轨迹记录、L2 策略管理、L3 世界模型，<br>以及由反馈驱动结晶的技能（Skills）。</li></ul> | 🌐 [官网](https://memos-claw.openmem.net/) · 📖 [文档](https://memos-docs.openmem.net/cn/openclaw/local_plugin) · 🐙 [GitHub](https://github.com/hijzy/MemOS/tree/main/apps/memos-local-plugin) · 📦 [NPM](https://www.npmjs.com/package/@memtensor/memos-local-plugin) |
| ☁️ [**OpenClaw Cloud Plugin**](https://x.com/MemOS_dev/status/2019254160919769171?s=20) | <ul><li>[Token 使用量降低 72%。](https://x.com/MemOS_dev/status/2020854044583924111)</li><li>[通过 `user_id` 实现多 Agent 记忆共享。](https://x.com/MemOS_dev/status/2020538135487062094)</li></ul> | 🖥️ [MemOS 控制台](https://memos-dashboard.openmem.net/login/) · 📖 [完整教程](https://memos-docs.openmem.net/openclaw/guide#_4-update-plugin) |

</div>
<br>

## 👾 MemOS：面向大语言模型与 AI Agent 的记忆操作系统

**MemOS** 是一款专为大语言模型（LLM）和 AI Agent 设计的记忆操作系统，统一了长程记忆的**存储 / 检索 / 管理**功能，原生支持**上下文感知**与**个性化**交互，并内置知识库、多模态处理、工具记忆及企业级优化能力。


### 核心特性

- **统一的记忆 API**：提供一套单一 API 用于添加、检索、编辑和删除记忆——数据以图结构组织，设计上支持直观检查与修改，而非黑盒式的向量嵌入（embedding）存储。
- **多模态记忆**：原生支持文本、图像、工具轨迹及角色设定（Persona），在单一记忆系统中进行联合检索与推理。
- **多 Cube 知识库管理**：将多个知识库作为可组合的“记忆立方体”进行管理，实现用户、项目及 Agent 之间的隔离、受控共享与动态组合。
- **MemScheduler 异步摄入**：支持以毫秒级延迟运行异步记忆操作，确保高并发场景下的生产环境稳定性。
- **记忆反馈与修正**：通过自然语言反馈优化记忆——随时间推移对现有记忆进行纠正、补充或替换。


### 最新动态

- **2026-05-09** · 🧠 **memos-local-plugin 2.0**
  面向 **Hermes Agent** 和 **OpenClaw** 的官方本地记忆插件。单一核心驱动跨 L1 轨迹、L2 策略、L3 世界模型及结晶技能的自我演进记忆，采用以本地优先的存储架构与反馈驱动的检索机制。

- **2026-04-10** · 👧🏻 **MemOS Hermes Agent Local Plugin**
  官方 Hermes Agent 记忆插件正式发布：支持混合检索（FTS5 + 向量）、智能去重、分层技能演进及多 Agent 协作。完全本地化运行，零云端依赖。
  
- **2026-03-08** · 🦞 **MemOS OpenClaw Plugin — Cloud & Local**
  官方 OpenClaw 记忆插件正式发布。**云插件**：托管式记忆服务，Token 使用量降低 72%，支持多 Agent 记忆共享（[MemOS-Cloud-OpenClaw-Plugin](https://github.com/MemTensor/MemOS-Cloud-OpenClaw-Plugin)）。**本地插件** (`v1.0.0`)：100% 端侧运行，采用持久化 SQLite、混合搜索（FTS5 + 向量）、任务摘要与技能演进功能，支持多 Agent 协作及完整的记忆查看器仪表盘。

- **2025-12-24** · 🎉 **MemOS v2.0: Stardust (星尘) Release**
  全面升级知识库（文档/URL 解析 + 跨项目共享）、记忆反馈与精准删除、多模态记忆（图像/图表）、Agent 规划工具记忆、Redis Streams 调度及数据库优化、流式/非流式对话、MCP 协议升级，以及轻量级快速/完整部署模式。
  <details>
    <summary>✨ <b>新增特性</b></summary>

  **知识库与记忆**
  - 新增对文档和 URL 长程记忆的本地知识库支持

  **反馈与记忆管理**
  - 新增自然语言反馈与修正功能
  - 新增通过记忆 ID 删除记忆的 API
  - 新增 MCP 支持的记忆删除与反馈接口

  **对话与检索**
  - 新增感知记忆的对话 API
  - 新增自定义标签过滤记忆（云端版 & 开源版）

  **多模态与工具记忆**
  - 新增记录工具使用历史的工具体系记忆
  - 新增图像记忆支持，涵盖对话与文档场景

  </details>

  <details>
    <summary>📈 <b>性能优化</b></summary>

  **数据与基础设施**
  - 升级数据库以提升稳定性与性能表现

  **调度器**
  - 基于 Redis Streams 重构任务调度器，实现队列隔离
  - 新增任务优先级、自动恢复及配额制调度机制

  **部署与工程化**
  - 新增轻量级部署模式，支持快速启动与完整安装两种选项

  </details>

  <details>
    <summary>🐞 <b>Bug 修复</b></summary>

  **记忆调度与更新**
  - 修复遗留的调度 API，确保正确的记忆隔离机制
  - 修复记忆更新日志，现可正确显示新增记忆内容

  </details>

- **2025-08-07** · 🎉 **MemOS v1.0.0 (MemCube) Release**
  首个 MemCube 版本发布，包含文字游戏演示、LongMemEval 评估体系、BochaAISearchRetriever 集成、搜索能力优化及官方 Playground 正式上线。

  <details>
    <summary>✨ <b>新增特性</b></summary>

  **Playground**
  - 扩展 Playground 功能并提升算法性能表现。

  **MemCube 构建**
  - 新增基于 MemCube 小说的文字游戏演示。

  **扩展评估集**
  - 新增 LongMemEval 评估结果及相关脚本。

  </details>

  <details>
    <summary>📈 <b>性能优化</b></summary>

  **纯文本记忆**
  - 集成 Bocha 互联网搜索能力。
  - 扩展图数据库支持范围。
  - 新增树状结构纯文本记忆搜索接口的上下文理解能力。

  </details>

  <details>
    <summary>🐞 <b>Bug 修复</b></summary>

  **KV Cache 拼接**
  - 修复 `concat_cache` 方法逻辑。

  **纯文本记忆**
  - 修复图搜索相关异常问题。

  </details>

- **2025-07-07** · 🎉 **MemOS v1.0: Stellar (星河) Preview Release**
  面向大语言模型的 SOTA 记忆操作系统现已开源。
- **2025-07-04** · 🎉 **MemOS Paper Release**
  [论文《MemOS：面向 AI 系统的记忆操作系统》](https://arxiv.org/abs/2507.03724) 已在 arXiv 发布。
- **2024-07-04** · 🎉 **Memory3 Model Release at WAIC 2024**
  采用记忆分层架构的 Memory3 模型于 2024 世界人工智能大会（WAIC）正式亮相。

<br>

## 🚀 快速入门指南

### ☁️ 1、云 API（托管服务）
#### 获取 API Key
- 在 [MemOS 控制台](https://memos-dashboard.openmem.net/cn/quickstart/?source=landing) 注册账号
- 进入 **API Keys** 页面并复制你的密钥

#### 后续步骤
- [MemOS 云快速入门](https://memos-docs.openmem.net/memos_cloud/quick_start/)
  连接至 MemOS 云端并在几分钟内启用记忆功能。
- [MemOS 云平台](https://memos.openmem.net/?from=/quickstart/)
  探索云端控制台、功能特性与工作流。

### 🖥️ 2、自托管（本地/私有部署）
1. 获取代码仓库。
    ```bash
    git clone https://github.com/MemTensor/MemOS.git
    cd MemOS
    pip install -r ./docker/requirements.txt
    ```
2. 配置 `docker/.env.example` 并复制至 `MemOS/.env`
 - `OPENAI_API_KEY`、`MOS_EMBEDDER_API_KEY`、`MEMRADER_API_KEY` 及其他密钥可通过 [百炼控制台](https://bailian.console.aliyun.com/?spm=a2c4g.11186623.0.0.2f2165b08fRk4l&tab=api#/api) 申请。
 - 将对应配置填入 `MemOS/.env` 文件中。
 - 支持的 LLM 服务商包括：**OpenAI**、**Azure OpenAI**、**Qwen（DashScope）**、**DeepSeek**、**MiniMax**、**Ollama**、**HuggingFace**、**vLLM**。设置 `MOS_CHAT_MODEL_PROVIDER` 以选择后端（例如 `openai`、`qwen`、`deepseek`、`minimax`）。
3. 启动服务。

- 通过 Docker 启动
  ###### 提示：请确保已成功安装 Docker Compose，并在执行以下命令前进入 docker 目录（使用 `cd docker`）。
  ```bash
  # Enter docker directory
  docker compose up
  ```
  ##### 详细步骤请参阅[`Docker 参考文档`](https://docs.openmem.net/open_source/getting_started/rest_api_server/#method-1-docker-use-repository-dependency-package-imagestart-recommended-use)。

- 通过 uvicorn 命令行界面（CLI）启动
  ###### 提示：请确保在执行以下命令前，Neo4j 和 Qdrant 服务已正常运行。
  ```bash
  cd src
  uvicorn memos.api.server_api:app --host 0.0.0.0 --port 8001 --workers 1
  ```
  ##### 详细集成步骤请参阅[`CLI 参考文档`](https://docs.openmem.net/open_source/getting_started/rest_api_server/#method-3client-install-with-CLI)。



### 基础用法（自托管）
  - 添加用户消息
    ```python
    import requests
    import json

    data = {
        "user_id": "8736b16e-1d20-4163-980b-a5063c3facdc",
        "mem_cube_id": "b32d0977-435d-4828-a86f-4f47f8b55bca",
        "messages": [
            {
                "role": "user",
                "content": "I like strawberry"
            }
        ],
        "async_mode": "sync"
    }
    headers = {
        "Content-Type": "application/json"
    }
    url = "http://localhost:8000/product/add"

    res = requests.post(url=url, headers=headers, data=json.dumps(data))
    print(f"result: {res.json()}")
    ```
  - 检索用户记忆
    ```python
    import requests
    import json

    data = {
        "query": "What do I like",
        "user_id": "8736b16e-1d20-4163-980b-a5063c3facdc",
        "mem_cube_id": "b32d0977-435d-4828-a86f-4f47f8b55bca"
    }
    headers = {
        "Content-Type": "application/json"
    }
    url = "http://localhost:8000/product/search"

    res = requests.post(url=url, headers=headers, data=json.dumps(data))
    print(f"result: {res.json()}")
    ```
    
<br>

## 📚 资源链接

- **Awesome-AI-Memory**
  这是一个精心策划的仓库，专门收录大语言模型记忆及相关系统的资源。系统性地收集了相关研究论文、框架、工具及实践心得。旨在整理并展示 LLM 记忆领域快速演进的研究格局，涵盖自然语言处理、信息检索、Agent 系统及认知科学等多个研究方向。<br/>
**开始使用** 👉🏻 [IAAR-Shanghai/Awesome-AI-Memory](https://github.com/IAAR-Shanghai/Awesome-AI-Memory)

- **MemOS Cloud OpenClaw Plugin**
  面向 MemOS 云端的官方 OpenClaw 生命周期插件。Agent 启动前会自动从 MemOS 召回上下文，任务结束后会将对话保存回 MemOS。<br/>
**开始使用** 👉🏻 [MemTensor/MemOS-Cloud-OpenClaw-Plugin](https://github.com/MemTensor/MemOS-Cloud-OpenClaw-Plugin)

<br>

## 💬 社区与支持

加入我们的社区，提问、分享项目并与其它开发者交流。

- **GitHub Issues**：在 <a href="https://github.com/MemTensor/MemOS/issues" target="_blank">GitHub Issues</a> 中提交 Bug 报告或功能请求。
- **GitHub Pull Requests**：通过 <a href="https://github.com/MemTensor/MemOS/pulls" target="_blank">Pull Requests</a> 贡献代码改进。
- **GitHub Discussions**：参与我们的 <a href="https://github.com/MemTensor/MemOS/discussions" target="_blank">GitHub Discussions</a>，提问或分享想法。
- **Discord**：加入我们的 <a href="https://discord.gg/Txbx3gebZR" target="_blank">Discord 服务器</a>。
- **微信**：扫描下方二维码加入微信群。

<div align="center">
  <img src="https://statics.memtensor.com.cn/memos/qr-code.png" alt="QR Code" width="300" />
</div>

<br>

## 📜 引用方式

> [!NOTE]
> 我们已于 **2025年5月28日** 公开了简短版论文，这是最早提出大语言模型记忆操作系统概念的工作之一。

如果你在研究中使用了 MemOS，欢迎引用我们的论文。

```bibtex

@article{li2025memos_long,
  title={MemOS: A Memory OS for AI System},
  author={Li, Zhiyu and Song, Shichao and Xi, Chenyang and Wang, Hanyu and Tang, Chen and Niu, Simin and Chen, Ding and Yang, Jiawei and Li, Chunyu and Yu, Qingchen and Zhao, Jihao and Wang, Yezhaohui and Liu, Peng and Lin, Zehao and Wang, Pengyuan and Huo, Jiahao and Chen, Tianyi and Chen, Kai and Li, Kehang and Tao, Zhen and Ren, Junpeng and Lai, Huayi and Wu, Hao and Tang, Bo and Wang, Zhenren and Fan, Zhaoxin and Zhang, Ningyu and Zhang, Linfeng and Yan, Junchi and Yang, Mingchuan and Xu, Tong and Xu, Wei and Chen, Huajun and Wang, Haofeng and Yang, Hongkang and Zhang, Wentao and Xu, Zhi-Qin John and Chen, Siheng and Xiong, Feiyu},
  journal={arXiv preprint arXiv:2507.03724},
  year={2025},
  url={https://arxiv.org/abs/2507.03724}
}

@article{li2025memos_short,
  title={MemOS: An Operating System for Memory-Augmented Generation (MAG) in Large Language Models},
  author={Li, Zhiyu and Song, Shichao and Wang, Hanyu and Niu, Simin and Chen, Ding and Yang, Jiawei and Xi, Chenyang and Lai, Huayi and Zhao, Jihao and Wang, Yezhaohui and others},
  journal={arXiv preprint arXiv:2505.22101},
  year={2025},
  url={https://arxiv.org/abs/2505.22101}
}

@article{yang2024memory3,
author = {Yang, Hongkang and Zehao, Lin and Wenjin, Wang and Wu, Hao and Zhiyu, Li and Tang, Bo and Wenqiang, Wei and Wang, Jinbo and Zeyun, Tang and Song, Shichao and Xi, Chenyang and Yu, Yu and Kai, Chen and Xiong, Feiyu and Tang, Linpeng and Weinan, E},
title = {Memory$^3$: Language Modeling with Explicit Memory},
journal = {Journal of Machine Learning},
year = {2024},
volume = {3},
number = {3},
pages = {300--346},
issn = {2790-2048},
doi = {https://doi.org/10.4208/jml.240708},
url = {https://global-sci.com/article/91443/memory3-language-modeling-with-explicit-memory}
}
```

<br>

## 🙌 贡献指南

我们欢迎社区贡献！请阅读我们的 [贡献指南](https://memos-docs.openmem.net/open_source/contribution/overview/) 以开始参与。

<br>

## 📄 许可证

MemOS 基于 [Apache 2.0 许可证](./LICENSE) 开源。
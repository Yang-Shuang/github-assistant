<div align="center" id="readme-top">

![banner-gif](https://github.com/user-attachments/assets/0bf97efd-580f-4a53-a2a2-58d6daea7290)

<p align="center">
  <a href="https://x.com/evermind"><img src="https://img.shields.io/badge/EverMind-000000?labelColor=gray&style=for-the-badge&logo=x&logoColor=white" alt="X"></a>
  <a href="https://huggingface.co/EverMind-AI"><img src="https://img.shields.io/badge/🤗_HuggingFace-EverMind-F5C842?labelColor=gray&style=for-the-badge" alt="HuggingFace"></a>
  <a href="https://discord.gg/gYep5nQRZJ"><img src="https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fdiscord.com%2Fapi%2Fv10%2Finvites%2FgYep5nQRZJ%3Fwith_counts%3Dtrue&query=%24.approximate_presence_count&suffix=%20online&label=Discord&color=404EED&labelColor=gray&style=for-the-badge&logo=discord&logoColor=white" alt="Discord"></a>
  <a href="https://github.com/EverMind-AI/EverOS/discussions/67"><img src="https://img.shields.io/badge/WeCom-EverMind_社区-07C160?labelColor=gray&style=for-the-badge&logo=wechat&logoColor=white" alt="WeChat"></a>
</p>

[Website](https://evermind.ai) · [Documentation](https://docs.evermind.ai) · [Blog](https://evermind.ai/blogs)

</div>


<br>

<details open>
  <summary><kbd>目录</kbd></summary>

<br>

- [项目概览](#project-overview)
- [应用场景](#use-cases)
- [快速开始](#quick-start)
- [架构方法](#architecture-methods)
- [基准测试](#benchmarks)
- [评估](#evaluation)
- [引用文献](#citations)
- [持续关注](#stay-tuned)
- [贡献指南](#contributing)

<br>

</details>



## 项目概览

**EverOS** 是应用于、构建和评估自进化智能体（Agent）长期记忆的统一平台。该仓库围绕三个核心部分组织：

| 组成部分 | 提供内容 | 从这里开始 |
| :--- | :--- | :--- |
| **应用场景** | 展示记忆如何改变真实智能体工作流的应用、演示和集成。 | [use-cases/](use-cases/) |
| **架构方法** | 可运行、扩展或对比的记忆系统与算法。 | [methods/](methods/) |
| **基准测试** | 用于记忆质量和智能体自进化的开源评估套件。 | [benchmarks/](benchmarks/) |

EverOS 的核心是 **EverCore**，一个面向智能体的长期记忆操作系统。如果你是项目新手，建议先浏览应用场景以了解记忆能实现什么功能，然后按照 [快速开始](#quick-start) 在本地运行 EverCore。当你准备好对比系统或复现结果时，下方的架构和基准测试部分将为你提供深入的参考资料。

<br>

## 应用场景

应用场景展示了持久化记忆在实际产品和流程中能实现的功能。以下是一些示例；其他则指向外部演示或集成，供你研究并适配。

<table>
<tr>
<td width="50%" valign="top">

[![banner-gif](https://github.com/user-attachments/assets/840470d7-a838-4c05-8685-dd797d4e9cdf)](https://evermind.ai/usecase_reunite)

#### Reunite - 借助 EverOS 寻人

父母描述他们记得的内容，孩子描述他们的回忆。Reunite 利用语义记忆来揭示这些关联。

[了解更多](https://evermind.ai/usecase_reunite)

</td>
<td width="50%" valign="top">

[![banner-gif](https://github.com/user-attachments/assets/7282b38b-56bf-4356-aa7b-06a845e7683d)](https://github.com/tt-a1i/hive)

#### Hive 协调器

面向 CLI 编程智能体的浏览器原生“蜂巢思维”——通过团队协议，Claude Code、Codex、Gemini 和 OpenCode 作为真实的 PTY 进程进行协作。

[代码](https://github.com/tt-a1i/hive)

</td>
</tr>

<tr>
<td width="50%" valign="top">

[![banner-gif](https://github.com/user-attachments/assets/867d9329-ce9a-496f-ab1e-15c77974e5fa)](https://github.com/tt-a1i/evermemos-mcp)

#### 借助 EverOS 的 AI 编程助手

由 EverOS 驱动的通用长期记忆层，适用于各类 AI 编程助手。

[代码](https://github.com/tt-a1i/evermemos-mcp)

</td>
<td width="50%" valign="top">

[![banner-gif](https://github.com/user-attachments/assets/a4f0fd86-1c81-4445-bebc-e51eb5e33b30)](https://github.com/yuansui123/AI-Data-Technician-EverMemOS)

#### AI 数据技术员

一种智能体 AI 系统，通过与科学家交互进行学习，用于检查、分析和分类高维时间序列数据——具备跨会话持续改进的持久记忆。

[代码](https://github.com/yuansui123/AI-Data-Technician-EverMemOS)

</td>
</tr>

<tr>
<td width="50%" valign="top">

![banner-gif](https://github.com/user-attachments/assets/650b901b-c9ba-4001-bac7-626b009df830)

#### 借助 EverOS 的 Rokid AI 助手

在 Rokid 眼镜中接入 EverOS，为你的所有智能活动提供长期记忆支持。

即将上线

</td>
<td width="50%" valign="top">

![banner-gif](https://github.com/user-attachments/assets/85b338b2-e48e-4a65-9f30-0bc6998df872)

#### 带记忆的创意助手

具备长期记忆的创意助手，从此不再遗忘你的创作灵感。

即将上线

</td>
</tr>

<tr>
<td width="50%" valign="top">

[![banner-gif](https://github.com/user-attachments/assets/f30617a1-adc0-4271-bc0e-c3a0b28cb903)](https://github.com/xunyud/Earth-Online)

#### Earth Online 记忆游戏

Earth Online 是一款具有记忆感知能力的生产力游戏，将日常规划转化为动态的任务日志。

[代码](https://github.com/xunyud/Earth-Online)

</td>
<td width="50%" valign="top">

[![banner-gif](https://github.com/user-attachments/assets/57d8cda7-35a5-4561-b794-5520dffc917b)](https://github.com/golutra/golutra) 

#### 多智能体编排平台

Golutra 为工程团队提供多智能体工作流，将 IDE 模型从单一助手扩展至协同工作的智能体集群。

[代码](https://github.com/golutra/golutra)

</td>
</tr>
<tr>
<td width="50%" valign="top">

[![banner-gif](https://github.com/user-attachments/assets/75f19db5-30f6-4eed-9b1e-c9c6a0e6b7de)](https://github.com/Yangtze-Seventh/taste-verse)

#### 你的个人品鉴宇宙

通过沉浸式 3D 星图记录、可视化并探索你的品鉴之旅。

[代码](https://github.com/Yangtze-Seventh/taste-verse)

</td>
<td width="50%" valign="top">

[![banner-gif](https://github.com/user-attachments/assets/93ac2a68-4f18-4fcb-8d87-80aeb00a9d7c)](https://github.com/kellyvv/OpenHer) 

#### EverOS Open Her

打造有感知力的 AI。开源人格引擎——个性源于神经驱动，而非提示词。灵感源自电影《Her》。

[代码](https://github.com/kellyvv/OpenHer)

</td>
</tr>

<tr>
<td width="50%" valign="top">

[![banner-gif](https://github.com/user-attachments/assets/550071c1-dc39-4964-9f67-ffdfad792345)](https://chromewebstore.google.com/detail/ruminer-browser-agent/lbccjohfpdpimbhpckljimgolndfmfif)

#### 个人记忆浏览器智能体

Ruminer 为浏览器智能体引入持久化记忆，使其能在跨网页任务中携带个人上下文信息。

[插件](https://chromewebstore.google.com/detail/ruminer-browser-agent/lbccjohfpdpimbhpckljimgolndfmfif)

</td>
<td width="50%" valign="top">

[![banner-gif](https://github.com/user-attachments/assets/c258a6c4-fe70-497a-98d1-3dade4a932f6)](https://github.com/nanxingw/EverMem) 

#### EverMem 与 EverOS 同步

一条命令即可将任意 AI 编程 CLI 连接至 EverMemOS 长期记忆系统。

[代码](https://github.com/nanxingw/EverMem)

</td>
</tr>

<tr>
<td width="50%" valign="top">

[![banner-gif](https://github.com/user-attachments/assets/39274473-ceb3-48fb-a031-e22230decbe2)](https://github.com/mco-org/mco)

#### MCO - 编排 AI 编程智能体

MCO 为你的主智能体配备一个智能体团队，协同解决复杂任务。

[代码](https://github.com/mco-org/mco)

</td>
<td width="50%" valign="top">

[![banner-gif](https://github.com/user-attachments/assets/314c9126-8e08-4688-bbbb-8555ad58cf67)](https://github.com/onenewborn/StudyBuddy-public) 

#### 具备自进化记忆的学习伙伴

与拥有自进化记忆的智能体一起主动学习。

[代码](https://github.com/onenewborn/StudyBuddy-public)

</td>
</tr>

<tr>
<td width="50%" valign="top">

[![banner-gif](https://github.com/user-attachments/assets/21da76aa-9a8b-48e0-9134-42429d7390e7)](https://github.com/TonyLiangDesign/MemoCare)

#### 阿尔茨海默症记忆助手

为个人提供先进的记忆支持与日常辅助。

[代码](https://github.com/TonyLiangDesign/MemoCare)

</td>
<td width="50%" valign="top">

[![banner-gif](https://github.com/user-attachments/assets/e2428df3-ea11-4e88-8f9c-dad437dd8998)](https://github.com/AlexL1024/NeuralConnect) 

#### 记忆驱动的多智能体 NPC 体验

一款 iOS 科幻悬疑游戏，玩家在其中探索并揭开真相。

[代码](https://github.com/AlexL1024/NeuralConnect)

</td>
</tr>

<tr>
<td width="50%" valign="top">

[![banner-gif](https://github.com/user-attachments/assets/e6eaf308-a874-483f-8874-6934bf95a78f)](https://github.com/elontusk5219-prog/Mobi)

#### Mobi 伴侣

一款 iOS 应用，用户可创建、培养并与个性化 AI 伴侣 Mobi 共同生活。

[代码](https://github.com/elontusk5219-prog/Mobi)

</td>
<td width="50%" valign="top">

[![banner-gif](https://github.com/user-attachments/assets/9aabcaa9-f97a-49d2-9109-0b5bb696ed41)](https://github.com/JaMesLiMers/EvermemCompetition-Spiro)

#### 带记忆的 AI 可穿戴设备

原生感知上下文的 AI 可穿戴设备，聆听日常生活并将对话转化为记忆。

[代码](https://github.com/JaMesLiMers/EvermemCompetition-Spiro)

</td>
</tr>
<tr>
<td width="50%" valign="top">

[![banner-gif](https://github.com/user-attachments/assets/df9677ec-386f-4c56-a428-08bca25c54dc)](https://github.com/EverMind-AI/EverOS/tree/0f49826ba0f9a94e1974c97614a46a68e0a08b52/evermemos-openclaw-plugin)

#### OpenClaw 智能体记忆

提供跨会话持续学习记忆的 7x24 小时不间断智能体工作流。

[插件](https://github.com/EverMind-AI/EverOS/tree/0f49826ba0f9a94e1974c97614a46a68e0a08b52/evermemos-openclaw-plugin)

</td>
<td width="50%" valign="top">

[![banner-gif](https://github.com/user-attachments/assets/3a2357a1-c0c3-464a-8979-0d1cdfc9b0d4)](https://github.com/TEN-framework/ten-framework/tree/04cb80601374fa9e35b4e544b2dbd23286ca7763/ai_agents/agents/examples/voice-assistant-with-EverMemOS)

#### 带记忆的 Live2D 角色

为实时 Live2D 角色添加长期记忆，由 [TEN Framework](https://github.com/TEN-framework/ten-framework) 提供支持。

[代码](https://github.com/TEN-framework/ten-framework/tree/04cb80601374fa9e35b4e544b2dbd23286ca7763/ai_agents/agents/examples/voice-assistant-with-EverMemOS)

</td>
</tr>
<tr>
<td width="50%" valign="top">

[![banner-gif](https://github.com/user-attachments/assets/c36bdc04-97d3-4fe9-97d9-4b93b475595a)](https://screenshot-analysis-vercel.vercel.app/)

#### 带记忆的计算机操作 (Computer-Use)

使用计算机操作功能运行基于截图的分析，并将结果存储至记忆中。

[在线演示](https://screenshot-analysis-vercel.vercel.app/)

</td>
<td width="50%" valign="top">

[![banner-gif](https://github.com/user-attachments/assets/54a7cf8f-62c4-4fbc-9d50-b214d034e051)](use-cases/game-of-throne-demo)

#### 《权力的游戏》记忆

通过《权力的游戏》互动问答体验，展示 AI 记忆基础设施的演示项目。

[代码](use-cases/game-of-throne-demo)

</td>
</tr>
<tr>
<td width="50%" valign="top">

[![banner-gif](https://github.com/user-attachments/assets/af37c1f6-7ba5-430c-b99d-2a7e7eac618f)](use-cases/claude-code-plugin)

#### Claude Code 插件

为 Claude Code 提供持久化记忆支持。自动保存并调用过往编程会话中的上下文信息。

[代码](use-cases/claude-code-plugin)

</td>
<td width="50%" valign="top">

[![banner-gif](https://github.com/user-attachments/assets/d521d28c-0ccd-44ff-aecc-828245e2f973)](https://main.d2j21qxnymu6wl.amplifyapp.com/graph.html)

#### 记忆图谱可视化

在图界面中探索存储的实体与关系。前端演示版；后端集成正在进行中。

[在线演示](https://main.d2j21qxnymu6wl.amplifyapp.com/graph.html)

</td>
</tr>
</table>

<br>
<div align="right">

[![](https://img.shields.io/badge/-Back_to_top-gray?style=flat-square)](#readme-top)

</div>

## 快速开始

根据你的目标选择对应路径：

```bash
git clone https://github.com/EverMind-AI/EverOS.git
cd EverOS
```

| 目标 | 组件 | 入口点 |
| :--- | :--- | :--- |
| 构建具备长期记忆的智能体 | **EverCore** | [methods/EverCore/](methods/EverCore/) |
| 探索超图记忆架构 | **HyperMem** | [methods/HyperMem/](methods/HyperMem/) |
| 评估记忆系统质量 | **EverMemBench** | [benchmarks/EverMemBench/](benchmarks/EverMemBench/) |
| 衡量智能体自进化能力 | **EvoAgentBench** | [benchmarks/EvoAgentBench/](benchmarks/EvoAgentBench/) |
| 适配示例应用或集成 | **应用场景** | [use-cases/](use-cases/) |

> 每个组件均配有独立的安装指南、依赖配置和使用示例。

### EverCore

在本地运行记忆系统的最快方式是先从 EverCore 开始：

```bash
cd methods/EverCore

# Requires Python 3.12 and Docker.

# Start Docker services
docker compose up -d

# Install dependencies
curl -LsSf https://astral.sh/uv/install.sh | sh
uv sync

# Configure API keys
cp env.template .env
# Edit .env and set:
#   - LLM_API_KEY (for memory extraction)
#   - VECTORIZE_API_KEY (for embedding/rerank)

# Start server
uv run python src/run.py

# Verify installation
curl http://localhost:1995/health
# Expected response: {"status": "healthy", ...}
```

服务运行于 `http://localhost:1995` · [完整安装指南](methods/EverCore/docs/installation/SETUP.md)

### 基础用法

使用简单的 Python 代码即可存储和检索记忆：

```python
import os
import requests

API_BASE = os.getenv("EVERCORE_API_BASE", "http://localhost:1995/api/v1")

# 1. Store a conversation memory
add_payload = {
    "user_id": "user_001",
    "session_id": "quickstart_session",
    "messages": [
        {
            "message_id": "msg_001",
            "sender_id": "user_001",
            "sender_name": "User",
            "role": "user",
            "timestamp": 1738404000000,
            "content": "I love playing soccer on weekends",
        }
    ],
}
add_result = requests.post(f"{API_BASE}/memories", json=add_payload)
add_result.raise_for_status()
add_result = add_result.json()
print(add_result["data"]["status"])

# 2. Search for relevant memories
search_payload = {
    "query": "What sports does the user like?",
    "method": "hybrid",
    "memory_types": ["episodic_memory"],
    "top_k": 5,
    "filters": {"user_id": "user_001"},
}
search_result = requests.post(f"{API_BASE}/memories/search", json=search_payload)
search_result.raise_for_status()
search_result = search_result.json()

for episode in search_result["data"]["episodes"]:
    print(episode["episode"])
```

[更多示例](methods/EverCore/docs/usage/USAGE_EXAMPLES.md) · [API 参考](https://docs.evermind.ai/api-reference/introduction) · [交互式演示](methods/EverCore/docs/usage/DEMOS.md)

<br>
<div align="right">

[![](https://img.shields.io/badge/-Back_to_top-gray?style=flat-square)](#readme-top)

</div>

## 架构方法

以下是 EverOS 当前包含的记忆架构。你可以将其作为可运行的系统、研究参考，或构建自有智能体记忆层的起点。

<table>
<tr>
<td width="50%" valign="top">

### EverCore

受生物印记启发的自组织记忆操作系统。从对话中提取、结构化并检索长期知识，使智能体能够记住、理解并持续进化。

LoCoMo **93.05%** · LongMemEval **83.00%**

[论文](https://arxiv.org/abs/2601.02163) · [文档](methods/EverCore/)

</td>
<td width="50%" valign="top">

### HyperMem

基于超图的层次化记忆架构，通过超边捕捉高阶关联，包含主题、事件和事实层，支持从粗到细的对话检索。

LoCoMo **92.73%**

[论文](https://arxiv.org/abs/2604.08256) · [文档](methods/HyperMem/)

</td>
</tr>
</table>

<br>
<div align="right">

[![](https://img.shields.io/badge/-Back_to_top-gray?style=flat-square)](#readme-top)

</div>

## 基准测试

这些基准测试为跨系统衡量记忆质量和智能体自进化能力提供了统一标准。

<table>
<tr>
<td width="50%" valign="top">

### EverMemBench

三层记忆质量评估：事实回忆、应用推理与个性化泛化。

[论文](https://arxiv.org/abs/2602.01313) · [数据集](https://huggingface.co/datasets/EverMind-AI/EverMemBench-Dynamic) · [文档](benchmarks/EverMemBench/)

</td>
<td width="50%" valign="top">

### EvoAgentBench

通过纵向成长曲线、迁移效率、错误规避和技能命中率来评估智能体自进化能力。

[数据集](https://huggingface.co/datasets/EverMind-AI/EvoAgentBench) · [文档](benchmarks/EvoAgentBench/)

</td>
</tr>
</table>

<br>
<div align="right">

[![](https://img.shields.io/badge/-Back_to_top-gray?style=flat-square)](#readme-top)

</div>

## 评估

使用评估运行器复现 EverCore 结果，或将其他记忆系统与相同的基准任务进行对比。

### 基准测试结果

![EverOS Benchmark Results](https://github.com/user-attachments/assets/41b656e7-6f82-41b7-891d-d6079d10dd39)

### 支持的基准测试

- **[LoCoMo](https://github.com/snap-research/locomo)** — 支持单跳/多跳推理的长上下文记忆基准测试
- **[LongMemEval](https://huggingface.co/datasets/xiaowu0162/longmemeval-cleaned)** — 多会话对话评估数据集
- **[PersonaMem](https://huggingface.co/datasets/bowen-upenn/PersonaMem)** — 基于人格的记忆评估数据集

### 运行评估

```bash
cd methods/EverCore

# Install evaluation dependencies
uv sync --group evaluation

# Run smoke test (quick verification)
uv run python -m evaluation.cli --dataset locomo --system everos --smoke

# Run full evaluation
uv run python -m evaluation.cli --dataset locomo --system everos

# View results
cat evaluation/results/locomo-everos/report.txt
```

[完整评估指南](methods/EverCore/evaluation/README.md) · [全部结果](https://huggingface.co/datasets/EverMind-AI/everos_Eval_Results)

<br>
<div align="right">

[![](https://img.shields.io/badge/-Back_to_top-gray?style=flat-square)](#readme-top)

</div>

## 引用文献

如果 EverOS 对你的研究有所帮助，请引用相关论文：

```bibtex
@article{hu2026evermemos,
  title   = {EverMemOS: A Self-Organizing Memory Operating System for Structured Long-Horizon Reasoning},
  author  = {Chuanrui Hu and Xingze Gao and Zuyi Zhou and Dannong Xu and Yi Bai and Xintong Li and Hui Zhang and Tong Li and Chong Zhang and Lidong Bing and Yafeng Deng},
  journal = {arXiv preprint arXiv:2601.02163},
  year    = {2026}
}

@article{yue2026hypermem,
  title   = {HyperMem: Hypergraph Memory for Long-Term Conversations},
  author  = {Juwei Yue and Chuanrui Hu and Jiawei Sheng and Zuyi Zhou and Wenyuan Zhang and Tingwen Liu and Li Guo and Yafeng Deng},
  journal = {arXiv preprint arXiv:2604.08256},
  year    = {2026}
}

@article{hu2026evaluating,
  title   = {Evaluating Long-Horizon Memory for Multi-Party Collaborative Dialogues},
  author  = {Chuanrui Hu and Tong Li and Xingze Gao and Hongda Chen and Yi Bai and Dannong Xu and Tianwei Lin and Xiaohong Li and Yunyun Han and Jian Pei and Yafeng Deng},
  journal = {arXiv preprint arXiv:2602.01313},
  year    = {2026}
}
```

<br>
<div align="right">

[![](https://img.shields.io/badge/-Back_to_top-gray?style=flat-square)](#readme-top)

</div>

## 持续关注

给仓库点星或加入上方的社区链接，以关注新的架构方法、基准测试发布以及记忆赋能的应用场景。

![star us gif](https://github.com/user-attachments/assets/0c512570-945a-483a-9f47-8e067bd34484)

<br>
<div align="right">

[![](https://img.shields.io/badge/-Back_to_top-gray?style=flat-square)](#readme-top)

</div>

## 贡献指南

欢迎为整个仓库做出贡献：涵盖架构方法、基准测试覆盖范围、用例示例、文档完善和 Bug 修复。浏览 [Issues](https://github.com/EverMind-AI/EverOS/issues) 寻找合适的切入点，准备就绪后提交 PR。

<br>

> [!TIP]
>
> **欢迎各种形式的贡献** 🎉
>
> 帮助 EverOS 变得更好。代码、文档、基准测试报告、用例撰写和集成示例都极具价值。欢迎在社交媒体上分享你的项目以激励他人。
>
> 如需获取项目更新、参与讨论或寻求合作机会，可通过 𝕏 联系 [@elliotchen200](https://x.com/elliotchen200) 或在 GitHub 上联系 [@cyfyifanchen](https://github.com/cyfyifanchen)。

![divider](https://github.com/user-attachments/assets/2e2bbcc6-e6d8-4227-83c6-0620fc96f761#gh-light-mode-only)
![divider](https://github.com/user-attachments/assets/d57fad08-4f49-4a1c-bdfc-f659a5d86150#gh-dark-mode-only)

### 代码贡献者

[![EverOS Contributors](https://contrib.rocks/image?repo=EverMind-AI/EverOS)](https://github.com/EverMind-AI/EverOS/graphs/contributors)

![divider](https://github.com/user-attachments/assets/2e2bbcc6-e6d8-4227-83c6-0620fc96f761#gh-light-mode-only)
![divider](https://github.com/user-attachments/assets/d57fad08-4f49-4a1c-bdfc-f659a5d86150#gh-dark-mode-only)

### 贡献指南

请阅读 [Contribution Guidelines](.github/CONTRIBUTING.md) 了解环境配置、PR 规范及用例提交说明。如需负责任地披露安全问题，请参阅 [Security Policy](.github/SECURITY.md)。

![divider](https://github.com/user-attachments/assets/2e2bbcc6-e6d8-4227-83c6-0620fc96f761#gh-light-mode-only)
![divider](https://github.com/user-attachments/assets/d57fad08-4f49-4a1c-bdfc-f659a5d86150#gh-dark-mode-only)

### 许可证、行为准则与鸣谢

[Apache 2.0](https://github.com/EverMind-AI/EverOS/blob/main/LICENSE) • [Code of Conduct](.github/CODE_OF_CONDUCT.md) • [Acknowledgments](methods/EverCore/docs/ACKNOWLEDGMENTS.md)

<br>

<div align="right">

[![](https://img.shields.io/badge/-Back_to_top-gray?style=flat-square)](#readme-top)

</div>
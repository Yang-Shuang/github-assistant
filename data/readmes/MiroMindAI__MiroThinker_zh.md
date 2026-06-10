<div align="center">
  <img src="assets/mirothinker_logo.png" width="55%" alt="MiroThinker" />
</div>

<br>

<div align="center">

[![MODEL](https://img.shields.io/badge/Model-FFD21E?style=for-the-badge&logo=huggingface&logoColor=white)](https://huggingface.co/collections/miromind-ai/mirothinker-17)
[![REPORT](https://img.shields.io/badge/Report-B31B1B?style=for-the-badge&logo=arxiv&logoColor=white)](https://arxiv.org/pdf/2603.15726)
[![Blog](https://img.shields.io/badge/Blog-4285F4?style=for-the-badge&logo=google-chrome&logoColor=white)](https://miromind.ai/#blog)
[![DATA](https://img.shields.io/badge/Data-0040A1?style=for-the-badge&logo=huggingface&logoColor=ffffff&labelColor)](https://huggingface.co/datasets/miromind-ai/MiroVerse-v0.1)

[![GITHUB](https://img.shields.io/badge/Github-24292F?style=for-the-badge&logo=github&logoColor=white)](https://github.com/MiroMindAI)
[![WEBSITE](https://img.shields.io/badge/Website-4285F4?style=for-the-badge&logo=google-chrome&logoColor=white)](https://miromind.ai/)
[![DISCORD](https://img.shields.io/badge/Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.com/invite/GPqEnkzQZd)

</div>

<div align="center">

### 🚀 [体验 MiroThinker!](https://dr.miromind.ai/)

</div>

**MiroThinker**: 一款针对研究与预测优化的深度研究智能体（Deep Research Agent）。它在极具挑战性的 BrowseComp 基准测试中取得了 88.2 分的成绩。详见 [快速开始](#-quick-start)。


## 📋 目录

- 📰 [新闻与更新](#-news--updates)
- 📝 [简介](#-introduction)
- ✨ [核心特性](#-key-features)
- 📈 [基准测试表现](#-performance-on-benchmarks)
- 🚀 [快速开始](#-quick-start)
- 📊 [基准评估](#-benchmark-evaluation)
- 🔬 [轨迹收集](#-trace-collection)
- ❓ [常见问题与故障排除](#-faq--troubleshooting)
- 📄 [许可证](#-license)
- 🙏 [致谢](#-acknowledgments)

## 📰 新闻与更新
- **[2026-03-11]** 🎉🎉🎉 推出 [MiroThinker-1.7](https://huggingface.co/collections/miromind-ai/mirothinker-17)，包含 [MiroThinker-1.7-mini](https://huggingface.co/miromind-ai/MiroThinker-1.7-mini) 和 [MiroThinker-1.7](https://huggingface.co/miromind-ai/MiroThinker-1.7)。MiroThinker-1.7-mini 在 BrowseComp-ZH 上取得 72.3 分的成绩，同时仅使用 30B 参数量级便在开源模型中创下新的 SOTA（State-of-the-Art）记录。我们的专有智能体 MiroThinker-H1 在 BrowseComp 和 BrowseComp-ZH 上的表现均领先于所有开源及商业模型。
- **\[2026-01-23\]** 🎉 我们为 [MiroThinker 在线平台](http://dr.miromind.ai)带来了两项重要更新：(a) 核心研究报告生成：深度研究在线报告现已支持生成、预览与分享。(b) 扩展文档上传类型：现支持上传多种文件格式，如 `.pdf`、`.doc`、`.ppt`、`.xls`、`.jpg`。欢迎试用！MiroThinker 将持续维护并迭代升级，致力于成为你使用过的最佳研究智能体！ 
- **\[2026-01-05\]** 🎉🎉 我们发布了 [MiroThinker-v1.5](https://huggingface.co/collections/miromind-ai/mirothinker-v15)，这是一系列针对金融预测优化的开源深度研究智能体。[MiroThinker-v1.5-30B](https://huggingface.co/miromind-ai/MiroThinker-v1.5-30B) 以仅 1/30 的参数量级，在 BrowseComp-ZH 上超越了 Kimi-K2-Thinking，且成本大幅降低。[MiroThinker-v1.5-235B](https://huggingface.co/miromind-ai/MiroThinker-v1.5-235B) 在 HLE-Text、BrowseComp、BrowseComp-ZH 和 GAIA-Val-165 上分别取得 39.2%、69.8%、71.5% 和 80.8% 的成绩，刷新了搜索智能体的 SOTA 记录。


<details>
  <summary>📜 点击展开历史更新</summary>

- **\[2025-11-13\]** 🎉 [MiroThinker-v1.0](https://huggingface.co/collections/miromind-ai/mirothinker-v10) 现已发布！引入**交互扩展（Interactive Scaling）**作为性能提升的第三维度，MiroThinker v1.0 支持 256K 上下文窗口和每个任务最多 600 次工具调用。提供 8B、30B 和 72B 参数量级版本，分别在 HLE-Text、BrowseComp、BrowseComp-ZH 和 GAIA-Text-103 上取得 37.7%、47.1%、55.6% 和 81.9% 的成绩。详见 [技术报告](https://arxiv.org/abs/2511.11793)。
- **\[2025-09-11\]** MiroThinker-72B-Preview 在本周的 FutureX 基准测试中排名第 4。参见 [FutureX](https://futurex-ai.github.io/)。
- **\[2025-09-08\]** [MiroThinker-v0.2](https://huggingface.co/collections/miromind-ai/mirothinker-v02) 现已发布，在多个基准测试中取得开源 SOTA 表现，包括 HLE (17.8%)、HLE-Text-Only (19.1%)、BrowseComp-EN (17.2%)、BrowseComp-ZH (29.4%)、XBench-DeepSearch (56.0%) 和 Frames (74.8%)。
- **\[2025-09-07\]** 我们支持了更多基准测试，包括 [BrowseComp-ZH](https://arxiv.org/abs/2504.19314)、[XBench-DeepSearch](https://xbench.org/agi/aisearch) 和 [FutureX](https://futurex-ai.github.io/)。我们计划在未来添加更多基准测试。
- **\[2025-08-22\]** 推出精简化的 MiroThinker 部署选项，优化了资源使用并缩短了启动时间。体验交互演示：[🚀 尝试 Gradio Demo](apps/gradio-demo)
- **\[2025-08-08\]** [MiroThinker-v0.1](https://huggingface.co/collections/miromind-ai/mirothinker-v01-689301b6d0563321862d44a1) 发布。

</details>

## 📝 简介

### MiroThinker-1.7
我们全新的 MiroThinker 家族在构建用于长链任务的可靠智能体方面实现了重大飞跃。凭借增强的后训练流水线，我们的 MiroThinker-1.7 家族在深度研究任务中达到了开源模型的 SOTA 表现。


**核心特性**

- 🚀 MiroThinker-1.7 支持 256K 上下文窗口、长视野推理和深度的多步分析。
- 🔧 每个任务可处理多达 300 次工具交互，现在具备更精确的逐步推理与决策能力。
- 📦 提供 30B 和 235B 两种参数量级版本，并附带全面的工具与工作流套件，灵活支持多样化的研究场景与计算预算。
- 🔬 我们的专有智能体 MiroThinker-H1 为长链可验证推理提供了有力证据——即步骤可验证且全局可验证的推理过程，从而提升了复杂智能体工作流的性能。

<div align="center">

|      模型名称       |         参数量级            | 最大上下文 | 最大工具调用次数 |                              HuggingFace 链接                               |
|:---------------------:|:-----------------------------:|:-----------:|:--------------:|:------------------------------------------------------------------:|
| MiroThinker-1.7-mini  | 30B   |    256K     |      300       | [🤗 link](https://huggingface.co/miromind-ai/MiroThinker-1.7-mini) |
| MiroThinker-1.7 | 235B |    256K     |      300       | [🤗 link](https://huggingface.co/miromind-ai/MiroThinker-1.7) |

</div>

MiroThinker-1.7 在广泛的基准测试中展现出强大的通用研究性能，分别在 BrowseComp、BrowseComp-ZH、GAIA-Val-165 和 HLE-Text 上取得 74.0%、75.3%、82.7% 和 42.9% 的成绩。MiroThinker-1.7 在 BrowseComp-ZH 上达到了 SOTA 表现。

![image](/assets/1.7_main_results.png)




### MiroThinker-v1.5

<details>
  <summary>📦 点击展开 MiroThinker-v1.5 详情</summary>

MiroThinker v1.5 是全球领先的开源搜索智能体，通过**交互扩展（Interactive Scaling）**推动工具增强推理的发展——将训练重点放在让智能体处理更深、更频繁的智能体-环境交互上，作为模型尺寸和上下文长度之外的第三维性能提升手段。

![image](https://huggingface.co/datasets/miromind-ai/MiroFlow-Benchmarks/resolve/main/assets/mirothinker_v1.5_framework.png)

**核心特性**

- 🚀 MiroThinker v1.5 支持 256K 上下文窗口、长视野推理和深度的多步分析。
- 🔧 每个任务可处理多达 400 次工具调用——相较于以往的开源研究智能体有显著提升。
- 📦 提供 30B 和 235B 两种参数量级版本，并附带全面的工具与工作流套件，灵活支持多样化的研究场景与计算预算。

<div align="center">

|      智能体名称       |         基础模型            | 最大上下文 | 最大工具调用次数 |                              HuggingFace 链接                               |
|:---------------------:|:-----------------------------:|:-----------:|:--------------:|:------------------------------------------------------------------:|
| MiroThinker-v1.5-30B  | Qwen3-30B-A3B-Thinking-2507   |    256K     |      400       | [🤗 link](https://huggingface.co/miromind-ai/MiroThinker-v1.5-30B) |
| MiroThinker-v1.5-235B | Qwen3-235B-A22B-Thinking-2507 |    256K     |      400       | [🤗 link](https://huggingface.co/miromind-ai/MiroThinker-v1.5-235B) |

</div>

MiroThinker v1.5 在广泛的基准测试中展现出强大的通用研究性能，分别在 HLE-Text、BrowseComp、BrowseComp-ZH 和 GAIA-Val-165 上取得 39.2%、69.8%、71.5% 和 80.8% 的成绩。这些结果超越了以往的开源智能体，并刷新了 BrowseComp 的 SOTA 表现记录。

![image](https://huggingface.co/datasets/miromind-ai/MiroFlow-Benchmarks/resolve/main/assets/mirothinker_v1.5_browsecomp.png)

</details>

### MiroThinker-v1.0

<details>
  <summary>📦 点击展开 MiroThinker-v1.0 详情</summary>

与以往仅扩展模型尺寸或上下文长度的智能体不同，MiroThinker v1.0 在智能体层面引入了**交互扩展（Interactive Scaling）**，系统性地训练智能体处理更深、更频繁的智能体-环境交互，作为性能提升的第三维度。交互扩展利用环境反馈和外部信息获取来纠正错误并优化推理轨迹。

![image](https://huggingface.co/datasets/miromind-ai/MiroFlow-Benchmarks/resolve/main/assets/MiroThinker_v1.0_Overall.png)

### ✨ 核心特性

- 🚀 **256K 上下文窗口**：支持长视野推理和深度的多步分析
- 🔧 **600 次工具调用**：每个任务最多可处理 600 次工具调用——相较于以往的开源研究智能体有显著提升
- 📦 **多种参数量级**：提供 8B、30B 和 72B 版本，并附带全面的工具与工作流套件，灵活支持多样化的研究场景与计算预算

<div align="center">

|      智能体名称       |         基础模型          | 最大上下文 | 最大工具调用次数 |                              HuggingFace 链接                               |
|:--------------------:|:---------------------------:|:-----------:|:--------------:|:------------------------------------------------------------------:|
| MiroThinker-v1.0-8B  |        Qwen3-8B             |    256K     |      600       | [🤗 link](https://huggingface.co/miromind-ai/MiroThinker-v1.0-8B)  |
| MiroThinker-v1.0-30B | Qwen3-30B-A3B-Thinking-2507 |    256K    |      600       | [🤗 link](https://huggingface.co/miromind-ai/MiroThinker-v1.0-30B) |
| MiroThinker-v1.0-72B |    Qwen2.5-72B-Instruct     |    256K    |      600       | [🤗 link](https://huggingface.co/miromind-ai/MiroThinker-v1.0-72B) |

</div>

MiroThinker v1.0 在广泛的基准测试中展现出强大的通用研究性能，分别在 HLE-Text、BrowseComp、BrowseComp-ZH 和 GAIA-Text-103 上取得 **37.7%**、**47.1%**、**55.6%** 和 **81.9%** 的成绩。这些结果超越了以往的开源智能体，并缩小了与 **GPT-5-high** 等商业模型之间的差距。

<div align="center">
  <img src="https://huggingface.co/datasets/miromind-ai/MiroFlow-Benchmarks/resolve/main/assets/MiroThinker_v1.0_Performance_1.png" width="100%" alt="MiroThinker" />
</div>

</details>

### MiroThinker-v0.2

<details>
  <summary>📦 点击展开 MiroThinker-v0.2 详情</summary>

在此新版本中，我们引入了三项关键改进：

- 📚 **更丰富的训练数据**：涵盖英文和中文来源的数据，显著提升了基准测试表现与泛化能力
- 🎯 **统一的 DPO 训练**：使用单一偏好数据集对所有智能体进行训练
- 📏 **扩展上下文长度**：从 40k 提升至 64k，以应对更具挑战性的多轮工具调用任务

相较于 v0.1，MiroThinker v0.2 在各项基准测试中均实现了稳定提升。例如，在 **GAIA-Text-103** 上得分从 **57.3 → 64.1**，在 **BrowseComp-ZH** 上从 **17.0 → 29.4**，反映出模型通用研究智能体能力的重大进步。

<div align="center">

|        智能体名称         |      基础模型       | 最大上下文 |                                HuggingFace 链接                                 |
|:------------------------:|:---------------------:|:-----------:|:----------------------------------------------------------------------:|
| MiroThinker-4B-SFT-v0.2  |       Qwen3-4B        |    64K     | [🤗 link](https://huggingface.co/miromind-ai/MiroThinker-4B-SFT-v0.2)  |
| MiroThinker-4B-DPO-v0.2  |       Qwen3-4B        |    64K     | [🤗 link](https://huggingface.co/miromind-ai/MiroThinker-4B-DPO-v0.2)  |
| MiroThinker-8B-SFT-v0.2  |       Qwen3-8B        |    64K     | [🤗 link](https://huggingface.co/miromind-ai/MiroThinker-8B-SFT-v0.2)  |
| MiroThinker-8B-DPO-v0.2  |       Qwen3-8B        |    64K     | [🤗 link](https://huggingface.co/miromind-ai/MiroThinker-8B-DPO-v0.2)  |
| MiroThinker-14B-SFT-v0.2 |       Qwen3-14B       |    64K     | [🤗 link](https://huggingface.co/miromind-ai/MiroThinker-14B-SFT-v0.2) |
| MiroThinker-14B-DPO-v0.2 |       Qwen3-14B       |    64K     | [🤗 link](https://huggingface.co/miromind-ai/MiroThinker-14B-DPO-v0.2) |
| MiroThinker-32B-SFT-v0.2 |       Qwen3-32B       |    64K     | [🤗 link](https://huggingface.co/miromind-ai/MiroThinker-32B-SFT-v0.2) |
| MiroThinker-32B-DPO-v0.2 |       Qwen3-32B       |    64K     | [🤗 link](https://huggingface.co/miromind-ai/MiroThinker-32B-DPO-v0.2) |

</div>

</details>

### MiroThinker-v0.1

<details>
  <summary>📦 点击展开 MiroThinker-v0.1 详情</summary>

<div align="center">
  <img src="assets/gaia_text_103.png" width="98%" alt="MiroFlow Performance on GAIA-Validation" />
  <p><strong>开源智能体在 GAIA-Validation 基准测试中的表现。</strong></p>
</div>

我们发布了 **MiroThinker v0.1** 系列，包含 **8B**、**14B** 和 **32B** 参数量级的 SFT 与 DPO 变体。值得注意的是，MiroThinker v0.1 在 [GAIA benchmark](https://huggingface.co/datasets/gaia-benchmark/GAIA)（一项针对高级智能体能力的严格评估套件）上取得了开源模型中的 **SOTA 表现**，证明了其在长上下文、高决策强度及真实任务场景下的强大能力。

<div align="center">

| Agent Name                | Base Agent | Max Context | HF Link                                                               |
| :-----------------------: |:----------:|:-----------:| :--------------------------------------------------------------------:|
| MiroThinker-8B-SFT-v0.1   |  Qwen3-8B  |    40K     | [🤗 link](https://huggingface.co/miromind-ai/MiroThinker-8B-SFT-v0.1)  |
| MiroThinker-8B-DPO-v0.1   |  Qwen3-8B  |    40K     | [🤗 link](https://huggingface.co/miromind-ai/MiroThinker-8B-DPO-v0.1)  |
| MiroThinker-14B-SFT-v0.1  | Qwen3-14B  |    40K     | [🤗 link](https://huggingface.co/miromind-ai/MiroThinker-14B-SFT-v0.1) |
| MiroThinker-14B-DPO-v0.1  | Qwen3-14B  |    40K     | [🤗 link](https://huggingface.co/miromind-ai/MiroThinker-14B-DPO-v0.1) |
| MiroThinker-32B-SFT-v0.1  | Qwen3-32B  |    40K     | [🤗 link](https://huggingface.co/miromind-ai/MiroThinker-32B-SFT-v0.1) |
| MiroThinker-32B-DPO-v0.1  | Qwen3-32B  |    40K     | [🤗 link](https://huggingface.co/miromind-ai/MiroThinker-32B-DPO-v0.1) |

</div>

</details>

## ✨ 核心特性

### 🤖 **MiroThinker 优化框架**

- 🔓 **完全开源的智能体框架**：框架与智能体全面开放，实现完全透明
- 🔗 **工具集成**：无缝对接外部工具与 API
- 📝 **轨迹收集（Trace Collection）**：提供全面的日志记录与交互分析功能，显示耗时及预估完成时间（分钟级），可直接用于 SFT 和 DPO 训练
- 📊 **基准评估**：在多个基准数据集上进行了广泛测试

### 📊 **综合基准套件**

<details open>
  <summary>📋 点击展开基准列表</summary>

- **GAIA Validation**: 通用 AI 助手基准测试。([论文](https://arxiv.org/abs/2311.12983))
- **GAIA-Text-103**: GAIA Validation 中专为纯文本任务设计的子集。([论文](https://arxiv.org/abs/2505.22648))
- **HLE**: Humanity's Last Exam（人类终极考试）。([论文](https://arxiv.org/abs/2501.14249))
- **HLE-Text-2158**: HLE 中专为纯文本任务设计的子集。([论文](https://arxiv.org/abs/2501.14249))
- **HLE-Text-500**: HLE 中专为纯文本任务设计的子集，由 [WebThinker](https://arxiv.org/pdf/2504.21776) 创建。([论文](https://arxiv.org/pdf/2504.21776))
- **BrowseComp-EN**: 网页浏览与理解任务。([论文](https://arxiv.org/abs/2504.12516))
- **BrowseComp-ZH**: BrowseComp 的中文版。([论文](https://arxiv.org/abs/2504.19314))
- **WebWalkerQA**: 网页导航与问答任务。([论文](https://arxiv.org/abs/2501.07572))
- **Frames**: Factuality, Retrieval, And reasoning MEasurement Set（事实性、检索与推理测量集）。([论文](https://arxiv.org/abs/2409.12941))
- **XBench-DeepSearch**: 深度研究智能体基准测试。([官网](https://xbench.org/agi/aisearch))
- **FutureX**: 专为预测未知未来设计的实时基准测试。([官网](https://futurex-ai.github.io/))
- **SEAL-0**: 评估 LLM 在冲突证据网页问答中表现的基准测试。([论文](https://arxiv.org/abs/2506.01062))
- **AIME2025**: 美国邀请数学考试 2025。([官网](https://artificialanalysis.ai/evaluations/aime-2025))
- **DeepSearchQA**: Google 的深度搜索问答基准测试。([论文](https://arxiv.org/abs/2505.20827))

</details>

## 📈 基准测试表现

### MiroThinker-1.7

> 为防止潜在的信息泄露（例如从 HuggingFace 检索基准答案），我们在评估期间屏蔽了部分网站的访问权限。

<div>
  <img src="assets/17_table.png" width="100%" alt="MiroThinker" />
</div>



### MiroThinker-v1.5

<details>
  <summary>📦 点击展开 MiroThinker-v1.5 详情</summary>

> 为防止潜在的信息泄露（例如从 HuggingFace 搜索基准答案），这些工具中已明确禁用了对 HuggingFace 的访问权限。

> 我们进一步对所有轨迹的工具输出进行了 canary string（金丝雀字符串）测试，并忽略任何发现被污染的轨迹，将其视为错误答案。

<div>
  <img src="https://huggingface.co/datasets/miromind-ai/MiroFlow-Benchmarks/resolve/main/assets/mirothinker_v1.5_performance.png" width="100%" alt="MiroThinker" />
</div>

</details>

### MiroThinker-v1.0

<details>
  <summary>📦 点击展开 MiroThinker-v1.0 详情</summary>

<div align="center">
  <img src="https://github.com/user-attachments/assets/108a2105-4e1d-499e-a001-4713a03fd8ac" width="100%" alt="MiroThinker" />
</div>

</details>

### MiroThinker-v0.2

<details>
  <summary>📦 点击展开 MiroThinker-v0.2 详情</summary>

#### 与 SOTA 研究智能体对比

<div align="center">
  <img src="https://huggingface.co/datasets/miromind-ai/MiroFlow-Benchmarks/resolve/main/assets/MiroThinker_v0.2_Performance_2.png" width="90%" alt="MiroThinker" />
</div>

#### GAIA Benchmark

<div align="center">
  <img src="https://huggingface.co/datasets/miromind-ai/MiroFlow-Benchmarks/resolve/main/assets/MiroThinker_v0.2_Performance_1.png" width="80%" alt="MiroThinker" />
</div>

</details>

### MiroThinker-v0.1

<details>
  <summary>📦 点击展开 MiroThinker-v0.1 详情</summary>

#### GAIA Benchmark

<div align="center">

| **方法**                   | Text-103<br>最佳 Pass@1 | Text-103<br>Pass@1 (Avg@8) | Val-165<br>最佳 Pass@1 | Val-165<br>Pass@1 (Avg@8) |
|------------------------------|:-----------------------:|:--------------------------:|:----------------------:|:-------------------------:|
| **🔹—— 7B/8B 智能体 ——**     |                         |                            |                        |                           |
| Search-o1-7B                 |          17.5           |             -              |           -            |             -             |
| R1-Searcher-7B               |          20.4           |             -              |           -            |             -             |
| WebDancer-7B                 |          31.0           |             -              |           -            |             -             |
| WebSailor-7B                 |          37.9           |             -              |           -            |             -             |
| CK-Pro-8B                    |          40.3           |             -              |          32.7          |             -             |
| **MiroThinker-8B-SFT-v0.1**  |          44.7           |            40.1            |          34.6          |           31.8            |
|     + Commercial Tools       |          46.6           |            42.1            |          37.6          |           33.9            |
| **MiroThinker-8B-DPO-v0.1**  |          46.6           |            44.8            |          37.0          |           35.4            |
|     + Commercial Tools       |        **50.5**         |          **46.7**          |        **38.2**        |         **35.9**          |
| **🔹—— 14B 智能体 ——**       |                         |                            |                        |                           |
| **MiroThinker-14B-SFT-v0.1** |          47.6           |            44.4            |          37.0          |           34.4            |
|     + Commercial Tools       |          49.5           |            47.5            |          41.8          |           39.8            |
| **MiroThinker-14B-DPO-v0.1** |          48.5           |            46.6            |          42.4          |           39.2            |
|     + Commercial Tools       |        **52.4**         |          **48.5**          |        **45.5**        |         **42.0**          |
| **🔹—— 32B 智能体 ——**       |                         |                            |                        |                           |
| Qwen3-32B                    |          31.1           |            26.7            |          29.7          |           26.4            |
| Search-o1-32B                |          28.2           |             -              |           -            |             -             |
| WebThinker-32B-RL            |          48.5           |             -              |           -            |             -             |
| WebDancer-QwQ-32B            |          51.5           |             -              |           -            |             -             |
| WebSailor-32B                |          53.2           |             -              |           -            |             -             |
| WebShaper-QwQ-32B            |          53.3           |             -              |           -            |             -             |
| **MiroThinker-32B-SFT-v0.1** |          55.3           |            51.3            |          44.9          |           42.7            |
|     + Commercial Tools       |          58.3           |            54.2            |          48.5          |           45.8            |
| **MiroThinker-32B-DPO-v0.1** |          57.3           |            54.1            |          48.5          |           45.9            |
|     + Commercial Tools       |        **60.2**         |          **57.9**          |        **50.9**        |         **48.9**          |

</div>

1. 遵循 WebThinker、WebAgents 和 CognitiveKernel 的做法，我们报告 Best Pass@1（三次运行中的最高分数），这通常能反映更强的性能，但可能存在一定波动性。为了提供更稳定的指标，我们还额外报告了 Pass@1 (Avg@8)，它在牺牲少量分数的情况下提供了更高的稳定性。

2. 为与之前的开源工作保持一致，我们使用 WebAgents LLM-as-a-Judge（大模型裁判）模板评估 GAIA-Text-103，并使用官方 GAIA 评分脚本报告 GAIA-Val-165 的结果。

3. 默认情况下，我们在可能的情况下均使用开源工具，代码工具 [E2B](https://github.com/e2b-dev/E2B) 和 Google 搜索工具 [Serper](https://serper.dev/) 除外。我们的实现使用了 [Whisper](https://huggingface.co/openai/whisper-large-v3-turbo)、[Qwen2.5-VL-72B-Instruct](https://huggingface.co/Qwen/Qwen2.5-VL-72B-Instruct) 和 [Qwen3-235B-A22B-Thinking-2507](https://huggingface.co/Qwen/Qwen3-235B-A22B-Thinking-2507)。该框架可轻松扩展至你选择的任何其他开源工具。

4. 将这些开源工具替换为商业替代品可获得性能提升。商业工具主要用于多模态能力及某些复杂的推理子任务。大多数任务，包括规划、浏览、优化、导航等均由我们的智能体处理。

#### 更多基准测试

<div align="center">

| Method                       | HLE<br>Pass@1 | Frames<br>Pass@1 | BrowseComp<br>Pass@1 | BrowseComp-ZH<br>Pass@1 | WebWalkerQA<br>Pass@1 |
|------------------------------|:-------------:|:----------------:|:--------------------:|:-----------------------:|:---------------------:|
| OpenAI Deep Research         |     26.6      |        -         |         51.5         |          42.9           |           -           |
| Gemini Deep Research         |     26.9      |        -         |          -           |            -            |           -           |
| Kimi-Researcher              |     26.9      |       78.8       |          -           |            -            |           -           |
|                              |               |                  |                      |                         |                       |
| WebDancer-7B                 |       -       |        -         |          -           |            -            |         36.0          |
| WebSailor-7B                 |       -       |        -         |         6.7          |          14.2           |           -           |
| **MiroThinker-8B-SFT-v0.1**  |       -       |       58.0       |         5.5          |           9.3           |         41.3          |
| **MiroThinker-8B-DPO-v0.1**  |       -       |       64.4       |         8.7          |          13.6           |         45.7          |
|                              |               |                  |                      |                         |                       |
| WebThinker-32B-RL            |       -       |        -         |          -           |            -            |         46.5          |
| WebDancer-QwQ-32B            |       -       |        -         |         3.8          |          18.0           |         47.9          |
| WebSailor-32B                |       -       |        -         |         10.5         |          25.5           |           -           |
| WebShaper-32B                |       -       |        -         |          -           |            -            |         51.4          |
| **MiroThinker-32B-SFT-v0.1** |     10.2      |       70.4       |         10.6         |          13.8           |         45.7          |
| **MiroThinker-32B-DPO-v0.1** |     11.8      |       71.7       |         13.0         |          17.0           |         49.3          |

</div>

1. MiroThinker 的性能基于本仓库及开源工具测试；其他智能体的结果来自其论文与官方网站。
2. 由于 [MiroVerse-v0.1](https://huggingface.co/datasets/miromind-ai/MiroVerse-v0.1) 主要包含英文数据，该智能体的中文能力有限。我们计划在下一版本中添加更多中文数据以优化表现。

</details>

## 🚀 快速开始

为获得最佳使用体验，建议搭配本工具启用型智能体框架（Agent Framework）并开启思考模式运行 MiroThinker。

### 前置条件

- 🐍 **Python 3.10+**
- 📦 **uv 包管理器**（[安装指南](https://github.com/astral-sh/uv)）
- 🔑 **必需的 API Key**（详见下方配置部分）

### 安装步骤

```bash
# 克隆仓库
git clone https://github.com/MiroMindAI/MiroThinker
cd MiroThinker

# 设置环境
cd apps/miroflow-agent
uv sync

# 配置 API Keys
cp .env.example .env
# 在 .env 中编辑你的 API Key（SERPER_API_KEY, JINA_API_KEY, E2B_API_KEY 等）
```

> **📝 环境变量**：详见 [工具配置](#tool-configuration) 部分以获取必需的 API Keys。

### 工具配置

#### MiroThinker-1.7 最小化配置

| Server | 描述 | 提供的工具 | 必需的环境变量 |
|:-------|:------------|:---------------|:-------------------------------|
| **`tool-python`** | 执行环境与文件管理（E2B 沙箱） | `create_sandbox`, `run_command`, `run_python_code`, `upload_file_from_local_to_sandbox`, `download_file_from_sandbox_to_local`, `download_file_from_internet_to_sandbox` | `E2B_API_KEY` |
| **`search_and_scrape_webpage`** | 通过 Serper API 进行 Google 搜索 | `google_search` | `SERPER_API_KEY`, `SERPER_BASE_URL` |
| **`jina_scrape_llm_summary`** | 基于 LLM 信息提取的网页抓取 | `scrape_and_extract_info` | `JINA_API_KEY`, `JINA_BASE_URL`, `SUMMARY_LLM_BASE_URL`, `SUMMARY_LLM_MODEL_NAME`, `SUMMARY_LLM_API_KEY` |

**最小化 `.env` 配置示例：**

```bash
# MiroThinker v1.5 和 v1.0 必需（最小化设置）
SERPER_API_KEY=your_serper_key
SERPER_BASE_URL="https://google.serper.dev"
JINA_API_KEY=your_jina_key
JINA_BASE_URL="https://r.jina.ai"
E2B_API_KEY=your_e2b_key

# jina_scrape_llm_summary 必需
# 注意：摘要 LLM 可以是小模型（例如 Qwen3-14B 或 GPT-5-Nano）
# 选择对性能影响极小，使用你最方便的即可
SUMMARY_LLM_BASE_URL="https://your_summary_llm_base_url/v1/chat/completions"
SUMMARY_LLM_MODEL_NAME=your_llm_model_name  # 例如 "Qwen/Qwen3-14B" 或 "gpt-5-nano"
SUMMARY_LLM_API_KEY=your_llm_api_key  # 可选，取决于 LLM 提供商

# 基准评估必需（LLM-as-a-Judge）
OPENAI_API_KEY=your_openai_key  # 运行基准评估必需
OPENAI_BASE_URL="https://api.openai.com/v1"  # 可选，默认使用 OpenAI API
```

> **💡 为何这是最小化配置**：这 3 个 MCP Server 覆盖了研究任务所需的核心能力：网页搜索、内容提取和代码执行。其他服务器均为可选增强功能。
>
> **🤖 摘要 LLM（Summary LLM）**：`SUMMARY_LLM` 可以是 Qwen3-14B 或 GPT-5-Nano 等小模型。选择对整体性能影响极小，使用你最方便的即可。
>
> **📊 用于基准评估**：如果你计划运行基准测试，还需要 `OPENAI_API_KEY`（以及可选的 `OPENAI_BASE_URL`）以在评估脚本中使用 LLM-as-a-Judge 功能。
>
> **🖼️ 用于 GAIA 多模态任务**：GAIA-Val-165 包含带有图像/音频/视频文件的任务。由于 MiroThinker 是纯文本 LLM，GPT-4o 被用于将这些文件预处理为文本描述。相同的 `OPENAI_API_KEY` 同时用于此预处理和 LLM-as-a-Judge。
>
> **📖 更多详情**：参见 [MiroFlow Tools README](libs/miroflow-tools/README.md) 获取所有可用工具的完整文档。

<details>
  <summary>🔧 点击展开其他可用工具</summary>

以下可选工具在 MiroThinker v1.0-1.7 评估中未被使用：

| Server Name          | Type         | Description                                 |
|:---------------------|:-------------|:--------------------------------------------|
| `tool-vqa`           | Commercial   | 基于 Claude 的视觉处理              |
| `tool-vqa-os`        | Open-Source  | 视觉处理（开源替代方案） |
| `tool-transcribe`    | Commercial   | 基于 OpenAI 的音频转录            |
| `tool-transcribe-os` | Open-Source  | 基于 Whisper 的音频转录           |
| `tool-reasoning`     | Commercial   | 基于 Claude 的推理引擎               |
| `tool-reasoning-os`  | Open-Source  | 推理引擎（开源替代方案）  |
| `tool-reading`       | Open-Source  | 使用 MarkItDown 进行文档阅读           |
| `tool-google-search` | Commercial   | 使用 Google + 抓取的网络搜索          |
| `tool-sogou-search` | Commercial   | 使用搜狗（中文）的网络搜索           |

> **📖 本地部署**：有关在本地部署开源工具（`tool-vqa-os`, `tool-transcribe-os`, `tool-reasoning-os`）的说明，参见 [本地工具部署指南](assets/LOCAL-TOOL-DEPLOYMENT.md)。

所有可用工具的完整文档请参见 [MiroFlow Tools README](libs/miroflow-tools/README.md)。

</details>

#### 预置智能体设置

`apps/miroflow-agent/conf/agent/` 目录包含多个预配置的智能体设置。每个配置使用不同的工具，并需要在 `.env` 文件中提供相应的环境变量。

> **💡 推荐**：对于 MiroThinker-1.7，请使用 `mirothinker_1.7_keep5_max200`（带上下文管理，适用于大多数任务）或 `mirothinker_v1.7_keep5_max300`（仅用于 BrowseComp 和 BrowseComp-ZH）。 

| Configuration                          | Description | Max Turns | Context Retention | Required Environment Variables                                                                                                                               | Recommended For |
|:---------------------------------------|:------------|:----------|:------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------|
| **`mirothinker_1.7_keep5_max200`** ⭐  | Single-agent with context management | 200 | Keep 5 most recent | `SERPER_API_KEY`, `SERPER_BASE_URL`, `JINA_API_KEY`, `JINA_BASE_URL`, `E2B_API_KEY`, `SUMMARY_LLM_BASE_URL`, `SUMMARY_LLM_MODEL_NAME`, `SUMMARY_LLM_API_KEY` | **1.7 (推荐用于大多数任务)** |
| **`mirothinker_1.7_keep5_max300`** ⭐  | Single-agent with context management | 300 | Keep 5 most recent | Same as above                                                                                                                              | **1.7 (用于 BrowseComp & BrowseComp-ZH)** |


<details>
  <summary>📦 点击展开历史配置（v0.1/v0.2）</summary>

| Configuration            | Description | Max Turns | Context Retention | Required Environment Variables | Recommended For |
|:-------------------------|:------------|:----------|:------------------|:-------------------------------|:----------------|
| **`mirothinker_v1.5_keep5_max200`**  | Single-agent with context management | 200 | Keep 5 most recent | `SERPER_API_KEY`, `SERPER_BASE_URL`, `JINA_API_KEY`, `JINA_BASE_URL`, `E2B_API_KEY`, `SUMMARY_LLM_BASE_URL`, `SUMMARY_LLM_MODEL_NAME`, `SUMMARY_LLM_API_KEY` | **v1.5 (推荐用于大多数任务)** |
| **`mirothinker_v1.5_keep5_max400`**  | Single-agent with context management | 400 | Keep 5 most recent | Same as above                                                                                                                              | **v1.5 (用于 BrowseComp & BrowseComp-ZH)** |
| **`mirothinker_v1.5`**                 | Single-agent for MiroThinker v1.5 | 600 | Keep all results | Same as above | **v1.5** |
| **`mirothinker_v1.0_keep5`**           | Single-agent with context management | 600 | Keep 5 most recent | Same as above                                                                                                                                   | **v1.0** |
| **`mirothinker_v1.0`**                 | Single-agent for MiroThinker v1.0 | 600 | Keep all results | Same as above | **v1.0** |
| **`multi_agent`**        | Multi-agent with commercial tools (v0.1/v0.2) | 50 | Keep all results | `E2B_API_KEY`, `ANTHROPIC_API_KEY`, `ANTHROPIC_BASE_URL`, `OPENAI_API_KEY`, `OPENAI_BASE_URL`, `SERPER_API_KEY`, `SERPER_BASE_URL`, `JINA_API_KEY`, `JINA_BASE_URL` | v0.1/v0.2 |
| **`multi_agent_os`**     | Multi-agent with open-source tools (v0.1/v0.2) | 50 | Keep all results | `E2B_API_KEY`, `VISION_API_KEY`, `VISION_BASE_URL`, `VISION_MODEL_NAME`, `WHISPER_API_KEY`, `WHISPER_BASE_URL`, `WHISPER_MODEL_NAME`, `REASONING_API_KEY`, `REASONING_BASE_URL`, `REASONING_MODEL_NAME`, `SERPER_API_KEY`, `SERPER_BASE_URL`, `JINA_API_KEY`, `JINA_BASE_URL` | v0.1/v0.2 |

</details>

> **💡 注意**：所有环境变量均列于 `apps/miroflow-agent/.env.example`。将其复制至 `.env` 并填写你计划使用的工具对应的值。

#### 创建自定义工具配置

<details>
  <summary>🔧 点击展开自定义工具配置指南</summary>

你可以创建自己的 YAML 配置文件以自由组合 MCP Server。操作步骤如下：

1. **在 `apps/miroflow-agent/conf/agent/` 中创建新的 YAML 文件**：

```yaml
# conf/agent/my_custom_config.yaml
defaults:
  - default
  - _self_

main_agent:
  tools:
    - tool-python                    # 执行环境
    - search_and_scrape_webpage      # Google 搜索
    - jina_scrape_llm_summary        # LLM 网页抓取
    - tool-vqa                       # 视觉处理（可选）
    - tool-transcribe                # 音频处理（可选）
    - tool-reasoning                 # 推理引擎（可选）
    - tool-reading                   # 文档阅读（可选）
  max_turns: 300  # 最大回合数

sub_agents:
  agent-browsing:  # 可选的子智能体
    tools:
      - tool-google-search
      - tool-vqa
      - tool-reading
      - tool-python
    max_turns: 50

keep_tool_result: -1  # 上下文保留预算：-1 保留所有工具结果，或指定 K 仅保留最近的 K 个工具响应
```

> **💡 上下文保留策略**：`keep_tool_result` 参数实现了基于**近期优先（recency-based）**的上下文保留策略。在标准的 ReAct 范式中，所有工具输出都会保留在消息历史中，这可能导致上下文利用效率低下。经验表明，智能体的后续操作主要依赖于最近的观察结果而非遥远的历史记录。该策略仅保留最近的 K 个工具响应（K 为 `keep_tool_result` 的值），同时完整保留思维与行动序列。
>
> **优势：**
>
> - ✅ 保留推理与行动轨迹
> - ✅ 使智能体注意力聚焦于最具上下文相关性的观察结果
> - ✅ 释放更多上下文空间以支持更长的推理和更深入的工具使用轨迹
> - ✅ 在允许更多交互扩展空间的同时，不会导致性能下降
>
> **用法**：设置 `keep_tool_result: -1` 保留所有工具结果，或指定正整数 K（例如 `keep_tool_result: 5`）仅保留最近的 K 个工具响应。

2. **运行评估时使用你的自定义配置**：

```bash
cd apps/miroflow-agent
uv run main.py llm=qwen-3 agent=my_custom_config llm.base_url=https://your_base_url/v1
```

3. **根据你使用的工具在 `.env` 中配置环境变量**。

   所有可用的环境变量均列于 `apps/miroflow-agent/.env.example`。将其复制至 `.env` 并根据所选配置进行设置：

   ```bash
   cd apps/miroflow-agent
   cp .env.example .env
   # 在 .env 中编辑你的实际 API Key
   ```

   **对于 MiroThinker v1.5**（`mirothinker_v1.5_keep5_max200.yaml`, `mirothinker_v1.5_keep5_max400.yaml` 或 `mirothinker_v1.5.yaml`）和 **v1.0**（`mirothinker_v1.0_keep5.yaml` 或 `mirothinker_v1.0.yaml`），请参阅上方的 [最小化配置](#minimal-configuration-for-mirothinker-v15-and-v10) 部分获取完整配置示例。

   **对于其他配置**，请参考上方的 [预置智能体设置](#pre-configured-agent-settings) 表格查看所需的环境变量。

</details>

<details>
  <summary>🔑 点击展开可选 API Keys</summary>

```bash
# LLM-as-a-Judge API（用于基准测试，运行评估必需）
OPENAI_API_KEY=your_openai_key
OPENAI_BASE_URL="https://api.openai.com/v1"  # 可选，默认使用 OpenAI API

# 开源音频转录工具 API（用于基准测试，可选）
WHISPER_MODEL_NAME="openai/whisper-large-v3-turbo"
WHISPER_API_KEY=your_whisper_key
WHISPER_BASE_URL="https://your_whisper_base_url/v1"

# 开源 VQA 工具 API（用于基准测试，可选）
VISION_MODEL_NAME="Qwen/Qwen2.5-VL-72B-Instruct"
VISION_API_KEY=your_vision_key
VISION_BASE_URL="https://your_vision_base_url/v1/chat/completions"

# 开源推理工具 API（用于基准测试，可选）
REASONING_MODEL_NAME="Qwen/Qwen3-235B-A22B-Thinking-2507"
REASONING_API_KEY=your_reasoning_key
REASONING_BASE_URL="https://your_reasoning_base_url/v1/chat/completions"

# Claude Sonnet 3.7 商业工具 API（可选）
ANTHROPIC_API_KEY=your_anthropic_key

# 搜狗搜索 API（可选）
TENCENTCLOUD_SECRET_ID=your_tencent_cloud_secret_id
TENCENTCLOUD_SECRET_KEY=your_tencent_cloud_secret_key

# 摘要 LLM API（可使用 Qwen3-14B 或 GPT-5-Nano 等小模型）
SUMMARY_LLM_BASE_URL="https://your_summary_llm_base_url/v1/chat/completions"
SUMMARY_LLM_MODEL_NAME=your_summary_llm_model_name  # 例如 "Qwen/Qwen3-14B" 或 "gpt-5-nano"
SUMMARY_LLM_API_KEY=your_summary_llm_api_key
```

</details>

### 部署 MiroThinker 智能体服务

#### 方案一（推荐）：使用 SGLang 或 vLLM 提供服务

使用 SGLang 在端口 61002 上部署 MiroThinker 模型：

```bash
NUM_GPUS=4
PORT=61002

# 从 HF 下载智能体 
AGENT_PATH=miromind-ai/MiroThinker-1.7-mini


python3 -m sglang.launch_server \
    --model-path $AGENT_PATH \
    --tp $NUM_GPUS \
    --dp 1 \
    --host 0.0.0.0 \
    --port $PORT \
    --trust-remote-code
```

> **📍 服务器地址**：这将在 `http://0.0.0.0:$PORT` 启动服务。请将其作为你的服务端基础 URL（例如 `http://0.0.0.0:61002/v1`）。

#### 方案二：量化轻量级选项

我们还提供了使用 CPU 优化和 GPU 加速的量化技术来部署 MiroThinker 智能体的完整指南，以及针对 llama.cpp、Ollama、SGLang 等推理框架的详细分析与部署建议。

> **📖 完整指南**：参见 [部署文档](apps/gradio-demo/) 获取详细操作说明。

### 运行你的第一个任务

完成环境配置并启动服务后，运行 `main.py` 使用默认问题进行测试：*"What is the title of today's arxiv paper in computer science?"*（今天计算机科学领域 arXiv 论文的标题是什么？）

```bash
cd apps/miroflow-agent

# 使用 MiroThinker 智能体（需配置你自己的服务端）
uv run python main.py llm=qwen-3 agent=mirothinker_1.7_keep5_max200 llm.base_url=http://localhost:61002/v1

# 或使用 Claude（需在 .env 中设置 ANTHROPIC_API_KEY）
uv run python main.py llm=claude-3-7 agent=single_agent_keep5

# 或使用 GPT-5（需在 .env 中设置 OPENAI_API_KEY）
uv run python main.py llm=gpt-5 agent=single_agent_keep5
```

**自定义你的问题**，请编辑 `main.py` 第 32 行：

```python
task_description = "Your custom question here"
```

智能体将搜索网页、按需执行代码，并提供带有来源的答案。

> **📖 更多详情**：参见 [apps/miroflow-agent/README.md](apps/miroflow-agent/README.md) 获取可用配置与故障排除指南。

## 📊 基准评估

> 供希望复现我们基准结果或在标准基准上自行评估的研究人员使用。

### 下载基准数据

```bash
cd MiroThinker  # 返回项目根目录
wget https://huggingface.co/datasets/miromind-ai/MiroFlow-Benchmarks/resolve/main/data_20251115_password_protected.zip
unzip data_20251115_password_protected.zip
# 密码: pf4*
rm data_20251115_password_protected.zip
```

### 运行基准评估

> **注意**：对于 MiroThinker-1.7，请使用 `mirothinker_1.7_keep5_max200`（带上下文管理）或 `mirothinker_1.7_keep5_max300`（带上下文管理）。

**可用参数：**

你可以通过在运行脚本前设置以下环境变量来自定义评估：

| 参数 | 默认值 | 描述 |
|:----------|:--------|:------------|
| `LLM_MODEL` | `"MiroThinker-Agents"` | 智能体名称标识符 |
| `BASE_URL` | `"https://your-api.com/v1"` | 服务端基础 URL |
| `NUM_RUNS` | 因基准而异 | 评估运行次数（大多数基准为 3，GAIA/XBench/FutureX/SEAL-0 为 8，AIME2025 为 32） |
| `LLM_PROVIDER` | `"qwen"` | LLM 提供商（例如 `qwen`, `openai`, `anthropic`） |
| `AGENT_SET` | `"mirothinker_1.7_keep5_max200"` | 智能体配置（例如 `mirothinker_1.7_keep5_max200`, `mirothinker_1.7_keep5_max300`。） |
| `MAX_CONTEXT_LENGTH` | `262144` | 最大上下文长度（256K） |
| `MAX_CONCURRENT` | `10` | 最大并发任务数 |
| `PASS_AT_K` | `1` | Pass@K 评估指标 |
| `TEMPERATURE` | `1.0` | 采样温度 |
| `API_KEY` | `"xxx"` | 服务端 API Key |

**使用示例：**

```bash
# 首先导航至 miroflow-agent 目录
cd apps/miroflow-agent

# 基础用法（v1.5，推荐）
NUM_RUNS=8 LLM_MODEL="MiroThinker-1.7-mini" BASE_URL="https://your-api.com/v1" bash scripts/run_evaluate_multiple_runs_gaia-validation-text-103.sh

# 或使用 v1.0
# NUM_RUNS=8 LLM_MODEL="MiroThinker-v1.0-30B" BASE_URL="https://your-api.com/v1" bash scripts/run_evaluate_multiple_runs_gaia-validation-text-103.sh

# 自定义运行次数与智能体配置（v1.5 带上下文管理）
LLM_MODEL="MiroThinker-1.7-mini" \
BASE_URL="https://your-api.com/v1" \
NUM_RUNS=8 \
AGENT_SET="mirothinker_1.7_keep5_max200" \
bash scripts/run_evaluate_multiple_runs_gaia-validation-text-103.sh

```

<details open>
  <summary>📋 点击展开所有基准测试命令</summary>

> **⚠️ MiroThinker-1.7 重要提示**：为复现我们报告的结果，你必须设置正确的 `AGENT_SET`：
>
> - **BrowseComp & BrowseComp-ZH**：使用 `AGENT_SET="mirothinker_1.7_keep5_max300"`
> - **所有其他基准测试**：使用 `AGENT_SET="mirothinker_1.7_keep5_max200"`

```bash
# 首先导航至 miroflow-agent 目录
cd apps/miroflow-agent

# HLE
NUM_RUNS=3 LLM_MODEL="xxx" BASE_URL="xxx" AGENT_SET="mirothinker_1.7_keep5_max200" bash scripts/run_evaluate_multiple_runs_hle.sh

# HLE-Text-2158
NUM_RUNS=3 LLM_MODEL="xxx" BASE_URL="xxx" AGENT_SET="mirothinker_1.7_keep5_max200" bash scripts/run_evaluate_multiple_runs_hle-text-2158.sh

# HLE-Text-500
NUM_RUNS=3 LLM_MODEL="xxx" BASE_URL="xxx" AGENT_SET="mirothinker_1.7_keep5_max200" bash scripts/run_evaluate_multiple_runs_hle-text-500.sh

# GAIA-Text-103
NUM_RUNS=8 LLM_MODEL="xxx" BASE_URL="xxx" AGENT_SET="mirothinker_1.7_keep5_max200" bash scripts/run_evaluate_multiple_runs_gaia-validation-text-103.sh

# GAIA-Validation (GAIA-Val-165)
NUM_RUNS=8 LLM_MODEL="xxx" BASE_URL="xxx" AGENT_SET="mirothinker_1.7_keep5_max200" bash scripts/run_evaluate_multiple_runs_gaia-validation.sh

# BrowseComp-EN（⚠️ 使用 max300）
NUM_RUNS=3 LLM_MODEL="xxx" BASE_URL="xxx" AGENT_SET="mirothinker_1.7_keep5_max300" bash scripts/run_evaluate_multiple_runs_browsecomp.sh

# BrowseComp-ZH（⚠️ 使用 max300）
NUM_RUNS=3 LLM_MODEL="xxx" BASE_URL="xxx" AGENT_SET="mirothinker_1.7_keep5_max300" bash scripts/run_evaluate_multiple_runs_browsecomp_zh.sh

# WebWalkerQA
NUM_RUNS=3 LLM_MODEL="xxx" BASE_URL="xxx" AGENT_SET="mirothinker_1.7_keep5_max200" bash scripts/run_evaluate_multiple_runs_webwalkerqa.sh

# XBench-DeepSearch
NUM_RUNS=8 LLM_MODEL="xxx" BASE_URL="xxx" AGENT_SET="mirothinker_1.7_keep5_max200" bash scripts/run_evaluate_multiple_runs_xbench_deepsearch.sh

# FRAMES
NUM_RUNS=3 LLM_MODEL="xxx" BASE_URL="xxx" AGENT_SET="mirothinker_1.7_keep5_max200" bash scripts/run_evaluate_multiple_runs_frames.sh

# SEAL-0
NUM_RUNS=8 LLM_MODEL="xxx" BASE_URL="xxx" AGENT_SET="mirothinker_1.7_keep5_max200" bash scripts/run_evaluate_multiple_runs_seal-0.sh

# FutureX
NUM_RUNS=8 LLM_MODEL="xxx" BASE_URL="xxx" AGENT_SET="mirothinker_1.7_keep5_max200" bash scripts/run_evaluate_multiple_runs_futurex.sh

# AIME2025
NUM_RUNS=32 LLM_MODEL="xxx" BASE_URL="xxx" AGENT_SET="mirothinker_1.7_keep5_max200" bash scripts/run_evaluate_multiple_runs_aime2025.sh

# DeepSearchQA
NUM_RUNS=3 LLM_MODEL="xxx" BASE_URL="xxx" AGENT_SET="mirothinker_1.7_keep5_max200" bash scripts/run_evaluate_multiple_runs_deepsearchqa.sh
```

</details>

#### 3. **监控评估进度**

<details>
  <summary>📊 点击展开进度监控命令</summary>

```bash
# 首先导航至 miroflow-agent 目录
cd apps/miroflow-agent

# HLE
python benchmarks/check_progress/check_progress_hle.py /path/to/evaluation/logs

# HLE-Text-2158
python benchmarks/check_progress/check_progress_hle-text-2158.py /path/to/evaluation/logs

# HLE-Text-500
python benchmarks/check_progress/check_progress_hle-text-500.py /path/to/evaluation/logs

# BrowseComp-EN
python benchmarks/check_progress/check_progress_browsecomp.py /path/to/evaluation/logs

# BrowseComp-ZH
python benchmarks/check_progress/check_progress_browsecomp_zh.py /path/to/evaluation/logs

# GAIA-Validation
python benchmarks/check_progress/check_progress_gaia-validation.py /path/to/evaluation/logs

# GAIA-Text-103
python benchmarks/check_progress/check_progress_gaia-validation-text-103.py /path/to/evaluation/logs

# WebWalkerQA
python benchmarks/check_progress/check_progress_webwalkerqa.py /path/to/evaluation/logs

# Frames
python benchmarks/check_progress/check_progress_frames.py /path/to/evaluation/logs

# XBench-DeepSearch
python benchmarks/check_progress/check_progress_xbench_deepsearch.py /path/to/evaluation/logs

# SEAL-0
python benchmarks/check_progress/check_progress_seal-0.py /path/to/evaluation/logs

# AIME2025
python benchmarks/check_progress/check_progress_aime2025.py /path/to/evaluation/logs

# DeepSearchQA
python benchmarks/check_progress/check_progress_deepsearchqa.py /path/to/evaluation/logs
```

</details>

## 🔬 轨迹收集（Trace Collection）

<details>
<summary>📋 点击展开轨迹收集命令</summary>

```bash
cd apps/collect-trace

# 收集 SFT 轨迹
bash scripts/collect_trace_claude37.sh
bash scripts/collect_trace_gpt5.sh

# 收集 DPO 轨迹
bash scripts/collect_trace_qwen3.sh
```

</details>

## ❓ 常见问题与故障排除

### 常见问题

<details>
  <summary>🔧 点击展开故障排除指南</summary>

#### **Q：我应该使用哪个版本？**

**A：** 我们推荐使用 **MiroThinker-1.7** ⭐ 搭配最小化配置：

- **v1.7** ⭐：最新版本，支持 256K 上下文，性能全球领先。请使用以下带上下文管理的配置：
  - `mirothinker_1.7_keep5_max200`（最多 200 轮回合，推荐用于大多数任务）
  - `mirothinker_1.7_keep5_max300`（最多 300 轮回合，仅用于 BrowseComp 和 BrowseComp-ZH）

#### **Q：如何获取 API Keys？**

**A：** 最小化设置你需要以下 Key：

- **SERPER_API_KEY**：从 [Serper.dev](https://serper.dev/) 获取（Google 搜索 API）
- **JINA_API_KEY**：从 [Jina.ai](https://jina.ai/) 获取（网页抓取）
- **E2B_API_KEY**：从 [E2B.dev](https://e2b.dev/) 获取（代码执行沙箱）
- **SUMMARY_LLM_API_KEY**：你的 LLM API 凭证（用于内容摘要）。可使用 Qwen3-14B 或 GPT-5-Nano 等小模型，选择对性能影响极小。
- **OPENAI_API_KEY**：从 [OpenAI](https://platform.openai.com/) 获取（基准评估必需，用于 LLM-as-a-Judge）
- **OPENAI_BASE_URL**：可选，默认为 `https://api.openai.com/v1`。可更改为使用 OpenAI 兼容 API。

#### **Q：智能体服务端连接错误**

**A：** 常见问题排查：

- **检查基础 URL 格式**：应以 `/v1` 结尾（例如 `https://your-api.com/v1`）
- **验证 API Key**：确保环境变量或脚本中正确设置了 `API_KEY`
- **检查服务状态**：确认你的服务端正在运行且可访问
- **网络问题**：验证防火墙/网络设置是否允许连接

#### **Q：评估脚本无法运行**

**A：** 排查步骤：

1. **检查工作目录**：确保你位于 `apps/miroflow-agent` 目录下
2. **验证环境**：运行 `uv sync` 确保依赖已安装
3. **检查 .env 文件**：确保所有必需的环境变量均已设置
4. **查看日志**：检查 `logs/` 目录以获取详细错误信息
5. **验证数据路径**：确保基准数据已下载且位于正确位置

#### **Q：WSL 上 `uv sync` 报内存分配错误**

**A：** WSL2 存在内存上限，在构建重型包（如 `transformers`, `pillow`）时可能导致 `uv sync` 失败。提供两种解决方案：

1. **增加 WSL2 内存限制**（推荐）：在你的 Windows 主机上创建或编辑 `%UserProfile%\.wslconfig`，然后重启 WSL（执行 `wsl --shutdown`）：
   ```ini
   [wsl2]
   memory=8GB
   ```

2. **限制并行包构建数**（无需重启）：在运行 `uv sync` 前设置 `UV_CONCURRENT_BUILDS` 环境变量：
   ```bash
   UV_CONCURRENT_BUILDS=1 uv sync
   ```

#### **Q：内存溢出错误（Out of memory）**

**A：** 解决方案：

- **减少上下文长度**：将 `MAX_CONTEXT_LENGTH` 设置为更小的值（例如 131072 表示 128K）
- **使用带较少回合的上下文管理配置**：
  - 对于 v1.5：使用 `mirothinker_1.7_keep5_max200` 或 `mirothinker_1.7_keep5_max300`（带上下文管理）
- **减少并发任务数**：将 `MAX_CONCURRENT` 设置为更小的数字（例如 5）
- **使用较小规模的智能体**：
  - 对于 v1.5：尝试 30B 而非 235B
  - 对于 v1.0：尝试 8B 或 30B 而非 72B

#### **Q：工具执行错误**

**A：** 常见修复方法：

- **E2B 报错**：验证 `E2B_API_KEY` 是否有效且账户有余额
- **Serper 报错**：检查 `SERPER_API_KEY` 和速率限制
- **Jina 报错**：验证 `JINA_API_KEY` 和 `JINA_BASE_URL` 是否正确
- **LLM 摘要报错**：检查 `SUMMARY_LLM_*` 变量及智能体可用性

#### **Q：如何监控长时间运行的评估任务？**

**A：** 使用进度监控脚本：

```bash
cd apps/miroflow-agent
python benchmarks/check_progress/check_progress_<benchmark_name>.py /path/to/logs
```

该脚本会显示完成状态、已用时间及预估剩余时间。

</details>

### 获取帮助

- 📖 **文档**：查看 [MiroFlow Tools README](libs/miroflow-tools/README.md) 了解工具详情
- 💬 **Discord**：加入我们的 [Discord 社区](https://discord.com/invite/GPqEnkzQZd)
- 🐛 **Issues**：在 [GitHub Issues](https://github.com/MiroMindAI/MiroThinker/issues) 报告 Bug
- 📧 **联系**：访问 [我们的官网](https://miromind.ai/) 获取更多信息

## 📄 许可证

本项目采用 Apache 2.0 License 开源——详见 [LICENSE](LICENSE) 文件。

## 🙏 致谢

我们向以下各方致以诚挚的感谢：

- 🏆 **基准测试贡献者** 提供了全面的评估数据集
- 🌍 **开源社区** 提供了使本项目成为可能的工具与库
- 👥 **所有贡献者** 帮助 MiroThinker 变得更好

<div align="center">
  <a href="https://github.com/MiroMindAI/MiroThinker/graphs/contributors">
    <img src="https://contrib.rocks/image?repo=MiroMindAI/MiroThinker" />
  </a>
</div>

加入我们的社区，共同构建 AI 智能体的未来！

### 参考文献

如果你在研究中使用了本项目，请考虑引用：

**MiroThinker** (模型与方法)
```
@article{miromind2026mirothinker,
  title={MiroThinker-1.7 & H1: Towards Heavy-Duty Research Agents via Verification},
  author={MiroMind Team and Bai, S. and Bing, L. and Lei, L. and Li, R. and Li, X. and Lin, X. and Min, E. and Su, L. and Wang, B. and Wang, L. and Wang, L. and Wang, S. and Wang, X. and Zhang, Y. and Zhang, Z. and others},
  journal={arXiv preprint arXiv:2603.15726},
  year={2026}
}

@article{miromind2025mirothinker,
  title={MiroThinker: Pushing the Performance Boundaries of Open-Source Research Agents via Model, Context, and Interactive Scaling},
  author={MiroMind Team and Bai, Song and Bing, Lidong and Chen, Carson and Chen, Guanzheng and Chen, Yuntao and Chen, Zhe and Chen, Ziyi and Dong, Xuan and others},
  journal={arXiv preprint arXiv:2511.11793},
  year={2025}
}
```

**MiroFlow** (框架)
```bibtex
@article{miromind2026miroflow,
  title={MiroFlow: Towards High-Performance and Robust Open-Source Agent Framework for General Deep Research Tasks},
  author={Su, Shiqian and Xing, Sen and Dong, Xuan and Zhong, Muyan and Wang, Bin and Zhu, Xizhou and Chen, Yuntao and Wang, Wenhai and Deng, Yue and Zhu, Pengxiang and others},
  journal={arXiv preprint arXiv:2602.22808},
  year={2026}
}
```

[![Star History Chart](https://api.star-history.com/svg?repos=MiroMindAI/MiroThinker&type=Date)](https://star-history.com/#MiroMindAI/MiroThinker&Date)
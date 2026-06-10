<div align="center">

<a href="https://art.openpipe.ai"><picture>
<img alt="ART logo" src="https://github.com/openpipe/art/raw/main/assets/ART_logo.png" width="160px">
</picture></a>

<p align="center">
  <h1>Agent Reinforcement Trainer</h1>
</p>

<p>
使用 GRPO 为现实任务训练多步智能体。
</p>

[![PRs-Welcome][contribute-image]][contribute-url]
[![PyPI version](https://img.shields.io/pypi/v/openpipe-art?color=364fc7)][pypi-url]
[![Train Agent](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/openpipe/art-notebooks/blob/main/examples/2048/2048.ipynb)

[![Join Discord](https://img.shields.io/badge/Join%20Discord-5865F2?style=plastic&logo=discord&logoColor=white)](https://discord.gg/EceeVdhpxD)
[![Documentation](https://img.shields.io/badge/Documentation-orange?style=plastic&logo=gitbook&logoColor=white)](https://art.openpipe.ai)

</div>

## 🚀 W&B Training：无服务器强化学习（Serverless RL）

**W&B Training（无服务器强化学习）**是首个公开发布的灵活进行强化学习模型训练的服务。它自动管理你的训练和推理基础设施，让你专注于定义数据、环境和奖励函数——从而加快反馈周期、降低成本并大幅减少运维工作。

✨ **核心优势：**

- **成本降低 40%** - 在共享的生产级推理集群上进行资源复用
- **训练速度提升 28%** - 支持跨多 GPU 扩展至 2000+ 并发请求
- **零基础设施烦恼** - 完全托管且保持健康的基础设施
- **即时部署** - 每个检查点（checkpoint）均可通过 W&B Inference 立即访问

```python
# Before: Hours of GPU setup and infra management
# RuntimeError: CUDA error: out of memory 😢

# After: Serverless RL with instant feedback
from art.serverless.backend import ServerlessBackend

model = art.TrainableModel(
  project="voice-agent",
  name="agent-001",
  base_model="Qwen/Qwen3.6-27B"
)

backend = ServerlessBackend(
    api_key="your_wandb_api_key"
)
model.register(backend)
# Edit and iterate in minutes, not hours!
```

[📖 了解 W&B Training 详情 →](https://docs.wandb.ai/guides/training)

## ART 概述

ART 是一个开源的强化学习（RL）框架，通过让大语言模型（LLM）**从经验中学习**来提升智能体的可靠性。ART 提供了一个易于使用的工具包，用于将 GRPO 集成到任何 Python 应用中。如需快速上手体验，请运行下方的任意一个 Notebook。当你准备好深入了解时，请参阅[文档](https://art.openpipe.ai)。

## 📒 Notebooks（示例笔记本）

| Agent Task          | Example Notebook                                                                                                                       | Description                                         | Comparative Performance                                                                                                                                                                                                     |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **ART•E [Serverless]**   | [🏋️ Train agent](https://colab.research.google.com/github/openpipe/art-notebooks/blob/main/examples/art-e.ipynb)                       | Qwen 3.6 27B 学习使用 RULER 搜索邮件                | <img src="https://github.com/openpipe/art/raw/main/assets/benchmarks/email_agent/accuracy-training-progress.svg" height="72"> [benchmarks](/dev/art-e/art_e/evaluate/display_benchmarks.ipynb)                              |
| **2048 [Serverless]** | [🏋️ Train agent](https://colab.research.google.com/github/openpipe/art-notebooks/blob/main/examples/2048/2048.ipynb)                   | Qwen 3.6 27B 学习玩 2048 游戏                       | <img src="https://github.com/openpipe/art/raw/main/assets/benchmarks/2048/accuracy-training-progress.svg" height="72"> [benchmarks](/examples/2048/display_benchmarks.ipynb)                                                |
| **ART•E LangGraph** | [🏋️ Train agent](https://colab.research.google.com/github/openpipe/art-notebooks/blob/main/examples/langgraph/art-e-langgraph.ipynb)   | Qwen 2.5 7B 学习使用 LangGraph 搜索邮件             | [Link coming soon]                                                                                                                                                                                                          |
| **MCP•RL**          | [🏋️ Train agent](https://colab.research.google.com/github/openpipe/art-notebooks/blob/main/examples/mcp-rl/mcp-rl.ipynb)               | Qwen 2.5 3B 掌握 NWS MCP 服务器操作                 | [Link coming soon]                                                                                                                                                                                                          |
| **Temporal Clue**   | [🏋️ Train agent](https://colab.research.google.com/github/openpipe/art-notebooks/blob/main/examples/temporal_clue/temporal-clue.ipynb) | Qwen 2.5 7B 学习解决 Temporal Clue（时间线索）谜题  | [Link coming soon]                                                                                                                                                                                                          |
| **Tic Tac Toe**     | [🏋️ Train agent](https://colab.research.google.com/github/openpipe/art-notebooks/blob/main/examples/tic_tac_toe/tic-tac-toe.ipynb)     | Qwen 2.5 3B 学习玩井字棋游戏                        | <img src="https://github.com/openpipe/art/raw/main/assets/benchmarks/tic-tac-toe-local/accuracy-training-progress.svg" height="72"> [benchmarks](/examples/tic_tac_toe/display-benchmarks.ipynb)                            |
| **Codenames**       | [🏋️ Train agent](https://colab.research.google.com/github/openpipe/art-notebooks/blob/main/examples/codenames/Codenames_RL.ipynb)      | Qwen 2.5 3B 学习玩密码游戏（Codenames）              | <img src="https://github.com/openpipe/art/raw/main/assets/benchmarks/codenames/win_rate_over_time.png" height="72"> [benchmarks](https://github.com/OpenPipe/art-notebooks/blob/main/examples/codenames/Codenames_RL.ipynb) |
| **AutoRL [RULER]**  | [🏋️ Train agent](https://colab.research.google.com/github/openpipe/art-notebooks/blob/main/examples/auto_rl.ipynb)                     | 训练 Qwen 2.5 7B 掌握任意任务                       | [Link coming soon]                                                                                                                                                                                                          |
| **Distillation (SFT)** | [🏋️ Train model](https://colab.research.google.com/github/openpipe/art-notebooks/blob/main/examples/sft/distillation.ipynb)         | 将文本转 SQL（text-to-SQL）能力从 Qwen 3 235B 蒸馏至 Qwen 3.6 27B | [Link coming soon]                                                                                                                                                                                                          |
| **Summarizer (SFT + RL)** | [🏋️ Train model](https://colab.research.google.com/github/openpipe/art-notebooks/blob/main/examples/sft/sft-rl.ipynb)            | 结合 SFT 预热与强化学习训练文档摘要模型             | [Link coming soon]                                                                                                                                                                                                          |
| **SFT from a dataset** | [🏋️ Train model](https://colab.research.google.com/github/openpipe/art-notebooks/blob/main/examples/sft/train_from_file.ipynb)      | 基于数据集对 Qwen 3.6 27B 进行文本转 SQL（text-to-SQL）微调 | [Link coming soon]                                                                                                                                                                                                          |

## 📰 ART 动态

探索我们在构建顶尖智能体方面的最新研究与更新。

- 🗞️ **[ART 现已无缝集成 LangGraph](https://art.openpipe.ai/integrations/langgraph-integration)** - 使用强化学习训练你的 LangGraph 智能体，实现更智能的多步推理和更好的工具调用。
- 🗞️ **[MCP•RL：让你的模型掌握任意 MCP 服务器](https://x.com/corbtt/status/1953171838382817625)** - 通过强化学习自动训练模型以有效使用 MCP 服务器工具。
- 🗞️ **[AutoRL：零数据任务训练](https://x.com/mattshumer_/status/1950572449025650733)** - 利用自动输入生成和 RULER 评估，无需标注数据即可训练自定义 AI 模型。
- 🗞️ **[RULER：强化学习奖励的轻松模式](https://openpipe.ai/blog/ruler-easy-mode-for-rl-rewards)**现已上线，支持自动化奖励生成。
- 🗞️ **[ART·E：我们如何打造击败 o3 的邮件研究智能体](https://openpipe.ai/blog/art-e-mail-agent)**展示了 Qwen 2.5 14B 邮件智能体在性能上超越 OpenAI o3 的案例。
- 🗞️ **[ART Trainer：专为智能体设计的全新强化学习训练器](https://openpipe.ai/blog/art-trainer)**，支持使用 GRPO 轻松训练基于大语言模型的智能体。

[📖 查看所有博客文章 →](https://openpipe.ai/blog)

## 为什么选择 ART？

- ART 为在现有应用中引入强化学习（RL）训练提供了便捷的封装接口。我们将训练服务器抽象为一个模块化服务，你的代码无需直接与其交互。
- **随处可训**。在笔记本上运行 ART 客户端，由 ART 服务器启动按需分配的 GPU 环境，或直接在本地 GPU 上运行。
- 与 W&B、Langfuse 和 OpenPipe 等托管平台的集成提供了灵活的监控能力，并**简化了调试流程**。
- ART 具备智能默认配置且高度可定制。你可以根据特定需求配置训练参数和推理引擎设置，或直接使用已针对训练效率和稳定性进行优化的默认配置。

## 安装

任何运行 Python 的客户端机器均可用于训练 ART 智能体。若要将其添加到现有项目中，请运行以下命令：

```
pip install openpipe-art
```

## 🤖 ART•E 智能体

想了解如何将 ART 应用于现实任务？请阅读[ART•E 智能体](https://openpipe.ai/blog/art-e-mail-agent)博客文章，其中详细说明了我们是怎样训练 Qwen 2.5 14B 在邮件检索任务中击败 o3 的！

<img src="https://github.com/openpipe/art/raw/main/assets/ART_E_graphs.png" width="700">

## 🔁 训练循环概述

ART 的功能划分为**客户端**和**服务器**。兼容 OpenAI 协议的客户端负责在 ART 和你的代码库之间进行交互。使用客户端，你可以在大语言模型（LLM）不断优化的过程中传递消息并获取补全结果。服务器可在任何配备 GPU 的机器上独立运行。它抽象化了强化学习循环中推理和训练部分的复杂性，同时允许进行一定的自定义配置。训练循环概述如下：

1. **推理阶段**
   1. 你的代码使用 ART 客户端执行智能体工作流（通常并行执行多次 rollout 以更快收集数据）。
   2. 补全请求被路由至 ART 服务器，后者在 vLLM 中运行模型最新的 LoRA。
   3. 随着智能体执行，每条 `system`、`user` 和 `assistant` 消息都会被存入轨迹（Trajectory）中。
   4. 当一次 rollout 结束时，你的代码会为其轨迹分配一个奖励值（reward），以反映大语言模型的性能表现。

2. **训练阶段**
   1. 每次 rollout 完成后，轨迹会被分组并发送至服务器。在训练执行期间，推理过程将被阻塞。
   2. 服务器使用 GRPO 算法训练你的模型，从最新的检查点（或首次迭代时的空 LoRA）开始初始化。
   3. 服务器将新训练的 LoRA 保存至本地目录并加载到 vLLM 中。
   4. 推理过程解除阻塞，循环从第 1 步重新开始。

该训练循环将持续运行，直到完成指定数量的推理和训练迭代次数。

## 🧩 支持的模型

ART 应能兼容大多数支持 vLLM / Hugging Face transformers 的因果语言模型，或至少包含 [Unsloth](https://docs.unsloth.ai/get-started/all-our-models) 支持的模型。目前暂不支持 Gemma 3。如果你尝试使用其他模型遇到问题，欢迎在 [Discord](https://discord.gg/zbBHRUpwf4) 上告知我们或在 [GitHub](https://github.com/openpipe/art/issues) 提交 Issue！

## 🤝 贡献指南

ART 正处于积极开发阶段，非常欢迎贡献代码！更多信息请参阅 [CONTRIBUTING.md](CONTRIBUTING.md)。

## 📖 引用格式

```bibtex
@misc{hilton2025art,
  author = {Brad Hilton and Kyle Corbitt and David Corbitt and Saumya Gandhi and Angky William and Bohdan Kovalevskyi and Andie Jones},
  title = {ART: Agent Reinforcement Trainer},
  year = {2025},
  publisher = {GitHub},
  journal = {GitHub repository},
  howpublished = {\url{https://github.com/openpipe/art}}
}
```

## ⚖️ 许可证

本仓库的源代码遵循 [Apache-2.0 License](LICENSE) 开源协议。

## 🙏 鸣谢

ART 的成功得益于站在巨人的肩膀上。虽然 ART 开发的许多理念和早期实验归功于广泛的开源强化学习社区，但我们特别感谢以下项目的作者：

- [Unsloth](https://github.com/unslothai/unsloth)
- [vLLM](https://github.com/vllm-project/vllm)
- [trl](https://github.com/huggingface/trl)
- [torchtune](https://github.com/pytorch/torchtune)

最后，感谢协助我们在真实环境中测试 ART 的合作伙伴！我们非常期待看到大家利用它构建出的精彩项目。

[pypi-url]: https://pypi.org/project/openpipe-art/
[contribute-url]: https://github.com/openpipe/art/blob/main/CONTRIBUTING.md
[contribute-image]: https://img.shields.io/badge/PRs-welcome-blue.svg
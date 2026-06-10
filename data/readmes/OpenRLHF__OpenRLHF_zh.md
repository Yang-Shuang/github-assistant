<div align="center">
    <img alt="OpenRLHF logo" src="./docs/logo.png" style="height: 140px;" />
</div>
<div align="center">
<p align="center">
      <a href="https://github.com/OpenRLHF/OpenRLHF/graphs/contributors">
        <img alt="GitHub Contributors" src="https://img.shields.io/github/contributors/OpenRLHF/OpenRLHF" />
      </a>
      <a href="https://github.com/OpenRLHF/OpenRLHF/issues">
        <img alt="Issues" src="https://img.shields.io/github/issues/OpenRLHF/OpenRLHF?color=0088ff" />
      </a>
      <a href="https://github.com/OpenRLHF/OpenRLHF/discussions">
        <img alt="Discussions" src="https://img.shields.io/github/discussions/OpenRLHF/OpenRLHF?color=0088ff" />
      </a>
      <a href="https://github.com/OpenRLHF/OpenRLHF/pulls">
        <img alt="GitHub pull requests" src="https://img.shields.io/github/issues-pr/OpenRLHF/OpenRLHF?color=0088ff" />
      </a>
      <a href="https://github.com/OpenRLHF/OpenRLHF/stargazers">
        <img alt="GitHub stars" src="https://img.shields.io/github/stars/OpenRLHF/OpenRLHF?color=ccf" />
      </a>
      <a href="https://deepwiki.com/OpenRLHF/OpenRLHF"><img src="https://deepwiki.com/badge.svg" alt="Ask DeepWiki"></a>
      <br>
      <em>开源 / 全面 / 轻量级 / 易用</em>
    </p>
</div>

<hr>

<span>[ English | <a href="README_zh.md">中文</a> | <a href="README_ja.md">日本語</a> ]</span>

OpenRLHF 是**首个**高性能、面向生产环境的开源 RLHF（基于人类反馈的强化学习）框架，结合了 **Ray + vLLM 分布式架构**与**统一的基于智能体（Agent）的设计范式**，旨在实现可扩展且易扩展的人类反馈强化学习。

📚 **了解更多**: [文档](https://openrlhf.readthedocs.io/) | [幻灯片](https://docs.google.com/presentation/d/1JRhB1d7csofx0PIZBmfyBdMluxNd5JLPpUHrrvVhGnk/edit?usp=sharing) | [技术报告](https://www.researchgate.net/publication/393414548_OpenRLHF_An_Easy-to-use_Scalable_and_High-performance_RLHF_Framework) | [视频](https://www.bilibili.com/video/BV1dv2jBxEQG/)

## 📖 目录

- [🗞️ 新闻](#news)
- [🏗️ 架构基础：Ray + vLLM 分布式](#architecture-foundation-ray--vllm-distribution) - Ray + vLLM + DeepSpeed 分布式基础设施
- [🎯 设计范式](#design-paradigm-agent-based-execution) - 统一的基于智能体的执行流程
- [🚀 RL 算法](#state-of-the-art-rl-algorithms) - PPO、REINFORCE++、GRPO、RLOO
- [📋 功能概览](#comprehensive-features) - 完整的 RLHF 流水线能力
- [🎬 快速开始](#quick-start) - 安装与典型工作流
- [🎓 训练指南](#supervised-fine-tuning) - SFT、奖励模型、RL 训练
- [🎯 单轮智能体](#single-turn-agent-reinforced-fine-tuning-with-custom-rewards) - 自定义奖励函数
- [🤖 多轮智能体](#multi-turn-agent-complex-environment-interactions) - 复杂环境交互
- [🔧 高级主题](#advanced-topics) - LoRA、性能调优

---

<a id="news"></a>
## 🗞️ 新闻

<details>
<summary>Show News</summary>

- [2026/4] OpenRLHF 0.10 新增 **多轮视觉语言模型（VLM）强化学习** —— 支持在提示词和环境反馈（如截图）中进行带图像的多步交互。示例：[vlm_multiturn_agent.py](./examples/python/vlm_multiturn_agent.py)
- [2026/4] OpenRLHF 0.10 新增 **VLM（视觉语言模型）RLHF 支持** —— 端到端训练带有图像输入的 VLM（如 Qwen3.5）。训练脚本：[train_vlm_math_hybrid_engine.sh](./examples/scripts/train_vlm_math_hybrid_engine.sh)
- [2026/2] [ProRL V2](https://developer.nvidia.com/blog/scaling-llm-reinforcement-learning-with-prolonged-training-using-prorl-v2/) 使用 REINFORCE++-baseline 结合长时间强化学习训练出当前最优的 1.5B 推理模型。训练脚本：[train_prorlv2_math_hybrid_engine.sh](./examples/scripts/train_prorlv2_math_hybrid_engine.sh)
- [2025/10] [ScaleRL](https://arxiv.org/abs/2510.13786) 验证了 REINFORCE++-baseline 在大规模训练场景下的有效性。发布了 [REINFORCE++ 幻灯片](https://docs.google.com/presentation/d/1stieP_3PM1z4Hq1YWR3GywFkxcHEAlstXMaS23KlGN4)
- [2025/6] [Magistral](https://mistral.ai/static/research/magistral.pdf) 使用了与 REINFORCE++-baseline 非常相似的方法训练推理模型。
- [2025/5] [MARTI](https://github.com/TsinghuaC3I/MARTI) 作为 OpenRLHF 的分支版本发布。它旨在通过将集中式多智能体交互与分布式策略训练相结合，使用 RL 训练基于 LLM 的多智能体系统。
- [2025/5] OpenRLHF 0.8.0 支持通过 `--train.async_enable` 进行异步 RLHF 训练，以及通过 `--train.agent_func_path` 进行异步智能体 RLHF 训练。可运行示例见 [train_reinforce_baseline_ray_agent_async.sh](./examples/scripts/train_reinforce_baseline_ray_agent_async.sh)。
- [2025/4] 发布博客 [Accelerating RLHF with vLLM, Best Practice from OpenRLHF](https://blog.vllm.ai/2025/04/23/openrlhf-vllm.html)
- [2025/4] Clean OpenRLHF：基于单控制器（Single Controller）和统一样本打包（Unified Packing Samples）重构了源代码
- [2025/3] 卡内基梅隆大学 [Advanced Natural Language Processing Spring 2025](https://cmu-l3.github.io/anlp-spring2025/) 课程使用 OpenRLHF 作为 RLHF 框架的教学案例。
- [2025/2] [Logic-RL](https://arxiv.org/abs/2502.14768) 和 [PRIME](https://arxiv.org/abs/2502.01456) 证明 REINFORCE++ 相比 GRPO 训练更稳定，且比 PPO 更快。
- [2025/2] [LMM-R1](https://github.com/TideDra/lmm-r1) 是 OpenRLHF 的分支版本，旨在为多模态任务上的 DeepSeek-R1 复现提供高性能 RL 基础设施。
- [2025/2] MIT & Microsoft 使用 OpenRLHF 提出了论文 [On the Emergence of Thinking in LLMs I: Searching for the Right Intuition](https://arxiv.org/pdf/2502.06773)
- [2025/1] HKUST 使用 OpenRLHF 复现了 [DeepSeek-R1-Zero and DeepSeek-R1 training on small models using OpenRLHF](https://github.com/hkust-nlp/simpleRL-reason)
- [2024/12] 我们“提出”😊了 [REINFORCE++: A Simple and Efficient Approach for Aligning Large Language Models](https://www.researchgate.net/publication/387487679_REINFORCE_An_Efficient_RLHF_Algorithm_with_Robustnessto_Both_Prompt_and_Reward_Models)。
- [2024/12] 我们在 [Notion 博客](https://hijkzzz.notion.site/unraveling-rlhf-and-its-variants-engineering-insights#147d9a33ecc9806090f3d5c749d31f05) 中分析了 PPO、REINFORCE++、GRPO 和 RLOO。
- [2023/8] OpenRLHF 开源发布。

</details>

---

<a id="architecture-foundation-ray--vllm-distribution"></a>
## 🏗️ 架构基础：Ray + vLLM 分布式

OpenRLHF 是首个基于 Ray + vLLM 分布式架构构建的 RLHF 框架，高效编排跨 GPU 的多个组件：

<div align="center">
  <img alt="OpenRLHF Architecture (Ray + vLLM)" src="./docs/openrlhf_architecture.svg" style="max-width: 100%; height: auto;" />
</div>

### 核心基础设施组件

**Ray - 分布式调度器与控制器**  
OpenRLHF 利用 [Ray](https://github.com/ray-project/ray) 实现高效的分布式调度。它将 Actor、Reward、Reference 和 Critic 模型分离到不同的 GPU 上，支持最高 **70B+ 参数**模型的扩展训练。

**混合引擎调度（Hybrid Engine Scheduling）**：所有模型和 vLLM 引擎均可共享 GPU 资源——最小化空闲时间并最大化 GPU 利用率。这使得在有限硬件上运行完整的 RLHF 流水线成为可能。

**vLLM - 高性能推理引擎**  
RLHF 训练中 **80% 的时间消耗在样本生成上**。依托 [vLLM](https://github.com/vllm-project/vllm) 的自动张量并行（AutoTP）和流水线并行（PP），OpenRLHF 提供高吞吐量、内存高效的生成功能。

**DeepSpeed - 内存高效训练**  
基于 [DeepSpeed](https://github.com/deepspeedai/DeepSpeed) ZeRO-3、[deepcompile](https://github.com/deepspeedai/DeepSpeed/blob/master/blogs/deepcompile/README.md)、[AutoTP](https://github.com/deepspeedai/DeepSpeed/blob/master/blogs/huggingface-tp/README.md) 和 RingAttention。在不依赖重型框架的情况下实现大模型训练，并可直接与 HuggingFace 模型配合使用。

**Transformers - 模型接口**  
原生集成 HuggingFace Transformers，支持无缝加载预训练模型、状态管理及微调。

**NCCL / CUDA IPC - 高速通信**  
用于分布式训练和推理的高效 GPU 间通信。

---

<a id="design-paradigm-agent-based-execution"></a>
## 🎯 设计范式：基于智能体的执行流程

**在 Ray 分布式架构之上**，OpenRLHF 是首个实现**统一智能体（Agent）范式**的 RLHF 框架。无论标准 PPO 还是复杂的多轮推理训练，均遵循一致的 Agent 执行流水线。

### 为什么采用基于智能体的设计？

OpenRLHF **通过词元输入-输出（Token-in-Token-out）的智能体执行流程统一了生成与训练**，确保完美的一致性、易于单/多轮扩展，并彻底消除文本层面的不匹配问题。

### 智能体架构

```
                 ┌─────────────────────────────┐
                 │    AgentExecutorBase        │
                 │  (Token-in-Token-out Core)  │
                 └─────────────────────────────┘
                              │
                 ┌────────────┴────────────┐
                 ↓                         ↓
         SingleTurnExecutor        MultiTurnExecutor
                 │                         │
      ┌──────────┴──────────┐   ┌─────────┴──────────┐
      ↓                     ↓   ↓                    ↓
  Standard RLHF      Custom Reward   Multi-Step    External Env
  (One-shot gen)     Function      Reasoning     (OpenAI Agent Server)
      ↓                     ↓           ↓                ↓
      └─────────────────────┴───────────┴────────────────┘
                              │
                    Consistent Token Trajectories
                              │
                    ┌─────────┴─────────┐
                    │  RL Algorithms    │
                    │  (Decoupled)      │
                    │                   │
                    │  PPO, REINFORCE++ │
                    │  GRPO, RLOO, etc. │
                    └───────────────────┘
```

### 核心设计原则

<details>
<summary>Show core design principles</summary>

| 原则 | 描述 | 优势 |
|-----------|-------------|---------|
| **词元输入-输出（Token-in-Token-out）** | 所有采样均生成词元级轨迹 | 零文本层面不匹配 |
| **统一接口** | 所有模式共享相同的 `AgentExecutorBase` API | 一键切换模式 |
| **算法无关性** | RL 算法（PPO、REINFORCE++ 等）与智能体执行器解耦 | 任意算法可适配任意模式 |
| **可扩展性** | 轻松插入自定义奖励/环境 | 快速实验验证 |
| **生产就绪** | 支持同步/异步/混合引擎 | 从研究到部署无缝衔接 |

</details>

### 两种执行模式（与 RL 算法正交）

智能体执行模式与你选择的 RL 算法**相互独立**。你可以将**任意算法**（PPO、REINFORCE++、GRPO 等）与**任意执行模式**结合使用：

| 模式 | 适用场景 | 接口 | 复杂度 |
|------|-----------|-----------|------------|
| **单轮（Single-Turn）** | 标准 RLHF、自定义奖励函数 | 可选 `reward_func()` | ⭐ 默认（99% 用例） |
| **多轮（Multi-Turn）** | 多步推理、交互式环境 | `reset()` + `step()` | ⭐⭐ 进阶 |

---

<a id="state-of-the-art-rl-algorithms"></a>
## 🚀 前沿 RL 算法

OpenRLHF 实现了 **PPO、REINFORCE++、REINFORCE++-baseline、GRPO、RLOO**，并融合了实践指南与社区最佳实践的先进优化技巧。 

**核心设计**：RL 算法**与智能体执行模式解耦**。所有算法均可无缝配合单轮和多轮智能体执行器运行，通过统一的词元输入-输出流水线确保行为一致性。

<details>
<summary>Show algorithm comparison table</summary>

| 算法 | `--algo.advantage.estimator` | 核心特性 | 最佳适用场景 |
|-----------|------------------------|-------------|---------------|
| **PPO** | (默认) | 完整 Critic 网络 | 稳定训练、经过验证的效果 |
| **REINFORCE++** | `reinforce` | 借鉴 PPO 技巧但无需 Critic | 高效训练、内存占用更低 |
| **REINFORCE++-baseline** | `reinforce_baseline` | 均值奖励基线 | 推理任务（RLVR）、对奖励尺度鲁棒 |
| **RLOO** | `rloo` | 词元级 KL + PPO-clip | 多样本训练 |
| **GRPO** | `group_norm` | 分组归一化 | 基于批次的训练 |
| **Dr. GRPO** | `dr_grpo` | 简化版 GRPO | 移除局部 `/std` 归一化 |

</details>

参考：[知乎文章](https://zhuanlan.zhihu.com/p/622134699) | [Notion 最佳实践](https://hijkzzz.notion.site/rlhf-implementation-tricks?v=158d9a33ecc98132bf9e000c39227361)

---

<a id="comprehensive-features"></a>
## 📋 功能概览

OpenRLHF 提供完整的 RLHF 流水线，并具备基于智能体的灵活性：

### 🎯 基于智能体的 RL 训练（核心创新）

<details>
<summary>Show agent-based RL training details</summary>

**单轮模式（默认 - 99% 的用例）**
- 每个提示词仅生成一次
- 支持所有 RL 算法：[PPO](./examples/scripts/train_ppo_ray_hybrid_engine.sh)、[REINFORCE++/baseline/GRPO/RLOO](./examples/scripts/train_reinforce_baseline_hybrid_engine.sh)
- [自定义奖励函数](./examples/scripts/train_ppo_with_reward_fn.sh) (`--reward.remote_url`)
- [混合引擎（Hybrid Engine）](./examples/scripts/train_ppo_ray_hybrid_engine.sh) 实现 GPU 利用率最大化

**多轮模式（进阶 - 交互式任务）**
- 与环境反馈进行多步交互
- 支持所有 RL 算法
- [自定义智能体函数](./examples/scripts/train_reinforce_baseline_ray_agent_async.sh) (`--train.agent_func_path`)
- OpenAI 兼容服务器：见 `examples/python/agent_func_openai_server_executor.py`，将 vLLM 封装为本地 OpenAI Agent Server 的智能体执行器
- 异步流水线（`--train.async_enable`）提升吞吐量：[train_reinforce_baseline_ray_agent_async.sh](./examples/scripts/train_reinforce_baseline_ray_agent_async.sh)

</details>

### 🎓 监督训练与偏好学习

<details>
<summary>Show supervised training & preference learning table</summary>

| 方法 | 脚本 | 描述 |
|--------|--------|-------------|
| **SFT** | [train_sft.sh](./examples/scripts/train_sft.sh) | 带样本打包的监督微调 |
| **DPO/IPO/cDPO** | [train_dpo_llama.sh](./examples/scripts/train_dpo_llama.sh) | 直接偏好优化 |
| **Reward Model** | [train_rm.sh](./examples/scripts/train_rm.sh) | 训练奖励模型 |

</details>

### ⚡ 高级能力

<details>
<summary>Show advanced capabilities</summary>

**效率优化**
- 样本打包（`--ds.packing_samples`）适用于所有训练模式
- vLLM 加速（`--vllm.num_engines`）实现快速生成
- DAPO [动态过滤](./examples/scripts/train_dapo_ray_hybrid_engine.sh) (`--algo.dynamic_filtering_enable`)
  - 🎲 动态采样：针对每个提示词，生成多个响应并通过你的奖励/智能体 **0–1 `scores`** 信号进行**过滤**
    - 启用：`--algo.dynamic_filtering_enable`
    - 分数范围：`--algo.dynamic_filtering_range 0.0 1.0`
    - 依赖：`--rollout.n_samples_per_prompt > 1` 且需配置 `--reward.remote_url` 或 `--train.agent_func_path`
    - 示例：`./examples/scripts/train_dapo_ray_hybrid_engine.sh`

**扩展性**
- DeepSpeed AutoTP 用于张量并行（见训练脚本中的 `--ds.tensor_parallel_size`）
- [RingAttention](./examples/test_scripts/train_dpo_ring_llama.sh) 支持长上下文（`--ds.ring_attn_size`）
- 通过 [SLURM](./examples/scripts/train_ppo_ray_slurm.sh) 进行多节点训练

**模型支持**
- [VLM（视觉语言模型）](./examples/scripts/train_vlm_math_hybrid_engine.sh) —— 单轮及[带图像反馈的多轮](./examples/python/vlm_multiturn_agent.py) (`--data.image_key`, `--data.max_images_per_prompt`)
- [LoRA/QLoRA](./examples/scripts/train_sft_mixtral_lora.sh) (`--ds.lora.rank`, `--ds.load_in_4bit`)
- [混合专家模型（MoE）](./examples/test_scripts/train_sft_moe.sh) (`--actor.aux_loss_coef`)
- FlashAttention (`--ds.attn_implementation`)
- HuggingFace 对话模板 (`--data.apply_chat_template`)

**优化器**
- AdamW (默认): `--{actor,critic}.optim adam --{actor,critic}.adam.lr 2e-6`
- [Muon](https://kellerjordan.github.io/posts/muon/) (需 DeepSpeed ≥ 0.18.2，仅支持 2D 权重；嵌入层/头/一维参数使用辅助 AdamW): `--{actor,critic}.optim muon --{actor,critic}.muon.lr 1e-4 --{actor,critic}.muon.momentum 0.95`。Newton-Schulz 产生尺度不变更新，因此需禁用全局梯度裁剪：`--{actor,critic}.max_norm 0`（Adam 默认值 `1.0` 会截断 Muon 更新）。

**奖励塑造（Reward Shaping）**
- DAPO 风格超长惩罚用于长度控制 (`--reward.overlong_buffer_len`, `--reward.overlong_penalty_factor`) —— 对超过 `max_new_tokens - overlong_buffer_len` 的响应进行软惩罚
- ProRL 风格截断惩罚 (`--reward.stop_properly_penalty_coef`) —— 针对 `finish_reason='length'` 的样本：`coef ∈ [0, 1]` 按比例缩放奖励；`coef < 0` 将奖励设为固定值（如 `-0.5`）

**生产特性**
- Wandb (`--logger.wandb.key`) 和 TensorBoard (`--logger.tensorboard_dir`) 日志记录
- 检查点恢复 (`--ckpt.load_enable`, `--ckpt.save_steps`)
- 根据评估指标保存最佳检查点 (`--ckpt.best_metric_key`)
- 评估数据集 (`--eval.dataset`, `--eval.temperature`, `--eval.n_samples_per_prompt`) —— 支持异步训练
- 多进程数据加载 (`--data.dataloader_num_workers`，适用于 PPO/SFT/RM/DPO)
- PPO 可观测性：Actor/Critic 梯度范数及各阶段耗时 (`timing/make_experience`, `timing/ppo_train`, `timing/broadcast`, `timing/generation`, `timing/step_total`)

</details>

---

<a id="quick-start"></a>
## 🎬 快速开始

### 安装

**推荐方式**：使用 Docker 免配置部署

```bash
# 1. 启动 Docker 容器
docker run --runtime=nvidia -it --rm --shm-size="10g" --cap-add=SYS_ADMIN \
  -v $PWD:/openrlhf nvcr.io/nvidia/pytorch:25.11-py3 bash

# 2. 清理冲突包
sudo pip uninstall xgboost transformer_engine flash_attn pynvml -y

# 3. 安装 OpenRLHF（任选其一）
pip install openrlhf                    # 基础版
pip install openrlhf[vllm]              # + vLLM 0.19.1（推荐）
pip install openrlhf[vllm_latest]       # + 最新版 vLLM
pip install openrlhf[vllm,ring,liger]   # + 全部优化项
```

**备选：从源码安装**

```bash
git clone https://github.com/OpenRLHF/OpenRLHF.git
cd OpenRLHF
pip install -e .
```

> [!TIP]
> 我们推荐 **vLLM 0.19.1+** 以获得最佳性能。详见 [Dockerfiles](./dockerfile/) 和 [Nvidia-Docker 安装脚本](./examples/scripts/nvidia_docker_install.sh)。

### 准备数据集

OpenRLHF 提供灵活的数据处理方法：

**关键参数**:
- `--data.input_key`: 指定输入数据的 JSON key 名称
- `--data.apply_chat_template`: 使用 HuggingFace tokenizer 的 [对话模板](https://huggingface.co/docs/transformers/main/en/chat_templating)
- `--data.input_template`: 自定义模板字符串（替代对话模板）
- `--data.prompt_probs` / `--data.dataset_probs`: 混合多个数据集（例如 `0.1,0.4,0.5`）
- `--eval.dataset`: 指定评估数据集路径

**对话模板示例**:

```python
dataset = [{"input_key": [
  {"role": "user", "content": "Hello, how are you?"},
  {"role": "assistant", "content": "I'm doing great. How can I help you today?"},
  {"role": "user", "content": "I'd like to show off how chat templating works!"},
]}]

tokenizer.apply_chat_template(dataset[0]["input_key"], tokenize=False)
# Output: "<s>[INST] Hello, how are you? [/INST]I'm doing great...</s> [INST] I'd like to show off... [/INST]"
```

> [!NOTE]
> JSON key 选项因数据集类型而异。详见 [Reward Dataset](https://github.com/OpenRLHF/OpenRLHF/blob/main/openrlhf/datasets/reward_dataset.py#L10)、[SFT Dataset](https://github.com/OpenRLHF/OpenRLHF/blob/main/openrlhf/datasets/sft_dataset.py#L9) 和 [Prompt Dataset](https://github.com/OpenRLHF/OpenRLHF/blob/main/openrlhf/datasets/prompts_dataset.py#L6)。

<a id="supervised-fine-tuning"></a>
### 监督微调（SFT）

OpenRLHF 的模型检查点与 HuggingFace 模型完全兼容。你可通过 `--actor.model_name_or_path {name or path}`、`--reward.model_name_or_path {name or path}` 和 `--critic.model_name_or_path {name or path}` 指定模型名称或路径。我们在 [HuggingFace OpenRLHF](https://huggingface.co/OpenRLHF) 上提供了一些预训练检查点和数据集。

随后你可使用我们提供的启动脚本（位于 [examples/scripts](./examples/scripts/) 目录），或使用以下命令开始训练。

<details>
<summary>SFT command</summary>

```bash
deepspeed --module openrlhf.cli.train_sft \
   --data.max_len 4096 \
   --data.dataset Open-Orca/OpenOrca \
   --data.input_key question \
   --data.output_key response \
   --data.input_template $'User: {}\nAssistant: ' \
   --train.batch_size 256 \
   --train.micro_batch_size 2 \
   --data.max_samples 500000 \
   --actor.model_name_or_path meta-llama/Meta-Llama-3-8B \
   --ckpt.output_dir ./checkpoint/llama3-8b-sft \
   --ckpt.save_steps -1 \
   --logger.logging_steps 1 \
   --eval.steps -1 \
   --ds.zero_stage 2 \
   --train.max_epochs 1 \
   --ds.packing_samples \
   --ds.param_dtype bf16 \
   --adam.lr 5e-6 \
   --actor.gradient_checkpointing_enable \
   --logger.wandb.key {wandb_token}

# Additional options:
# --data.apply_chat_template                # Use HF tokenizer chat template
# --ds.ring_attn_size 2                      # Enable RingAttention (install ring_flash_attn first)
# --data.multiturn                          # Multi-turn fine-tuning loss
# --actor.pretrain_mode_enable                      # Continued pre-training mode
```

</details>


### 奖励模型训练

<details>
<summary>Reward model training command</summary>

```bash
deepspeed --module openrlhf.cli.train_rm \
   --ckpt.output_dir ./checkpoint/llama3-8b-rm \
   --ckpt.save_steps -1 \
   --logger.logging_steps 1 \
   --eval.steps -1 \
   --train.batch_size 256 \
   --train.micro_batch_size 1 \
   --actor.model_name_or_path OpenRLHF/Llama-3-8b-sft-mixture \
   --ds.param_dtype bf16 \
   --train.max_epochs 1 \
   --data.max_len 8192 \
   --ds.zero_stage 3 \
   --adam.lr 9e-6 \
   --data.dataset OpenRLHF/preference_dataset_mixture2_and_safe_pku \
   --data.apply_chat_template \
   --chosen_key chosen \
   --rejected_key rejected \
   --ds.packing_samples \
   --actor.gradient_checkpointing_enable \
   --logger.wandb.key {wandb_token}

```

</details>

建议将奖励模型的 `--value_prefix_head` 选项设置为 `score`，以便我们使用 `AutoModelForSequenceClassification` 加载模型：

```python
reward_model = AutoModelForSequenceClassification.from_pretrained(
              reward_model_path,
              num_labels=1,
              torch_dtype=torch.bfloat16,
              attn_implementation="flash_attention_2",
              use_cache=False,
          )
inputs = xxxx (Left Padding Input Tokens)
reward = reward_model.model(*inputs).last_hidden_state
reward = reward_model.score(reward)[:, -1]
```

### RL 训练：PPO/REINFORCE++ with Ray and vLLM

OpenRLHF 中的所有 RL 训练均通过**智能体执行流水线**运行。以下示例展示了使用混合引擎以获得最佳性能的单轮智能体执行（默认模式）：

```bash
# launch the master node of ray in container
ray start --head --node-ip-address 0.0.0.0 --num-gpus 8

# if you want to launch ray on more nodes, use
ray start --address {MASTER-NODE-ADDRESS}:6379  --num-gpus 8

ray job submit --address="http://127.0.0.1:8265" \
   --runtime-env-json='{"working_dir": "/openrlhf"}' \
   -- python3 -m openrlhf.cli.train_ppo_ray \
   --ref.num_nodes 1 \
   --ref.num_gpus_per_node 8 \
   --reward.num_nodes 1 \
   --reward.num_gpus_per_node 8 \
   --critic.num_nodes 1 \
   --critic.num_gpus_per_node 8 \
   --actor.num_nodes 1 \
   --actor.num_gpus_per_node 8 \
   --vllm.num_engines 4 \
   --vllm.tensor_parallel_size 2 \
   --train.colocate_all \
   --vllm.gpu_memory_utilization 0.5 \
   --actor.model_name_or_path OpenRLHF/Llama-3-8b-sft-mixture \
   --reward.model_name_or_path OpenRLHF/Llama-3-8b-rm-700k \
   --ckpt.output_dir /openrlhf/examples/test_scripts/final/llama3-8b-rlhf \
   --ckpt.path /openrlhf/examples/test_scripts/ckpt/llama3-8b-rlhf \
   --ckpt.save_hf \
   --train.batch_size 128 \
   --rollout.batch_size 1024 \
   --train.dynamic_batch_enable \
   --rollout.n_samples_per_prompt 1 \
   --train.max_epochs 1 \
   --prompt_max_len 1024 \
   --data.max_samples 100000 \
   --generate_max_len 1024 \
   --ds.zero_stage 3 \
   --ds.param_dtype bf16 \
   --actor.adam.lr 5e-7 \
   --critic.adam.lr 9e-6 \
   --algo.kl.init_coef 0.01 \
   --data.prompt_dataset OpenRLHF/prompt-collection-v0.1 \
   --data.input_key context_messages \
   --data.apply_chat_template \
   --reward.normalize_enable \
   --actor.gradient_checkpointing_enable \
   --ds.packing_samples \
   --vllm.sync_backend nccl \
   --vllm.enforce_eager \
   --vllm.enable_sleep \
   --ds.enable_sleep \
   --logger.wandb.key {wandb_token}

# Algorithm Variants (all use single-turn agent execution):
# --algo.advantage.estimator reinforce        # REINFORCE++
# --algo.advantage.estimator rloo             # RLOO
# --algo.advantage.estimator reinforce_baseline  # REINFORCE++-baseline (best for RLVR)
# --algo.advantage.estimator group_norm       # GRPO
# --algo.advantage.estimator dr_grpo          # Dr. GRPO

# Advanced Options:
# --algo.kl.init_coef 0                                    # No reference model
# --reward.remote_url http://host:5000/get_reward         # HTTP reward model
# --rollout.n_samples_per_prompt 4                            # Multiple samples per prompt
# --rollout.vllm_generate_batch_size 2048                     # Oversample at generation (> rollout_batch_size); requires --train.async_enable
# --algo.advantage.is_correction_enable                         # vLLM importance sampling correction for off-policy rollouts
# --algo.advantage.is_correction_type tis                       # Correction type: tis (token clamp) | icepop (token filter) | seq-mask-tis (seq-level geom mean)
# --algo.advantage.is_correction_threshold 0.5 5.0               # IS truncation interval: [low, high]
# --ckpt.best_metric_key eval_default_pass1                # Save best checkpoint by eval metric (empty = auto-detect first pass1, 'none' = disable)
# --actor.policy_loss_type gspo                             # Use GSPO policy loss variant (vs default 'ppo')
```

> [!TIP]
> **推理任务（RLVR）**: 使用 `--algo.advantage.estimator reinforce_baseline` 启用 REINFORCE++-baseline——它对不同奖励尺度具有鲁棒性。

> [!NOTE]
> **Ray 环境配置**: 让 Ray 自动部署，使用 `--runtime-env-json='{"setup_commands": ["pip install openrlhf[vllm]"]}'`

> [!NOTE]
> **排查 GPU 索引错误**: 如果遇到 DeepSpeed GPU 设备设置问题，请设置 `export RAY_EXPERIMENTAL_NOSET_CUDA_VISIBLE_DEVICES=1`。

📚 **更多示例**: 见 [examples/scripts](./examples/scripts/) 和 [文档](https://openrlhf.readthedocs.io/en/latest/usage.html)

---

<a id="single-turn-agent-reinforced-fine-tuning-with-custom-rewards"></a>
## 🎯 单轮智能体：带自定义奖励的强化微调

**单轮智能体执行（默认模式）** 支持自定义奖励函数——非常适合在没有训练好的奖励模型的情况下进行强化微调。你无需使用预训练的奖励模型，而是提供一个 Python 函数来实时计算奖励。

**适用场景**:
- 基于规则的奖励（长度、格式、代码执行、数学验证）
- 外部 API 奖励（评判模型、编译器、测试套件）
- 混合奖励（结合多个信号）

### 示例：自定义奖励函数

```python
# reward_func.py
import torch

def reward_func(queries, prompts, labels):
    """
    Compute custom rewards for generated responses.
    
    Args:
        queries: List[str] - Full text (prompt + response)
        prompts: List[str] - Original prompts only
        labels: List[str] - Ground truth labels (from --label_key)
    
    Returns:
        dict with:
            - rewards: Tensor for advantage calculation
            - scores: Tensor for dynamic filtering (0-1 range)
            - extra_logs: Dict for wandb logging
    """
    batch_size = len(queries)
    
    # Example: Random rewards (replace with your logic)
    # Real examples: code execution, math verification, format checking
    reward = torch.randint(0, 2, (batch_size,)).float()

    return {
        "rewards": reward,           # Used in RL advantage calculation
        "scores": reward,            # Used for dynamic filtering (--dynamic_filtering)
        "extra_logs": {              # Logged to wandb
            "custom_metric": reward.mean().item(),
        },
    }
```

### 使用方法

```bash
ray job submit --address="http://127.0.0.1:8265" \
  --runtime-env-json='{"working_dir": "/openrlhf"}' \
  -- python3 -m openrlhf.cli.train_ppo_ray \
  --actor.model_name_or_path meta-llama/Meta-Llama-3-8B \
  --train.dynamic_batch_enable \
  --reward.remote_url /path/to/reward_func.py \
  --data.label_key answer \
  --data.prompt_dataset your_prompt_dataset \
  ... # other training args
```

**关键参数**: `--data.label_key answer` 将数据集中的 "answer" 字段传递给 `reward_func` 作为 `labels`。

> [!TIP]
> **用例**: 代码生成（执行测试）、数学（验证解法）、格式化（检查结构）、多目标（结合多个信号）

📖 **完整示例**: [examples/scripts/train_ppo_with_reward_fn.sh](./examples/scripts/train_ppo_with_reward_fn.sh)

---

<a id="multi-turn-agent-complex-environment-interactions"></a>
## 🤖 多轮智能体：复杂环境交互

对于需要**多步交互**的任务（推理链、带反馈的编码、游戏博弈），OpenRLHF 提供了 **Multi-Turn Agent Execution（多轮智能体执行）** 模式。

### 构建自定义多轮智能体

实现 `AgentInstanceBase` 并包含 `reset/step` 方法：

```python
# agent_func.py
import random
from typing import Any, Dict

import torch
from openrlhf.utils.agent import AgentInstanceBase, MultiTurnAgentExecutor


# A simple n-step random environment
class AgentInstance(AgentInstanceBase):
    async def __init__(self, *args, **kwargs):
        self.step_idx = 0
        self.max_steps = random.randint(1, 3)  # 1-3 steps

    async def reset(self, states: dict, **kwargs):
        return {"observation": states["observation"]}  # Return original text observation

    async def step(self, states: dict, **kwargs) -> Dict[str, Any]:
        print(f"step_idx: {self.step_idx}, max_steps: {self.max_steps}")

        observation_text = states["observation_text"]
        action_text = states["action_text"]
        label = states["label"]

        # Check if episode is done
        done = self.step_idx >= self.max_steps
        reward = torch.randint(0, 2, (1,)).float() if done else torch.tensor(0)

        # Generate environment feedback based on whether episode is done
        environment_feedback = (
            "\n\nHuman: [CORRECT]\n</s>"
            if done
            else "\n\nHuman: [INCORRECT]\nPlease analyze the issues and try again.\n</s>\n\nAssistant: "
        )

        self.step_idx += 1

        return {
            "rewards": reward,  # Rewards for advantage calculation
            "scores": reward,  # Scores for dynamic filtering (0-1 reward)
            "environment_feedback": environment_feedback,  # Environment feedback text
            "done": done,  # Boolean indicating if the episode is complete
            "sampling_params": states.get("sampling_params", None),  # Parameters for vLLM sampling in next step
            "extra_logs": {"dummy_scores": reward},  # Additional logging information
        }


class AgentExecutor(MultiTurnAgentExecutor):
    def __init__(self):
        super().__init__(AgentInstance)
```

随后通过以下命令启动：

```bash
ray job submit --address="http://127.0.0.1:8265" \
  --runtime-env-json='{"working_dir": "/openrlhf"}' \
  -- python3 -m openrlhf.cli.train_ppo_ray \
  ...
  --train.dynamic_batch_enable \
  --train.agent_func_path /path/to/agent_func.py \
  --train.async_enable  # Optional: enable async pipeline
```

### 配置选项

**异步流水线（用于更高吞吐量）**:
- 启用：`--train.async_enable`
- 缓冲区大小：`--train.async_queue_size 1`（越大 = 偏离策略程度越高，默认 1）
- 部分生成（Partial rollout）：`--train.partial_rollout_enable` —— 使用 vLLM 暂停/恢复进行权重同步而非锁定，允许生成与训练重叠。飞行中样本可能包含新旧权重的词元。

**训练模式**:
- **同步（Synchronous）**：默认值，稳定性更好
- **异步（Asynchronous）**：吞吐量更高，可能影响收敛性
- **混合引擎（Hybrid Engine）**：配合 `--train.colocate_all` 获得最佳 GPU 利用率（移除 `--train.async_enable`）

> [!NOTE]
> 对于完全自定义的词元级执行，继承 `AgentExecutorBase` 并实现 `execute()`。该设计强制执行**词元输入-输出原则**以保持采样与训练的一致性。

> [!WARNING] 
> 异步训练可能影响训练稳定性。仅当吞吐量至关重要且收敛性已得到验证时才使用。

📚 **示例**:
- 单轮：[train_ppo_ray_hybrid_engine.sh](./examples/scripts/train_ppo_ray_hybrid_engine.sh)
- 自定义奖励：[train_ppo_with_reward_fn.sh](./examples/scripts/train_ppo_with_reward_fn.sh)
- 多轮：[train_reinforce_baseline_ray_agent_async.sh](./examples/scripts/train_reinforce_baseline_ray_agent_async.sh)
- 多轮 VLM（图像反馈）：[vlm_multiturn_agent.py](./examples/python/vlm_multiturn_agent.py)

### OpenAI 兼容智能体服务器

对于需要 OpenAI 兼容聊天 API 的多轮智能体（例如集成外部工具使用框架），[`agent_func_openai_server_executor.py`](./examples/python/agent_func_openai_server_executor.py) 将 vLLM 封装为本地 `/v1/chat/completions` 服务器，同时收集词元级轨迹用于 RL 训练。

- 暴露标准 OpenAI 端点 (`/v1/chat/completions`, `/v1/models`, `/tokenize`)
- 自动按会话收集词元 ID 和 logprobs 用于 RL 训练
- Delta-tokenization 在多轮调用中复用前缀词元
- 重写 `run_agent()` 以接入你自己的多轮工作流

```bash
python3 -m openrlhf.cli.train_ppo_ray \
  --train.agent_func_path examples/python/agent_func_openai_server_executor.py \
  ... # other training args
```

---

<a id="advanced-topics"></a>
## 🔧 高级主题

### LoRA：合并适配器（Merging Adapters）

使用 LoRA/QLoRA 时，OpenRLHF 仅保存适配器权重。要部署或继续训练，需将适配器与基础模型合并：

```bash
python -m openrlhf.cli.lora_combiner \
    --model_path meta-llama/Meta-Llama-3-8B \
    --lora_path ./checkpoint/llama3-8b-rm \
    --output_path ./checkpoint/llama-3-8b-rm-combined \
    --is_rm \
    --ds.param_dtype bf16
```

### 性能调优指南（Performance Tuning Guide）

根据你的硬件和工作负载优化 OpenRLHF：

#### 🎯 执行模式：吞吐量 vs. 稳定性

根据优先级选择执行模式——OpenRLHF 提供清晰的权衡选项：

| 模式 | 标志位 | 特性 | 适用场景 |
|------|-------|-----------------|-------------|
| **混合引擎（同置）** | `--train.colocate_all`<br>`--vllm.enable_sleep`<br>`--ds.enable_sleep` | **最稳定** —— 严格遵循策略，每次生成均使用最新权重。串行 generate→train 循环。 | 研究、对 RL 算法敏感的场景、可复现性、配方验证 |
| **异步训练（Async Training）** | `--train.async_enable`<br>`--train.async_queue_size N` | **最高吞吐量** —— 生成与训练并行运行。通过 `--train.async_queue_size` 调整偏离策略程度（越大 = 越高）。 | 收敛性已验证的生产环境吞吐量优化 |
| **异步 + 部分生成** | `--train.async_enable`<br>`--train.partial_rollout_enable` | **最大重叠度** —— vLLM 暂停/恢复替代锁定，飞行中样本可能混合新旧权重。偏离策略程度最高。 | 进一步压榨异步吞吐量；建议搭配 `--algo.advantage.is_correction_enable` 使用 |

#### ⚡ 其他速度优化

| 优化项 | 标志位 | 适用场景 |
|--------------|------|-------------|
| **样本打包（Sample Packing）** | `--ds.packing_samples` | 始终启用（尤其是训练阶段） |
| **动态批次** | `--train.dynamic_batch_enable` | 变长序列 |
| **DeepCompile** | `--ds.deepcompile` | PyTorch 2.0+ |
| **通信重叠** | `--ds.overlap_comm` | GPU 内存充足时 |
| **前缀缓存（Prefix Caching）** | vLLM config | `n_samples_per_prompt` > 1 |
| **过采样（Oversampling）** | `--rollout.vllm_generate_batch_size > --rollout.batch_size` | 异步模式，分摊生成成本/喂入动态过滤 |

#### 💾 内存管理

**当你拥有充足内存时**:
- ✅ 禁用 `--ds.adam_offload`
- ✅ 启用 `--ds.overlap_comm`
- ✅ 使用 `--train.colocate_critic_reward` 和 `--train.colocate_actor_ref`

**当遇到 OOM（显存溢出）时**:
- ❌ 禁用所有 `--colocate_*` 选项
- ✅ 减小批次大小
- ✅ 启用梯度检查点（Gradient Checkpointing）

#### 🎮 批次大小调优

1. **生成阶段**：最大化 `--rollout.micro_batch_size`，最小化 vLLM TP 大小
2. **训练阶段**：最大化 `--train.micro_batch_size`，启用 `--ds.packing_samples`
3. **vLLM**：始终使用 `--vllm.sync_backend nccl`

> [!TIP]
> **快速启动模板**: 对于 8x A100 (80GB)，尝试混合引擎 + `--vllm.gpu_memory_utilization 0.5` + `--train.colocate_all`

📖 **更多细节**: [性能调优文档](https://openrlhf.readthedocs.io/en/latest/performance.html)


## 使用 OpenRLHF 的公司与组织

- Google
- ByteDance
- Tencent
- Alibaba
- Baidu
- China Telecom
- Vivo
- Allen AI
- NexusFlow
- Jülich Supercomputing Centre (JSC)
- Berkeley Starling Team
- M-A-P
- ...

## 加入我们（Join Us）

**如何加入？**

1. 发送邮件至 janhu9527@gmail.com 或加入 [GitHub Organization](https://github.com/OpenRLHF)。请包含以下信息：
   - 你的姓名
   - 你的 GitHub 用户名
   - 你的兴趣领域
   - 你在 NLP 和/或 AI 相关的技能与经验
1. 你也可通过官方 GitHub [OpenRLHF ↗](https://github.com/OpenRLHF/OpenRLHF) 项目页面加入我们。只需创建一个关于你贡献意愿的 Issue，我们会与你联系。

**你能做什么？**

1. 加入团队并参与 OpenRLHF 项目的开发。
1. 通过提交 Pull Requests 为项目做出贡献。
1. 帮助改进文档、修复 Bug 或创建新功能。
1. 分享该项目并帮助我们壮大社区。

## 赞助我们（Sponsor Us）

你的赞助将帮助我们维护和改善 OpenRLHF。如果你觉得这个项目有用，请考虑赞助我们。你可以在 [Open Collective ↗](https://opencollective.com/OpenRLHF) 上赞助我们。

## Starchart

[![Star History Chart](https://api.star-history.com/svg?repos=OpenRLHF/OpenRLHF&type=Date)](https://star-history.com/#OpenRLHF/OpenRLHF&Date)

## Contributors

感谢所有贡献者！如果你想做出贡献，欢迎提交 Pull Request 或创建 Issue。

<a href="https://github.com/OpenRLHF/OpenRLHF/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=OpenRLHF/OpenRLHF" />
</a>

## References & Acknowledgements

我们要向以下项目和组织在 AI 和 NLP 领域的贡献表示感谢：

- [Hugging Face Transformers ↗](https://github.com/huggingface/transformers)
- [OpenAI GPT ↗](https://github.com/openai/gpt-3)
- [LLaMA ↗](https://llama.meta.com/)
- [DeepSpeed ↗](https://github.com/microsoft/DeepSpeed)
- [Ray ↗](https://github.com/ray-project/ray)

我们的项目还要感谢 [ColossalChat](https://github.com/hpcaitech/ColossalAI/tree/main/applications/ColossalChat) 和 [DeepSpeedChat](https://github.com/microsoft/DeepSpeedExamples/tree/master/applications/DeepSpeed-Chat)。在项目早期阶段，我们参考了它们的代码设计。
我们的项目还要感谢 [Netmind.AI](https://www.netmind.ai/) 为开发 Ring Attention 提供的 GPU 支持。

(2024/7) 我们的 GitHub 组织已从 OpenLLMAI 更名为 OpenRLHF。

## Citation
OpenRLHF

```
@article{hu2024openrlhf,
  title={OpenRLHF: An Easy-to-use, Scalable and High-performance RLHF Framework},
  author={Jian Hu and Xibin Wu and Zilin Zhu and Xianyu and Weixun Wang and Dehao Zhang and Yu Cao},
  journal={arXiv preprint arXiv:2405.11143},
  year={2024}
}
```
REINFORCE++-baseline
```
@article{hu2026reinforce++,
  title={Reinforce++: A simple and efficient approach for aligning large language models},
  author={Hu, Jian},
  journal={arXiv preprint arXiv:2501.03262},
  year={2026}
}
```

______________________________________________________________________

*OpenRLHF © 2026 OpenRLHF. All Rights Reserved.*
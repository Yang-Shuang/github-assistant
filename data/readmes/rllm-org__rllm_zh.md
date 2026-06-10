<div align="center">

# rLLM

**使用强化学习（RL）训练你的 AI Agent。支持任意框架，仅需极少的代码修改。**

[![Documentation](https://img.shields.io/badge/Documentation-blue?style=for-the-badge&logo=googledocs&logoColor=white)](https://docs.rllm-project.com/)
[![Slack](https://img.shields.io/badge/Slack-4A154B?style=for-the-badge&logo=slack&logoColor=white)](https://join.slack.com/t/rllmproject/shared_invite/zt-3pyblo6ef-m9kqAoInI8xSyUBkpuOyXA)
[![Website](https://img.shields.io/badge/Site-%233f72af.svg?style=for-the-badge&logo=semanticweb&logoColor=white)](https://rllm-project.com)
[![Blogs](https://img.shields.io/badge/Blogs-007AFF?style=for-the-badge)](https://rllm-project.com/blog)
[![X](https://img.shields.io/badge/-black?logo=X&style=for-the-badge)](https://x.com/rllm_project)

<!-- [![PyPI](https://img.shields.io/pypi/v/rllm?style=for-the-badge)](https://pypi.org/project/rllm/) -->

</div>

rLLM 是一个开源框架，用于通过强化学习（RL）训练 AI Agent。只需替换受监控的客户端、定义奖励函数，即可让 RL 处理其余工作——无论你使用何种 Agent 框架。

## 核心特性

- **兼容任意 Agent 框架** —— LangGraph、SmolAgent、Strands、OpenAI Agents SDK、Google ADK，或直接使用 `openai.OpenAI`。只需替换客户端即可。🔌
- **近乎零代码修改** —— 添加 `@rllm.rollout` 装饰器包裹你的 Agent 代码，rLLM 会自动追踪每一次 LLM 调用。🪄
- **以 CLI 优先的工作流** —— 通过命令行进行评测与训练，内置 50 多个基准测试。运行 `rllm eval gsm8k` 即可直接使用。⚡
- **经过实战检验的效果** —— 经 rLLM 训练的 Agent 可击败参数量大其 50 倍的模型（4B → 在金融任务上超越 235B 模型，1.5B → 在数学任务上超越 O1-Preview）。📈
- **支持多种 RL 算法** —— 包括 GRPO、REINFORCE、RLOO、拒绝采样等。🧠
- **双训练后端** —— 使用 `verl` 进行分布式多 GPU 训练，使用 `tinker` 进行单机/CPU 部署。两者提供相同的 API。🔧

更多详情请查阅[官方文档站点](https://docs.rllm-project.com/)。

## 安装指南

rLLM 需要 `Python >= 3.11`。你可以通过 pip 直接安装，或从源码编译。

```bash
uv pip install "rllm @ git+https://github.com/rllm-org/rllm.git"
```

此命令将安装运行 rLLM CLI 所需的依赖项，默认使用 Tinker 作为训练后端。 

若要将 `verl` 用作训练后端（需 GPU 机器），请通过以下命令安装：

```bash
# For distributed GPU training (verl + vLLM/SGLang)
uv pip install rllm[verl] @ git+https://github.com/rllm-org/rllm.git
```

如需从源码构建或使用 Docker，请参阅[安装指南](https://docs.rllm-project.com/installation)。

## 快速开始

### 选项 A：CLI（无需编写代码）

```bash
# 1. Configure your model provider
rllm model setup

# 2. Evaluate on a benchmark
rllm eval gsm8k

# 3. Train with RL
rllm train gsm8k
```

### 选项 B：Python API

定义一个 rollout（你的 Agent）和一个 evaluator（你的奖励函数），然后将它们交给训练器：

```python
# my_flow.py
from openai import OpenAI
import rllm
from rllm.types import AgentConfig, Episode, Task, Trajectory

@rllm.rollout
def solve(task: Task, config: AgentConfig) -> Episode:
    client = OpenAI(base_url=config.base_url, api_key="EMPTY")
    response = client.chat.completions.create(
        model=config.model,
        messages=[{"role": "user", "content": task.instruction}],
    )
    answer = response.choices[0].message.content or ""
    return Episode(
        trajectories=[Trajectory(name="solver", steps=[])],
        artifacts={"answer": answer},
    )
```

```python
# my_evaluator.py
import rllm
from rllm.eval.types import EvalOutput, Signal
from rllm.types import Episode

@rllm.evaluator
def score(task: dict, episode: Episode) -> EvalOutput:
    answer = str(episode.artifacts.get("answer", ""))
    is_correct = answer.strip() == task["ground_truth"].strip()
    reward = 1.0 if is_correct else 0.0
    return EvalOutput(reward=reward, is_correct=is_correct,
                      signals=[Signal(name="accuracy", value=reward)])
```

```python
# train.py
from rllm.experimental.unified_trainer import AgentTrainer

trainer = AgentTrainer(
    backend="tinker",
    agent_flow=solve,
    evaluator=score,
    config=config,
    train_dataset=dataset,
)
trainer.train()
```

在训练过程中，`config.base_url` 指向一个网关，该网关会透明地捕获 Token ID 和 Logprobs——你的 Agent 代码在评测与训练中完全一致。

完整的可运行示例（单轮 VLM 求解器、多 Agent 求解-评判模式等）请参阅[Cookbook](./cookbooks)。

## 架构设计

rLLM 遵循一条简洁的流水线：**运行你的 Agent → 收集轨迹（Traces）→ 计算奖励（Rewards）→ 更新模型**。

```
┌──────────────┐    ┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│  Your Agent  │───▶│    Traces     │───▶│   Rewards    │───▶│  RL Update   │
│  (any code)  │    │  (auto-logged)│    │ (your logic) │    │  (GRPO etc.) │
└──────────────┘    └──────────────┘    └──────────────┘    └──────────────┘
```

你的 Agent 按原样运行——rLLM 的模型网关通过基于 URL 路由的会话捕获 LLM 调用（Token ID + Logprobs），并将其结构化为 **Episodes**（单次任务），其中包含由 **Trajectories**（一次 Agent 运行）组成的 **Steps**（单次 LLM 调用）。奖励函数对结果进行评分，RL 算法随后更新模型权重。同一份 Agent 代码可同时用于评测和训练。

底层实现包括：
- **工作流引擎（Workflow Engine）**：运行 N 个并行的 Agent 实例以收集 Rollout 数据
- **模型网关（Model Gateway）**：路由请求并捕获 Token ID 与 Logprobs
- **转换流水线（Transform Pipeline）**：对 Trajectories 进行分组以计算优势值（Advantage）
- **训练后端（Training Backend）**（verl 或 tinker）：负责策略更新

## 社区项目

- [Tongyi DeepResearch](https://github.com/Alibaba-NLP/DeepResearch) —— 阿里 NLP 开源的 AI 研究人员工具 [![Stars](https://img.shields.io/github/stars/Alibaba-NLP/DeepResearch)](https://github.com/Alibaba-NLP/DeepResearch)
- [Terminal-Bench-RL](https://github.com/Danau5tin/terminal-bench-rl) —— 使用 RL 训练长视野终端 Agent [![Stars](https://img.shields.io/github/stars/Danau5tin/terminal-bench-rl)](https://github.com/Danau5tin/terminal-bench-rl)
- [PettingLLMs](https://github.com/pettingllms-ai/PettingLLMs) —— 基于在线策略（on-policy）的多 Agent RL [![Stars](https://img.shields.io/github/stars/pettingllms-ai/PettingLLMs)](https://github.com/pettingllms-ai/PettingLLMs)
- [SETA](https://github.com/camel-ai/seta) —— 扩展终端 Agent 的训练环境 [![Stars](https://img.shields.io/github/stars/camel-ai/seta)](https://github.com/camel-ai/seta)
- [LLM-in-Sandbox](https://github.com/llm-in-sandbox/llm-in-sandbox) —— 在沙盒中运行 LLM 以构建通用 Agent [![Stars](https://img.shields.io/github/stars/llm-in-sandbox/llm-in-sandbox)](https://github.com/llm-in-sandbox/llm-in-sandbox)
- [Vision-DeepResearch](https://github.com/Osilly/Vision-DeepResearch) —— 首个长视野多模态深度研究 MLLM [![Stars](https://img.shields.io/github/stars/Osilly/Vision-DeepResearch)](https://github.com/Osilly/Vision-DeepResearch)
- [OpenSearch-VL](https://github.com/shawn0728/OpenSearch-VL) - 面向前沿多模态搜索 Agent 的开源方案 [![Stars](https://img.shields.io/github/stars/shawn0728/OpenSearch-VL)](https://github.com/shawn0728/OpenSearch-VL)
- [Cogito, Ergo Ludo](https://www.arxiv.org/abs/2509.25052) —— 一种通过推理与规划学习游玩规则的 Agent
- [Cut the Bill, Keep the Turns](https://agate-slipper-ef0.notion.site/Cut-the-Bill-Keep-the-Turns-Affordable-Multi-Turn-Search-RL-003f78214a4d451fb06f453d084e666c) —— 经济实惠的多轮搜索 RL
- [Experiential Reinforcement Learning](https://arxiv.org/abs/2602.13949) —— 针对稀疏奖励的“体验-反思-巩固”RL 循环
- [V1: Unifying Generation and Self-Verification](https://arxiv.org/abs/2603.04304) —— 用于并行测试时扩展的成对自验证方法
- [TherapyGym](https://therapygym.stanford.edu/) - 评估与对齐临床治疗聊天机器人的专业度与安全性的基准
- [SandMLE](https://arxiv.org/pdf/2604.04872) - 用于训练 MLE Agent 的合成沙盒

## 文章与博客

- [rLLM UI：面向 Agent 训练与评测的实时可观测工具](https://rllm-project.com/post.html?post=rllm_ui.md) — Mar 2026
- [rLLM 在线策略蒸馏：从强教师模型训练小型学生模型](https://rllm-project.com/post.html?post=opd.md) — Mar 2026
- [更快更强：基于全异步训练的开源深度研究 Agent 方案](https://rllm-project.com/post.html?post=async_rl.md) — Feb 2026
- [rLLM-FinQA：4B 模型如何超越 235B 并媲美 Gemini 2.5 Pro（金融分析）](https://rllm-project.com/post.html?post=finqa.md) — Feb 2026
- [rLLM SDK：无需修改代码即可训练任意 Agent 程序](https://rllm-project.com/post.html?post=sdk.md) — Dec 2025
- [rLLM v0.2：面向通用 Agent 程序的 RL 训练](https://rllm-project.com/post.html?post=rllm_v0.2.md) — Oct 2025
- [DeepSWE：基于 RL 的开源 SWE Agent](https://pretty-radio-b75.notion.site/DeepSWE-Training-a-Fully-Open-sourced-State-of-the-Art-Coding-Agent-by-Scaling-RL-22281902c1468193aabbe9a8c59bbe33) — Jul 2025
- [DeepCoder：达到 O3-mini 水平的 14B 代码生成模型](https://pretty-radio-b75.notion.site/DeepCoder-A-Fully-Open-Source-14B-Coder-at-O3-mini-Level-1cf81902c14680b3bee5eb349a512a51) — Apr 2025
- [DeepScaleR：1.5B 模型超越 O1-Preview](https://pretty-radio-b75.notion.site/DeepScaleR-Surpassing-O1-Preview-with-a-1-5B-Model-by-Scaling-RL-19681902c1468005bed8ca303013a4e2) — Feb 2025

## 致谢

本工作由[伯克利天空计算实验室（Berkeley Sky Computing Lab）](https://sky.cs.berkeley.edu/)支持完成。rLLM 团队衷心感谢 [Laude Institute](https://www.laude.org/)、[AWS](https://aws.amazon.com/)、[Hyperbolic](https://www.hyperbolic.ai/)、[Fireworks AI](https://fireworks.ai/) 和 [Modal](https://modal.com/) 提供的资金支持。特别感谢 [Together AI](https://www.together.ai/) 在研究合作与算力资源方面的大力支持。

## 引用

```bibtex
@misc{rllm2025,
  title={rLLM: A Framework for Post-Training Language Agents},
  author={Sijun Tan and Michael Luo and Colin Cai and Tarun Venkat and Kyle Montgomery and Aaron Hao and Tianhao Wu and Arnav Balyan and Manan Roongta and Chenguang Wang and Li Erran Li and Raluca Ada Popa and Ion Stoica},
  year={2025},
  howpublished={\url{https://pretty-radio-b75.notion.site/rLLM-A-Framework-for-Post-Training-Language-Agents-21b81902c146819db63cd98a54ba5f31}},
  note={Notion Blog},
}
```

你也可以引用我们之前的工作 [DeepScaleR](https://scholar.googleusercontent.com/scholar.bib?q=info:PrmBADk39GwJ:scholar.google.com/&output=citation&scisdr=CgIJFx-xEMCQ6zOgcuI:AAZF9b8AAAAAaPCmauIfzg8Rm9ImNYDad0uPUK8&scisig=AAZF9b8AAAAAaPCmahXsNqb1jTQBw2iPfw2vm9g&scisf=4&ct=citation&cd=-1&hl=en&scfhb=1)、[DeepCoder](https://scholar.googleusercontent.com/scholar.bib?q=info:xpZNEPI6opAJ:scholar.google.com/&output=citation&scisdr=CgIJFx-xEMCQ6zOgjM8:AAZF9b8AAAAAaPCmlM_hb3S0tzBSVrRYBZYDLWg&scisig=AAZF9b8AAAAAaPCmlG109SG8d8230AiDP4jMxlw&scisf=4&ct=citation&cd=-1&hl=en&scfhb=1) 和 [DeepSWE](https://scholar.googleusercontent.com/scholar.bib?q=info:J9rT3SnY_aMJ:scholar.google.com/&output=citation&scisdr=CgIJFx-xEMCQ6zOg3D4:AAZF9b8AAAAAaPCmxD7Nl0xA_AcAeydpcE1BXCo&scisig=AAZF9b8AAAAAaPCmxE2Spzf5lf-2Toys5xEpnuA&scisf=4&ct=citation&cd=-1&hl=en&scfhb=1)。
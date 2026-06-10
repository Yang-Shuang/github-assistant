# AI Research `Skills` 库

> **最全面的开源技能库，赋能 AI 智能体自主开展 AI 研究——从构思到论文成稿**

<p align="center">
  <img src="docs/assets/promo.gif" alt="AI Research Skills Demo" width="700">
</p>

<p align="center">
  <a href="https://opensource.org/licenses/MIT"><img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="License: MIT"></a>
  <a href="https://www.npmjs.com/package/@orchestra-research/ai-research-skills"><img src="https://img.shields.io/npm/v/@orchestra-research/ai-research-skills.svg" alt="npm version"></a>
  <a href="https://www.orchestra-research.com/perspectives/ai-research-skills"><img src="https://img.shields.io/badge/Blog-Read%20More-orange.svg" alt="Blog Post"></a>
  <a href="https://join.slack.com/t/orchestrarese-efu1990/shared_invite/zt-3iu6gr8io-zJvpkZTPToEviQ9KFZvNSg"><img src="https://img.shields.io/badge/Slack-Join%20Community-4A154B.svg?logo=slack" alt="Slack"></a>
  <a href="https://x.com/orch_research"><img src="https://img.shields.io/badge/Twitter-Follow-1DA1F2.svg?logo=x" alt="Twitter"></a>
  <a href="https://www.linkedin.com/company/orchestra-research/"><img src="https://img.shields.io/badge/LinkedIn-Follow-0A66C2.svg?logo=linkedin" alt="LinkedIn"></a>
</p>

<div align="center">

### **2026 年驱动 AI 研究的 98 项技能**

</div>

<details>
<summary><b>查看所有 23 个分类</b></summary>

<div align="center">

| | | |
|:---:|:---:|:---:|
| **Autoresearch**（1） | **Ideation**（2） | **ML Paper Writing**（2） |
| **Model Architecture**（5） | **Fine-Tuning**（4） | **Post-Training**（8） |
| **Distributed Training**（6） | **Optimization**（6） | **Inference**（4） |
| **Tokenization**（2） | **Data Processing**（2） | **Evaluation**（3） |
| **Safety & Alignment**（4） | **Agents**（4） | **RAG**（5） |
| **Multimodal**（7） | **Prompt Engineering**（4） | **MLOps**（3） |
| **Observability**（2） | **Infrastructure**（3） | **Mech Interp**（4） |
| **Emerging Techniques**（6） | **Agent-Native Research Artifact**（3） | |

</div>

</details>

---

## 目录

- [我们的使命](#我们的使命)
- [迈向 AI 研究智能体的路径](#迈向-ai-研究智能体的路径)
- [可用的 AI 研究工程技能](#可用的-ai-研究工程技能)
- [演示示例](#演示示例)
- [技能结构](#技能结构)
- [路线图](#路线图)
- [仓库结构](#仓库结构)
- [使用场景](#使用场景)
- [贡献者](#贡献者)
- [引用格式](#引用格式)
- [社区](#社区)


## 我们的使命

我们赋能 AI 智能体**自主开展 AI 研究**——涵盖文献调研、构思生成、实验执行到论文撰写的全流程。该库提供了每个阶段所需的**研究编排层**（自动研究、创意构思、论文写作）以及**工程技能**（训练、评估、部署）。
<p align="center">
  <img src="docs/skills.png" alt="AI Research Agent System" width="50%">
  <br>
  <em>AI 研究智能体系统架构图</em>
</p>

## 迈向 AI 研究智能体的路径

现代 AI 研究需要掌握数十种专业工具与框架。研究人员往往将大量时间耗费在调试基础设施上，而非验证假设——这拖慢了科学发现的步伐。我们提供了一套全面的技能库，使 AI 智能体能够自主完成从头脑风暴到论文撰写的全生命周期研究工作：
- **自动研究**：**autoresearch**（自动研究）技能使用双循环架构编排整个研究工作流，按需路由至领域技能
- **垂直领域专长**：每个领域技能均提供针对特定框架（Megatron-LM、vLLM、TRL 等）的深度生产级知识
- **端到端覆盖**：98 项技能贯穿 AI 研究全生命周期，从构思与文献调研到实验和论文写作
- **科研级质量**：文档源自官方仓库、真实 GitHub Issue 及经过实战检验的生产工作流

## 可用的 AI 研究工程技能

**质量优于数量**：每项技能均提供全面、专家级的指导，包含真实代码示例、故障排除指南及生产就绪型工作流。

### 📦 快速安装（推荐）

**面向人类用户**——一条命令启动交互式安装程序：

```bash
npx @orchestra-research/ai-research-skills
```

**面向 AI 智能体**——将你的智能体指向欢迎文档，后续步骤由它自动处理：

```
Read https://www.orchestra-research.com/ai-research-skills/welcome.md and follow the instructions to install and use AI Research Skills.
```

此操作将安装全部 98 项技能，加载 **autoresearch**（自动研究）编排层，并启动自主研究工作。

<details>
<summary><b>安装程序的功能</b></summary>

- **自动检测**已安装的编程智能体（Claude Code、Hermes Agent、OpenCode、Cursor、Gemini CLI 等）
- **安装**技能至 `~/.orchestra/skills/`，并为各智能体创建软链接（Windows 下自动回退为复制）
- **提供**全套、快速入门包、按分类或单个技能的选项
- **更新**已安装技能至最新版本
- **卸载**全部或部分选定技能

</details>

<details>
<summary><b>CLI 命令</b></summary>

```bash
# Interactive installer (recommended)
npx @orchestra-research/ai-research-skills

# Direct commands
npx @orchestra-research/ai-research-skills list      # View installed skills
npx @orchestra-research/ai-research-skills update    # Update installed skills
```

</details>

<details>
<summary><b>Claude Code 市场（替代方案）</b></summary>

使用 **Claude Code CLI** 直接安装技能分类：

```bash
# Add the marketplace
/plugin marketplace add orchestra-research/AI-research-SKILLs

# Install by category (23 categories available)
/plugin install fine-tuning@ai-research-skills        # Axolotl, LLaMA-Factory, PEFT, Unsloth
/plugin install post-training@ai-research-skills      # TRL, GRPO, OpenRLHF, SimPO, verl, slime, miles, torchforge
/plugin install inference-serving@ai-research-skills  # vLLM, TensorRT-LLM, llama.cpp, SGLang
/plugin install distributed-training@ai-research-skills
/plugin install optimization@ai-research-skills
```

</details>

### 全部 23 个分类（98 项技能）

| Category | Skills | Included |
|----------|--------|----------|
| **Autoresearch** | **1** | **自主研究工作流编排——核心层，管理全生命周期并路由至所有其他技能** |
| Ideation | 2 | Research Brainstorming, Creative Thinking |
| ML Paper Writing | 2 | ML Paper Writing (LaTeX templates, citation verification), Academic Plotting |
| Model Architecture | 5 | LitGPT, Mamba, NanoGPT, RWKV, TorchTitan |
| Tokenization | 2 | HuggingFace Tokenizers, SentencePiece |
| Fine-Tuning | 4 | Axolotl, LLaMA-Factory, PEFT, Unsloth |
| Mech Interp | 4 | TransformerLens, SAELens, pyvene, nnsight |
| Data Processing | 2 | NeMo Curator, Ray Data |
| Post-Training | 8 | TRL, GRPO, OpenRLHF, SimPO, verl, slime, miles, torchforge |
| Safety | 4 | Constitutional AI, LlamaGuard, NeMo Guardrails, Prompt Guard |
| Distributed | 6 | DeepSpeed, FSDP, Accelerate, Megatron-Core, Lightning, Ray Train |
| Infrastructure | 3 | Modal, Lambda Labs, SkyPilot |
| Optimization | 6 | Flash Attention, bitsandbytes, GPTQ, AWQ, HQQ, GGUF |
| Evaluation | 3 | lm-evaluation-harness, BigCode, NeMo Evaluator |
| Inference | 4 | vLLM, TensorRT-LLM, llama.cpp, SGLang |
| MLOps | 3 | W&B, MLflow, TensorBoard |
| Agents | 4 | LangChain, LlamaIndex, CrewAI, AutoGPT |
| RAG | 5 | Chroma, FAISS, Pinecone, Qdrant, Sentence Transformers |
| Prompt Eng | 4 | DSPy, Instructor, Guidance, Outlines |
| Observability | 2 | LangSmith, Phoenix |
| Multimodal | 7 | CLIP, Whisper, LLaVA, BLIP-2, SAM, Stable Diffusion, AudioCraft |
| Emerging | 6 | MoE, Model Merging, Long Context, Speculative Decoding, Distillation, Pruning |
| Agent-Native Research Artifact | 3 | ARA Compiler, Research Manager, Rigor Reviewer |

<details>
<summary><b>查看所有 98 项技能详情</b></summary>

### 🔬 Autoresearch（1 项技能）——核心编排层
- **[Autoresearch](0-autoresearch-skill/)** - 使用双循环架构（内层优化 + 外层综合）实现自主研究编排。管理从文献调研到论文撰写的全生命周期，并路由至所有领域特定技能。支持 Claude Code /loop 和 OpenClaw heartbeat 以实现持续运行（390 lines + 3 refs）

### 🏗️ Model Architecture（5 项技能）
- **[LitGPT](01-model-architecture/litgpt/)** - Lightning AI 的 20+ 种精简 LLM 实现及生产级训练配方（462 lines + 4 refs）
- **[Mamba](01-model-architecture/mamba/)** - O(n) 复杂度的状态空间模型，速度比 Transformers 快 5×（253 lines + 3 refs）
- **[RWKV](01-model-architecture/rwkv/)** - RNN+Transformer 混合架构，支持无限上下文，Linux Foundation 项目（253 lines + 3 refs）
- **[NanoGPT](01-model-architecture/nanogpt/)** - Karpathy 编写的约 ~300 行的教育级 GPT 实现（283 lines + 3 refs）
- **[TorchTitan](01-model-architecture/torchtitan/)** - PyTorch 原生分布式训练框架，支持 Llama 3.1 的 4D 并行化

### 🔤 Tokenization（2 项技能）
- **[HuggingFace Tokenizers](02-tokenization/huggingface-tokenizers/)** - Rust 实现，<20s/GB，支持 BPE/WordPiece/Unigram 算法（486 lines + 4 refs）
- **[SentencePiece](02-tokenization/sentencepiece/)** - 语言无关分词器，50k sentences/sec，被 T5/ALBERT 广泛使用（228 lines + 2 refs）

### 🎯 Fine-Tuning（4 项技能）
- **[Axolotl](03-fine-tuning/axolotl/)** - 基于 YAML 的微调框架，支持 100+ 模型（156 lines + 4 refs）
- **[LLaMA-Factory](03-fine-tuning/llama-factory/)** - WebUI 无代码微调界面（78 lines + 5 refs）
- **[Unsloth](03-fine-tuning/unsloth/)** - QLoRA 微调速度提升 2×（75 lines + 4 refs）
- **[PEFT](03-fine-tuning/peft/)** - 参数高效微调，支持 LoRA、QLoRA、DoRA 等 25+ 种方法（431 lines + 2 refs）

### 🔬 Mechanistic Interpretability（4 项技能）
- **[TransformerLens](04-mechanistic-interpretability/transformer-lens/)** - Neel Nanda 开发的 mech interp 库，支持 HookPoints、激活缓存与电路分析（346 lines + 3 refs）
- **[SAELens](04-mechanistic-interpretability/saelens/)** - 稀疏自编码器训练与分析工具，用于特征发现与单义性研究（386 lines + 3 refs）
- **[pyvene](04-mechanistic-interpretability/pyvene/)** - Stanford 的因果干预库，支持声明式配置、DAS 与激活修补（473 lines + 3 refs）
- **[nnsight](04-mechanistic-interpretability/nnsight/)** - 通过 NDIF 实现远程可解释性，可在无本地 GPU 的情况下对 70B+ 模型运行实验（436 lines + 3 refs）

### 📊 Data Processing（2 项技能）
- **[Ray Data](05-data-processing/ray-data/)** - 分布式 ML 数据处理框架，支持流式执行与 GPU 加速（318 lines + 2 refs）
- **[NeMo Curator](05-data-processing/nemo-curator/)** - GPU 加速数据策展工具，去重速度提升 16×（375 lines + 2 refs）

### 🎓 Post-Training（8 项技能）
- **[TRL Fine-Tuning](06-post-training/trl-fine-tuning/)** - Transformer Reinforcement Learning（447 lines + 4 refs）
- **[GRPO-RL-Training](06-post-training/grpo-rl-training/)** (TRL) - Group Relative Policy Optimization，基于 TRL 实现（569 lines，**金标准**）
- **[OpenRLHF](06-post-training/openrlhf/)** - 完整 RLHF 流水线，集成 Ray + vLLM（241 lines + 4 refs）
- **[SimPO](06-post-training/simpo/)** - Simple Preference Optimization，无需参考模型（211 lines + 3 refs）
- **[verl](06-post-training/verl/)** - ByteDance HybridFlow RL 框架，支持 FSDP/Megatron + vLLM/SGLang 后端（389 lines + 2 refs）
- **[slime](06-post-training/slime/)** - THUDM Megatron+SGLang 框架，驱动 GLM-4.x 模型训练（464 lines + 2 refs）
- **[miles](06-post-training/miles/)** - slime 的企业级分支，支持 FP8、INT4 及 MoE 训练的 speculative RL（315 lines + 2 refs）
- **[torchforge](06-post-training/torchforge/)** - Meta PyTorch 原生 RL 框架，集成 Monarch+TorchTitan+vLLM（380 lines + 2 refs）

### 🛡️ Safety & Alignment（4 项技能）
- **[Constitutional AI](07-safety-alignment/constitutional-ai/)** - 通过原则驱动实现 AI 自我改进（282 lines）
- **[LlamaGuard](07-safety-alignment/llamaguard/)** - LLM 输入/输出的安全分类器（329 lines）
- **[NeMo Guardrails](07-safety-alignment/nemo-guardrails/)** - 基于 Colang 的可编程护栏框架（289 lines）
- **[Prompt Guard](07-safety-alignment/prompt-guard/)** - Meta 的 86M Prompt 注入与越狱检测器，TPR >99%，GPU 延迟 <2ms（313 lines）

### ⚡ Distributed Training（6 项技能）
- **[Megatron-Core](08-distributed-training/megatron-core/)** - NVIDIA 训练框架，支持 2B-462B 参数模型在 H100 上达到 47% MFU（359 lines + 4 refs）
- **[DeepSpeed](08-distributed-training/deepspeed/)** - Microsoft ZeRO 优化方案（137 lines + 9 refs）
- **[PyTorch FSDP2](08-distributed-training/pytorch-fsdp2/)** - Fully Sharded Data Parallel v2，支持 `fully_shard` 与 DTensor（231 lines + 12 refs）
- **[Accelerate](08-distributed-training/accelerate/)** - HuggingFace 的 4 行分布式训练 API（324 lines + 3 refs）
- **[PyTorch Lightning](08-distributed-training/pytorch-lightning/)** - 高级训练框架，提供 Trainer 类封装（339 lines + 3 refs）
- **[Ray Train](08-distributed-training/ray-train/)** - 多节点编排与超参数调优工具（399 lines + 1 ref）

### 🚀 Optimization（6 项技能）
- **[Flash Attention](10-optimization/flash-attention/)** - 提升 2-4× 速度的注意力机制，兼顾内存效率（359 lines + 2 refs）
- **[bitsandbytes](10-optimization/bitsandbytes/)** - 8-bit/4-bit 量化方案，减少 50-75% 显存占用（403 lines + 3 refs）
- **[GPTQ](10-optimization/gptq/)** - 4-bit 训练后量化，内存缩减 4×，精度损失 <2%（443 lines + 3 refs）
- **[AWQ](10-optimization/awq/)** - 激活感知权重量化，4-bit 下保持极低精度损失（310 lines + 2 refs）
- **[HQQ](10-optimization/hqq/)** - Half-Quadratic Quantization，无需校准数据，支持多后端（370 lines + 2 refs）
- **[GGUF](10-optimization/gguf/)** - llama.cpp 量化格式，K-quant 方法，支持 CPU/Metal 推理（380 lines + 2 refs）

### 📊 Evaluation（3 项技能）
- **[lm-evaluation-harness](11-evaluation/lm-evaluation-harness/)** - EleutherAI 标准评测框架，覆盖 60+ 任务（482 lines + 4 refs）
- **[BigCode Evaluation Harness](11-evaluation/bigcode-evaluation-harness/)** - 代码模型基准测试，支持 HumanEval、MBPP、MultiPL-E 及 pass@k 指标（406 lines + 3 refs）
- **[NeMo Evaluator](11-evaluation/nemo-evaluator/)** - NVIDIA 企业级评测平台，覆盖 18+ 框架的 100+ 基准测试，支持多后端执行（454 lines + 4 refs）

### ☁️ Infrastructure（3 项技能）
- **[Modal](09-infrastructure/modal/)** - Serverless GPU 云，Python 原生 API，按需调用 T4-H200（342 lines + 2 refs）
- **[SkyPilot](09-infrastructure/skypilot/)** - 跨 20+ 云厂商的多云编排框架，支持 Spot 实例恢复（390 lines + 2 refs）
- **[Lambda Labs](09-infrastructure/lambda-labs/)** - 预留/按需 GPU 云服务，提供 H100/A100 及持久化文件系统（390 lines + 2 refs）

### 🔥 Inference & Serving（4 项技能）
- **[vLLM](12-inference-serving/vllm/)** - 基于 PagedAttention 的高吞吐 LLM 推理服务（356 lines + 4 refs，**生产就绪**）
- **[TensorRT-LLM](12-inference-serving/tensorrt-llm/)** - NVIDIA 最快推理引擎，达 24k tok/s，支持 FP8/INT4 量化（180 lines + 3 refs）
- **[llama.cpp](12-inference-serving/llama-cpp/)** - CPU/Apple Silicon 推理框架，支持 GGUF 量化（251 lines + 3 refs）
- **[SGLang](12-inference-serving/sglang/)** - 基于 RadixAttention 的结构化生成，智能体推理提速 5-10×（435 lines + 3 refs）

### 🤖 Agents（4 项技能）
- **[LangChain](14-agents/langchain/)** - 最流行的智能体框架，支持 500+ 集成与 ReAct 模式（658 lines + 3 refs，**生产就绪**）
- **[LlamaIndex](14-agents/llamaindex/)** - LLM 应用数据框架，提供 300+ 连接器，专注 RAG（535 lines + 3 refs）
- **[CrewAI](14-agents/crewai/)** - 多智能体编排平台，支持角色协作与自主工作流（498 lines + 3 refs）
- **[AutoGPT](14-agents/autogpt/)** - 自主 AI 智能体平台，提供可视化工作流构建器与持续执行能力（400 lines + 2 refs）

### 🔍 RAG（5 项技能）
- **[Chroma](15-rag/chroma/)** - 开源嵌入数据库，支持本地/云端部署，24k stars（385 lines + 1 ref）
- **[FAISS](15-rag/faiss/)** - Facebook 相似度搜索框架，支持十亿级数据与 GPU 加速（295 lines）
- **[Sentence Transformers](15-rag/sentence-transformers/)** - 5000+ 嵌入模型库，多语言支持，15k stars（370 lines）
- **[Pinecone](15-rag/pinecone/)** - 托管向量数据库，自动扩缩容，延迟 <100ms（410 lines）
- **[Qdrant](15-rag/qdrant/)** - 高性能 Rust 向量搜索引擎，支持混合搜索与过滤（493 lines + 2 refs）

### 🎨 Multimodal（7 项技能）
- **[CLIP](18-multimodal/clip/)** - OpenAI 视觉语言模型，支持零样本分类，25k stars（320 lines）
- **[Whisper](18-multimodal/whisper/)** - 鲁棒语音识别模型，覆盖 99 种语言，73k stars（395 lines）
- **[LLaVA](18-multimodal/llava/)** - 视觉语言助手，支持图像对话，性能对标 GPT-4V（360 lines）
- **[Stable Diffusion](18-multimodal/stable-diffusion/)** - 基于 HuggingFace Diffusers 的文生图框架，支持 SDXL、ControlNet（380 lines + 2 refs）
- **[Segment Anything](18-multimodal/segment-anything/)** - Meta SAM 模型，支持点/框提示的零样本图像分割（500 lines + 2 refs）
- **[BLIP-2](18-multimodal/blip-2/)** - 基于 Q-Former 的视觉语言预训练框架，支持图像描述与 VQA（500 lines + 2 refs）
- **[AudioCraft](18-multimodal/audiocraft/)** - Meta MusicGen/AudioGen 工具包，支持文生音乐与文生声音（470 lines + 2 refs）

### 🎯 Prompt Engineering（4 项技能）
- **[DSPy](16-prompt-engineering/dspy/)** - 声明式提示编程框架，内置优化器，Stanford NLP 出品，22k stars（438 lines + 3 refs）
- **[Instructor](16-prompt-engineering/instructor/)** - 结构化 LLM 输出生成，支持 Pydantic 验证，15k stars（726 lines + 3 refs）
- **[Guidance](16-prompt-engineering/guidance/)** - 基于正则表达式/语法的约束生成框架，Microsoft Research 出品，18k stars（485 lines + 3 refs）
- **[Outlines](16-prompt-engineering/outlines/)** - 基于 FSM 的结构化文本生成，零开销，8k stars（601 lines + 3 refs）

### 📊 MLOps（3 项技能）
- **[Weights & Biases](13-mlops/weights-and-biases/)** - 实验追踪、超参扫描、Artifact 管理与模型注册表（427 lines + 3 refs）
- **[MLflow](13-mlops/mlflow/)** - 模型注册、实验追踪、部署与自动日志记录（514 lines + 3 refs）
- **[TensorBoard](13-mlops/tensorboard/)** - 可视化分析、性能剖析、Embeddings 与标量/图像监控（538 lines + 3 refs）

### 👁️ Observability（2 项技能）
- **[LangSmith](17-observability/langsmith/)** - LLM 可观测性平台，支持追踪、评估与 AI 应用监控（422 lines + 2 refs）
- **[Phoenix](17-observability/phoenix/)** - 开源 AI 可观测性工具，集成 OpenTelemetry 追踪与 LLM 评测（380 lines + 2 refs）

### 🔬 Emerging Techniques（6 项技能）
- **[MoE Training](19-emerging-techniques/moe-training/)** - MoE 训练框架，集成 DeepSpeed、Mixtral 8x7B，成本降低 5×（515 lines + 3 refs）
- **[Model Merging](19-emerging-techniques/model-merging/)** - 使用 TIES、DARE、SLERP 等算法合并模型，基于 mergekit（528 lines + 3 refs）
- **[Long Context](19-emerging-techniques/long-context/)** - 扩展上下文窗口技术，支持 RoPE、YaRN、ALiBi，覆盖 32k-128k tokens（624 lines + 3 refs）
- **[Speculative Decoding](19-emerging-techniques/speculative-decoding/)** - 基于 Medusa/Lookahead 的推理加速技术，提速 1.5-3.6×（379 lines）
- **[Knowledge Distillation](19-emerging-techniques/knowledge-distillation/)** - 模型压缩方案，支持 70B→7B 蒸馏，结合 MiniLLM 与温度缩放（424 lines）
- **[Model Pruning](19-emerging-techniques/model-pruning/)** - 稀疏化剪枝技术，基于 Wanda/SparseGPT，精度损失 <1%（417 lines）

### 📝 ML Paper Writing（2 项技能）
- **[ML Paper Writing](20-ml-paper-writing/)** - 撰写符合 NeurIPS、ICML、ICLR、ACL、AAAI、COLM 等顶会标准的论文，内置 LaTeX 模板、引用验证与写作规范（532 lines + 5 refs）
- **[Academic Plotting](20-ml-paper-writing/academic-plotting/)** - 生成出版级 ML 图表：通过 Gemini AI 绘制架构图，结合 matplotlib/seaborn 生成数据驱动图表及特定期会排版风格（479 lines + 3 refs）

### 💡 Ideation（2 项技能）
- **[Research Brainstorming](21-research-ideation/brainstorming-research-ideas/)** - 结构化构思框架，结合 10 种互补视角发掘高影响力研究方向（384 lines）
- **[Creative Thinking](21-research-ideation/creative-thinking-for-research/)** - 认知科学框架（双关联、结构映射、约束操控），激发真正新颖的研究思路（366 lines）

### 🧬 Agent-Native Research Artifact（3 项技能）
- **[ARA Compiler](22-agent-native-research-artifact/compiler/)** - 将任意研究输入（PDF 论文、仓库、实验日志、原始笔记）编译为完整的 Agent-Native Research Artifact，包含主张、探索图、证据与代码存根（245 lines + 3 refs）
- **[ARA Research Manager](22-agent-native-research-artifact/research-manager/)** - 会话结束时的后置记录工具，从对话历史中提取决策、实验、死胡同与转向点，写入 `ara/` 目录并标记 user-vs-AI 溯源标签（324 lines + 3 refs）
- **[ARA Rigor Reviewer](22-agent-native-research-artifact/rigor-reviewer/)** - ARA Seal Level 2 语义认识论评审，对证据相关性、可证伪性、范围校准、逻辑连贯性、探索完整性与方法严谨性六个维度进行评分，输出严重性排序的审查报告（322 lines + 1 ref）

</details>

## 演示示例

本仓库中的全部技能将自动同步至 [Orchestra Research](https://www.orchestra-research.com/research-skills)，你可一键将其添加至项目中，并与 AI 研究智能体配合使用。

**查看技能实际运行效果 → [demos/](demos/README.md)**

我们维护了一份精选的演示仓库合集，展示如何利用这些技能开展真实的 AI 研究任务：

| Demo | Skills Used | What It Does |
|------|-------------|--------------|
| **[Norm Heterogeneity → LoRA Brittleness](demos/autoresearch-norm-heterogeneity/)** | Autoresearch, ML Paper Writing, Ideation | 智能体自主发现规范异质性可预测微调难度（r=-0.99），从 ETF 重叠的零结果转向新结论 |
| **[RL Algorithm Brain Scan](demos/autoresearch-rl-brain-scan/)** | Autoresearch, GRPO, TRL, SAELens, TransformerLens, ML Paper Writing | 智能体发现 DPO 本质上是秩-1 扰动（从单一 SVD 方向恢复率达 95.6%），而在线 RL 呈分布式且保持结构特性 |
| **[NeMo Eval: GPQA Benchmark](https://github.com/zechenzhangAGI/Nemo-Eval-Skill-Demo)** | NeMo Evaluator | 在研究生级科学问题上对比 Llama 8B/70B/405B 的表现 |
| **[LoRA Without Regret Reproduction](https://www.orchestra-research.com/perspectives/LLM-with-Orchestra)** | GRPO, TRL | 通过提示工程复现 SFT + GRPO RL 实验 |
| **[Layer-Wise Quantization Experiment](https://github.com/AmberLJC/llama-quantization-experiment)** | llama.cpp, GGUF | 探究最优层精度分配——早期层采用 Q8 可实现 1.9× 压缩且困惑度损失仅 1.3% |
| **[Cross-Lingual Alignment Analysis](https://github.com/AmberLJC/faiss-demo)** | FAISS | 利用 FAISS 相似度搜索量化多语言嵌入在 8 种语言间对齐语义概念的效果 |
| **[Scientific Plotting Demo](demos/scientific-plotting-demo/)** | Academic Plotting | 为 Andes QoE-aware LLM 推理服务论文生成出版级图表——Gemini AI 架构图 + matplotlib 数据图（CDF、多面板网格、柱状图） |

**重点推荐演示**：两项完全由 AI 智能体使用 **autoresearch**（自动研究）技能生成的论文。[Norm Heterogeneity paper](demos/autoresearch-norm-heterogeneity/) 展示了自主研究工作流中的假设反转——智能体推翻了自身初始假设并发现了更强的结论。[RL Brain Scan paper](demos/autoresearch-rl-brain-scan/) 展示了多技能编排能力——智能体训练了 RL 模型，利用可解释性工具分析内部机制，并综合得出“DPO 是秩-1 对齐”的洞察。两篇论文均由该智能体从头至尾独立撰写。

## 技能结构

每项技能均采用经过实战检验的结构，以提供最大实用性：

```
skill-name/
├── SKILL.md                    # Quick reference (50-150 lines)
│   ├── Metadata (name, description, version)
│   ├── When to use this skill
│   ├── Quick patterns & examples
│   └── Links to references
│
├── references/                 # Deep documentation (300KB+)
│   ├── README.md              # From GitHub/official docs
│   ├── api.md                 # API reference
│   ├── tutorials.md           # Step-by-step guides
│   ├── issues.md              # Real GitHub issues & solutions
│   ├── releases.md            # Version history & breaking changes
│   └── file_structure.md      # Codebase navigation
│
├── scripts/                    # Helper scripts (optional)
└── assets/                     # Templates & examples (optional)
```

<details>
<summary><b>质量标准</b></summary>

- **官方来源文档**：超过 300KB
- **真实 GitHub Issue 与解决方案**（如有）
- **带语言检测的代码示例**
- **版本历史与破坏性更新说明**
- **官方文档链接**

</details>

## 路线图

我们正在构建覆盖 AI 研究全生命周期的 80 项综合技能。完整开发计划请参见我们的[详细路线图](docs/ROADMAP.md)。

[查看完整路线图 →](docs/ROADMAP.md)

<details>
<summary><b>查看详细统计数据</b></summary>

| Metric | Current | Target |
|--------|---------|--------|
| **Skills** | **87** (high-quality, standardized YAML) | 80 ✅ |
| **Avg Lines/Skill** | **420 lines** (focused + progressive disclosure) | 200-600 lines |
| **Documentation** | **~130,000 lines** total (SKILL.md + references) | 100,000+ lines |
| **Gold Standard Skills** | **65** with comprehensive references | 50+ |
| **Contributors** | 1 | 100+ |
| **Coverage** | Architecture, Tokenization, Fine-Tuning, Mechanistic Interpretability, Data Processing, Post-Training, Safety, Distributed, Optimization, Evaluation, Infrastructure, Inference, Agents, RAG, Multimodal, Prompt Engineering, MLOps, Observability, ML Paper Writing, Ideation, Autoresearch | Full Lifecycle ✅ |

**近期进展**：npm 包 `@orchestra-research/ai-research-skills`，支持一键安装至所有编程智能体

**理念**：质量 > 数量。遵循 [Anthropic 官方最佳实践](anthropic_official_docs/best_practices.md)——每项技能提供 200-500 行聚焦且可操作的指导内容，采用渐进式披露策略。

</details>



## 仓库结构

```
claude-ai-research-skills/
├── README.md                    ← You are here
├── CONTRIBUTING.md              ← Contribution guide
├── demos/                       ← Curated demo gallery (links to demo repos)
├── docs/
├── 0-autoresearch-skill/        (1 skill ✓ - Autonomous research orchestration)
├── 01-model-architecture/       (5 skills ✓ - LitGPT, Mamba, RWKV, NanoGPT, TorchTitan)
├── 02-tokenization/             (2 skills ✓ - HuggingFace Tokenizers, SentencePiece)
├── 03-fine-tuning/              (4 skills ✓ - Axolotl, LLaMA-Factory, Unsloth, PEFT)
├── 04-mechanistic-interpretability/ (4 skills ✓ - TransformerLens, SAELens, pyvene, nnsight)
├── 05-data-processing/          (2 skills ✓ - Ray Data, NeMo Curator)
├── 06-post-training/            (8 skills ✓ - TRL, GRPO, OpenRLHF, SimPO, verl, slime, miles, torchforge)
├── 07-safety-alignment/         (4 skills ✓ - Constitutional AI, LlamaGuard, NeMo Guardrails, Prompt Guard)
├── 08-distributed-training/     (6 skills ✓ - Megatron-Core, DeepSpeed, FSDP, Accelerate, Lightning, Ray Train)
├── 09-infrastructure/           (3 skills ✓ - Modal, SkyPilot, Lambda Labs)
├── 10-optimization/             (6 skills ✓ - Flash Attention, bitsandbytes, GPTQ, AWQ, HQQ, GGUF)
├── 11-evaluation/               (3 skills ✓ - lm-evaluation-harness, BigCode, NeMo Evaluator)
├── 12-inference-serving/        (4 skills ✓ - vLLM, TensorRT-LLM, llama.cpp, SGLang)
├── 13-mlops/                    (3 skills ✓ - Weights & Biases, MLflow, TensorBoard)
├── 14-agents/                   (4 skills ✓ - LangChain, LlamaIndex, CrewAI, AutoGPT)
├── 15-rag/                      (5 skills ✓ - Chroma, FAISS, Sentence Transformers, Pinecone, Qdrant)
├── 16-prompt-engineering/       (4 skills ✓ - DSPy, Instructor, Guidance, Outlines)
├── 17-observability/            (2 skills ✓ - LangSmith, Phoenix)
├── 18-multimodal/               (7 skills ✓ - CLIP, Whisper, LLaVA, Stable Diffusion, SAM, BLIP-2, AudioCraft)
├── 19-emerging-techniques/      (6 skills ✓ - MoE, Model Merging, Long Context, Speculative Decoding, Distillation, Pruning)
├── 20-ml-paper-writing/         (2 skills ✓ - ML Paper Writing with LaTeX templates, Academic Plotting)
├── 21-research-ideation/           (2 skills ✓ - Research Brainstorming, Creative Thinking)
├── 22-agent-native-research-artifact/ (3 skills ✓ - ARA Compiler, Research Manager, Rigor Reviewer)
└── packages/ai-research-skills/ (npm package for one-command installation)
```

## 使用场景

### For Researchers
"I need to fine-tune Llama 3 with custom data"
→ **03-fine-tuning/axolotl/** - YAML configs, 100+ model support

### For ML Engineers
"How do I optimize inference latency?"
→ **12-inference-serving/vllm/** - PagedAttention, batching

### For Students
"I want to learn how transformers work"
→ **01-model-architecture/litgpt/** - Clean implementations

### For Teams
"We need to scale training to 100 GPUs"
→ **08-distributed-training/deepspeed/** - ZeRO stages, 3D parallelism

## License

MIT License - See [LICENSE](LICENSE) for details.

**Note**: Individual skills may reference libraries with different licenses. Please check each project's license before use.

## Citation

If you use AI Research Skills in your work or find it helpful for a publication, we'd appreciate a citation:

**BibTeX**
```bibtex
@software{ai_research_skills,
  title     = {AI Research Skills Library},
  author    = {{Orchestra Research}},
  year      = {2025},
  url       = {https://github.com/orchestra-research/AI-research-SKILLs},
  note      = {Open-source skills library enabling AI agents to autonomously conduct AI research}
}
```

**APA**
> Orchestra Research. (2025). *AI Research Skills Library* [Computer software]. https://github.com/orchestra-research/AI-research-SKILLs

**Chicago**
> Orchestra Research. "AI Research Skills Library." GitHub, 2025. https://github.com/orchestra-research/AI-research-SKILLs.

**IEEE**
> Orchestra Research, "AI Research Skills Library," 2025. [Online]. Available: https://github.com/orchestra-research/AI-research-SKILLs

> **Tip**: You can also click **"Cite this repository"** in the GitHub sidebar for auto-formatted citations.

## Acknowledgments

Built with:
- **[Claude Code](https://www.claude.com/product/claude-code)** - AI pair programming
- **[Skill Seeker](https://github.com/yusufkaraaslan/Skill_Seekers)** - Automated doc scraping
- **Open Source AI Community** - For amazing tools and docs

Special thanks to:
- EleutherAI, HuggingFace, NVIDIA, Lightning AI, Meta AI, Anthropic
- All researchers who maintain excellent documentation
 
## Contributors

Thanks to all the people who have contributed to the AI Research Skills Library:

<a href="https://github.com/orchestra-research/AI-research-SKILLs/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=orchestra-research/AI-research-SKILLs" />
</a> 

We welcome contributions from the AI research community! See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines on:

- Adding new skills
- Improving existing skills
- Quality standards and best practices
- Submission process

## Recent Updates

<details open>
<summary><b>April 2026 - v1.6.0 🧬 Agent-Native Research Artifact (ARA) — 23rd Category, 98 Skills</b></summary>

- 🧬 **NEW CATEGORY**: `22-agent-native-research-artifact/`（第 23 个分类）——三项将研究成果转化为可证伪、智能体可遍历工件的技能：
  - 🛠️ **[ARA Compiler](22-agent-native-research-artifact/compiler/)** — 编译任意输入（PDF 论文、GitHub 仓库、实验日志、原始笔记）为结构化 ARA，包含认知层（主张、概念、启发式规则）、物理层（配置、代码存根）、探索图（研究 DAG）与实证证据
  - 📋 **[ARA Research Manager](22-agent-native-research-artifact/research-manager/)** — 会话结束时的后置记录模块，扫描对话历史并将决策、实验、死胡同、主张、启发式规则与转向点写入 `ara/` 目录，附带 `user` / `ai-suggested` / `ai-executed` / `user-revised` 溯源标签
  - 🔍 **[ARA Rigor Reviewer](22-agent-native-research-artifact/rigor-reviewer/)** — Seal Level 2 语义认识论评审，对证据相关性、可证伪性、范围校准、逻辑连贯性、探索完整性与方法严谨性六个维度进行评分，输出严重性排序报告及 Strong Accept-to-Reject 建议
- 🔗 源自 [Agent-Native-Research-Artifact-Init](https://github.com/Orchestra-Research/Agent-Native-Research-Artifact-Init) 参考仓库，已按 AI-research-SKILLs 标准重构（kebab-case 命名、第三人称描述、Title-Case 标签、一级深度 references）
- 🧩 `.claude-plugin/marketplace.json` 新增 `agent-native-research-artifact` 插件入口；CLI 分类注册为 `22-agent-native-research-artifact`，npm 安装程序包含三个独立技能条目
- 🔄 通过 `sync-skills.yml` 在 push 时自动同步至 Orchestra 市场；版本更新后通过 `publish-npm.yml` 重新发布 npm 包 `@orchestra-research/ai-research-skills@1.6.0`
- 📊 **总计 98 项技能**，覆盖 **23 个分类**——完整生命周期：构思 → 论文 → 可证伪、可审计工件

</details>

<details>
<summary><b>March 2026 - v1.4.0 🔬 Autoresearch & 86 Skills — Full Research Lifecycle</b></summary>

- 🔬 **NEW SKILL**: **Autoresearch**（自动研究）——使用双循环架构（内层优化循环 + 外层综合循环）实现自主研究编排
- 🧠 管理全生命周期：文献调研 → 构思生成 → 实验执行 → 综合总结 → 论文撰写
- 🔄 自动路由至全部 86 项领域技能——智能体无需手动选择具体技能
- ⏰ 强制使用 `/loop`（Claude Code）与 cron job（OpenClaw）以实现持续自主运行
- 📊 生成包含优化轨迹图的 HTML/PDF 研究报告供人类审阅
- 📝 `Findings.md` 作为跨会话的持久化项目记忆，跟踪“经验教训与约束条件”
- 🗂️ 结构化工作区：research-state.yaml、findings.md、research-log.md、literature/、experiments/、src/、data/、to_human/
- 📄 **两项由 autoresearch 生成的演示论文**：[Norm Heterogeneity → LoRA Brittleness](demos/autoresearch-norm-heterogeneity/) 与 [RL Algorithm Brain Scan](demos/autoresearch-rl-brain-scan/)
- 🚀 WELCOME.md 用于冷启动智能体引导——一个 URL 即可从零进入自主研究状态
- 📦 npm v1.4.x 支持 Windows 软链接回退，全部 22 个分类均可安装
- 🤖 **支持的智能体**：Claude Code、Hermes Agent、OpenCode、OpenClaw、Cursor、Codex、Gemini CLI、Qwen Code
- 📊 **总计 87 项技能**，覆盖 **22 个分类**——完整研究生命周期

</details>

<details>
<summary><b>February 2026 - v0.15.0 🛡️ Prompt Guard & 83 Skills</b></summary>

- 🛡️ **NEW SKILL**: Prompt Guard —— Meta 的 86M Prompt 注入与越狱检测器
- ⚡ TPR >99%，FPR <1%，GPU 延迟 <2ms，支持多语言（8 种）
- 🔒 3 个工作流：用户输入过滤、第三方数据过滤、批量 RAG 处理
- 📊 **总计 83 项技能**，覆盖 20 个分类

</details>

<details>
<summary><b>January 2026 - v0.14.0 📦 npm Package & 82 Skills</b></summary>

- 📦 **NEW**: `npx @orchestra-research/ai-research-skills` ——一键安装至所有编程智能体
- 🤖 **支持的智能体**：Claude Code、OpenCode、Cursor、Codex、Gemini CLI、Qwen Code
- ✨ 交互式安装程序，支持按分类或单个技能选择
- 🔄 更新已安装技能，支持选择性卸载
- 📊 **总计 82 项技能**（新增 5 项 post-training 技能：verl, slime, miles, torchforge + TorchTitan）
- 🏗️ Megatron-Core 移至 Distributed Training 分类

</details>

<details>
<summary><b>January 2026 - v0.13.0 📝 ML Paper Writing & Demos Gallery</b></summary>

- 📝 **NEW CATEGORY**: ML Paper Writing（第 20 个分类，第 77 项技能）
- 🎯 撰写符合 NeurIPS、ICML、ICLR、ACL、AAAI、COLM 等顶会标准的论文
- 📚 汇聚顶尖研究者写作理念（Neel Nanda, Farquhar, Gopen & Swan, Lipton, Perez）
- 🔬 引用验证工作流——杜绝幻觉引用
- 📄 6 大顶级会议 LaTeX 模板
- 🎪 **NEW**: 精选演示画廊 (`demos/`)，展示技能的实际应用效果
- 🔗 演示仓库：NeMo Evaluator 基准测试、LoRA Without Regret 复现项目
- 📖 936 行综合 SKILL.md，包含 4 个工作流

</details>

<details>
<summary><b>January 2026 - v0.12.0 📊 NeMo Evaluator SDK</b></summary>

- 📊 **NEW SKILL**: NeMo Evaluator SDK ——企业级 LLM 基准测试工具
- 🔧 NVIDIA 评测平台，覆盖 18+ 框架的 100+ 基准（MMLU, HumanEval, GSM8K, safety, VLM）
- ⚡ 多后端执行：本地 Docker、Slurm HPC、Lepton cloud
- 📦 容器优先架构，确保评测可复现性
- 📝 454 行 SKILL.md + 4 份综合参考文件（约 ~48KB 文档）

</details>

<details>
<summary><b>December 2025 - v0.11.0 🔬 Mechanistic Interpretability</b></summary>

- 🔬 **NEW CATEGORY**: Mechanistic Interpretability（4 项技能）
- 🔍 TransformerLens：Neel Nanda 的 mech interp 库，支持 HookPoints、激活缓存与电路分析
- 🧠 SAELens：稀疏自编码器训练与分析工具，用于特征发现与单义性研究
- ⚡ pyvene：Stanford 因果干预库，支持声明式配置、DAS 与激活修补
- 🌐 nnsight：通过 NDIF 实现远程可解释性，无需本地 GPU 即可对 70B+ 模型运行实验
- 📝 新增 ~6,500 行文档，覆盖 16 个文件
- **总计 76 项技能**（填补了缺失的 04 分类位置）

</details>

<details>
<summary><b>November 25, 2025 - v0.10.0 🎉 70 Skills Complete!</b></summary>

- 🎉 **ROADMAP COMPLETE**: 达成 70 项技能里程碑！
- 🚀 新增 4 项技能：Lambda Labs、Segment Anything (SAM)、BLIP-2、AudioCraft
- ☁️ Lambda Labs：预留/按需 GPU 云服务，支持 H100/A100、持久化文件系统与 1-Click Clusters
- 🖼️ SAM：Meta Segment Anything，支持点/框/掩码提示的零样本图像分割
- 👁️ BLIP-2：基于 Q-Former 的视觉语言预训练框架，支持图像描述与 VQA
- 🎵 AudioCraft：Meta MusicGen/AudioGen 工具包，支持文生音乐与文生声音生成
- 📝 新增 ~10,000 行文档，覆盖 12 个文件
- **总计 70 项技能**（路线图完成率 100%！）

</details>

<details>
<summary><b>November 25, 2025 - v0.9.0</b></summary>

- 🚀 新增 2 项基础设施技能：Modal、SkyPilot
- ☁️ Modal：Serverless GPU 云，Python 原生 API，按需调用 T4-H200，支持自动扩缩容
- 🌐 SkyPilot：跨 20+ 云厂商的多云编排框架，支持 Spot 实例恢复
- ✨ 新增 Infrastructure 分类（2 项技能——Serverless GPU 与多云编排）
- 📝 新增 ~2,500 行文档，覆盖 6 个文件
- **总计 66 项技能**（距 70 项目标完成度达 94%）

</details>

<details>
<summary><b>November 25, 2025 - v0.8.0</b></summary>

- 🚀 新增 5 项高优先级技能：HQQ、GGUF、Phoenix、AutoGPT、Stable Diffusion
- ⚡ HQQ：Half-Quadratic Quantization，无需校准数据，支持多后端
- 📦 GGUF：llama.cpp 量化格式，K-quant 方法，支持 CPU/Metal 推理
- 👁️ Phoenix：开源 AI 可观测性工具，集成 OpenTelemetry 追踪与 LLM 评测
- 🤖 AutoGPT：自主 AI 智能体平台，提供可视化工作流构建器
- 🎨 Stable Diffusion：基于 Diffusers 的文生图框架，支持 SDXL、ControlNet、LoRA
- 📝 新增 ~9,000 行文档，覆盖 15 个文件
- **总计 64 项技能**（距 70 项目标完成度达 91%）

</details>

<details>
<summary><b>November 25, 2025 - v0.7.0</b></summary>

- 🚀 新增 5 项高优先级技能：PEFT、CrewAI、Qdrant、AWQ、LangSmith
- ✨ 新增 Observability 分类，集成 LangSmith 用于 LLM 追踪与评测
- 🎯 PEFT：参数高效微调，支持 LoRA、QLoRA、DoRA 等 25+ 种方法
- 🤖 CrewAI：多智能体编排框架，支持角色协作
- 🔍 Qdrant：高性能 Rust 向量搜索引擎，支持混合过滤查询
- ⚡ AWQ：激活感知 4-bit 量化，精度损失极低
- 📝 新增 ~8,000 行文档，覆盖 15 个文件
- **总计 59 项技能**（距 70 项目标完成度达 84%）

</details>

<details>
<summary><b>November 15, 2025 - v0.6.0</b></summary>

- 📊 新增 3 项综合 MLOps 技能：Weights & Biases、MLflow、TensorBoard
- ✨ 新增 MLOps 分类（3 项技能——实验追踪、模型注册表、可视化）
- 📝 新增 ~10,000 行文档，覆盖 13 个文件
- 🔧 全面覆盖：实验追踪、超参扫描、模型注册表、性能剖析、Embeddings 可视化
- **总计 54 项技能**（距 70 项目标完成度达 77%）

</details>

<details>
<summary><b>November 12, 2025 - v0.5.0</b></summary>

- 🎯 新增 4 项综合 Prompt Engineering 技能：DSPy、Instructor、Guidance、Outlines
- ✨ 新增 Prompt Engineering 分类（4 项技能）
- 📝 新增 ~10,000 行文档，覆盖 16 个文件
- 🔧 全面覆盖：声明式编程、结构化输出、约束生成、基于 FSM 的文本生成
- **总计 47 项技能**（距 70 项目标完成度达 67%）

</details>

<details>
<summary><b>November 9, 2025 - v0.4.0</b></summary>

- 🤖 新增 11 项综合技能：LangChain、LlamaIndex、Chroma、FAISS、Sentence Transformers、Pinecone、CLIP、Whisper、LLaVA
- ✨ 新增 Agents 分类（2 项技能）
- 🔍 新增 RAG 分类（4 项技能）
- 🎨 新增 Multimodal 分类（3 项技能）
- 📝 新增 ~15,000 行文档
- **总计 43 项技能**（距 70 项目标完成度达 61%）

</details>

<details>
<summary><b>November 8, 2025 - v0.3.0</b></summary>

- 🚀 新增 8 项综合技能：TensorRT-LLM、llama.cpp、SGLang、GPTQ、HuggingFace Tokenizers、SentencePiece、Ray Data、NeMo Curator
- ⚡ 完成 Inference & Serving 分类（4/4 项技能）
- 🔤 新增 Tokenization 分类（2 项技能）
- 📊 新增 Data Processing 分类（2 项技能）
- 📝 新增 9,617 行文档，覆盖 30 个文件
- **总计 32 项技能**（距 70 项目标完成度达 45%）

</details>

<details>
<summary><b>November 6, 2025 - v0.2.0</b></summary>

- 从 GitHub 新增 10 项技能（Megatron-Core、Lightning、Ray Train 等）
- 完善技能结构，增加综合参考文档
- 制定战略路线图至 70 项目标
- 新增贡献指南

</details>

<details>
<summary><b>November 3, 2025 - v0.1.0</b></summary>

- 🎉 初始版本发布，包含 5 项微调技能

</details>

## Community

Join our community to stay updated, ask questions, and connect with other AI researchers:

- **[SkillEvolve Meta-Skill](https://github.com/Skill-Evolve/meta-skill)** - Connect your agent to the collective intelligence of the community. Captures techniques discovered during sessions and shares them back as curated skills.
- **[Slack Community](https://join.slack.com/t/orchestrarese-efu1990/shared_invite/zt-3iu6gr8io-zJvpkZTPToEviQ9KFZvNSg)** - Chat with the team and other users
- **[Twitter/X](https://x.com/orch_research)** - Follow for updates and announcements
- **[LinkedIn](https://www.linkedin.com/company/orchestra-research/)** - Connect professionally

## Star History

<a href="https://star-history.com/#orchestra-research/AI-research-SKILLs&Date">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=orchestra-research/AI-research-SKILLs&type=Date&theme=dark" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/svg?repos=orchestra-research/AI-research-SKILLs&type=Date" />
   <img alt="Star History Chart" src="https://api.star-history.com/svg?repos=orchestra-research/AI-research-SKILLs&type=Date" />
 </picture>
</a>
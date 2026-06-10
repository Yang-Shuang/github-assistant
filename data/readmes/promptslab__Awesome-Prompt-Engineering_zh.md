<h2 align="center">Awesome Prompt Engineering 🧙‍♂️</h2>

<p align="center">
  <img width="650" src="https://raw.githubusercontent.com/promptslab/Awesome-Prompt-Engineering/main/_source/prompt.png">
</p>

<p align="center">
  精心策划的提示词工程（Prompt Engineering）与上下文工程资源合集——涵盖与大语言模型协作相关的论文、工具、模型、API、基准测试、课程和社区。
</p>

<p align="center">
https://promptslab.github.io
  </p>
 <h4 align="center">
  
  ```
     Master Prompt Engineering. Join the Course at https://promptslab.github.io
  ```
  <a href="https://awesome.re"><img src="https://awesome.re/badge.svg" alt="Awesome" /></a>
  <a href="https://github.com/promptslab/Awesome-Prompt-Engineering/blob/main/LICENSE"><img src="https://img.shields.io/badge/License-Apache_2.0-blue.svg" alt="License" /></a>
  <a href="http://makeapullrequest.com"><img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square" alt="PRs Welcome" /></a>
  <a href="https://discord.gg/m88xfYMbK6"><img src="https://img.shields.io/badge/Discord-Community-orange" alt="Community" /></a>
  <img src="https://img.shields.io/badge/Last%20Updated-February%202026-brightgreen" alt="Last Updated" />
</p>

---

## 🚀 从这里开始

刚接触提示词工程？请遵循以下学习路径：

<p align="center">
  <img width="1000" src="https://raw.githubusercontent.com/promptslab/Awesome-Prompt-Engineering/refs/heads/main/_source/main.jpg">
</p>

1. **学习基础** → [面向开发者的 ChatGPT 提示词工程](https://www.deeplearning.ai/short-courses/chatgpt-prompt-engineering-for-developers/)（免费，约 90 分钟）
2. **阅读指南** → [DAIR.AI 提示词工程指南](https://www.promptingguide.ai/)（开源、全面）
3. **研读官方文档** → [OpenAI 提示词工程指南](https://platform.openai.com/docs/guides/prompt-engineering) · [Anthropic 提示词工程指南](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview)
4. **了解领域发展方向** → [Anthropic：AI Agent 的高效上下文工程](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
5. **阅读前沿研究** → [提示词报告（The Prompt Report）](https://arxiv.org/abs/2406.06608) —— 基于 1,500+ 篇论文整理的 58+ 种提示技巧分类体系

---

## 目录

- [论文](#papers)
  - [主要综述](#major-surveys)
  - [提示词优化与自动提示](#prompt-optimization-and-automatic-prompting)
  - [提示词压缩](#prompt-compression)
  - [推理能力进展](#reasoning-advances)
  - [上下文中学习（In-Context Learning）](#in-context-learning)
  - [Agent 提示与多 Agent 系统](#agentic-prompting-and-multi-agent-systems)
  - [多模态提示词工程](#multimodal-prompting)
  - [结构化输出与格式控制](#structured-output-and-format-control)
  - [提示词注入与安全](#prompt-injection-and-security)
  - [提示词工程应用](#applications-of-prompt-engineering)
  - [文生图生成](#text-to-image-generation)
  - [文生音乐/音频生成](#text-to-musicaudio-generation)
  - [奠基性论文（2024年之前）](#foundational-papers-pre-2024)
- [工具与代码](#tools-and-code)
  - [提示词管理与测试](#prompt-management-and-testing)
  - [大语言模型评估工具](#llm-evaluation-tools)
  - [Agent 框架](#agent-frameworks)
  - [提示词优化工具](#prompt-optimization-tools)
  - [红队测试与提示词安全](#red-teaming-and-prompt-security)
  - [MCP（模型上下文协议）](#mcp-model-context-protocol)
  - [Vibe Coding 与 AI 编程助手](#vibe-coding-and-ai-coding-assistants)
    - [基于 CLI 的编程 Agent](#cli-based-coding-agents)
    - [AI 代码编辑器 / IDE](#ai-code-editors--ides)
    - [IDE 扩展/插件](#ide-extensions--plugins)
    - [AI 编程平台/云端 Agent](#ai-coding-platforms--cloud-agents)
    - [开源编程 Agent 框架](#open-source-coding-agent-frameworks)
  - [其他值得关注的仓库](#other-notable-repositories)
- [API](#apis)
- [数据集与基准测试](#datasets-and-benchmarks)
- [模型](#models)
- [AI 内容检测器](#ai-content-detectors)
- [书籍](#books)
- [课程](#courses)
- [教程与指南](#tutorials-and-guides)
- [视频](#videos)
- [社区](#communities)
- [自主研究与自进化 Agent](#autonomous-research--self-improving-agents)
- [如何贡献](#how-to-contribute)

---

## 论文
📄

### 主要综述

- [The Prompt Report: A Systematic Survey of Prompting Techniques](https://arxiv.org/abs/2406.06608) [2024] — 最全面的综述：基于 1,500+ 篇论文，对 58 种文本提示和 40 种多模态提示技术进行分类。由 OpenAI、微软、Google、斯坦福等联合撰写。
- [A Systematic Survey of Prompt Engineering in Large Language Models: Techniques and Applications](https://arxiv.org/abs/2402.07927) [2024] — 涵盖应用领域的 44 种技术，并提供各任务的性能总结。
- [A Survey of Prompt Engineering Methods in LLMs for Different NLP Tasks](https://arxiv.org/abs/2407.12994) [2024] — 覆盖 29 个 NLP 任务的 39 种提示方法。
- [A Survey of Automatic Prompt Engineering: An Optimization Perspective](https://arxiv.org/abs/2502.11560) [2025] — 将自动 PE 方法形式化为离散/连续/混合优化问题。
- [Efficient Prompting Methods for Large Language Models: A Survey](https://arxiv.org/abs/2404.01077) [2024] — 面向效率的提示词工程综述（压缩、优化、APE），旨在降低计算量与延迟。
- [Navigate through Enigmatic Labyrinth: A Survey of Chain of Thought Reasoning](https://arxiv.org/abs/2309.15402) [2023, ACL 2024] — 思维链（CoT）的系统性综述。
- [Demystifying Chains, Trees, and Graphs of Thoughts](https://arxiv.org/abs/2401.14295) [2024] — 多提示词推理拓扑的统一框架。
- [Towards Goal-oriented Prompt Engineering for Large Language Models: A Survey](https://arxiv.org/abs/2401.14043) [2024] — 聚焦围绕明确任务目标设计的提示词。
- [Towards Reasoning Era: A Survey of Long Chain-of-Thought for Reasoning LLMs](https://arxiv.org/abs/2503.09567) [2025] — 区分 o1/R1 时代模型中的长思维链与短思维链。

### 提示词优化与自动提示

- [OPRO: Large Language Models as Optimizers](https://arxiv.org/abs/2309.03409) [2023, NeurIPS 2024] — 通过元提示（meta-prompts）将 LLM 用作优化器；在 BBH 基准上，优化后的提示词比人工设计的性能高出高达 50%。
- [DSPy: Compiling Declarative Language Model Calls into Self-Impro型 Pipelines](https://arxiv.org/abs/2310.03714) [2023, ICLR 2024] — 用于编程（而非提示）LLM 的框架，内置自动提示词优化。
- [MIPRO: Optimizing Instructions and Demonstrations for Multi-Stage Language Model Programs](https://arxiv.org/abs/2406.11695) [2024, EMNLP 2024] — 针对多阶段语言模型程序的贝叶斯优化；准确率提升最高达 13%。
- [TextGrad: Automatic "Differentiation" via Text](https://arxiv.org/abs/2406.07496) [2024] — 将复合 AI 系统视为计算图，以文本反馈作为梯度。发表于 Nature。
- [EvoPrompt](https://arxiv.org/abs/2309.08532) [2023, ACL 2024] — 采用进化算法自动优化离散提示词。
- [Meta Prompting for AI Systems](https://arxiv.org/abs/2311.11482) [2023, ICLR 2024 Workshop] — 使用范畴理论形式化的、与示例无关的结构化模板。
- [Prompt Engineering a Prompt Engineer (PE²)](https://arxiv.org/abs/2311.05661) [2024, ACL Findings] — 利用 LLM 对自身进行元提示，通过逐步模板优化提示词，显著提升推理能力。
- [Large Language Models Are Human-Level Prompt Engineers](https://arxiv.org/abs/2211.01910) [2022] — 基于 APE 的自动提示词生成。
- [Hard Prompts Made Easy: Gradient-Based Discrete Optimization for Prompt Tuning](https://arxiv.org/abs/2302.03668) [2023]
- [SPO: Self-Supervised Prompt Optimization](https://arxiv.org/abs/2502.06855) [2025] — 以先前方法 1–6% 的成本实现具有竞争力的性能。

### 提示词压缩

- [LLMLingua-2: Data Distillation for Efficient and Faithful Task-Agnostic Prompt Compression](https://arxiv.org/abs/2403.12968) [2024, ACL 2024] — 借助 GPT-4 数据蒸馏，速度比 LLMLingua 快 3–6 倍。
- [LongLLMLingua](https://arxiv.org/abs/2310.06839) [2023, ACL 2024] — 面向长上下文的问答感知压缩；在 token 数减少 4 倍的情况下性能提升 21.4%。
- [Prompt Compression for Large Language Models: A Survey](https://arxiv.org/abs/2410.12388) [2024] — 硬提示与软提示压缩方法的全面综述。

### 推理能力进展

- [Scaling LLM Test-Time Compute Optimally](https://arxiv.org/abs/2408.03314) [2024] — 证明最优的测试时计算分配可超越大 14 倍的模型。
- [DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning](https://arxiv.org/abs/2501.12948) [2025] — 纯 RL 训练的推理模型，性能对标 o1；开源并提供蒸馏变体。
- [s1: Simple Test-Time Scaling](https://arxiv.org/abs/2501.19393) [2025] — 仅在 1,000 个样本上进行 SFT，通过“预算强制”机制即可构建具有竞争力的推理模型。
- [Reasoning Language Models: A Blueprint](https://arxiv.org/abs/2501.11223) [2025] — 系统化组织推理语言模型方法的框架。
- [Demystifying Long Chain-of-Thought Reasoning in LLMs](https://arxiv.org/abs/2502.03373) [2025] — 分析现代推理模型中长思维链的行为模式。
- [Graph of Thoughts: Solving Elaborate Problems with LLMs](https://arxiv.org/abs/2308.09687) [2023, AAAI 2024] — 将思维建模为任意图结构；在排序任务上质量比 ToT 提升 62%。
- [Tree of Thoughts: Deliberate Problem Solving with LLMs](https://arxiv.org/abs/2305.10601) [2023, NeurIPS 2023] — 在推理路径上进行树搜索。
- [Everything of Thoughts](https://arxiv.org/abs/2311.04254) [2023] — 通过 MCTS 整合 CoT、ToT 与外部求解器。
- [Skeleton-of-Thought](https://arxiv.org/abs/2307.15337) [2023] — 通过答案骨架生成实现并行解码，加速比最高达 2.69x。
- [Chain of Thought Prompting Elicits Reasoning in Large Language Models](https://arxiv.org/abs/2201.11903) [2022] — CoT 奠基性论文。
- [Self-Consistency Improves Chain of Thought Reasoning](https://arxiv.org/abs/2203.11171) [2022] — 聚合多个 CoT 输出以提升可靠性。
- [Large Language Models are Zero-Shot Reasoners](https://arxiv.org/abs/2205.11916) [2022] — “让我们一步步思考”作为零样本推理触发器。
- [ReAct: Synergizing Reasoning and Acting in Language Models](https://arxiv.org/abs/2210.03629) [2022] — 交织推理与工具使用。

### 上下文中学习（In-Context Learning）

- [Many-Shot In-Context Learning](https://arxiv.org/abs/2404.11018) [2024, NeurIPS 2024 Spotlight] — 将 ICL 扩展到数百/数千个样本可获得显著收益；提出强化与无监督 ICL。
- [Many-Shot In-Context Learning in Multimodal Foundation Models](https://arxiv.org/abs/2405.09798) [2024] — 将多模态 ICL 扩展到约 2,000 个样本，覆盖 14 个数据集。
- [Rethinking the Role of Demonstrations: What Makes In-Context Learning Work?](https://arxiv.org/abs/2202.12837) [2022]
- [Fantastically Ordered Prompts and Where to Find Them](https://arxiv.org/abs/2104.08786) [2021] — 克服少样本提示词顺序敏感性。
- [Calibrate Before Use: Improving Few-Shot Performance of Language Models](https://arxiv.org/abs/2102.09690) [2021]

### Agent 提示与多 Agent 系统

- [Agentic Large Language Models: A Survey](https://arxiv.org/abs/2503.23037) [2025] — 全面综述，按推理、行动与交互能力对 Agentic LLMs 进行分类。
- [Large Language Model based Multi-Agents: A Survey of Progress and Challenges](https://arxiv.org/abs/2402.01680) [2024] — 覆盖画像、通信与成长机制。
- [Multi-Agent Collaboration Mechanisms: A Survey of LLMs](https://arxiv.org/abs/2501.06322) [2025] — 综述基于 LLM 的多 Agent 系统中的辩论与合作策略。
- [AutoGen: Enabling Next-Gen LLM Applications via Multi-Agent Conversation](https://arxiv.org/abs/2308.08155) [2023] — 微软奠基性的多 Agent 框架论文。
- [ToolLLM: Facilitating Large Language Models to Master 16000+ Real-World APIs](https://arxiv.org/abs/2307.16789) [2023, ICLR 2024] — 训练 LLM 使用海量真实世界 API。
- [SWE-bench: Can Language Models Resolve Real-World GitHub Issues?](https://arxiv.org/abs/2310.06770) [2023, ICLR 2024] — 驱动编程 Agent 进展的基准测试。
- [AgentBench: Evaluating LLMs as Agents](https://arxiv.org/abs/2308.03688) [2023, ICLR 2024] — 覆盖 8 个环境的基准测试。
- [PAL: Program-aided Language Models](https://arxiv.org/abs/2211.10435) [2023] — 将计算卸载至代码解释器。

### 多模态提示词工程

- [Visual Prompting in Multimodal Large Language Models: A Survey](https://arxiv.org/abs/2409.15310) [2024] — MLLMs 中视觉提示方法的全面综述。
- [Set-of-Mark Prompting Unleashes Extraordinary Visual Grounding in GPT-4V](https://arxiv.org/abs/2310.11441) [2023] — 视觉标记显著提升视觉定位能力。
- [A Comprehensive Survey and Guide to Multimodal Large Language Models in Vision-Language Tasks](https://arxiv.org/abs/2411.06284) [2024] — 覆盖文本、图像、视频、音频 MLLMs。
- [Multimodal Chain-of-Thought Reasoning in Language Models](https://arxiv.org/abs/2302.00923) [2023]
- [From Prompt Engineering to Prompt Craft](https://arxiv.org/abs/2411.13422) [2024] — 从设计研究视角探讨扩散模型的提示词“工艺”。

### 结构化输出与格式控制

- [Let Me Speak Freely? A Study on the Impact of Format Restrictions on Performance of LLMs](https://arxiv.org/abs/2408.02442) [2024] — 研究将输出约束为结构化格式对推理性能的影响。
- [Batch Prompting: Efficient Inference with LLM APIs](https://arxiv.org/abs/2301.08721) [2023]
- [Structured Prompting: Scaling In-Context Learning to 1,000 Examples](https://arxiv.org/abs/2212.06713) [2022]

### 提示词注入与安全

- [Formalizing and Benchmarking Prompt Injection Attacks and Defenses](https://arxiv.org/abs/2310.12815) [2023, USENIX Security 2024] — 提供形式化框架，系统评估 10 个 LLM 上的 5 种攻击与 10 种防御。
- [The Instruction Hierarchy: Training LLMs to Prioritize Privileged Instructions](https://arxiv.org/abs/2404.13208) [2024] — OpenAI 的优先级训练方案，用于防御注入攻击。
- [AgentDojo: A Dynamic Environment to Evaluate Prompt Injection Attacks and Defenses](https://arxiv.org/abs/2406.13352) [2024] — 真实 Agent 场景基准测试。
- [InjecAgent: Benchmarking Indirect Prompt Injections in Tool-Integrated LLM Agents](https://arxiv.org/abs/2403.02691) [2024]
- [SecAlign: Defending Against Prompt Injection with Preference Optimization](https://arxiv.org/abs/2410.05451) [2024] — 基于 DPO 的防御方案。
- [WASP: Benchmarking Web Agent Security Against Prompt Injection](https://arxiv.org/abs/2504.18575) [2025] — 面向网页/电脑使用 Agent 的安全基准测试。
- [Many-Shot Jailbreaking](https://www.anthropic.com/research/many-shot-jailbreaking) [2024] — 在长上下文窗口中扩展有害样本可实现越狱（Anthropic 技术报告）。
- [Constitutional AI: Harmlessness from AI Feedback](https://arxiv.org/abs/2212.08073) [2022]
- [Ignore Previous Prompt: Attack Techniques For Language Models](https://arxiv.org/abs/2211.09527) [2022]
- [Artificial Intelligence and Cybersecurity: Documented Risks, Enterprise Guardrails, and Emerging Threats in 2024–2025](https://www.ijfmr.com/research-paper.php?id=62200) [2025] — 真实提示词注入事件综述，提供实用的治理提示模式。

### 提示词工程应用

- [Rephrase and Respond: Let Large Language Models Ask Better Questions for Themselves](https://arxiv.org/abs/2311.04205) [2023]
- [Legal Prompt Engineering for Multilingual Legal Judgement Prediction](https://arxiv.org/abs/2212.02199) [2023]
- [Conversing with Copilot: Exploring Prompt Engineering for Solving CS1 Problems](https://arxiv.org/abs/2210.15157) [2022]
- [Commonsense-Aware Prompting for Controllable Empathetic Dialogue Generation](https://arxiv.org/abs/2302.01441) [2023]
- [PLACES: Prompting Language Models for Social Conversation Synthesis](https://arxiv.org/abs/2302.03269) [2023]
- [Medical Image Segmentation Using Transformer Encoders and Prompt-Based Learning: A Systematic Review](https://ieeexplore.ieee.org/document/11313186/) [2025]
- [TableRAG: A Retrieval Augmented Generation Framework for Heterogeneous Document Reasoning](https://arxiv.org/abs/2506.10380) [2025] — 基于 SQL 的接口，保留表格结构以支持多跳查询。

### 文生图生成

- [A Taxonomy of Prompt Modifiers for Text-To-Image Generation](https://arxiv.org/abs/2204.13988) [2022]
- [Design Guidelines for Prompt Engineering Text-to-Image Generative Models](https://arxiv.org/abs/2109.06977) [2021]
- [High-Resolution Image Synthesis with Latent Diffusion Models](https://arxiv.org/abs/2112.10752) [2021]
- [DALL·E: Creating Images from Text](https://arxiv.org/abs/2102.12092) [2021]
- [Investigating Prompt Engineering in Diffusion Models](https://arxiv.org/abs/2211.15462) [2022]

### 文生音乐/音频生成

- [MusicLM: Generating Music From Text](https://arxiv.org/abs/2301.11325) [2023]
- [ERNIE-Music: Text-to-Waveform Music Generation with Diffusion Models](https://arxiv.org/pdf/2302.04456) [2023]
- [AudioLM: A Language Modeling Approach to Audio Generation](https://arxiv.org/pdf/2209.03143) [2023]
- [Make-An-Audio: Text-To-Audio Generation with Prompt-Enhanced Diffusion Models](https://arxiv.org/pdf/2301.12661.pdf) [2023]

### 奠基性论文（2024年之前）

这些论文奠定了现代提示词工程的核心概念：

- [Language Models are Few-Shot Learners (GPT-3)](https://arxiv.org/abs/2005.14165) [2020] — 大规模展示少样本提示能力。
- [Prefix-Tuning: Optimizing Continuous Prompts for Generation](https://arxiv.org/abs/2101.00190) [2021]
- [The Power of Scale for Parameter-Efficient Prompt Tuning](https://arxiv.org/abs/2104.08691) [2021]
- [Prompt Programming for Large Language Models: Beyond the Few-Shot Paradigm](https://arxiv.org/abs/2102.07350) [2021]
- [Show Your Work: Scratchpads for Intermediate Computation with Language Models](https://arxiv.org/abs/2112.00114) [2021]
- [Generated Knowledge Prompting for Commonsense Reasoning](https://arxiv.org/abs/2110.08387) [2021]
- [Making Pre-trained Language Models Better Few-shot Learners](https://aclanthology.org/2021.acl-long.295) [2021]
- [AutoPrompt: Eliciting Knowledge from Language Models with Automatically Generated Prompts](https://arxiv.org/abs/2010.15980) [2020]
- [How Can We Know What Language Models Know?](https://direct.mit.edu/tacl/article/doi/10.1162/tacl_a_00324/96460/) [2020]
- [A Prompt Pattern Catalog to Enhance Prompt Engineering with ChatGPT](https://arxiv.org/abs/2302.11382) [2023]
- [Synthetic Prompting: Generating Chain-of-Thought Demonstrations for LLMs](https://arxiv.org/abs/2302.00618) [2023]
- [Progressive Prompts: Continual Learning for Language Models](https://arxiv.org/abs/2301.12314) [2023]
- [Successive Prompting for Decompleting Complex Questions](https://arxiv.org/abs/2212.04092) [2022]
- [Decomposed Prompting: A Modular Approach for Solving Complex Tasks](https://arxiv.org/abs/2210.02406) [2022]
- [PromptChainer: Chaining Large Language Model Prompts through Visual Programming](https://arxiv.org/abs/2203.06566) [2022]
- [Ask Me Anything: A Simple Strategy for Prompting Language Models](https://paperswithcode.com/paper/ask-me-anything-a-simple-strategy-for) [2022]
- [Prompting GPT-3 To Be Reliable](https://arxiv.org/abs/2210.09150) [2022]
- [On Second Thought, Let's Not Think Step by Step! Bias and Toxicity in Zero-Shot Reasoning](https://arxiv.org/abs/2212.08061) [2022]

---

## 工具与代码
🔧

### 提示词管理与测试

| Name | Description | Link |
|:-----|:-----------|:----:|
| **Promptfoo** | 用于测试、评估和对大语言模型提示词进行红队测试的开源 CLI。支持 YAML 配置、CI/CD 集成与对抗性测试。~9K+ ⭐ | [GitHub](https://github.com/promptfoo/promptfoo) |
| **Promptify** | 使用 LLM 解决 NLP 问题，轻松为 GPT、PaLM 等流行生成模型生成不同任务的提示词。 | [[Github]](https://github.com/promptslab/Promptify) |
| **Agenta** | 开源 LLM 开发者平台，提供提示词管理、评估、人工反馈与部署功能。 | [GitHub](https://github.com/Agenta-AI/agenta) |
| **PromptLayer** | 版本控制、测试并监控每个提示词与 Agent，内置强大评估、追踪与回归集。 | [Website](https://promptlayer.com/) |
| **Helicone** | 生产级提示词监控与优化平台。 | [Website](https://helicone.ai/) |
| **LangGPT** | 结构化与元提示设计框架。10K+ ⭐ | [GitHub](https://github.com/langgpt/LangGPT) |
| **ChainForge** | 无需代码即可构建、测试和比较 LLM 提示词响应结果的可视化工具箱。 | [GitHub](https://github.com/ianarawjo/ChainForge) |
| **LMQL** | 一种用于 LLM 的查询语言，使复杂的提示逻辑可编程化。 | [GitHub](https://github.com/eth-sri/lmql) |
| **Promptotype** | 开发、测试和管理结构化 LLM 提示词的平台。 | [Website](https://www.promptotype.io) |
| **PromptPanda** | AI 驱动的提示词管理系统，简化工作流。 | [Website](https://promptpanda.io) |
| **Promptimize AI** | 浏览器扩展插件，自动优化用户针对任何 AI 模型的提示词。 | [Website](https://promptimize.ai) |
| **PROMPTMETHEUS** | 基于 Web 的“提示词工程 IDE”，支持迭代创建与运行提示词。 | [Website](https://promptmetheus.com) |
| **Better Prompt** | LLM 提示词上线前的测试套件。 | [GitHub](https://github.com/krrishdholakia/betterprompt) |
| **OpenPrompt** | 开源提示学习研究框架。 | [GitHub](https://github.com/thunlp/OpenPrompt) |
| **Prompt Source** | 创建、分享和使用自然语言提示词的工具包。 | [GitHub](https://github.com/bigscience-workshop/promptsource) |
| **Prompt Engine** | Microsoft 提供的 NPM 实用库，用于创建和维护 LLM 提示词。 | [GitHub](https://github.com/microsoft/prompt-engine) |
| **PromptInject** | 量化分析 LLM 对抗性提示攻击鲁棒性的框架。 | [GitHub](https://github.com/agencyenterprise/PromptInject) |
| **LynxPrompt** | 可自托管的 AI IDE 配置文件（`.cursorrules`, `CLAUDE.md`, `copilot-instructions.md`）管理平台。提供 Web UI、REST API、CLI，以及支持 30+ AI 编程助手的联邦蓝图市场。 | [GitHub](https://github.com/GeiserX/LynxPrompt) |
| **flompt** | 可视化 AI 提示词构建器，将提示词分解为 12 个语义块（角色、上下文、约束、示例等）并编译为优化后的 XML。提供 ChatGPT/Claude/Gemini 浏览器扩展及 Claude Code Agent MCP 服务器。免费开源。 | [Website](https://flompt.dev) |

### 大语言模型评估工具

| Name | Description | Link |
|:-----|:-----------|:----:|
| **DeepEval** | 覆盖 RAG、Agent 和对话的开源评估框架，支持 CI/CD 集成。~7K+ ⭐ | [GitHub](https://github.com/confident-ai/deepeval) |
| **Ragas** | RAG 评估工具，基于知识图谱生成测试集并提供 30+ 项指标。~8K+ ⭐ | [GitHub](https://github.com/explodinggradients/ragas) |
| **LangSmith** | LangChain 推出的平台，用于调试、测试、评估和监控 LLM 应用。 | [Website](https://smith.langchain.com/) |
| **Langfuse** | 开源 LLM 可观测性平台，提供追踪、提示词管理与人工标注功能。~7K+ ⭐ | [GitHub](https://github.com/langfuse/langfuse) |
| **Braintrust** | 端到端 AI 评估平台，通过 SOC2 Type II 认证。 | [Website](https://www.braintrust.dev/) |
| **Arize AI / Phoenix** | 实时 LLM 监控，具备漂移检测与追踪功能。 | [GitHub](https://github.com/Arize-ai/phoenix) |
| **TruLens** | 评估并解释 LLM 应用；追踪幻觉、相关性与事实依据性。 | [GitHub](https://github.com/truera/trulens) |
| **InspectAI** | 专为基于基准测试评估 Agent 而设计（UK AISI）。 | [GitHub](https://github.com/UKGovernmentBEIS/inspect_ai) |
| **Opik** | 在开发与生产生命周期中评估、测试并交付 LLM 应用。 | [GitHub](https://github.com/comet-ml/opik) |
| **EvalView** | CLI 工具，支持使用 YAML 测试用例测试多步 AI Agent，具备回归检测与生产监控功能。 |[GitHub](https://github.com/hidai25/eval-view) |

### Agent 框架

| Name | Description | Link |
|:-----|:-----------|:----:|
| **LangChain / LangGraph** | 采用最广泛的 LLM 应用框架；LangGraph 增加基于图的多步 Agent 工作流。~100K+ / ~10K+ ⭐ | [GitHub](https://github.com/langchain-ai/langchain) · [LangGraph](https://github.com/langchain-ai/langgraph) |
| **CrewAI** | 角色扮演 AI Agent 编排系统，集成 700+ 工具。~44K+ ⭐ | [GitHub](https://github.com/crewAIInc/crewAI) |
| **AutoGen (AG2)** | 微软的多 Agent 对话框架。~40K+ ⭐ | [GitHub](https://github.com/microsoft/autogen) |
| **DSPy** | 斯坦福大学推出的 LLM 编程框架，内置自动提示词/权重优化。~22K+ ⭐ | [GitHub](https://github.com/stanfordnlp/dspy) |
| **OpenAI Agents SDK** | 官方 Agent 框架，支持函数调用、护栏（guardrails）与交接功能。~10K+ ⭐ | [GitHub](https://github.com/openai/openai-agents-python) |
| **Semantic Kernel** | 微软的 AI 框架，驱动 M365 Copilot；支持 C#、Python、Java。~24K+ ⭐ | [GitHub](https://github.com/microsoft/semantic-kernel) |
| **LlamaIndex** | 面向 RAG 与 Agent 能力的底层数据框架。~40K+ ⭐ | [GitHub](https://github.com/run-llama/llama_index) |
| **Haystack** | 开源 NLP 框架，采用流水线架构支持 RAG 与 Agent。~20K+ ⭐ | [GitHub](https://github.com/deepset-ai/haystack) |
| **Agno (formerly Phidata)** | Python Agent 框架，实例化速度达微秒级。~20K+ ⭐ | [GitHub](https://github.com/agno-agi/agno) |
| **Smolagents** | Hugging Face 推出的极简代码优先 Agent 框架（约 1000 LOC）。~15K+ ⭐ | [GitHub](https://github.com/huggingface/smolagents) |
| **Pydantic AI** | 基于 Pydantic 实现结构化验证的类型安全 Agent 框架。~8K+ ⭐ | [GitHub](https://github.com/pydantic/pydantic-ai) |
| **Mastra** | TypeScript AI Agent 框架，支持助手、RAG 与可观测性。~20K+ ⭐ | [GitHub](https://github.com/mastra-ai/mastra) |
| **Google ADK** | 深度集成 Gemini 与 Google Cloud 的 Agent 开发套件。 | [GitHub](https://github.com/google/adk-python) |
| **Strands Agents (AWS)** | 模型无关框架，深度集成 AWS 服务。 | [GitHub](https://github.com/strands-agents/sdk-python) |
| **Langflow** | 基于节点的可视化 Agent 构建器，支持拖拽操作。~50K+ ⭐ | [GitHub](https://github.com/langflow-ai/langflow) |
| **n8n** | 工作流自动化平台，内置 AI Agent 能力与 400+ 集成。~60K+ ⭐ | [GitHub](https://github.com/n8n-io/n8n) |
| **Dify** | 面向 Agent 工作流的端到端后端平台，支持工具调用型 Agent 与 RAG。 | [GitHub](https://github.com/langgenius/dify) |
| **PraisonAI** | 多 AI Agent 框架，支持 100+ LLM、MCP 集成与内置记忆功能。 | [GitHub](https://github.com/MervinPraison/PraisonAI) |
| **Neurolink** | 统一 12+ 提供商的多模型 AI Agent 框架，提供工作流编排能力。 | [GitHub](https://github.com/juspay/neurolink) |
| **Composio** | 零配置为 AI Agent 连接 100+ 工具。 | [GitHub](https://github.com/composiohq/composio) |

### 提示词优化工具

| Name | Description | Link |
|:-----|:-----------|:----:|
| **DSPy** | 提供多种优化器（MIPROv2, BootstrapFewShot, COPRO）用于自动提示词调优。~22K+ ⭐ | [GitHub](https://github.com/stanfordnlp/dspy) |
| **TextGrad** | 基于文本的自动微分技术（斯坦福）。~2K+ ⭐ | [GitHub](https://github.com/zou-group/textgrad) |
| **OPRO** | Google DeepMind 推出的提示词优化方案。 | [GitHub](https://github.com/google-deepmind/opro) |

### 红队测试与提示词安全

| Name | Description | Link |
|:-----|:-----------|:----:|
| **Garak (NVIDIA)** | LLM 漏洞扫描器，检测幻觉、注入与越狱——被称为“LLM 界的 nmap”。~3K+ ⭐ | [GitHub](https://github.com/NVIDIA/garak) |
| **PyRIT (Microsoft)** | Python 风险识别工具，用于自动化红队测试。~3K+ ⭐ | [GitHub](https://github.com/Azure/PyRIT) |
| **DeepTeam** | 覆盖 40+ 漏洞、10+ 攻击方法，支持 OWASP Top 10。 | [GitHub](https://github.com/confident-ai/deepteam) |
| **LLM Guard** | LLM 输入/输出验证的安全工具包。~2K+ ⭐ | [GitHub](https://github.com/protectai/llm-guard) |
| **NeMo Guardrails (NVIDIA)** | 为对话系统提供可编程护栏。~5K+ ⭐ | [GitHub](https://github.com/NVIDIA/NeMo-Guardrails) |
| **Guardrails AI** | 定义严格的输出格式（JSON Schema）以确保系统可靠性。 | [Website](https://www.guardrailsai.com) |
| **Lakera** | AI 安全平台，支持实时提示词注入检测。 | [Website](https://lakera.ai/) |
| **Purple Llama (Meta)** | 开源 LLM 安全评估工具集，包含 CyberSecEval。 | [GitHub](https://github.com/meta-llama/PurpleLlama) |
| **GPTFuzz** | 自动化越狱模板生成器，成功率超 90%。 | [GitHub](https://github.com/sherdencooper/GPTFuzz) |
| **Rebuff** | 开源提示词注入检测与防御工具。 | [GitHub](https://github.com/protectai/rebuff) |
| **AgentSeal** | “开源扫描器，运行 150 种攻击探针以测试 AI Agent 的提示词注入与提取漏洞。” | [GitHub](https://github.com/agentseal/agentseal) |

### MCP（模型上下文协议）

MCP 是由 Anthropic 开发的开放标准（2024年11月发布，2025年12月捐赠至 Linux Foundation），用于通过标准化接口将 AI 助手连接到外部数据源与工具。其 SDK **月下载量超 9700万**，已被 GitHub、Google 及各大主流 AI 厂商采用。

| Name | Description | Link |
|:-----|:-----------|:----:|
| **MCP Specification** | 核心协议规范与 SDK。~15K+ ⭐ | [GitHub](https://github.com/modelcontextprotocol/modelcontextprotocol) |
| **MCP Reference Servers** | 官方参考实现：fetch、filesystem、GitHub、Slack、Postgres。 | [GitHub](https://github.com/modelcontextprotocol/servers) |
| **FastMCP (Python)** | 用于构建 MCP Server 的高级 Pythonic 框架。~5K+ ⭐ | [GitHub](https://github.com/jlowin/fastmcp) |
| **GitHub MCP Server** | GitHub 官方 MCP 服务器，支持仓库、Issue、PR 与 Actions 交互。~15K+ ⭐ | [GitHub](https://github.com/github/github-mcp-server) |
| **Awesome MCP Servers** | 精选的 10,000+ 社区 MCP Server 列表。~30K+ ⭐ | [GitHub](https://github.com/punkpeye/awesome-mcp-servers) |
| **Context7** | MCP 服务器，提供版本特定的文档以减少代码幻觉。 | [GitHub](https://github.com/upstash/context7) |
| **GitMCP** | 通过更改域名即可为任意 GitHub 仓库创建远程 MCP Server。 | [Website](https://gitmcp.io/) |
| **MCP Inspector** | MCP Server 开发的可视化测试工具。 | [GitHub](https://github.com/modelcontextprotocol/inspector) |

### Vibe Coding 与 AI 编程助手

> 🟢 = 开源 · 🔵 = 商业闭源 · 🟣 = 开源核心 + 商业云服务/API

#### 基于 CLI 的编程 Agent

原生终端 Agent 工具，理解你的代码库并执行多步任务。

| Name | Description | Type | Link |
|:-----|:-----------|:----:|:----:|
| **Claude Code** | Anthropic 推出的 Agentic 编码 CLI；理解完整代码库并通过自然语言执行复杂的多步任务。 | 🔵 | [Docs](https://docs.anthropic.com/en/docs/claude-code) |
| **OpenAI Codex CLI** | OpenAI 开源的终端编程 Agent；轻量级、本地优先，支持沙盒代码执行。~68K+ ⭐ | 🟣 | [GitHub](https://github.com/openai/codex) |
| **Gemini CLI** | Google 开源的终端 AI Agent，具备 1M token 上下文窗口与 Google Search 定位能力。~96K+ ⭐ | 🟣 | [GitHub](https://github.com/google-gemini/gemini-cli) |
| **Qwen Code** | 专为 Qwen3-Coder 优化的开源终端 AI Agent；支持多协议（OpenAI/Anthropic/Gemini API），每日 1,000 次免费请求。~21K+ ⭐ | 🟢 | [GitHub](https://github.com/QwenLM/qwen-code) |
| **Aider** | 终端内 AI 结对编程，深度集成 Git；映射整个代码库并自动提交更改。~42K+ ⭐ | 🟢 | [GitHub](https://github.com/Aider-AI/aider) |
| **OpenCode** | 功能强大的开源 AI 编程 Agent，提供美观的 TUI；支持几乎所有 AI 模型提供商。~120K+ ⭐ | 🟢 | [GitHub](https://github.com/opencode-ai/opencode) |
| **Goose** | Block (Square/Cash App) 推出的可扩展开源 AI Agent；安装、执行、编辑与测试，兼容任意 LLM。~29K+ ⭐ | 🟢 | [GitHub](https://github.com/block/goose) |
| **Crush** | Charmbracelet 推出的华丽 Agentic 编程 Agent，支持多模型、LSP 集成与美观的终端 UI。~9K+ ⭐ | 🟢 | [GitHub](https://github.com/charmbracelet/crush) |
| **Amazon Q Developer CLI** | AWS 提供的终端 Agentic 对话体验；正逐步过渡至 Kiro CLI。 | 🟣 | [GitHub](https://github.com/aws/amazon-q-developer-cli) |
| **Amp** | Sourcegraph 推出的 Agentic 编程工具（Cody 继任者）；支持 CLI 与 IDE。 | 🔵 | [Website](https://ampcode.com) |
| **Junie CLI** | JetBrains 的 LLM 无关编码 Agent CLI（2026 beta版）；支持所有主流模型提供商。 | 🔵 | [Website](https://www.jetbrains.com/junie/) |
| **Autohand Code CLI** | 自进化自主终端编程 Agent，支持多提供商 LLM、40+ 工具与模块化技能系统。 | 🟢 | [GitHub](https://github.com/autohandai/code-cli) |

#### AI 代码编辑器 / IDE

深度集成 AI 的独立编辑器或 IDE 分支版本。

| Name | Description | Type | Link |
|:-----|:-----------|:----:|:----:|
| **Cursor** | 领先的 AI 原生代码编辑器（VS Code fork）；Composer 可根据自然语言生成完整应用，支持 Agentic 多文件编辑。 | 🔵 | [Website](https://cursor.com) |
| **Windsurf** | AI 驱动 IDE（VS Code fork），内置专有 Cascade Agent 与 SWE-1.5 模型；已被 Cognition AI 收购。 | 🔵 | [Website](https://windsurf.com) |
| **Zed** | Rust 编写的高性能编辑器，原生支持 AI 功能、Zeta 编辑预测与 Agent Client Protocol。~77K+ ⭐ | 🟢 | [GitHub](https://github.com/zed-industries/zed) |
| **Trae** | 字节跳动推出的免费 AI IDE（“真正的 AI 工程师”），内置 Builder Mode；免费提供 Claude、GPT-4o 与 DeepSeek 访问权限。 | 🔵 | [Website](https://www.trae.ai) |
| **Google Antigravity** | Google 的 Agent-first IDE（VS Code fork）；提供 Manager 视图以并行编排多个 Agent；由 Gemini 驱动。 | 🔵 | [Website](https://antigravity.google) |
| **Kiro** | AWS 推出的规范驱动型 Agentic AI IDE（VS Code fork）；将提示词转化为规范，再输出可运行代码、文档与测试。 | 🔵 | [Website](https://kiro.dev) |
| **PearAI** | 开源 AI 代码编辑器（VS Code fork），基于 Continue 实现聊天与补全功能。~40K+ ⭐ | 🟢 | [GitHub](https://github.com/trypear/pearai-app) |
| **Void** | 开源 Cursor 替代品（VS Code fork）；支持任意模型或本地部署，提供变更可视化功能。~28K+ ⭐ | 🟢 | [GitHub](https://github.com/voideditor/void) |
| **Melty** | 聊天优先的开源 AI 代码编辑器，支持多文件编辑与深度 Git 集成。~7K+ ⭐ | 🟢 | [GitHub](https://github.com/meltylabs/melty) |
| **Emdash** | YC W26 支持的开源 Agentic 开发环境，可在隔离的 Git worktree 中并行运行多个编程 Agent。 | 🟢 | [GitHub](https://github.com/generalaction/emdash) |

#### IDE 扩展/插件

适用于 VS Code、JetBrains、Neovim 等编辑器的插件。

| Name | Description | Type | Link |
|:-----|:-----------|:----:|:----:|
| **GitHub Copilot** | 采用最广泛的 AI 编程助手；提供行内补全、聊天与 Agentic 编码功能，支持 VS Code、JetBrains、Neovim。 | 🔵 | [Website](https://github.com/features/copilot) |
| **Cline** | VS Code 中的自主编程 Agent，支持人工审批回路；具备文件编辑、终端命令与浏览器操作能力。~59K+ ⭐ | 🟢 | [GitHub](https://github.com/cline/cline) |
| **Continue** | 开源的 VS Code 和 JetBrains 扩展插件，用于创建自定义模块化 AI 开发系统；支持任意模型。~32K+ ⭐ | 🟢 | [GitHub](https://github.com/continuedev/continue) |
| **Cody** | 由 Sourcegraph 驱动的 AI 助手，从本地与远程代码库提取上下文；支持 VS Code、JetBrains、Visual Studio。 | 🔵 | [Website](https://sourcegraph.com/cody) |
| **Codeium** | 免费 AI 编程扩展插件，支持 40+ IDE，提供补全、聊天功能并覆盖 70+ 语言。 | 🟣 | [Website](https://codeium.com) |
| **Amazon Q Developer** | AWS 的 AI 编程助手，提供补全、行内聊天与 Agent 模式；深度集成 AWS 服务。 | 🟣 | [Website](https://aws.amazon.com/q/developer/) |
| **Gemini Code Assist** | Google IDE 扩展插件，由 Gemini 驱动，支持补全、Next Edit Predictions 与行内差异对比；个人用户免费。 | 🟣 | [Website](https://codeassist.google) |
| **Tabnine** | 隐私优先的 AI 助手，基于宽松许可的开源代码训练；支持所有主流 IDE 并提供本地部署方案。 | 🔵 | [Website](https://www.tabnine.com) |
| **Augment Code** | 企业级 AI 编程助手，配备 20万 token Context Engine 以深度理解代码库。 | 🔵 | [Website](https://www.augmentcode.com) |
| **Qodo** | AI 代码审查与质量平台，采用多 Agent 架构；支持测试生成、代码审查与 CI/CD 强制检查。 | 🟣 | [Website](https://www.qodo.ai) |
| **CodeGeeX** | 开源多语言代码生成模型，支持 20+ 语言及 VS Code/JetBrains 扩展插件。~11K+ ⭐ | 🟢 | [GitHub](https://github.com/zai-org/CodeGeeX) |
| **Tabby** | 自托管开源 AI 编程助手（Copilot 替代品）；完全运行在你的基础设施上。~25K+ ⭐ | 🟢 | [GitHub](https://github.com/TabbyML/tabby) |

#### AI 编程平台/云端 Agent

基于浏览器或云托管的 Agent，可自主构建、测试与部署应用。

| Name | Description | Type | Link |
|:-----|:-----------|:----:|:----:|
| **Devin** | 首款完全自主的云原生 AI 软件工程师；独立规划、编码、测试并创建 PR。 | 🔵 | [Website](https://devin.ai) |
| **Replit Agent** | 云原生 AI Agent，可在浏览器中自主构建、测试与部署全栈应用；支持 50+ 语言。 | 🔵 | [Website](https://replit.com/products/agent) |
| **bolt.new** | AI 驱动的 Web 开发 Agent；通过 WebContainers 在浏览器内直接提示、运行、编辑和部署全栈应用。~15K+ ⭐ | 🟢 | [GitHub](https://github.com/stackblitz/bolt.new) |
| **bolt.diy** | bolt.new 的社区分支，扩展功能并支持更广泛的 LLM 灵活性。~12K+ ⭐ | 🟢 | [GitHub](https://github.com/stackblitz-labs/bolt.diy) |
| **Lovable** | 通过自然语言生成全栈应用，内置 Supabase、认证与一键部署；欧洲增速最快达到 2000万 ARR 的初创公司之一。 | 🔵 | [Website](https://lovable.dev) |
| **v0** | Vercel 推出的 AI 平台，根据自然语言生成高质量的 React/Next.js UI 组件。 | 🔵 | [Website](https://v0.dev) |
| **GitHub Copilot Workspace** | 云端编程环境，内置规划、头脑风暴与修复 Agent；包含在付费 Copilot 套餐中。 | 🔵 | [Website](https://githubnext.com/projects/copilot-workspace) |
| **Firebase Studio** | Google 推出的 Agentic 云原生开发环境。 | 🔵 | [Website](https://firebase.google.com/studio) |

#### 开源编程 Agent 框架

用于构建自主编程 Agent 的框架与研究项目。

| Name | Description | Type | Link |
|:-----|:-----------|:----:|:----:|
| **OpenHands** | 领先的云端编程 Agent 平台；在 SWE-bench 上持续名列前茅。前身为 OpenDevin。~69K+ ⭐ | 🟢 | [GitHub](https://github.com/OpenHands/OpenHands) |
| **SWE-agent** | 接收 GitHub Issue 并自动修复，采用自定义的 Agent-Computer 接口。[NeurIPS 2024] ~19K+ ⭐ | 🟢 | [GitHub](https://github.com/SWE-agent/SWE-agent) |
| **Open SWE** | LangChain 推出的异步云托管编程 Agent 框架，基于 LangGraph 构建并集成 Slack/Linear。~8K+ ⭐ | 🟢 | [GitHub](https://github.com/langchain-ai/open-swe) |
| **Devika** | 开源 Agentic 软件工程师；拆解指令、研究并编写代码。Devin 的替代品。~18K+ ⭐ | 🟢 | [GitHub](https://github.com/stitionai/devika) |
| **AutoCodeRover** | 结合 LLM 与故障定位的自主程序改进工具，用于解决 GitHub Issue。~2.8K+ ⭐ | 🟢 | [GitHub](https://github.com/nus-apr/auto-code-rover) |
| **Agentless** | 简化的三阶段方法（定位 → 修复 → 验证）以解决软件开发问题。~2K+ ⭐ | 🟢 | [GitHub](https://github.com/OpenAutoCoder/Agentless) |
| **Devon** | 开源结对编程 SWE Agent，支持代码编写、规划与研究；兼容 Claude、GPT-4、Llama、Ollama。~3.5K+ ⭐ | 🟢 | [GitHub](https://github.com/entropy-research/Devon) |

### 其他值得关注的仓库

| Name | Description | Link |
|:-----|:-----------|:----:|
| **Prompt Engineering Guide (DAIR.AI)** | 权威的开源指南与资源枢纽。300万+学习者。~55K+ ⭐ | [GitHub](https://github.com/dair-ai/Prompt-Engineering-Guide) |
| **Awesome ChatGPT Prompts / Prompts.chat** | 全球最大的开源提示词库。涵盖数千个主流模型的提示词。 | [GitHub](https://github.com/f/awesome-chatgpt-prompts) |
| **12-Factor Agents** | 构建生产级 LLM 驱动软件的指导原则。~17K+ ⭐ | [GitHub](https://github.com/humanlayer/12-factor-agents) |
| **NirDiamant/Prompt_Engineering** | 22 个动手实践 Jupyter Notebook 教程。~3K+ ⭐ | [GitHub](https://github.com/NirDiamant/Prompt_Engineering) |
| **Context Engineering Repository** | 从提示词工程转向上下文设计的原理手册。 | [GitHub](https://github.com/davidkimai/Context-Engineering) |
| **AI Agent System Prompts Library** | 生产级 AI 编程 Agent（Claude Code, Gemini CLI, Cline, Aider, Roo Code）的系统提示词合集。 | [GitHub](https://github.com/tallesborges/agentic-system-prompts) |
| **Awesome Vibe Coding** | 精选的 245+ 工具与资源，用于通过自然语言提示构建软件。 | [GitHub](https://github.com/taskade/awesome-vibe-coding) |
| **OpenAI Cookbook** | 官方提示词、工具、RAG 与评估示例。 | [GitHub](https://github.com/openai/openai-cookbook) |
| **Embedchain** | 基于你的数据集创建 ChatGPT 风格机器人的框架。 | [GitHub](https://github.com/embedchain/embedchain) |
| **ThoughtSource** | 机器思维科学的开发框架。 | [GitHub](https://github.com/OpenBioLink/ThoughtSource) |
| **Promptext** | 提取并格式化 AI 提示词所需的代码上下文，支持 token 计数。 | [GitHub](https://github.com/1broseidon/promptext) |
| **Price Per Token** | 对比 200+ 模型的 LLM API 定价。 | [Website](https://pricepertoken.com/) |
| **OpenPaw** | CLI 工具（`npx pawmode`），通过生成带有个性、记忆与 38 个技能路由器的系统提示词（CLAUDE.md + SOUL.md），将 Claude Code 转化为个人助手。 | [GitHub](https://github.com/daxaur/openpaw) |
| **Think Better** | 开源 CLI，永久注入 10 种结构化决策框架（MECE、Issue Trees、Pre-Mortems）与 12 个认知偏差检测器到 AI 助手提示词中。Go 语言编写，MIT 协议。 | [GitHub](https://github.com/HoangTheQuyen/think-better) |

---

## API
💻

### OpenAI

| Model | Context | Price (Input/Output per 1M tokens) | Key Feature |
|:------|:--------|:-----------------------------------|:------------|
| GPT-5.2 / 5.2 Thinking | 400K | $1.75 / $14 | 最新旗舰，90% 缓存折扣，支持可配置推理 |
| GPT-5.1 | 400K | $1.25 / $10 | 上一代旗舰模型 |
| GPT-4.1 / 4.1 mini / nano | 1M | $2 / $8 | 最佳非推理模型，比 GPT-4o 快 40% 且便宜 80% |
| o3 / o3-pro | 200K | Varies | 原生支持工具调用的推理模型 |
| o4-mini | 200K | Cost-efficient | 快速推理，在其成本级别中 AIME 表现最佳 |
| GPT-OSS-120B / 20B | 128K | $0.03 / $0.30 | 首款开源权重模型，Apache 2.0 协议 |

核心功能：Responses API、Agents SDK、结构化输出、函数调用、提示词缓存（90% 折扣）、Batch API（50% 折扣）、MCP 支持。[平台文档](https://platform.openai.com/docs/models)

### Anthropic (Claude)

| Model | Context | Price (Input/Output per 1M tokens) | Key Feature |
|:------|:--------|:-----------------------------------|:------------|
| Claude Opus 4.6 | 1M (beta) | $5 / $25 | 最强模型，SOTA 编码与 Agentic 任务表现 |
| Claude Sonnet 4.5 | 200K | $3 / $15 | 最佳编码模型，OSWorld（电脑使用）得分 61.4% |
| Claude Haiku 4.5 | 200K | Fast tier | 近前沿性能，最快模型类别 |
| Claude Opus 4 / Sonnet 4 | 200K | $15/$75 (Opus) | Opus: SWE-bench 得分 72.5%，Sonnet 4 驱动 GitHub Copilot |

核心功能：扩展思考（Extended Thinking）结合工具调用、Computer Use、MCP（在此起源）、提示词缓存、Claude Code CLI，支持 AWS Bedrock 与 Google Vertex AI。[API文档](https://docs.anthropic.com/)

### Google (Gemini)

| Model | Context | Price (Input/Output per 1M tokens) | Key Feature |
|:------|:--------|:-----------------------------------|:------------|
| Gemini 3 Pro Preview | 1M | $2 / $12 | Google 最智能模型，已部署至 20亿+ Search 用户 |
| Gemini 2.5 Pro | 1M | $1.25 / $10 | 编码/Agentic 任务首选，推理模式 |
| Gemini 2.5 Flash / Flash-Lite | 1M | $0.30/$1.50 · $0.10/$0.40 | 性价比领先者 |

核心功能：Thinking（所有 2.5+ 模型内置）、Google Search 定位、代码执行、Live API（实时音视频）、上下文缓存。[Google AI Studio](https://ai.google.dev/)

### Meta (Llama)

| Model | Architecture | Context | Key Feature |
|:------|:------------|:--------|:------------|
| Llama 4 Scout | 109B MoE / 17B active | 10M | 适配单张 H100，多模态，开源权重 |
| Llama 4 Maverick | 400B MoE / 17B active, 128 experts | 1M | 超越 GPT-4o，开源权重 |
| Llama 3.3 70B | Dense | 128K | 性能对标 Llama 3.1 405B |

支持 25+ 云合作伙伴、Hugging Face 及推理 API。[Llama](https://ai.meta.com/llama/)

### 其他值得关注的提供商

| Provider | Description | Link |
|:---------|:-----------|:----:|
| **Mistral AI** | Mistral Large 3 (675B MoE)、Devstral 2、Ministra1 3。Apache 2.0。 | [Website](https://mistral.ai) |
| **DeepSeek** | V3.2 (671B MoE)、R1（推理模型，MIT 协议）。$0.15/$0.75 per 1M tokens。 | [Website](https://deepseek.com) |
| **xAI (Grok)** | Grok 4.1 Fast: 2M 上下文，$0.20/$0.50 per 1M tokens。 | [Website](https://x.ai) |
| **Cohere** | Command A (111B, 256K context)、Embed v4、Rerank 4.0。在 RAG 场景表现优异。 | [Website](https://cohere.com) |
| **Together AI** | 200+ 开源模型，延迟低于 100ms。 | [Website](https://together.ai) |
| **Groq** | LPU 硬件加速推理，约 300+ tokens/sec。 | [Website](https://groq.com) |
| **Fireworks AI** | 快速推理，符合 HIPAA + SOC2 合规标准。 | [Website](https://fireworks.ai) |
| **OpenRouter** | 统一 API，支持所有提供商的 300+ 模型。 | [Website](https://openrouter.ai) |
| **Cerebras** | 晶圆级芯片，提供最佳总响应时间。 | [Website](https://cerebras.ai) |
| **Perplexity AI** | 搜索增强型 API，支持引用标注。 | [Website](https://perplexity.ai) |
| **Amazon Bedrock** | 托管多模型服务，集成 Claude、Llama、Mistral、Cohere。 | [Website](https://aws.amazon.com/bedrock/) |
| **Hugging Face Inference** | 通过 API 访问开源模型。 | [Website](https://huggingface.co/docs/api-inference/index) |

---

## 数据集与基准测试
💾

### 主要基准测试（2024–2026）

| Name | Description | Link |
|:-----|:-----------|:----:|
| **Chatbot Arena / LM Arena** | 600万+ 用户投票，用于 Elo 评级 pairwise LLM 比较。人类偏好事实标准。 | [Website](https://lmarena.ai/) |
| **MMLU-Pro** | 覆盖 14 个领域的 12,000+ 研究生级别问题。NeurIPS 2024 Spotlight。 | [GitHub](https://github.com/TIGER-AI-Lab/MMLU-Pro) |
| **GPQA** | 448 道“Google-proof”STEM 题目；非专家验证者仅能达到 34% 正确率。 | [arXiv](https://arxiv.org/abs/2311.12022) |
| **SWE-bench Verified** | 人工验证的 500 任务子集，用于真实世界 GitHub Issue 解决评估。 | [Website](https://www.swebench.com/) |
| **SWE-bench Pro** | 覆盖 41 个专业仓库的 1,865 项任务；最佳模型得分仅约 23%。 | [Leaderboard](https://scale.com/leaderboard/swe_bench_pro_public) |
| **Humanity's Last Exam (HLE)** | 2,500 道专家审核题目；顶级 AI 得分仅约 10–30%。 | [Website](https://agi.safe.ai/) |
| **BigCodeBench** | 覆盖 7 个领域的 1,140 项编程任务；AI 达成率约 35.5%，人类为 97%。 | [Leaderboard](https://huggingface.co/spaces/bigcode/bigcodebench-leaderboard) |
| **LiveBench** | 防污染基准，题目频繁更新。 | [Paper](https://openreview.net/forum?id=sKYHBTAxVa) |
| **FrontierMath** | 研究级数学题；AI 仅能解决约 2%。 | Research |
| **ARC-AGI v2** | 抽象推理测试，衡量流体智力。 | Research |
| **IFEval** | 指令遵循评估，包含格式/内容约束。 | [arXiv](https://arxiv.org/abs/2311.07911) |
| **MLE-bench** | OpenAI 推出的 Kaggle 风格 ML 工程评估基准。 | [GitHub](https://github.com/openai/mle-bench) |
| **PaperBench** | 评估 AI 从零复现 20 篇 ICML 2024 论文的能力。 | [GitHub](https://github.com/openai/preparedness) |

### 排行榜与元基准测试

| Name | Description | Link |
|:-----|:-----------|:----:|
| **Hugging Face Open LLM Leaderboard v2** | 在 MMLU-Pro、GPQA、IFEval、MATH 上评估开源模型。 | [Leaderboard](https://huggingface.co/spaces/open-llm-leaderboard/open_llm_leaderboard) |
| **Artificial Analysis Intelligence Index v3** | 聚合 10 项评估指标。 | [Website](https://artificialanalysis.ai/) |
| **SEAL by Scale AI** | 托管 SWE-bench Pro 与 Agentic 评估。 | [Leaderboard](https://scale.com/leaderboard) |

### 提示词与指令数据集

| Name | Description | Link |
|:-----|:-----------|:----:|
| **P3 (Public Pool of Prompts)** | 用于训练 T0 及类似模型的 270+ NLP 任务提示模板。 | [HuggingFace](https://huggingface.co/datasets/bigscience/P3) |
| **System Prompts Dataset** | 944 个 Agent 工作流系统提示词模板（Daniel Rosehill, 2025年8月）。 | [HuggingFace](https://huggingface.co/datasets/danielrosehill/system_prompts) |
| **OpenAssistant Conversations (OASST)** | 35 种语言的 161,443 条消息，附带 461,292 次质量评分。 | [HuggingFace](https://huggingface.co/datasets/OpenAssistant/oasst1) |
| **UltraChat / UltraFeedback** | 大规模合成指令与偏好数据集，用于对齐训练。 | HuggingFace |
| **SoftAge Prompt Engineering Dataset** | 覆盖 10 个类别的 1,000 个多样化提示词，用于基准测试提示性能。 | HuggingFace |
| **Text Transformation Prompt Library** | 全面的文本转换提示词合集（2025年5月）。 | HuggingFace |
| **Writing Prompts** | ~30万个人类创作故事及对应的 r/WritingPrompts 提示词。 | [Kaggle](https://www.kaggle.com/datasets/ratthachat/writing-prompts) |
| **Midjourney Prompts** | 从 MidJourney 公开 Discord 爬取的文本提示与图片 URL。 | [HuggingFace](https://huggingface.co/datasets/succinctly/midjourney-prompts) |
| **CodeAlpaca-20k** | 20,000 个编程指令-输出对。 | [HuggingFace](https://huggingface.co/datasets/sahil2801/CodeAlpaca-20k) |
| **ProPEX-RAG** | 面向 RAG 工作流提示词优化的数据集。 | HuggingFace |
| **NanoBanana Trending Prompts** | 1,000+ 精选 AI 图像提示词，源自 X/Twitter，按互动量排名。 | [GitHub](https://github.com/jau123/nanobanana-trending-prompts) |

### 红队测试与对抗性数据集

| Name | Description | Link |
|:-----|:-----------|:----:|
| **HarmBench** | 覆盖标准、上下文、版权与多模态类别的 510 种有害行为。 | [Website](https://safetyprompts.com/) |
| **JailbreakBench** | 开源鲁棒性基准测试，包含 100 个越狱提示词。 | Research |
| **AgentHarm** | 覆盖 11 种危害类别的 110 项恶意 Agent 任务。 | [arXiv](https://arxiv.org/abs/2410.09024) |
| **DecodingTrust** | 评估 8 个视角下可信度的 243,877 条提示词。 | Research |
| **SafetyPrompts.com** | 聚合跟踪 50+ 安全/红队测试数据集的门户。 | [Website](https://safetyprompts.com/) |

---

## 模型
🧠

### 前沿模型（2025–2026）

| Model | Provider | Context | Key Strength |
|:------|:---------|:--------|:-------------|
| **GPT-5.2** | OpenAI | 400K | 通用智能，AIME 2025 满分（100%） |
| **Claude Opus 4.6** | Anthropic | 1M (beta) | 编码、Agentic 任务、扩展思考能力 |
| **Gemini 3 Pro** | Google | 1M | LMArena #1（~1500 Elo），多模态 |
| **Grok 4.1** | xAI | 2M | LMArena #2（1483 Elo），低幻觉率 |
| **Mistral Large 3** | Mistral AI | 256K | 最佳开源权重（675B MoE/41B active），Apache 2.0 |
| **DeepSeek-V3.2** | DeepSeek | 128K | 最佳性价比（671B MoE/37B active），MIT 协议 |
| **Llama 4 Maverick** | Meta | 1M | 超越 GPT-4o（400B MoE/17B active），开源权重 |

### 推理模型

| Model | Key Detail |
|:------|:-----------|
| **OpenAI o3 / o3-pro** | GPQA Diamond 得分 87.7%。原生工具调用。 |
| **OpenAI o4-mini** | 视觉推理能力出色，在其成本级别中 AIME 表现最佳。 |
| **DeepSeek-R1 / R1-0528** | 开源权重，RL 训练。AIME 2025 得分 87.5%。MIT 协议。 |
| **QwQ (Qwen with Questions)** | 32B 推理模型。Apache 2.0。性能对标 R1。 |
| **Gemini 2.5 Pro/Flash (Thinking)** | 内置推理能力，支持可配置思考预算。 |
| **Claude Extended Thinking** | 混合模式，提供可见的思维链与工具调用。 |
| **Phi-4 Reasoning / Plus** | 14B 推理模型，性能媲美更大规模模型。开源权重。 |
| **GPT-OSS-120B** | OpenAI 开源权重模型，支持 CoT。性能接近 o4-mini。Apache 2.0。 |

### 值得关注的开源模型

| Model | Provider | Key Detail |
|:------|:---------|:-----------|
| **Qwen3-235B-A22B** | Alibaba | 旗舰 MoE。推理/代码/多语言能力强。Apache 2.0。HuggingFace 下载量最高的家族之一。 |
| **Gemma 3** | Google | 270M 至 27B。多模态。128K 上下文。支持 140+ 语言。 |
| **OLMo 2/3** | Allen AI | 完全开源（数据、代码、权重、日志）。OLMo 2 32B 超越 GPT-3.5。Apache 2.0。 |
| **SmolLM3-3B** | Hugging Face | 性能超越 Llama-3.2-3B。双模式推理。128K 上下文。 |
| **Kimi K2** | Moonshot AI | 32B active。开源权重。专为编码/Agentic 场景优化。 |
| **Llama 4 Scout** | Meta | 109B MoE/17B active。10M token 上下文。适配单张 H100。 |

### 代码专用模型

| Model | Key Detail |
|:------|:-----------|
| **Qwen3-Coder (480B-A35B)** | SWE-bench 得分 69.6% —— 开源编程里程碑。256K 上下文。Apache 2.0。 |
| **Devstral 2 (123B)** | SWE-bench Verified 得分 72.2%。性价比是 Claude Sonnet 的 7 倍。 |
| **Codestral 25.01** | Mistral 代码模型。支持 80+ 语言。支持 Fill-in-the-Middle。 |
| **DeepSeek-Coder-V2** | 236B MoE / 21B active。支持 338 种编程语言。 |
| **Qwen 2.5-Coder** | 7B/32B。92 种编程语言。HumanEval 得分 88.4%。Apache 2.0。 |

### 奠基性模型（历史参考）

这些模型确立了关键概念，但在实际应用中大多已被取代：

| Model | Provider | Significance |
|:------|:---------|:-------------|
| GLM-130B | Tsinghua | 开源英中双语 LLM (2023) |
| Falcon 180B | TII | 大型开源生成模型 (2023) |
| Mixtral 8x7B | Mistral AI | 率先为开源模型引入 MoE 架构 (2023) |
| GPT-NeoX-20B | EleutherAI | 早期开源自回归 LLM |
| GPT-J-6B | EleutherAI | 早期开源因果语言模型 |

---

## AI 内容检测器
🔎

### 主流商业检测器

| Name | Accuracy | Key Feature | Link |
|:-----|:---------|:------------|:----:|
| **GPTZero** | 声称 99% | 1000万+ 用户，2025年 G2 排名第一。支持检测 GPT-4/5、Gemini、Claude、Llama。提供免费套餐。 | [Website](https://gptzero.me) |
| **Originality.ai** | 98–100%（同行评审） |  consistently rated most accurate. Combines AI detection + plagiarism + fact checking. From $14.95/month. | [Website](https://originality.ai) |
| **Turnitin AI Detection** | 未修改 AI 文本检测率 98%+ | 学术界主导。2025年8月推出 AI 绕过/人性化检测功能。机构授权许可。 | [Website](https://www.turnitin.com/solutions/topics/ai-writing/) |
| **Copyleaks** | 声称 99%+ | 企业级工具，支持 30+ 语言 AI 检测。集成 LMS。 | [Website](https://copyleaks.com) |
| **Winston AI** | 声称 99.98% | OCR 扫描文档检测、AI 图像/深度伪造检测。支持 11 种语言。 | [Website](https://gowinston.ai) |
| **Pangram Labs** | 99.3% (COLING 2025) | COLING 2025 Shared Task 得分最高。“人性化”文本 TPR 达 100%，对抗鲁棒性 97.7%。 | [Website](https://www.pangram.com) |

### 免费与研究级检测器

| Name | Description | Link |
|:-----|:-----------|:----:|
| **Binoculars** | 开源研究检测器，利用两个 LLM 之间的交叉困惑度进行判断。 | [arXiv](https://arxiv.org/abs/2401.12070) |
| **DetectGPT / Fast-DetectGPT** | 统计方法，比较原始文本与扰动文本的对数概率差异。 | [arXiv](https://arxiv.org/abs/2301.11305) |
| **Openai Detector** | AI 分类器（用于标识 AI 生成文本的 Python 包装器）。 | [[GitHub]](https://github.com/promptslab/openai-detector) |
| **Sapling AI Detector** | 免费浏览器检测器（上限 2,000 字符）。部分研究中准确率达 97%。 | [Website](https://sapling.ai/) |
| **QuillBot AI Detector** | 免费，无需注册。 | [Website](https://quillbot.com/ai-content-detector) |
| **Writer AI Content Detector** | 免费工具，提供彩色编码结果。 | [Website](https://writer.com/ai-content-detector/) |
| **ZeroGPT** | 流行免费检测器，在多篇学术研究中得到评估。 | [Website](https://www.zerogpt.com/) |

### 水印方案

| Name | Description | Link |
|:-----|:-----------|:----:|
| **SynthID (Google DeepMind)** | 通过统计 token 采样为 AI 文本、图像与音频添加水印。已部署于 Google 产品中。 | [Website](https://deepmind.google/technologies/synthid/) |
| **OpenAI Text Watermarking** | 2025年仍处于实验阶段。研究表明其存在脆弱性风险。 | Experimental |

**重要提示：** 目前没有任何检测器声称达到 100% 准确率。混合人类/AI 文本最难检测（准确率约 50–70%）。对抗鲁棒性差异较大。AI 检测市场预计将从 2025 年的 ~23亿美元增长至 2035 年的 150亿美元。

---

## 书籍
📖

### 提示词工程

| Title | Author(s) | Publisher | Year |
|:------|:----------|:---------|:-----|
| **Prompt Engineering for LLMs** | John Berryman & Albert Ziegler | O'Reilly | 2024 |
| **Prompt Engineering for Generative AI** | James Phoenix & Mike Taylor | O'Reilly | 2024 |
| **Prompt Engineering for LLMs** | Thomas R. Caldwell | Independent | 2025 |

### LLM 应用开发

| Title | Author(s) | Publisher | Year |
|:------|:----------|:---------|:-----|
| **AI Engineering: Building Applications with Foundation Models** | Chip Huyen | O'Reilly | 2025 |
| **Build a Large Language Model (From Scratch)** | Sebastian Raschka | Manning | 2024 |
| **Building LLMs for Production** | Louis-François Bouchard & Louie Peters | O'Reilly | 2024 |
| **LLM Engineer's Handbook** | Paul Iusztin & Maxime Labonne | Packt | 2024 |
| **The Hundred-Page Language Models Book** | Andriy Burkov | Self-Published | 2025 |

### AI Agent

| Title | Author(s) | Publisher | Year |
|:------|:----------|:---------|:-----|
| **Building Applications with AI Agents** | Michael Albada | O'Reilly | 2025 |
| **AI Agents and Applications** | Roberto Infante | Manning | 2025 |
| **AI Agents in Action** | Micheal Lanham | Manning | 2025 |

### 生产、可靠性与安全

| Title | Author(s) | Publisher | Year |
|:------|:----------|:---------|:-----|
| **LLMs in Production** | Christopher Brousseau & Matthew Sharp | Manning | 2025 |
| **Building Reliable AI Systems** | Rush Shahani | Manning | 2025 |
| **The Developer's Playbook for LLM Security** | Steve Wilson | O'Reilly | 2024 |

---

## 课程
👩‍🏫

### 免费短课程

- [面向开发者的 ChatGPT 提示词工程](https://www.deeplearning.ai/short-courses/chatgpt-prompt-engineering-for-developers/) — Andrew Ng 与 OpenAI Isa Fulford 联合授课。基础入门首选。(DeepLearning.AI)
- [使用 ChatGPT API 构建系统](https://www.deeplearning.ai/short-courses/building-systems-with-chatgpt/) — 面向生产的多步 LLM 系统设计。(DeepLearning.AI)
- [LangGraph 中的 AI Agent](https://www.deeplearning.ai/short-courses/ai-agents-in-langgraph/) — 结合工具使用与研究型 Agent 的 Agentic 数据流。(DeepLearning.AI)
- [基于 LlamaIndex 构建 Agentic RAG](https://www.deeplearning.ai/short-courses/building-agentic-rag-with-llamaindex/) — RAG 研究型 Agent 架构设计。(DeepLearning.AI)
- [LangChain 中的函数、工具与 Agent](https://www.deeplearning.ai/short-courses/functions-tools-agents-langchain/) — 函数调用与 Agent 构建。(DeepLearning.AI)
- [视觉模型提示词工程](https://www.deeplearning.ai/short-courses/prompt-engineering-for-vision-models/) — 视觉提示技巧。(DeepLearning.AI)

### 大学与平台课程

- [提示词工程专项证书 (Vanderbilt)](https://www.coursera.org/specializations/prompt-engineering) — Jules White 博士主讲的 3 门系列课程，覆盖基础到高级 PE。(Coursera)
- [使用 LLM 的生成式 AI (DeepLearning.AI + AWS)](https://www.coursera.org/learn/generative-ai-with-llms) — LLM 生命周期、Transformer、RLHF、部署。(Coursera)
- [Stanford CS336: 从零构建语言模型](https://cs336.stanford.edu/) — 端到端构建 LLM。(Stanford, 2024–2026)
- [MIT 6.S191: 深度学习导论](https://introtodeeplearning.com/) — 年度课程，涵盖 LLM 与生成式 AI。(MIT, 2024–2026)
- [AI 提示词工程完整训练营](https://www.udemy.com/course/prompt-engineering-for-ai/) — 覆盖 GPT-5、DSPy、LangGraph、Agent 架构。58K+ 评分。(Udemy, 2026年2月更新)

### 免费平台课程

- [Google Prompting Essentials](https://grow.google/prompting-essentials/) — 5步提示词设计、元提示、Gemini。总时长不足 6 小时。
- [Microsoft Azure AI Fundamentals: Generative AI](https://learn.microsoft.com/en-us/training/paths/introduction-generative-ai/) — 免费学习路径，涵盖 LLM、提示词、Agent、Azure OpenAI。
- [Hugging Face LLM Course](https://huggingface.co/learn/llm-course/chapter1/1) — 社区驱动课程，覆盖 Transformer、微调与推理模型构建。
- [Hugging Face AI Agents Course](https://huggingface.co/learn) — Agent 理论到实践。10万+ 注册学生。

### Learn Prompting Courses

- [ChatGPT for Everyone](https://learnprompting.org/courses/chatgpt-for-everyone)
- [Introduction to Prompt Engineering](https://learnprompting.org/courses/introduction_to_prompt_engineering)
- [Advanced Prompt Engineering](https://learnprompting.org/courses/advanced-prompt-engineering)
- [Introduction to Prompt Hacking](https://learnprompting.org/courses/intro-to-prompt-hacking)
- [Advanced Prompt Hacking](https://learnprompting.org/courses/advanced-prompt-hacking)
- [Introduction to Generative AI Agents for Business Professionals](https://learnprompting.org/courses/introduction-to-agents)
- [AI Safety](https://learnprompting.org/courses/ai-safety)

---

## 教程与指南
📚

### 官方提供商指南

- [OpenAI 提示词工程指南](https://platform.openai.com/docs/guides/prompt-engineering) — 全面覆盖，含 GPT-4.1/5 提示、推理模型、结构化输出、Agentic 工作流。持续更新。
- [OpenAI GPT-4.1 Prompting Guide](https://cookbook.openai.com/articles/gpt-4-1-prompting-guide) [2025] — 类 Agent 结构化提示设计：目标持久化、工具集成、长上下文处理。
- [Anthropic 提示词工程概述](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview) — 迭代式提示设计、XML 标签、思维链、角色分配。内置提示生成器。
- [Anthropic Claude 4 最佳实践](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/claude-4-best-practices) [2025–2026] — 并行工具执行、思考能力、图像处理。
- [Anthropic：AI Agent 的高效上下文工程](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) [2025] — 从提示词工程到上下文工程的演进：Agent 状态、记忆、工具与 MCP。
- [Google Gemini 提示策略](https://ai.google.dev/docs/prompt_best_practices) — 通过 Vertex AI 和 AI Studio 为 Gemini 提供多模态提示支持。
- [Microsoft Azure AI Studio 中的提示词工程](https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/prompt-engineering) — 工具调用、函数设计、少样本提示、提示链。

### 社区与独立指南

- [Prompt Engineering Guide (DAIR.AI / promptingguide.ai)](https://www.promptingguide.ai/) — 最全面的开源指南。18+ 种技巧、模型专属指南、研究论文。300万+学习者。现已包含上下文工程内容。
- [Learn Prompting (learnprompting.org)](https://learnprompting.org/) — 结构化免费平台。涵盖初级到高级 PE、AI 安全与 HackAPrompt 竞赛。
- [IBM 2026 提示词工程指南](https://www.ibm.com/think/prompt-engineering) [2026] — 精选工具、教程、真实案例，附带 Python 代码示例。
- [Anthropic Interactive Tutorial](https://github.com/anthropics/prompt-eng-interactive-tutorial) — 9章 Jupyter Notebook 课程，含动手练习。
- [Lilian Weng's Prompt Engineering Guide](https://lilianweng.github.io/posts/2023-03-15-prompt-engineering/) [2023] — OpenAI 研究员撰写的备受推崇的技术博客。
- [Google 提示词工程指南（68页 PDF）](https://www.reddit.com/r/PromptEngineering/comments/1kggmh0/google_dropped_a_68page_prompt_engineering_guide/) [2025] — Gemini 内部最佳实践指南，含具体模式示例。
- [DigitalOcean：提示词工程最佳实践](https://www.digitalocean.com/resources/articles/prompt-engineering-best-practices) [2025] — 更新版指南总结技巧：少样本、思维链、角色提示等。
- [Aakash Gupta: Prompt Engineering in 2025](https://news.aakashg.com) [2025] — 结合在 OpenAI、Shopify 与 Google 的实战经验提供的实用指南。
- [Best practices for prompt engineering with OpenAI API](https://help.openai.com/en/articles/6654000-best-practices-for-prompt-engineering-with-openai-api) — OpenAI 官方入门最佳实践。
- [OpenAI Cookbook](https://github.com/openai/openai-cookbook) — 函数调用、RAG、评估与复杂工作流的官方示例。
- [Microsoft Prompt Engineering Docs](https://microsoft.github.io/prompt-engineering) — Microsoft 开源提示词工程资源。
- [DALLE Prompt Book](https://dallery.gallery/the-dalle-2-prompt-book) — 文生图提示可视化指南。
- [Best 100+ Stable Diffusion Prompts](https://mpost.io/best-100-stable-diffusion-prompts-the-most-beautiful-ai-text-to-image-prompts) — 社区精选图像生成提示词。
- [Vibe Engineering (Manning)](https://www.manning.com/books/vibe-engineering) — Tomasz Lelek & Artur Skowronski 著，讲述如何通过自然语言提示构建软件。

---

## 视频
🎥

- [Andrej Karpathy: "Deep Dive into LLMs" & "How I Use LLMs"](https://www.youtube.com/@AndrejKarpathy) [2024–2025] — 2024–2025 最具影响力的 AI 视频之一。全面技术深入解析结合实用使用模式。
- [Karpathy: "Software in the Era of AI" (YC AI Startup School)](https://karpathy.ai/) [2025] — 提出“Vibe Coding”（2025年2月）并推崇“上下文工程”（2025年6月）。
- [Karpathy: Neural Networks: Zero to Hero](https://www.youtube.com/@AndrejKarpathy) [2023–2024] — 完整讲座系列，从反向传播构建至 GPT。
- [3Blue1Brown: Neural Networks Series](https://www.youtube.com/@3blue1brown) [Updated 2024] — Transformer 与注意力机制的经典动画可视化解释。700万+订阅者。
- [AI Explained](https://www.youtube.com/@aiexplained-official) [2024–2025] — 长视频深度解析论文、模型能力与 PE 进展。
- [Sam Witteveen](https://www.youtube.com/@samwitteveen) [2024–2025] — 提示词工程、LangChain、RAG 与 Agent 的实用教程。
- [Matthew Berman](https://www.youtube.com/@matthew_berman) [2024–2025] — 热门频道，覆盖模型发布与 LLM 实用使用技巧。60万+订阅者。
- [DeepLearning.AI YouTube](https://www.youtube.com/@Deeplearningai) [2024–2026] — 结构化课程、预览视频及 Andrew Ng 关于 Agent 与 AI 职业发展的演讲。
- [Lex Fridman Podcast (AI Episodes)](https://www.youtube.com/@lexfridman) [2024–2025] — 长访谈，对话 Altman、Hinton、Amodei 等探讨 LLM、提示与安全。
- [ICSE 2025: AIware Prompt Engineering Tutorial](https://conf.researchr.org/details/icse-2025/icse-2025-tutorials/) [2025] — 会议教程，覆盖提示模式、脆弱性、反模式与优化 DSL。
- [CMU Advanced NLP 2022: Prompting](https://youtube.com/watch?v=5ef83Wljm-M) — 提示方法的奠基性学术讲座。
- [ChatGPT: 5 Prompt Engineering Secrets For Beginners](https://www.youtube.com/watch?v=2zg3V66-Fzs) — 面向初学者的入门介绍。

---

## 社区
🤝

### Discord Servers

- [Learn Prompting](https://learnprompting.org/discord) — 4万+成员。最大 PE Discord，提供课程、黑客松与 HackAPrompt 竞赛。
- [PromptsLab Discord](https://discord.gg/m88xfYMbK6) - Community
- [Midjourney](https://discord.gg/midjourney) — 100万+成员。文生图提示分享主阵地。
- [OpenAI Discord](https://discord.gg/openai) — 官方社区，设有 GPTs、Sora、DALL-E 与 API 帮助频道。
- [Anthropic Discord](https://discord.gg/anthropic) — Claude 官方社区，用于 AI 开发协作。
- [Hugging Face Discord](https://discord.gg/huggingface) — 模型讨论、库支持与社区活动。
- [FlowGPT](https://flowgpt.com/) — 3.3万+成员。覆盖 ChatGPT、DALL-E、Stable Diffusion、Claude 的 10万+提示词。

### Reddit

- [r/PromptEngineering](https://reddit.com/r/PromptEngineering) — 专注提示词创作技巧与讨论的子版块。
- [r/ChatGPT](https://reddit.com/r/ChatGPT) — 1000万+成员。ChatGPT 用户与提示分享主阵地。
- [r/LocalLLaMA](https://reddit.com/r/LocalLLaMA) — 高度技术化社区，专注本地运行开源 LLM。
- [r/ClaudeAI](https://reddit.com/r/ClaudeAI) — Anthropic Claude 社区：提示分享、API 技巧与模型对比。
- [r/MachineLearning](https://reddit.com/r/MachineLearning) — 学术导向的 ML 研究讨论。
- [r/OpenAI](https://reddit.com/r/OpenAI) — OpenAI 产品与 API 讨论。
- [r/StableDiffusion](https://reddit.com/r/StableDiffusion) — 45万+成员，专注 AI 绘画提示与工作流。
- [r/ChatGPTPromptGenius](https://reddit.com/r/ChatGPTPromptGenius) — 3.5万+成员分享与优化提示词。


### Forums and Platforms

- [OpenAI Developer Community](https://community.openai.com/) — API 帮助、最佳实践与项目分享的官方论坛。
- [Hugging Face Community](https://huggingface.co/) — 开源 AI 协作枢纽。
- [DeepLearning.AI Community](https://community.deeplearning.ai/) — 学员讨论课程与 AI 职业发展的论坛。
- [LessWrong](https://www.lesswrong.com/) — 深入探讨 AI 能力与安全的技术文章平台。
- [AI Alignment Forum](https://www.alignmentforum.org/) — 专注对齐研究的专项论坛。
- [CivitAI](https://civitai.com/) — 生成式 AI 创作者平台，分享模型、LoRAs 与提示词。

### GitHub Organizations

- [LangChain](https://github.com/langchain-ai) — 开源 LLM 应用框架。10万+ Stars。
- [Promptslab](https://github.com/promptslab)  — Generative Models | Prompt-Engineering | LLMs 
- [Hugging Face](https://github.com/huggingface) — 核心枢纽：Transformers、Diffusers、Datasets、TRL。
- [DSPy (Stanford NLP)](https://github.com/stanfordnlp/dspy) — 系统化提示词优化社区持续壮大。
- [OpenAI](https://github.com/openai) — 开源模型、基准测试与工具。

---

<!-- AUTORESEARCH-START -->
## 🔬 自主研究与自进化 Agent
> Auto-synced from [awesome-autoresearch](https://github.com/alvinunreal/awesome-autoresearch) · Last synced: 2026-06-01

### 通用型后代项目

- [kayba-ai/recursive-improve](https://github.com/kayba-ai/recursive-improve) — 递归自进化框架，Agent 捕获执行轨迹、分析失败模式，并通过保留或回滚（keep-or-revert）评估机制应用针对性修复。
- [vukrosic/auto-research](https://github.com/vukrosic/auto-research) — 面向开源自主 AI 实验室的纯文档控制平面——基于文件的操作系统模型，支持人类指令与 Agent 执行。
- [uditgoenka/autoresearch](https://github.com/uditgoenka/autoresearch) — Claude Code 技能，将自动研究泛化为可复用循环，适用于软件、文档、安全、发布、调试等可量化目标。
- [leo-lilinxiao/codex-autoresearch](https://github.com/leo-lilinxiao/codex-autoresearch) — Codex 原生自动研究技能，支持简历解析、跨运行经验积累、可选并行实验及模式特定工作流。
- [SeeleAI/Thoth](https://github.com/SeeleAI/Thoth) — 仪表板优先的 Claude Code 与 Codex 运行时环境，用于自动研究；具备持久化运行、锁定任务项、可见账本与可审查裁决功能。
- [supratikpm/gemini-autoresearch](https://github.com/supratikpm/gemini-autoresearch) — Gemini CLI 技能，将自动研究泛化为任意可量化目标。Gemini 原生：在循环内使用 Google Search 定位作为实时验证源，支持通过 `--yolo --prompt` 实现真正的无头夜间模式及 1M token 上下文。亦可通过 `.agents/skills/` 在 Antigravity IDE 中使用。
- [davebcn87/pi-autoresearch](https://github.com/davebcn87/pi-autoresearch) — `pi` 扩展与仪表板，支持持久化实验循环、实时指标、置信度追踪及可恢复的自动研究会话。
- [drivelineresearch/autoresearch-claude-code](https://github.com/drivelineresearch/autoresearch-claude-code) — `pi-autoresearch` 的 Claude Code 插件/端口，提供清晰的实验循环工作流与具体的生物力学案例研究。
- [greyhaven-ai/autocontext](https://github.com/greyhaven-ai/autocontext) — 闭环控制平面用于重复 Agent 改进，包含评估、持久化知识、分阶段验证及可选蒸馏至低成本本地运行时环境。
- [jmilinovich/goal-md](https://github.com/jmilinovich/goal-md) — 将自动研究泛化为 `GOAL.md` 模式，适用于要求 Agent 先构建可量化适应度函数再进行优化的仓库场景。
- [james-s-tayler/lazy-developer](https://github.com/james-s-tayler/lazy-developer) — Claude Code 技能，通过 GOAL.md 作为引擎编排按优先级排序的优化目标序列（覆盖率、测试速度、构建速度、复杂度、LOC、性能）。支持独立运行与 Ralph Mode 多实例执行。
- [mutable-state-inc/autoresearch-at-home](https://github.com/mutable-state-inc/autoresearch-at-home) — 上游 autoresearch 的合作分支，增加实验认领、最佳配置同步、假设交换及单 GPU Agent 间的蜂群式协调功能。
- [zkarimi22/autoresearch-anything](https://github.com/zkarimi22/autoresearch-anything) — 将自动研究泛化为**任意可量化指标**——系统提示词、API 性能、落地页、测试套件、配置调优、SQL 查询。“凡可测量，皆可优化。”
- [Entrpi/autoresearch-everywhere](https://github.com/Entrpi/autoresearch-everywhere) — 跨平台扩展，自动检测硬件配置并启动循环。作为 autoresearch 的“胶水与泛化”模块。
- [ShengranHu/ADAS](https://github.com/ShengranHu/ADAS) — **智能体系统自动化设计** —— ICLR 2025。元 Agent 通过编程自行发明新颖的 Agent 架构。
- [MaximeRobeyns/self_improving_coding_agent](https://github.com/MaximeRobeyns/self_improving_coding_agent) — **SICA**: 自进化编码 Agent，可编辑自身代码库。ICLR 2025 Workshop 论文，展示在编程基准测试中的脚手架级自改进能力。
- [peterskoett/self-improving-agent](https://github.com/peterskoett/self-improving-agent) — 具备反思与元学习循环的替代架构自进化 Agent。
- [metauto-ai/HGM](https://github.com/metauto-ai/HGM) — **Huxley-Gödel Machine** 编码 Agent —— 通过元级优化将自改进应用于 SWE-bench 性能。
- [gepa-ai/gepa](https://github.com/gepa-ai/gepa) — **GEPA (Genetic-Pareto)** —— ICLR 2026 Oral。反思式提示词进化，在基准测试中超越 RL（GRPO）。使用自然语言反思优化任意文本参数与指标。
- [sentient-agi/EvoSkill](https://github.com/sentient-agi/EvoSkill) — 编码 Agent 自动技能发现：从失败轨迹中演化可复用技能与提示词，支持 Claude Code、Codex CLI、OpenCode、OpenHands 与 Goose。
- [MrTsepa/autoevolve](https://github.com/MrTsepa/autoevolve) — GEPA 启发的自博弈自动研究：变异代码策略、头对头评估、使用 Elo/Bradley-Terry 评级、从帕累托前沿分支。Agent 读取匹配轨迹以定位目标突变点。可作为 Claude Code 技能运行。
- [HKUDS/ClawTeam](https://github.com/HKUDS/ClawTeam) — 自动研究的 Agent 蜂群智能——并行生成 GPU 研究方向，跨 Agent 分配任务并聚合结果。
- [Orchestra-Research/AI-Research-SKILLs](https://github.com/Orchestra-Research/AI-Research-SKILLs) — 综合技能库，包含具双循环架构（内部优化 + 外部合成）的自动研究编排能力。
- [WecoAI/aideml](https://github.com/WecoAI/aideml) — **AIDE**: 树搜索驱动的 ML 工程 Agent，通过迭代代码生成与评估自主提升模型性能。
- [weco.ai](https://weco.ai) — **Weco**: AIDE 云端平台，提供可观测性、实验追踪与管理型运行环境——将自动研究循环带入生产级应用。

### 研究型 Agent 系统

- [aiming-lab/AutoResearchClaw](https://github.com/aiming-lab/AutoResearchClaw) — 端到端研究流水线，将主题转化为文献综述、实验、分析、同行评审与论文草稿；范围超出自动研究范畴，但明确属于同一技术谱系。
- [OpenRaiser/NanoResearch](https://github.com/OpenRaiser/NanoResearch) — 端到端自主研究引擎，规划实验、生成代码、在本地或 SLURM 上运行作业、分析真实结果并基于输出撰写论文。
- [kaust-ark/ARK](https://github.com/kaust-ark/ARK) — **ARK (Automatic Research Kit)**: 想法 + 会议 → 论文流水线，编排 6 个 Agent——提案分析、文献检索、Slurm 实验、LaTeX 起草、迭代同行评审。支持 CLI、Web 仪表板或 Telegram 控制。
- [wanshuiyin/Auto-claude-code-research-in-sleep](https://github.com/wanshuiyin/Auto-claude-code-research-in-sleep) — 面向 Claude Code 及其他 Agent 的 Markdown 优先研究工作流，聚焦自主文献综述、实验、论文迭代与跨模型批判。
- [skyllwt/AutoSci](https://github.com/skyllwt/AutoSci) — 基于 Claude Code 构建的 Wiki 中心全生命周期研究平台，实现 Karpathy 的 LLM-Wiki 愿景。20+ 技能覆盖完整循环：摄入 → 构思 → 新颖性检查 → 实验设计/运行/评估 → 论文撰写。研究状态存储在结构化知识 Wiki 与交互式图谱中。
- [Sibyl-Research-Team/AutoResearch-SibylSystem](https://github.com/Sibyl-Research-Team/AutoResearch-SibylSystem) — 完全自主的 AI 科学家，基于 Claude Code 构建，具备明确的 AutoResearch 谱系、多 Agent 研究迭代、GPU 实验执行与自进化外循环。
- [eimenhmdt/autoresearcher](https://github.com/eimenhmdt/autoresearcher) — 早期开源包，用于自动化科学工作流，目前聚焦文献综述生成，并致力于向更广泛的自主研究演进。
- [hyperspaceai/agi](https://github.com/hyperspaceai/agi) — 分布式点对点研究网络，自主 Agent 运行实验、交换发现结果、维护 CRDT 排行榜并将结果归档至 GitHub，覆盖多个研究领域。
- [Human-Agent-Society/CORAL](https://github.com/Human-Agent-Society/CORAL) — **CORAL**: 面向开放发现的自主多 Agent 进化系统 ([arXiv:2604.01658](https://arxiv.org/abs/2604.01658))。具备共享持久记忆、异步执行与心跳干预机制的长运行 Agent；在 10 项数学/算法/系统任务上达到 SOTA。
- [SakanaAI/AI-Scientist](https://github.com/SakanaAI/AI-Scientist) — **The AI Scientist**: 首个全自动科学发现综合系统。从想法生成到论文撰写，仅需极少人工干预。
- [SakanaAI/AI-Scientist-v2](https://github.com/SakanaAI/AI-Scientist-v2) — 基于 Agentic 树搜索的 Workshop 级自动科学发现。移除 v1 模板依赖，跨研究领域泛化能力更强。
- [AweAI-Team/AiScientist](https://github.com/AweAI-Team/AiScientist) — **AiScientist**: 长周期 ML 研究实验室，采用分层编排与 File-as-Bus 协调机制——工作区文件作为持久化系统记录。驱动自主论文复现（PaperBench）与竞赛式 MLE-Bench 迭代循环，受限于固定计算/时间预算。([arXiv 2604.13018](https://arxiv.org/abs/2604.13018))
- [HKUDS/AI-Researcher](https://github.com/HKUDS/AI-Researcher) — NeurIPS 2025 论文。全端到端研究自动化：假设 → 实验 → 手稿 → 同行评审。生产版位于 [novix.science](https://novix.science/chat)。
- [openags/Auto-Research](https://github.com/openags/Auto-Research) — **OpenAGS**: 编排 AI Agent 团队完成全研究生命周期——文献综述、假设生成、实验、手稿撰写与同行评审。
- [SamuelSchmidgall/AgentLaboratory](https://github.com/SamuelSchmidgall/AgentLaboratory) — 端到端自主研究工作流：想法 → 文献综述 → 实验 → 报告。支持全自动与协作者模式。
- [AgentRxiv](https://agentrxiv.github.io/) — 协作式自主研究框架，Agent 实验室共享预印本服务器以迭代构建彼此工作成果。
- [JinheonBaek/ResearchAgent](https://github.com/JinheonBaek/ResearchAgent) — 基于 LLM 的科学文献迭代研究想法生成。多 Agent 评审与反馈循环。
- [du-nlp-lab/MLR-Copilot](https://github.com/du-nlp-lab/MLR-Copilot) — 自主 ML 研究框架——生成想法、实现实验、分析结果。
- [MASWorks/ML-Agent](https://github.com/MASWorks/ML-Agent) — 强化 LLM Agent 用于自主 ML 工程。通过试错学习以提升模型性能。
- [PouriaRouzrokh/LatteReview](https://github.com/PouriaRouzrokh/LatteReview) — 低代码 Python 包，通过 AI Agent 实现**自动化系统文献综述**。
- [LitLLM/LitLLM](https://github.com/LitLLM/LitLLM) — AI 驱动文献综述助手，利用 RAG 为学术写作生成准确、结构良好的相关工作章节。
- [Agent Laboratory](https://agentlaboratory.github.io/) — 三阶段研究流水线：文献综述 → 实验 → 报告撰写，各阶段配备专用 Agent。
- [WecoAI/aideml](https://github.com/WecoAI/aideml) — **AIDE**: AI 驱动探索——基于树搜索的 ML 工程 Agent，自动化实验设计、代码生成与评估。将 ML 工程视为针对任意指标的代码优化过程。

### 平台移植版与硬件分支版

- [gianfrancopiana/openclaw-autoresearch](https://github.com/gianfrancopiana/openclaw-autoresearch) — pi-autoresearch 的 OpenClaw 移植版；面向任意优化目标的自主实验循环，附带统计置信度评分。
- [miolini/autoresearch-macos](https://github.com/miolini/autoresearch-macos) — 广泛采用的 macOS 分支，适配 Apple Silicon / MPS，同时保留原始循环结构。
- [trevin-creator/autoresearch-mlx](https://github.com/trevin-creator/autoresearch-mlx) — MLX 原生 Apple Silicon 移植版，保持上游固定预算 `val_bpb` 循环，彻底移除 PyTorch/CUDA 依赖。
- [jsegov/autoresearch-win-rtx](https://github.com/jsegov/autoresearch-win-rtx) — Windows 原生 RTX 分支，聚焦消费级 NVIDIA GPU，提供明确的显存下限与桌面端部署路径。
- [iii-hq/n-autoresearch](https://github.com/iii-hq/n-autoresearch) — 多 GPU 自动研究基础设施，具备结构化实验追踪、自适应搜索策略、崩溃恢复及围绕经典 `train.py` 循环的可查询编排能力。
- [lucasgelfond/autoresearch-webgpu](https://github.com/lucasgelfond/autoresearch-webgpu) — 浏览器/WebGPU 移植版，允许 Agent 在浏览器内生成训练代码、运行实验并将结果反馈至循环中，无需 Python 环境。
- [tonitangpotato/autoresearch-engram](https://github.com/tonitangpotato/autoresearch-engram) — 带有**持久认知记忆**的分支版本——通过频率加权检索跨会话知识，提升实验连续性。
- **Colab/Kaggle T4 移植版** - 适配免费 T4 GPU（Google Colab / Kaggle），零成本且无需本地设置。关键改动：Flash Attention 3 → PyTorch SDPA，移除仅 H100 依赖的内核。([上游 Issue #208](https://github.com/karpathy/autoresearch/issues/208))
- [ArmanJR-Lab/autoautoresearch](https://github.com/ArmanJR-Lab/autoautoresearch) — Jetson AGX Orin 移植版，内置**导演（director）**——一个 Go 二进制程序，作为“创意总监”向循环注入新颖性（arxiv 论文 + DeepSeek Reasoner）以跳出局部最优。包含多实验对比（基线 vs 导演引导）及详细停滞分析。

### 领域特定适配版

- [mattprusak/autoresearch-genealogy](https://github.com/mattprusak/autoresearch-genealogy) — 将自动研究模式应用于家谱研究，使用结构化提示词、档案指南、来源核查与档案工作流迭代扩展并验证家族历史研究。
- [ArchishmanSengupta/autovoiceevals](https://github.com/ArchishmanSengupta/autovoiceevals) — 结合对抗性呼叫者与保留或回滚提示词编辑，强化 Vapi、Smallest AI 与 ElevenLabs 上的语音 AI Agent。
- [chrisworsey55/atlas-gic](https://github.com/chrisworsey55/atlas-gic) — 将自动研究保留或回滚循环应用于交易 Agent，针对滚动夏普比率而非模型损失优化提示词与投资组合编排。
- [RightNow-AI/autokernel](https://github.com/RightNow-AI/autokernel) — 将自动研究循环应用于 GPU Kernel 优化：分析瓶颈、编辑单个 Kernel、基准测试、保留或回滚，循环执行。
- [Agent-Analytics/autoresearch-growth](https://github.com/Agent-Analytics/autoresearch-growth) — 将自动研究应用于落地页定位与 A/B 测试候选方案，利用分析快照与实测实验结果引导后续轮次。
- [Rkcr7/autoresearch-sudoku](https://github.com/Rkcr7/autoresearch-sudoku) — 增强型自动研究工作流，AI Agent 迭代重写并基准测试 Rust 数独求解器，最终在困难基准集上击败领先的人类构建求解器。
- [jeongph/autospec](https://github.com/jeongph/autospec) — 读取自然语言业务规则并通过保留或回滚循环自主构建 Spring Boot 服务及测试用例。使用 Gradle build + JUnit XML 评估。5 个循环内从 119 行骨架扩展至 950 行代码。

### 评估与基准测试

- [snap-stanford/MLAgentBench](https://github.com/snap-stanford/MLAgentBench) — 用于在 ML 实验任务上评估 AI Agent 的基准套件。涵盖 CIFAR-10 至 BabyLM 等 13 项任务。
- [openai/mle-bench](https://github.com/openai/mle-bench) — OpenAI 推出的基准测试，衡量 AI Agent 在 ML 工程中的表现能力。
- [chchenhui/mlrbench](https://github.com/chchenhui/mlrbench) — MLR-Bench: 评估 AI Agent 在开放式 ML 研究中的能力。涵盖 NeurIPS/ICLR/ICML Workshop 的 201 项任务。
- [gersteinlab/ML-Bench](https://github.com/gersteinlab/ML-Bench) — 评估 LLMs 与 Agent 在仓库级代码上的 ML 任务表现。
- [THUDM/AgentBench](https://github.com/THUDM/AgentBench) — 覆盖 8 个独立环境的 LLM-as-Agent 综合基准测试。ICLR 2024。

### 相关资源

- [ai-agents-2030/awesome-deep-research-agent](https://github.com/ai-agents-2030/awesome-deep-research-agent) — 深度研究 Agent 论文与系统的精选列表。
- [YoungDubbyDu/LLM-Agent-Optimization](https://github.com/YoungDubbyDu/LLM-Agent-Optimization) — LLM Agent 优化方法相关论文。
- [VoltAgent/awesome-ai-agent-papers](https://github.com/VoltAgent/awesome-ai-agent-papers) — 2026年精选 AI Agent 论文——涵盖 Agent 工程、记忆、评估、工作流与自主系统。
- [masamasa59/ai-agent-papers](https://github.com/masamasa59/ai-agent-papers) — 通过自动化 arxiv 搜索并人工筛选，每两周更新的 AI Agent 研究论文。
- [tmgthb/Autonomous-Agents](https://github.com/tmgthb/Autonomous-Agents) — 自主 Agent 研究论文，每日更新。
- [HKUST-KnowComp/Awesome-LLM-Scientific-Discovery](https://github.com/HKUST-KnowComp/Awesome-LLM-Scientific-Discovery) — EMNLP 2025 LLMs in Scientific Discovery 综述。
- [openags/Awesome-AI-Scientist-Papers](https://github.com/openags/Awesome-AI-Scientist-Papers) — AI Scientist / Robot Scientist 论文合集。
- [agenticscience.github.io](https://agenticscience.github.io/) — 综述：《从 AI for Science 到 Agentic Science：自主科学发现综述》。
- [dspy.ai/GEPA](https://dspy.ai/api/optimizers/GEPA/overview/) — DSPy 集成的 GEPA 反思式提示词优化器，面向复合 AI 系统。
- [OpenAI Cookbook: Self-Evolving Agents](https://developers.openai.com/cookbook/examples/partners/self_evolving_agents/autonomous_agent_retraining) — 使用 GEPA 风格反射进化进行自主 Agent 重训练的示例代码。
- [WecoAI/awesome-autoresearch](https://github.com/WecoAI/awesome-autoresearch) — 精选自动研究用例列表，附带可验证轨迹与进度图表，按领域（LLM 训练、GPU Kernel、语音 Agent、交易等）组织。

<!-- AUTORESEARCH-END -->

---

## 如何贡献

我们欢迎对本列表的贡献！在提交之前，请花几分钟阅读我们的[贡献指南](contributing.md)。这些指南将帮助确保你的贡献符合我们的目标，并达到质量与相关性的标准。

**我们正在寻找：**
- 新增高质量论文、工具或资源，附带简要说明其价值所在
- 更新现有条目（修复失效链接、修正过时信息）
- 更正 Star 数、定价或模型细节
- 翻译内容与无障碍改进

**质量标准：**
- 所有工具应保持活跃维护状态（近 6 个月内有过更新）
- 论文应来自同行评审会议或在社区具有显著影响力
- 数据集应对公众开放可访问
- 请附带一行说明，解释该资源为何有价值

感谢你对本项目的关注与贡献！

<a href="https://github.com/promptslab/Awesome-Prompt-Engineering/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=promptslab/Awesome-Prompt-Engineering" />
</a>

---

<p align="center">
  <sub>Maintained by <a href="https://promptslab.github.io">PromptsLab</a> · <a href="https://github.com/promptslab/Awesome-Prompt-Engineering">Star this repo</a> if you find it useful!</sub>
</p>
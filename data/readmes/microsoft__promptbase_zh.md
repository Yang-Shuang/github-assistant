# promptbase

`promptbase` 是一个不断发展的资源库，包含最佳实践和示例脚本，旨在激发 GPT-4 等基础模型的最佳性能。我们目前托管了演示 [`Medprompt` 方法](https://arxiv.org/abs/2311.16452) 的脚本，其中包括如何将这套提示（prompting）技巧集合进一步扩展到非医疗领域（即 "`Medprompt+`"）的示例：

| Benchmark | GPT-4 Prompt | GPT-4 Results | Gemini Ultra Results |
| ---- | ------- | ------- | ---- |
| MMLU | Medprompt+ | 90.10% | 90.04% |
| GSM8K | Zero-shot | 95.3% | 94.4% |
| MATH | Zero-shot | 68.4% | 53.2% |
| HumanEval | Zero-shot | 87.8% | 74.4% |
| BIG-Bench-Hard | Few-shot + CoT | 89.0% | 83.6% |
| DROP | Zero-shot + CoT | 83.7% | 82.4% |
| HellaSwag | 10-shot | 95.3% | 87.8% |

未来不久，`promptbase` 还将提供关于提示工程背后科学流程的更多案例研究和结构化访谈。我们也会深入介绍能够强化提示工程过程的专业工具。敬请期待！

## `Medprompt` and The Power of Prompting

<details>
<summary>
    <em>"Can Generalist Foundation Models Outcompete Special-Purpose Tuning? Case Study in Medicine" (H. Nori, Y. T. Lee, S. Zhang, D. Carignan, R. Edgar, N. Fusi, N. King, J. Larson, Y. Li, W. Liu, R. Luo, S. M. McKinney, R. O. Ness, H. Poon, T. Qin, N. Usuyama, C. White, E. Horvitz 2023)</em>
</summary>
<br/>
<pre>

@article{nori2023can,
  title={Can Generalist Foundation Models Outcompete Special-Purpose Tuning? Case Study in Medicine},
  author={Nori, Harsha and Lee, Yin Tat and Zhang, Sheng and Carignan, Dean and Edgar, Richard and Fusi, Nicolo and King, Nicholas and Larson, Jonathan and Li, Yuanzhi and Liu, Weishung and others},
  journal={arXiv preprint arXiv:2311.16452},
  year={2023}
}
    </pre>
    <a href="https://arxiv.org/pdf/1909.09223.pdf">Paper link</a>
</details>

![](images/medprompt_radar.png)

在最近的一项[研究](https://arxiv.org/abs/2311.16452)中，我们展示了如何将多种提示策略组合成一种称为 `Medprompt` 的方法，从而高效引导 GPT-4 等通用模型取得顶尖性能，甚至优于专为医学微调的模型。`Medprompt` 结合了三种不同的策略——动态少样本选择、自生成思维链（Chain of Thought）和选项打乱集成（choice-shuffle ensembling）——以激发 GPT-4 达到专家级表现。我们在此简要介绍这些策略：

![](images/medprompt_sa_graphic.png)

- **Dynamic Few Shots**：少样本学习（Few-shot learning）——向基础模型提供任务及响应的多个示例——使模型能够快速适应特定领域并学会遵循任务格式。为简化和提高效率，提示中应用的少样本示例通常是固定的；它们在测试用例间保持不变。这就要求所选的少样本示例必须广泛具有代表性且与大量文本相关。满足这些要求的一种方法是让领域专家仔细手工编写示例。即便如此，这种方法也无法保证精心挑选的固定少样本示例能恰当代表每一个测试用例。然而，如果有足够的数据可用，我们可以为不同的任务输入选择_不同_的少样本示例。我们将此方法称为使用动态少样本示例。该方法利用一种机制来根据与当前案例的相似性识别示例。对于 Medprompt，我们采用以下步骤来识别代表性少样本：给定一个测试用例，我们在嵌入空间中通过 k-NN 聚类选择语义相似的 k 个训练示例。具体而言，我们首先使用 OpenAI 的 `text-embedding-ada-002` 模型对候选示例进行嵌入。然后，对于每个测试问题 x，我们从训练集中检索其最近的 k 个邻居 x1, x2, ..., xk（根据 text-embedding-ada-002 嵌入空间中的距离）。这些示例——即嵌入空间中与测试问题最相似的示例——最终会被注册到提示中。

- **Self-Generated Chain of Thought (CoT)**：思维链使用自然语言陈述（如“让我们一步步思考”）来显式鼓励模型生成一系列中间推理步骤。该方法已被证明能显著提升基础模型执行复杂推理的能力。大多数思维链方法依赖于专家手动编写带有思维链的少样本示例用于提示。我们没有依赖人类专家，而是探索了一种自动化创建思维链示例的机制。我们发现只需让 GPT-4 为训练示例生成思维链即可，同时设置适当的护栏以降低因错误推理链导致幻觉的风险。

- **Majority Vote Ensembling**：[集成学习](https://en.wikipedia.org/wiki/Ensemble_learning)指结合多个算法的输出以获得比任何单一算法更好的预测性能。`GPT-4` 等前沿模型从其自身输出的集成中受益。一种简单技术是准备多种提示，或使用带有不同 `temperature`（温度）参数的单个提示，并报告集成成员中最常出现的答案。对于多选题，我们采用了一种增加集成多样性的技巧，称为 `choice-shuffle`（选项打乱），即在生成每条推理路径前打乱答案选项的相对顺序。随后我们选择最一致的答案，即对选项打乱最不敏感的那个答案，从而提升结果的鲁棒性。

这三种技术的结合使 Medprompt 在医学挑战题中取得了突破性表现。这些技术的具体实现细节可在此查看：https://github.com/microsoft/promptbase/tree/main/src/promptbase/mmlu

## `Medprompt+` | Extending the power of prompting 

我们在此提供直观细节，说明如何扩展 `medprompt` 提示框架，以在 MMLU（大规模多任务语言理解）基准测试中获得更强的领域外性能。MMLU 旨在测试大语言模型的综合知识及推理能力。完整的 MMLU 基准包含数万个不同形式的挑战性问题，涵盖从基础数学到美国历史、法律、计算机科学、工程、医学等 57 个领域。

![](images/mmlu_accuracy_ablation.png)

我们发现，在不修改的情况下将 Medprompt 应用于整个 MMLU，得分达到 89.1%。对于单一策略在如此多样化的问题上工作而言，这已经很不错了！但我们能否让 Medprompt 表现得更好？简单地扩大规模即可带来进一步收益。作为第一步，我们将集成调用的数量从 5 次增加到 20 次。这将性能提升到了 89.56%。 

在进一步打磨 Medprompt 的过程中，我们注意到其在 MMLU 的某些特定主题上表现相对较差。MMLU 包含多种类型的题目，具体取决于学科和当前的基准测试。面对如此多样化的问题，我们如何能让 GPT-4 在 MMLU 上表现得更好呢？

我们专注于将其扩展为一种组合策略（portfolio approach），基于以下观察：某些主题倾向于提出需要多步推理甚至借助草稿区来跟踪解决方案多个部分的问题。而其他领域则寻求更直接源于问题的事实性答案。Medprompt 采用“思维链”（CoT）推理，这与多步求解相契合。我们不禁想到，对于非常简单的问题，复杂的经典 Medprompt 方法是否表现不佳？如果针对事实性问题使用更简单的方法，系统是否会表现得更好？ 

基于这一思路，我们发现通过为 MedPrompt 扩展一个简单的双方法提示组合集，可以提升 MMLU 的性能。我们在经典 Medprompt 的基础上增加了一组 10 个简单、直接的少样本提示，要求直接给出答案而不使用思维链。随后我们请 GPT-4 协助决定每个主题和问题的最佳策略。作为筛选步骤，对于每个问题，我们首先让 GPT-4 回答：
```
# Question
{{ question }}
 
# Task
Does answering the question above require a scratch-pad?
A. Yes
B. No
```

如果 GPT-4 认为该问题确实需要草稿区，则集成中思维链组件的贡献翻倍。如果不需，则该贡献减半（让集成更多地依赖直接少样本提示）。在集成中动态利用适当的提示技术，使 MMLU 的整体性能进一步提升了 +0.5%。

我们注意到，Medprompt+ 依赖于访问 GPT-4 的置信度分数（logprobs）。这些目前未通过公开 API 提供，但预计将在近期向所有人开放。


## Running Scripts

> **注意**：此处托管的部分脚本仅为方法论参考，可能无法立即针对公共 API 直接执行。我们正努力在未来几天内让运行流程更易于“开箱即用”，在此期间感谢您的耐心！

首先，克隆仓库并安装 promptbase 包：

```bash
cd src
pip install -e .
```

接下来，决定要运行哪些测试。你可以选择：

- bigbench
- drop
- gsm8k
- humaneval
- math
- mmlu

在运行测试之前，你需要从原始来源下载数据集（见下文），并将它们放入 `src/promptbase/datasets` 目录中。

下载数据集并安装 promptbase 包后，你可以通过以下命令运行测试：

`python -m promptbase dataset_name`

例如：

`python -m promptbase gsm8k`

## Dataset Links

要运行评估，请下载这些数据集并将它们添加到 `/src/promptbase/datasets/`

 - MMLU: https://github.com/hendrycks/test
    - 从上述页面下载 `data.tar` 文件
    - 解压内容
    - 运行 `mkdir src/promptbase/datasets/mmlu`
    - 运行 `python ./src/promptbase/format/format_mmlu.py --mmlu_csv_dir /path/to/extracted/csv/files --output_path ./src/promptbase/datasets/mmlu`
    - 你还需要设置以下环境变量：
      - `AZURE_OPENAI_API_KEY`
      - `AZURE_OPENAI_CHAT_API_KEY`
      - `AZURE_OPENAI_CHAT_ENDPOINT_URL`
      - `AZURE_OPENAI_EMBEDDINGS_URL`
    - 运行命令 `python -m promptbase mmlu --subject <SUBJECT>`，其中 `<SUBJECT>` 是 MMLU 数据集之一（例如 'abstract_algebra'）
    - 除了单独的主题外，`format_mmlu.py` 脚本还会准备文件，允许将 `all` 作为主题传入，从而在整个数据集上运行
 - HumanEval: https://huggingface.co/datasets/openai_humaneval
 - DROP: https://allenai.org/data/drop
 - GSM8K: https://github.com/openai/grade-school-math
 - MATH: https://huggingface.co/datasets/hendrycks/competition_math
 - Big-Bench-Hard: https://github.com/suzgunmirac/BIG-Bench-Hard
   此仓库的内容需要放入 `datasets` 目录中名为 `BigBench` 的目录下

## Other Resources:

**Medprompt Blog**: https://www.microsoft.com/en-us/research/blog/the-power-of-prompting/

**Medprompt Research Paper**: https://arxiv.org/abs/2311.16452

**Medprompt+**: https://www.microsoft.com/en-us/research/blog/steering-at-the-frontier-extending-the-power-of-prompting/

**Microsoft Introduction to Prompt Engineering**: https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/prompt-engineering

**Microsoft Advanced Prompt Engineering Guide**: https://learn.microsoft.com/en-us/azure/ai-services/openai/concepts/advanced-prompt-engineering?pivots=programming-language-chat-completions
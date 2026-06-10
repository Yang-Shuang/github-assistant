# [Brex的](https://brex.com) 提示词工程指南

本指南由 Brex 编写，仅供内部使用。它基于我们在研究和为生产环境创建大语言模型（LLM）提示词过程中积累的实践经验。内容涵盖了 LLM 的发展历史，以及在使用和构建基于大型语言模型的程序化系统时的策略、指南和安全建议，例如 [OpenAI 的 GPT-4](https://openai.com/research/gpt-4)。

本文档中的示例由非确定性语言模型生成，相同的提示词可能会得到不同的结果。

这是一份持续更新的文档。关于 LLM 的最佳实践和策略每天都在快速演进。我们鼓励讨论并提出改进建议。

## 目录
- [什么是大语言模型？](#what-is-a-large-language-model-llm)
  - [一段简短、不完整且略有偏差的语言模型发展史](#a-brief-incomplete-and-somewhat-incorrect-history-of-language-models)
    - [2000年以前](#pre-2000s)
    - [2000年代中期](#mid-2000s)
    - [2010年代初](#early-2010s)
    - [2010年代末](#late-2010s)
    - [2020年代](#2020s)
- [什么是提示词？](#what-is-a-prompt)
  - [隐藏提示词](#hidden-prompts)
  - [Token（词元）](#tokens)
  - [Token 限制](#token-limits)
  - [提示词攻击](#prompt-hacking)
    - [越狱 (Jailbreaks)](#jailbreaks)
    - [信息泄露 (Leaks)](#leaks)
- [为什么需要提示词工程？](#why-do-we-need-prompt-engineering)
  - [授人以鱼](#give-a-bot-a-fish)
    - [语义搜索](#semantic-search)
  - [授人以渔](#teach-a-bot-to-fish)
    - [命令语法](#command-grammars)
    - [ReAct](#react)
    - [GPT-4 与 GPT-3.5 的对比](#gpt-4-vs-gpt-35)
- [策略](#strategies)
  - [嵌入数据](#embedding-data)
    - [简单列表](#simple-lists)
    - [Markdown 表格](#markdown-tables)
    - [JSON](#json)
    - [自由文本](#freeform-text)
    - [嵌套数据](#nested-data)
  - [引用来源](#citations)
  - [程序化解析](#programmatic-consumption)
  - [思维链（Chain of Thought）](#chain-of-thought)
    - [计算平均值](#averaging)
    - [代码解读](#interpreting-code)
    - [分隔符](#delimiters)
  - [微调 (Fine Tuning)](#fine-tuning)
    - [局限性](#downsides)
- [更多资源](#additional-resources)

## 什么是大语言模型（LLM）？

大语言模型是一个预测引擎，它接收一段词序列，并尝试预测紧随其后的最可能出现的词序列[^1]。它是通过为可能的后续序列分配概率，然后从中采样来选择下一个序列来实现的[^2]。该过程会不断重复，直到满足某个停止条件为止。

大型语言模型通过在海量文本语料库上进行训练来学习这些概率。由此产生的一个结果是，模型在某些用例上的表现会更好（例如，如果它在 GitHub 数据上进行了训练，它将非常擅长理解源代码序列的概率）。另一个结果是，模型可能会生成看似合理但实际上只是随机拼凑、缺乏现实依据的陈述。

随着语言模型在预测序列方面变得越来越准确，[许多令人惊讶的能力开始涌现](https://www.assemblyai.com/blog/emergent-abilities-of-large-language-models/)。

[^1]: 语言模型实际上使用的是 Token（词元），而不是单词。一个 Token 大致对应单词中的一个音节，或约等于 4 个字符。
[^2]: 存在多种不同的剪枝和采样策略来改变序列的行为和性能表现。

### 一段简短、不完整且略有偏差的语言模型发展史

> :pushpin: 如果你想跳过语言模型的发展历史，请直接[跳到此处](#what-is-a-prompt)。本节适合好奇心强的读者阅读，同时也能帮助你更好地理解后续建议背后的推理逻辑。

#### 2000年以前

[语言模型](https://en.wikipedia.org/wiki/Language_model#Model_types)已经存在了几十年，但传统的语言模型（例如 [n-gram 模型](https://en.wikipedia.org/wiki/N-gram_language_model)）在状态空间爆炸（[维度灾难](https://en.wikipedia.org/wiki/Curse_of_dimensionality)）以及处理从未见过的新短语方面存在许多缺陷。简而言之，旧版语言模型生成的文本可能在统计上 vaguely 类似于人类生成的文本，但输出内部缺乏一致性——读者很快就会意识到这全是胡言乱语。此外，n-gram 模型无法扩展到较大的 N 值，因此本质上受到限制。

#### 2000年代中期

2007年，因在1980年代普及反向传播算法而闻名的 Geoffrey Hinton [发表了一篇关于神经网络训练的重要进展](http://www.cs.toronto.edu/~fritz/absps/tics.pdf)，解锁了更深层的网络。将这些简单的深度神经网络应用于语言建模有助于缓解语言模型的一些问题——它们以有限且连续的方式表示细微的任意概念，从而优雅地处理训练语料库中未出现的序列。这些简单神经网络很好地学习了其训练语料库的概率，但输出在统计上只是匹配训练数据，通常与输入序列缺乏连贯性。

#### 2010年代初

尽管长短期记忆网络（LSTM）早在1995年就已引入，但它们真正大放异彩是在2010年代。LSTM 允许模型处理任意长度的序列，并且重要的是，它能够在处理输入时动态改变内部状态，从而记住之前看到的内容。这一微小的改进带来了显著的性能提升。2015年，Andrej Karpathy [著名地撰文介绍了如何创建一个字符级 LSTM](http://karpathy.github.io/2015/05/21/rnn-effectiveness/)，其表现远超预期。

LSTM 似乎拥有近乎神奇的能力，但在处理长期依赖方面存在困难。如果你让它补全句子：“在法国，我们四处旅行，吃了很多糕点，喝了很多酒……（大量文本）……但从未学会说_______”，模型可能在预测“法语”时会遇到困难。此外，它们一次只能处理一个 Token，因此本质上是顺序处理的，训练速度慢，且第 `N` 个 Token 仅知道它之前的 `N-1` 个 Token。

#### 2010年代末

2017年，Google 发表了一篇论文 [《Attention Is All You Need》](https://arxiv.org/pdf/1706.03762.pdf)，引入了 [Transformer 网络](https://en.wikipedia.org/wiki/Transformer_(machine_learning_model))，并引发了自然语言处理领域的巨大革命。一夜之间，机器突然能够像人类（有时甚至优于人类）一样进行跨语言翻译。Transformer 高度可并行化，并引入了一种称为“注意力机制”的机制，使模型能够高效地将重点放在输入的特定部分上。Transformer 一次性并行分析整个输入，选择最重要和最具影响力的部分。每个输出 Token 都受到所有输入 Token 的影响。

Transformer 高度可并行化、训练效率高，并能产生惊人的结果。Transformer 的一个缺点是它们的输入和输出大小是固定的——即上下文窗口（context window），且计算量随该窗口大小的增加呈二次方增长（在某些情况下，内存消耗也是如此！）[^3]。

Transformer 并非终点，但近年来自然语言处理的绝大多数改进都涉及它们。目前仍有大量活跃的研究致力于各种实现和应用方式，例如 [Amazon 的 AlexaTM 20B](https://www.amazon.science/blog/20b-parameter-alexa-model-sets-new-marks-in-few-shot-learning)，它在多项任务中超越了 GPT-3，且参数量小了一个数量级。

[^3]: 近年来出现了更多变体以提高计算和内存效率，但这仍然是一个活跃的研究领域。

#### 2020年代

虽然从技术上讲始于2018年，但2020年代的主题是生成式预训练模型——更为人熟知的是 GPT。在《Attention Is All You Need》论文发表一年后，OpenAI 发布了 [《通过生成式预训练提升语言理解能力》](https://s3-us-west-2.amazonaws.com/openai-assets/research-covers/language-unsupervised/language_understanding_paper.pdf)。该论文确立了这样一个事实：你可以在没有任何特定目标的情况下在海量数据上训练大型语言模型，然后在模型掌握了语言的通用特性后，针对特定任务进行微调，并迅速获得最先进的结果。

2020年，OpenAI 发布了 GPT-3 的后续论文 [《语言模型是少样本学习者》](https://proceedings.neurips.cc/paper/2020/file/1457c0d6bfcb4967418bfb8ac142f64a-Paper.pdf)，展示了如果将类 GPT 模型的参数量和训练数据量再扩大约 10 倍，你就不再需要为许多任务进行微调。这些能力会自然涌现，你只需通过文本与模型交互即可获得最先进的结果。

2022年，OpenAI 在 GPT-3 的成果基础上发布了 [InstructGPT](https://openai.com/research/instruction-following)。其目的是调整模型以更好地遵循指令，同时减少输出中的毒性和偏见。这里的关键成分是 [基于人类反馈的强化学习（RLHF）](https://arxiv.org/pdf/1706.03741.pdf)，这一概念由 Google 和 OpenAI 在2017年共同提出[^4]，它允许人类参与训练循环，微调模型输出以更符合人类的偏好。InstructGPT 是如今著名的 [ChatGPT](https://en.wikipedia.org/wiki/ChatGPT) 的前身。

过去几年里，OpenAI 一直是大型语言模型的主要贡献者之一，包括最近推出的 [GPT-4](https://cdn.openai.com/papers/gpt-4.pdf)，但他们并非孤军奋战。Meta 推出了许多开源大语言模型，如 [OPT](https://huggingface.co/facebook/opt-66b)、[OPT-IML](https://huggingface.co/facebook/opt-iml-30b)（指令微调版）和 [LLaMa](https://ai.facebook.com/blog/large-language-model-llama-meta-ai/)。Google 发布了如 [FLAN-T5](https://huggingface.co/google/flan-t5-xxl) 和 [BERT](https://huggingface.co/bert-base-uncased) 等模型。此外，还有庞大的开源研究社区在发布如 [BLOOM](https://huggingface.co/bigscience/bloom) 和 [StableLM](https://github.com/stability-AI/stableLM/) 等模型。

如今的发展速度极快，每隔几周最先进的技术就会更新换代，曾经需要集群才能运行的模型现在甚至可以在树莓派上运行。

[^4]: 2017年是自然语言处理领域的大年。

## 什么是提示词？

提示词（Prompt），有时也称为上下文（context），是在模型开始生成输出之前提供给它的文本。它引导模型探索其已学习内容的特定区域，从而使输出与你的目标相关。打个比方，如果你把语言模型看作是一个源代码解释器，那么提示词就是待解释的源代码。有趣的是，语言模型会非常乐意尝试猜测这段源代码的作用：

<p align="center">
  <img width="450" src="https://user-images.githubusercontent.com/89960/231946874-be91d3de-d773-4a6c-a4ea-21043bd5fc13.png" title="GPT-4 模型解释 Python 代码。">
</p>

而且它*几乎*完美地解释了这段 Python 代码！

通常，提示词会是一条指令或一个问题，例如：

 <p align="center">
  <img width="500" src="https://user-images.githubusercontent.com/89960/232413246-81db18dc-ef5b-4073-9827-77bd0317d031.png">
</p>

另一方面，如果你不指定提示词，模型将没有锚点来工作，你会发现它只是**从它曾接触过的所有内容中随机采样**：

**来自 GPT-3-Davinci：**

| ![image](https://user-images.githubusercontent.com/89960/232413846-70b05cd1-31b6-4977-93f0-20bf29af7132.png) | ![image](https://user-images.githubusercontent.com/89960/232413930-7d414dcd-87e5-431a-91c8-bb6e0ef54f42.png) | ![image](https://user-images.githubusercontent.com/89960/232413978-59c7f47d-ec20-4673-9458-85471a41fee0.png) |
| --- | --- | --- |

**来自 GPT-4：**
| ![image](https://user-images.githubusercontent.com/89960/232414631-928955e5-ebab-4d57-b1d6-5e56f00ffda1.png) | ![image](https://user-images.githubusercontent.com/89960/232414678-e5b6d3f4-36c6-420f-b38f-2f9c8df391fb.png) | ![image](https://user-images.githubusercontent.com/89960/232414734-c8f09cad-aceb-4149-a28a-33675cde8011.png) |
| --- | --- | --- |

### 隐藏提示词

> :warning: 始终假设隐藏提示词中的任何内容都可能被用户看到。

在用户与模型动态交互的应用中（例如与模型聊天），通常会有部分提示词是故意不向用户展示的。这些隐藏部分可能出现在任何位置，尽管对话开头几乎总是会有一个隐藏提示词。

这通常包括一段初始文本，用于设定基调、模型约束和目标，以及特定于当前会话的其他动态信息——用户名、位置、一天中的时间等。

模型在某一时刻被静态锁定并冻结，因此如果你想让它了解当前信息（如时间或天气），你必须提供给它。

如果你正在使用 [OpenAI Chat API](https://platform.openai.com/docs/guides/chat/introduction)，它们通过将隐藏提示词内容放在 `system` 角色中来划定界限。

下面是一个隐藏提示词及其交互内容的示例：

<p align="center">
  <img width="550" src="https://user-images.githubusercontent.com/89960/232416074-84ebcc10-2dfc-49e1-9f48-a240102877ee.png" title="一个非常简单的隐藏提示词。">
</p>

在这个示例中，你可以看到我们向机器人解释了各种角色、关于用户的一些背景信息、我们希望机器人访问的动态数据，以及它应如何响应的指导原则。

在实际应用中，隐藏提示词可能非常大。以下是从 [ChatGPT 命令行助手](https://github.com/manno/chatgpt-linux-assistant/blob/main/system_prompt.txt)中提取的一个较大提示词：

<details>
  <summary>来源: https://github.com/manno/chatgpt-linux-assistant </summary>

```
We are a in a chatroom with 3 users. 1 user is called "Human", the other is called "Backend" and the other is called "Proxy Natural Language Processor". I will type what "Human" says and what "Backend" replies. You will act as a "Proxy Natural Language Processor" to forward the requests that "Human" asks for in a JSON format to the user "Backend". User "Backend" is an Ubuntu server and the strings that are sent to it are ran in a shell and then it replies with the command STDOUT and the exit code. The Ubuntu server is mine. When "Backend" replies with the STDOUT and exit code, you "Proxy Natural Language Processor" will parse and format that data into a simple English friendly way and send it to "Human". Here is an example:

I ask as human:
Human: How many unedited videos are left?
Then you send a command to the Backend:
Proxy Natural Language Processor: @Backend {"command":"find ./Videos/Unedited/ -iname '*.mp4' | wc -l"}
Then the backend responds with the command STDOUT and exit code:
Backend: {"STDOUT":"5", "EXITCODE":"0"}
Then you reply to the user:
Proxy Natural Language Processor: @Human There are 5 unedited videos left.

Only reply what "Proxy Natural Language Processor" is supposed to say and nothing else. Not now nor in the future for any reason.

Another example:

I ask as human:
Human: What is a PEM certificate?
Then you send a command to the Backend:
Proxy Natural Language Processor: @Backend {"command":"xdg-open 'https://en.wikipedia.org/wiki/Privacy-Enhanced_Mail'"}
Then the backend responds with the command STDOUT and exit code:
Backend: {"STDOUT":"", "EXITCODE":"0"}
Then you reply to the user:
Proxy Natural Language Processor: @Human I have opened a link which describes what a PEM certificate is.


Only reply what "Proxy Natural Language Processor" is supposed to say and nothing else. Not now nor in the future for any reason.

Do NOT REPLY as Backend. DO NOT complete what Backend is supposed to reply. YOU ARE NOT TO COMPLETE what Backend is supposed to reply.
Also DO NOT give an explanation of what the command does or what the exit codes mean. DO NOT EVER, NOW OR IN THE FUTURE, REPLY AS BACKEND.

Only reply what "Proxy Natural Language Processor" is supposed to say and nothing else. Not now nor in the future for any reason.
```
</details>

你会看到其中包含了一些良好的实践，例如提供大量示例、对重要行为特征进行重复强调、限制回复内容等。

> :warning: 始终假设隐藏提示词中的任何内容都可能被用户看到。

### Token（词元）

如果你认为2022年的 Token 已经 :fire: 了，那么2023年的 Token 简直处于另一个维度。语言模型的消费基本单位不是“单词”，而是“Token”。你可以将 Token 大致理解为音节，平均而言，每 1,000 个 Token 大约对应 750 个单词。它们代表的概念远不止字母字符——还包括标点符号、句子边界和文档结尾等。

以下是 GPT 可能对序列进行分词的示例：

<p align="center">
  <img width="550" src="https://user-images.githubusercontent.com/89960/232417569-8d562792-64b5-423d-a7a2-db7513dd4d61.png" title="分词示例。你可以在这里尝试：https://platform.openai.com/tokenizer ">
</p>

你可以在此处尝试分词器：[https://platform.openai.com/tokenizer](https://platform.openai.com/tokenizer)

不同的模型会使用不同粒度的分词器。理论上，你可以向模型输入 0 和 1——但那样模型就需要从比特中学习字符的概念，再从字符学习单词的概念，依此类推。同样，你也可以向模型输入原始字符流，但那样模型就需要学习单词、标点等概念……总体而言，模型的表现会更差。

想了解更多，[Hugging Face 提供了一份关于分词器的精彩介绍](https://huggingface.co/docs/transformers/tokenizer_summary)以及它们为何必须存在的原因。

分词涉及大量细微差别，例如词汇表大小或不同语言对句子结构的处理方式（例如单词之间没有空格分隔）。幸运的是，语言模型 API 几乎总是接受原始文本作为输入并在后台进行分词——*所以你很少需要关心 Token 的问题*。

**除了一个重要的场景，我们将在下一节讨论：Token 限制。**

### Token 限制

提示词通常是追加式的，因为你希望机器人拥有对话中所有先前消息的完整上下文。语言模型在整体上是无状态的，不会记住之前对它们的任何请求，因此你总是需要包含它可能需要的、特定于当前会话的所有信息。

这样做的主要缺点是，目前主流的语言模型架构 Transformer 具有固定的输入和输出大小——到了一定程度提示词就无法再增长了。提示词的总大小（有时称为“上下文窗口”）取决于具体模型。对于 GPT-3，它是 4,096 个 Token。对于 GPT-4，根据你使用的变体不同，它是 8,192 或 32,768 个 Token。

如果你的上下文超出了模型的容量，最常见的策略是以滑动窗口的方式截断上下文。如果你将提示词视为 `隐藏初始化提示词 + messages[]`，通常隐藏提示词会保持不变，而 `messages[]` 数组会保留最近的 N 条消息。

你可能会看到更巧妙的提示词截断技巧——例如首先仅丢弃用户消息，以便机器人的先前回答能尽可能长时间地留在上下文中；或者要求 LLM 总结对话，然后用一条包含该摘要的消息替换所有消息。这里没有标准答案，解决方案取决于你的应用场景。

重要的是，在截断上下文时，你必须足够激进地截断，以**为响应留出空间**。OpenAI 的 Token 限制同时包括输入长度和输出长度。如果你的 GPT-3 输入是 4,090 个 Token，它只能生成 6 个 Token 作为响应。

> 🧙‍♂️ 如果你想在将原始文本发送给模型之前计算 Token 数量，具体使用的分词器取决于你正在使用的模型。OpenAI 有一个名为 [tiktoken](https://github.com/openai/tiktoken/blob/main/README.md) 的库，你可以将其与他们的模型一起使用——但需要注意的是，他们内部的分词器计数可能会有细微差异，并且可能会附加其他元数据，因此请将其视为近似值。
> 
> 如果你没有分词器访问权限但又想要一个近似值，`input.length / 4` 会给出一个粗略但比预期更好的英文输入近似值。

### 提示词攻击

提示词工程和大型语言模型是一个相对新兴的领域，因此每天都会有新的绕过方法被发现。两大类的攻击是：
1. 让机器人绕过你设定的任何指导原则。
2. 让机器人输出隐藏上下文中本不该让用户看到的内容。

目前还没有已知的机制能全面阻止这些行为，因此重要的是你要假设与对抗性用户交互时，机器人可能会做出或说出任何事情。幸运的是，在实践中，这主要是表面上的担忧。

将提示词视为改善普通用户体验的一种方式。**我们设计提示词是为了让普通用户不会偏离我们预期的交互范围——但始终要假设坚定的用户能够绕过我们的提示词约束。**

#### 越狱 (Jailbreaks)

通常隐藏提示词会指示机器人以特定人设行事，专注于特定任务或避免某些词汇。对于非对抗性用户来说，假设机器人会遵循这些指导原则通常是安全的，尽管非对抗性用户也可能无意中绕过这些规则。

例如，我们可以告诉机器人：
```
你是一个乐于助人的助手，但你永远不允许使用“computer”这个词。
```
如果我们随后问它关于电脑的问题，它会将其称为“用于计算的装置”，因为它不能使用“computer”这个词。

<p align="center">
  <img width="550" src="https://user-images.githubusercontent.com/89960/232420043-ebe5bcf1-25d9-4a31-ba84-13e9e1f62de2.png" title="GPT-4 努力避免说出 computer 这个词。">
</p>

它会绝对拒绝说这个词：

<p align="center">
  <img width="550" src="https://user-images.githubusercontent.com/89960/232420306-6fcdd6e2-b107-45d5-a1ee-4132fbb5853e.png">
</p>

但我们可以通过欺骗它来绕过这些指令，让它愉快地使用该词，例如要求它将“computer”的猪拉丁语版本翻译成英文。

<p align="center">
  <img width="550" src="https://user-images.githubusercontent.com/89960/232420600-56083a10-b382-46a7-be18-eb9c005b8371.png">
</p>

你可以采取[一些防御措施](https://learnprompting.org/docs/prompt_hacking/defensive_measures/overview)，但通常最好的办法是尽可能靠近提示词末尾重申你最关键的约束。对于 OpenAI 聊天 API，这可能意味着将其作为 `system` 消息放在最后一个 `user` 消息之后。这是一个示例：

| ![image](https://user-images.githubusercontent.com/89960/232421097-adcaace3-0b21-4c1e-a5c8-46bb25faa2f7.png) | ![image](https://user-images.githubusercontent.com/89960/232421142-a47e75b4-5ff6-429d-9abd-a78dbc72466e.png) |
| --- | --- |

尽管 OpenAI 在越狱防护上投入了大量精力，但[非常巧妙的绕过方法](https://twitter.com/alexalbert__/status/1636488551817965568)[每天都在被分享](https://twitter.com/zswitten/status/1598088267789787136)。

#### 信息泄露 (Leaks)

如果你错过了本文前面的警告，**你应该始终假设任何暴露给语言模型的数据最终都会被用户看到**。

在构建提示词时，你通常会将大量数据嵌入到隐藏提示词（又称系统提示词）中。**机器人会非常乐意将这些信息传达给用户**：

<p align="center">
  <img width="550" src="https://user-images.githubusercontent.com/89960/232422860-731c1de2-9e77-4957-b257-b0bbda48558c.png" title="机器人愉快地复述它知道的关于用户的信息。">
</p>

即使你指示它不要透露这些信息，并且它服从了指令，也有数百万种方式可以从隐藏提示词中泄露数据。

这里有一个例子，机器人本不应提及我的城市，但通过简单的问题重构就让它露出了马脚。

<p align="center">
  <img width="550" src="https://user-images.githubusercontent.com/89960/232423121-76568893-fa42-4ad8-b2bc-e1001327fa1e.png" title="机器人拒绝透露个人信息，但我们说服它告诉了我所在的城市。">
</p>

同样，我们让机器人告诉我们它不被允许说的词是什么，而实际上从未直接说出那个词：

<p align="center">
  <img width="550" src="https://user-images.githubusercontent.com/89960/232423283-1718f822-59d0-4d18-9a4d-22dd3a2672c0.png" title="严格来说，机器人从未说过 'computer'，但我仍然成功让它告诉了我所有需要了解的信息。">
</p>

你应该将隐藏提示词视为一种改善用户体验或使其更符合目标人设的手段。**切勿在提示词中放置任何你不想让用户在屏幕上直接阅读的信息**。

## 为什么需要提示词工程？

在上面，我们使用了将提示词比作语言模型“解释”的“源代码”的类比。**提示词工程就是编写提示词的艺术，目的是让语言模型按照我们的意愿行事**——就像软件工程是编写源代码让计算机按我们意愿行事的艺术一样。

在编写好的提示词时，你必须考虑你所使用的模型的怪癖。策略会随着任务的复杂性而变化。你需要想出机制来约束模型以获得可靠的结果，融入模型无法训练的动态数据，应对模型训练数据的局限性，围绕上下文限制进行设计，以及许多其他维度。

有一句老话：计算机只会做你告诉它们做的事。**把这条建议扔出窗外**。提示词工程颠覆了这种智慧。它就像是用自然语言编程，面对的是一个非确定性的计算机，它会做任何你没有明确引导它不要做的事情。

提示词工程的 approaches 主要分为两大类。

### 授人以鱼

“授人以鱼”适用于以下场景：你可以在隐藏上下文中明确地给机器人提供完成任何请求任务所需的所有信息。

例如，如果用户加载了他们的仪表板，而我们想向他们显示一条简短友好的消息，告诉他们有哪些待办事项，我们可以通过提供一个完整的收件箱列表以及我们希望它拥有的任何其他用户上下文，让机器人将其总结为：

> 你有4个收据/备忘录需要上传。最新的是3月5日来自 Target 的，最旧的是1月17日来自 Blink Fitness 的。感谢你对开支的管理！

<p align="center">
  <img width="550" src="https://user-images.githubusercontent.com/89960/233465165-e0c6b266-b347-4128-8eaa-73974e852e45.png" title="GPT-3 总结任务收件箱。">
</p>

同样，如果你正在帮助用户预订行程，你可以：
- 询问用户的日期和目的地。
- 在后台搜索航班和酒店。
- 将航班和酒店预订结果嵌入隐藏上下文。
- 同时将公司的差旅政策也嵌入隐藏上下文。

这样机器人就拥有了实时旅行信息 + 约束条件，可以用来回答用户的问题。以下是机器人推荐选项以及用户要求细化建议的示例：

<p align="center">
  <img width="550" src="https://user-images.githubusercontent.com/89960/233465425-9e06320c-b6d9-40ef-b5a4-c556861c1328.png" title="GPT-4 帮助用户预订行程。">
</p>
<details>

  <summary>(完整提示词)</summary>

```
Brex is a platform for managing business expenses. 

The following is a travel expense policy on Brex:

- Airline highest fare class for flights under 6 hours is economy.
- Airline highest fare class for flights over 6 hours is premium economy.
- Car rentals must have an average daily rate of $75 or under.
- Lodging must have an average nightly rate of $400 or under.
- Lodging must be rated 4 stars or higher.
- Meals from restaurants, food delivery, grocery, bars & nightlife must be under $75
- All other expenses must be under $5,000.
- Reimbursements require review.

The hotel options are:
| Hotel Name | Price | Reviews |
| --- | --- | --- |
| Hilton Financial District | $109/night | 3.9 stars |
| Hotel VIA | $131/night | 4.4 stars |
| Hyatt Place San Francisco | $186/night | 4.2 stars |
| Hotel Zephyr | $119/night | 4.1 stars review |

The flight options are:
| Airline | Flight Time | Duration | Number of Stops | Class | Price |
| --- | --- | --- | --- | --- | --- |
| United | 5:30am-7:37am | 2hr 7 min | Nonstop | Economy | $248 |
| Delta | 1:20pm-3:36pm | 2hr 16 min | Nonstop | Economy | $248 |
| Alaska | 9:50pm-11:58pm | 2hr 8 min | Nonstop | Premium | $512 |

An employee is booking travel to San Francisco for February 20th to February 25th.

Recommend a hotel and flight that are in policy. Keep the recommendation concise, no longer than a sentence or two, but include pleasantries as though you are a friendly colleague helping me out:
```
 
</details>

这与 Microsoft Bing 等产品利用动态数据的方法相同。当你与 Bing 聊天时，它会要求机器人生成三个搜索查询。然后它们运行三次网络搜索，并将摘要结果包含在机器人的隐藏上下文中供其使用。

总结本节内容：打造良好体验的技巧在于根据用户正在尝试做的事情动态改变上下文。

> 🧙‍♂️ “授人以鱼”是确保机器人得到鱼的可靠方法。使用该策略你将获得最一致和可靠的结果。**只要可行，就请使用此方法。**

#### 语义搜索

如果你只需要机器人对世界有更多了解，[一种常见的方法是执行语义搜索](https://github.com/openai/openai-cookbook/blob/main/examples/Question_answering_using_embeddings.ipynb)。

语义搜索围绕文档嵌入展开——你可以将其视为一个固定长度的数组[^5]，其中每个数字代表文档的某个方面（例如，如果它是科学文档，第 843 个数字可能很大；但如果是艺术文档，第 1,115 个数字可能很大——这过于简化，但传达了概念）[^6]。

除了为文档计算嵌入外，你还可以使用相同的函数为用户查询计算嵌入。如果用户问“为什么天空是蓝色的？”——你计算该问题的嵌入，理论上，此嵌入将与提及天空的文档的嵌入更相似，而不是与不谈论天空的文档的嵌入相似。

为了找到与用户查询相关的文档，你计算嵌入然后找出 Top-N 个具有最相似嵌入的文档。然后将这些文档（或这些文档的摘要）放入隐藏上下文中供机器人参考。

值得注意的是，有时用户查询非常短，以至于嵌入的价值不大。[2022年12月发表的一篇论文](https://arxiv.org/pdf/2212.10496.pdf)中描述了一种名为“假设文档嵌入”（Hypothetical Document Embedding，简称 HyDE）的巧妙技术。使用这种技术时，你要求模型根据用户查询生成一篇假设性文档，然后计算该生成文档的嵌入。模型凭空捏造了一篇文档——但这种方法确实有效！

HyDE 技术使用了更多的模型调用，但对于许多用例而言，结果有显著提升。

[^5]: 通常被称为向量（Vector）。
[^6]: 向量特征是通过自动学习获得的，没有额外努力的话人类无法直接解释其具体数值。

### 授人以渔

有时你希望机器人具备代表用户执行操作的能力，例如向收据添加备忘录或绘制图表。或者我们希望它以比语义搜索允许的更精细的方式检索数据，例如检索过去90天的开支记录。

在这些场景中，我们需要教机器人如何“捕鱼”。

#### 命令语法

我们可以给机器人提供一套系统可解释的命令列表，以及这些命令的描述和示例，然后让它生成由这些命令组成的程序。

采用这种方法时有很多需要注意的地方。对于复杂的命令语法，机器人往往会“幻觉”出可能合理但实际上不存在的命令或参数。掌握此技巧的关键在于枚举具有相对较高抽象级别的命令，同时给予机器人足够的灵活性以新颖且有用的方式组合它们。

例如，给机器人一个 `plot-the-last-90-days-of-expenses` 命令在机器人能做什么方面并不特别灵活或可组合。同样，一个 `draw-pixel-at-x-y [x] [y] [rgb]` 命令会过于底层。但给机器人提供 `plot-expenses` 和 `list-expenses` 命令则提供了一些良好的基础原语，让机器人有一定的灵活性。

在下面的示例中，我们使用这组命令：

| Command | Arguments | Description |
| --- | --- | --- |
| list-expenses | budget | Returns a list of expenses for a given budget |
| converse | message | A message to show to the user |
| plot-expenses | expenses[] | Plots a list of expenses |
| get-budget-by-name | budget_name | Retrieves a budget by name |
| list-budgets | | Returns a list of budgets the user has access to |
| add-memo | inbox_item_id, memo message | Adds a memo to the provided inbox item |

我们以 Markdown 格式将此表提供给模型，语言模型处理得非常好—— presumably 因为 OpenAI 在 GitHub 数据上进行了大量训练。

在下面的示例中，我们要求模型以 [逆波兰表示法](https://en.wikipedia.org/wiki/Reverse_Polish_notation)[^7] 输出命令。

[^7]: 模型极其出色地处理了 RPN 的简洁性。

<p align="center">
  <img width="550" src="https://user-images.githubusercontent.com/89960/233505150-aef4409c-03ba-4669-95d7-6c48f3c2c3ea.png" title="机器人愉快地生成响应用户查询的命令。">
</p>

> 🧠 那个示例中有一些有趣的微妙之处，不仅仅是命令生成。当我们要求它向“shake shack”开支添加备忘录时，模型知道 `add-memo` 命令需要一个开支 ID。但我们从未告诉它该 ID，所以它在我们要提供的开支表中查找“Shake Shack”，然后从相应的 ID 列中提取 ID，并将其作为参数传递给 `add-memo`。

在复杂情况下让命令语法可靠工作可能很棘手。我们在这里最好的杠杆是提供大量描述，以及尽可能**多的使用示例**。大型语言模型是 [少样本学习者](https://en.wikipedia.org/wiki/Few-shot_learning_(natural_language_processing))，这意味着它们可以通过仅提供少量样本来学习新任务。通常，你提供的示例越多越好——但这也会消耗你的 Token 预算，因此需要权衡。

这是一个更复杂的示例，输出指定为 JSON 而不是 RPN。我们使用 TypeScript 定义命令的返回类型。

<p align="center">
  <img width="550" src="https://user-images.githubusercontent.com/89960/233505696-fc440931-9baf-4d06-80e7-54801532d63f.png" title="机器人愉快地生成响应用户查询的命令。">
</p>

<details>

  <summary>(完整提示词)</summary>
  
~~~
You are a financial assistant working at Brex, but you are also an expert programmer.

I am a customer of Brex.

You are to answer my questions by composing a series of commands.

The output types are:

```typescript
type LinkedAccount = {
    id: string,
    bank_details: {
        name: string,
        type: string,
    },
    brex_account_id: string,
    last_four: string,
    available_balance: {
        amount: number,
        as_of_date: Date,
    },
    current_balance: {
            amount: number,
        as_of_date: Date,
    },
}

type Expense = {
  id: string,
  memo: string,
  amount: number,
}

type Budget = {
  id: string,
  name: string,
  description: string,
  limit: {
    amount: number,
    currency: string,
  }
}
```

The commands you have available are:

| Command | Arguments | Description | Output Format |
| --- | --- | --- | --- |
| nth | index, values[] | Return the nth item from an array | any |
| push | value | Adds a value to the stack to be consumed by a future command | any |
| value | key, object | Returns the value associated with a key | any |
| values | key, object[] | Returns an array of values pulled from the corresponding key in array of objects | any[] |
| sum | value[] | Sums an array of numbers | number |
| plot | title, values[] | Plots the set of values in a chart with the given title | Plot |
| list-linked-accounts |  | "Lists all bank connections that are eligible to make ACH transfers to Brex cash account" | LinkedAccount[] |
| list-expenses | budget_id | Given a budget id, returns the list of expenses for it | Expense[]
| get-budget-by-name | name | Given a name, returns the budget | Budget |
| add-memo | expense_id, message | Adds a memo to an expense | bool |
| converse | message | Send the user a message | null |

Only respond with commands.

Output the commands in JSON as an abstract syntax tree.

IMPORTANT - Only respond with a program. Do not respond with any text that isn't part of a program. Do not write prose, even if instructed. Do not explain yourself.

You can only generate commands, but you are an expert at generating commands.
~~~

</details>

如果你的编程语言有 `JSON.parse` 函数，这个版本更容易解析和解释。

> 🧙‍♂️ 目前行业尚未建立为模型生成程序定义 DSL 的最佳格式。因此请将其视为一个活跃的研究领域。你会遇到限制。随着我们克服这些限制，我们可能会发现更优的命令定义方式。

#### ReAct

2023年3月，普林斯顿大学和 Google 发布了一篇论文 [《ReAct: Synergizing Reasoning and Acting in Language Models》](https://arxiv.org/pdf/2210.03629.pdf)，其中引入了一种命令语法变体，允许完全自主地交互执行动作和检索数据。

模型被指示返回一个 `thought`（思考）和一个它想要执行的 `action`（行动）。另一个代理（例如我们的客户端）随后执行该 `action` 并将其作为 `observation`（观察结果）返回给模型。然后模型将循环继续返回更多的思考和行动，直到它返回一个 `answer`（答案）。

这是一种非常强大的技术， effectively 允许机器人成为自己的研究助手，并可能代表用户采取操作。结合强大的命令语法，机器人应能快速回答大量用户请求。

在此示例中，我们向模型提供了一组与获取员工数据和搜索维基百科相关的少量命令：

| Command | Arguments | Description |
| --- | --- | --- |
| find_employee | name | Retrieves an employee by name |
| get_employee | id | Retrieves an employee by ID |
| get_location | id | Retrieves a location by ID |
| get_reports | employee_id | Retrieves a list of employee ids that report to the employee associated with employee_id. |
| wikipedia | article | Retrieves a wikipedia article on a topic. |

然后我们问机器人一个简单的问题：“我的经理有名吗？”。

我们看到机器人：
1. 首先查找我们的员工档案。
2. 从我们的档案中获取经理的 ID 并查找其档案。
3. 提取经理的名字并在维基百科上搜索他们。
    - 在此场景中，我为经理选择了一个虚构角色。
4. 机器人阅读维基百科文章并得出结论：这不可能是我的经理，因为它是虚构人物。
5. 机器人随后修改了搜索条件以包含 (real person)。
6. 看到没有结果后，机器人得出结论：我的经理并不出名。

| ![image](https://user-images.githubusercontent.com/89960/233506839-5c8b2d77-1d78-46d-bc33-a725e12f2624.png) | ![image](https://user-images.githubusercontent.com/89960/233506870-05fc415d-efa2-48b7-aad9-b5035e535e6d.png) |
| --- | --- |

<details>
<summary>(完整提示词)</summary>

~~~
You are a helpful assistant. You run in a loop, seeking additional information to answer a user's question until you are able to answer the question.

Today is June 1, 2025. My name is Fabian Seacaster. My employee ID is 82442.

The commands to seek information are:

| Command | Arguments | Description |
| --- | --- | --- |
| find_employee | name | Retrieves an employee by name |
| get_employee | id | Retrieves an employee by ID |
| get_location | id | Retrieves a location by ID |
| get_reports | employee_id | Retrieves a list of employee ids that report to the employee associated with `employee_id`. |
| wikipedia | article | Retrieves a wikipedia article on a topic. |

Your response will be in JSON and will include a "Thought" + "Action" to retrieve data that you need in order to answer the question, or it will include the "Answer". When data has been retrieved, it will be included as an "Observation".

You will continue generating thoughts and actions until you get to an answer, or conclude that you can't.

Example 1:
```
User: What is the population of Philadelphia?

Assistant: {
  "thought": "Wikipedia likely has this information. I'm looking it up...",
  "action": {"command": "wikipedia", "article": "Philadelphia"}
}

Assistant: {
  "observation": "Philadelphia, often called Philly, is the largest city in the Commonwealth of Pennsylvania and the second-largest city in both the Northeast megalopolis and Mid-Atlantic regions after New York City. It is one of the most historically significant cities in the United States and served as the nation's capital city until 1800. Philadelphia is the nation's sixth-largest city with a population of 1,603,797 as of the 2020 census. Since 1854, the city has been coextensive with Philadelphia County, the most populous county in Pennsylvania and the urban core of the Delaware Valley, the nation's seventh-largest and one of the world's largest metropolitan regions with 6.245 million residents in 2020. Philadelphia is known for its extensive contributions to American history and for its role in the life sciences, business and industry, art, literature, and music."
}

Assistant: {
  "answer": "The population of Philadelphia, as of the 2020 census, is 1,603,797 people."
}
```

Example 2:
```
User: What is my manager's city?

Assistant: {
  "thought": "Let me look up who your manager is. First, I need to look up your profile.",
  "action": {"command": "get_employee", "id": 92352}
}

Assistant: {
  "observation": {
    "id": 78334,
    "name": "Ms. Manager",
    "location_id": 8832
  }
}

Assistant: {
  "thought": "Your manager is Ms. Manager. I'm looking up their location.",
  "action": {"command": "get_location", "id": 8832}
}

Assistant: {
  "observation": {
    "id": 8832,
    "name": "Philadelphia"
  }
}

Assistant: {
  "answer": "Your manager lives in Philadelphia."
}
```
~~~
</details>

#### GPT-4 与 GPT-3.5 的对比

在本文的大多数示例中，GPT-3.5 和 GPT-4 之间的差异可以忽略不计，但在“授人以渔”的场景中，模型之间的差异是显著的。

例如，上述所有命令语法示例如果不进行实质性修改，都无法在 GPT-3.5 上运行。至少你必须提供一定数量的示例（每个命令至少一个使用示例）才能获得合理结果。而且对于复杂的命令集，它可能会幻觉出新的命令或创建虚构的参数。

通过足够详尽的隐藏提示词，你应该能够克服这些限制。GPT-4 能够用简单得多的提示词实现更一致和复杂的逻辑（甚至可以零或少量示例运行——尽管尽可能多地包含示例总是有益的）。

## 策略

本节包含针对特定需求或问题的示例和策略。要成功进行提示词工程，你需要结合本文列举的所有策略中的一部分。不要害怕混合搭配事物——或者发明你自己的方法。

### 嵌入数据

在隐藏上下文中，你经常需要嵌入各种数据。具体策略将取决于你要嵌入的数据类型和数量。

#### 简单列表

对于一次性对象，在普通的项目符号列表中枚举字段+值效果相当不错：

<p align="center">
  <img width="550" src="https://user-images.githubusercontent.com/89960/233507156-0bdbc0af-d977-44e0-a8d5-b30538c5bbd9.png" title="GPT-4 从属性列表中提取 Steve 的职业。">
</p>

它也适用于较大的集合，但对于数据列表，GPT 能更可靠地处理其他格式。无论如何，这里有一个示例：

<p align="center">
  <img width="550" src="https://user-images.githubusercontent.com/89960/233507223-9cda591e-62f3-4339-b227-a07c37b90724.png" title="GPT-4 回答关于一组开支的问题。">
</p>

#### Markdown 表格

Markdown 表格非常适合你需要枚举大量同类项目的场景。

幸运的是，OpenAI 的模型在处理 Markdown 表格方面非常出色（ presumably 源于它们在海量 GitHub 数据上的训练）。

我们可以使用 Markdown 表格重新表述上面的内容：

<p align="center">
  <img width="550" src="https://user-images.githubusercontent.com/89960/233507313-7ccd825c-71b9-46d3-80c9-30bf97a8e090.png" title="GPT-4 从 Markdown 表格中回答关于一组开支的问题。">
</p>

<p align="center">
  <img width="550" src="https://user-images.githubusercontent.com/89960/233507395-b8ecb641-726c-4e57-b85e-13f1b7717f22.png" title="GPT-4 从 Markdown 表格中回答关于一组开支的问题。">
</p>

> 🧠 注意，在这个最后一个示例中，表中的项目有明确的日期：2月2日。在我们的问题中，我们问了“今天”。而在提示词 earlier 部分我们提到今天是2月2日。模型正确处理了传递性推理——将“今天”转换为“2月2日”，然后在表中查找“2月2日”。

#### JSON

Markdown 表格在许多用例中效果非常好，并且由于密度高且模型能可靠处理而应优先使用，但你可能会遇到以下场景：列非常多导致模型难以处理，或者每个项目都有自定义属性，此时拥有数十列空数据毫无意义。

在这些场景中，JSON 是另一种模型处理得非常好的格式。`keys` 与 `values` 的紧密相邻使模型很容易保持映射清晰。

以下是 Markdown 表格的相同示例，但改用 JSON：

<p align="center">
  <img width="550" src="https://user-images.githubusercontent.com/89960/233507559-26e6615d-4896-4a2c-b6ff-44cbd7d349dc.png" title="GPT-4 从 JSON 块中回答关于一组开支的问题。">
</p>

#### 自由文本

偶尔你希望在提示词中包含自由文本，并希望将其与提示词的其余部分区分开来——例如嵌入供机器人参考的文档。在这些场景中，用三个反引号 ```` ``` ```` 包围文档效果很好[^8]。

<p align="center">
  <img width="550" src="https://user-images.githubusercontent.com/89960/233507684-93222728-e216-47b4-8554-04acf9ec6201.png" title="GPT-4 从 JSON 块中回答关于一组开支的问题。">
</p>

[^8]: 一个很好的经验法则是，在提示词中做任何事情时，都要 heavily rely on 模型从 GitHub 学到的内容。

#### 嵌套数据

并非所有数据都是扁平线性的。有时你需要嵌入具有嵌套关系或与其他数据有关联的数据。在这些场景中，依赖 `JSON`：

<p align="center">
  <img width="550" src="https://user-images.githubusercontent.com/89960/233507758-7baffcaa-647b-4869-9cfb-a7cf8849c453.png" title="GPT-4 非常可靠地处理嵌套 JSON。">
</p>

<details>
<summary>(完整提示词)</summary>

~~~
You are a helpful assistant. You answer questions about users. Here is what you know about them:

{
  "users": [
    {
      "id": 1,
      "name": "John Doe",
      "contact": {
        "address": {
          "street": "123 Main St",
          "city": "Anytown",
          "state": "CA",
          "zip": "12345"
        },
        "phone": "555-555-1234",
        "email": "johndoe@example.com"
      }
    },
    {
      "id": 2,
      "name": "Jane Smith",
      "contact": {
        "address": {
          "street": "456 Elm St",
          "city": "Sometown",
          "state": "TX",
          "zip": "54321"
        },
        "phone": "555-555-5678",
        "email": "janesmith@example.com"
      }
    },
    {
      "id": 3,
      "name": "Alice Johnson",
      "contact": {
        "address": {
          "street": "789 Oak St",
          "city": "Othertown",
          "state": "NY",
          "zip": "67890"
        },
        "phone": "555-555-2468",
        "email": "alicejohnson@example.com"
      }
    },
    {
      "id": 4,
      "name": "Bob Williams",
      "contact": {
        "address": {
          "street": "135 Maple St",
          "city": "Thistown",
          "state": "FL",
          "zip": "98765"
        },
        "phone": "555-555-8642",
        "email": "bobwilliams@example.com"
      }
    },
    {
      "id": 5,
      "name": "Charlie Brown",
      "contact": {
        "address": {
          "street": "246 Pine St",
          "city": "Thatstown",
          "state": "WA",
          "zip": "86420"
        },
        "phone": "555-555-7531",
        "email": "charliebrown@example.com"
      }
    },
    {
      "id": 6,
      "name": "Diane Davis",
      "contact": {
        "address": {
          "street": "369 Willow St",
          "city": "Sumtown",
          "state": "CO",
          "zip": "15980"
        },
        "phone": "555-555-9512",
        "email": "dianedavis@example.com"
      }
    },
    {
      "id": 7,
      "name": "Edward Martinez",
      "contact": {
        "address": {
          "street": "482 Aspen St",
          "city": "Newtown",
          "state": "MI",
          "zip": "35742"
        },
        "phone": "555-555-6813",
        "email": "edwardmartinez@example.com"
      }
    },
    {
      "id": 8,
      "name": "Fiona Taylor",
      "contact": {
        "address": {
          "street": "531 Birch St",
          "city": "Oldtown",
          "state": "OH",
          "zip": "85249"
        },
        "phone": "555-555-4268",
        "email": "fionataylor@example.com"
      }
    },
    {
      "id": 9,
      "name": "George Thompson",
      "contact": {
        "address": {
          "street": "678 Cedar St",
          "city": "Nexttown",
          "state": "GA",
          "zip": "74125"
        },
        "phone": "555-555-3142",
        "email": "georgethompson@example.com"
      }
    },
    {
      "id": 10,
      "name": "Helen White",
      "contact": {
        "address": {
          "street": "852 Spruce St",
          "city": "Lasttown",
          "state": "VA",
          "zip": "96321"
        },
        "phone": "555-555-7890",
        "email": "helenwhite@example.com"
      }
    }
  ]
}
~~~
</details>

如果使用嵌套 `JSON` 导致你的 Token 预算过于冗长，可以回退到用 `Markdown` 定义的 `关系表`：

<p align="center">
  <img width="550" src="https://user-images.githubusercontent.com/89960/233507968-a378587b-e468-4882-a1e8-678d9f3933d3.png" title="GPT-4 处理关系表也相当可靠。">
</p>

<details>
<summary>(完整提示词)</summary>

~~~
You are a helpful assistant. You answer questions about users. Here is what you know about them:

Table 1: users
| id (PK) | name          |
|---------|---------------|
| 1       | John Doe      |
| 2       | Jane Smith    |
| 3       | Alice Johnson |
| 4       | Bob Williams  |
| 5       | Charlie Brown |
| 6       | Diane Davis   |
| 7       | Edward Martinez |
| 8       | Fiona Taylor  |
| 9       | George Thompson |
| 10      | Helen White   |

Table 2: addresses
| id (PK) | user_id (FK) | street      | city       | state | zip   |
|---------|--------------|-------------|------------|-------|-------|
| 1       | 1            | 123 Main St | Anytown    | CA    | 12345 |
| 2       | 2            | 456 Elm St  | Sometown   | TX    | 54321 |
| 3       | 3            | 789 Oak St  | Othertown  | NY    | 67890 |
| 4       | 4            | 135 Maple St | Thistown  | FL    | 98765 |
| 5       | 5            | 246 Pine St | Thatstown  | WA    | 86420 |
| 6       | 6            | 369 Willow St | Sumtown  | CO    | 15980 |
| 7       | 7            | 482 Aspen St | Newtown   | MI    | 35742 |
| 8       | 8            | 531 Birch St | Oldtown   | OH    | 85249 |
| 9       | 9            | 678 Cedar St | Nexttown  | GA    | 74125 |
| 10      | 10           | 852 Spruce St | Lasttown | VA    | 96321 |

Table 3: phone_numbers
| id (PK) | user_id (FK) | phone       |
|---------|--------------|-------------|
| 1       | 1            | 555-555-1234 |
| 2       | 2            | 555-555-5678 |
| 3       | 3            | 555-555-2468 |
| 4       | 4            | 555-555-8642 |
| 5       | 5            | 555-555-7531 |
| 6       | 6            | 555-555-9512 |
| 7       | 7            | 555-555-6813 |
| 8       | 8            | 555-555-4268 |
| 9       | 9            | 555-555-3142 |
| 10      | 10           | 555-555-7890 |

Table 4: emails
| id (PK) | user_id (FK) | email                 |
|---------|--------------|-----------------------|
| 1       | 1            | johndoe@example.com   |
| 2       | 2            | janesmith@example.com |
| 3       | 3            | alicejohnson@example.com |
| 4       | 4            | bobwilliams@example.com |
| 5       | 5            | charliebrown@example.com |
| 6       | 6            | dianedavis@example.com |
| 7       | 7            | edwardmartinez@example.com |
| 8       | 8            | fionataylor@example.com |
| 9       | 9            | georgethompson@example.com |
| 10      | 10           | helenwhite@example.com |

Table 5: cities
| id (PK) | name         | state | population | median_income |
|---------|--------------|-------|------------|---------------|
| 1       | Anytown     | CA    | 50,000     | $70,000      |
| 2       | Sometown    | TX    | 100,000    | $60,000      |
| 3       | Othertown   | NY    | 25,000     | $80,000      |
| 4       | Thistown    | FL    | 75,000     | $65,000      |
| 5       | Thatstown   | WA    | 40,000     | $75,000      |
| 6       | Sumtown     | CO    | 20,000     | $85,000      |
| 7       | Newtown     | MI    | 60,000     | $55,000      |
| 8       | Oldtown     | OH    | 30,000     | $70,000      |
| 9       | Nexttown    | GA    | 15,000     | $90,000      |
| 10      | Lasttown    | VA    | 10,000     | $100,000     |
~~~

</details>

> 🧠 模型在处理 [第三范式](https://en.wikipedia.org/wiki/Third_normal_form) 数据时表现良好，但可能在处理过多连接时遇到困难。在实验中，它似乎能很好地处理至少三层嵌套连接。在上述示例中，模型成功地将 `users` 连接到 `addresses` 再到 `cities`，从而推断出 George 的可能收入为 $90,000。

### 引用来源

通常，自然语言回复本身是不够的，你希望模型的输出能够引用数据来源。

这里有一个有用的注意事项：任何你想要引用的内容都应该有唯一的 ID。最简单的方法是直接要求模型链接到它引用的任何内容：

<p align="center">
  <img width="550" src="https://user-images.githubusercontent.com/89960/233509069-1dcbffa2-8357-49b5-be43-9791f93bd0f8.png" title="如果你要求，GPT-4 会可靠地链接到数据。">
</p>

### 程序化解析

默认情况下，语言模型输出自然语言文本，但通常我们需要以超出简单打印在屏幕上的方式与这些结果进行交互。你可以通过要求模型以你最爱的序列化格式（JSON 和 YAML 似乎效果最佳）输出结果来实现这一点。

确保给模型一个你想要的输出格式示例。基于我们之前的旅行示例，我们可以扩充提示词来告诉它：

~~~
Produce your output as JSON. The format should be:
```
{
    message: "The message to show the user",
    hotelId: 432,
    flightId: 831
}
```

Do not include the IDs in your message.
~~~

现在我们将得到这样的交互：

<p align="center">
  <img width="550" src="https://user-images.githubusercontent.com/89960/233509174-be0c3bc5-08e3-4d1a-8841-52c401def770.png" title="GPT-4 提供易于处理的旅行推荐。">
</p>

你可以想象 UI 将此消息渲染为普通文本，然后添加预订航班+酒店的离散按钮，或为用户自动填充表单。

作为另一个示例，让我们基于 [引用来源](#citations) 示例构建——但超越 Markdown 链接。我们可以要求它生成 JSON，包含一条正常消息以及用于创建该消息的项目列表。在这种场景下，你不知道确切在消息的哪个位置使用了引用，但你知道它们在某处被使用了。

<p align="center">
  <img width="550" src="https://user-images.githubusercontent.com/89960/233509280-59d9ff46-0e95-48a-b314-a7d2b7c9bfa3.png" title="要求模型提供引用列表是可靠地以编程方式知道模型在响应中依赖哪些数据的方法。">
</p>

> 🧠 有趣的是，在模型回答“我在 Target 花了多少钱？”时，它提供了一个单一值 $188.16，但**重要的是**在 `citations` 数组中列出了用于计算该值的单独开支项。

### 思维链（Chain of Thought）

有时你会对着提示词苦思冥想试图让模型输出可靠的结果，但无论你怎么做就是不行。这通常发生在机器人的最终输出需要中间思考过程，但你只要求机器人提供输出而不做任何其他操作时。

答案可能会让你惊讶：要求机器人展示它的工作过程。2022年10月，Google 发布了一篇论文 [《思维链提示词在大型语言模型中激发推理能力》](https://arxiv.org/pdf/2201.11903.pdf)，他们展示了如果在隐藏提示词中给机器人提供通过展示工作过程来回答问题的示例，那么当你要求机器人回答问题时，它会展示工作过程并产生更可靠的答案。

就在该论文发表几周后，即2022年10月底，东京大学和 Google 发布了论文 [《大型语言模型是零样本推理者》](https://openreview.net/pdf?id=e2TBb5y0yFf)，他们展示了你甚至不需要提供示例——**你只需要要求机器人逐步思考**。

#### 计算平均值

这是一个我们要求计算机器人计算平均开支（排除 Target）的示例。实际答案是 $136.77，机器人几乎算对了，得到 $136.43。

<p align="center">
  <img width="550" src="https://user-images.githubusercontent.com/89960/233509534-2b32c8dd-a1ee-42ea-82fb-4f84cfe7e9ba.png" title="模型 **几乎** 算对了平均值，但差了几美分。">
</p>

如果我们只是加上“让我们逐步思考”，模型就会得到正确答案：

<p align="center">
  <img width="550" src="https://user-images.githubusercontent.com/89960/233509608-6e53995b-668b-47f6-9b5e-67afad89f8bc.png" title="当我们要求模型展示工作过程时，它得到了正确答案。">
</p>

#### 代码解读

让我们回顾一下之前的 Python 示例，并将思维链提示词应用到我们的问题中。提醒一下，当我们要机器人评估这段 Python 代码时，它稍微出错了。正确答案是 `Hello, Brex!!Brex!!Brex!!!`，但机器人在包含多少个感叹号上感到困惑。在下面的示例中，它输出的是 `Hello, Brex!!!Brex!!!Brex!!!`:

<p align="center">
  <img width="550" src="https://user-images.githubusercontent.com/89960/233509724-8f3302f8-59eb-4d4b-8939-53d7f63b0299.png" title="机器人几乎正确解释了 Python 代码，但有点偏差。">
</p>

如果我们要求机器人展示它的工作过程，它就会得到正确答案：

<p align="center">
  <img width="550" src="https://user-images.githubusercontent.com/89960/233509790-2a0f2189-d864-4d27-aacb-cfc936fad907.png" title="如果你要求机器人展示工作过程，它会正确解释 Python 代码。">
</p>

#### 分隔符

在许多场景中，你可能不想向最终用户展示机器人的所有思考过程，而只想展示最终答案。你可以要求机器人将最终答案与其思考过程区分开。有很多方法可以做到这一点，但让我们使用 JSON 以便于解析：

<p align="center">
  <img width="550" src="https://user-images.githubusercontent.com/89960/233509865-4f3e7265-6645-4d43-8644-ecac5c0ca4a7.png" title="机器人展示工作过程的同时也分隔了最终答案以便轻松提取。">
</p>

使用思维链提示词会消耗更多 Token，导致成本增加和延迟升高，但对于许多场景而言结果明显更可靠。当需要机器人尽可能可靠地执行复杂任务时，这是一个非常有价值的工具。

### 微调 (Fine Tuning)

有时无论你向模型抛出什么技巧，它就是不按你的意愿行事。在这些场景中，你**可以**回退到微调。这通常应作为最后的手段。

[微调](https://platform.openai.com/docs/guides/fine-tuning) 是获取已经训练好的模型，然后给它成千上万（或更多）的 `input:output` 示例对的过程。

它并不能消除对隐藏提示词的需求，因为你仍然需要嵌入动态数据，但它可能使提示词更小且更可靠。

#### 局限性

微调有许多缺点。如果有任何可能的话，利用语言模型作为 [零样本、单样本和少样本学习者](https://en.wikipedia.org/wiki/Few-shot_learning_(natural_language_processing)) 的特性，通过在提示词中教它们做某事而不是进行微调。

一些缺点包括：
- **不可行**：[GPT-3.5/GPT-4 无法微调](https://platform.openai.com/docs/guides/chat/is-fine-tuning-available-for-gpt-3-5-turbo)，这是我们主要使用的模型/API，所以我们根本无法依赖微调。
- **开销**：微调需要手动创建大量数据。
- **迭代速度**：迭代循环变得慢得多——每次你想添加新功能时，与其在提示词中添加几行代码，不如你需要创建一堆假数据，然后运行微调过程，最后使用新微调的模型。
- **成本**：使用微调后的 GPT-3 模型比使用标准的 `gpt-3.5-turbo` 模型贵多达 60 倍。而使用微调后的 GPT-3 模型比使用标准 GPT-4 模型贵 2 倍。

> ⛔️ 如果你微调了模型，**切勿使用真实的客户数据**。始终使用合成数据。模型可能会记住你提供的数据部分，并可能向不应看到它的其他用户复述私有数据。
>
> 如果你从不微调模型，我们就无需担心意外将数据泄露到模型中。

## 更多资源
- :star2: [OpenAI Cookbook](https://github.com/openai/openai-cookbook) :star2:
- :technologist: [提示词攻击 (Prompt Hacking)](https://learnprompting.org/docs/category/-prompt-hacking) :technologist: 
- :books: [Dair.ai 提示词工程指南](https://github.com/dair-ai/Prompt-Engineering-Guide) :books:
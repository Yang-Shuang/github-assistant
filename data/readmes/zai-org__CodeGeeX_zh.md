<img src="resources/logo/codegeex_logo.png">

<p align="center">
    🏠 <a href="https://codegeex.cn" target="_blank">官网</a> | 📖 <a href="https://models.aminer.cn/codegeex/blog/" target="_blank">博客</a> | 🪧 <a href="https://models.aminer.cn/codegeex/playground" target="_blank">在线体验 (DEMO)</a> | 🤖 <a href="https://codegeex.cn/download/request" target="_blank">下载模型</a> | 📄 <a href="https://arxiv.org/abs/2303.17568" target="_blank">论文</a> | 🌐 <a href="README_zh.md" target="_blank">中文</a>
</p>
<p align="center">
    🛠 <a href="https://marketplace.visualstudio.com/items?itemName=aminer.codegeex" target="_blank">VS Code 插件</a>, <a href="https://plugins.jetbrains.com/plugin/20587-codegeex" target="_blank">JetBrains 插件</a>, <a href="https://plugins.jetbrains.com/plugin/20587-codegeex" target="_blank">Cloud Studio 插件</a> | 👋 加入我们的 <a href="https://discord.gg/8gjHdkmAN6" target="_blank">Discord</a>, <a href="https://join.slack.com/t/codegeexworkspace/shared_invite/zt-1s118ffrp-mpKKhQD0tKBmzNZVCyEZLw" target="_blank">Slack</a>, <a href="https://t.me/+IipIayJ32B1jOTg1" target="_blank">Telegram</a>, <a href="resources/zh/wechat.md"target="_blank">微信</a>
</p>



🌟 最新的 [CodeGeeX4](https://github.com/THUDM/CodeGeeX4) 已发布。 | 最新一代 [CodeGeeX4](https://github.com/THUDM/CodeGeeX4) 模型已经正式开源。

- [CodeGeeX：多语言代码生成模型](#codegeex-a-multilingual-code-generation-model)
  - [更新动态](#news)
  - [快速开始](#getting-started)
    - [安装](#installation)
    - [模型权重](#model-weights)
    - [GPU 推理](#inference-on-gpus)
    - [VS Code 与 JetBrains 插件使用指南](#vs-code-and-jetbrains-extension-guidance)
  - [CodeGeeX：架构、代码语料库与实现细节](#codegeex-architecture-code-corpus-and-implementation)
  - [HumanEval-X：多语言程序合成的新基准测试集](#humaneval-x-a-new-benchmark-for-multilingual-program-synthesis)
    - [多语言代码生成](#multilingual-code-generation)
    - [跨语言代码翻译](#crosslingual-code-translation)
    - [如何使用 HumanEval-X 并为其做贡献？](#how-to-use-humaneval-x-and-contribute-to-it)
  - [许可证](#license)
  - [引用](#citation)

# CodeGeeX：多语言代码生成模型

我们推出了 CodeGeeX，这是一个拥有 130 亿参数的多语言代码生成大模型，在包含超过 20 种编程语言的庞大代码语料库上进行预训练。截至 **2022年6月22日**，CodeGeeX 已在由 1,536 块 [Ascend 910 AI Processor](https://e.huawei.com/en/products/servers/ascend)（昇腾）组成的集群上完成了超过 8,500 亿 token 的训练。CodeGeeX 具有以下独特功能：
* **多语言代码生成**：CodeGeeX 在多种主流编程语言（包括 Python、C++、Java、JavaScript、Go 等）的可执行程序生成方面表现优异。[在线体验](https://models.aminer.cn/codegeex)
* **跨语言代码翻译**：CodeGeeX 支持在不同编程语言之间进行代码片段的转换。只需一键，即可将程序高精度地转换为任意目标语言。[在线体验](https://models.aminer.cn/codegeex/codeTranslator)
* **可定制的编程助手**：CodeGeeX 在 VS Code 插件市场中**免费**提供。它支持代码补全、解释、摘要等功能，为用户带来更佳的编码体验。[VS Code 扩展](https://marketplace.visualstudio.com/items?itemName=aminer.codegeex)
* **开源与跨平台**：所有代码和模型权重均公开用于研究目的。CodeGeeX 同时支持昇腾（Ascend）和 NVIDIA 平台，可在单块 Ascend 910、NVIDIA V100 或 A100 GPU 上进行推理。[申请模型权重](https://models.aminer.cn/codegeex/download/request)

**面向真实多语言基准测试的 HumanEval-X。** 为了规范多语言代码生成与翻译的评估，我们开发并发布了 **HumanEval-X** 基准数据集。HumanEval-X 是一个全新的多语言评测集，包含 **5** 种编程语言（Python、C++、Java、JavaScript 和 Go）下的 **820 个人工编写**编程问题，每个问题均附有测试用例与参考答案。[使用指南](codegeex/benchmark/README.md) [🤗 HuggingFace 数据集](https://huggingface.co/datasets/THUDM/humaneval-x)

<img src="resources/en/hx_boxplot.png">

<p align="center"><i>与其他开源多语言基线模型相比，CodeGeeX 取得了最高的平均性能。</i></p>

## 更新动态

* 🌟 **2023-07-24**：[CodeGeeX2](https://github.com/THUDM/CodeGeeX2) 已发布，功能更强大、速度更快且更加轻量。支持 100+ 种编程语言及多项新功能。

* **2023-05-16**：CodeGeeX 论文已被 [KDD 2023（长滩）](https://kdd.org/kdd2023/) 接收，并将在会议上进行展示。

* **2023-03-30**：CodeGeeX 论文现已在 [arxiv](https://arxiv.org/abs/2303.17568) 公开。

* **2023-02-14**：CodeGeeX 现已支持腾讯推出的优秀 Web IDE [Cloud Studio](https://cloudstudio.net/)。点击本页面顶部的徽章即可快速启动环境体验 CodeGeeX。

* **2023-02-13**：感谢 [OneFlow](https://github.com/Oneflow-Inc/oneflow) 团队为 CodeGeeX 推理添加了 OneFlow 后端（在 FP16 下甚至比 FasterTransformer 更快！）。更多详情请查看[此处](https://github.com/THUDM/CodeGeeX/pull/65)。

* **2023-02**：我们正在举办 CodeGeeX “Coding With AI” 黑客松活动 [CodeGeeX "Coding With AI" Hackathon](https://dorahacks.io/hackathon/codegeex/)，基于 CodeGeeX 设计酷炫的应用并赢取奖品（RTX 4090、DJI 无人机等）！

* **2022-12-31**：我们在 [codegeex-fastertransformer](https://github.com/CodeGeeX/codegeex-fastertransformer) 发布了 CodeGeeX 的 FasterTransformer 版本。INT8 加速版本的平均速度达到 <15ms/token。祝大家新年快乐！

* **2022-12-13**：我们在 [codegeex-vscode-extension](https://github.com/CodeGeeX/codegeex-vscode-extension) 开源了 CodeGeeX VS Code 扩展的源码。请参照[快速开始](https://github.com/CodeGeeX/codegeex-vscode-extension/blob/main/doc/quickstart.md)启动开发。

* **2022-12-11**：CodeGeeX 现已支持 JetBrains IDE（IntelliJ IDEA、PyCharm、GoLand、CLion 等），请在此[下载](https://plugins.jetbrains.com/plugin/20587-codegeex)。

* **2022-12-04**：我们发布了量化版本源码（显存需求更低：27GB -> 15GB）和模型并行化方案（可在多块 <8G 显存的 GPU 上运行）。
 
* **2022-09-30**：我们开源了同时支持昇腾和 NVIDIA 平台的代码及模型权重。

## 快速开始

CodeGeeX 最初基于 MindSpore 实现，并在昇腾 910 AI Processor 上进行训练。我们提供了一个基于 [Megatron-LM](https://github.com/NVIDIA/Megatron-LM) 的 PyTorch 兼容版本，以便在 GPU 平台上使用。
### 安装

需要 Python 3.7+、CUDA 11+、PyTorch 1.10+ 和 DeepSpeed 0.6+。通过以下命令安装 ``codegeex`` 包： 
```bash
git clone git@github.com:THUDM/CodeGeeX.git
cd CodeGeeX
pip install -e .
```
或者使用 [CodeGeeX Docker 镜像](https://hub.docker.com/r/codegeex/codegeex) 快速搭建环境（需已安装 [nvidia-docker](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#docker)）：
```bash
docker pull codegeex/codegeex:latest
# 若要启用 GPU 支持，请通过 --device 指定设备 ID
docker run --gpus '"device=0,1"' -it --ipc=host --name=codegeex codegeex/codegeex
```

### 模型权重

通过此[链接](https://models.aminer.cn/codegeex/download/request)申请并下载模型权重。你将收到一封包含临时下载链接的邮件（``urls.txt``）。我们建议使用 [aria2](https://aria2.github.io/) 按以下命令进行下载（请确保有足够的磁盘空间来下载 checkpoint，约 26GB）：
```bash
aria2c -x 16 -s 16 -j 4 --continue=true -i urls.txt 
```
运行以下命令合并并解压完整的模型权重文件：
```bash
cat codegeex_13b.tar.gz.* > codegeex_13b.tar.gz
tar xvf codegeex_13b.tar.gz
```

### GPU 推理

使用 CodeGeeX 生成第一个程序。首先，在 ``configs/codegeex_13b.sh`` 中指定模型权重路径。其次，将提示词（自然语言描述或代码片段）写入文件，例如 ``tests/test_prompt.txt``，然后运行以下脚本：
```bash
# 单卡推理（显存需大于 27GB）
bash ./scripts/test_inference.sh <GPU_ID> ./tests/test_prompt.txt

# 量化推理（显存需大于 15GB）
bash ./scripts/test_inference_quantized.sh <GPU_ID> ./tests/test_prompt.txt

# 多卡推理（每卡显存需大于 6GB，需先将 ckpt 转换为 MP_SIZE 分区）
bash ./scripts/convert_ckpt_parallel.sh <LOAD_CKPT_PATH> <SAVE_CKPT_PATH> <MP_SIZE>
bash ./scripts/test_inference_parallel.sh <MP_SIZE> ./tests/test_prompt.txt
```

### VS Code 与 JetBrains 插件使用指南

基于 CodeGeeX，我们还开发了免费的 VS Code 和 JetBrains IDE 插件，未来还将推出更多。 

对于 VS Code，可在插件市场中搜索 "codegeex" 或在此[安装](https://marketplace.visualstudio.com/items?itemName=aminer.codegeex)。详细说明请参见 [VS Code 扩展使用指南](vscode-extension/README.md)。开发者也可在 [codegeex-vscode-extension](https://github.com/CodeGeeX/codegeex-vscode-extension) 获取源码，请参照 [快速开始](https://github.com/CodeGeeX/codegeex-vscode-extension/blob/main/doc/quickstart.md) 进行开发。

对于 JetBrains IDE，可在插件市场中搜索 "codegeex" 或在此[安装](https://plugins.jetbrains.com/plugin/20587-codegeex)。 
请确保你的 IDE 版本为 2021.1 或更高。CodeGeeX 现已支持 IntelliJ IDEA、PyCharm、GoLand、CLion、Android Studio、AppCode、Aqua、DataSpell、DataGrip、Rider、RubyMine 和 WebStorm。 

## CodeGeeX：架构、代码语料库与实现细节

**架构**：CodeGeeX 是一个基于 Transformer 的大规模预训练编程语言模型。它是一个从左到右的自回归解码器，以代码和自然语言为输入，预测下一个 token（词元）的概率。CodeGeeX 包含 40 层 Transformer 层，自注意力块的隐藏层大小为 5,120，前馈层的隐藏层大小为 20,480，参数量达到 130 亿。它支持的最大序列长度为 2,048。

<img src="resources/en/codegeex_training.png">
<p align="center"><i><b>左：</b> CodeGeeX 训练数据中各编程语言的占比。<b>右：</b> CodeGeeX 训练损失随训练步数变化的曲线。</i></p>

**代码语料库**：我们的训练数据包含两部分。第一部分来自开源代码数据集，[The Pile](https://pile.eleuther.ai/) 和 [CodeParrot](https://github.com/huggingface/transformers/tree/main/examples/research_projects/codeparrot)。The Pile 包含一个代码子集，收集了 GitHub 上星标数超过 100 的公开仓库，我们从中筛选出 23 种流行编程语言的代码。第二部分是从未出现在之前数据集中的公共 GitHub 仓库中直接爬取的补充数据，包括 Python、Java 和 C++。为了获取可能更高质量的数据，我们选择了至少拥有 1 个星标且大小小于 10MB 的仓库。如果文件满足以下条件之一则会被过滤：1) 平均每行字符数超过 100；2) 为自动生成代码；3) 字母比例低于 40%；4) 文件大小大于 100KB 或小于 1KB。为了帮助模型区分不同语言，我们在每个数据段开头添加了特定语言的标记，格式为 ``[注释符号] language: [LANG]``，例如 ``# language: Python``。在分词方面，我们使用与 GPT-2 相同的 tokenizer，并将空白字符作为额外 token 处理，最终词汇表大小为 50,400。总体而言，该代码语料库涵盖 23 种编程语言，共计 1,587B tokens。

**训练过程**：我们在 [MindSpore 1.7](https://www.mindspore.cn/) 中实现了 CodeGeeX，并在 1,536 块昇腾 910 AI Processor（32GB）上进行训练。模型权重采用 FP16 格式，但层归一化（layer-norm）和 softmax 使用 FP32 以保证更高的精度和稳定性。整个模型占用约 27GB 显存。为了提高训练效率，我们采用了 8 路模型并行与 192 路数据并行的混合策略，并启用了 ZeRO-2 优化器。微批次大小（micro-batch size）为 16，全局批次大小达到 3,072。此外，我们还采用了元素级算子融合、快速 gelu 激活函数、矩阵乘法维度优化等技术进一步提升训练效率。整个训练过程历时近两个月（从 2022年4月18日 至 6月22日），共输入了 850B tokens 进行训练，即超过 5 个 epoch。

## HumanEval-X：多语言程序合成的新基准测试集
为了更好地评估代码生成模型的多语言能力，我们提出了新的基准测试集 HumanEval-X。以往的研究通常使用语义相似度（如 [CodeBLEU](https://arxiv.org/abs/2009.10297)）来评估多语言程序合成，但这往往具有误导性；而 HumanEval-X 则直接评估生成代码的功能正确性。HumanEval-X 包含 Python、C++、Java、JavaScript 和 Go 共 5 种语言的 820 个高质量人工编写数据样本（每个均附有测试用例），可用于多种任务。

<img src="resources/en/hx_tasks.png">

<p align="center"><i><b>HumanEval-X</b> 支持的任务示意图。声明、文档字符串和解决方案分别用红色、绿色和蓝色标记。<b>代码生成</b>使用声明和文档字符串作为输入来生成解决方案。<b>代码翻译</b>使用两种语言的声明，并将源语言中的解决方案翻译成目标语言。</i></p>

在 HumanEval-X 中，每种语言的每个样本都包含函数声明、文档字符串和解决方案，可以以不同方式组合以支持生成、翻译、摘要等下游任务。我们目前重点关注两个任务：**代码生成**与**代码翻译**。对于代码生成，模型使用声明和文档字符串作为输入来生成解决方案。对于代码翻译，模型同时接收两种语言的声明以及源语言中的解决方案作为输入，以生成目标语言的解决方案。在代码翻译任务中，我们去除了自然语言描述，以防止模型直接解题。对于这两个任务，我们均采用 [Codex](https://arxiv.org/abs/2107.03374) 提出的无偏 pass@k 指标：$\text{pass}@k:= \mathbb{E}[1-\frac{\tbinom{n-c}{k}}{\tbinom{n}{k}}]$，其中 $n=200$，$k\in(1,10,100)$。

### 多语言代码生成

<img src="resources/en/hx_generattion_radar_horizon.png">
<p align="center"><i><b>左</b>：HumanEval-X 中五种语言在代码生成任务上的详细 pass@k (k=1,10,100) 性能。<b>右</b>：各模型在所有语言上的平均表现。与其他开源模型（InCoder-6.7B、CodeGen-Multi-6B 和 CodeGen-Multi-16B）相比，CodeGeeX 取得了最高的平均性能。</i></p>


我们将 CodeGeeX 与另外两个开源代码生成模型 [InCoder](https://github.com/dpfried/incoder)（Meta）和 [CodeGen](https://github.com/salesforce/CodeGen)（Salesforce）进行了对比。具体评估了 InCoder-6.7B、CodeGen-Multi-6B 和 CodeGen-Multi-16B。CodeGeeX 在性能上显著优于参数量更小的模型（高出 7.5%~16.3%），并与参数量更大的 CodeGen-Multi-16B 相当（平均性能 54.76% vs. 54.39%）。CodeGeeX 在各语言上的平均表现最佳。

### 跨语言代码翻译

<img src="resources/en/hx_translation.png">

<p align="center"><i>HumanEval-X <b>代码翻译</b>任务结果。各语言下的最优成绩已<b>加粗</b>显示。</i></p>

我们还评估了跨编程语言翻译的性能。我们测试了 CodeGeeX 的零样本（zero-shot）性能，以及微调后的 CodeGeeX-13B-FT（使用 [XLCoST](https://github.com/reddy-lab-code-research/XLCoST) 代码翻译任务训练集进行微调；原始数据集中缺少 Go，因此我们为其补充了一小部分）。结果表明模型存在语言偏好，例如：CodeGeeX 擅长将其他语言翻译成 Python 和 C++，而 CodeGen-Multi-16B 更擅长翻译成 JavaScript 和 Go；这可能与训练语料库中的语言分布差异有关。在 20 个翻译对中，我们还观察到 A→B 与 B→A 的性能始终呈负相关，这可能表明当前模型尚无法很好地掌握所有语言。 

### 如何使用 HumanEval-X 并为其做贡献？

关于如何使用的更多详情，请参见[使用指南](codegeex/benchmark/README.md)。我们非常欢迎社区通过添加更多问题或将其扩展到其他语言来为 HumanEval-X 做出贡献。请先查看 HumanEval-X 的[标准格式](codegeex/benchmark/README.md#how-to-use-humaneval-x)并提交 Pull Request。 

如有任何意见或建议，请通过 [codegeex@aminer.cn](mailto:codegeex@aminer.cn) 联系我们。

<details>
<summary><b>生成示例</b></summary>
<img src="resources/en/hx_examples.png">
</details>

<details>
<summary><b>致谢</b></summary>
<br/>
本项目由国家杰出青年科学基金（No. 61825602）资助。 

### 核心贡献者

Qinkai Zheng ([Tsinghua KEG](http://keg.cs.tsinghua.edu.cn/glm-130b/)), Xiao Xia (清华大学 KEG), Xu Zou (清华大学 KEG)

### 贡献者

清华大学 KEG（知识工程组）：Aohan Zeng, Wendi Zheng, Lilong Xue

清华大学 IIIS（交叉信息研究院）Zhilin Yang 课题组：Yifeng Liu, Yanru Chen, Yichen Xu (北京邮电大学，工作期间访问清华大学)

鹏城实验室：Qingyu Chen, Zhongqi Li, Gaojun Fan

智谱 AI：Yufei Xue, Shan Wang, Jiecai Shan, Haohan Jiang, Lu Liu, Xuan Xue, Peng Zhang

昇腾与 MindSpore 团队：Yifan Yao, Teng Su, Qihui Deng, Bin Zhou

### 数据标注

Ruijie Cheng (清华大学), Peinan Yu (清华大学), Jingyao Zhang (智谱 AI), Bowen Huang (智谱 AI), Shaoyu Wang (智谱 AI) 
    
### 指导教师

[Zhilin Yang](https://kimiyoung.github.io/) (清华大学 IIIS), Yuxiao Dong (清华大学 KEG), Wenguang Chen (清华大学 PACMAN), Jie Tang (清华大学 KEG)
    

### 算力支持单位

[鹏城实验室](https://www.pcl.ac.cn/index.html)

[智谱 AI](https://www.zhipu.ai/)——致力于让机器像人类一样思考的 AI 初创公司

### 项目负责人 

[Jie Tang](http://keg.cs.tsinghua.edu.cn/jietang/) (清华大学 KEG & BAAI)
</details>

## 许可证

我们的代码遵循 [Apache-2.0 许可证](LICENSE)。
我们的模型遵循[特定许可证](MODEL_LICENSE)。

## 引用

如果您觉得我们的工作有用，请引用：

```
@inproceedings{zheng2023codegeex,
  title={CodeGeeX: A Pre-Trained Model for Code Generation with Multilingual Benchmarking on HumanEval-X},
  author={Qinkai Zheng and Xiao Xia and Xu Zou and Yuxiao Dong and Shan Wang and Yufei Xue and Zihan Wang and Lei Shen and Andi Wang and Yang Li and Teng Su and Zhilin Yang and Jie Tang},
  booktitle={Proceedings of the 29th ACM SIGKDD Conference on Knowledge Discovery and Data Mining},
  pages={5673--5684},
  year={2023}
}
```
# Agent Laboratory：将大语言模型智能体作为研究助手

<p align="center">
  <img src="media/AgentLabLogo.png" alt="Demonstration of the flow of AgentClinic" style="width: 99%;">
</p>

<p align="center">
    【English | <a href="readme/README-chinese.md">中文</a> | <a href="readme/README-japanese.md">日本語</a> | <a href="readme/README-korean.md">한국어</a> | <a href="readme/README-filipino.md">Filipino</a> | <a href="readme/README-french.md">Français</a> | <a href="readme/README-slovak.md">Slovenčina</a> | <a href="readme/README-portugese.md">Português</a> | <a href="readme/README-spanish.md">Español</a> | <a href="readme/README-turkish.md">Türkçe</a> | <a href="readme/README-hindi.md">हिंदी</a> | <a href="readme/README-bengali.md">বাংলা</a> | <a href="readme/README-vietnamese.md">Tiếng Việt</a> | <a href="readme/README-russian.md">Русский</a> | <a href="readme/README-arabic.md">العربية</a> | <a href="readme/README-farsi.md">فارسی</a> | <a href="readme/README-italian.md">Italiano</a>】
</p>

<p align="center">
    【📝 <a href="https://arxiv.org/pdf/2501.04227">Paper</a> | 🌐 <a href="https://agentlaboratory.github.io/">Website</a> | 🌐 <a href="https://agentrxiv.github.io/">AgentRxiv Website</a> | 💻 <a href="https://github.com/SamuelSchmidgall/AgentLaboratory">Software</a> | 📰 <a href="https://agentlaboratory.github.io/#citation-ref">Citation</a>】
</p>

### 最新动态 
* [2025年3月24日] 🎉 🎊 🎉 现已推出 **AgentRxiv**，这是一个让自主研究智能体能够上传、检索并基于彼此研究成果进行构建的框架。这使得智能体能够在其研究中实现累积性进展。

## 📖 概述

- **Agent Laboratory** 是一个端到端的自主研究工作流，旨在协助作为人类研究者的**你**实现**你的研究构想**。Agent Laboratory 由大语言模型（LLM）驱动的专业智能体组成，支持你完成整个研究工作流——从文献综述和计划制定，到实验执行和撰写综合报告。 
- 该系统并非旨在取代你的创造力，而是对其进行补充，使你能够专注于构思和批判性思维，同时将编码和文档编写等重复且耗时的任务自动化。通过适应不同级别的计算资源和人类参与度，Agent Laboratory 旨在加速科学发现并优化你的研究生产力。
<p align="center">
  <img src="media/AgentLab.png" alt="Demonstration of the flow of AgentClinic" style="width: 99%;">
</p>

- Agent Laboratory 还支持 **AgentRxiv**，这是一个让自主研究智能体能够上传、检索并基于彼此研究成果进行构建的框架。这使得智能体能够在其研究中实现累积性进展。

<p align="center">
  <img src="media/agentrxiv.png" alt="Demonstration of the flow of AgentClinic" style="width: 99%;">
</p>


### 🔬 Agent Laboratory 如何工作？

- Agent Laboratory 包含三个主要阶段，系统地引导研究过程：（1）文献综述、（2）实验执行和（3）报告撰写。在每个阶段中，由大语言模型驱动的专业智能体会协作完成各自的目标，并整合 arXiv、Hugging Face、Python 和 LaTeX 等外部工具以优化结果。该结构化工作流始于独立收集和分析相关研究论文，经过协同规划和数据准备，最终实现自动化实验和综合报告生成。有关这些阶段中具体智能体角色及其贡献的详细信息，请参阅论文。

<p align="center">
  <img src="media/AgentLabWF.png" alt="Demonstration of the flow of AgentClinic" style="width: 99%;">
</p>


### 👾 目前支持的模型

* **OpenAI**：o1、o1-preview、o1-mini、gpt-4o、o3-mini
* **DeepSeek**：deepseek-chat（deepseek-v3）

要选择特定的大语言模型，请设置标志 `--llm-backend="llm_model"`，例如 `--llm-backend="gpt-4o"` 或 `--llm-backend="deepseek-chat"`。欢迎根据需求提交 PR 以支持新模型！

## 🖥️ 安装

### Python venv 选项

* 建议使用 Python 3.12

1. **克隆 GitHub 仓库**：首先使用以下命令克隆仓库：
```bash
git clone git@github.com:SamuelSchmidgall/AgentLaboratory.git
```

2. **设置并激活 Python 环境**
```bash
python -m venv venv_agent_lab
```
- 现在激活该环境：
```bash
source venv_agent_lab/bin/activate
```

3. **安装所需的库**
```bash
pip install -r requirements.txt
```

4. **安装 pdflatex [可选]**
```bash
sudo apt install pdflatex
```
- 这将允许智能体编译 LaTeX 源码。
- **[重要]** 如果因没有 sudo 权限而无法运行此步骤，可通过设置 `--compile-latex` 标志为 `false`（即 `--compile-latex "false"`）来关闭 PDF 编译功能。



5. **现在运行 Agent Laboratory！**

`python ai_lab_repo.py --yaml-location "experiment_configs/MATH_agentlab.yaml"`


### Co-Pilot 模式

要在 Co-Pilot 模式下运行 Agent Laboratory，只需在 YAML 配置中将 `copilot-mode` 标志设置为 `"true"`

-----
## 提升研究成果的技巧


#### [提示 #1] 📝 务必撰写详细的笔记！📝

**撰写详细笔记非常重要**，它能帮助你的智能体理解你在项目中希望完成的目标以及任何风格偏好。笔记可以包含你希望智能体执行的实验、提供 API 密钥、要求包含的特定图表或图片，或者你在进行研究时希望智能体知道的其他信息。

这也是你让智能体了解**其可访问的计算资源**的机会，例如 GPU（数量、类型、显存大小）、CPU（核心数、型号）、存储限制和硬件规格。

要添加笔记，你必须修改 `ai_lab_repo.py` 内部的 `task_notes_LLM` 结构。以下提供了一些我们在实验中使用的示例笔记： 


```
task-notes:
  plan-formulation:
    - 'You should come up with a plan for only ONE experiment aimed at maximizing performance on the test set of MATH using prompting techniques.'
    - 'Please use gpt-4o-mini for your experiments'
    - 'You must evaluate on the entire 500 test questions of MATH'
  data-preparation:
    - 'Please use gpt-4o-mini for your experiments'
    - 'You must evaluate on the entire 500 test questions of MATH'
    - 'Here is a sample code you can use to load MATH\nfrom datasets import load_dataset\nMATH_test_set = load_dataset("HuggingFaceH4/MATH-500")["test"]'
...
```

--------

#### [提示 #2] 🚀 使用更强大的模型通常能带来更好的研究成果 🚀

进行研究时，**模型的选择会显著影响结果的质量**。更强大的模型往往具有更高的准确性、更强的推理能力和更好的报告生成能力。如果计算资源允许，请优先使用 o1-(mini/preview) 或类似的最先进大语言模型。

然而，**平衡性能与成本效益非常重要**。虽然强大的模型可能产生更好的结果，但它们通常运行成本更高且耗时更长。建议选择性使用它们——例如用于关键实验或最终分析——而在迭代任务或初步原型开发中依赖更小、更高效的模型。

当资源受限时，可通过在特定数据集上微调较小模型，或将预训练模型与任务特定的提示词结合使用来优化，从而在性能与计算效率之间取得理想的平衡。

-----

#### [提示 #3] ✅ 你可以从检查点加载之前的存档 ✅

**如果你丢失了进度、断开了网络连接，或某个子任务失败，你始终可以从之前的状态加载。** 你的所有进度默认保存在 `state_saves` 变量中，该变量存储每个独立的检查点。 

-----


#### [提示 #4] 🈯 如果你使用非英语语言运行 🈲

如果你使用非英语语言运行 Agent Laboratory，没有问题，只需确保向智能体提供一个语言标志，以便用你首选的语言进行研究。请注意，我们尚未广泛研究在其他语言下运行 Agent Laboratory 的情况，因此请务必报告你遇到的任何问题。

例如，如果你使用中文运行，请在 YAML 中设置语言：

`language:  "中文"`

----


#### [提示 #5] 🌟 仍有大量改进空间 🌟

该代码库有大量的改进空间，如果你进行了更改并希望帮助社区，请随时分享你所做的修改！希望这个工具能对你有所帮助！


## 📜 许可证

源代码许可：本项目的源代码采用 MIT 许可证。该许可证允许在遵守 MIT 许可证所述特定条件的情况下使用、修改和分发代码。

## 📬 联系方式

如需联系，请随时发送邮件至 [sschmi46@jhu.edu](mailto:sschmi46@jhu.edu)

## 引用 / BibTeX


### Agent Laboratory
```bibtex
@misc{schmidgall2025agentlaboratoryusingllm,
      title={Agent Laboratory: Using LLM Agents as Research Assistants}, 
      author={Samuel Schmidgall and Yusheng Su and Ze Wang and Ximeng Sun and Jialian Wu and Xiaodong Yu and Jiang Liu and Michael Moor and Zicheng Liu and Emad Barsoum},
      year={2025},
      eprint={2501.04227},
      archivePrefix={arXiv},
      primaryClass={cs.HC},
      url={https://arxiv.org/abs/2501.04227}, 
}
```

### AgentRxiv
```bibtex
@misc{schmidgall2025agentrxiv,
      title={AgentRxiv: Towards Collaborative Autonomous Research}, 
      author={Samuel Schmidgall and Michael Moor},
      year={2025},
      eprint={2503.18102},
      archivePrefix={arXiv},
      primaryClass={cs.AI},
      url={https://arxiv.org/abs/2503.18102}, 
}
```
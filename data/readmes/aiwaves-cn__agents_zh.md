<div align="center">
<img src='./assets/agents-logo.png'  width=300px>

## <p align="center">Agents 2.0: Symbolic Learning Enables Self-Evolving Agents</p>

<p align="center">
<a href="https://aiwaves-cn.github.io/agents/">[🤖Project]</a>
<a href="https://arxiv.org/abs/2406.18532">[📄Paper]</a>
<a href="https://agentsv2.readthedocs.io/">[📝Docs]</a>
<a href="#overview">[🌟Overview]</a>
<a href="#installation">[🔧Installation]</a>
<a href="#citation">[🚩Citation]</a>
</p>

![](https://img.shields.io/badge/version-v2.0.0-blue)
[![License: Apache](https://img.shields.io/badge/License-Apache2.0-yellow.svg)](https://opensource.org/license/apache-2-0)
![](https://img.shields.io/github/last-commit/aiwaves-cn/agents?color=green)
![](https://img.shields.io/badge/PRs-Welcome-red) 

---

</div>


## 🔔更新动态
- [2024-06-25] 我们发布了 [Agents](https://agentsv2.readthedocs.io/en/latest/) 2.0，这是对原库的重大版本更新，新增了对智能体（Agent）学习与评估的支持。
---

## 🌟概述

智能体符号学习（Agent Symbolic Learning）是一种用于训练语言智能体的系统性框架，其灵感来源于神经网络训练中采用的联结主义学习流程。我们将语言智能体与神经网络进行类比：智能体的处理流水线对应神经网络的计算图，流水线中的节点对应网络中的一层，而节点的提示词（prompt）和工具则对应该层的权重。通过这种映射关系，我们能够在使用基于语言的损失函数、梯度及权重的智能体训练上下文中，实现联结主义学习的主要组件——即反向传播与基于梯度的权重更新。

<img src='./assets/overview.png'>

我们通过精心设计的提示词流水线，在智能体训练框架中实现了损失函数计算、反向传播机制与权重优化器。以单个训练样本为例，我们的框架首先执行“前向传递”（即智能体实际运行），并将每个节点中的输入、输出、提示词及工具调用记录在一个“轨迹（trajectory）”中。随后，我们利用基于提示词的损失函数对运行结果进行评估，生成“语言损失”。接着，我们沿该轨迹从末端节点向起始节点反向传播语言损失，从而为每个节点内的符号组件生成文本分析与反思内容，我们将其称为“语言梯度”。最后，我们借助另一组精心设计的提示词，依据这些语言梯度更新每个节点中的所有符号组件，以及由节点和连接构成的计算图。该方法也天然支持多智能体系统的优化：既可将不同节点视为独立智能体，也可允许单个节点内多个智能体协同执行动作。 

### 工作流程示意

<img src='./assets/workflow.gif'>

---


## 🔧安装指南

**从 Git 仓库分支安装：**
```
pip install git+https://github.com/aiwaves-cn/agents@master
```

**本地开发环境安装：**
```
git clone -b master https://github.com/aiwaves-cn/agents
cd agents
pip install -e .
```

---

## ⭐ Star 历史记录  
[![Star History Chart](https://api.star-history.com/svg?repos=aiwaves-cn/agents&type=Date)](https://star-history.com/#aiwaves-cn/agents&Date)

---

## 🚩引用方式

如果您的研究使用了本仓库，请考虑引用以下文献：
```bibtex
@article{zhou2024agents2,
      title={Symbolic Learning Enables Self-Evolving Agents}, 
      author={Wangchunshu Zhou and Yixin Ou and Shengwei Ding and Long Li and Jialong Wu and Tiannan Wang and Jiamin Chen and Shuai Wang and Xiaohua Xu and Ningyu Zhang and Huajun Chen and Yuchen Eleanor Jiang},
      year={2024},
      eprint={2406.18532},
      archivePrefix={arXiv},
      primaryClass={cs.CL},
      url={https://arxiv.org/abs/2406.18532}, 
}

@article{zhou2023agents,
      title={Agents: An Open-source Framework for Autonomous Language Agents}, 
      author={Wangchunshu Zhou and Yuchen Eleanor Jiang and Long Li and Jialong Wu and Tiannan Wang and Shi Qiu and Jintian Zhang and Jing Chen and Ruipu Wu and Shuai Wang and Shiding Zhu and Jiyu Chen and Wentao Zhang and Xiangru Tang and Ningyu Zhang and Huajun Chen and Peng Cui and Mrinmaya Sachan},
      year={2023},
      eprint={2309.07870},
      archivePrefix={arXiv},
      primaryClass={cs.CL},
      url={https://arxiv.org/abs/2309.07870}, 
}
```
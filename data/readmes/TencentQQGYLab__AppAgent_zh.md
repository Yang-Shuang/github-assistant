# [CHI 2025] AppAgent 

<div align="center">

<a href='https://arxiv.org/abs/2312.13771'><img src='https://img.shields.io/badge/arXiv-2312.13771-b31b1b.svg'></a> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
 <a href='https://appagent-official.github.io'><img src='https://img.shields.io/badge/Project-Page-Green'></a> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
 <a href='https://github.com/buaacyw/GaussianEditor/blob/master/LICENSE.txt'><img src='https://img.shields.io/badge/License-MIT-blue'></a> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
 <a href="https://twitter.com/dr_chizhang"><img src="https://img.shields.io/twitter/follow/dr_chizhang?style=social" alt="Twitter Follow"></a> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
 <br><br>
 <!-- [![Model](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Model-blue)](https://huggingface.co/listen2you002/ChartLlama-13b) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 
[![Dataset](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Dataset-blue)](https://huggingface.co/datasets/listen2you002/ChartLlama-Dataset) -->

[**Chi Zhang***†](https://icoz69.github.io/), [**Zhao Yang***](https://github.com/yz93), [**Jiaxuan Liu***](https://www.linkedin.com/in/jiaxuan-liu-9051b7105/), [Yucheng Han](http://tingxueronghua.github.io), [Xin Chen](https://chenxin.tech/), [Zebiao Huang](),
<br>
[Bin Fu](https://openreview.net/profile?id=~BIN_FU2), [Gang Yu✦](https://www.skicyyu.org/)
<br>
(* equal contribution, † Project Leader, ✦ Corresponding Author )
</div>


![](./assets/teaser.png)

ℹ️ 🔥🔥🔥 [AppAgentX](https://appagentx.github.io/) 已发布，这是一款具备演化机制的下一代图形用户界面（GUI）智能体。

ℹ️ 在使用本项目时如遇任何问题⚠️，欢迎在 [GitHub Issues](https://github.com/mnotgod96/AppAgent/issues) 上提交反馈，或通过邮件联系 [Dr. Chi Zhang](https://icoz69.github.io/) (dr.zhang.chi@outlook.com)。

ℹ️ 本项目将在官方 [TencentQQGYLab](https://github.com/TencentQQGYLab/AppAgent) GitHub 页面上同步更新。

## 📝 更新日志

- __[2025.3.5]__: 🔥🔥🔥发布 [AppAgentX](https://appagentx.github.io/)，这是一款具备演化机制的下一代图形用户界面（GUI）智能体。
- __[2024.2.8]__: 新增 `qwen-vl-max`（通义千问-VL）作为可选的多模态模型。该模型目前可免费使用，但性能相较于 GPT-4V 稍弱。
- __[2024.1.31]__: 发布我们在测试 AppAgent 时使用的 [评估基准（benchmark）](https://github.com/mnotgod96/AppAgent/blob/main/assets/testset.md)
- __[2024.1.2]__: 新增一种可选方法，允许智能体在屏幕上显示网格覆盖层，以支持**点击/滑动屏幕任意位置**。
- __[2023.12.26]__: 新增 [使用技巧（Tips）](#tips) 章节以优化使用体验；为没有实体安卓设备的用户补充了使用 **Android Studio 模拟器** 的操作指南。
- __[2023.12.21]__: 开源 Git 仓库，包含实现我们 AppAgent 的详细配置步骤！


## 🔆 简介

我们提出了一种新颖的基于大语言模型（LLM）的多模态智能体框架，旨在操控智能手机应用程序。 

该框架使智能体能够通过简化的动作空间操控手机应用，模拟人类点击、滑动等交互行为。这种新颖的方法无需访问系统底层接口，从而拓宽了其在各类应用中的适用性。

智能体功能的核心在于其创新的计算方法。它可以通过自主探索或观察人类演示来学习如何导航和使用新应用。该过程会生成一个文档说明库（documentation base），供智能体在执行跨应用的复杂任务时参考调用。


## ✨ 演示

演示视频展示了在部署阶段使用 AppAgent 关注 X（Twitter）上某位用户的过程。

https://github.com/mnotgod96/AppAgent/assets/40715314/db99d650-dec1-4531-b4b2-e085bfcadfb7

一项有趣的实验，展示 AppAgent 通过人机验证（CAPTCHA）的能力。

https://github.com/mnotgod96/AppAgent/assets/27103154/5cc7ba50-dbab-42a0-a411-a9a862482548

使用网格覆盖层定位未标注数字标签的 UI 元素的示例。

https://github.com/mnotgod96/AppAgent/assets/27103154/71603333-274c-46ed-8381-2f9a34cdfc53

## 🚀 快速开始

本节将指导你如何快速使用 `gpt-4-vision-preview`（或 `qwen-vl-max`）作为智能体，在安卓应用上为你完成特定任务。

### ⚙️ 步骤 1：前置条件

1. 在你的电脑上下载并安装 [Android Debug Bridge](https://developer.android.com/tools/adb)（adb），这是一个命令行工具，允许你从电脑与安卓设备进行通信。

2. 准备一台安卓设备，并在设置中的开发者选项里开启 USB 调试功能。

3. 使用 USB 数据线将你的设备连接到电脑。

4. （可选）如果你没有安卓设备但仍想尝试 AppAgent，建议你下载 [Android Studio](https://developer.android.com/studio/run/emulator) 并使用其自带的模拟器。你可以在 Android Studio 的设备管理器中找到该模拟器。可以通过从网上下载 APK 文件并拖拽到模拟器中来安装应用。AppAgent 能够检测模拟设备并在其上操控应用，效果与操作真机无异。

   <img width="570" alt="Screenshot 2023-12-26 at 22 25 42" src="https://github.com/mnotgod96/AppAgent/assets/27103154/5d76b810-1f42-44c8-b024-d63ec7776789">

5. 克隆本仓库并安装依赖项。本项目所有脚本均使用 Python 3 编写，请确保已安装该环境。

```bash
cd AppAgent
pip install -r requirements.txt
```

### 🤖 步骤 2：配置智能体

AppAgent 需要由能够接收文本和视觉输入的多模态模型驱动。在我们的实验中，我们使用 `gpt-4-vision-preview` 作为决策模型，以决定如何在智能手机上执行操作来完成既定任务。

要配置对 GPT-4V 的请求，你需要修改根目录下的 `config.yaml` 文件。尝试运行 AppAgent 必须配置以下两个关键参数：
1. **OpenAI API 密钥**：你必须从 OpenAI 购买有效的 API 密钥以访问 GPT-4V。
2. **请求间隔**：这是连续两次向 GPT-4V 发送请求之间的时间间隔（秒），用于控制请求频率。请根据你的账户状态调整此值。

`config.yaml` 中的其他参数均附有详细注释，可根据需要自行修改。

> ⚠️ 请注意，GPT-4V 并非免费服务。本项目涉及的每次请求/响应交互成本约为 $0.03，请合理使用。

你也可以尝试使用 `qwen-vl-max`（通义千问-VL）作为替代的多模态模型来驱动 AppAgent。该模型目前可免费使用，但在 AppAgent 场景下的性能相较于 GPT-4V 稍弱。

若要使用它，你需要注册阿里云账号并[创建 Dashscope API 密钥](https://help.aliyun.com/zh/dashscope/developer-reference/activate-dashscope-and-create-an-api-key?spm=a2c4g.11186623.0.i1)，将其填入 `config.yaml` 文件中的 `DASHSCOPE_API_KEY` 字段。同时，将 `MODEL` 字段的值从 `OpenAI` 改为 `Qwen`。

如果你想使用自己的模型测试 AppAgent，请在 `scripts/model.py` 中相应地编写新的模型类。

### 🔍 步骤 3：探索阶段

我们的论文提出了一种新颖的解决方案，包含“探索”和“部署”两个阶段，旨在将 GPT-4V 转化为能够辅助用户操作安卓手机的智能体。探索阶段始于你给出的任务指令，你可以选择让智能体自主探索应用，或从你的演示中学习。无论哪种方式，智能体都会为交互过程中涉及的元素生成文档说明，并保存以供部署阶段使用。

#### 选项 1：自主探索 (`autonomous exploration`)

该方案采用完全自主的探索模式，允许智能体在不干预的情况下尝试完成给定任务，从而探索应用的使用方法。

开始运行前，请在根目录执行 `python learn.py`。按照提示选择 `autonomous exploration`（自主探索）作为操作模式，并提供应用名称和任务描述即可。随后智能体会自动完成任务。在此模式下，AppAgent 会反思其先前动作以确保符合给定任务要求，并为探索过的元素生成文档说明。

```bash
python learn.py
```

#### 选项 2：从人类演示中学习 (`human demonstration`)

该方案要求用户首先演示一个类似的任务。AppAgent 将从演示中学习，并为演示过程中看到的 UI 元素生成文档说明。

开始人类演示前，请在根目录执行 `python learn.py`。按照提示选择 `human demonstration`（人类演示）作为操作模式，并提供应用名称和任务描述。系统将截取手机屏幕截图，并对屏幕上显示的所有交互元素进行数字标签标注。你需要根据提示确定下一步动作及其目标对象。当你认为演示完成时，输入 `stop` 结束演示。

```bash
python learn.py
```

![](./assets/demo.png)

### 📱 步骤 4：部署阶段

探索阶段结束后，你可以在根目录运行 `run.py`。按照提示输入应用名称，选择智能体应使用的文档说明库（documentation base），并提供任务描述即可。随后智能体会自动执行任务。该模块会自动检测是否已为该应用生成过文档库；若未找到相关文档，你也可以选择不加载任何文档直接运行智能体（成功率不保证）。

```bash
python run.py
```

## 💡 使用技巧 <a name="tips"></a>
- 为获得更好的体验，你可以通过自主探索让 AppAgent 执行更广泛的任务，或直接演示更多应用功能以完善应用文档。通常，提供给智能体的文档越详尽，任务成功完成的可能性就越高。
- 建议定期检查智能体生成的文档说明。如果发现某些文档未能准确描述元素功能，你也可以手动进行修订。


## 📊 评估测试
请参阅 [评估基准（benchmark）](https://github.com/mnotgod96/AppAgent/blob/main/assets/testset.md)。


## 📖 待办事项
- [ ] 集成更多大语言模型（LLM）API。
- [x] 开源评估基准（Benchmark）。
- [x] 开源配置文件。

## 😉 引用格式
```bib
@misc{yang2023appagent,
      title={AppAgent: Multimodal Agents as Smartphone Users}, 
      author={Chi Zhang and Zhao Yang and Jiaxuan Liu and Yucheng Han and Xin Chen and Zebiao Huang and Bin Fu and Gang Yu},
      year={2023},
      eprint={2312.13771},
      archivePrefix={arXiv},
      primaryClass={cs.CV}
}
```

## ⭐ Star 历史

[![Star History Chart](https://api.star-history.com/svg?repos=mnotgod96/AppAgent&type=Date)](https://star-history.com/#mnotgod96/AppAgent&Date)


## 📜 许可证
遵循 [MIT 许可证](./assets/license.txt)。
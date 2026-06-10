![](https://s3.ca-central-1.amazonaws.com/serpent-ai-assets/SerpentFBCover.png)

# Serpent.AI - 游戏智能体（Game Agent）框架（Python）

[![](https://img.shields.io/badge/project-website-brightgreen.svg?colorB=1bcc6f&longCache=true)](http://serpent.ai)
[![](https://img.shields.io/badge/project-blog-brightgreen.svg?colorB=1bcc6f&longCache=true)](http://blog.serpent.ai)
[![](https://img.shields.io/badge/project-wiki-brightgreen.svg?colorB=1bcc6f&longCache=true)](https://github.com/SerpentAI/SerpentAI/wiki)    
[![](https://img.shields.io/badge/pypi-v2018.1.2-brightgreen.svg?colorB=007ec6&longCache=true)]()
[![](https://img.shields.io/badge/python-3.6-brightgreen.svg?colorB=007ec6&longCache=true)]()
[![](https://img.shields.io/badge/license-MIT-brightgreen.svg?colorB=007ec6&longCache=true)]()  
[![](https://img.shields.io/badge/twitter-@Serpent__AI-brightgreen.svg?colorB=1da1f2&longCache=true)](https://twitter.com/Serpent_AI)

## 更新：复活（2020年5月）

框架的开发工作已重新启动，目标是将项目更新至 2020 年标准：支持 Python 3.8+、减少依赖项、提升易用性（提供安装程序与图形界面 GUI）等！依然保持开源及宽松许可证，并正在探索面向非技术用户的 Steam 发行版。🐍

## ~~警告：生命周期结束（2018年11月）~~

Serpent.AI 是一个简单却强大、新颖的框架，旨在协助开发者创建游戏智能体（Game Agent）。只需使用熟悉的 Python 代码，即可将你拥有的任意电子游戏转化为适合实验的沙盒环境。该框架的 _raison d'être（根本宗旨）_ 是为机器学习与人工智能研究提供有价值的工具。此外，作为业余爱好来使用也极其有趣（而且非常上瘾；特此提醒）！

该框架包含大量辅助模块，为使用电子游戏作为环境时常见的场景提供解决方案，并附带命令行工具（CLI）以加速开发。它提供一些有用的约定，但绝对不对你的智能体内部实现做强制限制：想使用最新、最前沿的深度强化学习算法？允许。想用计算机视觉技术、图像处理或三角学？允许。想随机按下左键或右键？_叹气_ 允许。最重要的是，Serpent.AI 采用完全基于插件的设计（涵盖游戏支持与智能体本身），因此你的实验成果实际上具备可移植性，可以分发给同行乃至互联网上的陌生人。

Serpent.AI 支持 Linux、Windows ~~及 macOS~~。

_该框架的下一个版本将正式停止支持 macOS。苹果产品对 Nvidia 显卡的排斥意味着，近期的任何 Mac 电脑都无法运行 CUDA——这是 Serpent.AI 实时训练不可或缺的技术。此外，Catalina 阻止 32 位应用运行以及弃用 OpenGL 等决策，也使得继续支持该系统变得缺乏合理性。_ 

![](https://s3.ca-central-1.amazonaws.com/serpent-ai-assets/demo_isaac.gif)

_实验：游戏智能体学习击败怪物“蒙斯特”（以撒的结合：重生+）_

## 背景

该项目源于对 [OpenAI Universe](https://github.com/openai/universe) 的赞赏与因使用挫折而产生的反思。坦白说，它的理念非常完美，但部分实现细节仍有待改进。基于此，确立了该框架的核心原则：

1. 必须原生运行。不得使用 Docker 容器或 VNC 服务器。
2. 允许用户使用自己的游戏。不得等待授权协议或特殊的游戏 API。
3. 鼓励多样化与创造性的方法。不得仅支持“月度流行”的 AI 方案。

_想了解 Serpent.AI 是如何诞生的吗？请阅读博客上的文章《Serpent.AI 背后的故事》！_

## 文档

指南、教程和视频正在制作中并更新至 [GitHub Wiki](https://github.com/SerpentAI/SerpentAI/wiki)。目前它是官方唯一的文档来源。

![](https://s3.ca-central-1.amazonaws.com/serpent-ai-assets/demo_ymbab.gif)

_实验：游戏智能体学习匹配方块（你必须造一艘船）_

_商务联系：info@serpent.ai_
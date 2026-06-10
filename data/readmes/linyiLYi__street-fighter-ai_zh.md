# SFighterAI

[简体中文](README_CN.md) | English | [Español](README_ES.md)

本项目是一个使用深度强化学习（deep reinforcement learning）训练的 AI 智能体，用于击败游戏《街头霸王 II：特别冠军版》的最终 Boss。该智能体仅根据游戏屏幕的 RGB 像素值做出决策。在提供的存档状态下，智能体在最终关卡的第一回合取得了 100% 的胜利胜率（此处发生了过拟合现象，详见 [运行测试](#running-tests) 部分）。

### 文件结构

```bash
├───data
├───main
│   ├───logs
│   ├───trained_models
│   └───scripts
├───utils
│   └───scripts
```

游戏配置文件存放在 `data/` 文件夹中，项目主代码位于 `main/` 文件夹内。在 `main/` 目录下，`logs/` 文件夹包含终端输出和记录训练过程的数据曲线（可使用 Tensorboard 查看），而 `trained_models/` 文件夹则存放了不同阶段的模型权重。这些权重可用于运行 `test.py` 中的测试，以观察 AI 智能体在不同训练阶段所学策略的表现。

## 运行指南

本项目基于 Python 编程语言，主要使用 [OpenAI Gym Retro](https://retro.readthedocs.io/en/latest/getting_started.html) 和 [Stable-Baselines3](https://stable-baselines3.readthedocs.io/en/master/) 等标准库。项目使用的 Python 版本为 3.8.10，建议使用 [Anaconda](https://www.anaconda.com) 配置 Python 环境。以下搭建流程已在 Windows 11 系统上测试通过。下方均为控制台/终端命令。

### 环境配置

```bash
# Create a conda environment named StreetFighterAI with Python version 3.8.10
conda create -n StreetFighterAI python=3.8.10
conda activate StreetFighterAI

# Install Python libraries
cd [parent_directory_of_project]/street-fighter-ai/main
pip install -r requirements.txt

# Run script to locate gym-retro game folder
cd ..
python .\utils\print_game_lib_folder.py
```

控制台输出文件夹路径后，请将其复制到文件资源管理器并导航至该路径。此文件夹包含 gym-retro 中《街头霸王 II：特别冠军版》的游戏数据文件，包括游戏 ROM 文件和配置文件。请将本项目 `data/` 文件夹中的 `Champion.Level12.RyuVsBison.state`、`data.json`、`metadata.json` 和 `scenario.json` 复制到该游戏数据文件夹中，替换原有文件（可能需要管理员权限）。`.state` 文件为游戏最高难度的存档状态，三个 `.json` 文件是 gym-retro 的配置文件，用于存储游戏信息的内存地址（本项目仅使用 `[agent_hp]` 和 `[enemy_hp]` 来实时读取角色血量值）。

运行程序还需要《街头霸王 II：特别冠军版》的游戏 ROM 文件，该文件不由 gym-retro 提供，需通过其他合法途径获取。你可以参考此[链接](https://wowroms.com/en/roms/sega-genesis-megadrive/street-fighter-ii-special-champion-edition-europe/26496.html)。

合法获取游戏 ROM 文件后，将其复制到上述 gym-retro 游戏数据文件夹中，并重命名为 `rom.md`。至此环境配置完成。

注意 1：如果你想手动抓取游戏存档状态并查找内存变量，可以使用 gym-retro 的集成 UI。将 `data/Gym Retro Integration.exe` 复制到上述 gym-retro 游戏数据文件夹的上两级目录（即 `retro/` 文件夹）中。

注意 2：如果你想录制 AI 智能体的游戏视频，需要安装 [ffmpeg](https://ffmpeg.org/)。

```bash
conda install ffmpeg
```

### <a name="running-tests"></a>运行测试

环境配置完成后，你可以在 `main/` 文件夹中运行 `test.py` 来测试并体验 AI 智能体在不同训练阶段的性能。

```bash
cd [parent_directory_of_project]/street-fighter-ai/main
python test.py
```

模型权重文件存放在 `main/trained_models/` 文件夹中。`test.py` 默认使用的模型为 `ppo_ryu_2500000_steps_updated.zip`，该模型泛化能力较好，能够击败《街头霸王 II：特别冠军版》的最终关卡。若想查看其他模型的表现，可将 `test.py` 中的 `model_path` 变量修改为对应模型文件的路径。各训练阶段模型的实测表现如下：

* ppo_ryu_2000000_steps_updated: 刚开始进入过拟合状态，具备一定泛化能力但尚不足以稳定取胜。
* ppo_ryu_2500000_steps_updated: 接近最终过拟合状态，无法完全压制第一回合但具备部分泛化能力。击败最终关卡的概率较高。
* ppo_ryu_3000000_steps_updated: 接近最终过拟合状态，几乎能压制第一回合但泛化能力极弱。
* ppo_ryu_7000000_steps_updated: 已完全过拟合，可压制第一回合但缺乏泛化能力。 

### 训练模型

若想训练自己的模型，可在 `main/` 文件夹中运行 `train.py`。

```bash
cd [parent_directory_of_project]/street-fighter-ai/main
python train.py
```

### 查看训练曲线

项目内置了 Tensorboard 训练过程图表。你可以使用 Tensorboard 查看详细数据。推荐使用 VSCode 集成的 Tensorboard 插件直接查看数据，传统查看方法如下：

```bash
cd [parent_directory_of_project]/street-fighter-ai/main
tensorboard --logdir=logs/
```

在浏览器中打开默认的 Tensorboard 服务地址 `http://localhost:6006/`，即可查看训练过程的交互式图表。

## 致谢
本项目使用了 [OpenAI Gym Retro](https://retro.readthedocs.io/en/latest/getting_started.html)、[Stable-Baselines3](https://stable-baselines3.readthedocs.io/en/master/) 等开源库。感谢所有开发者对开源社区的贡献！

以下两篇论文对本项目产生了重要影响：

[1] [DIAMBRA Arena A New Reinforcement Learning Platform for Research and Experimentation](https://arxiv.org/abs/2210.10595)
该论文总结了格斗游戏中深度强化学习模型超参数（hyperparameters）设置的宝贵经验，对本项目的训练过程提供了极大帮助。

[2] [Mitigating Cowardice for Reinforcement Learning](https://ieee-cog.org/2022/assets/papers/paper_111.pdf)
该论文提出的“惩罚衰减”（penalty decay）机制有效解决了 AI 的“怯战”问题（即总是躲避对手，甚至不敢尝试攻击指令）。
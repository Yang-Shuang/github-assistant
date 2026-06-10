<p align="center">

  <img src="docs/source/_static/logo.jpg" width="200" alt="TensorTrade Logo">

</p>



# TensorTrade



**训练强化学习（RL）代理进行交易。它们能跑赢“买入并持有”策略吗？**



[![Tests](https://github.com/tensortrade-org/tensortrade/actions/workflows/tests.yml/badge.svg)](https://github.com/tensortrade-org/tensortrade/actions/workflows/tests.yml)

[![Documentation Status](https://readthedocs.org/projects/tensortrade/badge/?version=latest)](https://tensortrade.org)

[![Apache License](https://img.shields.io/github/license/tensortrade-org/tensortrade.svg?color=brightgreen)](http://www.apache.org/licenses/LICENSE-2.0)

[![Discord](https://img.shields.io/discord/592446624882491402.svg?color=brightgreen)](https://discord.gg/ZZ7BGWh)

[![Python 3.12+](https://img.shields.io/badge/python-3.12+-blue.svg)](https://www.python.org/downloads/release/python-3120/)



TensorTrade 是一个开源的 Python 框架，用于构建、训练和评估用于算法交易的强化学习（Reinforcement Learning）代理。该框架提供了可组合的环境、动作方案、奖励函数和数据流组件，可以灵活搭配以创建自定义交易系统。



## 快速开始



```bash

# Requires Python 3.12+

python3.12 -m venv tensortrade-env && source tensortrade-env/bin/activate

pip install -e .



# For training with Ray/RLlib (recommended)

pip install -r examples/requirements.txt



# Run training

python examples/training/train_simple.py

```



## 文档与教程



📚 **[教程索引](docs/tutorials/index.md)** — 完整学习路线的起点。



### 基础概念

- [三大支柱](docs/tutorials/01-foundations/01-three-pillars.md) — 强化学习、交易与数据核心概念

- [架构设计](docs/tutorials/01-foundations/02-architecture.md) — 组件协同工作原理

- [首次运行](docs/tutorials/01-foundations/03-your-first-run.md) — 运行代码并理解输出结果



### 领域知识

- [面向强化学习实践者的交易基础](docs/tutorials/02-domains/track-a-trading-for-rl/01-trading-basics.md)

- [面向交易员的强化学习入门](docs/tutorials/02-domains/track-b-rl-for-traders/01-rl-fundamentals.md)

- [常见失败案例](docs/tutorials/02-domains/track-b-rl-for-traders/02-common-failures.md) — 必须避免的关键陷阱

- [综合导论](docs/tutorials/02-domains/track-c-full-intro/README.md) — 双领域零基础入门



### 核心组件

- [动作方案](docs/tutorials/03-components/01-action-schemes.md) — BSH（买入/卖出/持有）与订单执行

- [奖励方案](docs/tutorials/03-components/02-reward-schemes.md) — PBR（基于头寸的回报）为何有效

- [观测器与数据流](docs/tutorials/03-components/03-observers-feeds.md) — 特征工程



### 训练指南

- [首次训练](docs/tutorials/04-training/01-first-training.md) — 使用 Ray RLlib 进行训练

- [Ray RLlib 深度解析](docs/tutorials/04-training/02-ray-rllib.md) — 配置选项详解

- [Optuna 优化](docs/tutorials/04-training/03-optuna.md) — 超参数调优



### 进阶主题

- [过拟合](docs/tutorials/05-advanced/01-overfitting.md) — 检测与防范策略

- [佣金分析](docs/tutorials/05-advanced/02-commission.md) — 核心研究发现

- [前向滚动验证](docs/tutorials/05-advanced/03-walk-forward.md) — 正确的评估方法



### 其他资源

- [实验日志](docs/EXPERIMENTS.md) — 完整研究文档

- [环境配置](docs/ENVIRONMENT_SETUP.md) — 详细安装指南

- [API 参考手册](https://www.tensortrade.org/en/latest/)



---



## 研究发现



我们对 PPO 代理在 BTC/USD 上的训练进行了大量实验。关键结果如下：



| Configuration | Test P&L | vs Buy-and-Hold |

|---------------|----------|-----------------|

| Agent (0% commission) | +$239 | +$594 |

| Agent (0.1% commission) | -$650 | -$295 |

| Buy-and-Hold | -$355 | — |



在零佣金条件下，代理展现了方向性预测能力。当前的主要挑战在于交易频率——佣金成本目前超过了预测带来的利润。有关方法论和详细分析，请参阅 [实验日志](docs/EXPERIMENTS.md)。



---



## 架构设计



```

┌─────────────────────────────────────────────────────────────────┐

│                        TradingEnv                               │

│                                                                 │

│   Observer ──────> Agent ──────> ActionScheme ──────> Portfolio │

│   (features)      (policy)      (BSH/Orders)        (wallets)  │

│       ^                                                  │      │

│       └──────────── RewardScheme <───────────────────────┘      │

│                        (PBR)                                    │

│                                                                 │

│   DataFeed ──────> Exchange ──────> Broker ──────> Trades       │

└─────────────────────────────────────────────────────────────────┘

```



| Component | Purpose | Default |

|-----------|---------|---------|

| ActionScheme | Converts agent output to orders | BSH (Buy/Sell/Hold) |

| RewardScheme | Computes learning signal | PBR (Position-Based Returns) |

| Observer | Generates observations | Windowed features |

| Portfolio | Manages wallets and positions | USD + BTC |

| Exchange | Simulates execution | Configurable commission |



---



## 训练脚本



| Script | Description |

|--------|-------------|

| `examples/training/train_simple.py` | Basic demo with wallet tracking |

| `examples/training/train_ray_long.py` | Distributed training with Ray RLlib |

| `examples/training/train_optuna.py` | Hyperparameter optimization |

| `examples/training/train_best.py` | Best configuration from experiments |



---



## 安装指南



**环境要求：** Python 3.11 或 3.12



```bash

# Create environment

python3.12 -m venv tensortrade-env

source tensortrade-env/bin/activate  # Windows: tensortrade-env\Scripts\activate



# Install

pip install --upgrade pip

pip install -r requirements.txt

pip install -e .



# Verify

pytest tests/tensortrade/unit -v



# Training dependencies (optional)

pip install -r examples/requirements.txt

```



有关特定平台的安装说明和故障排除，请参阅 [环境配置指南](docs/ENVIRONMENT_SETUP.md)。



### Docker 部署



```bash

make run-notebook  # Jupyter

make run-docs      # Documentation

make run-tests     # Test suite

```



---



## 项目结构



```

tensortrade/

├── tensortrade/           # Core library

│   ├── env/              # Trading environments

│   ├── feed/             # Data pipeline

│   ├── oms/              # Order management

│   └── data/             # Data fetching

├── examples/

│   ├── training/         # Training scripts

│   └── notebooks/        # Jupyter tutorials

├── docs/

│   ├── tutorials/        # Learning curriculum

│   └── EXPERIMENTS.md    # Research log

└── tests/

```



---



## 常见问题与解决



| Issue | Solution |

|-------|----------|

| "No stream satisfies selector" | Update to v1.0.4-dev1+ |

| Ray installation fails | Run `pip install --upgrade pip` first |

| NumPy version conflict | `pip install "numpy>=1.26.4,<2.0"` |

| TensorFlow CUDA issues | `pip install tensorflow[and-cuda]>=2.15.1` |



---



## 贡献指南



请参阅 [贡献指南](CONTRIBUTING.md)。



优先改进方向：

1. 降低交易频率（头寸规模控制、持仓周期管理）

2. 考虑佣金的奖励方案

3. 替代动作空间设计



---



## 社区交流



- [Discord](https://discord.gg/ZZ7BGWh)

- [GitHub Issues](https://github.com/notadamking/tensortrade/issues)

- [Documentation](https://www.tensortrade.org/)



---



## 开源协议



[Apache 2.0](LICENSE)
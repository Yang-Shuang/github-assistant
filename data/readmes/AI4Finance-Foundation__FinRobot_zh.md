# FinRobot：基于大语言模型的金融分析开源 AI Agent 平台
[![Downloads](https://static.pepy.tech/badge/finrobot)]([https://pepy.tech/project/finrobot](https://pepy.tech/project/finrobot))
[![Downloads](https://static.pepy.tech/badge/finrobot/week)](https://pepy.tech/project/finrobot)
[![Join Discord](https://img.shields.io/badge/Discord-Join-blue)](https://discord.gg/trsr8SXpW5)
[![Python 3.8](https://img.shields.io/badge/python-3.6-blue.svg)](https://www.python.org/downloads/release/python-360/)
[![PyPI](https://img.shields.io/pypi/v/finrobot.svg)](https://pypi.org/project/finrobot/)
![License](https://img.shields.io/github/license/AI4Finance-Foundation/finrobot.svg?color=brightgreen)
![](https://img.shields.io/github/issues-raw/AI4Finance-Foundation/finrobot?label=Issues)
![](https://img.shields.io/github/issues-closed-raw/AI4Finance-Foundation/finrobot?label=Closed+Issues)
![](https://img.shields.io/github/issues-pr-raw/AI4Finance-Foundation/finrobot?label=Open+PRs)
![](https://img.shields.io/github/issues-pr-closed-raw/AI4Finance-Foundation/finrobot?label=Closed+PRs)


<div align="center">
<img align="center" src=figs/logo_white_background.jpg width="40%"/>
</div>

**FinRobot** 是一款专为金融应用打造的 AI Agent（智能体）平台，超越了 FinGPT 的单模型方法。它整合了多种人工智能技术——包括大语言模型（LLMs）、强化学习和量化分析——以驱动投资研究自动化、算法交易策略和风险评估，为金融行业提供全栈式智能解决方案。

**AI Agent（智能体）概念**：AI Agent 是一种以大型语言模型为“大脑”的智能实体，能够感知环境、做出决策并执行操作。与传统人工智能不同，AI Agent 具备独立思考的能力，并能利用工具逐步实现既定目标。

[FinRobot 白皮书](https://arxiv.org/abs/2405.14767)

![Visitors](https://api.visitorbadge.io/api/VisitorHit?user=AI4Finance-Foundation&repo=FinRobot&countColor=%23B17A)
[![Discord](https://dcbadge.limes.pink/api/server/trsr8SXpW5?v=20260320)](https://discord.gg/trsr8SXpW5)

## 🎬 FinRobot Pro —— 你的个人 AI 驱动股票研究助手
🌐 https://finrobot.ai/

<div align="center">
  <a href="https://www.youtube.com/watch?v=ebgPiJINi-k" target="_blank">
    <img src="https://github.com/user-attachments/assets/de3b9f9c-50aa-49f0-82c6-3d2b938f4670" width="90%" />
  </a>
</div>

<p align="center">
  ▶️ 点击上方图片观看演示视频，或查看下方简短预览。
</p>

一款本地部署的 AI 助手，可获取财务数据、运行多智能体大语言模型分析，并生成专业的股票研究报告。

**1. 配置 API 密钥**
```bash
cp finrobot_equity/core/config/config.ini.example finrobot_equity/core/config/config.ini
```
使用你的密钥编辑 `config.ini`：
```ini
[API_KEYS]
fmp_api_key = YOUR_FMP_API_KEY          # https://financialmodelingprep.com/developer
openai_api_key = YOUR_OPENAI_API_KEY    # https://platform.openai.com/account/api-keys
adanos_api_key = YOUR_ADANOS_API_KEY    # Optional: enables Retail Sentiment Insights
```

**2. 一键部署（Web 界面）**
```bash
chmod +x deploy.sh
./deploy.sh start

#if deploy.sh not working then
python3 -m venv venv                                                                                                                                           
source venv/bin/activate
pip install -r requirements-equity.txt                                                                                                                         
python run_web_app.py  
```
访问地址：`http://127.0.0.1:8001`

| 命令 | 描述 |
|:---|:---|
| `./deploy.sh start` | 启动 Web 应用（自动安装依赖） |
| `./deploy.sh stop` | 停止应用程序 |
| `./deploy.sh restart` | 重启应用程序 |
| `./deploy.sh status` | 检查运行状态 |

**3. 或通过命令行运行**
```bash
# Step 1: Financial analysis
python finrobot_equity/core/src/generate_financial_analysis.py \
    --company-ticker NVDA \
    --company-name "NVIDIA Corporation" \
    --config-file finrobot_equity/core/config/config.ini \
    --peer-tickers AMD INTC \
    --generate-text-sections

# Step 2: Generate report
python finrobot_equity/core/src/create_equity_report.py \
    --company-ticker NVDA \
    --company-name "NVIDIA Corporation" \
    --analysis-csv output/NVDA/analysis/financial_metrics_and_forecasts.csv \
    --ratios-csv output/NVDA/analysis/ratios_raw_data.csv \
    --config-file finrobot_equity/core/config/config.ini
```

**处理流程**：
1. **获取财务数据**：通过 FMP API 获取利润表、资产负债表和现金流量表
2. **处理与预测**：生成三年财务预测、DCF（现金流折现）估值及同业对比
3. **AI Agent 分析**：8 个专用智能体生成投资论点、风险评估、估值概览等
4. **报告生成**：生成包含 15 种以上图表类型的专业多页 HTML/PDF 报告

### 示例报告
- [NVDA 股票研究报告](https://ai4finance-foundation.github.io/FinRobot/finrobot_equity/core/output/NVDA_Equity_Research_Report.html)
- [MSFT 股票研究报告](https://ai4finance-foundation.github.io/FinRobot/finrobot_equity/core/output/MSFT_Equity_Research_Report.html)
- [COP 股票研究报告](https://ai4finance-foundation.github.io/FinRobot/finrobot_equity/core/output/COP_Equity_Research_Report.html)
- [TSLA 股票研究报告](https://ai4finance-foundation.github.io/FinRobot/finrobot_equity/core/output/TSLA_Equity_Research_Report.html)
- [META 股票研究报告](https://ai4finance-foundation.github.io/FinRobot/finrobot_equity/core/output/META_Equity_Research_Report.html)

完整文档请参阅 [finrobot_equity/README.md](finrobot_equity/README.md)。


## FinRobot Pro 是什么？


https://github.com/user-attachments/assets/93ec0f1e-e28b-4474-a0bf-a79e0c12f0ff


[FinRobot Pro](https://finrobot.ai/ ) 是一款基于人工智能的股票研究平台，利用大语言模型（LLMs）和 AI Agent（智能体）实现专业股票分析的自动化。

**核心功能：**

- **报告自动生成** – 即时生成专业的股票研究报告
- **财务分析** – 深入剖析利润表、资产负债表和现金流量表
- **估值分析** – 市盈率（P/E）、企业价值倍数（EV/EBITDA）及同业对比
- **风险评估** – 全面的投资组合风险评估


## FinRobot 生态系统
<div align="center">
<img align="center" src="https://github.com/AI4Finance-Foundation/FinRobot/assets/31713746/6b30d9c1-35e5-4d36-a138-7e2769718f62" width="90%"/>
</div>

### FinRobot 的整体框架分为四个独立的层级，每层旨在解决金融 AI 处理与应用中的特定方面：
1. **金融 AI Agent（智能体）层**：该层现已引入金融思维链（Chain-of-Thought, CoT）提示技术，以增强复杂分析与决策能力。市场预测智能体、文档分析智能体和交易策略智能体利用 CoT 将金融挑战分解为逻辑步骤，使其先进算法与领域专业知识相契合，从而精准把握金融市场动态变化，提供可操作的洞察。
2. **金融大语言模型（LLMs）算法层**：配置并利用针对特定领域和全球市场分析专门微调的模型。 
3. **LLMOps 与 DataOps 层**：LLMOps 层实施多源集成策略，为特定的金融任务选择最合适的 LLMs，利用一系列最先进的模型。 
4. **多源大语言模型基础层**：该基础层支持各类通用和专用 LLMs 的即插即用功能。 


## FinRobot：智能体工作流
<div align="center">
<img align="center" src="https://github.com/AI4Finance-Foundation/FinRobot/assets/31713746/ff8033be-2326-424a-ac11-17e2c9c4983d" width="60%"/>
</div>

1. **感知（Perception）**：该模块从市场数据源、新闻和经济指标中捕获并解析多模态金融数据，采用复杂技术对数据进行结构化处理，以支持深度分析。

2. **大脑（Brain）**：作为核心处理单元，该模块利用大语言模型解析来自感知模块的数据，并运用金融思维链（CoT）流程生成结构化指令。

3. **执行（Action）**：该模块执行大脑模块的指令，调用工具将分析洞察转化为可操作的结果。操作包括交易、投资组合调整、生成报告或发送警报等，从而主动影响金融环境。

## FinRobot：智能调度器
<div align="center">
<img align="center" src="https://github.com/AI4Finance-Foundation/FinRobot/assets/31713746/06fa0b78-ac53-48d3-8a6e-98d15386327e" width="60%"/>
</div>

智能调度器是确保模型多样性以及优化各任务最适配大语言模型集成与选择的核心组件。
* **导演智能体（Director Agent）**：该组件负责协调任务分配流程，根据性能指标和任务匹配度将任务合理分配给各个智能体。
* **智能体注册（Agent Registration）**：管理系统中智能体的注册状态并跟踪其可用性，以促进高效的资源调度。
* **智能体适配器（Agent Adaptor）**：针对特定任务定制智能体功能，提升其在整体系统中的性能与集成度。
* **任务管理器（Task Manager）**：管理与存储针对不同金融任务定制的通用及微调大语言模型智能体，并定期更新以确保其相关性与有效性。

## 文件结构

主文件夹 **finrobot** 包含三个子文件夹：**agents、data_source、functional**。 

```
FinRobot
├── finrobot (main folder)
│   ├── agents
│   	├── agent_library.py
│   	└── workflow.py
│   ├── data_source
│   	├── finnhub_utils.py
│   	├── finnlp_utils.py
│   	├── fmp_utils.py
│   	├── sec_utils.py
│   	└── yfinance_utils.py
│   ├── functional
│   	├── analyzer.py
│   	├── charting.py
│   	├── coding.py
│   	├── quantitative.py
│   	├── reportlab.py
│   	└── text.py
│   ├── toolkits.py
│   └── utils.py
│
├── configs
├── experiments
├── tutorials_beginner (hands-on tutorial)
│   ├── agent_fingpt_forecaster.ipynb
│   └── agent_annual_report.ipynb 
├── tutorials_advanced (advanced tutorials for potential finrobot developers)
│   ├── agent_trade_strategist.ipynb
│   ├── agent_fingpt_forecaster.ipynb
│   ├── agent_annual_report.ipynb 
│   ├── lmm_agent_mplfinance.ipynb
│   └── lmm_agent_opt_smacross.ipynb
├── setup.py
├── OAI_CONFIG_LIST_sample
├── config_api_keys_sample
├── requirements.txt
└── README.md
```

## 安装指南：

**1. （推荐）创建新的虚拟环境**
```shell
conda create --name finrobot python=3.10
conda activate finrobot
```
**2. 使用终端下载 FinRobot 仓库或手动下载**
```shell
git clone https://github.com/AI4Finance-Foundation/FinRobot.git
cd FinRobot
```
**3. 从源码或 PyPI 安装 finrobot 及其依赖项**

通过 PyPI 获取最新版本：
```bash
pip install -U finrobot
```
或直接从此仓库安装：
```
pip install -e .
```
**4. 修改 `OAI_CONFIG_LIST_sample` 文件**
```shell
1) rename OAI_CONFIG_LIST_sample to OAI_CONFIG_LIST
2) remove the four lines of comment within the OAI_CONFIG_LIST file
3) add your own openai api-key <your OpenAI API key here>
```
**5. 修改 `config_api_keys_sample` 文件**
```shell
1) rename config_api_keys_sample to config_api_keys
2) remove the comment within the config_api_keys file
3) add your own finnhub-api "YOUR_FINNHUB_API_KEY"
4) add your own financialmodelingprep and sec-api keys "YOUR_FMP_API_KEY" and "YOUR_SEC_API_KEY" (for financial report generation)
```
**6. 开始浏览以下教程或演示：**
```
# find these notebooks in tutorials
1) agent_annual_report.ipynb
2) agent_fingpt_forecaster.ipynb
3) agent_trade_strategist.ipynb
4) lmm_agent_mplfinance.ipynb
5) lmm_agent_opt_smacross.ipynb
```

## 演示示例
### 1. 市场预测智能体（预测股票走势方向）
接收公司股票代码、近期基础财务数据和市场新闻作为输入，并预测其股价变动。

1. 导入依赖 
```python
import autogen
from finrobot.utils import get_current_date, register_keys_from_json
from finrobot.agents.workflow import SingleAssistant
```
2. 配置
```python
# Read OpenAI API keys from a JSON file
llm_config = {
    "config_list": autogen.config_list_from_json(
        "../OAI_CONFIG_LIST",
        filter_dict={"model": ["gpt-4-0125-preview"]},
    ),
    "timeout": 120,
    "temperature": 0,
}

# Register FINNHUB API keys
register_keys_from_json("../config_api_keys")
```
3. 运行
```python
company = "NVDA"

assitant = SingleAssistant(
    "Market_Analyst",
    llm_config,
    # set to "ALWAYS" if you want to chat instead of simply receiving the prediciton
    human_input_mode="NEVER",
)
assitant.chat(
    f"Use all the tools provided to retrieve information available for {company} upon {get_current_date()}. Analyze the positive developments and potential concerns of {company} "
    "with 2-4 most important factors respectively and keep them concise. Most factors should be inferred from company related news. "
    f"Then make a rough prediction (e.g. up/down by 2-3%) of the {company} stock price movement for next week. Provide a summary analysis to support your prediction."
)
```

### 2. 个人 AI 股票研究助手（股票研究报告）
### 3. 具备多模态能力的交易策略智能体


## AI Agent 相关论文

+ [斯坦福大学 & 微软研究院] [Agent AI：多模态交互的广阔前景综述](https://arxiv.org/abs/2401.03568)
+ [斯坦福大学] [生成式智能体：人类行为的交互式模拟](https://arxiv.org/abs/2304.03442)
+ [复旦大学自然语言处理实验室] [基于大语言模型的智能体崛起与潜力：综述](https://arxiv.org/abs/2309.07864)
+ [复旦大学自然语言处理实验室] [LLM 智能体论文列表](https://github.com/WooooDyy/LLM-Agent-Paper-List)
+ [清华大学] [大语言模型赋能的基于智能体的建模与仿真：综述与展望](https://arxiv.org/abs/2312.11970)
+ [中国人民大学] [基于大语言模型的自主智能体综述](https://pdf...链接保留)
+ [南洋理工大学] [FinAgent：面向金融交易的多模态基础智能体：工具增强、多样化与通用型](https://arxiv.org/abs/2402.18485)


## AI Agent 开源框架与工具
+ [AutoGPT (183k stars)](https://github.com/Significant-Gravitas/AutoGPT)：自主 AI 智能体平台。
+ [Dify (134k stars)](https://github.com/langgenius/dify)：支持工作流编排与 RAG 的 LLM 应用开发平台。
+ [LangChain (130k stars)](https://github.com/langchain-ai/langchain)：构建上下文感知 LLM 应用的框架。
+ [MetaGPT (65.6k stars)](https://github.com/geekan/MetaGPT)：基于角色协作的多智能体框架。
+ [AutoGen (56k stars)](https://github.com/microsoft/autogen)：支持工具调用与人类交互的多智能体 LLM 应用框架。
+ [CrewAI (46.6k stars)](https://github.com/joaomdmoura/crewAI)：编排协作式 AI 智能体的框架。
+ [ChatDev (31.7k stars)](https://github.com/OpenBMB/ChatDev)：面向软件开发任务的多智能体框架。
+ [FastGPT (27.4k stars)](https://github.com/labring/FastGPT)：支持工作流的基于知识的 LLM 平台。
+ [Langfuse (23.4k stars)](https://github.com/langfuse/langfuse)：开源的 LLM 可观测性与评估平台。
+ [BabyAGI (22.2k stars)](https://github.com/yoheinakajima/babyagi)：任务驱动的实验性自主智能体框架。
+ [SuperAGI (17.3k stars)](https://github.com/TransformerOptimus/SuperAGI)：面向开发者的自主智能体框架。
+ [CAMEL (16.4k stars)](https://github.com/camel-ai/camel)：协作与通信型 AI 智能体框架。
+ [Bisheng (11.2k stars)](https://github.com/dataelement/bisheng)：企业级开源 LLM 应用平台。

## 引用 FinRobot
```
@article{yang2024finrobot,
  title={FinRobot: An Open-Source AI Agent Platform for Financial Applications using Large Language Models},
  author={Yang, Hongyang and Zhang, Boyu and Wang, Neng and Guo, Cheng and Zhang, Xiaoli and Lin, Likun and Wang, Junlin and Zhou, Tianyu and Guan, Mao and Zhang, Runjia and others},
  journal={arXiv preprint arXiv:2405.14767},
  year={2024}
}

@inproceedings{
zhou2024finrobot,
title={FinRobot: {AI} Agent for Equity Research and Valuation with Large Language Models},
author={Tianyu Zhou and Pinqiao Wang and Yilin Wu and Hongyang Yang},
booktitle={ICAIF 2024: The 1st Workshop on Large Language Models and Generative AI for Finance},
year={2024}
}


@inproceedings{han2024enhancing,
  title={Enhancing Investment Analysis: Optimizing AI-Agent Collaboration in Financial Research},
  author={Han, Xuewen and Wang, Neng and Che, Shangkun and Yang, Hongyang and Zhang, Kunpeng and Xu, Sean Xin},
  booktitle={ICAIF 2024: Proceedings of the 5th ACM International Conference on AI in Finance},
  pages={538--546},
  year={2024}
}
```
**免责声明**：此处提供的代码和文档均在 Apache-2.0 许可证下发布。它们不应被视为财务建议或实盘交易推荐。在进行任何交易或投资操作前，务必保持谨慎并咨询合格的金融专业人士。


<div align="center">
<img align="center" width="30%" alt="image" src="https://github.com/AI4Finance-Foundation/FinGPT/assets/31713746/e0371951-1ce1-488e-aa25-0992dafcc139">
</div>
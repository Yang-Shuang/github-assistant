# AIOS：AI 智能体操作系统

<a href='https://arxiv.org/abs/2403.16971'><img src='https://img.shields.io/badge/Paper-PDF-red'></a>
<a href='https://arxiv.org/abs/2312.03815'><img src='https://img.shields.io/badge/Paper-PDF-blue'></a>
<a href='https://docs.aios.foundation/'><img src='https://img.shields.io/badge/Documentation-AIOS-green'></a>
<a href='https://discord.gg/B2HFxEgTJX'><img src='https://img.shields.io/badge/Community-Discord-8A2BE2'></a>
[![Gurubase](https://img.shields.io/badge/Gurubase-Ask%20AIOS%20Guru-006BFF)](https://gurubase.io/g/aios)

<a href="https://trendshift.io/repositories/8908" target="_blank"><img src="https://trendshift.io/api/badge/repositories/8908" alt="agiresearch%2FAIOS | Trendshift" style="width: 250px; height: 55px;" width="250" height="55"/></a>
<a href="https://give.rutgersfoundation.org/aios-project/23717.html" target="_blank"><img src="docs/assets/sponsor.png" alt="Sponsor" style="width: 250px; height: 55px;" width="250" height="55"/></a>

AIOS 是 AI 智能体操作系统，它将大语言模型（LLM）嵌入到操作系统中，以促进基于 LLM 的 AI 智能体的开发与部署。AIOS 旨在解决基于 LLM 的智能体在开发与部署过程中遇到的问题（例如调度、上下文切换、内存管理、存储管理、工具管理、智能体 SDK 管理等），从而为智能体开发者和用户构建更完善的 AIOS-智能体生态系统。AIOS 包含 AIOS 内核（本 [AIOS](https://github.com/agiresearch/AIOS) 仓库）和 AIOS SDK（[Cerebrum](https://github.com/agiresearch/Cerebrum) 仓库）。AIOS 同时支持 Web UI 和终端界面。

## 🏠 AIOS 架构
### 概览
<p align="center">
<img src="docs/assets/aios-figs/architecture.jpg">
</p>

AIOS 系统由两个核心组件构成：AIOS 内核与 AIOS SDK。
AIOS 内核作为操作系统内核的抽象层，管理智能体所需的各类资源，如 LLM、内存、存储和工具。 
AIOS SDK 面向智能体用户与开发者设计，使其能够通过与 AIOS 内核交互来构建和运行智能体应用。
AIOS 内核即为当前仓库，AIOS SDK 可在此处查看：[Cerebrum](https://github.com/agiresearch/Cerebrum)

### 模块与连接
下图展示了智能体如何利用 AIOS SDK 与 AIOS 内核进行交互，以及 AIOS 内核如何接收智能体查询，并利用调度后分发到不同模块执行的系统调用（syscall）链。 
<p align="center">
<img src="docs/assets/aios-figs/details.png">
</p>

### 计算机操作专用架构
针对计算机操作（computer-use）智能体，该架构在 AIOS 内核基础上进行了以“计算机上下文感知”为核心的显著增强。在保留 LLM Core（大模型核心）、Context Manager（上下文管理器）和 Memory Manager（内存管理器）等核心组件的同时，Tool Manager（工具管理器）模块经过彻底重构，引入了 VM（虚拟机）控制器与 MCP Server。
此次重构创建了一个沙盒环境，使智能体能够在保持智能体意图与计算机操作之间语义映射一致的前提下，安全地与计算机系统交互。 

<p align="center">
<img src="docs/assets/litecua-figs/architecture.png">
</p>

## 📰 更新日志
- **[2025-07-08]** 🎉 基础论文 [AIOS: LLM Agent Operating System](https://arxiv.org/abs/2403.16971) 已被语言建模会议（COLM 2025）接收。祝贺团队！
- **[2025-07-02]** 🎉 AIOS 入选由 Berkeley RDI 与高级 LLM Agents MOOC 联合举办的 AgentX – LLM Agents MOOC 竞赛决赛名单。祝贺团队！
- **[2025-05-24]** 📋 查看我们关于计算机操作智能体的论文：[LiteCUA: Computer as MCP Server for Computer-Use Agent on AIOS](https://arxiv.org/pdf/2505.18829) 及对应的 [代码库](https://github.com/agiresearch/LiteCUA)。 
- **[2025-03-13]** 📋 论文 [Cerebrum (AIOS SDK): A Platform for Agent Development, Deployment, Distribution, and Discovery](https://arxiv.org/abs/2503.11444) 已被 NAACL 2025 接收！相关功能已集成至 [Cerebrum](https://github.com/agiresearch/Cerebrum)。
- **[2025-03-12]** 🔥 代码库已完成重大重构，集成了多项强大新功能。请查看 AIOS v0.2.2 版本说明。
- **[2025-03-10]** 📋 查看我们关于智能体记忆的论文 [A-MEM: Agentic Memory for LLM Agents](https://arxiv.org/abs/2502.12110) 及对应的 [代码库](https://github.com/agiresearch/A-mem)。 
- **[2025-02-07]** 📋 我们的论文 [From Commands to Prompts: LLM-based Semantic File System for AIOS](https://arxiv.org/abs/2410.11843) 已被 ICLR 2025 接收！该论文的功能已作为 **终端界面（Terminal UI）** 集成至 AIOS。 
- **[2025-01-27]** 🔥 Deepseek-r1 (1.5b, 7b, 8b, 14b, 32b, 70b, 671b) 已全面支持，包括开源版本及 DeepSeek API（deepseek-chat 和 deepseek-reasoner）。 
- **[2024-11-30]** 🔥 AIOS v0.2：解耦了 AIOS 内核（本 [AIOS](https://github.com/agiresearch/AIOS) 仓库）与 AIOS SDK（[Cerebrum](https://github.com/agiresearch/Cerebrum) 仓库），并为智能体用户提供了远程内核支持。 
- **[2024-09-01]** 🔥 AIOS 支持多种智能体创建框架（例如 ReAct、Reflexion、OpenAGI、AutoGen、Open Interpreter、MetaGPT）。通过这些框架创建的智能体均可接入 AIOS。接入指南详见 [文档](https://docs.aios.foundation/aios-docs/aios-agent/how-to-develop-agents)。
- **[2024-07-10]** 📖 AIOS 官方文档已上线，请访问 [网站](https://docs.aios.foundation/)。
- **[2024-06-20]** 🔥 支持开源 LLM（原生 HuggingFace、vLLM、Ollama）的函数调用功能。
- **[2024-05-20]** 🚀 新增更多基于 ChatGPT 工具调用的智能体（即 MathAgent、RecAgent、TravelAgent、AcademicAgent 和 CreationAgent），其配置文件与工作流详见 [OpenAGI](https://github.com/agiresearch/OpenAGI)。
- **[2024-05-13]** 🛠️ 集成了来自 HuggingFace 的本地模型（扩散模型）作为工具。
- **[2024-05-01]** 🛠️ AIOS 中的智能体创建流程已重构，详见我们的 [OpenAGI](https://github.com/agiresearch/OpenAGI) 包。
- **[2024-04-05]** 🛠️ AIOS 目前支持外部工具调用（Google 搜索、WolframAlpha、Rapid API 等）。
- **[2024-04-02]** 🤝 AIOS [Discord 社区](https://discord.gg/B2HFxEgTJX) 已上线。欢迎加入社区进行讨论、头脑风暴、开发或随意交流！如需了解如何为 AIOS 做出贡献，请参阅 [CONTRIBUTE](https://github.com/agiresearch/AIOS/blob/main/docs/CONTRIBUTE.md)。
- **[2024-03-25]** ✈️ 我们的论文 [AIOS: LLM Agent Operating System](https://arxiv.org/abs/2403.16971) 正式发布！
- **[2023-12-06]** 📋 经过数月的研发，我们的观点论文 [LLM as OS, Agents as Apps: Envisioning AIOS, Agents and the AIOS-Agent Ecosystem](https://arxiv.org/abs/2312.03815) 正式发布。

## AIOS 的不同部署模式
在介绍 AIOS 不同模式之前，请先了解以下关键术语： 
- **AHM（智能体中心机）**：托管智能体市场/仓库的中心服务器，用户可在此发布、下载和共享智能体。作为所有智能体相关资源的分发中心。
- **AUM（智能体交互界面机）**：提供用户界面的客户端设备，用于与智能体交互。支持从手机到桌面端的任何能进行智能体可视化与控制设备的终端。
- **ADM（智能体开发机）**：开发者编写、调试和测试智能体的开发环境。需配备合适的开发工具库。
- **ARM（智能体运行机）**：实际执行任务并运行智能体的计算环境。需具备充足的算力资源以支持智能体操作。

下文将介绍 AIOS 的不同部署模式。**目前，AIOS 已支持 Mode 1 和 Mode 2，其他带有新功能的高级模式仍在持续开发中。**

### Mode 1（本地内核模式）

<p align="center">
<img src="docs/assets/aios-figs/stage1.png" width=300>
</p>

- 特性：
  - 面向智能体用户：可从机器 B 下载智能体，并在机器 A 上运行。 
  - 面向开发者：可在机器 A 开发测试智能体，并将智能体上传至机器 B 的智能体中心。

### Mode 2（远程内核模式）

<p align="center">
<img src="docs/assets/aios-figs/stage2.png" width=300>
</p>

- 特性： 
  - 远程使用智能体：用户/开发者可在机器 B 上使用智能体，该机器可与开发或运行机（机器 A）分离。  
  - 特别适合资源受限设备（如手机或边缘设备）的用户。

### Mode 2.5（远程内核开发模式）

<p align="center">
<img src="docs/assets/aios-figs/stage2.5.png" width=300>
</p>

- 特性：
  - 远程开发智能体：开发者可在机器 B 上进行开发，同时在机器 A 上运行和测试。适合资源受限设备的开发者。
- 关键技术：
  - 跨机器的打包与传输机制，以支持分布式开发与测试。

### Mode 3（个人远程内核模式）

<p align="center">
<img src="docs/assets/aios-figs/stage3.png" width=800>
</p>

- 进行中特性：
  - 在 AIOS 生态中注册账号的用户可拥有专属的 AIOS，并保留长期持久化数据。
  - 同一账号下的个人数据可同步至不同设备。

- 关键技术：
  - 用户账户注册与验证机制
  - 每个用户 AIOS 的持久化数据存储
  - 同一账号下跨设备的多实例同步
  - 数据安全隐私机制

### Mode 4（个人远程虚拟内核模式）

<p align="center">
<img src="docs/assets/aios-figs/stage4.png" width=800>
</p>

- 进行中特性：
  - 通过虚拟化技术，使不同用户的专属 AIOS 内核可在同一台物理机上共存。
- 关键技术：
  - 同机多实例内核的虚拟化
  - 跨虚拟机调度与资源分配机制


## ✈️ 快速入门
请参阅我们持续更新的 [文档](https://docs.aios.foundation/) 获取更多信息。
- [安装指南](https://docs.aios.foundation/aios-docs/getting-started/installation)
- [快速启动](https://docs.aios.foundation/aios-docs/getting-started/quickstart)
- [WebUI 快速启动](https://docs.aios.foundation/aios-docs/getting-started/webui-quickstart)

### 安装指南
#### 环境要求
##### Python
- 支持版本：**Python 3.10 - 3.11**

#### 从源码安装

##### 步骤 1：安装 AIOS 内核
克隆 AIOS 内核代码库
```bash
git clone https://github.com/agiresearch/AIOS.git
```
创建虚拟环境
```bash
python3.x -m venv venv # 仅支持 Python 3.10 和 3.11
source venv/bin/activate
```
或使用 conda 创建环境
```bash
conda create -n venv python=3.x  # 仅支持 Python 3.10 和 3.11
conda activate venv
```

> [!TIP]
> 我们强烈建议使用 [uv](https://github.com/astral-sh/uv) 进行更快、更可靠的包安装。
> 安装 uv： 
> ```bash pip install uv```

**GPU 环境：**
```bash
uv pip install -r requirements-cuda.txt
```

**纯 CPU 环境：**
```bash
uv pip install -r requirements.txt
```

或者，如果你偏好使用 pip：

**GPU 环境：**
```bash
pip install -r requirements-cuda.txt
```

**纯 CPU 环境：**
```bash
pip install -r requirements.txt
```

##### 步骤 2：安装 AIOS SDK（Cerebrum）
1. 克隆 Cerebrum 代码库：
   ```bash
   git clone https://github.com/agiresearch/Cerebrum.git
   ```
  
2. 使用 uv 安装（推荐）：
   ```bash
   cd Cerebrum && uv pip install -e .
   ```
   
   或使用 pip：
   ```bash
   cd Cerebrum && pip install -e .
   ```

##### 步骤 3：安装虚拟化环境（可选）
若要为计算机操作智能体使用 MCP，我们强烈建议你安装配备图形界面（GUI）的虚拟化环境。具体说明请参见[此处](https://github.com/xlang-ai/OSWorld)。 

**注意**：安装 AIOS 内核（AIOS）的机器也必须安装 AIOS SDK（Cerebrum）。默认情况下，安装 AIOS 内核会自动附带安装 AIOS SDK。如果你使用的是本地内核模式（即在单机上同时运行 AIOS 和智能体），只需在该机器上分别安装 AIOS 和 Cerebrum 即可。如果你使用的是远程内核模式（即 Machine 1 运行 AIOS，Machine 2 运行智能体并与内核远程交互），则需在 Machine 1 上安装 AIOS 内核与 SDK，并在 Machine 2 上单独安装 SDK。SDK 的安装指南请参见 [Cerebrum](https://github.com/agiresearch/Cerebrum)。

### 快速启动
在启动 AIOS 之前，需先完成配置。AIOS 提供两种配置方式：直接修改配置文件，或交互式设置。 

#### 直接配置文件（推荐）
你需要配置 OpenAI、Anthropic、Groq 和 HuggingFace 等服务的 API Key。最简单的方式是编辑 `aios/config/config.yaml` 文件。

> [!TIP]
> 重要提示：我们强烈建议使用 `aios/config/config.yaml` 文件来配置你的 API Key。该方法直观且能有效避免环境变量同步问题。 

在 `aios/config/config.yaml` 中配置 API Key 的简单示例如下：
```yaml
api_keys:
  openai: "your-openai-key"    
  gemini: "your-gemini-key"    
  groq: "your-groq-key"      
  anthropic: "your-anthropic-key" 
  huggingface:
    auth_token: "your-huggingface-token-for-authorized-models"  
    cache_dir: "your-cache-dir-for-saving-models"
  novita: "your-novita-api-key"
```

获取这些 API Key 的途径如下：
1. Deepseek API：访问 https://api-docs.deepseek.com/
2. OpenAI API：访问 https://platform.openai.com/api-keys
3. Google Gemini API：访问 https://makersuite.google.com/app/apikey
4. Groq API：访问 https://console.groq.com/keys
5. HuggingFace Token：访问 https://huggingface.co/settings/tokens
6. Anthropic API：访问 https://console.anthropic.com/keys
7. Novita AI API：访问 https://novita.ai/api-keys

#### 配置大语言模型
你可以在同一个 `aios/config/config.yaml` 文件中配置要使用的 LLM 模型。示例如下：

```yaml
llms:
  models:
    # Ollama Models
    - name: "qwen2.5:7b"
      backend: "ollama"
      hostname: "http://localhost:11434"  # 请确保已启动 ollama server

    # vLLM Models
    - name: "meta-llama/Llama-3.1-8B-Instruct"
      backend: "vllm"
      hostname: "http://localhost:8091/v1"  # 请确保已启动 vllm server
```

**使用 Ollama 模型：** 
1. 首先，从 https://ollama.com/ 下载 ollama。
2. 在另一个终端中启动 ollama 服务：
```bash
ollama serve
```
3. 从 https://ollama.com/library 拉取你需要的模型：
```bash
ollama pull qwen2.5:7b  # 示例模型
```

> [!TIP]
> Ollama 同时支持纯 CPU 和 GPU 环境。更多用法详见[Ollama 文档](https://github.com/ollama/ollama)。

**使用 vLLM 模型：**
1. 按照其[安装指南](https://docs.vllm.ai/en/latest/getting_started/installation.html)安装 vLLM。
2. 在另一个终端中启动 vLLM 服务：
```bash
vllm serve meta-llama/Llama-3.1-8B-Instruct --port 8091
```

> [!NOTE]
> vLLM 目前仅支持 Linux 和 GPU 环境。如无兼容环境，请选择其他后端选项。
> 启用 vllm 的 tool calling（工具调用）功能，请参阅 https://docs.vllm.ai/en/latest/features/tool_calling.html

**使用 HuggingFace 模型：** 
你可以为 HuggingFace 模型配置特定的显存分配：
```yaml
- name: "meta-llama/Llama-3.1-8B-Instruct"
  backend: "huggingface"
  max_gpu_memory: {0: "24GB", 1: "24GB"}  # GPU 显存分配
  eval_device: "cuda:0"  # 模型评估设备
```

#### 交互式设置

或者，你也可以通过以下命令进行交互式配置： 

- `aios env list`：显示当前环境变量；若未设置变量，则显示可用的 API Key。
- `aios env set`：查看/配置当前环境变量（若未设置，则显示可用的 API Key）。
- `aios refresh`：刷新 AIOS 配置。
  重新加载 `aios/config/config.yaml` 中的配置。
  在不重启服务器的情况下重新初始化所有组件。服务器必须处于运行状态。

当未设置环境变量时，将显示以下可用的 API Key：
- `DEEPSEEK_API_KEY`：用于访问 Deepseek 服务的 API Key
- `OPENAI_API_KEY`：用于访问 OpenAI 服务的 API Key
- `GEMINI_API_KEY`：用于访问 Google Gemini 服务的 API Key
- `GROQ_API_KEY`：用于访问 Groq 服务的 API Key
- `HF_AUTH_TOKEN`：用于访问 HuggingFace 模型的认证 Token
- `HF_HOME`：可选，存储 HuggingFace 模型的路径
- `NOVITA_API_KEY`：用于访问 Novita AI 服务的 API Key

#### 启动 AIOS
完成密钥或环境参数配置后，可按以下步骤启动：

运行：

```
bash runtime/launch_kernel.sh
```

或者，如果你需要通过显式指定 Python 版本（如 `python3.10`、`python3.11`、`python3` 等）来运行，请执行以下命令：

```
python3.x -m uvicorn runtime.launch:app --host 0.0.0.0 --port 8000 # 请将端口替换为你自己的端口
```

你还需在 Cerebrum（AIOS SDK）的配置中设置 `host` 和 `port`，以确保与 AIOS 配置一致。 

你也可以通过以下方式强制内核在后台运行：
```
python3.x -m uvicorn runtime.launch:app --host 0.0.0.0 > uvicorn.log 2>&1 &
```

若需在终端关闭后继续运行，可在命令前添加 `nohup`。

推荐在后台启动内核的命令（使其在活跃 shell 关闭后仍持续运行，并将日志输出到指定文件）：

```
nohup python3 -m uvicorn runtime.launch:app --host 0.0.0.0 --port 8000 > uvicorn.log 2>&1 &
```

#### 与 AIOS 终端交互

要与 AIOS 终端（基于 LLM 的语义文件系统）进行交互，请运行以下命令启动：

```
python scripts/run_terminal.py
```

随后即可通过输入自然语言指令开始与 AIOS 终端交互。 

成功启动后，界面将显示如下： 

<p align="center">
<img src="docs/assets/terminal-figs/example.png" width=800>
</p>

详细使用指南请参见[此处](https://github.com/agiresearch/AIOS-LSFS)。

> [!WARNING]
> AIOS 终端的回滚功能依赖 Redis 服务器连接。如需使用该功能，请确保已启动 Redis 服务。

#### 运行计算机操作智能体
确保已安装带 GUI 的虚拟化环境后，可参考 [Cerebrum](https://github.com/agiresearch/Cerebrum) 了解如何运行计算机操作智能体。 

### 支持的智能体框架
- [OpenAGI](https://github.com/agiresearch/openagi)
- [AutoGen](https://github.com/microsoft/autogen)
- [Open-Interpreter](https://github.com/OpenInterpreter/open-interpreter)
- [MetaGPT](https://github.com/geekan/MetaGPT?tab=readme-ov-file)

### 支持的大语言模型后端
| 提供商 🏢 | 模型名称 🤖 | 开源 🔓 | 模型标识 ⌨️ | 后端引擎 ⚙️ | 所需 API Key |
|:------------|:-------------|:---------------|:---------------|:---------------|:----------------|
| Anthropic | [All Models](https://makersuite.google.com/app/apikey) | ❌ | model-name | anthropic | ANTHROPIC_API_KEY |
| OpenAI | [All Models](https://platform.openai.com/docs/models) | ✅ | model-name | openai | OPENAI_API_KEY |
| Deepseek | [All Models](https://api-docs.deepseek.com/) | ✅ | model-name | deepseek | DEEPSEEK_API_KEY |
| Google | [All Models](https://makersuite.google.com/app/apikey) | ❌ | model-name | gemini| GEMINI_API_KEY |
| Groq | [All Models](https://console.groq.com/keys) | ✅ | model-name | groq | GROQ_API_KEY |
| HuggingFace | [All Models](https://huggingface.co/models/) | ✅ | model-name |huggingface| HF_HOME |
| ollama | [All Models](https://ollama.com/search) | ✅ | model-name | ollama | - |
| vLLM | [All Models](https://docs.vllm.ai/en/latest/) | ✅ | model-name | vllm | - |
| Novita | [All Models](https://novita.ai/models/llm) | ✅ | model-name | novita | NOVITA_API_KEY |

## 🔧 实验性 Rust 重写版本（aios-rs）
`aios-rs/` 目录下包含早期的实验性 Rust 框架，提供了 Trait 定义及最小化的占位实现（涵盖 context、memory、storage、tool、scheduler、llm）。目前尚未实现功能完全对等；它旨在作为增量迁移的基础，并用于构建性能导向的组件。

### 试用方法
```bash
cd aios-rs
cargo build
cargo test
```

### 示例（Echo LLM + Noop 调度器）
```rust
use aios_rs::prelude::*;

fn main() -> anyhow::Result<()> {
  let llm = std::sync::Arc::new(EchoLLM);
  let memory = std::sync::Arc::new(std::sync::Mutex::new(InMemoryMemoryManager::new()));
  let storage = std::sync::Arc::new(FsStorageManager::new("/tmp/aios_store"));
  let tool = std::sync::Arc::new(NoopToolManager);
  let mut scheduler = NoopScheduler::new(llm, memory, storage, tool);
  scheduler.start()?;
  scheduler.stop()?;
  Ok(())
}
```

## 引用文献
```
@article{mei2025aios,
  title={AIOS: LLM Agent Operating System},
  author={Mei, Kai and Zhu, Xi and Xu, Wujiang and Hua, Wenyue and Jin, Mingyu and Li, Zelong and Xu, Shuyuan and Ye, Ruosong and Ge, Yingqiang and Zhang, Yongfeng}
  journal={In Proceedings of the 2nd Conference on Language Modeling (COLM 2025)},
  year={2025}
}
@article{mei2025litecua,
  title={LiteCUA: Computer as MCP Server for Computer-Use Agent on AIOS},
  author={Mei, Kai and Zhu, Xi and Gao, Hang and Lin, Shuhang and Zhang, Yongfeng},
  journal={arXiv preprint arXiv:2505.18829},
  year={2025}
}
@article{xu2025mem,
  title={A-Mem: Agentic Memory for LLM Agents},
  author={Xu, Wujiang and Liang, Zujie and Mei, Kai and Gao, Hang and Tan, Juntao and Zhang, Yongfeng},
  journal={arXiv:2502.12110},
  year={2025}
}
@inproceedings{rama2025cerebrum,
  title={Cerebrum (AIOS SDK): A Platform for Agent Development, Deployment, Distribution, and Discovery}, 
  author={Balaji Rama and Kai Mei and Yongfeng Zhang},
  booktitle={2025 Annual Conference of the Nations of the Americas Chapter of the Association for Computational Linguistics},
  year={2025}
}
@inproceedings{shi2025from,
  title={From Commands to Prompts: {LLM}-based Semantic File System for AIOS},
  author={Zeru Shi and Kai Mei and Mingyu Jin and Yongye Su and Chaoji Zuo and Wenyue Hua and Wujiang Xu and Yujie Ren and Zirui Liu and Mengnan Du and Dong Deng and Yongfeng Zhang},
  booktitle={The Thirteenth International Conference on Learning Representations},
  year={2025},
  url={https://openreview.net/forum?id=2G021ZqUEZ}
}
@article{ge2023llm,
  title={LLM as OS, Agents as Apps: Envisioning AIOS, Agents and the AIOS-Agent Ecosystem},
  author={Ge, Yingqiang and Ren, Yujie and Hua, Wenyue and Xu, Shuyuan and Tan, Juntao and Zhang, Yongfeng},
  journal={arXiv:2312.03815},
  year={2023}
}
```

## 🚀 贡献指南
参与贡献请参阅 [CONTRIBUTE](https://github.com/agiresearch/AIOS/blob/main/docs/CONTRIBUTE.md)。如果你希望为代码库做出贡献，[issues](https://github.com/agiresearch/AIOS/issues) 或 [pull requests](https://github.com/agiresearch/AIOS/pulls) 均欢迎提交！

## 🌍 AIOS 贡献者
[![AIOS contributors](https://contrib.rocks/image?repo=agiresearch/AIOS&max=300)](https://github.com/agiresearch/AIOS/graphs/contributors)

## 致谢
我们在设计与代码实现上借鉴了以下项目：[LiteLLM](https://docs.litellm.ai/docs/)、[OSWorld](https://os-world.github.io/)。

## 🤝 Discord 社区
欢迎加入我们的 [Discord Community](https://discord.gg/B2HFxEgTJX)！在这里你可以提问、与同好交流、探讨或提议新功能，并参与后续开发。
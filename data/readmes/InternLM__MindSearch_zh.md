<div id="top"></div>

<div align="center">

<picture>
  <source srcset="assets/logo.svg" media="(prefers-color-scheme: light)">
  <source srcset="assets/logo-darkmode.svg" media="(prefers-color-scheme: dark)">
  <img src="assets/logo.svg" alt="Logo" width="50%">
</picture>

[📃 Paper](https://arxiv.org/abs/2407.20183) | [💻 Demo](https://internlm-chat.intern-ai.org.cn/)

English | [简体中文](README_zh-CN.md)

<https://github.com/user-attachments/assets/44ffe4b9-be26-4b93-a77b-02fed16e33fe>

</div>
</p>

## ✨ MindSearch：模拟人类心智，激发深度AI搜索能力

## 📅 更新日志

- 2024/11/05: 🥳 MindSearch 现已部署至 Puyu！👉 [点击尝试](https://internlm-chat.intern-ai.org.cn/) 👈
  - 基于 [Lagent v0.5](https://github.com/InternLM/lagent) 重构了 Agent（智能体）模块，以提升并发处理能力。
  - 优化了用户界面（UI），以直观展示多查询并行搜索过程。


## ⚽️ 构建你自己的 MindSearch

### 步骤一：安装依赖项

```bash
git clone https://github.com/InternLM/MindSearch
cd MindSearch
pip install -r requirements.txt
```

### 步骤二：配置环境变量

在部署 API 之前，你需要先配置环境变量。将 `.env.example` 文件重命名为 `.env` 并填写所需值。

```bash
mv .env.example .env
# 打开 .env 文件并添加你的密钥及模型配置
```

### 步骤三：部署 MindSearch API

启动 FastAPI 服务。

```bash
python -m mindsearch.app --lang en --model_format internlm_server --search_engine DuckDuckGoSearch --asy 
```

- `--lang`：模型语言，`en` 表示英文，`cn` 表示中文。
- `--model_format`：模型调用格式。
  - `internlm_server` 用于本地服务器部署的 InternLM2.5-7b-chat。（该模型对中文进行了更优优化。）
  - `gpt4` 用于调用 GPT-4。
    如需使用其他模型，请修改 [models](./mindsearch/agent/models.py) 文件。
- `--search_engine`：搜索引擎。
  - `DuckDuckGoSearch` 使用 DuckDuckGo 搜索引擎。
  - `BingSearch` 使用必应（Bing）搜索引擎。
  - `BraveSearch` 使用 Brave Web API 引擎。
  - `GoogleSearch` 使用 Google Serper Web Search API 引擎。
  - `TencentSearch` 使用腾讯搜索 API 引擎。
  
  除非使用 DuckDuckGo 或腾讯搜索（TencentSearch），否则请将你的网页搜索引擎 API Key 设置为环境变量 `WEB_SEARCH_API_KEY`。若使用腾讯搜索，还需将密钥 ID 配置为 `TENCENT_SEARCH_SECRET_ID`，密钥 Key 配置为 `TENCENT_SEARCH_SECRET_KEY`。
- `--asy`：部署异步 Agent（智能体）。

### 步骤四：配置前端界面

提供以下前端交互界面供选择：

- React

首先配置 Vite 代理的后端地址。

```bash
HOST="127.0.0.1"  # modify as you need
PORT=8002
sed -i -r "s/target:\s*\"\"/target: \"${HOST}:${PORT}\"/" frontend/React/vite.config.ts
```

```bash
# Install Node.js and npm
# for Ubuntu
sudo apt install nodejs npm

# for windows
# download from https://nodejs.org/zh-cn/download/prebuilt-installer

# Install dependencies

cd frontend/React
npm install
npm start
```

详细信息请查看 [React](./frontend/React/README.md) 文档。

- Gradio

```bash
python frontend/mindsearch_gradio.py
```

- Streamlit

```bash
streamlit run frontend/mindsearch_streamlit.py
```

## 🌐 更换网页搜索 API

如需使用其他类型的网页搜索 API，请修改位于 `mindsearch/agent/__init__.py` 中的 `searcher_cfg` 下的 `searcher_type` 属性。目前支持的网页搜索 API 包括：

- `GoogleSearch`
- `DuckDuckGoSearch`
- `BraveSearch`
- `BingSearch`
- `TencentSearch`

例如，若要切换至 Brave Search API，可按如下方式配置：

```python
BingBrowser(
    searcher_type='BraveSearch',
    topk=2,
    api_key=os.environ.get('BRAVE_API_KEY', 'YOUR BRAVE API')
)
```

## 🐞 仅使用后端（无前端）

对于希望直接与后端交互的用户，可使用 `backend_example.py` 脚本。该脚本演示了如何向后端发送查询并处理响应。

```bash
python backend_example.py
```

执行脚本前，请确保已配置好环境变量且后端服务正在运行。

## 🐞 本地调试

```bash
python -m mindsearch.terminal
```

## 📝 许可证

本项目遵循 [Apache 2.0 license](LICENSE) 开源。

## 引用

如果你的研究使用了该项目，请考虑引用：

```
@article{chen2024mindsearch,
  title={MindSearch: Mimicking Human Minds Elicits Deep AI Searcher},
  author={Chen, Zehui and Liu, Kuikun and Wang, Qiuchen and Liu, Jiangning and Zhang, Wenwei and Chen, Kai and Zhao, Feng},
  journal={arXiv preprint arXiv:2407.20183},
  year={2024}
}
```

## 相关项目

探索我们在大语言模型领域的其他研究成果，重点关注 LLM（大型语言模型）智能体。

- [Lagent](https://github.com/InternLM/lagent): A lightweight framework for building LLM-based agents
- [AgentFLAN](https://github.com/InternLM/Agent-FLAN): An innovative approach for constructing and training with high-quality agent datasets (ACL 2024 Findings)
- [T-Eval](https://github.com/open-compass/T-Eval): A Fine-grained tool utilization evaluation benchmark (ACL 2024)
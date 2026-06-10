![PySpur](./docs/images/hero.png)

<p align="center"><strong>迭代速度提升 10 倍。AI 工程师使用 PySpur 以可视化方式迭代 AI Agent（智能体），无需重复造轮子。</strong></p>

<p align="center">
  <a href="./README.md"><img alt="README in English" src="https://img.shields.io/badge/English-blue"></a>
  <a href="./README_CN.md"><img alt="简体中文版自述文件" src="https://img.chields.io/badge/简体中文-blue"></a>
  <a href="./README_JA.md"><img alt="日本語のREADME" src="https://img.shields.io/badge/日本語-blue"></a>
  <a href="./README_KR.md"><img alt="README in Korean" src="https://img.chields.io/badge/한국어-blue"></a>
  <a href="./README_DE.md"><img alt="Deutsche Version der README" src="https://img.shields.io/badge/Deutsch-blue"></a>
<a href="./README_FR.md"><img alt="Version française du README" src="https://img.chields.io/badge/Français-blue"></a>
<a href="./README_ES.md"><img alt="Versión en español del README" src="https://img.shields.io/badge/Español-blue"></a>
</p>

<p align="center">
<a href="https://docs.pyspur.dev/" target="_blank">
  <img alt="Docs" src="https://img.chields.io/badge/Docs-green.svg?style=for-the-badge&logo=readthedocs&logoColor=white">
</a>
<a href="https://forms.gle/5wHRctedMpgfNGah7" target="_blank">
  <img alt="Cloud" src="https://img.chields.io/badge/Cloud-orange.svg?style=for-the-badge&logo=cloud&logoColor=white">
</a>
</p>

https://github.com/user-attachments/assets/54d0619f-22fd-476c-bf19-9be083d7e710

# 🕸️ 为什么选择 PySpur？

## 痛点：让 AI 变得可靠，需历经上千次细微的折磨

如今的 AI 工程师在构建 Agent（智能体）时面临三大难题： 

* **提示词地狱**：花费数小时反复调整提示词，陷入试错的挫败感中。
* **工作流盲区**：缺乏对步骤间交互的可见性，导致隐藏的错误和逻辑混乱。
* **终端测试噩梦**：盯着原始输出结果，手动解析 JSON 数据。

我们也曾深陷其中。2024 年初我们上线了一款图形设计 Agent，迅速积累了数千名用户，但受限于可靠性不足和现有调试工具的缺失，开发过程举步维艰。 

## 解决方案：节省时间的 Agent 沙盒（Playground）

### 步骤 1：定义测试用例

https://github.com/user-attachments/assets/ed9ca45f-7346-463f-b8a4-205bf2c4588f
 
### 步骤 2：通过 Python 代码或 UI 构建 Agent

https://github.com/user-attachments/assets/7043aae4-fad1-42bd-953a-80c94fce8253

### 步骤 3：高频迭代调试

https://github.com/user-attachments/assets/72c9901d-a39c-4f80-85a5-f6f76e55f473

### 步骤 4：部署上线

https://github.com/user-attachments/assets/b14f34b2-9f16-4bd0-8a0f-1c26e690af93

# ✨ 核心功能：

- 👤 **人工介入（Human-in-the-Loop）**：支持持久化工作流，可等待人工审批后继续执行。
- 🔄 **循环调用**：具备记忆功能的迭代式工具调用机制。
- 📤 **文件上传**：支持上传文件或粘贴 URL 以处理文档。
- 📋 **结构化输出**：提供 JSON Schema 的可视化编辑器。
- 🗃️ **RAG（检索增强生成）**：支持解析、分块、向量化及数据写入向量数据库。
- 🖼️ **多模态**：全面支持视频、图像、音频、文本和代码处理。
- 🧰 **工具集成**：内置 Slack、Firecrawl.dev、Google Sheets、GitHub 等丰富插件。
- 📊 **执行追踪（Traces）**：自动捕获已部署 Agent 的运行轨迹与日志。
- 🧪 **效果评估（Evals）**：基于真实数据集对 Agent 进行性能评估。
- 🚀 **一键部署**：发布为 API 接口，灵活集成到任意业务场景中。
- 🐍 **基于 Python**：仅需创建一个 Python 文件即可添加自定义节点。
- 🎛️ **全厂商支持**：兼容 100+ 大语言模型（LLM）提供商、Embedding 模型及向量数据库。

# ⚡ 快速入门

这是最快的上手方式，需安装 Python 3.11 或更高版本。

1. **安装 PySpur：**
    ```sh
    pip install pyspur
    ```

2. **初始化新项目：**
    ```sh
    pyspur init my-project
    cd my-project
    ```
    这将创建一个包含 `.env` 配置文件的目录。

3. **启动服务：**
    ```sh
    pyspur serve --sqlite
    ```
    默认情况下，此命令将在 `http://localhost:6080` 启动 PySpur 应用（使用 SQLite 数据库）。建议你在 `.env` 文件中配置 PostgreSQL 实例地址，以获得更稳定的运行体验。

4. **【可选】配置环境变量并添加 API Key：**
    - **应用界面**：前往“API Keys”标签页添加提供商密钥（OpenAI、Anthropic 等）
    - **手动配置**：编辑 `.env` 文件（推荐配置 PostgreSQL），然后运行 `pyspur serve` 重启服务


# 😎 功能演示

## 人工介入断点：

当流程运行至这些断点时会暂停，等待人工审批后继续执行。该功能为需要质量保证的工作流提供了人工监督机制：在流程推进前验证关键输出结果。

https://github.com/user-attachments/assets/98cb2b4e-207c-4d97-965b-4fee47c94ce8

## 节点级调试：

https://github.com/user-attachments/assets/6e82ad25-2a46-4c50-b030-415ea9994690

## 多模态支持（上传文件或粘贴 URL）

PDFs、视频、音频、图像等...

https://github.com/user-attachments/assets/83ed9a22-1ec1-4d86-9dd6-5d945588fd0b

## 循环机制

<img width="1919" alt="Loops" src="https://github.com/user-attachments/assets/3aea63dc-f46f-46e9-bddd-e2af9c2a56bf" />

## RAG（检索增强生成）

### 步骤 1：创建文档集合（分块与解析）

https://github.com/user-attachments/assets/c77723b1-c076-4a64-a01d-6d6677e9c60e

### 步骤 2：创建向量索引（向量化与数据写入）

https://github.com/user-attachments/assets/50e5c711-dd01-4d92-bb23-181a1c5bba25

## 模块化构建模块

https://github.com/user-attachments/assets/6442f0ad-86d8-43d9-aa70-e5c01e55e876

## 评估最终性能

https://github.com/user-attachments/assets/4dc2abc3-c6e6-4d6d-a5c3-787d518de7ae

## 即将推出：自我优化（Self-improvement）

https://github.com/user-attachments/assets/5bef7a16-ef9f-4650-b385-4ea70fa54c8a

# 🛠️ PySpur 开发环境搭建
#### 【适用于类 Unix 系统的开发说明。暂不支持 Windows/PC 环境】

推荐使用我们的开发容器（`.devcontainer/devcontainer.json`）配合 Cursor 或 VS Code，以便获得：
- 统一的开发环境，预置了所需工具与扩展插件
- 针对 Python 和 TypeScript 开发的优化配置
- 自动热重载与端口转发功能

**方案一：Cursor/VS Code 开发容器（推荐）**
1. 安装 [Cursor](https://www.cursor.com/)/[VS Code](https://code.visualstudio.com/) 及 [Dev Containers 扩展插件](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)
2. 克隆并打开项目仓库
3. 根据提示点击“在容器中重新打开”

**方案二：手动配置**
1. **克隆仓库：**
    ```sh
    git clone https://github.com/PySpur-com/pyspur.git
    cd pyspur
    ```

2. **使用 Docker Compose 启动服务：**
    ```sh
    docker compose -f docker-compose.dev.yml up --build -d
    ```

3. **自定义配置：**
    编辑 `.env` 文件以配置运行环境（例如 PostgreSQL 相关设置）。

注意：手动方案需要额外的配置步骤，且可能无法完全复现开发容器的全部功能。

# ⭐ 支持我们

如果你认可我们的工作，欢迎给我们点个 Star！非常感谢！

![star](https://github.com/user-attachments/assets/71f65273-6755-469d-be44-087bb89d5e76)

你的反馈对我们至关重要。请通过 [邮件告知我们](mailto:founders@pyspur.dev?subject=Feature%20Request&body=I%20want%20this%20feature%3Ai) 你希望优先看到列表中的哪些功能，或提出全新的需求建议。
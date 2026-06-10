<div align="center">
  <a href="https://code2prompt.dev">
    <img align="center" width="550px" src="https://github.com/mufeedvh/code2prompt/blob/main/.assets/logo_dark_v0.0.2.svg?raw=true" alt="Code2prompt"/>
  </a>
  <br>
  <h3>将你的代码库转换为单个大语言模型（LLM）提示词。</h3>
</div>

<p align="center">
  <a href="https://code2prompt.dev"><b>网站</b></a> •
  <a href="https://code2prompt.dev/docs/welcome/"><b>文档</b></a> •
  <a href="https://discord.com/invite/ZZyBbsHTwH"><b>Discord</b></a>
</p>

<div align="center">

[![License](https://img.shields.io/github/license/mufeedvh/code2prompt.svg?style=flat-square)](https://github.com/mufeedvh/code2prompt/blob/master/LICENSE)
[![Crates.io](https://img.shields.io/crates/v/code2prompt.svg?style=flat-square)](https://crates.io/crates/code2prompt)
[![PyPI](https://img.shields.io/pypi/v/code2prompt-rs?style=flat-square&logo=pypi&logoColor=white)](https://pypi.org/project/code2prompt-rs/)
[![CI](https://github.com/mufeedvh/code2prompt/actions/workflows/ci.yml/badge.svg?style=flat-square)](https://github.com/mufeedvh/code2prompt/actions)
[![Discord](https://img.shields.io/discord/1342336677905039451?style=flat-square&logo=discord&logoColor=white)](https://discord.com/invite/ZZyBbsHTwH)
[![Docs.rs](https://docs.rs/code2prompt-core/badge.svg?style=flat-square)](https://docs.rs/code2prompt-core)
[![Crates.io Downloads](https://img.shields.io/crates/d/code2prompt.svg?style=flat-square)](https://crates.io/crates/code2prompt)
[![GitHub Stars](https://img.shields.io/github/stars/mufeedvh/code2prompt?style=social)](https://github.com/mufeedvh/code2prompt)

</div>

---

<h1 align="center">
  <a href="https://code2prompt.dev"><img src="https://github.com/mufeedvh/code2prompt/blob/main/.assets/demo.gif?raw=true" alt="code2prompt demo"></a>
</h1>

![Flow Diagram](https://github.com/mufeedvh/code2prompt/blob/main/.assets/flow_diagram.png?raw=true)

**Code2Prompt** 是一款强大的上下文工程（Context Engineering）工具，旨在解析代码库并将其格式化为适合大语言模型使用的提示词。无论你是手动为 ChatGPT 复制上下文、通过 Python 构建 AI Agent，还是运行 MCP Server，Code2Prompt 都能简化你的上下文准备流程。

## ⚡ 快速安装

### Cargo

```bash
cargo install code2prompt 
```

如需启用可选的 Wayland 支持（例如用于基于 Wayland 系统的剪贴板集成），请使用 `wayland` 特性标志：

```bash
cargo install --features wayland code2prompt
```

### Homebrew

```bash
brew install code2prompt
```

### 通过 pip 安装 SDK 🐍

```bash
pip install code2prompt-rs
```

## 🚀 快速上手

安装完成后，只需将工具指向你的项目目录即可生成提示词。

**基本用法**：从当前目录生成提示词并复制到剪贴板。

```sh
code2prompt .
```

**保存到文件**：

```sh
code2prompt path/to/project --output-file prompt.txt
```

## 🌐 生态系统

Code2Prompt 不仅仅是一个命令行工具，它是一个完整的代码库上下文生态体系。

| 🧱 核心库 <br><img src="https://img.shields.io/badge/Rust-FF6700?style=for-the-badge&logo=rust&logoColor=white" alt="Rust Core Badge"/>| 💻 CLI 工具 <br><img src="https://img.shields.io/badge/Terminal-2C3E50?style=for-the-badge&logo=gnu-bash&logoColor=white" alt="CLI Badge"/> | 🐍 Python SDK <br><img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python SDK Badge"/> | 🤖 MCP Server <img src="https://img.shields.io/badge/Agentic%20Flow-7E57C2?style=for-the-badge&logo=server&logoColor=white" alt="MCP Server Badge"/> |
| :---: | :---: | :---: | :---: |
| 内部高速库，负责安全地遍历文件、遵循 `.gitignore` 规则并结构化 Git 元数据。 | 专为人类设计，提供极简的命令行界面（CLI）和交互式终端用户界面（TUI）。生成格式化提示词、跟踪 Token 使用情况，并将结果输出到剪贴板或标准输出。 | 提供对 Rust 核心库的快速 Python 绑定。非常适合用于 AI Agent、自动化脚本或深度集成到 RAG 流水线中。已在 PyPI 发布。 | 将 Code2Prompt 作为本地服务运行，使智能体应用能够高效读取你的本地代码库，同时避免上下文窗口被过度占用。 |

## 📚 文档

请参阅在线[文档](https://code2prompt.dev/docs/welcome/)获取详细说明。

## ✨ 功能特性

Code2Prompt 将你的整个代码库转换为结构清晰的大语言模型提示词。主要功能包括：

- **终端用户界面（TUI）**：交互式终端界面，用于配置和生成提示词
- **智能过滤**：使用通配符模式包含/排除文件，并遵循 `.gitignore` 规则
- **灵活模板**：通过 Handlebars 模板针对不同用例自定义提示词
- **自动代码处理**：将任意规模的代码库转换为可读、格式化的提示词
- **Token 跟踪**：追踪 Token 使用情况，确保不超出大语言模型的上下文限制
- **智能文件读取**：简化大语言模型对多种文件格式（如 CSV、Notebook、JSONL 等）的读取过程
- **Git 集成**：在提示词中包含代码差异（diffs）、日志和分支对比信息
- **极速运行**：基于 Rust 构建，性能卓越且资源占用极低

停止手动复制文件和为 LLM 格式化代码。Code2Prompt 替你处理繁琐的工作，让你专注于从 AI 模型中获取见解和解决方案。

## 替代安装方式

请参阅[文档](https://code2prompt.dev/docs/how_to/install/)获取详细的安装说明。

### Binary releases

从 [Release 页面](https://github.com/mufeedvh/code2prompt/releases)下载适用于你操作系统的最新二进制文件。

### Source build

需要：

- [Git](https://git-scm.org/downloads)、[Rust](https://rust-lang.org/tools/install) 和 `Cargo`。

```sh
git clone https://github.com/mufeedvh/code2prompt.git
cd code2prompt/
cargo install --path crates/code2prompt
```

## ⭐ Star Gazing

[![Star History Chart](https://api.star-history.com/svg?repos=mufeedvh/code2prompt&type=Date)](https://star-history.com/#mufeedvh/code2prompt&Date)

## 📜 License

本项目采用 MIT 许可证，详见 <a href="https://github.com/mufeedvh/code2prompt/blob/master/LICENSE">LICENSE</a>。

## Liked the project?

如果你喜欢这个项目并觉得它有用，请给它一个 :star: !

## 👥 Contribution

参与贡献的方式：

- 提出功能建议
- 报告 Bug
- 修复问题并提交 Pull Request
- 协助编写代码文档
- 分享推广
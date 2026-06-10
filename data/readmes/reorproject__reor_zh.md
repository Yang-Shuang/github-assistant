<h1 align="center">Reor 项目</h1>
<!-- <p align="center">
    <img src="logo_or_graphic_representation.png" alt="Reor Logo">
</p> -->

<h4 align="center">私密且本地运行的 AI 个人知识管理应用。</h4>

<p align="center">
    <a href="https://tooomm.github.io/github-release-stats/?username=reorproject&repository=reor">    <img alt="GitHub Downloads (all assets, all releases)" src="https://img.shields.io/github/downloads/reorproject/reor/total"></a>
<a href="https://discord.gg/b7zanGCTUY" target="_blank"><img src="https://dcbadge.vercel.app/api/server/QBhGUFJYuH?style=flat&compact=true" alt="Discord"></a>
    <img alt="GitHub Repo stars" src="https://img.shields.io/github/stars/reorproject/reor">

</p>

> ### 📢 公告
>
> 我们现在已入驻 [Discord](https://discord.gg/b7zanGCTUY)！我们的团队目前正以极快的速度迭代开发，因此分享你的 ❤️反馈❤️ 将极大地帮助我们塑造产品 🚀

## About

**Reor** 是一款由 AI 驱动的桌面笔记应用：它能自动关联相关笔记、解答关于你笔记的提问，并提供语义搜索功能。所有数据均本地存储，你可以使用类 Obsidian 的 Markdown 编辑器来编辑你的笔记。

该项目的核心假设是：思维辅助类的 AI 工具应默认在本地运行模型。Reor 站在 [Ollama](https://github.com/ollama/ollama)、[Transformers.js](https://github.com/xenova/transformers.js) 和 [LanceDB](https://github.com/lancedb/lancedb) 这些巨人的肩膀上，实现了大语言模型（LLM）和嵌入模型在本地运行：

1. 你编写的每篇笔记都会被分块并嵌入到内部的向量数据库中。
2. 相关笔记会通过向量相似度自动连接。
3. LLM 驱动的问答功能会对你的笔记语料库进行 RAG（检索增强生成）处理。
4. 所有内容均支持语义搜索。

<https://github.com/reorproject/reor/assets/17236551/94a1dfeb-3361-45cd-8ebc-5cfed81ed9cb>

可以将 Reor 视为一个拥有两个生成器的 RAG（检索增强生成）应用：LLM 和人类。在问答模式下，系统会将从语料库中检索到的上下文提供给 LLM，以协助回答查询。同样地，在编辑器模式下，你可以切换侧边栏来显示从语料库“检索”出的相关笔记。这是一种相当强大的方式来“增强”你的思考——通过将当前笔记中的想法与语料库中的相关想法进行交叉引用。

### Getting Started

1. 从 [reorproject.org](https://reorproject.org) 或 [发行版页面](https://github.com/reorproject/reor/releases) 下载。支持 Mac、Linux 和 Windows。
2. 像安装普通应用一样进行安装即可。

### Running local models

Reor 直接与 Ollama 交互，这意味着你可以直接在 Reor 内部下载并运行本地模型。前往“设置” -> “添加新的本地 LLM”，然后输入你希望 Reor 下载的模型名称。你可以在 [这里](https://ollama.com/library) 查看可用的模型列表。

你也可以[连接到兼容 OpenAI 的 API](https://www.reorproject.org/docs/documentation/openai-like-api)，例如 Oobabooga、Ollama 或 OpenAI 本身！

### Importing notes from other apps

Reor 在文件系统的单个目录内运行。首次启动时，你需要选择该目录。
要从其他应用导入笔记/文件，你需要手动在该目录中放入 Markdown 文件。请注意，如果你的 Markdown 文件中包含 `frontmatter`（元数据头），可能无法正确解析。与其他应用的集成功能预计很快就会推出！

### Building from source

请确保已安装 [nodejs](https://nodejs.org/en/download)。

#### Clone repo

```
git clone https://github.com/reorproject/reor.git
```

#### Install dependencies

```
npm install
```

#### Run for dev

```
npm run dev
```

#### Build

```
npm run build
```

### Interested in contributing?

我们一直在寻找渴望共同塑造知识管理未来的贡献者。有功能想法？想修复 Bug？想优化界面样式？欢迎随时告诉我们。请查看我们的 Issues 页面和[贡献指南](https://www.reorproject.org/docs/documentation/contributing)以开始参与。

## License

AGPL-3.0 许可证。详情请参阅 `LICENSE` 文件。

_Reor 在拉丁语中意为“思考”。_
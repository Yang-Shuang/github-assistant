> [!WARNING]  
> 该版本已超过一年未进行开发。我目前正在一个私有测试版中进行重写/重新发布——旨在收集反馈，同时避免通过发布不完整的软件来浪费大家的时间。如果你有兴趣加入，请随时联系我。

# LLocalSearch

## 项目简介与功能

LLocalSearch 是一个封装了本地运行的 `大型语言模型`（Large Language Models）的包装器，允许它从一组工具中进行选择。这些工具使其能够搜索互联网以获取关于你问题的最新信息。该过程是递归的，这意味着正在运行的 LLM 可以根据你提供的信息以及其他工具的调用结果，自由地决定使用哪些工具（甚至可以多次调用）。 

[demo.webm](https://github.com/nilsherzig/LLocalSearch/assets/72463901/e13e2531-05a8-40af-8551-965ed9d24eb4)

### 为什么要使用这个项目，而不是选择其他方案？

OpenAI 正通过 [销售](https://www.adweek.com/media/openai-preferred-publisher-program-deck/) 给大型媒体的长期计划如下：

> 此外，该项目的成员在聊天对话中会获得优先展示和“更丰富的品牌表达”，其内容也会受益于更显眼的链接处理。 

如果你反感自己的搜索结果可能被“价高者得”的逻辑所操纵，不妨试试这类更中立的替代方案，例如本项目。 

### 功能特性

- 🕵‍♀ 完全本地运行（无需 API Key），因此更注重隐私保护
- 💸 可在“低端”硬件上运行（演示视频使用的是价值约 300 欧元的显卡）
- 🤓 答案中提供实时日志和链接，帮助你更好地理解智能体正在执行的操作以及回答所依据的信息。这为你深入研究提供了绝佳的切入点。
- 🤔 支持追问/多轮对话
- 📱 移动端友好设计
- 🌓 深色与浅色模式切换


## 开发路线图

### 当前正在推进的工作 👷

#### LLaMA 3 支持 🦙

我使用的 `langchain` 库没有正确遵循 LLaMA3 的停止词（stop words），这导致模型在对话轮次结束时容易产生幻觉。我已经有一个可用的补丁（可检出 experiments 分支查看），但由于不确定我的解决方案是否是最优解，目前仍在等待 [langchaingo](https://github.com/tmc/langchaingo) 团队的回复。

#### 界面重构 🌟

全面重构用户界面，支持更灵活的面板布局并更高效地利用屏幕空间。 
设计灵感来源于 [Obsidian](https://obsidian.md) 当前的排版布局。

#### 聊天记录/近期对话支持 🕵‍♀

仍需大量工作，例如重构内部数据结构，以便在未来更灵活、更高效地扩展功能，而无需再次重写整个数据传输和界面部分。


### 近期规划

#### 用户账户系统 🙆

为 RAG（检索增强生成）链中的私有信息处理奠定基础，例如支持上传个人文档，或将 LLocalSearch 接入 Google Drive、Confluence 等服务。

#### 长期记忆功能 🧠

目前尚不确定是否有最佳实现方案，但计划为主智能体链提供用户相关信息（如偏好设置），并为每个用户分配独立的向量数据库命名空间（Vector DB Namespace）以存储持久化信息。

## 安装指南

### Docker 🐳

1. 克隆 GitHub 仓库

```bash
git@github.com:nilsherzig/LLocalSearch.git
cd LLocalSearch
```

2. 创建并编辑 `.env` 文件，如果你需要修改某些默认设置。通常仅当你将 Ollama 运行在其他设备上，或希望搭建更复杂的部署环境（例如供多人使用而非仅限个人）时才需要此步骤。如果无法顺利建立 Ollama 连接，请阅读 [Ollama Setup Guide](./Ollama_Guide.md)。

```bash
touch .env
code .env # open file with vscode
nvim .env # open file with neovim
```

3. 启动容器

```bash
docker-compose up -d
```
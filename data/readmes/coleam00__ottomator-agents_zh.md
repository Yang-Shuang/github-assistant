# 什么是 Live Agent Studio？

[Live Agent Studio](https://studio.ottomator.ai) 是由 [oTTomator](https://ottomator.ai) 开发的一个社区驱动型平台，旨在帮助你探索前沿的 AI Agent（智能体），并学习如何将其应用于个人或企业业务中！该平台上的所有 Agent 均为开源项目，随着时间的推移，将覆盖极其广泛的使用场景。

该工作室的目标是打造一个教育平台，让你学习如何利用 AI 实现令人惊叹的功能；同时提供实用的价值，让你仅仅因为 Agent 能为你带来的实际帮助而愿意使用它们！

该平台目前仍处于 Beta（测试）阶段——在负载较高时可能会出现响应延迟；未来几个月 Agent 库将快速增长；此外，Cole Medin 的 YouTube 频道也将很快上线大量关于本平台的新内容！

# 此仓库的用途是什么？

此仓库包含了 Live Agent Studio 平台上所有 Agent 的源代码和工作流 JSON！目前，所有新加入平台的 Agent 都会在此开源。这样我们不仅能作为社区共同打造一个精选的前沿 Agent 合集，还能互相学习！

## Tokens（平台积分）

在 Live Agent Studio 上，大多数 Agent 的使用需要消耗 Token。这些 Token 可在平台上购买。不过，当你首次登录时，系统会赠送一定数量的初始 Token，让你可以免费试用这些 Agent！Agent 需要消耗 Token 的最大原因是：由于我们托管了由你及社区其他成员开发的所有 Agent，因此我们需要承担 LLM（大语言模型）的调用费用！

[购买 Token](https://studio.ottomator.ai/pricing)

## 未来计划

随着 Live Agent Studio 的发展，它将成为了解 AI Agent 能力边界的首选平台！每当出现新的 AI 技术、突破性的 Agent 研究，或用于构建 Agent 的新工具/库时，平台都会通过相应的 Agent 进行展示。这是一个宏大的目标，但我们为 oTTomator 社区制定了宏伟计划，并且有信心能够逐步实现它！

## FAQ（常见问题）

### 我想开发一个 Agent 并在 Live Agent Studio 上展示！我该怎么做？

请访问此处学习如何为平台开发 Agent：

[Developer Guide](https://studio.ottomator.ai/guide)

此外，你可以参考 [the sample n8n agent](~sample-n8n-agent~) 作为开发 Live Agent Studio 的 n8n Agent 的起点，以及 [the sample Python agent](~sample-python-agent~) 用于 Python。

### 使用一个 Agent 需要消耗多少 Token？

每个 Agent 都会按提示词（Prompt）次数收费。具体消耗的 Token 数量取决于 Agent 本身，因为有些 Agent 使用更大的 LLM，有些会多次调用 LLM，还有些会使用付费 API。

### 我想讨论这些 Agent 并寻求自行实现的帮助，该去哪里？

欢迎前往我们的 Think Tank 社区，随时发帖交流！

[Think Tank Community](https://thinktank.ottomator.ai)

---

&copy; 2024 Live Agent Studio。保留所有权利。  
由 oTTomator 创建
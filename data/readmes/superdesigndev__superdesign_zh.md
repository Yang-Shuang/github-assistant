# 🧠 SuperDesign — 你的 IDE 专属 AI 设计 Agent

**🆕 新增：**[SuperDesign Chrome 扩展插件](https://chromewebstore.google.com/detail/obpjaonipoaomjnokbimppohbpjibflm) - 克隆任意网站与 UI

---

![SuperDesign Cover](cover.png)

### **作者：**[AI Jason](https://x.com/jasonzhou1993)

SuperDesign 是首款**开源设计 Agent**，直接运行在你的 IDE 中。  
通过自然语言提示词（Prompt），直接生成 UI 原型、组件和线框图。  
与 Cursor、Windsurf、Claude Code 以及原生版 VS Code 无缝协作。

> ✨ “既然能探索十种方案，何必只设计一种？” —— SuperDesign

[加入 Discord](https://discord.gg/FYr49d6cQ9)

[在 HackerNews 上投票支持](https://news.ycombinator.com/item?id=44376003)

[安装指南](https://www.superdesign.dev/ide-extension)

---

## 🎬 演示视频（点击播放）

[![SuperDesign Demo](https://img.youtube.com/vi/INv6oZDhhUM/maxresdefault.jpg)](https://youtu.be/INv6oZDhhUM)

---

## 🚀 核心功能

- 🖼️ **产品原型（Mock）**：通过单条提示词即时生成完整的 UI 界面
- 🧩 **UI 组件**：创建可复用组件，直接嵌入你的代码中
- 📝 **线框图（Wireframes）**：探索低保真布局，实现快速迭代
- 🔁 **分叉与迭代（Fork & Iterate）**：轻松复制并演进设计方案
- 📥 **提示词直达 IDE**：将提示词复制到你的首选 AI IDE 中（Cursor、Windsurf、Claude Code）

---

## 🧠 完美兼容 Cursor、Windsurf、Claude Code 与 VS Code

👉 [点击此处安装](https://www.superdesign.dev/ide-extension)

---

## 🛠️ 快速上手

1. **安装扩展插件**：从 Cursor/VS Code 应用市场获取
2. 打开左侧的 `SuperDesign` 侧边栏面板
3. 输入提示词（例如：_“设计一个现代风格的登录界面”_）
4. 查看生成的原型、组件和线框图
5. 分叉修改，调整后将代码粘贴到你的项目中

---

## 可以使用我自己的 Claude Code 或 Cursor 订阅吗？
可以。初始化 SuperDesign 扩展后，系统会自动添加部分 Cursor/Claude Code 规则。这样你就可以通过提示词让 Agent 执行设计任务，并在 SuperDesign Canvas（画布）中预览效果了。（快捷键：`cmd + shift + p` -> 输入 `superdesign: open canva`）

如果你使用的是 Cursor，强烈建议将 `design.mdc` 中的提示词复制出来，并在 Cursor 中基于该系统提示词创建一个自定义模式（Custom Mode）；这将显著提升生成效果。

操作指南视频（点击播放）： 
[![Instruction video](v0.0.11.png)](https://youtu.be/KChmJMCDOB0?si=pvU0kNRO4GRWjsec&t=122)

## 如何配置本地兼容 OpenAI 的服务器？
1. 在 AI 模型提供商 (Ai Model Provider) 中选择 OpenAI
2. 在 OpenAI API Key 输入框中输入任意内容（本地服务通常无需真实密钥）
3. 在 OpenAI URL 输入框中填入你的服务地址（例如 LM Studio：`http://127.0.0.1:1234/v1`）

## 📂 我的设计文件存储在哪里？

你生成的所有设计文件均本地保存在 `.superdesign/` 目录中。

---

## ❓ 常见问题（FAQ）

**它是免费开源的吗？**  
是的！我们完全开源——欢迎 Fork、二次开发或自由改编。

**我可以自定义设计 Agent 吗？**  
可以——支持使用你自己的提示词模板，修改行为逻辑或添加命令。

**SuperDesign 能更新现有 UI 吗？**  
完全可以——选中组件，描述你的修改需求，剩下的交给 Agent 处理即可。

<img width="886" height="586" alt="image" src="https://github.com/user-attachments/assets/71b7cfcc-6123-40ea-aae5-05ea6cdcea96" />


**如何参与贡献？**  
欢迎提交 Pull Request。给项目点个 Star，并加入我们的 [Discord](https://discord.gg/FYr49d6cQ9)！

---

## 🔗 相关链接

- 🌐 官网：[https://superdesign.dev/ide-extension](https://superdesign.dev/ide-extension)
- 📦 GitHub 仓库：[https://github.com/superdesigndev/superdesign](https://github.com/superdesigndev/superdesign)
- 💬 Discord：[加入社区](https://discord.gg/FYr49d6cQ9)
- 🐦 Twitter / X：[@SuperDesignDev](https://x.com/SuperDesignDev)
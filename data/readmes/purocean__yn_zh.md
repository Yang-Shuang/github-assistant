# Yank Note

一款**高度可扩展**的 Markdown 编辑器，专为提升效率而设计。 **[下载](https://github.com/purocean/yn/releases)** | **[在线体验 >>>](https://demo.yank-note.com/)**

[![Download](./help/mas_en.svg?.inline)](https://apps.apple.com/cn/app/yank-note/id1551528618) [不推荐](https://github.com/purocean/yn/issues/65#issuecomment-1065799677)

英文文档 | [中文说明](./README_ZH-CN.md) | [Русский](./README_RU.md)

[toc]{level: [2]}

![Screenshot](./help/1.png)

## 核心亮点

- **AI 助手：**支持 AI Copilot 进行文本补全、内容生成及图像创作（兼容 OpenAI、Ollama、Gemini、Kimi、通义千问、Flux.1 等）；支持 OpenCode AI Agent 提供智能编码辅助。
- **易于使用：**采用 Monaco 编辑器内核，针对 Markdown 编辑深度优化，带来与 VS Code 一致的流畅体验。
- **功能强大：**支持版本控制；文档中可嵌入小部件（Applets）、可运行代码块、表格、PlantUML、Draw.io、宏替换等功能。
- **高兼容性：**数据以本地 Markdown 文件形式保存，扩展功能尽可能通过 Markdown 原生语法实现。
- **插件扩展：**支持用户编写自定义插件，自由拓展编辑器能力边界。
- **支持加密：**可使用加密方式安全存储账号等隐私文件，且每个文件可独立设置密码。

## 注意事项

- **为了更高的可扩展性，Yank Note 牺牲了部分沙箱安全保护（如命令执行、任意文件读写）。如果你打算用它打开来源不明的 Markdown 文件，⚠️请务必仔细甄别文件内容是否可信⚠️。**
- 加密文件的加解密均在客户端（前端）完成。请**务必牢记你的密码**，一旦丢失，仅能通过暴力破解尝试恢复。

## 特色功能

有关以下功能的详细使用说明，请参阅 [特色功能说明](./help/FEATURES.md)

- **同步滚动：**编辑区与预览区联动滚动，且支持独立控制预览区滚动位置
- **大纲导航：**通过预览区中的目录树快速跳转到文档对应章节
- **版本控制：**支持回溯并恢复文档的历史版本
- **文件加密：**以 `.c.md` 结尾的文件将被自动识别为加密文件
- **自动保存：**编辑后自动保存文件，未保存状态会在标题栏显示橙色提示（加密文档默认不启用自动保存）
- **列表补全：**输入列表符号后按回车，自动延续列表格式
- **粘贴图片：**可快速从剪贴板粘贴图片，并选择以本地文件或 Base64 编码形式插入
- **嵌入附件：**可向文档添加附件，点击即可在操作系统中直接打开
- **代码运行：**支持内联运行 JavaScript、PHP、Node.js、Python、Bash 等代码片段
- **待办事项：**支持在文档中可视化展示任务进度，点击即可快速切换完成状态
- **快速打开：**可通过快捷键呼出文件面板，快速切换文件、标签页或进行全文内容搜索
- **集成终端：**支持在编辑器内直接唤起终端，并快速同步当前工作目录
- **数学公式：**完整支持 LaTeX 表达式渲染
- **样式主题：**Markdown 默认采用 GitHub 风格及特性解析
- **多存储位置：**可定义多个数据仓库（Repository）用于文档分类管理
- **外链转换：**自动将外部链接或 Base64 图片转换为本地引用路径
- **HTML 解析：**文档中可直接编写 HTML 代码，或通过快捷键复制粘贴 HTML 并自动转为 Markdown 语法
- **多格式导出：**后端集成 pandoc 作为核心转换引擎
- **目录生成（TOC）：**输入 `[toc]{type:** "ol", level:** [1,2,3]}` 可在指定位置自动生成多级目录
- **表格编辑：**双击任意单元格即可快速进入行内编辑模式
- **标题链接复制：**一键将标题锚点路径复制到剪贴板，方便插入到其他文件中
- **嵌入小部件（Applets）：**文档支持直接内嵌 HTML Applets
- **嵌入 PlantUML 图表：**文档原生支持渲染 PlantUML 图形
- **嵌入 Draw.io 图表：**文档原生支持渲染 Draw.io 图形
- **嵌入 ECharts 图表：**文档原生支持渲染 Echarts 数据可视化图表
- **嵌入 Mermaid 图表：**文档原生支持渲染 Mermaid 流程图/时序图等
- **嵌入 Luckysheet 表格：**文档原生支持渲染 Luckysheet 在线表格组件
- **思维导图：**嵌套列表可自动渲染为思维导图形式展示
- **元素属性自定义：**支持为任意 DOM 元素设置自定义属性（Attribute）
- **表格增强：**支持多行文本表头、单元格内嵌列表等高级排版特性
- **文档链接：**支持在文档内部引用其他文件，并实现双向锚点跳转
- **脚注：**支持编写标准 Markdown 格式脚注
- **自定义容器：**支持类似 VuePress 默认主题的语法容器（如 `tip`、`warning` 等）
- **宏替换：**支持嵌入 JavaScript 表达式，动态计算并替换文档内容
- **图床服务：**支持集成 [PicGo](https://picgo.github.io/PicGo-Doc/) 图片托管服务
- **自定义插件：**支持编写 JavaScript 插件以拓展编辑器功能。插件文件需放置于 `用户主目录/plugins` 目录下。详细开发指南请参阅 [插件开发文档](./help/PLUGIN.md)

## 截图展示

![Screenshot](./help/6.png)
![Screenshot](./help/7.png)
![Screenshot](./help/2.png)
![Screenshot](./help/3.png)
![Screenshot](./help/4.png)
![Screenshot](./help/5.png)

## 更新日志

### [v3.90.0](https://github.com/purocean/yn/releases/tag/v3.90.0) 2026-05-16

[Windows](https://github.com/purocean/yn/releases/download/v3.90.0/Yank-Note-win-x64-3.90.0.exe) | [macOS arm64](https://github.com/purocean/yn/releases/download/v3.90.0/Yank-Note-mac-arm64-3.90.0.dmg) | [macOS x64](https://github.com/purocean/yn/releases/download/v3.90.0/Yank-Note-mac-x64-3.90.0.dmg) | [Linux AppImage](https://github.com/purocean/yn/releases/download/v3.90.0/Yank-Note-linux-x86_64-3.90.0.AppImage) | [Linux deb](https://github.com/purocean/yn/releases/download/v3.90.0/Yank-Note-linux-amd64-3.90.0.deb)

1. **新增：** MCP 配置检查工具，支持读取配置文件 Schema、获取当前配置值，以及通过特定键名或分组直接打开设置面板
2. **新增：** 粘贴图片文件名模板功能，支持时间戳与哈希占位符
3. **优化：** 新增中日友好（CJK）Markdown 渲染选项，优化中文/日文的强调符号解析体验
4. **编辑器：** 点击预览区行内容时聚焦浮动编辑器窗口，失焦后自动关闭

[查看更多发布说明](https://github.com/purocean/yn/releases)

## 支持我们 / 加入社区

微信交流群

<img src="./help/qrcode-wechat.jpg?.inline" width="150">
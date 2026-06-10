## Android 技能

**Android 技能（Android skills）**是一套专为 AI 优化的模块化指令与资源库，旨在帮助大语言模型（LLM）更好地理解并执行符合 [developer.android.com](https://developer.android.com) 上 Android 开发最佳实践和指导原则的特定模式。

Android 技能遵循 [开放标准 Agent 技能规范（agent skills）](https://agentskills.io/home)，即提供任务技术规范的 Markdown 文件（SKILL.md），通过提供专业领域和工作流相关的背景信息，为 **LLM** 提供扎实的知识基础（grounding）。

我们的 Android 技能开发主要聚焦于**评估显示 LLM 表现不佳的用例和工作流**。我们不会优先处理 LLM 已经熟练掌握的成熟领域，例如基础的 Jetpack Compose 最佳实践。

欲了解更多详情，请参阅官方文档：

- [Android 技能](https://developer.android.com/tools/agents/android-skills)
- [Android CLI](https://developer.android.com/tools/agents/android-cli)
- [Android Studio](https://developer.android.com/studio/gemini/skills)

### 安装 Android 技能

使用 Android CLI 将特定技能安装到当前目录：

```
android skills add --skill=r8-analyzer --project=.
```

使用 Android CLI 将所有 Android 技能安装到所有已检测到的 Agent 对应的目录中：

```
android skills add --all
```

如果你没有现有的 Agent 目录，且未指定特定 Agent，则技能将安装到 `Gemini` 和 `Antigravity` 对应的路径：`~/.gemini/antigravity/skills`。

**参数选项：**

- `--all` - 安装所有 Android 技能。若省略该参数（且未指定 `--skill`），则仅会安装 `android-cli` 技能。
- `--agent` - 以逗号分隔的 Agent 列表，用于指定技能安装的对应对象。若省略该参数，则将为所有已检测到的 Agent 安装技能。
- `--skill` - 你想要安装的特定技能名称。若省略该参数（且未指定 `--all`），则仅会安装 `android-cli` 技能。
- `--project` - 用于安装技能的工程根目录路径。

## 免责声明

AI 可能会产生错误，请务必仔细核对输出结果。

## 贡献指南

请提交 GitHub Issue 以提供反馈、报告问题，或提出新增技能的需求与修改建议。

目前暂不接受外部公开贡献。

## 许可证

Android Skills 采用 [Apache License 2.0](LICENSE.txt) 许可协议。详细信息请参阅 `LICENSE.txt` 文件。

## 查阅社区行为准则

本项目遵循 [Google 开源项目社区行为准则](https://opensource.google/conduct/)。
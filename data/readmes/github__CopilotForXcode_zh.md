# <img align="center" height="70" src="./Docs/Images/AppIcon.png"/> GitHub Copilot for Xcode

[GitHub Copilot](https://github.com/features/copilot) 是面向 Swift、Objective-C 以及 iOS/macOS 开发的领先 AI 编程助手。它提供智能代码补全（Completions）、聊天对话（Chat）与代码审查（Code Review），并内置 Agent Mode、Next Edit Suggestions、MCP Registry 和 Copilot Vision 等高级功能，让你的 Xcode 开发更高效、更智能。

> [!IMPORTANT]  
> 从 v0.50.0 版本开始，我们已内部支持即将推出的基于用量的计费体验，包括用量面板、用量通知和模型选择器的界面更新。这些更改将在基于用量的计费功能正式推出后显示。 
> 
> 为确保与新计费体验兼容，我们强烈建议你尽快升级至最新插件版本： 
> 
> * **GitHub Copilot for Xcode: v0.50.0 或更高版本**
> 
> 使用旧版插件的客户端仍可继续运行。但计费与用量体验可能不够理想，且无法准确反映最新的基于用量的计费情况。 

## Chat

通过 GitHub Copilot Chat，你可以就具体的编码任务获取 AI 建议。
<img alt="Chat of GitHub Copilot for Xcode" src="./Docs/Images/chat_agent.gif" width="800" />

## Agent Mode

GitHub Copilot Agent Mode 提供由 AI 驱动的帮助，能够直接理解并修改你的代码库。使用 Agent Mode，你可以：
- 获取智能的代码编辑建议，并直接应用到文件中
- 在界面内运行终端命令并查看输出结果
- 搜索整个代码库以查找相关文件与代码片段
- 根据项目需要创建新文件和目录
- 在多文件和多文件夹间获得具备更强上下文感知能力的辅助
- 运行你配置的模型上下文协议（Model Context Protocol, MCP）工具以扩展功能

Agent Mode 与 Xcode 环境深度集成，打造无缝的开发体验。Copilot 能够全面理解你的项目，从而协助你实现功能、修复 Bug 以及重构代码。

## Code Completion

你可以通过开始编写代码，或编写描述代码功能的自然语言注释，来获取 GitHub Copilot 的自动补全建议。
<img alt="Code Completion of GitHub Copilot for Xcode" src="./Docs/Images/demo.gif" width="800" />

## Requirements

- macOS 13+
- Xcode 14+
- GitHub 账号

## Getting Started

1. 通过 [Homebrew](https://brew.sh/) 安装：

   ```sh
   brew install --cask github-copilot-for-xcode
   ```

   或从[最新版本发布页](https://github.com/github/CopilotForXcode/releases/latest/download/GitHubCopilotForXcode.dmg)下载 `.dmg` 安装包。将 `GitHub Copilot for Xcode` 拖入“应用程序”文件夹：

   <p align="center">
     <img alt="Screenshot of opened dmg" src="./Docs/Images/dmg-open.png" width="512" />
   </p>

   应用内支持直接下载并安装更新。

2. 打开“GitHub Copilot for Xcode”应用程序（从“应用程序”文件夹中）。接受安全警告提示。
   <p align="center">
     <img alt="Screenshot of MacOS download permission request" src="./Docs/Images/macos-download-open-confirm.png" width="350" />
   </p>

3. 系统会自动添加一个后台项目，以允许 GitHub Copilot for Xcode 扩展应用连接至宿主应用。首次启动时通常会自动授予此权限。
   <p align="center">
     <img alt="Screenshot of background item" src="./Docs/Images/background-item.png" width="370" />
   </p>

4. GitHub Copilot for Xcode 正常运行需要三项权限：`Background`、`Accessibility`（辅助功能）和 `Xcode Source Editor Extension`。如需了解这些权限的必要性，请参阅 [TROUBLESHOOTING.md](./TROUBLESHOOTING.md)。

   首次运行应用时，会请求 `Accessibility` 权限：

   <p align="center">
     <img alt="Screenshot of accessibility permission request" src="./Docs/Images/accessibility-permission-request.png" width="529" />
   </p>

   需手动启用 `Xcode Source Editor Extension` 权限。在“GitHub Copilot for Xcode”应用的设置中点击 `Extension Permission`（扩展权限），以打开系统偏好设置的 `Extensions` 面板。选择 `Xcode Source Editor` 并启用 `GitHub Copilot`：

   <p align="center">
     <img alt="Screenshot of extension permission" src="./Docs/Images/extension-permission.png" width="582" />
   </p>

5. 授予扩展权限后，打开 Xcode。检查 Xcode “Editor”（编辑）菜单下是否已出现并启用 `Github Copilot` 菜单项。
    <br>
    <p align="center">
      <img alt="Screenshot of Xcode Editor GitHub Copilot menu item" src="./Docs/Images/xcode-menu.png" width="648" />
    </p>

    你可以在 Xcode 偏好设置的“Key Bindings”（快捷键绑定）部分为所有菜单项设置键盘快捷键。

6. 要登录 GitHub Copilot，请在设置应用中点击 `Sign in`（登录）按钮。这将打开浏览器窗口并将代码复制到剪贴板。将代码粘贴至 GitHub 登录页面并授权该应用。
    <p align="center">
      <img alt="Screenshot of sign-in popup" src="./Docs/Images/device-code.png" width="372" />
    </p>

7. 要安装更新，请点击菜单项或设置应用中的 `Check for Updates`（检查更新）。

   安装新版本后，必须重启 Xcode 才能正常使用该版本。

   你也可以从发布页下载的 `.dmg` 文件中手动安装新版本。通过 `.dmg` 安装新版本的初次运行时，需手动运行一次以接受“来自互联网的应用”安全警告。

8. 为避免功能冲突或提示混乱，建议前往 `Xcode` > `Preferences`（偏好设置）> `Text Editing`（文本编辑）> `Editing`（编辑），关闭“Predictive code completion”（预测性代码补全）。

9. 按 `Tab` 键接受建议的第一行，按住 `Option` 键查看完整建议，并按 `Option` + `Tab` 组合键接受完整建议。

## How to use Chat

   在 GitHub Copilot 中打开 Copilot Chat。
  - 通过 Xcode 菜单路径：`Xcode` > `Editor`（编辑）> `GitHub Copilot` > `Open Chat`（打开聊天）。
  <p align="center">
    <img alt="Screenshot of Xcode Editor GitHub Copilot menu item" src="./Docs/Images/xcode-menu_dark.png" width="648" />
  </p>

  - 通过 GitHub Copilot 应用菜单：点击 `Open Chat`。

  <p align="center">
    <img alt="Screenshot of GitHub Copilot menu item" src="./Docs/Images/copilot-menu_dark.png" width="244" />
  </p>

## How to use Code Completion

   按 `Tab` 键接受建议的第一行，按住 `Option` 键查看完整建议，并按 `Option` + `Tab` 组合键接受完整建议。

## License

本项目遵循 MIT 开源许可证条款。完整条款请参阅 [LICENSE.txt](./LICENSE.txt)。

## Privacy

我们遵循负责任的做法，并严格遵守我们的[隐私声明](https://docs.github.com/en/site-policy/privacy-policies/github-privacy-statement)。

为获取最新的安全修复，请使用 GitHub Copilot for Xcode 的最新版本。

## Support

我们非常欢迎你的帮助，共同改进 GitHub Copilot！如有反馈或遇到问题，请前往我们的[反馈论坛](https://github.com/github/CopilotForXcode/discussions)与我们联系。

## Acknowledgements

感谢 @intitni 创建了本项目所基于的原始项目。

运行应用后在“关于”页面，或查看 [Credits.rtf](./Copilot%20for%20Xcode/Credits.rtf) 文件即可获取完整的归属声明。
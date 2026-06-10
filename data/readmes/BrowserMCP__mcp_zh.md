<a href="https://browsermcp.io">
  <img src="./.github/images/banner.png" alt="Browser MCP banner">
</a>

<h3 align="center">Browser MCP</h3>

<p align="center">
  使用 AI 自动化你的浏览器。
  <br />
  <a href="https://browsermcp.io"><strong>官网</strong></a> 
  •
  <a href="https://docs.browsermcp.io"><strong>文档</strong></a>
</p>

## 简介

Browser MCP 是一个 MCP Server + Chrome 扩展，让你能够使用 VS Code、Claude、Cursor 和 Windsurf 等 AI 应用来自动化操作浏览器。

## 核心特性

- ⚡ **快速**：自动化过程在本地机器上运行，无需网络延迟，性能更优。
- 🔒 **隐私安全**：由于自动化在本地完成，你的浏览器活动仅保留在本设备上，不会发送至远程服务器。
- 👤 **已登录状态**：使用你现有的浏览器配置文件（Profile），保持所有服务的登录状态。
- 🥷🏼 **防检测/隐蔽性**：通过使用真实的浏览器指纹，绕过基础的机器人检测和验证码（CAPTCHA）。

## 参与贡献

该仓库包含了 Browser MCP 的核心 MCP 代码。但由于其依赖于开发单体仓库（monorepo）中的 utils 和 types，目前无法单独构建运行。

## 致谢

Browser MCP 改编自 [Playwright MCP server](https://github.com/microsoft/playwright-mcp)，旨在自动化用户浏览器而非创建新的浏览器实例。这使得我们可以利用用户的现有浏览器配置文件来使用已登录的会话，并避免常见的自动化工具检测机制。
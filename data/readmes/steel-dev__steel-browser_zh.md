<br />
<p align="center">
<a href="https://steel.dev">
  <img src="images/steel_header_logo.png" alt="Steel Logo" width="100">
</a>
</p>



<h3 align="center"><b>Steel</b></h3>
<p align="center">
    <b>面向 AI 智能体与应用的开源浏览器 API。</b> <br />
    构建实时 Web 智能体和浏览器自动化工具的最佳方式。
</p>

<div align="center">

[![Commit Activity](https://img.shields.io/github/commit-activity/m/steel-dev/steel-browser?color=yellow)](https://github.com/steel-dev/steel-browser/commits/main)
[![License](https://img.shields.io/github/license/steel-dev/steel-browser?color=yellow)](https://github.com/steel-dev/steel-browser/blob/main/LICENSE)
[![Discord](https://img.shields.io/discord/1285696350117167226?label=discord)](https://discord.gg/steel-dev)
[![Twitter Follow](https://img.shields.io/twitter/follow/steeldotdev)](https://twitter.com/steeldotdev)
[![GitHub stars](https://img.shields.io/github/stars/steel-dev/steel-browser)](https://github.com/steel-dev/steel-browser)

</div>

<h4 align="center">
    <a href="https://app.steel.dev/sign-up" target="_blank">
      快速开始
  </a>  ·
    <a href="https://docs.steel.dev/" target="_blank">
      文档
  </a>  ·
  <a href="https://steel.dev/" target="_blank">
      官网
  </a> ·
  <a href="https://github.com/steel-dev/steel-cookbook" target="_blank">
      示例集
  </a>
</h4>

<p align="center">
  <img src="images/demo.gif" alt="Steel Demo" width="600">
</p>

## ✨ 核心特性

[Steel.dev](https://steel.dev) 是一个开源浏览器 API，让你能够轻松构建与 Web 交互的 AI 应用和智能体。你无需从零搭建自动化基础设施，只需专注于你的 AI 应用，复杂性交由 Steel 处理。

底层方面，它管理会话（Session）、页面和浏览器进程，让你能够以编程方式执行复杂的浏览任务，而无需担心各种麻烦：
- **完整的浏览器控制**：基于 Puppeteer 和 CDP（Chrome DevTools Protocol），完全掌控 Chrome 实例——支持通过 Puppeteer、Playwright 或 Selenium 连接。
- **会话管理**：跨请求保持浏览器状态、Cookie 和本地存储数据
- **代理支持**：内置代理链管理，实现 IP 轮换
- **扩展支持**：加载自定义 Chrome 扩展以增强功能
- **调试工具**：内置请求日志记录及用于查看/调试会话的 UI
- **反检测机制**：集成隐身插件与指纹管理
- **资源管理**：自动清理与浏览器生命周期管理
- **浏览器工具**：提供 API 快速将页面转换为 Markdown、可读文本、截图或 PDF。

有关详细的 API 文档和示例，请查阅我们的 [API 参考手册](https://docs.steel.dev/api-reference)，或直接访问 `http://0.0.0.0:3000/documentation` 查看 Swagger UI。

> Steel 目前处于公测阶段，并每天都在迭代更新。你的建议、想法和反馈的 Bug 对我们帮助极大。欢迎随时在 [Discord](https://discord.gg/steel-dev) 参与讨论或提交 GitHub Issue。我们会阅读所有内容，回复大部分问题，并且非常感谢你。

如果你热爱开源、AI 和开发者工具，[我们正在全栈招聘](https://jobs.ashbyhq.com/steel)!

### 别忘了给我们点个 Star ⭐

<img width="200" alt="在 GitHub 上关注我们！" src="images/star_img.png">

## 🛠️ 快速开始
使用 Steel 最简单的方式是注册一个 [Steel Cloud](https://app.steel.dev) 账号。否则，你也可以将此 Steel 浏览器实例部署到云服务提供商或本地运行。

## ⚡ 快速部署
如果你打算将服务部署到云平台，我们已为你准备好方案。

| 部署方式 | 链接 |
| -------------------- | ----- |
| 预构建 Docker 镜像（API + UI 整合版） | [![Deploy with Github Container Registry](https://img.shields.io/badge/GHCR-478CFF?style=for-the-badge&labelColor=478CFF&logo=github&logoColor=white)](https://github.com/steel-dev/steel-browser/pkgs/container/steel-browser) |
| Railway 一键部署 | [![Deploy on Railway](https://img.shields.io/badge/Railway-B039CB?style=for-the-badge&labelColor=B039CB&logo=railway&logoColor=white)](https://railway.app/deploy/steelbrowser) |
| Render 一键部署 | [![Deploy to Render](https://render.com/images/deploy-to-render-button.svg)](https://render.com/deploy) |


## 💻 本地运行

### Docker

在本地部署/运行 Steel 浏览器实例的最简单方法是使用预构建的 Docker 镜像：

```bash
# 拉取并运行 Docker 镜像
docker run -p 3000:3000 -p 9223:9223 ghcr.io/steel-dev/steel-browser
```

这将在端口 3000（http://localhost:3000）启动 Steel 浏览器服务器，并在 http://localhost:3000/ui 提供 UI。端口 9223 用于控制台调试器。

你现在可以创建会话、抓取页面、截图等。请跳转到 [使用指南](#usage) 部分查看快速操作示例。

或者，你也可以通过 docker compose 分别运行 API 和 UI：

```bash
docker compose up
```

对于 Apple Silicon（Mac 芯片）用户，你需要向 Docker Compose 命令传递此环境变量标志，以便在正确的平台上运行镜像：
```bash
DOCKER_DEFAULT_PLATFORM=linux/arm64 docker compose up
```

## 贡献者快速入门
在本地开发时，你需要运行 [`docker-compose.dev.yml`](./docker-compose.dev.yml) 文件而非默认的 [`docker-compose.yml`](./docker-compose.yml)，以便使你的本地更改生效。这将构建来自 [`api`](./api) 和 [`ui`](./ui) 目录的 Docker 镜像，并分别在端口 3000 和 5173 上运行服务器和 UI。

```bash
docker compose -f docker-compose.dev.yml up
```

你还需要加上 `--build` 参数，以确保每次修改代码后都能重新构建 Docker 镜像：

```bash
docker compose -f docker-compose.dev.yml up --build
```

如果你在自定义主机上运行，请创建 `.env` 文件（变量说明见 `docs/DEVELOPMENT_SETUP.md`），或修改 `docker-compose.dev.yml` 中使用的环境变量以匹配你的主机地址。

### Node.js
或者，如果你已安装 Node.js 和 Chrome，也可以直接运行服务器和 UI：

```bash
npm install
npm run dev
```

这将在端口 3000 启动 Steel 服务器，并在端口 5173 提供 UI。

请确保已安装 Chrome 可执行文件（Executable），并位于以下路径之一：

- **Linux**：
  `/usr/bin/google-chrome`

- **MacOS**：
  `/Applications/Google Chrome.app/Contents/MacOS/Google Chrome`

- **Windows**：
  - `C:\Program Files\Google\Chrome\Application\chrome.exe` 或
  - `C:\Program Files (x86)\Google\Chrome\Application\chrome.exe`

#### 自定义 Chrome 可执行文件路径

如果你有自定义的 Chrome 可执行文件或位于不同路径，可以将环境变量 `CHROME_EXECUTABLE_PATH` 设置为你的 Chrome 可执行文件路径：

```bash
export CHROME_EXECUTABLE_PATH=/path/to/your/chrome
npm run dev
```

有关此检查机制的更多详情，请查看 [`api/src/utils/browser.ts`](./api/src/utils/browser.ts)。

## 🏄🏽‍♂️ 使用指南
> 如果你需要关于如何使用 Steel 的快速示例，请查阅 [Cookbook（示例集）](https://github.com/steel-dev/steel-cookbook)。
>
> 或者你也可以尝试运行 REPL 包：执行 `cd repl` 和 `npm run start`

与 Steel 浏览器 API 交互主要有两种方式：
1. [使用会话](#sessions)
2. [使用快速操作接口](#quick-actions-api)

以下示例中，我们假设你的自定义 Steel API 端点（Endpoint）为 `http://localhost:3000`。

完整的 REST OpenAPI 文档可在我们的[官网](https://docs.steel.dev/api-reference)以及本地 Steel 实例的 `http://localhost:3000/documentation` 处查看。

#### 使用 SDK
如果你更倾向于使用我们的 Python 和 Node.js SDK，可以安装对应的 `steel-sdk` 包。

这些 SDK 基于 REST API 构建，提供了更便捷的与 Steel 浏览器 API 交互的方式。它们具备完整的类型定义（Typed），并且兼容 Steel Cloud 和自托管的 Steel 实例（Node.js 使用 `baseURL` 选项配置，Python 使用 `base_url` 配置）。

有关安装和使用 SDK 的更多详情，请参阅 [Node SDK 参考文档](https://github.com/steel-dev/steel-node/blob/main/api.md) 和 [Python SDK 参考文档](https://github.com/steel-dev/steel-python/blob/main/api.md)。


### 会话管理
`/sessions` 接口允许你使用自定义选项或扩展（例如自定义代理）重新启动浏览器，并重置浏览器状态。非常适合需要精细控制的复杂、有状态工作流。

获取会话后，你可以使用会话 ID 或根 URL 与浏览器进行交互。为此，你需要使用 Puppeteer 或 Playwright。你可以在下方的文档中找到一些将 Puppeteer 和 Playwright 与 Steel 配合使用的示例：
* [与 Puppeteer 集成](https://docs.steel.dev/overview/guides/puppeteer)
* [Node.js + Playwright](https://docs.steel.dev/overview/guides/playwright-node)
* [Python + Playwright](https://docs.steel.dev/overview/guides/playwright-python)

<details open>
<summary><b>使用 Node SDK 创建会话</b></summary>
<br>

```typescript
import Steel from 'steel-sdk';

const client = new Steel({
  baseURL: "http://localhost:3000", // Custom API Base URL override
});

(async () => {
  try {
    // Create a new browser session with current API fields
    const session = await client.sessions.create({
      blockAds: true,
      proxyUrl: "user:pass@host:port", // optional
      dimensions: { width: 1280, height: 800 }, // optional
    });
    console.log("Created session with ID:", session.id);
  } catch (error) {
    console.error("Error creating session:", error);
  }
})();
````
</details>

<details>
<summary><b>使用 Python SDK 创建会话</b></summary>
<br>

````python
import os
from steel import Steel

client = Steel(
    base_url="http://localhost:3000",  # Custom API Base URL override
)

try:
    # Create a new browser session with custom options
    session = client.sessions.create(
        block_ads=True,
        proxy_url="user:pass@host:port",  # optional
        dimensions={"width": 1280, "height": 800},  # optional
    )
    print("Created session with ID:", session.id)
except Exception as e:
    print("Error creating session:", e)
````
</details>

<details>
<summary><b>使用 Curl 创建会话</b></summary>
<br>

```bash
# Launch a new browser session
curl -X POST http://localhost:3000/v1/sessions \
  -H "Content-Type: application/json" \
  -d '{
    "proxyUrl": "user:pass@host:port",
    "blockAds": true,
    "dimensions": { "width": 1280, "height": 800 }
  }'
```
</details>


#### Selenium 会话
>**注意：** 此集成不支持基于 CDP 的浏览器会话 API 的所有功能。

对于已有 Selenium 工作流的团队，Steel 浏览器提供了一个即插即用的替代方案，在保持兼容性的同时增加了增强功能。你只需使用 `isSelenium` 选项即可创建 Selenium 会话：

```typescript
// Using the Node SDK
const session = await client.sessions.create({ isSelenium: true });
```
```python
# Using the Python SDK
session = client.sessions.create(is_selenium=True)
```
<details>
<summary><b>使用 Curl</b></summary>
<br>

```bash
# Launch a Selenium session
curl -X POST http://localhost:3000/v1/sessions \
  -H "Content-Type: application/json" \
  -d '{
    "isSelenium": true
  }'
```
</details>
<br>

Selenium API 完全兼容 Selenium 的 WebDriver 协议，因此你可以使用任何现有的 Selenium 客户端连接到 Steel 浏览器。**有关将 Selenium 与 Steel 配合使用的更多详情，请参阅 [Selenium 文档](https://docs.steel.dev/overview/guides/selenium)。**

### 快速操作接口
`/scrape`、`/screenshot` 和 `/pdf` 端点允许你利用正在运行的 Steel 服务器，从任意网页快速提取干净且格式良好的数据。非常适合简单的、只读的按需任务：

<details open>
<summary><b>抓取网页</b></summary>
<br>

提取网页的 HTML 内容。

```bash
# Example using the Actions API
curl -X POST http://0.0.0.0:3000/v1/scrape \
  -H "Content-Type: application/json" \
  -d '{
    "url": "https://example.com",
    "delay": 1000
  }'
```
</details>

<details>
<summary><b>截取网页截图</b></summary>
<br>

对网页进行截图。
```bash
# Example using the Actions API
curl -X POST http://0.0.0.0:3000/v1/screenshot \
  -H "Content-Type: application/json" \
  -d '{
    "url": "https://example.com",
    "fullPage": true
  }' --output screenshot.png
```
</details>

<details>
<summary><b>下载网页 PDF</b></summary>
<br>

将网页保存为 PDF 文件。
```bash
# Example using the Actions API
curl -X POST http://0.0.0.0:3000/v1/pdf \
  -H "Content-Type: application/json" \
  -d '{
    "url": "https://example.com"
  }' --output output.pdf
```
</details>

## 参与贡献
Steel 浏览器是一个开源项目，我们欢迎所有贡献！
- **疑问/想法/反馈？** 欢迎在 [Discord](https://discord.gg/steel-dev) 交流讨论
- **发现 Bug？** 请在 [GitHub](https://github.com/steel-dev/steel-browser/issues) 提交 Issue

## 许可证
[Apache 2.0](./LICENSE)

---

由 Steel 团队用 ❤️ 制作。
<h1 align="center">
    <a href="https://crawlee.dev">
        <picture>
          <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/apify/crawlee-python/master/website/static/img/crawlee-dark.svg?sanitize=true">
          <img alt="Crawlee" src="https://raw.githubusercontent.com/apify/crawlee-python/master/website/static/img/crawlee-light.svg?sanitize=true" width="500">
        </picture>
    </a>
    <br>
    <small>网页抓取与浏览器自动化库</small>
</h1>

<p align=center>
  <a href="https://trendshift.io/repositories/11169" target="_blank"><img src="https://trendshift.io/api/badge/repositories/11169" alt="apify%2Fcrawlee-python | Trendshift" style="width: 250px; height: 55px;" width="250" height="55"/></a>
</p>

<p align="center">
  <a href="https://badge.fury.io/py/crawlee" rel="nofollow"><img src="https://badge.fury.io/py/crawlee.svg" alt="PyPI package version"></a>
  <a href="https://pypi.org/project/crawlee/" rel="nofollow"><img src="https://img.shields.io/pypi/dm/crawlee" alt="PyPI package downloads"></a>
  <a href="https://codecov.io/gh/apify/crawlee-python"><img src="https://codecov.io/gh/apify/crawlee-python/graph/badge.svg?token=cCju61iPQG" alt="Codecov report"></a>
  <a href="https://pypi.org/project/crawlee/" rel="nofollow"><img src="https://img.shields.io/pypi/pyversions/crawlee" alt="PyPI Python version"></a>
  <a href="https://discord.gg/jyEM2PRvMU" rel="nofollow"><img src="https://img.shields.io/discord/801163717915574323?label=discord" alt="Chat on Discord"></a>
</p>

Crawlee 覆盖了端到端的爬取与抓取工作流，**助你快速构建可靠的爬虫。**

即使使用默认配置，你的爬虫也会表现得非常接近人类行为，从而轻松绕过现代反爬机制。Crawlee 提供了在网页中抓取链接、提取数据并以机器可读格式持久化存储的工具，你无需担心底层技术细节。此外，得益于丰富的配置选项，如果默认设置无法满足需求，你可以调整 Crawlee 的几乎任何方面以适应项目需要。

> 👉 **[在 Crawlee 项目官网查看完整文档、指南和示例](https://crawlee.dev/python/)** 👈

我们还提供了基于 TypeScript 的 Crawlee 实现，供你在项目中探索和使用。访问我们的 GitHub 仓库获取更多信息：[GitHub 上的 Crawlee (JS/TS)](https://github.com/apify/crawlee)。

## 安装

更多信息请参阅 Crawlee 文档中的[入门教程](https://crawlee.dev/python/docs/introduction)。

Crawlee 在 PyPI 上以 [`crawlee`](https://pypi.org/project/crawlee/) 包的形式提供。该包包含核心功能，额外功能则以可选依赖（extras）的形式提供，以保持依赖项和包体积最小化。

要安装包含所有功能的 Crawlee，请运行以下命令：

```sh
python -m pip install 'crawlee[all]'
```

然后，安装 [Playwright](https://playwright.dev/) 依赖项：

```sh
playwright install
```

验证 Crawlee 是否已成功安装：

```sh
python -c 'import crawlee; print(crawlee.__version__)'
```

详细安装说明请参阅[环境配置](https://crawlee.dev/python/docs/introduction/setting-up)文档页面。

### 使用 Crawlee CLI

使用 Crawlee CLI 并选择一个预设模板是上手 Crawlee 最快的方式。首先，确保你已经安装了 [uv](https://pypi.org/project/uv/)：

```sh
uv --help
```

如果未安装 [uv](https://pypi.org/project/uv/)，请按照官方[安装指南](https://docs.astral.sh/uv/getting-started/installation/)进行操作。

然后，运行 CLI 并从可用模板中选择：

```sh
uvx 'crawlee[cli]' create my-crawler
```

如果你已经安装了 `crawlee`，可以通过运行以下命令启动它：

```sh
crawlee create my-crawler
```

## 示例

以下是一些实用示例，帮助你快速上手 Crawlee 中的不同类型爬虫。每个示例都演示了如何为特定用例设置和运行爬虫，无论你是需要处理简单的 HTML 页面还是与重度依赖 JavaScript 的站点交互。运行爬虫会在当前工作目录下创建一个 `storage/` 目录。

### BeautifulSoupCrawler

[`BeautifulSoupCrawler`](https://crawlee.dev/python/api/class/BeautifulSoupCrawler) 使用 HTTP 库下载网页，并向用户提供解析后的 HTML 内容。默认情况下，它使用 [`HttpxHttpClient`](https://crawlee.dev/python/api/class/HttpxHttpClient) 进行 HTTP 通信，并使用 [BeautifulSoup](https://pypi.org/project/beautifulsoup4/) 解析 HTML。它非常适合需要从 HTML 内容中高效提取数据的项目。由于不依赖浏览器，该爬虫性能极佳。然而，如果你需要执行客户端 JavaScript 来获取内容，仅靠它是无法实现的，此时你需要使用 [`PlaywrightCrawler`](https://crawlee.dev/python/api/class/PlaywrightCrawler)。此外，若要使用此爬虫，请确保安装 `crawlee` 时包含 `beautifulsoup` 可选依赖。

```python
import asyncio

from crawlee.crawlers import BeautifulSoupCrawler, BeautifulSoupCrawlingContext


async def main() -> None:
    crawler = BeautifulSoupCrawler(
        # Limit the crawl to max requests. Remove or increase it for crawling all links.
        max_requests_per_crawl=10,
    )

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: BeautifulSoupCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Extract data from the page.
        data = {
            'url': context.request.url,
            'title': context.soup.title.string if context.soup.title else None,
        }

        # Push the extracted data to the default dataset.
        await context.push_data(data)

        # Enqueue all links found on the page.
        await context.enqueue_links()

    # Run the crawler with the initial list of URLs.
    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

### PlaywrightCrawler

[`PlaywrightCrawler`](https://crawlee.dev/python/api/class/PlaywrightCrawler) 使用无头浏览器下载网页，并提供用于数据提取的 API。它基于 [Playwright](https://playwright.dev/) 构建，这是一个专为管理无头浏览器而设计的自动化库。它在获取依赖客户端 JavaScript 生成内容的网页，或需要与 JS 驱动内容交互的任务方面表现出色。如果场景不需要执行 JavaScript 或对性能有更高要求，建议考虑使用 [`BeautifulSoupCrawler`](https://crawlee.dev/python/api/class/BeautifulSoupCrawler)。此外，若要使用此爬虫，请确保安装 `crawlee` 时包含 `playwright` 可选依赖。

```python
import asyncio

from crawlee.crawlers import PlaywrightCrawler, PlaywrightCrawlingContext


async def main() -> None:
    crawler = PlaywrightCrawler(
        # Limit the crawl to max requests. Remove or increase it for crawling all links.
        max_requests_per_crawl=10,
    )

    # Define the default request handler, which will be called for every request.
    @crawler.router.default_handler
    async def request_handler(context: PlaywrightCrawlingContext) -> None:
        context.log.info(f'Processing {context.request.url} ...')

        # Extract data from the page.
        data = {
            'url': context.request.url,
            'title': await context.page.title(),
        }

        # Push the extracted data to the default dataset.
        await context.push_data(data)

        # Enqueue all links found on the page.
        await context.enqueue_links()

    # Run the crawler with the initial list of requests.
    await crawler.run(['https://crawlee.dev'])


if __name__ == '__main__':
    asyncio.run(main())
```

### 更多示例

浏览 Crawlee 文档中的[示例](https://crawlee.dev/python/docs/examples)页面，探索更广泛的其他用例和演示。

## 功能特性

为什么 Crawlee 是网页抓取与爬取的首选？

### 为什么不直接使用普通的 HTTP 库配合 HTML 解析器，而要使用 Crawlee？

- 提供统一的接口支持 **HTTP 与无头浏览器** 爬取。
- 基于可用系统资源自动进行**并行爬取**。
- 使用 Python 编写并包含完整的**类型提示（Type Hints）**——提升开发者体验（DX，如 IDE 自动补全）并减少错误（静态类型检查）。
- 遇到错误或被封禁时自动进行**重试**。
- 集成**代理轮换**与会话管理。
- 可配置的**请求路由**——将 URL 定向到相应的处理程序。
- 持久化的待爬取 **URL 队列**。
- 支持插件化的**存储**机制，兼容表格数据与文件。
- 健壮的**错误处理**机制。

### 为什么选择 Crawlee 而不是 Scrapy？

- **基于 Asyncio**——利用标准的 [Asyncio](https://docs.python.org/3/library/asyncio.html) 库，Crawlee 提供更优的性能，并能与其他现代异步库无缝兼容。
- **类型提示（Type Hints）**——作为基于现代 Python 构建的新项目，提供完整的类型提示覆盖，带来更好的开发者体验。
- **集成简单**——Crawlee 爬虫是标准的 Python 脚本，无需额外的启动执行器。这种灵活性允许你将爬虫直接集成到其他应用程序中。
- **状态持久化**——支持中断期间的状态保存，避免因问题导致需要从头重启抓取流水线，从而节省时间和成本。
- **结构化的数据存储**——允许在单次抓取运行中保存多种类型的结果。提供多种存储选项（参见[数据集](https://crawlee.dev/python/api/class/Dataset)与[键值存储](https://crawlee.dev/python/api/class/KeyValueStore)）。

## 在 Apify 平台上运行

Crawlee 是开源的，可在任何地方运行。但由于它由 [Apify](https://apify.com) 开发，因此在 Apify 平台上部署并云端运行也非常方便。访问 [Apify SDK 官网](https://docs.apify.com/sdk/python/) 了解将 Crawlee 部署到 Apify 平台的更多信息。

## 支持

如果你在 Crawlee 中发现任何 Bug 或问题，请在 GitHub 上[提交 Issue](https://github.com/apify/crawlee-python/issues)。如有疑问，你可以在 [Stack Overflow](https://stackoverflow.com/questions/tagged/apify) 提问、在 GitHub Discussions 中讨论，或加入我们的 [Discord 服务器](https://discord.com/invite/jyEM2PRvMU)。

## 贡献代码

我们非常欢迎你的代码贡献，并将永远铭记你的付出！如果你有改进建议，请提交 Issue 或创建 Pull Request。关于贡献指南和行为规范，请参阅[CONTRIBUTING.md](https://github.com/apify/crawlee-python/blob/master/CONTRIBUTING.md)。

## 许可证

本项目采用 Apache License 2.0 许可协议——详见[LICENSE](https://github.com/apify/crawlee-python/blob/master/LICENSE)文件。
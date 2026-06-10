<div align="center">

# bb-browser

### BadBoy Browser

**你的浏览器即 API。无需密钥，无需机器人，无需爬虫。**

[![npm](https://img.shields.io/npm/v/bb-browser?color=CB3837&logo=npm&logoColor=white)](https://www.npmjs.com/package/bb-browser)
[![Node.js](https://img.shields.io/badge/Node.js-18+-339933?logo=node.js&logoColor=white)](https://nodejs.org)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

[English](README.md) · [中文](README.zh-CN.md)

</div>

---

你已经在 Twitter、Reddit、YouTube、知乎、Bilibili、LinkedIn、GitHub 等平台登录了——bb-browser 让 AI Agent **直接使用这些状态**。

```bash
bb-browser site twitter/search "AI agent"       # search tweets
bb-browser site zhihu/hot                        # trending on Zhihu
bb-browser site arxiv/search "transformer"       # search papers
bb-browser site eastmoney/stock "茅台"            # real-time stock quote
bb-browser site boss/search "AI engineer"        # search jobs
bb-browser site wikipedia/summary "Python"       # Wikipedia summary
bb-browser site youtube/transcript VIDEO_ID      # full transcript
bb-browser site stackoverflow/search "async"     # search SO questions
```

**涵盖 36 个平台，103 条命令。** 全部复用你真实浏览器的登录态。[完整列表 →](https://github.com/epiral/bb-sites)

## 核心思路

互联网是为浏览器而生的。AI Agent 一直在尝试通过 API（应用程序编程接口）访问它——但 99% 的网站并不提供 API。

bb-browser 颠覆了这一逻辑：**与其强迫网站提供机器接口，不如让机器直接使用人类界面。** 适配器会在你的浏览器标签页内执行 `eval`，使用你的 Cookie 调用 `fetch()`，或调用页面自身的 webpack 模块。网站会认为操作者是你。因为**它确实就是你**。

| | Playwright / Selenium | 爬虫库 (Scraping libs) | bb-browser |
|---|---|---|---|
| 浏览器 | 无头，隔离环境 | 无需浏览器 | 你真实的 Chrome |
| 登录态 | 无，需重新登录 | Cookie 提取 | 已自动保持 |
| 反爬检测 | 容易被识别 | 猫鼠游戏 | 隐形——它就是用户本人 |
| 复杂鉴权 | 难以模拟 | 逆向工程 | 页面自身处理即可 |

## 快速上手

### 安装

```bash
npm install -g bb-browser
```

### 使用

```bash
bb-browser site update        # pull community adapters
bb-browser site recommend     # see which adapters match your browsing habits
bb-browser site zhihu/hot     # go
```

### OpenClaw（无需扩展）

如果你使用 [OpenClaw](https://openclaw.ai)，bb-browser 可直接通过 OpenClaw 内置的浏览器运行——无需 Chrome 扩展或守护进程：

```bash
bb-browser site reddit/hot --openclaw
bb-browser site xueqiu/hot-stock 5 --openclaw --jq '.items[] | {name, changePercent}'
```

ClawHub 技能页: [bb-browser-openclaw](https://clawhub.ai/yan5xu/bb-browser)

### MCP（Claude Code / Cursor）

```json
{
  "mcpServers": {
    "bb-browser": {
      "command": "npx",
      "args": ["-y", "bb-browser", "--mcp"]
    }
  }
}
```

## 36 个平台，103 条命令

由社区驱动，通过 [bb-sites](https://github.com/epiral/bb-sites) 维护。每条命令对应一个 JS 文件。

| 分类 | 平台 | 命令 |
|----------|-----------|----------|
| **搜索** | Google、百度、Bing、DuckDuckGo、搜狗微信 | search |
| **社交** | Twitter/X、Reddit、微博、小红书、即刻 (Jike)、LinkedIn、虎扑 (Hupu) | search, feed, thread, user, notifications, hot |
| **资讯** | BBC、Reuters、36kr、Toutiao、东方财富 (Eastmoney) | headlines, search, newsflash, hot |
| **开发** | GitHub、StackOverflow、HackerNews、CSDN、cnblogs、V2EX、Dev.to、npm、PyPI、arXiv | search, issues, repo, top, thread, package |
| **视频** | YouTube、Bilibili | search, video, transcript, popular, comments, feed |
| **娱乐/影视** | Douban、IMDb、Genius、Qidian | movie, search, top250 |
| **财经** | Xueqiu、东方财富 (Eastmoney)、Yahoo Finance | stock, hot stocks, feed, watchlist, search |
| **求职** | BOSS Zhipin、LinkedIn | search, detail, profile |
| **知识库** | Wikipedia、Zhihu、Open Library | search, summary, hot, question |
| **购物/优惠** | SMZDM | search deals |
| **工具** | Youdao、GSMArena、Product Hunt、Ctrip | translate, phone specs, trending products |

## 10 分钟接入任意网站

```bash
bb-browser guide    # full tutorial
```

告诉你的 AI Agent：“把 XX 网站变成 CLI”。它会阅读指南，通过 `network --with-body` 逆向工程 API，编写适配器，测试并提 PR。全程自主完成。

适配器的复杂度分为三个等级：

| 级别 | 鉴权方式 | 示例 | 耗时 |
|------|-------------|---------|------|
| **1** | Cookie（直接 fetch） | Reddit、GitHub、V2EX | ~1 分钟 |
| **2** | Bearer Token + CSRF Token | Twitter、Zhihu | ~3 分钟 |
| **3** | Webpack 注入 / Pinia Store | Twitter 搜索、小红书 | ~10 分钟 |

我们进行了测试：**20 个 AI Agent 并行运行，各自独立逆向一个网站并生成可用的适配器。** 将新网站接入 Agent 可访问互联网的边际成本正趋近于零。

## 对 AI Agent 的意义

没有 bb-browser，AI Agent 的世界是：**文件 + 终端 + 少数带密钥的 API。**

有了 bb-browser：**文件 + 终端 + 整个互联网。**

Agent 现在可以在一分钟内完成：

```bash
# Cross-platform research on any topic
bb-browser site arxiv/search "retrieval augmented generation"
bb-browser site twitter/search "RAG"
bb-browser site github search rag-framework
bb-browser site stackoverflow/search "RAG implementation"
bb-browser site zhihu/search "RAG"
bb-browser site 36kr/newsflash
```

六个平台，六个维度，结构化 JSON。比任何人类研究员更快、更广。

## 同时也是一套完整的浏览器自动化工具

```bash
bb-browser open https://example.com
bb-browser snapshot -i                # accessibility tree
bb-browser click @3                   # click element
bb-browser fill @5 "hello"            # fill input
bb-browser eval "document.title"      # run JS
bb-browser fetch URL --json           # authenticated fetch
bb-browser network requests --with-body --json  # capture traffic
bb-browser screenshot                 # take screenshot
```

所有命令均支持 `--json` 输出、通过 `--jq <expr>` 进行内联过滤，以及使用 `--tab <id>` 实现并发多标签页操作。

```bash
bb-browser site xueqiu/hot-stock 5 --jq '.items[] | {name, changePercent}'
# {"name":"云天化","changePercent":"2.08%"}
# {"name":"东芯股份","changePercent":"-7.60%"}

bb-browser site info xueqiu/stock   # view adapter args, example, domain
```

## 守护进程配置

守护进程默认绑定到 `127.0.0.1:19824`。你可以通过 `--host` 自定义主机地址：

```bash
bb-browser daemon --host 127.0.0.1    # IPv4 only (fix macOS IPv6 issues)
bb-browser daemon --host 0.0.0.0      # listen on all interfaces (for Tailscale / ZeroTier remote access)
```

## 架构设计

```
AI Agent (Claude Code、Codex、Cursor 等)
       │ CLI 或 MCP (stdio)
       ▼
bb-browser CLI ──HTTP──▶ Daemon ──CDP WebSocket──▶ 你真实的浏览器
                           │
                    ┌──────┴──────┐
                    │ 每个标签页   │
                    │ 事件缓存     │
                    │ (网络请求、  │
                    │ 控制台日志、 │
                    │ 错误信息)    │
                    └─────────────┘
```

## 许可证

[MIT](LICENSE)
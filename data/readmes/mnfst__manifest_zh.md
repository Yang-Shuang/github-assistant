<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/mnfst/manifest/HEAD/.github/assets/logo-white.svg" />
    <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/mnfst/manifest/HEAD/.github/assets/logo-dark.svg" />
    <img src="https://raw.githubusercontent.com/mnfst/manifest/HEAD/.github/assets/logo-dark.svg" alt="Manifest" height="53" title="Manifest"/>
  </picture>
</p>
<p align="center">
降低你的 AI 成本 
</p>

![manifest-gh](https://github.com/user-attachments/assets/7dd74fc2-f7d6-4558-a95a-014ed754a125)

<p align="center">
  <span><img src="https://img.shields.io/badge/status-beta-yellow" alt="beta" /></span>
  &nbsp;
  <a href="https://github.com/mnfst/manifest/stargazers"><img src="https://img.shields.io/github/stars/mnfst/manifest?style=flat" alt="GitHub stars" /></a>
  &nbsp;
  <a href="https://hub.docker.com/r/manifestdotbuild/manifest"><img src="https://img.shields.io/docker/pulls/manifestdotbuild/manifest?color=2496ED&label=docker%20pulls" alt="Docker pulls" /></a>
  &nbsp;
  <a href="https://hub.docker.com/r/manifestdotbuild/manifest/tags"><img src="https://img.shields.io/docker/image-size/manifestdotbuild/manifest/latest?color=2496ED&label=image%20size" alt="Docker image size" /></a>
  &nbsp;
  <a href="https://github.com/mnfst/manifest/actions/workflows/ci.yml"><img src="https://img.shields.io/github/actions/workflow/status/mnfst/manifest/ci.yml?branch=main&label=CI" alt="CI status" /></a>
  &nbsp;
  <a href="https://app.codecov.io/gh/mnfst/manifest"><img src="https://img.shields.io/codecov/c/github/mnfst/manifest?label=coverage" alt="Codecov" /></a>
  &nbsp;
  <a href="LICENSE"><img src="https://img.shields.io/github/license/mnfst/manifest?color=blue" alt="license" /></a>
  &nbsp;
  <a href="https://discord.gg/FepAked3W7"><img src="https://img.shields.io/badge/Discord-Join-5865F2?logo=discord&logoColor=white" alt="Discord" /></a>
</p>

<p align="center">
<a href="https://trendshift.io/repositories/12890" target="_blank"><img src="https://trendshift.io/api/badge/repositories/12890" alt="mnfst%2Fmanifest | Trendshift" style="width: 250px; height: 55px;" width="250" height="55"/></a>
</p>

## Manifest 是什么？

Manifest 是一款面向智能体（Agents）和 AI 应用的智能模型路由器，可将每次查询自动路由至最合适的模型，最高节省 70% 的 AI 成本。

- 🔀 基于复杂度、具体性及自定义 HTTP 头进行路由
- 🎛️ 混合使用你的提供商：API 密钥、订阅服务、本地模型及自定义提供商
- 📊 追踪每一笔支出，设置通知与额度限制
- 🚑 查询失败时自动回退至其他模型

## 快速上手

### 云端版

访问 [app.manifest.build](https://app.manifest.build) 并按照引导操作。

### 自托管版本

Manifest 提供 [Docker 镜像](https://hub.docker.com/r/manifestdotbuild/manifest)。只需一条命令：

```bash
bash <(curl -sSL https://raw.githubusercontent.com/mnfst/manifest/main/docker/install.sh)
```

打开 [http://localhost:2099](http://localhost:2099) 并注册 —— 你创建的第一个账户将成为管理员。完整自托管指南：[docker/DOCKER_README.md](docker/DOCKER_README.md)。

> 旧的 `manifest` npm 包已弃用，且不再发布。

## 模型提供商

Manifest 已接入 **17 家提供商的 300+ 模型**，并支持任意自定义提供商（兼容 OpenAI/Anthropic 协议）。你可以自带 API 密钥、复用已有的付费订阅，或在本地运行模型 —— 所有请求均通过统一的 `/auto` 端点进行路由。

| 提供商 | API 密钥 | 订阅服务 | 精选模型 |
| --- | :---: | :--- | :--- |
| [**OpenAI**](https://platform.openai.com/) | ✅ | ✅ ChatGPT Plus / Pro / Team | gpt-5, gpt-5-mini, o4, o4-mini |
| [**Anthropic**](https://www.anthropic.com/) | ✅ | ✅ Claude Max / Pro | claude-opus-4-7, claude-sonnet-4-6, claude-haiku-4-5 |
| [**Google**](https://ai.google.dev/) | ✅ | — | gemini-2.5-pro, gemini-2.5-flash, gemini-2.0-flash |
| [**xAI**](https://x.ai/) | ✅ | — | grok-4, grok-3, grok-code-fast |
| [**DeepSeek**](https://www.deepseek.com/) | ✅ | — | deepseek-v3.2, deepseek-r1 |
| [**Mistral**](https://mistral.ai/) | ✅ | — | mistral-large, codestral, magistral |
| [**Qwen** (Alibaba Cloud)](https://www.alibabacloud.com/en/solutions/generative-ai/qwen) | ✅ | — | qwen3-max, qwen3-coder, qwq-32b |
| [**Moonshot** (Kimi)](https://kimi.ai/) | ✅ | ✅ Kimi Coding Plan | kimi-k2, kimi-for-coding, moonshot-v1-128k |
| [**MiniMax**](https://www.minimax.io/) | ✅ | ✅ MiniMax Coding Plan | minimax-m2, abab7-chat-preview |
| [**Z.ai** (Zhipu)](https://z.ai/) | ✅ | ✅ GLM Coding Plan | glm-4.6, glm-4.5-air |
| [**BytePlus**](https://www.byteplus.com/en/activity/codingplan) | — | ✅ ModelArk Coding Plan | ark-code-latest, bytedance-seed-code, deepseek-v4-flash |
| [**OpenCode**](https://opencode.ai/) | — | ✅ Go 订阅 | 通过 OpenCode Go 目录路由 |
| [**Ollama**](https://ollama.com/) | 🖥️ 本地 | ✅ Ollama Cloud | 任意 GGUF 模型，端口 `11434` |
| [**LM Studio**](https://lmstudio.ai/) | 🖥️ 本地 | — | 任意 GGUF 模型，端口 `1234` |
| [**llama.cpp**](https://github.com/ggml-org/llama.cpp) | 🖥️ 本地 | — | 任意 GGUF 模型，端口 `8080` |
| [**OpenRouter**](https://openrouter.ai/) | ✅ | — | 路由至各大实验室的 300+ 模型 |
| [**GitHub Copilot**](https://github.com/features/copilot) | — | ✅ Copilot 订阅 | OAuth 认证，无需 API 密钥 |
| **自定义**（兼容 OpenAI/Anthropic）| ✅ | — | 任意 `/v1/chat/completions` 或 `/v1/messages` 端点 |

## 快速链接

- [文档](https://manifest.build/docs)
- [Discord](https://discord.com/invite/FepAked3W7)
- [讨论区](https://github.com/mnfst/manifest/discussions)
- [贡献指南](CONTRIBUTING.md)
- [GitHub](https://github.com/mnfst/manifest)

## 许可证

[MIT](LICENSE)
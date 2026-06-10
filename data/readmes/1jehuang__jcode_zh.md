<div align="center">

# jcode

[![Latest Release](https://badgen.net/github/release/1jehuang/jcode?icon=github)](https://github.com/1jehuang/jcode/releases)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue?style=flat-square)](LICENSE)
[![Platforms](https://img.shields.io/badge/platforms-Linux%20%7C%20macOS%20%7C%20Windows-blue?style=flat-square)](https://github.com/1jehuang/jcode/releases)
[![Last Commit](https://badgen.net/github/last-commit/1jehuang/jcode/master?icon=github)](https://github.com/1jehuang/jcode/commits/master)
[![GitHub Stars](https://badgen.net/github/stars/1jehuang/jcode?icon=github)](https://github.com/1jehuang/jcode/stargazers)
[![Discord](https://img.shields.io/badge/Discord-Join%20Community-5865F2?style=flat-square&logo=discord&logoColor=white)](https://discord.gg/nBe9vGyK9a)

新一代编码智能体框架，助你突破技术天花板。<br>
专为多会话工作流、无限自定义与高性能打造。 

<br>

<a href="https://github.com/1jehuang/jcode/releases/download/readme-assets/jcode-memory-demo.mp4">
  <img src="https://github.com/1jehuang/jcode/releases/download/readme-assets/jcode-memory-demo.webp" alt="jcode memory demonstration" width="800">
</a>

<br>

[核心特性](#features) · [安装指南](#installation) · [快速上手](#quick-start) · [深入阅读](#further-reading) · [贡献指南](CONTRIBUTING.md)

</div>

---

<div align="center">

## 安装指南

</div>

```bash
# macOS & Linux
curl -fsSL https://raw.githubusercontent.com/1jehuang/jcode/master/scripts/install.sh | bash
```

需要 Windows 版、Homebrew 安装、源码编译、Provider 配置，或者想让智能体自动帮你完成设置？
[查看详细安装指南](#detailed-installation)。

---


<div align="center">

## 性能与资源效率

</div>

`jcode` 旨在实现极致的性能与资源效率。各项指标均经过深度优化，这对于扩展多会话工作流至关重要。以下选取部分核心指标进行对比：内存占用（RAM）与启动速度。

### 内存占用 (PSS) 对比

<div align="center">

<table>
  <tr>
    <td valign="top" align="center" width="50%">
      <strong>1 个活跃会话</strong>
      <table>
        <thead>
          <tr>
            <th>工具</th>
            <th>PSS</th>
            <th>对比</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td><strong>jcode (关闭本地嵌入)</strong></td>
            <td align="right"><strong>27.8 MB</strong></td>
            <td align="right">基准</td>
          </tr>
          <tr>
            <td><strong>jcode</strong></td>
            <td align="right"><strong>167.1 MB</strong></td>
            <td align="right"><strong>多 6.0× 内存</strong></td>
          </tr>
          <tr>
            <td><strong>pi</strong></td>
            <td align="right"><strong>144.4 MB</strong></td>
            <td align="right"><strong>多 5.2× 内存</strong></td>
          </tr>
          <tr>
            <td><strong>Codex CLI</strong></td>
            <td align="right"><strong>140.0 MB</strong></td>
            <td align="right"><strong>多 5.0× 内存</strong></td>
          </tr>
          <tr>
            <td><strong>OpenCode</strong></td>
            <td align="right"><strong>371.5 MB</strong></td>
            <td align="right"><strong>多 13.4× 内存</strong></td>
          </tr>
          <tr>
            <td><strong>GitHub Copilot CLI</strong></td>
            <td align="right"><strong>333.3 MB</strong></td>
            <td align="right"><strong>多 12.0× 内存</strong></td>
          </tr>
          <tr>
            <td><strong>Cursor Agent</strong></td>
            <td align="right"><strong>214.9 MB</strong></td>
            <td align="right"><strong>多 7.7× 内存</strong></td>
          </tr>
          <tr>
            <td><strong>Claude Code</strong></td>
            <td align="right"><strong>386.6 MB</strong></td>
            <td align="right"><strong>多 13.9× 内存</strong></td>
          </tr>
          <tr>
            <td><strong>Antigravity CLI</strong></td>
            <td align="right"><strong>243.7 MB</strong></td>
            <td align="right"><strong>多 8.8× 内存</strong></td>
          </tr>
        </tbody>
      </table>
    </td>
    <td width="24"></td>
    <td valign="top" align="center" width="50%">
      <strong>10 个活跃会话</strong>
      <table>
        <thead>
          <tr>
            <th>工具</th>
            <th>PSS</th>
            <th>对比</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td><strong>jcode (关闭本地嵌入)</strong></td>
            <td align="right"><strong>117.0 MB</strong></td>
            <td align="right">基准</td>
          </tr>
          <tr>
            <td><strong>jcode</strong></td>
            <td align="right"><strong>260.8 MB</strong></td>
            <td align="right"><strong>多 2.2× 内存</strong></td>
          </tr>
          <tr>
            <td><strong>pi</strong></td>
            <td align="right"><strong>833.0 MB</strong></td>
            <td align="right"><strong>多 7.1× 内存</strong></td>
          </tr>
          <tr>
            <td><strong>Codex CLI</strong></td>
            <td align="right"><strong>334.8 MB</strong></td>
            <td align="right"><strong>多 2.9× 内存</strong></td>
          </tr>
          <tr>
            <td><strong>OpenCode</strong></td>
            <td align="right"><strong>3237.2 MB</strong></td>
            <td align="right"><strong>多 27.7× 内存</strong></td>
          </tr>
          <tr>
            <td><strong>GitHub Copilot CLI</strong></td>
            <td align="right"><strong>1756.5 MB</strong></td>
            <td align="right"><strong>多 15.0× 内存</strong></td>
          </tr>
          <tr>
            <td><strong>Cursor Agent</strong></td>
            <td align="right"><strong>1632.4 MB</strong></td>
            <td align="right"><strong>多 14.0× 内存</strong></td>
          </tr>
          <tr>
            <td><strong>Claude Code</strong></td>
            <td align="right"><strong>2300.6 MB</strong></td>
            <td align="right"><strong>多 19.7× 内存</strong></td>
          </tr>
          <tr>
            <td><strong>Antigravity CLI</strong></td>
            <td align="right"><strong>1021.2 MB</strong></td>
            <td align="right"><strong>多 8.7× 内存</strong></td>
          </tr>
        </tbody>
      </table>
    </td>
  </tr>
</table>

</div>

### 首帧渲染时间 (Time to first frame)

<div align="center">

| 工具 | 首帧时间 | 波动范围 | 对比 |
|---|---:|---:|---|
| **jcode** | **14.0 ms** | 10.1–19.3 ms | 基准 |
| **Antigravity CLI** | **383.5 ms** | 363.1–415.4 ms | **慢 27.4×** |
| **pi** | **590.7 ms** | 369.6–934.8 ms | **慢 42.2×** |
| **Codex CLI** | **882.8 ms** | 742.3–1640.9 ms | **慢 63.1×** |
| **OpenCode** | **1035.9 ms** | 922.5–1104.4 ms | **慢 74.0×** |
| **GitHub Copilot CLI** | **1518.6 ms** | 1357.4–1826.8 ms | **慢 108.5×** |
| **Cursor Agent** | **1949.7 ms** | 1711.0–2104.8 ms | **慢 139.3×** |
| **Claude Code** | **3436.9 ms** | 2032.7–8927.2 ms | **慢 245.5×** |

</div>

测试环境：本 Linux 机器，共进行 10 次交互式 PTY 启动。

### 首输入响应时间 (Time to first input)
(键入探测文本后出现在渲染屏幕上的耗时；Antigravity 使用其内部就绪日志标记，因为其登录界面会抑制探测回显。)
<div align="center">

| 工具 | 首输入时间 | 波动范围 | 对比 |
|---|---:|---:|---|
| **jcode** | **48.7 ms** | 30.3–62.7 ms | 基准 |
| **Antigravity CLI** | **383.7 ms** | 363.4–415.7 ms | **慢 7.9×** |
| **pi** | **596.4 ms** | 373.9–955.2 ms | **慢 12.2×** |
| **Codex CLI** | **905.8 ms** | 760.1–1675.7 ms | **慢 18.6×** |
| **OpenCode** | **1047.9 ms** | 931.1–1116.9 ms | **慢 21.5×** |
| **GitHub Copilot CLI** | **1583.4 ms** | 1422.8–1880.0 ms | **慢 32.5×** |
| **Cursor Agent** | **1978.7 ms** | 1727.3–2130.0 ms | **慢 40.6×** |
| **Claude Code** | **3512.8 ms** | 2137.4–9002.0 ms | **慢 72.2×** |

</div>

测试环境：本 Linux 机器，共进行 10 次交互式 PTY 启动。本次运行中 Antigravity CLI 未认证；其登录界面正常渲染并输出了内部 `CLI ready for user input` 标记，但未回显键入的探测文本。

### 多客户端扩展与内存增长 (Additional clients / memory scaling)

<div align="center">

| 工具 | 每新增会话的额外 PSS | 对比 |
|---|---:|---|
| **jcode (关闭本地嵌入)** | **~9.9 MB** | 基准 |
| **jcode** | **~10.4 MB** | **多 1.1× 内存** |
| **pi** | **~76.5 MB** | **多 7.7× 内存** |
| **Codex CLI** | **~21.6 MB** | **多 2.2× 内存** |
| **OpenCode** | **~318.4 MB** | **多 32.2× 内存** |
| **GitHub Copilot CLI** | **~158.1 MB** | **多 16.0× 内存** |
| **Cursor Agent** | **~157.5 MB** | **多 15.9× 内存** |
| **Claude Code** | **~212.7 MB** | **多 21.5× 内存** |
| **Antigravity CLI** | **~86.4 MB** | **多 8.7× 内存** |

</div>
本次修正后的内存重测使用的版本：

- `jcode v0.9.1888-dev (be386f2)`
- `pi 0.62.0`
- `codex-cli 0.120.0`
- `opencode 1.0.203`
- `GitHub Copilot CLI 1.0.24`（1会话重测）/ `GitHub Copilot CLI 1.0.27`（10会话重测）
- `Cursor Agent 2026.04.08-a41fba1`
- `Claude Code 2.1.86 (Claude Code)`
- `Antigravity CLI 1.0.0`

<div align="center">

  <a href="https://github.com/1jehuang/jcode/releases/download/readme-assets/jcode-performance-demo.mp4">
    <img src="https://github.com/1jehuang/jcode/releases/download/readme-assets/jcode-performance-demo.webp" alt="jcode performance demonstration" width="900">
  </a>

  <p><em>jcode 性能演示</em></p>

</div>


---

## 记忆系统 (Agent memory)

`jcode` 将每一轮对话/响应嵌入为语义向量。每轮交互都会查询记忆图谱，通过余弦相似度计算高效检索相关记忆条目。这些匹配到的记忆会被注入到上下文中；或者可选地启用一个“记忆侧智能体”（memory sideagent）来验证记忆的相关性，并在注入前执行额外的信息检索工作。这构建了一个类人的记忆系统，使智能体能够自动召回与当前对话相关的信息，而无需主动调用记忆工具或浪费 Token。 
要成功检索记忆，还需将其提取并存储。每隔一段时间（如语义漂移、距上次提取已达 K 轮、会话结束等），记忆侧智能体会自动执行提取操作，并将结果存入记忆图谱中。 

该框架还提供了显式的记忆工具，允许智能体主动搜索或存储记忆，而不完全依赖后台被动进程。此外，还提供基于传统 RAG 的会话历史检索功能。 

通过环境模式（ambient mode），记忆会定期自动合并重组。系统会自动整理、检查过期数据及冲突等。

<div align="center">

  <a href="https://github.com/1jehuang/jcode/releases/download/readme-assets/jcode-memory-demo.mp4">
    <img src="https://github.com/1jehuang/jcode/releases/download/readme-assets/jcode-memory-demo.webp" alt="jcode memory demonstration" width="900">
  </a>

  <p><em>jcode 记忆演示</em></p>

</div>

<!-- Memory demo media is hosted in the readme-assets release. -->

---

## 用户界面：侧边栏、图表、信息组件、渲染与滚动

侧边栏用于展示辅助信息。你可以让智能体将文件加载到侧边栏并实时查看更新，或直接写入内容，或将其用作差异对比（diff）查看器。侧边栏和聊天窗口均支持内联渲染 Mermaid 图表。 
<img width="2877" height="1762" alt="image" src="https://github.com/user-attachments/assets/6c7bec81-ef3f-434d-8a7b-d55f8a54e5cf" />

为实现此功能，我开发了一个全新的 Mermaid 渲染库，渲染速度提升了 1800 倍。它不依赖浏览器或 TypeScript。详见：https://github.com/1jehuang/mermaid-rs-renderer

为了在不占用屏幕响应空间的前提下展示重要信息，我开发了“信息组件”（info widgets）。它们仅利用屏幕的负空间显示内容，若无可用空间则自动隐藏。 

`jcode` 渲染帧率可达每秒千帧以上。你的显示器刷新率可能无法完全体现这一点，但这意味着你将彻底告别画面闪烁问题。 

`jcode` 的自定义回滚（scrollback）实现支持比原生滚动更丰富的功能。但受限于终端底层，自定义回滚无法实现平滑的部分行滚动。为此我开发了专属终端 Handterm (https://github.com/1jehuang/handterm)，它实现了原生滚动 API 且性能极佳。该项目仍在持续优化中。对于普通终端，滚动功能也已完善支持。

`jcode` 默认左对齐。你可通过快捷键 `Alt+C`、命令 `/alignment` 或配置文件切换为居中对齐模式。

---

## 智能体集群 (Swarm)

在同一仓库中启动两个或更多智能体，服务器将自动管理它们以实现原生协作。当智能体 A 编辑了智能体 B 已读取的文件（即底层代码发生变化）时，服务器会通知智能体 B。智能体 B 可忽略无关变更，或通过检查差异确保无冲突。每个智能体均具备通信能力，支持单聊、向服务器托管的所有智能体广播，或仅与同仓库的智能体通信。这允许你在同一仓库中启动多个会话，并自动解决所有冲突。

<div align="center">

  <a href="https://github.com/1jehuang/jcode/releases/download/readme-assets/swarm-demo.mp4">
    <img src="https://github.com/1jehuang/jcode/releases/download/readme-assets/jcode-swarm-demonstration.webp" alt="jcode swarm demonstration" width="900">
  </a>

  <p><em>jcode 集群演示</em></p>

</div>

智能体还能自主创建子集群。通过“集群工具”（swarm tool），它们可并行召唤队友以完成任务。此时主智能体转为协调者，被调用的智能体转为执行者。智能体分组、通信频道及完成状态等均由系统自动管理。此功能支持无头模式与有界面模式。

---

## OAuth 认证与 Provider (服务提供商)

`jcode` 支持基于订阅的 OAuth 流程及多种 Provider 集成，让你能继续使用已付费的模型服务，并在需要时回退到直连 API。

### 支持的内置登录流程

- **Claude** (`jcode login --provider claude`)
- **OpenAI / ChatGPT / Codex** (`jcode login --provider openai`)
- **Google Gemini** (`jcode login --provider gemini`)
- **GitHub Copilot** (`jcode login --provider copilot`)
- **Azure OpenAI** (`jcode login --provider azure`)
- **Alibaba Cloud Coding Plan** (`jcode login --provider alibaba-coding-plan`)
- **Fireworks** (`jcode login --provider fireworks`)
- **MiniMax** (`jcode login --provider minimax`)
- **LM Studio** (`jcode login --provider lmstudio`)
- **Ollama** (`jcode login --provider ollama`)
- **自定义 OpenAI 兼容端点** (`jcode login --provider openai-compatible`)

对于自定义 OpenAI 兼容端点，`jcode` 现在会提示输入 API Base URL，并支持无需 API Key 的本地服务器。

### 配置文件设置（自托管端点与 MCP）

如果你偏好通过编辑文件而非登录界面进行配置，`jcode` 同时支持自定义 OpenAI 兼容端点配置和 MCP 配置文件。

#### OpenAI 兼容型 Provider

许多托管服务遵循标准的 OpenAI `/v1/chat/completions` API。`jcode` 通过统一的 OpenAI 兼容 Provider 与之通信，因此你几乎可以使用任何此类端点，无需等待专属集成。

有两种设置方式：

- **内置命名配置** — `jcode` 预置了多个流行 OpenAI 兼容服务的配置文件。通过 ID 登录即可，`jcode` 会自动为你填入 Base URL 和密钥环境变量：

  ```bash
  jcode login --provider <profile-id>
  # 例如：
  jcode login --provider openrouter
  jcode login --provider deepseek
  jcode login --provider opencode      # OpenCode Zen
  jcode login --provider moonshotai
  ```

  内置的 OpenAI 兼容 Profile ID 包括：`openrouter`, `deepseek`, `zai`, `kimi`, `moonshotai`, `opencode` (OpenCode Zen), `opencode-go`, `302ai`, `baseten`, `cortecs`, `huggingface`, `nebius`, `scaleway`, `stackit`, 以及 `firmware`。每个 Profile 仅设置端点和密钥变量；你仍需通过 `/model`（或 `--model`）选择模型。运行不带 Provider 参数的 `jcode login` 可查看交互式列表。

- **任意其他端点** — 使用 `jcode login --provider openai-compatible` 或下文描述的脚本化命令 `jcode provider add`，将 `jcode` 指向任意 OpenAI 兼容 API（托管或本地）。

这些端点的有用环境变量覆盖项：

- `JCODE_STREAM_IDLE_TIMEOUT_SECS` — 提高流式空闲超时时间（默认 180s），适用于在输出 Token 前会静默思考的慢速推理模型。也可在 `config.toml` 中设置为 `[provider] stream_idle_timeout_secs`。
- `[[providers.<name>.models]]` 条目中的每模型 `context_window`（别名 `context_limit`） — 当端点无法返回有效的 `/v1/models` 响应时，设置上下文窗口大小，避免 `jcode` 回退到通用的 200k 默认值。

关于自托管、本地运行时及配置文件具体结构的详情，请参阅下文。

#### 自托管 OpenAI 兼容端点（含 vLLM）

对于智能体和脚本，推荐使用一次性 Provider Profile 命令。它会将命名配置写入 `~/.jcode/config.toml`，在请求时将密钥安全存储于 `jcode` 的私有应用配置目录中，并打印精确的运行/验证命令：

```bash
# 托管 OpenAI 兼容 API 的安全设置
printf '%s' "$MY_API_KEY" | jcode provider add my-api \
  --base-url https://llm.example.com/v1 \
  --model my-model-id \
  --api-key-stdin \
  --set-default \
  --json

# 冒烟测试 Profile
jcode --provider-profile my-api auth-test --prompt 'Reply exactly JCODE_PROVIDER_SETUP_OK'

# 直接使用
jcode --provider-profile my-api run 'hello'
```

对于无需认证的本地服务器：

```bash
jcode provider add local-vllm \
  --base-url http://localhost:8000/v1 \
  --model Qwen/Qwen3-Coder-30B-A3B-Instruct \
  --no-api-key \
  --set-default
```

常用桌面/本地运行时已提供内置本地 Profile：

```bash
# Ollama：先启动本地服务器并安装模型。
ollama pull llama3.2
jcode login --provider ollama
jcode --provider ollama --model llama3.2 run 'hello'

# LM Studio：启动 Local Server，加载聊天模型，然后使用 LM Studio 或 curl http://localhost:1234/v1/models 显示的精确模型标识符。
jcode login --provider lmstudio
jcode --provider lmstudio --model '<model-id>' run 'hello'
```

Ollama 和 LM Studio 均暴露 OpenAI 兼容的 `/v1/models` 和 `/v1/chat/completions` 端点。`jcode` 使用流式聊天补全、函数/工具调用及 OpenAI 风格的图像内容以支持具备视觉能力的本地模型。若本地服务器需要 Token，请在 `jcode login` 时输入，或使用 `--api-key-stdin` 创建命名 Profile。

有用参数：

- `--api-key-env NAME`：引用现有环境变量而非存储密钥。
- `--api-key-stdin`：读取并存储密钥，避免泄露至 Shell 历史记录。
- `--context-window TOKENS`：持久化模型上下文窗口大小，用于模型选择与路由。
- `--overwrite`：覆盖同名现有 Profile。
- `--model-catalog`：除已配置的模型外，额外使用端点的 `/models` 响应。

生成的 Profile 也可在 `~/.jcode/config.toml` 中手动编辑：

```toml
[provider]
default_provider = "my-api"
default_model = "my-model-id"

[providers.my-api]
type = "openai-compatible"
base_url = "https://llm.example.com/v1"
api_key_env = "JCODE_PROVIDER_MY_API_API_KEY"
env_file = "provider-my-api.env"
default_model = "my-model-id"

[[providers.my-api.models]]
id = "my-model-id"
context_window = 128000
```

自定义 OpenAI 兼容 Provider 会从环境变量或 `jcode` 应用配置目录中的 env 文件读取覆盖项。在 Linux 上通常位于 `~/.config/jcode/`，因此默认文件通常为：

```text
~/.config/jcode/openai-compatible.env
```

本地或局域网 vLLM 服务器示例：

```bash
JCODE_OPENAI_COMPAT_API_BASE=http://192.168.1.50:8000/v1
JCODE_OPENAI_COMPAT_DEFAULT_MODEL=Qwen/Qwen3-Coder-30B-A3B-Instruct
# 若你的服务器需要认证则取消注释
OPENAI_COMPAT_API_KEY=your-token-here
```

注意事项：

- `jcode login --provider openai-compatible` 可自动创建或更新此文件。
- `http://` 协议接受用于 `localhost` 和私有局域网 IP。公共远程 HTTP 仍会被拒绝。
- HTTPS 端点按常规方式工作。

#### MCP 配置文件

MCP 配置独立于 `config.toml`。

主配置文件：

- `~/.jcode/mcp.json`（全局 MCP 服务器）
- `.jcode/mcp.json`（项目级 MCP 服务器）

兼容性回退机制：

- `.claude/mcp.json`

MCP 配置示例：

```json
{
  "servers": {
    "filesystem": {
      "command": "/path/to/mcp-server",
      "args": ["--root", "/workspace"],
      "env": {},
      "shared": true
    }
  }
}
```

首次运行时，若 `~/.jcode/mcp.json` 尚不存在，`jcode` 还会尝试从 `~/.claude/mcp.json` 和 `~/.codex/config.toml` 导入 MCP 服务器。

对于无头模式或 SSH 会话，OAuth 风格 Provider 支持 `jcode login --provider <provider> --no-browser`（别名：`--headless`），此时 `jcode` 会打印认证 URL/二维码并回退至手动输入代码或粘贴回调地址，而非尝试启动本地浏览器。

对于更多脚本化的远程流程，`claude`、`openai`、`gemini` 和 `antigravity` 也支持两步式模式：

```bash
# 步骤 1：打印可恢复的认证 URL
jcode login --provider openai --print-auth-url --json

# 步骤 2：后续使用回调地址或认证码完成
jcode login --provider openai --callback-url 'http://localhost:1455/auth/callback?...'
jcode login --provider gemini --auth-code '...'
```

其他脚本化场景：

```bash
# Copilot 设备流：打印 URL + 用户代码，后续完成认证
jcode login --provider copilot --print-auth-url --json
jcode login --provider copilot --complete

# 已配置凭据后的 Gmail/Google OAuth
jcode login --provider google --print-auth-url --google-access-tier readonly
jcode login --provider google --callback-url 'http://127.0.0.1:8456?...'
```

待处理的脚本化登录状态存储于 `~/.jcode/pending-login/`，会自动过期。当新的脚本化登录开始或恢复时，过期条目会被自动清理。

对于内置的 OpenAI 登录流程，`jcode` 默认在 `http://localhost:1455/auth/callback` 开启本地回调监听。

<img width="2877" height="1762" alt="Screenshot from 2026-04-02 14-28-51" src="https://github.com/user-attachments/assets/530684c0-9d12-4363-aa0e-1b39a0d4e1be" />
上图展示了 Provider 登录的第一页

### 支持的 Provider

- **原生 / 第一方风格 Provider：** `claude`, `openai`, `copilot`, `gemini`, `azure`, `alibaba-coding-plan`
- **聚合 / 兼容型 Provider：** `openrouter`, `openai-compatible`
- **其他集成支持：** `opencode`, `opencode-go`, `zai` / `kimi`, `302ai`, `baseten`, `cortecs`, `deepseek`, `firmware`, `huggingface`, `moonshotai`, `nebius`, `scaleway`, `stackit`, `groq`, `mistral`, `perplexity`, `togetherai`, `deepinfra`, `fireworks`, `minimax`, `xai`, `lmstudio`, `ollama`, `chutes`, `cerebras`, `cursor`, `antigravity`, `google`

`jcode` 还支持便捷的多账号切换。如果你的 ChatGPT Pro 订阅 Token 用完了？使用 `/account` 即可快速切换到第二个账号。 

---

## 自定义能力与自我开发 (Self-Dev)

`jcode` 正在开创一种全新的自定义范式。它不再将你的能力局限于插件或扩展所能实现的范畴。告诉智能体进入“自我开发模式”，它将开始修改自身的源代码。`jcode` 针对自我迭代进行了深度优化。围绕自我开发构建了完善的底层设施，允许其编辑、构建和测试自身源码，随后自动重载二进制文件并继续工作（支持你开启的多个会话），全程全自动完成。 

建议为此使用前沿模型。`jcode` 的代码库并不简单，较弱模型可能会做出细微但破坏性的更改。GPT-5.5 或当前最新的前沿模型效果最佳。

<!-- Add self-dev demo thumbnail/video and fuller writeup here. -->

---

## 其他特性 (Misc.)

细节决定成败。`jcode` 实现了许多未文档化的优化与贴心功能。部分示例如下： 

Anthropic 的 Claude 缓存会在 5 分钟后失效。若在此之后发起请求，将导致缓存未命中（cache miss），可能消耗大量 Token。UI 会在缓存冷却时发出警告，并在发生非预期缓存未命中时通知你。 

`jcode` 内置了如何配置 Firefox Agent Bridge 的指南。让智能体帮你设置后，即可在 `jcode` 中实现浏览器自动化。 

`agent grep` 是我专为 `jcode` 开发的搜索工具。它在返回结果中加入文件结构信息（如函数列表、偏移量等），使智能体无需读取完整文件即可推断其内容。此外，它还实现了框架级集成，可根据智能体已看到的内容自适应截断返回结果，大幅节省上下文空间。 

默认情况下，输入流会与当前工作智能体交错发送。它会在不破坏 KV 缓存的前提下尽快发送输入。若改用 Shift+Enter 提交，则会改为队列发送模式，等待智能体完全结束当前回合后再继续发送。

支持跨框架恢复会话。`Claude Code` 出问题了？你可以从 `jcode` 恢复该会话并接续之前的工作。目前支持 Codex、Claude Code、OpenCode 和 pi 的会话恢复功能。 

<img width="2877" height="1762" alt="Screenshot from 2026-04-11 16-28-52" src="https://github.com/user-attachments/assets/c2b383cf-2531-4217-85ae-6a863354dc97" />
`/Resume` for codex sessions 截图

技能并非全部在启动时加载。对话内容会被嵌入为语义向量，若检测到与记忆相似的匹配项，会自动注入相关技能。智能体提供“技能工具”供你随时手动激活技能，也可通过斜杠命令（slash commands）启用。 

---

## iOS 应用 / 原生 OpenClaw

`jcode` 的原生 iOS 版本即将推出。这将允许你通过 Tailscale 在手机端直接操作本地机器的环境。iOS 版将内置类似 OpenClaw 的功能特性。 

---

## 其他计划中的功能

智能体通常不喜欢在存在未提交更改的脏 Git 状态下进行提交。Git 显然并非为多智能体工作流设计，而 Git Worktrees 也不是理想的解决方案。因此，我认为这是一个孕育新型类 Git 原语的机会。 

构建速度优化：在我的机器上，启用缓存的增量调试 Cargo 构建约需 1 分钟。目标是缩短至 5~20 秒。通过重构和 Crate 拆分（crates seams）有望实现该目标。 

<!-- Add iOS / native OpenClaw preview and fuller writeup here. -->

---

<div align="center">

## 快速上手

</div>

```bash
# 启动 TUI
jcode

# 非交互式运行单条命令
jcode run "say hello"

# 通过记忆名称恢复之前的会话
jcode --resume fox

# 作为持久化后台服务器运行，随后附加更多客户端
jcode serve
jcode connect

# 从配置的 STT 命令发送语音输入
jcode dictate
```

`jcode` 支持交互式 TUI 使用、非交互模式运行、持久化服务端/客户端工作流，以及快捷键友好的语音输入功能，且无需捆绑内置的语音转文本（STT）组件。

<div align="center">

  <a href="https://github.com/1jehuang/jcode/releases/download/readme-assets/workflow.mp4">
    <img src="https://github.com/1jehuang/jcode/releases/download/readme-assets/jcode-workflow-demonstration.webp" alt="jcode workflow demonstration" width="900">
  </a>

  <p><em>jcode 工作流演示</em></p>

</div>

---

## 浏览器自动化

`jcode` 内置了首-class 的 `browser` 工具，用于在智能体会话中控制浏览器。

当前内置后端：
- Firefox（通过 Firefox Agent Bridge）

当前内置工具操作包括：
- `status`
- `setup`
- `open`
- `snapshot`
- `get_content`
- `interactables`
- `click`
- `type`
- `fill_form`
- `select`
- `wait`
- `screenshot`
- `eval`
- `scroll`
- `upload`
- `press`

快速设置：

```bash
jcode browser status
jcode browser setup
```

设置完成后，模型可直接使用内置的 `browser` 工具。UI 也会紧凑地总结浏览器工具调用（例如打开 URL、点击选择器或向字段输入文本），且不会回显敏感输入内容。

注意事项：
- Provider/工具架构已就位，支持后续添加更多后端
- Firefox 是目前唯一绑定的内置后端
- Chrome Bridge / 远程调试风格的 Provider 可在同一浏览器工具之上后续扩展

---

## 深入阅读

- [环境模式 / OpenClaw](docs/AMBIENT_MODE.md)
- [浏览器 Provider 协议](docs/BROWSER_PROVIDER_PROTOCOL.md)
- [记忆架构](docs/MEMORY_ARCHITECTURE.md)
- [集群架构](docs/SWARM_ARCHITECTURE.md)
- [服务端架构](docs/SERVER_ARCHITECTURE.md)
- [iOS 客户端说明](docs/IOS_CLIENT.md)
- [安全系统](docs/SAFETY_SYSTEM.md)
- [Windows 注意事项](docs/WINDOWS.md)
- [包装器与 Shell 集成](docs/WRAPPERS.md)
- [重构说明](docs/REFACTORING.md)

---

## 详细安装指南

### 设置

如果你想让另一个智能体帮你完成 `jcode` 的设置，请提供以下提示词：

```text
Set up jcode on this machine for me.

1. Detect the operating system, available package managers, and shell environment, then install jcode using the best matching command below instead of referring me somewhere else:

   - macOS with Homebrew available:
     brew tap 1jehuang/jcode
     brew install jcode

   - macOS or Linux via install script:
     curl -fsSL https://raw.githubusercontent.com/1jehuang/jcode/master/scripts/install.sh | bash

   - Windows PowerShell:
     irm https://raw.githubusercontent.com/1jehuang/jcode/master/scripts/install.ps1 | iex

   - From source if the above paths are not appropriate:
     git clone https://github.com/1jehuang/jcode.git
     cd jcode
     cargo build --release
     scripts/install_release.sh

   - For local self-dev / refactor work on Linux x86_64, prefer:
     scripts/dev_cargo.sh build --release -p jcode --bin jcode
     scripts/dev_cargo.sh --print-setup
     scripts/install_release.sh

2. Verify that `jcode` is on my `PATH`.
3. Launch `jcode` once in a new terminal window/session to confirm it starts successfully.
4. Before attempting any interactive login flow, assess which providers are already available non-interactively and prefer those first. Check existing local credentials, config files, CLI sessions, and environment variables such as:
   - Claude: `~/.jcode/auth.json`, `~/.claude/.credentials.json`, `~/.local/share/opencode/auth.json`, `ANTHROPIC_API_KEY`
   - OpenAI: `~/.jcode/openai-auth.json`, `~/.codex/auth.json`, `OPENAI_API_KEY`
   - Gemini: `~/.jcode/gemini_oauth.json`, `~/.gemini/oauth_creds.json`
   - GitHub Copilot: existing auth under `~/.config/github-copilot/`
   - Azure OpenAI: `~/.config/jcode/azure-openai.env`, `AZURE_OPENAI_*`, or an existing `az login`
   - OpenRouter: `OPENROUTER_API_KEY`
   - Fireworks: `~/.config/jcode/fireworks.env`, `FIREWORKS_API_KEY`
   - MiniMax: `~/.config/jcode/minimax.env`, `MINIMAX_API_KEY`
   - NVIDIA NIM: `~/.config/jcode/nvidia-nim.env`, `NVIDIA_API_KEY`
   - Alibaba Cloud Coding Plan: existing jcode config/env if present
5. Prefer whichever provider is already configured and verify it with `jcode auth-test --all-configured` or a provider-specific auth test when appropriate.
6. Only if no usable provider is already configured, guide me through the minimal manual step needed:
   - Claude: `jcode login --provider claude`
   - GitHub Copilot: `jcode login --provider copilot`
   - OpenAI: `jcode login --provider openai`
   - Gemini: `jcode login --provider gemini`
   - Azure OpenAI: `jcode login --provider azure`
   - Fireworks: `jcode login --provider fireworks`
   - MiniMax: `jcode login --provider minimax`
   - NVIDIA NIM: `jcode login --provider nvidia-nim`
   - Alibaba Cloud Coding Plan: `jcode login --provider alibaba-coding-plan`
   - OpenRouter: help me set `OPENROUTER_API_KEY`
   - Anthropic direct API: help me set `ANTHROPIC_API_KEY`
7. After setup, run a simple smoke test with `jcode run "say hello"` and confirm it works.
8. If I want browser automation, also check `jcode browser status`. If browser automation is not ready, run `jcode browser setup`, verify the built-in `browser` tool works, and explain any remaining manual step.
9. Explain any manual step that still needs me, especially browser OAuth, device login, API key entry, or browser extension approval.
```

此提示词专为让 `jcode` 自身或其他编码智能体一键自举设置而设计。

### 快速安装

```bash
# macOS & Linux
curl -fsSL https://raw.githubusercontent.com/1jehuang/jcode/master/scripts/install.sh | bash
```

在 Termux 上，请先安装 glibc 运行时和 `patchelf`，以便安装脚本能将下载的 Linux 二进制文件修补至 Termux 的 glibc 动态链接器，并创建避免 Termux `LD_PRELOAD` shim 的启动器：

```bash
pkg install glibc patchelf
curl -fsSL https://raw.githubusercontent.com/1jehuang/jcode/master/scripts/install.sh | bash
```

```powershell
# Windows (PowerShell)
irm https://raw.githubusercontent.com/1jehuang/jcode/master/scripts/install.ps1 | iex
```

### macOS 通过 Homebrew 安装

```bash
brew tap 1jehuang/jcode
brew install jcode
```

### 从源码编译（全平台）

```bash
git clone https://github.com/1jehuang/jcode.git
cd jcode
cargo build --release
```

若在 Linux x86_64 上进行本地自我开发 / 重构工作，推荐使用：

```bash
scripts/dev_cargo.sh build --release -p jcode --bin jcode
scripts/dev_cargo.sh --print-setup
```

该包装器会在可用时自动使用 `sccache`，优先采用快速的本地链接器设置（`clang + lld`）而非假设每台机器的 `mold` 配置均有效，并可通过 `--print-setup` 打印当前链接器/缓存状态，便于排查慢速构建问题。

随后创建 PATH 软链接：

```bash
scripts/install_release.sh
```

### 平台支持

| 平台 | 状态 |
|---|---|
| **Linux** x86_64 / aarch64 | 完全支持 |
| **macOS** Apple Silicon & Intel | 支持 |
| **Windows** x86_64 | 支持（原生 + WSL2） |
| **Termux** aarch64 / x86_64 | 支持（需 `pkg install glibc patchelf`） |

</div>
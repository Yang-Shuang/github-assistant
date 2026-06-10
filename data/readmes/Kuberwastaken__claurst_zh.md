<div align="center">

<h1>CLAURST</h1>
<h2><em>面向高效交付开发者的智能体编程</em></h2>
<img src="public/Ship.png" alt="Rustle 与船只" width="350" />

<p>
    <a href="https://github.com/kuberwastaken/claurst"><img src="https://img.shields.io/badge/Built_with-Rust-CE4D2B?style=for-the-badge&logo=rust&logoColor=white" alt="Built with Rust"></a>
    <a href="https://github.com/kuberwastaken/claurst"><img src="https://img.shields.io/badge/Version-0.1.4-2E8B57?style=for-the-badge" alt="Version 0.1.4"></a>
    <a href="https://github.com/kuberwastaken/claurst/blob/main/LICENSE.md"><img src="https://img.shields.io/badge/License-GPL--3.0-blue?style=for-the-badge" alt="GPL-3.0 License"></a>
</p>

<br />

<img src="public/screenshot.png" alt="Claurst 运行效果" width="1080" />
</div>

---

Claurst 是一款**完全使用 Rust 从零构建的开源、多提供商终端编程智能体**。它最初是对 [Claude Code](https://github.com/kuberwastaken/claurst/tree/main/spec) 行为规范的干净室（Clean-room）重新实现，随后已演进为一个功能强大的 TUI（终端用户界面）结对编程工具，支持多提供商接入、丰富的 UI、插件系统、名为 Rustle 的伴侣助手、聊天分支、记忆整合等功能。

它运行快速、内存占用低，完全由你自由掌控，且没有任何追踪或遥测数据收集。

---

> [!IMPORTANT]
> **Claurst 现已正式进入测试版（v0.1.4）。** 核心智能体、多提供商路由和 TUI 已足够稳定，可投入日常使用——实验性功能（见下文标注）可能仍有不完善之处。欢迎提交 Bug 报告和 PR。

> [!NOTE]
> **最新更新：**
>
> - **支持 `/share`：** 使用 `/share` 通过未列出的 GitHub Gist 与他人共享聊天会话。`[实验性功能]`
>
> - **免费模式（Free Mode）：** 在 `/connect` 中尝试使用“Free”选项，即可完全免费（或接近免费）体验 Claurst 出色的智能体编程功能。`[实验性功能]` 
>
> - **支持 `/goal`：** 尝试使用 `/goal <目标>`，观察 Claurst 如何持续完成指定目标，跨越多个回合而非仅执行一次正常交互。`[实验性功能]`

---

# 快速开始

## 一键安装（单行命令）

**Linux / macOS：**

```bash
curl -fsSL https://github.com/kuberwastaken/claurst/releases/latest/download/install.sh | bash
```

**Windows (PowerShell)：**

```powershell
irm https://github.com/kuberwastaken/claurst/releases/latest/download/install.ps1 | iex
```

这会将 `claurst` 放置到 `~/.claurst/bin`（Windows 为 `%USERPROFILE%\.claurst\bin`）并自动添加到你的 `PATH` 环境变量中。打开新终端窗口，运行 `claurst` 即可。

## 通过 npm / bun 安装

如果你已安装 Node.js 或 Bun，可以将其作为全局包进行安装。`postinstall` 脚本会自动为你下载对应平台的预编译二进制文件。

```bash
# npm
npm install -g claurst

# bun
bun install -g claurst

# 或直接运行（无需全局安装）
npx claurst
bunx claurst
```

后续升级请运行：

```bash
claurst upgrade
```

> 在任一安装命令后附加 `--version 0.1.0`，或运行 `claurst upgrade --version 0.1.0` 可锁定特定版本。

## 手动下载

如果你更倾向于自行获取二进制文件，最新版本归档请前往 [**GitHub Releases**](https://github.com/kuberwastaken/claurst/releases)：

| Platform | Archive |
|----------|---------|
| **Windows** x86_64 | `claurst-windows-x86_64.zip` |
| **Linux** x86_64 | `claurst-linux-x86_64.tar.gz` |
| **Linux** aarch64 | `claurst-linux-aarch64.tar.gz` |
| **macOS** Intel | `claurst-macos-x86_64.tar.gz` |
| **macOS** Apple Silicon | `claurst-macos-aarch64.tar.gz` |

每个归档文件仅包含一个 `claurst`（或 Windows 下的 `claurst.exe`）二进制文件。解压后将其添加到你的 `PATH` 即可。

## 从源码构建

```bash
git clone https://github.com/kuberwastaken/claurst.git
cd claurst/src-rust
cargo build --release --package claurst

# 编译后的二进制文件位于 target/release/claurst
```

**树莓派 / 无 ALSA 的系统**（例如 Debian Trixie、无头服务器）：

```bash
# 构建时不启用语音/麦克风支持——无需安装 libasound2-dev
cargo build --release --package claurst --no-default-features
```

## 首次运行

```bash
# 设置你的 API Key（或在 Claurst 内使用 /connect 进行配置）
export ANTHROPIC_API_KEY=sk-ant-...

# 启动 Claurst
claurst

# 或运行一次性无头查询
claurst -p "explain this codebase"
```

## Devcontainer 环境配置

克隆本仓库后，在 VS Code 中打开它，并使用“Reopen in Container”（重新在容器中打开）来启动开发环境。

**前置要求：**
- 宿主机已安装 Docker：https://www.docker.com/products/docker-desktop/

Devcontainer 中已启用 GPG 和 SSH 转发（前提是你已在宿主机上完成配置）。如需帮助，请查阅[此指南](https://code.visualstudio.com/remote/advancedcontainers/sharing-git-credentials)。

### Devcontainer 特性

- 基础镜像：`rust:1-bullseye`。
- 预装构建依赖项：`gnupg2`、`libasound2-dev`、`libxdo-dev` 和 `pkg-config`。
- 启用的 Devcontainer 特性：`common-utils`（配置 `vscode` 用户 `uid/gid 为 1000`，禁用 Zsh 安装）、`git` 和 `docker-outside-of-docker`（`moby: false`）。
- 默认以 `vscode` 用户身份运行。
- 通过命名卷持久化 Cargo 缓存，挂载路径为 `/usr/local/cargo/registry` 和 `/usr/local/cargo/git`。
- 将本地 `.claurst` 目录绑定至 `/home/vscode/.claurst`，以便访问本地配置与会话历史。
- 设置环境变量 `GNUPGHOME=/home/vscode/.gnupg`，并将 `src-rust/target/debug` 与 `src-rust/target/release` 追加至 `PATH`。
- 创建后脚本会初始化并设置 `.gnupg` 权限，同时修复 `/usr/local/cargo` 的所有权。
- 启用 VS Code 配置项 `terminal.integrated.inheritEnv`。

## 编辑器集成（智能体客户端协议 / Agent Client Protocol）

Claurst 支持 **[智能体客户端协议（ACP）**](https://agentclientprotocol.com)——由 Zed 首创的用于编辑器与智能体通信的开放协议。任何支持 ACP 的编辑器（如 Zed、Neovim、JetBrains 插件等）均可将 Claurst 作为子进程驱动，并在编辑器的原生聊天界面中展示。

若要在编辑器中将 Claurst 设为智能体代理，请将其 ACP 集成指向：

```
command: claurst
args:    ["acp"]
```

**Zed 示例**（配置文件 `~/.config/zed/settings.json`）：

```jsonc
{
  "agent_servers": {
    "claurst": {
      "command": "claurst",
      "args": ["acp"]
    }
  }
}
```

Claurst 将通过 stdio 以 JSON-RPC 2.0 模式运行。它实现了 `initialize`、`session/new`、`session/prompt` 和 `session/cancel`，流式推送 `session/update` 通知（包含文本增量、智能体思考过程、工具调用及其进度与结果），并通过 `session/request_permission` 路由所有工具权限请求，以便编辑器展示原生审批对话框。

启动前请在 `~/.claurst/settings.json`（或运行 `claurst auth login` / `claurst /connect`）中配置你的提供商与 API Key——ACP 智能体将使用与交互式 TUI 相同的凭据和提供商。

通过设置环境变量 `CLAURST_ACP_LOG=debug` 可启用详细的 ACP 日志记录（输出至 stderr——切勿输出到 stdout，否则会导致协议损坏）。

### 收录于 ACP 注册表

**[智能体客户端协议注册表](https://github.com/agentclientprotocol/registry)** 是编辑器在提供“可用智能体”时查询的标准目录。若要将 Claurst 收录其中：

1. Fork [`agentclientprotocol/registry`](https://github.com/agentclientprotocol/registry)。
2. 在仓库根目录创建 `claurst/` 文件夹，并放入本仓库中准备好的清单文件：[`src-rust/crates/acp/registry-template/agent.json`](src-rust/crates/acp/registry-template/agent.json)。将 `version` 和发布归档 URL 更新为最新的 GitHub Release。
3. 添加 `claurst/icon.svg`（建议尺寸 16×16）——[`public/`](public/) 目录中的 Rustle Logo 是一个不错的起点。
4. 向注册表仓库提交 PR。合并前，注册表的 CI 将使用[该 Schema](https://github.com/agentclientprotocol/registry/blob/main/agent.schema.json) 对 `agent.json` 进行校验。

合并后，Zed 及其他支持 ACP 的编辑器将在下次刷新注册表时自动识别并收录 Claurst。

## 文档

有关如何配置 Claurst 的更多信息，[请前往我们的文档站点](https://claurst.kuber.studio/docs)。

>**附注：** 该项目最初源于我对 Claude Code 源码的分析发现（即该项目启动时的技术拆解），完整的技术复盘文章发布在 [我的博客](https://kuber.studio/blog/AI/Claude-Code's-Entire-Source-Code-Got-Leaked-via-a-Sourcemap-in-npm,-Let's-Talk-About-it) 上，详细记录了发现内容、泄露过程及其揭示的技术细节。

---

## 贡献指南

Claurst 由社区构建并服务于社区，我们非常期待你的帮助让它变得更好。
请参阅并遵守 `AGENTS.md` 中的项目特定规范（适用于人类开发者与 AI 智能体）。

遇到 Bug、有想法或疑问请[提交 Issue](https://github.com/Kuberwastaken/claurst/issues/new)，或通过[提交 PR](https://github.com/Kuberwastaken/claurst/pulls/new) 修复 Bug、添加功能或完善文档。

---

## 重要声明

本仓库不包含任何闭源 Claude Code TypeScript 源码的副本。
这是对 Claude Code 行为规范的**干净室（Clean-room）Rust 重新实现**。

开发过程明确分为两个阶段：

**规范制定（Specification）** [`spec/`](https://github.com/kuberwastaken/claurst/tree/main/spec) —— AI 智能体分析了原始源码，生成了详尽的行为规范与改进建议，并完全脱离了原版：架构、数据流、工具契约及系统设计。未沿用任何源代码。

**代码实现（Implementation）** [`src-rust/`](https://github.com/kuberwastaken/claurst/tree/main/src-rust) —— 另一独立的 AI 智能体仅依据上述规范进行编码，从未参考原始 TypeScript。输出结果为符合 Rust 惯用法的代码，旨在复现行为而非复制表达形式。

此举遵循了 Phoenix Technologies v. IBM（1984）案确立的法律先例——即 BIOS 的干净室工程实践，以及 Baker v. Selden（1879）案中“版权保护的是表达形式而非思想或行为”的原则。
<p align="center">
  <img src="apps/marketing/public/og-image.webp" alt="Plannotator" width="80%" />
</p>

# Plannotator

在浏览器中审查 AI Agent 的计划与代码差异（Diff）。添加行内注释，将结构化反馈发送回你的 Agent，并与团队成员分享加密的审查链接。支持 **Claude Code**、**Copilot CLI**、**Gemini CLI**、**OpenCode**、**Pi**、**Codex**、**Droid** 和 **Amp**。

**计划模式演示：**
<table>
<tr>
<td align="center" width="50%">
<h3>Claude Code</h3>
<a href="https://www.youtube.com/watch?v=a_AT7cEN_9I">
<img src="apps/marketing/public/youtube.png" alt="Claude Code Demo" width="100%" />
</a>
<p><a href="https://www.youtube.com/watch?v=a_AT7cEN_9I">观看演示</a></p>
</td>
<td align="center" width="50%">
<h3>OpenCode</h3>
<a href="https://youtu.be/_N7uo0EFI-U">
<img src="apps/marketing/public/youtube-opencode.png" alt="OpenCode Demo" width="100%" />
</a>
<p><a href="https://youtu.be/_N7uo0EFI-U">观看演示</a></p>
</td>
</tr>
</table>

**注释：** 计划、规范、文件夹、文件、URL。直接向 Agent 发送反馈。 

**新增：** [代码审查（Code Review）](https://x.com/backnotprop/status/2031145299738263567?s=20)
  
  - 将你的反馈发送给 Agent
  - 内置功能： 
    - Ask AI（向 AI 提问）
    - Agent 代码审查 

### 特性

<table>
<tr><td><strong>可视化计划审查</strong></td><td>内置 Hook</td><td>通过行内注释和 Ask AI 侧边栏聊天批准或拒绝 Agent 的计划</td></tr>
<tr><td><strong>计划差异（Plan Diff）</strong></td><td>自动</td><td>查看 Agent 修改计划时的变更内容</td></tr>
<tr><td><strong>代码审查</strong></td><td><code>/plannotator-review</code></td><td>查看 Git Diff 或远程 PR。在审查时打包注释，并向 AI 提问关于代码的问题。</td></tr>
<tr><td><strong>注释任意文件</strong></td><td><code>/plannotator-annotate &lt;file|folder|url&gt;</code></td><td>注释 Markdown、HTML、URL 或文件夹，向 AI 询问当前文档内容，并向你的 Agent 发送反馈。</td></tr>
<tr><td><strong>注释最后一条消息</strong></td><td><code>/plannotator-last</code></td><td>注释 Agent 的最后一次回复并发送结构化反馈</td></tr>
</table>

#### 分享计划

Plannotator 允许你与同事私密地共享计划、注释和反馈。例如，同事可以批注已分享的计划，你可以导入他们的反馈并直接发送回编程 Agent。

**小型计划**完全编码在 URL Hash 中。无需服务器参与，不存储任何数据。

**大型计划**使用带有**端到端加密（End-to-End Encryption）**的短链接服务。你的计划在上传前会在浏览器中使用 AES-256-GCM 进行加密。服务器仅存储无法读取的密文。解密密钥仅存在于你分享的 URL 中。粘贴内容将在 7 天后自动删除。

- 零知识存储，类似于 [PrivateBin](https://privatebin.info/)
- 完全开源且支持**自托管（Self-host）**（[查看文档](https://plannotator.ai/docs/guides/sharing-and-collaboration/)）

## 安装

- [Claude Code](#install-for-claude-code)
- [Copilot CLI](#install-for-copilot-cli)
- [Gemini CLI](#install-for-gemini-cli)
- [OpenCode](#install-for-opencode)
- [Pi](#install-for-pi)
- [Codex](#install-for-codex)
- [Droid](#install-for-droid)

## 安装 Claude Code

**安装 `plannotator` 命令：**

**macOS / Linux / WSL：**

```bash
curl -fsSL https://plannotator.ai/install.sh | bash
```

**Windows PowerShell：**

```powershell
irm https://plannotator.ai/install.ps1 | iex
```

**然后在 Claude Code 中执行：**

```
/plugin marketplace add backnotprop/plannotator
```

插件安装完成后重启 Claude Code。

<details>
<summary>固定特定版本或验证来源（Provenance）</summary>

```bash
curl -fsSL https://plannotator.ai/install.sh | bash -s -- --version vX.Y.Z
```

```powershell
& ([scriptblock]::Create((irm https://plannotator.ai/install.ps1))) -Version vX.Y.Z
```

每个发布的二进制文件均附带 SHA256 校验文件（自动验证）。从 v0.17.2 开始支持 [SLSA 来源证明（Provenance）](https://slsa.dev/) 验证——详见[安装文档](https://plannotator.ai/docs/getting-started/installation/#verifying-your-install)。

</details>

详细的安装说明（包括手动 Hook 方式）请参阅 [apps/hook/README.md](apps/hook/README.md)。

---

## 安装 Copilot CLI

**安装 `plannotator` 命令：**

**macOS / Linux / WSL：**

```bash
curl -fsSL https://plannotator.ai/install.sh | bash
```

**Windows PowerShell：**

```powershell
irm https://plannotator.ai/install.ps1 | iex
```

**然后在 Copilot CLI 中执行：**

```
/plugin marketplace add backnotprop/plannotator
/plugin install plannotator-copilot@plannotator
```

插件安装完成后重启 Copilot CLI。当你使用计划模式（按 `Shift+Tab` 进入）时，代码审查功能将自动激活。

详见 [apps/copilot/README.md](apps/copilot/README.md)。

---

## 安装 Gemini CLI

**安装 `plannotator` 命令：**

**macOS / Linux / WSL：**

```bash
curl -fsSL https://plannotator.ai/install.sh | bash
```

**Windows PowerShell：**

```powershell
irm https://plannotator.ai/install.ps1 | iex
```

安装程序会自动检测 Gemini CLI（检查 `~/.gemini` 目录）并配置计划审查 Hook 和策略。同时还会安装 `/plannotator-review` 和 `/plannotator-annotate` 斜杠命令。

**然后在 Gemini CLI 中执行：**

```
/plan                              # 进入计划模式 — 计划在浏览器中打开
/plannotator-review                # 当前变更的代码审查
/plannotator-review <pr-url>       # 审查 GitHub Pull Request
/plannotator-annotate <file.md>    # 注释 Markdown 文件
```

需要 Gemini CLI 0.36.0 或更高版本。

详见 [apps/gemini/README.md](apps/gemini/README.md)。

---

## 安装 OpenCode

添加到你的 `opencode.json`：

```json
{
  "plugin": ["@plannotator/opencode@latest"]
}
```

**运行安装脚本**以获取 `/plannotator-review`：

```bash
curl -fsSL https://plannotator.ai/install.sh | bash
```

**Windows：**
```powershell
irm https://plannotator.ai/install.ps1 | iex
```

此操作还会清除任何缓存的插件版本。然后重启 OpenCode。

---

## 安装 Pi

```bash
pi install npm:@plannotator/pi-extension
```

然后通过 `--plan` 启动 Pi 以进入计划模式，或在会话期间使用 `/plannotator` 切换。

详见 [apps/pi-extension/README.md](apps/pi-extension/README.md) 获取完整的使用说明、命令和参数。

---

## 安装 Codex

**安装 `plannotator` 命令：**

**macOS / Linux / WSL：**

```bash
curl -fsSL https://plannotator.ai/install.sh | bash
```

当检测到已安装 Codex 或 `~/.codex` 目录存在时，安装程序还会启用 Codex Stop Hook。安装或更改 Hook 后请重启 Codex Desktop。

**Windows PowerShell：**

```powershell
irm https://plannotator.ai/install.ps1 | iex
```

在 macOS、Linux 和 WSL 上，Codex 计划审查为自动启用。官方文档中目前禁用了 Windows 上的 Codex Hook，因此 Windows 安装程序不会自动启用它们；但直接使用的 `!plannotator` 命令仍然有效。

**然后在 Codex 中使用——反馈会自动流回 Agent 循环：**

```
$plannotator-review          # 当前变更的代码审查技能
$plannotator-annotate        # 注释 Markdown 文件、URL 或文件夹
$plannotator-last            # 注释最后一条 Agent 消息
```

```
!plannotator review           # 当前变更的代码审查
!plannotator review <pr-url>  # 审查 GitHub Pull Request
!plannotator annotate file.md # 注释 Markdown 文件
!plannotator last             # 注释最后一条 Agent 消息
```

计划审查在 macOS、Linux 和 WSL 上使用 Codex 的实验性 `Stop` Hook。

详见 [apps/codex/README.md](apps/codex/README.md)。

---

## 安装 Droid

**安装 `plannotator` 命令：**

**macOS / Linux / WSL：**

```bash
curl -fsSL https://plannotator.ai/install.sh | bash
```

**Windows PowerShell：**

```powershell
irm https://plannotator.ai/install.ps1 | iex
```

**然后在 Droid 中执行：**

```bash
droid plugin marketplace add https://github.com/backnotprop/plannotator
droid plugin install plannotator@plannotator
```

该 Droid 插件仅包含命令功能。它新增：

```text
/plannotator-review
/plannotator-annotate <file|folder|url>
/plannotator-last
/plannotator-archive
```

目前它不会拦截 Droid 的计划流程。

详见 [apps/droid-plugin/README.md](apps/droid-plugin/README.md)。

---

## 工作原理

当你的 AI Agent 完成计划后，Plannotator 会：

1. 在浏览器中打开 Plannotator UI
2. 允许你可视化地批注计划（删除、插入、替换、评论）
3. 当有可用的提供商时，允许你向 AI 询问关于计划或高亮选区的问题
4. **批准（Approve）** → Agent 开始执行实现
5. **请求修改（Request changes）** → 你的批注将作为结构化反馈发送回去

（代码审查的流程类似，不同之处在于你还可以针对具体的代码差异行添加评论）

---

## 许可证

Copyright 2025-2026 backnotprop

本项目采用以下任一许可协议授权：
- [Apache License, Version 2.0](LICENSE-APACHE) ([http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0))
- [MIT license](LICENSE-MIT) ([http://opensource.org/licenses/MIT](http://opensource.org/licenses/MIT))

由你自行选择。

### 贡献

除非你明确声明，否则你有意提交给本项目的任何贡献（如 Apache-2.0 许可证所定义），均将按上述条款进行双重许可，不附加其他条款或条件。

## 开发环境

若要在此代码库中运行全局 `plannotator` 命令：

```bash
bun install
bun link
```

链接完成后，如 `plannotator review` 等命令将使用你本地仓库中的 `apps/hook/server/index.ts`。修改 UI 代码后需重新构建打包的 HTML：

```bash
bun run --cwd apps/review build && bun run build:hook
```
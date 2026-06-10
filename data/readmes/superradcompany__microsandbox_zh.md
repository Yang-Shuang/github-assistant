<div align="center">
    <a href="./#gh-dark-mode-only" target="_blank" align="center">
        <img width="35%" src="./assets/microsandbox-gh-banner-dark.png" alt="microsandbox-banner-xl-dark">
    </a>
</div>

<div align="center">
    <a href="./#gh-light-mode-only" target="_blank">
        <img width="35%" src="./assets/microsandbox-gh-banner-light.png" alt="microsandbox-banner-xl">
    </a>
</div>

<br />

<div align="center"><b>——&nbsp;&nbsp;&nbsp;给你的智能体一台专属电脑的最简单方式&nbsp;&nbsp;&nbsp;——</b></div>

<br />
<br />

<div align='center'>
  <a href="https://github.com/superradcompany/microsandbox/releases"><img src="https://img.shields.io/github/v/release/superradcompany/microsandbox?include_prereleases&style=for-the-badge" alt="GitHub release"></a>
  <a href="https://discord.gg/T95Y3XnEAK"><img src="https://img.shields.io/discord/1315784565562019870?label=Discord&logo=discord&logoColor=white&color=5865F2&style=for-the-badge" alt="Discord"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-Apache%202.0-blue.svg?style=for-the-badge" alt="Apache 2.0 License"></a>
</div>

<br />

**Microsandbox** 通过我们的 SDK 在毫秒级启动**轻量级虚拟机**。直接在本地机器上运行。无需配置服务器，无后台守护进程残留。全部嵌入且采用 rootless（无根）架构！

##

- <img height="14" src="https://octicons-col.vercel.app/shield-lock/A770EF"> **硬件隔离 (Hardware Isolation)**：基于微虚拟机技术的硬件级别隔离。
- <img height="14" src="https://octicons-col.vercel.app/zap/A770EF"> **秒级启动**：平均启动时间低于 100 毫秒。
- <img height="14" src="https://octicons-col.vercel.app/plug/A770EF"> **可嵌入 (Embeddable)**：直接在代码中创建虚拟机。无需配置服务器，无长期运行的守护进程。
- <img height="14" src="https://octicons-col.vercel.app/lock/A770EF"> **机密信息防泄露**：无法被利用的密钥永远不会进入虚拟机内部。
- <img height="14" src="https://octicons-col.vercel.app/package/A770EF"> **兼容 OCI 标准 (OCI Compatible)**：支持运行来自 Docker Hub、GHCR 或任何 OCI 注册表的常规容器镜像。
- <img height="14" src="https://octicons-col.vercel.app/database/A770EF"> **长时运行 (Long-Running)**：沙箱可脱离模式（detached）运行，非常适合长时间会话。
- <img height="14" src="https://octicons-col.vercel.app/terminal/A770EF"> **智能体就绪 (Agent-Ready)**：你的智能体可通过我们的 [Agent Skills](https://github.com/superradcompany/skills) 和 [MCP server](https://github.com/superradcompany/microsandbox-mcp) 创建自己的沙箱。


<br />

## <a href="./#gh-dark-mode-only" target="_blank"><img height="13" src="https://octicons-col.vercel.app/rocket/ffffff" alt="rocket-dark"></a><a href="./#gh-light-mode-only" target="_blank"><img height="13" src="https://octicons-col.vercel.app/rocket/000000" alt="rocket"></a>&nbsp;&nbsp;快速开始

#### <img height="14" src="https://octicons-col.vercel.app/move-to-bottom/A770EF">&nbsp;&nbsp;安装 SDK

> ```sh
> cargo add microsandbox                                   # 🦀 Rust
> ```
> ```sh
> uv add microsandbox                                      # 🐍 Python
> ```
> ```sh
> npm i microsandbox                                       # 🟦 TypeScript
> ```
> ```sh
> go get github.com/superradcompany/microsandbox/sdk/go    # 🐹 Go
> ```

#### <img height="14" src="https://octicons-col.vercel.app/download/A770EF">&nbsp;&nbsp;安装 CLI **（可选）**

> 一条命令即可启动微虚拟机。
>
> ```sh
> npx microsandbox run debian
> ```
>
> 或全局安装 `msb` 命令：
>
> ```sh
> curl -fsSL https://install.microsandbox.dev | sh
> ```
>
> ```sh
> msb run debian
> ```

##

> **环境要求**：需启用 KVM 的 Linux，或搭载 Apple Silicon 芯片的 macOS。<br />
> **警告**：Microsandbox 目前仍处于 **测试阶段**。请预期可能会有破坏性变更、功能缺失及体验粗糙之处。

<br />

## <a href="./#gh-dark-mode-only" target="_blank"><img height="18" src="https://octicons-col.vercel.app/package-dependencies/ffffff" alt="sdk-dark"></a><a href="./#gh-light-mode-only" target="_blank"><img height="18" src="https://octicons-col.vercel.app/package-dependencies/000000" alt="sdk"></a>&nbsp;&nbsp;SDK

该 SDK 允许你直接从应用程序中创建和控制沙箱。`Sandbox::builder("...").create()` 会将微虚拟机作为子进程启动。无需任何基础设施支持。

#### <img height="14" src="https://octicons-col.vercel.app/play/A770EF">&nbsp;&nbsp;在沙箱中运行代码

> ```rs
> use microsandbox::Sandbox;
>
> #[tokio::main]
> async fn main() -> Result<(), Box<dyn std::error::Error>> {
>     let sandbox = Sandbox::builder("my-sandbox")
>         .image("python")
>         .cpus(1)
>         .memory(512)
>         .create()
>         .await?;
>
>     let output = sandbox
>         .exec("python", ["-c", "print('Hello from a microVM!')"])
>         .await?;
>
>     println!("{}", output.stdout()?);
>
>     sandbox.stop_and_wait().await?;
>
>     Ok(())
> }
> ```
>
> <details>
> <summary><b>&nbsp;Python Example →</b></summary>
>
> ```python
> import asyncio
> from microsandbox import Sandbox
>
> async def main():
>     sandbox = await Sandbox.create(
>         "my-sandbox",
>         image="python",
>         cpus=1,
>         memory=512,
>     )
>
>     output = await sandbox.exec("python", ["-c", "print('Hello from a microVM!')"])
>
>     print(output.stdout_text)
>
>     await sandbox.stop_and_wait()
>
> asyncio.run(main())
> ```
>
> </details>
>
> <details>
> <summary><b>&nbsp;TypeScript Example →</b></summary>
>
> ```typescript
> import { Sandbox } from "microsandbox";
>
> await using sandbox = await Sandbox.builder("my-sandbox")
>   .image("python")
>   .cpus(1)
>   .memory=512)
>   .create();
>
> const output = await sandbox.exec("python", ["-c", "print('Hello from a microVM!')"]);
>
> console.log(output.stdout());
> ```
>
> </details>
>
> <details>
> <summary><b>&nbsp;Go Example →</b></summary>
>
> ```go
> package main
>
> import (
>     "context"
>     "fmt"
>     "log"
>
>     microsandbox "github.com/superradcompany/microsandbox/sdk/go"
> )
>
> func main() {
>     ctx := context.Background()
>
>     // Downloads the microsandbox runtime to ~/.microsandbox/ on first run.
>     if err := microsandbox.EnsureInstalled(ctx); err != nil {
>         log.Fatal(err)
>     }
>
>     sandbox, err := microsandbox.CreateSandbox(ctx, "my-sandbox",
>         microsandbox.WithImage("python"),
>         microsandbox.WithCPUs(1),
>         microsandbox.WithMemory(512),
>     )
>     if err != nil {
>         log.Fatal(err)
>     }
>     defer sandbox.StopAndWait(ctx)
>
>     output, err := sandbox.Exec(ctx, "python", []string{"-c", "print('Hello from a microVM!')"})
>     if err != nil {
>         log.Fatal(err)
>     }
>
>     fmt.Println(output.Stdout())
> }
> ```
>
> </details>


> 首次调用 `create()` 时，若本地未缓存镜像则会自动拉取，耗时可能因网络状况而异。后续运行将复用缓存。

<br />

<a href="https://docs.microsandbox.dev/sdk/overview"><img src="https://img.shields.io/badge/SDK_Docs-%E2%86%92-A770EF?style=flat-square&labelColor=2b2b2b" alt="SDK Docs"></a>

<br />

## <a href="./#gh-dark-mode-only" target="_blank"><img height="18" src="https://octicons-col.vercel.app/terminal/ffffff" alt="cli-dark"></a><a href="./#gh-light-mode-only" target="_blank"><img height="18" src="https://octicons-col.vercel.app/terminal/000000" alt="cli"></a>&nbsp;&nbsp;CLI

`msb` CLI 提供了管理沙箱、镜像和卷的完整接口。

#### <img height="14" src="https://octicons-col.vercel.app/play/A770EF">&nbsp;&nbsp;运行命令

> ```sh
> msb run python -- python3 -c "print('Hello from a microVM!')"
> ```

#### <img height="14" src="https://octicons-col.vercel.app/stopwatch/A770EF">&nbsp;&nbsp;命名沙箱 (Named Sandboxes)

> ```sh
> # Create and start a named sandbox
> msb create --name my-app python
> ```
>
> ```sh
> # Execute commands
> msb exec my-app -- python -c "import this"
> msb exec my-app -- curl https://example.com
> ```
>
> ```sh
> # Lifecycle
> msb stop my-app
> msb start my-app
> msb rm my-app
> ```

#### <img height="14" src="https://octicons-col.vercel.app/cache/A770EF">&nbsp;&nbsp;镜像管理 (Image Management)

> ```sh
> msb pull python           # Pull an image
> msb image ls              # List cached images
> msb image rm python       # Remove an image
> ```

#### <img height="14" src="https://octicons-col.vercel.app/download/A770EF">&nbsp;&nbsp;安装与卸载沙箱 (Install & Uninstall Sandboxes)

> ```sh
> msb install ubuntu               # Install ubuntu sandbox as 'ubuntu' command
> ubuntu                           # Opens Ubuntu in a microVM
> msb uninstall ubuntu             # Uninstall the ubuntu sandbox
> ```

#### <img height="14" src="https://octicons-col.vercel.app/list-unordered/A770EF">&nbsp;&nbsp;状态与检查 (Status & Inspection)

> ```sh
> msb ls                         # List all sandboxes
> msb ps my-app                  # Show sandbox status
> msb inspect my-app             # Detailed sandbox info
> msb metrics my-app             # Live CPU/memory/network stats
> ```

> [!TIP]
>
> 运行 `msb --tree` 查看所有可用命令及其选项。

<br />

<a href="https://docs.microsandbox.dev/cli/overview"><img src="https://img.shields.io/badge/CLI_Docs-%E2%86%92-A770EF?style=flat-square&labelColor=2b2b2b" alt="CLI Docs"></a>

<br />

## <a href="./#gh-dark-mode-only" target="_blank"><img height="18" src="https://octicons-col.vercel.app/dependabot/ffffff" alt="agents-dark"></a><a href="./#gh-light-mode-only" target="_blank"><img height="18" src="https://octicons-col.vercel.app/dependabot/000000" alt="agents"></a>&nbsp;&nbsp;AI 智能体

让你的 AI 智能体具备创建和管理自身沙箱的能力。

#### <img height="14" src="https://octicons-col.vercel.app/book/A770EF">&nbsp;&nbsp;Agent Skills（智能体技能）

> 通过安装 [Agent Skills](https://github.com/superradcompany/skills)，教会任意 AI 编程智能体使用 Microsandbox。兼容 Claude Code、Cursor、Codex、Gemini CLI、GitHub Copilot 等工具。
>
> ```sh
> npx skills add superradcompany/skills
> ```

#### <img height="14" src="https://octicons-col.vercel.app/plug/A770EF">&nbsp;&nbsp;MCP Server（服务器）

> 通过 [MCP server](https://github.com/superradcompany/microsandbox-mcp) 将任意兼容 MCP 的智能体接入 Microsandbox。提供用于沙箱生命周期管理、命令执行、文件系统访问、卷操作及监控的结构化工具调用。
>
> ```sh
> # Claude Code
> claude mcp add --transport stdio microsandbox -- npx -y microsandbox-mcp
> ```

<br />

## <a href="./#gh-dark-mode-only" target="_blank"><img height="18" src="https://octicons-col.vercel.app/book/ffffff" alt="docs-dark"></a><a href="./#gh-light-mode-only" target="_blank"><img height="18" src="https://octicons-col.vercel.app/book/000000" alt="docs"></a>&nbsp;&nbsp;文档

如需使用指南、API 参考和示例，请访问 [microsandbox 官方文档](https://docs.microsandbox.dev)。

<br />

## <a href="./#gh-dark-mode-only" target="_blank"><img height="18" src="https://octicons-col.vercel.app/gear/ffffff" alt="contributing-dark"></a><a href="./#gh-light-mode-only" target="_blank"><img height="18" src="https://octicons-col.vercel.app/gear/000000" alt="contributing"></a>&nbsp;&nbsp;贡献指南

有兴趣为 `microsandbox` 贡献力量？请查阅我们的 [CONTRIBUTING.md](./CONTRIBUTING.md) 了解贡献规范，以及 [DEVELOPMENT.md](./DEVELOPMENT.md) 获取构建、测试和发布说明。

<br />

## <a href="./#gh-dark-mode-only" target="_blank"><img height="18" src="https://octicons-col.vercel.app/law/ffffff" alt="license-dark"></a><a href="./#gh-light-mode-only" target="_blank"><img height="18" src="https://octicons-col.vercel.app/law/000000" alt="license"></a>&nbsp;&nbsp;开源协议

本项目采用 [Apache License 2.0](./LICENSE) 授权。

<br />

## <a href="./#gh-dark-mode-only" target="_blank"><img height="18" src="https://octicons-col.vercel.app/heart/ffffff" alt="acknowledgements-dark"></a><a href="./#gh-light-mode-only" target="_blank"><img height="18" src="https://octicons-col.vercel.app/heart/000000" alt="acknowledgements"></a>&nbsp;&nbsp;致谢

特别感谢所有贡献者、测试人员及社区成员，是你们让 Microsandbox 每天变得更好！同时感谢为 `microsandbox` 提供技术支持的项目与社区：[libkrun](https://github.com/containers/libkrun) 和 [smoltcp](https://github.com/smoltcp-rs/smoltcp)。

<br />

<div align='center'>
  <a href="https://www.ycombinator.com/"><img src="https://img.shields.io/badge/BACKED%20BY-Y%20COMBINATOR-F26522?style=for-the-badge&logo=ycombinator&logoColor=white" alt="Backed by Y Combinator"></a>
</div>

<br />
<br />
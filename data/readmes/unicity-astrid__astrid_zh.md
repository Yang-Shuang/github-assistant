# Astrid

**面向 AI Agent 的操作系统。**

[![CI](https://github.com/unicity-astrid/astrid/actions/workflows/ci.yml/badge.svg)](https://github.com/unicity-astrid/astrid/actions)
[![License: MIT OR Apache-2.0](https://img.shields.io/badge/License-MIT%20OR%20Apache--2.0-blue.svg)](LICENSE-MIT)
[![MSRV](https://img.shields.io/badge/MSRV-1.94-blue)](https://www.rust-lang.org)
[![Rust 2024](https://img.shields.io/badge/Rust-2024_edition-orange)](https://www.rust-lang.org)

---

Astrid 是一个用户态微内核，它以 Linux 对待进程的方式对待 AI Agent。它包含一个带有启动序列的内核、支持写时复制（copy-on-write）覆盖层的虚拟文件系统、ed25519 能力令牌（capability tokens）、IPC 事件总线、WASM 进程隔离机制，以及一条密码学审计链（每条记录都哈希前一条）。

内核是固定的。其余一切皆为可替换的**胶囊（capsule）**：提供器、编排器、工具、前端、拦截器。你不需要通过 Fork Astrid 来定制它，而是将胶囊组合成符合你使用场景的配置。相同的底层核心 OS，不同的胶囊集合，无限多的配置可能。

当前版本为 v0.5.0。运行于用户态。目前唯一的前端是内置 CLI（`astrid chat`）。架构设计支持 Unikernel 部署。

## 为什么胶囊很重要

大多数 Agent 框架将假设直接写死在代码中。LLM 提供器只是一个库导入，编排循环是一个硬编码函数，工具集是一个静态列表。更改其中任何一项都意味着需要 Fork 该框架、理解其内部实现，并维护一个分叉版本。

Astrid 颠覆了这一模式。内核负责沙箱隔离、IPC、文件系统、能力令牌、预算执行和审计。边界之上的所有内容都是胶囊：一个由 `Capsule.toml` 清单描述的独立 WASM 进程。胶囊通过类型化的 `[imports]`/`[exports]` 表声明其提供和依赖项。内核通过拓扑排序解析依赖并按序启动它们。

这不是在应用上硬塞的插件系统，而是该应用的架构本身。

### 这使得什么成为可能

**完全离线运行。** 将提供器胶囊替换为与 Ollama 或 vLLM 通信的版本。其余部分完全相同。编排器并不知晓也不关心底层模型后端是什么。

**构建新颖的 Agent 架构。** 编写自定义编排器胶囊：辩论系统、蒙特卡洛树搜索规划器、验证链循环。Agent 架构是 AI 研究的前沿领域。Astrid 为研究人员提供了一个生产级运行时，沙箱隔离、预算执行和审计均已就绪。

**通过透明缓存降低 LLM 成本。** 在编排器和提供器之间安装一个缓存胶囊作为中间件。如果之前见过该提示词？直接返回缓存响应。无需修改编排器或提供器。

**支持整夜运行的自主 Agent。** 用自主工作器胶囊替换默认编排器。它能生成代码、运行测试、读取错误、自我修正，并循环直到全部通过。聊天机器人和自主 Agent 的区别在于编排逻辑，而该逻辑是一个可替换的胶囊。

**自由混用提供器。** 同时运行多个提供器胶囊。路由胶囊会检查每个请求，并根据复杂度、成本或延迟选择最佳提供器。所有提供器均使用相同的 IPC 事件协议。

**自我修改的 Agent。** Agent 可以编写新胶囊——Rust 源码、`Capsule.toml`、测试文件——通过 `astrid-build` 构建，使用 `capsule install` 安装，并通过向 IPC 主题发布消息来验证。它可以在运行时扩展自己的 OS：添加新工具、新拦截器、新功能。它还可以跨会话修改自身现有的配置、环境和持久化状态。身份胶囊已在此方面做了小规模实现——LLM 在初始化期间会重写自身的 `spark.toml`。完整图景是一个能编写、测试并部署自身胶囊的 Agent——在能力沙箱内演进自己的运行环境。

**发布自定义发行版。** 打包一个 `Distro.toml` 及胶囊集合。企业 A 获得带审批门禁的编排器，初创公司 B 获得搭载本地模型的自主工作器。安全补丁同时分发给所有用户。

> 这些场景在架构上今天即可实现。内核、IPC 总线、胶囊清单系统和依赖解析器均已存在并经过测试。差异仅在于目前在此基础上构建了多少胶囊。

## Agent 拥有自主权，人类拥有控制权

传统计算以人类为中心。AI Agent 颠覆了这一关系。Agent 负责操作、推理和执行。人类负责监督、审批和引导。Astrid 从底层即为这种倒置模型而构建。

内核强制执行边界，使 Agent 能在其中自由行动。审批门禁确保人类在关键时刻介入，而非每一步都干预。审计链为每项操作提供密码学问责。能力系统允许随着 Agent 表现可靠逐步扩大信任范围。

你保留多少控制权由你自己决定。`mode = "safe"` 会在工作区外的每次操作前询问。`mode = "guided"` 自动允许读取，写入时询问。`mode = "autonomous"` 解除所有限制。而对于大胆的体验者（Astrinauts）：`mode = "yolo"`。

## 安全模型

每项敏感操作在执行前需经过五层过滤：

```text
Agent proposes action
       |
  [1. Policy]    Hard blocks. "sudo" is always denied. Path traversal is always denied.
       |         Admin-controlled deny lists, allowed paths, denied hosts.
       |         Cannot be overridden by tokens or approvals.
       |
  [2. Token]     Does a valid ed25519 capability token cover this action?
       |         Scoped to resource patterns via globset matching.
       |         Time-bounded. Linked to the audit entry that created it.
       |
  [3. Budget]    Is the session within its spending limit?
       |         Per-action and per-session limits, enforced atomically.
       |         Dual-budget: session budget AND workspace budget must both allow.
       |         Reservation-based: cost is held during approval, refunded on denial.
       |
  [4. Approval]  No token? Ask the human.
       |         Allow Once / Allow Session / Allow Workspace / Allow Always / Deny.
       |         "Allow Always" mints a signed capability token for next time.
       |         "Allow Session" creates a scoped allowance that auto-matches future calls.
       |         Human unavailable? The action queues, not silently skips.
       |
  [5. Audit]     Every decision — allowed, denied, deferred — is logged.
                 Each entry is signed by the runtime's ed25519 key.
                 Each entry contains the content hash of the previous.
                 Tamper with the history and the chain breaks.
```

这是真实代码。[`SecurityInterceptor`](crates/astrid-approval/src/interceptor/mod.rs) 实现了此确切流程。测试覆盖了策略拦截、预算耗尽、拒绝时的预算预留退款、异步取消时的预算退款、能力令牌授权、“Allow Session”授权铸造路径以及“Allow Always”令牌铸造路径。

## 双重沙箱

**WASM 沙箱。** 胶囊通过 Extism/Wasmtime 在 WebAssembly 中运行。无系统调用、无文件描述符、无法访问主机内存。所有外部资源（文件系统、网络、IPC、KV 存储）均受能力检查的主机函数限制。主机 ABI 暴露了 49 个跨文件系统、IPC、存储、网络、身份、生命周期、进程管理、审批、钩子和时钟子系统的函数。硬性限制：64 MB 内存上限、5 分钟墙钟超时、胶囊二进制文件的 BLAKE3 哈希验证（无哈希或哈希错误则拒绝加载）。

**虚拟文件系统覆盖层。** Agent 操作于写时复制文件系统之上。工作区为只读下层，写入操作进入由临时目录支持的瞬态上层。会话结束：将差异提交至工作区，或丢弃临时目录以放弃更改。路径遍历（`../../etc/passwd`）在到达主机文件系统前会被 VFS 层拒绝。文件句柄使用基于能力的 `DirHandle`/`FileHandle` 类型。

## 主机 ABI

WASM 到主机的边界是一个扁平的系统调用表（syscall table）。WASM 访客无法导入任意主机函数。

| 子系统 | 系统调用 |
|---|---|
| **文件系统** | `astrid_fs_exists`, `astrid_read_file`, `astrid_write_file`, `astrid_fs_mkdir`, `astrid_fs_readdir`, `astrid_fs_stat`, `astrid_fs_unlink` |
| **IPC** | `astrid_ipc_publish`, `astrid_ipc_subscribe`, `astrid_ipc_recv` (blocking), `astrid_ipc_poll` (non-blocking), `astrid_ipc_unsubscribe` |
| **Uplinks** | `astrid_uplink_register`, `astrid_uplink_send` |
| **存储** | `astrid_kv_get`, `astrid_kv_set`, `astrid_kv_delete`, `astrid_kv_list_keys`, `astrid_kv_clear_prefix` |
| **HTTP** | `astrid_http_request`, `astrid_http_stream_start`, `astrid_http_stream_read`, `astrid_http_stream_close` |
| **网络** | `astrid_net_bind_unix`, `astrid_net_accept`, `astrid_net_poll_accept`, `astrid_net_read`, `astrid_net_write`, `astrid_net_close_stream` |
| **身份** | `astrid_identity_resolve`, `astrid_identity_link`, `astrid_identity_unlink`, `astrid_identity_create_user`, `astrid_identity_list_links` |
| **生命周期** | `astrid_elicit` (user input during install), `astrid_has_secret`, `astrid_signal_ready`, `astrid_get_caller`, `astrid_get_config` |
| **进程** | `astrid_spawn_host`, `astrid_spawn_background_host`, `astrid_read_process_logs_host`, `astrid_kill_process_host` |
| **审批** | `astrid_request_approval` (blocks guest until human responds or timeout) |
| **安全** | `astrid_check_capsule_capability` |
| **钩子** | `astrid_trigger_hook`, `astrid_get_interceptor_handles` |
| **时钟** | `astrid_clock_ms` |
| **日志** | `astrid_log` |

每个参数均以原始字节形式跨越边界。[SDK](https://github.com/unicity-astrid/sdk-rust) 在此基础上添加了类型化便利封装，镜像 `std` 模块布局（`fs`, `net`, `process`, `env`, `time`, `log`）以及 Astrid 专属模块（`ipc`, `kv`, `http`, `hooks`, `uplink`, `identity`, `approval`, `runtime`）。

## 胶囊

在 OS 模型中，胶囊即为进程：由 `Capsule.toml` 清单描述的独立执行单元。一个胶囊可组合多种引擎：

- **WASM** — 编译型沙箱，通过系统调用完全访问主机 ABI
- **MCP** — 原生子进程，通过 JSON-RPC（MCP 2025-11-25 规范，封装 `rmcp`）代理
- **Static** — 声明式上下文注入（文件、提示词）

清单声明胶囊的 `[imports]`（需要从其他胶囊获取的内容）和 `[exports]`（向系统提供的功能），使用带命名空间接口名称及 semver 版本要求。胶囊间的依赖关系在启动时通过拓扑排序解析。内核会在任何胶囊启动前验证所有必需的导入是否已满足。

清单还可声明命令、技能、拦截器、IPC 主题、MCP 服务器和上行链路（uplinks）。

```rust
use astrid_sdk::prelude::*;

#[derive(Default)]
pub struct MyTools;

#[capsule]
impl MyTools {
    #[astrid::tool]
    fn search_issues(&self, args: SearchArgs) -> Result<SearchResult, SysError> {
        let token = env::var("GITHUB_TOKEN")?;
        let resp = http::get(&format!(
            "https://api.github.com/search/issues?q={}", args.query
        ))?;
        // ...
    }
}
```

`#[capsule]` 过程宏（proc macro）生成所有 WASM ABI 样板代码：`extern "C"` 导出、跨边界 JSON 序列化，以及工具、命令、钩子、安装和升级入口点的分发路由。胶囊作者依赖 `astrid-sdk` 和 `serde`。

OpenClaw 生态系统的 TypeScript 和 JavaScript 插件通过全 Rust 管道（OXC 转译器、QuickJS/Wizer、导出拼接器）编译为 WASM。Tier 1 插件无需 Node.js。

## 拦截器

胶囊可在 IPC 主题上注册拦截器——一种 eBPF 风格的中间件，在核心处理器执行前（或替代其）触发。拦截器返回 `Continue`、`Final` 或 `Deny` 以控制链条。优先级为 10 的守卫可以在核心处理器（优先级 100）看到事件之前否决它。工具是一种 IPC 约定：工具胶囊拦截 `tool.v1.execute.<name>` 和 `tool.v1.request.describe` 主题。路由胶囊负责发现和分发。内核不感知任何工具模式。

## 快速开始

**前置条件：** Rust 1.94+。默认发行版需要 LLM 提供器（例如 Anthropic API Key），但内核本身不需要。

```bash
# Install from crates.io (installs both astrid and astrid-daemon binaries)
cargo install astrid

# Initialize — fetches the default distro, installs capsules, sets up PATH
astrid init

# Start a session (daemon boots automatically on first use)
ANTHROPIC_API_KEY=sk-... astrid chat

# Or build from source
git clone https://github.com/unicity-astrid/astrid.git
cd astrid
cargo build --release
./target/release/astrid init
```

三个二进制文件协同工作：`astrid`（CLI 前端）、`astrid-daemon`（内核进程）和 `astrid-build`（胶囊编译器）。运行 `astrid chat` 时，CLI 会自动将守护进程作为后台进程启动，通过 Unix 域套接字连接并渲染流式事件。守护进程管理 VFS、胶囊、IPC、审计和安全。CLI 负责输入和显示。

### 无头/脚本模式

```bash
# Single-prompt, non-interactive — prints response and exits
astrid -p "summarize the git log"

# Pipe stdin
git diff HEAD~1 | astrid -p "write a commit message for this diff"

# Multi-turn scripted conversation
SESSION=$(astrid -p "start a task" --print-session 2>&1 | tail -1)
astrid -p "continue the task" --session "$SESSION"

# Autonomous mode (auto-approve all tool requests)
astrid -p "fix all failing tests" --yes
```

### 守护进程生命周期

```bash
astrid start     # Start a persistent daemon (survives terminal close)
astrid status    # Show PID, uptime, connected clients, loaded capsules
astrid stop      # Graceful shutdown
astrid self-update  # Download the latest release binary to ~/.astrid/bin/
```

## 发行版系统

**发行版（distro）** 是一个描述特定用途胶囊集合的 `Distro.toml` 清单。`astrid init` 获取该清单，展示多选提供器组选择器，通过交互式提示解析 `{{ var }}` 模板变量，并安装所有选定的胶囊及进度条。写入原子化的 `Distro.lock`，包含每个已安装胶囊的 BLAKE3 哈希值以实现可重现部署。

```bash
# Install the default distro (astralis)
astrid init

# Install a custom distro
astrid init --distro @myorg/my-distro

# Install from a local Distro.toml
astrid init --distro ./path/to/Distro.toml
```

## 胶囊管理

```bash
# Install from GitHub (downloads pre-built .wasm release asset, falls back to build from source)
astrid capsule install @org/capsule-name

# Install from a local path
astrid capsule install ./path/to/capsule

# List installed capsules with capability metadata
astrid capsule list
astrid capsule list --verbose

# Show the imports/exports dependency graph
astrid capsule tree

# Update a specific capsule (or all capsules)
astrid capsule update my-capsule
astrid capsule update

# Remove a capsule (checks dependents before removing)
astrid capsule remove my-capsule
astrid capsule remove my-capsule --force  # bypass dependency check
```

内容寻址（content-addressed）的 WASM 二进制文件存储于 `~/.astrid/bin/`，使用 BLAKE3 哈希命名。当没有其他胶囊引用相同哈希时，移除胶囊会清理 `bin/` 中的二进制文件。二进制存储本身（`bin/` 和 `wit/`）是追加只写的；计划提供 `astrid gc` 用于显式清理。

## 目录结构

Astrid 在 `~/.astrid/` 下采用与 Linux FHS 对齐的布局（可通过 `$ASTRID_HOME` 覆盖）：

```text
~/.astrid/
├── etc/
│   ├── config.toml          deployment config
│   ├── servers.toml         MCP server config
│   ├── gateway.toml         daemon config
│   └── hooks/               system hooks
├── var/
│   └── state.db/            system KV (SurrealKV, persistent)
├── run/                     ephemeral runtime state
│   ├── system.sock          Unix domain socket
│   ├── system.token         session authentication token
│   └── system.ready         daemon readiness sentinel
├── log/                     system logs
├── keys/
│   └── runtime.key          ed25519 signing key
├── bin/                     content-addressed WASM binaries (BLAKE3-named)
├── wit/                     content-addressed WIT interface definitions
└── home/
    └── {principal}/         per-principal isolation
        ├── .local/
        │   ├── capsules/    user-installed capsules
        │   ├── kv/          capsule KV data
        │   ├── log/         capsule logs (daily rotation, 7-day retention)
        │   ├── audit/       per-principal audit chain
        │   ├── tokens/      capability tokens
        │   └── tmp/         VFS /tmp mount
        └── .config/
            └── env/         capsule env config overrides

<project>/.astrid/           workspace-level config (committable)
├── workspace-id             UUID linking project to global state
└── ASTRID.md                project-level agent instructions
```

配置遵循优先级链：工作区 > 用户 > 系统 > 环境变量 > 编译默认值。工作区配置只能**收紧**安全设置，绝不能放宽。

## 多主体支持

每个主体（用户身份）在 `home/{principal}/` 下获得完全隔离的胶囊、KV 数据、审计链、能力令牌和日志。执行主体通过每条 IPC 消息链透明传递——胶囊从不查看或触碰主体路由。KV 命名空间格式：`{principal}:capsule:{name}`。每次调用的主体解析确保跨用户调用写入正确的主体审计日志和 KV。

## 架构

Astrid 遵循严格的内核/用户态划分。内核（原生 Rust 守护进程）拥有所有特权资源。胶囊（WASM 访客）零环境权限，必须通过主机 ABI 请求所有内容。

### 内核 Crates

| Crate | 职责 |
|---|---|
| `astrid-kernel` | 启动运行时。管理 VFS、IPC 总线、胶囊注册表、MCP 客户端、审计日志、KV 存储。监听 Unix 套接字以接受 CLI 连接。 |
| `astrid-approval` | `SecurityInterceptor`：五层过滤门控。策略引擎、预算追踪器、授权存储、审批管理器。 |
| `astrid-capabilities` | ed25519 签名能力令牌，支持通配符资源模式和时间边界。 |
| `astrid-audit` | 链式密码学审计日志。每条记录均带签名并哈希前一条。基于 SurrealKV 实现并含链验证。按主体拆分审计链。 |
| `astrid-vfs` | 写时复制覆盖文件系统。提供 `Vfs` trait，包含 `HostVfs` 和 `OverlayVfs` 实现。基于能力的 `DirHandle`/`FileHandle`。 |
| `astrid-events` | IPC 事件总线。基于广播机制，支持异步接收器和同步订阅回调。类型从 `astrid-types` 重新导出。 |
| `astrid-types` | 共享数据类型：IPC payload、LLM schema、内核 API。依赖极简且兼容 WASM。被内核和 SDK 共同使用。 |
| `astrid-capsule` | 胶囊运行时：清单解析、WASM/MCP/Static 引擎、基于拓扑排序的依赖解析、胶囊注册表、热重载监听器。 |
| `astrid-mcp` | MCP 客户端/服务器生命周期。封装 `rmcp`，提供二进制哈希验证、能力门控和提示支持。 |
| `astrid-crypto` | Ed25519 密钥对（通过 `ed25519-dalek`）、BLAKE3 内容哈希、签名。Drop 时自动清零密钥。 |
| `astrid-storage` | 两级持久化存储。Tier 1：嵌入式 SurrealKV 原生 KV。Tier 2：完整 SurrealDB 查询引擎（SurrealQL）。 |
| `astrid-config` | 分层 TOML 配置：工作区 > 用户 > 系统 > 环境变量 > 默认值。工作区配置只能收紧安全设置，绝不能放宽。 |
| `astrid-workspace` | 工作区边界检测与进程沙箱配置。 |
| `astrid-hooks` | 会话生命周期、工具调用和审批流程的钩子系统。处理器：command, HTTP, WASM。 |
| `astrid-core` | 基础类型：`SessionId`, `PrincipalId`, `Permission`，身份原语，提示类型，会话令牌。 |

### 用户态 Crates

| Crate | 职责 |
|---|---|
| [`astrid-sdk`](https://github.com/unicity-astrid/sdk-rust) | 面向胶囊作者的安全 Rust SDK。镜像 `std` 布局。包含 `astrid-sys`（系统调用表）和 `astrid-sdk-macros`（`#[capsule]` 过程宏）。独立仓库。 |
| `astrid-openclaw` | OpenClaw 插件兼容的 TypeScript 转 WASM 编译器。全 Rust 管道：OXC + QuickJS/Wizer。 |

### 二进制文件

| 二进制文件 | Crate | 职责 |
|---|---|---|
| `astrid` | `astrid-cli` | 终端前端。通过 Unix 套接字连接守护进程。TUI 渲染、无头/脚本模式、胶囊管理、发行版初始化、守护进程生命周期命令。 |
| `astrid-daemon` | `astrid-daemon` | 后台内核进程。启动内核，加载胶囊，响应 IPC 请求。支持 `--ephemeral` 标志用于 CLI 派生实例。 |
| `astrid-build` | `astrid-build` | 胶囊编译器与打包器。处理 Rust、OpenClaw（JS/TS）及遗留 MCP 项目。由 CLI 作为配套二进制文件调用。 |

### 基础设施 Crates

| Crate | 职责 |
|---|---|
| `astrid-telemetry` | 基于 `tracing` 的结构化日志。支持 JSON 和人类可读输出。带每日轮转的文件输出。 |
| `astrid-prelude` | 内部 Crate 的通用重新导出集合。 |

## 存储

两级架构，统一 API 表面：

| 部署场景 | KV 后端 | DB 后端 |
|---|---|---|
| 开发 / 单 Agent | SurrealKV（嵌入式） | SurrealDB（嵌入式，基于 SurrealKV） |
| 生产 / 多节点 | SurrealKV（嵌入式） | SurrealDB（基于 TiKV, Raft） |

胶囊 KV 存储按主体和胶囊划分命名空间。内核、审计日志、能力存储和身份系统使用数据库层。从嵌入式扩展到分布式仅需更改配置。

## v0.5.0 亮点

本次发布的主要变更：

- **FHS 目录布局** — `~/.astrid/` 重构为 `etc/`, `var/`, `run/`, `log/`, `keys/`, `bin/`, `home/`。现有 `~/.astrid/` 必须在升级前删除（无迁移路径）。
- **多主体隔离** — 每个主体在 `home/{principal}/` 下获得隔离的胶囊、KV、审计链、令牌和配置。
- **工具为纯 IPC 约定** — 内核不再解析或管理工具模式。工具胶囊使用 IPC 拦截器。路由胶囊负责发现和分发。
- **LLM 提供器为纯 IPC 约定** — `[[llm_provider]]` 和 `LlmProviderDef` 已从清单中移除。LLM 胶囊通过拦截器自我描述。
- **`[imports]`/`[exports]` 清单格式** — 取代旧的字符串数组 `[dependencies]`，改为带命名空间 TOML 表、semver 版本要求、可选导入及命名空间/接口名称验证。
- **`astrid self-update`** — 从 GitHub Releases 下载平台特定二进制文件至 `~/.astrid/bin/`，无需 sudo。启动更新横幅（缓存 24h）。
- **`astrid init` 发行版系统** — 获取 `Distro.toml`，多选提供器组，`{{ var }}` 模板解析，带 BLAKE3 哈希的原子化 `Distro.lock` 写入。
- **导出冲突检测** — `astrid capsule install` 检测新胶囊是否导出了已由已安装胶囊提供的接口，并提示替换。
- **拦截器优先级** — `[[interceptor]]` 上的 `priority` 字段启用分层拦截链。
- **短路拦截器** — `Continue`, `Final`, 或 `Deny` wire format 控制中间件链条。
- **按主体审计链** — 可通过 `verify_principal_chain()` 独立验证。
- **`astrid capsule tree`** — 渲染导入/导出依赖图。
- **OpenClaw Tier 2** — 带 npm 依赖的 TypeScript 插件可安装、转译并作为 MCP 胶囊运行。
- **`--snapshot-tui`** — 将完整 TUI 渲染至 stdout，用于无需交互式终端的自动化冒烟测试。

完整变更、修复和破坏性更改列表请参阅 [CHANGELOG.md](CHANGELOG.md)。

## 当前状态

**v0.5.0。** 核心运行时已端到端打通：

- 内核启动，发现并加载胶囊，管理 VFS 覆盖层，监听 Unix 套接字
- `SecurityInterceptor` 包含全部五层过滤，测试涵盖策略拦截、预算耗尽、令牌认证、会话/工作区授权及“Allow Always”令牌铸造路径
- WASM 沙箱支持 49 个主机函数，64 MB 内存上限，5 分钟工具超时
- 链式密码学审计日志，带 ed25519 签名及按主体验证的链完整性检查
- MCP 客户端（2025-11-25 规范），通过 `rmcp` 实现能力门控与二进制哈希验证
- IPC 事件总线，支持广播订阅及基于能力的发布/订阅 ACL
- 胶囊依赖解析，通过拓扑排序匹配 semver 版本接口
- 支持命令、技能、拦截器、IPC 主题、MCP 服务器和上行链路的胶囊清单
- OpenClaw TypeScript 转 WASM 编译器（OXC + QuickJS/Wizer，Tier 1 & Tier 2）
- CLI 支持 TUI、流式响应、会话持久化、无头模式及胶囊管理
- 发行版系统含 `Distro.toml` 清单与可重现安装的 `Distro.lock`
- 分层配置，支持工作区级安全收紧
- `astrid self-update` 从 GitHub Releases 下载更新

**尚未完成：** 多节点 SurrealDB（TiKV/Raft）。WASM Component Model 迁移（从 Extism 到 WIT 绑定）。除 CLI 外的其他前端。用于分发的胶囊注册表。

## 开发

```bash
# Build
cargo build --workspace

# Test
cargo test --workspace -- --quiet

# Lint
cargo clippy --workspace --all-features -- -D warnings
cargo fmt --all -- --check
```

所有 Crate 均强制启用 `#![deny(unsafe_code)]`，除 `astrid-sys` 和 `astrid-sdk`（WASM FFI 需要它）。Clippy 以 pedantic 级别运行。整数算术溢出为 lint 错误（`clippy::arithmetic_side_effects = "deny"`）。

通过 [release workflow](.github/workflows/release.yml) 在标签推送时自动构建 macOS (x86_64, aarch64) 和 Linux (x86_64, aarch64) 发布版二进制文件。

## 运维文档

- [网关部署手册](docs/gateway-deployment.md) — 在反向代理后或原生 TLS 下设置 HTTP 管理网关、监控、密钥轮换及故障排查。
- [生成网关 API 客户端](docs/gateway-client.md) — 基于 OpenAPI 规范为 HTTP 管理 API 构建浏览器/原生客户端，以及为何它不应属于胶囊 SDK。
- [统一配置模式](docs/config.md) — `astrid.toml` 参考文档。
- [SDK 易用性说明](docs/sdk-ergonomics.md) — 胶囊作者指南。

## 贡献

欢迎贡献。Astrid 采用分级贡献者系统，以保护安全关键代码的同时保持对新贡献者的开放。每个 PR 必须关联一个 GitHub Issue。请参阅 [CONTRIBUTING.md](CONTRIBUTING.md) 了解完整流程，包括 Issue-first 工作流、分级说明及安全关键 Crate 限制。

## 许可证

采用 [MIT](LICENSE-MIT) 和 [Apache 2.0](LICENSE-APACHE) 双重许可。

Copyright (c) 2025-2026 Joshua J. Bouw and Unicity Labs.
<p align="center">
<picture>
    <source media="(prefers-color-scheme: dark)" srcset="img/rig-rebranded-logo-white.svg">
    <source media="(prefers-color-scheme: light)" srcset="img/rig-rebranded-logo-black.svg">
    <img src="img/rig-rebranded-logo-white.svg" style="width: 40%; height: 40%;" alt="Rig 标志">
</picture>
<br>
<br>
<a href="https://docs.rig.rs"><img src="https://img.shields.io/badge/📖 docs-rig.rs-dca282.svg" /></a> &nbsp;
<a href="https://docs.rs/rig/latest/rig/"><img src="https://img.shields.io/badge/docs-API Reference-dca282.svg" /></a> &nbsp;
<a href="https://crates.io/crates/rig"><img src="https://img.shields.io/crates/v/rig.svg?color=dca282" /></a>
&nbsp;
<a href="https://crates.io/crates/rig"><img src="https://img.shields.io/crates/d/rig-core.svg?color=dca282" /></a>
&nbsp;
<a href="LICENSE"><img src="https://img.shields.io/crates/l/rig.svg?color=dca282" /></a>
</br>
<a href="https://discord.gg/playgrounds"><img src="https://img.shields.io/discord/511303648119226382?color=%236d82cc&label=Discord&logo=discord&logoColor=white" /></a>
&nbsp;
<a href=""><img src="https://img.shields.io/badge/built_with-Rust-dca282.svg?logo=rust" /></a>
&nbsp;
<a href="https://github.com/0xPlaygrounds/rig"><img src="https://img.shields.io/github/stars/0xPlaygrounds/rig?style=social" alt="rig 星数" /></a>
<br>

<br>
</p>
&nbsp;


<div align="center">

[📑 文档](https://docs.rig.rs)
<span>&nbsp;&nbsp;•&nbsp;&nbsp;</span>
[🌐 官网](https://rig.rs)
<span>&nbsp;&nbsp;•&nbsp;&nbsp;</span>
[🤝 贡献代码](https://github.com/0xPlaygrounds/rig/issues/new)
<span>&nbsp;&nbsp;•&nbsp;&nbsp;</span>
[✍🏽 博客指南](https://docs.rig.rs/guides)

</div>

✨ 如果你希望帮助推广 Rig，请考虑给本项目点个 Star！

> [!WARNING]
> ⚠️ 前方高能！由于我们计划在未来几个月内发布大量新功能，未来的更新**将包含破坏性变更**。随着 Rig 的不断演进，我们会在遇到此类情况时标注具体更改内容并指明迁移路径。

## 目录

- [目录](#目录)
- [什么是 Rig？](#什么是-rig)
- [功能特性](#功能特性)
- [谁在使用 Rig？](#谁在使用-rig)
- [快速开始](#快速开始)
  - [简单示例](#简单示例)
- [支持的集成](#支持的集成)

## 什么是 Rig？
Rig 是一个用于构建可扩展、模块化且易于使用（符合 Rust 惯用法）的**大语言模型（LLM）驱动**应用的 Rust 库。

有关该 Crate 的更多信息，请参阅[官方文档](https://docs.rig.rs)和[Crate 参考手册](https://docs.rs/rig/latest/rig/)。

## 功能特性
- 支持多轮流式对话与提示（prompting）的 Agent 工作流
- 完全兼容 [GenAI 语义规范](https://opentelemetry.io/docs/specs/semconv/gen-ai/)
- 支持 20+ 模型提供商，统一接口调用
- 集成 10+ 向量数据库，统一接口调用
- 完整支持 LLM 文本生成（Completion）与 Embedding 工作流
- 支持语音转录、音频生成及图像生成等模型能力
- 以极少的样板代码将 LLM 集成到你的应用中
- 完整兼容 WASM（仅限核心库）

## 谁在使用 Rig？
以下是使用 Rig 的部分公司及开发者列表：
- [St Jude](https://www.stjude.org/) - 在基因组可视化工具 [`proteinpaint`](https://github.com/stjude/proteinpaint) 中作为聊天机器人工具使用 Rig。
- [Coral Protocol](https://www.coralprotocol.org/) - 广泛使用 Rig，包括内部项目及 [Coral Rust SDK.](https://github.com/Coral-Protocol/coral-rs)。
- [VT Code](https://github.com/vinhnx/vtcode) - VT Code 是一个基于 Rust 的终端编码 Agent，通过 Tree-sitter 和 ast-grep 提供语义代码智能。使用 `rig` 简化 LLM 调用并实现模型选择器。
- [Con](https://github.com/nowledge-co/con) - Con 是一款带有内置 AI Agent 框架的 GPU 加速终端模拟器。它使用 Rig 作为集成编码代理的多提供商抽象层。
- [Dria](https://dria.co/) - 去中心化 AI 网络。目前在其 [计算节点.](https://github.com/firstbatchxyz/dkn-compute-node) 中使用 Rig。
- [Nethermind](https://www.nethermind.io/) - 在 [Neural Interconnected Nodes Engine](https://github.com/NethermindEth/nine) 框架中使用 Rig。
- [Neon](https://neon.com) - 在其 Rust 重构项目 [app.build](https://github.com/neondatabase/appdotbuild-agent) V2 中使用 Rig。
- [Listen](https://github.com/piotrostr/listen) - 旨在成为 AI 投资组合管理 Agent 首选框架的框架。为 [Listen 应用.](https://app.listen-rs.com/) 提供动力。
- [Cairnify](https://cairnify.com/) - 通过智能搜索栏帮助用户即时查找文档、链接和信息。Rig 为 Cairnify 的 AI 搜索体验提供了 Agent 基础架构，支持工具调用、推理和检索工作流。
- [Ryzome](https://ryzome.ai) - Ryzome 是一个可视化 AI 工作区，允许你构建相互关联的思维、研究和 AI Agent 画布，以编排复杂的知识工作。
- [deepwiki-rs](https://github.com/sopaco/deepwiki-rs) - 将代码转化为清晰的文档。在几分钟内生成准确的技术文档和 AI 就绪上下文——完美适配人类团队与智能 Agent。
- [Cortex Memory](https://github.com/sopaco/cortex-mem) - 面向智能 Agent 的生产级记忆系统。提供从提取、向量搜索到自动优化的完整内存管理解决方案，内置 REST API、MCP、CLI 和洞察仪表盘。
- [Ironclaw](https://github.com/nearai/ironclaw) - 安全的个人 AI 助手
- [ilert](https://www.ilert.com/) - 事件管理与告警平台。在驱动 ilert AI 的 Agent LLM 代理中，使用 Rig 作为多提供商抽象层。

完整列表请参阅我们的 [ECOSYSTEM.md 文件.](https://www.github.com/0xPlaygrounds/rig/tree/main/ECOSYSTEM.md)

你也在使用 Rig 吗？[提交一个 Issue](https://www.github.com/0xPlaygrounds/rig/issues) 让我们把你加上去！

## 快速开始
如果你需要通过特性开关访问配套 Crate，请使用根模块 `rig`；如果只需要核心提供商抽象层，可直接使用 `rig-core`。

```bash
cargo add rig
# or: cargo add rig-core
```

### 简单示例
```rust
use rig::client::{CompletionClient, ProviderClient};
use rig::completion::Prompt;
use rig::providers::openai;

#[tokio::main]
async fn main() -> Result<(), anyhow::Error> {
    // Create OpenAI client
    let client = openai::Client::from_env()?;

    // Create agent with a single context prompt
    let comedian_agent = client
        .agent(openai::GPT_5_2)
        .preamble("You are a comedian here to entertain the user using humour and jokes.")
        .build();

    // Prompt the agent and print the response
    let response = comedian_agent.prompt("Entertain me!").await?;

    println!("{response}");

    Ok(())
}
```
注意：使用 `#[tokio::main]` 需要启用 tokio 的 `macros` 和 `rt-multi-thread` 特性，或直接启用 `full` 以开启所有特性（执行 `cargo add tokio --features macros,rt-multi-thread`）。

你可以在每个 Crate 的 `examples` 目录中找到更多示例（例如 [`examples`](./examples)）。针对特定提供商的集成测试位于 [`tests/providers`](./tests/providers)，默认使用录制回放（Cassette）进行离线测试，仅在仍需真实 API 时保留在线测试。有关测试目标、回放、录制及安全命令的说明，请参阅 [`tests/README.md`](./tests/README.md)。更多详细的使用案例教程会定期发布在我们的 [Dev.to 博客](https://dev.to/0thtachi)上，并同步更新至 Rig 官方文档 [docs.rig.rs](https://docs.rig.rs)。

## 支持的集成

根模块 `rig` 通过每个集成对应一个特性来暴露配套 Crate：

```toml
rig = { version = "0.36.0", features = ["lancedb", "fastembed"] }
```

| 集成名称 | Crate 包名 | 特性开关 | 模块路径 |
| --- | --- | --- | --- |
| AWS Bedrock | [`rig-bedrock`](https://github.com/0xPlaygrounds/rig/tree/main/crates/rig-bedrock) | `bedrock` | `rig::bedrock` |
| AWS S3Vectors | [`rig-s3vectors`](https://github.com/0xPlaygrounds/rig/tree/main/crates/rig-s3vectors) | `s3vectors` | `rig::s3vectors` |
| Cloudflare Vectorize | [`rig-vectorize`](https://github.com/0xPlaygrounds/rig/tree/main/crates/rig-vectorize) | `vectorize` | `rig::vectorize` |
| FastEmbed | [`rig-fastembed`](https://github.com/0xPlaygrounds/rig/tree/main/crates/rig-fastembed) | `fastembed` | `rig::fastembed` |
| Google Gemini gRPC | [`rig-gemini-grpc`](https://github.com/0xPlaygrounds/rig/tree/main/crates/rig-gemini-grpc) | `gemini-grpc` | `rig::gemini_grpc` |
| Google Vertex AI | [`rig-vertexai`](https://github.com/0xPlaygrounds/rig/tree/main/crates/rig-vertexai) | `vertexai` | `rig::vertexai` |
| HelixDB | [`rig-helixdb`](https://github.com/0xPlaygrounds/rig/tree/main/crates/rig-helixdb) | `helixdb` | `rig::helixdb` |
| LanceDB | [`rig-lancedb`](https://github.com/0xPlaygrounds/rig/tree/main/crates/rig-lancedb) | `lancedb` | `rig::lancedb` |
| Memory policies | [`rig-memory`](https://github.com/0xPlaygrounds/rig/tree/main/crates/rig-memory) | `memory` | `rig::memory` |
| Milvus | [`rig-milvus`](https://github.com/0xPlaygrounds/rig/tree/main/crates/rig-milvus) | `milvus` | `rig::milvus` |
| MongoDB | [`rig-mongodb`](https://github.com/0xPlaygrounds/rig/tree/main/crates/rig-mongodb) | `mongodb` | `rig::mongodb` |
| Neo4j | [`rig-neo4j`](https://github.com/0xPlaygrounds/rig/tree/main/crates/rig-neo4j) | `neo4j` | `rig::neo4j` |
| PostgreSQL | [`rig-postgres`](https://github.com/0xPlaygrounds/rig/tree/main/crates/rig-postgres) | `postgres` | `rig::postgres` |
| Qdrant | [`rig-qdrant`](https://github.com/0xPlaygrounds/rig/tree/main/crates/rig-qdrant) | `qdrant` | `rig::qdrant` |
| ScyllaDB | [`rig-scylladb`](https://github.com/0xPlaygrounds/rig/tree/main/crates/rig-scylladb) | `scylladb` | `rig::scylladb` |
| SQLite | [`rig-sqlite`](https://github.com/0xPlaygrounds/rig/tree/main/crates/rig-sqlite) | `sqlite` | `rig::sqlite` |
| SurrealDB | [`rig-surrealdb`](https://github.com/0xPlaygrounds/rig/tree/main/crates/rig-surrealdb) | `surrealdb` | `rig::surrealdb` |

即使未启用 `memory` 特性，`rig::memory` 也可用；它包含了从 `rig-core` 重新导出的核心对话记忆 trait 和内存后端。启用 `features = ["memory"]` 后，同一模块将增加来自配套 Crate `rig-memory` 的可复用历史上下文管理策略类型。

此外，还有一些相关的配套 Crate 提供了额外功能，在使用 Rig 时可能会对你有所帮助：
- `rig-onchain-kit` - [Rig Onchain Kit.](https://github.com/0xPlaygrounds/rig-onchain-kit) 旨在简化 Solana/EVM 与 Rig 之间的交互实现。


<p align="center">
<br>
<br>
<img src="img/built-by-playgrounds.svg" alt="由 Playgrounds 构建" width="30%">
</p>
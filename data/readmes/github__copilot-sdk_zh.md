# GitHub Copilot CLI SDK

![GitHub Copilot SDK](./assets/RepoHeader_01.png)

[![NPM Downloads](https://img.shields.io/npm/dm/%40github%2Fcopilot-sdk?label=npm)](https://www.npmjs.com/package/@github/copilot-sdk)
[![PyPI - Downloads](https://img.shields.io/pypi/dm/github-copilot-sdk?label=PyPI)](https://pypi.org/project/github-copilot-sdk/)
[![NuGet Downloads](https://img.shields.io/nuget/dt/GitHub.Copilot.SDK?label=NuGet)](https://www.nuget.org/packages/GitHub.Copilot.SDK)
[![Go Reference](https://img.shields.io/badge/Go-Reference-00ADD8?logo=go&logoColor=white)](https://pkg.go.dev/github.com/github/copilot-sdk/go)
[![crates.io](https://img.shields.io/crates/v/github-copilot-sdk?label=crates.io)](https://crates.io/crates/github-copilot-sdk)
[![Maven Central](https://img.shields.io/maven-central/v/com.github/copilot-sdk-java?label=Maven%20Central)](https://central.sonatype.com/artifact/com.github/copilot-sdk-java)

为每个应用打造智能体（Agent）。

使用 GitHub Copilot SDK（Python、TypeScript、Go、.NET、Java 和 Rust）将 Copilot 的智能体工作流嵌入你的应用中。

GitHub Copilot SDK 暴露了 Copilot CLI 背后的同一引擎：一个经过生产环境验证、可编程调用的智能体运行时。你无需自行构建编排逻辑——只需定义智能体的行为，Copilot 将负责规划、工具调用、文件编辑等任务。

## 可用 SDK

| SDK                      | 路径                                                                | Cookbook（示例）                                                                                              | 安装命令                                                                                                                                                                                                                               |
| ------------------------ | ----------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Node.js / TypeScript** | [`nodejs/`](./nodejs/)                                                  | [Cookbook](https://github.com/github/awesome-copilot/blob/main/cookbook/copilot-sdk/nodejs/README.md) | `npm install @github/copilot-sdk`                                                                                                                                                                                                          |
| **Python**               | [`python/`](./python/)                                                  | [Cookbook](https://github.com/github/awesome-copilot/blob/main/cookbook/copilot-sdk/python/README.md) | `pip install github-copilot-sdk`                                                                                                                                                                                                           |
| **Go**                   | [`go/`](./go/)                                                          | [Cookbook](https://github.com/github/awesome-copilot/blob/main/cookbook/copilot-sdk/go/README.md)     | `go get github.com/github/copilot-sdk/go`                                                                                                                                                                                                  |
| **.NET**                 | [`dotnet/`](./dotnet/)                                                  | [Cookbook](https://github.com/github/awesome-copilot/blob/main/cookbook/copilot-sdk/dotnet/README.md) | `dotnet add package GitHub.Copilot.SDK`                                                                                                                                                                                                    |
| **Rust**                 | [`rust/`](./rust/)                                                      | —                                                                                                     | `cargo add github-copilot-sdk`                                                                                                                                                                                                             |
| **Java**                 | [`java/`](./java/) | [Cookbook](https://github.com/github/awesome-copilot/blob/main/cookbook/copilot-sdk/java/README.md)                                                                                                   | Maven 坐标<br>`com.github:copilot-sdk-java`<br>请参阅 [Maven](./java/README.md#maven) 和 [Gradle](./java/README.md#gradle) 的安装说明 |

有关安装、使用示例和 API 参考，请查看各 SDK 的独立 README。

## 快速入门

完整指南请参阅 **[入门指南](./docs/getting-started.md)**。

快速步骤：

1. **（可选）安装 Copilot CLI**

对于 Node.js、Python 和 .NET SDK，Copilot CLI 已自动打包在内，无需单独安装。
对于 Go、Java 和 Rust，请 [手动安装 CLI](https://github.com/features/copilot/cli) 或确保 `copilot` 在你的 PATH 环境变量中可用。Go 和 Rust 还提供了应用级别的 CLI 打包功能。

2. **使用上述命令安装你偏好的 SDK**。

3. **查看对应 SDK 的 README** 获取使用示例和 API 文档。

## 架构设计

所有 SDK 均通过 JSON-RPC 与 Copilot CLI 服务端通信：

```
Your Application
       ↓
  SDK Client
       ↓ JSON-RPC
  Copilot CLI (server mode)
```

SDK 会自动管理 CLI 进程的生命周期。你也可以连接到外部 CLI 服务器——有关以服务端模式运行 CLI 的详细信息，请参阅 [入门指南](./docs/getting-started.md#connecting-to-an-external-cli-server)。

## 常见问题 (FAQ)

### 使用 SDK 是否需要 GitHub Copilot 订阅？

是的，使用 GitHub Copilot SDK **需要**有效的 GitHub Copilot 订阅，**除非你使用的是自带密钥（BYOK）**。通过 BYOK，你可以通过配置受支持的 LLM 提供商的自有 API 密钥来在无 GitHub 身份验证的情况下使用 SDK。对于标准用法（非 BYOK），请参阅 [GitHub Copilot 定价页面](https://github.com/features/copilot#pricing)，其中包含一个带有有限使用量的免费层级。

### SDK 使用的计费方式是怎样的？

GitHub Copilot SDK 的计费模型与 Copilot CLI 相同，每次提示词调用将计入你的高级请求配额。有关高级请求的更多信息，请参阅 [GitHub Copilot 中的请求](https://docs.github.com/en/copilot/concepts/billing/copilot-requests)。

### 是否支持自带密钥（BYOK）？

是的，GitHub Copilot SDK 支持 BYOK（自带密钥）。你可以将 SDK 配置为使用受支持的 LLM 提供商（例如 OpenAI、Azure AI Foundry、Anthropic）的自有 API 密钥来访问模型。请参阅 **[BYOK 文档](./docs/auth/byok.md)** 获取设置说明和示例。

**注意：** BYOK 仅支持基于密钥的身份验证。不支持 Microsoft Entra ID (Azure AD)、托管标识（Managed Identities）和第三方身份提供商。

### 支持哪些身份验证方法？

SDK 支持多种身份验证方式：

- **GitHub 已登录用户** - 使用 `copilot` CLI 登录时存储的 OAuth 凭据
- **OAuth GitHub App** - 传递来自你的 GitHub OAuth 应用的用户令牌
- **环境变量** - `COPILOT_GITHUB_TOKEN`、`GH_TOKEN`、`GITHUB_TOKEN`
- **BYOK** - 使用你自己的 API 密钥（无需 GitHub 身份验证）

有关每种方法的详细信息，请参阅 **[身份验证文档](./docs/auth/index.md)**。

### 是否需要单独安装 Copilot CLI？

不需要——对于 Node.js、Python 和 .NET SDK，Copilot CLI 已作为依赖项自动打包在内。你无需单独安装它。

对于 Go、Java 和 Rust SDK，CLI **默认未**打包在内。请手动安装 CLI 或确保 `copilot` 在你的 PATH 环境变量中可用。Go 和 Rust 还提供了应用级别的 CLI 打包功能。

高级用法：你可以覆盖 CLI 二进制文件或连接到外部服务器。有关特定于语言的选项，请参阅各 SDK 的 README。

### 默认启用了哪些工具？

默认情况下，SDK 会暴露 Copilot CLI 的官方内置工具，类似于使用 `--allow-all` 参数运行 CLI。工具执行仍受每个 SDK 权限处理器（permission handler）的控制，因此应用可以批准、拒绝或自定义工具调用。你可以通过配置 SDK 客户端选项来启用和禁用特定工具以自定义工具可用性。有关工具配置的详细信息请参阅各 SDK 文档，可用工具列表请参阅 Copilot CLI 文档。

### 我可以使用自定义智能体、技能或工具吗？

可以。GitHub Copilot SDK 允许你定义自定义智能体（Agent）、技能（Skills）和工具。你可以通过实现自己的逻辑并集成额外的工具来扩展智能体的功能。有关更多详细信息，请参阅你所选语言的 SDK 文档。

### 是否有针对 Copilot 的说明或 SDK 指导以加速开发？

可以，请查看以下自定义指令和特定于 SDK 的指导：

- **[Node.js / TypeScript](https://github.com/github/awesome-copilot/blob/main/instructions/copilot-sdk-nodejs.instructions.md)**
- **[Python](https://github.com/github/awesome-copilot/blob/main/instructions/copilot-sdk-python.instructions.md)**
- **[.NET](https://github.com/github/awesome-copilot/blob/main/instructions/copilot-sdk-csharp.instructions.md)**
- **[Go](https://github.com/github/awesome-copilot/blob/main/instructions/copilot-sdk-go.instructions.md)**
- **[Rust](./rust/README.md)**（SDK 指导；自定义指令尚未发布）
- **[Java](https://github.com/github/awesome-copilot/blob/main/instructions/copilot-sdk-java.instructions.md)**

### 支持哪些模型？

所有通过 Copilot CLI 可用的模型均在 SDK 中得到支持。SDK 还提供了一个方法，可在运行时返回可用模型列表以便访问。

### SDK 是否已具备生产就绪状态（Production-Ready）？

GitHub Copilot SDK 已正式发布并遵循语义化版本控制。请参阅 [CHANGELOG.md](./CHANGELOG.md) 获取发行说明。

### 如何报告问题或请求功能？

请使用 [GitHub Issues](https://github.com/github/copilot-sdk/issues) 页面来报告错误或请求新功能。我们欢迎你的反馈以帮助改进 SDK。

## 快捷链接

- **[文档](./docs/index.md)** – 完整文档索引
- **[入门指南](./docs/getting-started.md)** – 快速上手的教程
- **[设置指南](./docs/setup/index.md)** – 架构、部署与扩展
- **[身份验证](./docs/auth/index.md)** – GitHub OAuth、BYOK 等
- **[功能特性](./docs/features/index.md)** – Hooks、自定义智能体、MCP、技能等
- **[故障排除](./docs/troubleshooting/debugging.md)** – 常见问题及解决方案
- **[示例代码库 (Cookbook)](https://github.com/github/awesome-copilot/blob/main/cookbook/copilot-sdk)** – 跨所有语言的实用任务配方
- **[更多资源](https://github.com/github/awesome-copilot/blob/main/collections/copilot-sdk.md)** – 额外示例、教程和社区资源

## 非官方社区维护的 SDK

⚠️ 免责声明：这些是非官方的、由社区驱动的 SDK，GitHub 不提供支持。请自行评估风险使用。

| SDK         | 路径                                                 |
| ----------- | -------------------------------------------------------- |
| **Clojure** | [copilot-community-sdk/copilot-sdk-clojure][sdk-clojure] |
| **C++**     | [0xeb/copilot-sdk-cpp][sdk-cpp]                          |

[sdk-cpp]: https://github.com/0xeb/copilot-sdk-cpp
[sdk-clojure]: https://github.com/copilot-community-sdk/copilot-sdk-clojure

## 贡献指南

请参阅 [CONTRIBUTING.md](./CONTRIBUTING.md) 了解贡献规范。

## 许可证

MIT
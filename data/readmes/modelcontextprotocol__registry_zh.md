# MCP 注册表

MCP 注册表为 MCP 客户端提供了一份 MCP 服务器列表，类似于 MCP 服务器的应用商店。

[**📤 发布我的 MCP 服务器**](docs/modelcontextprotocol-io/quickstart.mdx) | [**⚡️ 实时 API 文档**](https://registry.modelcontextprotocol.io/docs) | [**👀 生态愿景**](docs/design/ecosystem-vision.md) | 📖 **[完整文档](./docs)**

## 开发状态

**2025-10-24 更新**：注册表 API 已进入 **API 冻结期（v0.1）** 🎉。在接下来的一个月或更长时间内，API 将保持稳定，不会发生破坏性变更，以便集成方可以放心地实现支持功能。此冻结期适用于 v0.1，而开发工作将继续推进至 v1。我们将利用这段时间在实际集成中验证 API，并收集反馈以塑造面向广泛可用性（GA）的 v1 版本。感谢大家的贡献与耐心——你们的参与对我们至关重要！

**2025-09-08 更新**：注册表已发布预览版 🎉（[公告博客文章](https://blog.modelcontextprotocol.io/posts/2025-09-08-mcp-registry-preview/)）。虽然系统现在更加稳定，但这仍是一个预览版本，可能会发生破坏性变更或数据重置。正式发布（GA）版本将在稍后推出。我们非常欢迎你在 [GitHub 讨论区](https://github.com/modelcontextprotocol/registry/discussions/new?category=ideas) 或 [#registry-dev Discord](https://discord.com/channels/1358869848138059966/1369487942862504016)（[加入详情见此处](https://modelcontextprotocol.io/community/communication)）中提供反馈。

当前主要维护者：
- **Adam Jones** (Anthropic) [@domdomegg](https://github.com/domdomegg)  
- **Tadas Antanavicius** (PulseMCP) [@tadasant](https://github.com/tadasant)
- **Toby Padilla** (GitHub) [@toby](https://github.com/toby)
- **Radoslav (Rado) Dimitrov** (Stacklok) [@rdimitrov](https://github.com/rdimitrov)

## 参与贡献

我们使用多种渠道进行协作——详见 [modelcontextprotocol.io/community/communication](https://modelcontextprotocol.io/community/communication)。

通常（但并非总是）想法会遵循以下流程流转：

- **[Discord](https://modelcontextprotocol.io/community/communication)** - 社区实时讨论
- **[Discussion 讨论区](https://github.com/modelcontextprotocol/registry/discussions)** - 提出并讨论产品/技术需求
- **[Issue 工单](https://github.com/modelcontextprotocol/registry/issues)** - 跟踪范围明确的技术工作  
- **[Pull Request (PR)](https://github.com/modelcontextprotocol/registry/pulls)** - 针对 Issue 提交贡献代码

### 快速开始：

#### 环境要求

- **Docker**
- **Go 1.24.x**
- **ko** - Go 容器镜像构建工具（[安装说明](https://ko.build/install/)）
- **golangci-lint v2.4.0**

#### 运行服务

```bash
# Start full development environment
make dev-compose
```

此命令将在 [`localhost:8080`](http://localhost:8080) 启动注册表服务并连接 PostgreSQL。数据库使用临时存储，每次重启容器时都会重置，从而确保开发和测试环境始终处于干净状态。

**注意：** 注册表使用 [ko](https://ko.build) 构建容器镜像。`make dev-compose` 命令会自动使用 ko 构建注册表镜像，并在启动服务前将其加载到本地 Docker 守护进程中。

默认情况下，注册表会从生产 API 获取过滤后的服务器子集进行初始化（以保持启动速度）。这确保了你的本地环境与生产环境行为一致，且所有种子数据均通过验证。如需离线开发，可通过 `MCP_REGISTRY_SEED_FROM=data/seed.json MCP_REGISTRY_ENABLE_REGISTRY_VALIDATION=false make dev-compose` 从文件加载种子数据并跳过验证。

该配置可通过环境变量进行自定义，详见 [docker-compose.yml](./docker-compose.yml)。参考示例请查看 [.env.example](./.env.example)。

<details>
<summary>替代方案：运行预构建的 Docker 镜像</summary>

预构建的 Docker 镜像会自动发布到 GitHub Container Registry。请注意，该镜像未内置 PostgreSQL，因此你需要自行运行数据库实例，并通过 `MCP_REGISTRY_DATABASE_URL` 环境变量将其指向注册表（参见 [docker-compose.yml](./docker-compose.yml) 中的可用示例）：

```bash
# Run latest stable release
docker run -p 8080:8080 ghcr.io/modelcontextprotocol/registry:latest

# Run latest from main branch (continuous deployment)
docker run -p 8080:8080 ghcr.io/modelcontextprotocol/registry:main

# Run specific release version
docker run -p 8080:8080 ghcr.io/modelcontextprotocol/registry:v1.0.0

# Run development build from main branch
docker run -p 8080:8080 ghcr.io/modelcontextprotocol/registry:main-20250906-abc123d
```

**可用标签：** 
- **Release 版本**：`latest`、`v1.0.0`、`v1.1.0` 等
- **持续集成（CI）**：`main`（最新主分支构建）
- **开发版本**：`main-<日期>-<SHA>`（特定提交构建）

</details>

#### 发布服务器

为了发布服务器，我们开发了一个简单的 CLI 工具。你可以通过以下方式运行：

```bash
# Build the latest CLI
make publisher

# Use it!
./bin/mcp-publisher --help
```

更多详情请参阅 [发布指南](./docs/modelcontextprotocol-io/quickstart.mdx)。

#### 其他命令

```bash
# Run lint, unit tests and integration tests
make check
```

此外还有几个对开发有帮助的命令。运行 `make help` 查看更多，或直接查看 [Makefile](./Makefile)。

<!--
For Claude and other AI tools: Always prefer make targets over custom commands where possible.
-->

## 架构设计

### 项目结构

```
├── cmd/                     # Application entry points
│   └── publisher/           # Server publishing tool
├── data/                    # Seed data
├── deploy/                  # Deployment configuration (Pulumi)
├── docs/                    # Documentation
├── internal/                # Private application code
│   ├── api/                 # HTTP handlers and routing
│   ├── auth/                # Authentication (GitHub OAuth, JWT, namespace blocking)
│   ├── config/              # Configuration management
│   ├── database/            # Data persistence (PostgreSQL)
│   ├── service/             # Business logic
│   ├── telemetry/           # Metrics and monitoring
│   └── validators/          # Input validation
├── pkg/                     # Public packages
│   ├── api/                 # API types and structures
│   │   └── v0/              # Version 0 API types
│   └── model/               # Data models for server.json
├── scripts/                 # Development and testing scripts
├── tests/                   # Integration tests
└── tools/                   # CLI tools and utilities
    └── validate-*.sh        # Schema validation tools
```

### 认证机制

发布功能支持多种认证方式：
- **GitHub OAuth** - 通过登录 GitHub 进行发布
- **GitHub OIDC** - 从 GitHub Actions 进行发布
- **DNS 验证** - 证明对域名及其子域名的所有权
- **HTTP 验证** - 证明对域名的所有权

注册表在发布时会校验命名空间的所有权。例如，若要发布：
- `io.github.domdomegg/my-cool-mcp` 需以 `domdomegg` 身份登录 GitHub，或作为 `domdomegg` 仓库的 GitHub Actions 运行
- `me.adamjones/my-cool-mcp` 需通过 DNS 或 HTTP Challenge 证明对 `adamjones.me` 的所有权

## 社区项目

查看 [社区项目](docs/community-projects.md)，探索由社区创建的与注册表相关的优秀工作。

## 更多文档

如果你的问题在此未得到解答，请参阅 [完整文档](./docs) 获取更多详情！
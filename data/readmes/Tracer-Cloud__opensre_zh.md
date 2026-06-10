<div align="center">

<p align="center">
  <img src="docs/logo/opensre-logo-white.svg" alt="OpenSRE" width="360" />
</p>

<h1>OpenSRE v0.1：构建你自己的 AI SRE 智能体</h1>

<p>用于 AI SRE（站点可靠性工程）智能体的开源框架，以及它们提升所需的训练与评估环境。连接你已运行的 60 多种工具，定义你自己的工作流程，并在自有基础设施上自主排查故障事件。</p>

<p align="center">
  <a href="https://github.com/Tracer-Cloud/opensre/actions/workflows/ci.yml?branch=main"><img src="https://img.shields.io/github/actions/workflow/status/Tracer-Cloud/opensre/ci.yml?branch=main&style=for-the-badge" alt="CI status"></a>
<a href="https://github.com/Tracer-Cloud/opensre/releases"><img src="https://img.shields.io/badge/status-pre--alpha-orange?style=for-the-badge" alt="Project status: pre-alpha"></a>
  <a href="https://github.com/Tracer-Cloud/opensre/blob/main/LICENSE"><img src="https://img.shields.io/badge/License-Apache%202.0-blue.svg?style=for-the-badge" alt="Apache 2.0 License"></a>
  <a href="https://discord.gg/7NTpevXf7w"><img src="https://img.shields.io/badge/Discord-Join%20Us-5865F2?style=for-the-badge&logo=discord&logoColor=white" alt="Discord"></a>
</p>

<p align="center">
  <a href="https://trendshift.io/repositories/25889" target="_blank">
    <img
      src="https://trendshift.io/api/badge/repositories/25889"
      alt="Tracer-Cloud%2Fopensre | Trendshift"
      style="height: 30px; width: auto;"
      height="30"
    />
  </a>
</p>

<p align="center">
  <strong>
    <a href="https://www.opensre.com/docs/quickstart">快速开始</a> ·
    <a href="https://www.opensre.com/docs">文档</a> ·
    <a href="https://opensre.com/docs/faq">常见问题</a> ·
    <a href="https://trust.tracer.cloud/">安全</a>
  </strong>
</p>

</div>

---

> 🚧 公开测试版（Public Alpha）：核心工作流可用于早期探索，但尚未完全稳定。项目正在积极开发中，API 和集成接口可能会发生变化。

---

## 目录

- [为什么选择 OpenSRE？](#why-opensre)
- [安装](#install)
- [快速开始](#quick-start)
- [部署](#deployment)
- [OpenSRE 工作原理](#how-opensre-works)
- [基准测试](#benchmark)
- [功能与集成](#capabilities--integrations)
- [贡献与开发](#contributing--development)
- [安全](#security)
- [遥测数据](#telemetry)
- [许可证](#license)
- [引用](#citations)

---

## 为什么选择 OpenSRE？

当生产环境出现故障时，证据通常分散在日志、指标、链路追踪、运行手册和 Slack 会话中。OpenSRE 是一个用于排查生产故障的 AI SRE 智能体开源框架，专为在自有基础设施上运行而设计。

我们致力于此是因为 SWE-bench<sup>1</sup> 为代码智能体提供了可扩展的训练数据和明确的反馈机制，而生产故障响应领域仍缺乏类似的基准。

分布式故障比本地代码任务更慢、噪声更大，且更难模拟和评估，这也是为什么 AI SRE（以及更广泛的用于生产环境调试的 AI）至今仍未被彻底解决。

OpenSRE 正在构建这一缺失的层级：

> 一个用于智能体基础设施故障响应的开源强化学习环境，提供端到端测试和针对真实生产故障的合成事件模拟

我们通过以下方式实现：

- 构建易于部署且可定制的 AI SRE 智能体，用于生产事件的调查与响应
- 运行带评分的合成根因分析（RCA）测试套件，验证根因准确性、必要证据及对抗性干扰项 [(tests/synthetic)](tests/synthetic/rds_postgres)
- 运行覆盖云原生场景的真实端到端测试，包括 Kubernetes、EC2、CloudWatch、Lambda、ECS Fargate 和 Flink [(tests/e2e)](tests/e2e)
- 保持语义化的测试目录命名规范，使端到端与合成、本地与云端的边界清晰可见 [(tests/README.md)](tests/README.md)

我们的使命是在此基础上构建 AI SRE 智能体，将其扩展至数千个真实的故障场景，并将 OpenSRE 打造为 AI SRE 领域的基准测试平台与训练场。

<sup>1</sup> https://arxiv.org/abs/2310.06770

---

## 安装

根安装程序会自动检测 Unix Shell 或 PowerShell。如果你希望获取来自 `main` 分支的最新滚动构建版本（而非最新稳定版），请添加 `--main` 参数。

最新稳定版：

```bash
curl -fsSL https://install.opensre.com | bash
```

来自 `main` 分支的最新构建：

```bash
curl -fsSL https://install.opensre.com | bash -s -- --main
```

Homebrew：

```bash
brew tap tracer-cloud/tap
brew install tracer-cloud/tap/opensre
```

Windows（PowerShell）：

```powershell
irm https://install.opensre.com | iex
```

<!--
```bash
pipx install opensre
``` -->

---

## 快速开始

仅需一次配置，即可选择你偏好的调查运行方式：

```bash
opensre onboard
```

**交互式 Shell** — 不输入任何子命令时，`opensre` 将启动一个 REPL（需要 TTY）。用自然语言描述故障事件、流式输出调查过程，并使用 `/help`、`/status`、`/clear`、`/reset`、`/trust`、`/effort`、`/exit` 等斜杠命令。`/effort` 用于设置 **OpenAI** 和 **Codex** 提供商的推理深度（支持 `low`、`medium`、`high`、`xhigh` 或 `max`；其他提供商将忽略此参数）。按 `Ctrl+C` 可取消正在进行的调查，且不会丢失会话状态。

```bash
opensre
```

**单次运行调查** —— 针对告警文件单次运行智能体：

```bash
opensre investigate -i tests/e2e/kubernetes/fixtures/datadog_k8s_alert.json
```

其他常用命令：

```bash
opensre update
opensre uninstall   # 移除 opensre 及所有本地数据
```

---

## 部署

使用仓库中的 `Dockerfile` 或托管应用主机（如 Railway、EC2、ECS 或 Vercel）将 OpenSRE 部署为标准的 Python/FastAPI 运行时。设置 `LLM_PROVIDER` 及对应的 API 密钥（参见 `.env.example`）；需要持久化存储的托管环境还需配置 `DATABASE_URI` 和 `REDIS_URI`。

**[完整部署步骤、Railway 注意事项及 `opensre remote ops` 命令说明 → docs/DEVELOPMENT.md](docs/DEVELOPMENT.md#deployment)**

---

## OpenSRE 工作原理

<img
  src="https://github.com/user-attachments/assets/936ab1f2-9bda-438d-9897-e8e9cd98e335"
  width="1064"
  height="568"
  alt="opensre-how-it-works-github"
/>

当告警触发时，OpenSRE 会自动执行以下操作：

1. **获取**告警上下文及相关联的日志、指标和链路追踪数据
2. **推理**已连接的系统以识别异常
3. **生成**包含可能根因的结构化调查报告
4. **建议**后续步骤，并可选择性地执行修复操作
5. **发布**摘要至 Slack 或 PagerDuty —— 无需切换上下文即可直接查看

关于移除旧版图（graph）和链式（chain）框架层后的当前代码级智能体架构，请参阅 [AGENT_ARCHITECTURE.md](AGENT_ARCHITECTURE.md)。

---

## 基准测试

使用 **`make benchmark`** 重新生成数据；通过 **`make benchmark-update-readme`** 从缓存结果刷新此表格。详情见 **[docs/DEVELOPMENT.md](docs/DEVELOPMENT.md#benchmark)**。

<!-- BENCHMARK-START -->

_No benchmark results yet._

<!-- BENCHMARK-END -->

---

## 功能与集成

|                                          |                                                                                  |
| ---------------------------------------- | -------------------------------------------------------------------------------- |
| 🔍 **结构化事件调查**               | 跨所有信号源的关联根因分析                           |
| 📋 **运行手册感知推理**           | OpenSRE 会读取你的运行手册并自动应用                       |
| 🔮 **预测性故障检测**          | 在故障触发告警前捕获潜在问题                                       |
| 🔗 **数据支撑的根因**        | 每项结论均附带支撑数据                                 |
| 🤖 **完整的 LLM 灵活性**              | 自由选用模型 —— Anthropic、OpenAI、Ollama、Gemini、OpenRouter、NVIDIA NIM |

OpenSRE 已集成 **60+** 工具，涵盖大语言模型（LLM）、可观测性平台、云基础设施、数据平台、事件管理及 MCP。完整矩阵（含路线图链接）位于 **[产品文档](https://www.opensre.com/docs)**；随着项目发展，仓库内也维护着详细目录。

---

## 集成

OpenSRE 连接了现代云技术栈中的 60+ 工具和服務，涵盖 LLM 提供商、可观测性平台、基础设施、数据库及事件管理系统。

| Category                | Integrations                                                                                                                                                                                                                                                                                                                                           | Roadmap                                                                                                                                                                                                                                                            |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **AI / LLM 提供商**  | Anthropic · OpenAI · Ollama · Google Gemini · OpenRouter · NVIDIA NIM · Bedrock                                                                                                                                                                                                                                                                        |                                                                                                                                                                                                                                                                    |
| **可观测性 (Observability)**       | <img src="docs/assets/icons/grafana.webp" width="16"> Grafana (Loki · Mimir · Tempo) · <img src="docs/assets/icons/datadog.svg" width="16"> Datadog · Honeycomb · Coralogix · <img src="docs/assets/icons/cloudwatch.png" width="16"> CloudWatch · <img src="docs/assets/icons/sentry.png" width="16"> Sentry · Elasticsearch · Better Stack Telemetry | [Splunk](https://github.com/Tracer-Cloud/opensre/issues/319) · [New Relic](https://github.com/Tracer-Cloud/opensre/issues/139) · [Victoria Logs](https://github.com/Tracer-Cloud/opensre/issues/126)                                                               |
| **基础设施 (Infrastructure)**      | <img src="docs/assets/icons/kubernetes.png" width="16"> Kubernetes · <img src="docs/assets/icons/aws.png" width="16"> AWS (S3 · Lambda · EKS · EC2 · Bedrock) · <img src="docs/assets/icons/gcp.jpg" width="16"> GCP · <img src="docs/assets/icons/azure.png" width="16"> Azure                                                                        | [Helm](https://github.com/Tracer-Cloud/opensre/issues/321) · [ArgoCD](https://github.com/Tracer-Cloud/opensre/issues/320)                                                                                                                                          |
| **数据库 (Database)**            | MongoDB · ClickHouse · PostgreSQL · MySQL · MariaDB · MongoDB Atlas · Azure SQL · Snowflake                                                                                                                                                                                                                                                            | [RDS](https://github.com/Tracer-Cloud/opensre/issues/125)                                                                                                                                                                                                          |
| **数据平台 (Data Platform)**       | Apache Airflow · Apache Kafka · Apache Spark · Prefect · RabbitMQ                                                                                                                                                                                                                                                                                      |                                                                                                                                                                                                                                                                    |
| **开发工具 (Dev Tools)**           | <img src="docs/assets/icons/github.webp" width="16"> GitHub · GitHub MCP · Bitbucket · GitLab                                                                                                                                                                                                                                                          |                                                                                                                                                                                                                                                                    |
| **事件管理 (Incident Management)** | <img src="docs/assets/icons/pagerduty.png" width="16"> PagerDuty · Opsgenie · Jira · Alertmanager                                                                                                                                                                                                                                                      | [Trello](https://github.com/Tracer-Cloud/opensre/issues/361) · [ServiceNow](https://github.com/Tracer-Cloud/opensre/issues/314) · [incident.io](https://github.com/Tracer-Cloud/opensre/issues/317) · [Linear](https://github.com/Tracer-Cloud/opensre/issues/124) |
| **通信 (Communication)**       | <img src="docs/assets/icons/slack.png" width="16"> Slack · Google Docs · Discord · Telegram                                                                                                                                                                                                                                                            | [Notion](https://github.com/Tracer-Cloud/opensre/issues/286) · [Teams](https://github.com/Tracer-Cloud/opensre/issues/138) · [WhatsApp](https://github.com/Tracer-Cloud/opensre/issues/360) · [Confluence](https://github.com/Tracer-Cloud/opensre/issues/313)     |
| **智能体部署 (Agent Deployment)**    | <img src="docs/assets/icons/vercel.png" width="16"> Vercel · <img src="docs/assets/icons/aws.png" width="16"> EC2 · <img src="docs/assets/icons/aws.png" width="16"> ECS · Railway                                                                                                  |                                                                                                                                                                                                                                                                    |
| **协议 (Protocols)**           | <img src="docs/assets/icons/mcp.svg" width="16"> MCP · <img src="docs/assets/icons/acp.png" width="16"> ACP · <img src="docs/assets/icons/openclaw.jpg" width="16"> OpenClaw                                                                                                                                                                           |                                                                                                                                                                                                                                                                    |

OpenSRE 由社区共同构建。想寻找安全的入门贡献机会？可浏览 [`good first issue`](https://github.com/Tracer-Cloud/opensre/issues?q=is%3Aissue+is%3Aopen+label%3A%22good+first+issue%22) 标签的议题，或查看 [Good First Issues 指南](docs/good-first-issues/README.md)。完整工作流请参阅 **[CONTRIBUTING.md](CONTRIBUTING.md)**。

**本地环境配置：** **[SETUP.md](SETUP.md)**（支持所有平台、Windows 及 MCP/OpenClaw）。

**在仓库中开发：** **[docs/DEVELOPMENT.md](docs/DEVELOPMENT.md)**（源码安装、CI 一致性检查、开发容器、基准测试、部署详情及遥测参考）。

<p>
  <a href="https://discord.gg/7NTpevXf7w">
    <img src="https://img.shields.io/badge/Join%20our%20Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white" alt="Join our Discord" />
  </a>
</p>

<p align="center">
  <a href="https://www.star-history.com/#Tracer-Cloud/opensre&Date">
    <img src="https://api.star-history.com/svg?repos=Tracer-Cloud/opensre&type=Date" alt="Star History Chart">
  </a>
</p>

感谢这些出色的贡献者：

<!-- readme: contributors -start -->
<a href="https://github.com/Tracer-Cloud/opensre/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=Tracer-Cloud/opensre&max=200" alt="Contributors" />
</a>
<!-- readme: contributors -end -->

---

## 安全

OpenSRE 专为生产环境设计：提供结构化且可审计的 LLM Prompt，默认在本地处理对话记录，且不静默批量导出原始日志。有关负责任的安全披露机制，请参阅 **[SECURITY.md](SECURITY.md)**。

---

## 遥测数据

PostHog（产品分析）和 Sentry（错误追踪）**默认启用，但支持退出关闭**。快速禁用方法：

```bash
export OPENSRE_NO_TELEMETRY=1
```

**[完整配置矩阵、DSN 覆盖及本地事件日志记录 → docs/DEVELOPMENT.md](docs/DEVELOPMENT.md#telemetry-and-privacy)**

---

## 许可证

Apache 2.0 —— 详见 [LICENSE](LICENSE)。

## 引用

<sup>1</sup> https://arxiv.org/abs/2310.06770
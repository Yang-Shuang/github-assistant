<div align="center">
<a href ="https://hatchet.run?utm_source=github&utm_campaign=readme">
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./assets/hatchet_logo_dark.svg">
  <img width="200" alt="Hatchet Logo" src="./assets/hatchet_logo_light.svg">
</picture>
</a>

### 用于后台任务、AI Agent 和持久化工作流的编排引擎

[![Docs](https://img.shields.io/badge/docs-docs.hatchet.run-3F16E4)](https://docs.hatchet.run) [![License: MIT](https://img.shields.io/badge/License-MIT-purple.svg)](https://opensource.org/licenses/MIT) [![Go Reference](https://pkg.go.dev/badge/github.com/hatchet-dev/hatchet.svg)](https://pkg.go.dev/github.com/hatchet-dev/hatchet) [![NPM Downloads](https://img.shields.io/npm/dm/%40hatchet-dev%2Ftypescript-sdk)](https://www.npmjs.com/package/@hatchet-dev/typescript-sdk)

[![Discord](https://img.shields.io/discord/1088927970518909068?style=social&logo=discord)](https://hatchet.run/discord)
[![Twitter](https://img.shields.io/twitter/url/https/twitter.com/hatchet-dev.svg?style=social&label=Follow%20%40hatchet-dev)](https://twitter.com/hatchet_dev)
[![GitHub Repo stars](https://img.shields.io/github/stars/hatchet-dev/hatchet?style=social)](https://github.com/hatchet-dev/hatchet)

  <p align="center">
    <a href="https://cloud.hatchet.run">Hatchet Cloud</a>
    ·
    <a href="https://docs.hatchet.run">Documentation</a>
    ·
    <a href="https://hatchet.run">Website</a>
    ·
    <a href="https://github.com/hatchet-dev/hatchet/issues">Issues</a>
  </p>

</div>

### 什么是 Hatchet？

Hatchet 是一个用于大规模编排后台任务、AI Agent 和持久化工作流（Durable Workflows）的平台。它支持使用 Python、TypeScript、Go 和 Ruby 编写的应用程序，可通过 [Hatchet Cloud](https://cloud.hatchet.run) 作为托管服务使用，或进行[自托管部署](https://docs.hatchet.run/self-hosting)。Hatchet 提供了完整的平台能力，涵盖任务队列、自动重试、持久化保障、实时监控、告警和日志记录。

### 快速上手

快速体验 Hatchet 的最佳方式是注册 [Hatchet Cloud](https://cloud.hatchet.run)！即使你计划自托管，我们也推荐先试用一下，以便直观了解完整部署的 Hatchet 平台长什么样。

要在本地运行 Hatchet，最快的设置方式是安装 Hatchet CLI（支持 MacOS、Linux 或 WSL）——注意：这需要本地已安装 [Docker](https://www.docker.com/get-started) 才能正常工作：

```sh
curl -fsSL https://install.hatchet.run/install.sh | bash
hatchet --version
hatchet server start
```

如需查看自托管和云服务使用的完整文档，请查阅[官方文档](https://docs.hatchet.run)。

### 何时使用 Hatchet？

你可以使用 Hatchet 运行后台任务、AI Agent 或其他类型的长生命周期工作流。它旨在为那些对**正确性、可靠性、水平扩展能力和可观测性**有严格要求的系统提供功能完备的解决方案。从技术角度来看，它与其他方案的不同之处在于：它将 Postgres 作为任务运行时和可观测性系统的持久化层（Durability Layer），这使得自托管变得尤为简单。

如需了解使用 Hatchet 构建工作流的端到端示例，请参阅我们的[实战指南](https://docs.hatchet.run/cookbooks)。

### Hatchet 功能特性

#### 后台任务

- [后台任务](https://docs.hatchet.run/v1/tasks)：Hatchet 支持将一次性后台任务定义为简单的函数。它同时支持“即发即忘”（fire-and-forget）和“带订阅的等待结果”（fire-and-wait）模式的任务
- [重试策略](https://docs.hatchet.run/v1/retry-policies)：灵活可配置的重试机制，并可选配[指数退避](https://docs.hatchet.run/v1/retry-policies#exponential-backoff)算法
- [定时任务](https://docs.hatchet.run/v1/cron-runs) 和 [计划运行](https://docs.hatchet.run/v1/scheduled-runs)：用于在未来指定时间点调度任务执行
- [任务路由](https://docs.hatchet.run/v1/advanced-assignment/worker-affinity)：基于严格条件（如 **Worker 标签**）或更复杂的加权调度规则（使用 **Worker 亲和性**）进行分配
- [事件触发](https://docs.hatchet.run/v1/events) 和 [监听器](https://docs.hatchet.run/v1/durable-event-waits)：用于构建事件驱动的高度分布式系统
- [Webhook 触发](https://docs.hatchet.run/v1/webhooks)：便于从上游数据源轻松触发 Hatchet 任务

#### 任务编排与工作流

- [持久化任务](https://docs.hatchet.run/v1/durable-tasks)：用于构建容错能力强、可长周期运行的工作流，并能轻松从故障中恢复
- [有向无环图（DAG）](https://docs.hatchet.run/v1/directed-acyclic-graphs)：用于构建数据管道和简单工作流。请参阅[我们的指南](https://docs.hatchet.run/cookbooks/durable-tasks-vs-dags) 了解如何在持久化任务和 DAG 之间做出选择
- 使用 [持久化休眠](https://docs.hatchet.run/v1/durable-sleep)、[事件等待](https://docs.hatchet.run/v1/durable-event-waits) 或两者结合，实现复杂的暂停/恢复条件控制

#### 扩展能力

- [优先级调度](https://docs.hatchet.run/v1/priority)：确保关键任务优先于对延迟不敏感的任务（如数据回填作业）运行
- [速率限制](https://docs.hatchet.run/v1/rate-limits)：用于应对第三方 API 调用，或通过 **动态速率限制** 实现按用户维度的限流控制
- [公平调度](https://docs.hatchet.run/v1/concurrency)：基于 Hatchet 的并发策略，可根据动态键（Dynamic Keys）为任务设置并发上限
- [Worker 槽位管理](https://docs.hatchet.run/v1/workers#slots)：确保 Worker 不会承担超出其处理能力的工作量

#### 监控、可观测性与管理

- 提供带告警、监控和日志功能的实时 Web UI
- [OpenTelemetry](https://docs.hatchet.run/v1/opentelemetry)（支持使用 Hatchet 内置的 Collector 或外部数据源）
- [Prometheus 指标](https://docs.hatchet.run/v1/prometheus-metrics)
- 默认支持**多租户（Multi-tenant）**，单个 Hatchet 实例即可服务多个团队
- 用户与角色管理

#### [Hatchet Cloud](https://cloud.hatchet.run) 专属功能

- 自动扩缩容与按需付费计划
- 多区域部署
- 单点登录（SSO）
- 监控、日志和可观测性性能优化

### 文档

最新文档请访问：https://docs.hatchet.run。

### 社区与支持

- [Discord](https://discord.gg/ZMeUafwH89) - 用于与核心维护者交流及社区互动
- [Github Issues](https://github.com/hatchet-dev/hatchet/issues) - 提交 Bug 报告
- [Github Discussions](https://github.com/hatchet-dev/hatchet/discussions) - 发起适合异步沟通的深入技术讨论
- [Email](mailto:contact@hatchet.run) - 获取 Hatchet Cloud 技术支持，以及处理账单、数据删除等事宜

### Hatchet 对比

<details>
<summary>Hatchet vs 持久化执行平台（Temporal, DBOS）</summary>

####

Hatchet 的[持久化任务](https://docs.hatchet.run/v1/durable-tasks)功能可作为 Temporal 或 DBOS 工作流的无缝替换方案。此外你还将获得：

- 基于 OpenTelemetry 实现持久化任务的端到端可观测性，涵盖监控与日志
- 面向大规模运行的内置特性（如限流、复杂路由、Worker 级槽位控制）
- 开箱即用的多租户及用户角色支持

除了让持久化执行更易上手外，Hatchet 还可作为通用消息队列、基于 DAG 的编排器或持久化执行引擎使用（甚至三者兼用），帮助团队将异步与后台处理集中到一个平台上。

</details>

<details>

<summary>Hatchet vs 传统任务队列（Celery, BullMQ）</summary>

####

BullMQ 和 Celery 等传统任务队列通常以牺牲持久性为代价换取吞吐量。任务仅在代理端（通常为 Redis 或 RabbitMQ）执行期间保持持久化，完成后即被清除。这使得构建复杂工作流变得困难，因为缺乏持久的中间状态。同时，这也导致恢复和重放已失败并从队列中移除的任务非常棘手，往往需要开发自定义的管理工具来配合这些库进行大规模运维。

相比之下，Hatchet 是一个**持久化任务队列**，它会记录所有执行的历史记录（在设定的保留期内），从而便于监控、调试和实现持久化任务特性。Hatchet 的持久化功能会带来一定开销：虽然经过负载测试可支持每秒 10k 个任务，但其资源消耗高于基于 Redis 或 RabbitMQ 的系统（后者可达到更高的吞吐量）。

</details>

<details>

<summary>Hatchet vs 基于 DAG 的平台（Airflow, Prefect, Dagster）</summary>

####

这些工具通常面向数据工程师设计，并非专为高流量应用的一部分而构建。它们通常延迟较高、成本较大，主要卖点是内置了常见数据存储和连接器的集成。

**何时选择 Hatchet：** 当你希望使用基于 DAG 的框架、编写自定义集成与函数，且需要更高吞吐量（>100/s）时。

**何时选择其他 DAG 平台：** 当你希望开箱即用多种数据存储和连接器时。

</details>

### Issues（问题反馈）

请通过 GitHub Issues 提交你遇到的任何 Bug。

### 参与贡献

欢迎在 [Discord](https://discord.gg/ZMeUafwH89) 的 `#contributing` 频道告诉我们你想参与的方向。这将帮助我们明确项目演进路线，并让协作更加顺畅！
<p align="center">
  <picture>
    <source srcset=".github/RisingWave-logo-dark.svg" width="500px" media="(prefers-color-scheme: dark)">
    <img src=".github/RisingWave-logo-light.svg" width="500px">
  </picture>
</p>


<div align="center">

### 🌊 面向智能体（Agentic AI）的事件流处理平台

</div>
<p align="center">
  <a href="https://docs.risingwave.com/">文档</a> | <a href="https://docs.risingwave.com/get-started/rw-benchmarks-stream-processing">基准测试</a> | <a href="https://docs.risingwave.com/demos/overview">演示</a> | <a href="https://risingwave.com/customers/">客户案例</a>
</p>

<p align="center">

<div align="center">
  <a
    href="https://github.com/risingwavelabs/risingwave/releases/latest"
    target="_blank"
  >
    <img alt="Release" src="https://img.shields.io/github/v/release/risingwavelabs/risingwave.svg?sort=semver" />
  </a>
  <a
    href="https://go.risingwave.com/slack"
    target="_blank"
  >
    <img alt="Slack" src="https://badgen.net/badge/Slack/Join%20RisingWave/0abd59?icon=slack" />
  </a>
  <a
    href="https://x.com/risingwavelabs"
    target="_blank"
  >
    <img alt="X" src="https://img.shields.io/twitter/follow/risingwavelabs" />
  </a>
  <a
    href="https://www.youtube.com/@risingwave-labs"
    target="_blank"
  >
    <img alt="YouTube" src="https://img.shields.io/youtube/channel/views/UCsHwdyBRxBpmkA5RRd0YNEA" />
  </a>
</div>

RisingWave 是一款面向智能体（Agentic AI）的事件流处理平台。它持续从数据库、事件流和 Webhook 中摄取数据，进行增量计算，并以低延迟提供最新结果。RisingWave 用单一系统取代了传统的流式数据处理栈（例如 Debezium + Kafka + Flink + 服务数据库）。

![RisingWave](./docs/dev/src/images/architecture_20250609.jpg)

---

## 60秒快速体验

```shell
curl -L https://risingwave.com/sh | sh
```

如需使用 Docker、Kubernetes 或其他部署方式，请参阅[快速入门指南](https://docs.risingwave.com/get-started/quickstart)。

---

## 核心痛点

Agent 和实时应用需要始终最新且支持低延迟查询的数据。传统方案通常将用于 CDC（变更数据捕获）的 Debezium、用于传输的 Kafka、用于处理的 Flink 以及用于查询的服务数据库串联起来。每次数据流转都会增加延迟，且每个系统都会带来额外的运维开销。

RisingWave 取代了整个技术栈：涵盖数据摄取、处理、服务与存储。

---

## 工作原理

### 统一接入任意数据源

RisingWave 支持全谱系的数据摄入：

- **Webhook**：通过 HTTP 协议从 SaaS 应用和外部系统接收事件
- **数据库变更**：通过读取事务日志，原生支持 PostgreSQL、MySQL 等数据库的 CDC
- **事件流**：支持 Kafka、Pulsar、Kinesis 及其他消息队列中间件
- **历史数据**：从 S3、数据仓库及其他存储系统进行批量导入

所有数据源均通过统一的 SQL 接口进行访问。流数据和表数据可以自由地进行 JOIN 操作。

### 持续增量计算

RisingWave 对摄入的数据执行增量计算。当上游数据发生变化时，仅重新计算受影响的结果。端到端的数据新鲜度延迟低于 100 毫秒。

这是 RisingWave 所有功能背后的核心机制：物化视图始终保持最新，无需每次查询都进行全量重算。

### 低延迟查询服务

查询结果存储在 RisingWave 的内部行存储中，p99 延迟仅为 10~20 毫秒。Agent 和应用程序可直接使用标准 SQL 查询该层数据。无需轮询、预热缓存或管理 TTL（过期时间）。

### 基于 Apache Iceberg™ 的存储层

为满足长期数据保留和分析查询需求，RisingWave 将数据写入 Apache Iceberg™ 表。它直接托管 Iceberg REST Catalog，并自动处理表维护工作（如压缩、小文件优化、快照清理），无需依赖外部工具。Iceberg 查询通过向量化查询引擎 [Apache DataFusion](https://datafusion.apache.org/) 执行。由于 Iceberg 是开放格式，数据同样可被 Spark、Trino、DuckDB 及其他引擎读取。

行存储与 Iceberg 层各司其职：行存储用于低延迟查询服务，Iceberg 用于持久化、开放格式的存储与分析查询。RisingWave 统一管理这两层架构。

---

## 典型应用场景

- **监控与告警**：持续将流式指标与阈值进行比对评估
- **特征库（Feature Store）**：在统一的数据管道中计算批量与流式特征，并通过同一系统提供服务
- **实时仪表盘**：基于增量更新的物化视图，无需定时刷新
- **实时数据增强**：在投递下游前，将实时事件与历史参考数据进行动态关联
- **流式湖仓一体（Streaming Lakehouse）**：以精确一次语义持续写入开放格式表，并自动管理压缩与快照

---

## 核心设计理念

### 极致的成本效益

内部状态、表和物化视图均存储在对象存储（如 S3）中，其成本仅为内存的约 1/100。这使得系统能够实现弹性扩缩容而无需数据重平衡，并在秒级完成故障恢复。针对对延迟敏感的工作负载，[弹性磁盘缓存](https://docs.risingwave.com/get-started/disk-cache) 可将热点数据驻留在本地 SSD 或 EBS 上，将 p99 查询延迟保持在 10~20 毫秒。

### 面向人类与 Agent 的原生体验

RisingWave 采用 PostgreSQL 网络协议进行连接，完全兼容 psql、JDBC 及任何支持 PostgreSQL 的工具生态。针对 Agent，RisingWave 提供了 MCP Server、CLI 命令行工具以及 Skills（技能），使 Agent 无需定制开发即可直接查询和操作 RisingWave。

### 开放生态

RisingWave [原生集成 Apache Iceberg™](https://docs.risingwave.com/iceberg/overview)，支持持续流式数据摄入、通过 DataFusion 直接读取以及自动化的表维护。Iceberg 中的数据采用开放格式，可被任何兼容的查询引擎访问。

---

## 部署方式

[**RisingWave Cloud**](https://cloud.risingwave.com) 为托管服务选项。

如需自托管（Self-hosted）：
- [Docker Compose](https://docs.risingwave.com/deploy/risingwave-docker-compose/)
- [Kubernetes with Helm](https://docs.risingwave.com/deploy/risingwave-k8s-helm/)
- [Kubernetes with Operator](https://docs.risingwave.com/deploy/risingwave-kubernetes/)

---

## 社区交流

欢迎加入我们的 [Slack](https://go.risingwave.com/slack)，参与提问、讨论与贡献。

---

## 遥测数据（Telemetry）

RisingWave 使用 [Scarf](https://scarf.sh/) 收集匿名的安装分析数据，并汇总匿名使用情况统计以改进产品。用户可随时选择退出（opt-out）。详情请参阅[遥测文档](https://docs.risingwave.com/operate/telemetry/)。

---

## 许可证

Apache License 2.0。详见 [LICENSE](LICENSE)。

## 参与贡献

请参阅 [RisingWave 开发者指南](https://risingwavelabs.github.io/risingwave/)。
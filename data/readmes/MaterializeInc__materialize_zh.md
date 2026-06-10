[![Build status](https://badge.buildkite.com/97d6604e015bf633d1c2a12d166bb46f3b43a927d3952c999a.svg?branch=main)](https://buildkite.com/materialize/test)
[![Doc reference](https://img.shields.io/badge/doc-reference-orange)](https://materialize.com/docs)
[![Chat on Slack](https://img.shields.io/badge/chat-on%20slack-purple)](https://materialize.com/s/chat)

[<img src="https://github.com/MaterializeInc/materialize/assets/23521087/39270ecb-7ac4-4829-b98b-c5b5699a16b8" width=35%>](https://materialize.com)

Materialize 是一个实时数据集成平台，能够创建并持续更新来自您整个组织的交易型数据的一致视图。其 SQL 接口降低了使用门槛，使提供和访问实时数据的能力得以普及。Materialize 可部署在您基础设施运行的任何地方。

使用 Materialize 您可以执行以下操作：为 AI/RAG 管道提供新鲜上下文、驱动运营仪表板，以及打造更具动态性的客户体验，而无需构建耗时且定制的数据管道。


采用 Materialize 的三种最常见模式如下：

- 查询卸载（Query Offload / CQRS） - 比只读副本更高效地扩展复杂读取查询，并避免缓存失效带来的麻烦。
- 集成中心（Integration Hub / ODS） - 从多个数据源提取、加载数据并进行增量转换。创建可直接查询或向下游推送的数据实时视图。
- 运营数据网格（Operational Data Mesh / ODM） - 使用 SQL 创建并提供实时的强一致（strongly consistent）数据产品，以简化跨服务和领域间的协调工作。


## Get started

准备好试用 Materialize 了吗？您可以[注册](https://materialize.com/register/)免费云版试用，或[下载](https://materialize.com/download/)我们的社区版（对于使用内存小于 24 GiB 且磁盘小于 48 GiB 的部署，永久免费！）。

有问题？我们非常乐意听取你的意见：
  * [加入我们的 Slack](https://materialize.com/s/chat)
  * [给我们发送邮件](https://materialize.com/contact/)

## About

Materialize 专注于以极低延迟提供正确且[一致（consistent）](https://materialize.com/docs/overview/isolation-level/)的答案，不要求你接受近似答案或最终一致性。即使连接来自[多个上游系统](https://materialize.com/blog/strong-consistency-in-materialize/)的数据，这一保证依然成立。每当 Materialize 回答查询时，该答案都是基于您数据某个特定（且近期）版本上的正确结果。Materialize 通过将你的 SQL 查询重构为*数据流（dataflows）*来实现这一切，从而能够高效响应数据的实时变化。

我们的全托管服务采用云原生架构，具备通过多活复制实现的**高可用性**、通过跨多台机器无缝扩展数据流实现的**水平可扩展性**，以及利用云对象存储（例如 Amazon S3）实现的**近乎无限的存储空间**。你可以使用我们的企业版或社区版自行管理 Materialize。

我们支持大部分 PostgreSQL 功能，并正在积极扩展对更多内置 PostgreSQL 函数的支持。如果你有改进建议，请提交 Issue！

## Get data in

Materialize 可直接读取来自 [PostgreSQL](https://materialize.com/docs/sql/create-source/postgres/) 或 [MySQL](https://materialize.com/docs/sql/create-source/mysql/) 的复制流，[Kafka](https://materialize.com/docs/sql/create-source/kafka/)（以及其他兼容 Kafka API 的系统如 [Redpanda](https://materialize.com/docs/integrations/redpanda/)），或通过 Webhook 从 SaaS 应用读取数据。

## Transform, manipulate, and read your data

数据导入后，你可通过 PostgreSQL 协议定义视图并执行读取操作。使用你喜欢的 SQL 客户端即可，包括你可能已安装在系统上的 `psql`。在生产环境中使用 Materialize 的客户倾向于使用 [dbt Core](https://www.getdbt.com/)。

Materialize 支持丰富的 SQL 功能特性，均基于 PostgreSQL 方言和协议：

-   连接（Joins），连接，再连接！Materialize 支持多列连接条件、多路连接、自连接、交叉连接、内连接、外连接等。
-   增量连接（Delta-joins）可避免中间状态膨胀，相比仅能规划嵌套二元连接的系统表现更佳——已在多达 64 个关系的连接测试中得到验证。
-   支持子查询。Materialize 的 SQL 优化器开箱即用即可执行子查询去相关处理（subquery decorrelation），无需手动将子查询重写为连接操作。
-   Materialize 可在任意插入、更新和删除操作下增量维护视图。无需使用通配符 `*`。
-   所有聚合函数：`min`、`max`、`count`、`sum`、`stddev` 等。
-   `HAVING`
-   `ORDER BY`
-   `LIMIT`
-   `DISTINCT`
-   PostgreSQL 方言中的 JSON 支持，包括 `->`、`->>`、`@>`、`?`、`jsonb_array_element`、`jsonb_each` 等操作符和函数。Materialize 会自动规划横向连接（lateral joins）以高效支持 `jsonb_each`。
-   视图套视图，无限嵌套！
-   具有重叠子计划的多个视图可共享底层索引以提升空间和计算效率，因此只需声明式地定义*你想要什么*，剩下的优化维护工作交给我们。

我们还扩展了 SQL 支持以启用[递归](https://materialize.com/blog/recursion-in-materialize/)功能，支持对树和图结构进行增量更新。

### Just show us what it can do!

这里有一个在 Materialize 中运行良好的示例连接查询，即 `TPC-H` 的查询 15：

```sql
CREATE SOURCE tpch
  FROM LOAD GENERATOR TPCH (SCALE FACTOR 1)
  FOR ALL TABLES;

-- Views define commonly reused subqueries.
CREATE VIEW revenue (supplier_no, total_revenue) AS
    SELECT
        l_suppkey,
        SUM(l_extendedprice * (1 - l_discount))
    FROM
        lineitem
    WHERE
        l_shipdate >= DATE '1996-01-01'
        AND l_shipdate < DATE '1996-01-01' + INTERVAL '3' month
    GROUP BY
        l_suppkey;

-- The MATERIALIZED keyword is the trigger to begin
-- eagerly, consistently, and incrementally maintaining
-- results that are stored directly in durable storage.
CREATE MATERIALIZED VIEW tpch_q15 AS
  SELECT
    s_suppkey,
    s_name,
    s_address,
    s_phone,
    total_revenue
FROM
    supplier,
    revenue
WHERE
    s_suppkey = supplier_no
    AND total_revenue = (
        SELECT
            max(total_revenue)
        FROM
            revenue
    )
ORDER BY
    s_suppkey;

-- Creating an index keeps results always up to date and in memory.
-- In this example, the index will allow for fast point lookups of
-- individual supply keys.
CREATE INDEX tpch_q15_idx ON tpch_q15 (s_suppkey);
```

对底层表（`lineitem` 和 `supplier`）流式执行插入、更新和删除操作后，Materialize 会持续增量更新物化视图。你可以直接输入 `SELECT * FROM tpch_q15`，并立即看到最新结果！

## Get data out

**基于拉取（Pull-based）**：使用任何语言/环境中的 PostgreSQL 兼容驱动程序对您的视图执行 `SELECT` 查询。告诉它们正在与 PostgreSQL 数据库通信即可，无需了解其他细节。这对于直接将服务和 BI 工具指向 Materialize 特别有帮助。

**基于推送（Push-based）**：直接使用 `SUBSCRIBE` 监听变更，或配置 Materialize 在视图发生变化时将结果流式传输到 Kafka 主题中。你也可以将更新内容复制到对象存储中。

## Documentation

请查阅[我们的文档](https://materialize.com/docs/)。

## License

Materialize 以自托管产品和全托管云服务的形式提供，采用[基于积分的付费模式](https://materialize.com/pricing/)。价格包含专有的云原生功能，如水平可扩展性、高可用性以及 Web 管理控制台。

我们坚信推动人类知识的边界。为此，独立数据库引擎的源代码在[本仓库](https://github.com/MaterializeInc/materialize)中公开提供，并根据 [BSL 1.1](LICENSE) 许可协议发布，4 年后转换为开源 Apache 2.0 许可证。正如 BSL 所述，在单节点上使用独立数据库引擎将永久免费。

Materialize 依赖于许多开源的 Rust crate（依赖包）。我们维护了[这些 crate 及其许可协议的列表](https://dev.materialize.com/licenses.html)，包含指向其源代码仓库的链接。

## For developers

Materialize 主要由 Rust 编写。

开发者可在 [doc/developer](doc/developer) 查阅文档，Rust API 文档托管于 <https://dev.materialize.com/api/rust/>。

欢迎贡献代码。潜在的外部贡献者可参考 [D-good for external contributors](https://github.com/MaterializeInc/materialize/discussions/categories/contribute-to-materialize?discussions_q=is%3Aopen+category%3A%22Contribute+to+Materialize%22+label%3A%22D-good+for+external+contributors%22) 讨论标签。更多指导请参见 [CONTRIBUTING.md](https://github.com/MaterializeInc/materialize/blob/main/CONTRIBUTING.md)。

## Credits

Materialize 由[一支开发者团队](https://github.com/MaterializeInc/materialize/graphs/contributors)和一位机器人精心打造。[加入我们](https://materialize.com/careers/)吧！
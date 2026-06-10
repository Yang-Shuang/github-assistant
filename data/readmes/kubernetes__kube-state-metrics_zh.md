# 概述

[![Build Status](https://github.com/kubernetes/kube-state-metrics/workflows/continuous-integration/badge.svg)](https://github.com/kubernetes/kube-state-metrics/actions)
[![Go Report Card](https://goreportcard.com/badge/github.com/kubernetes/kube-state-metrics)](https://goreportcard.com/report/github.com/kubernetes/kube-state-metrics)
[![Go Reference](https://pkg.go.dev/badge/github.com/kubernetes/kube-state-metrics.svg)](https://pkg.go.dev/github.com/kubernetes/kube-state-metrics)
[![govulncheck](https://github.com/kubernetes/kube-state-metrics/actions/workflows/govulncheck.yml/badge.svg)](https://github.com/kubernetes/kube-state-metrics/actions/workflows/govulncheck.yml)
[![OpenSSF Best Practices](https://www.bestpractices.dev/projects/8696/badge)](https://www.bestpractices.dev/projects/8696)
[![OpenSSF Scorecard](https://api.securityscorecards.dev/projects/github.com/kubernetes/kube-state-metrics/badge)](https://api.securityscorecards.dev/projects/github.com/kubernetes/kube-state-metrics)

`kube-state-metrics`（简称 KSM）是一个简单的服务，它监听 Kubernetes API 服务器并生成关于对象状态的指标（metrics）。（详见下方“指标”部分中的示例。）它不关注单个 Kubernetes 组件的健康状况，而是关注内部各种对象（如部署、节点和 Pod）的运行状态。

`kube-state-metrics` 旨在从未经修改的 Kubernetes API 对象直接生成指标。这确保了 `kube-state-metrics` 提供的功能与 Kubernetes API 对象本身具有相同的稳定性等级。反过来，这也意味着在某些情况下，`kube-state-metrics` 显示的值可能与 `kubectl` 不完全相同，因为 `kubectl` 会应用某些启发式逻辑来显示易于理解的消息。`kube-state-metrics` 暴露的是未经修改的原始数据，这样用户就可以获取所需的全部数据，并按需自行进行启发式处理。

指标通过监听端口（默认为 8080）上的 HTTP 端点 `/metrics` 导出。它们以纯文本格式提供。这些指标设计为由 Prometheus 本身或与抓取 Prometheus 客户端端点兼容的抓取工具来消费。你也可以在浏览器中打开 `/metrics` 查看原始指标。请注意，`/metrics` 端点上暴露的指标反映了 Kubernetes 集群的当前状态。当删除 Kubernetes 对象时，它们将不再出现在 `/metrics` 端点上。

> [!NOTE]
> 本 README 是从[模板](./README.md.tpl)生成的。请在此处进行修改并运行 `make generate-template`。

## 目录

* [版本控制](#版本控制)
  * [Kubernetes 版本](#kubernetes-版本)
  * [兼容性矩阵](#兼容性矩阵)
  * [资源组版本兼容性](#资源组版本兼容性)
  * [容器镜像](#容器镜像)
* [指标文档](#指标文档)
  * [允许和拒绝列表的 ECMAScript 正则表达式支持](#ecmascript-正则表达式支持)
  * [标签名称中的冲突解决](#标签名称冲突解决)
* [`kube-state-metrics` 自身指标](#kube-state-metrics-自身指标)
* [`kube-state-metrics` vs. `metrics-server`](#kube-state-metrics-vs-metrics-server)
* [扩展 `kube-state-metrics`](#扩展-kube-state-metrics)
  * [资源建议](#资源建议)
  * [延迟](#延迟)
  * [关于成本的说明](#关于成本的说明)
  * [水平分片（Horizontal Sharding）](#水平分片horizontal-sharding)
    * [自动分片](#自动分片)
    * [基于部署的分片](#基于部署的分片)
  * [Pod 指标的 DaemonSet 分片](#pod-指标的-daemonset-分片)
  * [资源过滤](#资源过滤)
* [安装与配置](#安装与配置)
  * [构建 Docker 镜像](#构建-docker-镜像)
* [使用指南](#使用指南)
  * [Kubernetes 部署](#kubernetes-部署)
  * [受限权限环境](#受限权限环境)
  * [Helm Chart](#helm-chart)
  * [开发环境](#开发环境)
  * [开发者贡献指南](#开发者贡献指南)
  * [社区支持](#社区支持)

### 版本控制

#### Kubernetes 版本

`kube-state-metrics` 使用 [`client-go`](https://github.com/kubernetes/client-go) 与集群进行通信。支持的 Kubernetes 集群版本由 [`client-go`](https://github.com/kubernetes/client-go#compatibility-matrix) 决定。所有额外的兼容性仅为尽力支持，或碰巧仍然/已经受支持。

#### 兼容性矩阵

最多记录 5 个 `kube-state-metrics` 和 5 个 [Kubernetes 版本](https://github.com/kubernetes/kubernetes/releases)。通常建议使用最新版本的 `kube-state-metrics`。如果你运行非常新的 Kubernetes 版本，可能需要使用未发布的版本以获取完整的受支持资源范围。如果你运行较旧的 Kubernetes 版本，则可能需要运行旧版以获得对所有资源的完整支持。请注意，维护者仅支持最新版本。旧版本可能由社区中感兴趣的用户提供支持。

| kube-state-metrics | Kubernetes client-go Version |
|--------------------|:----------------------------:|
| **v2.15.0**        | v1.32                        |
| **v2.16.0**        | v1.32                        |
| **v2.17.0**        | v1.33                        |
| **v2.18.0**        | v1.34                        |
| **v2.19.0**        | v1.35                        |
| **main**           | v1.35                        |

#### 资源组版本兼容性

Kubernetes 中的资源可能会演进，即不同 Kubernetes 版本中资源的组版本可能从 alpha 变为 beta，最终成为 GA（正式发布）。目前，`kube-state-metrics` 仅使用最新版本中可用的最旧 API。

#### 容器镜像

最新容器镜像可在以下位置找到：

* `registry.k8s.io/kube-state-metrics/kube-state-metrics:v2.19.0` (架构: `amd64`, `arm`, `arm64`, `ppc64le` and `s390x`)
* [多架构镜像](https://explore.ggcr.dev/?image=registry.k8s.io%2Fkube-state-metrics%2Fkube-state-metrics:v2.19.0)

### 指标文档

任何基于 Alpha 版 Kubernetes API 的资源与指标均不受稳定性保证，这可能在任意版本中发生变化。

有关暴露指标的更多信息，请参阅 [`docs`](docs) 目录。

#### ECMAScript 正则表达式支持

自 [#2616](https://github.com/kubernetes/kube-state-metrics/pull/2616/files) 起，`kube-state-metrics` 支持在允许和拒绝列表（allow/deny lists）中使用 ECMAScript 的 `regexp`。此举是为了作为对 Go 语言 `regexp` 包限制的变通方案，该包因非线性时间复杂度而不支持先行断言（lookarounds）。请注意，虽然现在允许和拒绝列表已支持先行断言，但正则表达式的计算时间被限制在一分钟内，以防止性能问题。

#### 标签名称冲突解决

`*_labels` 系列的指标将 Kubernetes 标签作为 Prometheus 标签暴露。由于 [Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/#syntax-and-character-set) 在标签名称允许的字符方面比 [Prometheus](https://prometheus.io/docs/concepts/data_model/#metric-names-and-labels) 更宽松，我们自动将不支持的字符转换为下划线。例如，`app.kubernetes.io/name` 变为 `label_app_kubernetes_io_name`。

这种转换可能会在多个 Kubernetes 标签（如 `foo-bar` 和 `foo_bar`）被转换为同一个 Prometheus 标签 `label_foo_bar` 时产生冲突。

`kube-state-metrics` 会自动添加后缀 `_conflictN` 来解决此冲突，因此它将上述标签转换为 `label_foo_bar_conflict1` 和 `label_foo_bar_conflict2`。

如果你希望更精确地控制此冲突的解决方式，可以考虑在架构的不同层级上处理此问题，例如使用 [准入 Webhook](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/) 标准化 Kubernetes 标签，以确保不存在潜在冲突。

### `kube-state-metrics` 自身指标

`kube-state-metrics` 通过 `--telemetry-host` 和 `--telemetry-port`（默认为 8081）暴露其自身的通用进程指标。

`kube-state-metrics` 还会暴露列表（list）和监听（watch）的成功与错误指标。这些可用于计算资源列表或监听的错误率。如果你在指标中遇到这些错误，最可能的原因是配置或权限问题，接下来应检查 `kube-state-metrics` 的日志。

上述指标的示例：

```prometheus
kube_state_metrics_list_total{resource="*v1.Node",result="success"} 1
kube_state_metrics_list_total{resource="*v1.Node",result="error"} 52
kube_state_metrics_watch_total{resource="*v1beta1.Ingress",result="success"} 1
```

`kube-state-metrics` 还会暴露一些 HTTP 请求指标，示例如下：

```prometheus
http_request_duration_seconds_bucket{handler="metrics",method="get",le="2.5"} 30
http_request_duration_seconds_bucket{handler="metrics",method="get",le="5"} 30
http_request_duration_seconds_bucket{handler="metrics",method="get",le="10"} 30
http_request_duration_seconds_bucket{handler="metrics",method="get",le="+Inf"} 30
http_request_duration_seconds_sum{handler="metrics",method="get"} 0.021113919999999998
http_request_duration_seconds_count{handler="metrics",method="get"} 30
```

`kube-state-metrics` 还会暴露构建和配置指标：

```prometheus
kube_state_metrics_build_info{branch="main",goversion="go1.15.3",revision="6c9d775d",version="v2.0.0-beta"} 1
kube_state_metrics_shard_ordinal{shard_ordinal="0"} 0
kube_state_metrics_total_shards 1
```

`kube_state_metrics_build_info` 用于暴露版本及其他构建信息。有关该 info 模式的更多用法，请参阅此 [博客文章](https://www.robustperception.io/exposing-the-software-version-to-prometheus)。分片指标暴露了 `--shard` 和 `--total-shards` 标志，可用于验证运行时配置，参见 [`/examples/prometheus-alerting-rules`](./examples/prometheus-alerting-rules)。

`kube-state-metrics` 还会暴露关于其配置文件和自定义资源状态（Custom Resource State）配置文件的指标：

```prometheus
kube_state_metrics_config_hash{filename="crs.yml",type="customresourceconfig"} 2.38272279311849e+14
kube_state_metrics_config_hash{filename="config.yml",type="config"} 2.65285922340846e+14
kube_state_metrics_last_config_reload_success_timestamp_seconds{filename="crs.yml",type="customresourceconfig"} 1.6704882592037103e+09
kube_state_metrics_last_config_reload_success_timestamp_seconds{filename="config.yml",type="config"} 1.6704882592035313e+09
kube_state_metrics_last_config_reload_successful{filename="crs.yml",type="customresourceconfig"} 1
kube_state_metrics_last_config_reload_successful{filename="config.yml",type="config"} 1
```

### `kube-state-metrics` vs. `metrics-server`

[metrics-server](https://github.com/kubernetes-incubator/metrics-server) 是一个受 [Heapster](https://github.com/kubernetes-retired/heapster) 启发的项目，旨在实现 [Kubernetes 监控架构](https://github.com/kubernetes/design-proposals-archive/blob/main/instrumentation/monitoring_architecture.md) 中核心指标管道的目标。它是一个集群级组件，定期通过 Metrics API 从所有由 Kubelet 服务的 Kubernetes 节点抓取指标。这些指标经过聚合、存储在内存中，并以 [Metrics API 格式](https://git.k8s.io/metrics/pkg/apis/metrics/v1alpha1/types.go) 提供服务。metrics-server 仅存储最新值，不负责将指标转发到第三方目的地。

`kube-state-metrics` 专注于从 Kubernetes 对象状态生成完全新的指标（例如基于部署、副本集等的指标）。它在内存中持有整个 Kubernetes 状态的快照，并持续从中生成新指标。与 metrics-server 一样，它也不负责将指标导出到任何地方。

将 `kube-state-metrics` 作为独立项目也允许从 Prometheus 等监控系统访问这些指标。

### 扩展 `kube-state-metrics`

#### 资源建议

`kube-state-metrics` 的资源使用量随集群中 Kubernetes 对象（Pod/节点/部署/密钥等）的数量而变化。在一定程度上，集群中的 Kubernetes 对象数量与节点数成正比。

作为一般规则，你应该分配：
* 250MiB 内存
* 0.1 核 CPU

请注意，如果 CPU 限制设置过低，`kube-state-metrics` 的内部队列将无法及时清空，导致随着队列长度增加而消耗更多内存。如果你遇到因高内存分配或 CPU 节流引起的问题，请尝试提高 CPU 限制。

#### 延迟

在 100 节点集群的扩展测试中，延迟数据如下：

```text
"Perc50": 259615384 ns,
"Perc90": 475000000 ns,
"Perc99": 906666666 ns.
```

#### 关于成本的说明

默认情况下，`kube-state-metrics` 会暴露集群中事件的多个指标。如果你的集群中有大量频繁更新的资源，可能会发现大量数据被摄入这些指标中。这可能在某些云提供商处产生高昂费用。请花一点时间 [配置你想要暴露的指标](docs/developer/cli-arguments.md)，并查阅你的 Kubernetes 环境文档，以避免意外的高额费用。

#### 水平分片（Horizontal Sharding）

为了水平分片 `kube-state-metrics`，实现了一些自动分片功能。它通过以下标志进行配置：
* `--shard`（从零开始索引）
* `--total-shards`

分片通过对 Kubernetes 对象的 UID 取 md5 和并对总分片数执行模运算来完成。每个分片决定该对象是否由相应的 `kube-state-metrics` 实例处理。请注意，这意味着所有 `kube-state-metrics` 实例（即使已分片）都会产生网络流量以及为所有对象（而不仅仅是它们负责的对象）反序列化对象的资源消耗。要进一步优化这一点，Kubernetes API 需要支持分片的 list/watch 功能。在理想情况下，每个分片的内存消耗将是未分片设置的 1/n。通常，`kube-state-metrics` 需要进行内存和延迟优化，以便快速向 Prometheus 返回其指标。降低 `kube-state-metrics` 与 kube-apiserver 之间延迟的一种方法是使用 `--use-apiserver-cache` 标志运行 KSM。除了减少延迟外，此选项还将减轻 etcd 的负载。

应谨慎使用分片功能，并设置额外的监控以确保分片按预期配置和运行（例如，总分片中每个分片的实例都已正确配置）。

##### 自动分片

自动分片允许每个分片在部署到 `StatefulSet` 时发现其名义位置，这对于自动配置分片非常有用。这是一个实验性功能，可能会在不通知的情况下损坏或移除。

要启用自动分片，`kube-state-metrics` 必须由 `StatefulSet` 运行，并且必须通过 `--pod` 和 `--pod-namespace` 标志将 Pod 名称和命名空间传递给 `kube-state-metrics` 进程。演示自动分片功能的示例清单可在 [`/examples/autosharding`](./examples/autosharding) 中找到。

当你希望通过单个 Kubernetes 资源（此处为单个 `StatefulSet`）管理 KSM 分片，而不是每个分片一个 `Deployment` 时，这种部署分片的方式非常有用。在部署大量分片时，优势可能尤为显著。

使用自动分片设置的缺点来自于 `StatefulSet` 支持的滚动更新策略。当由 `StatefulSet` 管理时，Pod 会逐个替换，每个 Pod 先被终止然后重新创建。除了此类滚动更新速度较慢外，还会导致每个分片出现短暂停机。如果在滚动更新期间发生 Prometheus 抓取，它可能会错过 `kube-state-metrics` 导出的一些指标。

##### 基于部署的分片

如果你更喜欢将分片作为独立的 `Deployment` 对象进行管理，而不是使用单个 `StatefulSet`，可以使用基于部署的分片。在此模型中，每个 `Deployment` 均通过 `--shard=<N>` 配置明确的索引，并通过 `--total-shards=<N>` 配置总分片数。

基于部署的分片的示例清单可在 [`/examples/deploymentsharding`](./examples/deploymentsharding) 中找到。

与自动分片相比，此方法：
* 使用标准的 `Deployment` 滚动更新行为，可降低升级期间指标缺失的风险
* 为每个分片分配固定且显式的索引

其权衡在于：
* 你必须将每个分片作为单独的 Kubernetes `Deployment` 进行管理
* 你必须在所有分片 `Deployment` 对象之间保持分片配置一致，例如总分片数和共享设置
  * 这意味着扩展分片数量需要重新部署所有分片

### Pod 指标的 DaemonSet 分片

对于 Pod 指标，可以通过以下标志按节点进行分片：
* `--node=$(NODE_NAME)`

每个 `kube-state-metrics` Pod 使用 FieldSelector（spec.nodeName）仅在同一节点上监听/列表 Pod 指标。

DaemonSet kube-state-metrics 示例：

```yaml
apiVersion: apps/v1
kind: DaemonSet
spec:
  template:
    spec:
      containers:
      - image: registry.k8s.io/kube-state-metrics/kube-state-metrics:IMAGE_TAG
        name: kube-state-metrics
        args:
        - --resources=pods
        - --node=$(NODE_NAME)
        env:
        - name: NODE_NAME
          valueFrom:
            fieldRef:
              apiVersion: v1
              fieldPath: spec.nodeName
```

若要跟踪未分配 Pod 的指标，你需要添加额外的部署并设置 `--track-unscheduled-pods`，如下例所示：

```yaml
apiVersion: apps/v1
kind: Deployment
spec:
  template:
    spec:
      containers:
      - image: registry.k8s.io/kube-state-metrics/kube-state-metrics:IMAGE_TAG
        name: kube-state-metrics
        args:
        - --resources=pods
        - --track-unscheduled-pods
```

其他指标可通过 [水平分片](#水平分片horizontal-sharding) 进行分片。

#### 资源过滤

`/metrics` 端点支持使用 `resources` 查询参数按资源类型进行过滤。这允许你仅抓取特定 Kubernetes 资源的指标，这对于减少抓取的数据量或为不同资源类型创建单独的抓取任务非常有用。

示例：
`curl 'http://localhost:8080/metrics?resources=pods,secrets'`

多个资源可以逗号分隔列表的形式指定，或者多次提供 `resources` 参数。

你还可以使用 `exclude_resources` 查询参数排除特定资源。如果你希望抓取除少数几个特定资源外的所有指标，这将非常有用。

示例：
`curl 'http://localhost:8080/metrics?exclude_resources=pods'`

如果同时提供了 `resources` 和 `exclude_resources`，则 `resources` 参数充当允许列表（allowlist），而 `exclude_resources` 充当拒绝列表（denylist），会从允许的资源中过滤掉 `exclude_resources` 参数中指定的任何资源。此处 `exclude_resources` 优先，且你只能对 `kube-state-metrics` 中已启用的资源进行过滤。

### 安装与配置

使用 `go get` 将此项目安装到你的 `$GOPATH` 中：

```bash
go get k8s.io/kube-state-metrics/v2
```

#### 构建 Docker 镜像

只需在此根目录中运行以下命令，它将创建一个自包含的静态链接二进制文件并构建 Docker 镜像：

```bash
make container
```

### 使用指南

只需在具有只读访问 Kubernetes 集群权限的服务账户令牌的 Pod 内部构建并运行 `kube-state-metrics`。

#### prometheus-operator/kube-prometheus 堆栈用户

([`kube-prometheus`](https://github.com/prometheus-operator/kube-prometheus/)) 堆栈已将 `kube-state-metrics` 作为其[组件](https://github.com/prometheus-operator/kube-prometheus#kube-prometheus)之一进行安装；如果你使用的是 kube-prometheus 堆栈，则无需单独安装 `kube-state-metrics`。

如果你想修改 kube-prometheus 的默认配置（例如启用非默认指标），请参阅 [自定义 Kube-Prometheus](https://github.com/prometheus-operator/kube-prometheus/blob/main/docs/customizing.md)。

#### Kubernetes 部署

要部署此项目，只需运行 `kubectl apply -f examples/standard`，系统将创建一个 Kubernetes 服务和部署。（注意：如果你的 Kubernetes 集群版本不是 1.8+，请调整某些资源的 apiVersion，详情请查看 YAML 文件）。

为了让 Prometheus 发现 `kube-state-metrics` 实例，建议为 `kube-state-metrics` 创建特定的 Prometheus 抓取配置以捕获两个指标端点。不建议使用基于注解的发现方式，因为只能选择一个端点；此外，`kube-state-metrics` 通常具有特殊的认证和授权要求，因为它本质上通过指标端点授予了对大部分可用信息的读取权限。

**注意：** Google Kubernetes Engine (GKE) 用户请注意——GKE 有严格的角色权限限制，会阻止创建 `kube-state-metrics` 的角色（Role）和角色绑定（RoleBinding）。为了解决此问题，你可以通过运行以下单行命令为你的 GCP 身份赋予 cluster-admin 角色：

```bash
kubectl create clusterrolebinding cluster-admin-binding --clusterrole=cluster-admin --user=$(gcloud info --format='value(config.account)')
```

请注意，你的 GCP 身份信息区分大小写，但截至 Google Cloud SDK 221.0.0，`gcloud info` 不区分大小写。这意味着如果你的 IAM 成员包含大写字母，上述单行命令可能对你无效。如果在运行上述命令和 `kubectl apply -f examples/standard` 后出现 403 Forbidden 响应，请检查你的账户关联的 IAM 成员：<https://console.cloud.google.com/iam-admin/iam?project=PROJECT_ID>。如果其中包含大写字母，你可能需要将上述命令中的 --user 标志设置为 <https://console.cloud.google.com/iam-admin/iam?project=PROJECT_ID> 中列出的区分大小写的角色名称。

运行上述命令后，如果看到 `Clusterrolebinding "cluster-admin-binding" created`，则你可以继续此服务的安装设置。

#### 健康检查端点（Healthcheck Endpoints）

以下健康检查端点可用（`self` 指遥测端口，而 `main` 指标暴露端口）：
* `/healthz`（在 `main` 上暴露）：如果应用程序正在运行，则返回 200 状态码。建议将其用于启动探针（startup probe）。
* `/livez`（在 `main` 上暴露）：如果应用程序不受 Kubernetes API Server 中断的影响，则返回 200 状态码。建议将其用于存活探针（liveness probe）。
* `/readyz`（在 `self` 上暴露）：如果应用程序已准备好接受请求并暴露指标，则返回 200 状态码。建议将其用于就绪探针（readiness probe）。

请注意，当代理暴露数据时，不建议对任何探针使用遥测指标端点。

#### 受限权限环境

如果你想在缺乏 cluster-reader 角色的环境中运行 `kube-state-metrics`，可以执行以下操作：
* 创建服务账户 (ServiceAccount)

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: kube-state-metrics
  namespace: your-namespace-where-kube-state-metrics-will-deployed
```

* 在特定命名空间上授予其 `view` 权限（使用 RoleBinding）（*注意：你可以将此 RoleBinding 添加到你希望服务账户访问的所有 NS 中*）

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: kube-state-metrics
  namespace: project1
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: view
subjects:
  - kind: ServiceAccount
    name: kube-state-metrics
    namespace: your-namespace-where-kube-state-metrics-will-deployed
```

* 然后在 `kube-state-metrics` 部署配置中指定你的服务账户有权访问的命名空间集合（使用 `--namespaces` 选项）和 Kubernetes 对象集合（使用 `--resources`）

```yaml
spec:
  template:
    spec:
      containers:
      - name: kube-state-metrics
        args:
          - '--resources=pods'
          - '--namespaces=project1'
```

有关可用参数的完整列表，请参阅 [docs/developer/cli-arguments.md](./docs/developer/cli-arguments.md) 中的文档。

#### Helm Chart

自 `kube-state-metrics` Chart `v2.13.3`（镜像 `v1.9.8`）起，官方 [Helm Chart](https://artifacthub.io/packages/helm/prometheus-community/kube-state-metrics/) 由 [prometheus-community/helm-charts](https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-state-metrics) 维护。自 `kube-state-metrics` Chart `v3.0.0` 起，仅支持 `v2.0.0 +` 的镜像。

#### 开发环境

开发时，可通过运行以下命令在你的本地 Kubernetes 集群上测试指标转储：
> 用户可使用 `--apiserver` 命令行参数覆盖 KUBE-CONFIG 文件中的 apiserver 地址。

```bash
go install
kube-state-metrics --port=8080 --telemetry-port=8081 --kubeconfig=<KUBE-CONFIG> --apiserver=<APISERVER>
```

然后 curl 指标端点：

```bash
curl localhost:8080/metrics
```

要在本地运行 e2e 测试，请参阅 [tests/README.md](./tests/README.md) 中的文档。

#### 开发者贡献指南

开发时，需遵循特定的代码模式以提升你的贡献体验及提高 e2e 和其他 CI 测试的通过率。了解更多详情，请参阅 [docs/developer/guide.md](./docs/developer/guide.md) 中的文档。

#### 社区支持

本项目由 [SIG Instrumentation](https://github.com/kubernetes/community/tree/master/sig-instrumentation) 赞助。

Kubernetes 的 Slack 上也有 [#kube-state-metrics](https://kubernetes.slack.com/archives/CJJ529RUY) 频道。

你还可以加入 SIG Instrumentation [邮件列表](https://groups.google.com/forum/#!forum/kubernetes-sig-instrumentation)。这通常会将以下会议的邀请添加到你的日历中，你可以在其中讨论与 `kube-state-metrics` 相关的话题：
* 常规 SIG 会议：[每周四太平洋时间 9:30](https://zoom.us/j/5342565819?pwd=RlVsK21NVnR1dmE3SWZQSXhveHZPdz09)（每两周一次）。[转换到你的时区](http://www.thetimezoneconverter.com/?t=9:30&tz=PT%20%28Pacific%20Time%29)。
* 常规问题排查会议（Triage Meeting）：[每周四太平洋时间 9:30](https://zoom.us/j/5342565819?pwd=RlVsK21NVnR1dmE3SWZQSXhveHZPdz09)（每两周一次，与常规会议交替进行）。[转换到你的时区](http://www.thetimezoneconverter.com/?t=9:30&tz=PT%20%28Pacific%20Time%29)。
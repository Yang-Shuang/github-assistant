<p align="right">
  English | <a href="./README_CN.md">中文</a>
</p>

<div align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://zvec.oss-cn-hongkong.aliyuncs.com/logo/github_log_2.svg" />
    <img src="https://zvec.oss-cn-hongkong.aliyuncs.com/logo/github_logo_1.svg" width="400" alt="zvec logo" />
  </picture>
</div>

<p align="center">
  <a href="https://codecov.io/github/alibaba/zvec"><img src="https://codecov.io/github/alibaba/zvec/graph/badge.svg?token=O81CT45B66" alt="Code Coverage"/></a>
  <a href="https://github.com/alibaba/zvec/actions/workflows/01-ci-pipeline.yml"><img src="https://github.com/alibaba/zvec/actions/workflows/01-ci-pipeline.yml/badge.svg?branch=main" alt="Main"/></a>
  <a href="https://github.com/alibaba/zvec/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-Apache%202.0-blue.svg" alt="License"/></a>
  <a href="https://pypi.org/project/zvec/"><img src="https://img.shields.io/pypi/v/zvec.svg" alt="PyPI Release"/></a>
  <a href="https://pypi.org/project/zvec/"><img src="https://img.shields.io/badge/python-3.10%20~%203.14-blue.svg" alt="Python Versions"/></a>
  <a href="https://www.npmjs.com/package/@zvec/zvec"><img src="https://img.shields.io/npm/v/@zvec/zvec.svg" alt="npm Release"/></a>
</p>

<p align="center">
  <a href="https://trendshift.io/repositories/20830" target="_blank"><img src="https://trendshift.io/api/badge/repositories/20830" alt="alibaba%2Fzvec | Trendshift" style="width: 250px; height: 55px;" width="250" height="55"/></a>
</p>

<p align="center">
  <a href="https://zvec.org/en/docs/db/quickstart/">🚀 <strong>快速开始</strong></a> |
  <a href="https://zvec.org/en/">🏠 <strong>主页</strong></a> |
  <a href="https://zvec.org/en/docs/db/">📚 <strong>文档</strong></a> |
  <a href="https://zvec.org/en/docs/db/benchmarks/">📊 <strong>基准测试</strong></a> |
  <a href="https://deepwiki.com/alibaba/zvec">🔎 <strong>DeepWiki</strong></a> |
  <a href="https://discord.gg/rKddFBBu9z">🎮 <strong>Discord</strong></a> |
  <a href="https://x.com/ZvecAI">🐦 <strong>X (Twitter)</strong></a>
</p>

**Zvec** 是一款开源的进程内向量数据库（in-process vector database）——轻量、极速，专为直接嵌入应用程序而设计。经过阿里巴巴集团内部实战检验，它以极简的配置提供生产级、低延迟且可扩展的相似度搜索能力。

> [!Important]
> 🚀 **v0.4.0 (May 9, 2026)**
>
> - **Dart/Flutter SDK**：发布官方 [zvec](https://github.com/zvec-ai/zvec-dart) Flutter 包，内置 FFI 绑定。支持 Android (`arm64-v8a`) 和 iOS (`arm64`)，无需手动进行原生编译。
> - **iOS 构建支持**：新增对 iOS 平台的构建支持，进一步扩展跨平台覆盖范围。
> - **扩大 topK 限制**：放宽了 `topK` 的上限，以支持更大规模的召回场景。
> - **缺陷修复**：SQ8 量化器召回率下降问题；Windows 路径处理；稀疏向量索引排序问题。
>
> 👉 [查看发布说明](https://github.com/alibaba/zvec/releases/tag/v0.4.0) | [查看路线图 📍](https://github.com/alibaba/zvec/issues/309)

## 💫 核心特性

- **极速检索**：毫秒级完成数十亿向量的相似度搜索。
- **开箱即用**：[安装](#-安装) 后即可在数秒内开始搜索。纯本地运行，无需服务器、无需配置、无繁琐设置。
- **稠密与稀疏向量（Dense + Sparse Vectors）**：同时支持稠密和稀疏嵌入向量，单次调用即可原生支持多向量查询。
- **混合搜索**：将语义相似度与结构化过滤条件结合，实现精准检索结果。
- **持久化存储**：采用预写日志机制（Write-Ahead Logging, WAL）保障数据持久性——即使进程崩溃或断电也不会丢失数据。
- **并发访问**：多个进程可同时读取同一集合；写入操作独占单进程。
- **随处运行**：作为进程内库，Zvec 可在你的代码运行的任何环境中执行——无论是 Notebook、服务器、CLI 工具还是边缘设备。

## 📦 安装

### [Python](https://pypi.org/project/zvec/)

**环境要求**：Python 3.10 - 3.14

```bash
pip install zvec
```

### [Node.js](https://www.npmjs.com/package/@zvec/zvec)

```bash
npm install @zvec/zvec
```

### ✅ 支持的平台

- Linux (x86_64, ARM64)
- macOS (ARM64)
- Windows (x86_64)

### 🛠️ 从源码构建

如需从源码构建 Zvec，请参阅 [从源码构建](https://zvec.org/en/docs/db/build/) 指南。

## ⚡ 一分钟示例

```python
import zvec

# Define collection schema
schema = zvec.CollectionSchema(
    name="example",
    vectors=zvec.VectorSchema("embedding", zvec.DataType.VECTOR_FP32, 4),
)

# Create collection
collection = zvec.create_and_open(path="./zvec_example", schema=schema)

# Insert documents
collection.insert([
    zvec.Doc(id="doc_1", vectors={"embedding": [0.1, 0.2, 0.3, 0.4]}),
    zvec.Doc(id="doc_2", vectors={"embedding": [0.2, 0.3, 0.4, 0.1]}),
])

# Search by vector similarity
results = collection.query(
    zvec.VectorQuery("embedding", vector=[0.4, 0.3, 0.3, 0.1]),
    topk=10
)

# Results: list of {'id': str, 'score': float, ...}, sorted by relevance
print(results)
```

## 📈 大规模性能表现

Zvec 提供卓越的速度与效率，是应对高负载生产环境的理想选择。

<img src="https://zvec.oss-cn-hongkong.aliyuncs.com/qps_10M.svg" width="800" alt="Zvec Performance Benchmarks" />

如需详细的基准测试方法、配置及完整结果，请参阅我们的 [基准测试文档](https://zvec.org/en/docs/db/benchmarks/)。

## 🤝 加入社区

<div align="center">

<div align="center">

| 💬 钉钉 | 📱 微信 | 🎮 Discord | X (Twitter) |
| :---: | :---: | :---: | :---: |
| <img src="https://zvec.oss-cn-hongkong.aliyuncs.com/qrcode/dingding.png" width="150" alt="DingTalk QR Code"/> | <img src="https://zvec.oss-cn-hongkong.aliyuncs.com/qrcode/wechat.png?v=6" width="150" alt="WeChat QR Code"/> | [![Discord](https://img.shields.io/badge/Discord-Join%20Server-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/rKddFBBu9z) | [![X (formerly Twitter) Follow](https://img.shields.io/twitter/follow/ZvecAI)](<https://x.com/ZvecAI>) |
| 扫码加入 | 扫码加入 | 点击加入 | 点击关注 |

</div>

</div>

## ❤️ 贡献指南

我们欢迎并感谢社区贡献！无论你是修复 Bug、添加新功能还是完善文档，你的帮助都将让 Zvec 变得更好。

请查阅我们的 [贡献指南](./CONTRIBUTING.md) 开始参与！
<!-- Copyright Vespa.ai. Licensed under the terms of the Apache 2.0 license. See LICENSE in the project root. -->

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://assets.vespa.ai/logos/Vespa-logo-green-RGB.svg">
  <source media="(prefers-color-scheme: light)" srcset="https://assets.vespa.ai/logos/Vespa-logo-dark-RGB.svg">
  <img alt="#Vespa" width="200" src="https://assets.vespa.ai/logos/Vespa-logo-dark-RGB.svg" style="margin-bottom: 25px;">
</picture>
<br/><br/>

[![Build status](https://badge.buildkite.com/34f7cb35b91da4f929794c5fd7aa722fc15ca0224ad240270b.svg)](https://buildkite.com/vespaai/vespa-engine-vespa)
![GitHub License](https://img.shields.io/github/license/vespa-engine/vespa)
![Maven metadata URL](https://img.shields.io/maven-metadata/v?metadataUrl=https%3A%2F%2Frepo1.maven.org%2Fmaven2%2Fcom%2Fyahoo%2Fvespa%2Fparent%2Fmaven-metadata.xml)



在任意规模下，对向量、张量、文本和结构化数据进行检索、推理与组织，并满足实时服务需求。

本仓库包含构建和运行整个 Vespa 所需的全部代码，并展示所有实时开发进展。
本仓库中的所有内容的许可协议均为 Apache License 2.0。

每周一到周四的早晨（中欧时间），都会从该仓库的 `master` 分支发布一个新的 Vespa 版本。

- 官网：[https://vespa.ai](https://vespa.ai)
- 文档：[https://docs.vespa.ai](https://docs.vespa.ai)
- 持续构建：[https://factory.vespa.ai](https://factory.vespa.ai)
- 免费在云端运行应用：[vespa.ai/free-trial](https://vespa.ai/free-trial/)

## Table of contents

- [背景](#background)
- [安装](#install)
- [使用](#usage)
- [参与贡献](#contribute)
- [构建](#building)
- [许可证](#license)

## Background

搜索、推荐和个性化等用例需要从海量数据集中筛选出子集，在选定的数据上评估机器学习模型，对其进行组织与聚合后返回结果。通常要求在不到 100 毫秒内完成这些操作，且在此期间数据集会持续发生变化。

这很难实现，尤其是当需要处理大型数据集并将其分布在多个节点上进行并行评估时。Vespa 是一个能够以高可用性和高性能为你执行这些操作的平台。它已开发多年，被用于多个大型互联网服务和应用中，每秒可响应数十万次来自 Vespa 的查询。

## Install

将你的 Vespa 应用部署到云服务：[console.vespa-cloud.com](https://console.vespa-cloud.com/)，
或自行运行 Vespa 实例：[https://docs.vespa.ai/en/getting-started.html](https://docs.vespa.ai/en/getting-started.html)

## Usage

- 上述入门指南中创建的应用已完全具备功能且可用于生产环境，但你可能需要 [add more nodes](https://docs.vespa.ai/en/multinode-systems.html) 以实现冗余备份。
- 参见 [developing applications](https://docs.vespa.ai/en/developer-guide.html)，了解如何向你的 Vespa 应用中添加自定义 Java 组件。
- [Vespa APIs](https://docs.vespa.ai/en/api.html) 有助于了解如何与 Vespa 进行交互
- 浏览 [sample applications](https://github.com/vespa-engine/sample-apps/tree/master)
- 关注 [Vespa Blog](https://blog.vespa.ai/) 获取功能更新与用例分享
- 加入 [Vespa Slack community](https://slack.vespa.ai/) 提问并分享反馈

完整文档请访问：[https://docs.vespa.ai](https://docs.vespa.ai)。

## Contribute

我们欢迎贡献！请参阅 [CONTRIBUTING.md](CONTRIBUTING.md) 了解如何参与贡献。

如果你想为文档做出贡献，请访问
[https://github.com/vespa-engine/documentation](https://github.com/vespa-engine/documentation)

## Building

使用 Vespa 无需自行构建，但若你想参与贡献，则需要具备编译代码的能力。
本节将介绍如何构建和测试 Vespa。如需了解应在何处进行修改，请参阅 [Code-map.md](Code-map.md)。
[TODO.md](TODO.md) 中列出了一些建议的改进项及对应的代码位置。

### Development environment

Vespa 支持在 AlmaLinux 8 上构建 C++ 和 Java。
Java 源码也可在任何安装了 Java 17 和 Maven 3.8+ 的平台上进行编译。
使用以下指南通过 Docker 搭建完整的开发环境，用于构建 Vespa、运行单元测试和系统测试：
[Vespa development on AlmaLinux 8](https://github.com/vespa-engine/docker-image-dev#vespa-development-on-almalinux-8)。

#### Java environment for Mac
1. 通过 [Homebrew](https://brew.sh/) 安装 [JDK17](https://openjdk.org/projects/jdk/17/)、 
   [Maven Version Manager](https://bitbucket.org/mjensen/mvnvm/src/master/) 和 [jEnv](https://www.jenv.be)
```sh
brew install jenv mvnvm openjdk@17
```

2. 为了让系统 Java 包装器找到该 JDK，请创建符号链接：
```sh
sudo ln -sfn /opt/homebrew/opt/openjdk@17/libexec/openjdk.jdk /Library/Java/JavaVirtualMachines/openjdk-17.jdk
```

3. 按照 https://www.jenv.be 中的“Configure your shell”进行操作。配置因 Shell 而异，对于 `zsh` 请使用以下命令：
```sh
echo 'export PATH="$HOME/.jenv/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(jenv init -)"' >> ~/.zshrc
eval "$(jenv init -)"
jenv enable-plugin export
exec $SHELL -l
```

4. 将 JDK17 添加到 jEnv
```sh
jenv add $(/usr/libexec/java_home -v 17)
```

5. 在源码根目录下执行以下命令，通过 Maven 验证配置。
   输出结果应显示 [.java-version](.java-version) 和 [mvnvm.properties](mvnvm.properties) 中指定的 JDK 与 Maven 版本。
```sh
mvn -v
```

### Build Java modules

    export MAVEN_OPTS="-Xms128m -Xmx1024m"
    ./bootstrap.sh java
    mvn install --threads 1C

如果你仅需构建 Java 模块，请使用此方法；否则请遵循上述完整的开发指南。

### Run tests for shell scripts (on Mac)
Shell 脚本使用 [BATS](https://bats-core.readthedocs.io/en/stable/) 进行测试。
若要在本地运行测试，请安装该测试框架及其插件：:
```bash
brew install node
sudo npm install -g bats bats-assert bats-support bats-mock
```
导出 `BATS_PLUGIN_PATH` 环境变量，使其指向包含 BATS 插件的全局 npm 模块目录：
```bash
export BATS_PLUGIN_PATH="$(npm root -g)"
```
然后使用以下命令运行所有测试（从仓库根目录执行）：
```bash
bats -r .
```
若要运行特定测试，请使用：
```bash
bats test_dir/test_name.bats
```
你也可以在 IntelliJ IDEA 中配合 [BashSupport Pro](https://plugins.jetbrains.com/plugin/13841-bashsupport-pro)
插件运行测试。请在启动 IDE 前确保已导出 `BATS_PLUGIN_PATH` 环境变量，以避免每次运行配置时都需手动设置。

## License

代码采用 Apache License 2.0 许可协议。具体条款请参阅 [LICENSE](LICENSE)。
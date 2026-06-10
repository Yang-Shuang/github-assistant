# DevOpsGPT：AI 驱动的软件自动化开发解决方案

<p align="center">
<a href="docs/README_CN.md"><img src="docs/files/%E6%96%87%E6%A1%A3-%E4%B8%AD%E6%96%87%E7%89%88-blue.svg" alt="中文文档"></a>
<a href="README.md"><img src="docs/files/document-English-blue.svg" alt="英文文档"></a>
<a href="docs/README_JA.md"><img src="docs/files/ドキュメント-日本語-blue.svg" alt="日文文档"></a>
<a href="http://www.kuafuai.net"><img src="docs/files/%E5%AE%98%E7%BD%91-%E4%BC%81%E4%B8%9A%E7%89%88-purple.svg" alt="官网"></a>
<a href="docs/CONTACT.md"><img src="docs/files/WeChat-%E5%BE%AE%E4%BF%A1-green.svg" alt="联系方式"></a>
<a href="https://discord.gg/4RMUCZwnxF"><img src="https://img.shields.io/badge/Discord-DevOpsGPT-green" alt="Discord 社区"></a>
</p>

### 💡 获取帮助 - [常见问题解答 (Q&A)](https://github.com/kuafuai/DevOpsGPT/issues) 
### 💡 提交需求 - [讨论区 (Issue)](https://github.com/kuafuai/DevOpsGPT/discussions)
### 💡 技术交流 - service@kuafuai.net

<hr/>

## 简介
欢迎使用 AI 驱动的软件自动化开发解决方案，简称 DevOpsGPT。我们将大语言模型（LLM）与 DevOps 工具相结合，将自然语言需求转化为可运行的软件。这一创新功能显著提升了开发效率，缩短了开发周期，降低了沟通成本，从而交付更高质量的软件。

<img src="docs/files/intro-flow-simple.png"></a>

## 特性与优势

- **提升开发效率**：无需编写繁琐的需求文档和进行详细解释。用户可直接与 DevOpsGPT 交互，快速将需求转化为功能型软件。
- **缩短开发周期**：自动化的软件开发流程大幅缩短了交付时间，加速了软件的部署与迭代。
- **降低沟通成本**：通过精准理解用户需求，DevOpsGPT 最大程度降低了沟通误差和误解的风险，提升了研发与业务团队之间的协作效率。
- **高质量交付物**：DevOpsGPT 自动生成代码并进行验证，确保所交付软件的质量与可靠性。
- **[企业版] 现有项目分析**：通过 AI 自动分析现有项目信息，在已有项目基础上精准拆解并开发所需任务。
- **[企业版] 专业模型选择**：支持比 GPT 更强大的垂直领域语言模型服务，以更好地完成需求开发任务，并支持私有化部署。
- **[企业版] 支持更多 DevOps 平台**：可对接更多 DevOps 平台，实现全流程的开发与部署自动化。

## 演示视频（点击播放）

1. <a href="https://www.youtube.com/watch?v=KGeWgM6HzR4" target="_blank">DevOpsGPT Vision 演示</a>
2. <a href="https://www.youtube.com/watch?v=3peUJeB_afo" target="_blank">Demo - 软件开发与云部署</a>
3. <a href="https://www.youtube.com/watch?v=IWUPbGrJQOU" target="_blank">Demo - 使用 Java SpringBoot 开发添加用户的 API</a>

## 工作流程
通过上述介绍与演示，你可能对 DevOpsGPT 如何在现有项目中实现全流程自动化需求开发感到好奇。以下是整体流程的简要概述：

![工作流程](docs/files/intro-flow-en.png)

- **明确需求文档**：与 DevOpsGPT 交互，澄清并确认需求文档中的细节。
- **生成接口文档**：DevOpsGPT 可根据需求自动生成接口文档，便于开发人员设计与实现接口。
- **基于现有项目编写伪代码**：分析现有项目以生成对应的伪代码，为开发者提供参考与起点。
- **细化并优化代码功能**：开发者根据生成的代码进行功能改进与优化。
- **持续集成（CI）**：利用 DevOps 工具实现自动化代码合并与测试。
- **软件版本发布**：使用 DevOpsGPT 及 DevOps 工具将软件版本部署至目标环境。

## 使用云服务
访问 [kuafuai.net](https://www.kuafuai.net)

## 快速开始

1. **通过源码运行**
    1. 下载[发布版本](https://github.com/kuafuai/DevOpsGPT/releases)，或克隆最新代码（可能不稳定）。确保已安装 SQLite 和 Python3.7 及以上版本。
    2. 生成配置文件：复制 `env.yaml.tpl` 并重命名为 `env.yaml`。
    3. 修改配置文件：编辑 `env.yaml`，添加 GPT Token 等必要信息（详细说明请参考[文档链接](docs/DOCUMENT.md)）。
    4. 运行服务：在 Linux 或 Mac 上执行 `sh run.sh`，或在 Windows 上双击 `run.bat`。
    5. 访问服务：通过浏览器访问（查看启动日志获取地址，默认为 http://127.0.0.1:8080）。
    6. 完成需求开发：按照页面提示完成需求开发，生成的代码可在 `./workspace` 目录下查看。

2. **通过 Docker 运行**
    1. 创建目录：执行 `mkdir -p workspace`
    2. 将仓库中的 [env.yaml.tpl](https://github.com/kuafuai/DevOpsGPT/blob/master/env.yaml.tpl) 复制到当前目录并重命名为 `env.yaml`
    3. 修改配置文件：编辑 `env.yaml`，添加 GPT Token 等必要信息。
    4. ```
        docker run -it \
        -v$PWD/workspace:/app/workspace \
        -v$PWD/env.yaml:/app/env.yaml \
        -p8080:8080 -p8081:8081 kuafuai/devopsgpt:latest
        ```
    5. 访问服务：通过浏览器访问（查看启动日志获取地址，默认为 http://127.0.0.1:8080）。
    6. 完成需求开发：按照页面引导完成需求开发，生成的代码可在 `./workspace` 目录下查看。

**详细文档与配置参数请参考[文档链接](docs/DOCUMENT.md)。**


## 局限性
尽管我们致力于借助大语言模型提升企业级软件开发效率并降低门槛，但当前版本仍存在以下局限：

- **需求与接口文档生成精度有限**：在复杂场景下可能无法完全契合开发者的预期意图。
- **当前版本暂不支持自动理解现有项目代码**：我们正在探索新的解决方案，验证效果良好，将在后续版本中引入。

## 产品路线图

- 基于现有项目进行精准的需求拆解与开发任务分解。
- 新产品体验：支持快速导入开发需求，并实现软件开发与部署的并行自动化。
- 引入更多软件工程工具及专业插件，在 AI 规划与执行下快速完成各类软件开发生命周期任务。

我们邀请您参与 DevOpsGPT 项目，[贡献](./docs/CONTRIBUTING.md)于软件开发的自动化与创新，共同打造更智能、高效的软件系统！

## 免责声明

本项目 DevOpsGPT 为实验性应用，按“现状”提供，不提供任何明示或暗示的保证。使用本软件即表示你同意承担与其相关的所有风险，包括但不限于数据丢失、系统故障或其他可能产生的问题。

本项目的开发者与贡献者不对因使用本软件而导致的任何损失、损害或其他后果承担责任或义务。你对基于 DevOpsGPT 提供的信息所做出的任何决策和行动负全部责任。

请注意，由于 Token 消耗，使用 GPT 语言模型可能会产生较高费用。使用本项目即表示你知悉并同意自行负责监控和管理自己的 Token 使用情况及相关成本。强烈建议你定期检查 OpenAI API 的使用情况，并设置必要的限额或警报，以避免意外扣费。

作为自主实验项目，DevOpsGPT 可能会生成不符合实际业务实践或法律要求的内容/采取相关行动。确保基于本软件输出所做出的任何决策符合所有适用法律法规及伦理标准是你的责任。本项目开发者与贡献者不对由此产生的任何后果负责。

使用 DevOpsGPT 即表示你同意对因使用本软件或违反本条款而引发的任何索赔、损失、责任及费用（含合理律师费）进行赔偿，并保护开发者、贡献者及相关方免受此类追责。

## 引用项目
- https://github.com/Significant-Gravitas/Auto-GPT
- https://github.com/AntonOsika/gpt-engineer
- https://github.com/hwchase17/langchain
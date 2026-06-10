<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="docs/_assets/magentic-lite-logo-dark.png">
    <img src="docs/_assets/magentic-lite-logo-light.png" alt="MagenticLite" width="420">
  </picture>
</p>

<p align="center">
  <em>大任务，小模型。</em>
</p>

---

**MagenticLite** 是 Magentic-UI 的下一代产品——由 **Microsoft AI Frontiers** 团队打造的智能体（Agentic）应用，经过重新设计，旨在以更少的资源实现更多功能。它将一款适合本地设备运行的编排模型（[MagenticBrain](https://aka.ms/MagenticBrain-foundry)）与一款专用的浏览器操作模型（[Fara](https://aka.ms/fara-foundry)）相结合，让你无需依赖前沿级算力即可自动化处理实际工作。

- **专为小模型打造，设计高效。** 无需重型计算资源即可获得强大的智能体性能——无需使用前沿级大语言模型。
- **跨浏览器与本地文件系统运行。** 网页调研、表单填写、文件管理，一站式工作流即可完成。
- **全程由你主导与掌控。** 随时引导、审批或接管操作。在执行关键动作前，MagenticLite 会暂停并征求你的意见。
- **设计即安全。** 浏览器会话在轻量级虚拟机（VM）沙箱中运行（[Quicksand](https://microsoft.github.io/quicksand/)），未经你明确授权，智能体无法访问你计算机的其他部分。

## 查看实际效果

点击下方任意任务展开，观看 MagenticLite 如何端到端地处理该任务。

<details open>
  <summary><b>填写报销表单</b></summary>

  https://github.com/user-attachments/assets/a982b60d-127e-4310-96e6-9f094dffb7f0

</details>

<details>
  <summary><b>查找食谱食材价格</b></summary>

  https://github.com/user-attachments/assets/7ff87917-752f-4e40-b319-8036e08ab8f9

</details>

<details>
  <summary><b>搜索并预订餐厅</b></summary>

  https://github.com/user-attachments/assets/ee1f967e-ee1b-4554-b329-36b56b595aa4

</details>

<details>
  <summary><b>整理本地文件</b></summary>

  https://github.com/user-attachments/assets/aff385dd-f856-4db4-8f26-08fd0f940aa4

</details>

## 快速开始

按照以下步骤可在 macOS 或 Windows（WSL）上运行。如需更多详情或使用其他平台，请参阅[安装指南](./docs/installation.md)。

### 1. 安装 MagenticLite

```bash
# Create a project directory
mkdir magentic-lite && cd magentic-lite

# Create and activate a virtual environment
uv venv --python=3.12 --seed .venv
source .venv/bin/activate

# Install the latest 0.2.x release from PyPI
uv pip install "magentic_ui>=0.2.0"
```

### 2. 运行

```bash
magentic-ui --port 8081
```

打开 <http://127.0.0.1:8081/>，并按照应用内的引导流程连接模型端点。如果你还没有配置，请参阅[模型托管指南](./docs/model-hosting-guide.md)。

> **正在寻找之前的 Magentic-UI 0.1 版本**（专为运行前沿级模型优化）？该版本位于 [`magentic-ui-0.1`](https://github.com/microsoft/magentic-ui/tree/magentic-ui-0.1) 分支。

## 文档

| 文档链接                                               | 内容说明                                                                                   |
| ------------------------------------------------------ | ------------------------------------------------------------------------------------------ |
| [安装指南](./docs/installation.md)                     | 支持的平台、macOS / WSL 前置条件、安装与运行命令                                           |
| [从源码构建](./docs/build-from-source.md)              | 如何克隆本仓库并运行 MagenticLite（`uv sync`、`pnpm dev` 等）                              |
| [模型托管指南](./docs/model-hosting-guide.md)          | 搭建模型端点并将 MagenticLite 连接至该端点的端到端教程                                     |
| [配置说明](./docs/configuration.md)                    | 沙箱设置、智能体模式、工具审批机制及完整的 `config.yaml` 示例                              |
| [故障排除](./docs/troubleshooting.md)                  | 常见错误及其解决方法                                                                       |
| [限制说明](./docs/limitations.md)                      | MagenticLite 目前尚不擅长处理的任务与使用场景                                              |
| [透明度声明](./docs/TRANSPARENCY_NOTE.md)              | 预期用途、负责任使用指南、潜在风险及缓解措施                                               |

## 许可证

微软及其任何贡献者均在 [MIT 许可证](https://opensource.org/licenses/MIT) 下授予你使用本仓库中任意代码的许可。请参阅 [LICENSE](LICENSE) 文件。

文档中提及的 Microsoft、Windows、Microsoft Azure 及其他微软产品或服务，可能是微软在美国和/或其他国家的商标或注册商标。本项目的许可证并未授予你使用任何微软名称、徽标或商标的权利。微软的一般商标指南可访问 <http://go.microsoft.com/fwlink/?LinkID=254653> 查看。

对第三方商标或徽标的任何使用均受限于该第三方的政策。

隐私信息可访问 <https://go.microsoft.com/fwlink/?LinkId=521839> 查看。

微软及任何贡献者保留所有其他权利，无论基于其各自的版权、专利或商标，也无论是通过暗示、禁反言还是其他方式。
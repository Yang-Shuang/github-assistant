<div align="center">

<img width="947" alt="Upsonic_README" src="https://github.com/user-attachments/assets/acb3f413-e4fe-44a6-9aff-40d4e9031188" />

# Upsonic

**使用 Python 构建自主 AI Agent**

[![PyPI version](https://badge.fury.io/py/upsonic.svg)](https://badge.fury.io/py/upsonic)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENCE)
[![Python Version](https://img.shields.io/pypi/pyversions/upsonic.svg)](https://pypi.org/project/upsonic/)
[![GitHub stars](https://img.shields.io/github/stars/Upsonic/Upsonic.svg?style=social&label=Star)](https://github.com/Upsonic/Upsonic)
[![GitHub issues](https://img.shields.io/github/issues/Upsonic/Upsonic.svg)](https://github.com/Upsonic/Upsonic/issues)
[![Documentation](https://img.shields.io/badge/docs-upsonic.ai-brightgreen.svg)](https://docs.upsonic.ai)
[![Discord](https://img.shields.io/badge/Discord-Join%20Community-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/pmYDMSQHqY)

[文档](https://docs.upsonic.ai) • [快速入门](https://docs.upsonic.ai/get-started/quickstart) • [示例](https://docs.upsonic.ai/examples) • [Discord](https://discord.gg/pmYDMSQHqY)

</div>

---

## 概述

Upsonic 是一个用于构建自主 Agent（如 OpenClaw 和 Claude Cowork）以及传统 Agent 系统的 Python 框架。

## 快速入门

### 安装

```bash
uv pip install upsonic
# pip install upsonic
```

### IDE 集成

在你的编码工具中将 Upsonic 文档添加为知识来源：

**Cursor：**设置 → 索引与文档（Indexing & Docs）→ 添加 `https://docs.upsonic.ai/llms-full.txt`

同样适用于 VS Code、Windsurf 及其他类似工具。

---

## 创建自主 Agent

### 自定义构建

```python
from upsonic import AutonomousAgent, Task

agent = AutonomousAgent(
    model="anthropic/claude-sonnet-4-5",
    workspace="/path/to/logs"
)

task = Task("Analyze server logs and detect anomaly patterns")

agent.print_do(task)
```

所有文件和 Shell 操作均限制在 `workspace`（工作区）内。路径遍历和危险命令将被阻止。

### 使用预构建的 Agent

预构建的自主 Agent 由 Upsonic 社区打造，开箱即用。每个 Agent 都封装了技能、系统提示词（System Prompt）和首条消息，让你能在几秒内完成安装并运行。该集合[接受贡献](https://github.com/Upsonic/Upsonic/tree/master/src/upsonic/prebuilt)，欢迎提交你的 Agent 并发起 PR。

了解更多：[预构建自主 Agent 概述](https://docs.upsonic.ai/concepts/prebuilt-autonomous-agents/overview)

> **下一步：**连接 [沙箱提供商（E2B）](https://docs.upsonic.ai/concepts/autonomous-agent/overview) 以获取隔离的云端执行环境。

---

## 创建传统 Agent

```python
from upsonic import Agent, Task

agent = Agent(model="anthropic/claude-sonnet-4-5", name="Stock Analyst Agent")

task = Task(description="Analyze the current market trends")

agent.print_do(task)
```

### 添加自定义工具

```python
from upsonic import Agent, Task
from upsonic.tools import tool

@tool
def sum_tool(a: float, b: float) -> float:
    """
    Add two numbers together.

    Args:
        a: First number
        b: Second number

    Returns:
        The sum of a and b
    """
    return a + b

task = Task(
    description="Calculate 15 + 27",
    tools=[sum_tool]
)

agent = Agent(model="anthropic/claude-sonnet-4-5", name="Calculator Agent")

result = agent.print_do(task)
```

> **下一步：**集成 [MCP Tools](https://docs.upsonic.ai/concepts/tools/mcp-tools/overview)，将你的 Agent 连接到数千个外部数据源和服务。

---

## OCR 与文档处理

Upsonic 提供了一套统一的 OCR 接口，采用分层流水线架构：Layer 0（第 0 层）负责文档预处理（如 PDF 转图片、图像增强等），Layer 1（第 1 层）运行 OCR 引擎。

```bash
uv pip install "upsonic[ocr]"
```

```python
from upsonic.ocr import OCR
from upsonic.ocr.layer_1.engines import EasyOCREngine

engine = EasyOCREngine(languages=["en"])
ocr = OCR(layer_1_ocr_engine=engine)

text = ocr.get_text("invoice.pdf")
print(text)
```

支持的引擎：EasyOCR、RapidOCR、Tesseract、PaddleOCR、DeepSeek OCR，以及通过 Ollama 调用的 DeepSeek。

了解更多：[OCR 文档](https://docs.upsonic.ai/concepts/ocr/overview)

---

## 演示视频

<table>
  <tr>
    <td align="center">
      <a href="https://www.youtube.com/watch?v=GOYko0KfBtg">
        <img src="https://img.youtube.com/vi/GOYko0KfBtg/maxresdefault.jpg" width="400" alt="Upsonic 演示视频 1"/>
      </a>
    </td>
    <td align="center">
      <a href="https://www.youtube.com/watch?v=ulUEFIolesQ">
        <img src="https://img.youtube.com/vi/ulUEFIolesQ/maxresdefault.jpg" width="400" alt="Upsonic 演示视频 2"/>
      </a>
    </td>
  </tr>
</table>

---

## 文档与资源

- **[官方文档](https://docs.upsonic.ai)** - 完整指南与 API 参考
- **[快速入门指南](https://docs.upsonic.ai/get-started/quickstart)** - 5 分钟上手
- **[示例代码](https://docs.upsonic.ai/examples)** - 真实场景案例与用法
- **[API 参考](https://docs.upsonic.ai/reference)** - 详细的 API 文档说明

## 社区与支持

> **💬 [加入我们的 Discord 社区！](https://discord.gg/pmYDMSQHqY)** —— 提问交流、分享你的项目、获取团队帮助，并与使用 Upsonic 的其他开发者建立联系。

- **[Discord](https://discord.gg/pmYDMSQHqY)** - 与社区互动并获取实时支持
- **[问题追踪器](https://github.com/Upsonic/Upsonic/issues)** - 提交 Bug 报告和功能建议
- **[更新日志](https://docs.upsonic.ai/changelog)** - 查看各版本新增内容

## 许可证

Upsonic 基于 MIT 许可证发布。详情请参阅 [LICENCE](LICENCE)。

## 贡献指南

我们欢迎社区的贡献！请在提交 Pull Request（PR）前阅读我们的[贡献指南](CONTRIBUTING.md)及行为准则。
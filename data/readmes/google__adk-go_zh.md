# Agent Development Kit (ADK) for Go

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE)
[![Go Doc](https://img.shields.io/badge/Go%20Package-Doc-blue.svg)](https://pkg.go.dev/google.golang.org/adk)
[![Nightly Check](https://github.com/google/adk-go/actions/workflows/nightly.yml/badge.svg)](https://github.com/google/adk-go/actions/workflows/nightly.yml)
[![r/agentdevelopmentkit](https://img.shields.io/badge/Reddit-r%2Fagentdevelopmentkit-FF4500?style=flat&logo=reddit&logoColor=white)](https://www.reddit.com/r/agentdevelopmentkit/)
[![View Code Wiki](https://www.gstatic.com/_/boq-sdlc-agents-ui/_/r/YUi5dj2UWvE.svg)](https://codewiki.google/github.com/google/adk-go)

<html>
    <h2 align="center">
      <img src="https://raw.githubusercontent.com/google/adk-python/main/assets/agent-development-kit.png" width="256"/>
    </h2>
    <h3 align="center">
      一个开源的、代码优先（Code-First）的 Go 工具包，用于构建、评估和部署复杂的 AI Agent，兼具灵活性与可控性。
    </h3>
    <h3 align="center">
      重要链接：
      <a href="https://google.github.io/adk-docs/">Docs</a> &
      <a href="https://github.com/google/adk-go/tree/main/examples">Samples</a> &
      <a href="https://github.com/google/adk-python">Python ADK</a> &
      <a href="https://github.com/google/adk-java">Java ADK</a> & 
      <a href="https://github.com/google/adk-web">ADK Web</a>.
    </h3>
</html>

Agent Development Kit (ADK) 是一个灵活且模块化的框架，将软件工程原则应用于 AI Agent（智能体）的创建中。它旨在简化从简单任务到复杂系统的 Agent 工作流的构建、部署与编排过程。虽然针对 Gemini 进行了优化，但 ADK 支持任意模型（model-agnostic）、任意部署环境，并与其他框架兼容。

本 Go 版本的 ADK 非常适合构建云原生 Agent 应用的开发者，充分利用了 Go 在并发处理和高性能方面的优势。

---

## ✨ Key Features

*   **Idiomatic Go:** Designed to feel natural and leverage the power of Go.
    *   **符合 Go 语言习惯**：设计贴合 Go 开发者的直觉，充分发挥 Go 的强大能力。
*   **Rich Tool Ecosystem:** Utilize pre-built tools, custom functions, or integrate existing tools to give agents diverse capabilities.
    *   **丰富的工具生态**：使用预构建工具、自定义函数或集成现有工具，为 Agent 赋予多样化的能力。
*   **Code-First Development:** Define agent logic, tools, and orchestration directly in Go for ultimate flexibility, testability, and versioning.
    *   **代码优先开发（Code-First）**：直接在 Go 中定义 Agent 逻辑、工具和编排流程，实现极致的灵活性、可测试性与版本控制。
*   **Modular Multi-Agent Systems:** Design scalable applications by composing multiple specialized agents.
    *   **模块化多 Agent 系统**：通过组合多个专业化的 Agent 来设计可扩展的应用程序。
*   **Deploy Anywhere:** Easily containerize and deploy agents, with strong support for cloud-native environments like Google Cloud Run.
    *   **随处部署**：轻松将 Agent 容器化并部署，对 Google Cloud Run 等云原生环境提供强力支持。

## 🚀 Installation

To add ADK Go to your project, run:

```bash
go get google.golang.org/adk
```

## 📄 License

This project is licensed under the Apache 2.0 License - see the
[LICENSE](LICENSE) file for details.

The exception is internal/httprr - see its [LICENSE file](internal/httprr/LICENSE).
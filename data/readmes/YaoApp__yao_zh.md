# Yao —— AI 时代的应用运行时

Yao 是一个开源运行时，用于构建 AI Agent 和 Web 应用——以单一可执行文件形式发布。

![Mission Control](docs/mission-control.png)

**🏠 官网：** [https://yaoagents.com](https://yaoagents.com)

**📚 文档：** [https://yaoagents.com/docs](https://yaoagents.com/docs)

**🖥️ Yao Desktop：** [https://yaoagents.com/download](https://yaoagents.com/download)

---

## 工作原理

将 Yao Agent 视为一个**笼子，而非动物**。你放入其中的内容决定了其行为；而笼子则确保它始终处于受控状态。

所有请求均经过相同的处理流程：

![Pipeline](docs/pipeline.png)

`Create Hook` 在执行器之前运行——注入上下文、强制执行约束条件、路由请求。  
`Next Hook` 在之后运行——验证输出、触发下游操作、驱动多步循环。  
**AI 负责核心运算，你划定运行边界。**

### 三种模式

| 模式 | 执行器 (Executor) | 适用场景 |
|------|----------|-------------|
| **LLM** | OpenAI、Anthropic 等 | 对话式助手、问答、内容生成 |
| **CLI Agent** | OpenCode、Claude Code、容器中的 Codex | 计算机操作、沙箱隔离、SKILL 生态 |
| **Pure Hook** | 你自己的 TypeScript 代码 | 确定性逻辑、路由、菜单交互流程——无需 AI 参与 |

这三种模式共享相同的 Hook 接口。你可以自由混合使用——将部分请求路由至 LLM，用纯代码处理其他请求，全部在一个 `Create Hook` 内完成。

---

## 功能特性

### Agent 框架

- **TypeScript Hooks** —— `Create` 和 `Next` 钩子拦截所有请求；内置 V8 引擎
- **原生 MCP 支持** —— 通过进程、SSE 或 STDIO 传输连接工具
- **Memory API（内存接口）** —— 四种作用域：请求级、会话级、用户级、团队级
- **Multi-Agent（多智能体协作）** —— 委托给专家 Agent，或以并行方式调用多个 Agent
- **CLI Agent / 沙箱** —— 在隔离容器中运行 Claude Code（或其他 CLI 执行器），支持 VNC 桌面访问
- **Skills Ecosystem（技能生态）** —— 将可复用的能力包（`SKILL.md`）直接放入任意 CLI Agent

### 全栈运行时

所有功能集成于单个可执行文件中：

- **数据模型** —— 在 JSON/YAML 中定义数据库表及关系
- **REST APIs** —— 将路由映射至模型查询或 TypeScript 处理器
- **SUI 页面** —— 基于组件的 Web UI，支持服务端渲染 (SSR)
- **Chat UI（CUI）** —— 内置 Agent 对话界面
- **TypeScript** —— 内置 V8 引擎；无需 Node.js
- **Single Binary（单二进制文件）** —— 支持 ARM64/x64 架构；宿主机无需安装 Python、Node.js 或容器环境

### 内置搜索

- **Vector Search（向量检索）** —— 使用 OpenAI 或 FastEmbed 生成嵌入向量
- **Knowledge Graph（知识图谱）** —— 实体关系检索
- **GraphRAG** —— 混合向量与图谱的检索增强生成

---

## 关于名称

Yao（爻，yáo）是《易经》中的基本符号——八卦的构成单元。如同二进制位，它只有两种状态。它们的组合描述了世间万物的规律。
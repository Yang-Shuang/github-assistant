<div align="center">
<a href="https://boundaryml.com?utm_source=github" target="_blank" rel="noopener noreferrer">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="fern/assets/baml-lamb-white.png">
    <img src="fern/assets/baml-lamb-white.png" height="64" id="top">
  </picture>
</a>

</div>

<div align="center">

[![BAML Version](https://img.shields.io/pypi/v/baml-py?color=006dad&label=BAML%20Version)](https://pypi.org/project/baml-py/)

## BAML: Basically a Made-up Language
<h4>

[官网](https://www.boundaryml.com/) | [文档](https://docs.boundaryml.com) | [BAML AI 对话](https://www.boundaryml.com/chat) | [Discord](https://discord.gg/BTNBeXGuaS)



</h4>


</div>

BAML 是一种用于构建可靠 **AI 工作流和智能体（agents）** 的简单提示词语言。

通过将提示词工程转化为 _模式设计（schema engineering）_，BAML 让提示词编写变得简单——你只需专注于定义提示词的参数结构，即可获得更可靠的输出。无需将整个应用用 BAML 重写，只需编写提示词！你可以使用任何语言来接入你的 LLM 函数！请参阅我们的快速入门指南：[Python](https://docs.boundaryml.com/guide/installation-language/python)、[TypeScript](https://docs.boundaryml.com/guide/installation-language/typescript)、[Ruby](https://docs.boundaryml.com/guide/installation-language/ruby) 和 [Go，以及更多语言](https://docs.boundaryml.com/guide/installation-language/rest-api-other-languages)。

BAML 开箱即用，内置完整的类型安全、流式输出（streaming）、重试机制及广泛的模型支持，即使这些模型不支持原生的 [工具调用 API（tool-calling APIs）]。

**体验 BAML**：[Prompt Fiddle](https://www.promptfiddle.com) • [交互式应用示例](https://baml-examples.vercel.app/)


## 核心原则：LLM 提示词即函数

BAML 的基本构建单元是函数。每个提示词都是一个接收参数并返回特定类型的函数。

```rust
function ChatAgent(message: Message[], tone: "happy" | "sad") -> string
```

每个函数还会额外定义所使用的模型及其提示词内容。

```rust
function ChatAgent(message: Message[], tone: "happy" | "sad") -> StopTool | ReplyTool {
    client "openai/gpt-4o-mini"

    prompt #"
        Be a {{ tone }} bot.

        {{ ctx.output_format }}

        {% for m in message %}
        {{ _.role(m.role) }}
        {{ m.content }}
        {% endfor %}
    "#
}

class Message {
    role string
    content string
}

class ReplyTool {
  response string
}

class StopTool {
  action "stop" @description(#"
    when it might be a good time to end the conversation
  "#)
}
```

## 支持任意语言调用 BAML 函数
下面我们通过 Python 调用在 BAML 中定义的 `ChatAgent` 函数。BAML 的 Rust 编译器会生成一个 `baml_client` 供你访问和调用这些函数。

```python
from baml_client import b
from baml_client.types import Message, StopTool

messages = [Message(role="assistant", content="How can I help?")]

while True:
  print(messages[-1].content)
  user_reply = input()
  messages.append(Message(role="user", content=user_reply))
  tool = b.ChatAgent(messages, "happy")
  if isinstance(tool, StopTool):
    print("Goodbye!")
    break
  else:
    messages.append(Message(role="assistant", content=tool.response))
```

你可以使用链式调用的 BAML 函数编写任意类型的智能体或工作流。智能体本质上是一个带有状态机的 `while` 循环，用于调用 Chat BAML 函数。

如果需要流式输出，只需再添加几行代码：
```python
stream = b.stream.ChatAgent(messages, "happy")
# partial is a Partial type with all Optional fields
for tool in stream:
    if isinstance(tool, StopTool):
      ...
    
final = stream.get_final_response()
```

并为流中的每个数据块提供完整的类型安全输出。

## 在 IDE 中实现 10 倍速的提示词测试
BAML 为 [VS Code](https://docs.boundaryml.com/guide/installation-editors/vs-code-extension) 和 [JetBrains IDEs](https://docs.boundaryml.com/guide/installation-editors/jetbrains) 提供了原生工具支持，并持续扩展对[其他编辑器](https://docs.boundaryml.com/guide/installation-editors/others)的支持。

**可视化完整提示词（包含多模态资源）及 API 请求**。BAML 让你完全掌握提示词的透明度和控制权。

![raw-curl](https://github.com/user-attachments/assets/c0b34db9-80cd-45a7-a356-6b5ab4a9c5b7)

**使用 AI 的核心在于迭代速度。**

如果测试一次流水线需要 2 分钟，20 分钟内你只能验证 10 个想法。

如果缩短到 5 秒，同样时间内你可以验证 240 个想法。
![resume-attempt2-smaller2](https://github.com/user-attachments/assets/6fc6b8a6-ffed-4cfc-80b8-78bc8a3d66a6)

Playground（沙盒环境）还支持并行运行测试——带来更快的迭代速度 🚀。

无需登录网页，也无需手动定义 JSON Schema。

## 为任意模型启用可靠的工具调用
即使模型不支持原生的工具调用 API，BAML 也能正常工作。我们开发了 SAP（模式对齐解析 / schema-aligned parsing）算法，以支持 LLM 提供的灵活输出格式，例如 JSON 数据块中的 Markdown 文本或回答前的思维链（chain-of-thought）。[了解更多关于 SAP 的信息](https://www.boundaryml.com/blog/schema-aligned-parsing)

使用 BAML，你的结构化输出可在模型发布首日即可正常运行。无需再纠结模型是否支持并行工具调用、递归模式，或是 `anyOf` / `oneOf` 等复杂语法。

可参考以下实际案例：**[Deepseek-R1](https://www.boundaryml.com/blog/deepseek-r1-function-calling)** 和 [OpenAI O1](https://www.boundaryml.com/blog/openai-o1)。



## 仅需几行代码即可切换上百种模型
```diff
function Extract() -> Resume {
+  client openai/o3-mini
  prompt #"
    ....
  "#
}
```

[重试策略（Retry policies）](https://docs.boundaryml.com/ref/llm-client-strategies/retry-policy) • [降级机制（fallbacks）](https://docs.boundaryml.com/ref/llm-client-strategies/fallback) • [模型轮转（model rotations）](https://docs.boundaryml.com/ref/llm-client-strategies/round-robin)。全部静态定义，无需运行时配置。
![Fallback Retry](https://www.boundaryml.com/blog/2025-01-24-ai-agents-need-a-new-syntax/06-fallback-retry.gif)

需要在运行时动态选择模型？请查看 [客户端注册表（Client Registry）](https://docs.boundaryml.com/guide/baml-advanced/llm-client-registry)。

我们支持：[OpenAI](https://docs.boundaryml.com/ref/llm-client-providers/open-ai) • [Anthropic](https://docs.boundaryml.com/ref/llm-client-providers/anthropic) • [Gemini](https://docs.boundaryml.com/ref/llm-client-providers/google-ai-gemini) • [Vertex](https://docs.boundaryml.com/ref/llm-client-providers/google-vertex) • [Bedrock](https://docs.boundaryml.com/ref/llm-client-providers/aws-bedrock) • [Azure OpenAI](https://docs.boundaryml.com/ref/llm-client-providers/open-ai-from-azure) • [任何兼容 OpenAI 的接口](https://docs.boundaryml.com/ref/llm-client-providers/openai-generic)（包括 [Ollama](https://docs.boundaryml.com/ref/llm-client-providers/openai-generic-ollama)、[OpenRouter](https://docs.boundaryml.com/ref/llm-client-providers/openai-generic-open-router)、[VLLM](https://docs.boundaryml.com/ref/llm-client-providers/openai-generic-v-llm)、[LMStudio](https://docs.boundaryml.com/ref/llm-client-providers/openai-generic-lm-studio)、[TogetherAI](https://docs.boundaryml.com/ref/llm-client-providers/openai-generic-together-ai) 等）

## 构建精美的流式 UI
BAML 为 NextJS、Python（以及任意语言）生成了大量工具，让流式 UI 的开发变得轻松。
![recipe-generator](https://github.com/user-attachments/assets/cf82495b-21fc-40bf-ae98-93eef923d620)

BAML 的流式接口具备完整的类型安全特性。请参阅 [流式输出文档（Streaming Docs）](https://docs.boundaryml.com/guide/baml-basics/streaming) 及我们的 [React Hooks 指南](https://docs.boundaryml.com/guide/framework-integration/react-next-js/quick-start)。

## 完全开源且支持离线使用
- 100% 开源（Apache 2 许可证）
- 100% 隐私保护。AGI 不需要联网，BAML 同样不需要
    - 除你明确设置的模型调用外，不会发起任何网络请求
    - 数据不会被存储或用于任何形式的训练
- BAML 文件可保存至本地机器并提交至 GitHub，方便进行代码差异对比（diff）。
- 基于 Rust 构建。速度极快，快到让你感觉不到它的存在。

## BAML 的设计哲学

在创造新语法时，一切皆可借鉴。只要你能用代码实现，它就能为你所用。以下是我们用来收敛思路的设计原则：

- **1：** 尽可能避免重复造轮子
    - 是的，提示词需要版本管理——我们有优秀的版本控制工具：Git
    - 是的，你需要保存提示词——我们有优秀的存储方案：文件系统（filesystems）
- **2：** 任何文件编辑器和终端都应足以支持其使用
- **3：** 追求极致速度
- **4：** 大一学生也能轻松理解它

## 为什么需要一门新的编程语言？

我们过去是这样写网站的：

```python
def home():
    return "<button onclick=\"() => alert(\\\"hello!\\\")\">Click</button>"
```

而现在我们会这样写：

```jsx
function Home() {
  return <button onClick={() => setCount(prev => prev + 1)}>
          {count} clicks!
         </button>
}
```

新语法在表达新概念方面具有惊人的优势。此外，还要维护成百上千个用于提示词的 f-string（格式化字符串），这让我们感到不适 🤮。纯字符串不利于代码的可维护性，我们更倾向于结构化的字符串。

BAML 的目标是赋予你英语般的表达能力，同时保留代码的结构化特性。

完整 [博客文章](https://www.boundaryml.com/blog/ai-agents-need-new-syntax) 由我们撰写。


## 结语

随着模型能力的不断提升，我们对它们的期望也会越来越高。但有一点永远不会改变：我们需要一种方法来编写可维护的、调用这些模型的代码。目前大家拼凑字符串的做法，很像早期 Web 开发中 PHP/HTML 混写的“汤”式代码。希望我们今天分享的这些理念，能为大家明天编写代码的方式带来一丝启发与改变。

## FAQ
|   |   |
| - | - |
| 我是否需要用 BAML 重写整个应用？ | 不需要，只需编写提示词！BAML 会将定义转换为你所选的语言！[Python](https://docs.boundaryml.com/guide/installation-language/python)、[TypeScript](https://docs.boundaryml.com/guide/installation-language/typescript)、[Ruby](https://docs.boundaryml.com/guide/installation-language/ruby) 及[更多语言](https://docs.boundaryml.com/guide/installation-language/rest-api-other-languages)。 |
| BAML 稳定吗？ | 是的，许多公司已在生产环境中使用！我们每周都会发布更新！ |
| 为什么需要一门新语言？ | [跳转至相关章节](#why-a-new-programming-language) |


## 贡献指南（Contributing）

请查阅我们的[入门指南](/CONTRIBUTING.md)。

## 引用（Citation）

你可以通过以下方式引用 BAML 仓库：
```bibtex
@software{baml,
  author = {Boundary ML},
  title = {BAML},
  url = {https://github.com/boundaryml/baml},
  year = {2024}
}
```

---

由 Boundary 团队 ❤️ 打造

总部位于华盛顿州西雅图市

P.S. 我们正在招聘热爱 Rust 的软件开发工程师。[发送邮件](mailto:founders@boundaryml.com)或在 [Discord](https://discord.gg/ENtBB6kkXH) 上联系我们！

<div align="left" style="align-items: left;">
        <a href="#top">
            <img src="https://img.shields.io/badge/Back%20to%20Top-000000?style=for-the-badge&logo=github&logoColor=white" alt="Back to Top">
        </a>
</div>

<img src="https://imgs.xkcd.com/comics/standards.png" alt_text="hi" />
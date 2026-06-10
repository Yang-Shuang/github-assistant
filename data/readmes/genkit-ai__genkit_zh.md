![Genkit logo](docs/resources/genkit-logo-dark.png#gh-dark-mode-only 'Genkit')
![Genkit logo](docs/resources/genkit-logo.png#gh-light-mode-only 'Genkit')

[Genkit](https://genkit.dev) 是一个开源框架，用于构建全栈 AI 驱动的应用程序。它由 Google Firebase 开发并在生产环境中使用。它为多种编程语言提供了 SDK，稳定性各不相同：

- **JavaScript/TypeScript**：已准备好投入生产环境，功能完整支持
- **Go**：已准备好投入生产环境，功能完整支持
- **Python（Beta）**：广泛的功能支持，正接近生产就绪状态
- **Dart（Preview）**：早期开发阶段，具备核心功能

它提供了一个统一的接口，用于集成来自 [Google](https://genkit.dev/docs/plugins/google-genai)、[OpenAI](https://genkit.dev/docs/plugins/openai)、[Anthropic](https://thefireco.github.io/genkit-plugins/docs/plugins/genkitx-anthropic)、[Ollama](https://genkit.dev/docs/plugins/ollama/) 等提供商的 AI 模型。利用针对多模态内容、结构化输出、工具调用和智能体工作流的精简 API，快速构建并部署生产就绪的聊天机器人、自动化系统和推荐系统。

只需几行代码即可开始：

```ts
import { genkit } from 'genkit';
import { googleAI } from '@genkit-ai/google-genai';

const ai = genkit({ plugins: [googleAI()] });

const { text } = await ai.generate({
    model: googleAI.model('gemini-flash-latest'),
    prompt: 'What is the meaning of life?'
});
```

## 使用 Genkit 探索与构建

免费体验 AI 示例应用，并可视化查看驱动这些应用的 Genkit 代码。

[通过示例探索 Genkit](https://examples.genkit.dev)

## 核心功能

<table>
  <tr>
    <td><strong>广泛支持各类 AI 模型</strong></td>
    <td>使用统一的接口集成来自 <a href="https://genkit.dev/docs/plugins/google-genai">Google</a>、<a href="https://genkit.dev/docs/plugins/openai">OpenAI</a>、<a href="https://thefireco.github.io/genkit-plugins/docs/plugins/genkitx-anthropic">Anthropic</a>、<a href="https://genkit.dev/docs/plugins/ollama">Ollama</a> 等提供商的数百种模型。探索、比较并选择最适合你需求的模型。</td>
  </tr>
  <tr>
    <td><strong>简化 AI 开发</strong></td>
    <td>使用精简的 API 构建具备 <a href="https://genkit.dev/docs/models#structured-output">结构化输出（Structured Output）</a>、<a href="https://genkit.dev/docs/tool-calling">智能体工具调用（Agentic Tool Calling）</a>、<a href="https://genkit.dev/docs/rag">上下文感知生成（Context-aware Generation）</a>、<a href="https://genkit.dev/docs/models#multimodal">多模态输入/输出</a> 等 AI 功能。Genkit 处理了 AI 开发的底层复杂性，让你能够更快地构建和迭代。</td>
  </tr>
  <tr>
    <td><strong>支持 Web 与移动端</strong></td>
    <td>通过专为 <a href="https://genkit.dev/docs/firebase">客户端 SDK（Client SDKs）</a> 和辅助工具，无缝集成 Next.js、React、Angular、iOS、Android 等框架与平台。</td>
  </tr>
  <tr>
    <td><strong>跨语言支持</strong></td>
    <td>使用最适合你项目的语言进行开发。Genkit 为 JavaScript/TypeScript、Go、Python（Beta）和 Dart（Preview）提供了 SDK，在所有受支持的语言中保持一致的 API 和功能。</td>
  </tr>
  <tr>
    <td><strong>随处部署</strong></td>
    <td>将 AI 逻辑部署到任何支持你所选编程语言的环境中，例如 <a href="https://genkit.dev/docs/firebase">Firebase Cloud Functions</a>、<a href="https://genkit.dev/docs/cloud-run">Google Cloud Run</a> 或 <a href="https://genkit.dev/docs/deploy-node">第三方平台</a>，无论是否使用 Google 服务均可。</td>
  </tr>
  <tr>
    <td><strong>开发者工具</strong></td>
    <td>通过专为本地设计的 <a href="https://genkit.dev/docs/devtools">命令行界面（CLI）和开发者 UI</a> 加速 AI 开发。针对单个输入或数据集测试提示词和工作流，比较不同模型的输出结果，利用详细的执行轨迹进行调试，并通过即时可视化反馈快速迭代提示词。</td>
  </tr>
  <tr>
    <td><strong>生产环境监控</strong></td>
    <td>借助全面的生产环境监控功能，自信地发布 AI 功能。在 <a href="https://genkit.dev/docs/observability/getting-started">专属仪表盘（Dashboard）</a> 中跟踪模型性能、请求量、延迟和错误率。通过详细的可观测性指标快速识别问题，确保你的 AI 功能在实际使用中符合质量和性能目标。</td>
  </tr>
</table>

## 工作原理

Genkit 通过开源 SDK 和跨模型提供商及编程语言的统一 API，简化了 AI 集成。它抽象出了底层复杂性，让你能够专注于打造卓越的用户体验。

Genkit 提供的一些关键功能包括：

* [文本与图像生成](https://genkit.dev/docs/models)
* [类型安全的结构化数据生成](https://genkit.dev/docs/models#structured-output)
* [工具调用（Tool Calling）](https://genkit.dev/docs/tool-calling)
* [提示词模板化（Prompt Templating）](https://genkit.dev/docs/dotprompt)
* [持久化聊天界面](https://genkit.dev/docs/chat)
* [AI 工作流（Flows）](https://genkit.dev/docs/flows)
* [AI 驱动的数据检索（RAG）](https://genkit.dev/docs/rag)

Genkit 专为多语言环境下的服务端部署而设计，同时通过专用辅助工具和 [客户端 SDK](https://genkit.dev/docs/firebase) 提供无缝的客户端集成。

## 实施路径

<table>
<tr>
  <td><span>1</span></td>
  <td>选择语言与模型提供商</td>
  <td>为你偏好的语言（JavaScript/TypeScript、Go、Python (Beta)、Dart (Preview)）选择对应的 Genkit SDK。选择一个模型提供商（如 <a href="https://genkit.dev/docs/plugins/google-genai">Google Gemini</a> 或 Anthropic），并获取 API 密钥。部分提供商（如 <a href="https://genkit.dev/docs/plugins/vertex-ai">Vertex AI</a>）可能依赖不同的认证方式。</td>
</tr>
<tr>
  <td><span>2</span></td>
  <td>安装 SDK 并初始化</td>
  <td>安装 Genkit SDK、所选的模型提供商包以及 Genkit CLI。导入 Genkit 和提供商包，并使用提供商 API 密钥初始化 Genkit。</td>
</tr>
<tr>
  <td><span>3</span></td>
  <td>编写并测试 AI 功能</td>
  <td>使用 Genkit SDK 为你的用例构建 AI 功能，从基础的文本生成到复杂的多步工作流和智能体。利用 CLI 和开发者 UI 帮助你快速测试与迭代。</td>
</tr>
<tr>
  <td><span>4</span></td>
  <td>部署并监控</td>
  <td>将你的 AI 功能部署到 Firebase、Google Cloud Run 或任何支持你所选编程语言的环境中。将其集成到你的应用中，并在 Firebase 控制台中监控生产环境运行情况。</td>
</tr>
</table>

## 快速入门

- [JavaScript/TypeScript 快速入门](https://genkit.dev/docs/js/get-started/)
- [Go 快速入门](https://genkit.dev/docs/go/get-started/)
- [Python 快速入门](https://genkit.dev/docs/python/get-started/)（Beta）
- [Dart 快速入门](https://genkit.dev/docs/dart/get-started/)（Preview）

## 开发工具

Genkit 提供了命令行界面和本地 UI，以简化你的 AI 开发工作流。

### CLI

Genkit CLI 包含用于运行和评估 Genkit 函数（工作流）以及收集遥测数据与日志的命令。

- **安装：** `npm install -g genkit-cli`
- **运行命令（附带遥测数据、交互式开发者 UI 等）：** `genkit start -- <command to run your code>`

### 开发者 UI

Genkit 开发者 UI 是一个本地界面，用于测试、调试和迭代你的 AI 应用。

核心功能：

- **运行（Run）：** 在专属沙盒中执行并实验 Genkit 工作流、提示词、查询等。
- **检查（Inspect）：** 分析过往执行的详细轨迹，包括复杂工作流的逐步拆解。
- **评估（Evaluate）：** 查看针对你的工作流运行的评估结果，包括性能指标和相关轨迹链接。

<img src="docs/resources/readme-ui-traces-screenshot.png" width="700" alt="Screenshot of Genkit Developer UI showing traces">

## 联系我们

- [**在 X/Twitter 上关注我们**](https://x.com/GenkitFramework) – 获取 Genkit 团队发布的最新新闻、更新、版本发布、技巧及示例。
- [**加入我们的 Reddit 社区**](https://reddit.com/r/GenkitFramework) – 提问交流，学习高级功能，与团队及其他开发者建立联系，阅读最新动态。
- [**加入我们的 Discord 频道**](https://discord.gg/qXt5zzQKpc) – 获取帮助、分享想法并与其他开发者聊天交流。
- [**在 GitHub 上贡献代码**](https://github.com/genkit-ai/genkit/issues) – 报告 Bug、提出功能建议或浏览源代码。
- [**为文档和示例贡献内容**](https://github.com/genkit-ai/) – 在 Genkit 的 [文档](https://github.com/genkit-ai/docsite) 中报告问题，或提交 [示例代码](https://github.com/genkit-ai/samples)。

[![Ask DeepWiki](https://deepwiki.com/badge.svg)](https://deepwiki.com/firebase/genkit)

## 贡献指南

欢迎并非常感谢大家对 Genkit 的贡献！请参阅我们的 [贡献指南](CONTRIBUTING.md) 开始参与。

## 作者

Genkit 由 [Google](https://developers.google.com/) 开发，并得到了 [开源社区](https://github.com/genkit-ai/genkit/graphs/contributors) 的贡献支持。
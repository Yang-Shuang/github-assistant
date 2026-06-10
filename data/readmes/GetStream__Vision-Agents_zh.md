![VisionAgents](assets/repo_image.png)

# Stream 开源视觉智能体 (Open Vision Agents by Stream)

[![build](https://github.com/GetStream/Vision-Agents/actions/workflows/ci.yml/badge.svg)](https://github.com/GetStream/Vision-Agents/actions)
[![PyPI version](https://badge.fury.io/py/vision-agents.svg)](http://badge.fury.io/py/vision-agents)
![PyPI - Python Version](https://img.shields.io/pypi/pyversions/vision-agents.svg)
[![License](https://img.shields.io/github/license/GetStream/Vision-Agents)](https://github.com/GetStream/Vision-Agents/blob/main/LICENSE)
[![Discord](https://img.shields.io/discord/1108586339550638090)](https://discord.gg/RkhX9PxMS6)
[![X (Twitter)](https://img.shields.io/badge/X-@visionagents__ai-000000?logo=x&logoColor=white)](https://x.com/visionagents_ai)

### 能够观看、聆听并理解视频的跨模态 AI 智能体（Agents）。

[Vision Agents](https://visionagents.ai/) 为你提供核心构建模块，让你能够利用自有模型、基础设施和业务场景，打造智能且低延迟的视频体验。

### 核心亮点

- **视频 AI：**专为实时视频 AI 打造。可实时将 YOLO、Roboflow 等视觉模型与 Gemini/OpenAI 结合使用。
- **低延迟：**快速加入（500ms），并通过 [Stream 边缘网络](https://getstream.io/video/?utm_source=github.com&utm_medium=referral&utm_campaign=vision_agents) 将音视频延迟控制在 30ms 以内。
- **开放架构：**由 Stream 打造，但兼容任意视频边缘网络。
- **原生 API：**直接调用 OpenAI（`create response`）、Gemini（`generate`）和 Claude（`create message`）的原生 SDK 方法，始终获取最新的 LLM 能力。
- **多端 SDK：**提供适用于 React、Android、iOS、Flutter、React Native 和 Unity 的 SDK，由 Stream 超低延迟网络驱动。

## 快速开始

**步骤 1：通过 uv 安装**

`uv add vision-agents`

**步骤 2：（可选）安装额外集成组件**

`uv add "vision-agents[getstream, openai, elevenlabs, deepgram]"`

**步骤 3：获取你的 Stream API 凭据**

从 [Stream](https://getstream.io/try-for-free/?utm_source=github.com&utm_medium=referral&utm_campaign=vision_agents) 获取免费的 API Key。开发者每月可获得 **333,000 参与者分钟数**，并通过 Maker Program 获得额外额度。

按照[快速入门指南](https://visionagents.ai/introduction/quickstart)构建你的第一个智能体（agent）。

## 运行演示

https://github.com/user-attachments/assets/d1258ac2-ca98-4019-80e4-41ec5530117e

本示例向你展示如何使用 YOLO 和 Gemini Live 构建高尔夫教练 AI。将快速的目标检测模型（如 YOLO）与完整的实时 AI 结合，可广泛应用于多种视频 AI 场景。例如：无人机火灾检测、体育/游戏陪练、物理治疗、健身指导、Just Dance 类游戏等。

```python
# partial example, full example: examples/02_golf_coach_example/golf_coach_example.py
agent = Agent(
    edge=getstream.Edge(),
    agent_user=agent_user,
    instructions="Read @golf_coach.md",
    llm=gemini.Realtime(fps=10),
    processors=[ultralytics.YOLOPoseProcessor(model_path="yolo11n-pose.pt", device="cuda")],
)
```

## 功能特性

| **功能特性**           | **说明**                                                                                         |
|--------------------------|---------------------------------------------------------------------------------------------------------|
| **实时 WebRTC**          | 将视频流直接推送至模型提供商，实现即时的视觉理解。                              |
| **视频处理**             | 支持可插拔的处理器流水线（如 YOLO、Roboflow 或自定义 PyTorch/ONNX 模型），可在 LLM 调用前后运行。 |
| **发言检测 (Turn Detection)** | 结合 VAD、说话人分离与智能轮转机制，实现自然流畅的对话交互。                                 |
| **工具调用 & MCP**       | 在对话过程中执行代码和 API —— 支持 Linear 工单、天气查询、电话服务或任意 MCP 服务器。          |
| **电话集成**             | 通过 Twilio 进行双向语音通话，并支持音频流的双向传输。                         |
| **RAG (检索增强生成)**   | 结合 TurboPuffer/Qdrant 向量搜索或 Gemini FileSearch 实现检索增强生成。                     |
| **记忆能力**             | 智能体可通过 Stream Chat 在对话轮次和会话间记住上下文信息。                                        |
| **文本反向通道 (Text Back-channel)** | 通话期间可静默向智能体发送消息 —— 用于教练提示、无声指令等。                 |
| **生产环境就绪**         | 内置 HTTP 服务器、Prometheus 指标监控、水平扩展能力及 Kubernetes 部署支持。                |

## 开箱即用的集成服务

**大语言模型 (LLMs)：** [OpenAI](https://visionagents.ai/integrations/openai) · [Gemini](https://visionagents.ai/integrations/gemini) · [xAI](https://visionagents.ai/integrations/xai) · [OpenRouter](https://visionagents.ai/integrations/openrouter) · [Hugging Face](https://visionagents.ai/integrations/huggingface) · [Kimi AI](https://visionagents.ai/integrations/kimi)

**实时通信 (Realtime)：** [OpenAI Realtime](https://visionagents.ai/integrations/openai) · [Gemini Live](https://visionagents.ai/integrations/gemini) · [AWS Nova Sonic](https://visionagents.ai/integrations/aws-bedrock) · [Qwen](https://visionagents.ai/integrations/qwen) · [Inworld](https://visionagents.ai/integrations/inworld)

**语音转文本 (STT)：** [Deepgram](https://visionagents.ai/integrations/deepgram) · [AssemblyAI](https://www.assemblyai.com/docs/streaming/universal-3-pro) · [Fast-Whisper](https://visionagents.ai/integrations/fast-whisper) · [Fish Audio](https://visionagents.ai/integrations/fish) · [Wizper](https://visionagents.ai/integrations/wizper) · [Mistral Voxtral](https://visionagents.ai/integrations/mistral)

**文本转语音 (TTS)：** [ElevenLabs](https://visionagents.ai/integrations/elevenlabs) · [Cartesia](https://visionagents.ai/integrations/cartesia) · [Deepgram](https://visionagents.ai/integrations/deepgram) · [AWS Polly](https://visionagents.ai/integrations/aws-polly) · [Pocket](https://visionagents.ai/integrations/pocket) · [Kokoro](https://visionagents.ai/integrations/kokoro) · [Inworld](https://visionagents.ai/integrations/inworld) · [Fish Audio](https://visionagents.ai/integrations/fish)

**视觉模型 (Vision)：** [Ultralytics](https://visionagents.ai/integrations/ultralytics) · [Roboflow](https://visionagents.ai/integrations/roboflow) · [Moondream](https://visionagents.ai/integrations/moondream) · [NVIDIA Cosmos](https://visionagents.ai/integrations/nvidia) · [Decart](https://visionagents.ai/integrations/decart)

**虚拟形象 (Avatars)：** [LemonSlice](https://visionagents.ai/integrations/lemonslice)

**发言检测 (Turn Detection)：** [Vogent](https://visionagents.ai/integrations/vogent) · [Smart Turn](https://visionagents.ai/integrations/smart-turn)

**其他集成：** [Twilio](https://github.com/GetStream/Vision-Agents/tree/main/examples/03_phone_and_rag_example) · [TurboPuffer](https://visionagents.ai/guides/rag)

## 文档中心

访问 [VisionAgents.ai](https://visionagents.ai/) 查阅完整文档。

**快速入门：**[语音 AI](https://visionagents.ai/introduction/voice-agents) · [视频 AI](https://visionagents.ai/introduction/video-agents)

**使用指南：**[MCP & 函数调用](https://visionagents.ai/guides/mcp-tool-calling) · [视频处理器](https://visionagents.ai/guides/video-processors) · [电话呼叫](https://visionagents.ai/guides/calling) · [RAG](https://visionagents.ai/guides/rag) · [测试](https://visionagents.ai/guides/testing)

**生产部署：**[HTTP 服务器](https://visionagents.ai/guides/http-server) · [部署流程](https://visionagents.ai/guides/deployment) · [Kubernetes](https://visionagents.ai/guides/kubernetes-deployment) · [水平扩展](https://visionagents.ai/guides/horizontal-scaling) · [Prometheus 指标](https://visionagents.ai/guides/prometheus-metrics)

## 示例项目

| 🔮 Demo Applications                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |                                                                                         |
|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|
| <br><h3>语音智能体（低延迟 + RAG + 文件搜索）</h3>构建快速响应、具备知识推理能力、支持文件检索并实时回复的语音智能体。<br><br>• 低延迟语音交互<br>• 检索增强型回复<br>• 文件与知识库检索<br><br>[>查看源码与教程](https://github.com/GetStream/Vision-Agents/tree/main/plugins/cartesia/example)                                                                                                                                                    | <img src="assets/demo_gifs/cartesia.gif" width="320" alt="Voice Agent Demo">               |
| <br><h3>实时陪练与视频理解</h3>通过实时姿态追踪和处理器流水线，打造逐帧理解的交互式教练应用。<br><br>• 实时姿态追踪<br>• 可执行的教练反馈<br>• 视频处理器流水线支持<br><br>[>查看源码与教程](https://github.com/GetStream/Vision-Agents/tree/main/examples/02_golf_coach_example)                                                     | <img src="assets/demo_gifs/golf.gif" width="320" alt="Realtime Coaching Demo">                 |
| <br><h3>视频重绘与虚拟形象</h3>使用 Decart Lucy 等模型构建虚拟试穿、风格化场景，或为智能体赋予视觉身份。<br><br>• 实时视频风格化<br>• 虚拟试穿体验<br>• 类 Avatar 视觉呈现<br><br>[>查看源码与教程](https://github.com/GetStream/Vision-Agents/tree/main/plugins/decart/example)                                                                                                    | <img src="assets/demo_gifs/mirage.gif" width="320" alt="Video Restyling Demo">           |
| <br><h3>自定义视频模型（Roboflow、YOLO 等）</h3>训练并运行自定义计算机视觉模型，用于安防监控、内容审核及其他垂直领域工作流。<br><br>• 支持自有 CV 模型<br>• 实时审核流水线<br>• 安防与检测场景<br><br>[>查看源码与教程](https://github.com/GetStream/Vision-Agents/tree/main/examples/11_moderation_example) | <img src="assets/demo_gifs/security_camera.gif" width="320" alt="Custom Video Models Demo">          |
| <br><h3>工具调用、MCP 与电话服务</h3>连接外部 API 和服务，使智能体能在实时对话中验证数据并执行现实世界操作。<br><br>• 支持 MCP 和函数调用<br>• 基于 Twilio 的电话工作流<br>• 实时欺诈响应自动化<br><br>[>查看源码与教程](https://github.com/GetStream/Vision-Agents/tree/main/examples/03_phone_and_rag_example) · [>欺诈处理示例](https://github.com/GetStream/Vision-Agents/tree/main/plugins/openai/examples/nemotron_example) | <img src="assets/demo_gifs/fraud_detection.gif" width="320" alt="Tools and Phone Demo"> |

## 社区精选

由社区和 Stream 团队打造的进阶演示项目——这些完整应用超越了仓库内的基础示例，展示了 Vision Agents 在生产环境中的实际潜力。

拥有精彩的演示作品想要展示？请提交 PR 或在 [Discord](https://discord.gg/RkhX9PxMS6) 联系我们。

- [销售助手演示 (Sales Assistant Demo)](https://github.com/GetStream/vision-agents-sales-assistant-demo) —— 一款实时 AI 会议教练，以半透明 macOS 桌面浮窗形式运行。基于 Vision Agents 和 Flutter 构建。
- [情绪陪伴助手 (Crashout Buddy)](https://github.com/GetStream/crashout-buddy) —— 一款具备情感感知能力的语音智能体演示，基于 Vision Agents 和 Stream Video 打造。

## 开发指南

详见 [DEVELOPMENT.md](DEVELOPMENT.md)

想要添加你的平台或服务商？请参阅[创建自定义插件](https://visionagents.ai/integrations/create-your-own-plugin)，或通过邮件联系 **nash@getstream.io**。

## 当前限制

- 视频 AI 对细小文字的处理能力较弱——模型可能会产生幻觉，误识别比分、路牌等。
- 在连续视频理解中，长会话（约 30 秒以上）的上下文记忆会衰减。
- 大多数应用场景需要将专用模型（如 YOLO、Roboflow）与大型 LLM 结合使用。
- 实时模型需要依赖音频或文本输入来触发响应——仅靠视频画面无法直接生成输出。

## ⭐ Star 历史

[![Star History Chart](https://api.star-history.com/svg?repos=GetStream/vision-agents&type=timeline&legend=top-left)](https://www.star-history.com/#GetStream/vision-agents&type=timeline&legend=top-left)
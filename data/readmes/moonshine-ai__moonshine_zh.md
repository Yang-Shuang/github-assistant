![Moonshine Voice Logo](images/logo.png)

# Moonshine Voice

**面向所有人的语音界面**

- [快速开始（Quickstart）](#quickstart)
- [何时选择 Moonshine 而非 Whisper？](#when-should-you-choose-moonshine-over-whisper)
- [使用库（Using the Library）](#using-the-library)
- [模型（Models）](#models)
- [API 参考（API Reference）](#api-reference)
- [支持（Support）](#support)
- [路线图（Roadmap）](#roadmap)
- [致谢（Acknowledgements）](#acknowledgements)
- [许可证（License）](#license)

[Moonshine](https://moonshine.ai) Voice 是一个开源 AI 开发工具包，专为构建实时语音代理和应用程序而设计。

- 所有计算均在本地设备运行，因此速度快、隐私安全，且你无需注册账号、绑定信用卡或配置 API Key。
- 框架与模型针对流式（streaming）应用进行了优化，在用户仍在说话时即可并行处理大量计算，从而提供低延迟响应。
- 所有语音转文字（STT）模型均基于我们[前沿的研究成果](https://arxiv.org/abs/2602.12241)从头训练，因此我们能在高端场景下[提供比 Whisper Large V3 更高的准确率](https://huggingface.co/spaces/hf-audio/open_asr_leaderboard)，同时也能将模型压缩至仅 26MB，适用于资源受限的部署环境。
- 跨平台集成非常简单，同一套库可在 [Python](#python)、[iOS](#ios)、[Android](#android)、[MacOS](#macos)、[Linux](#linux)、[Windows](#windows)、[树莓派（Raspberry Pi）](#raspberry-pi)、[IoT 设备](https://www.linkedin.com/posts/petewarden_most-of-the-recent-news-about-ai-seems-to-activity-7384664255242932224-v6Mr/) 和可穿戴设备上运行。
- 开箱即用（Batteries included）。其高级 API 提供了针对常见任务的完整解决方案，如语音转录、文字转语音（TTS）、说话人识别（Diarization）、指令识别以及[对话代理](#getting-started-with-a-conversational-agent)，让你仅凭一个库即可构建完整的语音应用。
- 支持多语言。STT 支持英语、西班牙语、普通话、日语、韩语、越南语、乌克兰语和阿拉伯语；TTS 支持英语、西班牙语、阿拉伯语、德语、法语、印地语、意大利语、日语、韩语、荷兰语、葡萄牙语、俄语、土耳其语、乌克兰语、越南语和普通话。

## Quickstart（快速开始）

[加入我们的 Discord 社区获取实时技术支持](https://discord.gg/27qp9zSRXF)。

iOS、Android、macOS、Windows 和树莓派的示例应用已发布在 [GitHub Releases](https://github.com/moonshine-ai/moonshine/releases/latest)，以独立压缩包形式提供（通常为 **`{platform}-{Project}.tar.gz`**，对应 [`examples/`](examples/) 下的文件夹结构；Windows 还附带了 C++ 示例的 [`moonshine-voice-windows-x86_64.tar.gz`](https://github.com/moonshine-ai/moonshine/releases/latest/download/moonshine-voice-windows-x86_64.tar.gz)）。完整下载列表请参见 [Examples](#examples) 章节。

### Python

```bash
pip install moonshine-voice
python -m moonshine_voice.mic_transcriber --language en
```

监听麦克风输入，并在转录结果更新时实时打印到终端。

```bash
python -m moonshine_voice.intent_recognizer
```

监听用户定义的指令短语（如 "Turn on the lights"），使用语义匹配机制识别自然语言的不同表达变体。更多详情请查看 [我们的“入门”Colab 笔记本](https://bit.ly/moonshine-colab) 和 [演示视频](https://www.youtube.com/watch?v=WH-AGvHmtoM)。

```bash
python -m moonshine_voice.tts --language en_us --text "Hello world"
```

合成语音并播放。

### iOS

下载 [github.com/moonshine-ai/moonshine/releases/latest/download/ios-Transcriber.tar.gz](https://github.com/moonshine-ai/moonshine/releases/latest/download/ios-Transcriber.tar.gz)，解压后在 Xcode 中打开 `Transcriber/Transcriber.xcodeproj` 项目。

### Android

下载 [github.com/moonshine-ai/moonshine/releases/latest/download/android-Transcriber.tar.gz](https://github.com/moonshine-ai/moonshine/releases/latest/download/android-Transcriber.tar.gz)，解压后在 Android Studio 中打开 `Transcriber` 文件夹。

### Linux

[下载](https://github.com/moonshine-ai/moonshine/archive/refs/heads/main.zip) 或 `git clone` 本仓库，然后运行：

```bash
cd core
mkdir -p build
cd build
cmake ..
cmake --build .
./moonshine-cpp-test
```

### MacOS

Moonshine Voice 支持 Apple Silicon (arm64) 和 Intel (x86_64) Mac。

下载 [github.com/moonshine-ai/moonshine/releases/latest/download/macos-MicTranscription.tar.gz](https://github.com/moonshine-ai/moonshine/releases/latest/download/macos-MicTranscription.tar.gz)，解压后在 Xcode 中打开 `MicTranscription/MicTranscription.xcodeproj` 项目。

### Windows

下载 [github.com/moonshine-ai/moonshine/releases/latest/download/windows-cli-transcriber.tar.gz](https://github.com/moonshine-ai/moonshine/releases/latest/download/windows-cli-transcriber.tar.gz)，解压后在 Visual Studio 中打开 `cli-transcriber\cli-transcriber.vcxproj` 项目。

这是一个独立压缩包，已包含库和模型文件，因此按 Ctrl+Shift+B 或 F7 即可编译生成可执行文件。

### Raspberry Pi（树莓派）

你需要插入一个 USB 麦克风以获取音频输入，但 Python pip 包已针对树莓派进行了优化，因此你可以直接运行：

```bash
 sudo pip install --break-system-packages moonshine-voice
 python -m moonshine_voice.mic_transcriber --language en
```

我已录制 [YouTube 入门 screencast](https://www.youtube.com/watch?v=NNcqx1wFxl0) 供你参考，你也可以下载 [github.com/moonshine-ai/moonshine/releases/latest/download/raspberry-pi-my-dalek.tar.gz](https://github.com/moonshine-ai/moonshine/releases/latest/download/raspberry-pi-my-dalek.tar.gz) 获取一些有趣的树莓派专属示例。[该 README](examples/raspberry-pi/my-dalek/README.md) 提供了关于使用虚拟环境安装 Python（如果你不想用 `--break-system-packages`）的说明。

你可以查看 [github.com/moonshine-ai/pi-help-bot](https://github.com/moonshine-ai/pi-help-bot) 获取更复杂的示例。

## When should you choose Moonshine over Whisper?（何时选择 Moonshine 而非 Whisper？）

TL;DR - 当你处理实时语音时。

| Model                      | WER    | # Parameters | MacBook Pro | Linux x86 | R. Pi 5   |
| -------------------------- | ------ | ------------ | ----------- | --------- | --------- |
| Moonshine Medium Streaming | 6.65%  | 245 million  | 107ms       | 269ms     | 802ms     |
| Whisper Large v3           | 7.44%  | 1.5 billion  | 11,286ms    | 16,919ms  | N/A       |
| Moonshine Small Streaming  | 7.84%  | 123 million  | 73ms        | 165ms     | 527ms     |
| Whisper Small              | 8.59%  | 244 million  | 1940ms      | 3,425ms   | 10,397ms  |
| Moonshine Tiny Streaming   | 12.00% | 34 million   | 34ms        | 69ms      | 237ms     |
| Whisper Tiny               | 12.81% | 39 million   | 277ms       | 1,141ms   | 5,863ms   |

_详见 [benchmarks](#benchmarks) 了解这些数据的测量方式。_

[OpenAI 发布其 Whisper 系列模型]() 是开源语音转文字领域的重大突破。它们提供了多种尺寸，允许开发者在计算资源、存储空间和准确率之间进行权衡以适应应用需求。其最大的模型（如 Large v3）也达到了仅 Google 或 Apple 等大型科技公司内部模型才能匹敌的准确率水平。Moonshine 团队早期就积极采用了 Whisper，我们至今仍是这些模型以及围绕它们构建的优秀框架（如 [FasterWhisper](https://github.com/SYSTRAN/faster-whisper) 等）的忠实拥趸。

然而，在开发需要实时语音交互的应用时，我们发现 Whisper 缺少一些关键功能：

- **Whisper 始终使用 30 秒的固定输入窗口**。在处理大批量音频文件时这不是问题，你通常可以向前查看并截取约 30 秒的语音片段进行处理。但语音界面无法“预读”输入流来拼接更大的片段，且日常短语很少超过五到十秒。这意味着编码器在零填充（zero padding）上浪费了计算资源，导致返回结果的延迟增加。由于响应速度（通常定义为低于 200ms 的延迟）是任何交互界面的核心要求之一，这即使在算力充裕的平台也会损害用户体验，而在资源受限的设备上则完全无法使用。
- **Whisper 不缓存任何状态**。语音界面的另一个常见需求是在用户说话时实时显示反馈，让用户知道应用正在倾听并理解其意图。这意味着需要随着句子逐句说出而反复调用 STT 模型。大部分音频输入是相同的，仅在末尾有少量新增。尽管大量输入保持不变，但 Whisper 每次都会从头开始计算，对已听过的音频进行冗余处理。与固定窗口类似，这种不必要的延迟会严重影响用户体验。
- **Whisper 对多语言的支持较差**。其多语言能力是一项工程壮举，证明了单个模型可以处理多种语言并提供翻译功能。这张来自 OpenAI 的图表（[原始数据见附录 D-2.4](https://cdn.openai.com/papers/whisper.pdf)）展示了在最大的 15 亿参数模型下词错误率（WER）随语言的下降情况。

![Language Chart](images/lang-chart.png)

列出了 82 种语言，但只有 33 种的 WER 低于 20%（我们认为可接受的水平）。对于边缘设备常用的 Base 模型尺寸，仅有 5 种语言的 WER 低于 20%。韩语和日语等亚洲语言拥有庞大的科技市场和创新生态，但 Whisper 在这些语言上的准确率不足以支撑大多数应用需求。通过 OpenAI 云 API 提供的专有内部版本似乎准确率更高，但它们并未作为开源模型提供。

- **边缘端支持碎片化**。围绕 Whisper 已经形成了一个丰富的生态系统，有许多成熟的框架可用于部署模型。然而这些框架通常侧重于桌面级机器和操作系统。虽然有跨 iOS、Android 或 Raspberry Pi OS 的项目可用，但它们的接口、功能和优化程度各不相同，这使得构建需要运行在多种设备上的应用变得不必要地困难。

所有这些限制促使我们创建了自己的模型家族，以更好地满足实时语音交互的需求。由于公开可用的语音数据集总量与网络文本数据相比非常小，我们花费了一些时间进行数据收集和训练工作。经过 extensive 的数据准备工作后，我们发布了 [第一代 Moonshine 模型](https://arxiv.org/abs/2410.15608)。这些模型消除了固定输入窗口的限制，并带来了一些架构改进，在实时语音应用中显著降低了延迟，通常比 Whisper 快 5 倍或更多。

然而，我们仍遇到需要更低延迟且运行在更受限平台上的应用需求。同时我们也希望提供比初始模型最高端（Base 等效）更高的准确率。这促使我们推出了第二代 Moonshine 模型，其优势包括：

- **灵活的输入窗口**。你可以提供任意长度的音频（建议保持在约 30 秒以内），模型只会针对该输入进行计算，无需零填充。这带来了显著的延迟提升。
- **流式缓存支持**。我们的模型现在支持随时间增量添加音频，并缓存输入编码和部分解码器状态，从而跳过更多计算，大幅降低延迟。
- **语言专属模型**。我们已收集数据并为多种语言（包括阿拉伯语、日语、韩语、西班牙语、乌克兰语、越南语和中文）训练了专属模型。正如我们在 [《Flavors of Moonshine》论文](https://arxiv.org/abs/2509.0.553) 中所述，我们发现将模型限制为专注单一语言，相比多语言混合训练，可以在相同尺寸和算力下获得高得多的准确率。
- **跨平台库支持**。我们自己也在构建应用，因此需要能够将这些模型部署到 Linux、MacOS、Windows、iOS 和 Android，并支持从 Python、Swift、Java 和 C++ 等语言调用。为此我们架构了一个可移植的 C++ 核心库来处理所有计算，使用 OnnxRuntime 确保跨系统的良好性能，并为所有所需的高级语言构建了原生接口。这使得开发者只需学习一套 API，即可将其部署到几乎任何目标平台。
- **优于 Whisper V3 Large 的准确率**。在 [HuggingFace OpenASR Leaderboard](https://huggingface.co/spaces/hf-audio/open_asr_leaderboard) 上，我们最新的英语流式模型 Medium Streaming 达到了比 OpenAI 最准确模型更低的词错误率。值得注意的是，Moonshine 仅使用 2.5 亿参数，而 Large v3 使用了 15 亿参数，这使得在边缘端部署变得容易得多。

希望这能让你对 Moonshine 与 Whisper 的对比有清晰的了解。如果你主要在云端 GPU 上批量处理数据且吞吐量最重要，那么 Whisper（或 Nvidia 替代品如 Parakeet）具有批处理等优势；但我们坚信在处理实时语音方面我们无可匹敌。我们构建了我们在最初开发语音应用时希望拥有的框架和模型，因此如果你正在处理实时语音输入，[请尝试 Moonshine](#quickstart)。

## Using the Library（使用库）

Moonshine API 旨在接管捕获和转录实时语音的细节工作，为开发者提供专注于可操作事件的高级接口。我将以 Python 为例说明其工作原理，但 API 在所有支持的语言中保持一致。

- [架构（Architecture）](#architecture)
- [核心概念（Concepts）](#concepts)
- [转录入门（Getting Started with Transcription）](#getting-started-with-transcription)
  - [转录事件流（Transcription Event Flow）](#transcription-event-flow)
- [对话代理入门（Getting Started with a Conversational Agent）](#getting-started-with-a-conversational-agent)
  - [代理设置（Agent Setup）](#agent-setup)
- [文字转语音入门（Getting Started with Text to Speech）](#getting-started-with-text-to-speech)
  - [字素到音素的转换（Converting Graphemes to Phonemes）](#converting-graphemes-to-phonemes)
- [示例（Examples）](#examples)
- [将库添加到你的应用（Adding the Library to your own App）](#adding-the-library-to-your-own-app)
- [Python](#python-1)
- [iOS 或 MacOS](#ios-or-macos)
- [Android](#android-1)
- [Windows](#windowsc)
- [调试（Debugging）](#debugging)
  - [控制台日志（Console Logs）](#console-logs)
  - [输入保存（Input Saving）](#input-saving)
  - [API 调用日志（API Call Logging）](#api-call-logging)
- [从源码构建（Building from Source）](#building-from-source)
  - [Cmake](#cmake)
  - [语言绑定（Language Bindings）](#language-bindings)
  - [移植（Porting）](#porting)
- [下载模型（Downloading Models）](#downloading-models)
  - [语音转文字模型（Speech to Text Models）](#speech-to-text-models)
  - [意图识别模型（Intent Recognition Models）](#intent-recognition-models)
  - [文字转语音模型（Text to Speech Models）](#text-to-speech-models)
- [基准测试（Benchmarking）](#benchmarking)

### Architecture（架构）

我们的目标是构建一个任何开发者都能上手使用的框架，即使没有语音技术经验。我们抽象掉了大量不必要的细节，提供了一个简洁的接口让你专注于应用开发，这也体现在我们的系统架构中。

基本流程如下：

- 根据需求创建 `Transcriber` 或 `IntentRecognizer` 对象（前者用于获取 spoken text，后者仅用于检测用户是否触发了特定动作）。
- 附加一个 `EventListener`，当发生重要事件（如短语结束或动作触发）时被调用，使你的应用能够做出响应。
- 使用 `TextToSpeech` 对象实现双向对话。

传统上，为应用或产品添加语音交互需要集成多个不同的库来处理音频捕获和转换所需的复杂流程。主要步骤包括：麦克风采集、语音活动检测（Voice Activity Detection / VAD，用于将连续音频流切分为语音片段）、语音转文字、说话人识别和意图识别。每个步骤通常涉及不同的框架，极大地增加了集成、优化和维护这些依赖的复杂度。

Moonshine Voice 将这些阶段全部整合在一个库中，并抽象掉了所有非必要细节，只暴露你的应用响应语音所需的关键信息，无论你是想转录文本还是触发指令。

![Moonshine Voice Architecture](images/moonshine-voice-architecture.png)

大多数开发者可以将该库视为一个黑盒，通过基于事件（event-based）的类来实现应用逻辑，只需知道“发生了有趣的事情”即可。当然框架是完全开源的，语音专家可以深入底层进行定制，但这并非必需。

### Concepts（核心概念）

[**Transcriber**](python/src/moonshine_voice/transcriber.py#L66) 接收音频输入并将所有语音转换为文本。这是使用 Moonshine 时首先需要创建的对象，你需要为其提供 [已下载的模型路径](#downloading-models)。

一个 [**MicTranscriber**](python/src/moonshine_voice/mic_transcriber.py#L10) 是基于通用 Transcriber 的辅助类，负责利用平台内置支持（如 Python 中的 sounddevice）连接麦克风，并在捕获音频后自动喂入处理。

一个 [**Stream**](python/src/moonshine_voice/transcriber.py#L297) 是音频输入的处理器。引入 Stream 的原因是你可能需要同时处理多个音频输入源，而单个 Transcriber 可以通过多个 Stream 支持这些输入，且无需重复加载模型资源。如果你只有一个输入源，Transcriber 类本身就包含了与 Stream 相同的方法（start/stop/add_audio），你可以直接使用它而忽略 Stream。

一个 [**TranscriptLine**](python/src/moonshine_voice/moonshine_api.py#L51) 是保存转录本中单行信息的结构体。当有人说话时，库会等待短暂停顿（对应书面语中的标点位置）并开启新行。这些并不完全是完整的句子，因为语音停顿不一定是句末标志，但这确实将连续音频切分为可视为短语的片段。该行包含状态信息，如是否刚开始、仍在进行中或已完成，以及开始时间和持续时间。

一个 [**Transcript**](python/src/moonshine_voice/moonshine_api.py#67) 是按时间顺序排列的行列表，保存已识别文本及其他状态（如捕获时间）。

一个 [**TranscriptEvent**](python/src/moonshine_voice/transcriber.py#L22) 包含转录本变更的信息。事件类型包括新行开始、行内文本更新和行完成。事件对象包含其引用的 `transcript line`，持有该行的最新状态。

一个 [**TranscriptEventListener**](python/src/moonshine_voice/transcriber.py#L266) 是一个协议（protocol），允许应用定义的函数在转录事件发生时被调用。这是大多数应用与转录结果交互的主要方式。实时语音处理时，应用通常需要在新语音被识别时立即响应或显示结果，此方法让你能以类似传统 UI 事件（如触摸屏手势或鼠标点击）的方式处理这些变更。

一个 [**IntentRecognizer**](python/src/moonshine_voice/intent_recognizer.py#L44) 是 `TranscriptEventListener` 的一种特殊类型，允许你在检测到预编程意图时调用不同的回调函数。这非常适合构建语音指令识别功能。

一个 [**TextToSpeech**](python/src/moonshine_voice/tts.py#L20) 对象合成音频供用户播放。

一个 [**DialogFlow**](python/src/moonshine_voice/dialog_flow.py#L453) 对象管理用户与代理之间的对话流程。

一个 [**Dialog**](python/src/moonshine_voice/dialog_flow.py#L335) 对象为每次对话交互创建，允许代理与用户进行多步骤讨论。

### Getting Started with Transcription（转录入门）

我们为大多数平台提供了 [示例](#examples)，建议首先查看针对你目标系统的现有示例。

接下来，你需要 [将库添加到项目中](#adding-the-library-to-your-own-app)。我们致力于通过各平台的原生包管理器提供预编译二进制文件。Python 对应 pip install，Android 对应 Maven 包，MacOS 和 iOS 我们通过 SPM 提供 Swift 包。

Transcriber 需要访问你所用模型的源文件，因此 [下载后](#downloading-models) 你需要将它们放在应用可访问的位置并记录路径。如果你计划分发应用，通常需将其添加为 IDE 资源；如果仅用于实验，可使用硬编码路径。下载脚本完成后会输出模型位置及其架构类型。

现在你可以尝试创建 Transcriber。Python 示例如下：

```python
transcriber = Transcriber(model_path=model_path, model_arch=model_arch)
```

如果未找到模型或发生其他错误，这将抛出包含问题信息的异常。你也可以在控制台查看核心库的日志，它们会打印到 `stderr` 或系统等效位置。

接下来我们创建一个包含应用逻辑的监听器，用于在转录更新时触发相应操作，并将其附加到 Transcriber：

```python
class TestListener(TranscriptEventListener):
    def on_line_started(self, event):
        print(f"Line started: {event.line.text}")

    def on_line_text_changed(self, event):
        print(f"Line text changed: {event.line.text}")

    def on_line_completed(self, event):
        print(f"Line completed: {event.line.text}")

transcriber.add_listener(listener)
```

Transcriber 需要一些音频数据才能工作。如果你想用麦克风测试，可将创建行改为使用 MicTranscriber；如果想先用 .wav 文件测试，可按以下方式喂入：

```python
    audio_data, sample_rate = load_wav_file(wav_path)

    transcriber.start()

    # Loop through the audio data in chunks to simulate live streaming
    # from a microphone or other source.
    chunk_duration = 0.1
    chunk_size = int(chunk_duration * sample_rate)
    for i in range(0, len(audio_data), chunk_size):
        chunk = audio_data[i: i + chunk_size]
        transcriber.add_audio(chunk, sample_rate)

    transcriber.stop()
```

这里需要注意的重点：

- 我们使用 Moonshine 库内置的便捷函数 `load_wav_file()` 从 wav 文件创建了单声道音频数组。
- 调用 start() 激活 Transcriber 的处理代码。
- 循环以分块方式添加音频。这些分块的长度和采样率可以是任意的，库会处理所有底层维护工作。
- 随着音频添加，你注册的 event listener 会被调用，提供最新语音的信息。

在实际应用中，你会从接收源数据的音频处理器中调用 `add_audio()`。由于库能处理任意时长和采样率，只需确保是单声道数据并按原样喂入即可。

Transcriber 默认每 500ms 输入分析一次语音。你可以通过 Transcriber 构造函数的 `update_interval` 参数修改此间隔。对于流式模型，大部分计算在音频添加时已完成，且会在短语结束时自动触发，因此更改此值通常不会大幅影响负载或延迟。

核心要点是：你通常无需关心转录数据结构本身，事件系统会告诉你何时发生了重要变更。如果你需要检查状态，可以手动调用 `update_transcription()` 获取包含当前会话所有信息的 Transcript 对象。

通过对 Transcriber（或 Stream）调用 `start()` 和 `stop()`，我们开始并结束一个会话。每个会话关联一个独立的 Transcript 文档，每次调用 `start()` 都会重置它，因此在此之前应备份你需要的数据。

Transcriber 类还提供了一个更简单的 `transcribe_without_streaming()` 方法，适用于你有历史音频数组（如文件或录音）只需分析的场景。

我们还提供了基类 `Transcriber` 的特化版本 `MicTranscriber`。其具体实现因语言和平台而异，但应提供一个自动连接到系统主麦克风的 Transcriber。这使得从该通用源开始转录变得简单，因为它支持与基类相同的所有监听器回调。

#### Transcription Event Flow（转录事件流）

库与应用之间的主要通信渠道是通过传递给已注册监听器的 **事件**。主要有四种事件类型：

- `LineStarted`：当检测到新语音片段开始时发送给监听器。可能包含文本也可能不包含，但由于在话语初期触发，该文本随时间推移很可能会变化。
- `LineUpdated`：每当行的任何信息（包括时长、音频数据和文本）发生变化时调用。
- `LineTextChanged`：仅在与行关联的文本更新时调用。这是 `LineUpdated` 的子集，专注于尽可能频繁刷新用户界面文本以维持交互体验的常见需求。
- `LineCompleted`：当我们检测到说话人暂停且当前片段结束时发送。该行数据结构包含文本、时长和说话人 ID 的最终值。

我们对此类事件提供以下保证：

- `LineStarted` 对任何片段仅调用一次。
- `LineCompleted` 对任何片段在 `LineStarted` 后仅调用一次。
- `LineUpdated` 和 `LineTextChanged` 仅在片段的 `LineStarted` 之后、`LineCompleted` 之前被调用。
- 这些更新事件不保证一定会被触发（实践中可通过将 `update_interval` 设为极大值来禁用）。
- 任意给定 Stream 在同一时间仅有一行处于活跃状态。
- 一旦 `LineCompleted` 被调用，库将不再修改该行数据。
- 如果在 Transcriber 或 Stream 上调用了 `stop()`，所有活跃行的 `LineCompleted` 都会被触发。
- 每行都有一个 64 位 `lineId`，设计为足以避免碰撞。
- 该 `lineId` 从首次 `LineStarted` 事件开始在整个生命周期内保持不变。

### Getting Started with a Conversational Agent（对话代理入门）

许多应用需要能够理解用户意图并适当回复的语音代理。为使实现尽可能简单，我们允许你定义不同的对话流程。流程可以是对查询的直接回复，也可以是包含动作触发的多步骤分支对话。

要定义这些流程，你需要使用 [`DialogFlow`](#dialogflow) 对象，并通过回调函数接收 [`Dialog`](#dialog) 参数。以下是一个取自 [github.com/moonshine-ai/pi-help-bot](https://github.com/moonshine-ai/pi-help-bot) 示例代码的简单流程：

```python
    def report_ip_address(d: Dialog):
        ip = _find_local_ip()
        if ip is None:
            yield d.say("Sorry, I couldn't find a local IP address.")
            return
        speech_ip = re.sub(r"(\d)", r"\1 ", ip.replace(".", " dot "))
        yield d.say([
            f"Okay. Your local IP address is {speech_ip}. ",
            f"To repeat, that's {speech_ip}."
        ])

    dialog_flow.register_flow("What is my IP address?", report_ip_address)
```

这会将 `report_ip_address()` 函数注册为：当用户说出类似 "What is my IP address?" 的任何内容时触发。匹配通过语义完成，因此 "Tell me your IP address" 或 "Can you tell me the local IP address?" 等变体也会触发它。你可以注册任意数量的顶级对话启动短语，系统会监听并路由到语义最接近的项。

该函数本身接收一个代表当前对话交互的 `Dialog` 参数。在此简单案例中我们不需要用户额外输入，因此仅用它来 `say()` 请求的信息。我们将 IP 地址按数字拆分为单独单词以提高清晰度，并将连接点替换为明确的 "dot"，使 192.178.4.72 变为 "1 9 2 dot 1 7 8 dot 4 dot 72"，因为这是语音中的标准读法。

对于更复杂的对话（如设置新 Wi-Fi），你可以直接在 Python 中定义多个步骤和分支点：

```python
   def connect_to_wifi(d: Dialog):
        input_ssid = yield d.ask("What's the name of your Wi-Fi network? Say list if you want to pick from a list or spell if you want to spell out the start of the name")
        input_ssid = input_ssid.strip()

        networks = _scan_wifi_networks()

        if input_ssid.lower().strip(string.punctuation) == "list":
            yield d.say("Say yes to the network you want to connect to.")
            for network in networks:
                if (yield d.confirm(f"{network}?")):
                    input_ssid = network
                    break
        elif input_ssid.lower().strip(string.punctuation) == "spell":
            input_ssid = yield d.ask("Spell out the start of the network name.", mode=SPELLED)

        found_ssid = fuzzy_match_network(input_ssid, networks)
        if found_ssid is None:
            yield d.say(f"Sorry, I couldn't find a matching network for {input_ssid}.")
            return

        password = yield d.ask(
            f"Please spell the Wi-Fi password for {found_ssid} one character at a time, and say done when finished.",
            mode=SPELLED,
        )

        yield d.say(f"Connecting to {found_ssid}.")

        try:
            result = subprocess.run(
                ["sudo", "nmcli", "device", "wifi",
                    "connect", found_ssid, "password", password],
                capture_output=True, text=True, timeout=30,
            )
        except FileNotFoundError:
            yield d.say("Sorry, network manager was not found on this system.")
            return
        except subprocess.TimeoutExpired:
            yield d.say("Sorry, the connection attempt timed out.")
            return

        if result.returncode == 0:
            yield d.say(f"Connected to {found_ssid}.")
        else:
            print(f"[ERROR] nmcli stderr: {result.stderr}", file=sys.stderr)
            yield d.say(
                f"Sorry, I wasn't able to connect to {found_ssid}. "
                "Please check the network name and password and try again."
            )

    dialog_flow.register_flow("Connect to Wi-Fi", connect_to_wifi)
```

函数首先通过调用询问用户要加入的网络名称：

```python
input_ssid = yield d.ask("What's the name of your Wi-Fi network?...")
```

Dialog 类允许你向用户提问，并返回包含其回复的字符串。与常规 Python 代码相比，这里唯一的特殊之处在于 `yield` 关键字。由于用户可能需要时间才能回应，我们调用 yield 将控制权交还给主脚本，直到收到回复。这是 `DialogFlow` 的通用模式，凡是我们等待用户说话的地方都会看到它，以避免阻塞。

```python
        if input_ssid.lower().strip(string.punctuation) == "list":
            yield d.say("Say yes to the network you want to connect to.")
            for network in networks:
                if (yield d.confirm(f"{network}?")):
                    input_ssid = network
                    break
```

我们的示例应用支持几种不同的输入方式：浏览网络列表、拼出前几个字母或说出名称。这里我们通过遍历所有可用网络并询问用户是否为所需网络来实现列表选项。你可以看到常规循环和条件判断在 Python 中按预期工作。

对于每个网络，我们调用 `confirm()`，它提出是/否问题并等待肯定或否定结果。与系统中所有匹配一样，这是通过语义完成的，因此 "okay"、"affirmative" 和 "go ahead" 都会被视为肯定，而 "no"、"cancel" 和 "stop" 视为否定。

```python
        password = yield d.ask(
            f"Please spell the Wi-Fi password for {found_ssid} one character at a time, and say done when finished.",
            mode=SPELLED,
        )
```

密码输入比较棘手，因为它们由任意字母、数字和符号组成，必须由用户逐字拼出。Moonshine 通过 `mode=SPELLED` 参数支持此功能。这要求用户逐个拼写字符，并使用微调模型识别每个字符的发音。除了常规发音（如 "aitch" 或 "capital zee"）外，它还支持北约音标字母表（"alpha", "bravo" 等），甚至简短描述性短语（如 "E as in elephant"）。它会回显听到的内容，并允许你删除错误输入。

```python
        try:
            result = subprocess.run(
                ["sudo", "nmcli", "device", "wifi",
                    "connect", found_ssid, "password", password],
                capture_output=True, text=True, timeout=30,
            )
        except FileNotFoundError:
            yield d.say("Sorry, network manager was not found on this system.")
            return
        except subprocess.TimeoutExpired:
            yield d.say("Sorry, the connection attempt timed out.")
            return
```

该流程也兼容异常处理器等控制结构，因此你可以使用惯用代码定义对话，包括错误恢复逻辑。

要亲自尝试此功能，请运行内置示例：

```bash
python -m moonshine_voice.dialog_flow
```

### Agent Setup（代理设置）

一个代理需要一个语音转文字 `Transcriber` 对象接收输入、一个 `IntentRecognizer` 理解输入，以及一个 `TextToSpeech` 对象进行回复：

```python
    embedding_model_path, embedding_model_arch = get_embedding_model()
    intent_recognizer = IntentRecognizer(
        model_path=embedding_model_path,
        model_arch=embedding_model_arch
    )

    tts = TextToSpeech(args.tts_language)

    model_path, model_arch = get_model_for_language(args.language)
    mic_transcriber = MicTranscriber(
        model_path=model_path, model_arch=model_arch
    )

    dialog_flow = DialogFlow(
        tts=tts,
        intent_recognizer=intent_recognizer
    )
    add_commands(dialog_flow, tts)

    mic_transcriber.add_listener(dialog_flow)

    mic_transcriber.start()
```

`add_commands()` 函数会为代理应识别的所有短语调用 `register_flow()`。

### Getting Started with Text to Speech（文字转语音入门）

语音界面通常需要双向对话，Moonshine 的 `TextToSpeech` 旨在简化多语言场景下的实现。它也是自包含的，因此你可以独立于转录和意图识别模块使用它。

最简单的方式是指定输出语言来创建语音合成器对象，然后传入文本在默认音频设备上播放：

```python
from moonshine_voice import TextToSpeech

tts = TextToSpeech("fr")
tts.say("Bonjour, mon ami")
tts.wait()  # block until playback finishes
```

`say()` 立即返回并将文本排队进行后台合成与播放。多次调用 `say()` 会按顺序排列每次话语，当前话语播放时会预合成下一段。你也可以传入字符串列表、用 `stop()` 取消所有操作，或用 `is_talking()` 轮询状态：

```python
tts.say(["One.", "Two.", "Three."])
tts.stop()  # cancel remaining utterances and halt playback
```

如果你在没有音频输出的机器上运行，或需要进行进一步处理，可以使用 `synthesize()` 方法获取音频样本：

```python
from moonshine_voice import TextToSpeech

tts = TextToSpeech("en-us")
audio_data, sample_rate = tts.synthesize("Howdy, partner")
```

如你所见，文字转语音支持多语言。要查看可用列表，请运行 `list_tts_languages()` 函数：

```python
from moonshine_voice import list_tts_languages
list_tts_languages()

['ar-msa', 'de-de', 'en-gb', 'en-us', 'es-ar', 'es-es', 'es-mx', 'fr-fr', 'hi-in', 'it-it', 'ja-jp', 'ko-kr', 'nl-nl', 'pt-br', 'pt-pt', 'ru-ru', 'tr-tr', 'uk-ua', 'vi-vn', 'zh-hans']
```

对于每种语言，你可以列出可用声音：

```python
from moonshine_voice import list_tts_voices

list_tts_voices("ru")

{'present': [], 'downloadable': ['piper_ru_RU-denis-medium', 'piper_ru_RU-dmitri-medium', 'piper_ru_RU-irina-medium', 'piper_ru_RU-ruslan-medium']}
```

如果声音标记为 `downloadable`，意味着当你将其传入 `TextToSpeech` 构造函数时，Moonshine 会自动下载它到缓存中（只要 `download` 参数保持默认值 true），后续调用无需联网即可使用。

#### Converting Graphemes to Phonemes（字素到音素的转换）

从声音名称你可能已注意到，Moonshine Voice 使用了出色的 [Kokoro](https://github.com/hexgrad/kokoro) 和 [PiperTTS](https://huggingface.co/rhasspy/piper-voices) 项目的模型。你可以在 [core/moonshine-tts/data/README.md](core/moonshine-tts/data/README.md) 找到所有 TTS 模型和数据源的详细信息。

既然已有其他优秀的 TTS 项目，为什么世界还需要另一个实现？Moonshine 力求运行在尽可能多的平台上并支持商业应用，而 Kokoro 和 Piper 均使用 [espeak-ng](https://github.com/espeak-ng/espeak-ng/) 将文本字符串转换为音素（国际音标 IPA 中表示句子声音的表示）。Espeak-ng 采用 GPL 许可证，虽然我是自由软件的拥趸，但其条款使得将其整合到不公开源代码的应用中变得困难。

在云端这不成问题，因为许多 espeak-ng 的使用可通过调用外部可执行文件实现，依赖影响不大。但在许多边缘操作系统上这不是选项，因为在 iOS 或 Android 上包含代码的唯一方式是链接到应用中，这需要开源调用代码。

为了支持更广泛的使用，我们开发了自有的“字素到音素（Grapheme to Phoneme / G2P）”模块，扮演类似角色但完全从头编写。你可以在 [core/moonshine-tts](core/moonshine-tts) 找到实现，它与其他代码一样采用 MIT License 发布。

每种语言将书面形式转换为语音的过程都不同，且通常因方言而异。这就是 espeak-ng 被广泛使用的原因：它经过多年开发，将语言学知识编码为复杂的规则集，其中许多启发式方法需要大量测试才能准确。Moonshine Voice G2P 引擎仍较新，需要类似调优以处理跨语言的所有变体，但我希望初始实现是一个良好的开端，并将在未来受益于社区反馈和贡献。以下是使用 [scripts/tts_g2p_intelligibility.py](scripts/tts_g2p_intelligibility.py) 测试的各语言清晰度结果：

| Language | Moonshine CER | Reference CER |
| --- | --- | --- |
| ar_msa | 20.8% | 15.3% |
| de_de | 18.3% | 9.2% |
| en_us | 12.6% | 9.8% |
| es_ar | 7.9% | 10.6% |
| es_es | 4.2% | 4.5% |
| es_mx | 3.2% | 2.6% |
| fr_fr | 14.8% | 9.4% |
| hi_in | 26.5% | 15.9% |
| it_it | 24.2% | 11.4% |
| ja_jp | 38.1% | 16.8% |
| ko_kr | 25.0% | 18.6% |
| nl_nl | 15.9% | 3.3% |
| pt_br | 19.7% | 4.9% |
| pt_pt | 43.8% | 24.6% |
| ru_ru | 16.9% | 5.0% |
| tr_tr | 8.9% | 7.9% |
| uk_ua | 27.7% | 15.6% |
| vi_vn | 79.0% | 36.5% |
| zh_hans | 37.8% | 32.6% |

如果你只想使用字素到音素功能而不需要语音合成，可以直接调用它：

```python
from moonshine_voice import GraphemeToPhonemizer

g2p = GraphemeToPhonemizer("en-us")
g2p.to_ipa("Hello world")

'həlˈoʊ wˈɝld'
```

### Examples（示例）

[`examples`](examples/) 文件夹包含按平台组织的代码示例。我们使用各技术栈的标准工具（Apple 平台的 Android Studio & Gradle、Xcode & Swift，Windows 的 Visual Studio）。[GitHub Releases](https://github.com/moonshine-ai/moonshine/releases/latest) 目前提供以下可下载资产（示例目录通常命名为 **`{platform}-{Project}.tar.gz`**；Windows 和 C++ 还包含预编译的原生库捆绑包）。

- **[Android](examples/android/)**
  - [IntentRecognizer](https://github.com/moonshine-ai/moonshine/releases/latest/download/android-IntentRecognizer.tar.gz)
  - [TextToSpeech](https://github.com/moonshine-ai/moonshine/releases/latest/download/android-TextToSpeech.tar.gz)
  - [Transcriber](https://github.com/moonshine-ai/moonshine/releases/latest/download/android-Transcriber.tar.gz)
- **[Portable C++](examples/c++/README.md)**
  - [transcriber.cpp](examples/c++/transcriber.cpp)
  - [text-to-speech.cpp](examples/c++/text-to-speech.cpp)
- **[iOS](examples/ios/)**
  - [IntentRecognizer](https://github.com/moonshine-ai/moonshine/releases/latest/download/ios-IntentRecognizer.tar.gz)
  - [TextToSpeech](https://github.com/moonshine-ai/moonshine/releases/latest/download/ios-TextToSpeech.tar.gz)
  - [Transcriber](https://github.com/moonshine-ai/moonshine/releases/latest/download/ios-Transcriber.tar.gz)
- **[MacOS](examples/macos/)**
  - [BasicTranscription](https://github.com/moonshine-ai/moonshine/releases/latest/download/macos-BasicTranscription.tar.gz)
  - [MicTranscription](https://github.com/moonshine-ai/moonshine/releases/latest/download/macos-MicTranscription.tar.gz)
  - [TextToSpeech](https://github.com/moonshine-ai/moonshine/releases/latest/download/macos-TextToSpeech.tar.gz)
- **[Windows](examples/windows/)**
  - [cli-transcriber](https://github.com/moonshine-ai/moonshine/releases/latest/download/windows-cli-transcriber.tar.gz)
- **[Python](examples/python/)**
  - [basic_transcription.py](examples/python/basic_transcription.py)
  - [mic_transcription.py](examples/python/mic_transcription.py)
  - [intent_recognition.py](examples/python/intent_recognition.py)
  - [ollama-voice/ollama_voice.py](examples/python/ollama-voice/ollama_voice.py )
- **[Raspberry Pi](examples/raspberry-pi/)**
  - [my-dalek](https://github.com/moonshine-ai/moonshine/releases/latest/download/raspberry-pi-my-dalek.tar.gz)
  - [Pi Help Bot](https://github.com/moonshine-ai/pi-help-bot/archive/refs/heads/main.zip)

示例通常包含一个最小项目（仅创建 Transcriber 并喂入 WAV 文件数据）和一个使用平台默认框架从麦克风获取音频的项目。对于 Android，[`examples/android/IntentRecognizer`](examples/android/IntentRecognizer/) 是一个独立的 Gradle 项目，你可以将其复制出目录树：它依赖 Maven Central 的 **`ai.moonshine:moonshine-voice:0.0.62`**（包含 `IntentRecognizer`）并在 `app/src/main/assets/` 下捆绑了 **small English streaming** ASR 及 **embeddinggemma-300m**（Git LFS）。 

流式权重在运行时从资源镜像到内部存储，然后通过 `MicTranscriber.loadFromFiles` 和 `MOONSHINE_MODEL_ARCH_SMALL_STREAMING` 加载。[`examples/android/TextToSpeech`](examples/android/TextToSpeech/) 是相同风格的 Gradle 示例用于设备端 TTS：它使用 **`moonshine-voice`** 中的 `TextToSpeech` 类，并在 `app/src/main/assets/tts-data/`（Git LFS）下捆绑了默认英语语音离线运行所需的一切——**Kokoro** 模型、`af_alloy` 声音及 `en_us` G2P + OOV 文件（`dict_filtered_heteronyms.tsv`, `g2p-config.json`, `oov/model.onnx`, `oov/onnx-config.json`）。 

其他所有声音——完整的 Kokoro 目录及全语言 Piper 声音——均通过 `moonshine_get_tts_dependencies` 解析，并在用户首次选择所需声音时从 `https://download.moonshine.ai/tts/` 按需下载，获取资产时会显示小型进度指示器。下载内容缓存在 `filesDir` 下，后续启动将离线复用。 

[`examples/ios/TextToSpeech`](examples/ios/TextToSpeech/) 在 Apple 平台上遵循相同模式：Xcode 项目通过 Swift Package Manager 拉取 **`MoonshineVoice`**，并在 `tts-data/`（Git LFS）下捆绑相同的 Kokoro + `af_alloy` + `en_us` 离线集。首次启动时打包目录被暂存至 `Application Support/tts-data/`，随后使用 `TextToSpeech.getDependencies` 从 `https://download.moonshine.ai/tts/` 下载缺失文件，UI 显示进度指示器。切换至不同声音会触发相同的按需下载，缓存文件在后续启动中复用。

### Adding the Library to your own App（将库添加到你的应用）

我们通过各平台最广泛使用的包管理器分发该库。以下是如何在不同系统上将其添加到现有项目的方法。

#### Python

Python 包 [托管于 PyPi](https://pypi.org/project/moonshine-voice/)，因此你只需执行 `pip install moonshine-voice`，然后在项目中 `import moonshine_voice` 即可安装。

#### iOS or MacOS（iOS 或 MacOS）

对于 iOS 我们使用 Swift Package Manager，[一个自动更新的 GitHub 仓库](https://github.com/moonshine-ai/moonshine-swift/) 托管每个版本。要直接使用它，在 Xcode 文件视图侧边栏右键选择菜单中的 "Add Package Dependencies..."。对话框打开后，将 `https://github.com/moonshine-ai/moonshine-swift/` 粘贴到顶部搜索框，应会看到 `moonshine-swift`。选中并点击 "Add Package"，它将被添加到你的项目中。现在你应该可以 `import MoonshineVoice` 并使用该库。你需要将所用模型文件添加至应用包并确保在部署阶段复制它们，以便设备端访问。

供参考，你可以在 [`examples/ios/Transcriber`](examples/ios/Transcriber) 和 [`examples/macos/BasicTranscription`](examples/macos/BasicTranscription/) 中找到已应用这些更改的 Xcode 项目。

#### Android（Android）

在 Android 上我们 [将包发布至 Maven](https://mvnrepository.com/artifact/ai.moonshine/moonshine-voice)。要在 Android Studio 和 Gradle 项目中包含它，首先在 `gradle/libs.versions.toml` 文件中添加所需版本号，例如在 `[versions]` 部分插入一行：`moonshineVoice = "0.0.62"`。然后在 `[libraries]` 部分添加包引用：`moonshine-voice = { group = "ai.moonshine", name = "moonshine-voice", version.ref = "moonshineVoice" }`。

最后在 `app/build.gradle.kts` 中将库添加到 `dependencies` 列表：`implementation(libs.moonshine.voice)`。[`examples/android/IntentRecognizer`](examples/android/IntentRecognizer/) 和 [`examples/android/TextToSpeech`](examples/android/TextToSpeech/) 示例使用相同的坐标（其目录中为 `moonshineVoice = "0.0.62"`）。

#### Windows/C++（Windows）

我们未能找到被大多数 Windows 开发者使用的单一包管理器，因此改为提供原始库和头文件的下载。[`examples/windows/cli-transcriber/download-lib.bat`](examples/windows/cli-transcriber/download-lib.bat) 中的脚本将为你获取这些文件。你会看到一个 `include` 文件夹，应将其添加到项目设置的包含搜索路径中，以及一个 `lib` 目录也应添加到包含搜索路径中。然后将 `lib` 文件夹中的所有库文件添加到你项目的链接器依赖项中。

Windows 上推荐的接口是 C++ 语言绑定。这是一个仅头文件的库，提供比底层 C 版本更高级的 API。你可以 `#include "moonshine-cpp.h"` 从 C++ 代码访问 Moonshine。如果你想查看所有更改的综合示例，请查看 [`examples/windows/cli-transcriber`](examples/windows/cli-transcriber)。

### Debugging（调试）

#### Console Logs（控制台日志）

该库旨在帮助你理解出现问题时的状况。如果某些功能未按预期工作，首先应检查控制台的日志消息。每当核心库中出现失败点或异常时，你都会看到提供问题详细信息的消息。你的语言绑定也应能识别核心库返回的错误并抛出适当的异常，但有时日志因包含更多细节而更有帮助。

#### Input Saving（输入保存）

如果未报告错误但转录质量不符合预期，值得排查 Transcriber 接收的音频数据是否存在问题。为便于此操作，你可以在创建 Transcriber 时传入 `save_input_wav_path` 选项。这会将接收到的所有音频保存为你指定文件夹中的 .wav 文件。Python 示例：

```python
python -m moonshine_voice.transcriber --options='save_input_wav_path=.'
```

这将使测试音频通过 Transcriber，并将接收到的音频写入当前目录下的 `input_1.wav` 文件。如果你运行多个 Stream，你会看到每个额外流生成 `input_2.wav` 等。这些 wav 仅包含最新会话的音频数据，并在每次启动后被覆盖。收听这些文件应能帮助你确认输入符合预期且未失真或损坏。

#### API Call Logging（API 调用日志）

如果遇到错误，跟踪与库交互的时间线可能很困难。`log_api_calls` 选项会将触发的底层 API 调用打印到控制台，以便你调查任何排序或时序问题。

```python
uv run -m moonshine_voice.transcriber --options='log_api_calls=true'
```

### Building from Source（从源码构建）

如果你想调试库内部、添加仪器以了解其运行方式，或添加改进/自定义功能，所有源代码均可供你自行构建。

#### Cmake（Cmake）

库的核心引擎包含在此仓库的 `core` 文件夹中。它使用 C++ 编写并提供 C 接口以便与其他语言轻松集成。我们使用 cmake 在所有平台上进行构建，因此入门的最简单方式如下：

```bash
cd core
mkdir -p build
cd build
cmake ..
cmake --build .
```

完成后你应拥有一组可在自己系统上运行的二进制可执行文件。这些可执行文件均为单元测试，需从 `test-assets` 文件夹运行。你可以使用 [`scripts/test-core.sh`](scripts/test-core.sh) 一步完成构建和测试流程，Windows 则使用 [`scripts/test-core.bat`](scripts/test-core.bat)。所有测试应编译并运行无误。

#### Language Bindings（语言绑定）

有各种用于不同平台和语言的构建脚本，但若要查看如何为所有支持系统构建的示例，请查阅 [`scripts/build-all-platforms.sh`](scripts/build-all-platforms.sh)。这是我们在每次发布时调用的脚本，它构建了我们上传至各包管理器系统的所有工件。

不同平台和语言在 C 接口之上有一层封装，以便在不同环境中惯用地使用库。主要系统在仓库中有自己的顶级文件夹，例如：[`python`](python/)、[`android`](android/) 和 [`swift`](swift/)（用于 iOS 和 MacOS）。你可以在这里找到调用底层核心库例程的代码，以及处理各平台事件系统的代码。

#### Porting（移植）

如果你有不受支持的设备，可以尝试在你的系统上 [使用 cmake 构建](#cmake)。C++ 核心库唯一的重大依赖是 [Onnx Runtime](https://github.com/microsoft/onnxruntime)。我们为所有支持的系统提供了 [预编译二进制库文件](core/third-party/onnxruntime/lib/)，但如果我们提供的库不覆盖你的用例，你需要自行查找或构建版本。

如果你想从我们不支持的语言调用此库，请查看 [C 接口绑定](core/moonshine-c-api.h)。大多数语言都有某种方式调用 C 函数，因此你可以使用这些及其它语言的绑定示例来指导实现。

### Downloading Models（下载模型）

#### Speech to Text Models（语音转文字模型）

获取转录所需模型文件的最简单方法是使用 Python 下载模块。[安装后](#python) 运行下载器：

```bash
python -m moonshine_voice.download --language en
```

`language` 参数可使用两位代码或英文名称。若要查看当前版本支持的语言，它们 [列于下方](#available-models)，或者你可以向此命令提供一个无效语言作为参数：

```bash
python -m moonshine_voice.download --language foo
```

你还可以使用 `model-arch` 标志可选地请求特定模型架构，从 [moonshine-c-api.h](/core/moonshine-c-api.h) 中的数字选择。如果未设置架构，脚本将加载可用最高质量模型。

下载脚本会记录下载的模型文件位置及模型架构，例如：

```bash
encoder_model.ort: 100%|███████████████████████████████████████████████████████| 29.9M/29.9M [00:00<00:00, 34.5MB/s]
decoder_model_merged.ort: 100%|██████████████████████████████████████████████████| 104M/104M [00:02<00:00, 52.6MB/s]
tokenizer.bin: 100%|█████████████████████████████████████████████████████████████| 244k/244k [00:00<00:00, 1.44MB/s]
Model download url: https://download.moonshine.ai/model/base-en/quantized/base-en
Model components: ['encoder_model.ort', 'decoder_model_merged.ort', 'tokenizer.bin']
Model arch: 1
Downloaded model path: /Users/petewarden/Library/Caches/moonshine_voice/download.moonshine.ai/model/base-en/quantized/base-en
```

最后两行告诉你使用的模型架构及磁盘上的模型文件位置。默认使用你的用户缓存目录，MacOS 上为 `~/Library/Caches/moonshine_voice`，但你可以通过在执行脚本前设置 `MOONSHINE_VOICE_CACHE` 环境变量来更改位置。

#### Intent Recognition Models（意图识别模型）

下载模块还帮助你获取识别意图所需的资产，主要是句子嵌入模型。 

```python
python -m moonshine_voice.download --intent
```

```bash
model_q4.onnx: 100%|███████████████████████████████████████████████| 507k/507k [00:00<00:00, 4.59MB/s]
model_q4.onnx_data: 100%|██████████████████████████████████████████| 188M/188M [00:06<00:00, 32.6MB/s]
Embedding model path: /Users/petewarden/Library/Caches/moonshine_voice/download.moonshine.ai/model/embeddinggemma-300m
/Users/petewarden/Library/Caches/moonshine_voice/download.moonshine.ai/model/embeddinggemma-300m
```

#### Text to Speech Models（文字转语音模型）

TTS 需要大量模型、字典及其他文件，且因语言差异很大。你可以使用下载模块精确拉取特定语言所需的内容，并可选地指定声音：

```bash
python -m moonshine_voice.download --tts --root /tmp/tts-files/

dict_filtered_heteronyms.tsv: 100%|██████████████████████████████| 2.77M/2.77M [00:00<00:00, 15.5MB/s]
g2p-config.json: 100%|██████████████████████████████████████████████| 60.0.62.0 [00:00<00:00, 160kB/s]
model.onnx: 100%|████████████████████████████████████████████████| 20.9M/20.9M [00:00<00:00, 37.7MB/s]
onnx-config.json: 100%|██████████████████████████████████████████| 4.53k/4.53k [00:00<00:00, 11.7MB/s]
model.onnx: 100%|████████████████████████████████████████████████| 88.1M/88.1M [00:01<00:00, 85.6MB/s]
config.json: 100%|███████████████████████████████████████████████| 2.30k/2.30k [00:00<00:00, 6.88MB/s]
af_heart.kokorovoice: 100%|████████████████████████████████████████| 510k/510k [00:00<00:00, 3.82MB/s]
TTS assets root (use as g2p_root): /private/tmp/tts-files
/private/tmp/tts-files
```

下载的模型放置在根文件夹下的子文件夹中，默认情况下文字转语音模块期望文件具有相同的相对路径以便仅凭父路径即可自动找到它们。如果你确实需要将它们移动到其他位置，你可以使用 `TextToSpeech` 构造函数的 `options` 参数为每个文件提供新路径，以常规相对路径作为键，实际文件路径作为值。

如果你的应用可能在安装后存储在任意位置，你也可以传入 `tts_root` 选项在运行时设置 TTS 数据根文件夹的实际路径。

### Benchmarks（基准测试）

核心库包含一个基准测试工具，通过加载 .wav 音频文件并以分块方式喂入模型来模拟处理实时音频。运行它：

```
cd core
md build
cd build
cmake ..
cmake --build . --config Release
./benchmark
```

这将报告处理音频的绝对时间、该时间占音频文件时长的百分比，以及响应的平均延迟。

百分比很有用，因为它近似估算模型在你的硬件上占用的计算负载比例。例如显示 20% 意味着语音处理将占用应用运行中五分之一的计算时间，留下 80% 供你的其他代码使用。

延迟指标需要稍作解释。大多数应用关心的是用户说完短语后多久收到通知，因为这决定了产品响应速度。与任何 UI 一样，从语音结束应用到执行操作的时间决定了语音界面的响应感，目标通常保持在低于 200ms。此处记录的延迟指标是库判定用户停止说话到向客户端交付该短语最终转录本之间的平均时间。流式模型在此影响最大，因为它们在实际语音仍在发生时已完成大量前期工作，因此通常能极快完成。

默认情况下基准测试二进制文件使用嵌入框架的 Tiny English 模型，但你可以通过 `--model-path` 和 `--model-arch` 参数选择 [你已下载的模型](#downloading-models)。

你还可以使用 `--transcription-interval` 参数选择转录更新的频率。默认为 0.5 秒，但合适值取决于你的应用需要多快的更新速度。更长的间隔会略微减少计算量，代价是更新变慢。

#### Whisper Comparisons（Whisper 对比）

对于支持 Python 的平台，你可以运行 [`scripts/run-benchmarks.py`](scripts/run-benchmarks.py) 脚本评估类似指标，其优势在于它还能下载模型，你无需担心路径处理问题。

它还评估了等效的 Whisper 模型。这是一个相当主观的基准测试，考察两种模型家族在代表许多常见实时语音应用需求的场景下的延迟和总计算成本：

- 用户完成短语后需尽快得到响应。
- 短语时长范围在一到十秒之间。

这与批量离线处理场景的需求截然不同，后者更看重系统整体吞吐量而非单个语音片段的延迟，因此允许批处理等优化。

我们并非声称 Whisper 不是优秀的离线处理模型，但我们希望突出 Moonshine 在具有实时延迟要求的实时语音应用中提供的优势。

实验设置如下：

- 我们以 two_cities.wav 音频文件作为测试用例，因为它包含短长混合短语。你可以通过 `--wav_path` 参数传入自己的音频文件来更改此项。
- 我们使用 Moonshine Tiny、Base、Tiny Streaming、Small Streaming 和 Medium Streaming 模型。
- 我们将这些与 Whisper Tiny、Base、Small 和 Large v3 模型对比。由于 Moonshine Medium Streaming 的 WER 低于 Whisper Large v3，我们对这两者进行对比，否则按同名对比。
- 我们使用 Moonshine VAD 分段器将音频切分为短语，并将每个短语喂入 Whisper 进行转录。
- 两种模型的响应延迟均测量为 VAD 分段器判定短语完成到返回转录文本之间的时间。对 Whisper 而言这是完整转录时间，但由于 Moonshine 模型是流式的，我们可以在语音仍在发生时完成大量工作，因此延迟低得多。
- 我们通过累加每个模型的音频处理时长来测量总计算成本，然后表示为总音频时长的百分比。这与常用的实时因子（RTF）指标相反，但反映了实时应用所需的计算负载。
- 我们对 Whisper 使用 faster-whisper，因为它似乎提供了最佳跨平台性能。我们仍坚持使用 CPU，因为大多数应用无法依赖目标平台上存在 GPU 或 NPU 加速。我们知道有很多优秀的 GPU/NPU 加速 Whisper 实现，但这些不够便携，对我们关心的应用无用。

## Models（模型）

Moonshine Voice 基于 Moonshine AI 团队创建的语音转文字模型家族。若要下载与框架配合使用的模型，你可以 [使用 Python 包访问它们](#downloading-models)。本节包含关于我们提供的模型历史和特性的更多信息。

 - [论文（Papers）](#papers)
 - [可用模型（Available Models）](#available-models)
 - [领域定制（Domain Customization）](#domain-customization)
 - [量化（Quantization）](#quantization)
 - [HuggingFace](#huggingface)

### Papers（论文）

这些研究论文是了解模型背后架构和性能策略的良好资源：

- [**Moonshine: Speech Recognition for Live Transcription and Voice Commands**](https://arxiv.org/abs/2410.15608): 描述第一代模型架构，支持灵活时长输入窗口，改进了 Whisper 的固定 30 秒要求。
- [**Flavors of Moonshine: Tiny Specialized ASR Models for Edge Devices**](https://arxiv.org/abs/2509.0.553): 介绍我们如何通过训练单语模型提升非英语语言准确率。
- [**Moonshine v2: Ergodic Streaming Encoder ASR for Latency-Critical Speech Applications**](https://arxiv.org/abs/2602.12241): 引入我们的流式方法及其为实时语音应用带来的优势。

### Available Models（可用模型）

以下是当前可用的模型。获取方式见 [Downloading Models](#downloading-models)。本库使用 Onnx 模型格式，已转换为内存映射的 OnnxRuntime (`.ort`) flatbuffer 编码。`safetensor` 版本请参见 [HuggingFace](#huggingface) 章节。

| Language   | Architecture     | # Parameters | WER/CER |
| ---------- | ---------------- | ------------ | ------- |
| English    | Tiny             | 26 million   | 12.66%  |
| English    | Tiny Streaming   | 34 million   | 12.00%  |
| English    | Base             | 58 million   | 10.07%  |
| English    | Small Streaming  | 123 million  | 7.84%   |
| English    | Medium Streaming | 245 million  | 6.65%   |
| Arabic     | Base             | 58 million   | 5.63%   |
| Japanese   | Base             | 58 million   | 13.62%  |
| Korean     | Tiny             | 26 million   | 6.46%   |
| Mandarin   | Base             | 58 million   | 25.76%  |
| Spanish    | Base             | 58 million   | 4.33%   |
| Ukrainian  | Base             | 58 million   | 14.55%  |
| Vietnamese | Base             | 58 million   | 8.82%   |

英语评估使用 [HuggingFace OpenASR Leaderboard](https://huggingface.co/spaces/hf-audio/open_asr_leaderboard) 数据集和方法完成。其他语言使用 FLEURS 数据集和 [`scripts/eval-model-accuracy`](scripts/eval-model-accuracy.py) 脚本评估，按语言选择字符或词错误率。

如果你使用的是非拉丁字母模型（即除英语和西班牙语外的任何语言），需注意的一个常见问题是：创建 Transcriber 时需将 [`max_tokens_per_second` 选项](#transcriber-options) 设置为 13.0。这是因为最常见的幻觉模式是无限重复最后几个词，而我们检测此情况的启发式方法是检查片段时长内是否有异常高的 token 数量。不幸的是，由于我们的分词方式，非拉丁语言每秒的基础 token 数远高于英语，因此你必须手动调高阈值以避免截断有效输出。

### Domain Customization（领域定制）

通常能够针对应用中预期听到的特定词汇（如技术术语、俚语或特定方言/口音）校准语音转文字模型会很有用。[Moonshine AI 提供使用内部数据集进行完整重训练以进行定制的付费商业服务](mailto:contact@moonshine.ai)，我们希望在未来支持免费轻量级方法。你可以在社区项目 [github.com/pierre-cheneau/finetune-moonshine-asr](https://github.com/pierre-cheneau/finetune-moonshine-asr) 找到相关工作。

### Quantization（量化）

我们通常对所有模型统一采用八位权重，对 MatMul 等重操作采用八位计算。这全部是后训练量化，结合使用 OnnxRuntime 工具和 [我的 Onnx Shrink Ray 实用程序](https://pypi.org/project/onnx-shrink-ray/)。过程中唯一的例外是对前端的处理，它使用卷积层生成特征，产生与传统 MEL 频谱图预处理类似的结果，但以标准 ML 操作的学习方式进行。此初始阶段的输入对应于原始音频数据的 16 位有符号整数（尽管编码为浮点数），因此我们发现有必要将卷积运算至少保留在 B16 浮点精度下。 

你可以在 [scripts/quantize-streaming-model.sh](scripts/quantize-streaming-model.sh) 中看到我们用于转换的选项。

### HuggingFace（HuggingFace）

我们在 HF 组织页面上链接了模型的 `safetensors` 版本：[huggingface.co/UsefulSensors/models](https://huggingface.co/UsefulSensors/models)。组织名称来自公司早期形态，当时我们专注于提供集成在内置麦克风的低成本芯片上的完整语音交互解决方案。这些全部是从我们的训练管道导出的浮点检查点。

## API Reference（API 参考）

本文档涵盖 Python API，但所有其他支持语言中均存在相同的函数和类，仅带有原生适配（例如 CamelCase）。你可将其作为库运行平台的标准参考。

- [数据结构（Data Structures）](#data-structures)
  - [TranscriberLine](#transcriberline)
  - [Transcript](#transcript)
  - [TranscriptEvent](#transcriptevent)
  - [IntentMatch](#intentmatch)
  - [TtsVoiceEntry](#ttsvoiceentry)
  - [TtsVoicesByAvailability](#ttsvoicesbyavailability)
- [类（Classes）](#classes)
  - [Transcriber](#transcriber)
  - [MicTranscriber](#mictranscriber)
  - [Stream](#stream)
  - [TranscriptEventListener](#transcripteventlistener)
  - [IntentRecognizer](#intentrecognizer)
  - [DialogFlow](#dialogflow)
  - [Dialog](#dialog)
  - [TextToSpeech](#texttospeech)
  - [GraphemeToPhonemizer](#graphemetophonemizer)

### Data Structures（数据结构）

#### TranscriberLine

表示转录本中的单个“行”或语音片段。它包含话语的时序、说话人和文本内容信息，以及状态（如语音是否仍在进行中）。如果你正在构建涉及转录的应用，此数据结构提供了每行语音的所有可用信息。请注意，随着用户持续说话，每行可能会被多次更新以添加新文本及其他信息。

- `text`: 包含从此片段音频提取的 UTF-8 编码字符串。
- `start_time`: 浮点数，表示自当前会话开始以来首次检测到该话语的时间（秒）。
- `duration`: 浮点数，表示当前话语的持续时间（秒）。
- `line_id`: 无符号 64 位整数，以防碰撞方式表示行，用于存储并确保应用能跟踪随时间变化的行。详见 [Transcription Event Flow](#transcription-event-flow)。
- `is_complete`: 布尔值，在片段完成前为 false，之后剩余生命周期内为 true。

- `is_updated`: 布尔值，如果自上次转录更新以来行的任何信息已变更则为 true。由于库会在你添加音频块时定期内部更新转录本，因此不能依赖轮询此字段来检测变更。应改用事件/监听器流捕获修改。以下所有布尔值同理适用。
- `is_new`: 布尔值，指示该行是否由上次更新调用添加到转录本中。
- `has_text_changed`: 布尔值，如果行的文本内容在最后一次转录更新中被修改则设置。若已设置，`is_updated` 必然同时设置；但如果行的其他属性（如时长或音频数据）变更而文本保持不变，则 `is_updated` 可为 true 而 `has_text_changed` 为 false。

- `has_speaker_id`: 是否已识别该行说话人。除非传递给 Transcriber 的 `identify_speakers` 选项设为 false，否则在行完成时此值始终为 true，且可能更早设置。说话人识别过程仍处于实验阶段，当前准确率可能对某些应用不可靠。

- `speaker_id`: 独特的无符号 64 位整数，设计用于存储或在多次会话中标识同一说话人。

- `speaker_index`: 整数，表示说话人在转录本中出现的顺序，便于为说话人分配默认名称如 "Speaker 1:" 等。

- `audio_data`: 32 位浮点数组，表示该行基于的原始音频数据，格式为 0.0 到 1.0 之间的 16KHz 单声道 PCM 数据。这对进一步处理很有用（例如驱动视觉指示器或在行完成后喂入专用 STT 模型）。

#### Transcript

Transcript 包含按降序时间排列的 TranscriberLines 列表。每次调用 `Transcriber.start()` 时转录本都会重置，因此若需保留其中的信息，应显式复制。大多数应用不会直接与此结构交互，因为所有相同信息均可通过事件回调获取。

#### TranscriptEvent

包含关于转录本变更的信息。它有四个子类，在 [the transcription event flow section](#transcription-event-flow) 中有更详细说明。大部分信息包含在 `line` 成员中，此外还有 `stream_handle`，若你运行多个 Stream，应用可用它来区分行的来源。

#### IntentMatch

表示匹配意图的数据类，由 `get_closest_intents()` 返回并传递给 `set_on_intent()` 回调。

- `canonical_phrase`: 代表标准指令的字符串，与你向识别器注册时完全一致。
- `utterance`: 触发匹配的 utterance 文本。
- `similarity`: 浮点数，反映识别器对 utterance 与指令含义相同的置信度，0 为最低置信，1 为最高。
- `trigger_phrase`: `canonical_phrase` 的只读别名（向后兼容）。

#### TtsVoiceEntry

来自原生 TTS 目录的单行声音数据（作为 `get_tts_voice_catalog()` 返回映射的一部分）。

- `id`: 声音标识字符串（通常带 `kokoro_` 或 `piper_` 前缀以固定声码器）。
- `state`: `"found"`（已解析资产根下存在资产）或 `"missing"`（目录中列出但磁盘上尚未存在）。

#### TtsVoicesByAvailability

`list_tts_voices()` 返回的字典结构。

- `present`: 排序列表，包含查询所用资产根下已可用的声音 ID。
- `downloadable`: 排序列表，包含磁盘上尚不存在但可获取的目录声音 ID（例如使用 `download=True` 构造 `TextToSpeech` 时）。

### Classes（类）

#### Transcriber

处理语音转文字流水线。

- <a id="transcriber-init"></a>`__init__()`: 加载并初始化 Transcriber。
  - `model_path`: 包含完整流程所需组件模型文件的目录路径。**注意**：这是 **文件夹** 的路径，而非单个 **文件**。你可以使用 [download_model()](#downloading-models) 函数下载并获得标准模型的缓存版本路径。
  - `model_arch`: 要加载的模型架构，从 `ModelArch` 定义的选项中选择。
  - `update_interval`: 默认情况下 Transcriber 会定期运行文本转录以触发更新事件。此值指定 STT 模型运行的频率。你可以将其设为较大时长以抑制行开始与结束之间的更新，但由于流式模型在最终 STT 阶段前已完成大量工作，这可能不会大幅降低整体延迟。
  - <a id="transcriber-options"></a>`options`: 影响库内转录过程工作方式标志的字典映射（字符串到字符串），通常启用性能优化或调试日志。即使值需解释为数字也传递字符串——例如 `{"max_tokens_per_second", "15"}`。
    - `skip_transcription`: 若你仅需语音活动检测和分段，但想在应用中进行进一步处理，可设为 "true"，随后使用每行的 `audioData` 数组。
    - `max_tokens_per_second`: 模型偶尔会陷入无限解码循环，不断重复相同词语。作为检测启发式方法，我们将当前运行的 token 数与音频时长对比，若 token 过多则截断解码。默认设为 6.5，但对于产生大量每秒原始 token 的非英语语言，你可能希望将其调至 13.0。
    - `transcription_interval`: 运行转录的频率（秒）。
    - `vad_threshold`: 控制初始语音活动检测阶段的灵敏度，决定如何将原始音频切分为片段。默认为 0.5，较低值生成较长片段（可能包含更多背景噪声段），较高值将 speech 拆分为较小块，但存在因裁剪丢失实际语音的风险。
    - `save_input_wav_path`: 转录质量差的最常见原因之一是喂入流水线的音频转换错误或损坏。若将此选项设为文件夹路径，Transcriber 会将接收到的内容精确保存为 16KHz 单声道 WAV 文件，以便你确保输入音频符合预期。
    - `log_api_calls`: 另一调试选项，开启后每次调用库中 C API 入口点时都会将参数信息写入 stderr 或控制台。
    - `log_ort_runs`: 打印 ONNXRuntime 推理运行及其耗时信息。
    - `vad_window_duration`: VAD 每 30ms 运行一次，但为获得更高置信度值我们随时间平均结果。此值为平均时长（秒）。默认为 0.5s，较短间隔更快检测 speech 但精度较低，较高值可能提升精度但代价是错过短 utterance。
    - `vad_look_behind_sample_count`: 由于我们随时间平均，均值 VAD 信号会滞后于初始语音检测。为补偿此延迟，检测到 speech 时我们会拉取平均值通过阈值前的一些音频。此值为要前置的样本数，默认为 8192（均为 16KHz）。
    - `vad_max_segment_duration`: 在快速连续 speech 中寻找间隙可能很困难，但许多应用希望文本以非无限块呈现。此选项设置行标记为完成并启动新片段前的最大时长。默认为 15 秒，为提高找到自然停顿的几率，`vad_threshold` 会随时间线性从最大时长的三分之二降至最大值。
    - `identify_speakers`: 布尔值，控制是否运行流水线中的说话人识别阶段。
    - `return_audio_data`: 默认情况下 Transcriber 返回与文本行对应的音频数据片段连同转录结果。若需减少内存开销可禁用此功能。
    - `log_output_text`: 启用后 STT 模型结果将记录到控制台。

- <a id="transcriber-transcribe-without-streaming"></a>`transcribe_without_streaming()`: 便捷函数，用于从非实时音频源（如文件）提取文本。我们针对流式用例优化，因此若频繁使用且有性能约束，可能更适合使用专攻批量转录的库。此方法仍会调用已注册的事件监听器处理行，因此可用于测试应用或轻松集成离线音频源。
  - `audio_data`: 32 位浮点数组，表示 -1.0 到 1.0 之间的单声道 PCM 音频，用于分析语音。
  - `sample_rate`: 每秒样本数。库内部使用此值转换为工作速率（16KHz）。
  - `flags`: 整数，当前未使用。

- <a id="transcriber-start"></a>`start()`: 开始新的转录会话。创建 `Transcriber` 后且在添加任何音频前需调用此方法。
- <a id="transcriber-stop"></a>`stop()`: 结束转录会话。若语音片段仍在活跃，标记为完成并调用相应事件处理器。
- <a id="transcriber-add-audio"></a>`add_audio()`: 每次从输入获取新音频块时调用以开始处理。音频大小和采样率应为源数据的自然格式，库会处理所有转换。
  - `audio_data`: 表示单声道 PCM 音频块的 32 位浮点数组。
  - `sample_rate`: 输入音频中每秒样本数。库使用此值将数据转换为其首选速率。
- <a id="transcriber-update-transcription"></a>`update_transcription`: 转录本通常随音频添加定期更新，但若需手动触发（例如用户按下刷新时）或想访问完整转录本，可手动调用此方法。
  - `flags`: 整数，使用位或 (`|`) 组合的标志。
    - `MOONSHINE_FLAG_FORCE_UPDATE`: 默认情况下若自上次转录以来新音频少于 200ms，Transcriber 返回缓存版转录本，但设置此项可确保无论何种情况均触发转录。

- <a id="transcriber-create-stream"></a>`create_stream()`: 若应用从多个源接收音频输入（如麦克风和系统音频），则需在单个 Transcriber 上创建多个 Stream 以避免加载多份模型副本。每个 Stream 拥有独立转录本，行事件标记其来源 Stream Handle。若只需处理单一输入无需关心此项，直接使用 `Transcriber` 类的 `start()`、`stop()` 等即可。此函数返回 `Stream` 类对象。
  - `flags`: 整数，保留用于未来扩展。
  - `update_interval`: 转录更新之间的周期（秒）。

- <a id="transcriber-add-listener"></a>`add_listener()`: 向 Transcriber 注册可调用对象。该对象将在音频输入和文本提取时被回调。
  - `listener`: 通常是 `TranscriptEventListener` 的子类，但也可以是普通函数。定义语音事件发生时调用的代码。

- <a id="transcriber-remove-listener"></a>`remove_listener()`: 删除监听器使其不再接收事件。
  - `listener`: 你之前传入 `add_listener()` 的对象。

- <a id="transcriber-remove-all-listeners"></a>`remove_all_listeners()`: 删除所有已注册监听器，使它们均不再接收事件。

#### MicTranscriber（MicTranscriber）

此类支持 [`Transcriber`](#transcriber) 的 [`start()`](#transcriber-start)、[`stop()`](#transcriber-stop) 和监听器函数，但内部创建并附加到系统麦克风输入，因此你无需自行调用 [`add_audio()`](#transcriber-add-audio)。在 Python 中此使用 [`sounddevice` 库]()，在其他语言中该类底层使用原生音频 API。

#### Stream（Stream）

当你需将多个音频输入喂入单个 Transcriber 时的访问入口。支持 [`Transcriber`](#transcriber) 类文档中记录的 [`start()`](#transcriber-start)、[`stop()`](#transcriber-stop)、[`add_audio()`](#transcriber-add-audio)、[`update_transcription()`](#transcriber-update-transcription)、[`add_listener()`](#transcriber-add-listener)、[`remove_listener()`](#transcriber-remove-listener) 和 [`remove_all_listeners()`](#transcriber-remove-all-listeners)。

#### TranscriptEventListener（TranscriptEventListener）

用于派生自定义监听器代码的便捷类。重写 `on_line_started()`、`on_line_updated()`、`on_line_text_changed()` 和 `on_line_completed()` 中的任意或全部方法，它们将在对应事件发生时被回调。

#### IntentRecognizer（IntentRecognizer）

一种特殊的事件监听器类型，作为监听器添加到 `Transcriber`，随后分析转录结果以确定是否说出了指定指令中的任何内容，使用自然语言模糊匹配。

- <a id="intentrecognizer-init"></a>`__init__()`: 构造新识别器，加载所需模型。
  - `model_path`: 字符串，包含所需嵌入模型文件的文件夹路径。你可通过调用 `download_embedding_model()` 下载并获得路径。
  - `model_arch`: `EmbeddingModelArch`，从 `download_embedding_model()` 函数获取。
  - `model_variant`: 运行模型的精度。推荐 "q4"。
  - `threshold`: utterance 需多接近目标句子才能触发事件。
- <a id="intentrecognizer-register-intent"></a>`register_intent()`: 注册识别器匹配的标准短语，可选预计算嵌入和优先级。
  - `trigger_phrase`: 要匹配的标准指令句。
  - `handler`: *(可选)* 可调用 `(canonical_phrase, utterance, similarity) -> None`，由 `process_utterance()` 为最佳匹配项调用。
  - `embedding`: *(可选，关键字参数)* 表示预计算嵌入的浮点数列表。当 `None`（默认）时原生库自动从 `trigger_phrase` 计算嵌入。使用 `calculate_embedding()` 预计算嵌入。
  - `priority`: *(可选，关键字参数)* 整数优先级。在 `get_closest_intents()` 中高优先级意图排在低优先级之上，即使其相似度分数较低。默认为 `0`。
- <a id="intentrecognizer-unregister-intent"></a>`unregister_intent()`: 从识别器移除意图。
  - `trigger_phrase`: 要移除的意图触发短语。
- <a id="intentrecognizer-calculate-embedding"></a>`calculate_embedding()`: 计算句子的嵌入向量。这对预计算嵌入以便后续通过 `embedding` 参数传递给 `register_intent()`，或外部存储嵌入很有用。
  - `sentence`: 要嵌入的输入文本。
  - `model_name`: *(可选，关键字参数)* 保留用于未来使用；传递 `None`。
  - **返回**: 表示嵌入向量的浮点数列表。
- <a id="intentrecognizer-get-closest-intents"></a>`get_closest_intents()`: 按与 utterance 的相似度排名返回已注册意图。
  - `utterance`: 要匹配已注册意图的口语文本。
  - `tolerance_threshold`: *(可选)* 最小相似度阈值。未提供时使用实例 `threshold`。
  - **返回**: 按优先级（降序）、然后相似度（降序）排序的 `IntentMatch` 对象列表。
- <a id="intentrecognizer-intent-count"></a>`intent_count()`: 返回已注册意图数量。
- <a id="intentrecognizer-clear-intents"></a>`clear_intents()`: 从识别器移除所有已注册意图。
- <a id="intentrecognizer-set-on-intent"></a>`set_on_intent()`: 设置可调用对象，当任何注册动作触发时被调用（不仅限于单个指令，区别于 `register_intent()`）。

#### DialogFlow（DialogFlow）

驱动基于生成器对话流程的调度器。你向触发短语注册流函数，调度器将完成的转录行路由到其配置的 `IntentRecognizer`（无活跃流时）或当前挂起的生成器（有活跃流时）。它实现了 [`TranscriptEventListener`](#transcripteventlistener) 接口，因此你可以像附加 `IntentRecognizer` 一样通过 [`add_listener()`](#transcriber-add-listener) 将其附加到 `Transcriber` 或 `MicTranscriber`。用法示例见 [Getting Started with a Conversational Agent](#getting-started-with-a-conversational-agent)。

流是普通 Python 生成器函数，接收 [`Dialog`](#dialog) 作为参数并 yield 提示对象返回给调度器。调度器执行每个提示（说话、等待用户回复）并通过 `.send()` 将答案恢复生成器。这让你使用常规 Python 控制流编写多步骤分支对话，包括循环和异常处理器，无需任何异步机制。触发匹配、确认和选项选择均通过嵌入模型语义完成，因此替代说法无需枚举即可工作。

- <a id="dialogflow-init"></a>`__init__()`: 构造调度器，可选 TTS、意图识别器和音频管道钩子。所有参数均为关键字参数。
  - `tts`: 可选 [`TextToSpeech`](#texttospeech) 实例用于朗读提示。设置后调度器调用 `tts.say(text)` 并在恢复流之前阻塞于 `tts.wait()`。若 `tts.play_success` 和 `tts.play_error` 可用则自动接线为识别提示音回调。
  - `intent_recognizer`: 可选 [`IntentRecognizer`](#intentrecognizer) 用于计算驱动触发短语匹配的嵌入。未匹配任何注册流或全局的 utterance 也会转发至此识别器供应用层处理。
  - `speak_fn`: 可选可调用 `(text) -> None`，朗读文本并阻塞直到播放完成。设置时覆盖 `tts`，对测试和替代 TTS 后端很有用。
  - `mute_fn`: 可选可调用 `(should_mute: bool) -> None`，在每个朗读提示前后调用以便在助手说话时静音麦克风，避免代理转录自身。
  - `spelling_mode_fn`: 可选可调用 `(active: bool) -> None`，每当调度器进入或离开 `SPELLED` / `DIGITS` 提示时调用。将其接线到底层 Transcriber 的 `set_transcribe_flags()` 以仅在预期拼写输入时翻转 `MOONSHINE_FLAG_SPELLING_MODE`，从而对密码和代码听写使用拼写-CNN 融合路径而不干扰自由格式识别。
  - `success_beep_fn`: 可选可调用 `() -> None`，在完成的转录行被识别且任何 TTS 回复开始前播放。当 `tts` 暴露一个时默认为 `tts.play_success()`。传递 `lambda: None` 静音。
  - `error_beep_fn`: 可选可调用 `() -> None`，在未识别完成的转录行时播放：无触发匹配、无活跃流能解释它且无全局处理器接管它。可用时默认为 `tts.play_error()`。
  - `trigger_threshold`: 0 到 1 之间的浮点数，设置 utterance 计为匹配已注册触发短语所需的最低嵌入相似度分数。默认为 `0.7`。
  - `spell_feedback`: 布尔值（默认 `True`），控制是否在 `SPELLED` / `DIGITS` 提示期间识别的每个字符都作为确认回显给用户，以及 `"deleting <character>"` 用于撤销命令。传递 `False` 静音逐字回显（例如未接线 TTS 时）。
  - `ignore_stt_during_tts`: 布尔值（默认 `True`）。设置后，调度器处于提示中间时（即 TTS 正在积极朗读）到达的每个 utterance 在推进流、匹配全局触发或落入意图识别器之前被丢弃。这防止了在回声消除较弱的设备上自我捕获。仅在拥有可靠回声消除且想要打断功能时禁用。
  - `log_io`: 布尔值（默认 `False`）。启用后调度器接收的每个 utterance 和助手朗读的每个提示均以干净的 `user: ...` / `assistant: ...` 格式记录到 stderr。区别于 `debug`：这是用户可见对话转录本，不含冗长内部跟踪。
  - `debug`: 布尔值（默认 `False`）。启用后带有每步和累计计时的阶段转换跟踪写入 stderr，对诊断延迟或缺失提示音问题很有用。

- <a id="dialogflow-register-flow"></a>`register_flow()`: 注册流生成器函数，当触发短语匹配到达 utterance 时启动。
  - `trigger_phrase`: 标准短语，在注册时嵌入一次并通过余弦相似度与 utterance 对比，因此相同含义的替代说法都会启动该流。
  - `flow`: 接收 [`Dialog`](#dialog) 并返回 yield 提示的生成器的可调用对象。通常为生成器函数。

- <a id="dialogflow-unregister-flow"></a>`unregister_flow()`: 移除先前注册的流。若移除了流返回 `True`，否则 `False`。
  - `trigger_phrase`: 注册流时使用的触发短语。

- <a id="dialogflow-register-global"></a>`register_global()`: 注册始终活跃的短语，即使在流运行时也有效。适用于 "cancel" 或 "start over" 等应中断任何进行中的对话的指令。
  - `trigger_phrase`: 要匹配的标准短语，与 `register_flow()` 相同方式。
  - `handler`: 接收当前 [`Dialog`](#dialog) 并返回可选提示以朗读（或 `None`）的可调用对象。处理器也可调用 `d.cancel()` 或 `d.restart()` 放弃或重置活跃流。

- <a id="dialogflow-process-utterance"></a>`process_utterance()`: 手动路由 utterance，不经过转录事件。若 utterance 被流或全局处理器消耗返回 `True`，否则 `False`。对单元测试或从非 `Transcriber` 输入源驱动调度器很有用。
  - `utterance`: 要路由的字符串。

- <a id="dialogflow-cancel-active"></a>`cancel_active()`: 放弃当前运行的流（若有）。若取消了流返回 `True`。

- <a id="dialogflow-say"></a>`say()`: 通过配置的 TTS 朗读 `text`，不在任何流内。适用于欢迎消息、状态公告和无需完整流注册的错误通知。阻塞直到播放完成，并与流内提示共享相同播放路径，因此 `mute_fn` 和自我捕获抑制仍然适用。
  - `text`: 要朗读的字符串。

- `is_active`: 只读布尔属性，当流正在进行时为 `True`。
- `active_trigger`: 只读属性返回活跃流的触发短语，若无活跃流则为 `None`。
- `registered_flows`: 只读列表包含所有已注册流触发短语。

`DialogFlow` 也实现了 [`TranscriptEventListener`](#transcripteventlistener) 接口，因此一旦你通过 `transcriber.add_listener(dialog_flow)` 附加它，完成的行会自动通过 `process_utterance()` 路由，无需你自己调用。

#### Dialog（Dialog）

作为第一个参数传递给每个流函数的上下文对象。每个方法返回提示对象供流 `yield` 回调度器；调度器随后执行该提示（朗读文本、等待输入）并将结果（若有）通过 `.send()` 发回生成器。`Dialog` 本身不执行 I/O，因此流可通过构造 `Dialog`、调用流函数并手动驱动生成的生成器进行单元测试，无需任何音频、TTS 或事件循环。

- `trigger_phrase`: 启动流的短语，对流函数可用为 `d.trigger_phrase`。
- `state`: 流的每次对话状态 `dict`，初始为空。

- <a id="dialog-say"></a>`say()`: 返回提示对象，yield 后朗读 `text` 并在播放完成后恢复流。流从 `yield` 接收 `None`。
  - `text`: 助手要朗读的字符串。
  - `barge_in`: 保留用于未来使用；支持时将允许用户通过说话打断播放。

- <a id="dialog-ask"></a>`ask()`: 返回提示对象，提出问题并以用户的下一个 utterance（作为字符串）恢复流。
  - `prompt`: 助手在监听前朗读的字符串。
  - `mode`: `FREE`（自由格式自然语言输入，默认）、`SPELLED`（用户逐个字符听写，以 "done"/"stop"/"finish" 终止，逐字回显反馈并支持北约音标字母表单词和 "delete"/"undo" 命令）、`DIGITS`（仅数字拼写输入）或 `PHRASE`（单个短语）。这些常量从 `moonshine_voice` 包导出。
  - `bias_terms`: 可选字符串列表，识别器在解释回复时应偏向的术语。
  - `timeout`: 等待回复前的秒数，超时后重新提示。默认为 8 秒。
  - `no_input_reprompt`: 超时无输入时重新提示用户的模板。`{prompt}` 替换为原始提示文本。传递 `None` 跳过重提示。
  - `max_retries`: 在流中引发 `NoInputError` 前的重提示次数。默认为 2。

- <a id="dialog-confirm"></a>`confirm()`: 返回提示对象，提出是/否问题并以 `bool` 恢复流。匹配为语义化，因此 "okay"、"affirmative" 和 "go ahead" 均计为 yes，而 "no"、"cancel" 和 "stop" 计为 no。
  - `prompt`: 助手要朗读的是/否问题。
  - `timeout`: 等待回复前的秒数。默认为 6 秒。
  - `max_retries`: 在流中引发 `NoMatchError` 前的重提示次数。默认为 1。

- <a id="dialog-choose"></a>`choose()`: 返回提示对象，要求用户从命名选项集中选择并以匹配选项的键（字符串）恢复流。每个选项键关联一组短语；使用嵌入模型对键及其短语的并集进行匹配。
  - `prompt`: 助手要朗读的字符串。
  - `options`: 选项键到可能说出的关联短语列表的映射。
  - `timeout`: 等待回复前的秒数。默认为 8 秒。
  - `max_retries`: 引发 `NoMatchError` 前的重提示次数。默认为 2。

- <a id="dialog-cancel"></a>`cancel()`: 向生成器抛出 `DialogCancelled` 以完全放弃活跃流。通常由通过 `DialogFlow.register_global()` 注册的全局处理器调用。

- <a id="dialog-restart"></a>`restart()`: 向生成器抛出 `DialogRestart` 从头重启活跃流。通常由全局处理器调用。

- <a id="dialog-replay-last-prompt"></a>`replay_last_prompt()`: 返回重新朗读最近问题的 `Say` 提示。适用于全局 "repeat" / "say that again" 处理器；若尚未朗读任何内容则返回 `None`。

#### TextToSpeech（TextToSpeech）

使用 Moonshine 原生栈（Kokoro 和 Piper 声码器及每语言 G2P 资产）的设备端文字转语音。所需文件从 CDN 解析，除非你传递 `download=False` 并提供已填充的目录树。无效的语言标签抛出 `MoonshineTtsLanguageError`；缺失或未知声音抛出 `MoonshineTtsVoiceError`。来自 `say()` 的播放失败抛出 `MoonshineAudioOutputError`（枚举成功时附带输出设备列表）。

`say()` 非阻塞且排队：每次调用立即返回，utterance 由后台流水线按序播放。专用合成线程在当前 utterance 播放时预合成下一个 utterance，最小化连续 utterance 之间的间隙。使用 `stop()` 取消所有待处理语音，`wait()` 阻塞直到全部播放完成，`is_talking()` 轮询播放状态。Python、Swift 和 Android（Java）均提供相同 API 形状。

使用 `list_tts_languages()`、`list_tts_voices()` 和 `get_tts_voice_catalog()` 发现支持标签和声音。资产布局和许可证总结在 [`core/moonshine-tts/data/README.md`](core/moonshine-tts/data/README.md)；另见 [Downloading Models](#text-to-speech-models)。

- <a id="texttospeech-init"></a>`__init__()`: 创建合成器并可选将依赖项下载到包缓存（或自定义根目录）。
  - `language`: BCP-47 风格标签用于说话区域设置（例如 `en_us`, `de`, `fr`）。别名如 `en-us` 由库规范化。
  - `voice`: 可选声音 ID。前缀 `kokoro_` 或 `piper_` 选择声码器（例如 `kokoro_af_heart`）。当 `download` 为 true 时，目录中尚未在磁盘上的已注册声音会自动下载。
  - `options`: 可选字符串到字符串、数字或布尔值的映射，透传给原生选项解析器（见下文）。Python 绑定始终将 `g2p_root` 设为解析后的资产目录；不要依赖覆盖该键以适配不同布局——改用 `asset_root` / `tts_root` 风格选项。
  - `asset_root`: 可选目录用作 TTS 缓存或磁盘上资产树。当 `download` 为 true 时，下载内容置于该根目录下（若设置）；为 false 时此路径必须已包含预期的 `g2p_root` 布局。
  - `download`: 为 true（默认）时缺失 TTS 资产从 `https://download.moonshine.ai/tts/` 下载。为 false 时必需 `asset_root` 且必须已包含原生层期望的文件。

- `language`: 只读属性返回正在使用的规范化语言标签。

- `asset_root`: 只读属性返回传递给原生层的 `pathlib.Path` 目录作为 `g2p_root`。

- <a id="texttospeech-synthesize"></a>`synthesize()`: 将 `text` 转换为单声道 PCM 音频。
  - `text`: 要朗读的 UTF-8 字符串。
  - `options`: 仅本次调用可选额外原生选项（在 C 侧与构造函数的 `options` 语义合并，如文档所述）。
  - 返回元组 `(samples, sample_rate)`，其中 `samples` 是约 −1.0…1.0 范围的 32 位浮点数列表，`sample_rate` 是输出采样率（Hz）。

- <a id="texttospeech-say"></a>`say()`: 排队文本进行合成和播放，立即返回。后台合成线程将文本转换为音频，然后交给播放线程在选定输出设备上播放。下一个 utterance 的合成与当前播放重叠。Python 需要 `pip install numpy sounddevice`。
  - `text`: 要朗读的字符串或字符串列表。列表等效于按序对每个元素调用一次 `say()`。
  - `device`: (Python/Swift-macOS) `None` 为主机默认输出，整数 PortAudio 输出设备索引，十进制字符串索引，或设备名称的不区分大小写子串。Android 上传递 `Context`（必需）和可选 `AudioDeviceInfo`。
  - `options`: 可选每次调用原生选项，透传给合成器不变。

- <a id="texttospeech-stop"></a>`stop()`: 清除 utterance 队列并停止当前任何音频播放。在所有待处理 utterance 被丢弃且活跃播放已停止后返回。之后安全地再次调用 `say()`。

- <a id="texttospeech-wait"></a>`wait()`: 阻塞调用线程直到所有排队 utterance 合成完毕并播放完成。Android 上命名为 `waitUntilDone()`。

- <a id="texttospeech-is-talking"></a>`is_talking()`: 若仍有 utterance 排队、正在合成或当前播放中返回 `True`。Swift 和 Android 上命名为 `isTalking()`。

- <a id="texttospeech-close"></a>`close()`: 停止任何进行中的播放，丢弃待处理 utterance，释放原生合成器句柄。使用 `with TextToSpeech(...) as tts:` 块或垃圾回收时自动调用。

<a id="texttospeech-options"></a>**常见 `options` 键（TTS）：** 这些镜像 C++ 层的 `MoonshineTTSOptions`。值在底层 API 中为字符串；Python 绑定按注明接受布尔值和数字。

- `tts_root`, `path_root`, `model_root`: 资产根目录别名，当你需要覆盖布局发现时使用（与原生解析器中的 `g2p_root` 角色相同）。
- `voice`: 未传入构造函数时的默认声音 ID（典型使用中两者均设置时构造函数参数优先）。
- `speed`: 语速乘数（浮点数）。
- `kokoro_dir`, `kokoro_model` / `kokoro_model_onnx`, `kokoro_config` / `kokoro_config_json`: 覆盖资产树中 Kokoro ONNX 和配置的路径。
- `piper_onnx` / `piper_model_onnx`, `piper_onnx_json`, `piper_voices_dir` / `voices_dir`, `piper_voices_json_dir` / `voices_json_dir`: 覆盖 Piper 模型、JSON 辅助文件和声音目录的路径。
- `normalize_audio` / `piper_normalize_audio`（遗留别名）, `output_volume` / `piper_output_volume`（遗留别名）：应用于 Kokoro 和 Piper 输出的共享后合成效果（峰值归一化，应用增益，然后裁剪到 `[-1, 1]`）。
- `piper_noise_scale` / `piper_noise_scale_override`, `piper_noise_w` / `piper_noise_w_override`: Piper 推理调优（类型见原生选项解析）。

额外键转发至 G2P 选项解析器（语言特定 ONNX 覆盖、功能标志等）。

#### GraphemeToPhonemizer（GraphemeToPhonemizer）

IPA 字符串生成无需语音合成。依赖项与 TTS 相同 CDN 词典和 ONNX 捆绑包，但仅限于 `moonshine_get_g2p_dependencies` 报告的语言所需内容。当 `download` 为 true 时资产放置于包缓存或 `asset_root`；为 false 时 `asset_root` 必须已包含这些文件。

- <a id="graphemetophonemizer-init"></a>`__init__()`: 创建原生 G2P 句柄。
  - `language`: 区域设置标签（例如 `en_us`, `ja`）。与 TTS 相同方式规范化。
  - `options`: 可选映射传递给原生层（仅 G2P 键；绑定自动设置 `g2p_root`）。
  - `asset_root`: 可选缓存或预填充目录，语义同 `TextToSpeech`。
  - `download`: 为 true（默认）时下载缺失 G2P 资产。为 false 时必需 `asset_root`。

- `language`: 只读规范化标签。

- `asset_root`: 只读 `pathlib.Path` 用作 `g2p_root` 的目录。

- <a id="graphemetophonemizer-to-ipa"></a>`to_ipa()`: 返回输入文本的单条 IPA 字符串。
  - `text`: UTF-8 表面字符串。
  - `options`: 可选每次调用原生 G2P 选项。

- <a id="graphemetophonemizer-close"></a>`close()`: 释放原生句柄；也由上下文管理器退出和 `__del__` 调用。

## Support（支持）

我们的主要支持渠道是 [Moonshine Discord](https://discord.gg/27qp9zSRXF)。我们会尽力回复该处的提问，以及其他渠道如 [GitHub issues](https://github.com/moonshine-ai/moonshine/issues)。我们也为需要跨平台移植或加速、模型定制、更多语言或其他服务的商业客户提供付费支持，请 [联系我们](mailto:contact@moonshine.ai)。

## Roadmap（路线图）

本库处于活跃开发中，我们计划实现：

- 移动端部署的二进制体积缩减。
- 更多语言支持。
- 更多流式模型。
- 改进的说话人识别。
- 轻量级领域定制。

## Acknowledgements（致谢）

感谢以下贡献者：

- Lambda 和 Stephen Balaban 通过 [他们的底层模型资助](https://lambda.ai/research) 支持我们的模型训练。
- ONNX Runtime 社区构建 [快速跨平台推理引擎](https://github.com/microsoft/onnxruntime)。
- [Alexander Veysov](https://github.com/snakers4) 提供出色的 [Silero 语音活动检测器](https://github.com/snakers4/silero-vad)。
- [Viktor Kirilov](https://github.com/onqtam) 提供 [优秀的 DocTest C++ 测试框架](https://github.com/doctest/doctest)。
- [Nemanja Trifunovic](https://github.com/nemtrif) 提供 [非常实用的 UTF8 CPP 库](https://github.com/nemtrif/utfcpp)。
- [Pyannote 团队](https://www.pyannote.ai/) 开放其说话人嵌入模型。
- [espeak-ng 社区](https://github.com/espeak-ng/espeak-ng/)，感谢他们解决将书面文字转换为语音的无尽复杂性的启发工作。
- [CMU Pronouncing Dictionary](https://github.com/cmusphinx/cmudict) 和 [eSpeak NG](https://github.com/espeak-ng/espeak-ng) 提供英语 G2P 词典和发音过滤（[`core/moonshine-tts/data/en_us`](core/moonshine-tts/data/en_us)）。
- [open-dict-data/ipa-dict](https://github.com/open-dict-data/ipa-dict) 提供跨多区域设置的 IPA 词典数据（[`core/moonshine-tts/data`](core/moonshine-tts/data)）。
- [WikiPron](https://github.com/CUNY-CL/wikipron) (CUNY-CL) 提供意大利语、俄语和欧洲葡萄牙语发音。
- [Koichi Yasuoka](https://huggingface.co/KoichiYasuoka) 提供 Hugging Face 模型 [chinese-roberta-base-upos](https://huggingface.co/KoichiYasuoka/chinese-roberta-base-upos), [roberta-small-japanese-char-luw-upos](https://huggingface.co/KoichiYasuoka/roberta-small-japanese-char-luw-upos) 和 [roberta-base-korean-morph-upos](https://huggingface.co/KoichiYasuoka/roberta-base-korean-morph-upos)。
- [hexgrad/Kokoro-82M](https://huggingface.co/hexgrad/Kokoro-82M) 和 [onnx-community/Kokoro-82M-ONNX](https://huggingface.co/onnx-community/Kokoro-82M-ONNX) 提供 Kokoro TTS 权重和 ONNX（[`core/moonshine-tts/data/kokoro`](core/moonshine-tts/data/kokoro)）。
- [PiperTTS](https://huggingface.co/rhasspy/piper-voices) 提供出色的轻量级 TTS 模型。
- [MyShell](https://myshell.ai) 的 [MeloTTS](https://github.com/myshell-ai/MeloTTS) 作为韩语 Piper 声音训练的参考（[`core/moonshine-tts/data/ko`](core/moonshine-tts/data/ko)）。
- [English Wiktionary](https://en.wiktionary.org/wiki/Wiktionary:Copyrights) 和 [hermitdave/FrequencyWords](https://github.com/hermitdave/FrequencyWords) 提供印地语词典材料（[`core/moonshine-tts/data/hi`](core/moonshine-tts/data/hi)）。
- [hbenbel/French-Dictionary](https://github.com/hbenbel/French-Dictionary) 提供相关法语连读词典工作（[`core/moonshine-tts/data/fr`](core/moonshine-tts/data/fr)）。
- [AbderrahmanSkiredj1/arabertv02_tashkeel_fadel](https://huggingface.co/AbderrahmanSkiredj1/arabertv02_tashkeel_fadel) 提供阿拉伯语标音，[CAMeL Tools](https://camel-tools.readthedocs.io/) 提供可选阿拉伯语 MSA 词典构建（[`core/moonshine-tts/data/ar_msa`](core/moonshine-tts/data/ar_msa)）。

## License（许可证）

除 `core/third-party` 中的源代码外，本代码采用 MIT License 许可，详见仓库中的 LICENSE。

英语模型也采用 MIT License 发布。其他语言模型采用 [Moonshine Community License](https://moonshine.ai) 发布，为非商业许可证。

`core/third-party` 中的代码根据其来源开源项目的条款许可，详细信息在各子文件夹的 LICENSE 文件中。

文字转语音和字素到音素模型及数据文件按其 readmes 和源仓库中列出的条款许可。各语言详情和再生说明位于 [`core/moonshine-tts/data/`](core/moonshine-tts/data/README.md)。
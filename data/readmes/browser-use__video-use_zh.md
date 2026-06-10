<p align="center">
  <img src="static/video-use-banner.png" alt="video-use" width="100%">
</p>

# video-use

介绍 **video-use** —— 使用 Claude Code 编辑视频。100% 开源。

将原始素材放入文件夹，与 Claude Code 对话，即可得到 `final.mp4`。适用于任何内容类型——口播、混剪、教程、旅行记录、访谈等——无需预设或菜单。

## What it does（功能特性）

- **自动剔除语气词**（如“嗯”、“呃”）、口误及镜头间的空白停顿
- **自动调色**每个片段（暖色调电影感、中性高对比，或自定义 `ffmpeg` 滤镜链）
- **每次剪辑处添加 30ms 音频淡入淡出**，避免爆音/咔哒声
- **以你的风格烧录字幕**——默认使用双词大写块显示，支持完全自定义
- **生成动画叠加层**：通过 [HyperFrames](https://github.com/heygen-com/hyperframes)、[Remotion](https://www.remotion.dev/)、[Manim](https://www.manim.community/) 或 PIL 实现——由并行子 Agent（每个动画一个）生成
- **自我评估渲染输出**：在展示前对每次剪辑边界进行自检
- **持久化会话记忆**：保存在 `project.md` 中，以便下周的会话能接续你之前的进度

## Setup prompt（设置提示词）

将其粘贴到 Claude Code、Codex、Hermes、Openclaw，或任何具有 Shell 访问权限的 Agent 中：

```text
Set up https://github.com/browser-use/video-use for me.

Read install.md first to install this repo, wire up ffmpeg, register the skill with whichever agent you're running under, and set up the ElevenLabs API key — ask me to paste it when you need it. Then read SKILL.md for daily usage, and always read helpers/ because that's where the editing scripts live. After install, don't transcribe anything on your own — just tell me it's ready and wait for me to drop footage into a folder.
```

Agent 会处理代码克隆、依赖安装、技能注册，并仅提示你输入一次 ElevenLabs API Key（可在 [elevenlabs.io/app/settings/api-keys](https://elevenlabs.io/app/settings/api-keys) 获取）。

随后将你的 Agent 指向包含原始素材的文件夹：

```bash
cd /path/to/your/videos
claude    # or codex, hermes, etc.
```

若需从你自己的 VPS 或 Telegram 实现持续运行的编辑，可通过 [Browser Use Box](https://browser-use.com/bux) 运行该 Agent。[观看 15 秒演示视频](https://www.tiktok.com/@browser_use/video/7639824093721758989)。

在会话中：

> edit these into a launch video（将这些素材剪辑成发布视频）

Agent 会盘点源文件、提出剪辑策略，等待你的确认后，生成 `edit/final.mp4`。所有输出均位于 `<videos_dir>/edit/` 目录下——技能目录保持整洁。

## Manual install（手动安装）

如果你想手动操作：

```bash
# 1. Clone and symlink into your agent's skills directory
git clone https://github.com/browser-use/video-use ~/Developer/video-use
ln -sfn ~/Developer/video-use ~/.claude/skills/video-use        # Claude Code
# ln -sfn ~/Developer/video-use ~/.codex/skills/video-use       # Codex

# 2. Install deps
cd ~/Developer/video-use
uv sync                         # or: pip install -e .
brew install ffmpeg             # required
brew install yt-dlp             # optional, for downloading online sources

# 3. Add your ElevenLabs API key
cp .env.example .env
$EDITOR .env                    # ELEVENLABS_API_KEY=...
```

## How it works（工作原理）

LLM 从不“观看”视频。它通过两个层级来**读取**内容，从而获得以词边界精度进行剪辑所需的全部信息。

<p align="center">
  <img src="static/timeline-view.svg" alt="timeline_view composite — filmstrip + speaker track + waveform + word labels + silence-gap cut candidates" width="100%">
</p>

**第一层——音频转录（始终加载）**：每个源文件调用一次 ElevenLabs Scribe，即可获取词级时间戳、说话人分离结果及音频事件（如 `(laughter)` 笑声、`(applause)` 掌声、`(sigh)` 叹息）。所有素材片段打包为单个约 12KB 的 `takes_packed.md`——这是 LLM 的主要阅读视图。

```
## C0103  (duration: 43.0s, 8 phrases)
  [002.52-005.36] S0 Ninety percent of what a web agent does is completely wasted.
  [006.08-006.74] S0 We fixed this.
```

**第二层——视觉合成（按需调用）**：`timeline_view` 可为任意时间段生成包含胶片条、波形图及词标签的 PNG。仅在需要决策时调用——例如模糊停顿判断、重拍对比或剪辑点合理性检查。

> Naive approach: 30,000 frames × 1,500 tokens = **45M tokens of noise**.
> Video Use: **12KB text + a handful of PNGs**.

其思路与 `browser-use` 为 LLM 提供结构化 DOM（文档对象模型）而非截图类似——只不过这里应用于视频。

## Pipeline（处理流程）

```
Transcribe ──> Pack ──> LLM Reasons ──> EDL ──> Render ──> Self-Eval
                                                              │
                                                              └─ issue? fix + re-render (max 3)
```

自检循环会在每次剪辑边界对_渲染输出_运行 `timeline_view`——用于检测画面跳帧、音频爆音及隐藏字幕。只有全部通过后，你才会看到预览结果。

## Design principles（设计原则）

1. **文本为主，按需加载视觉信息**。不导出帧序列。转录文本是主要交互层。
2. **音频优先，视觉跟随**。剪辑点基于语音边界和静音间隙生成。
3. **询问 → 确认 → 执行 → 自检 → 持久化**。未经策略批准绝不擅自修改剪辑。
4. **不对内容类型做任何预设假设**。先观察，再提问，最后编辑。
5. **12 条硬性规则，其余保留创作自由**。制作规范性不可妥协，审美则交由你决定。

完整的制作规范与剪辑技巧请参阅 [`SKILL.md`](./SKILL.md)。
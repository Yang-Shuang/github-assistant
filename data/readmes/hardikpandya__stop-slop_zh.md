# Stop Slop（去除 AI 写作痕迹）

一个用于去除文本中 AI 写作痕迹的 Skill。

<img width="3840" height="2160" alt="G-Yg4RVbIAAhVxW" src="https://github.com/user-attachments/assets/902afc15-1f40-4a9d-af24-8cd67afb8ebf" />

## 简介

AI 写作往往带有固定的模式：可预测的短语、结构和节奏。该 Skill（技能规则）旨在教会 Claude（或任何大语言模型 LLM）识别并清除这些痕迹。

## Skill 结构

```
stop-slop/
├── SKILL.md              # Core instructions
├── references/
│   ├── phrases.md        # Phrases to remove
│   ├── structures.md     # Structural patterns to avoid
│   └── examples.md       # Before/after transformations
├── README.md
└── LICENSE
```

## 快速开始

- **Claude Code：** 将此文件夹添加为 Skill。
- **Claude Projects（项目知识库）：** 将 `SKILL.md` 和参考文件上传至项目知识中。
- **自定义指令：** 复制 `SKILL.md` 中的核心规则。
- **API 调用：** 在系统提示词（system prompt）中包含 `SKILL.md`。参考文件可按需加载。

## 拦截内容

- **禁用短语（Banned phrases）**：铺垫性开场白、强调性套话、商业黑话、所有副词、模糊的陈述句、元评论。详见 `references/phrases.md`。
- **结构套路（Structural clichés）**：二元对立对比、负面列举、戏剧化碎片断句、修辞铺垫、虚假主体感、疏离叙述者视角、被动语态。详见 `references/structures.md`。
- **句子级规则**：禁止使用 Wh- 疑问词开头，禁止使用破折号（em dash），禁止断奏式碎片化，避免过度极端的表述，必须使用主动语态。

## 评分标准

从以下维度进行 1-10 分打分：

| 维度 | 评估问题 |
|---|---|
| 直接性（Directness） | 是直陈观点，还是像公告一样生硬？ |
| 节奏感（Rhythm） | 句式多变，还是如节拍器般单调？ |
| 信任度（Trust） | 是否尊重读者的理解力？ |
| 真实感（Authenticity） | 读起来像真人写的吗？ |
| 信息密度（Density） | 是否有可删减的冗余内容？ |

总分低于 35/50：需进行修订。

## 作者

[Hardik Pandya](https://hvpandya.com)

## 许可协议 (License)

MIT。可自由使用，欢迎广泛分享。
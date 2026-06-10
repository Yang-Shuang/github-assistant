# 45 个 Claude Code 技巧：从基础到进阶

以下是我关于如何充分利用 Claude Code 的技巧，包括自定义状态栏脚本、将系统提示词（system prompt）减半、使用 Gemini CLI 作为 Claude Code 的“小弟”，以及在容器中让 Claude Code 自我运行。此外还包含了 [dx 插件](#tip-44-install-the-dx-plugin)。

📺 [快速演示视频](https://www.youtube.com/watch?v=hiISl558JGE) - 观看多 Claude 工作流和语音输入下的部分技巧实际效果：

[![演示视频缩略图](assets/demo-thumbnail.png)](https://www.youtube.com/watch?v=hiISl558JGE)

<!-- TOC -->
## 目录

- [Tip 0: 自定义你的状态栏](#tip-0-customize-your-status-line)
- [Tip 1: 掌握几个关键的斜杠命令](#tip-1-learn-a-few-essential-slash-commands)
- [Tip 2: 用语音与 Claude Code 交流](#tip-2-talk-to-claude-code-with-your-voice)
- [Tip 3: 将大问题分解为小问题](#tip-3-break-down-large-problems-into-smaller-ones)
- [Tip 4: 像专家一样使用 Git 和 GitHub CLI](#tip-4-using-git-and-github-cli-like-a-pro)
- [Tip 5: AI 上下文就像牛奶；新鲜浓缩才最好！](#tip-5-ai-context-is-like-milk-its-best-served-fresh-and-condensed)
- [Tip 6: 将输出内容从终端中提取出来](#tip-6-getting-output-out-of-your-terminal)
- [Tip 7: 设置终端别名以便快速访问](#tip-7-set-up-terminal-aliases-for-quick-access)
- [Tip 8: 主动压缩你的上下文](#tip-8-proactively-compact-your-context)
- [Tip 9: 完成自主任务的编写测试循环](#tip-9-complete-the-write-test-cycle-for-autonomous-tasks)
- [Tip 10: Cmd+A 和 Ctrl+A 是你的好朋友](#tip-10-cmda-and-ctrla-are-your-friends)
- [Tip 11: 使用 Gemini CLI 作为被屏蔽网站的备用方案](#tip-11-use-gemini-cli-as-a-fallback-for-blocked-sites)
- [Tip 12: 投资你自己的工作流](#tip-12-invest-in-your-own-workflow)
- [Tip 13: 搜索你的对话历史](#tip-13-search-through-your-conversation-history)
- [Tip 14: 使用终端标签页进行多任务处理](#tip-14-multitasking-with-terminal-tabs)
- [Tip 15: 精简系统提示词](#tip-15-slim-down-the-system-prompt)
- [Tip 16: Git worktrees 用于并行分支工作](#tip-16-git-worktrees-for-parallel-branch-work)
- [Tip 17: 手动指数退避处理长时间运行的任务](#tip-17-manual-exponential-backoff-for-long-running-jobs)
- [Tip 18: Claude Code 作为写作助手](#tip-18-claude-code-as-a-writing-assistant)
- [Tip 19: Markdown 是神技 (Markdown is the s**t)](#tip-19-markdown-is-the-st)
- [Tip 20: 使用 Notion 在粘贴时保留链接](#tip-20-use-notion-to-preserve-links-when-pasting)
- [Tip 21: 容器用于长时间运行的风险任务](#tip-21-containers-for-long-running-risky-tasks)
- [Tip 22: 使用 Claude Code 最好的方法就是使用它](#tip-22-the-best-way-to-get-better-at-using-claude-code-is-by-using-it)
- [Tip 23: 克隆/分支和半克隆对话](#tip-23-clonefork-and-half-clone-conversations)
- [Tip 24: 使用 realpath 获取绝对路径](#tip-24-use-realpath-to-get-absolute-paths)
- [Tip 25: 理解 CLAUDE.md、Skills（技能）、斜杠命令与插件的区别](#tip-25-understanding-claudemd-vs-skills-vs-slash-commands-vs-plugins)
- [Tip 26: 交互式 PR 审查](#tip-26-interactive-pr-reviews)
- [Tip 27: Claude Code 作为研究工具](#tip-27-claude-code-as-a-research-tool)
- [Tip 28: 掌握验证其输出的不同方法](#tip-28-mastering-different-ways-of-verifying-its-output)
- [Tip 29: Claude Code 作为 DevOps 工程师](#tip-29-claude-code-as-a-devops-engineer)
- [Tip 30: 保持 CLAUDE.md 简洁并定期审查](#tip-30-keep-claudemd-simple-and-review-it-periodically)
- [Tip 31: Claude Code 作为通用接口](#tip-31-claude-code-as-the-universal-interface)
- [Tip 32: 关键在于选择合适的抽象层级](#tip-32-its-all-about-choosing-the-right-level-of-abstraction)
- [Tip 33: 审计你批准的命令](#tip-33-audit-your-approved-commands)
- [Tip 34: 编写大量测试（并使用 TDD）](#tip-34-write-lots-of-tests-and-use-tdd)
- [Tip 35: 在未知领域要更大胆；迭代式解决问题](#tip-35-be-braver-in-the-unknown-iterative-problem-solving)
- [Tip 36: 在后台运行 bash 命令和子代理](#tip-36-running-bash-commands-and-subagents-in-the-background)
- [Tip 37: 个性化软件时代已到来](#tip-37-the-era-of-personalized-software-is-here)
- [Tip 38: 导航和编辑你的输入框](#tip-38-navigating-and-editing-your-input-box)
- [Tip 39: 花些时间规划，但也快速原型开发](#tip-39-spend-some-time-planning-but-also-prototype-quickly)
- [Tip 40: 简化过于复杂的代码](#tip-40-simplify-overcomplicated-code)
- [Tip 41: 自动化的自动化](#tip-41-automation-of-automation)
- [Tip 42: 分享你的知识并在力所能及的范围内贡献](#tip-42-share-your-knowledge-and-contribute-where-you-can)
- [Tip 43: 保持学习！](#tip-43-keep-learning)
- [Tip 44: 安装 dx 插件](#tip-44-install-the-dx-plugin)
- [Tip 45: 快速设置脚本](#tip-45-quick-setup-script)

<!-- /TOC -->

## Tip 0: 自定义你的状态栏

你可以自定义 Claude Code 底部的状态栏以显示有用信息。我将其设置为显示模型、当前目录、Git 分支（如果有）、未提交文件数量、与 origin 的同步状态以及令牌使用情况的可视化进度条。它还显示了第二行我的上一条消息，这样我可以知道对话是关于什么的：

```
Opus 4.5 | 📁claude-code-tips | 🔀main (scripts/context-bar.sh uncommitted, synced 12m ago) | ██░░░░░░░░ 18% of 200k tokens
💬 This is good. I don't think we need to change the documentation as long as we don't say that the default color is orange el...
```

这对于关注上下文使用情况以及记住你正在处理的事情特别有帮助。该脚本还支持 10 种颜色主题（橙色、蓝色、青色、绿色、薰衣草色、玫瑰色、金色、石板灰、青色或灰色）。

![颜色预览选项](scripts/color-preview.png)

要设置此功能，你可以使用 [这个示例脚本](scripts/context-bar.sh)，并查看 [安装说明](scripts/README.md)。

## Tip 1: 掌握几个关键的斜杠命令

内置了许多斜杠命令（输入 `/` 查看所有）。以下是其中几个值得了解的：

### /usage

检查你的速率限制：

```
 Current session
 █████████▌                                         19% used
 Resets 12:59am (America/Vancouver)

 Current week (all models)
 █████████████████████▌                             43% used
 Resets Feb 3 at 1:59pm (America/Vancouver)

 Current week (Sonnet only)
 ███████████████████▌                               39% used
 Resets 8:59am (America/Vancouver)
```

如果你想密切关注使用情况，请将其保持在打开的标签页中，并使用 Tab 然后 Shift+Tab 或 ← 然后 → 进行刷新。

### /chrome

切换 Claude 的原生浏览器集成：

```
> /chrome
Chrome integration enabled
```

### /mcp

管理 MCP（模型上下文协议）服务器：

```
 Manage MCP servers
 1 server

 ❯ 1. playwright  ✔ connected · Enter to view details

 MCP Config locations (by scope):
  • User config (available in all your projects):
    • /Users/yk/.claude.json
```

### /stats

查看带有 GitHub 风格活动图的你的使用统计信息：

```
      Feb Mar Apr May Jun Jul Aug Sep Oct Nov Dec Jan
      ········································▒█░▓░█░▓▒▒
  Mon ········································▒▒██▓░█▓█░█
      ········································░▒█▒▓░█▒█▒█
  Wed ········································░▓▒█▓▓░▒▓▒██
      ········································░▓░█▓▓▓▓█░▒█
  Fri ········································▒░░▓▒▒█▓▓▓█
      ········································▒▒░▓░░▓▒▒░░

      Less ░ ▒ ▓ █ More

  Favorite model: Opus 4.5        Total tokens: 17.6m

  Sessions: 4.1k                  Longest session: 20h 40m 45s
  Active days: 79/80              Longest streak: 75 days
  Most active day: Jan 26         Current streak: 74 days

  You've used ~24x more tokens than War and Peace
```

### /clear

清除对话并重新开始。

## Tip 2: 用语音与 Claude Code 交流

我发现你用语音沟通比打字要快得多。在本地机器上使用语音转录系统对此非常有帮助。

在我的 Mac 上，我尝试过几种不同的选项：
- [superwhisper](https://superwhisper.com/)
- [MacWhisper](https://goodsnooze.gumroad.com/l/macwhisper)
- [Super Voice Assistant](https://github.com/ykdojo/super-voice-assistant)（开源，支持 Parakeet v2/v3）

你可以使用托管服务来获得更高的准确率，但我发现本地模型对于此目的来说已经足够强大。即使转录中出现错误或有拼写错误，Claude 也足够聪明，能够理解你想说什么。有时你需要把某些事情说得更清楚一些，但总的来说，本地模型的效果已经很好了。

例如，在这个截图中你可以看到 Claude 能够正确解释误识别的单词，如 "ExcelElanishMark" 和 "advast"，将其理解为 "exclamation mark"（感叹号）和 "Advanced"：

![语音转录错误被正确解读](assets/voice-transcription-mistakes.png)

我认为最好的思考方式是就像你在和朋友交流一样。当然，你可以通过文本沟通。这对某些人来说可能更容易，或者通过电子邮件？这完全没问题。大多数人似乎都是这样使用 Claude Code 的。但如果你想更快地交流，为什么不打个简短的电话呢？你可以只发送语音消息。你不需要真的和 Claude Code 进行电话通话。只需发送一堆语音消息即可。对我来说，作为一个多年来练习过说话艺术的人，这样做更快。但我认为对大多数人来说，这也会更快。

常见的反对意见是“如果你和其他人在一个房间里怎么办？”我只是用耳机低语——我个人喜欢 Apple EarPods（不是 AirPods）。它们价格实惠，质量足够好，你只需对着它们轻声低语即可。我曾在其他人面前这样做过，效果很好。在办公室里，人们本来就会说话——与其和同事交谈，不如低声与你的语音转录系统交流。我认为这没有任何问题。这种方法效果非常好，甚至在飞机上也适用。声音大到别人听不见，但如果你离麦克风足够近，本地模型仍然能理解你在说什么。（事实上，我正在航班上使用该方法撰写这段文字。）

**更新：** Claude Code 现在有了 [内置的语音模式](https://x.com/bcherny/status/2032238378389840018)。我测试过它，效果很好，但我个人仍然使用本地模型，因为我觉得它更快。

## Tip 3: 将大问题分解为小问题

这是最需要掌握的概念之一。这与传统的软件工程完全相同——最好的软件工程师已经知道如何做到这一点，这也适用于 Claude Code。

如果你发现 Claude Code 无法一次性解决困难的问题或编码任务，请让它将其分解为多个较小的问题。看看它是否能解决该问题的各个部分。如果仍然太难，看看它是否能解决更小的子问题。继续下去直到一切都可解。

本质上，与其从 A 直接到 B：

![直接方法](assets/breakdown-direct.png)

你可以从 A 到 A1 再到 A2 再到 A3，然后到 B：

![逐步方法](assets/breakdown-steps.png)

一个很好的例子是我在构建自己的语音转录系统时。我需要构建一个允许用户选择和下载模型、使用键盘快捷键、开始转录、将转录文本放在用户的光标处，并将所有这些包装在一个漂亮的 UI 中的系统。这很复杂。所以我将其分解为更小的任务。首先，我创建了一个只下载模型的执行文件，没有其他功能。然后我又创建了一个只录音的。接着是另一个只做预录音频转录的。我以这种方式逐个完成它们，最后将它们组合在一起。

与此高度相关的是：你的解决问题能力和软件工程技能在代理式编码和 Claude Code 的世界中仍然非常相关。它能够独立解决很多问题，但当你将通用的解决问题和软件工程技能应用于它时，它会变得强大得多。

## Tip 4: 像专家一样使用 Git 和 GitHub CLI

只需让 Claude 处理你的 Git 和 GitHub CLI 任务即可。这包括提交（这样你就不必手动编写提交信息）、分支、拉取和推送。

我个人允许自动拉取但不允许自动推送，因为推送风险更大——如果拉取出错，不会污染 origin。

对于 GitHub CLI (`gh`)，你可以做很多事情。在使用 Claude Code 后我开始更多地做的事情之一是创建草稿 PR（Pull Request）。这让 Claude Code 以低风险处理 PR 创建过程——你可以在将其标记为准备审查之前查看所有内容。

事实证明，`gh` 相当强大。你甚至可以通过它发送任意的 GraphQL 查询。例如，你甚至可以找到 GitHub PR 描述被编辑的确切时间：

```
⏺ Bash(gh api graphql -f query='
      query {
        repository(owner: "...", name: "...") {
          pullRequest(number: ...) {
            userContentEdits(first: 100) {
              nodes { editedAt editor { login } }
            }
          }
        }
      }')

⏺ Here's the full edit history for your PR description:

  | #  | Edited At (UTC)     | Editor |
  |----|---------------------|--------|
  | 1  | 2025-12-01 00:08:34 | ykdojo |
  | 2  | 2025-12-01 15:57:21 | ykdojo |
  | 3  | 2025-12-01 16:24:33 | ykdojo |
  | 4  | 2025-12-01 16:27:00 | ykdojo |
  | 5  | 2025-12-04 00:40:02 | ykdojo |
  ...
```

### 禁用提交/PR 署名

默认情况下，Claude Code 会在提交中添加 `Co-Authored-By` 尾部，并在 PR 中添加署名页脚。你可以通过将此添加到 `~/.claude/settings.json` 来禁用两者：

```json
{
  "attribution": {
    "commit": "",
    "pr": ""
  }
}
```

将两者设置为空字符串将完全移除署名。这取代了较旧的 `includeCoAuthoredBy` 设置，该设置现已弃用。

## Tip 5: AI 上下文就像牛奶；新鲜浓缩才最好！

当你开始与 Claude Code 的新对话时，它的表现是最好的，因为它不需要处理来自对话早期部分的先前上下文的额外复杂性。但是随着你与它交谈的时间越来越长，上下文会变长，性能往往会下降。

因此，对于每个新主题或当性能开始下降时，最好开始新的对话。

## Tip 6: 将输出内容从终端中提取出来

有时你想复制和粘贴 Claude Code 的输出，但直接从终端复制并不总是干净的。这里有几种更容易获取内容的方法：

- **`/copy` 命令**：最简单的选项——只需输入 `/copy` 即可将 Claude 的最后一次响应作为 markdown 复制到你的剪贴板
- **直接复制到剪贴板**：在 Mac 或 Linux 上，让 Claude 使用 `pbcopy` 直接将输出发送到你的剪贴板
- **写入文件**：让 Claude 将内容放入文件中，然后让它在你喜欢的编辑器（如 VS Code）中打开它以便复制。你也可以指定行号，这样你可以让 Claude 打开它刚刚编辑的特定行。对于 markdown 文件，一旦它在 VS Code 中打开，你可以使用 Cmd+Shift+P（或在 Linux/Windows 上使用 Ctrl+Shift+P）并选择“Markdown: Open Preview”以查看渲染版本
- **打开 URL**：如果你想检查某个 URL，让 Claude 在你的浏览器中打开它。在 Mac 上，你可以让它使用 `open` 命令，但一般来说，要求在你喜欢的浏览器中打开在任何平台上都应该有效
- **GitHub Desktop**：你可以让 Claude 在当前仓库的 GitHub Desktop 中打开。当它在非根目录工作时特别有用——例如，如果你让它在一个不同的目录中创建一个 git worktree，而你还没有从那里打开 Claude Code

你也可以将其中一些结合起来使用。例如，如果你想编辑 GitHub PR 描述，与其让 Claude 直接编辑它（这可能会搞砸），你可以让它先将内容复制到本地文件中。让它编辑那个文件，你自己检查结果，一旦看起来不错，再让它复制并粘贴回 GitHub PR。这非常有效。或者如果你自己想这样做，你只需要求它在 VS Code 中打开它或通过 pbcopy 给你，以便你手动复制和粘贴。

当然，你可以自己运行这些命令，但如果你发现自己重复这样做，让 Claude 为你运行它们会有帮助。

## Tip 7: 设置终端别名以便快速访问

由于我因为 Claude Code 而更多地使用终端，我发现设置简短的别名以便快速启动东西很有帮助。以下是我使用的：

- `c` 用于 Claude Code（这是我使用最多的）
- `ch` 用于带有 Chrome 集成的 Claude Code
- `gb` 用于 GitHub Desktop
- `co` 用于 VS Code
- `q` 用于进入我拥有大多数项目的目录。从那里我可以手动 cd 到单个文件夹以处理该项目，或者我可以直接使用 `c` 启动 Claude Code，让它基本上可以访问它需要访问的任何项目。

要设置这些，将类似这样的行添加到你的 shell 配置文件中（`~/.zshrc` 或 `~/.bashrc`）：

```bash
alias c='claude'
alias ch='claude --chrome'
alias gb='github'
alias co='code'
alias q='cd ~/Desktop/projects'
```

设置好这些别名后，你可以将它们与标志结合使用：`c -c` 继续你上一次的对话，`c -r` 显示最近对话列表以恢复。它们也可以与 `ch` 一起使用（`ch -c`, `ch -r`）用于 Chrome 会话。

## Tip 8: 主动压缩你的上下文

Claude Code 中有一个 `/compact` 命令可以总结你的对话以释放上下文空间。当完整可用的上下文被填满时，也会自动发生压缩。Opus 4.5 的总可用上下文窗口目前是 200k，其中 45k 保留用于自动压缩。大约 10% 的总 200k 会自动填充系统提示词、工具、记忆和动态上下文。但我发现主动做这件事并手动调整更好。我通过 `/config` 关闭了自动压缩，这样我的主对话就有更多的可用上下文，并且对何时以及如何压缩有更多的控制权。

我是这样做的：在重新开始之前让 Claude 编写一份交接文档。类似于：

> 将计划的其余部分放在 system-prompt-extraction 文件夹中作为 HANDOFF.md。解释你已经尝试了什么、什么有效、什么无效，以便下一个具有新鲜上下文的代理只需加载该文件而无需其他内容即可开始此任务并完成它。

Claude 将创建一个总结当前工作状态的文件：

```
⏺ Write(experiments/system-prompt-extraction/HANDOFF.md)
  ⎿  Wrote 129 lines to experiments/system-prompt-extraction/HANDOFF.md
     # System Prompt Slimming - Handoff Document
     ## Goal
     Reduce Claude Code's system prompt by ~45% (currently at 11%, need ~34% more).
     ## Current Progress
     ### What's Been Done
     - **Backup/restore system**: `backup-cli.sh` and `restore-cli.sh` with SHA256 verification
     - **Patch system**: `patch-cli.js` that restores from backup then applies patches
     ...
```

Claude 编写后，快速审查一下。如果缺少什么，要求编辑：

> 你是否添加了关于迭代测试而不是试图一次性完成所有事情的说明？

然后开始新的对话。对于新代理，你只需给出文件路径而无需其他内容，如下所示，它应该可以正常工作：

```
> experiments/system-prompt-extraction/HANDOFF.md
```

在随后的对话中，你可以让代理更新文档以供下一个代理使用。

我还创建了一个 `/handoff` 斜杠命令来自动化此过程——它会检查是否存在现有的 HANDOFF.md，如果存在则读取它，然后使用目标、进展、什么有效、什么无效以及下一步来创建或更新它。你可以在 [skills 文件夹](skills/handoff/SKILL.md) 中找到它，或通过 [dx 插件](#tip-44-install-the-dx-plugin) 安装。

**替代方案：使用计划模式**

另一个选项是使用 plan mode（计划模式）。通过 `/plan` 或 Shift+Tab 进入。让 Claude 收集所有相关上下文并为下一个代理创建一个全面的计划：

> 我刚刚启用了计划模式。把下一个代理需要的所有上下文带过来。下一个代理将没有任何其他上下文，所以你需要非常全面。

Claude 将探索代码库、收集上下文并编写详细的计划。完成后，你会看到类似这样的选项：

```
Would you like to proceed?

❯ 1. Yes, clear context and auto-accept edits (shift+tab)
  2. Yes, auto-accept edits
  3. Yes, manually approve edits
  4. Type here to tell Claude what to change
```

选项 1 清除之前的上下文并开始使用计划的新会话。新的 Claude 实例仅看到计划，因此它可以专注于而不受旧对话的负担影响。它还获得了指向旧转录文件的链接，以防它需要查找特定细节。

## Tip 9: 完成自主任务的编写测试循环

如果你想让 Claude Code 自主运行某些内容（如 `git bisect`），你需要给它一种验证结果的方法。关键在于完成编写-测试循环：编写代码、运行它、检查结果，然后重复。

例如，假设你正在处理 Claude Code 本身，并注意到 `/compact` 停止工作并开始抛出 400 错误。查找导致此问题的确切提交的一个经典工具是 `git bisect`。好处是你可以让 Claude Code 对自己进行 bisect，但它需要一种测试每个提交的方法。

对于涉及交互式终端的任务（如 Claude Code），你可以使用 tmux。模式如下：

1. 启动一个 tmux 会话
2. 向其发送命令
3. 捕获输出
4. 验证它是否符合你的预期

这是一个简单的示例，用于测试 `/context` 是否有效：

```bash
tmux kill-session -t test-session 2>/dev/null
tmux new-session -d -s test-session
tmux send-keys -t test-session 'claude' Enter
sleep 2
tmux send-keys -t test-session '/context' Enter
sleep 1
tmux capture-pane -t test-session -p
```

一旦你有了这样的测试，Claude Code 就可以运行 `git bisect` 并自动测试每个提交直到找到破坏事物的那个。

这也是为什么你的软件工程技能仍然重要的一个例子。如果你是软件工程师，你可能知道像 `git bisect` 这样的工具。这种知识在与 AI 合作时仍然非常有价值——你只是以新的方式应用它。

另一个例子是简单地编写测试。在你让 Claude Code 编写一些代码后，如果你想测试它，你可以让它为自己编写测试。并让它自行运行并在可以修复时修复问题。当然，它并不总是朝着正确的方向发展，有时你需要监督它，但它能够独立完成令人惊讶数量的编码任务。

### 创造性测试策略

有时你需要在如何完成编写-测试循环方面发挥创造力。例如，如果你正在构建一个 Web 应用，你可以使用 Playwright MCP、Chrome DevTools MCP 或 Claude 的原生浏览器集成（通过 `/chrome`）。我还没有尝试过 Chrome DevTools，但我已经尝试过 Playwright 和 Claude 的原生集成。总的来说，Playwright 通常效果更好。它确实使用了大量上下文，但 200k 的上下文窗口对于单个任务或几个较小的任务来说通常足够了。

这两者之间的主要区别似乎是 Playwright 专注于无障碍树（关于页面元素的结构化数据）而不是截图。它具有截图的能力，但它通常不使用它们来采取行动。另一方面，Claude 的原生浏览器集成更侧重于通过特定坐标点击元素进行截图。它有时可以点击随机东西，整个过程可能会很慢。

这可能会随着时间的推移而改善，但默认情况下，对于大多数非视觉密集型任务，我会选择 Playwright。只有当我需要登录状态而不必提供凭据（因为它在你的浏览器配置文件中运行）或它确实需要使用坐标在视觉上点击某些内容时，我才会使用 Claude 的原生浏览器集成。

这就是为什么我默认禁用 Claude 的原生浏览器集成并通过我之前定义的 `ch` 快捷方式使用它。这样 Playwright 处理大多数浏览器任务，只有在我特别需要时才启用 Claude 的原生集成。

此外，你可以让它使用无障碍树引用而不是坐标。以下是我在我的 CLAUDE.md 中为此放置的内容：

```markdown
# Claude for Chrome

- Use `read_page` to get element refs from the accessibility tree
- Use `find` to locate elements by description
- Click/interact using `ref`, not coordinates
- NEVER take screenshots unless explicitly requested by the user
```

在我的个人经验中，我也遇到过一种情况：我正在处理一个 Python 库 ([Daft](https://github.com/Eventual-Inc/Daft)) 并需要在 Google Colab 上测试我本地构建的版本。麻烦在于在 Google Colab 上使用 Rust 后端构建 Python 库很难——它似乎效果不太好。所以我需要实际在本地构建成 wheel，然后手动上传以便在 Google Colab 上运行。我也尝试了猴子补丁（monkey patching），这在等待整个 wheel 在本地构建之前短期有效。我想出了这些测试策略并通过与 Claude Code 来回沟通执行它们。

我遇到的另一个情况是我需要在 Windows 上测试某些内容，但我没有运行 Windows 机器。我在同一仓库上的 CI 测试失败了，因为我们在 Windows 上有 Rust 问题，而我无法在本地进行测试。所以我需要创建一个包含所有更改的草稿 PR，以及另一个包含相同更改并启用非主分支上 Windows CI 运行的草稿 PR。我指示 Claude Code 完成所有这些操作，然后我直接在该新分支中测试了 CI。

## Tip 10: Cmd+A 和 Ctrl+A 是你的好朋友

我已经说了几年了：Cmd+A 和 Ctrl+A 是 AI 世界的好朋友。这也适用于 Claude Code。

有时你想给 Claude Code 一个 URL，但它无法直接访问它。也许它是一个私人页面（不敏感数据，只是不是公开可访问的），或者像 Reddit 帖子这样 Claude Code 难以获取的内容。在这种情况下，你可以只需选择你看到的所有内容（在 Mac 上是 Cmd+A，在其他平台上是 Ctrl+A），复制并直接粘贴到 Claude Code 中。这是一种相当强大的方法。

这也适用于终端输出。当我有来自 Claude Code 本身或任何其他 CLI 应用程序的输出时，我可以使用同样的技巧：全选、复制，然后粘贴回 CC。非常有帮助。

某些页面默认不适合全选——但有一些技巧可以先把它们置于更好的状态。例如，对于 Gmail 线程，点击“打印全部”以获取打印预览（但取消实际打印）。该页面会展开显示线程中的所有电子邮件，因此你可以 Cmd+A 整个对话。对于询问关于 YouTube 视频的问题或总结它，你可以在 YouTube 视频中点击“显示转录”，然后执行 Cmd+A 或 Ctrl+A。

这不仅适用于 Claude Code，也适用于任何 AI。

## Tip 11: 使用 Gemini CLI 作为被屏蔽网站的备用方案

Claude Code 的 WebFetch 工具无法访问某些网站，如 Reddit。但你可以通过创建一个告诉 Claude 使用 Gemini CLI 作为备用的技能来绕过此限制。Gemini 具有网络访问权限，可以获取 Claude 无法直接访问的网站内容。

这使用了与 Tip 9 中相同的 tmux 模式——启动会话、发送命令、捕获输出。技能文件位于 `~/.claude/skills/reddit-fetch/SKILL.md`。完整内容请参阅 [skills/reddit-fetch/SKILL.md](skills/reddit-fetch/SKILL.md)。

Skills（技能）更节省令牌，因为 Claude Code 仅在需要时加载它们。如果你想要更简单的东西，你可以将精简版本放在 `~/.claude/CLAUDE.md` 中，但这会将其加载到每次对话中，无论你是否需要它。

我通过让 Claude Code 检查 Reddit 上对 Claude Code 技能的看法来测试此功能——有点元。它与 Gemini 来回沟通了一段时间，所以不是很快，但报告质量出奇地好。显然，你需要安装 Gemini CLI 才能使其工作。你也可以通过 [dx 插件](#tip-44-install-the-dx-plugin) 安装此技能。

## Tip 12: 投资你自己的工作流

就个人而言，我完全用 Swift 从头创建了属于自己的语音转录应用。我用 Claude Code 从头创建了自己的自定义状态栏（使用 bash）。我还创建了自己的系统来简化 Claude Code 的 minified JavaScript 文件中的系统提示词。

但你不必像那样过度投入。只需照顾好你自己的 CLAUDE.md，确保它尽可能简洁同时又能帮助你实现目标——诸如此类的事情是有帮助的。当然，学习这些技巧、学习这些工具以及一些最重要的功能也是必要的。

这些都是对你用来构建任何你想构建的东西的投资。我认为花至少一点时间在这方面很重要。

## Tip 13: 搜索你的对话历史

你可以询问 Claude Code 关于你过去的对话，它会帮助你查找和搜索它们。你的对话历史存储在本地 `~/.claude/projects/` 中，文件夹名称基于项目路径（斜杠变为连字符）。

例如，位于 `/Users/yk/Desktop/projects/claude-code-tips` 的项目的对话将存储在：

```
~/.claude/projects/-Users-yk-Desktop-projects-claude-code-tips/
```

每个对话都是一个 `.jsonl` 文件。你可以使用基本的 bash 命令搜索它们：

```bash
# Find all conversations mentioning "Reddit"
grep -l -i "reddit" ~/.claude/projects/-Users-yk-Desktop-projects-*/*.jsonl

# Find today's conversations about a topic
find ~/.claude/projects/-Users-yk-Desktop-projects-*/*.jsonl -mtime 0 -exec grep -l -i "keyword" {} \;

# Extract just the user messages from a conversation (requires jq)
cat ~/.claude/projects/.../conversation-id.jsonl | jq -r 'select(.type=="user") | .message.content'
```

或者直接询问 Claude Code：“我们今天讨论了关于 X 的什么内容？”它会为你搜索历史记录。

## Tip 14: 使用终端标签页进行多任务处理

当运行多个 Claude Code 实例时，保持组织有序比任何特定的技术设置（如 Git worktrees）更重要。我建议专注于同时最多三个或四个任务。

我个人的方法是我称之为“级联”——每当我开始一个新任务时，我只是在右侧打开一个新标签页。然后我从左到右扫描，从左到右，从最旧的任务到最新的任务。总体方向保持一致，除非我需要检查某些任务、接收通知等。

我的设置通常如下所示：

![显示多任务工作流的终端标签页](assets/multitasking-terminal-tabs.png)

在此示例中：
1. **最左侧标签页** - 运行我语音转录系统的持久化标签页（始终停留在这里）
2. **第二个标签页** - 设置 Docker 容器
3. **第三个标签页** - 检查本地机器上的磁盘使用情况
4. **第四个标签页** - 处理工程项目
5. **第五个标签页（当前）** - 撰写此技巧

## Tip 15: 精简系统提示词

Claude Code 的系统提示词和工具定义在你开始工作之前就会占用大约 19k 令牌（约 200k 上下文的 ~10%）。我创建了一个补丁系统将其减少到大约 9k 令牌——节省了大约 10,000 令牌（开销的 ~50%）。

| Component | Before | After | Savings |
|-----------|--------|-------|---------|
| System prompt | 3.0k | 1.8k | 1,200 tokens |
| System tools | 15.6k | 7.4k | 8,200 tokens |
| **Total** | **~19k** | **~9k** | **~10k tokens (~50%)** |

这是打补丁前后 `/context` 的样子：

**Unpatched (~20k, 10%)**

![未修补上下文](assets/context-unpatched.png)

**Patched (~10k, 5%)**

![已修补上下文](assets/context-patched.png)

补丁通过修剪 minified CLI bundle 中的冗长示例和冗余文本来工作，同时保留所有基本说明。

我已经广泛测试过它并且效果很好。感觉更原始——更有力量，但可能稍微不那么受监管，这很有道理，因为系统指令较短。当你这样使用时，它更像是一个专业工具。我真的很喜欢从较低的上下文开始，因为在填满之前你有更多的空间，这给了你继续对话稍长时间的选项。这肯定是此策略的最佳部分。

查看 [system-prompt 文件夹](system-prompt/) 以获取补丁脚本以及被修剪内容的详细信息。

**为什么打补丁？** Claude Code 有标志允许你从文件提供简化的系统提示词（`--system-prompt` 或 `--system-prompt-file`），所以这是另一种方法。但对于工具描述，没有官方选项来自定义它们。修补 CLI bundle 是唯一的方法。由于我的补丁系统在一个统一的方法中处理所有事情，我暂时保持这种方式。我将来可能会使用标志重新实现系统提示词部分。

**支持的安装：** npm 和原生二进制文件（macOS 和 Linux）。

**重要：** 如果你想保留你的已修补系统提示词，通过将其添加到 `~/.claude/settings.json` 来禁用自动更新：

```json
{
  "env": {
    "DISABLE_AUTOUPDATER": "1"
  }
}
```

这适用于所有 Claude Code 会话，无论 shell 类型如何（交互式、非交互式、tmux）。当你准备好将补丁重新应用到新版本时，你可以手动更新。

### 按需加载 MCP 工具

如果你使用 MCP 服务器，它们的工具定义默认会加载到每次对话中——即使你不使用它们。这会增加显著的开销，尤其是在配置了多个服务器的情况下。

启用按需加载以便仅在需要时加载 MCP 工具：

```json
{
  "env": {
    "ENABLE_TOOL_SEARCH": "true"
  }
}
```

将其添加到 `~/.claude/settings.json`。Claude 将按需搜索和加载 MCP 工具，而不是从一开始就全部存在。截至版本 2.1.7，当 MCP 工具描述超过上下文窗口的 10% 时会自动发生这种情况。

## Tip 16: Git worktrees 用于并行分支工作

如果你在同一个项目中同时处理多件事并且不想让它们产生冲突，Git worktrees 是一种很好的方法。你只需让 Claude Code 创建一个 git worktree 并开始在那里工作——不必担心具体的语法。

基本思想是你可以在不同的目录中在不同的分支上工作。它本质上是一个分支 + 一个目录。

你可以在我在多任务技巧中讨论的级联方法之上添加这一层 Git worktrees。

### 什么是 git worktrees？

git worktree 就像任何其他 git 分支一样，但有一个专门分配给它的目录。

所以如果你在处理 main 分支和 feature-branch-1，那么没有 git worktrees，你一次只能处理它们中的一个，因为你的项目文件夹一次只能设置为一个分支。

然而，有了 git worktree，你可以在原始项目文件夹中继续处理 main 分支（或任何其他分支），同时在新的文件夹中处理 feature-branch-1。

![显示在不同目录中并行分支工作的 Git worktrees 图](assets/git-worktrees.png)

## Tip 17: 手动指数退避处理长时间运行的任务

当等待像 Docker 构建或 GitHub CI 这样的长时间运行任务时，你可以让 Claude Code 进行手动指数退避。指数退避是软件工程中的常见技术，但你也可以在这里应用它。让 Claude Code 以逐渐增加的睡眠间隔检查状态——一分钟，然后两分钟，然后四分钟，依此类推。这不是以传统意义上的编程方式进行的——AI 正在手动执行此操作——但它效果很好。

这样代理可以持续检查状态并在完成后通知你。

（对于 GitHub CI  specifically，`gh run watch` 存在但会连续输出许多行，这浪费了令牌。使用 `gh run view <run-id> | grep <job-name>` 进行手动指数退避实际上更节省令牌。这也是一种通用技术，即使你没有专门的等待命令也可以使用。）

例如，如果你在后台运行 Docker 构建：

![检查 Docker 构建进度的手动指数退避](assets/manual-exponential-backoff.png)

它会一直持续直到任务完成。

## Tip 18: Claude Code 作为写作助手

Claude Code 是一个出色的写作助手和伙伴。我用于写作的我是首先给它所有关于我正在尝试写的东西的上下文，然后通过语音对它给出详细的说明。这给了我初稿。如果不够好，我会试几次。

然后我基本上逐行检查它。我说好吧，让我们一起看看它。我喜欢这一行的原因是这些。我觉得这一行需要移到那里。这一行需要以这种方式改变。我也可能会询问参考资料。

所以这是一种来回的过程，也许终端在左边，代码编辑器在右边：

![带有 Claude Code 的并排写作工作流](assets/writing-assistant-side-by-side.png)

这通常效果很好。

## Tip 19: Markdown 是神技 (Markdown is the s**t)

通常当人们编写新文档时，他们可能会使用像 Google Docs 或 Maybe Notion 这样的东西。但现在我真心认为最有效的方法是 markdown。

即使在 AI 之前，markdown 已经相当不错了，但特别是对于 Claude Code，因为它在写作方面非常高效（正如我之前提到的），我认为它提高了 markdown 的价值。无论何时你想写博客文章甚至 LinkedIn 帖子，你都可以与 Claude Code 交谈，让它保存为 markdown，然后从那里开始。

关于这一点的一个快速提示：如果你想将 markdown 内容复制并粘贴到不容易接受它的平台上，你可以先将其粘贴到一个新的 Notion 文件中，然后从 Notion 复制到另一个平台。Notion 会将其转换为其他平台可以接受的格式。如果常规粘贴不起作用，尝试使用 Command + Shift + V 以无格式粘贴。

## Tip 20: 使用 Notion 在粘贴时保留链接

事实证明反过来也有效。如果你有来自其他地方（比如 Slack）的带有链接的文本，你可以复制它。如果你直接将其粘贴到 Claude Code 中，它不会显示链接。但如果你先把它放在一个 Notion 文档中，然后从那里复制，你会得到 markdown，当然 Claude Code 可以读取它。

## Tip 21: 容器用于长时间运行的风险任务

常规会话更适合于有方法的工作，你控制给予的权限并更仔细地审查输出。容器化环境非常适合 `--dangerously-skip-permissions` 会话，在那里你不必为每一件小事授予权限。你可以让它自行运行一段时间。

这对于研究或实验很有用，那些花费很长时间且可能具有风险的事情。一个很好的例子是 Tip 11 中的 Reddit 研究工作流，其中 reddit-fetch 技能通过 tmux 与 Gemini CLI 来回沟通。在主系统上无监督地运行这是有风险的，但在容器中，如果出现问题，它会被隔离。

另一个例子是我如何在这个仓库中创建 [system prompt patching scripts](system-prompt/)。当新版本 Claude Code 发布时，我需要更新 minified CLI bundle 的补丁。与其在我的主机上以 `--dangerously-skip-permissions` 运行 Claude Code（在那里它可以访问所有东西），我在容器中运行它。Claude Code 可以探索 minified JavaScript，找到变量映射并创建新的补丁文件，而无需我批准每一件小事。

事实上，它能够几乎独立地完成迁移。它尝试应用补丁，发现某些与新版本不兼容，迭代修复它们，甚至根据它所学到的改进了 [instruction document](system-prompt/UPGRADING.md) 以供将来实例使用。

我还创建了 [SafeClaw](https://github.com/ykdojo/safeclaw) 以轻松运行容器化的 Claude Code 会话。它允许你启动多个隔离的会话，每个会话都有一个 Web 终端，并从仪表板管理它们。它使用了此仓库中的几个自定义项，包括优化的系统提示词、[DX 插件](#tip-44-install-the-dx-plugin) 和 [状态栏](#tip-0-customize-your-status-line)。

### 高级：编排容器中的工作器 Claude Code

你可以通过让你的本地 Claude Code 控制另一个在容器中运行的 Claude Code 实例来进一步扩展这一点。诀窍是使用 tmux 作为控制层：

1. 你的本地 Claude Code 启动一个 tmux 会话
2. 在该 tmux 会话中，它运行或连接到容器
3. 在容器内，Claude Code 以 `--dangerously-skip-permissions` 运行
4. 你的外部 Claude Code 使用 `tmux send-keys` 发送提示并使用 `capture-pane` 读取输出

这给你一个完全自主的“工作器” Claude Code，可以运行实验性或长时间运行的任务而无需你批准每个操作。完成后，你的本地 Claude Code 可以将结果拉回。如果出现问题，它都在容器中沙盒化。

### 高级：多模型编排

不仅限于 Claude Code，你可以在容器中运行不同的 AI CLI——Codex、Gemini CLI 或其他。我尝试过 OpenAI Codex 进行代码审查，效果很好。重点不是你不能直接在主机上运行这些 CLI——你显然可以。价值在于 Claude Code 的 UI/UX 足够流畅，你可以只是与它交谈并让它处理编排：启动不同的模型，在容器和你的主机之间发送数据。与其手动切换终端和复制粘贴，Claude Code 成为协调一切的中央接口。

## Tip 22: 使用 Claude Code 最好的方法就是使用它

最近我看到一位世界级的攀岩者接受另一位攀岩者的采访。她被问到“你如何变得擅长攀岩？”她简单地说，“通过攀岩。”

我对这也感觉如此。当然，你可以做补充的事情，比如看视频、读书、学习技巧。但使用 Claude Code 是学习如何使用它的最佳方法。使用 AI 本身是学习如何使用 AI 的最佳方式。

我喜欢把它想象成“万亿令牌规则”而不是“一万小时规则”。如果你想变得擅长 AI 并真正对它的工作原理有良好的直觉，最好的方法是消耗大量令牌。而现在这是可能的。我发现特别是对于 Opus 4.5，它足够强大但又足够实惠，你可以同时运行多个会话。你不必像以前那样担心令牌使用情况，这让你轻松了很多。

## Tip 23: 克隆/分支和半克隆对话

有时你想从对话的特定时间点尝试不同的方法而不丢失原始线程。[clone-conversation script](scripts/clone-conversation.sh) 允许你用新的 UUID 复制对话以便你可以分支出去。

**内置替代方案（较新版本）：** Claude Code 现在有了原生 fork：
- `/fork` - 在对话内 fork 当前会话
- `--fork-session` - 与 `--resume` 或 `--continue` 一起使用（例如，`claude -c --fork-session`）

由于 `--fork-session` 没有简短形式，你可以将此函数添加到你的 `~/.zshrc` 或 `~/.bashrc` 以将 `--fs` 用作快捷方式：

```bash
claude() {
  local args=()
  for arg in "$@"; do
    if [[ "$arg" == "--fs" ]]; then
      args+=("--fork-session")
    else
      args+=("$arg")
    done
  command claude "${args[@]}"
}
```

这会拦截所有 `claude` 命令，将 `--fs` 扩展为 `--fork-session`，并原样传递其他所有内容。也适用于别名（见 [Tip 7](#tip-7-set-up-terminal-aliases-for-quick-access)）：`c -c --fs`, `ch -c --fs` 等。

下面的克隆脚本早于这些内置选项，但下面的半克隆脚本对于减少上下文仍然是独特的。

第一条消息标记为 `[CLONED <timestamp>]`（例如，`[CLONED Jan 7 14:30]`），这会显示在 `claude -r` 列表中以及对话内部。

要手动设置它，链接两个文件：
```bash
ln -s /path/to/this/repo/scripts/clone-conversation.sh ~/.claude/scripts/clone-conversation.sh
ln -s /path/to/this/repo/skills/clone ~/.claude/skills/clone
```

或通过 [dx 插件](#tip-44-install-the-dx-plugin) 安装——不需要链接。

然后在任何对话中只需输入 `/clone`（如果使用插件则为 `/dx:clone`），Claude 将处理查找会话 ID 并运行脚本。

我已经广泛测试过它并且克隆效果非常好。

### 半克隆以减少上下文

当对话太长时，[half-clone-conversation script](scripts/half-clone-conversation.sh) 只保留后半部分。这减少了令牌使用同时保留了你的近期工作。第一条消息标记为 `[HALF-CLONE <timestamp>]`（例如，`[HALF-CLONE Jan 7 14:30]`）。

要手动设置它，链接两个文件：
```bash
ln -s /path/to/this/repo/scripts/half-clone-conversation.sh ~/.claude/scripts/half-clone-conversation.sh
ln -s /path/to/this/repo/skills/half-clone ~/.claude/skills/half-clone
```

或通过 [dx 插件](#tip-44-install-the-dx-plugin) 安装——不需要链接。

### 使用钩子自动建议半克隆

可选地，你可以使用 [hook](https://docs.anthropic.com/en/docs/claude-code/hooks) 在你的上下文太长时自动触发 `/half-clone`。[check-context script](scripts/check-context.sh) 在每次 Claude 响应后运行并检查上下文使用情况。如果超过 85%，它会告诉 Claude 运行 `/half-clone`，这会创建一个只有后半部分的新对话以便新代理可以在那里继续。

要设置它，首先复制脚本：
```bash
cp /path/to/this/repo/scripts/check-context.sh ~/.claude/scripts/check-context.sh
chmod +x ~/.claude/scripts/check-context.sh
```

然后将钩子添加到你的 `~/.claude/settings.json`：
```json
{
  "hooks": {
    "Stop": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "~/.claude/scripts/check-context.sh"
          }
        ]
      }
    ]
  }
}
```

这需要禁用自动压缩（`/config` > Auto-compact > false），否则 Claude Code 可能会在钩子有机会触发之前压缩上下文。当触发时，钩子会阻止 Claude 停止并告诉它运行 `/half-clone`。与自动压缩相比的优势在于半克隆是确定性的且快速——它保持你的实际消息完整而不是总结它们。

### 克隆脚本的推荐权限

两个克隆脚本都需要读取 `~/.claude`（用于对话文件和历史记录）。为了避免来自任何项目的权限提示，将以下内容添加到你的全局设置中（`~/.claude/settings.json`）：
```json
{
  "permissions": {
    "allow": ["Read(~/.claude)"]
  }
}
```

## Tip 24: 使用 realpath 获取绝对路径

当你需要告诉 Claude Code 关于不同文件夹中的文件时，使用 `realpath` 获取完整的绝对路径：

```bash
realpath some/relative/path
```

## Tip 25: 理解 CLAUDE.md、Skills（技能）、斜杠命令与插件的区别

这些功能有些相似，我最初发现它们相当令人困惑。我一直在解析它们并尽力试图理解它们，所以我想分享我所学到的。

**CLAUDE.md** 是最简单的一个。它是一堆被视为默认提示词的文件，无论什么情况都会加载到每次对话的开头。好处是简单性。你可以解释特定项目中的项目是什么（`./CLAUDE.md`）或全局（`~/.claude/CLAUDE.md`）。

**Skills（技能）** 就像是结构更好的 CLAUDE.md 文件。它们可以在相关时由 Claude 自动调用，或由用户手动通过斜杠调用（例如 `/my-skill`）。例如，你可以有一个技能，当你询问如何用某种语言发音单词时以适当的格式打开 Google Translate 链接。如果这些说明在技能中，它们仅在需要时加载。如果它们在 CLAUDE.md 中，它们已经在那里占用空间。所以从理论上讲，Skills（技能）更节省令牌。

**斜杠命令** 与 Skills（技能）类似，因为它们是将指令单独打包的方式。它们可以由用户手动调用，或由 Claude 本身调用。如果你需要更精确的东西，在你自己的节奏下在正确的时间调用，斜杠命令是使用工具。

Skills（技能）和斜杠命令在功能方式上非常相似。区别在于设计意图——Skills（技能）主要旨在供 Claude 使用，而斜杠命令主要旨在供用户使用。然而，他们最终 [合并了它们](https://www.reddit.com/r/ClaudeAI/comments/1q92wwv/merged_commands-and-skills-in-213-update/)，正如我 [建议此更改](https://github.com/anthropics/claude-code/issues/13115) 一样。

**插件（Plugins）** 是一种将 Skills（技能）、斜杠命令、代理、钩子和 MCP 服务器打包在一起的方式。但插件不必使用所有这些。Anthropic 的官方 `frontend-design` 插件本质上只是一个 Skill（技能），没有其他内容。它可以作为独立的 Skill（技能）分发，但插件格式使其更容易安装。

例如，我构建了一个名为 `dx` 的插件，将斜杠命令和此仓库中的 Skill（技能）捆绑在一起。你可以在 [安装 dx 插件](#tip-44-install-the-dx-plugin) 部分查看它是如何工作的。

## Tip 26: 交互式 PR 审查

Claude Code 非常适合 PR 审查。流程非常简单：你让它使用 `gh` 命令检索 PR 信息，然后你可以按照你想要的方式审查它。

你可以进行一般性审查，或逐文件、逐步进行。你控制节奏。你控制你想深入研究多少细节以及你想工作的复杂程度。也许你只想了解一般结构，或者你可能想让它也运行测试。

关键区别在于 Claude Code 充当交互式 PR 审查者，而不仅仅是一次性机器。一些 AI 工具擅长一次性审查（包括最新的 GPT 模型），但使用 Claude Code 你可以进行对话。

## Tip 27: Claude Code 作为研究工具

Claude Code 对于任何类型的研究来说都很棒。它本质上是一个 Google 替代品或深度研究替代品，但在几个方面更先进。无论你是研究为什么某些 GitHub Actions 失败（我最近一直在做这个）、在 Reddit 上进行情绪或市场分析、探索你的代码库还是探索公共信息以寻找某物——它都能做到这一点。

关键是为它提供正确的信息片段以及关于如何访问这些信息的说明。这可能是 `gh` 终端命令访问，或者是容器方法（Tip 21），或者通过 Gemini CLI 的 Reddit（Tip 11），或者通过像 Slack MCP 这样的 MCP 的私人信息，或者是 Cmd+A / Ctrl+A 方法（Tip 10）——无论是什么。此外，如果 Claude Code 难以加载某些 URL，你可以尝试使用 Playwright MCP 或 Claude 的原生浏览器集成（见 Tip 9）。对于科学研究，我创建了一个 [paper-search](https://github.com/ykdojo/paper-search) 插件用于搜索学术论文。

事实上，我甚至能够通过 [使用 Claude Code 进行研究节省 $10,000](content/how-i-saved-10k-with-claude-code.md)。

## Tip 28: 掌握验证其输出的不同方法

如果它是代码，验证其输出的一种方法是让它编写测试并确保测试总体看起来不错。这是一种方式，但你当然可以在它进行时检查它生成的代码，只是在 Claude Code UI 上。另一件事是你可以使用像 GitHub Desktop 这样的可视化 Git 客户端。我个人使用它。它不是一个完美的产品，但对于快速检查更改来说足够好。以及让它在前面提到的时候创建一个 PR 也是一种很好的方法。让它创建一个草稿 PR，在将其变成真正的 PR 之前检查内容。

另一个是让自我检查、自己的工作。如果它给你某种输出，比如来自某些研究，你可以说“你确定吗？能再检查一下吗？”我最喜欢的提示之一是“仔细检查所有内容，对你产生的每一个声明进行双重检查，并在最后制作一个你能验证什么的表格”——这似乎效果非常好。

## Tip 29: Claude Code 作为 DevOps 工程师

我特意为此创建一个单独的提示，因为它对我来说非常棒。每当有 GitHub Actions CI 失败时，我只是把它交给 Claude Code 并说“深入研究这个问题，尝试找到根本原因。”有时它会给你表面答案，但如果你继续问——是特定提交引起的吗？特定的 PR 吗？还是间歇性问题？——它真的有助于你深入挖掘这些很难手动挖掘的棘手问题。你需要穿过一堆日志，手动做这会非常痛苦，但 Claude Code 能够处理很多那部分。

我已经将此工作流程打包为 `/gha` 斜杠命令——只需运行 `/gha <url>` 并附带任何 GitHub Actions URL，它将自动调查失败、检查间歇性、识别破坏性提交并提出修复建议。你可以在 [skills 文件夹](skills/gha/SKILL.md) 中找到它，或通过 [dx 插件](#tip-44-install-the-dx-plugin) 安装。

一旦你确定了特定问题是什么，你可以创建一个草稿 PR 并浏览我之前提到的一些技巧——检查结果，确保看起来不错，让它验证自己的输出，然后将其变成真正的 PR 以实际修复问题。这对我个人来说效果非常好。

## Tip 30: 保持 CLAUDE.md 简洁并定期审查

保持 CLAUDE.md 简单和尽可能简洁很重要。你可以完全从没有 CLAUDE.md 开始。如果你发现你一遍又一遍地告诉 Claude Code 同样的事情，那么你可以将其添加到 CLAUDE.md 中。我知道可以通过 `#` 符号做到这一点，但我更喜欢只是让 Claude Code 要么将它添加到项目级别的 CLAUDE.md 或全局的 CLAUDE.md，它会知道要编辑什么确切内容。

![保持简单梗图](assets/keep-it-simple-meme.jpg)

定期审查你的 CLAUDE.md 文件也很重要，因为它们可能会随着时间的推移而过时。以前有意义的说明可能不再相关，或者你可能有新的模式应该记录。我创建了一个名为 [`review-claudemd`](skills/review-claudemd/SKILL.md) 的技能来分析你最近的对话并建议改进你的 CLAUDE.md 文件。

## Tip 31: Claude Code 作为通用接口

我曾经认为与 Claude Code，CLI 就像新的 IDE，这在某种程度上仍然是真的。我认为它总是很好的第一个地方来打开你的项目无论何时你想进行快速编辑等。但取决于你项目的严重程度，你想要比仅仅停留在 vibe coding（氛围编码）级别更仔细地对待输出。

但同样真实的是，那个更一般的情况是 Claude Code 真的是你计算机的通用接口、数字世界、你所拥有的任何类型的数字问题。在许多情况下你可以让它弄清楚。例如，如果你需要对你的视频进行快速编辑，你只需要求它做那件事——它可能会通过 ffmpeg 或类似的东西找出如何做。如果你想转录你在本地拥有的一堆音频文件或视频文件，你只需要求它做那件事——它可能会建议使用 Python 中的 Whisper。如果你想分析 CSV 文件中的一些数据，它可能会建议使用 Python 或 JavaScript 来可视化那个。当然还有互联网访问——Reddit、GitHub、MCPs——可能性是无限的。

它也非常适合你想在本地计算机上执行的任何操作。例如，如果你的存储空间不足，你只需要求它给你一些关于如何清理它的建议。它会查看你的本地文件夹和文件，尝试找出占用大量空间的东西，然后给你如何清理它们的建议——也许删除特别大的文件。在我的情况下，我有一些非常大的 Final Cut Pro 文件我应该清理掉。Claude Code 告诉了我。也许它会告诉你使用 `docker system prune` 清理未使用的 Docker 镜像和容器。或者也许它会告诉你清理一些你从未意识到仍然存在的缓存。无论你想在计算机上做什么，现在 Claude Code 是我首先去的地方。

我认为这有点有趣，因为计算机以文本界面开始。而我们，以一种方式回到这个文本界面，你可以一次启动三个或四个标签页，正如我之前提到的。对我来说，这真的很令人兴奋。感觉就像你有一个第二大脑。但由于它的结构方式，因为它只是一个终端标签页，你可以打开第三个大脑、第四个大脑、第五个大脑、第六个大脑。随着模型变得更有力量，你可以委托给这些东西的思考比例——不是重要的事情，而是你不想要做或你觉得无聊或太繁琐的事情——你可以让它们处理它。正如我之前提到的，一个很好的例子是查看 GitHub Actions。谁想做那个？但事实证明这些代理在这些枯燥的任务上非常擅长。

## Tip 32: 关键在于选择合适的抽象层级

正如我之前提到的，有时停留在 vibe coding（氛围编码）级别是可以的。如果你在处理一次性项目或非关键代码库部分时，你不必担心每一行代码。但其他时候，你想要更深入地挖掘——查看文件结构和函数、单行代码，甚至检查依赖项。

![Vibe coding 光谱](assets/vibe-coding-spectrum.png)

关键在于这不是二元的。有些人说 vibe coding 很糟糕是因为你不知道你在做什么，但有时完全没问题。但其他时候，深入挖掘很有帮助，使用你的软件工程技能，以粒度级别理解代码，或者复制和粘贴代码库的特定部分或特定的错误日志来询问 Claude Code 关于它们的具体问题。

这有点像你正在探索一座巨大的冰山。如果你想停留在 vibe coding 级别，你可以只是飞越顶部并从远处检查它。然后你可以靠近一点。你可以进入潜水模式。你可以更深入地挖掘，以 Claude Code 作为你的向导。

## Tip 33: 审计你批准的命令

我最近看到 [这篇文章](https://www.reddit.com/r/ClaudeAI/comments/1pgxckk/claude_cli_deleted-my-entire-home-directory-wiped/) 其中某人的 Claude Code 运行了 `rm -rf tests/ patches/ plan/ ~/` 并清除了他的主目录。很容易将其视为 vibe coder 的错误，但任何人都可能犯这种错误。所以定期审计你批准的命令很重要。为了使其更容易，我构建了 **cc-safe**——一个 CLI，扫描你的 `.claude/settings.json` 文件以查找有风险的批准命令。

它检测模式如下：
- `sudo`, `rm -rf`, `Bash`, `chmod 777`, `curl | sh`
- `git reset --hard`, `npm publish`, `docker run --privileged`
- 更多——它是容器感知的所以 `docker exec` 命令被跳过

它递归扫描所有子目录，因此你可以指向你的项目文件夹以一次性检查所有内容。你可以手动运行它或让 Claude Code 为你运行它：

```bash
npm install -g cc-safe
cc-safe ~/projects
```

或者直接使用 npx 运行它：

```bash
npx cc-safe .
```

GitHub: [cc-safe](https://github.com/ykdojo/cc-safe)

## Tip 34: 编写大量测试（并使用 TDD）

随着你用 Claude Code 编写更多代码，犯错误变得更容易。PR 审查和可视化 Git 客户端有助于捕获问题（正如我之前提到的），但随着你的代码库变大，编写测试至关重要。

你可以让 Claude Code 为它自己的代码编写测试。有些人说 AI 不能测试自己的工作，但事实证明它可以——类似于人类大脑的工作方式。当你编写测试时，你以不同的方式思考同一个问题。这也适用于 AI。

我发现 TDD（测试驱动开发）与 Claude Code 配合得非常好：

1. 首先编写测试
2. 确保它们失败
3. 提交测试
4. 编写代码使它们通过

这实际上是我如何构建 [cc-safe](https://github.com/ykdojo/cc-safe) 的。通过首先编写失败的测试并在实现之前提交它们，你为代码应该做什么创建了明确的契约。然后 Claude Code 有一个具体的目标要达成，并且可以通过运行测试来验证实现是否正确。

如果你想额外确定，自己审查测试以确保它们没有做任何愚蠢的事情比如只是返回 true。

## Tip 35: 在未知领域要更大胆；迭代式解决问题

自从我更密集地使用 Claude Code 以来，我注意到我在未知领域中变得越来越勇敢。

例如，当我开始在 [Daft](https://github.com/Eventual-Inc/Daft) 工作时，我注意到我们前端代码中有一个问题。我不是 React 专家，但我决定无论如何都要深入研究它。我只是开始询问关于代码库和问题的事情。最终我能够解决它因为我知道如何与 Claude Code 迭代解决问题。

最近发生了类似的事情。我正在为 Daft 的用户构建指南并遇到了一些非常具体的问题：cloudpickle 不能与 Google Colab 中的 Pydantic 一起工作，以及 Python 和一些 Rust 的单独问题，其中东西在 JupyterLab 中没有正确打印尽管它们在终端中运行良好。我从未处理过 Rust。

我可以只是创建一个问题并让其他工程师处理它。但我想，让我深入研究代码库。Claude Code 提出了一个初步解决方案，但那不是很好。所以我慢了下来。一位同事建议我们只是禁用那部分，但我不想有任何回归。我们能找到更好的解决方案吗？

随之而来的是协作和迭代的过程。Claude Code 提出了潜在的根本原因和解决方案。我尝试了那些。有些变成了死胡同，所以我们朝另一个方向前进。在此期间，我控制了我的节奏。有时我走得更快，比如让它探索不同的解决方案空间或代码库部分时。有时我走得更慢，问“这一行确切是什么意思？”控制抽象的级别，控制速度。

最终我发现了一个相当优雅的解决方案。教训是：即使在未知领域，你可以用 Claude Code 做比你想象的更多的事情。

## Tip 36: 在后台运行 bash 命令和子代理

当你在 Claude Code 中有长时间运行的 bash 命令时，你可以按 Ctrl+B 将其移动到后台运行。Claude Code 知道如何管理后台进程——它可以在以后使用 BashOutput 工具检查它们。

当你意识到一个命令花费的时间比预期长并且你想让 Claude 同时做其他事情时这是有用的。然后你可以让它使用我在 Tip 17 中提到的指数退避方法检查进度，或者只是让它在进程运行时完全处理其他东西。

Claude Code 还具有在后台运行子代理的能力。如果你需要做长时间的研究或让代理定期检查某些内容，你不必保持它在前景运行。只需让 Claude Code 在后台运行一个代理或任务，它会在你继续其他工作时处理它。

### 战略性使用子代理

除了在后台运行东西之外，当你要分解一个大任务时子代理也很有用。例如，如果你有一个巨大的代码库需要分析，你可以让子代理以不同的方式分析它或在并行中查看代码库的不同部分。只需让 Claude 生成多个子代理来处理不同的部分。

你可以通过只是询问来自定义子代理：
- **多少个** - 让 Claude 生成你想要的数量
- **后台与前景** - 要求它们在后台运行，或按 Ctrl+B
- **哪个模型** - 根据每个任务的复杂性要求 Opus、Sonnet 或 Haiku（子代理默认为 Sonnet）

## Tip 37: 个性化软件时代已到来

我们正进入一个个性化、定制软件的时代。自 AI 出现以来——ChatGPT 一般，但特别是 Claude Code——我注意到我能够创建更多的软件，有时只是为我自己，有时是为小项目。

正如我之前在这份文件中提到的，我已经创建了自定义转录工具我每天用来与 Claude Code 交谈。我已经创建了自定义 Claude Code 本身的方法。我还使用 Python 做了很多数据可视化和数据分析任务比我原本可以做的快得多。

这是另一个例子：[korotovsky/slack-mcp-server](https://github.com/korotovsky/slack-mcp-server)，一个流行的 Slack MCP，有近 1,000 个星，设计为作为 Docker 容器运行。我在自己的 Docker 容器中平滑使用它时有麻烦（Docker-in-Docker 并发症）。与其与那个设置搏斗，我只是让 Claude Code 直接使用 Slack 的 Node SDK 编写 CLI。效果非常好。

这是一个令人兴奋的时代。无论你想完成什么，你都可以要求 Claude Code 去做。如果足够小，你可以在一两个小时内构建它。我甚至创建了一个 [幻灯片模板](https://ykdojo.github.io/claude-code-tips/content/spectrum-slides.html)——一个带有 CSS 和 JavaScript 的单个 HTML 文件，让你在其中嵌入交互式、持久的终端进程。

## Tip 38: 导航和编辑你的输入框

Claude Code 的输入框旨在模拟常见的终端/readline 快捷键，这使如果你习惯于在终端中工作感觉自然。以下是一些有用的：

**导航：**
- `Ctrl+A` - 跳转到行首
- `Ctrl+E` - 跳转到行尾
- `Option+左/右` (Mac) 或 `Alt+左/右` - 按单词向后/向前跳转

**编辑：**
- `Ctrl+W` - 删除前一个词
- `Ctrl+U` - 从光标到行首删除
- `Ctrl+K` - 从光标到行尾删除
- `Ctrl+C` / `Ctrl+L` - 清除当前输入
- `Ctrl+G` - 在外部编辑器中打开你的提示（对于粘贴长文本很有用，因为直接粘贴到终端可能很慢）

如果你熟悉 bash、zsh 或其他 shell，你会觉得宾至如归。

对于 `Ctrl+G`，编辑器由你的 `EDITOR` 环境变量决定。你可以在你的 shell 配置中设置它（`~/.zshrc` 或 `~/.bashrc`）：

```bash
export EDITOR=vim      # or nano, code, nvim, etc.
```

或在 `~/.claude/settings.json` 中（需要重启）：

```json
{
  "env": {
    "EDITOR": "vim"
  }
}
```

**输入换行符（多行输入）：**

最快的方法在任何地方都有效无需任何设置：键入 `\` 后跟 Enter 以创建换行。对于键盘快捷键，在 Claude Code 中运行 `/terminal-setup`。在 Mac Terminal.app 上，我使用 Option+Enter。

**粘贴图片：**
- `Ctrl+V` (Mac/Linux) 或 `Alt+V` (Windows) - 从剪贴板粘贴图片

注意：在 Mac 上是 `Ctrl+V`，而不是 `Cmd+V`。

## Tip 39: 花些时间规划，但也快速原型开发

你想花费足够的时间进行规划以便 Claude Code 知道要构建什么以及如何构建它。这意味着尽早做出高层决策：使用什么技术、项目应该如何结构化、每个功能应该住在哪里、东西应该在哪些文件中。尽早做出好的决定很重要。

有时原型开发有助于那个。只是通过快速制作一个简单的原型，你可能能够说“好吧，这项技术适用于这个特定目的”或“那项其他技术效果更好”。

例如，我最近正在尝试创建差异查看器。我首先尝试了一个带有 tmux 和 lazygit 的简单 bash 原型，然后尝试用 Ink 和 Node 制作我自己的 git 查看器。我在不同的东西上遇到了很多麻烦，最终没有发布任何这些结果。但这个项目提醒我的事情是规划和原型开发的重要性。我发现只是通过在让它编写代码之前更好地规划一点，你能够更好地指导它。你仍然需要在编码过程中引导它，但让它在开始时先计划一下真的很有帮助。

你可以使用 plan mode 通过按 Shift+Tab 切换到它来实现这一点。或者你只需在编写任何代码之前要求 Claude Code 制定一个计划。

## Tip 40: 简化过于复杂的代码

我发现 Claude Code 有时会过度复杂化事情并编写太多代码。它会做你没有要求的更改。它似乎只是有编写更多代码的偏见。如果你遵循本指南中的其他技巧，代码可能会正确工作，但它将难以维护和检查。如果你没有足够审查它，它可能有点噩梦。

所以有时你想检查代码并要求它简化东西。你可以自己修复东西，但你也可以只是要求它简化。你可以问诸如“你为什么做这个特定更改？”或“你为什么添加这一行？”之类的问题。

有些人说如果你只通过 AI 编写代码，你将永远不会理解它。但这只有在你没有问足够问题的情况下才是真的。如果你确保你理解每一件事，你实际上可以比其他情况更快地理解代码因为你可以向 AI 询问它。特别是当你处理大型项目时。

请注意这也适用于散文。Claude Code 经常试图在最后一段总结前面的段落，或在最后一句话中总结前面的句子。它可以变得相当重复。有时这很有帮助，但大多数时候你需要要求它删除或简化它。

## Tip 41: 自动化的自动化

归根结底，一切都是关于自动化的自动化。我的意思是那就是我发现的不仅是变得更高效而且使过程更有趣的方法。至少对我来说，这种自动化的自动化的整个过程真的很有趣。

我个人从 ChatGPT 开始并想要自动化复制粘贴和运行 ChatGPT 给我的命令的过程。我通过构建一个名为 [Kaguya](https://github.com/ykdojo/kaguya) 的 ChatGPT 插件自动化了那个整个过程。从那以后我一直致力于越来越多的自动化。

如今，幸运的是，我们甚至不必构建像那样的工具因为像 Claude Code 这样的工具存在并且它们工作得非常好。而且随着我越来越多地使用它，我发现自己思考，好吧，如果我能够自动化打字的过程呢？所以我使用 Claude Code 本身来构建我的语音转录应用，正如我之前提到的。

然后我开始想，我发现自己有时在重复自己。所以我会把那些东西放在 CLAUDE.md 中。然后我会想，好的，有时我一遍又一遍地运行相同的命令。我怎么自动化那个？也许我可以要求 Claude Code 去做。或者也许我可以把它们放在 Skills（技能）中。或者甚至可以让它创建一个脚本以便我不必一遍又一遍地重复相同的过程。

我认为最终我们正朝着那个方向前进。每当你发现自己一遍又一遍地做同样的任务或执行相同的命令时，几次是可以的，但如果你一遍又一遍地重复它，那么考虑一种方法来自动化那个整个过程。

## Tip 42: 分享你的知识并在力所能及的范围内贡献

这个提示与其他提示有点不同。我发现通过尽可能多地学习，你能够与他人分享你的知识。也许通过这些帖子，甚至书籍、课程、视频。我最近还为我 [Daft 的同事举办了一次内部会议](https://www.daft.ai/blog/how-we-use-ai-coding-agents)。这非常有回报性。

每当我分享技巧时，我经常得到信息反馈。例如，当我分享我的缩短系统提示词和工具描述的技巧（Tip 15）时，有些人告诉我关于你可以用作替代方案的 `--system-prompt` 标志。另一次，我分享了斜杠命令和技能之间的区别（Tip 25），我从那个 Reddit 帖子的评论中学到了新东西。

所以分享你的知识不仅仅是为了建立你的品牌或巩固你的学习。它也是通过那个过程学习新的东西。这不总是一条单行道。

关于贡献，我一直在向 Claude Code 仓库发送问题。我想，好的，如果他们听，酷。如果他们没有，那完全没问题。我没有任何期望。但在版本 2.0.67 中，我注意到他们接受了我报告中的多个建议：

- 修复了 `/permissions` 中删除权限规则后滚动位置重置的问题
- 向 `/permissions` 命令添加了搜索功能

团队对功能请求和错误报告的响应速度之快真是令人惊讶。但这很有道理因为他们使用 Claude Code 来构建 Claude Code 本身。

## Tip 43: 保持学习！

有几种有效的方法来继续学习关于 Claude Code：

**询问 Claude Code 本身** - 如果你对 Claude Code 有疑问，只需问它。Claude Code 有一个专门的子代理用于回答有关其自身功能、斜杠命令、设置、钩子、MCP 服务器等的问题。

**检查发布说明** - 输入 `/release-notes` 以查看当前版本中的新功能。这是了解最新功能的最佳方式。

**向社区学习** - [r/ClaudeAI](https://www.reddit.com/r/ClaudeAI/) subreddit 是向其他用户学习并查看人们使用的工作流的好地方。

**关注 Ado 获取技巧** - Ado ([@adocomplete](https://x.com/adocomplete)) 是 Anthropic 的 DevRel，他在 2025 年 12 月发布了每日 Claude Code 技巧在他的“Advent of Claude”系列中。虽然这个特定系列已经结束，但他继续在 X 上分享有用的技巧。

- [Twitter/X: Advent of Claude posts](https://x.com/search?q=from%3Aadocomplete%20advent%20of%20claude&src=typed_query&f=live)
- [LinkedIn: Advent of Claude posts](https://www.linkedin.com/search/results/content/?fromMember=%5B%22ACoAAAFdD3IBYHwKSh6FsyGqOh1SpbrZ9ZHTjnI%22%5D&keywords=advent%20of%20claude&origin=FACETED_SEARCH&sid=zDV&sortBy=%22date_posted%22)

## Tip 44: 安装 dx 插件

这个仓库也是一个名为 `dx`（developer experience）的 Claude Code 插件。它将上述几个工具捆绑到一个单独的安装中：

| Skill | Description |
|-------|-------------|
| `/dx:gha <url>` | 分析 GitHub Actions 失败 (Tip 29) |
| `/dx:handoff` | 创建上下文连续性的交接文档 (Tip 8) |
| `/dx:clone` | 克隆对话以分支出去 (Tip 23) |
| `/dx:half-clone` | 半克隆以减少上下文 (Tip 23) |
| `/dx:reddit-fetch` | 通过 Gemini CLI 获取 Reddit 内容 (Tip 11) |
| `/dx:review-claudemd` | 审查对话以改进 CLAUDE.md 文件 (Tip 30) |

**使用两个命令安装：**

```bash
claude plugin marketplace add ykdojo/claude-code-tips
claude plugin install dx@ykdojo
```

安装后，命令作为 `/dx:clone`、`/dx:half-clone`、`/dx:handoff` 和 `/dx:gha` 可用。`reddit-fetch` 技能在你询问 Reddit URL 时自动调用。`review-claudemd` 技能分析你最近的对话并建议改进你的 CLAUDE.md 文件。对于克隆命令，请参阅 [推荐权限](#recommended-permission-for-clone-scripts)。

**推荐的配套：** [Playwright MCP](https://github.com/microsoft/playwright-mcp) 用于浏览器自动化——使用 `claude mcp add -s user playwright npx @playwright/mcp@latest` 添加

## Tip 45: 快速设置脚本

如果你想一次性设置此仓库中的多个推荐项，有一个处理其中许多内容的设置脚本：

```bash
bash <(curl -s https://raw.githubusercontent.com/ykdojo/claude-code-tips/main/scripts/setup.sh)
```

该脚本向你显示它将配置的所有内容并允许你跳过任何项目：

```
INSTALLS:
  1. DX plugin - slash commands (/dx:gha, /dx:clone, /dx:handoff) and skills (reddit-fetch)
  2. cc-safe - scans your settings for risky approved commands like 'rm -rf' or 'sudo'

SETTINGS (~/.claude/settings.json):
  3. Status line - shows model, git branch, uncommitted files, token usage at bottom of screen
  4. Disable auto-updates - prevents Claude Code from auto-updating (useful for system prompt patches)
  5. Lazy-load MCP tools - only loads MCP tool definitions when needed, saves context
  6. Read(~/.claude) permission - allows clone/half-clone commands to read conversation history
  7. Read(//tmp/**) permission - allows reading temporary files without prompts
  8. Disable attribution - removes Co-Authored-By from commits and attribution from PRs

SHELL CONFIG (~/.zshrc or ~/.bashrc):
  9. Aliases: c=claude, ch=claude --chrome, cs=claude --dangerously-skip-permissions
 10. Fork shortcut: --fs expands to --fork-session (e.g., claude -c --fs)

Skip any? [e.g., 1 4 7 or Enter for all]:
```

---

📺 **相关演讲**: [Claude Code Masterclass](https://youtu.be/9UdZhTnMrTA) - 来自 31 个月代理式编码的课程和项目示例

📝 **故事**: [我是如何凭借 Claude Code 获得全职工作的](content/how-i-got-a-job-with-claude-code.md)

📰 **Newsletter**: [Agentic Coding with Discipline and Skill](https://agenticcoding.substack.com/) - 将代理式编码的实践提升到下一个水平
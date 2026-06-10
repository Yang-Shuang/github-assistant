[![npm version][npm-version-src]][npm-version-href]
[![npm downloads][npm-downloads-src]][npm-downloads-href]
[![License][license-src]][license-href]
[![Claude Code][claude-code-src]][claude-code-href]
[![codecov][codecov-src]][codecov-href]
[![JSDocs][jsdocs-src]][jsdocs-href]
[![Ask DeepWiki][deepwiki-src]][deepwiki-href]

<div align="center">
  <img src="./src/assets/banner.webp" alt="Banner"/>

  <h1>
    ZCF - Zero-Config Code Flow
  </h1>

  <p align="center">
  <b>English</b> | <a href="README_zh-CN.md">中文</a> | <a href="README_ja-JP.md">日本語</a> | <a href="CHANGELOG.md">Changelog（更新日志）</a>

**✨ 完整文档**: [ZCF Docs](https://zcf.ufomiao.com/)

> 零配置，一键设置 Claude Code & Codex。支持双语、智能 Agent 系统及个性化 AI 助手
</p>
</div>

## ♥️ 赞助商

[![GLM](./src/assets/GLM-en.png)](https://z.ai/subscribe?ic=8JVLJQFSKB)

本项目由 Z.ai 赞助，感谢他们通过 GLM CODING PLAN 提供支持。
GLM CODING PLAN 是一项专为 AI 编程设计的订阅服务，月费低至 $10/月起。它提供旗舰级 GLM-4.7 & （仅 Pro 用户可用 GLM-5）模型，支持 Claude Code、Cline、Roo Code 等 10+ 款主流 AI 编程工具，为开发者提供顶级、快速且稳定的编码体验。
领取 GLM CODING PLAN 9折优惠：https://z.ai/subscribe?ic=8JVLJQFSKB

---

[![Sponsor PatewayAI](./src/assets/pateway.ai-en.png)](https://pateway.ai/?ch=vnr0h5&aff=9AWWH87C)
PatewayAI 是一家专注于官方直连的高质量模型 API 中转服务商，面向专业 AI 开发者提供完整的 Claude 和 Codex 系列模型。100% 官方源头货源，无掺假——欢迎查验。计费透明，支持按 Token 级别逐行开具发票审计。企业级并发支持，配备专属企业管理平台，包含正式合同与开票服务。PatewayAI 为 ZCF 用户提供专属福利：通过 <a href="https://pateway.ai/?ch=vnr0h5&aff=9AWWH87C">此链接</a> 注册可获赠 $3 免费体验额度，充值低至 6 折，双边邀请奖励最高可达 $150！

---

[![Sponsor AI API](./src/assets/302.ai-en.jpg)](https://share.302.ai/gAT9VG)
[302.AI](https://share.302.ai/gAT9VG) 是一个按量付费的企业级 AI 资源库，提供市场上最新、最全面的 AI 模型与 API，以及多种开箱即用的在线 AI 应用。

---

<table>
<tbody>
<tr>
<td width="180"><a href="https://www.packyapi.com/register?aff=zcf"><img src="./src/assets/packycode.png" alt="PackyCode" width="150"></a></td>
<td>感谢 PackyCode 赞助本项目！PackyCode 是一家可靠高效的 API 中转服务商，提供 Claude Code、Codex、Gemini 等服务的代理。PackyCode 为我们的软件用户提供专属优惠：使用 <a href="https://www.packyapi.com/register?aff=zcf">此链接</a> 注册，充值时填写推广码 "zcf" 可享 9 折优惠。</td>
</tr>
<tr>
<td width="180"><a href="https://apikey.fun/register?aff=ZCFZCF"><img src="./src/assets/apikey-fun.png" alt="APIKEY.FUN" width="150"></a></td>
<td>感谢 APIKEY.FUN 赞助本项目！APIKEY.FUN 是一家专业的企业级 AI 中转平台，致力于为企业和个人开发者提供稳定、高效且低成本的 API 访问服务。平台支持 Claude、OpenAI、Gemini 等主流模型，价格低至官方价的 7 折。通过 <a href="https://apikey.fun/register?aff=ZCFZCF">此链接</a> 注册可享专属优惠：充值永久享受最高 95 折（5 折优惠）。</td>
</tr>
<tr>
<td width="180"><a href="https://www.aicodemirror.com/register?invitecode=ZCFZCF"><img src="./src/assets/AICodeMirror.jpg" alt="AICodeMirror" width="150"></a></td>
<td>感谢 AICodeMirror 赞助本项目！AICodeMirror 提供 Claude Code/Codex/Gemini CLI 的官方高稳定性代理服务，支持企业级高并发、快速开票及 7x24 专属技术支持。Claude Code/Codex/Gemini 官方渠道折扣低至 38%/2%/10.9%，充值还可叠加优惠！AICodeMirror 为 ZCF 用户提供专属福利：通过 <a href="https://www.aicodemirror.com/register?invitecode=ZCFZCF">此链接</a> 注册可享首充 8 折，企业客户最高可享 75 折！</td>
</tr>
<tr>
<td width="180"><a href="https://crazyrouter.com/?utm_source=github&utm_medium=sponsor&utm_campaign=zcf&aff=yJFo"><img src="./src/assets/crazyrouter.svg" alt="Crazyrouter" width="150"></a></td>
<td>感谢 Crazyrouter 赞助本项目！Crazyrouter 是一款高性能 AI API 聚合网关——一把 API Key 即可调用 300+ 模型（GPT、Claude、Gemini、DeepSeek 等）。所有模型定价均为官方价的 55%，支持自动故障转移、智能路由及无限并发。完全兼容 OpenAI，与 Claude Code、Codex、Gemini CLI 无缝对接。Crazyrouter 为 ZCF 用户提供专属优惠：通过 <a href="https://crazyrouter.com/?utm_source=github&utm_medium=sponsor&utm_campaign=zcf&aff=yJFo">此链接</a> 注册可立即获赠 $2 免费额度！</td>
</tr>
</tbody>
</table>

## 🚀 快速上手

- 推荐用法：运行 `npx zcf` 打开交互式菜单，按需选择。
- 常用命令：

```bash
npx zcf i        # 完整初始化：安装 + workflows + API/CCR + MCP
npx zcf u        # 仅更新 workflows
npx zcf --lang zh-CN  # 切换界面语言（示例）
```

- 非交互示例（预设服务商）：

```bash
npx zcf i -s -p 302ai -k "sk-xxx"
```

更多用法、选项及工作流详情，请参阅文档。

## 📖 完整文档

- https://zcf.ufomiao.com/

## 💬 社区交流

加入我们的 Telegram 群组获取支持、参与讨论及接收更新：

[![Telegram](https://img.shields.io/badge/Telegram-Join%20Chat-blue?style=flat&logo=telegram)](https://t.me/ufomiao_zcf)

## 🙏 鸣谢

本项目受以下项目启发并借鉴了其工作：

- [LINUX DO - New Ideal Community](https://linux.do)
- [CCR](https://github.com/musistudio/claude-code-router)
- [CCometixLine](https://github.com/Haleclipse/CCometixLine)
- [ccusage](https://github.com/ryoppippi/ccusage)
- [BMad Method](https://github.com/bmad-code-org/BMAD-METHOD)

感谢这些社区贡献者的分享！

## ❤️ 支持与赞助

如果你觉得本项目对你有帮助，欢迎考虑赞助其开发。你的支持对我们至关重要！

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/UfoMiao)

<table>
  <tr>
    <td><img src="/src/assets/alipay.webp" width="200" alt="Alipay" /></td>
    <td><img src="/src/assets/wechat.webp" width="200" alt="WeChat Pay" /></td>
  </tr>
</table>

### 我们的赞助商

衷心感谢所有赞助商的慷慨支持！

【企业赞助商】

- [302.AI](https://share.302.ai/gAT9VG)（首家企业赞助 🤠）
- [GLM](https://z.ai/subscribe?ic=8JVLJQFSKB)（首款 AI 模型赞助 🤖）
- [PackyCode](https://www.packyapi.com/register?aff=zcf)（首家 API 代理服务商赞助 🧝🏻‍♀️）
- [APIKEY.FUN](https://apikey.fun/register?aff=ZCFZCF)（企业 AI 中转赞助 🎁）
- [AICodeMirror](https://www.aicodemirror.com/register?invitecode=ZCFZCF)（官方高稳定性代理服务赞助 🪞）
- [UUCode](https://www.uucode.org/auth?ref=JQ2DJ1T8)（赞助 $100 代理额度 💰）
- [Crazyrouter](https://crazyrouter.com/?utm_source=github&utm_medium=sponsor&utm_campaign=zcf&aff=yJFo)（AI API 聚合网关赞助 🚀）
- [PatewayAI](https://pateway.ai/?ch=vnr0h5&aff=9AWWH87C)（官方直连代理服务赞助 🛡️）

【个人赞助商】

- Tc（首位赞助商）
- Argolinhas（首位 ko-fi 赞助者 ٩(•̤̀ᵕ•̤́๑))
- r*r（首位匿名赞助者 🤣）
- **康（首位 KFC 赞助者 🍗）
- *东（首位咖啡赞助者 ☕️）
- 炼*3（首位 Termux 用户赞助者 📱）
- [chamo101](https://github.com/chamo101)（首位 GitHub Issue 赞助者 🎉）
- 初屿贤（首位 Codex 用户赞助者 🙅🏻‍♂️）
- Protein（首位 1688 赞助者 😏）
- [musistudio](https://github.com/musistudio)（首位开源项目作者赞助者，[CCR](https://github.com/musistudio/claude-code-router) 的作者 🤩）
- *年（首位 100 CNY 赞助者 💴）
- [BeatSeat](https://github.com/BeatSeat)（社区专家 😎，提供 $1000 Claude 额度）
- [wenwen](https://github.com/wenwen12345)（社区专家 🤓，每日提供 $100 Claude&GPT 额度）
- 16°C coffee（我的好朋友 🤪，提供 ChatGPT Pro $200 套餐）

### 推广鸣谢

感谢以下作者对本项目的推广：

- 逛逛 GitHub, 文章: https://mp.weixin.qq.com/s/phqwSRb16MKCHHVozTFeiQ
- Geek, tweet: https://x.com/geekbb/status/1955174718618866076

## 📄 开源协议

[MIT License](LICENSE)

---

## 🚀 贡献者

<a href="https://github.com/UfoMiao/zcf/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=UfoMiao/zcf" />
</a>
<br /><br />

## ⭐️ Star 历史

如果本项目对你有帮助，请给我一个 ⭐️ Star！

[![Star History Chart](https://api.star-history.com/svg?repos=UfoMiao/zcf&type=Date)](https://star-history.com/#UfoMiao/zcf&Date)

<!-- Badges -->

[npm-version-src]: https://img.shields.io/npm/v/zcf?style=flat&colorA=080f12&colorB=1fa669
[npm-version-href]: https://npmjs.com/package/zcf
[npm-downloads-src]: https://img.shields.io/npm/dm/zcf?style=flat&colorA=080f12&colorB=1fa669
[npm-downloads-href]: https://npmjs.com/package/zcf
[license-src]: https://img.shields.io/github/license/ufomiao/zcf.svg?style=flat&colorA=080f12&colorB=1fa669
[license-href]: https://github.com/ufomiao/zcf/blob/main/LICENSE
[claude-code-src]: https://img.shields.io/badge/Claude-Code-1fa669?style=flat&colorA=080f12&colorB=1fa669
[claude-code-href]: https://claude.ai/code
[codecov-src]: https://codecov.io/gh/UfoMiao/zcf/graph/badge.svg?token=HZI6K4Y7D7&style=flat&colorA=080f12&colorB=1fa669
[codecov-href]: https://codecov.io/gh/UfoMiao/zcf
[jsdocs-src]: https://img.shields.io/badge/jsdocs-reference-1fa669?style=flat&colorA=080f12&colorB=1fa669
[jsdocs-href]: https://www.jsdocs.io/package/zcf
[deepwiki-src]: https://img.shields.io/badge/Ask-DeepWiki-1fa669?style=flat&colorA=080f12&colorB=1fa669
[deepwiki-href]: https://deepwiki.com/UfoMiao/zcf
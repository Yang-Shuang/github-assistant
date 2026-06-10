# jscpd

![stand with Ukraine](https://badgen.net/badge/support/UKRAINE/?color=0057B8&labelColor=FFD700)

[![npm](https://img.shields.io/npm/v/jscpd.svg?style=flat-square)](https://www.npmjs.com/package/jscpd)
![jscpd](https://raw.githubusercontent.com/kucherenko/jscpd/master/assets/jscpd-badge.svg?sanitize=true)
[![license](https://img.shields.io/github/license/kucherenko/jscpd.svg?style=flat-square)](https://github.com/kucherenko/jscpd/blob/master/LICENSE)
[![npm](https://img.shields.io/npm/dw/jscpd.svg?style=flat-square)](https://www.npmjs.com/package/jscpd)


[![jscpd CI](https://github.com/kucherenko/jscpd/actions/workflows/nodejs.yml/badge.svg)](https://github.com/kucherenko/jscpd/actions/workflows/nodejs.yml)
[![codecov](https://codecov.io/gh/kucherenko/jscpd/branch/master/graph/badge.svg)](https://codecov.io/gh/kucherenko/jscpd)
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Fkucherenko%2Fjscpd.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2Fkucherenko%2Fjscpd?ref=badge_shield)
[![Backers on Open Collective](https://opencollective.com/jscpd/backers/badge.svg)](#backers)
[![Sponsors on Open Collective](https://opencollective.com/jscpd/sponsors/badge.svg)](#sponsors)

[![NPM](https://nodei.co/npm/jscpd.svg)](https://nodei.co/npm/jscpd/)

> 面向编程源代码的复制/粘贴检测器，支持 223 种格式。具备 AI 就绪特性（包含 AI Skills、MCP Server 及 Token 高效 Reporter）。

复制/粘贴是许多项目中常见的技术债务。jscpd 能够检测并找出超过 223 种编程语言和数字文档格式中的重复代码块。该工具采用了 [Rabin-Karp](https://en.wikipedia.org/wiki/Rabin%E2%80%93Karp_algorithm) 算法进行重复内容搜索。

## Packages of jscpd

| name                 | version  |  description  |
|----------------------|----------|---------------|
| [jscpd](apps/jscpd) | [![npm](https://img.shields.io/npm/v/jscpd.svg?style=flat-square)](https://www.npmjs.com/package/jscpd) | jscpd 主程序（包含 CLI 和用于检测的 API） |
| [jscpd-server](apps/jscpd-server) | [![npm](https://img.shields.io/npm/v/jscpd-server.svg?style=flat-square)](https://www.npmjs.com/package/jscpd-server) | jscpd 服务端应用 |
| [@jscpd/core](packages/core) | [![npm](https://img.shields.io/npm/v/@jscpd/core.svg?style=flat-square)](https://www.npmjs.com/package/@jscpd/core) | 核心检测算法，可用于在不同环境中检测重复代码，仅依赖 eventemitter3 |
| [@jscpd/finder](packages/finder) | [![npm](https://img.shields.io/npm/v/@jscpd/finder.svg?style=flat-square)](https://www.npmjs.com/package/@jscpd/finder) | 文件级重复代码检测器 |
| [@jscpd/tokenizer](packages/tokenizer) | [![npm](https://img.shields.io/npm/v/@jscpd/tokenizer.svg?style=flat-square)](https://www.npmjs.com/package/@jscpd/tokenizer) | 编程源代码分词（Tokenization）工具 |
| [@jscpd/leveldb-store](packages/leveldb-store) | [![npm](https://img.shields.io/npm/v/@jscpd/leveldb-store.svg?style=flat-square)](https://www.npmjs.com/package/@jscpd/leveldb-store) | LevelDB 存储后端，适用于大型仓库，速度比默认存储稍慢 |
| [@jscpd/html-reporter](packages/html-reporter) | [![npm](https://img.shields.io/npm/v/@jscpd/html-reporter.svg?style=flat-square)](https://www.npmjs.com/package/@jscpd/html-reporter) | jscpd HTML 报告生成器（Reporter） |
| [@jscpd/badge-reporter](packages/badge-reporter) | [![npm](https://img.shields.io/npm/v/@jscpd/badge-reporter.svg?style=flat-square)](https://www.npmjs.com/package/@jscpd/badge-reporter) | jscpd 徽章报告生成器（Reporter） |
| [jscpd-sarif-reporter](packages/sarif-reporter) | [![npm](https://img.shields.io/npm/v/jscpd-sarif-reporter.svg?style=flat-square)](https://www.npmjs.com/package/jscpd-sarif-reporter) | jscpd SARIF 报告生成器（Reporter）（兼容 GitHub Code Scanning） |

## AI-Ready

jscpd 通过三种互补机制集成到 AI 驱动的开发工作流中。

### AI Reporter

`ai` Reporter 会输出紧凑且 Token 消耗极低的内容，专为直接输入到 LLM Prompt 或 Agent 工作流而设计。它采用公共路径前缀压缩技术，省略代码片段和颜色标记——仅保留克隆位置及摘要信息。

```bash
jscpd --reporters ai /path/to/source
```

Example output:
```
src/utils/ auth.ts:10-25 ~ helpers.ts:40-55
src/utils/auth.ts 30-45 ~ 80-95
src/ utils/auth.ts:10-25 ~ api/routes.ts:5-20
---
23 clones · 4.2% duplication
```

Benchmarked on the `fixtures/` directory (91 clones, 132 files):

| Reporter | Output size | Estimated tokens |
|----------|-------------|------------------|
| default (console) | ~21,800 chars | ~5,400 |
| `ai` | ~4,500 chars | ~1,100 |

相比默认的 console Reporter，Token 消耗减少约 79%。

### Agent Skills

jscpd 内置两项 AI Agent Skills，用于指导代码助手如何使用 jscpd 并对检测到的重复代码进行重构：

**jscpd** —— 工具参考技能（Tool Reference Skill）。涵盖所有 CLI 选项、AI Reporter 输出格式及配置文件语法。安装方式如下：
```bash
npx skills add kucherenko/jscpd --skill jscpd
```

**dry-refactoring** —— 重构工作流技能（Refactoring Workflow Skill）。提供引导式流程，用于读取克隆输出、选择正确的提取策略、执行重构并验证重复代码是否已消除。安装方式如下：
```bash
npx skills add kucherenko/jscpd --skill dry-refactoring
```

安装完成后，只需让 Agent 执行“查找并修复代码重复”指令，它便会自动调用带有正确参数的 jscpd 并根据结果采取行动。

### MCP Server

[jscpd-server](apps/jscpd-server) 实现了 [Model Context Protocol (MCP)](https://modelcontextprotocol.io)，将 jscpd 的检测能力封装为工具，供 AI 助手直接在编辑器中调用。只需针对你的代码库启动一次服务端，之后即可按需让 AI 助手检查任意代码片段的重复情况——无需手动执行 CLI 命令。

```bash
npm install -g jscpd-server
jscpd-server /path/to/project
```

Add to your MCP client config (e.g. Claude Desktop):

```json
{
  "mcpServers": {
    "jscpd": {
      "type": "streamable-http",
      "url": "http://localhost:3000/mcp"
    }
  }
}
```

可用的 MCP 工具包括：`check_duplication`、`get_statistics`、`check_current_directory`。完整 API 文档请参阅 [apps/jscpd-server](apps/jscpd-server)。

## What's New

**v4.2.x**

- **Custom tokenizer backend** —— 使用基于 [reprism](https://github.com/tannerlinsley/reprism) 语法引擎构建的自有后端替换了 `prismjs` npm 包。在实际项目中分词速度提升约 11.5%（在包含 548 个文件、223 种格式的扫描中，平均耗时从 1126ms 降至 997ms）。
- **Cross-format detection** —— 现在 Vue SFC (`.vue`)、Svelte (`.svelte`)、Astro (`.astro`) 和 Markdown 文件将按代码块/区块进行分词，从而支持跨文件格式的重复检测（例如 `.vue` 文件中的 `<script>` 块与 `.ts` 文件的匹配）。
- **New formats**: Apex, CFML/ColdFusion, GDScript, and 70+ additional formats (223 total, up from 152) -> 新增格式：Apex、CFML/ColdFusion、GDScript 以及 70 余种其他格式（总计支持 223 种，较之前的 152 种有所增加）
- **Shebang detection**: auto-detect language for extensionless executable scripts -> Shebang 检测：自动识别无扩展名可执行脚本的语言类型
- **`--store-path`**: configure LevelDB cache directory for parallel runs -> `--store-path`：配置并行运行时的 LevelDB 缓存目录
- **`--skipComments`**: shorthand flag for `--mode weak` -> `--skipComments`：`--mode weak` 的简写参数
- **`--formats-names`**: map specific filenames (e.g. `Makefile`, `Dockerfile`) to a format -> `--formats-names`：将特定文件名（如 `Makefile`、`Dockerfile`）映射到对应格式
- **`--noTips`**: suppress tip output in CI environments -> `--noTips`：在 CI 环境中抑制提示输出

### Bug Fixes

- **Entire-file duplicates silently dropped** —— RabinKarp 算法在文件末尾遇到存储命中（*hit*）时才刷新待检测克隆项，而非未命中（*miss*），导致完全相同的文件未被检测到。已在 `@jscpd/core` 中修复 (#728)。
- **ReDoS hang on Lisp/Elisp files** —— Lisp 字符串正则表达式 `/"(?:[^"\\]*|\\.)*"/` 在未闭合的字符串上可能发生灾难性回溯（O(2ⁿ)）。已替换为线性复杂度方案。已在 `@jscpd/tokenizer` 中修复 (#737)。
- **Process crash on malformed `package.json`** —— 当 jscpd 在包含无效 JSON 的 `package.json` 目录中运行时，`readJSONSync` 会抛出未处理的 `SyntaxError` 并终止进程。现已改为发出警告并使用空配置继续运行 (#739)。
- **Vue SFC cross-file detection broken** —— 检测器曾将所有 SFC 块的文件级格式（`vue`）用作存储命名空间，导致一个 `.vue` 文件中的 `<script>` 块永远无法与另一个匹配。现在命名空间已改为反映每个代码块解析后的子格式（如 `javascript`、`typescript`、`scss` 等）。
- **Vue SFC incorrect column numbers** —— 代码块第一行的 Token 曾使用相对于块的列号 1，而非文件绝对列号。已在 `@jscpd/tokenizer` 中修复。
- **50 dependency security vulnerabilities** remediated across the monorepo (Dependabot batches #DR-43 and #DR-7). -> 跨 Monorepo 修复了 50 项依赖安全漏洞（Dependabot 批次 #DR-43 和 #DR-7）。

## Installation
```bash
$ npm install -g jscpd
```
## Usage
```bash
$ npx jscpd /path/to/source
```
or

```bash
$ jscpd /path/to/code
```
or

```bash
$ jscpd --pattern "src/**/*.js"
```
CLI 更多信息请参见[此处](apps/jscpd)。

## JSCPD Server

JSCPD Server 是一款独立应用程序，提供用于检测代码重复的 API。你可将其集成到自有服务或工具中。

### Installation

```bash
$ npm install -g jscpd-server
```

### Usage

启动服务端：

```bash
$ jscpd-server
```

检查代码重复情况：

```bash
$ curl -X POST http://localhost:3000/api/check \
  -H "Content-Type: application/json" \
  -d '{
    "code": "console.log(\"hello\");\nconsole.log(\"world\");",
    "format": "javascript"
  }'
```

服务端更多信息请参见[此处](apps/jscpd-server)。

## Programming API

若要将复制/粘贴检测功能集成到你的应用中，可使用以下编程 API：

`jscpd` Promise API
```typescript
import {IClone} from '@jscpd/core';
import {jscpd} from 'jscpd';

const clones: Promise<IClone[]> = jscpd(process.argv);
```

`jscpd` async/await API
```typescript
import {IClone} from '@jscpd/core';
import {jscpd} from 'jscpd';
(async () => {
  const clones: IClone[] = await jscpd(['', '', __dirname + '/../fixtures', '-m', 'weak', '--silent']);
  console.log(clones);
})();

```

`detectClones` API
```typescript
import {detectClones} from "jscpd";

(async () => {
  const clones = await detectClones({
    path: [
      __dirname + '/../fixtures'
    ],
    silent: true
  });
  console.log(clones);
})()
```

`detectClones` with persist store
```typescript
import {detectClones} from "jscpd";
import {IMapFrame, MemoryStore} from "@jscpd/core";

(async () => {
  const store = new MemoryStore<IMapFrame>();

  await detectClones({
    path: [
      __dirname + '/../fixtures'
    ],
  }, store);

  await detectClones({
    path: [
      __dirname + '/../fixtures'
    ],
    silent: true
  }, store);
})()
```

如需对检测流程进行深度定制，你可以基于 `@jscpd/core`、`@jscpd/finder` 和 `@jscpd/tokenizer` 构建自己的工具。

## Start contribution

 - Fork the repo [kucherenko/jscpd](https://github.com/kucherenko/jscpd/)
 - Clone forked version (`git clone https://github.com/{your-id}/jscpd`)
 - Install dependencies (`pnpm install`)
 - Run the project in dev mode: `pnpm dev` (watch changes and rebuild the packages)
 - Add your changes
 - Add tests and check it with `pnpm test`
 - Build your project `pnpm build`
 - Create PR

## Who uses jscpd
 - [GitHub Super Linter](https://github.com/github/super-linter)：结合多种 Linter 的 GitHub Action 组合工具
 - [Code-Inspector](https://www.code-inspector.com/)：代码分析与技术债务管理服务
 - [Mega-Linter](https://nvuillam.github.io/mega-linter/)：100% 开源的 CI（GitHub Action 及其他 CI 工具）或本地运行的 Linter 聚合器
 - [Codacy](http://docs.codacy.com/getting-started/supported-languages-and-tools/)：自动分析源代码并实时识别问题，帮助你更高效地开发软件，减少后续隐患
 - [Natural](https://github.com/NaturalNode/natural)：面向 Node.js 的通用自然语言处理库，提供广泛的语言处理功能
 - [OpenClaw](https://github.com/openclaw/openclaw)：运行于你自有设备上的个人 AI 助手，支持 20+ 消息渠道及多平台配套应用


## Backers

感谢所有支持者！🙏 [[成为支持者](https://opencollective.com/jscpd#backer)]

<a href="https://opencollective.com/jscpd#backers" target="_blank"><img src="https://opencollective.com/jscpd/backers.svg?width=890"></a>
## Sponsors

通过成为赞助商来支持本项目。你的 Logo 将显示在此处并附带网站链接。 [[成为赞助商](https://opencollective.com/jscpd#sponsor)]

<a href="https://opencollective.com/jscpd/sponsor/0/website" target="_blank"><img src="https://opencollective.com/jscpd/sponsor/0/avatar.svg"></a>
<a href="https://opencollective.com/jscpd/sponsor/1/website" target="_blank"><img src="https://opencollective.com/jscpd/sponsor/1/avatar.svg"></a>
<a href="https://opencollective.com/jscpd/sponsor/2/website" target="_blank"><img src="https://opencollective.com/jscpd/sponsor/2/avatar.svg"></a>
<a href="https://opencollective.com/jscpd/sponsor/3/website" target="_blank"><img src="https://opencollective.com/jscpd/sponsor/3/avatar.svg"></a>
<a href="https://opencollective.com/jscpd/sponsor/4/website" target="_blank"><img src="https://opencollective.com/jscpd/sponsor/4/avatar.svg"></a>
<a href="https://opencollective.com/jscpd/sponsor/5/website" target="_blank"><img src="https://opencollective.com/jscpd/sponsor/5/avatar.svg"></a>
<a href="https://opencollective.com/jscpd/sponsor/6/website" target="_blank"><img src="https://opencollective.com/jscpd/sponsor/6/avatar.svg"></a>
<a href="https://opencollective.com/jscpd/sponsor/7/website" target="_blank"><img src="https://opencollective.com/jscpd/sponsor/7/avatar.svg"></a>
<a href="https://opencollective.com/jscpd/sponsor/8/website" target="_blank"><img src="https://opencollective.com/jscpd/sponsor/8/avatar.svg"></a>
<a href="https://opencollective.com/jscpd/sponsor/9/website" target="_blank"><img src="https://opencollective.com/jscpd/sponsor/9/avatar.svg"></a>

![ga tracker](https://www.google-analytics.com/collect?v=1&a=257770996&t=pageview&dl=https%3A%2F%2Fgithub.com%2Fkucherenko%2Fjscpd&ul=en-us&de=UTF-8&cid=978224512.1377738459&tid=UA-730549-17&z=887657232 "ga tracker")

## Star History

[![Star History Chart](https://api.star-history.com/chart?repos=kucherenko/jscpd&type=date&legend=top-left)](https://www.star-history.com/?repos=kucherenko%2Fjscpd&type=date&legend=top-left)

## License

[MIT](LICENSE) © Andrey Kucherenko
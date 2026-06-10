# Android 逆向工程与 API 提取 —— Claude Code 技能

[![License: Apache-2.0](https://img.shields.io/badge/License-Apache--2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0) [![GitHub stars](https://img.shields.io/github/stars/SimoneAvogadro/android-reverse-engineering-skill?style=social)](https://github.com/SimoneAvogadro/android-reverse-engineering-skill/stargazers) [![GitHub last commit](https://img.shields.io/github/last-commit/SimoneAvogadro/android-reverse-engineering-skill)](https://github.com/SimoneAvogadro/android-reverse-engineering-skill/commits/master)

一款用于 Claude Code 的技能，可反编译 Android APK/XAPK/JAR/AAR 文件并**提取应用使用的 HTTP API**（包括 Retrofit 端点、OkHttp 调用、硬编码 URL、认证模式等），让你无需原始源代码即可记录并复现这些接口。

> **Windows / PowerShell 支持（实验性）**：与 bash 脚本并列的 `*.ps1` 脚本是近期社区贡献的内容，目前仍在稳定化中。如遇任何问题，请在**本仓库**提交 Issue（请勿在贡献者的上游分叉仓库提交）：PowerShell 脚本由 [@SimoneAvogadro](https://github.com/SimoneAvogadro) 在此维护。

## 目录

- [功能说明](#what-it-does)
- [环境要求](#requirements)
- [安装步骤](#installation)
- [使用方法](#usage)
- [仓库结构](#repository-structure)
- [参考资料](#references)
- [鸣谢](#acknowledgments)
- [免责声明](#disclaimer)
- [开源协议](#license)

## 功能说明

| 功能 | 说明 |
|------------|-------------|
| **反编译** | 使用 jadx 和 Fernflower/Vineflower（单引擎或并排对比）对 APK、XAPK、JAR 及 AAR 文件进行反编译 |
| **提取 API** | 获取 Retrofit 端点、OkHttp 调用、硬编码 URL、认证头与令牌（token） |
| **追踪调用链路** | 从 Activity/Fragment 经 ViewModel 和 Repository 一路追溯至底层 HTTP 请求 |
| **分析结构** | 解析 AndroidManifest、包结构及架构模式 |
| **处理混淆** | 提供应对 ProGuard/R8 输出结果的导航与解析策略 |

## 环境要求

**必需：**

- Java JDK 17+
- [jadx](https://github.com/skylot/jadx)（命令行工具）

**可选（推荐安装）：**

- [Vineflower](https://github.com/Vineflower/vineflower) 或 [Fernflower](https://github.com/JetBrains/fernflower) —— 对复杂 Java 代码的反编译效果更好
- [dex2jar](https://github.com/ThexXTURBOXx/dex2jar) —— 用于在 APK/DEX 文件上使用 Fernflower

详细安装说明请参阅 `plugins/android-reverse-engineering/skills/android-reverse-engineering/references/setup-guide.md`。

## 安装步骤

### 从 GitHub 安装（推荐）

在 Claude Code 中执行：

```text
/plugin marketplace add SimoneAvogadro/android-reverse-engineering-skill
/plugin install android-reverse-engineering@android-reverse-engineering-skill
```

该技能将在所有后续会话中永久可用。

### 从本地克隆安装

```bash
git clone https://github.com/SimoneAvogadro/android-reverse-engineering-skill.git
```

然后在 Claude Code 中：

```text
/plugin marketplace add /path/to/android-reverse-engineering-skill
/plugin install android-reverse-engineering@android-reverse-engineering-skill
```

## 使用方法

### 斜杠命令

```text
/decompile path/to/app.apk
```

此命令将执行完整工作流：依赖检查、反编译以及初始结构分析。

### 自然语言指令

当使用以下类型的短语时，该技能将被激活：

- “反编译这个 APK”
- “逆向分析这款 Android 应用”
- “提取此应用的 API 端点”
- “追踪从 LoginActivity 开始的调用链路”
- “分析这个 AAR 库”

### 手动执行脚本

这些脚本也可独立运行：

```bash
# Check dependencies
bash plugins/android-reverse-engineering/skills/android-reverse-engineering/scripts/check-deps.sh

# Install a missing dependency (auto-detects OS and package manager)
bash plugins/android-reverse-engineering/skills/android-reverse-engineering/scripts/install-dep.sh jadx
bash plugins/android-reverse-engineering/skills/android-reverse-engineering/scripts/install-dep.sh vineflower

# Decompile APK with jadx (default)
bash plugins/android-reverse-engineering/skills/android-reverse-engineering/scripts/decompile.sh app.apk

# Decompile XAPK (auto-extracts and decompiles each APK inside)
bash plugins/android-reverse-engineering/skills/android-reverse-engineering/scripts/decompile.sh app-bundle.xapk

# Decompile with Fernflower
bash plugins/android-reverse-engineering/skills/android-reverse-engineering/scripts/decompile.sh --engine fernflower library.jar

# Run both engines and compare
bash plugins/android-reverse-engineering/skills/android-reverse-engineering/scripts/decompile.sh --engine both --deobf app.apk

# Find API calls
bash plugins/android-reverse-engineering/skills/android-reverse-engineering/scripts/find-api-calls.sh output/sources/
bash plugins/android-reverse-engineering/skills/android-reverse-engineering/scripts/find-api-calls.sh output/sources/ --retrofit
bash plugins/android-reverse-engineering/skills/android-reverse-engineering/scripts/find-api-calls.sh output/sources/ --urls
```

## 仓库结构

```text
android-reverse-engineering-skill/
├── .claude-plugin/
│   └── marketplace.json                    # Marketplace catalog
├── plugins/
│   └── android-reverse-engineering/
│       ├── .claude-plugin/
│       │   └── plugin.json                 # Plugin manifest
│       ├── skills/
│       │   └── android-reverse-engineering/
│       │       ├── SKILL.md                # Core workflow (5 phases)
│       │       ├── references/
│       │       │   ├── setup-guide.md
│       │       │   ├── jadx-usage.md
│       │       │   ├── fernflower-usage.md
│       │       │   ├── api-extraction-patterns.md
│       │       │   └── call-flow-analysis.md
│       │       └── scripts/
│       │           ├── check-deps.sh       # Bash
│       │           ├── check-deps.ps1      # PowerShell
│       │           ├── install-dep.sh
│       │           ├── install-dep.ps1
│       │           ├── decompile.sh
│       │           ├── decompile.ps1
│       │           ├── find-api-calls.sh
│       │           └── find-api-calls.ps1
│       └── commands/
│           └── decompile.md                # /decompile slash command
├── LICENSE
└── README.md
```

## 参考资料

- [jadx —— Dex 转 Java 反编译器](https://github.com/skylot/jadx)
- [Fernflower —— JetBrains 分析型反编译器](https://github.com/JetBrains/fernflower)
- [Vineflower —— Fernflower 社区分叉版](https://github.com/Vineflower/vineflower)
- [dex2jar —— DEX 转 JAR 转换器](https://github.com/ThexXTURBOXx/dex2jar)
- [apktool —— Android 资源解析器](https://apktool.org/)

## 鸣谢

感谢为完善此技能做出贡献的开发者：

- [@philjn](https://github.com/philjn) —— 提供原生 Windows / PowerShell 支持（`check-deps.ps1`、`install-dep.ps1`、`decompile.ps1`、`find-api-calls.ps1`）以及 `decompile.sh` 中的拆分/捆绑 APK 检测功能 (#8)
- [@txhno](https://github.com/txhno) —— 迁移至持续维护的 [`ThexXTURBOXx/dex2jar`](https://github.com/ThexXTURBOXx/dex2jar) 分叉仓库 (#12)
- [@muqiao215](https://github.com/muqiao215) —— 实现反编译部分成功处理、Fernflower 超时保护机制及中间产物目录管理 (#10)
- [@kevinaimonster](https://github.com/kevinaimonster) —— 中文本地化（`SKILL.md` 发现关键词）(#4)

## 免责声明

本插件仅提供用于**合法目的**，包括但不限于：

- 安全研究与授权渗透测试
- 符合适用法律允许的互操作性分析（例如欧盟指令 2009/24/EC、美国 DMCA §1201(f)）
- 恶意软件分析与事件响应
- 教学用途与 CTF 竞赛

**你需自行确保**对该工具的使用符合所有适用的法律、法规及服务条款。未经授权对你不拥有或无权分析的软件进行逆向工程，可能违反你所在司法管辖区的知识产权法及计算机欺诈相关法规。

作者不对任何滥用本工具的行为承担任何责任。

## 开源协议

Apache 2.0 —— 详见 [LICENSE](LICENSE)
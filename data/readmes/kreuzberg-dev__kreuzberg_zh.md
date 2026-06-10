# Kreuzberg

<div align="center" style="display: flex; flex-wrap: wrap; gap: 8px; justify-content: center; margin: 20px 0;">
  <!-- Built with -->
  <a href="https://github.com/kreuzberg-dev/alef">
    <img src="https://img.shields.io/badge/built%20with-alef%20%D7%90-007ec6" alt="Built with alef">
  </a>
  <!-- Language Bindings -->
  <a href="https://crates.io/crates/kreuzberg">
    <img src="https://img.shields.io/crates/v/kreuzberg?label=Rust&color=007ec6" alt="Rust">
  </a>
  <a href="https://hex.pm/packages/kreuzberg">
    <img src="https://img.shields.io/hexpm/v/kreuzberg?label=Elixir&color=007ec6" alt="Elixir">
  </a>
  <a href="https://pypi.org/project/kreuzberg/">
    <img src="https://img.shields.io/pypi/v/kreuzberg?label=Python&color=007ec6" alt="Python">
  </a>
  <a href="https://www.npmjs.com/package/@kreuzberg/node">
    <img src="https://img.shields.io/npm/v/@kreuzberg/node?label=Node.js&color=007ec6" alt="Node.js">
  </a>
  <a href="https://www.npmjs.com/package/@kreuzberg/wasm">
    <img src="https://img.shields.io/npm/v/@kreuzberg/wasm?label=WASM&color=007ec6" alt="WASM">
  </a>

  <a href="https://central.sonatype.com/artifact/dev.kreuzberg/kreuzberg">
    <img src="https://img.shields.io/maven-central/v/dev.kreuzberg/kreuzberg?label=Java&color=007ec6" alt="Java">
  </a>
  <a href="https://github.com/kreuzberg-dev/kreuzberg/releases">
    <img src="https://img.shields.io/github/v/tag/kreuzberg-dev/kreuzberg?label=Go&color=007ec6&filter=v5*" alt="Go">
  </a>
  <a href="https://www.nuget.org/packages/Kreuzberg/">
    <img src="https://img.shields.io/nuget/v/Kreuzberg?label=C%23&color=007ec6" alt="C#">
  </a>
  <a href="https://packagist.org/packages/kreuzberg/kreuzberg">
    <img src="https://img.shields.io/packagist/v/kreuzberg/kreuzberg?label=PHP&color=007ec6" alt="PHP">
  </a>
  <a href="https://rubygems.org/gems/kreuzberg">
    <img src="https://img.shields.io/gem/v/kreuzberg?label=Ruby&color=007ec6" alt="Ruby">
  </a>
  <a href="https://kreuzberg-dev.r-universe.dev/kreuzberg">
    <img src="https://img.shields.io/badge/R-kreuzberg-007ec6" alt="R">
  </a>
  <a href="https://github.com/kreuzberg-dev/kreuzberg/pkgs/container/kreuzberg">
    <img src="https://img.shields.io/badge/Docker-007ec6?logo=docker&logoColor=white" alt="Docker">
  </a>
  <a href="https://github.com/kreuzberg-dev/kreuzberg/releases">
    <img src="https://img.shields.io/badge/C-FFI-007ec6" alt="C">
  </a>
  <a href="https://artifacthub.io/packages/search?repo=kreuzberg">
    <img src="https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/kreuzberg" alt="Artifact Hub">
  </a>

  <!-- Project Info -->
  <a href="https://github.com/kreuzberg-dev/kreuzberg/blob/main/LICENSE">
    <img src="https://img.shields.io/badge/License-Elastic--2.0-blue.svg" alt="License">
  </a>
  <a href="https://docs.kreuzberg.dev">
    <img src="https://img.shields.io/badge/docs-kreuzberg.dev-007ec6" alt="Documentation">
  </a>
  <a href="https://docs.kreuzberg.dev/demo.html">
    <img src="https://img.shields.io/badge/%E2%96%B6%EF%B8%8F_Live_Demo-007ec6" alt="Live Demo">
  </a>
  <a href="https://huggingface.co/Kreuzberg">
    <img src="https://img.shields.io/badge/%F0%9F%A4%97_Hugging_Face-007ec6" alt="Hugging Face">
  </a>
</div>

<img width="3384" height="573" alt="Linkedin- Banner" src="https://github.com/user-attachments/assets/1b6c6ad7-3b6d-4171-b1c9-f2026cc9deb8" />

<div align="center" style="margin-top: 20px;">
  <a href="https://discord.gg/xt9WY3GnKR">
      <img height="22" src="https://img.shields.io/badge/Discord-Join%20our%20community-7289da?logo=discord&logoColor=white" alt="Discord">
  </a>
</div>

以原生速度从 91+ 种文件格式和 306 种编程语言中提取文本、元数据与代码智能，无需依赖 GPU。

## 核心功能

- **代码智能（Code Intelligence）** – 通过 tree-sitter 从 [306 种编程语言](https://docs.tree-sitter-language-pack.kreuzberg.dev) 提取函数、类、导入语句、符号及文档字符串。结果输出至 `ExtractionResult.code_intelligence`，并支持语义分块（semantic chunking）
- **可扩展架构** – 提供插件系统，支持自定义 OCR 后端、验证器、后处理器、文档提取器和渲染器
- **多语言绑定（Polyglot）** – 原生支持 Rust、Python、TypeScript/Node.js、Ruby、Go、Java、Kotlin、C#、PHP、Elixir、R、Dart、Swift、Zig 和 C
- **90+ 文件格式** – 涵盖 PDF、Office 文档、图像、HTML/XML、电子邮件、归档文件及学术格式，共 8 大类别
- **大模型智能（LLM Intelligence）** – 支持 VLM OCR（GPT-4o、Claude、Gemini、Ollama）、带模式约束的结构化 JSON 提取，以及通过 [liter-llm](https://github.com/kreuzberg-dev/liter-llm) 接入的 143 家 LLM 提供商托管嵌入向量（含本地引擎：Ollama、LM Studio、vLLM、llama.cpp）
- **OCR 支持** – 集成 Tesseract（全语言绑定，含浏览器端 WASM）、PaddleOCR（全原生绑定）、EasyOCR（Python），以及 VLM OCR（143 家视觉模型提供商及本地引擎），可通过插件 API 扩展
- **高性能** – 基于 Rust 核心，采用纯 Rust 实现的 PDF 解析器、SIMD 优化与全并行处理
- **灵活部署** – 可作为库、CLI 工具、REST API 服务器或 MCP 服务器使用
- **TOON Wire Format（TOON 传输格式）** – 专为 LLM/RAG 流水线设计的 Token 高效序列化格式，相比 JSON 减少约 30%-50% 的 Token 消耗
- **GFM 级输出质量** – 基于 Comrak 渲染，完美支持代码块、表格节点、括号转义及跨格式一致性（Markdown、HTML、Djot、纯文本）
- **HTML 直通处理（HTML Passthrough）** – HTML 转 Markdown 转换直接使用 `html-to-markdown` 输出，避免有损的中间往返处理
- **内存高效** – 采用流式解析器处理数 GB 级别的大文件

**[完整文档](https://kreuzberg.dev/) | [在线演示](https://docs.kreuzberg.dev/demo.html) | [安装指南](#installation)**

## 安装指南

每种语言绑定均提供包含示例与最佳实践的完整文档。请选择你的平台开始使用：

**脚本语言：**

- **[Python](https://github.com/kreuzberg-dev/kreuzberg/tree/main/packages/python)** – PyPI 包，支持异步/同步 API 及多种 OCR 后端（Tesseract、PaddleOCR、EasyOCR）
- **[Ruby](https://github.com/kreuzberg-dev/kreuzberg/tree/main/packages/ruby)** – RubyGems 包，符合 Ruby 习惯的 API 与原生绑定
- **[PHP](https://github.com/kreuzberg-dev/kreuzberg/tree/main/packages/php)** – Composer 包，现代 PHP 8.2+ 支持，类型安全 API，异步提取
- **[Elixir](https://github.com/kreuzberg-dev/kreuzberg/tree/main/packages/elixir)** – Hex 包，OTP 集成，并发处理
- **[R](https://github.com/kreuzberg-dev/kreuzberg/tree/main/packages/r)** – r-universe 包，符合 R 习惯的 API，extendr 绑定
- **[Dart / Flutter](https://github.com/kreuzberg-dev/kreuzberg/tree/main/packages/dart)** – pub.dev 包，flutter_rust_bridge 运行时，原生支持 macOS/iOS/Android/Linux/Windows

**JavaScript/TypeScript：**

- **[@kreuzberg/node](https://github.com/kreuzberg-dev/kreuzberg/tree/main/crates/kreuzberg-node)** – Node.js/Bun 的 NAPI-RS 原生绑定，性能最优
- **[@kreuzberg/wasm](https://github.com/kreuzberg-dev/kreuzberg/tree/main/packages/typescript)** – 适用于浏览器/Deno/Cloudflare Workers 的 WebAssembly，全面支持格式与 OCR（PDF、Excel、归档文件、全 Office 格式、通过 WASI 构建的真实 Tesseract）——仅排除 ORT 依赖功能（paddle-ocr、布局检测、嵌入向量、自动旋转）及服务器模式（api/mcp/cli）

**编译型语言：**

- **[Go](https://github.com/kreuzberg-dev/kreuzberg/tree/main/packages/go/v5)** – Go 模块，FFI 绑定，上下文感知异步
- **[Java](https://github.com/kreuzberg-dev/kreuzberg/tree/main/packages/java)** – Maven Central，Foreign Function & Memory API
- **[Kotlin](https://github.com/kreuzberg-dev/kreuzberg/tree/main/packages/kotlin)** – Maven Central，Kotlin/JVM 支持符合习惯的数据类、密封枚举及基于协程的异步
- **[C#](https://github.com/kreuzberg-dev/kreuzberg/tree/main/packages/csharp)** – NuGet 包，.NET 6.0+，完整 async/await 支持
- **[Swift](https://github.com/kreuzberg-dev/kreuzberg/tree/main/packages/swift)** – Swift Package Manager，macOS 13+/iOS 16+，原生 Swift 类型与 async/await

**底层/原生支持：**

- **[Rust](https://github.com/kreuzberg-dev/kreuzberg/tree/main/crates/kreuzberg)** – 核心库，灵活的特性标志（feature flags），零拷贝 API
- **[Zig](https://github.com/kreuzberg-dev/kreuzberg/tree/main/packages/zig)** – `zig fetch` + `build.zig.zon`，符合习惯的错误集、可选类型及基于切片（slice）的内存管理
- **[C (FFI)](https://github.com/kreuzberg-dev/kreuzberg/tree/main/crates/kreuzberg-ffi)** – C 头文件 + 共享库，支持 pkg-config/CMake，跨平台

**容器化部署：**

- **[Docker](https://docs.kreuzberg.dev/guides/docker/)** – 官方镜像，提供 API、CLI 与 MCP 服务器模式（Core：约 1.0-1.3GB，Full：约 1.0-1.3GB，含 OCR + 遗留格式支持）

**命令行工具：**

- **[CLI](https://docs.kreuzberg.dev/cli/usage/)** – 跨平台二进制文件，批量处理，MCP 服务器模式

> 所有语言绑定均提供 x86_64 和 aarch64 架构的预编译二进制文件，适用于 Linux 和 macOS。

## 平台支持

各语言绑定的完整架构覆盖情况：

| Language | Linux x86_64 | Linux aarch64 | macOS ARM64 | Windows x64 |
| -------- | :----------: | :-----------: | :---------: | :---------: |
| Python   |      ✅      |      ✅       |     ✅      |     ✅      |
| Node.js  |      ✅      |      ✅       |     ✅      |     ✅      |
| WASM     |      ✅      |      ✅       |     ✅      |     ✅      |
| Ruby     |      ✅      |      ✅       |     ✅      |      -      |
| R        |      ✅      |      ✅       |     ✅      |     ✅      |
| Elixir   |      ✅      |      ✅       |     ✅      |     ✅      |
| Go       |      ✅      |      ✅       |     ✅      |     ✅      |
| Java     |      ✅      |      ✅       |     ✅      |     ✅      |
| Kotlin   |      ✅      |      ✅       |     ✅      |     ✅      |
| C#       |      ✅      |      ✅       |     ✅      |     ✅      |
| PHP      |      ✅      |      ✅       |     ✅      |     ✅      |
| Swift    |      -       |      -        |     ✅      |      -      |
| Dart     |      ✅      |      ✅       |     ✅      |     ✅      |
| Zig      |      ✅      |      ✅       |     ✅      |     ✅      |
| Rust     |      ✅      |      ✅       |     ✅      |     ✅      |
| C (FFI)  |      ✅      |      ✅       |     ✅      |     ✅      |
| CLI      |      ✅      |      ✅       |     ✅      |     ✅      |
| Docker   |      ✅      |      ✅       |     ✅      |      -      |

**注意**：✅ 表示提供预编译二进制文件，可即时安装。WASM 可在任何支持 WebAssembly 的环境中运行（浏览器、Deno、Bun、Cloudflare Workers）。所有平台均通过 CI 测试。macOS 仅支持 Apple Silicon 架构。

### 移动端（iOS、Android）

| Target                                            | ORT-dependent features* |
| ------------------------------------------------- | :---------------------: |
| iOS (`aarch64-apple-ios`, `aarch64-apple-ios-sim`) |           ✅            |
| Android arm64 (`aarch64-linux-android`)            |           ✅            |
| Android x86_64 emulator (`x86_64-linux-android`)   |           ❌            |

*依赖 ORT 的功能：PaddleOCR、布局检测、嵌入向量（embeddings）、自动旋转。
所有非 ORT 功能（Tesseract OCR、全文档格式、分块、语言检测、关键词提取、tree-sitter 代码智能、API/MCP、LLM）在全部四种移动端目标平台上均可用。

`x86_64-linux-android` 模拟器三元组缺少上游预构建版本；kreuzberg 的 `kreuzberg` crate 暴露了一个名为 `android-target` 的聚合特性（aggregate feature），其选择了与 WASM 相同的无 ORT 功能集。`kreuzberg-ffi` 和 `kreuzberg-dart` crate 会通过目标条件依赖自动为该模拟器选择此聚合特性——主机设备和 arm64 手机将自动获得完整功能支持。

### 浏览器/边缘计算（WebAssembly）

WASM 排除了与 Android x86_64 模拟器相同的 ORT 依赖功能集。共享的无 ORT 基础位于核心 crate 的 `no-ort-target` 特性之后；`wasm-target` 和 `android-target` 均组合使用了该特性。

### 嵌入向量支持（可选）

要使用嵌入向量功能：

1. **安装 ONNX Runtime 1.24+**：
   - Linux：从 [ONNX Runtime releases](https://github.com/microsoft/onnxruntime/releases) 下载（Debian 软件包可能版本较旧）
   - MacOS：`brew install onnxruntime`
   - Windows：从 [ONNX Runtime releases](https://github.com/microsoft/onnxruntime/releases) 下载

2. 在代码中使用嵌入向量功能——详见[嵌入向量指南](https://docs.kreuzberg.dev/features/#embeddings)

**注意**：Kreuzberg 的嵌入向量功能需要 ONNX Runtime 1.24+。其他所有 Kreuzberg 功能均可在无 ONNX Runtime 的环境下运行。

## 支持的文件格式

涵盖 8 大类别的 90+ 种文件格式，内置智能格式检测与全面的元数据提取功能。

### 办公文档

| Category            | Formats                                                                                          | Capabilities                                       |
| ------------------- | ------------------------------------------------------------------------------------------------ | -------------------------------------------------- |
| **文字处理**        | `.docx`, `.docm`, `.dotx`, `.dotm`, `.dot`, `.odt`, `.pages`                                     | 全文、表格、列表、图像、元数据、样式               |
| **电子表格**        | `.xlsx`, `.xlsm`, `.xlsb`, `.xls`, `.xla`, `.xlam`, `.xltm`, `.xltx`, `.xlt`, `.ods`, `.numbers` | 工作表数据、公式、单元格元数据、图表               |
| **演示文稿**        | `.pptx`, `.pptm`, `.ppsx`, `.potx`, `.potm`, `.pot`, `.key`                                      | 幻灯片、演讲者备注、图像、元数据                   |
| **PDF**             | `.pdf`                                                                                           | 文本、表格、图像、元数据、OCR 支持                 |
| **电子书**          | `.epub`, `.fb2`                                                                                  | 章节、元数据、嵌入资源                             |
| **数据库**          | `.dbf`                                                                                           | 表数据提取、字段类型支持                           |
| **韩文文档**        | `.hwp`, `.hwpx`                                                                                  | 韩国标准文档格式，文本提取                         |

### 图像（支持 OCR）

| Category     | Formats                                                                          | Features                                                     |
| ------------ | -------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| **光栅图像**   | `.png`, `.jpg`, `.jpeg`, `.gif`, `.webp`, `.bmp`, `.tiff`, `.tif`                | OCR、表格检测、EXIF 元数据、尺寸、色彩空间                   |
| **高级格式**     | `.jp2`, `.jpx`, `.jpm`, `.mj2`, `.jbig2`, `.jb2`, `.pnm`, `.pbm`, `.pgm`, `.ppm` | 纯 Rust 解码器（JPEG 2000、JBIG2）、OCR、表格检测            |
| **矢量图形**     | `.svg`                                                                           | DOM 解析、嵌入文本、图形元数据                               |

### 网页与数据

| Category            | Formats                                                             | Features                                                          |
| ------------------- | ------------------------------------------------------------------- | ----------------------------------------------------------------- |
| **标记语言**          | `.html`, `.htm`, `.xhtml`, `.xml`, `.svg`                           | DOM 解析、元数据（Open Graph、Twitter Card）、链接提取             |
| **结构化数据**        | `.json`, `.yaml`, `.yml`, `.toml`, `.csv`, `.tsv`                   | 模式检测、嵌套结构、数据验证                                       |
| **文本与 Markdown**   | `.txt`, `.md`, `.markdown`, `.djot`, `.mdx`, `.rst`, `.org`, `.rtf` | CommonMark、GFM、Djot、MDX、reStructuredText、Org Mode、富文本格式 |

### 电子邮件与归档文件

| Category     | Formats                              | Features                                                |
| ------------ | ------------------------------------ | ------------------------------------------------------- |
| **电子邮件**    | `.eml`, `.msg`                       | 邮件头、正文（HTML/纯文本）、附件、UTF-16 支持          |
| **归档文件**      | `.zip`, `.tar`, `.tgz`, `.gz`, `.7z` | 递归提取、嵌套归档文件、元数据                          |

### 学术与科学文献

| Category          | Formats                                               | Features                                                    |
| ----------------- | ----------------------------------------------------- | ----------------------------------------------------------- |
| **参考文献**        | `.bib`, `.ris`, `.nbib`, `.enw`, `.csl`               | BibTeX/BibLaTeX、RIS、PubMed/MEDLINE、EndNote XML、CSL JSON |
| **学术排版/科学**    | `.tex`, `.latex`, `.typ`, `.typst`, `.jats`, `.ipynb` | LaTeX、Typst、JATS 期刊文章、Jupyter Notebook               |
| **出版格式**        | `.fb2`, `.docbook`, `.dbk`, `.opml`                   | FictionBook、DocBook XML、OPML 大纲                         |
| **文档系统**        | `.pod`, `.mdoc`, `.troff`                             | Perl POD、手册页（man pages）、troff                        |

**[完整格式参考 →](https://docs.kreuzberg.dev/reference/formats/)**

### 代码智能（支持 306 种语言）

| Feature                    | Description                                                   |
| -------------------------- | ------------------------------------------------------------- |
| **结构提取**               | 函数、类、方法、结构体、接口、枚举                            |
| **导入/导出分析**          | 模块依赖、重导出（re-exports）、通配符导入                    |
| **符号提取**               | 变量、常量、类型别名、属性                                    |
| **文档字符串解析**         | Google、NumPy、Sphinx、JSDoc、RustDoc 等 10+ 种标准格式       |
| **诊断信息（Diagnostics）**| 包含行列位置的语法/词法错误                                   |
| **语法感知分块**           | 按语义边界分割代码，而非任意字节偏移量                        |

由 [tree-sitter-language-pack](https://github.com/kreuzberg-dev/tree-sitter-language-pack) 驱动，支持动态下载语法包。完整语言列表请参阅 [TSLP 文档](https://docs.tree-sitter-language-pack.kreuzberg.dev)。

## 核心功能详解

<details>
<summary><strong>支持表格提取的 OCR</strong></summary>

集成多种 OCR 后端（Tesseract、EasyOCR、PaddleOCR），内置智能表格检测与重建算法。可从扫描件和图像中提取结构化数据，并支持配置准确率阈值。

**[OCR 后端文档 →](https://docs.kreuzberg.dev/guides/ocr/)**

</details>

<details>
<summary><strong>批量处理</strong></summary>

通过可配置的并发度并行处理多个文档。内置自动资源管理，优化大规模文档处理的吞吐量。

**[批量处理指南 →](https://docs.kreuzberg.dev/features/#batch-processing)**

</details>

<details>
<summary><strong>受密码保护的 PDF</strong></summary>

支持单密码或多密码尝试的加密 PDF 处理。兼容 RC4 和 AES 加密，并提供自动降级策略。

**[PDF 配置指南 →](https://docs.kreuzberg.dev/guides/configuration/)**

</details>

<details>
<summary><strong>语言检测</strong></summary>

使用 fast-langdetect 对提取的文本进行自动语言识别。支持配置置信度阈值并访问各语言的统计信息。

**[语言检测指南 →](https://docs.kreuzberg.dev/features/#language-detection)**

</details>

<details>
<summary><strong>元数据提取</strong></summary>

从所有支持的格式中提取全面的元数据：作者、标题、创建日期、页数、EXIF 数据及格式专属属性。

**[元数据指南 →](https://docs.kreuzberg.dev/reference/types/#metadata)**

</details>

## AI 编程助手

Kreuzberg 内置了 [Agent Skill（智能体技能）](https://agentskills.io)，用于指导 AI 编程助手正确使用该库。它兼容 Claude Code、Codex、Gemini CLI、Cursor、VS Code、Amp、Goose、Roo Code，以及任何支持 Agent Skills 标准的工具。

使用 [Vercel Skills CLI](https://github.com/vercel-labs/skills) 将技能安装到任意项目中：

```bash
npx skills add kreuzberg-dev/kreuzberg
```

该技能文件位于 [`skills/kreuzberg/SKILL.md`](skills/kreuzberg/SKILL.md)，安装后受支持的 AI 编程工具将自动发现它。

## 文档资源

- **[安装指南](https://docs.kreuzberg.dev/getting-started/installation/)** – 环境配置与依赖项
- **[用户指南](https://docs.kreuzberg.dev/guides/extraction/)** – 全面的使用教程
- **[API 参考](https://docs.kreuzberg.dev/reference/api-python/)** – 完整 API 文档
- **[格式支持](https://docs.kreuzberg.dev/reference/formats/)** – 支持的文件格式列表
- **[OCR 后端](https://docs.kreuzberg.dev/guides/ocr/)** – OCR 引擎配置指南
- **[CLI 使用指南](https://docs.kreuzberg.dev/cli/usage/)** – 命令行操作说明
- **[迁移指南](https://docs.kreuzberg.dev/migration/from-unstructured/)** – 从其他库升级至 Kreuzberg

## 参与贡献

欢迎提交 PR！详细规范请参阅 [CONTRIBUTING.md](CONTRIBUTING.md)。

## Kreuzberg.dev 生态组件

- [Kreuzberg Cloud](https://github.com/kreuzberg-dev/kreuzberg-cloud) — 托管式提取 API，提供 SDK、仪表盘与可观测性工具。
- [kreuzcrawl](https://github.com/kreuzberg-dev/kreuzcrawl) — 网页爬虫与数据采集，支持 HTML→Markdown 转换及无头 Chrome 降级方案。
- [html-to-markdown](https://github.com/kreuzberg-dev/html-to-markdown) — 快速、无损的 HTML→Markdown 引擎。
- [liter-llm](https://github.com/kreuzberg-dev/liter-llm) — 通用 LLM API 客户端，原生支持 14 种语言与 143 家提供商。
- [tree-sitter-language-pack](https://github.com/kreuzberg-dev/tree-sitter-language-pack) — tree-sitter 语法包与代码智能基础组件。
- [alef](https://github.com/kreuzberg-dev/alef) — 多语言绑定生成器，负责产出所有语言的绑定代码。
- [Discord](https://discord.gg/xt9WY3GnKR) — 社区交流、路线图更新与官方公告。

## 许可证

Elastic License 2.0 (ELv2) - 详见 [LICENSE](LICENSE)。完整协议文本请参阅 [https://www.elastic.co/licensing/elastic-license](https://www.elastic.co/licensing/elastic-license)。
# IDA Pro MCP

一个简单的 [MCP Server（模型上下文协议服务器）](https://modelcontextprotocol.io/introduction)，用于在 IDA Pro 中实现“氛围逆向”（vibe reversing）。

https://github.com/user-attachments/assets/6ebeaa92-a9db-43fa-b756-eececce2aca0

视频中使用的二进制文件和提示词可在 [mcp-reversing-dataset](https://github.com/mrexodia/mcp-reversing-dataset) 仓库中找到。

## 前置条件 (Prerequisites)

- [Python](https://www.python.org/downloads/)（**3.11 或更高版本**）
  - 使用 `idapyswitch` 切换到最新 Python 版本
- [IDA Pro](https://hex-rays.com/ida-pro)（8.3 或更高，推荐 9），**不支持 IDA Free 免费版**
- 支持的 MCP Client（客户端）（任选其一）
  - [Amazon Q Developer CLI](https://aws.amazon.com/q/developer/)
  - [Augment Code](https://www.augmentcode.com/)
  - [Claude](https://claude.ai/download)
  - [Claude Code](https://www.anthropic.com/code)
  - [Cline](https://cline.bot)
  - [Codex](https://github.com/openai/codex)
  - [Copilot CLI](https://docs.github.com/en/copilot)
  - [Crush](https://github.com/charmbracelet/crush)
  - [Cursor](https://cursor.com)
  - [Gemini CLI](https://google-gemini.github.io/gemini-cli/)
  - [Kilo Code](https://kilo.ai/)
  - [Kiro](https://kiro.dev/)
  - [LM Studio](https://lmstudio.ai/)
  - [Opencode](https://opencode.ai/)
  - [Qodo Gen](https://www.qodo.ai/)
  - [Qwen Coder](https://qwenlm.github.io/qwen-code-docs/)
  - [Roo Code](https://roocode.com)
  - [Trae](https://trae.ai/)
  - [VS Code](https://code.visualstudio.com/)
  - [VS Code Insiders](https://code.visualstudio.com/insiders)
  - [Warp](https://www.warp.dev/)
  - [Windsurf](https://windsurf.com)
  - [Zed](https://zed.dev/)
  - [其他 MCP Client](https://modelcontextprotocol.io/clients#example-clients)：运行 `ida-pro-mcp --config` 获取你的客户端 JSON 配置。

## 安装（Claude Code）

在 Claude Code 中安装无头版 IDA Pro MCP：

```bash
claude plugin marketplace add mrexodia/claude-marketplace
claude plugin install ida-pro-mcp@mrexodia
```

更新到最新版本：

```bash
claude plugin update ida-pro-mcp@mrexodia
```

**注意**：此操作要求全局激活 `idalib` 并已安装 [uv](https://astral.sh/uv)：

```bash
# windows
uv run "C:\Program Files\IDA Professional 9.3\idalib\python\py-activate-idalib.py"
# macos
uv run "/Applications/IDA Professional 9.3.app/Contents/MacOS/idalib/python/py-activate-idalib.py"
```

## 安装（图形界面）

**注意**：MCP 插件已不再推荐使用，未来将被弃用。请改用 `idalib-mcp`。

如果你想从 IDA GUI 手动配置 MCP Server：

```sh
pip uninstall ida-pro-mcp
pip install https://github.com/mrexodia/ida-pro-mcp/archive/refs/heads/main.zip
```

配置 MCP Servers 并安装 IDA 插件：

```
ida-pro-mcp --install
```

**重要**：请确保完全重启 IDA 和你的 MCP Client，以使安装生效。某些客户端（如 Claude）在后台运行，需要从托盘图标中退出。

## 提示词工程 (Prompt Engineering)

LLM（大语言模型）容易产生幻觉，因此你的 prompt（提示词）必须非常具体。对于逆向工程而言，整数与字节之间的转换尤其容易出错。以下是一个最小化示例 prompt，如果你使用其他 prompt 取得了良好效果，欢迎发起讨论或提交 issue：

```md
Your task is to analyze a crackme in IDA Pro. You can use the MCP tools to retrieve information. In general use the following strategy:

- Inspect the decompilation and add comments with your findings
- Rename variables to more sensible names
- Change the variable and argument types if necessary (especially pointer and array types)
- Change function names to be more descriptive
- If more details are necessary, disassemble the function and add comments with your findings
- NEVER convert number bases yourself. Use the `int_convert` MCP tool if needed!
- Do not attempt brute forcing, derive any solutions purely from the disassembly and simple python scripts
- Create a report.md with your findings and steps taken at the end
- When you find a solution, prompt to user for feedback with the password you found
```

此 prompt 仅是初步实验，如果你找到了提升输出质量的方法，请分享！

另一位用户 [@can1357](https://github.com/can1357) 提供的 prompt：

```md
Your task is to create a complete and comprehensive reverse engineering analysis. Reference AGENTS.md to understand the project goals and ensure the analysis serves our purposes.

Use the following systematic methodology:

1. **Decompilation Analysis**
   - Thoroughly inspect the decompiler output
   - Add detailed comments documenting your findings
   - Focus on understanding the actual functionality and purpose of each component (do not rely on old, incorrect comments)

2. **Improve Readability in the Database**
   - Rename variables to sensible, descriptive names
   - Correct variable and argument types where necessary (especially pointers and array types)
   - Update function names to be descriptive of their actual purpose

3. **Deep Dive When Needed**
   - If more details are necessary, examine the disassembly and add comments with findings
   - Document any low-level behaviors that aren't clear from the decompilation alone
   - Use sub-agents to perform detailed analysis

4. **Important Constraints**
   - NEVER convert number bases yourself - use the int_convert MCP tool if needed
   - Use MCP tools to retrieve information as necessary
   - Derive all conclusions from actual analysis, not assumptions

5. **Documentation**
   - Produce comprehensive RE/*.md files with your findings
   - Document the steps taken and methodology used
   - When asked by the user, ensure accuracy over previous analysis file
   - Organize findings in a way that serves the project goals outlined in AGENTS.md or CLAUDE.md
```

直播讨论提示词并展示真实恶意软件分析案例：

[![](https://img.youtube.com/vi/iFxNuk3kxhk/0.jpg)](https://www.youtube.com/watch?v=iFxNuk3kxhk)

## 提升 LLM 准确率的技巧 (Tips for Enhancing LLM Accuracy)

LLM（大语言模型）是强大的工具，但有时可能在复杂的数学计算上表现不佳或产生“幻觉”（编造事实）。请确保告知 LLM 使用 `int_convert` MCP tool，对于某些操作你可能还需要 [math-mcp](https://github.com/EthanHenrickson/math-mcp)。

另外需要注意的是，LLM 在处理混淆代码时效果通常不佳。在尝试让 LLM 解决问题之前，请先浏览二进制文件并花费一些时间（可自动化）移除以下内容：

- String encryption（字符串加密）
- Import hashing（导入哈希）
- Control flow flattening（控制流平坦化）
- Code encryption（代码加密）
- Anti-decompilation tricks（反编译对抗技巧）

你还应使用类似 Lumina 或 FLIRT 的工具来尝试解析所有开源库代码和 C++ STL，这将进一步提高准确率。

## 传输方式与无头 MCP (Transports & Headless MCP)

你可以运行一个 SSE Server 以连接用户界面：

```sh
uv run ida-pro-mcp --transport http://127.0.0.1:8744/sse
```

安装 [`idalib`](https://docs.hex-rays.com/core/idalib/getting-started) 后，你还可以运行无头 MCP Server。你可以从初始二进制文件开始：

```sh
uv run idalib-mcp --host 127.0.0.1 --port 8745 path/to/executable
```

或者不指定二进制文件启动，稍后通过 `idalib_open(...)` / `idalib_close(...)` 打开/关闭任意文件：

```sh
uv run idalib-mcp --host 127.0.0.1 --port 8745
```

对于基于 stdio 的客户端，请使用：

```sh
uv run idalib-mcp --stdio
```

`--stdio` 会将数据库状态保留在该 MCP Server 进程内。对于会启动独立 MCP Server 进程的 stdio 客户端（例如 Codex sub-agents），请改用 `--stdio-shared`：

```sh
uv run idalib-mcp --stdio-shared
```

`--stdio-shared` 会在配置的 host/port 上启动或复用共享的本地 HTTP Supervisor，并将 stdio JSON-RPC 代理到该服务，从而使独立的 stdio MCP 进程能够共享相同的已打开数据库 worker。

_注意_：`idalib` 功能由 [Willi Ballenthin](https://github.com/williballenthin) 贡献。

## 无头 idalib 会话模型 (Headless idalib Session Model)

`idalib-mcp` 是一个 Supervisor（协调器），它在独立的 idalib worker 进程中保持每个打开的数据库。支持不传入 `input_path` 启动；使用 `idalib_open(input_path, ...)` 动态打开数据库，并使用 `idalib_close(session_id)` 关闭它们。这使得单个无头 MCP Server 可以在其生命周期内处理任意文件。

如果请求的 IDB 已在运行插件的 GUI IDA 实例中打开，`idalib-mcp` 将使用该 GUI 实例而不是启动重复的无头 worker。如果该 GUI 实例随后消失，下次路由的请求在可能时会重新在无头 worker 中打开数据库。如果需要保留未保存的 GUI 更改，必须先将其保存。

工具默认作用于绑定到当前 MCP context（上下文）的数据库，或通过显式 `database` 参数指定。

```sh
uv run idalib-mcp --stdio --max-workers 4
```

典型流程：

```python
idalib_open("/path/to/binary_a.exe", session_id="binary_a")
idalib_open("/path/to/library.dll", session_id="library")

decompile("main", database="binary_a")
xrefs_to("ImportantExport", database="library")
```

`database` 接受会话 ID、文件名或输入路径。如果省略，工具将使用绑定到活动上下文的数据库。

使用 `--isolated-contexts` 启用严格的按传输隔离：

```sh
uv run idalib-mcp --isolated-contexts --host 127.0.0.1 --port 8745 path/to/executable
```

### 为何使用 `--isolated-contexts`？ (Why use `--isolated-contexts`?)

当多个 agent（智能体）连接到同一个 `idalib-mcp` Server，且你需要确定性的上下文隔离时使用：

- 防止一个 agent 意外更改另一个 agent 的活跃数据库。
- 明确每个传输上下文的默认数据库。
- 仍可通过传递 `database=...` 或将多个 agent 绑定到同一会话 ID 来实现有意协作。

启用 `--isolated-contexts` 后：

- 每个传输上下文拥有独立的绑定（`/mcp` 使用 `Mcp-Session-Id`，`/sse` 使用 `session`，stdio 使用 `stdio:default`）。
- 除非提供 `database`，否则未绑定的上下文对依赖 IDB 的工具/资源会快速失败。
- `idalib_switch(session_id)` 和 `idalib_open(...)` 仅绑定调用者上下文。

### Streamable HTTP 行为 (Streamable HTTP behavior)

启用 `--isolated-contexts` 后，将启用严格的 Streamable HTTP 会话语义，包括 `Mcp-Session-Id` 验证。

### 上下文工具 (Context tools)

- `idalib_open(input_path, ...)`：在 worker 中打开二进制文件，并将其绑定到活动上下文策略。
- `idalib_switch(session_id)`：将活动上下文策略重新绑定到现有会话。
- `idalib_current()`：返回绑定到活动上下文策略的会话。
- `idalib_unbind()`：移除活动上下文绑定。
- `idalib_list()`：包含 `is_active`、`is_current_context`、`bound_contexts`、后端（`worker` 或 `gui`）及进程 ID。

Worker 控制选项：

- `--max-workers N`：最大并发数据库 worker 数量（`0` 表示无限制，默认为 `4`）。
- `IDA_MCP_MAX_WORKERS`：`--max-workers` 的环境变量默认值。

## MCP 资源 (MCP Resources)

**Resource（资源）**代表可浏览的状态（只读数据），遵循 MCP 的设计哲学。

**核心 IDB 状态：**
- `ida://idb/metadata` - IDB 文件信息（路径、架构、基址、大小、哈希值）
- `ida://idb/segments` - 带权限的内存段
- `ida://idb/entrypoints` - 入口点（main、TLS 回调等）

**UI 状态：**
- `ida://cursor` - 当前光标位置及所在函数
- `ida://selection` - 当前选中范围

**类型信息：**
- `ida://types` - 所有本地类型
- `ida://structs` - 所有结构体/联合体
- `ida://struct/{name}` - 带字段的结构体定义

**查找：**
- `ida://import/{name}` - 按名称获取导入详情
- `ida://export/{name}` - 按名称获取导出详情
- `ida://xrefs/from/{addr}` - 从指定地址出发的交叉引用

## 核心函数 (Core Functions)

- `lookup_funcs(queries)`：按地址或名称获取函数（自动检测，接受列表或逗号分隔字符串）。
- `int_convert(inputs)`：将数字转换为不同格式（十进制、十六进制、字节、ASCII、二进制等）。
- `list_funcs(queries)`：列出函数（分页、可过滤）。
- `list_globals(queries)`：列出全局变量（分页、可过滤）。
- `imports(offset, count)`：列出所有导入符号及模块名（分页）。
- `decompile(addr)`：反编译指定地址的函数。
- `disasm(addr)`：反汇编函数并显示完整详情（参数、栈帧等）。
- `xrefs_to(addrs)`：获取指向指定地址的所有交叉引用。
- `xrefs_to_field(queries)`：获取指向特定结构体字段的交叉引用。
- `callees(addrs)`：获取指定地址函数所调用的其他函数。

## 修改操作 (Modification Operations)

- `set_comments(items)`：在反汇编和反编译视图中设置指定地址的注释。
- `patch_asm(items)`：修补指定地址的汇编指令。
- `declare_type(decls)`：在本地类型库中声明 C 类型。
- `define_func(items)`：在指定地址定义函数（可选指定 `end` 以明确边界）。
- `define_code(items)`：将指定地址的字节转换为代码指令。
- `undefine(items)`：取消定义指定地址的项目，将其还原为原始字节（可选指定 `end` 或 `size`）。

## 内存读取操作 (Memory Reading Operations)

- `get_bytes(addrs)`：读取指定地址的原始字节。
- `get_int(queries)`：使用类型（ty，如 i8/u64/i16le 等）读取整数值。
- `get_string(addrs)`：读取以空字符结尾的字符串。
- `get_global_value(queries)`：按地址或名称读取全局变量值（自动检测，编译时常量）。

## 栈帧操作 (Stack Frame Operations)

- `stack_frame(addrs)`：获取函数的栈帧变量。
- `declare_stack(items)`：在指定偏移量处创建栈变量。
- `delete_stack(items)`：按名称删除栈变量。

## 结构体操作 (Structure Operations)

- `read_struct(queries)`：读取指定地址的结构体字段值。
- `search_structs(filter)`：按名称模式搜索结构体。

## 调试器操作（扩展）(Debugger Operations)

默认隐藏调试器工具。通过 `?ext=dbg` 查询参数启用：

```
http://127.0.0.1:13337/mcp?ext=dbg
```

**控制：**
- `dbg_start()`：启动调试器进程。
- `dbg_exit()`：退出调试器进程。
- `dbg_continue()`：继续执行。
- `dbg_run_to(addr)`：运行至指定地址。
- `dbg_step_into()`：单步进入指令。
- `dbg_step_over()`：单步跳过指令。

**断点：**
- `dbg_bps()`：列出所有断点。
- `dbg_add_bp(addrs)`：添加断点。
- `dbg_delete_bp(addrs)`：删除断点。
- `dbg_toggle_bp(items)`：启用/禁用断点。

**寄存器：**
- `dbg_regs()`：当前线程的所有寄存器。
- `dbg_regs_all()`：所有线程的所有寄存器。
- `dbg_regs_remote(tids)`：指定线程的寄存器。
- `dbg_gpregs()`：当前线程的通用寄存器（GP）。
- `dbg_gpregs_remote(tids)`：指定线程的通用寄存器。
- `dbg_regs_named(names)`：当前线程的命名寄存器。
- `dbg_regs_named_remote(tid, names)`：指定线程的命名寄存器。

**栈与内存：**
- `dbg_stacktrace()`：带模块/符号信息的调用栈。
- `dbg_read(regions)`：从被调试进程读取内存。
- `dbg_write(regions)`：向被调试进程写入内存。

## 高级分析操作 (Advanced Analysis Operations)

- `py_eval(code)`：在 IDA 上下文中执行任意 Python 代码（返回包含结果/标准输出/标准错误的字典，支持 Jupyter 风格评估）。
- `analyze_funcs(addrs)`：全面分析函数（反编译、汇编、交叉引用、调用者/被调用者、字符串、常量、基本块等）。

## 模式匹配与搜索 (Pattern Matching & Search)

- `find_regex(queries)`：按不区分大小写的正则表达式搜索字符串（分页）。
- `find_bytes(patterns, limit=1000, offset=0)`：在二进制文件中查找字节模式（例如 "48 8B ?? ??"）。最大限制：10000。
- `find_insns(sequences, limit=1000, offset=0)`：在代码中查找指令序列（分页）。最大限制：10000。
- `find(type, targets, limit=1000, offset=0)`：高级搜索（立即数、字符串、数据/代码引用）。最大限制：10000。

## 控制流分析 (Control Flow Analysis)

- `basic_blocks(addrs)`：获取带有后继和前驱节点的基本块。

## 类型操作 (Type Operations)

- `set_type(edits)`：将类型应用于函数、全局变量、局部变量或栈变量。
- `infer_types(addrs)`：使用 Hex-Rays 启发式算法推断指定地址的类型。

## 导出操作 (Export Operations)

- `export_funcs(addrs, format)`：以指定格式（json、c_header 或 prototypes）导出函数。

## 图操作 (Graph Operations)

- `callgraph(roots, max_depth)`：从根函数构建可调用的调用图，支持配置深度。

## 批处理操作 (Batch Operations)

- `rename(batch)`：统一的批量重命名操作（适用于函数、全局变量、局部变量和栈变量，接受包含可选 `func`、`data`、`local`、`stack` 键的字典）。
- `patch(patches)`：一次性修补多个字节序列。
- `put_int(items)`：使用类型（ty，如 i8/u64/i16le 等）写入整数值。

**核心特性：**

- **类型安全的 API**：所有函数均使用强类型参数及 `TypedDict` 模式，以提供更好的 IDE 支持和 LLM 结构化输出
- **优先批处理设计**：大多数操作同时支持单个项目和列表
- **一致的错误处理**：所有批处理操作均返回 `[{..., error: null|string}, ...]` 格式
- **基于游标的分页**：搜索函数返回 `cursor: {next: offset}` 或 `{done: true}`（默认限制为 1000，强制最大值为 10000 以防止 Token 溢出）
- **性能优化**：字符串采用基于 MD5 的缓存失效机制，避免在大型项目中重复调用 `build_strlist`

## 开发指南 (Development)

添加新功能的过程非常简单且流畅。你只需在 `src/ida_pro_mcp/ida_mcp/api_*.py` 的模块化 API 文件中添加一个新的 `@tool` 函数，该函数即可在 MCP Server 中直接使用，无需任何额外样板代码！以下视频演示了我如何在不到 2 分钟内（含测试）添加 `get_metadata` 函数：

https://github.com/user-attachments/assets/951de823-88ea-4235-adcb-9257e316ae64

要测试 MCP Server 本身：

```sh
npx -y @modelcontextprotocol/inspector
```

这将在 http://localhost:5173 打开一个 Web 界面，允许你与 MCP tools 交互进行测试。

测试时我会创建到 IDA 插件的符号链接，然后直接向 `http://localhost:13337/mcp` POST JSON-RPC 请求。在 [启用符号链接](https://learn.microsoft.com/en-us/windows/apps/get-started/enable-your-device-for-development) 后，你可以运行以下命令：

```sh
uv run ida-pro-mcp --install
```

生成直接提交到 `main` 分支的更新日志（Changelog）：

```sh
git log --first-parent --no-merges 1.2.0..main "--pretty=- %s"
```
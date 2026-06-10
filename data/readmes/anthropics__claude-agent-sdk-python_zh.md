# Python SDK for Claude Agent

用于 Claude Agent 的 Python SDK。更多信息请参阅 [Claude Agent SDK 文档](https://platform.claude.com/docs/en/agent-sdk/python)。

## 安装

```bash
pip install claude-agent-sdk
```

**前置条件：**

- Python 3.10+

**注意：** Claude Code CLI 已自动随包捆绑提供，无需单独安装！SDK 默认会使用捆绑的 CLI。如果你偏好使用系统级安装或特定版本，可以：

- 单独安装 Claude Code：`curl -fsSL https://claude.ai/install.sh | bash`
- 指定自定义路径：`ClaudeAgentOptions(cli_path="/path/to/claude")`

## 快速开始

```python
import anyio
from claude_agent_sdk import query

async def main():
    async for message in query(prompt="What is 2 + 2?"):
        print(message)

anyio.run(main)
```

## 基本用法：query()

`query()` 是一个用于查询 Claude Code 的异步函数。它返回包含响应消息的 `AsyncIterator`（异步迭代器）。详见 [src/claude_agent_sdk/query.py](src/claude_agent_sdk/query.py)。

```python
from claude_agent_sdk import query, ClaudeAgentOptions, AssistantMessage, TextBlock

# Simple query
async for message in query(prompt="Hello Claude"):
    if isinstance(message, AssistantMessage):
        for block in message.content:
            if isinstance(block, TextBlock):
                print(block.text)

# With options
options = ClaudeAgentOptions(
    system_prompt="You are a helpful assistant",
    max_turns=1
)

async for message in query(prompt="Tell me a joke", options=options):
    print(message)
```

### 使用工具

默认情况下，Claude 可访问完整的 [Claude Code 工具集](https://code.claude.com/docs/en/settings#tools-available-to-claude)。`allowed_tools` 是一个权限白名单：列出的工具会自动获得批准，未列出的工具将回退到 `permission_mode` 和 `can_use_tool` 进行决策。它不会从 Claude 的工具集中移除任何工具。若要阻止特定工具，请使用 `disallowed_tools`。完整的评估顺序请参阅 [权限指南](https://platform.claude.com/docs/en/agent-sdk/permissions)。

```python
options = ClaudeAgentOptions(
    allowed_tools=["Read", "Write", "Bash"],  # auto-approve these tools
    permission_mode='acceptEdits'  # auto-accept file edits
)

async for message in query(
    prompt="Create a hello.py file",
    options=options
):
    # Process tool use and results
    pass
```

### 工作目录

```python
from pathlib import Path

options = ClaudeAgentOptions(
    cwd="/path/to/project"  # or Path("/path/to/project")
)
```

## ClaudeSDKClient

`ClaudeSDKClient` 支持与 Claude Code 进行双向交互式对话。详见 [src/claude_agent_sdk/client.py](src/claude_agent_sdk/client.py)。

与 `query()` 不同，`ClaudeSDKClient` 还支持**自定义工具（custom tools）**和**钩子（hooks）**，两者均可定义为 Python 函数。

### 自定义工具（作为进程内 SDK MCP 服务器）

**自定义工具**是你提供给 Claude 的 Python 函数，Claude 可根据需要调用它。

自定义工具以进程内 MCP 服务器的形式实现，直接在 Python 应用内部运行，无需像常规 MCP 服务器那样启动独立进程。

完整示例请参阅 [MCP Calculator](examples/mcp_calculator.py)。

#### 创建简单工具

```python
from claude_agent_sdk import tool, create_sdk_mcp_server, ClaudeAgentOptions, ClaudeSDKClient

# Define a tool using the @tool decorator
@tool("greet", "Greet a user", {"name": str})
async def greet_user(args):
    return {
        "content": [
            {"type": "text", "text": f"Hello, {args['name']}!"}
        ]
    }

# Create an SDK MCP server
server = create_sdk_mcp_server(
    name="my-tools",
    version="1.0.0",
    tools=[greet_user]
)

# Use it with Claude. allowed_tools pre-approves the tool so it runs
# without a permission prompt; it does not control tool availability.
options = ClaudeAgentOptions(
    mcp_servers={"tools": server},
    allowed_tools=["mcp__tools__greet"]
)

async with ClaudeSDKClient(options=options) as client:
    await client.query("Greet Alice")

    # Extract and print response
    async for msg in client.receive_response():
        print(msg)
```

#### 相比外部 MCP 服务器的优势

- **无需管理子进程** - 与你的应用运行在同一进程中
- **性能更优** - 工具调用无 IPC（进程间通信）开销
- **部署更简单** - 单个 Python 进程替代多个进程
- **调试更方便** - 所有代码均在同一进程中运行
- **类型安全** - 直接调用带类型提示的 Python 函数

#### 从外部服务器迁移

```python
# BEFORE: External MCP server (separate process)
options = ClaudeAgentOptions(
    mcp_servers={
        "calculator": {
            "type": "stdio",
            "command": "python",
            "args": ["-m", "calculator_server"]
        }
    }
)

# AFTER: SDK MCP server (in-process)
from my_tools import add, subtract  # Your tool functions

calculator = create_sdk_mcp_server(
    name="calculator",
    tools=[add, subtract]
)

options = ClaudeAgentOptions(
    mcp_servers={"calculator": calculator}
)
```

#### 混合服务器支持

你可以同时使用 SDK 和外部 MCP 服务器：

```python
options = ClaudeAgentOptions(
    mcp_servers={
        "internal": sdk_server,      # In-process SDK server
        "external": {                # External subprocess server
            "type": "stdio",
            "command": "external-server"
        }
    }
)
```

### 钩子（hooks）

**钩子（hook）**是 Claude Code _应用程序_（而非 Claude 本身）在 Claude Agent 循环的特定阶段调用的 Python 函数。钩子可为 Claude 提供确定性处理与自动化反馈。更多信息请参阅 [使用钩子拦截和控制 Agent 行为](https://platform.claude.com/docs/en/agent-sdk/hooks)。

更多示例，请参见 `examples/hooks.py`。

#### 示例

```python
from claude_agent_sdk import ClaudeAgentOptions, ClaudeSDKClient, HookMatcher

async def check_bash_command(input_data, tool_use_id, context):
    tool_name = input_data["tool_name"]
    tool_input = input_data["tool_input"]
    if tool_name != "Bash":
        return {}
    command = tool_input.get("command", "")
    block_patterns = ["foo.sh"]
    for pattern in block_patterns:
        if pattern in command:
            return {
                "hookSpecificOutput": {
                    "hookEventName": "PreToolUse",
                    "permissionDecision": "deny",
                    "permissionDecisionReason": f"Command contains invalid pattern: {pattern}",
                }
            }
    return {}

options = ClaudeAgentOptions(
    allowed_tools=["Bash"],
    hooks={
        "PreToolUse": [
            HookMatcher(matcher="Bash", hooks=[check_bash_command]),
        ],
    }
)

async with ClaudeSDKClient(options=options) as client:
    # Test 1: Command with forbidden pattern (will be blocked)
    await client.query("Run the bash command: ./foo.sh --help")
    async for msg in client.receive_response():
        print(msg)

    print("\n" + "=" * 50 + "\n")

    # Test 2: Safe command that should work
    await client.query("Run the bash command: echo 'Hello from hooks example!'")
    async for msg in client.receive_response():
        print(msg)
```

## 类型定义

完整类型定义请参阅 [src/claude_agent_sdk/types.py](src/claude_agent_sdk/types.py)：

- `ClaudeAgentOptions` - 配置选项
- `AssistantMessage`, `UserMessage`, `SystemMessage`, `ResultMessage` - 消息类型
- `TextBlock`, `ToolUseBlock`, `ToolResultBlock` - 内容块

## 错误处理

```python
from claude_agent_sdk import (
    ClaudeSDKError,      # Base error
    CLINotFoundError,    # Claude Code not installed
    CLIConnectionError,  # Connection issues
    ProcessError,        # Process failed
    CLIJSONDecodeError,  # JSON parsing issues
)

try:
    async for message in query(prompt="Hello"):
        pass
except CLINotFoundError:
    print("Please install Claude Code")
except ProcessError as e:
    print(f"Process failed with exit code: {e.exit_code}")
except CLIJSONDecodeError as e:
    print(f"Failed to parse response: {e}")
```

所有错误类型详见 [src/claude_agent_sdk/_errors.py](src/claude_agent_sdk/_errors.py)。

## 可用工具

完整列表请参阅 [Claude Code 文档](https://code.claude.com/docs/en/settings#tools-available-to-claude)。

## 示例

完整可运行的示例请参见 [examples/quick_start.py](examples/quick_start.py)。

涉及 `ClaudeSDKClient` 的综合示例见 [examples/streaming_mode.py](examples/streaming_mode.py)。你甚至可以通过 [examples/streaming_mode_ipython.py](examples/streaming_mode_ipython.py) 在 IPython 中运行交互式示例。

## 从 Claude Code SDK 迁移

如果你正从 Claude Code SDK（版本 < 0.1.0）升级，请参阅 [CHANGELOG.md](CHANGELOG.md#010) 了解破坏性变更和新功能的详细信息，包括：

- `ClaudeCodeOptions` → `ClaudeAgentOptions` 重命名
- 合并的系统提示词（system prompt）配置
- 设置隔离与显式控制
- 新增编程式子 Agent（subagent）与会话分叉功能

## 开发指南

如果你计划为此项目贡献代码，请运行初始设置脚本以安装 Git Hooks：

```bash
./scripts/initial-setup.sh
```

该脚本会安装一个 pre-push（推送前）Hook，在代码推送前执行 Lint 检查，与 CI 工作流保持一致。如需临时跳过此 Hook，请使用 `git push --no-verify`。

### 本地构建 Wheel

使用捆绑的 Claude Code CLI 构建 wheel：

```bash
# Install build dependencies
pip install build twine

# Build wheel with bundled CLI
python scripts/build_wheel.py

# Build with specific version
python scripts/build_wheel.py --version 0.1.4

# Build with specific CLI version
python scripts/build_wheel.py --cli-version 2.0.0

# Clean bundled CLI after building
python scripts/build_wheel.py --clean

# Skip CLI download (use existing)
python scripts/build_wheel.py --skip-download
```

构建脚本执行以下操作：

1. 下载适用于你平台的 Claude Code CLI
2. 将其打包到 wheel 中
3. 同时构建 wheel 和源码发行版（sdist）
4. 使用 twine 检查包

所有选项请参见 `python scripts/build_wheel.py --help`。

### 发布流程

该包通过位于 `.github/workflows/publish.yml` 的 GitHub Actions 工作流发布到 PyPI。创建新版本发布的步骤如下：

1. **手动触发工作流**：在 Actions 标签页中手动运行，并传入两个参数：
   - `version`：要发布的包版本（例如 `0.1.5`）
   - `claude_code_version`：要捆绑的 Claude Code CLI 版本（例如 `2.0.0` 或 `latest`）

2. **工作流将执行以下操作**：
   - 为 macOS、Linux 和 Windows 构建平台特定的 wheel
   - 在每个 wheel 中捆绑指定的 Claude Code CLI 版本
   - 构建源码发行版（sdist）
   - 将所有制品发布到 PyPI
   - 创建包含版本更新的发布分支
   - 向 `main` 分支提交 PR，包含：
     - 更新后的 `pyproject.toml` 版本号
     - 更新后的 `src/claude_agent_sdk/_version.py`
     - 使用捆绑的 CLI 版本更新 `src/claude_agent_sdk/_cli_version.py`
     - 自动生成的 `CHANGELOG.md` 条目

3. **审查并合并**发布 PR，以更新 `main` 分支中的新版本信息

该工作流独立跟踪包版本和捆绑的 CLI 版本，使你能够在不修改代码的情况下发布包含更新版 CLI 的新包版本。

## 许可与条款

使用本 SDK 受 Anthropic [商业服务条款](https://www.anthropic.com/legal/commercial-terms)的约束，即使在你将其用于为自有客户和终端用户提供产品与服务时亦适用，除非特定组件或依赖项在其 `LICENSE` 文件中标明采用了其他许可协议。
<div align="center">
  <div>
    <a href="https://strandsagents.com">
      <img src="https://strandsagents.com/latest/assets/logo-github.svg" alt="Strands Agents" width="55px" height="105px">
    </a>
  </div>

  <h1>
    Strands Agents
  </h1>

  <h2>
    仅需几行代码即可构建 AI Agent 的模型驱动方法。
  </h2>

  <div align="center">
    <a href="https://github.com/strands-agents/sdk-python/graphs/commit-activity"><img alt="GitHub commit activity" src="https://img.shields.io/github/commit-activity/m/strands-agents/sdk-python"/></a>
    <a href="https://github.com/strands-agents/sdk-python/issues"><img alt="GitHub open issues" src="https://img.shields.io/github/issues/strands-agents/sdk-python"/></a>
    <a href="https://github.com/strands-agents/sdk-python/pulls"><img alt="GitHub open pull requests" src="https://img.shields.io/github/issues-pr/strands-agents/sdk-python"/></a>
    <a href="https://github.com/strands-agents/sdk-python/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/github/license/strands-agents/sdk-python"/></a>
    <a href="https://pypi.org/project/strands-agents/"><img alt="PyPI version" src="https://img.shields.io/pypi/v/strands-agents"/></a>
    <a href="https://python.org"><img alt="Python versions" src="https://img.shields.io/pypi/pyversions/strands-agents"/></a>
    <a href="https://discord.gg/strands"><img alt="Strands Discord" src="https://img.shields.io/badge/Discord-Strands-5865F2?logo=discord&logoColor=white"/></a>
  </div>
  
  <p>
    <a href="https://strandsagents.com/">文档</a>
    ◆ <a href="https://github.com/strands-agents/samples">示例</a>
    ◆ <a href="https://github.com/strands-agents/tools">工具</a>
    ◆ <a href="https://github.com/strands-agents/agent-builder">Agent 构建器</a>
    ◆ <a href="https://github.com/strands-agents/mcp-server">MCP Server</a>
  </p>
</div>

Strands Agents 是一个简洁而强大的 SDK，采用模型驱动的方法来构建和运行 AI Agent。无论是简单的对话助手还是复杂的自主工作流，从本地开发到生产部署，Strands Agents 都能随你的需求灵活扩展。

该 Monorepo（单体仓库）包含 Python SDK、TypeScript SDK、文档站点及配套包：

| Directory | Description |
|-----------|-------------|
| `strands-py/` | Python SDK —— Agent 循环、模型提供商、工具（[PyPI](https://pypi.org/project/strands-agents/)） |
| `strands-ts/` | TypeScript SDK —— Agent 循环、模型提供商、工具（[npm](https://www.npmjs.com/package/@strands/agent)） |
| `strands-wasm/` | WebAssembly 绑定，用于在 TypeScript Agent 中运行 Python 工具 |
| `strands-py-wasm/` | WASM 组件的 Python 宿主（将 WIT 接口桥接至 Python） |
| `strandly/` | 用于本地构建、代码生成和工作区工具的开发人员 CLI |
| `site/` | 基于 Astro/Starlight 构建的文档站点（[strandsagents.com](https://strandsagents.com)） |
| `designs/` | 重大功能的设计提案（类 RFC 风格） |

## Feature Overview

- **Lightweight & Flexible**: Simple agent loop that just works and is fully customizable
- **Model Agnostic**: Support for Amazon Bedrock, Anthropic, Gemini, LiteLLM, Llama, Ollama, OpenAI, Writer, and custom providers
- **Advanced Capabilities**: Multi-agent systems, autonomous agents, and streaming support
- **Built-in MCP**: Native support for Model Context Protocol (MCP) servers, enabling access to thousands of pre-built tools

## Quick Start

```bash
# Install Strands Agents
pip install strands-agents strands-agents-tools
```

```python
from strands import Agent
from strands_tools import calculator
agent = Agent(tools=[calculator])
agent("What is the square root of 1764")
```

> **Note**: For the default Amazon Bedrock model provider, you'll need AWS credentials configured and model access enabled for Claude 4 Sonnet in the us-west-2 region. See the [Quickstart Guide](https://strandsagents.com/) for details on configuring other model providers.

## Installation

Ensure you have Python 3.10+ installed, then:

```bash
# Create and activate virtual environment
python -m venv .venv
source .venv/bin/activate  # On Windows use: .venv\Scripts\activate

# Install Strands and tools
pip install strands-agents strands-agents-tools
```

## Features at a Glance

### Python-Based Tools

Easily build tools using Python decorators:

```python
from strands import Agent, tool

@tool
def word_count(text: str) -> int:
    """Count words in text.

    This docstring is used by the LLM to understand the tool's purpose.
    """
    return len(text.split())

agent = Agent(tools=[word_count])
response = agent("How many words are in this sentence?")
```

**Hot Reloading from Directory:**
Enable automatic tool loading and reloading from the `./tools/` directory:

```python
from strands import Agent

# Agent will watch ./tools/ directory for changes
agent = Agent(load_tools_from_directory=True)
response = agent("Use any tools you find in the tools directory")
```

### MCP Support

Seamlessly integrate Model Context Protocol (MCP) servers:

```python
from strands import Agent
from strands.tools.mcp import MCPClient
from mcp import stdio_client, StdioServerParameters

aws_docs_client = MCPClient(
    lambda: stdio_client(StdioServerParameters(command="uvx", args=["awslabs.aws-documentation-mcp-server@latest"]))
)

with aws_docs_client:
   agent = Agent(tools=aws_docs_client.list_tools_sync())
   response = agent("Tell me about Amazon Bedrock and how to use it with Python")
```

### Multiple Model Providers

Support for various model providers:

```python
from strands import Agent
from strands.models import BedrockModel
from strands.models.ollama import OllamaModel
from strands.models.llamaapi import LlamaAPIModel
from strands.models.gemini import GeminiModel
from strands.models.llamacpp import LlamaCppModel

# Bedrock
bedrock_model = BedrockModel(
  model_id="us.amazon.nova-pro-v1:0",
  temperature=0.3,
  streaming=True, # Enable/disable streaming
)
agent = Agent(model=bedrock_model)
agent("Tell me about Agentic AI")

# Google Gemini
gemini_model = GeminiModel(
  client_args={
    "api_key": "your_gemini_api_key",
  },
  model_id="gemini-2.5-flash",
  params={"temperature": 0.7}
)
agent = Agent(model=gemini_model)
agent("Tell me about Agentic AI")

# Ollama
ollama_model = OllamaModel(
  host="http://localhost:11434",
  model_id="llama3"
)
agent = Agent(model=ollama_model)
agent("Tell me about Agentic AI")

# Llama API
llama_model = LlamaAPIModel(
    model_id="Llama-4-Maverick-17B-128E-Instruct-FP8",
)
agent = Agent(model=llama_model)
response = agent("Tell me about Agentic AI")
```

Built-in providers:
 - [Amazon Bedrock](https://strandsagents.com/docs/user-guide/concepts/model-providers/amazon-bedrock/)
 - [Anthropic](https://strandsagents.com/docs/user-guide/concepts/model-providers/anthropic/)
 - [Gemini](https://strandsagents.com/docs/user-guide/concepts/model-providers/gemini/)
 - [Cohere](https://strandsagents.com/docs/user-guide/concepts/model-providers/cohere/)
 - [LiteLLM](https://strandsagents.com/docs/user-guide/concepts/model-providers/litellm/)
 - [llama.cpp](https://strandsagents.com/docs/user-guide/concepts/model-providers/llamacpp/)
 - [LlamaAPI](https://strandsagents.com/docs/user-guide/concepts/model-providers/llamaapi/)
 - [MistralAI](https://strandsagents.com/docs/user-guide/concepts/model-providers/mistral/)
 - [Ollama](https://strandsagents.com/docs/user-guide/concepts/model-providers/ollama/)
 - [OpenAI](https://strandsagents.com/docs/user-guide/concepts/model-providers/openai/)
 - [OpenAI Responses API](https://strandsagents.com/docs/user-guide/concepts/model-providers/openai/)
 - [SageMaker](https://strandsagents.com/docs/user-guide/concepts/model-providers/sagemaker/)
 - [Writer](https://strandsagents.com/docs/user-guide/concepts/model-providers/writer/)

Custom providers can be implemented using [Custom Providers](https://strandsagents.com/docs/user-guide/concepts/model-providers/custom_model_provider/)

### Example tools

Strands offers an optional strands-agents-tools package with pre-built tools for quick experimentation:

```python
from strands import Agent
from strands_tools import calculator
agent = Agent(tools=[calculator])
agent("What is the square root of 1764")
```

It's also available on GitHub via [strands-agents/tools](https://github.com/strands-agents/tools).

### Bidirectional Streaming

> **⚠️ Experimental Feature**: Bidirectional streaming is currently in experimental status. APIs may change in future releases as we refine the feature based on user feedback and evolving model capabilities.

Build real-time voice and audio conversations with persistent streaming connections. Unlike traditional request-response patterns, bidirectional streaming maintains long-running conversations where users can interrupt, provide continuous input, and receive real-time audio responses. Get started with your first BidiAgent by following the [Quickstart](https://strandsagents.com/docs/user-guide/concepts/bidirectional-streaming/quickstart/) guide. 

**Supported Model Providers:**
- Amazon Nova Sonic (v1, v2)
- Google Gemini Live
- OpenAI Realtime API

**Installation:**

```bash
# Server-side only (no audio I/O dependencies)
pip install strands-agents[bidi]

# With audio I/O support (includes PyAudio dependency)
pip install strands-agents[bidi,bidi-io]
```

**Quick Example:**

```python
import asyncio
from strands.experimental.bidi import BidiAgent
from strands.experimental.bidi.models import BidiNovaSonicModel
from strands.experimental.bidi.io import BidiAudioIO, BidiTextIO
from strands.experimental.bidi.tools import stop_conversation
from strands_tools import calculator

async def main():
    # Create bidirectional agent with Nova Sonic v2
    model = BidiNovaSonicModel()
    agent = BidiAgent(model=model, tools=[calculator, stop_conversation])

    # Setup audio and text I/O (requires bidi-io extra)
    audio_io = BidiAudioIO()
    text_io = BidiTextIO()

    # Run with real-time audio streaming
    # Say "stop conversation" to gracefully end the conversation
    await agent.run(
        inputs=[audio_io.input()],
        outputs=[audio_io.output(), text_io.output()]
    )

if __name__ == "__main__":
    asyncio.run(main())
```

> **Note**: `BidiAudioIO` and `BidiTextIO` require the `bidi-io` extra. For server-side deployments where audio I/O is handled by clients (browsers, mobile apps), install only `strands-agents[bidi]` and implement custom input/output handlers using the `BidiInput` and `BidiOutput` protocols.

**Configuration Options:**

```python
from strands.experimental.bidi.models import BidiNovaSonicModel

# Configure audio settings and turn detection (v2 only)
model = BidiNovaSonicModel(
    provider_config={
        "audio": {
            "input_rate": 16000,
            "output_rate": 16000,
            "voice": "matthew"
        },
        "turn_detection": {
            "endpointingSensitivity": "MEDIUM"  # HIGH, MEDIUM, or LOW
        },
        "inference": {
            "max_tokens": 2048,
            "temperature": 0.7
        }
    }
)

# Configure I/O devices
audio_io = BidiAudioIO(
    input_device_index=0,  # Specific microphone
    output_device_index=1,  # Specific speaker
    input_buffer_size=10,
    output_buffer_size=10
)

# Text input mode (type messages instead of speaking)
text_io = BidiTextIO()
await agent.run(
    inputs=[text_io.input()],  # Use text input
    outputs=[audio_io.output(), text_io.output()]
)

# Multi-modal: Both audio and text input
await agent.run(
    inputs=[audio_io.input(), text_io.input()],  # Speak OR type
    outputs=[audio_io.output(), text_io.output()]
)
```

## Documentation

For detailed guidance & examples, explore our documentation:

- [User Guide](https://strandsagents.com/)
- [Quick Start Guide](https://strandsagents.com/docs/user-guide/quickstart/)
- [Agent Loop](https://strandsagents.com/docs/user-guide/concepts/agents/agent-loop/)
- [Examples](https://strandsagents.com/docs/examples/)
- [API Reference](https://strandsagents.com/docs/api/python/strands.agent.agent/)
- [Production & Deployment Guide](https://strandsagents.com/docs/user-guide/deploy/operating-agents-in-production/)

## Development

Git operations (commits, branches, PRs) are done from the repo root. Each package has its own toolchain:

**Python SDK** (`strands-py/`):
```bash
cd strands-py
pip install hatch
hatch test        # run unit tests
hatch fmt         # format & lint
```

**TypeScript SDK** (`strands-ts/`):
```bash
npm ci            # install from repo root
npm run build     # build
npm test          # run unit tests
```

**Documentation site** (`site/`):
```bash
cd site
npm install
npm run dev       # local dev server at http://localhost:4321/
```

## Contributing ❤️

We welcome contributions! See our [Contributing Guide](CONTRIBUTING.md) for details on:
- Reporting bugs & features
- Development setup
- Contributing via Pull Requests
- Code of Conduct
- Reporting of security issues

## Stay in touch with the team
Come meet the Strands team and other users on [**Discord**](https://discord.com/invite/strands)

## License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.
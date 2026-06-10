# NVIDIA OpenShell

[![License](https://img.shields.io/badge/License-Apache_2.0-blue)](https://github.com/NVIDIA/OpenShell/blob/main/LICENSE)
[![PyPI](https://img.shields.io/badge/PyPI-openshell-orange?logo=pypi)](https://pypi.org/project/openshell/)
[![Security Policy](https://img.shields.io/badge/Security-Report%20a%20Vulnerability-red)](SECURITY.md)
[![Documentation](https://img.shields.io/badge/docs-latest-brightgreen)](https://docs.nvidia.com/openshell/latest/index.html)
[![Project Status](https://img.shields.io/badge/status-alpha-orange)](https://docs.nvidia.com/openshell/latest/about/release-notes.html)

OpenShell 是用于自主 AI agent（智能体）的安全、私密运行时环境。它提供沙箱化执行环境，保护你的数据、凭证和基础设施——通过声明式 YAML 策略进行管控，防止未经授权的文件访问、数据泄露和非受控的网络活动。

OpenShell 采用 `agent` 优先架构构建。项目内置了多种 agent 技能，涵盖从网关故障排查到策略生成的各类场景，我们期望贡献者使用它们。

> **Alpha 阶段软件 —— 单用户模式。** OpenShell 目前处于概念验证阶段：面向单个开发者、单一环境、单一网关。我们正在向多租户企业级部署迈进，但起步阶段是让你自己的环境顺利运行。请预期可能会遇到一些粗糙之处（rough edges）。带上你的 agent 开始体验吧。

## Quickstart

### Prerequisites

- **受支持的主机** — macOS、搭载 WSL 2 的 Windows 或 Linux。
- **本地运行时** — Docker、Podman，或已启用 MicroVM 虚拟化以支持沙箱环境。

### Install

**二进制文件（推荐）：**

```bash
curl -LsSf https://raw.githubusercontent.com/NVIDIA/OpenShell/main/install.sh | sh
```

**从 PyPI 安装（需要 [uv](https://docs.astral.sh/uv/)）：**

```bash
uv tool install -U openshell
```

两种方法默认均会安装最新稳定版。要安装特定版本，可设置 `OPENSHELL_VERSION`（二进制方式）或使用 `uv tool install openshell==<version>` 指定版本号。此外还提供 [`dev`](https://github.com/NVIDIA/OpenShell/releases/tag/dev) 发行版，它会跟踪 `main` 分支的最新提交。

**Helm Chart：**

> **实验性功能** —— Kubernetes 部署路径正在积极开发中。请预期可能会遇到一些粗糙之处和破坏性变更。

从发布到 GHCR 的 OCI chart 将 OpenShell gateway 部署到 Kubernetes 集群：

```bash
helm install openshell oci://ghcr.io/nvidia/openshell/helm-chart
```

有关可用版本、dev tag 约定及配置说明，请参阅 [`deploy/helm/openshell/README.md`](deploy/helm/openshell/README.md)。

如需在 OpenShift 上部署 OpenShell，请参阅 [`deploy/helm/openshell/README.md#install-on-openshift`](deploy/helm/openshell/README.md#install-on-openshift)。

### Create a sandbox

```bash
openshell sandbox create -- claude  # or opencode, codex, copilot
```

沙箱容器默认包含以下工具：

| Category   | Tools                                                    |
| ---------- | -------------------------------------------------------- |
| Agent      | `claude`, `opencode`, `codex`, `copilot`                 |
| Language   | `python` (3.14), `node` (22)                             |
| Developer  | `gh`, `git`, `vim`, `nano`                               |
| Networking | `ping`, `dig`, `nslookup`, `nc`, `traceroute`, `netstat` |

更多详情见 https://github.com/NVIDIA/OpenShell-Community/tree/main/sandboxes/base。

### See network policy in action

每个沙箱默认仅开放**最小化的出站访问权限**。你可以通过简短的 YAML 策略开启额外权限，代理会在 HTTP 方法和路径级别强制执行这些策略，且无需重启任何服务。

```bash
# 1. Create a sandbox (starts with minimal outbound access)
openshell sandbox create

# 2. Inside the sandbox — blocked
sandbox$ curl -sS https://api.github.com/zen
curl: (56) Received HTTP code 403 from proxy after CONNECT

# 3. Back on the host — apply a read-only GitHub API policy
sandbox$ exit
openshell policy set demo --policy examples/sandbox-policy-quickstart/policy.yaml --wait

# 4. Reconnect — GET allowed, POST blocked by L7
openshell sandbox connect demo
sandbox$ curl -sS https://api.github.com/zen
Anything added dilutes everything else.

sandbox$ curl -sS -X POST https://api.github.com/repos/octocat/hello-world/issues -d '{"title":"oops"}'
{"error":"policy_denied","detail":"POST /repos/octocat/hello-world/issues not permitted by policy"}
```

查看[完整操作指南](examples/sandbox-policy-quickstart/)或运行自动化演示：

```bash
bash examples/sandbox-policy-quickstart/demo.sh
```

## How It Works

OpenShell 将每个沙箱隔离在独立的容器中，并通过策略强制实施出站路由。轻量级 gateway 协调沙箱生命周期，所有出站连接均会被策略引擎拦截，并执行以下三种操作之一：

- **Allows（允许）** — 目标地址和二进制文件匹配策略规则块。
- **Routes for inference（推理路由）** — 剥离调用方凭证，注入后端凭证，并转发至托管模型。
- **Denies（拒绝）** — 阻止请求并进行日志记录。

| Component          | Role                                                                                         |
| ------------------ | -------------------------------------------------------------------------------------------- |
| **Gateway**        | Control-plane API that coordinates sandbox lifecycle and acts as the auth boundary.          |
| **Sandbox**        | Isolated runtime with container supervision and policy-enforced egress routing.              |
| **Policy Engine**  | Enforces filesystem, network, and process constraints from application layer down to kernel. |
| **Privacy Router** | Privacy-aware LLM routing that keeps sensitive context on sandbox compute.                   |

OpenShell 运行一个 gateway 控制面，通过配置的 compute driver 管理沙箱生命周期。支持的计算平台包括 Docker、Podman、MicroVM 和 Kubernetes。

## Protection Layers

OpenShell 在四个策略领域实施纵深防御：

| Layer      | What it protects                                    | When it applies             |
| ---------- | --------------------------------------------------- | --------------------------- |
| Filesystem | Prevents reads/writes outside allowed paths.        | Locked at sandbox creation. |
| Network    | Blocks unauthorized outbound connections.           | Hot-reloadable at runtime.  |
| Process    | Blocks privilege escalation and dangerous syscalls. | Locked at sandbox creation. |
| Inference  | Reroutes model API calls to controlled backends.    | Hot-reloadable at runtime.  |

策略为声明式 YAML 文件。静态部分（文件系统、进程）在沙箱创建时锁定；动态部分（网络、推理）可通过 `openshell policy set` 对运行中的沙箱进行热重载。

## Providers

Agent 需要凭证 —— API keys、tokens、service accounts。OpenShell 将这些管理为 **providers**：命名凭证包，在沙箱创建时注入其中。CLI 会自动从你的 shell 环境中发现已识别 agent（Claude, Codex, OpenCode, Copilot）的凭证，或者你可以使用 `openshell provider create` 显式创建 providers。凭证绝不会泄露到沙箱文件系统中；它们会在运行时作为环境变量注入。

## GPU Support (Experimental)

> **实验性功能** —— GPU 直通在受支持的主机上可用，但仍在积极开发中。请预期可能会遇到一些粗糙之处和破坏性变更。

OpenShell 可将主机 GPU 直通至沙箱，用于本地推理、微调或任何 GPU 工作负载。创建沙箱时添加 `--gpu`：

```bash
openshell sandbox create --gpu --from [gpu-enabled-sandbox] -- claude
```

Docker 支持的 GPU 沙箱在可用时会自动选择 CDI，否则回退到 Docker 的 NVIDIA GPU 请求路径（`--gpus all`）。对于名称中包含 `gpu` 的社区镜像，GPU 意图也会自动推断。

**要求：** 主机必须安装 NVIDIA 驱动和 [NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html)。沙箱镜像本身必须包含适用于你工作负载的相应 GPU 驱动和库 —— 默认的 `base` 镜像不包含。参见 [BYOC example](https://github.com/NVIDIA/OpenShell/tree/main/examples/bring-your-own-container) 了解如何构建支持 GPU 的自定义沙箱镜像。

## Supported Agents

| Agent                                                         | Source                                                                           | Notes                                                                         |
| ------------------------------------------------------------- | -------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| [Claude Code](https://docs.anthropic.com/en/docs/claude-code) | [`base`](https://github.com/NVIDIA/OpenShell-Community/tree/main/sandboxes/base) | Works out of the box. Provider uses `ANTHROPIC_API_KEY`.                      |
| [OpenCode](https://opencode.ai/)                              | [`base`](https://github.com/NVIDIA/OpenShell-Community/tree/main/sandboxes/base) | Works out of the box. Provider uses `OPENAI_API_KEY` or `OPENROUTER_API_KEY`. |
| [Codex](https://developers.openai.com/codex)                  | [`base`](https://github.com/NVIDIA/OpenShell-Community/tree/main/sandboxes/base) | Works out of the box. Provider uses `OPENAI_API_KEY`.                         |
| [GitHub Copilot CLI](https://docs.github.com/en/copilot/github-copilot-in-the-cli) | [`base`](https://github.com/NVIDIA/OpenShell-Community/tree/main/sandboxes/base) | Works out of the box. Provider uses `GITHUB_TOKEN` or `COPILOT_GITHUB_TOKEN`. |
| [OpenClaw](https://openclaw.ai/)                 | [NemoClaw](https://github.com/NVIDIA/NemoClaw)                                   | Run OpenClaw more securely inside NVIDIA OpenShell with managed inference using NemoClaw.       |
| [Ollama](https://ollama.com/)                                 | [Community](https://github.com/NVIDIA/OpenShell-Community)                       | Launch with `openshell sandbox create --from ollama`.                         |
| [Pi](https://pi.dev/)                                 | [Community](https://github.com/NVIDIA/OpenShell-Community)                       | Launch with `openshell sandbox create --from pi`.                         |

## Key Commands

| Command                                                    | Description                                     |
| ---------------------------------------------------------- | ----------------------------------------------- |
| `openshell sandbox create -- <agent>`                      | Create a sandbox and launch an agent.           |
| `openshell sandbox connect [name]`                         | SSH into a running sandbox.                     |
| `openshell sandbox list`                                   | List all sandboxes.                             |
| `openshell provider create --type [type]] --from-existing` | Create a credential provider from env vars.     |
| `openshell policy set <name> --policy file.yaml`           | Apply or update a policy on a running sandbox.  |
| `openshell policy get <name>`                              | Show the active policy.                         |
| `openshell inference set --provider <p> --model <m>`       | Configure the `inference.local` endpoint.       |
| `openshell logs [name] --tail`                             | Stream sandbox logs.                            |
| `openshell term`                                           | Launch the real-time terminal UI for debugging. |

有关命令指南、教程和参考资料，请参阅[完整文档](https://docs.nvidia.com/openshell/latest)。

## Terminal UI

OpenShell 内置一个实时终端仪表板，用于监控 gateway、沙箱和 providers —— 灵感来源于 [k9s](https://k9scli.io/)。

```bash
openshell term
```

<p align="center">
  <img src="fern/assets/images/openshell-terminal.png" alt="OpenShell Terminal UI">
</p>

该 TUI（终端用户界面）为你提供对 gateway 和沙箱的实时、键盘驱动视图。使用 `Tab` 切换面板，`j`/`k` 浏览列表，`Enter` 选择项目，`:` 进入命令模式。Gateway 健康和沙箱状态每两秒自动刷新一次。

## Community Sandboxes and BYOC

使用 `--from` 从 [OpenShell Community](https://github.com/NVIDIA/OpenShell-Community) 目录、本地目录或容器镜像创建沙箱：

```bash
openshell sandbox create --from gemini             # community catalog
openshell sandbox create --from ./my-sandbox-dir   # local Dockerfile
openshell sandbox create --from registry.io/img:v1 # container image
```

详见 [community sandboxes](https://docs.nvidia.com/openshell/latest/sandboxes/community-sandboxes) 目录和 [BYOC example](https://github.com/NVIDIA/OpenShell/tree/main/examples/bring-your-own-container)。

## Explore with Your Agent

克隆仓库并将你的 coding agent 指向它。项目内置了 agent 技能，可回答问题、引导你完成工作流并诊断问题 —— 无需提交 issue。

```bash
git clone https://github.com/NVIDIA/OpenShell.git   # or git@github.com:NVIDIA/OpenShell.git
cd OpenShell
# Point your agent here — it will discover the skills in .agents/skills/ automatically
```

你的 agent 可加载以下技能的 CLI 使用（`openshell-cli`）、网关故障排查（`debug-openshell-cluster`）、推理故障排查（`debug-inference`）、策略生成（`generate-sandbox-policy`）等技能。完整技能表见 [CONTRIBUTING.md](CONTRIBUTING.md)。

## Built With Agents

OpenShell 使用与它所提供的相同 agent 驱动工作流进行开发。`.agents/skills/` 目录包含自动化工作流，支撑项目的开发周期：

- **Spike and build（探索与构建）：** 使用 `create-spike` 调查问题，经人类批准后通过 `build-from-issue` 实现。
- **Triage and route（分类与路由）：** 社区 issue 由 `triage-issue` 评估、分类并路由至探索-构建流水线。
- **Security review（安全审查）：** `review-security-issue` 生成严重性评估和修复计划，`fix-security-issue` 负责实施。
- **Policy authoring（策略编写）：** `generate-sandbox-policy` 根据自然语言需求或 API 文档生成 YAML 策略。

所有实现工作均由人类把关 —— agent 提出方案，人类审批，agent 构建代码。完整的工作流链文档见 [AGENTS.md](AGENTS.md)。

## Getting Help

- **Questions and discussion（问题与讨论）：** [GitHub Discussions](https://github.com/NVIDIA/OpenShell/discussions)
- **Bug reports（缺陷报告）：** [GitHub Issues](https://github.com/NVIDIA/OpenShell/issues) — 请使用缺陷报告模板
- **Security vulnerabilities（安全漏洞）：** 见 [SECURITY.md](SECURITY.md) —— 请勿使用 GitHub Issues
- **Agent-assisted help（Agent 辅助帮助）：** 克隆仓库并使用 `.agents/skills/` 中的 agent 技能进行自助诊断

## Learn More

- [Full Documentation](https://docs.nvidia.com/openshell/latest/index.html) — overview, architecture, tutorials, and reference
- [Quickstart](https://docs.nvidia.com/openshell/latest/get-started/quickstart) — detailed install and first sandbox walkthrough
- [GitHub Sandbox Tutorial](https://docs.nvidia.com/openshell/latest/tutorials/github-sandbox) — end-to-end scoped GitHub repo access
- [Architecture](https://github.com/NVIDIA/OpenShell/tree/main/architecture) — detailed architecture docs and design decisions
- [Roadmap](https://github.com/orgs/NVIDIA/projects/233) — planned work and project priorities
- [Support Matrix](https://docs.nvidia.com/openshell/latest/reference/support-matrix) — platforms, versions, and kernel requirements
- [Brev Launchable](https://brev.nvidia.com/launchable/deploy/now?launchableID=env-3Ap3tL55zq4a8kew1AuW0FpSLsg) — try OpenShell on cloud compute without local setup
- [Agent Instructions](AGENTS.md) — system prompt and workflow documentation for agent contributors

## Contributing

OpenShell 采用 `agent` 优先构建 —— 你的 agent 是你的第一位协作者。在提交 issue 或代码之前，请将你的 agent 指向仓库，让它使用 `.agents/skills/` 中的技能进行调查、诊断和原型验证。完整技能表、贡献工作流及开发环境配置见 [CONTRIBUTING.md](CONTRIBUTING.md)。

## Telemetry

OpenShell 收集匿名遥测数据以帮助改进项目。这些数据不会用于追踪单个用户的行为。它帮助我们了解沙箱、provider 和策略工作流的聚合使用情况，以便我们优先处理产品改进并与社区共享使用趋势。

可通过在 gateway 部署中设置 `OPENSHELL_TELEMETRY_ENABLED=false` 来禁用遥测功能。OpenShell 会将此部署配置传播至沙箱 supervisor 环境，从而同时禁用沙箱侧的遥测收集。

遥测事件仅限于匿名操作类别和计数，例如沙箱生命周期结果、provider 配置文件桶、策略决策计数以及聚合网络活动拒绝类别。OpenShell 遥测不收集沙箱名称或 ID、主机名、文件路径、二进制路径、prompt、凭证、provider 名称、模型名称或用户内容。

退出仅适用于 OpenShell 发出的遥测数据。你配置和使用的第三方服务、模型提供商、推理端点、agent 或与 OpenShell 配合使用的工具可能拥有自己的条款和隐私实践。

## Notice and Disclaimer

This software automatically retrieves, accesses or interacts with external materials. Those retrieved materials are not distributed with this software and are governed solely by separate terms, conditions and licenses. You are solely responsible for finding, reviewing and complying with all applicable terms, conditions, and licenses, and for verifying the security, integrity and suitability of any retrieved materials for your specific use case. This software is provided "AS IS", without warranty of any kind. The author makes no representations or warranties regarding any retrieved materials, and assumes no liability for any losses, damages, liabilities or legal consequences from your use or inability to use this software or any retrieved materials. Use this software and the retrieved materials at your own risk.

## License

This project is licensed under the [Apache License 2.0](https://github.com/NVIDIA/OpenShell/blob/main/LICENSE)。
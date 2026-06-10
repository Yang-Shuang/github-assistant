<p align="center">
  <img src="docs/assets/cube-sandbox-logo.png" alt="Cube Sandbox Logo" width="140" />
</p>

<h1 align="center">CubeSandbox</h1>

<p align="center">
  <strong>面向 AI Agent 的即时、并发、安全且轻量级的沙箱服务</strong>
</p>

<p align="center">
  <a href="https://github.com/tencentcloud/CubeSandbox/stargazers"><img src="https://img.shields.io/github/stars/tencentcloud/cubesandbox?style=social" alt="GitHub Stars" /></a>
  <a href="https://github.com/tencentcloud/CubeSandbox/issues"><img src="https://img.shields.io/github/issues/tencentcloud/cubesandbox" alt="GitHub Issues" /></a>
  <a href="./LICENSE"><img src="https://img.shields.io/badge/License-Apache_2.0-green" alt="Apache 2.0 License" /></a>
  <a href="./CONTRIBUTING.md"><img src="https://img.shields.io/badge/PRs-welcome-brightgreen" alt="PRs Welcome" /></a>
  <a href="https://pypi.org/project/cubesandbox/"><img src="https://img.shields.io/badge/PyPI-0.2.1-blue" alt="PyPI Version" /></a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/⚡_Startup-Tens_of_ms-blue" alt="Fast startup" />
  <img src="https://img.shields.io/badge/🔒_Isolation-Hardware_Level-critical" alt="Hardware-level isolation" />
  <img src="https://img.shields.io/badge/🔌_API-E2B_Compatible-blueviolet" alt="E2B compatible" />
  <img src="https://img.shields.io/badge/📦_Deploy-High_Concurrency·High_Density-orange" alt="High concurrency & high density" />
</p>

<p align="center">
  <a href="./README_zh.md"><strong>中文文档</strong></a> ·
  <a href="./docs/guide/quickstart.md"><strong>快速入门</strong></a> ·
  <a href="./docs/index.md"><strong>完整文档</strong></a> ·
  <a href="./docs/changelog/index.md"><strong>更新日志</strong></a> ·
  <a href="https://x.com/CubeSandbox_AI"><strong>X (Twitter)</strong></a>
</p>

---

Cube Sandbox 是一款基于 RustVMM 和 KVM 构建的高性能、开箱即用的安全沙箱服务。它支持单机部署，并可轻松扩展至多节点集群。该服务兼容 E2B SDK，能够在不到 60ms 的时间内创建具备硬件级隔离且功能完整的沙箱实例，内存开销低于 5MB。


<p align="center">
  <img src="./docs/assets/readme_speed_en_1.png" width="400" />
  <img src="./docs/assets/readme_overhead_en_1.png" width="400" />
</p>

## 📰 最新动态

<table>
  <tr>
    <td align="right" valign="top" width="100">
      <a href="./docs/changelog/v0.3.0.md">
        <img src="https://img.shields.io/badge/v0.3.0-New!-6f42c1?style=flat-square" alt="v0.3.0" />
      </a>
    </td>
    <td valign="top">
      <strong>快照、克隆与回滚达到毫秒级精度</strong><br/>
      CubeSandbox 0.3.0 引入了 <b>CubeCoW</b> 写时复制（Copy-on-Write）快照引擎，支持事件级快照、即时克隆以及回滚至任意已保存状态。
      <a href="./docs/changelog/v0.3.0.md">更新日志 →</a>
    </td>
  </tr>
  <tr>
    <td align="right" valign="top" width="100">
      <a href="./docs/changelog/v0.2.2.md">
        <img src="https://img.shields.io/badge/v0.2.2-2026.05.18-007bff?style=flat-square" alt="v0.2.2" />
      </a>
    </td>
    <td valign="top">
      <strong>安全加固与 E2B 兼容性改进</strong><br/>
      修复了 CVE-2023-50711 等漏洞，默认端口已对齐 E2B 协议规范，并附带关键稳定性修复。
      <a href="./docs/changelog/v0.2.2.md">更新日志 →</a>
    </td>
  </tr>
  <tr>
    <td align="right" valign="top" width="100">
      <a href="./docs/changelog/v0.1.0.md">
        <img src="https://img.shields.io/badge/v0.1.0-2026.04.20-28a745?style=flat-square" alt="v0.1.0" />
      </a>
    </td>
    <td valign="top">
      <strong>🎉 首次开源发布</strong><br/>
      Cube Sandbox 现已开源！毫秒级启动、硬件级隔离，专为 AI Agent 打造的 E2B 兼容沙箱。
      <a href="./docs/changelog/v0.1.0.md">更新日志 →</a>
    </td>
  </tr>
</table>

## 🎬 演示

<table align="center">
  <tr align="center" valign="middle">
    <td width="33%" valign="middle">
      <video src="https://github.com/user-attachments/assets/f87c409e-29fc-4e86-9eac-dbeaff2aca18" controls="controls" muted="muted" style="max-width: 100%;"></video>
    </td>
    <td width="33%" valign="middle">
      <video src="https://github.com/user-attachments/assets/50e7126e-bb73-4abc-aa85-677fdf2e8c67" controls="controls" muted="muted" style="max-width: 100%;"></video>
    </td>
    <td width="33%" valign="middle">
      <video src="https://github.com/user-attachments/assets/052e0e77-e2d9-409e-90b8-d13c28b80495" controls="controls" muted="muted" style="max-width: 100%;"></video>
    </td>
  </tr>
  <tr align="center" valign="top">
    <td>
      <em>安装与演示</em>
    </td>
    <td>
      <em>性能测试</em>
    </td>
    <td>
      <em>强化学习 (SWE-Bench)</em>
    </td>
  </tr>
</table>


## 🚀 核心亮点

- **极速冷启动：**基于资源池预分配和快照克隆技术，完全跳过耗时的初始化过程。功能完整的沙箱端到端冷启动时间平均低于 60ms。
- **单机高密度部署：**通过 CoW（写时复制）技术实现极致内存复用，结合 Rust 重写并大幅精简的运行环境，使单实例内存开销低于 5MB —— 在一台机器上即可运行数千个 Agent。
- **真正的内核级隔离：**告别不安全的 Docker 共享内核（Namespace）方案。每个 Agent 均拥有独立的 Guest OS 内核，彻底消除容器逃逸风险，安全执行任何 LLM 生成的代码。
- **零成本迁移（即插即用 E2B 替代方案）：**原生兼容 E2B SDK 接口。仅需修改一个 URL 环境变量即可无缝迁移，无需改动业务逻辑，即可从昂贵闭源沙箱切换至性能更优且免费的 Cube Sandbox。
- **网络安全：**基于 eBPF 的 CubeVS 在内核层面实施严格的沙箱间网络隔离，并提供细粒度的出站流量过滤策略。
- **开箱即用：**一键部署，支持单机与集群模式。
- **事件级快照回滚：**毫秒级高频快照回滚。可在运行中的沙箱创建检查点、回滚至任意保存状态，或从任意状态分叉出并行探索环境。
- **生产就绪：**Cube Sandbox 已在腾讯云生产环境中经过大规模验证，稳定可靠。

## 📊 性能基准测试

在 AI Agent 代码执行场景下，CubeSandbox 实现了安全性与性能的完美平衡：

| 指标 | Docker 容器 | 传统虚拟机 | CubeSandbox |
|---|---|---|---|
| **隔离级别** | 低（共享内核命名空间） | 高（独立内核） | **极高（独立内核 + eBPF）** |
| **启动速度** <br>*完整操作系统引导时间* | 200ms | 秒级 | **亚毫秒级 (<60ms)** |
| **内存开销** | 低（共享内核） | 高（完整操作系统） | **极低（深度精简，<5MB）** |
| **部署密度** | 高 | 低 | **极高（单节点数千实例）** |
| **兼容 E2B SDK** | / | / | **✅ 即插即用** |

*   *冷启动基准测试基于裸机环境。单并发下为 60ms；在 50 次以下并发创建时，平均耗时 67ms，P95 为 90ms，P99 为 137ms —— 始终保持在 150ms 以内。*
*   *内存开销基于沙箱规格 ≤ 32GB 进行测试。较大配置下可能会有轻微增加。*

有关启动延迟和资源开销的详细指标，请参阅：


<table align="center">
  <tr align="center" valign="middle">
    <td width="33%" valign="middle">
      <img src="./docs/assets/1-concurrency-create.png" />
    </td>
    <td width="33%" valign="middle">
      <img src="./docs/assets/50-concurrency-create.png" />
    </td>
    <td width="33%" valign="middle">
      <img src="./docs/assets/cube-sandbox-mem-overhead.png" />
    </td>
  </tr>
  <tr align="center" valign="top">
    <td colspan="2">
      <em>单并发与高并发负载下均能在 150ms 内交付沙箱</em>
    </td>
    <td>
      <em>CubeSandbox 在不同实例规格下的基础内存占用</em><br>
      <sup>(*蓝色：沙箱规格；橙色：基础内存开销)。请注意，随着实例规模扩大，内存消耗仅呈轻微增长。</sup>
    </td>
  </tr>
</table>


</br>

## ⚡ 快速入门

<p align="center">
  <img src="docs/assets/fast-start.gif" alt="Cube Sandbox fast start walkthrough" width="720" />
</p>

<p align="center">
  <em>⚡ 毫秒级启动 —— 观看上方的快速启动流程演示。</em>
</p>

Cube Sandbox 需要支持 **KVM** 的 **x86_64 Linux** 环境。

本指南将引导你通过**四个步骤**完成所有操作——准备服务器、安装 Cube Sandbox、创建沙箱模板，以及运行你的第一个 Agent 代码。无需源码编译，几分钟即可部署完毕。

<p align="center">
  <b>选择你的部署路径：</b>
</p>

<table align="center">
  <tr align="center">
    <td align="center">
      <a href="./docs/guide/pvm-deploy.md" style="
        display: inline-block;
        background: #28a745;
        color: white;
        padding: 12px 28px;
        border-radius: 8px;
        font-size: 15px;
        font-weight: bold;
        text-decoration: none;
        white-space: nowrap;
        font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif;
      ">
        🖥 PVM · 云虚拟机 →
      </a>
      <br/>
      <sup><b>🏆 推荐</b></sup>
    </td>
    <td align="center">
      <a href="./docs/guide/bare-metal-deploy.md" style="
        display: inline-block;
        background: #007bff;
        color: white;
        padding: 12px 28px;
        border-radius: 8px;
        font-size: 15px;
        font-weight: bold;
        text-decoration: none;
        white-space: nowrap;
        font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif;
      ">
        🏗 裸金属服务器 →
      </a>
    </td>
    <td align="center">
      <a href="./docs/guide/dev-environment.md" style="
        display: inline-block;
        background: #6c757d;
        color: white;
        padding: 12px 28px;
        border-radius: 8px;
        font-size: 15px;
        font-weight: bold;
        text-decoration: none;
        white-space: nowrap;
        font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif;
      ">
        💻 开发环境 →
      </a>
      <br/>
      <sup>⚠️ <b>不推荐——性能较差</b></sup>
    </td>
  </tr>
</table>

### 🔍 深入探索

- 📖 [文档首页](./docs/index.md) - 完整指南与 API 参考
- 🔧 [模板概念](./docs/guide/templates.md) - 镜像到模板的概念与工作流
- 🌟 [示例项目](./docs/guide/tutorials/examples.md) - 动手实践案例（代码执行、浏览器自动化、OpenClaw 集成、强化学习训练等）
- 📂 [`examples/`](./examples/) - 可运行的示例代码，涵盖 Shell 命令、文件操作、网络策略、暂停/恢复等功能
- 💻 [开发环境 (QEMU VM)](./docs/guide/dev-environment.md) - 无 KVM？快速启动一个临时虚拟机并在其中运行 Cube Sandbox
- ☁️ [PVM 部署](./docs/guide/pvm-deploy.md) - 在普通云虚拟机上部署，无需裸金属或嵌套虚拟化

## 🏗 架构设计

<p align="center">
  <img src="docs/assets/cube-sandbox-arch.png" alt="Cube Sandbox Architecture" />
</p>

| 组件 | 职责 |
|---|---|
| **CubeAPI** | 高并发 REST API 网关（Rust），兼容 E2B。更换 URL 即可无缝迁移。 |
| **CubeMaster** | 集群编排器。接收 API 请求并将其分发至对应的 Cubelet。管理资源调度与集群状态。 |
| **CubeProxy** | 反向代理，兼容 E2B 协议，将请求路由到相应的沙箱实例。 |
| **Cubelet** | 计算节点本地调度组件。管理该节点上所有沙箱实例的完整生命周期。 |
| **CubeVS** | 基于 eBPF 的虚拟交换机，提供内核级网络隔离与安全策略执行。 |
| **CubeHypervisor & CubeShim** | 虚拟化层 —— CubeHypervisor 管理 KVM MicroVMs，CubeShim 实现 containerd Shim v2 API 以将沙箱集成至容器运行时。 |

👉 更多细节请参阅 [架构设计文档](./docs/architecture/overview.md) 和 [CubeVS 网络模型](./docs/architecture/network.md)。

## 🤝 社区与贡献

我们欢迎任何形式的贡献——无论是提交 Bug 报告、功能建议、文档改进，还是代码提交！

- 🐞 **发现 Bug 或有疑问？** 请在 <a href="https://github.com/tencentcloud/CubeSandbox/issues" target="_blank">GitHub Issues</a> 提交 Issue。
- 💡 **有新想法？** 欢迎在 <a href="https://github.com/tencentcloud/CubeSandbox/discussions" target="_blank">GitHub Discussions</a> 参与讨论。
- 🛠️ **想贡献代码？** 请查阅我们的 <a href="./CONTRIBUTING.md" target="_blank">CONTRIBUTING.md</a> 了解如何提交 Pull Request。
- 📝 **想贡献文档？** 欢迎向社区文档频道提交双语 PR：<a href="./docs/guide/troubleshooting/index.md" target="_blank">故障排查</a>、<a href="./docs/guide/usecases/index.md" target="_blank">应用场景</a> 和 <a href="./docs/guide/integrations/index.md" target="_blank">集成指南</a>。
- 💬 **想交流？** 欢迎加入我们的 <a href="https://discord.gg/kkapzDXShb" target="_blank">Discord</a> 频道。

## 📜 开源协议

CubeSandbox 基于 [Apache License 2.0](./LICENSE) 开源协议发布。

CubeSandbox 的诞生得益于众多开源巨人的贡献。特别感谢 [Cloud Hypervisor](https://github.com/cloud-hypervisor/cloud-hypervisor)、[Kata Containers](https://github.com/kata-containers/kata-containers)、virtiofsd、containerd-shim-rs、ttrpc-rust 等项目。我们对部分组件进行了适配修改以契合 CubeSandbox 的执行模型，并保留了原始文件的版权声明。
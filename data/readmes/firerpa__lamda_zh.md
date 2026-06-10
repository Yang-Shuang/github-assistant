# **FIRERPA Android** ｜ AI 赋能自动化

<img src="image/logo.svg" alt="FIRERPA" width="200" align="right" />

<p>
<img src="https://img.shields.io/badge/python-3.6+-blue.svg?logo=python&labelColor=yellow" />
<img src="https://img.shields.io/badge/android-6.0+-blue.svg?logo=android&labelColor=white" />
<img src="https://img.shields.io/badge/root%20require-red.svg?logo=android&labelColor=black" />
<img src="https://img.shields.io/github/downloads/rev1si0n/lamda/total" />
<img src="https://img.shields.io/badge/Built--in%20MCP-000.svg?logo=anthropic&labelColor=black" />
</p>

<h6>一款集成的新一代 Android 自动化框架，将强大的端侧服务与面向 AI 的 Agent（智能体）及可扩展的工具调用能力深度融合。</h6>

<p align="left"><a href="https://device-farm.com/docs/en/">英文文档</a> | <a href="https://device-farm.com/docs/zh/">使用文档</a> | <a href="https://t.me/lamda_dev">TELEGRAM</a> | <a href="https://device-farm.com/llms.txt">llms.txt</a> | <a href="https://device-farm.com/llms-full.txt">llms-full.txt</a></p>

<h3>核心能力</h3>

FIRERPA 是一款轻量级的 Android 端侧自动化技术栈，无需任何外部依赖。它将低延迟的远程桌面与 160+ 项 API（涵盖设备发现/状态/日志、系统与应用控制、UI 自动化、OCR/图像匹配、文件读写、存储、任务调度及 Shell 执行）统一整合，并支持通过 Hub/FRP/OpenVPN 实现分布式部署。内置 ADB/SSH/SCP、日志记录、API 锁机制、证书管理、脚本加密、代理/VPN/MITM（中间人协议）工具，以及逆向辅助功能（Frida 持久化/导出/报告生成、IDA 调试、二进制补丁），全面覆盖生产级工作流。同时原生支持 MCP/Agent 工具调用与扩展能力。

<p align="center">
<img src="https://raw.githubusercontent.com/wiki/firerpa/lamda/images/banner.gif" alt="MCP" width="100%">
</p>

<h3>部署与稳定性</h3>

FIRERPA 可在 Android 6.0 至 16（含模拟器与云手机）环境下提供稳定的自动化能力。框架采用无侵入式设计，无需复杂配置即可运行；支持 Root 环境下的长期后台服务，并提供完整的安装/升级/卸载流程及可重复的生命周期控制机制。

<h3>160+ API 与 Python SDK</h3>

FIRERPA 提供覆盖系统配置、应用/进程控制、UI 元素选择器与手势操作、文件读写、加密键值存储、OCR 及图像匹配的丰富 API。Python SDK 完整映射底层接口，并提供更高层级的辅助函数，助你快速构建可靠的自动化流程。

<p align="center">
<img src="image/inspect.png" alt="demo" width="100%">
</p>

<h3>远程桌面与诊断</h3>

以极简配置实现设备的可视化监控与控制。内置文件上传/下载、WebSocket 视频流（支持 MJPEG/H.264）、触控同步、UI 审查及事件监听，满足自动化验证与实时诊断需求。

<p align="center">
<img src="image/demo.gif" alt="demo" width="100%">
</p>

---

为防止对抗成本攀升，本项目并未完全开源。我们承诺持续为社区提供免费版本。项目保证不含任何恶意代码；欢迎你对项目进行逆向工程与安全分析。如需企业级支持，请参阅我们的[隐私政策](https://device-farm.com/privacy)或[联系我们](https://device-farm.com/contact)。
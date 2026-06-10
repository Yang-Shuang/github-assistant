# 🎯 Claude Code Usage Monitor
[![PyPI Version](https://img.shields.io/pypi/v/claude-monitor.svg)](https://pypi.org/project/claude-monitor/)
[![Python Version](https://img.shields.io/badge/python-3.9+-blue.svg)](https://python.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)
[![codecov](https://codecov.io/gh/Maciek-roboblog/Claude-Code-Usage-Monitor/branch/main/graph/badge.svg)](https://codecov.io/gh/Maciek-roboblog/Claude-Code-Usage-Monitor)

一个用于 Claude AI 令牌（token）使用情况的精美实时终端监控工具，具备高级分析、基于机器学习的预测功能以及 Rich UI。追踪你的令牌消耗量、燃烧率（burn rate）、成本分析，并获得关于会话限制的智能预测。

![Claude Token Monitor Screenshot](https://raw.githubusercontent.com/Maciek-roboblog/Claude-Code-Usage-Monitor/main/doc/scnew.png)

---

## 📑 目录

- [✨ 核心功能](#-key-features)
- [🚀 安装指南](#-installation)
  - [⚡ 使用 uv 进行现代安装（推荐）](#-modern-installation-with-uv-recommended)
  - [📦 使用 pip 安装](#-installation-with-pip)
  - [🛠️ 其他包管理器](#️-other-package-managers)
- [📖 使用方法](#-usage)
  - [获取帮助](#get-help)
  - [基础用法](#basic-usage)
  - [配置选项](#configuration-options)
  - [可用套餐（Plans）](#available-plans)
- [🙏 请协助测试此版本！](#-please-help-test-this-release)
- [✨ 功能详解与工作原理](#-features--how-it-works)
  - [当前功能](#current-features)
  - [理解 Claude 会话机制](#understanding-claude-sessions)
  - [各套餐令牌限制](#token-limits-by-plan)
  - [智能检测特性](#smart-detection-features)
- [🚀 使用示例](#-usage-examples)
  - [常见场景](#common-scenarios)
  - [最佳实践](#best-practices)
- [🔧 开发环境安装](#-development-installation)
- [故障排除](#troubleshooting)
  - [安装问题](#installation-issues)
  - [运行时问题](#runtime-issues)
- [📞 联系方式](#-contact)
- [📚 附加文档](#-additional-documentation)
- [📝 许可证](#-license)
- [🤝 贡献者](#-contributors)
- [🙏 致谢](#-acknowledgments)



## ✨ 核心功能

### 🚀 **v3.0.0 重大更新 - 完整架构重构**

- **🔮 基于机器学习的预测** - P90 百分位计算与智能会话限制检测
- **🔄 实时监控** - 可配置的刷新率（0.1-20 Hz）配合智能显示更新
- **📊 高级 Rich UI** - 美观的彩色进度条、表格和布局，符合 WCAG 对比度标准
- **🤖 智能自动检测** - 自动切换套餐并自定义限制发现机制
- **📋 增强型套餐支持** - 更新后的限制：Pro（44k）、Max5（88k）、Max20（220k）、Custom（基于 P90）
- **⚠️ 高级警告系统** - 多级警报配合成本与时间预测
- **💼 专业架构设计** - 模块化设计，符合单一职责原则（Single Responsibility Principle, SRP）
- **🎨 智能主题适配** - 科学配色方案，自动检测终端背景色
- **⏰ 高级调度功能** - 自动检测系统时区与时间格式偏好
- **📈 成本分析** - 按模型定价，支持缓存令牌（cache token）计算
- **🔧 Pydantic 验证** - 类型安全的配置管理，内置自动校验
- **📝 全面日志记录** - 可选文件日志输出，支持可配置的日志级别
- **🧪 广泛测试覆盖** - 100+ 测试用例，实现全量覆盖
- **🎯 错误报告** - 可选 Sentry 集成，用于生产环境监控
- **⚡ 性能优化** - 高级缓存机制与高效数据处理

### 📋 默认自定义套餐（Custom Plan）

**Custom 套餐** 现已成为默认选项，专为 5 小时长的 Claude Code 会话设计。它监控三个关键指标：
- **令牌使用量** - 追踪你的令牌消耗情况
- **消息数量** - 监控对话轮次计数
- **成本用量** - 长会话中最核心的指标

Custom 套餐会根据你的实际使用习惯自动调整限制。它会分析你过去 192 小时（8天）内的所有会话数据，并基于真实使用情况计算个性化限额。这能确保预测和警告精准贴合你的具体工作流。


## 🚀 安装指南
### ⚡ 使用 uv 进行现代安装（推荐）

**为什么 uv 是最佳选择：**
- ✅ 自动创建隔离环境（避免系统冲突）
- ✅ 无 Python 版本兼容问题
- ✅ 不会出现 "externally-managed-environment" 错误
- ✅ 更新与卸载极其方便
- ✅ 全平台通用

安装并使用该监控工具的最快方式：

[![PyPI](https://img.shields.io/pypi/v/claude-monitor.svg)](https://pypi.org/project/claude-monitor/)

#### 从 PyPI 安装

```bash
# 使用 uv 直接从 PyPI 安装（最简便）
uv tool install claude-monitor

# 在任何位置运行
claude-monitor  # 或使用缩写 cmonitor、ccmonitor
```


#### 从源码安装

```bash
# 克隆并安装源码
git clone https://github.com/Maciek-roboblog/Claude-Code-Usage-Monitor.git
cd Claude-Code-Usage-Monitor
uv tool install .

# 在任何位置运行
claude-monitor
```


#### uv 首次使用者指南
如果你尚未安装 uv，只需一条命令即可获取：

```bash
# Linux/macOS:
curl -LsSf https://astral.sh/uv/install.sh | sh

# Windows:
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"

# 安装完成后，请重启终端
```


### 📦 使用 pip 安装

```bash
# 从 PyPI 安装
pip install claude-monitor

# 如果提示找不到 claude-monitor 命令，请将 ~/.local/bin 添加到 PATH：
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc  # 或重启终端

# 在任何位置运行
claude-monitor  # 或使用缩写 cmonitor、ccmonitor
```


>
> **⚠️ PATH 配置说明**：如果你看到 `WARNING: The script claude-monitor is installed in '/home/username/.local/bin' which is not on PATH`，请执行上述 `export PATH` 命令。
>
> **⚠️ 重要提示**：在现代 Linux 发行版（Ubuntu 23.04+、Debian 12+、Fedora 38+）上，你可能会遇到 "externally-managed-environment" 错误。我们强烈建议不要使用 `--break-system-packages`，而是采用以下方案：
> 1. **改用 uv**（见上文）- 更安全且便捷
> 2. **使用虚拟环境** - `python3 -m venv myenv && source myenv/bin/activate`
> 3. **使用 pipx** - `pipx install claude-monitor`
>
> 详细解决方案请参阅故障排除章节。

### 🛠️ 其他包管理器

#### pipx（隔离环境）
```bash
# 使用 pipx 安装
pipx install claude-monitor

# 在任何位置运行
claude-monitor  # 或 claude-code-monitor、cmonitor、ccmonitor、ccm
```


#### conda/mamba
```bash
# 在 conda 环境中通过 pip 安装
pip install claude-monitor

# 在任何位置运行
claude-monitor  # 或使用缩写 cmonitor、ccmonitor
```


## 📖 使用方法

### 获取帮助

```bash
# 显示帮助信息
claude-monitor --help
```

#### 可用的命令行参数

| 参数 | 类型 | 默认值 | 描述 |
|-----------|------|---------|-------------|
| --plan | string | custom | 套餐类型：pro、max5、max20 或 custom |
| --custom-limit-tokens | int | None | Custom 套餐的令牌上限（必须 > 0） |
| --view | string | realtime | 视图模式：realtime、daily 或 monthly |
| --timezone | string | auto | 时区（自动检测）。示例：UTC、America/New_York、Europe/London |
| --time-format | string | auto | 时间格式：12h、24h 或 auto |
| --theme | string | auto | 显示主题：light、dark、classic 或 auto |
| --refresh-rate | int | 10 | 数据刷新间隔（秒），范围 1-60 |
| --refresh-per-second | float | 0.75 | 界面刷新频率（Hz），范围 0.1-20.0 |
| --reset-hour | int | None | 每日重置时间（0-23） |
| --log-level | string | INFO | 日志级别：DEBUG、INFO、WARNING、ERROR、CRITICAL |
| --log-file | path | None | 日志文件路径 |
| --debug | flag | False | 启用调试日志 |
| --version, -v | flag | False | 显示版本信息 |
| --clear | flag | False | 清除已保存的配置 |

#### 套餐选项

| 套餐 | 令牌限制 | 成本上限       | 描述 |
|------|-------------|------------------|-------------|
| pro | 19,000 | $18.00           | Claude Pro 订阅版 |
| max5 | 88,000 | $35.00           | Claude Max5 订阅版 |
| max20 | 220,000 | $140.00          | Claude Max20 订阅版 |
| custom | P90动态计算 | (默认) $50.00 | 自动检测配合 ML 分析 |

#### 命令别名

该工具支持通过以下任意命令调用：
- claude-monitor（主命令）
- claude-code-monitor（完整名称）
- cmonitor（短别名）
- ccmonitor（短别名变体）
- ccm（最短别名）

#### 参数持久化保存功能

监控工具会自动将你的偏好设置保存到本地，避免每次运行都重新指定：

**会被保存的内容：**
- 视图模式 (--view)
- 主题偏好 (--theme)
- 时区设置 (--timezone)
- 时间格式 (--time-format)
- 刷新率 (--refresh-rate, --refresh-per-second)
- 重置小时数 (--reset-hour)
- 自定义令牌上限 (--custom-limit-tokens)

**配置保存位置：** ~/.claude-monitor/last_used.json

**使用示例：**
```bash
# 首次运行 - 指定偏好设置
claude-monitor --plan pro --theme dark --timezone "America/New_York"

# 后续运行 - 自动恢复已保存的设置
claude-monitor --plan pro

# 本次会话覆盖已保存的设置
claude-monitor --plan pro --theme light

# 清除所有已保存的偏好设置
claude-monitor --clear
```

**核心特性：**
- ✅ 跨会话自动持久化参数
- ✅ CLI 命令行参数始终优先于本地配置
- ✅ 原子文件操作防止配置文件损坏
- ✅ 配置文件损坏时优雅降级 fallback
- ✅ plan 参数永不保存（每次必须显式指定）

### 基础用法

#### 使用 uv tool 安装（推荐）
```bash
# 默认模式（Custom 套餐配合自动检测）
claude-monitor

# 替代命令
claude-code-monitor  # 完整描述性名称
cmonitor             # 短别名
ccmonitor            # 短别名变体
ccm                  # 最短别名

# 退出监控工具
# 按 Ctrl+C 优雅退出
```

#### 开发模式运行
如果从源码直接运行，请在 src/ 目录下使用 `python -m claude_monitor`。

### 配置选项

#### 指定你的套餐

```bash
# Custom 套餐配合 P90 自动检测（默认）
claude-monitor --plan custom

# Pro 套餐（约 44,000 令牌）
claude-monitor --plan pro

# Max5 套餐（约 88,000 令牌）
claude-monitor --plan max5

# Max20 套餐（约 220,000 令牌）
claude-monitor --plan max20

# Custom 套餐配合显式令牌上限
claude-monitor --plan custom --custom-limit-tokens 100000
```

#### 自定义重置时间

```bash
# 在凌晨 3 点重置
claude-monitor --reset-hour 3

# 在晚上 10 点重置
claude-monitor --reset-hour 22
```

#### 视图模式配置

```bash
# 实时监控配合动态更新（默认）
claude-monitor --view realtime

# 按日聚合的令牌使用量表格视图
claude-monitor --view daily

# 按月聚合的令牌使用量表格视图
claude-monitor --view monthly

```

#### 性能与显示配置

```bash
# 调整数据刷新间隔（1-60秒，默认：10）
claude-monitor --refresh-rate 5

# 调整界面渲染频率（0.1-20 Hz，默认：0.75）
claude-monitor --refresh-per-second 1.0

# 设置时间格式（默认自动检测）
claude-monitor --time-format 24h  # 或 12h

# 强制指定主题
claude-monitor --theme dark  # light、dark、classic、auto

# 清除已保存的配置
claude-monitor --clear
```

#### 时区配置

默认时区为**从你的系统自动检测**。你可以通过任意有效时区覆盖：

```bash
# 使用美国东部时间
claude-monitor --timezone America/New_York

# 使用东京时间
claude-monitor --timezone Asia/Tokyo

# 使用 UTC
claude-monitor --timezone UTC

# 使用伦敦时间
claude-monitor --timezone Europe/London
```

#### 日志与调试配置

```bash
# 启用调试日志
claude-monitor --debug

# 输出到文件
claude-monitor --log-file ~/.claude-monitor/logs/monitor.log

# 设置日志级别
claude-monitor --log-level WARNING  # DEBUG、INFO、WARNING、ERROR、CRITICAL
```

### 可用套餐（Plans）

| 套餐 | 令牌限制     | 适用场景 |
|------|-----------------|----------|
| **custom** | P90 自动检测 | 智能限额检测（默认） |
| **pro** | ~19,000         | Claude Pro 订阅版 |
| **max5** | ~88,000         | Claude Max5 订阅版 |
| **max20** | ~220,000        | Claude Max20 订阅版 |

#### 高级套餐特性

- **P90 分析**：Custom 套餐基于你的历史使用记录计算第 90 百分位数
- **成本追踪**：按模型定价，支持缓存令牌（cache token）费用计算
- **限制检测**：智能阈值检测，置信度达 95%


## 🚀 v3.0.0 新增内容

### 主要变更

#### **完整架构重构**
- 模块化设计，符合单一职责原则（SRP）
- 基于 Pydantic 的配置管理，具备类型安全与自动校验
- 高级错误处理机制，支持可选的 Sentry 集成
- 全面测试套件，包含 100+ 测试用例

#### **功能增强**
- **P90 分析**：基于机器学习的限制检测，采用第 90 百分位计算
- **更新套餐限额**：Pro（44k）、Max5（88k）、Max20（220k）令牌
- **成本分析**：按模型定价配合缓存令牌计算
- **Rich UI**：符合 WCAG 标准，支持自动终端背景检测

#### **新增 CLI 选项**
- --refresh-per-second：可配置界面刷新率（0.1-20 Hz）
- --time-format：自动识别 12h/24h 格式
- --custom-limit-tokens：Custom 套餐显式令牌上限
- --log-file 与 --log-level：高级日志功能
- --clear：重置已保存配置
- 命令别名：claude-code-monitor、cmonitor、ccmonitor、ccm 方便调用

#### **破坏性变更（Breaking Changes）**
- 包名从 claude-usage-monitor 更改为 claude-monitor
- 默认套餐从 pro 改为 custom（带自动检测）
- Python 最低版本提升至 3.9+
- CLI 结构更新（参见上方示例）


## ✨ 功能详解与工作原理

### v3.0.0 架构概览

新版本采用完整重构的模块化架构，严格遵循单一职责原则（SRP）：

### 🖥️ 用户界面层

| 组件            | 描述           |
| -------------------- | --------------------- |
| **CLI 模块**       | 基于 Pydantic        |
| **Settings/Config**  | 类型安全             |
| **Error Handling**   | 兼容 Sentry          |
| **Rich Terminal UI** | 自适应主题         |

---

### 🎛️ 监控编排器（Monitoring Orchestrator）

| 组件                | 核心职责                                             |
| ------------------------ | ---------------------------------------------------------------- |
| **Central Control Hub**  | 会话管理 · 实时数据流 · 组件协调      |
| **Data Manager**         | 缓存管理 · 文件 I/O · 状态持久化           |
| **Session Monitor**      | 实时监控 · 5小时窗口 · 令牌追踪           |
| **UI Controller**        | Rich 渲染 · 进度条 · 主题系统                     |
| **Analytics**            | P90 计算 · 消耗率分析 · 预测引擎                        |

---

### 🏗️ 基础层（Foundation Layer）

| 组件           | 核心功能                                           |
| ------------------- | ------------------------------------------------------- |
| **Core Models**     | 会话数据模型 · 配置 Schema · 类型安全             |
| **Analysis Engine** | ML 算法 · 统计分析 · 预测引擎              |
| **Terminal Themes** | 自动检测 · WCAG 配色 · 对比度优化            |
| **Claude API Data** | 令牌追踪 · 成本计算器 · 会话区块解析      |

---

**🔄 数据流向：**
Claude 配置文件 → 数据层 → 分析引擎 → UI 组件 → 终端显示


### 当前功能

#### 🔄 高级实时监控
- 可配置的更新间隔（1-60秒）
- 高精度界面刷新（0.1-20 Hz）
- 智能变更检测以最小化 CPU 占用
- 多线程编排配合回调系统

#### 📊 Rich UI 组件
- **进度条**：符合 WCAG 标准的配色方案与科学对比度
- **数据表格**：可排序列，展示按模型划分的统计信息
- **布局管理器**：响应式设计，自动适配终端窗口大小
- **主题系统**：自动检测终端背景色以优化可读性

#### 📈 多视图模式
- **实时视图（Realtime）**（默认）：动态进度条、当前会话数据与消耗率分析
- **每日视图（Daily）**：按日聚合统计，展示日期、模型、输入/输出/缓存令牌、总令牌数及成本
- **每月视图（Monthly）**：按月聚合数据，用于长期趋势分析与预算规划

#### 🔮 机器学习预测
- **P90 计算器**：基于第 90 百分位的智能限制检测
- **消耗率分析（Burn Rate Analytics）**：多会话消费模式分析
- **成本预估**：按模型定价配合缓存令牌计算
- **会话预测**：根据使用习惯预测会话耗尽时间

#### 🤖 智能自动检测
- **背景检测**：自动识别终端主题（亮色/暗色）
- **系统集成**：自动检测时区与时间格式偏好
- **套餐识别**：分析使用模式并推荐最优套餐
- **限制发现**：扫描历史数据以定位实际令牌上限

### 理解 Claude 会话机制

#### Claude Code 会话工作原理

Claude Code 采用**5小时滚动窗口（rolling session window）系统**：

1. **会话开始**：从你发送第一条消息给 Claude 时启动
2. **会话时长**：自首条消息起精确持续 5 小时
3. **令牌限制**：每个 5 小时窗口内独立计算限额
4. **多会话并行**：可同时存在多个活跃会话
5. **滚动机制**：新会话可在其他会话进行中随时启动

#### 会话重置时间线示例

10:30 AM - 发送首条消息（会话 A 于 10:00 AM 开始）
03:00 PM - 会话 A 过期（5小时后）

12:15 PM - 发送首条消息（会话 B 于 12:00 PM 开始）
05:15 PM - 会话 B 过期（5小时后）


#### 消耗率（Burn Rate）计算逻辑

监控工具通过高级分析计算消耗速率：

1. **数据采集**：收集过去一小时内所有会话的令牌使用量
2. **模式分析**：识别重叠会话间的消费趋势
3. **速度追踪**：计算每分钟消耗的令牌数
4. **预测引擎**：估算当前会话令牌耗尽时间
5. **实时更新**：随使用模式变化动态调整预测结果

### 各套餐令牌限制

#### v3.0.0 更新后的套餐限额

| 套餐 | 限制（令牌） | 成本上限       | 消息数 | 算法 |
|------|----------------|------------------|----------|-----------|
| **Claude Pro** | 19,000         | $18.00           | 250 | 固定限额 |
| **Claude Max5** | 88,000         | $35.00           | 1,000 | 固定限额 |
| **Claude Max20** | 220,000        | $140.00          | 2,000 | 固定限额 |
| **Custom** | P90动态计算      | (默认) $50.00 | 250+ | 机器学习 |

#### 高级限制检测机制

- **P90 分析**：基于历史使用记录的第 90 百分位数
- **置信度阈值**：限额检测准确率达 95%
- **缓存支持**：包含缓存创建与读取的令牌成本计算
- **模型适配**：自动兼容 Claude 3.5、Claude 4 及未来版本


### 技术需求

#### 依赖项（v3.0.0）

```toml
# 核心依赖（自动安装）
pytz>=2023.3                # 时区处理
rich>=13.7.0                # Rich 终端 UI
pydantic>=2.0.0             # 类型校验
pydantic-settings>=2.0.0    # 配置管理
numpy>=1.21.0               # 统计分析
sentry-sdk>=1.40.0          # 错误上报（可选）
pyyaml>=6.0                 # 配置文件解析
tzdata                      # Windows 时区数据支持
```

#### Python 版本要求

- **最低版本**：Python 3.9+
- **推荐版本**：Python 3.11+
- **已测试平台**：Python 3.9、3.10、3.11、3.12、3.13

### 智能检测特性

#### 自动套餐切换逻辑

使用默认 Pro 套餐时，工具会执行以下流程：

1. **触发检测**：当令牌消耗超过 7,000 时启动监控
2. **历史扫描**：分析过往会话以定位实际上限
3. **自动切换**：无缝切换至 custom_max 模式
4. **状态通知**：在终端清晰显示切换提示
5. **持续监控**：基于新限额继续跟踪

#### 限制发现流程

自动检测系统的工作机制：

1. **历史扫描**：检查所有可用的会话区块数据
2. **峰值识别**：找出已实现的最大令牌使用量
3. **数据校验**：确保数据质量与时效性
4. **上限设定**：将发现的峰值作为新限额基准
5. **模式学习**：自适应你的实际使用能力


## 🚀 使用示例

### 常见场景

#### 🌅 晨型开发者
**场景**：你通常在上午 9 点开始工作，希望令牌重置时间与工作节奏对齐。

```bash
# 设置自定义重置时间为早上 9 点
./claude_monitor.py --reset-hour 9

# 配合你的时区使用
./claude_monitor.py --reset-hour 9 --timezone US/Eastern
```


**优势**：
- 重置时间与你工作日程同步
- 更精准规划每日令牌分配
- 会话窗口可预测性强

#### 🌙 夜猫子程序员
**场景**：你经常熬夜编码，需要灵活的重置时间安排。

```bash
# 在午夜重置以划分清晰的日边界
./claude_monitor.py --reset-hour 0

# 晚间延迟重置（晚上 11 点）
./claude_monitor.py --reset-hour 23
```


**策略建议**：
- 围绕重置时间安排高强度编码任务
- 使用晚段重置跨越午夜工作时段
- 在高峰时段密切监控消耗率

#### 🔄 高用量且限额波动用户
**场景**：你的令牌限制似乎经常变化，不确定确切套餐档位。

```bash
# 自动检测历史最高使用量
claude-monitor --plan custom_max

# 配合自定义调度进行监控
claude-monitor --plan custom_max --reset-hour 6
```


**操作建议**：
- 让自动检测定位真实限额
- 连续监控一周以掌握波动规律
- 记录限额变化或重置节点

#### 🌍 跨国/出差用户
**场景**：你在不同国家工作，需要跨时区管理会话。

```bash
# 美国东海岸
claude-monitor --timezone America/New_York

# 欧洲
claude-monitor --timezone Europe/London

# 亚太
claude-monitor --timezone Asia/Singapore

# UTC 用于跨国团队协调
claude-monitor --timezone UTC --reset-hour 12
```


#### ⚡ 快速查看
**场景**：你只想快速查看当前状态，无需额外配置。

```bash
# 直接运行默认模式
claude-monitor

# 检查完毕后按 Ctrl+C 退出
```

#### 📊 使用量分析视图
**场景**：你需要分析不同时间维度的令牌消耗模式。

```bash
# 查看每日用量明细与详细统计
claude-monitor --view daily

# 分析月度令牌消费趋势
claude-monitor --view monthly --plan max20

# 导出每日数据至日志文件供后续分析
claude-monitor --view daily --log-file ~/daily-usage.log

# 切换时区查看用量记录
claude-monitor --view daily --timezone America/New_York
```

**适用场景**：
- **实时视图（Realtime）**：当前会话监控与消耗率追踪
- **每日视图（Daily）**：分析日常消费模式，识别高峰日
- **每月视图（Monthly）**：长期趋势分析与月度预算规划


### 套餐选择策略

#### 如何选择合适的套餐

**新手推荐从默认值开始**
```bash
# Pro 套餐检测配合自动切换
claude-monitor
```

- 监控工具会自动检测是否超出 Pro 限额
- 若超限则自动切换至 custom_max
- 切换时会显示明确提示通知

**已知订阅用户**
```bash
# 如果你确认持有 Max5 订阅
claude-monitor --plan max5

# 如果你确认持有 Max20 订阅
claude-monitor --plan max20
```


**不确定限额的用户**
```bash
# 基于历史使用记录自动检测
claude-monitor --plan custom_max
```


### 最佳实践

#### 环境配置建议

1. **尽早启动监控**

```bash
   # 在开始 Claude 工作时立即启动（uv 安装方式）
   claude-monitor

   # 或开发模式运行
   ./claude_monitor.py
   ```

   - 从会话起点即获得精准追踪
   - 消耗率计算更准确
   - 提前预警限额临界点

2. **采用现代安装方式（推荐）**

```bash
   # 使用 uv 实现便捷安装与更新
   uv tool install claude-monitor
   claude-monitor --plan max5
   ```

   - 系统环境干净无污染
   - 升级维护极其方便
   - 终端任意路径可直接调用

3. **自定义 Shell 别名（传统开发配置）**

```bash
   # 添加至 ~/.bashrc 或 ~/.zshrc（仅适用于开发环境）
   alias claude-monitor='cd ~/Claude-Code-Usage-Monitor && source venv/bin/activate && ./claude_monitor.py'
   ```


#### 使用建议

1. **密切关注消耗速率**
   - 留意令牌消耗的突增情况
   - 根据剩余时间动态调整编码强度
   - 将大型重构任务安排在会话重置前后

2. **战略性规划会话周期**

```bash
   # 围绕重置时间安排高负载任务
   claude-monitor --reset-hour 9
   ```

   - 大任务放在重置后执行
   - 接近限额时切换轻量级任务
   - 善用多会话重叠机制

3. **保持时区一致性**

```bash
   # 始终使用你所在地的真实时区
   claude-monitor --timezone Europe/Warsaw
   ```

   - 重置时间预测更准确
   - 更好匹配个人工作节奏
   - 会话过期预估更可靠

#### 优化技巧

1. **终端环境配置**
   - 使用宽度至少 80 字符的终端窗口
   - 启用颜色支持以获得更好的视觉反馈（检查 COLORTERM 环境变量）
   - 建议为监控工具分配独立终端窗口
   - 选用支持 truecolor 的终端以最佳展示主题效果

2. **工作流集成**

```bash
   # 配合开发会话启动监控（uv 安装方式）
   tmux new-session -d -s claude-monitor 'claude-monitor'

   # 或开发模式运行
   tmux new-session -d -s claude-monitor './claude_monitor.py'

   # 随时查看状态
   tmux attach -t claude-monitor
   ```


3. **多会话策略**
   - 牢记每个会话精确持续 5 小时
   - 可同时运行多个重叠会话
   - 合理跨会话边界规划任务优先级

#### 真实工作流示例

**大型项目开发**
```bash
# 配置长时间开发环境
claude-monitor --plan max20 --reset-hour 8 --timezone America/New_York
```


**日常流程**：
1. **上午 8:00**：令牌刷新，启动核心功能开发
2. **上午 10:00**：检查消耗率，调整编码节奏
3. **中午 12:00**：监控下午时段规划进度
4. **下午 2:00**：新会话窗口开启，攻坚复杂逻辑
5. **下午 4:00**：处理轻量任务，为晚间会话做准备

**学习与实验场景**
```bash
# 灵活配置用于学习探索
claude-monitor --plan pro
```


**敏捷冲刺开发**
```bash
# 高强度开发环境配置
claude-monitor --plan max20 --reset-hour 6
```


## 🔧 开发环境安装

面向贡献者与希望修改源码的开发者：

### 快速开始（开发/测试）

```bash
# 克隆仓库
git clone https://github.com/Maciek-roboblog/Claude-Code-Usage-Monitor.git
cd Claude-Code-Usage-Monitor

# 以开发模式安装依赖
pip install -e .

# 从源码运行
python -m claude_monitor
```


### v3.0.0 测试功能

新版本内置了全面的自动化测试套件：

- **100+ 测试用例**，实现全量覆盖
- **单元测试** 覆盖所有核心组件
- **集成测试** 验证端到端工作流
- **性能基准测试** 评估优化效果
- **Mock 对象隔离** 支持独立模块测试

```bash
# 运行全部测试
cd src/
python -m pytest

# 生成覆盖率报告
python -m pytest --cov=claude_monitor --cov-report=html

# 运行指定测试模块
python -m pytest tests/test_analysis.py -v
```


### 前置条件

1. **Python 3.9+** 已安装至系统
2. **Git** 用于克隆代码仓库


### 虚拟环境配置指南

#### 为什么推荐使用虚拟环境？

使用虚拟环境是**强烈建议**的做法，原因如下：

- **🛡️ 环境隔离**：保持系统 Python 纯净，避免依赖冲突
- **📦 跨平台移植**：轻松在不同机器上复现完全一致的环境
- **🔄 版本锁定**：固定依赖包版本以确保稳定性
- **🧹 干净卸载**：直接删除虚拟环境文件夹即可彻底清理
- **👥 团队协作**：确保所有成员使用相同的 Python 与包版本

#### 安装 virtualenv（如系统未自带）

如果你的系统缺少 venv 模块：

```bash
# Ubuntu/Debian
sudo apt-get update
sudo apt-get install python3-venv

# Fedora/RHEL/CentOS
sudo dnf install python3-venv

# macOS（通常随 Python 自带）
# 若缺失，可通过 Homebrew 安装：
brew install python3

# Windows（通常随 Python 自带）
# 若缺失，请从 python.org 重新安装
# 安装时务必勾选 "Add Python to PATH"
```


或使用 virtualenv 包替代：
```bash
# 通过 pip 安装 virtualenv
pip install virtualenv

# 随后创建虚拟环境：
virtualenv venv
# 替代命令：python3 -m venv venv
```


#### 逐步配置指南

```bash
# 1. 克隆仓库
git clone https://github.com/Maciek-roboblog/Claude-Code-Usage-Monitor.git
cd Claude-Code-Usage-Monitor

# 2. 创建虚拟环境
python3 -m venv venv
# 若使用 virtualenv 包：
# virtualenv venv

# 3. 激活虚拟环境
# Linux/Mac:
source venv/bin/activate
# Windows:
# venv\Scripts\activate

# 4. 安装 Python 依赖
pip install pytz
pip install rich>=13.0.0
# 5. 赋予脚本执行权限（仅 Linux/Mac）
chmod +x claude_monitor.py

# 6. 启动监控工具
python claude_monitor.py
```


#### 日常使用流程

完成初始配置后，你只需：

```bash
# 进入项目目录
cd Claude-Code-Usage-Monitor

# 激活虚拟环境
source venv/bin/activate  # Linux/Mac
# venv\Scripts\activate   # Windows

# 运行监控工具
./claude_monitor.py  # Linux/Mac
# python claude_monitor.py  # Windows

# 使用完毕后退出
deactivate
```


#### 进阶技巧：Shell 别名

创建快捷访问别名：
```bash
# 添加至 ~/.bashrc 或 ~/.zshrc
alias claude-monitor='cd ~/Claude-Code-Usage-Monitor && source venv/bin/activate && ./claude_monitor.py'

# 之后只需输入：
claude-monitor
```


## 故障排除

### 安装问题

#### "externally-managed-environment" 错误

在现代 Linux 发行版（Ubuntu 23.04+、Debian 12+、Fedora 38+）上，你可能会遇到：
```
error: externally-managed-environment
× This environment is externally managed
```


**解决方案（按推荐优先级排序）**：

1. **使用 uv（强烈推荐）**

```bash
   # 先安装 uv
   curl -LsSf https://astral.sh/uv/install.sh | sh

   # 然后通过 uv 安装
   uv tool install claude-monitor
   ```


2. **使用 pipx（隔离环境方案）**

```bash
   # 安装 pipx
   sudo apt install pipx  # Ubuntu/Debian
   # 或
   python3 -m pip install --user pipx

   # 安装监控工具
   pipx install claude-monitor
   ```


3. **使用虚拟环境**

```bash
   python3 -m venv myenv
   source myenv/bin/activate
   pip install claude-monitor
   ```


4. **强制安装（不推荐）**

```bash
   pip install --user claude-monitor --break-system-packages
   ```

   ⚠️ **警告**：此操作会绕过系统保护机制，可能引发依赖冲突。我们强烈建议优先使用虚拟环境方案。

#### pip 安装后提示找不到命令

如果通过 pip 安装后仍无法识别 `claude-monitor` 命令：

1. **检查是否为 PATH 问题**

```bash
   # 查看 pip install 时的警告信息：
   # WARNING: The script claude-monitor is installed in '/home/username/.local/bin' which is not on PATH
   ```


2. **将路径加入环境变量**

```bash
   # 添加至 ~/.bashrc 或 ~/.zshrc
   echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc

   # 重载 Shell 配置
   source ~/.bashrc  # 或 source ~/.zshrc
   ```


3. **验证安装位置**

```bash
   # 查找 pip 安装的脚本路径
   pip show -f claude-monitor | grep claude-monitor
   ```


4. **通过 Python 模块直接运行**

```bash
   python3 -m claude_monitor
   ```


#### Python 版本冲突

如果系统中存在多个 Python 版本：

1. **检查当前版本**

```bash
   python3 --version
   pip3 --version
   ```


2. **指定特定 Python 版本安装**

```bash
   python3.11 -m pip install claude-monitor
   python3.11 -m claude_monitor
   ```


3. **使用 uv（自动处理版本兼容）**

```bash
   uv tool install claude-monitor
   ```


### 运行时问题

#### No active session found（未找到活跃会话）
如果遇到此错误，请按以下步骤操作：

1. **初始测试**：
   启动 Claude Code 并至少发送两条消息。在某些情况下，首次尝试可能无法正确初始化会话，但经过几次交互后即可恢复正常。

2. **配置路径指定**：
   若问题持续存在，请尝试显式指定自定义配置路径。默认情况下 Claude Code 使用 `~/.config/claude`。根据你的运行环境可能需要调整此路径。

```bash
CLAUDE_CONFIG_DIR=~/.config/claude ./claude_monitor.py
```



## 📞 联系方式

有问题、建议或想参与协作？欢迎随时联系！

**📧 Email**: [maciek@roboblog.eu](mailto:maciek@roboblog.eu)

无论是需要安装协助、功能提议、Bug 反馈，还是探讨潜在改进方案，都请随时与我取得联系。我始终乐于提供帮助并倾听 Claude Code Usage Monitor 用户的声音！


## 📚 附加文档

- **[开发路线图](DEVELOPMENT.md)** - ML 特性、PyPI 包发布、Docker 部署计划
- **[贡献指南](CONTRIBUTING.md)** - 如何参与贡献、开发规范说明
- **[故障排除手册](TROUBLESHOOTING.md)** - 常见问题汇总与解决方案


## 📝 许可证

[MIT License](LICENSE) - 欢迎自由使用并根据需要进行修改。

## 🤝 贡献者

- [@adawalli](https://github.com/adawalli)
- [@taylorwilsdon](https://github.com/taylorwilsdon)
- [@moneroexamples](https://github.com/moneroexamples)

想参与贡献？请查阅我们的 [贡献指南](CONTRIBUTING.md)!


## 🙏 致谢

### 赞助者

特别感谢支持本项目持续发展的伙伴们：

**Ed** - *Buy Me Coffee 支持者*
> "感谢你向世界分享这些作品。它帮助我更好地保持日常专注。文档质量很高，整体内容也非常出色！"

## Star 历史记录

[![Star History Chart](https://api.star-history.com/svg?repos=Maciek-roboblog/Claude-Code-Usage-Monitor&type=Date)](https://www.star-history.com/#Maciek-roboblog/Claude-Code-Usage-Monitor&Date)

---

<div align="center">

**⭐ 如果觉得有用，请给本仓库点星！ ⭐**

[报告 Bug](https://github.com/Maciek-roboblog/Claude-Code-Usage-Monitor/issues) • [功能请求](https://github.com/Maciek-roboblog/Claude-Code-Usage-Monitor/issues) • [参与贡献](CONTRIBUTING.md)

</div>
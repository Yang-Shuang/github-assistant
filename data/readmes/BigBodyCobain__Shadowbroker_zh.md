<p align="center">
  <h1 align="center">🛰️ S H A D O W B R O K E R</h1>
  <p align="center"><strong>全球威胁拦截 —— 实时地理空间情报平台</strong></p>
  <p align="center">

  </p>
</p>

---




[![ShadowBroker](/uploads/46f99d19fa141a2efba37feee9de8aab/Title.jpg)](https://github.com/user-attachments/assets/248208ec-62f7-49d1-831d-4bd0a1fa6852)





**ShadowBroker** 是一个去中心化情报平台，它将来自 60 多个实时情报源的跨领域 OSINT（开源情报）遥测数据聚合到一个单页暗网行动地图界面中。飞机、船只、卫星、冲突区、CCTV 网络、GPS 干扰、联网设备、警用扫描仪、Mesh 无线电节点以及突发地缘政治事件——所有这些都在同一屏幕上实时更新，并配备混淆通信协议和信息交换基础设施。

基于 **Next.js**、**MapLibre GL**、**FastAPI** 和 **Python** 构建。包含 35+ 可切换数据层，包括 SAR（合成孔径雷达）地表变化检测。支持多种视觉模式（DEFAULT / SATELLITE / FLIR / NVG / CRT）。在地球上任意位置右键点击即可获取国家档案、国家元首查询以及最新的 Sentinel-2 卫星照片。ShadowBroker 无需账号，不收集产品遥测数据或分析信息；仪表盘直接与你自托管的后端通信，而可选的实时 OSINT 面板在你使用时会联系其配置好的公共数据提供商。

专为分析师、研究人员、无线电操作员以及希望将一切公开信号映射在同一地图上的任何人设计。


## 项目背景

全球遥测数据中已有相当一部分是公开的——飞机 ADS-B 广播、海事 AIS 信号、卫星轨道数据、地震传感器、Mesh 无线电网络、警用扫描仪频段、环境监测站、互联网基础设施遥测等。这些数据分散在数十种工具和 API 中。ShadowBroker 将它们整合到一个统一的界面中。

本项目不引入新的监控能力——它仅聚合和可视化现有的公共数据集。项目完全开源，任何人都可以审计具体访问了哪些数据以及如何使用。ShadowBroker 不包含产品遥测、分析功能或账号系统。操作员提供的密钥保留在你的本地部署环境中，但实时 OSINT 功能在运行时必然需要向你所启用的公共数据提供商发起出站请求。

### Shodan 连接器

ShadowBroker 包含一个可选的 Shodan 连接器，用于操作员提供的 API 访问。Shodan 结果通过你自己的 `SHODAN_API_KEY` 获取，渲染为本地调查覆盖层（不合并到核心数据源中），并受限于 Shodan 的服务条款。

---

## 典型用例

* **追踪空军一号**、亿万富翁和独裁者的私人喷气机，以及所有广播 ADS-B 的军用加油机、ISR（情报监视侦察）机和战斗机。空军一号及所有随行总统/副总统专机一旦起飞即高亮显示并持续监控。 
* **通过 ShadowBroker 的 HMAC 签名代理命令通道连接 AI 智能体作为协同分析师**——支持 OpenClaw 以及任何遵循该协议的智能体（Claude、GPT、LangChain、自定义）。智能体拥有对所有 35+ 数据层、图钉标记放置、地图控制、SAR 地表变化检测、Mesh 网络及警报推送的完整读写权限。它能看到操作员看到的一切，并能实时在地图上执行操作。
* **在 InfoNet 测试网上通信**——首个内置于 OSINT 工具的去中心化情报 Mesh。配备网关人设（gate personas）的混淆消息、Dead Drop（死投）点对点交换以及内置终端 CLI。无需账号或注册。目前不保证隐私——这是一个实验性测试网，但协议已上线并正在加固中。
* **在地球上任意位置右键点击**获取国家档案（元首、人口、语言）、维基百科摘要以及最新的 10 米分辨率 Sentinel-2 卫星照片。
* **点击 KiwiSDR 节点**直接在仪表盘内调谐收听实时短波无线电。点击警用扫描仪频段一键窃听。
* **观看覆盖 6 个国家的 11,000+ 路 CCTV 摄像头**——伦敦、纽约、加州、西班牙、新加坡等地的实时直播流直接显示在地图上。
* **实时查看 GPS 干扰区域**——基于飞机应答机数据的 NAC-P（导航精度类别）退化分析得出。
* **监控头顶卫星**按任务类型颜色编码——军事侦察、SIGINT（信号情报）、SAR、早期预警、空间站等，结合 SatNOGS 和 TinyGS 地面站网络。
* **追踪海上交通**包括 25,000+ AIS 船舶、Global Fishing Watch 的渔业活动以及亿万富翁的超级游艇。
* **跟踪地震、火山喷发、活跃野火**（NASA FIRMS）、恶劣天气警报及全球空气质量读数。
* **绘制军事基地、35,000+ 发电厂、2,000+ 数据中心和互联网中断区域**——自动交叉引用。
* **连接 Meshtastic Mesh 无线电节点**和 APRS 业余无线电网络——在地图上可见并集成到 Mesh Chat 中。
* **透过云层检测地表变化**使用 SAR（合成孔径雷达）——毫米级地面形变、洪水范围、植被干扰及 NASA OPERA 和 Copernicus EGMS 的损毁评估。可自定义监视区域并获得异常警报。需免费 NASA Earthdata 账号即可免费使用。
* **切换视觉模式**——通过 STYLE 按钮在 DEFAULT、SATELLITE、FLIR（热成像）、NVG（夜视仪）和 CRT（复古终端）之间切换。
* **实时追踪美国（Amtrak）和欧洲（DigiTraffic）的火车**。
* **使用自动化 GDELT 新闻抓取估算美军航母位置**——目前无其他开源工具能做到这一点。
* **通过 Shodan 搜索全球联网设备**——摄像头、SCADA 系统、数据库等，作为实时覆盖层绘制在地图上。


---

## ⚡ 快速启动（Docker）

### From GitHub (default — uses GHCR images)

```bash
git clone https://github.com/bigbodycobain/Shadowbroker.git
cd Shadowbroker
docker compose pull
docker compose up -d
```

### From GitLab (uses GitLab Container Registry)

```bash
git clone https://gitlab.com/bigbodycobain/Shadowbroker.git
cd Shadowbroker
docker compose -f docker-compose.yml -f docker-compose.gitlab.yml pull
docker compose -f docker-compose.yml -f docker-compose.gitlab.yml up -d
```

两种路径生成的容器完全一致——相同源码、相同 CI/CD、二进制镜像逐字节相同。选择你已使用的生态即可。

打开 `http://localhost:3000` 查看仪表盘！*(需 [Docker Desktop](https://www.docker.com/products/docker-desktop/) 或 Docker Engine)*

> **后端端口已被占用？** 浏览器仅需访问 `3000` 端口，但后端 API 也会在宿主机 `8000` 端口发布以供本地诊断。若其他应用已使用 `8000`，请在 `docker-compose.yml` 旁创建或编辑 `.env` 文件并设置 `BACKEND_PORT=8001`，然后运行 `docker compose up -d`。

> **启动几分钟后新闻/UAP（不明空中现象）/基地/废水数据仍为空？** 请检查后端是否因 OOM（内存不足）重启：`docker events --since 30m --filter container=shadowbroker-backend --filter event=oom`。默认 compose 文件为后端分配 4GB 内存；若宿主机内存较小，可禁用部分数据源或设置 `BACKEND_MEMORY_LIMIT=3G`，此时较慢/较重的图层预热会更缓慢。

> **Podman 用户：** Podman 可用，但 `podman compose` 仅为包装器，仍需安装 Compose provider。在 Windows/WSL 下若提示 `looking up compose provider failed`，请安装 `podman-compose` 并在克隆的 `Shadowbroker` 文件夹内运行 `podman-compose pull` 及 `podman-compose up -d`。Linux/macOS/WSL shell 中也可使用 `./compose.sh --engine podman pull` 和 `./compose.sh --engine podman up -d`。

---

## 🔄 **如何更新**

ShadowBroker 使用预构建的 Docker 镜像——无需本地编译。更新仅需数秒：

```bash
docker compose pull
docker compose up -d
```

仅此而已。`pull` 获取最新镜像，`up -d` 重启容器。

> **从旧版本升级？** 请先拉取最新仓库代码，再拉取镜像：
>
> ```bash
> git pull origin main
> docker compose down
> docker compose pull
> docker compose up -d
> ```
>
> Podman 用户应运行等效的 provider 命令，例如 `podman-compose pull` 和 `podman-compose up -d`，或在 bash 兼容 shell 中执行 `./compose.sh --engine podman pull` 及 `./compose.sh --engine podman up -d`。

### 更新完整性验证

Docker 更新通过签名容器镜像仓库分发。遗留的 ZIP 自更新器会通过以下链式顺序校验发布归档：

* `MESH_UPDATE_SHA256`（当操作员显式固定摘要时）。
* `backend/data/release_digests.json`（用于捆绑发布的固定版本）。
* GitHub 上的发布 `SHA256SUMS.txt` 资源文件（当缺少内置固定版本时）。

发布维护者在发布前应运行 `python backend/scripts/release_helper.py hash <ShadowBroker_vX.Y.Z.zip>`，随后在分发 ZIP 更新目标时发布 `SHA256SUMS.txt` 并更新 `backend/data/release_digests.json`。更新器会保留操作员覆盖路径，而非因缺少内置摘要而回退失败，从而避免现有安装因发布流程失误而中断。

### CSP（内容安全策略）加固

生产环境前端附带兼容 hydration 的 CSP 以及 `Content-Security-Policy-Report-Only` 中的严格 nonce-only CSP。仅在确认你的部署中构建能正确 hydration 后，才设置 `SHADOWBROKER_STRICT_CSP=1`。运行时 Google Fonts 非必需；内置 Next.js 字体管线会从应用构建中提供仪表盘所需字体。

### ⚠️ **卡在旧版本无法更新？**

**若 `git pull` 失败或 `docker compose up` 持续从源码构建而非拉取镜像**，说明你的克隆仓库早于 2026 年 3 月的仓库迁移（该迁移重写了提交历史）。常规 `git pull` 无法修复此问题。请运行：

```bash
# 备份你想保留的本地配置（.env 等）
cd ..
rm -rf Shadowbroker
git clone https://github.com/bigbodycobain/Shadowbroker.git
cd Shadowbroker
docker compose pull
docker compose up -d
```

**如何判断是否受影响：** 若 `docker compose up` 显示 `RUN apt-get`、`RUN npm ci` 或 `RUN pip install`，说明正在从源码构建而非拉取预编译镜像。你需要重新克隆仓库。

**其他故障排除：**

* **强制重新拉取：** `docker compose pull --no-cache`
* **清理旧镜像：** `docker image prune -f`
* **查看日志：** `docker compose logs -f backend`

---

### **☸️ Kubernetes / Helm（高级）**

针对高可用部署或家庭实验室集群，ShadowBroker 支持通过 **Helm** 进行部署。该 Chart 基于 `bjw-s-labs` 模板构建，为后端和前端提供健壮、模块化的设置方案。

**1. 添加仓库：**
```bash
helm repo add bjw-s-labs https://bjw-s-labs.github.io/helm-charts/
helm repo update
```

**2. 安装 Chart：**
```bash
# 默认 —— 从 GHCR 拉取镜像
helm install shadowbroker ./helm/chart --create-namespace --namespace shadowbroker

# GitLab 仓库变体
helm install shadowbroker ./helm/chart --create-namespace --namespace shadowbroker \
  -f helm/chart/values.yaml \
  -f helm/chart/values-gitlab.yaml
```

**3. 核心特性：**
*   **模块化架构：** 独立扩展情报后端与 HUD（平视显示器）前端。
*   **安全上下文：** 以受限 UID（1001）运行，增强容器安全性。
*   **Ingress 就绪：** 兼容 Traefik、Cert-Manager 和 Gateway API，为你的情报节点提供安全的外部访问入口。

*特别感谢 [@chr0n1x](https://github.com/chr0n1x) 贡献初始 Kubernetes 架构。*

---

## 实验性测试网 —— 不保证隐私

ShadowBroker v0.9.7 附带 **InfoNet**（去中心化情报 Mesh + 主权 Shell 治理经济）、**代理智能体命令通道**（支持 OpenClaw 及任何 HMAC 签名智能体）、**时光机快照回放**以及 **SAR 卫星地表变化检测**。这是一个 **实验性测试网**——并非私人信使，也非生产级治理系统。

| 频道 | 隐私状态 | 详情 |
|---|---|---|
| **Meshtastic / APRS** | **公开（PUBLIC）** | RF 无线电传输按设计为公开且可拦截的。 |
| **InfoNet Gate Chat** | **混淆（OBFUSCATED）** | 消息通过网关人设和标准载荷签名进行混淆，但**非端到端加密**。尽管架构基于 Tor 和 Reticulum，元数据仍未隐藏（进行中）。 |
| **Dead Drop DMs** | **当前最强通道（STRONGEST CURRENT LANE）** | 基于令牌的纪元邮箱配合 SAS 单词验证。本版本中最强通道，但尚未达到绝对隐私标准。 |
| **Sovereign Shell governance** | **公开账本（PUBLIC LEDGER）** | 请愿、投票、升级哈希及争议质押均为公共哈希链上的签名事件。通过网关人设保持伪匿名，但治理操作有意设为可观测。 |
| **Privacy primitives (RingCT / stealth / DEX)** | **尚未接入（NOT YET WIRED）** | 已锁定协议合约就位，但密码学方案尚未选定。隐私核心 Rust crate 是下一冲刺阶段的集成目标。 |

**切勿在任何频道传输敏感信息。** 目前请将所有通道视为公开开放。端到端加密及更深度的原生/Tauri 加固是下一阶段的里程碑。若你 fork 本项目，请保留这些标签，且不要做出超出实现能力的更强隐私声明。

> **要了解该 Mesh 实际防御了哪些威胁以及未覆盖的范围，请参阅**
> **[威胁模型](docs/mesh/threat-model.md) 和**
> **[主张核对表](docs/mesh/claims-reconciliation.md)。上述每句话均在此处映射到强制执行（或未执行）它的代码路径。**

---


## ✨ 功能特性

### 🧅 InfoNet —— 去中心化情报 Mesh + 主权 Shell（v0.9.7 扩展）

首个直接内置于 OSINT 平台中的去中心化情报通信与治理层。无需账号、注册或身份绑定。v0.9.7 将 InfoNet 从聊天层提升为完整的治理经济，并拥有通往隐私保护型去中心化情报平台的清晰路径。

**通信层（自 v0.9.6）：**

* **InfoNet 实验性测试网** —— 基于 Tor 和 Reticulum 的全球混淆消息中继。任何运行 ShadowBroker 的用户均可在 InfoNet 上收发消息。消息通过 Wormhole 中继层传递，配备网关人设、Ed25519 标准载荷签名及传输混淆。
* **Mesh Chat 面板** —— 三标签界面：**INFONET**（带混淆传输的网关聊天）、**MESH**（Meshtastic 无线电集成）、**DEAD DROP**（基于令牌的纪元邮箱点对点消息交换——当前最强通道）。
* **Gate Persona System** —— 伪匿名身份，配备 Ed25519 签名密钥、预置密钥包、SAS 单词联系人验证及滥用举报机制。
* **Mesh Terminal** —— 内置 CLI：`send`、`dm`、市场命令、网关状态检查。可拖拽面板，最小化至顶栏。输入 `help` 查看所有命令。
* **Crypto Stack** —— Ed25519 签名、X25519 Diffie-Hellman、AESGCM 加密配合 HKDF 密钥派生、哈希链承诺系统。双棘轮 DM 框架开发中。

**Sovereign Shell —— 治理经济（v0.9.7 新增）：**

* **请愿 + 治理 DSL** —— 通过签名请愿进行链上参数变更。支持类型安全的载荷执行器，用于 `UPDATE_PARAM`、`BATCH_UPDATE_PARAMS`、`ENABLE_FEATURE` 和 `DISABLE_FEATURE`。可调节旋钮按投票结果变更——无需代码部署。
* **升级哈希治理（Upgrade-Hash Governance）** —— 需要新逻辑的协议升级通过投票验证发布包的 SHA-256 哈希。80% 超级多数、40% 法定人数、67% Heavy-Node 激活。生命周期：签名 → 投票 → 挑战窗口 → 等待就绪 → 已激活。
* **决议与争议市场** —— 对市场决议结果（是/否/数据不可用）进行质押，使用绑定证据发起争议，并对争议确认或反转进行质押。每行提交状态保持隔离，确保并发操作不共享飞行中槽位。
* **证据提交** —— 客户端 SHA-256 标准化的绑定证据包，与 Python `repr()` 完全匹配，使哈希在链路上往返清晰。
* **网关暂停/关闭/申诉** —— 提供表单用于暂停或关闭网关，并配备可复用的自动定向至待处理请愿的申诉流程。
* **Bootstrap Eligible-Node-One-Vote** —— 前 100 个市场通过“合格节点一票制”而非质押加权决议进行结算。资格标准：身份年龄 ≥ 3 天、不在预测器排除集内、有效 Argon2id PoW（仅限 Heavy-Node）。在达到 1000 节点时过渡到质押决议。
* **双层状态 + 纪元最终性** —— Tier 1 事件以 CRDT 风格传播以实现低延迟；Tier 2 事件需在采取行动前获得纪元最终性。通过 `MappingProxyType` 强制执行身份轮换、渐进式惩罚、爬坡里程碑及宪法不变量。
* **自适应轮询（Adaptive Polling）** —— 主权 Shell 视图在活跃投票/挑战/激活阶段每 8 秒轮询一次，空闲时每 30–60 秒轮询一次。无需 websocket 层即可实现实时投票体验。
* **逐字诊断** —— 每次写入按钮均展示后端拒绝的逐字原因。无模糊的“已拒绝”提示框。

**隐私原语跑道（v0.9.7 新增）：**

* **功能密钥 —— 匿名凭证框架** —— 零知识证明、挑战-响应、两阶段提交回执、枚举否认码及批量结算的基础设施已就位。当前的挑战-响应仅为基于 HMAC 的集成测试占位符，并非生产级匿名或零知识公民身份验证。真正的不可链接发行仍在等待基础方案决策（RSA 盲签名 vs BBS+ vs U-Prove vs Idemix）。
* **锁定协议合约** —— `services/infonet/privacy/contracts.py` 中的环签名、隐身地址、Pedersen 承诺、范围证明及 DEX 匹配的接口已稳定。`privacy-core` Rust crate 为集成目标——隐私模块的调用者无需知晓当前激活的具体方案。
* **Sprint 11+ 路径** —— 选定密码学方案后，原语将无缝接入锁定协议，且无 API 变更。

> **实验性测试网 —— 不保证隐私：** InfoNet 消息已混淆但**非端到端加密**。Mesh 网络（Meshtastic/APRS）**不具备隐私性**——无线电传输本质上是公开的。隐私原语合约仅完成框架搭建尚未接入。切勿在任何频道发送敏感信息。目前请将所有通道视为公开开放。

### 🔍 Shodan 设备搜索（v0.9.6 新增）

* **互联网设备搜索** —— 直接从 ShadowBroker 查询 Shodan。支持按关键词、CVE、端口或服务类型搜索——结果作为实时覆盖层绘制在地图上。
* **可配置标记** —— 自定义 Shodan 结果的形状、颜色和大小。
* **操作员提供的 API** —— 使用你自己的 `SHODAN_API_KEY`；结果渲染为本地调查覆盖层。

### 🛩️ 航空追踪

* **商业航班** —— 通过 OpenSky Network 获取实时位置（~5,000+ 架飞机）。
* **私人飞机** — 轻型通用航空、涡桨飞机、公务机单独跟踪。
* **私人喷气机** —— 高净值个人飞行器，附带所有者识别信息。
* **军用航班** —— 通过 adsb.lol 军事端点获取加油机、ISR、战斗机及运输机数据。
* **飞行轨迹累积** —— 所有追踪飞机的持久化航迹标记。
* **盘旋模式检测** —— 自动标记绕圈飞行的飞机（总转向 >300°）。
* **机型分类** —— 形状准确的 SVG 图标：客机、涡桨、公务机、直升机。
* **地面停机检测** —— AGL 高度低于 100ft 的飞机渲染为灰色图标。

### 🚢 海事追踪

* **AIS 船舶流** —— 通过 aisstream.io WebSocket（实时）获取 25,000+ 艘船舶数据。
* **舰船分类** —— 货轮、油轮、客轮、游艇、军舰类型，配备颜色编码图标。
* **航母打击群追踪器** —— 所有 11 艘现役美国海军航空母舰及 OSINT 估算位置。目前无其他开源工具能做到这一点。
  * 自动化 GDELT 新闻抓取解析航母动向报道以估算位置。
  * 50+ 地理区域到坐标的映射（例如“东地中海” → lat/lng）。
  * 磁盘缓存位置，UTC 时间 00:00 & 12:00 自动刷新。
* **邮轮与客轮** —— 专用图层用于游轮和渡轮。
* **渔业活动** —— Global Fishing Watch 船舶事件（新增）。
* **聚类显示** — 低缩放级别下船舶聚合成带数量标签的集群，放大后解聚。

### 🚆 铁路追踪（v0.9.6 新增）

* **Amtrak 列车** —— 美国境内 Amtrak 列车的实时位置、速度、航向、路线及状态。
* **欧洲铁路** —— DigiTraffic 集成用于欧洲火车位置查询。

### 🛰️ 太空与卫星

* **轨道追踪** —— 通过 CelesTrak TLE 数据 + SGP4 传播模型获取实时卫星位置（2,000+ 活跃卫星，无需 API 密钥）。
* **任务类型分类** — 按任务颜色编码：军事侦察（红）、SAR（青）、SIGINT（白）、导航（蓝）、早期预警（品红）、商业成像（绿）、空间站（金）。
* **SatNOGS 地面站** —— 业余卫星地面站网络，附带实时观测数据（新增）。
* **TinyGS LoRa 卫星** — LoRa 卫星星座追踪（新增）。

### 🌍 地缘政治与冲突

* **全球事件** —— GDELT 驱动的冲突事件聚合（最近 8 小时，~1,000 个事件）。
* **乌克兰前线** —— DeepState Map 提供的实时战争前沿 GeoJSON。
* **乌克兰空袭警报** — 区域实时空袭警报（新增）。
* **SIGINT/RISINT 新闻流** — 来自多个情报来源的实时 RSS 聚合，支持用户自定义订阅源（最多 20 个源，可配置优先级权重 1-5）。
* **区域档案** —— 在地球上任意位置右键点击获取即时情报简报：
  * 国家概况（人口、首都、语言、货币、面积）
  * 现任国家元首及政府类型（实时 Wikidata SPARQL 查询）
  * 本地维基百科摘要与缩略图
  * 最新 Sentinel-2 卫星照片，附带拍摄日期和云量覆盖（10 米分辨率）。

### 🛰️ 卫星影像

* **NASA GIBS (MODIS Terra)** — 每日真彩色卫星影像叠加层，配备 30 天时间滑块、播放/暂停动画及透明度控制（~250m/像素）。
* **高分辨率卫星（Esri）** — 通过 Esri World Imagery 获取亚米级分辨率影像——可放大查看建筑与地形细节（缩放级别 18+）。
* **Sentinel-2 情报卡** —— 在地图上任意位置右键点击，弹出浮动情报卡片显示最新 Sentinel-2 卫星照片、拍摄日期、云量百分比及可点击的全分辨率图像（10 米分辨率，约每 5 天更新一次）。
* **Sentinel Hub Process API** — Copernicus CDSE 卫星影像配合 OAuth2 令牌流程（新增）。
* **VIIRS 夜光图** — 夜间灯光变化检测叠加层（新增）。
* **5 种视觉模式** —— 通过 STYLE 按钮切换整个地图美学：
  * **DEFAULT** — 深色 CARTO 底图。
  * **SATELLITE** — 亚米级 Esri World Imagery。
  * **FLIR** — 热成像美学（反转灰度）。
  * **NVG** — 夜视仪绿色荧光。
  * **CRT** — 复古终端扫描线叠加层。

### 🛰️ SAR 地表变化检测（新增）

* **合成孔径雷达图层** —— 穿透云层、在夜间或地球任何位置检测地表变化。两种模式均免费：
  * **A 模式（目录）** — 来自 Alaska Satellite Facility 的免费 Sentinel-1 场景元数据。无需账号。显示你的 AOI 区域何时经过雷达扫描以及下次扫描时间。
  * **B 模式（完整异常）** — NASA OPERA (DISP, DSWx, DIST-ALERT) 和 Copernicus EGMS 的实时地表变化警报。需免费 NASA Earthdata 账号——应用内向导引导你在一分钟内完成设置。
* **异常类型** —— 地面形变（毫米级沉降、滑坡）、地表水变化（洪水范围）、植被干扰（森林砍伐、燃烧疤痕、爆炸坑）、损毁评估（UNOSAT/Copernicus EMS 验证）及相干性变化检测。
* **地图可视化** — 按类型颜色编码的异常标记点（橙色为形变，青色为水体，绿色为植被，红色为损毁，紫色为相干性）。AOI 边界以虚线多边形绘制并分类着色。点击任意标记点弹出详情窗口，显示量级、置信度、求解器、场景数量及来源链接。
* **AOI 编辑器** —— 直接从地图定义兴趣区域（AOI）。激活 SAR 图层后点击“EDIT AOIs”按钮，使用十字准线工具在地图上点击放置 AOI 中心。设置名称、半径（1–500 km）和类别。AOI 立即显示在地图上。
* **OpenClaw 集成** —— AI 智能体可检查 SAR 异常详情（`sar_pin_click`）并引导操作员地图飞至任意 AOI 中心（`sar_focus_aoi`）——实现协同分析师工作流。
* **设置面板** — Settings 中的专用 SAR 标签页显示 A/B 模式状态、OpenClaw 集成状态，并提供一键撤销 Earthdata 凭证的功能。

### 📻 软件定义无线电与信号情报

* **KiwiSDR 接收器** — 全球分布的 500+ 公共 SDR 接收器，聚类琥珀色标记显示。
* **实时收音机调谐器** —— 点击任意 KiwiSDR 节点直接在 SIGINT 面板中打开嵌入式 SDR 调谐器。
* **元数据显示** — 节点名称、位置、天线类型、频段、活跃用户数。
* **Meshtastic Mesh 无线电** — 基于 MQTT 的 Mesh 无线电集成，附带节点地图并集成到 Mesh Chat（新增）。
* **APRS 集成** —— 通过 APRS-IS TCP 馈送实现业余无线电定位（新增）。
* **GPS 干扰检测** — 实时分析飞机 NAC-P（导航精度类别）值。
  * 基于网格的聚合识别干扰区域。
  * 红色叠加方块附带“GPS JAM XX%”严重性标签。
* **无线电拦截面板** —— 扫描器风格 UI，集成 OpenMHZ 警用/消防扫描仪馈送。点击任意系统实时收听。扫描模式自动循环活跃馈送。一键窃听真实应急通信。

### 📷 监控网络

* **CCTV Mesh** — 覆盖 6 个国家、13 个来源的 11,000+ 路实时交通摄像头：
  * 🇬🇧 Transport for London JamCams
  * 🇺🇸 NYC DOT, Austin TX (TxDOT)
  * 🇺🇸 California (12 Caltrans districts), Washington State (WSDOT), Georgia DOT, Illinois DOT, Michigan DOT
  * 🇪🇸 Spain DGT National (20 cities), Madrid City (357 cameras via KML)
  * 🇸🇬 Singapore LTA
  * 🌍 Windy Webcams
* **馈送渲染** — 自动检测并渲染视频、MJPEG、HLS、嵌入、卫星瓦片及图像馈送。
* **聚类地图显示** —— 绿色点聚合成带数量标签的集群，放大后解聚。

### 🔥 环境与灾害监测

* **NASA FIRMS 火热点（24h）** — NOAA-20 VIIRS 卫星的全球热异常数据（5,000+），每周期更新。火焰形状图标按火灾辐射功率（FRP）颜色编码：黄色（低）、橙色、红色、深红（强烈）。低缩放级别下聚类显示，附带火焰形状集群标记。
* **火山** — Smithsonian 全球火山学计划全新世火山全球分布图（新增）。
* **天气警报** —— 恶劣天气多边形及紧迫性/严重性指示器（新增）。
* **空气质量 (PM2.5)** — OpenAQ 全球站点实时颗粒物读数（新增）。
* **地震（24h）** — USGS 实时地震馈送，按震级缩放标记点。
* **空间天气徽章** —— 底部状态栏显示实时 NOAA 地磁风暴指示器。Kp 指数颜色编码：绿色（平静）、黄色（活跃）、红色（G1–G5 级风暴）。数据源自 SWPC 行星 K 指数 1 分钟馈送。

### 🏗️ 基础设施监测

* **互联网中断监控** —— Georgia Tech IODA 提供的区域互联网连接警报。受影响区域显示灰色标记及严重性百分比。仅使用可靠数据源（BGP 路由表、活跃 ping 探测）——无望远镜或插值数据。
* **数据中心映射** — 来自精选数据集的 2,000+ 全球数据中心分布图。紫色聚类标记附带服务器机架图标。点击可查看运营商、位置及按国家自动交叉引用的互联网中断情况。
* **军事基地** —— 全球军事设施与导弹基地数据库（新增）。
* **发电厂** — WRI 数据库中的 35,000+ 全球发电厂（新增）。

### 🌐 附加图层与工具

* **昼夜循环** — 显示全球日照/黑暗区域的太阳终止线叠加层。
* **全球市场行情** —— 实时金融市场指数（可最小化）。
* **测量工具** —— 地图上点对点距离与方位角测量。
* **LOCATE 栏** —— 按坐标（31.8, 34.8）或地点名称（Tehran, Strait of Hormuz）搜索，直接飞至任意位置——通过 OpenStreetMap Nominatim 进行地理编码。

![Gaza](https://gitlab.com/bigbodycobain/Shadowbroker/uploads/c55a0c8d49e5e05c6cd094279e6e089b/gaza-screenshot.jpg)

### 🤖 代理智能体命令通道 —— OpenClaw + 兼容智能体（v0.9.7 扩展）

ShadowBroker 暴露了一个**双向代理智能体命令通道**——一个带签名和层级门禁的桥梁，赋予任何兼容 AI 智能体对情报平台的完整读写权限。**OpenClaw 是参考智能体**，但该通道为开放协议：任何使用 HMAC-SHA256 签名的 LLM 驱动智能体（Claude Code、GPT、LangChain、自定义 Python/TypeScript 客户端或你自己的集成）均可连接为分析师，看到与操作员相同的数据并在地图上执行操作。ShadowBroker **不捆绑** LLM、智能体运行时或模型权重——它提供接口；你带来你的智能体。

v0.9.7 将 ShadowBroker 从人类观看的仪表盘转变为任何智能体均可操作的表面情报层。

**通道传输（v0.9.7 新增）：**

* **单一命令通道** — `POST /api/ai/channel/command` 接受 `{cmd, args}` 并分发至任意已注册工具。
* **批量并发执行** — `POST /api/ai/channel/batch` 一次请求最多接受 20 条命令。后端并发运行并返回扇出结果映射。相比顺序调用，智能体延迟降低一个数量级。
* **层级门禁访问** — `OPENCLAW_ACCESS_TIER` 控制智能体可调用的命令：`restricted` 暴露只读集，`full` 增加写入和注入权限。发现端点返回 `available_commands` 供智能体内省自身能力。
* **HMAC-SHA256 签名** — 每条命令均签名 `HMAC-SHA256(secret, METHOD|path|timestamp|nonce|sha256(body))`，附带时间戳 + 非ce replay 保护及请求完整性验证。支持本地模式（无需配置）和远程模式（智能体位于不同机器/VPS）。

**能力：**

* **完整遥测访问** — 智能体查询所有 35+ 数据层：航班、船舶、卫星、SIGINT、冲突事件、地震、火灾、废水、预测市场等。快/慢层级端点返回带地理坐标、时间戳及来源归属的丰富数据。
* **AI 情报图钉** — 直接在操作员地图上放置颜色编码的调查标记。14 种分类（威胁、异常、军事、海事、航空、SIGINT、基础设施等），附带置信度分数、TTL 过期时间、来源 URL，支持一次最多批量放置 100 个图钉。
* **地图控制** — 将操作员地图视图飞至任意坐标，触发卫星影像查询及区域档案打开。智能体可实时引导操作员注意力至特定位置。
* **SAR 地表变化** —— 查询 SAR 异常馈送、检查标记点详情、管理 AOI 并飞越监视区。智能体可监测地面形变、洪水范围或损毁并将异常提升为图钉。
* **原生图层注入** — 将自定义数据直接推送到 ShadowBroker 的原生图层（CCTV 摄像头、船舶、SIGINT 节点、军事基地等），使智能体发现的数据源与真实馈送并列渲染。
* **Wormhole Mesh 参与** —— 智能体可加入去中心化 InfoNet，发布签名消息、加入加密网关频道、发送/接收加密 DM，并与 Meshtastic 无线电和 Dead Drops 交互——作为完整 Mesh 节点运行。
* **Sovereign Shell 参与（v0.9.7）** — 提交请愿、签署并投票治理变更、对决议和争议进行质押、为升级信号 Heavy-Node 就绪状态——全部可编程执行，受层级和 HMAC 门禁控制。智能体成为去中心化情报经济的一等公民参与者。
* **地理编码与邻近扫描** —— 将地名解析为坐标，然后在半径内扫描所有图层以生成完整的邻近摘要。
* **新闻与 GDELT 近场搜索** — 拉取任意坐标附近的 GDELT 冲突事件和聚合新闻报道以实现区域态势感知。
* **警报推送** — 向 Discord Webhook 和 Telegram 频道发送品牌化情报简报、警告及威胁通知。
* **情报报告** —— 生成结构化报告，附带汇总统计、顶级军用航班、相关性分析、地震活动、SIGINT 计数及图钉清单。
* **可审计** —— 每次通道调用均记录日志；操作员可内省智能体执行的操作。

**连接智能体：** 打开左侧边栏的 AI Intel 面板，点击 **Connect Agent**，复制 HMAC 密钥。此后将任意兼容智能体指向该通道——对于 OpenClaw，从 OpenClaw 技能包导入 `ShadowBrokerClient`；对于其他智能体，使用上述文档中的相同 HMAC 契约（时间戳 + nonce + body digest，层级门禁）。该通道是协议本身，而非特定智能体。

### ⏱️ 时光机 —— 快照回放（v0.9.7 新增）

面向整个遥测馈送的多媒体风格传输控件。将实时地图视为可快进、暂停和回放的录像带。

* **Live ↔ Snapshot 切换** — 切换到快照模式会立即暂停全局轮询循环；切回 Live 会失效 ETags 并强制刷新快/慢层级，使仪表盘无缝追赶而不会出现陈旧帧闪烁。
* **小时索引** —— 每个捕获的快照均按小时桶索引，附带 `count`、`latest_id`、`latest_ts` 及完整 `snapshot_ids` 列表。可直接从时间线滑块跳转到任意已捕获的时间戳。
* **帧插值** — 移动实体（飞机、船舶、卫星、军用航班）在回放期间于记录帧之间平滑插值，即使快照稀疏也能保持运动连续性。
* **可变播放速度** —— 以可调速度逐步、播放、快进或倒带保存的遥测数据。
* **配置感知** — 每个快照均记录捕获时激活的隐私配置文件，确保回放忠实还原该配置下操作员所见内容。
* **操作员侧而非服务器侧存储** — 快照存储在本地后端；第三方永远无法查看回放时间线。

### 📦 API 密钥面板 —— 路径优先、只读模式（v0.9.7 新增）

Settings → API Keys 现已变为只读注册表。密钥值永不抵达浏览器进程——甚至不暴露混淆前缀。该面板展示：

* 后端 `.env` 文件的绝对路径，由 `Path(__file__).resolve()` 解析——适用于所有操作系统、驱动器及安装位置（Linux `/home/...`、macOS `/Users/...`、Windows 任意盘符、Docker 容器、云虚拟机）。
* 路径本身附带 `[exists]` / `[will be created on first save]` / `[NOT WRITABLE — edit by hand]` 指示器。
* `.env.example` 模板的路径，供用户复制并填入密钥。
* 每个密钥的 `CONFIGURED` / `NOT CONFIGURED` 二进制徽章，以及可一键复制粘贴的环境变量行（例如 `OPENSKY_CLIENT_ID=YOUR_VALUE`），供用户手动写入文件。

OpenSky API 凭证现已成为**关键警告级环境要求**：启动环境检查会对缺失的 OpenSky OAuth2 凭证发出强警告，且更新日志模态框直接链接至免费注册页面。若无此配置，航班图层将回退为仅 ADS-B 覆盖，在非洲、亚洲和拉丁美洲存在显著盲区。

---

## 🏗️ 架构设计

ShadowBroker v0.9.7 由三个垂直堆叠的平面组成——**操作员 UI**、**后端服务层**和**去中心化层（InfoNet）**，外加两个跨切面桥梁（**时光机**与**代理智能体通道**，即 OpenClaw 及其他兼容智能体连接的协议）以及一个 **Privacy Core** Rust crate，用于支撑旧版 Mesh 及未来的屏蔽币/DEX 工作。

```
╔═════════════════════════════════════════════════════════════════════════════╗
║                       OPERATOR UI  (Next.js + MapLibre)                     ║
║                                                                             ║
║  ┌────────────────┐  ┌──────────┐  ┌────────────────┐  ┌────────────────┐   ║
║  │ MapLibre GL    │  │ NewsFeed │  │ Sovereign Shell│  │   Mesh Chat    │   ║
║  │  WebGL render  │  │  SIGINT  │  │  Petitions /   │  │  + Mesh Term.  │   ║
║  │  + clusters    │  │  GDELT   │  │  Upgrades /    │  │  (Infonet /    │   ║
║  │                │  │  Threat  │  │  Disputes /    │  │   Mesh /       │   ║
║  │                │  │          │  │  Gates /       │  │   Dead Drop)   │   ║
║  │                │  │          │  │  Bootstrap /   │  │                │   ║
║  │                │  │          │  │  Function Keys │  │                │   ║
║  └──────┬─────────┘  └────┬─────┘  └────────┬───────┘  └────────┬───────┘   ║
║         │                 │                 │                   │           ║
║  ┌──────┴─────────────────┴─────────────────┴───────────────────┴───────┐   ║
║  │  Time Machine ◀── snapshot playback ── snapshotMode toggle ──▶ Live │   ║
║  │  hourly index │ frame interpolation │ profile-aware │ per-tier ETag  │   ║
║  └──────────────────────────────────┬───────────────────────────────────┘   ║
║                                     │ REST  +  /api/[...path] proxy         ║
╠═════════════════════════════════════╪═══════════════════════════════════════╣
║                       BACKEND SERVICE PLANE  (FastAPI)                      ║
║                                     │                                       ║
║  ┌──────────────────────────────────┴────────────────────────────────────┐  ║
║  │              Data Fetcher  (APScheduler — fast / slow tiers)          │  ║
║  │                                                                       │  ║
║  │  ┌───────────┬───────────┬───────────┬───────────┬───────────┐        │  ║
║  │  │  OpenSky* │ adsb.lol  │ CelesTrak │   USGS    │   AIS WS  │        │  ║
║  │  │  Flights  │ Military  │   Sats    │  Quakes   │   Ships   │        │  ║
║  │  ├───────────┼───────────┼───────────┼───────────┼───────────┤        │  ║
║  │  │  Carrier  │   GDELT   │ CCTV (12) │ DeepState │   NASA    │        │  ║
║  │  │  Tracker  │ Conflict  │  Cameras  │ Frontline │   FIRMS   │        │  ║
║  │  ├───────────┼───────────┼───────────┼───────────┼───────────┤        │  ║
║  │  │   GPS     │  KiwiSDR  │  Shodan   │  Amtrak   │  SatNOGS  │        │  ║
║  │  │  Jamming  │   Radios  │  Devices  │ DigiTraf  │  TinyGS   │        │  ║
║  │  ├───────────┼───────────┼───────────┼───────────┼───────────┤        │  ║
║  │  │ Volcanoes │  Weather  │  Fishing  │ Mil Bases │   IODA    │        │  ║
║  │  │  Air Qual │  Alerts   │  Activity │ PwrPlants │  Outages  │        │  ║
║  │  ├───────────┼───────────┼───────────┼───────────┼───────────┤        │  ║
║  │  │ Sentinel  │   MODIS   │   VIIRS   │   Data    │ Meshtastic│        │  ║
║  │  │  Hub/STAC │   Terra   │ Nightlts  │  Centers  │   APRS    │        │  ║
║  │  ├───────────┴───────────┴───────────┴───────────┴───────────┤        │  ║
║  │  │  SAR (NEW v0.9.7)                                         │        │  ║
║  │  │   Mode A: ASF Search catalog (free, no account)           │        │  ║
║  │  │   Mode B: NASA OPERA / Copernicus EGMS / GFM / EMS /      │        │  ║
║  │  │           UNOSAT  ground-change anomalies (opt-in)        │        │  ║
║  │  └───────────────────────────────────────────────────────────┘        │  ║
║  │   * OpenSky: REQUIRED for global flight coverage                      │  ║
║  └───────────────────────────────────────────────────────────────────────┘  ║
║                                     │                                       ║
║  ┌──────────────────────────────────┴────────────────────────────────────┐  ║
║  │                   Snapshot Store  (Time Machine source)               │  ║
║  │   Hourly index  │  per-snapshot layer manifest  │  profile metadata   │  ║
║  └───────────────────────────────────────────────────────────────────────┘  ║
║                                                                             ║
║  ┌───────────────────────────────────────────────────────────────────────┐  ║
║  │   Agentic AI Channel  (HMAC-SHA256, tier-gated  —  OpenClaw + others) │  ║
║  │                                                                       │  ║
║  │   POST /api/ai/channel/command   →  one tool call                     │  ║
║  │   POST /api/ai/channel/batch     →  up to 20 concurrent tool calls    │  ║
║  │                                                                       │  ║
║  │   Tier:   restricted (read-only)   │   full (read + write + inject)   │  ║
║  │   Auth:   X-SB-Timestamp + X-SB-Nonce + X-SB-Signature                │  ║
║  │   Sig  =  HMAC-SHA256(secret, METHOD|path|ts|nonce|sha256(body))      │  ║
║  └───────────────────────────────────────────────────────────────────────┘  ║
╠═════════════════════════════════════════════════════════════════════════════╣
║                  DECENTRALIZED LAYER  (InfoNet Testnet — signed events)     ║
║                                                                             ║
║  ┌────────────────────────────┐    ┌──────────────────────────────────┐     ║
║  │    Mesh Hashchain          │    │   Sovereign Shell Governance     │     ║
║  │                            │    │                                  │     ║
║  │  Ed25519 signed events     │    │  Petitions  (DSL: UPDATE_PARAM,  │     ║
║  │  Public-key binding        │    │              ENABLE_FEATURE …)   │     ║
║  │  Replay / sequence guard   │    │  Upgrade-Hash voting (80% / 40%  │     ║
║  │  Two-tier finality         │    │             quorum / 67% Heavy)  │     ║
║  │   ├ Tier 1 (CRDT, fast)    │    │  Resolution & Dispute markets    │     ║
║  │   └ Tier 2 (epoch finality)│    │  Gate suspend / shutdown / appeal│     ║
║  │  Identity rotation         │    │  Bootstrap eligible-node-1-vote  │     ║
║  │  Constitutional invariants │    │   (Argon2id PoW, Heavy-Node only)│     ║
║  │  (MappingProxyType)        │    │  Function Keys (5 of 6 pieces)   │     ║
║  └─────────────┬──────────────┘    └─────────────┬────────────────────┘     ║
║                │                                 │                          ║
║                └──────────────┬──────────────────┘                          ║
║                               │                                             ║
║  ┌────────────────────────────┴──────────────────────────────────────┐      ║
║  │            Wormhole / InfoNet Relay  (transport layer)            │      ║
║  │   Gate personas │ canonical signing │ Dead Drop epoch mailboxes   │      ║
║  └───────────────────────────────────────────────────────────────────┘      ║
╠═════════════════════════════════════════════════════════════════════════════╣
║              PRIVACY CORE  (Rust crate — locked Protocol contracts)         ║
║                                                                             ║
║   privacy-core/  ─►  Argon2id │ Ed25519/X25519 │ AESGCM │ HKDF              ║
║                      Ring sigs* │ Stealth addrs* │ Pedersen* │ Bulletproofs*║
║                      Blind-sig issuance* (RSA / BBS+ / U-Prove / Idemix)    ║
║                                                                             ║
║   * = locked Protocol contract; cryptographic primitive lands Sprint 11+    ║
╚═════════════════════════════════════════════════════════════════════════════╝

   Distribution
   ────────────
     GitHub (primary):  ghcr.io/bigbodycobain/shadowbroker-{backend,frontend}
     GitLab (mirror):   registry.gitlab.com/bigbodycobain/shadowbroker/{backend,frontend}
     Multi-arch:        linux/amd64  +  linux/arm64  (Raspberry Pi 5 supported)
     Desktop:           Tauri shell  →  packaged backend-runtime  +  Next.js frontend
```

---

## 📊 数据源与 API

| Source | Data | Update Frequency | API Key Required |
|---|---|---|---|
| [OpenSky Network](https://opensky-network.org) | Commercial & private flights | ~60s | **Yes** |
| [adsb.lol](https://adsb.lol) | Military aircraft | ~60s | No |
| [aisstream.io](https://aisstream.io) | AIS vessel positions | Real-time WebSocket | **Yes** |
| [CelesTrak](https://celestrak.org) | Satellite orbital positions (TLE + SGP4) | ~60s | No |
| [USGS Earthquake](https://earthquake.usgs.gov) | Global seismic events | ~60s | No |
| [GDELT Project](https://www.gdeltproject.org) | Global conflict events | ~6h | No |
| [DeepState Map](https://deepstatemap.live) | Ukraine frontline | ~30min | No |
| [Shodan](https://www.shodan.io) | Internet-connected device search | On-demand | **Yes** |
| [Amtrak](https://www.amtrak.com) | US train positions | ~60s | No |
| [DigiTraffic](https://www.digitraffic.fi) | European rail positions | ~60s | No |
| [Global Fishing Watch](https://globalfishingwatch.org) | Fishing vessel activity events | ~10min | No |
| Transport for London, NYC DOT, TxDOT | CCTV cameras (UK, US) | ~10min | No |
| Caltrans, WSDOT, GDOT, IDOT, MDOT | CCTV cameras (5 US states) | ~10min | No |
| Spain DGT, Madrid City | CCTV cameras (Spain) | ~10min | No |
| [Singapore LTA](https://datamall.lta.gov.sg) | Singapore traffic cameras | ~10min | **Yes** |
| [Windy Webcams](https://www.windy.com) | Global webcams | ~10min | No |
| [SatNOGS](https://satnogs.org) | Amateur satellite ground stations | ~30min | No |
| [TinyGS](https://tinygs.com) | LoRa satellite ground stations | ~30min | No |
| [Meshtastic MQTT](https://meshtastic.org) | Mesh radio node positions | Real-time | No |
| [APRS-IS](https://www.aprs-is.net) | Amateur radio positions | Real-time TCP | No |
| [KiwiSDR](https://kiwisdr.com) | Public SDR receiver locations | ~30min | No |
| [OpenMHZ](https://openmhz.com) | Police/fire scanner feeds | Real-time | No |
| [Smithsonian GVP](https://volcano.si.edu) | Holocene volcanoes worldwide | Static (cached) | No |
| [OpenAQ](https://openaq.org) | Air quality PM2.5 stations | ~120s | No |
| NOAA / NWS | Severe weather alerts & polygons | ~120s | No |
| [WRI Global Power Plant DB](https://datasets.wri.org) | 35,000+ power plants | Static (cached) | No |
| Military base datasets | Global military installations | Static (cached) | No |
| [NASA FIRMS](https://firms.modaps.eosdis.nasa.gov) | NOAA-20 VIIRS fire/thermal hotspots | ~120s | No |
| [NOAA SWPC](https://services.swpc.noaa.gov) | Space weather Kp index & solar events | ~120s | No |
| [IODA (Georgia Tech)](https://ioda.inetintel.cc.gatech.edu) | Regional internet outage alerts | ~120s | No |
| [DC Map (GitHub)](https://github.com/Ringmast4r/Data-Center-Map---Global) | Global data center locations | Static (cached 7d) | No |
| [NASA GIBS](https://gibs.earthdata.nasa.gov) | MODIS Terra daily satellite imagery | Daily (24-48h delay) | No |
| [Esri World Imagery](https://www.arcgis.com) | High-res satellite basemap | Static (periodically updated) | No |
| [MS Planetary Computer](https://planetarycomputer.microsoft.com) | Sentinel-2 L2A scenes (right-click) | On-demand | No |
| [Copernicus CDSE](https://dataspace.copernicus.eu) | Sentinel Hub imagery (Process API) | On-demand | **Yes** (free) |
| [VIIRS Nightlights](https://eogdata.mines.edu) | Night-time light change detection | Static | No |
| [RestCountries](https://restcountries.com) | Country profile data | On-demand (cached 24h) | No |
| [Wikidata SPARQL](https://query.wikidata.org) | Head of state data | On-demand (cached 24h) | No |
| [Wikipedia API](https://en.wikipedia.org/api) | Location summaries & aircraft images | On-demand (cached) | No |
| [OSM Nominatim](https://nominatim.openstreetmap.org) | Place name geocoding (LOCATE bar) | On-demand | No |
| [CARTO Basemaps](https://carto.com) | Dark map tiles | Continuous | No |

---

## 🚀 入门指南

### 🐳 Docker Setup（推荐自托管方式）

仓库包含 `docker-compose.yml`，从 GitHub Container Registry 拉取预构建镜像。

```bash
git clone https://github.com/BigBodyCobain/Shadowbroker.git
cd Shadowbroker
# 在仓库根目录的 .env 文件中添加 API 密钥（可选——详见下方环境变量）
docker compose pull
docker compose up -d
```

打开 `http://localhost:3000` 查看仪表盘。

> **公开部署或局域网部署？** 大多数设置无需额外配置。前端通过 Next.js 服务器将所有 API 调用代理至 `BACKEND_URL`，默认值为 `http://backend:8000`（Docker 内部网络）。宿主机端口 `8000` 仅用于本地 API/调试访问。若与其他服务冲突，请在 `.env` 中设置 `BACKEND_PORT=8001`；保持 `BACKEND_URL` 为 `http://backend:8000`（此为 Docker 内部端口）。后端内存上限由 `BACKEND_MEMORY_LIMIT` 控制，默认为 `4G`。若 Docker 报告 OOM 事件，后端将重启，较慢的图层在重新填充前可能显示为空。
>
> **若你的后端运行在不同主机或端口上**，可在运行时设置 `BACKEND_URL`——无需重新构建：
>
> ```bash
> # Linux / macOS
> BACKEND_URL=http://myserver.com:9096 docker compose up -d
>
> # Podman (via compose.sh wrapper)
> BACKEND_URL=http://192.168.1.50:9096 ./compose.sh up -d
>
> # Windows (PowerShell)
> $env:BACKEND_URL="http://myserver.com:9096"; docker compose up -d
>
> # 或添加到 `docker-compose.yml` 旁的 `.env` 文件中：
> # BACKEND_URL=http://myserver.com:9096
> ```

**Podman 用户：** 请勿将 GitHub URL 传递给 `podman compose pull`；请先克隆仓库，`cd Shadowbroker`，然后在该文件夹内运行 compose。`podman compose` 同样需要 Compose provider。若 Podman 提示 `looking up compose provider failed`，请安装一个：

```bash
# Linux / macOS / WSL
python3 -m pip install --user podman-compose
podman-compose pull
podman-compose up -d
```

```powershell
# Windows PowerShell
py -m pip install --user podman-compose
podman-compose pull
podman-compose up -d
```

若你在 bash 兼容 shell 中，内置包装器可自动检测 Docker 或 Podman：

```bash
./compose.sh --engine podman pull
./compose.sh --engine podman up -d
```

---

### 🐋 Standalone Deploy（Portainer、Uncloud、NAS 等）

无需克隆仓库。直接使用 GitHub Container Registry 中的预构建镜像。若你发布到 GitLab，也可使用其镜像作为备用源。

创建包含以下内容的 `docker-compose.yml` 并直接部署——粘贴至 Portainer 的堆栈编辑器、`uncloud deploy` 或任意 Docker 主机：

```yaml
## Image registry — uncomment ONE line per service:
##   GitHub  (primary): ghcr.io/bigbodycobain/shadowbroker-backend:latest
##   GitLab  (mirror):  registry.gitlab.com/bigbodycobain/shadowbroker/backend:latest


services:
  backend:
    image: ghcr.io/bigbodycobain/shadowbroker-backend:latest
    # image: registry.gitlab.com/bigbodycobain/shadowbroker/backend:latest
    container_name: shadowbroker-backend
    ports:
      - "${BACKEND_PORT:-8000}:8000"
    environment:
      - AIS_API_KEY=your_aisstream_key          # Required — get one free at aisstream.io
      - OPENSKY_CLIENT_ID=                       # Optional — higher flight data rate limits
      - OPENSKY_CLIENT_SECRET=                   # Optional — paired with Client ID above
      - LTA_ACCOUNT_KEY=                         # Optional — Singapore CCTV cameras
      - SHODAN_API_KEY=                          # Optional — Shodan device search overlay
      - SH_CLIENT_ID=                            # Optional — Sentinel Hub satellite imagery
      - SH_CLIENT_SECRET=                        # Optional — paired with Sentinel Hub ID
      - CORS_ORIGINS=                            # Optional — comma-separated allowed origins
    volumes:
      - backend_data:/app/data
    restart: unless-stopped

  frontend:
    image: ghcr.io/bigbodycobain/shadowbroker-frontend:latest
    # image: registry.gitlab.com/bigbodycobain/shadowbroker/frontend:latest
    container_name: shadowbroker-frontend
    ports:
      - "3000:3000"
    environment:
      - BACKEND_URL=http://backend:8000   # Docker internal networking — no rebuild needed
    depends_on:
      - backend
    restart: unless-stopped

volumes:
  backend_data:
```

> **工作原理：** 前端容器通过 Next.js 服务器将 `/api/*` 请求代理至 `BACKEND_URL`，使用 Docker 内部网络。浏览器仅与端口 3000 通信。后端宿主机端口用于本地 API/调试访问，可通过 `BACKEND_PORT=8001` 更改，且无需修改 `BACKEND_URL`。
>
> `BACKEND_URL` 是纯运行时环境变量（非构建时的 `NEXT_PUBLIC_*`），因此你可随时在 Portainer、Uncloud 或任意 compose 编辑器中修改它而无需重新构建镜像。将其设置为你的后端在 Docker 网络内可访问的地址即可（例如 `http://backend:8000`、`http://192.168.1.50:8000`）。

---

### 📦 Quick Start (No Code Required)

若你只想运行仪表盘而不想处理终端命令：

1. 前往此仓库页面右侧的 **[Releases](../../releases)** 标签页。
2. 下载发布的最新 `.zip` 文件。
3. 将文件夹解压至你的电脑。
4. **Windows：** 双击 `start.bat`。
   **Mac/Linux：** 打开终端，输入 `chmod +x start.sh`、`dos2unix start.sh`，然后运行 `./start.sh`。
5. 它将自动安装所有依赖并启动仪表盘！

本地启动器说明：

- `start.bat` / `start.sh` 在无 Docker 环境下运行应用——直接安装依赖并启动两个服务器。
- 若升级后 Wormhole 身份或 DM 联系人端点失败，请检查 `docs/mesh/` 文件夹中的故障排除指南。
- 关于 DM root witness、透明性及操作员监控的发布流程，请先阅读 `docs/mesh/wormhole-dm-root-operations-runbook.md`。
- 有关示例 DM root ops bridge 资源，另请参阅 `scripts/mesh/poll-dm-root-health-alerts.mjs`、`scripts/mesh/export-dm-root-health-prometheus.mjs`、`scripts/mesh/publish-external-root-witness-package.mjs`、`scripts/mesh/smoke-external-root-witness-flow.mjs`、`scripts/mesh/smoke-root-transparency-publication-flow.mjs`、`scripts/mesh/smoke-dm-root-deployment-flow.mjs`、`scripts/mesh/sync-dm-root-external-assurance.mjs` 及 `docs/mesh/examples/`。

---

### 💻 Developer Setup

若你想修改代码或从源码运行：

#### Prerequisites

* **Node.js** 18+ and **npm** — [nodejs.org](https://nodejs.org/)
* **Python** 3.10, 3.11, or 3.12 with `pip` — [python.org](https://www.python.org/downloads/) (**安装时勾选 "Add to PATH"**)
  * ⚠️ Python 3.13+ 可能与部分依赖存在兼容性问题。**推荐使用 3.11 或 3.12。**
* API keys for: `aisstream.io` (required), and optionally `opensky-network.org` (OAuth2), `lta.gov.sg`

### Installation

```bash
# Clone the repository
git clone https://github.com/BigBodyCobain/Shadowbroker.git
cd Shadowbroker

# Backend setup
cd backend
python -m venv venv
venv\Scripts\activate        # Windows
# source venv/bin/activate   # macOS/Linux
pip install .

# Optional helper scripts (creates venv + installs dev deps)
# Windows PowerShell
# .\backend\scripts\setup-venv.ps1
# macOS/Linux
# ./backend/scripts/setup-venv.sh

# Optional env check (prints warnings for missing keys)
# Windows PowerShell
# .\backend\scripts\check-env.ps1
# macOS/Linux
# ./backend/scripts/check-env.sh

# Create .env with your API keys
echo "AIS_API_KEY=your_aisstream_key" >> .env
echo "OPENSKY_CLIENT_ID=your_opensky_client_id" >> .env
echo "OPENSKY_CLIENT_SECRET=your_opensky_secret" >> .env

# Frontend setup
cd ../frontend
npm ci
```

### Running

```bash
# From the frontend directory — starts both frontend & backend concurrently
npm run dev
```

This starts:

* **Next.js** frontend on `http://localhost:3000`
* **FastAPI** backend on `http://localhost:8000`

### Pre-commit (Optional)

若你使用 pre-commit，只需从仓库根目录安装一次 hooks：

```bash
pre-commit install
```

### Local AIS Receiver (Optional)

你可以使用 RTL-SDR 接收器和开源 AIS 解码器 [AIS-catcher](https://github.com/jvde-github/AIS-catcher) 将本地 AIS 船舶数据喂入 ShadowBroker。这将为你提供所在区域的实时船舶覆盖——无需 API 密钥。

1. 插入 RTL-SDR 接收器
2. 安装 AIS-catcher ([releases](https://github.com/jvde-github/AIS-catcher/releases)) 或使用 Docker 镜像：
   ```bash
   docker run -d --device /dev/bus/usb \
     ghcr.io/jvde-github/ais-catcher -H http://host.docker.internal:4000/api/ais/feed interval 10
   ```
3. 或原生运行：
   ```bash
   AIS-catcher -H http://localhost:4000/api/ais/feed interval 10
   ```

AIS-catcher 解码 161.975 MHz 和 162.025 MHz 上的 VHF 无线电信号，并每 10 秒将解码后的船舶数据 POST 至 ShadowBroker。你的 SDR 天线检测到的船舶将与全球 AIS 流并列显示。

**Docker (ARM/Raspberry Pi)：** 请参阅 [docker-shipfeeder](https://github.com/sdr-enthusiasts/docker-shipfeeder) 获取针对 ARM 优化的生产级 Docker 镜像。

**注意：** AIS 覆盖范围取决于你的天线——基础设置通常为 20-40 海里，带海拔的船用 VHF 天线可达 60+ 海里。

---

## 🎛️ Data Layers

All 37 layers are independently toggleable from the left panel:

| Layer | Default | Description |
|---|---|---|
| Commercial Flights | ✅ ON | Airlines, cargo, GA aircraft |
| Private Flights | ✅ ON | Non-commercial private aircraft |
| Private Jets | ✅ ON | High-value bizjets with owner data |
| Military Flights | ✅ ON | Military & government aircraft |
| Tracked Aircraft | ✅ ON | Special interest watch list |
| GPS Jamming | ✅ ON | NAC-P degradation zones |
| Carriers / Mil / Cargo | ✅ ON | Navy carriers, cargo ships, tankers |
| Civilian Vessels | ✅ ON | Yachts, fishing, recreational |
| Cruise / Passenger | ✅ ON | Cruise ships and ferries |
| Tracked Yachts | ✅ ON | Billionaire & oligarch superyachts |
| Fishing Activity | ✅ ON | Global Fishing Watch vessel events |
| Trains | ✅ ON | Amtrak + European rail positions |
| Satellites | ✅ ON | Orbital assets by mission type |
| SatNOGS | ✅ ON | Amateur satellite ground stations |
| TinyGS | ✅ ON | LoRa satellite ground stations |
| Earthquakes (24h) | ✅ ON | USGS seismic events |
| Fire Hotspots (24h) | ✅ ON | NASA FIRMS VIIRS thermal anomalies |
| Volcanoes | ✅ ON | Smithsonian Holocene volcanoes |
| Weather Alerts | ✅ ON | Severe weather polygons |
| Air Quality (PM2.5) | ✅ ON | OpenAQ stations worldwide |
| Ukraine Frontline | ✅ ON | Live warfront positions |
| Ukraine Air Alerts | ✅ ON | Regional air raid alerts |
| Global Incidents | ✅ ON | GDELT conflict events |
| CCTV Mesh | ✅ ON | 11,000+ cameras across 13 sources, 6 countries |
| Internet Outages | ✅ ON | IODA regional connectivity alerts |
| Data Centers | ✅ ON | Global data center locations (2,000+) |
| Military Bases | ✅ ON | Global military installations |
| KiwiSDR Receivers | ✅ ON | Public SDR radio receivers |
| Meshtastic Nodes | ✅ ON | Mesh radio node positions |
| APRS | ✅ ON | Amateur radio positioning |
| Scanners | ✅ ON | Police/fire scanner feeds |
| Day / Night Cycle | ✅ ON | Solar terminator overlay |
| MODIS Terra (Daily) | ❌ OFF | NASA GIBS daily satellite imagery |
| High-Res Satellite | ❌ OFF | Esri sub-meter satellite imagery |
| Sentinel Hub | ❌ OFF | Copernicus CDSE Process API |
| VIIRS Nightlights | ❌ OFF | Night-time light change detection |
| Power Plants | ❌ OFF | 35,000+ global power plants |
| Shodan Overlay | ❌ OFF | Internet device search results |

---

## 🔧 Performance

The platform is optimized for handling massive real-time datasets:

* **Gzip Compression** — API payloads compressed ~92% (11.6 MB → 915 KB)
* **ETag Caching** — `304 Not Modified` responses skip redundant JSON parsing
* **Viewport Culling** — Only features within the visible map bounds (+20% buffer) are rendered
* **Imperative Map Updates** — High-volume layers (flights, satellites, fires) bypass React reconciliation via direct `setData()` calls
* **Clustered Rendering** — Ships, CCTV, earthquakes, and data centers use MapLibre clustering to reduce feature count
* **Debounced Viewport Updates** — 300ms debounce prevents GeoJSON rebuild thrash during pan/zoom; 2s debounce on dense layers (satellites, fires)
* **Position Interpolation** — Smooth 10s tick animation between data refreshes
* **React.memo** — Heavy components wrapped to prevent unnecessary re-renders
* **Coordinate Precision** — Lat/lng rounded to 5 decimals (~1m) to reduce JSON size

---

## 📁 Project Structure

```
Shadowbroker/
├── backend/
│   ├── main.py                     # FastAPI app, middleware, API routes (~4,000 lines)
│   ├── cctv.db                     # SQLite CCTV camera database (auto-generated)
│   ├── config/
│   │   └── news_feeds.json         # User-customizable RSS feed list
│   ├── services/
│   │   ├── data_fetcher.py         # Core scheduler — orchestrates all data sources
│   │   ├── ais_stream.py           # AIS WebSocket client (25K+ vessels)
│   │   ├── carrier_tracker.py      # OSINT carrier position estimator (GDELT news scraping)
│   │   ├── cctv_pipeline.py        # 13-source CCTV camera ingestion pipeline
│   │   ├── geopolitics.py          # GDELT + Ukraine frontline + air alerts
│   │   ├── region_dossier.py       # Right-click country/city intelligence
│   │   ├── radio_intercept.py      # Police scanner feeds + OpenMHZ
│   │   ├── kiwisdr_fetcher.py      # KiwiSDR receiver scraper
│   │   ├── sentinel_search.py      # Sentinel-2 STAC imagery search
│   │   ├── shodan_connector.py     # Shodan device search connector
│   │   ├── sigint_bridge.py        # APRS-IS TCP bridge
│   │   ├── network_utils.py        # HTTP client with curl fallback
│   │   ├── api_settings.py         # API key management
│   │   ├── news_feed_config.py     # RSS feed config manager
│   │   ├── fetchers/
│   │   │   ├── flights.py          # OpenSky, adsb.lol, GPS jamming, holding patterns
│   │   │   ├── geo.py              # AIS vessels, carriers, GDELT, fishing activity
│   │   │   ├── satellites.py       # CelesTrak TLE + SGP4 propagation
│   │   │   ├── earth_observation.py # Quakes, fires, volcanoes, air quality, weather
│   │   │   ├── infrastructure.py   # Data centers, power plants, military bases
│   │   │   ├── trains.py           # Amtrak + DigiTraffic European rail
│   │   │   ├── sigint.py           # SatNOGS, TinyGS, APRS, Meshtastic
│   │   │   ├── meshtastic_map.py   # Meshtastic MQTT + map node aggregation
│   │   │   ├── military.py         # Military aircraft classification
│   │   │   ├── news.py             # RSS intelligence feed aggregation
│   │   │   ├── financial.py        # Global markets data
│   │   │   └── ukraine_alerts.py   # Ukraine air raid alerts
│   │   └── mesh/                   # InfoNet / Wormhole protocol stack
│   │       ├── mesh_protocol.py    # Core mesh protocol + routing
│   │       ├── mesh_crypto.py      # Ed25519, X25519, AESGCM primitives
│   │       ├── mesh_hashchain.py   # Hash chain commitment system (~1,400 lines)
│   │       ├── mesh_router.py      # Multi-transport router (APRS, Meshtastic, WS)
│   │       ├── mesh_wormhole_persona.py  # Gate persona identity management
│   │       ├── mesh_wormhole_dead_drop.py # Dead Drop token-based DM mailbox
│   │       ├── mesh_wormhole_ratchet.py   # Double-ratchet DM scaffolding
│   │       ├── mesh_wormhole_gate_keys.py # Gate key management + rotation
│   │       ├── mesh_wormhole_seal.py      # Message sealing + unsealing
│   │       ├── mesh_merkle.py      # Merkle tree proofs for data commitment
│   │       ├── mesh_reputation.py  # Node reputation scoring
│   │       ├── mesh_oracle.py      # Oracle consensus protocol
│   │       └── mesh_secure_storage.py # Secure credential storage
├── frontend/
│   ├── src/
│   │   ├── app/
│   │   │   └── page.tsx            # Main dashboard — state, polling, layout
│   │   └── components/
│   │       ├── MaplibreViewer.tsx   # Core map — all GeoJSON layers
│   │       ├── MeshChat.tsx        # InfoNet / Mesh / Dead Drop chat panel
│   │       ├── MeshTerminal.tsx    # Draggable CLI terminal
│   │       ├── NewsFeed.tsx        # SIGINT feed + entity detail panels
│   │       ├── WorldviewLeftPanel.tsx   # Data layer toggles (35+ layers)
│   │       ├── WorldviewRightPanel.tsx  # Search + filter sidebar
│   │       ├── AdvancedFilterModal.tsx  # Airport/country/owner filtering
│   │       ├── MapLegend.tsx       # Dynamic legend with all icons
│   │       ├── MarketsPanel.tsx    # Global financial markets ticker
│   │       ├── RadioInterceptPanel.tsx # Scanner-style radio panel
│   │       ├── FindLocateBar.tsx   # Search/locate bar
│   │       ├── ChangelogModal.tsx  # Version changelog popup (auto-shows on upgrade)
│   │       ├── SettingsPanel.tsx   # API Keys + News Feed + Shodan config
│   │       ├── ScaleBar.tsx        # Map scale indicator
│   │       └── ErrorBoundary.tsx   # Crash recovery wrapper
│   └── package.json
```

---

## 🔑 Environment Variables

### Backend (`backend/.env`)

```env
# Required for airplane telemetry (NEW in v0.9.7 — startup env check flags these as critical)
# Free registration: https://opensky-network.org/index.php?option=com_users&view=registration
OPENSKY_CLIENT_ID=your_opensky_client_id      # OAuth2 — global flight state vectors
OPENSKY_CLIENT_SECRET=your_opensky_secret     # OAuth2 — paired with Client ID above

# Optional (enhances data quality)
AIS_API_KEY=your_aisstream_key                # Maritime vessel tracking (aisstream.io) — ships layer empty without it
LTA_ACCOUNT_KEY=your_lta_key                  # Singapore CCTV cameras
SHODAN_API_KEY=your_shodan_key                # Shodan device search overlay
SH_CLIENT_ID=your_sentinel_hub_id             # Copernicus CDSE Sentinel Hub imagery
SH_CLIENT_SECRET=your_sentinel_hub_secret     # Paired with Sentinel Hub Client ID
MESH_SAR_EARTHDATA_USER=                      # NASA Earthdata user (SAR Mode B — OPERA products)
MESH_SAR_EARTHDATA_TOKEN=                     # NASA Earthdata token (paired with user above)
MESH_SAR_COPERNICUS_USER=                     # Copernicus Data Space user (SAR Mode B — EGMS / EMS)
MESH_SAR_COPERNICUS_TOKEN=                    # Copernicus token (paired with user above)
OPENCLAW_ACCESS_TIER=restricted               # OpenClaw agent tier: "restricted" (read-only) or "full"

# Private-lane privacy-core pinning (required when Arti or RNS is enabled)
PRIVACY_CORE_MIN_VERSION=0.1.0
PRIVACY_CORE_ALLOWED_SHA256=your_privacy_core_sha256
# Optional override if you load a non-default shared library path
PRIVACY_CORE_LIB=
```

When `MESH_ARTI_ENABLED=true` or `MESH_RNS_ENABLED=true`, backend startup now fails closed unless the loaded `privacy-core` artifact reports a parseable version at or above `PRIVACY_CORE_MIN_VERSION` and matches one of the hashes in `PRIVACY_CORE_ALLOWED_SHA256`.

Generate the hash from the artifact you intend to ship:

```powershell
Get-FileHash .\privacy-core\target\release\privacy_core.dll -Algorithm SHA256
```

```bash
sha256sum ./privacy-core/target/release/libprivacy_core.so
```

Then confirm authenticated `GET /api/wormhole/status` or `GET /api/settings/wormhole-status` shows the same `privacy_core.version`, `privacy_core.library_path`, and `privacy_core.library_sha256`.

### Frontend

| Variable | Where to set | Purpose |
|---|---|---|
| `BACKEND_URL` | `environment` in `docker-compose.yml`, or shell env | URL the Next.js server uses to proxy API calls to the backend. Defaults to `http://backend:8000`. **Runtime variable — no rebuild needed.** |
| `BACKEND_PORT` | repo-root `.env` or shell env before `docker compose up` | Host port used to expose the backend API for local diagnostics. Defaults to `8000`; set `BACKEND_PORT=8001` if port 8000 is already in use. Does not change Docker-internal `BACKEND_URL`. |

**How it works:** The frontend proxies all `/api/*` requests through the Next.js server to `BACKEND_URL` using Docker's internal networking. Browsers only talk to port 3000; the backend host port is only for local diagnostics. For local dev without Docker, `BACKEND_URL` defaults to `http://localhost:8000`.

---

## 🤝 Contributors

ShadowBroker is built in the open. These people shipped real code:

| Who | What | PR |
|-----|------|----|
| [@Alienmajik](https://gitlab.com/Alienmajik) | Raspberry Pi 5 support — ARM64 packaging, headless deployment notes, runtime tuning for Pi-class hardware | — |
| [@wa1id](https://github.com/wa1id) | CCTV ingestion fix — threaded SQLite, persistent DB, startup hydration, cluster clickability | #92 |
| [@AlborzNazari](https://github.com/AlborzNazari) | Spain DGT + Madrid CCTV sources, STIX 2.1 threat intel export | #91 |
| [@adust09](https://github.com/adust09) | Power plants layer, East Asia intel coverage (JSDF bases, ICAO enrichment, Taiwan news, military classification) | #71, #72, #76, #77, #87 |
| [@Xpirix](https://github.com/Xpirix) | LocateBar style and interaction improvements | #78 |
| [@imqdcr](https://github.com/imqdcr) | Ship toggle split (4 categories) + stable MMSI/callsign entity IDs | — |
| [@csysp](https://github.com/csysp) | Dismissible threat alerts + stable entity IDs for GDELT & News | #48, #63 |
| [@suranyami](https://github.com/suranyami) | Parallel multi-arch Docker builds (11min → 3min) + runtime BACKEND_URL fix | #35, #44 |
| [@chr0n1x](https://github.com/chr0n1x) | Kubernetes / Helm chart architecture for HA deployments | — |

---

## ⚠️ Disclaimer

This tool is built entirely on publicly available, open-source intelligence (OSINT) data. No classified, restricted, or non-public data is used. Carrier positions are estimates based on public reporting. The military-themed UI is purely aesthetic.

---

## 📜 License

This project is for educational and personal research purposes. See individual API provider terms of service for data usage restrictions.

---

<p align="center">
  <sub>Built with ☕ and too many API calls</sub>
</p>
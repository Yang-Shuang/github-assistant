<div align="center">
<p align="center">
  <img src="assets/logo.png"/>
</p>
</div>

<div align="center">
<h2 style="font-size: 28px;">
	<img src="assets/tongyi.png" width="30px" style="vertical-align: middle; margin-right: 10px;">
 	Mobile-Agent：阿里巴巴通义实验室推出的强大 GUI 智能体家族
</h2>

<div align="center">
<p align="center">
  <img src="assets/gui_owl_15_logo.png"/>
</p>
</div>

<p align="center">
<a href="https://trendshift.io/repositories/7423" target="_blank"><img src="https://trendshift.io/api/badge/repositories/7423" alt="MobileAgent | Trendshift" style="width: 250px; height: 55px;" width="250" height="55"/></a>
</p>

👏 欢迎通过我们的 **[<img src="./assets/tongyi.png" width="14px" style="display:inline;"> ModelScope 在线演示](http://modelscope.cn/studios/MobileAgentTest/computer_use)** 或 **[<img src="./assets/aliyun.png" width="14px" style="display:inline;"> 百炼在线演示](https://bailian.console.aliyun.com/next?tab=demohouse#/experience/adk-computer-use/pc)** 体验 Mobile-Agent-v3.5！

❗️我们已在 <img src="./assets/aliyun.png" width="14px" style="display:inline;">百炼平台提供 Mobile-Agent-v3.5 API，供快速体验。请查看[文档](https://bailian.console.aliyun.com/cn-beijing?tab=model#/model-market/detail/gui-plus-2026-02-26)。

<p align="center">
	🤗 <a href="https://huggingface.co/collections/mPLUG/gui-owl-15" target="_blank">GUI-Owl-1.5 模型合集</a> |
	<img src="./assets/tongyi.png" width="14px" style="display:inline;"> <a href="https://modelscope.cn/collections/iic/GUI-Owl-15" target="_blank">GUI-Owl-1.5 模型合集</a> 
</p>
<p align="center">
	🤗 <a href="https://huggingface.co/mPLUG/GUI-Owl-32B" target="_blank">GUI-Owl-32B</a> | 
	<img src="./assets/tongyi.png" width="14px" style="display:inline;"> <a href="https://modelscope.cn/models/iic/GUI-Owl-32B" target="_blank">GUI-Owl-32B</a> ｜
	🤗 <a href="https://huggingface.co/mPLUG/GUI-Owl-7B" target="_blank">GUI-Owl-7B</a> |
	<img src="./assets/tongyi.png" width="14px" style="display:inline;"> <a href="https://modelscope.cn/models/iic/GUI-Owl-7B" target="_blank">GUI-Owl-7B</a>
</p>

</div>
<div align="center">
  <a href="README.md">English</a> | <a href="README_zh.md">简体中文</a>
<hr>
</div>

## 📢最新动态
- `[2026.5.12]` 🔥🔥🔥 **ToolCUA** 已发布！一款用于**最优 GUI-工具路径编排**的端到端 Computer Use Agent，采用两阶段训练流水线（轨迹感知工具合成 → 在线智能体强化学习），掌握何时使用 GUI 操作、调用工具以及在两者间切换。详见 [HuggingFace](https://huggingface.co/papers/2605.12481) 上的论文与模型权重。[Github](https://github.com/X-PLUG/ToolCUA)。
- `[2026.3.31]` 🔥🔥 Mobile-Agent-v3.5 现已上线**阿里云无影云手机** —— 一种基于云的 Android 环境，提供无缝的移动端使用体验。**了解更多**: [阿里云无影云手机](https://www.aliyun.com/product/cloud-phone) | [文档](https://help.aliyun.com/zh/ecp/quickly-experience-and-create-cloud-phone-mobileclaw)。
- `[2026.3.19]` 🔥🔥 **GUI-Owl-1.5** 系列模型现已支持在线推理。请参阅 [<img src="./assets/aliyun.png" width="14px" style="display:inline;"> **阿里云百炼平台**](https://bailian.console.aliyun.com/cn-beijing?tab=model#/model-market/detail/gui-plus-2026-02-26)，以及 [<img src="./assets/tongyi.png" width="14px" style="display:inline;"> **魔搭社区 API 推理**](https://modelscope.cn/models/iic/GUI-Owl-1.5-8B-Think)。
- `[2026.2.14]` 🔥 **GUI-Owl-1.5** 已发布！这是一个全新的原生多平台 GUI 智能体基础模型家族（包含 2B/4B/8B/32B/235B；指令版与思考版）。该下一代原生 GUI 智能体模型系列基于 Qwen3-VL 构建，支持**桌面/移动端/浏览器**自动化，在 **20+ 项 GUI 基准测试**中取得 SOTA 结果，并在端到端任务、定位（Grounding）、工具/MCP 调用及长程记忆方面表现优异。模型权重已开放于 [HuggingFace](https://huggingface.co/collections/mPLUG/gui-owl-15)。技术报告详见 [链接](https://arxiv.org/abs/2602.16855)。详细信息请参见 [GUI-Owl 1.5 README](https://github.com/X-PLUG/MobileAgent/tree/main/Mobile-Agent-v3.5)。
- `[2025.11.25]` GUI-Owl 系列模型现已支持在线推理，感谢[**阿里云百炼平台**](https://bailian.console.aliyun.com/?spm=5176.21213303.J_qCOwPWspKEuWcmp8qiZNQ.131.39712f3dOmFAxI&scm=20140722.S_card%40%40%E4%BA%A7%E5%93%81%40%402983180.S_card0.ID_card%40%40%E4%BA%A7%E5%93%81%40%402983180-RL_%E7%99%BE%E7%82%BC-LOC_search%7EUND%7Ecard%7EUND%7Eitem-OR_ser-V_3-P0_0&tab=model#/model-market/detail/gui-plus)提供的算力支持。请参阅 [链接](https://modelscope.cn/models/iic/GUI-Owl-7B)。
- `[2025.10.30]` 我们发布了 **OSWorld-MCP**，这是一个用于评估现实场景中模型上下文协议（MCP）工具调用能力的基准测试集。详见 [链接](https://github.com/X-PLUG/OSWorld-MCP)。
- `[2025.9.24]` 我们已发布基于无影云桌面和手机的 ModelScope 演示，无需本地部署模型或准备设备，只需输入指令即可体验 Mobile-Agent-v3！[<img src="./assets/tongyi.png" width="14px" style="display:inline;"> ModelScope 演示链接](https://modelscope.cn/studios/wangjunyang/Mobile-Agent-v3) 和 [<img src="./assets/aliyun.png" width="14px" style="display:inline;"> 百炼演示链接](https://bailian.console.aliyun.com/next?tab=demohouse#/experience/adk-computer-use/pc)。限时免费 Mobile-Agent-v3 API 请参见[文档](https://help.aliyun.com/zh/model-studio/ui-agent-api)。基于 Qwen-3-VL 的新版本即将推出。
- `[2025.9.19]` GUI-Critic-R1 已被 **第三十九届神经信息处理系统大会 (NeurIPS 2025)** 接收。 
- `[2025.9.16]` 我们发布了最新工作 **UI-S1: 通过半在线强化学习推进 GUI 自动化**。[论文](https://www.arxiv.org/abs/2509.11543)、[代码](https://github.com/X-PLUG/MobileAgent/tree/main/UI-S1)、[数据集](https://huggingface.co/datasets/mPLUG/UI_S1_dataset) 和 [模型](https://huggingface.co/mPLUG/UI-S1-7B) 现已开源。
- `[2025.9.16]` 我们已开源 GUI-Owl 和 Mobile-Agent-v3 在 OSWorld、AndroidWorld 及真实移动端场景下的代码。详见 [OSWorld 代码](https://github.com/X-PLUG/MobileAgent/tree/main/Mobile-Agent-v3#evaluation-on-osworld)。GUI-Owl 的 OSWorld RL 微调 [检查点](https://huggingface.co/mPLUG/GUI-Owl-7B-Desktop-RL) 也已发布。详见 [AndroidWorld 代码](https://github.com/X-PLUG/MobileAgent/tree/main/Mobile-Agent-v3#evaluation-on-androidworld) 和 [真实场景代码](https://github.com/X-PLUG/MobileAgent/tree/main/Mobile-Agent-v3#deploy-mobile-agent-v3-on-your-mobile-device)。
- `[2025.8.20]` 全新 **GUI-Owl** 与 **Mobile-Agent-v3** 已发布！技术报告请见 [此处](https://arxiv.org/abs/2508.15144)。模型权重将在 [GUI-Owl-7B](https://huggingface.co/mPLUG/GUI-Owl-7B) 和 [GUI-Owl-32B](https://huggingface.co/mPLUG/GUI-Owl-32B) 发布。
  - GUI-Owl 是一款具备 GUI 感知、定位与端到端操作能力的多模态跨平台 GUI VLM（视觉语言模型）。
  - Mobile-Agent-v3 是基于 GUI-Owl 的跨平台多智能体框架，提供规划、进度管理、反思和记忆等功能。
- `[2025.8.14]` Mobile-Agent-v3 荣获 ***第24届中国计算语言学全国会议 (CCL 2025)*** **最佳演示奖**。
- `[2025.3.17]` PC-Agent 已被 **ICLR 2025 Workshop** 接收。
- `[2024.9.26]` Mobile-Agent-v2 已被 **第三十八届神经信息处理系统大会 (NeurIPS 2024)** 接收。
- `[2024.7.29]` Mobile-Agent 荣获 ***第23届中国计算语言学全国会议 (CCL 2024)*** **最佳演示奖**。
- `[2024.3.10]` Mobile-Agent 已被 **ICLR 2024 Workshop** 接收。

## 📊实验结果

<div align="center">
<p align="center">
  <img src="assets/result.png"/>
</p>
</div>

## 👀核心特性

<div align="center">
<p align="center">
  <img src="assets/framework.png"/>
</p>
</div>

## 📝系列工作

- [**Mobile-Agent-v3.5**](https://github.com/X-PLUG/MobileAgent/tree/main/Mobile-Agent-v3.5) (预印本): 多平台基础 GUI 智能体。[**[论文]**](https://arxiv.org/abs/2602.16855) [**[代码]**](https://github.com/X-PLUG/MobileAgent/tree/main/Mobile-Agent-v3.5)
- [**Mobile-Agent-v3**](https://github.com/X-PLUG/MobileAgent/tree/main/Mobile-Agent-v3) (预印本): 多模态与跨平台 GUI 智能体。[**[论文]**](https://arxiv.org/abs/2508.15144) [**[代码]**](https://github.com/X-PLUG/MobileAgent/tree/main/Mobile-Agent-v3)
- [**UI-S1**](https://github.com/X-PLUG/MobileAgent/tree/main/UI-S1) (ACL 2026 主会): 通过半在线强化学习推进 GUI 自动化。[**[论文]**](https://arxiv.org/abs/2509.11543) [**[代码]**](https://github.com/X-PLUG/MobileAgent/tree/main/UI-S1) [**[数据集]**](https://huggingface.co/datasets/mPLUG/UI_S1_dataset)
- [**GUI-Critic-R1**](https://github.com/X-PLUG/MobileAgent/tree/main/GUI-Critic-R1) (NeurIPS 2025): 一种用于 GUI 自动化操作前错误诊断的审查器模型。[**[论文]**](https://arxiv.org/abs/2506.04614) [**[代码]**](https://github.com/X-PLUG/MobileAgent/tree/main/GUI-Critic-R1)
- [**PC-Agent**](https://github.com/X-PLUG/MobileAgent/tree/main/PC-Agent) (ICLR 2025 Workshop): 面向多模态 PC 操作的多智能体系统。[**[论文]**](https://arxiv.org/abs/2502.14282) [**[代码]**](https://github.com/X-PLUG/MobileAgent/tree/main/PC-Agent)
- [**Mobile-Agent-E**](https://github.com/X-PLUG/MobileAgent/tree/main/Mobile-Agent-E) (预印本): 面向手机自进化的多智能体系统。[**[论文]**](https://arxiv.org/abs/2501.11733) [**[代码]**](https://github.com/X-PLUG/MobileAgent/tree/main/Mobile-Agent-E)
- [**Mobile-Agent-v2**](https://github.com/X-PLUG/MobileAgent/tree/main/Mobile-Agent-v2) (NeurIPS 2024): 面向多模态手机操作的多智能体系统。[**[论文]**](https://arxiv.org/abs/2406.01014) [**[代码]**](https://github.com/X-PLUG/MobileAgent/tree/main/Mobile-Agent-v2)
- [**Mobile-Agent-v1**](https://github.com/X-PLUG/MobileAgent/tree/main/Mobile-Agent-v1) (ICLR 2024 Workshop): 面向多模态手机操作的单智能体系统。[**[论文]**](https://arxiv.org/abs/2401.16158) [**[代码]**](https://github.com/X-PLUG/MobileAgent/tree/main/Mobile-Agent-v1)

## 📺演示视频

<div align="left">
    <h3>了解 Mobile-Agent-v3.5</h3>
    <video src= "https://github.com/user-attachments/assets/97871c8c-5d1d-4f0f-aab0-84adddacbd0f"/>
</div>

### 💻PC + 🌐网页端

<div align="left">
    <h3>分别搜索 Apple 和 Nvidia 的股票价格。然后在 WPS Office 中创建新电子表格，在 A 列输入公司名称，B 列填入查到的股价。</h3>
    <video src= "https://github.com/user-attachments/assets/5dbc349b-0c99-4e66-a5c6-ad6d8accb933"/>
</div>

<div align="left">
    <h3>在 WPS Office 中新建文档并撰写一段约 12 号字体的阿里巴巴简介。随后在 Edge 浏览器中搜索阿里巴巴 Logo，复制一张图片粘贴至文档末尾。</h3>
    <video src= "https://github.com/user-attachments/assets/8122baec-b5a1-49d8-a47d-cb613d21ec72"/>
</div>

### 📱手机端

<div align="left">
    <h3>今天是 2025 年 2 月 15 日（星期日）。在携程上搜索五天后的广州至成都航班，查看最便宜的那班机票，然后搜索同路线的最便宜火车票并告诉我它们的价格。</h3>
    <video src= "https://github.com/user-attachments/assets/4c5f29b1-c319-41bb-876d-9915bc3e215f"/>
</div>

<div align="left">
    <h3>检查小红书和抖音上的“魔搭ModelScope社区”账号，然后告诉我这两个平台的总粉丝数。</h3>
    <video src= "https://github.com/user-attachments/assets/4ff3e951-f93a-49e8-b800-f060f765d67d"/>
</div>

## ⭐Star 历史

[![Star History Chart](https://api.star-history.com/svg?repos=X-PLUG/MobileAgent&type=Date)](https://star-history.com/#X-PLUG/MobileAgent&Date)

## 📑引用

如果您发现 Mobile-Agent 对您的研究或应用有所帮助，请使用以下 BibTeX 引用：
```
@article{xu2026mobile,
  title={Mobile-Agent-v3. 5: Multi-platform Fundamental GUI Agents},
  author={Xu, Haiyang and Zhang, Xi and Liu, Haowei and Wang, Junyang and Zhu, Zhaozai and Zhou, Shengjie and Hu, Xuhao and Gao, Feiyu and Cao, Junjie and Wang, Zihua and others},
  journal={arXiv preprint arXiv:2602.16855},
  year={2026}
}

@article{ye2025mobile,
  title={Mobile-Agent-v3: Foundamental Agents for GUI Automation},
  author={Ye, Jiabo and Zhang, Xi and Xu, Haiyang and Liu, Haowei and Wang, Junyang and Zhu, Zhaoqing and Zheng, Ziwei and Gao, Feiyu and Cao, Junjie and Lu, Zhengxi and others},
  journal={arXiv preprint arXiv:2508.15144},
  year={2025}
}

@article{lu2025ui,
  title={UI-S1: Advancing GUI Automation via Semi-online Reinforcement Learning},
  author={Lu, Zhengxi and Ye, Jiabo and Tang, Fei and Shen, Yongliang and Xu, Haiyang and Zheng, Ziwei and Lu, Weiming and Yan, Ming and Huang, Fei and Xiao, Jun and others},
  journal={arXiv preprint arXiv:2509.11543},
  year={2025}
}

@article{wanyan2025look,
  title={Look Before You Leap: A GUI-Critic-R1 Model for Pre-Operative Error Diagnosis in GUI Automation},
  author={Wanyan, Yuyang and Zhang, Xi and Xu, Haiyang and Liu, Haowei and Wang, Junyang and Ye, Jiabo and Kou, Yutong and Yan, Ming and Huang, Fei and Yang, Xiaoshan and others},
  journal={arXiv preprint arXiv:2506.04614},
  year={2025}
}

@article{liu2025pc,
  title={PC-Agent: A Hierarchical Multi-Agent Collaboration Framework for Complex Task Automation on PC},
  author={Liu, Haowei and Zhang, Xi and Xu, Haiyang and Wanyan, Yuyang and Wang, Junyang and Yan, Ming and Zhang, Ji and Yuan, Chunfeng and Xu, Changsheng and Hu, Weiming and Huang, Fei},
  journal={arXiv preprint arXiv:2502.14282},
  year={2025}
}

@article{wang2025mobile,
  title={Mobile-Agent-E: Self-Evolving Mobile Assistant for Complex Tasks},
  author={Wang, Zhenhailong and Xu, Haiyang and Wang, Junyang and Zhang, Xi and Yan, Ming and Zhang, Ji and Huang, Fei and Ji, Heng},
  journal={arXiv preprint arXiv:2501.11733},
  year={2025}
}

@article{wang2024mobile2,
  title={Mobile-Agent-v2: Mobile Device Operation Assistant with Effective Navigation via Multi-Agent Collaboration},
  author={Wang, Junyang and Xu, Haiyang and Jia, Haitao and Zhang, Xi and Yan, Ming and Shen, Weizhou and Zhang, Ji and Huang, Fei and Sang, Jitao},
  journal={arXiv preprint arXiv:2406.01014},
  year={2024}
}

@article{wang2024mobile,
  title={Mobile-Agent: Autonomous Multi-Modal Mobile Device Agent with Visual Perception},
  author={Wang, Junyang and Xu, Haiyang and Ye, Jiabo and Yan, Ming and Shen, Weizhou and Zhang, Ji and Huang, Fei and Sang, Jitao},
  journal={arXiv preprint arXiv:2401.16158},
  year={2024}
}
```
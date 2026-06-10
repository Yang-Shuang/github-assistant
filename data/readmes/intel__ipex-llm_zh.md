# 本项目已归档  
英特尔将不会为本项目提供或保证开发或支持，包括但不限于维护、错误修复、新版本发布或更新。  
英特尔不再接受对本项目的补丁提交。  
本项目已被发现存在已知安全问题。 

#  💫 Intel® LLM Library for PyTorch* 
<p>
  <b>< English</b> | <a href='./README.zh-CN.md'>中文</a> >
</p>

**`IPEX-LLM`** 是一款面向 Intel [GPU](docs/mddocs/Quickstart/install_windows_gpu.md)（例如带有核显的本地 PC、独立 GPU 如 Arc、Flex 和 Max）、[NPU](docs/mddocs/Quickstart/npu_quickstart.md) 和 CPU[^1] 的大语言模型加速库。
> [!NOTE]
> - *`IPEX-LLM` 与以下工具无缝集成：[llama.cpp](docs/mddocs/Quickstart/llamacpp_portable_zip_gpu_quickstart.md)、[Ollama](docs/mddocs/Quickstart/ollama_portable_zip_quickstart.md)、[vLLM](docs/mddocs/Quickstart/vLLM_quickstart.md)、[HuggingFace transformers](python/llm/example/GPU/HuggingFace)、[LangChain](python/llm/example/GPU/LangChain)、[LlamaIndex](python/llm/example/GPU/LlamaIndex)、[Text-Generation-WebUI](docs/mddocs/Quickstart/webui_quickstart.md)、[DeepSpeed-AutoTP](python/llm/example/GPU/Deepspeed-AutoTP)、[FastChat](docs/mddocs/Quickstart/fastchat_quickstart.md)、[Axolotl](docs/mddocs/Quickstart/axolotl_quickstart.md)、[HuggingFace PEFT](python/llm/example/GPU/LLM-Finetuning)、[HuggingFace TRL](python/llm/example/GPU/LLM-Finetuning/DPO)、[AutoGen](python/llm/example/CPU/Applications/autogen)、[ModelScope](python/llm/example/GPU/ModelScope-Models) 等。* 
> - ***70+ 个模型**已在 `ipex-llm` 上经过优化/验证（例如 Llama、Phi、Mistral、Mixtral、DeepSeek、Qwen、ChatGLM、MiniCPM、Qwen-VL、MiniCPM-V 等），具备最先进的 **LLM 优化**、**XPU 加速**和**低精度（FP8/FP6/FP4/INT4）支持**；完整列表请参见[此处](#verified-models)。*

## 最新更新 🔥 
- [2025/05] 现在，借助 `ipex-llm` 中的 [FlashMoE](docs/mddocs/Quickstart/flashmoe_quickstart.md)，你只需使用 1 或 2 张 Intel Arc GPU（如 A770 或 B580）即可运行 ***DeepSeek V3/R1 671B*** 和 ***Qwen3MoE 235B*** 模型。
- [2025/04] 我们发布了 `ipex-llm 2.2.0`，包含 [Ollama Portable Zip](docs/mddocs/Quickstart/ollama_portable_zip_quickstart.md) 和 [llama.cpp Portable Zip](docs/mddocs/Quickstart/llamacpp_portable_zip_gpu_quickstart.md)。
  > ⚠️ **警告（针对 llama.cpp Portable Zip）**  
  > *llama.cpp* 中基于 `mmap` 的模型加载在多租户或共享主机环境中可能通过侧信道泄露数据。  
  > 要禁用 `mmap`，请添加：  
  > ```bash
  > --no-mmap
  > ```
- [2025/04] 我们为 Intel GPU 添加了对 [PyTorch 2.6](docs/mddocs/Quickstart/install_pytorch26_gpu.md) 的支持。
- [2025/03] 我们在最新的 [llama.cpp Portable Zip](https://github.com/intel/ipex-llm/issues/12963#issuecomment-2724032898) 中添加了对 **Gemma3** 模型的支持。
- [2025/03] 借助最新的 [llama.cpp Portable Zip](docs/mddocs/Quickstart/llamacpp_portable_zip_gpu_quickstart.md#flashmoe-for-deepseek-v3r1)，你现在可以在 Xeon 上使用 1 或 2 张 Arc A770 运行 **DeepSeek-R1-671B-Q4_K_M**。
- [2025/02] 我们为 Intel **GPU**（[Windows](docs/mddocs/Quickstart/llamacpp_portable_zip_gpu_quickstart.md#windows-quickstart) 和 [Linux](docs/mddocs/Quickstart/llamacpp_portable_zip_gpu_quickstart.md#linux-quickstart)）以及 **NPU**（仅限 [Windows](docs/mddocs/Quickstart/llama_cpp_npu_portable_zip_quickstart.md)）添加了对 [llama.cpp Portable Zip](https://github.com/ipex-llm/ipex-llm/releases/tag/v2.3.0-nightly) 的支持。
- [2025/02] 我们添加了对 [Ollama Portable Zip](https://github.com/ipex-llm/ipex-llm/releases/tag/v2.3.0-nightly) 的支持，允许直接在 Intel **GPU**（[Windows](docs/mddocs/Quickstart/ollama_portable_zip_quickstart.md#windows-quickstart) 和 [Linux](docs/mddocs/Quickstart/ollama_portable_zip_quickstart.md#linux-quickstart)）上运行 Ollama（***无需手动安装***）。
- [2025/02] 我们支持在 Intel Arc GPU 上运行 [vLLM 0.6.6](docs/mddocs/DockerGuides/vllm_docker_quickstart.md)。
- [2025/01] 我们添加了在 Intel Arc [B580](docs/mddocs/Quickstart/bmg_quickstart.md) GPU 上运行 `ipex-llm` 的指南。
- [2025/01] 我们支持在 Intel GPU 上运行 [Ollama 0.5.4](docs/mddocs/Quickstart/ollama_quickstart.md)。
- [2024/12] 我们为 Intel Core Ultra [NPU](docs/mddocs/Quickstart/npu_quickstart.md)（包括 100H、200V、200K 和 200H 系列）添加了 ***Python*** 和 ***C++*** 支持。

<details><summary>更多更新</summary>
<br/>

- [2024/11] 我们支持在 Intel Arc GPU 上运行 [vLLM 0.6.2](docs/mddocs/DockerGuides/vllm_docker_quickstart.md)。
- [2024/07] 我们增加了对在 Intel GPU 上使用本地 LLM 运行微软 **GraphRAG** 的支持；快速入门指南请参见[此处](docs/mddocs/Quickstart/graphrag_quickstart.md)。
- [2024/07] 我们大幅增强了对大型多模态模型的支持，包括 [StableDiffusion](python/llm/example/GPU/HuggingFace/Multimodal/StableDiffusion)、[Phi-3-Vision](python/llm/example/GPU/HuggingFace/Multimodal/phi-3-vision)、[Qwen-VL](python/llm/example/GPU/HuggingFace/Multimodal/qwen-vl) 以及[更多模型](python/llm/example/GPU/HuggingFace/Multimodal)。
- [2024/07] 我们在 Intel [GPU](python/llm/example/GPU/HuggingFace/More-Data-Types) 上添加了 **FP6** 支持。 
- [2024/06] 我们为 Intel Core Ultra 处理器添加了实验性 **NPU** 支持；示例请参见[此处](python/llm/example/NPU/HF-Transformers-AutoModels)。 
- [2024/06] 我们大幅增强了 **流水线并行（Pipeline Parallel）**[推理](python/llm/example/GPU/Pipeline-Parallel-Inference)支持，使得使用 2 张或更多 Intel GPU（如 Arc）轻松运行大型 LLM 成为可能。
- [2024/06] 我们支持在 Intel [GPU](docs/mddocs/Quickstart/ragflow_quickstart.md) 上使用 `ipex-llm` 运行 **RAGFlow**。
- [2024/05] `ipex-llm` 现在支持在 Intel GPU 上使用 **Axolotl** 进行 LLM 微调；快速入门请参见[此处](docs/mddocs/Quickstart/axolotl_quickstart.md)。 
- [2024/05] 你现在可以轻松使用 **Docker** [镜像](#docker)运行 `ipex-llm` 的推理、服务部署和微调。
- [2024/05] 你现在只需使用“*[一条命令](docs/mddocs/Quickstart/install_windows_gpu.md#install-ipex-llm)*”即可在 Windows 上安装 `ipex-llm`。
- [2024/04] 你现在可以在 Intel GPU 上使用 `ipex-llm` 运行 **Open WebUI**；快速入门请参见[此处](docs/mddocs/Quickstart/open_webui_with_ollama_quickstart.md)。
- [2024/04] 你现在可以在 Intel GPU 上使用 `llama.cpp` 和 `ollama`（配合 `ipex-llm`）运行 **Llama 3**；快速入门请参见[此处](docs/mddocs/Quickstart/llama3_llamacpp_ollama_quickstart.md)。
- [2024/04] `ipex-llm` 现在支持在 Intel [GPU](python/llm/example/GPU/HuggingFace/LLM/llama3) 和 [CPU](python/llm/example/CPU/HF-Transformers-AutoModels/Model/llama3) 上运行 **Llama 3**。
- [2024/04] `ipex-llm` 现在提供 C++ 接口，可作为在 Intel GPU 上运行 [llama.cpp](docs/mddocs/Quickstart/llama_cpp_quickstart.md) 和 [ollama](docs/mddocs/Quickstart/ollama_quickstart.md) 的加速后端。
- [2024/03] `bigdl-llm` 现已更名为 `ipex-llm`（迁移指南请参见[此处](docs/mddocs/Quickstart/bigdl_llm_migration.md)）；原始 `BigDL` 项目可在[此处](https://github.com/intel-analytics/bigdl-2.x)找到。
- [2024/02] `ipex-llm` 现在支持直接从 [ModelScope](python/llm/example/GPU/ModelScope-Models)（[魔搭](python/llm/example/CPU/ModelScope-Models)）加载模型。
- [2024/02] `ipex-llm` 添加了初始的 **INT2** 支持（基于 llama.cpp [IQ2](python/llm/example/GPU/HuggingFace/Advanced-Quantizations/GGUF-IQ2) 机制），使得在显存为 16GB 的 Intel GPU 上运行大型 LLM（如 Mixtral-8x7B）成为可能。
- [2024/02] 用户现在可以通过 [Text-Generation-WebUI](https://github.com/intel-analytics/text-generation-webui) 图形界面使用 `ipex-llm`。
- [2024/02] `ipex-llm` 现在支持*[自预测解码（Self-Speculative Decoding）](docs/mddocs/Inference/Self_Speculative_Decoding.md)*，在实际应用中可为 Intel [GPU](python/llm/example/GPU/Speculative-Decoding) 和 [CPU](python/llm/example/CPU/Speculative-Decoding) 上的 FP16 与 BF16 推理延迟分别带来 **~30% 的加速**。
- [2024/02] `ipex-llm` 现在全面支持在 Intel GPU 上进行多种 LLM **微调**（包括 [LoRA](python/llm/example/GPU/LLM-Finetuning/LoRA)、[QLoRA](python/llm/example/GPU/LLM-Finetuning/QLoRA)、[DPO](python/llm/example/GPU/LLM-Finetuning/DPO)、[QA-LoRA](python/llm/example/GPU/LLM-Finetuning/QA-LoRA) 和 [ReLoRA](python/llm/example/GPU/LLM-Finetuning/ReLora)）。
- [2024/01] 借助 `ipex-llm` [QLoRA](python/llm/example/GPU/LLM-Finetuning/QLoRA)，我们在 8 张 Intel Max 1550 GPU 上仅用 **21 分钟**便完成了 LLaMA2-7B 的微调，用 **3.14 小时**完成了 LLaMA2-70B 的微调（针对 [Standford-Alpaca](python/llm/example/GPU/LLM-Finetuning/QLoRA/alpaca-qlora)；详见[博客](https://www.intel.com/content/www/us/en/developer/articles/technical/finetuning-llms-on-intel-gpus-using-bigdl-llm.html)）。 
- [2023/12] `ipex-llm` 现在支持 [ReLoRA](python/llm/example/GPU/LLM-Finetuning/ReLora)（参见*《["ReLoRA: High-Rank Training Through Low-Rank Updates"](https://arxiv.org/abs/2307.05695)*）。
- [2023/12] `ipex-llm` 现在支持在 Intel [GPU](python/llm/example/GPU/HuggingFace/LLM/mixtral) 和 [CPU](python/llm/example/CPU/HF-Transformers-AutoModels/Model/mixtral) 上运行 [Mixtral-8x7B](python/llm/example/GPU/HuggingFace/LLM/mixtral)。 
- [2023/12] `ipex-llm` 现在支持 [QA-LoRA](python/llm/example/GPU/LLM-Finetuning/QA-LoRA)（参见*《["QA-LoRA: Quantization-Aware Low-Rank Adaptation of Large Language Models"](https://arxiv.org/abs/2309.14717)*）。 
- [2023/12] `ipex-llm` 现在支持在 Intel ***GPU*** 上进行 [FP8 和 FP4 推理](python/llm/example/GPU/HuggingFace/More-Data-Types)。
- [2023/11] 现已提供直接将 [GGUF](python/llm/example/GPU/HuggingFace/Advanced-Quantizations/GGUF)、[AWQ](python/llm/example/GPU/HuggingFace/Advanced-Quantizations/AWQ) 和 [GPTQ](python/llm/example/GPU/HuggingFace/Advanced-Quantizations/GPTQ) 模型加载到 `ipex-llm` 的初始支持。
- [2023/11] `ipex-llm` 现在支持在 Intel [GPU](python/llm/example/GPU/vLLM-Serving) 和 [CPU](python/llm/example/CPU/vLLM-Serving) 上进行 [vLLM 连续批处理（Continuous Batching）](python/llm/example/GPU/vLLM-Serving)。
- [2023/10] `ipex-llm` 现在支持在 Intel [GPU](python/llm/example/GPU/LLM-Finetuning/QLoRA) 和 [CPU](python/llm/example/CPU/QLoRA-FineTuning) 上进行 [QLoRA 微调](python/llm/example/GPU/LLM-Finetuning/QLoRA)。
- [2023/10] `ipex-llm` 现在支持在 Intel CPU 和 GPU 上进行 [FastChat 服务部署（Serving）](python/llm/src/ipex_llm/llm/serving)。
- [2023/09] `ipex-llm` 现在支持 Intel GPU（包括核显、Arc、Flex 和 MAX）。
- [2023/09] `ipex-llm` [教程](https://github.com/intel-analytics/ipex-llm-tutorial) 已发布。
 
</details> 

## `ipex-llm` 演示

下方展示了使用 `ipex-llm` 在 *Intel Core Ultra 核显、Intel Core Ultra NPU、单张 Arc GPU 或多卡 Arc GPU* 上运行本地 LLM 的演示。

<table width="100%">
  <tr>
    <td align="center" colspan="1"><strong>Intel Core Ultra 核显</strong></td>
    <td align="center" colspan="1"><strong>Intel Core Ultra NPU</strong></td>
    <td align="center" colspan="1"><strong>双卡 Intel Arc dGPU</strong></td>
    <td align="center" colspan="1"><strong>Intel Xeon + Arc dGPU</strong></td>
  </tr>
  <tr>
    <td>
      <a href="https://llm-assets.readthedocs.io/en/latest/_images/mtl_mistral-7B_q4_k_m_ollama.gif" target="_blank">
        <img src="https://llm-assets.readthedocs.io/en/latest/_images/mtl_mistral-7B_q4_k_m_ollama.gif" width=100%; />
      </a>
    </td>
    <td>
      <a href="https://llm-assets.readthedocs.io/en/latest/_images/npu_llama3.2-3B.gif" target="_blank">
        <img src="https://llm-assets.readthedocs.io/en/latest/_images/npu_llama3.2-3B.gif" width=100%; />
      </a>
    </td>
    <td>
      <a href="https://llm-assets.readthedocs.io/en/latest/_images/2arc_DeepSeek-R1-Distill-Qwen-32B-Q4_K_M.gif" target="_blank">
        <img src="https://llm-assets.readthedocs.io/en/latest/_images/2arc_DeepSeek-R1-Distill-Qwen-32B-Q4_K_M.gif" width=100%; />
      </a>
    </td>
    <td>
      <a href="https://llm-assets.readthedocs.io/en/latest/_images/FlashMoE-Qwen3-235B.gif" target="_blank">
        <img src="https://llm-assets.readthedocs.io/en/latest/_images/FlashMoE-Qwen3-235B.gif" width=100%; />
      </a>
    </td>    
  </tr>
  <tr>
    <td align="center" width="25%">
      <a href="docs/mddocs/Quickstart/ollama_portable_zip_quickstart.md">Ollama <br> (Mistral-7B, Q4_K) </a>
    </td>
    <td align="center" width="25%">
      <a href="docs/mddocs/Quickstart/npu_quickstart.md">HuggingFace <br> (Llama3.2-3B, SYM_INT4)</a>
    </td>
    <td align="center" width="25%">
      <a href="docs/mddocs/Quickstart/llamacpp_portable_zip_gpu_quickstart.md">llama.cpp <br> (DeepSeek-R1-Distill-Qwen-32B, Q4_K)</a>
    </td>
    <td align="center" width="25%">
      <a href="docs/mddocs/Quickstart/flashmoe_quickstart.md">FlashMoE <br> (Qwen3MoE-235B, Q4_K) </a>
    </td>
  </tr>
</table>

<!--
See the demo of running [*Text-Generation-WebUI*](https://ipex-llm.readthedocs.io/en/latest/doc/LLM/Quickstart/webui_quickstart.html), [*local RAG using LangChain-Chatchat*](https://ipex-llm.readthedocs.io/en/latest/doc/LLM/Quickstart/chatchat_quickstart.html), [*llama.cpp*](https://ipex-llm.readthedocs.io/en/latest/doc/LLM/Quickstart/llamacpp_portable_zip_gpu_quickstart.md) and [*Ollama*](https://ipex-llm.readthedocs.io/en/latest/doc/LLM/Quickstart/ollama_quickstart.html) *(on either Intel Core Ultra laptop or Arc GPU)* with `ipex-llm`  below.

<table width="100%">
  <tr>
    <td align="center" colspan="2"><strong>Intel Core Ultra Laptop</strong></td>
    <td align="center" colspan="2"><strong>Intel Arc GPU</strong></td>
  </tr>
  <tr>
    <td>
      <video src="https://private-user-images.githubusercontent.com/1931082/319632616-895d56cd-e74b-4da1-b4d1-2157df341424.mp4?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MTIyNDE4MjUsIm5iZiI6MTcxMjI0MTUyNSwicGF0aCI6Ii8xOTMxMDgyLzMxOTYzMjYxNi04OTVkNTZjZC1lNzRiLTRkYTEtYjRkMS0yMTU3ZGYzNDE0MjQubXA0P1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQVZDT0RZTFNBNTNQUUs0WkElMkYyMDI0MDQwNCUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyNDA0MDRUMTQzODQ1WiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9Y2JmYzkxYWFhMGYyN2MxYTkxOTI3MGQ2NTFkZDY4ZjFjYjg3NmZhY2VkMzVhZTU2OGEyYjhjNzI5YTFhOGNhNSZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QmYWN0b3JfaWQ9MCZrZXlfaWQ9MCZyZXBvX2lkPTAifQ.Ga8mmCAO62DFCNzU1fdoyC_4MzqhDHzjZedzmi_2L-I" width=100% controls />
    </td>
    <td>
      <video src="https://private-user-images.githubusercontent.com/1931082/319625142-68da379e-59c6-4308-88e8-c17e40baba7b.mp4?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MTIyNDA2MzQsIm5iZiI6MTcxMjI0MDMzNCwicGF0aCI6Ii8xOTMxMDgyLzMxOTYyNTE0Mi02OGRhMzc5ZS01OWM2LTQzMDgtODhlOC1jMTdlNDBiYWJhN2IubXA0P1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQVZDT0RZTFNBNTNQUUs0WkElMkYyMDI0MDQwNCUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyNDA0MDRUMTQxODU0WiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9NzYwOWI4MmQxZjFhMjJlNGNhZTA3MGUyZDE4OTA0N2Q2YjQ4NTcwN2M2MTY1ODAwZmE3OTIzOWI0Y2U3YzYwNyZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QmYWN0b3JfaWQ9MCZrZXlfaWQ9MCZyZXBvX2lkPTAifQ.g0bYAj3J8IJci7pLzoJI6QDalyzXzMYtQkDY7aqZMc4" width=100% controls />
    </td>
    <td>
      <video src="https://private-user-images.githubusercontent.com/1931082/319625685-ff13b099-bcda-48f1-b11b-05421e7d386d.mp4?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MTIyNDA4MTcsIm5iZiI6MTcxMjI0MDUxNywicGF0aCI6Ii8xOTMxMDgyLzMxOTYyNTY4NS1mZjEzYjA5OS1iY2RhLTQ4ZjEtYjExYi0wNTQyMWU3ZDM4NmQubXA0P1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQVZDT0RZTFNBNTNQUUs0WkElMkYyMDI0MDQwNCUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyNDA0MDRUMTQyMTU3WiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9MWQ3MmEwZGRkNGVlY2RkNjAzMTliODM1NDEzODU3NWQ0ZGE4MjYyOGEyZjdkMjBiZjI0MjllYTU4ODQ4YzM0NCZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QmYWN0b3JfaWQ9MCZrZXlfaWQ9MCZyZXBvX2lkPTAifQ.OFxex8Yj6WyqJKMi6B1Q19KkmbYqYCg1rD49wUwxdXQ" width=100% controls />
    </td>
    <td>
      <video src="https://private-user-images.githubusercontent.com/1931082/325939544-2fc0ad5e-9ac7-4f95-b7b9-7885a8738443.mp4?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MTQxMjYwODAsIm5iZiI6MTcxNDEyNTc4MCwicGF0aCI6Ii8xOTMxMDgyLzMyNTkzOTU0NC0yZmMwYWQ1ZS05YWM3LTRmOTUtYjdiOS03ODg1YTg3Mzg0NDMubXA0P1gtQW16LUFsZ29yaXRobT1BV1M0LUhNQUMtU0hBMjU2JlgtQW16LUNyZWRlbnRpYWw9QUtJQVZDT0RZTFNBNTNQUUs0WkElMkYyMDI0MDQyNiUyRnVzLWVhc3QtMSUyRnMzJTJGYXdzNF9yZXF1ZXN0JlgtQW16LURhdGU9MjAyNDA0MjZUMTAwMzAwWiZYLUFtei1FeHBpcmVzPTMwMCZYLUFtei1TaWduYXR1cmU9YjZlZDE4YjFjZWJkMzQ4NmY3ZjNlMmRiYWUzMDYxMTI3YzcxYjRiYjgwNmE2NDliMjMwOTI0NWJhMDQ1NDY1YyZYLUFtei1TaWduZWRIZWFkZXJzPWhvc3QmYWN0b3JfaWQ9MCZrZXlfaWQ9MCZyZXBvX2lkPTAifQ.WfA2qwr8EP9W7a3oOYcKqaqsEKDlAkF254zbmn9dVv0" width=100% controls />
    </td>
  </tr>
  <tr>
    <td align="center" width="25%">
      <a href="https://ipex-llm.readthedocs.io/en/latest/doc/LLM/Quickstart/webui_quickstart.html">Text-Generation-WebUI</a>
    </td>
    <td align="center" width="25%">
      <a href="https://ipex-llm.readthedocs.io/en/latest/doc/LLM/Quickstart/chatchat_quickstart.html">Local RAG using LangChain-Chatchat</a>
    </td>
    <td align="center" width="25%">
      <a href="https://ipex-llm.readthedocs.io/en/latest/doc/LLM/Quickstart/llamacpp_portable_zip_gpu_quickstart.md">llama.cpp</a>
    </td>
    <td align="center" width="25%">
      <a href="https://ipex-llm.readthedocs.io/en/latest/doc/LLM/Quickstart/ollama_portable_zip_quickstart.md">Ollama</a>
    </td>  </tr>
</table>
-->

## `ipex-llm` 性能表现
下方展示在 *Intel Core Ultra* 和 *Intel Arc GPU* 上的 **Token 生成速度**[^1]（更多细节请参见 [[2]](https://www.intel.com/content/www/us/en/developer/articles/technical/accelerate-meta-llama3-with-intel-ai-solutions.html)[[3]](https://www.intel.com/content/www/us/en/developer/articles/technical/accelerate-microsoft-phi-3-models-intel-ai-soln.html)[[4]](https://www.intel.com/content/www/us/en/developer/articles/technical/intel-ai-solutions-accelerate-alibaba-qwen2-llms.html)）。

<table width="100%">
  <tr>
    <td>
      <a href="https://llm-assets.readthedocs.io/en/latest/_images/MTL_perf.jpg" target="_blank">
        <img src="https://llm-assets.readthedocs.io/en/latest/_images/MTL_perf.jpg" width=100%; />
      </a>
    </td>
    <td>
      <a href="https://llm-assets.readthedocs.io/en/latest/_images/Arc_perf.jpg" target="_blank">
        <img src="https://llm-assets.readthedocs.io/en/latest/_images/Arc_perf.jpg" width=100%; />
      </a>
    </td>
  </tr>
</table>

你可以按照 [基准测试指南](docs/mddocs/Quickstart/benchmark_quickstart.md) 自行运行 `ipex-llm` 性能基准测试。

## 模型精度
请参阅下方的 **困惑度（Perplexity）** 结果（使用 [此处](https://github.com/intel-analytics/ipex-llm/tree/main/python/llm/dev/benchmark/perplexity) 的脚本在 Wikitext 数据集上测试）。
|Perplexity                 |sym_int4	|q4_k	  |fp6	  |fp8_e5m2 |fp8_e4m3 |fp16   |
|---------------------------|---------|-------|-------|---------|---------|-------|
|Llama-2-7B-chat-hf	        |6.364 	  |6.218 	|6.092 	|6.180 	  |6.098    |6.096  | 
|Mistral-7B-Instruct-v0.2	  |5.365 	  |5.320 	|5.270 	|5.273 	  |5.246	   |5.244  |
|Baichuan2-7B-chat	         |6.734    |6.727	 |6.527	 |6.539	   |6.488	   |6.508  |
|Qwen1.5-7B-chat	           |8.865 	  |8.816 	|8.557 	|8.846 	  |8.530    |8.607  | 
|Llama-3.1-8B-Instruct	     |6.705	   |6.566	 |6.338	 |6.383	   |6.325	   |6.267  |
|gemma-2-9b-it	             |7.541	   |7.412	 |7.269	 |7.380	   |7.268	   |7.270  |
|Baichuan2-13B-Chat	        |6.313	   |6.160	 |6.070	 |6.145	   |6.086	   |6.031  |
|Llama-2-13b-chat-hf	       |5.449	   |5.422	 |5.341	 |5.384	   |5.332	   |5.329  |
|Qwen1.5-14B-Chat	          |7.529	   |7.520	 |7.367	 |7.504	   |7.297	   |7.334  |

[^1]: 性能因使用场景、配置及其他因素而异。`ipex-llm` 可能无法对非英特尔产品进行同等程度的优化。更多信息请访问 www.Intel.com/PerformanceIndex。

## `ipex-llm` 快速入门

### 使用方式
- [Ollama](docs/mddocs/Quickstart/ollama_portable_zip_quickstart.md)：在 Intel GPU 上运行 **Ollama**，***无需手动安装***
- [llama.cpp](docs/mddocs/Quickstart/llamacpp_portable_zip_gpu_quickstart.md)：在 Intel GPU 上运行 **llama.cpp**，***无需手动安装***
- [Arc B580](docs/mddocs/Quickstart/bmg_quickstart.md)：在 Intel Arc **B580** GPU 上使用 `ipex-llm`（支持 Ollama、llama.cpp、PyTorch、HuggingFace 等）
- [NPU](docs/mddocs/Quickstart/npu_quickstart.md)：在 Intel **NPU** 上运行 `ipex-llm`，支持 Python/C++ 或 [llama.cpp](docs/mddocs/Quickstart/llama_cpp_npu_portable_zip_quickstart.md) API
- [PyTorch/HuggingFace](docs/mddocs/Quickstart/install_windows_gpu.md)：在 Intel GPU（适用于 [Windows](docs/mddocs/Quickstart/install_windows_gpu.md) 和 [Linux](docs/mddocs/Quickstart/install_linux_gpu.md)）上使用 **PyTorch**、**HuggingFace**、**LangChain**、**LlamaIndex** 等（通过 `ipex-llm` Python 接口）
- [vLLM](docs/mddocs/Quickstart/vLLM_quickstart.md)：在 Intel [GPU](docs/mddocs/DockerGuides/vllm_docker_quickstart.md) 和 [CPU](docs/mddocs/DockerGuides/vllm_cpu_docker_quickstart.md) 上使用 **vLLM** 运行 `ipex-llm`
- [FastChat](docs/mddocs/Quickstart/fastchat_quickstart.md)：在 Intel GPU 和 CPU 上使用 **FastChat** 服务部署（Serving）运行 `ipex-llm`
- [多卡 GPU 推理服务](docs/mddocs/Quickstart/deepspeed_autotp_fastapi_quickstart.md)：利用 DeepSpeed AutoTP 和 FastAPI，在 Intel 多张 GPU 上运行 `ipex-llm` **服务部署**
- [Text-Generation-WebUI](docs/mddocs/Quickstart/webui_quickstart.md)：在 `oobabooga` **WebUI** 中运行 `ipex-llm`
- [Axolotl](docs/mddocs/Quickstart/axolotl_quickstart.md)：在 **Axolotl** 中使用 `ipex-llm` 进行 LLM 微调
- [基准测试](docs/mddocs/Quickstart/benchmark_quickstart.md)：在 Intel CPU 和 GPU 上运行 `ipex-llm`（延迟与吞吐量）的**性能基准测试**

### Docker 镜像
- [C++ GPU 推理](docs/mddocs/DockerGuides/docker_cpp_xpu_quickstart.md)：在 Intel GPU 上使用 `ipex-llm` 运行 `llama.cpp`、`ollama` 等
- [Python GPU 推理](docs/mddocs/DockerGuides/docker_pytorch_inference_gpu.md) : 在 Intel GPU 上使用 `ipex-llm` 运行 HuggingFace `transformers`、`LangChain`、`LlamaIndex`、`ModelScope` 等
- [GPU vLLM](docs/mddocs/DockerGuides/vllm_docker_quickstart.md)：在 Intel GPU 上使用 `ipex-llm` 运行 `vLLM` 服务部署
- [CPU vLLM](docs/mddocs/DockerGuides/vllm_cpu_docker_quickstart.md)：在 Intel CPU 上使用 `ipex-llm` 运行 `vLLM` 服务部署  
- [GPU FastChat](docs/mddocs/DockerGuides/fastchat_docker_quickstart.md)：在 Intel GPU 上使用 `ipex-llm` 运行 `FastChat` 服务部署
- [VSCode GPU 开发](docs/mddocs/DockerGuides/docker_run_pytorch_inference_in_vscode.md)：在 Intel GPU 上通过 VSCode 使用 Python 运行和开发 `ipex-llm` 应用

### 应用程序集成
- [GraphRAG](docs/mddocs/Quickstart/graphrag_quickstart.md)：使用本地 LLM（配合 `ipex-llm`）运行微软的 `GraphRAG`
- [RAGFlow](docs/mddocs/Quickstart/ragflow_quickstart.md)：使用 `ipex-llm` 运行 `RAGFlow`（开源 RAG 引擎）
- [LangChain-Chatchat](docs/mddocs/Quickstart/chatchat_quickstart.md)：使用 `ipex-llm` 运行 `LangChain-Chatchat`（基于 RAG 管道的知识库问答）
- [Coding copilot](docs/mddocs/Quickstart/continue_quickstart.md)：在 VSCode 中使用 `Continue`（编程助手，coding copilot）配合 `ipex-llm`
- [Open WebUI](docs/mddocs/Quickstart/open_webui_with_ollama_quickstart.md)：使用 `ipex-llm` 运行 `Open WebUI`
- [PrivateGPT](docs/mddocs/Quickstart/privateGPT_quickstart.md)：使用 `ipex-llm` 运行 `PrivateGPT` 实现文档交互
- [Dify platform](docs/mddocs/Quickstart/dify_quickstart.md)：在 `Dify`（生产级 LLM 应用开发平台）中使用 `ipex-llm`

### 安装指南 
- [Windows GPU](docs/mddocs/Quickstart/install_windows_gpu.md)：在 Windows 上搭配 Intel GPU 安装 `ipex-llm`
- [Linux GPU](docs/mddocs/Quickstart/install_linux_gpu.md)：在 Linux 上搭配 Intel GPU 安装 `ipex-llm`
- *更多细节请参阅[完整安装指南](docs/mddocs/Overview/install.md)*

### 代码示例
- #### 低精度推理
  - [INT4 推理](python/llm/example/GPU/HuggingFace/LLM)：在 Intel [GPU](python/llm/example/GPU/HuggingFace/LLM) 和 [CPU](python/llm/example/CPU/HF-Transformers-AutoModels/Model) 上进行 **INT4** LLM 推理
  - [FP8/FP6/FP4 推理](python/llm/example/GPU/HuggingFace/More-Data-Types)：在 Intel [GPU](python/llm/example/GPU/HuggingFace/More-Data-Types) 上进行 **FP8**、**FP6** 和 **FP4** LLM 推理
  - [INT8 推理](python/llm/example/GPU/HuggingFace/More-Data-Types)：在 Intel [GPU](python/llm/example/GPU/HuggingFace/More-Data-Types) 和 [CPU](python/llm/example/CPU/HF-Transformers-AutoModels/More-Data-Types) 上进行 **INT8** LLM 推理
  - [INT2 推理](python/llm/example/GPU/HuggingFace/Advanced-Quantizations/GGUF-IQ2)：在 Intel [GPU](python/llm/example/GPU/HuggingFace/Advanced-Quantizations/GGUF-IQ2) 上进行 **INT2** LLM 推理（基于 llama.cpp IQ2 机制）
- #### FP16/BF16 推理
  - 在 Intel [GPU](python/llm/example/GPU/Speculative-Decoding) 上进行 **FP16** LLM 推理，支持可选的 [自预测解码](docs/mddocs/Inference/Self_Speculative_Decoding.md) 优化
  - 在 Intel [CPU](python/llm/example/CPU/Speculative-Decoding) 上进行 **BF16** LLM 推理，支持可选的 [自预测解码](docs/mddocs/Inference/Self_Speculative_Decoding.md) 优化
- #### 分布式推理
  - 在 Intel [GPU](python/llm/example/GPU/Pipeline-Parallel-Inference) 上进行 **流水线并行（Pipeline Parallel）**推理
  - 在 Intel [GPU](python/llm/example/GPU/Deepspeed-AutoTP) 上使用 **DeepSpeed AutoTP** 进行推理
- #### 保存与加载
  - [低精度模型](python/llm/example/CPU/HF-Transformers-AutoModels/Save-Load)：保存和加载 `ipex-llm` 低精度模型（INT4/FP4/FP6/INT8/FP8/FP16 等）
  - [GGUF](python/llm/example/GPU/HuggingFace/Advanced-Quantizations/GGUF)：直接将 GGUF 模型加载到 `ipex-llm`
  - [AWQ](python/llm/example/GPU/HuggingFace/Advanced-Quantizations/AWQ)：直接将 AWQ 模型加载到 `ipex-llm`
  - [GPTQ](python/llm/example/GPU/HuggingFace/Advanced-Quantizations/GPTQ)：直接将 GPTQ 模型加载到 `ipex-llm`
- #### 微调
  - 在 Intel [GPU](python/llm/example/GPU/LLM-Finetuning) 上进行 LLM 微调，包括 [LoRA](python/llm/example/GPU/LLM-Finetuning/LoRA)、[QLoRA](python/llm/example/GPU/LLM-Finetuning/QLoRA)、[DPO](python/llm/example/GPU/LLM-Finetuning/DPO)、[QA-LoRA](python/llm/example/GPU/LLM-Finetuning/QA-LoRA) 和 [ReLoRA](python/llm/example/GPU/LLM-Finetuning/ReLora)
  - 在 Intel [CPU](python/llm/example/CPU/QLoRA-FineTuning) 上进行 QLoRA 微调
- #### 集成社区库
  - [HuggingFace transformers](python/llm/example/GPU/HuggingFace)
  - [标准 PyTorch 模型](python/llm/example/GPU/PyTorch-Models)
  - [LangChain](python/llm/example/GPU/LangChain)
  - [LlamaIndex](python/llm/example/GPU/LlamaIndex)
  - [DeepSpeed-AutoTP](python/llm/example/GPU/Deepspeed-AutoTP)
  - [Axolotl](docs/mddocs/Quickstart/axolotl_quickstart.md)
  - [HuggingFace PEFT](python/llm/example/GPU/LLM-Finetuning/HF-PEFT)
  - [HuggingFace TRL](python/llm/example/GPU/LLM-Finetuning/DPO)
  - [AutoGen](python/llm/example/CPU/Applications/autogen)
  - [ModelScope](python/llm/example/GPU/ModelScope-Models)
- [教程](https://github.com/intel-analytics/ipex-llm-tutorial)

## API 文档
- [类 HuggingFace Transformers 风格的 API（自动加载类）](docs/mddocs/PythonAPI/transformers.md)
- [任意 PyTorch 模型的 API](https://github.com/intel-analytics/ipex-llm/blob/main/docs/mddocs/PythonAPI/optimize.md)

## 常见问题解答 (FAQ)
- [常见问题与故障排除](docs/mddocs/Overview/FAQ/faq.md)

## 已验证模型
已有超过 70 个模型在 `ipex-llm` 上经过优化/验证，包括 *LLaMA/LLaMA2、Mistral、Mixtral、Gemma、LLaVA、Whisper、ChatGLM2/ChatGLM3、Baichuan/Baichuan2、Qwen/Qwen-1.5、InternLM* 等；列表如下。
  
| Model      | CPU Example                                  | GPU Example                                  | NPU Example                                  |
|------------|----------------------------------------------|----------------------------------------------|----------------------------------------------|
| LLaMA  | [link1](python/llm/example/CPU/Native-Models), [link2](python/llm/example/CPU/HF-Transformers-AutoModels/Model/vicuna) |[link](python/llm/example/GPU/HuggingFace/LLM/vicuna)|
| LLaMA 2    | [link1](python/llm/example/CPU/Native-Models), [link2](python/llm/example/CPU/HF-Transformers-AutoModels/Model/llama2) | [link](python/llm/example/GPU/HuggingFace/LLM/llama2)  | [Python link](python/llm/example/NPU/HF-Transformers-AutoModels/LLM), [C++ link](python/llm/example/NPU/HF-Transformers-AutoModels/LLM/CPP_Examples) |
| LLaMA 3    | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/llama3) | [link](python/llm/example/GPU/HuggingFace/LLM/llama3)  | [Python link](python/llm/example/NPU/HF-Transformers-AutoModels/LLM), [C++ link](python/llm/example/NPU/HF-Transformers-AutoModels/LLM/CPP_Examples) |
| LLaMA 3.1    | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/llama3.1) | [link](python/llm/example/GPU/HuggingFace/LLM/llama3.1)  |
| LLaMA 3.2    |  | [link](python/llm/example/GPU/HuggingFace/LLM/llama3.2)  | [Python link](python/llm/example/NPU/HF-Transformers-AutoModels/LLM), [C++ link](python/llm/example/NPU/HF-Transformers-AutoModels/LLM/CPP_Examples) |
| LLaMA 3.2-Vision    |  | [link](python/llm/example/GPU/PyTorch-Models/Model/llama3.2-vision/)  |
| ChatGLM    | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/chatglm)   |    | 
| ChatGLM2   | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/chatglm2)  | [link](python/llm/example/GPU/HuggingFace/LLM/chatglm2)   |
| ChatGLM3   | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/chatglm3)  | [link](python/llm/example/GPU/HuggingFace/LLM/chatglm3)   |
| GLM-4      | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/glm4)      | [link](python/llm/example/GPU/HuggingFace/LLM/glm4)       |
| GLM-4V     | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/glm-4v)    | [link](python/llm/example/GPU/HuggingFace/Multimodal/glm-4v)     |
| GLM-Edge   |  | [link](python/llm/example/GPU/HuggingFace/LLM/glm-edge) | [Python link](python/llm/example/NPU/HF-Transformers-AutoModels/LLM) |
| GLM-Edge-V   |  | [link](python/llm/example/GPU/HuggingFace/Multimodal/glm-edge-v) |
| Mistral    | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/mistral)   | [link](python/llm/example/GPU/HuggingFace/LLM/mistral)    |
| Mixtral    | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/mixtral)   | [link](python/llm/example/GPU/HuggingFace/LLM/mixtral)    |
| Falcon     | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/falcon)    | [link](python/llm/example/GPU/HuggingFace/LLM/falcon)     |
| MPT        | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/mpt)       | [link](python/llm/example/GPU/HuggingFace/LLM/mpt)        |
| Dolly-v1   | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/dolly_v1)  | [link](python/llm/example/GPU/HuggingFace/LLM/dolly-v1)   | 
| Dolly-v2   | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/dolly_v2)  | [link](python/llm/example/GPU/HuggingFace/LLM/dolly-v2)   | 
| Replit Code| [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/replit)    | [link](python/llm/example/GPU/HuggingFace/LLM/replit)     |
| RedPajama  | [link1](python/llm/example/CPU/Native-Models), [link2](python/llm/example/CPU/HF-Transformers-AutoModels/Model/redpajama) |    | 
| Phoenix    | [link1](python/llm/example/CPU/Native-Models), [link2](python/llm/example/CPU/HF-Transformers-AutoModels/Model/phoenix)   |    | 
| StarCoder  | [link1](python/llm/example/CPU/Native-Models), [link2](python/llm/example/CPU/HF-Transformers-AutoModels/Model/starcoder) | [link](python/llm/example/GPU/HuggingFace/LLM/starcoder) | 
| Baichuan   | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/baichuan)  | [link](python/llm/example/GPU/HuggingFace/LLM/baichuan)   |
| Baichuan2  | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/baichuan2) | [link](python/llm/example/GPU/HuggingFace/LLM/baichuan2)  | [Python link](python/llm/example/NPU/HF-Transformers-AutoModels/LLM) |
| InternLM   | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/internlm)  | [link](python/llm/example/GPU/HuggingFace/LLM/internlm)   |
| InternVL2   |   | [link](python/llm/example/GPU/HuggingFace/Multimodal/internvl2)   |
| Qwen       | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/qwen)      | [link](python/llm/example/GPU/HuggingFace/LLM/qwen)       |
| Qwen1.5 | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/qwen1.5) | [link](python/llm/example/GPU/HuggingFace/LLM/qwen1.5) |
| Qwen2 | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/qwen2) | [link](python/llm/example/GPU/HuggingFace/LLM/qwen2) | [Python link](python/llm/example/NPU/HF-Transformers-AutoModels/LLM), [C++ link](python/llm/example/NPU/HF-Transformers-AutoModels/LLM/CPP_Examples) |
| Qwen2.5 |  | [link](python/llm/example/GPU/HuggingFace/LLM/qwen2.5) | [Python link](python/llm/example/NPU/HF-Transformers-AutoModels/LLM), [C++ link](python/llm/example/NPU/HF-Transformers-AutoModels/LLM/CPP_Examples) |
| Qwen-VL    | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/qwen-vl)   | [link](python/llm/example/GPU/HuggingFace/Multimodal/qwen-vl)    |
| Qwen2-VL    || [link](python/llm/example/GPU/HuggingFace/Multimodal/qwen2-vl)    |
| Qwen2-Audio    |  | [link](python/llm/example/GPU/HuggingFace/Multimodal/qwen2-audio)    |
| Aquila     | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/aquila)    | [link](python/llm/example/GPU/HuggingFace/LLM/aquila)     |
| Aquila2     | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/aquila2)    | [link](python/llm/example/GPU/HuggingFace/LLM/aquila2)     |
| MOSS       | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/moss)      |    | 
| Whisper    | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/whisper)   | [link](python/llm/example/GPU/HuggingFace/Multimodal/whisper)    |
| Phi-1_5    | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/phi-1_5)   | [link](python/llm/example/GPU/HuggingFace/LLM/phi-1_5)    |
| Flan-t5    | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/flan-t5)   | [link](python/llm/example/GPU/HuggingFace/LLM/flan-t5)    |
| LLaVA      | [link](python/llm/example/CPU/PyTorch-Models/Model/llava)                 | [link](python/llm/example/GPU/PyTorch-Models/Model/llava)                  |
| CodeLlama  | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/codellama) | [link](python/llm/example/GPU/HuggingFace/LLM/codellama)  |
| Skywork      | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/skywork)                 |    |
| InternLM-XComposer  | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/internlm-xcomposer)   |    |
| WizardCoder-Python | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/wizardcoder-python) | |
| CodeShell | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/codeshell) | |
| Fuyu      | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/fuyu) | |
| Distil-Whisper | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/distil-whisper) | [link](python/llm/example/GPU/HuggingFace/Multimodal/distil-whisper) |
| Yi | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/yi) | [link](python/llm/example/GPU/HuggingFace/LLM/yi) |
| BlueLM | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/bluelm) | [link](python/llm/example/GPU/HuggingFace/LLM/bluelm) |
| Mamba | [link](python/llm/example/CPU/PyTorch-Models/Model/mamba) | [link](python/llm/example/GPU/PyTorch-Models/Model/mamba) |
| SOLAR | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/solar) | [link](python/llm/example/GPU/HuggingFace/LLM/solar) |
| Phixtral | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/phixtral) | [link](python/llm/example/GPU/HuggingFace/LLM/phixtral) |
| InternLM2 | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/internlm2) | [link](python/llm/example/GPU/HuggingFace/LLM/internlm2) |
| RWKV4 |  | [link](python/llm/example/GPU/HuggingFace/LLM/rwkv4) |
| RWKV5 |  | [link](python/llm/example/GPU/HuggingFace/LLM/rwkv5) |
| Bark | [link](python/llm/example/CPU/PyTorch-Models/Model/bark) | [link](python/llm/example/GPU/PyTorch-Models/Model/bark) |
| SpeechT5 |  | [link](python/llm/example/GPU/PyTorch-Models/Model/speech-t5) |
| DeepSeek-MoE | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/deepseek-moe) |  |
| Ziya-Coding-34B-v1.0 | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/ziya) | |
| Phi-2 | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/phi-2) | [link](python/llm/example/GPU/HuggingFace/LLM/phi-2) |
| Phi-3 | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/phi-3) | [link](python/llm/example/GPU/HuggingFace/LLM/phi-3) |
| Phi-3-vision | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/phi-3-vision) | [link](python/llm/example/GPU/HuggingFace/Multimodal/phi-3-vision) |
| Yuan2 | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/yuan2) | [link](python/llm/example/GPU/HuggingFace/LLM/yuan2) |
| Gemma | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/gemma) | [link](python/llm/example/GPU/HuggingFace/LLM/gemma) |
| Gemma2 |  | [link](python/llm/example/GPU/HuggingFace/LLM/gemma2) |
| DeciLM-7B | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/deciLM-7b) | [link](python/llm/example/GPU/HuggingFace/LLM/deciLM-7b) |
| Deepseek | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/deepseek) | [link](python/llm/example/GPU/HuggingFace/LLM/deepseek) |
| StableLM | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/stablelm) | [link](python/llm/example/GPU/HuggingFace/LLM/stablelm) |
| CodeGemma | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/codegemma) | [link](python/llm/example/GPU/HuggingFace/LLM/codegemma) |
| Command-R/cohere | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/cohere) | [link](python/llm/example/GPU/HuggingFace/LLM/cohere) |
| CodeGeeX2 | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/codegeex2) | [link](python/llm/example/GPU/HuggingFace/LLM/codegeex2) |
| MiniCPM | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/minicpm) | [link](python/llm/example/GPU/HuggingFace/LLM/minicpm) | [Python link](python/llm/example/NPU/HF-Transformers-AutoModels/LLM), [C++ link](python/llm/example/NPU/HF-Transformers-AutoModels/LLM/CPP_Examples) |
| MiniCPM3 |  | [link](python/llm/example/GPU/HuggingFace/LLM/minicpm3) |
| MiniCPM-V |  | [link](python/llm/example/GPU/HuggingFace/Multimodal/MiniCPM-V) |
| MiniCPM-V-2 | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/minicpm-v-2) | [link](python/llm/example/GPU/HuggingFace/Multimodal/MiniCPM-V-2) |
| MiniCPM-Llama3-V-2_5 |  | [link](python/llm/example/GPU/HuggingFace/Multimodal/MiniCPM-Llama3-V-2_5) | [Python link](python/llm/example/NPU/HF-Transformers-AutoModels/Multimodal) |
| MiniCPM-V-2_6 | [link](python/llm/example/CPU/HF-Transformers-AutoModels/Model/minicpm-v-2_6) | [link](python/llm/example/GPU/HuggingFace/Multimodal/MiniCPM-V-2_6) | [Python link](python/llm/example/NPU/HF-Transformers-AutoModels/Multimodal) |
| MiniCPM-o-2_6 | | [link](python/llm/example/GPU/HuggingFace/Multimodal/MiniCPM-o-2_6/) |
| Janus-Pro | | [link](python/llm/example/GPU/HuggingFace/Multimodal/janus-pro/) |
| Moonlight | |[link](python/llm/example/GPU/HuggingFace/LLM/moonlight/) |
| StableDiffusion | | [link](python/llm/example/GPU/HuggingFace/Multimodal/StableDiffusion) |
| Bce-Embedding-Base-V1 | | | [Python link](python/llm/example/NPU/HF-Transformers-AutoModels/Embedding) |
| Speech_Paraformer-Large | | | [Python link](python/llm/example/NPU/HF-Transformers-AutoModels/Multimodal) |

## 获取支持
- 请通过提交 [Github Issue](https://github.com/intel-analytics/ipex-llm/issues) 报告错误或提出功能请求
- 请通过创建草稿形式的 [GitHub Security Advisory](https://github.com/intel-analytics/ipex-llm/security/advisories) 报告安全漏洞
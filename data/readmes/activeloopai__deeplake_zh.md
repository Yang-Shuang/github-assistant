<img src="https://static.scarf.sh/a.png?x-pxid=bc3c57b0-9a65-49fe-b8ea-f711c4d35b82" /><p align="center">
     <img src="https://i.postimg.cc/rsjcWc3S/deeplake-logo.png" width="400"/>
</h1>

</br>

<h1 align="center">Deep Lake：AI 数据库</h1>

<p align="center">
    <a href="https://pypi.org/project/deeplake/"><img src="https://badge.fury.io/py/deeplake.svg" alt="PyPI version" height="18"></a>
    <a href="https://pepy.tech/project/deeplake"><img src="https://static.pepy.tech/badge/deeplake" alt="PyPI version" height="18"></a>
  <h3 align="center">
   <a href="https://docs.deeplake.ai/?utm_source=github&utm_medium=github&utm_campaign=github_readme&utm_id=readme"><b>文档</b></a> &bull;
   <a href="https://docs.deeplake.ai/latest/getting-started/quickstart/?utm_source=github&utm_medium=github&utm_campaign=github_readme&utm_id=readme"><b>快速入门</b></a> &bull;
   <a href="https://docs.deeplake.ai/latest/api/dataset/?utm_source=github&utm_medium=github&utm_campaign=github_readme&utm_id=readme"><b>API 参考</b></a> &bull;  
   <a href="http://learn.activeloop.ai"><b>LangChain 与向量数据库课程</b></a> &bull;
   <a href="https://www.activeloop.ai/resources/?utm_source=github&utm_medium=github&utm_campaign=github_readme&utm_id=readme"><b>博客</b></a> &bull;
   <a href="https://www.deeplake.ai/?utm_source=github&utm_medium=github&utm_campaign=github_readme&utm_id=readme"><b>白皮书</b></a> &bull;  
  <a href="http://slack.activeloop.ai"><b>Slack</b></a> &bull;
  <a href="https://twitter.com/intent/tweet?url=https%3A%2F%2Factiveloop.ai%2F&via=activeloopai&text=Deep%20Lake%20is%20the%20Database%20for%20all%20AI%20data.%20Check%20it%20out%21&hashtags=DeepLake%2Cactiveloop%2Copensource"><b>Twitter</b></a>
 </h3>

## Deep Lake 是什么？

Deep Lake 是一款由专为深度学习应用优化的存储格式驱动的 AI 数据库。Deep Lake 可用于：

1. 构建大语言模型（LLM）应用时，存储和搜索数据及向量
2. 训练深度学习模型时的数据集管理
   
Deep Lake 通过提供全数据类型存储（嵌入向量、音频、文本、视频、图像、DICOM、PDF、标注等 [更多类型](https://docs.deeplake.ai/latest/api/types/)）、查询与向量搜索、大规模训练时的数据流式传输、数据版本控制与血缘追踪，以及与 LangChain、LlamaIndex、Weights & Biases 等流行工具的集成，简化了企业级基于 LLM 产品的部署。Deep Lake 支持任意规模的数据，采用无服务器架构，并允许你将所有数据存储在自己的云端及统一位置。Deep Lake 已被英特尔、拜耳放射科、Matterport、ZERO Systems、红十字会、耶鲁大学与牛津大学等采用。 

### Deep Lake 包含以下功能：

<details>
  <summary><b>多云支持（S3、GCP、Azure）</b></summary>
使用统一的 API 将数据集上传至 S3、Azure、GCP、Activeloop 云、本地存储或内存中，也可从中下载和流式读取。兼容任何 S3 兼容型存储（如 MinIO）。 
</details>
<details>
  <summary><b>原生压缩与类 NumPy 的惰性索引</b></summary>
以原生压缩格式存储图像、音频和视频。像操作系统内存中的 NumPy 数组集合一样，对数据进行切片、索引、迭代和交互。Deep Lake 仅在需要时（例如训练模型或执行查询）才惰性加载数据。
</details>
<details>
  <summary><b>主流深度学习框架的数据加载器</b></summary>
Deep Lake 内置 PyTorch 和 TensorFlow 的数据加载器。只需几行代码即可训练模型——我们甚至帮你处理数据集打乱（shuffling）。 :)
</details>
<details>
  <summary><b>与强大工具的集成</b></summary>
Deep Lake 已与 <a href="https://github.com/hwchase17/langchain">Langchain</a> 和 <a href="https://github.com/jerryjliu/llama_index">LLamaIndex</a> 集成，作为 LLM 应用的向量存储；与 <a href="https://wandb.ai/">Weights & Biases</a> 集成以支持模型训练期间的数据血缘追踪；与 <a href="https://github.com/open-mmlab/mmdetection">MMDetection</a> 集成用于目标检测模型训练，以及 <a href="https://github.com/open-mmlab/mmsegmentation">MMSegmentation</a> 用于语义分割模型训练。
</details>
<details>
  <summary><b>数秒内即可获取 100+ 最受欢迎的图像、视频和音频数据集</b></summary>
Deep Lake 社区已上传 <a href="https://app.activeloop.ai/datasets/activeloop?utm_source=github&utm_medium=github&utm_campaign=github_readme&utm_id=readme">100+ 个图像、视频和音频数据集</a>，包括 <a href="https://app.activeloop.ai/activeloop/mnist-train?utm_source=github&utm_medium=github&utm_campaign=github_readme&utm_id=readme">MNIST</a>、<a href="https://app.activeloop.ai/activeloop/coco-train?utm_source=github&utm_medium=github&utm_campaign=github_readme&utm_id=readme">COCO</a>、  <a href="https://app.activeloop.ai/activeloop/imagenet-train?utm_source=github&utm_medium=github&utm_campaign=github_readme&utm_id=readme">ImageNet</a>、  <a href="https://app.activeloop.ai/activeloop/cifar100-test?utm_source=github&utm_medium=github&utm_campaign=github_readme&utm_id=readme">CIFAR</a>、  <a href="https://app.activeloop.ai/activeloop/gtzan-genre?utm_source=github&utm_medium=github&utm_campaign=github_readme&utm_id=readme">GTZAN</a> 等。
</details>
<details>
  <summary><b>在 <a href="https://app.activeloop.ai/?utm_source=github&utm_medium=github&utm_campaign=github_readme&utm_id=readme">Deep Lake App</a> 中即时可视化支持</b></summary>
Deep Lake 数据集可在 <a href="https://app.activeloop.ai/?utm_source=github&utm_medium=github&utm_campaign=github_readme&utm_id=readme">Deep Lake Visualizer</a>（见下图）中即时生成带边界框、掩码、标注等的可视化效果。
</details>

[![Visualizer](https://www.linkpicture.com/q/ReadMe.gif "Visualizer")](https://www.youtube.com/watch?v=SxsofpSIw3k)

## 🚀 如何安装 Deep Lake
可通过 pip 安装 Deep Lake：
```sh
pip install deeplake
```

### 如需使用 Deep Lake 的全部功能，请在 [Deep Lake App](https://app.activeloop.ai/register/) 注册。

## 🧠 按应用场景划分的 Deep Lake 代码示例

### 向量存储应用
将 Deep Lake 作为向量存储以构建 LLM 应用：
### - [向量存储快速入门](https://docs.deeplake.ai/latest/guides/rag/)
### - [向量存储教程](https://docs-v3.activeloop.ai/examples/rag/tutorials)
### - [LangChain 集成](https://docs-v3.activeloop.ai/examples/rag/langchain-integration)
### - [LlamaIndex 集成](https://docs-v3.activeloop.ai/examples/rag/llamaindex-integration)
### - [使用 Deep Lake 进行图像相似度搜索](https://docs.deeplake.ai/latest/guides/rag/#5-integrating-image-embeddings-for-multi-modal-search)


### 深度学习应用
将 Deep Lake 用于训练深度学习模型时的数据管理：
### - [深度学习快速入门](https://docs.deeplake.ai/latest/guides/deep-learning/deep-learning/)
### - [模型训练教程](https://docs-v3.activeloop.ai/examples/dl/tutorials/training-models)

## ⚙️ 集成

Deep Lake 提供与其他工具的集成，以简化你的深度学习工作流。当前集成包括：

* **大语言模型（LLM）应用**
  * 将 [Deep Lake 用作 LLM 应用的向量存储](https://www.activeloop.ai/resources/ultimate-guide-to-lang-chain-deep-lake-build-chat-gpt-to-answer-questions-on-your-financial-data/)。我们的集成将 [Langchain](https://github.com/hwchase17/langchain) 的 [VectorStores API](https://python.langchain.com/en/latest/reference/modules/vectorstore.html?highlight=pinecone#langchain.vectorstores.DeepLake) 与 Deep Lake 数据集（作为底层数据存储）相结合。该集成为无服务器向量存储，可部署在本地或你选择的云端。

## 📚 文档

入门指南、示例、教程、API 参考及其他有用信息可在我们的 [文档页面](http://docs.deeplake.ai/?utm_source=github&utm_medium=repo&utm_campaign=readme)找到。

## 🎓 面向学生与教育工作者
Deep Lake 用户可通过与 Deep Lake App 的免费集成，访问和可视化多种流行数据集。大学每月可免费获得 Tensor Database 1TB 数据存储和 10 万次查询额度。请在 [我们的网站](https://activeloop.ai)聊天以领取该权益！

## 👩‍💻 与常用工具的对比

<details>
  <summary><b>Deep Lake vs ChromaDB </b></summary>
  
两者均允许用户存储和搜索向量（嵌入），并提供与 LangChain 和 LlamaIndex 的集成。但在架构上存在显著差异：ChromaDB 是一款可部署在本地或服务器上的向量数据库（支持 Docker，即将推出托管方案）。Deep Lake 则是无服务器架构，部署于用户自有云端、本地或内存中。所有计算均在客户端运行，使用户能在数秒内支撑轻量级生产应用。与 ChromaDB 不同，Deep Lake 的数据格式除嵌入向量外，还能存储图像、视频和文本等原始数据。ChromaDB 仅限于在嵌入向量上附加轻量元数据且无可视化功能。Deep Lake 数据集支持可视化和版本控制。此外，Deep Lake 还提供高性能数据加载器，用于大语言模型的微调。

</details>

<details>
  <summary><b>Deep Lake vs Pinecone</b></summary>
  
两者均允许用户存储和搜索向量（嵌入），并提供与 LangChain 和 LlamaIndex 的集成。但在架构上存在显著差异：Pinecone 是一款全托管向量数据库，专为需要数十亿级向量搜索的高要求应用而优化。Deep Lake 采用无服务器架构。所有计算均在客户端运行，使用户能在数秒内快速上手。与 Pinecone 不同，Deep Lake 的数据格式除嵌入向量外，还能存储图像、视频和文本等原始数据。Deep Lake 数据集支持可视化和版本控制。Pinecone 仅限于在嵌入向量上附加轻量元数据且无可视化功能。此外，Deep Lake 还提供高性能数据加载器，用于大语言模型的微调。

</details>

<details>
  <summary><b>Deep Lake vs Weaviate</b></summary>
  
两者均允许用户存储和搜索向量（嵌入），并提供与 LangChain 和 LlamaIndex 的集成。但在架构上存在显著差异：Weaviate 是一款可部署为托管服务或通过 Kubernetes/Docker 由用户自行管理的向量数据库。Deep Lake 采用无服务器架构。所有计算均在客户端运行，使用户能在数秒内支撑轻量级生产应用。与 Weaviate 不同，Deep Lake 的数据格式除嵌入向量外，还能存储图像、视频和文本等原始数据。Deep Lake 数据集支持可视化和版本控制。Weaviate 仅限于在嵌入向量上附加轻量元数据且无可视化功能。此外，Deep Lake 还提供高性能数据加载器，用于大语言模型的微调。

</details>

<details>
  <summary><b>Deep Lake vs DVC</b></summary>
  
Deep Lake 和 DVC 均提供类似 Git 的数据集版本控制功能，但数据存储方式差异显著：Deep Lake 将数据转换并存储为分块压缩数组，可实现向机器学习（ML）模型的高速流式传输；而 DVC 则运行在效率较低的传统文件结构之上。当数据集由大量文件（如众多图像）组成时，相比 DVC 的传统文件结构，Deep Lake 格式使数据集版本控制变得显著更简单。另一区别在于，DVC 主要使用命令行界面，而 Deep Lake 是 Python 包。最后，Deep Lake 提供 API，可轻松将数据集连接至 ML 框架及其他常用 ML 工具，并通过 [Activeloop 的可视化工具](http://app.activeloop.ai/?utm_source=github&utm_medium=repo&utm_campaign=readme)实现数据集即时可视化。

</details>

<details>
  <summary><b>Deep Lake vs MosaicML MDS format </b></summary>
  
* **数据存储格式：** Deep Lake 采用列式存储格式，而 MDS 使用行式存储方法。这从根本上影响了两系统中数据的读取、写入和组织方式。
* **压缩机制：** Deep Lake 提供更灵活的压缩方案，允许对每列或张量分别控制块级和样本级压缩。该特性消除了对 zstd 等额外压缩算法的需求，从而避免在 jpeg 等格式之上解压时消耗更多 CPU 周期。
* **数据打乱：** MDS 目前提供更先进的打乱策略。
* **版本控制与可视化支持：** Deep Lake 的一大特色是原生支持版本控制和浏览器内数据可视化，MosaicML 数据格式暂无此功能。这在管理、理解和追踪不同版本的数据时能带来显著优势。

</details>

<details>
  <summary><b>Deep Lake vs TensorFlow Datasets (TFDS)</b></summary>
  
Deep Lake 和 TFDS 均可将流行数据集无缝对接至 ML 框架。Deep Lake 数据集兼容 PyTorch 和 TensorFlow，而 TFDS 仅兼容 TensorFlow。Deep Lake 与 TFDS 的关键区别在于：Deep Lake 数据集专为从云端流式读取设计，而 TFDS 必须预先下载到本地才能使用。因此，借助 Deep Lake，你可以直接从 TensorFlow Datasets 导入数据集，并将其流式传输至 PyTorch 或 TensorFlow。除提供公开流行数据集的访问权限外，Deep Lake 还提供强大的工具用于创建自定义数据集、将其存储于各类云服务商处，并通过简洁 API 与他人协作。TFDS 主要侧重于向公众便捷提供常用数据集，而非管理自定义数据集。完整对比文章请见 [此处](https://www.activeloop.ai/resources/tensor-flow-tf-data-activeloop-hub-how-to-implement-your-tensor-flow-data-pipelines-with-hub/)。

</details>

<details>
  <summary><b>Deep Lake vs HuggingFace</b></summary>
Deep Lake 和 HuggingFace 均提供流行数据集的访问权限，但 Deep Lake 主要聚焦于计算机视觉领域，而 HuggingFace 侧重于自然语言处理（NLP）。HuggingFace Transforms 及其他 NLP 计算工具的功能与 Deep Lake 提供的功能并不对等。

</details>

<details>
  <summary><b>Deep Lake vs WebDatasets</b></summary>
Deep Lake 和 WebDatasets 均提供跨网络的高速数据流式传输，两者流式速度几乎相同（底层网络请求和数据结构非常相似）。然而，Deep Lake 提供更优的随机访问和打乱功能；其 API 基于 Python 而非命令行；且 Deep Lake 允许在不重新创建数据集的情况下轻松索引和修改数据集。

</details>

<details>
  <summary><b>Deep Lake vs Zarr</b></summary>
Deep Lake 和 Zarr 均提供将数据作为分块数组的存储方案。但 Deep Lake 主要设计为通过简洁 API 返回数组格式的数据（尽管也支持直接存储原始数组）。Deep Lake 采用针对特定用例优化的格式存储数据，例如图像使用 jpeg/png，视频使用 mp4；用户可将数据视为数组操作，因为 Deep Lake 已处理中间的所有数据处理流程。此外，Deep Lake 在存储动态形状数组（ragged tensors）方面提供更强的灵活性，并提供了 Zarr 原生不具备的若干功能，如版本控制、数据流式传输以及与 ML 框架的连接。

</details>

## 社区

加入我们的 **[Slack 社区](https://slack.activeloop.ai)**，深入了解如何使用 Deep Lake 管理非结构化数据集，并获取 Activeloop 团队及其他用户的帮助。

欢迎通过填写我们 3 分钟的 **[调查表](https://forms.gle/rLi4w33dow6CSMcm9)** 提供反馈。

一如既往，感谢所有出色的贡献者！

<a href="https://github.com/activeloopai/deeplake/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=activeloopai/hub" />
</a>

由 [contributors-img](https://contrib.rocks) 生成。

请阅读 [CONTRIBUTING.md](CONTRIBUTING.md) 以开始为 Deep Lake 做出贡献。

## README 徽章

正在使用 Deep Lake？添加一个 README 徽章让所有人知道：

[![deeplake](https://img.shields.io/badge/powered%20by-Deep%20Lake%20-ff5a1f.svg)](https://github.com/activeloopai/deeplake)

```markdown
[![deeplake](https://img.shields.io/badge/powered%20by-Deep%20Lake%20-ff5a1f.svg)](https://github.com/activeloopai/deeplake)
```

## 免责声明

<details>
  <summary><b>数据集许可证</b></summary>
  
Deep Lake 用户可访问多种公开可用的数据集。我们不对这些数据集进行托管或分发，不为其质量或公平性背书，也不声称你拥有使用这些数据集的许可。你有责任自行确认是否在相关许可证下获得了使用权限。

如果你是数据集所有者且不希望你的数据集被收录于此库中，请通过 [GitHub Issue](https://github.com/activeloopai/deeplake/issues/new) 联系我们。感谢你对机器学习社区的贡献！

</details>

## 引用

如果你在研究中使用了 Deep Lake，请使用以下格式引用 Activeloop：

```markdown
@article{deeplake,
  title = {Deep Lake: a Lakehouse for Deep Learning},
  author = {Hambardzumyan, Sasun and Tuli, Abhinav and Ghukasyan, Levon and Rahman, Fariz and Topchyan, Hrant and Isayan, David and Harutyunyan, Mikayel and Hakobyan, Tatevik and Stranic, Ivo and Buniatyan, Davit},
  url = {https://www.cidrdb.org/cidr2023/papers/p69-buniatyan.pdf},
  booktitle={Proceedings of CIDR},
  year = {2023},
}
```


## 致谢

该技术灵感来源于我们在普林斯顿大学的研究工作。我们要感谢 William Silversmith (@SeungLab) 提供的出色 [cloud-volume](https://github.com/seung-lab/cloud-volume) 工具。
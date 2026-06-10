# Python 离群点检测库 (PyOD) 3

==================================

**PyOD 3：规模化智能体异常检测（Agentic Anomaly Detection At Scale）**

|badge_pypi| |badge_anaconda| |badge_docs| |badge_stars| |badge_forks| |badge_downloads| |badge_testing| |badge_coverage| |badge_maintainability| |badge_license| |badge_benchmark|

.. |badge_pypi| image:: https://img.shields.io/pypi/v/pyod.svg?color=brightgreen
   :target: https://pypi.org/project/pyod/
   :alt: PyPI version

.. |badge_anaconda| image:: https://anaconda.org/conda-forge/pyod/badges/version.svg
   :target: https://anaconda.org/conda-forge/pyod
   :alt: Anaconda version

.. |badge_docs| image:: https://readthedocs.org/projects/pyod/badge/?version=latest
   :target: https://pyod.readthedocs.io/en/latest/?badge=latest
   :alt: Documentation status

.. |badge_stars| image:: https://img.shields.io/github/stars/yzhao062/pyod.svg
   :target: https://github.com/yzhao062/pyod/stargazers
   :alt: GitHub stars

.. |badge_forks| image:: https://img.shields.io/github/forks/yzhao062/pyod.svg?color=blue
   :target: https://github.com/yzhao062/pyod/network
   :alt: GitHub forks

.. |badge_downloads| image:: https://pepy.tech/badge/pyod
   :target: https://pepy.tech/project/pyod
   :alt: Downloads

.. |badge_testing| image:: https://github.com/yzhao062/pyod/actions/workflows/testing.yml/badge.svg
   :target: https://github.com/yzhao062/pyod/actions/workflows/testing.yml
   :alt: Testing


.. |badge_coverage| image:: https://coveralls.io/repos/github/yzhao062/pyod/badge.svg
   :target: https://coveralls.io/github/yzhao062/pyod
   :alt: Coverage Status

.. |badge_maintainability| image:: https://api.codeclimate.com/v1/badges/bdc3d8d0454274c753c4/maintainability
   :target: https://codeclimate.com/github/yzhao062/Pyod/maintainability
   :alt: Maintainability

.. |badge_license| image:: https://img.shields.io/github/license/yzhao062/pyod.svg
   :target: https://github.com/yzhao062/pyod/blob/master/LICENSE
   :alt: License

.. |badge_benchmark| image:: https://img.shields.io/badge/ADBench-benchmark_results-pink
   :target: https://github.com/Minqi824/ADBench
   :alt: Benchmark


-----

    **PyOD 已全面支持 AI 智能体（Agent）。** Claude Code 和 Codex 可使用 `od-expert` 技能驱动 ADEngine 调查流程，而兼容 MCP 的智能体可查询 PyOD 的检测器知识与规划工具。经典的 ``fit``/``predict`` API 保持不变。

-----

PyOD 3 是目前最全面的 Python 异常检测库。四大核心支柱：

===========================  ========================================================================================
Pillar                       What it means
===========================  ========================================================================================
Multi-Modal                  多模态：覆盖**表格、时间序列、图、文本和图像**数据的 60+ 检测器，统一 API
Full Lifecycle               全生命周期：单次调用即可从原始数据生成可解释的异常结果及下一步指导
Agentic                      智能体驱动：`od-expert` 将自然语言请求转化为 ADEngine 工作流；MCP 为其他智能体提供结构化工具接口
Most Used                    使用最广：3800+ 万次下载；基于基准测试的自动路由（ADBench, TSB-AD, BOND, NLP-ADBench）
===========================  ========================================================================================

安装
^^^^^^^

核心库（所有激活路径均必需）：

.. code-block:: bash



    pip install pyod



然后选择匹配你智能体技术栈的激活路径：

.. code-block:: bash



    # 1. Claude Code / Claude Desktop / Codex — enables the od-expert skill
    pyod install skill              # Claude Code / Desktop: user-global (~/.claude/skills/)
    pyod install skill --project    # Codex: project-local (./skills/, Codex has no user-global dir)



    # 2. Any MCP-compatible LLM — requires the optional mcp extra
    pip install pyod[mcp]
    pyod mcp serve                 # alias for `python -m pyod.mcp_server`



    # 3. Pure Python — no extra step
    #    from pyod.utils.ad_engine import ADEngine



随时运行 ``pyod info`` 查看版本、检测器数量及各激活路径的安装状态。``pyod info`` 还会自动检测你已安装的技术栈（Claude Code 对应 `~/.claude/`，Codex 对应 `~/.codex/`）并推荐正确的安装命令。

如需了解 conda 安装、源码编译、依赖详情及故障排查，请参阅完整的 `安装指南 <https://pyod.readthedocs.io/en/latest/install.html>`__。v3.0.0 中的遗留命令 ``pyod-install-skill`` 仍可作为 ``pyod install skill`` 的别名使用。

**5 行代码完成离群点检测**（需先执行 `pip install pyod`）：

.. code-block:: python



    from pyod.models.iforest import IForest
    clf = IForest()
    clf.fit(X_train)
    y_train_scores = clf.decision_scores_          # training anomaly scores
    y_test_scores = clf.decision_function(X_test)   # test anomaly scores



**PyOD 的三种使用方式：**

=========  =====================  ======================================================================  =======================================
Layer      Name                   When to use                                                             Entry point
=========  =====================  ======================================================================  =======================================
1          Classic API            You know which detector you want                                        `Layer 1 examples <https://pyod.readthedocs.io/en/latest/examples/tabular.html>`__
2          ADEngine               You want PyOD to choose, compare, and assess automatically              `Layer 2 walkthrough <https://pyod.readthedocs.io/en/latest/examples/adengine.html>`__
3          Agentic Investigation  You want an AI agent to drive OD through natural conversation           `Layer 3 walkthrough <https://pyod.readthedocs.io/en/latest/examples/agentic.html>`__
=========  =====================  ======================================================================  =======================================

第 2 和第 3 层由 ``ADEngine``（PyOD 的智能编排核心）驱动。完整的 Layer 3 多轮调查流程可通过 Claude Code 和 Codex 的 `od-expert` 技能调用。MCP 服务器（`python -m pyod.mcp_server`）为兼容 MCP 的大语言模型提供 10 个无状态工具，涵盖知识查询（``list_detectors``, ``explain_detector``, ``compare_detectors``, ``get_benchmarks``）、规划（``profile_data``, ``plan_detection``, ``build_detector``）和检测（``run_detection``, ``analyze_results``, ``explain_findings``）；有状态的 `investigate` / `iterate` MCP 工具将在后续版本中推出。

.. image:: https://raw.githubusercontent.com/yzhao062/pyod/development/docs/figs/agentic-demo.png
   :alt: PyOD 3 agentic investigation demo on cardiotocography dataset
   :align: center
   :width: 720

上图展示了在 UCI Cardiotocography 数据集上进行的真实 5 轮智能体对话。请参阅 `完整教程 <https://pyod.readthedocs.io/en/latest/examples/agentic.html>`__、可运行的 `智能体示例 <https://github.com/yzhao062/pyod/blob/development/examples/agentic_example.py>`__，或交互式 `HTML 演示 <https://htmlpreview.github.io/?https://github.com/yzhao062/pyod/blob/development/examples/agentic_demo.html>`__。

**PyOD 生态系统与资源**：
`NLP-ADBench <https://github.com/USC-FORTIS/NLP-ADBench>`__ (NLP 异常检测) | `TODS <https://github.com/datamllab/tods>`__ (时间序列) | `PyGOD <https://pygod.org/>`__ (图) | `ADBench <https://github.com/Minqi824/ADBench>`__ (基准测试) | `AD-LLM <https://arxiv.org/abs/2412.11142>`__ (基于 LLM 的异常检测) [#Yang2024ad]_ | `Resources <https://github.com/yzhao062/anomaly-detection-resources>`__

----


关于 PyOD
^^^^^^^^^^

PyOD 成立于 2017 年，是运行时间最长、使用最广泛的 Python 异常检测库。凭借 `3800+ 万次下载 <https://pepy.tech/project/pyod>`__，它同时服务于学术研究（被 `Analytics Vidhya <https://www.analyticsvidhya.com/blog/2019/02/outlier-detection-python-pyod/>`__、`KDnuggets <https://www.kdnuggets.com/2019/02/outlier-detection-methods-cheat-sheet.html>`__ 和 `Towards Data Science <https://towardsdatascience.com/anomaly-detection-for-dummies-15f148e559c1>`__ 等媒体专题报道）和商业产品。

V3 版本引入了 ``ADEngine``（智能编排）和 `od-expert` 技能（智能体工作流），同时完全向后兼容经典的 ``fit``/``predict`` API。V3 底层基于 SUOD [#Zhao2021SUOD]_ 实现快速并行训练，并使用 numba JIT 进行单模型加速。

**影响力与认可：**

===================================  ===========================================================================
Area                                 Examples
===================================  ===========================================================================
Space & science                      欧洲航天局 `OPS-SAT 航天器遥测基准 <https://www.nature.com/articles/s41597-025-05035-3>`__ (*Nature Scientific Data*, 2025) 使用 PyOD 实现了全部 30 种算法。
Enterprise deployment                Walmart（每日超百万次价格更新，KDD 2019）、Databricks（Kakapo 框架集成 PyOD 与 MLflow/Hyperopt；内部威胁检测方案）、IQVIA（超 12.3 万条处方索赔数据）、Altair AI Studio、Ericsson（专利 `WO2023166515A1 <https://patents.google.com/patent/WO2023166515A1>`__）。
Books                                《Python 离群点检测》（Brett Kennedy, Manning）；《Python 异常检测手册》（Chris Kuo, Columbia）；《在数据中发现幽灵》（Kevin Feasel, Apress）。
Courses                              DataCamp `Python 中的异常检测 <https://www.datacamp.com/courses/anomaly-detection-in-python>`__（平台学习者超 1900 万）、Manning `liveProject <https://www.manning.com/liveproject/using-pyod-and-ensembles-methods>`__、O'Reilly 视频版及多门 Udemy 课程。
Podcasts                             `Talk Python To Me #497 <https://talkpython.fm/episodes/show/497/outlier-detection-with-python>`__、`Real Python Podcast #208 <https://realpython.com/podcasts/rpp/208/>`__。
International                        5 种非英语语言教程：中文（CSDN, 知乎, 搜狐, 机器之心, `aidoczh.com <https://www.aidoczh.com>`__ 完整文档翻译）、日语、韩语、德语、西班牙语。
===================================  ===========================================================================

请参阅 Read the Docs 上的 `完整影响力页面 <https://pyod.readthedocs.io/en/latest/impact.html>`__，获取完整的引用列表、企业部署案例、专利及媒体报道。

**引用 PyOD：**

如果你在学术出版物中使用 PyOD，我们将感谢你对以下论文的引用：

`PyOD 2: A Python Library for Outlier Detection with LLM-powered Model Selection <https://arxiv.org/abs/2412.12154>`__ 已作为预印本发布。如果你在学术论文中使用 PyOD，请引用以下论文：::



    @inproceedings{chen2025pyod,
      title={Pyod 2: A python library for outlier detection with llm-powered model selection},
      author={Chen, Sihan and Qian, Zhuangzhuang and Siu, Wingchun and Hu, Xingcan and Li, Jiaqi and Li, Shawn and Qin, Yuehan and Yang, Tiankai and Xiao, Zhuo and Ye, Wanghao and others},
      booktitle={Companion Proceedings of the ACM on Web Conference 2025},
      pages={2807--2810},
      year={2025}
    }





`PyOD paper <http://www.jmlr.org/papers/volume20/19-011/19-011.pdf>`__ 已发表于 `《机器学习研究杂志》（JMLR） <http://www.jmlr.org/>`__ (MLOSS track)。::



    @article{zhao2019pyod,
        author  = {Zhao, Yue and Nasrullah, Zain and Li, Zheng},
        title   = {PyOD: A Python Toolbox for Scalable Outlier Detection},
        journal = {Journal of Machine Learning Research},
        year    = {2019},
        volume  = {20},
        number  = {96},
        pages   = {1-7},
        url     = {http://jmlr.org/papers/v20/19-011.html}
    }



或::



    Zhao, Y., Nasrullah, Z. and Li, Z., 2019. PyOD: A Python Toolbox for Scalable Outlier Detection. Journal of machine learning research (JMLR), 20(96), pp.1-7.





如需更广泛地了解异常检测领域，请参阅我们在 NeurIPS 上发表的关于 `ADBench <https://arxiv.org/abs/2206.09426>`__ [#Han2022ADBench]_ 和 `ADGym <https://arxiv.org/abs/2309.15376>`__ 的论文。



**目录：**

* `API 速查表与参考文档 <#api-cheatsheet--reference>`__
* `基准测试 <#benchmarks>`__
* `已实现的算法 <#implemented-algorithms>`__（表格、时间序列、图、嵌入）
* `其他主题 <#additional-topics>`__（模型保存/加载、SUOD、阈值设定）
* `离群点检测快速入门 <#quick-start-for-outlier-detection>`__
* `如何贡献代码 <#how-to-contribute>`__
* `收录标准 <#inclusion-criteria>`__

----


API 速查表与参考文档
^^^^^^^^^^^^^^^^^^^^^^^^^^

完整的 API 参考文档按模态分类，详见 `PyOD 官方文档 <https://pyod.readthedocs.io/en/latest/>`__：`表格数据 <https://pyod.readthedocs.io/en/latest/pyod.models.tabular.html>`__、`时间序列 <https://pyod.readthedocs.io/en/latest/pyod.models.timeseries.html>`__、`图结构 <https://pyod.readthedocs.io/en/latest/pyod.models.graph.html>`__、`嵌入表示 <https://pyod.readthedocs.io/en/latest/pyod.models.embedding.html>`__、`ADEngine <https://pyod.readthedocs.io/en/latest/pyod.ad_engine.html>`__、`工具函数 <https://pyod.readthedocs.io/en/latest/pyod.utils.html>`__。以下是所有检测器的快速速查表：

* **fit(X)**: 训练检测器。在无监督方法中，参数 y 会被忽略。
* **decision_function(X)**: 使用已训练的检测器预测 X 的原始异常分数（anomaly scores）。
* **predict(X)**: 使用已训练的检测器将样本判定为正常或离群点，返回二分类标签。
* **predict_proba(X)**: 使用已训练的检测器估计样本属于离群点的概率。
* **predict_confidence(X)**: 评估模型对每个样本的预测置信度（适用于 predict 和 predict_proba） [#Perini2020Quantifying]_。
* **predict_with_rejection(X)**\ : 允许检测器拒绝（即 abstain from making）高度不确定的预测（输出 = -2） [#Perini2023Rejection]_。

**已训练模型的关键属性：**

* **decision_scores_**: 训练数据的离群分数。通常分数越高表示异常程度越大，离群点往往具有更高的分数。
* **labels_**: 训练数据的二分类标签，其中 0 表示正常样本（inliers），1 表示离群点/异常值（outliers/anomalies）。



----


基准测试
^^^^^^^^^^

* `ADBench <https://github.com/Minqi824/ADBench>`__ [#Han2022ADBench]_: 57 个表格数据集上的 30 种算法。详见 `对比代码 <https://github.com/yzhao062/pyod/blob/master/examples/compare_all_models.py>`__。
* `NLP-ADBench <https://github.com/USC-FORTIS/NLP-ADBench>`__: 8 个文本数据集上的 19 种方法。两阶段（嵌入 + 检测器）优于端到端模型。
* `TSB-AD <https://github.com/TheDatumOrg/TSB-AD>`__ [#Liu2024TSB]_: 1070 个时间序列数据集上的 40 种算法（NeurIPS 2024）。
* `BOND <https://arxiv.org/abs/2206.10071>`__ [#Liu2022BOND]_: 14 个图异常检测数据集上的 14 种算法（NeurIPS 2022）。



----


其他主题
^^^^^^^^^^^^^^^^^

* `模型保存与加载 <https://pyod.readthedocs.io/en/latest/model_persistence.html>`__: 使用 joblib 或 pickle 保存和加载 PyOD 模型。详见 `示例 <https://github.com/yzhao062/pyod/blob/master/examples/save_load_model_example.py>`__。
* `通过 SUOD 快速训练 <https://pyod.readthedocs.io/en/latest/fast_train.html>`__: 利用 SUOD 框架加速训练与预测过程 [#Zhao2021SUOD]_。详见 `示例 <https://github.com/yzhao062/pyod/blob/master/examples/suod_example.py>`__。
* `离群点分数阈值设定 <https://pyod.readthedocs.io/en/latest/thresholding.html>`__: 通过 `PyThresh <https://github.com/KulikDM/pythresh>`__ 实现数据驱动的污染率（contamination）设定方法。



----


已实现的算法
^^^^^^^^^^^^^^^^^^^^^^

PyOD 分为两大功能组：**(i) 检测算法**，包含表格、时间序列和图数据的专用子节（表格表中的 EmbeddingOD 通过基础模型编码器增加了文本和图像的多模态支持）；以及 **(ii) 工具函数**，用于数据生成、评估和智能编排。

**(i-a) 表格与多模态检测算法** :

.. list-table::
   :widths: 15 14 58 5 8
   :header-rows: 1

   * - Type
     - Abbr
     - Algorithm
     - Year
     - Ref
   * - Probabilistic
     - ECOD
     - Unsupervised Outlier Detection Using Empirical Cumulative Distribution Functions (`example <https://github.com/yzhao062/pyod/blob/development/examples/ecod_example.py>`__)
     - 2022
     - [#Li2021ECOD]_
   * - Probabilistic
     - ABOD
     - Angle-Based Outlier Detection (`example <https://github.com/yzhao062/pyod/blob/development/examples/abod_example.py>`__)
     - 2008
     - [#Kriegel2008Angle]_
   * - Probabilistic
     - FastABOD
     - Fast Angle-Based Outlier Detection using approximation (`example <https://github.com/yzhao062/pyod/blob/development/examples/abod_example.py>`__)
     - 2008
     - [#Kriegel2008Angle]_
   * - Probabilistic
     - COPOD
     - COPOD: Copula-Based Outlier Detection (`example <https://github.com/yzhao062/pyod/blob/development/examples/copod_example.py>`__)
     - 2020
     - [#Li2020COPOD]_
   * - Probabilistic
     - MAD
     - Median Absolute Deviation (MAD) (`example <https://github.com/yzhao062/pyod/blob/development/examples/mad_example.py>`__)
     - 1993
     - [#Iglewicz1993How]_
   * - Probabilistic
     - SOS
     - Stochastic Outlier Selection (`example <https://github.com/yzhao062/pyod/blob/development/examples/sos_example.py>`__)
     - 2012
     - [#Janssens2012Stochastic]_
   * - Probabilistic
     - QMCD
     - Quasi-Monte Carlo Discrepancy outlier detection (`example <https://github.com/yzhao062/pyod/blob/development/examples/qmcd_example.py>`__)
     - 2001
     - [#Fang2001Wrap]_
   * - Probabilistic
     - KDE
     - Outlier Detection with Kernel Density Functions (`example <https://github.com/yzhao062/pyod/blob/development/examples/kde_example.py>`__)
     - 2007
     - [#Latecki2007Outlier]_
   * - Probabilistic
     - Sampling
     - Rapid distance-based outlier detection via sampling (`example <https://github.com/yzhao062/pyod/blob/development/examples/sampling_example.py>`__)
     - 2013
     - [#Sugiyama2013Rapid]_
   * - Probabilistic
     - GMM
     - Probabilistic Mixture Modeling for Outlier Analysis (`example <https://github.com/yzhao062/pyod/blob/development/examples/gmm_example.py>`__)
     - 
     - [#Aggarwal2015Outlier]_ [Ch.2]
   * - Linear Model
     - PCA
     - Principal Component Analysis (sum of weighted projected distances to eigenvector hyperplanes) (`example <https://github.com/yzhao062/pyod/blob/development/examples/pca_example.py>`__)
     - 2003
     - [#Shyu2003A]_
   * - Linear Model
     - KPCA
     - Kernel Principal Component Analysis (`example <https://github.com/yzhao062/pyod/blob/development/examples/kpca_example.py>`__)
     - 2007
     - [#Hoffmann2007Kernel]_
   * - Linear Model
     - MCD
     - Minimum Covariance Determinant (Mahalanobis distances as outlier scores) (`example <https://github.com/yzhao062/pyod/blob/development/examples/mcd_example.py>`__)
     - 1999
     - [#Hardin2004Outlier]_ [#Rousseeuw1999A]_
   * - Linear Model
     - CD
     - Cook's distance for outlier detection (`example <https://github.com/yzhao062/pyod/blob/development/examples/cd_example.py>`__)
     - 1977
     - [#Cook1977Detection]_
   * - Linear Model
     - OCSVM
     - One-Class Support Vector Machines (`example <https://github.com/yzhao062/pyod/blob/development/examples/ocsvm_example.py>`__)
     - 2001
     - [#Scholkopf2001Estimating]_
   * - Linear Model
     - LMDD
     - Deviation-based Outlier Detection (LMDD) (`example <https://github.com/yzhao062/pyod/blob/development/examples/lmdd_example.py>`__)
     - 1996
     - [#Arning1996A]_
   * - Proximity-Based
     - LOF
     - Local Outlier Factor (`example <https://github.com/yzhao062/pyod/blob/development/examples/lof_example.py>`__)
     - 2000
     - [#Breunig2000LOF]_
   * - Proximity-Based
     - COF
     - Connectivity-Based Outlier Factor (`example <https://github.com/yzhao062/pyod/blob/development/examples/cof_example.py>`__)
     - 2002
     - [#Tang2002Enhancing]_
   * - Proximity-Based
     - (Incr.) COF
     - Memory Efficient Connectivity-Based Outlier Factor (slower, reduced storage) (`example <https://github.com/yzhao062/pyod/blob/development/examples/cof_example.py>`__)
     - 2002
     - [#Tang2002Enhancing]_
   * - Proximity-Based
     - CBLOF
     - Clustering-Based Local Outlier Factor (`example <https://github.com/yzhao062/pyod/blob/development/examples/cblof_example.py>`__)
     - 2003
     - [#He2003Discovering]_
   * - Proximity-Based
     - LOCI
     - LOCI: Fast outlier detection via local correlation integral (`example <https://github.com/yzhao062/pyod/blob/development/examples/loci_example.py>`__)
     - 2003
     - [#Papadimitriou2003LOCI]_
   * - Proximity-Based
     - HBOS
     - Histogram-based Outlier Score (`example <https://github.com/yzhao062/pyod/blob/development/examples/hbos_example.py>`__)
     - 2012
     - [#Goldstein2012Histogram]_
   * - Proximity-Based
     - HDBSCAN
     - Density-based clustering via hierarchical density estimates (`example <https://github.com/yzhao062/pyod/blob/development/examples/hdbscan_example.py>`__)
     - 2013
     - [#Campello2013Density]_
   * - Proximity-Based
     - kNN
     - k Nearest Neighbors (distance to k-th neighbor as outlier score) (`example <https://github.com/yzhao062/pyod/blob/development/examples/knn_example.py>`__)
     - 2000
     - [#Ramaswamy2000Efficient]_
   * - Proximity-Based
     - AvgKNN
     - Average kNN (average distance to k neighbors as outlier score) (`example <https://github.com/yzhao062/pyod/blob/development/examples/knn_example.py>`__)
     - 2002
     - [#Angiulli2002Fast]_
   * - Proximity-Based
     - MedKNN
     - Median kNN (median distance to k neighbors as outlier score) (`example <https://github.com/yzhao062/pyod/blob/development/examples/knn_example.py>`__)
     - 2002
     - [#Angiulli2002Fast]_
   * - Proximity-Based
     - SOD
     - Subspace Outlier Detection (`example <https://github.com/yzhao062/pyod/blob/development/examples/sod_example.py>`__)
     - 2009
     - [#Kriegel2009Outlier]_
   * - Proximity-Based
     - ROD
     - Rotation-based Outlier Detection (`example <https://github.com/yzhao062/pyod/blob/development/examples/rod_example.py>`__)
     - 2020
     - [#Almardeny2020A]_
   * - Outlier Ensembles
     - IForest
     - Isolation Forest (`example <https://github.com/yzhao062/pyod/blob/development/examples/iforest_example.py>`__)
     - 2008
     - [#Liu2008Isolation]_
   * - Outlier Ensembles
     - INNE
     - Isolation-based Anomaly Detection via Nearest-Neighbor Ensembles (`example <https://github.com/yzhao062/pyod/blob/development/examples/inne_example.py>`__)
     - 2018
     - [#Bandaragoda2018Isolation]_
   * - Outlier Ensembles
     - DIF
     - Deep Isolation Forest for Anomaly Detection (`example <https://github.com/yzhao062/pyod/blob/development/examples/dif_example.py>`__)
     - 2023
     - [#Xu2023Deep]_
   * - Outlier Ensembles
     - FB
     - Feature Bagging (`example <https://github.com/yzhao062/pyod/blob/development/examples/feature_bagging_example.py>`__)
     - 2005
     - [#Lazarevic2005Feature]_
   * - Outlier Ensembles
     - LSCP
     - LSCP: Locally Selective Combination of Parallel Outlier Ensembles (`example <https://github.com/yzhao062/pyod/blob/development/examples/lscp_example.py>`__)
     - 2019
     - [#Zhao2019LSCP]_
   * - Outlier Ensembles
     - XGBOD
     - Extreme Boosting Based Outlier Detection **(Supervised)** (`example <https://github.com/yzhao062/pyod/blob/development/examples/xgbod_example.py>`__)
     - 2018
     - [#Zhao2018XGBOD]_
   * - Outlier Ensembles
     - LODA
     - Lightweight On-line Detector of Anomalies (`example <https://github.com/yzhao062/pyod/blob/development/examples/loda_example.py>`__)
     - 2016
     - [#Pevny2016Loda]_
   * - Outlier Ensembles
     - SUOD
     - SUOD: Accelerating Large-scale Unsupervised Heterogeneous OD **(Acceleration)** (`example <https://github.com/yzhao062/pyod/blob/development/examples/suod_example.py>`__)
     - 2021
     - [#Zhao2021SUOD]_
   * - Neural Networks
     - AutoEncoder
     - Fully connected AutoEncoder (reconstruction error as outlier score) (`example <https://github.com/yzhao062/pyod/blob/development/examples/auto_encoder_example.py>`__)
     - 
     - [#Aggarwal2015Outlier]_ [Ch.3]
   * - Neural Networks
     - VAE
     - Variational AutoEncoder (reconstruction error as outlier score) (`example <https://github.com/yzhao062/pyod/blob/development/examples/vae_example.py>`__)
     - 2013
     - [#Kingma2013Auto]_
   * - Neural Networks
     - Beta-VAE
     - Variational AutoEncoder with customized loss (gamma and capacity) (`example <https://github.com/yzhao062/pyod/blob/development/examples/vae_example.py>`__)
     - 2018
     - [#Burgess2018Understanding]_
   * - Neural Networks
     - SO_GAAL
     - Single-Objective Generative Adversarial Active Learning (`example <https://github.com/yzhao062/pyod/blob/development/examples/so_gaal_example.py>`__)
     - 2019
     - [#Liu2019Generative]_
   * - Neural Networks
     - MO_GAAL
     - Multiple-Objective Generative Adversarial Active Learning (`example <https://github.com/yzhao062/pyod/blob/development/examples/mo_gaal_example.py>`__)
     - 2019
     - [#Liu2019Generative]_
   * - Neural Networks
     - DeepSVDD
     - Deep One-Class Classification (`example <https://github.com/yzhao062/pyod/blob/development/examples/deepsvdd_example.py>`__)
     - 2018
     - [#Ruff2018Deep]_
   * - Neural Networks
     - AnoGAN
     - Anomaly Detection with Generative Adversarial Networks
     - 2017
     - [#Schlegl2017Unsupervised]_
   * - Neural Networks
     - ALAD
     - Adversarially learned anomaly detection (`example <https://github.com/yzhao062/pyod/blob/development/examples/alad_example.py>`__)
     - 2018
     - [#Zenati2018Adversarially]_
   * - Neural Networks
     - AE1SVM
     - Autoencoder-based One-class Support Vector Machine (`example <https://github.com/yzhao062/pyod/blob/development/examples/ae1svm_example.py>`__)
     - 2019
     - [#Nguyen2019scalable]_
   * - Neural Networks
     - DevNet
     - Deep Anomaly Detection with Deviation Networks (`example <https://github.com/yzhao062/pyod/blob/development/examples/devnet_example.py>`__)
     - 2019
     - [#Pang2019Deep]_
   * - Graph-based
     - R-Graph
     - Outlier detection by R-graph (`example <https://github.com/yzhao062/pyod/blob/development/examples/rgraph_example.py>`__)
     - 2017
     - [#You2017Provable]_
   * - Graph-based
     - LUNAR
     - LUNAR: Unifying Local OD Methods via Graph Neural Networks (`example <https://github.com/yzhao062/pyod/blob/development/examples/lunar_example.py>`__)
     - 2022
     - [#Goodge2022Lunar]_
   * - Embedding-based
     - EmbeddingOD
     - Multi-modal anomaly detection via foundation model embeddings, text and image (`example <https://github.com/yzhao062/pyod/blob/development/examples/embedding_od_example.py>`__)
     - 2025
     - [#Li2024NLPADBench]_



集成方法（IForest, INNE, DIF, FB, LSCP, LODA, SUOD, XGBOD）已包含在上述表格中。分数组合函数（average, maximization, AOM, MOA, median, majority vote）位于 `pyod.models.combination` 模块中。详见 `API 文档 <https://pyod.readthedocs.io/en/latest/pyod.models.tabular.html>`__。



**(i-b) 时间序列异常检测** :

所有时间序列检测器均使用与表格检测器相同的 ``fit``/``predict``/``decision_function`` API，唯一例外是：`MatrixProfile` 为直推式（仅训练集；在 `fit()` 后使用 `decision_scores_` 和 `labels_`，不支持样本外预测）。

**输入格式**：一维数据形状为 `(n_timestamps,)`，多维数据形状为 `(n_timestamps, n_channels)`。每行代表一个时间步，列代表通道/特征。Pandas DataFrames 和列表会自动转换。**输出**：形状为 `(n_timestamps,)` 的 `decision_scores_`，每个时间步对应一个异常分数。

**3 行代码完成时间序列检测：**

.. code-block:: python



    from pyod.models.ts_kshape import KShape      # or any TS detector
    clf = KShape(window_size=20)
    clf.fit(X_train)                               # shape (n_timestamps,) or (n_timestamps, n_channels)
    scores = clf.decision_scores_                  # per-timestamp anomaly scores



基于 `TSB-AD 基准测试 <https://github.com/TheDatumOrg/TSB-AD>`__ [#Liu2024TSB]_（NeurIPS 2024，1070 个数据集）的算法排名：

.. list-table::
   :widths: 15 18 50 5 12
   :header-rows: 1

   * - Type
     - Abbr
     - Algorithm
     - Year
     - Ref
   * - Windowed Bridge
     - TimeSeriesOD
     - Any PyOD detector on sliding windows (`example <https://github.com/yzhao062/pyod/blob/development/examples/ts_od_example.py>`__)
     - 2026
     - 
   * - Subsequence
     - MatrixProfile
     - Matrix Profile via STOMP, transductive (`example <https://github.com/yzhao062/pyod/blob/development/examples/ts_matrix_profile_example.py>`__)
     - 2016
     - [#Yeh2016Matrix]_
   * - Frequency
     - SpectralResidual
     - Spectral Residual: FFT-based saliency (`example <https://github.com/yzhao062/pyod/blob/development/examples/ts_spectral_residual_example.py>`__)
     - 2019
     - [#Ren2019Time]_
   * - Clustering
     - KShape
     - k-Shape clustering (#2 in TSB-AD) (`example <https://github.com/yzhao062/pyod/blob/development/examples/ts_kshape_example.py>`__)
     - 2015
     - [#Paparrizos2015KShape]_
   * - Streaming
     - SAND
     - Streaming with drift adaptation, experimental (`example <https://github.com/yzhao062/pyod/blob/development/examples/ts_sand_example.py>`__)
     - 2021
     - [#Boniol2021SAND]_
   * - Deep Learning
     - LSTMAD
     - LSTM prediction error + Mahalanobis scoring
     - 2015
     - [#Malhotra2015Long]_
   * - Deep Learning
     - AnomalyTransformer
     - Transformer with association discrepancy (experimental)
     - 2022
     - [#Xu2022Anomaly]_





**(i-c) 图异常检测**（需执行 `pip install pyod[graph]`）：

v1 中所有图检测器均为 **直推式（transductive）**：在 `fit()` 后使用 `decision_scores_` 和 `labels_`。不支持样本外预测。输入格式为 PyG `Data` 对象，包含 `x`（节点特征）和 `edge_index`（COO 边）。SCAN 无需特征即可运行。

**3 行代码完成图检测**（需执行 `pip install pyod[graph]`）：

.. code-block:: python



    from pyod.models.pyg_dominant import DOMINANT
    clf = DOMINANT(hidden_dim=64, epochs=100)
    clf.fit(data)                                  # PyG Data object
    scores = clf.decision_scores_                  # per-node anomaly scores



基于 `BOND 基准测试 <https://arxiv.org/abs/2206.10071>`__ [#Liu2022BOND]_（NeurIPS 2022，14 个数据集）的算法排名：

.. list-table::
   :widths: 18 18 45 5 14
   :header-rows: 1

   * - Type
     - Abbr
     - Algorithm
     - Year
     - Ref
   * - GCN Autoencoder
     - DOMINANT
     - GCN AE, structure + attribute reconstruction (#1 BOND deep) (`dominant example <https://github.com/yzhao062/pyod/blob/development/examples/pyg_dominant_example.py>`__)
     - 2019
     - [#Ding2019DOMINANT]_
   * - Contrastive
     - CoLA
     - Contrastive self-supervised, local neighbor context (#2 BOND deep) (`cola example <https://github.com/yzhao062/pyod/blob/development/examples/pyg_cola_example.py>`__)
     - 2022
     - [#Liu2022CoLA]_
   * - Contrastive+AE
     - CONAD
     - Contrastive with anomalous-view injection + dual reconstruction (`conad example <https://github.com/yzhao062/pyod/blob/development/examples/pyg_conad_example.py>`__)
     - 2022
     - [#Xu2022CONAD]_
   * - Attention AE
     - AnomalyDAE
     - GAT structure encoder + MLP attribute encoder (`anomalydae example <https://github.com/yzhao062/pyod/blob/development/examples/pyg_anomalydae_example.py>`__)
     - 2020
     - [#Fan2020AnomalyDAE]_
   * - Motif AE
     - GUIDE
     - Dual GCN AE on original + triangle-motif adjacency (`guide example <https://github.com/yzhao062/pyod/blob/development/examples/pyg_guide_example.py>`__)
     - 2021
     - [#Yuan2021GUIDE]_
   * - Matrix Factor.
     - Radar
     - Residual analysis via matrix factorization (`radar example <https://github.com/yzhao062/pyod/blob/development/examples/pyg_radar_example.py>`__)
     - 2017
     - [#Li2017Radar]_
   * - Matrix Factor.
     - ANOMALOUS
     - Joint MF with Laplacian regularization (`anomalous example <https://github.com/yzhao062/pyod/blob/development/examples/pyg_anomalous_example.py>`__)
     - 2018
     - [#Peng2018ANOMALOUS]_
   * - Structural
     - SCAN
     - Structural clustering, no features needed (`scan example <https://github.com/yzhao062/pyod/blob/development/examples/pyg_scan_example.py>`__)
     - 2007
     - [#Xu2007SCAN]_





**(ii) 工具函数：**

===================  ============================  =====================================================================================================================================================
Type                 Name                          Function
===================  ============================  =====================================================================================================================================================
Data                 generate_data                 Synthesized data generation; normal data from multivariate Gaussian, outliers from uniform distribution
Data                 generate_data_clusters        Synthesized data generation in clusters for more complex patterns
Evaluation           evaluate_print                Print ROC-AUC and Precision @ Rank n for a detector
Evaluation           precision_n_scores            Calculate Precision @ Rank n
Utility              get_label_n                   Turn raw outlier scores into binary labels by assigning 1 to the top n scores
Stat                 wpearsonr                     Calculate the weighted Pearson correlation of two samples
Encoding             resolve_encoder               Resolve an encoder from a string name, BaseEncoder instance, or callable
Encoding             SentenceTransformerEncoder     Encode text via sentence-transformers models (e.g., MiniLM, mpnet)
Encoding             OpenAIEncoder                 Encode text via OpenAI Embeddings API (text-embedding-3-small/large)
Encoding             HuggingFaceEncoder            Encode text or images via HuggingFace transformers (BERT, DINOv2, CLIP)
===================  ============================  =====================================================================================================================================================



----


离群点检测快速入门
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

PyOD 在机器学习社区获得了广泛认可，多篇专题文章和教程对其进行了介绍。

**Analytics Vidhya**: `使用 PyOD 库学习 Python 离群点检测的绝佳教程 <https://www.analyticsvidhya.com/blog/2019/02/outlier-detection-python-pyod/>`__



**KDnuggets**: `直观可视化异常检测方法 <https://www.kdnuggets.com/2019/02/outlier-detection-methods-cheat-sheet.html>`__、《PyOD 离群点检测方法概述》<https://www.kdnuggets.com/2019/06/overview-outlier-detection-methods-pyod.html>`__



**Towards Data Science**: `面向新手的异常检测指南 <https://towardsdatascience.com/anomaly-detection-for-dummies-15f148e559c1>`__



《`examples/knn_example.py" <https://github.com/yzhao062/pyod/blob/master/examples/knn_example.py>`__》
演示了使用 kNN 检测器的基础 API。**请注意，所有其他算法的 API 均保持一致或高度相似**。

运行示例的详细说明可在 `examples 目录 <https://github.com/yzhao062/pyod/blob/master/examples>`__ 中找到。



#. 初始化 kNN 检测器，训练模型并做出预测。



   .. code-block:: python





       from pyod.models.knn import KNN   # kNN detector



       # train kNN detector
       clf_name = 'KNN'
       clf = KNN()
       clf.fit(X_train)



       # get the prediction label and outlier scores of the training data
       y_train_pred = clf.labels_  # binary labels (0: inliers, 1: outliers)
       y_train_scores = clf.decision_scores_  # raw outlier scores



       # get the prediction on the test data
       y_test_pred = clf.predict(X_test)  # outlier labels (0 or 1)
       y_test_scores = clf.decision_function(X_test)  # outlier scores



       # it is possible to get the prediction confidence as well
       y_test_pred, y_test_pred_confidence = clf.predict(X_test, return_confidence=True)  # outlier labels (0 or 1) and confidence in the range of [0,1]



#. 通过 ROC 和 Precision @ Rank n (p@n) 评估预测结果。



   .. code-block:: python



       from pyod.utils.data import evaluate_print
       

       # evaluate and print the results
       print("\nOn Training Data:")
       evaluate_print(clf_name, y_train, y_train_scores)
       print("\nOn Test Data:")
       evaluate_print(clf_name, y_test, y_test_scores)





#. 查看示例输出与可视化结果。





   .. code-block:: python





       On Training Data:
       KNN ROC:1.0, precision @ rank n:1.0



       On Test Data:
       KNN ROC:0.9989, precision @ rank n:0.9



   .. code-block:: python





       visualize(clf_name, X_train, y_train, X_test, y_test, y_train_pred,
           y_test_pred, show_figure=True, save_figure=False)



----


致谢
^^^^^^^^^^^^^^^

本工作基于美国国家科学基金会（NSF）资助项目 `2346158 <https://www.nsf.gov/awardsearch/showAward?AWD_ID=2346158>`_ “NSF POSE: Phase II: OpenAD: An Integrated Open-Source Ecosystem for Anomaly Detection.” 的支持。该项目的牵头单位为伊利诺伊大学芝加哥分校，子资助单位包括伊利诺伊理工学院、利哈伊大学和南加州大学。

本材料中表达的观点、发现、结论或建议仅代表作者本人，不一定反映美国国家科学基金会的观点。

----


参考文献
^^^^^^^^^





.. [#Aggarwal2015Outlier] Aggarwal, C.C., 2015. Outlier analysis. In Data mining (pp. 237-263). Springer, Cham.



.. [#Aggarwal2015Theoretical] Aggarwal, C.C. and Sathe, S., 2015. Theoretical foundations and algorithms for outlier ensembles.\ *ACM SIGKDD Explorations Newsletter*\ , 17(1), pp.24-47.



.. [#Aggarwal2017Outlier] Aggarwal, C.C. and Sathe, S., 2017. Outlier ensembles: An introduction. Springer.



.. [#Almardeny2020A] Almardeny, Y., Boujnah, N. and Cleary, F., 2020. A Novel Outlier Detection Method for Multivariate Data. *IEEE Transactions on Knowledge and Data Engineering*.



.. [#Angiulli2002Fast] Angiulli, F. and Pizzuti, C., 2002, August. Fast outlier detection in high dimensional spaces. In *European Conference on Principles of Data Mining and Knowledge Discovery* pp. 15-27.



.. [#Arning1996A] Arning, A., Agrawal, R. and Raghavan, P., 1996, August. A Linear Method for Deviation Detection in Large Databases. In *KDD* (Vol. 1141, No. 50, pp. 972-981).



.. [#Bandaragoda2018Isolation] Bandaragoda, T. R., Ting, K. M., Albrecht, D., Liu, F. T., Zhu, Y., and Wells, J. R., 2018, Isolation-based anomaly detection using nearest-neighbor ensembles. *Computational Intelligence*\ , 34(4), pp. 968-998.



.. [#Breunig2000LOF] Breunig, M.M., Kriegel, H.P., Ng, R.T. and Sander, J., 2000, May. LOF: identifying density-based local outliers. *ACM Sigmod Record*\ , 29(2), pp. 93-104.



.. [#Burgess2018Understanding] Burgess, Christopher P., et al. "Understanding disentangling in beta-VAE." arXiv preprint arXiv:1804.03599 (2018).



.. [#Campello2013Density] Campello, R.J.G.B., Moulavi, D. and Sander, J., 2013, April. Density-based clustering based on hierarchical density estimates. In *Pacific-Asia Conference on Knowledge Discovery and Data Mining* (pp. 160-172). Springer.



.. [#Cook1977Detection] Cook, R.D., 1977. Detection of influential observation in linear regression. Technometrics, 19(1), pp.15-18.



.. [#Chen2024PyOD] Chen, S., Qian, Z., Siu, W., Hu, X., Li, J., Li, S., Qin, Y., Yang, T., Xiao, Z., Ye, W. and Zhang, Y., 2024. PyOD 2: A Python Library for Outlier Detection with LLM-powered Model Selection. arXiv preprint arXiv:2412.12154.



.. [#Fang2001Wrap] Fang, K.T. and Ma, C.X., 2001. Wrap-around L2-discrepancy of random sampling, Latin hypercube and uniform designs. Journal of complexity, 17(4), pp.608-624.



.. [#Goldstein2012Histogram] Goldstein, M. and Dengel, A., 2012. Histogram-based outlier score (hbos): A fast unsupervised anomaly detection algorithm. In *KI-2012: Poster and Demo Track*\ , pp.59-63.



.. [#Goodge2022Lunar] Goodge, A., Hooi, B., Ng, S.K. and Ng, W.S., 2022, June. Lunar: Unifying local outlier detection methods via graph neural networks. In Proceedings of the AAAI Conference on Artificial Intelligence.



.. [#Gopalan2019PIDForest] Gopalan, P., Sharan, V. and Wieder, U., 2019. PIDForest: Anomaly Detection via Partial Identification. In Advances in Neural Information Processing Systems, pp. 15783-15793.



.. [#Han2022ADBench] Han, S., Hu, X., Huang, H., Jiang, M. and Zhao, Y., 2022. ADBench: Anomaly Detection Benchmark. arXiv preprint arXiv:2206.09426.



.. [#Hardin2004Outlier] Hardin, J. and Rocke, D.M., 2004. Outlier detection in the multiple cluster setting using the minimum covariance determinant estimator. *Computational Statistics & Data Analysis*\ , 44(4), pp.625-638.



.. [#He2003Discovering] He, Z., Xu, X. and Deng, S., 2003. Discovering cluster-based local outliers. *Pattern Recognition Letters*\ , 24(9-10), pp.1641-1650.



.. [#Hoffmann2007Kernel] Hoffmann, H., 2007. Kernel PCA for novelty detection. Pattern recognition, 40(3), pp.863-874.



.. [#Iglewicz1993How] Iglewicz, B. and Hoaglin, D.C., 1993. How to detect and handle outliers (Vol. 16). Asq Press.



.. [#Janssens2012Stochastic] Janssens, J.H.M., Huszár, F., Postma, E.O. and van den Herik, H.J., 2012. Stochastic outlier selection. Technical report TiCC TR 2012-001, Tilburg University, Tilburg Center for Cognition and Communication, Tilburg, The Netherlands.



.. [#Kingma2013Auto] Kingma, D.P. and Welling, M., 2013. Auto-encoding variational bayes. arXiv preprint arXiv:1312.6114.



.. [#Kriegel2008Angle] Kriegel, H.P. and Zimek, A., 2008, August. Angle-based outlier detection in high-dimensional data. In *KDD '08*\ , pp. 444-452. ACM.



.. [#Kriegel2009Outlier] Kriegel, H.P., Kröger, P., Schubert, E. and Zimek, A., 2009, April. Outlier detection in axis-parallel subspaces of high dimensional data. In *Pacific-Asia Conference on Knowledge Discovery and Data Mining*\ , pp. 831-838. Springer, Berlin, Heidelberg.



.. [#Latecki2007Outlier] Latecki, L.J., Lazarevic, A. and Pokrajac, D., 2007, July. Outlier detection with kernel density functions. In International Workshop on Machine Learning and Data Mining in Pattern Recognition (pp. 61-75). Springer, Berlin, Heidelberg.



.. [#Lazarevic2005Feature] Lazarevic, A. and Kumar, V., 2005, August. Feature bagging for outlier detection. In *KDD '05*. 2005.



.. [#Li2024NLPADBench] Li, Y., Li, J., Xiao, Z., Yang, T., Nian, Y., Hu, X. and Zhao, Y., 2025. NLP-ADBench: NLP Anomaly Detection Benchmark. In *Findings of the Association for Computational Linguistics: EMNLP 2025*.



.. [#Li2019MADGAN] Li, D., Chen, D., Jin, B., Shi, L., Goh, J. and Ng, S.K., 2019, September. MAD-GAN: Multivariate anomaly detection for time series data with generative adversarial networks. In *International Conference on Artificial Neural Networks* (pp. 703-716). Springer, Cham.



.. [#Li2020COPOD] Li, Z., Zhao, Y., Botta, N., Ionescu, C. and Hu, X. COPOD: Copula-Based Outlier Detection. *IEEE International Conference on Data Mining (ICDM)*, 2020.



.. [#Li2021ECOD] Li, Z., Zhao, Y., Hu, X., Botta, N., Ionescu, C. and Chen, H. G. ECOD: Unsupervised Outlier Detection Using Empirical Cumulative Distribution Functions. *IEEE Transactions on Knowledge and Data Engineering (TKDE)*, 2022.



.. [#Liu2008Isolation] Liu, F.T., Ting, K.M. and Zhou, Z.H., 2008, December. Isolation forest. In *International Conference on Data Mining*\ , pp. 413-422. IEEE.



.. [#Liu2019Generative] Liu, Y., Li, Z., Zhou, C., Jiang, Y., Sun, J., Wang, M. and He, X., 2019. Generative adversarial active learning for unsupervised outlier detection. *IEEE Transactions on Knowledge and Data Engineering*.



.. [#Nguyen2019scalable] Nguyen, M.N. and Vien, N.A., 2019. Scalable and interpretable one-class svms with deep learning and random fourier features. In *Machine Learning and Knowledge Discovery in Databases: European Conference*, ECML PKDD, 2018.



.. [#Pang2019Deep] Pang, Guansong, Chunhua Shen, and Anton Van Den Hengel. "Deep anomaly detection with deviation networks." In *KDD*, pp. 353-362. 2019.



.. [#Papadimitriou2003LOCI] Papadimitriou, S., Kitagawa, H., Gibbons, P.B. and Faloutsos, C., 2003, March. LOCI: Fast outlier detection using the local correlation integral. In *ICDE '03*, pp. 315-326. IEEE.



.. [#Pevny2016Loda] Pevný, T., 2016. Loda: Lightweight on-line detector of anomalies. *Machine Learning*, 102(2), pp.275-304.



.. [#Perini2020Quantifying] Perini, L., Vercruyssen, V., Davis, J. Quantifying the confidence of anomaly detectors in their example-wise predictions. In *Joint European Conference on Machine Learning and Knowledge Discovery in Databases (ECML-PKDD)*, 2020.



.. [#Perini2023Rejection] Perini, L., Davis, J. Unsupervised anomaly detection with rejection. In *Proceedings of the Thirty-Seven Conference on Neural Information Processing Systems (NeurIPS)*, 2023.



.. [#Ramaswamy2000Efficient] Ramaswamy, S., Rastogi, R. and Shim, K., 2000, May. Efficient algorithms for mining outliers from large data sets. *ACM Sigmod Record*\ , 29(2), pp. 427-438.



.. [#Rousseeuw1999A] Rousseeuw, P.J. and Driessen, K.V., 1999. A fast algorithm for the minimum covariance determinant estimator. *Technometrics*\ , 41(3), pp.212-223.



.. [#Ruff2018Deep] Ruff, L., Vandermeulen, R., Goernitz, N., Deecke, L., Siddiqui, S.A., Binder, A., Müller, E. and Kloft, M., 2018, July. Deep one-class classification. In *International conference on machine learning* (pp. 4393-4402). PMLR.



.. [#Schlegl2017Unsupervised] Schlegl, T., Seeböck, P., Waldstein, S.M., Schmidt-Erfurth, U. and Langs, G., 2017, June. Unsupervised anomaly detection with generative adversarial networks to guide marker discovery. In International conference on information processing in medical imaging (pp. 146-157). Springer, Cham.



.. [#Scholkopf2001Estimating] Scholkopf, B., Platt, J.C., Shawe-Taylor, J., Smola, A.J. and Williamson, R.C., 2001. Estimating the support of a high-dimensional distribution. *Neural Computation*, 13(7), pp.1443-1471.



.. [#Shyu2003A] Shyu, M.L., Chen, S.C., Sarinnapakorn, K. and Chang, L., 2003. A novel anomaly detection scheme based on principal component classifier. *MIAMI UNIV CORAL GABLES FL DEPT OF ELECTRICAL AND COMPUTER ENGINEERING*.



.. [#Sugiyama2013Rapid] Sugiyama, M. and Borgwardt, K., 2013. Rapid distance-based outlier detection via sampling. Advances in neural information processing systems, 26.



.. [#Tang2002Enhancing] Tang, J., Chen, Z., Fu, A.W.C. and Cheung, D.W., 2002, May. Enhancing effectiveness of outlier detections for low density patterns. In *Pacific-Asia Conference on Knowledge Discovery and Data Mining*, pp. 535-548. Springer, Berlin, Heidelberg.



.. [#Wang2020adVAE] Wang, X., Du, Y., Lin, S., Cui, P., Shen, Y. and Yang, Y., 2019. adVAE: A self-adversarial variational autoencoder with Gaussian anomaly prior knowledge for anomaly detection. *Knowledge-Based Systems*.



.. [#Xu2023Deep] Xu, H., Pang, G., Wang, Y., Wang, Y., 2023. Deep isolation forest for anomaly detection. *IEEE Transactions on Knowledge and Data Engineering*.



.. [#Yang2024ad] Yang, T., Nian, Y., Li, S., Xu, R., Li, Y., Li, J., Xiao, Z., Hu, X., Rossi, R., Ding, K. and Hu, X., 2024. AD-LLM: Benchmarking Large Language Models for Anomaly Detection. arXiv preprint arXiv:2412.11142.



.. [#You2017Provable] You, C., Robinson, D.P. and Vidal, R., 2017. Provable self-representation based outlier detection in a union of subspaces. In Proceedings of the IEEE conference on computer vision and pattern recognition.



.. [#Zenati2018Adversarially] Zenati, H., Romain, M., Foo, C.S., Lecouat, B. and Chandrasekhar, V., 2018, November. Adversarially learned anomaly detection. In 2018 IEEE International conference on data mining (ICDM) (pp. 727-736). IEEE.



.. [#Zhao2018XGBOD] Zhao, Y. and Hryniewicki, M.K. XGBOD: Improving Supervised Outlier Detection with Unsupervised Representation Learning. *IEEE International Joint Conference on Neural Networks*\ , 2018.



.. [#Zhao2019LSCP] Zhao, Y., Nasrullah, Z., Hryniewicki, M.K. and Li, Z., 2019, May. LSCP: Locally selective combination in parallel outlier ensembles. In *Proceedings of the 2019 SIAM International Conference on Data Mining (SDM)*, pp. 585-593. Society for Industrial and Applied Mathematics.



.. [#Zhao2021SUOD] Zhao, Y., Hu, X., Cheng, C., Wang, C., Wan, C., Wang, W., Yang, J., Bai, H., Li, Z., Xiao, C., Wang, Y., Qiao, Z., Sun, J. and Akoglu, L. (2021). SUOD: Accelerating Large-scale Unsupervised Heterogeneous Outlier Detection. *Conference on Machine Learning and Systems (MLSys)*.



.. [#Boniol2021SAND] Boniol, P., Paparrizos, J., Palpanas, T. and Franklin, M.J., 2021. SAND: Streaming Subsequence Anomaly Detection. *Proceedings of the VLDB Endowment*, 14(10), pp.1717-1729.



.. [#Malhotra2015Long] Malhotra, P., Vig, L., Shroff, G. and Agarwal, P., 2015. Long Short Term Memory Networks for Anomaly Detection in Time Series. In *European Symposium on Artificial Neural Networks (ESANN)*.



.. [#Paparrizos2015KShape] Paparrizos, J. and Gravano, L., 2015. k-Shape: Efficient and Accurate Clustering of Time Series. In *Proceedings of the 2015 ACM SIGMOD International Conference on Management of Data*, pp.1855-1870.



.. [#Ren2019Time] Ren, H., Xu, B., Wang, Y., Yi, C., Huang, C., Kou, X., Xing, T., Yang, M., Tong, J. and Zhang, Q., 2019. Time-Series Anomaly Detection Service at Microsoft. In *Proceedings of the 25th ACM SIGKDD International Conference on Knowledge Discovery & Data Mining*, pp.3009-3017.



.. [#Xu2022Anomaly] Xu, J., Wu, H., Wang, J. and Long, M., 2022. Anomaly Transformer: Time Series Anomaly Detection with Association Discrepancy. In *International Conference on Learning Representations (ICLR)*.



.. [#Yeh2016Matrix] Yeh, C.C.M., Zhu, Y., Ulanova, L., Begum, N., Ding, Y., Dau, H.A., Silva, D.F., Mueen, A. and Keogh, E., 2016. Matrix Profile I: All Pairs Similarity Joins for Time Series Subsequences. In *2016 IEEE 16th International Conference on Data Mining (ICDM)*, pp.1317-1322.



.. [#Ding2019DOMINANT] Ding, K., Li, J., Bhanushali, R. and Liu, H., 2019. Deep Anomaly Detection on Attributed Networks. In *Proceedings of the 2019 SIAM International Conference on Data Mining*, pp.594-602. SIAM.



.. [#Liu2022CoLA] Liu, Y., Li, Z., Pan, S., Gool, T., Xiang, T. and Gong, B., 2022. Anomaly Detection on Attributed Networks via Contrastive Self-Supervised Learning. In *Proceedings of the ACM Web Conference 2022*, pp.2137-2147.



.. [#Xu2022CONAD] Xu, Z., Huang, X., Zhao, Y., Dong, Y. and Li, J., 2022. Contrastive Attributed Network Anomaly Detection with Data Augmentation. In *Pacific-Asia Conference on Knowledge Discovery and Data Mining*, pp.444-457. Springer.



.. [#Fan2020AnomalyDAE] Fan, H., Zhang, F. and Li, Z., 2020. AnomalyDAE: Dual Autoencoder for Anomaly Detection on Attributed Networks. In *Proceedings of the 29th ACM International Conference on Information and Knowledge Management*, pp.747-756.



.. [#Yuan2021GUIDE] Yuan, X., Zhou, N., Yu, S., Huang, H., Chen, Z. and Xia, F., 2021. Higher-Order Structure Based Anomaly Detection on Attributed Networks. In *2021 IEEE International Conference on Big Data*, pp.2691-2700. IEEE.



.. [#Li2017Radar] Li, J., Dani, H., Hu, X. and Liu, H., 2017. Radar: Residual Analysis for Anomaly Detection in Attributed Networks. In *Proceedings of the Twenty-Sixth International Joint Conference on Artificial Intelligence*, pp.2152-2158.



.. [#Peng2018ANOMALOUS] Peng, Z., Luo, M., Li, J., Liu, H. and Zheng, Q., 2018. ANOMALOUS: A Joint Modeling Approach for Anomaly Detection on Attributed Networks. In *Proceedings of the Twenty-Seventh International Joint Conference on Artificial Intelligence*, pp.3529-3535.



.. [#Xu2007SCAN] Xu, X., Yuruk, N., Feng, Z. and Schweiger, T.A.J., 2007. SCAN: A Structural Clustering Algorithm for Networks. In *Proceedings of the 13th ACM SIGKDD International Conference on Knowledge Discovery and Data Mining*, pp.824-833.



.. [#Liu2024TSB] Liu, Q., Boniol, P., Palpanas, T. and Paparrizos, J., 2024. TSB-AD: Towards A Reliable Time-Series Anomaly Detection Benchmark. In *Advances in Neural Information Processing Systems (NeurIPS)*.



.. [#Liu2022BOND] Liu, K., Dou, Y., Zhao, Y., Ding, X., Hu, X., Zhang, R., Ding, K., Chen, C., Peng, H., Shu, K., Sun, L., Li, J., Chen, G.H., Jia, Z. and Yu, P.S., 2022. BOND: Benchmarking Unsupervised Outlier Node Detection on Static Attributed Graphs. In *Advances in Neural Information Processing Systems (NeurIPS)*.
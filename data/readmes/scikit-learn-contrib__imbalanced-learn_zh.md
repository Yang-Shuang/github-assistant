.. -*- mode: rst -*-

.. _scikit-learn: http://scikit-learn.org/stable/

.. _scikit-learn-contrib: https://github.com/scikit-learn-contrib

|GitHubActions|_ |Codecov|_ |CircleCI|_ |PythonVersion|_ |Pypi|_ |Gitter|_ |Black|_

.. |GitHubActions| image:: https://github.com/scikit-learn-contrib/imbalanced-learn/actions/workflows/tests.yml/badge.svg
.. _GitHubActions: https://github.com/scikit-learn-contrib/imbalanced-learn/actions/workflows/tests.yml

.. |Codecov| image:: https://codecov.io/gh/scikit-learn-contrib/imbalanced-learn/branch/master/graph/badge.svg
.. _Codecov: https://codecov.io/gh/scikit-learn-contrib/imbalanced-learn

.. |CircleCI| image:: https://circleci.com/gh/scikit-learn-contrib/imbalanced-learn.svg?style=shield
.. _CircleCI: https://circleci.com/gh/scikit-learn-contrib/imbalanced-learn/tree/master

.. |PythonVersion| image:: https://img.shields.io/pypi/pyversions/imbalanced-learn.svg
.. _PythonVersion: https://img.shields.io/pypi/pyversions/imbalanced-learn.svg

.. |Pypi| image:: https://badge.fury.io/py/imbalanced-learn.svg
.. _Pypi: https://badge.fury.io/py/imbalanced-learn

.. |Gitter| image:: https://badges.gitter.im/scikit-learn-contrib/imbalanced-learn.svg
.. _Gitter: https://gitter.im/scikit-learn-contrib/imbalanced-learn?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge

.. |Black| image:: https://img.shields.io/badge/code%20style-black-000000.svg
.. _Black: :target: https://github.com/psf/black

.. |PythonMinVersion| replace:: 3.10
.. |NumPyMinVersion| replace:: 1.25.2
.. |SciPyMinVersion| replace:: 1.11.4
.. |ScikitLearnMinVersion| replace:: 1.4.2
.. |MatplotlibMinVersion| replace:: 3.7.3
.. |PandasMinVersion| replace:: 2.0.3
.. |TensorflowMinVersion| replace:: 2.16.1
.. |KerasMinVersion| replace:: 3.3.3
.. |SeabornMinVersion| replace:: 0.12.2
.. |PytestMinVersion| replace:: 7.2.2

imbalanced-learn
================

`imbalanced-learn` 是一个 Python 包，提供了一系列常用于处理类间不平衡数据集的重采样技术。它与 scikit-learn_ 兼容，并属于 scikit-learn-contrib_ 项目的一部分。

Documentation
-------------

安装文档、API 文档和示例可在 documentation_ 中找到。

.. _documentation: https://imbalanced-learn.org/stable/

Installation
------------

Dependencies
~~~~~~~~~~~~

`imbalanced-learn` 需要以下依赖项：

- Python (>= |PythonMinVersion|)
- NumPy (>= |NumPyMinVersion|)
- SciPy (>= |SciPyMinVersion|)
- Scikit-learn (>= |ScikitLearnMinVersion|)
- Pytest (>= |PytestMinVersion|)

此外，`imbalanced-learn` 还需要以下可选依赖项：

- Pandas (>= |PandasMinVersion|)，用于处理 DataFrame
- Tensorflow (>= |TensorflowMinVersion|)，用于处理 TensorFlow 模型
- Keras (>= |KerasMinVersion|)，用于处理 Keras 模型

示例代码需要以下额外依赖项：

- Matplotlib (>= |MatplotlibMinVersion|)
- Seaborn (>= |SeabornMinVersion|)

Installation
~~~~~~~~~~~~

From PyPi or conda-forge repositories
.....................................

`imbalanced-learn` 目前可在 PyPI 上获取，你可以通过 `pip` 进行安装：

  pip install -U imbalanced-learn

该包也已发布在 Anaconda Cloud 平台上：

  conda install -c conda-forge imbalanced-learn

From source available on GitHub
...............................

如果你更倾向于从源码构建，可以克隆代码库并运行 `setup.py` 文件。使用以下命令从 GitHub 获取副本并安装所有依赖项：

  git clone https://github.com/scikit-learn-contrib/imbalanced-learn.git
  cd imbalanced-learn
  pip install .

请注意，你可以以开发者模式进行安装：

  pip install --no-build-isolation --editable .

如果你希望在 GitHub 上提交 Pull Request，我们建议你安装 `pre-commit`：

  pip install pre-commit
  pre-commit install

Testing
~~~~~~~

安装完成后，你可以使用 `pytest` 运行测试套件：

  make coverage

Development
-----------

本 scikit-learn-contrib 项目的开发与 scikit-learn 社区保持一致。因此，你可以参考他们的开发指南 `<http://scikit-learn.org/stable/developers>`_。

Endorsement of the Scientific Python Specification
--------------------------------------------------

我们支持科学 Python 生态系统协调组织（Scientific Python Ecosystem Coordination, SPEC）的良好实践。完整推荐列表见 `here`_。

以下是我们为 imbalanced-learn 项目所支持的推荐项列表：

|SPEC 0 — Minimum Supported Dependencies|

.. |SPEC 0 — Minimum Supported Dependencies| image:: https://img.shields.io/badge/SPEC-0-green?labelColor=%23004811&color=%235CA038
   :target: https://scientific-python.org/specs/spec-0000/

.. _here: https://scientific-python.org/specs/

About
-----

如果你在科学出版物中使用了 imbalanced-learn，我们将非常感谢你引用以下论文：

  @article{JMLR:v18:16-365,
  author  = {Guillaume  Lema{{\^i}}tre and Fernando Nogueira and Christos K. Aridas},
  title   = {Imbalanced-learn: A Python Toolbox to Tackle the Curse of Imbalanced Datasets in Machine Learning},
  journal = {Journal of Machine Learning Research},
  year    = {2017},
  volume  = {18},
  number  = {17},
  pages   = {1-5},
  url     = {http://jmlr.org/papers/v18/16-365}
  }

大多数分类算法在各类别样本数量大致相同时才能达到最佳性能。高度倾斜的数据集（少数类样本量远少于其他类别）一直是个难题，但同时正变得愈发普遍。

解决此问题的一种方法是通过对数据集进行重采样来抵消这种不平衡，从而期望获得比直接处理更稳健、更公平的决策边界。

你可以参考 `imbalanced-learn`_ 文档以了解已实现算法的详细信息。

.. _imbalanced-learn: https://imbalanced-learn.org/stable/user_guide.html
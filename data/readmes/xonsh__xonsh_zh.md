Xonsh
=====

.. raw:: html

    <img src="https://avatars.githubusercontent.com/u/17418188?s=200&v=4" alt="Xonsh shell icon." align="left" width="100px">

**Xonsh**（发音类似“consh”）是一款功能齐全且跨平台的基于 Python 的 Shell。该语言是 Python 3 的超集，无缝集成了 Shell 功能和命令。它支持所有主流平台，包括 Linux、macOS、Windows、BSD、Jupyter、Android 和 Raspberry Pi。

.. raw:: html

    <br clear="left"/>

.. list-table::
   :widths: 1 1

   *  -  **Xonsh 即 Shell**
      -  **Xonsh 即 Python**

   *  -  .. code-block:: shell

            cd $HOME

            id $(whoami) > ~/id.txt

            cat /etc/passwd | grep root

            $PROMPT = '@ '


      -  .. code-block:: python

            2 + 2

            var = "hello".upper()

            @.imp.json.loads('{"a":1}')

            [i for i in range(0,10)]

   *  -  **Xonsh：Python 里的 Shell**
      -  **Xonsh：Shell 里的 Python**

   *  -  .. code-block:: python

            len($(curl -L https://xon.sh))

            $PATH.append('/tmp')

            p'/etc/passwd'.read_text().find('usr')

            $(@json podman ps --format json)['ID']

      -  .. code-block:: python

            name = 'snail'
            echo @(name) > /tmp/@(name)

            with p'/tmp/dir'.mkdir().cd():
                touch @(input('File: '))

            aliases['e'] = 'echo @(2+2)'
            aliases['a'] = lambda args: print(args)

   *  -  **无处不在的 Xonsh**
      -  **生态丰富的 Xonsh**

   *  -  .. code-block:: python

            $PATH
            # ['/bin', '/sbin']           # Linux
            # ['/homebrew/bin']           # macOS
            # ['/usr/local/bin']          # FreeBSD
            # ['/mnt/c/Windows/System32'] # WSL
            # [r'c:\Windows\System32']    # Windows
            # ['/nix/store/0-python/bin'] # Nix
            # ['/data/termux/usr/bin']    # Termux
            # ['/tmp/.mount_x/usr/bin/']  # AppImage
            # ['/app/bin']                # Flatpak

            $PATH = ['/my/own/path']


      -  .. code-block:: python

            xontrib load term_integration \
                         prompt_starship  \
                         powerline        \
                         dracula          \
                         chatgpt          \
                         django           \
                         jupyter          \
                         1password        \
                         github_copilot   \
                         history_encrypt

   *  -  **元级 Shell（Meta-Shell）**
      -  **用户可扩展的 Xonsh**


   *  -  .. code-block:: python

            xontrib load sh \
                         fish_completer

            osqueryi ! SELECT platform FROM os_version

            def nudf(cmd):
                return @.imp.pandas.DataFrame(
                  $(@json nu -c @(cmd+'| to json')))
            nudf!(ls -la)

            aliases['ai'] = 'ollama run llama3'
            ai! how to remove images in podman

      -  .. code-block:: python

            @events.on_ptk_create
            def custom_keybindings(bindings, **kw):
                @bindings.add(Keys.ControlI)
                def say_whoami(event):
                    echo $(whoami)

            @events.on_postcommand
            def _prompt_err_cmd(cmd, rtn, out, ts):
                if rtn != 0:
                    $XONSH_PROMPT_NEXT_CMD = cmd.rstrip()

如果你喜欢 Xonsh，请给仓库 :star:（点赞）并分享推广 Xonsh。

.. class:: center

    .. image:: https://img.shields.io/badge/Zulip%20Community-xonsh-green
            :target: https://xonsh.zulipchat.com/
            :alt: Join to xonsh.zulipchat.com

    .. image:: https://repology.org/badge/tiny-repos/xonsh.svg
            :target: https://repology.org/project/xonsh/versions
            :alt: repology.org

    .. image:: https://img.shields.io/badge/Docker%20Hub-xonsh-blue
            :target: https://hub.docker.com/u/xonsh
            :alt: hub.docker.com

    .. image:: https://img.shields.io/badge/AppImage-xonsh-lightblue
            :target: https://xon.sh/appimage.html
            :alt: AppImage

    .. image:: https://github.com/xonsh/xonsh/actions/workflows/test.yml/badge.svg
            :target: https://github.com/xonsh/xonsh/actions/workflows/test.yml
            :alt: GitHub Actions

    .. image:: https://codecov.io/gh/xonsh/xonsh/branch/master/graphs/badge.svg?branch=main
            :target: https://codecov.io/github/xonsh/xonsh?branch=main
            :alt: codecov.io

First steps
***********

- `Installation <https://xon.sh/install.html>`_ - 隔离环境、包管理器、容器或便携版 AppImage。
- `Tutorial <https://xon.sh/tutorial.html>`_ - Xonsh 逐步入门指南。

Extensions
**********

Xonsh 拥有扩展/插件系统。我们将这些附加组件称为 ``xontribs``。

- `Xontribs on Github <https://github.com/topics/xontrib>`_
- `Awesome xontribs <https://github.com/xonsh/awesome-xontribs>`_
- `Core xontribs <https://xon.sh/api/_autosummary/xontribs/xontrib.html>`_
- `Create a xontrib step by step from template <https://github.com/xonsh/xontrib-template>`_

Projects that use Xonsh or compatible
*************************************

- `Assistant <https://gitlab.com/waser-technologies/technologies/assistant>`_: 一款配备完整 Xonsh 终端和多智能体 LLM 系统的 AI Shell。
- `CrateDB <https://github.com/crate>`_: 面向实时分析与混合搜索的数据库。
- `conda <https://conda.io/projects/conda/en/latest/>`_ and `mamba <https://mamba.readthedocs.io/en/latest/>`_: 跨平台包管理器。
- `Starship <https://starship.rs/>`_: 跨 Shell 提示符（Prompt）。
- `zoxide <https://github.com/ajeetdsouza/zoxide>`_: 更智能的 `cd` 命令。
- `gitsome <https://github.com/donnemartin/gitsome>`_: 集成 GitHub 功能的增强型 Git/Shell 自动补全工具。
- `xxh <https://github.com/xxh/xxh>`_: 通过 SSH 在任何地方使用 Xonsh。
- `kash <https://github.com/jlevy/kash>`_: 知识智能体 Shell。
- `Snakemake <https://snakemake.readthedocs.io/en/stable/snakefiles/rules.html#xonsh>`_: 用于创建可复现、可扩展数据分析的工作流管理系统。
- `any-nix-shell <https://github.com/haslersn/any-nix-shell>`_: 为 Nix 包管理器的 ``nix run`` 和 ``nix-shell`` 环境提供 Xonsh 支持。
- `lix <https://github.com/lix-project/lix>`_: 现代且美味的 Nix 包管理器实现。
- `x-cmd <https://www.x-cmd.com/>`_: 遵循 Unix 哲学理念的庞大而有趣的工具集合。
- `rever <https://regro.github.io/rever-docs/>`_: 跨平台软件发布工具。
- `Regro autotick bot <https://github.com/regro/cf-scripts>`_: Regro Conda-Forge 自动更新机器人。

Jupyter-based interactive notebooks via `xontrib-jupyter <https://github.com/xonsh/xontrib-jupyter>`_:

- `Jupyter and JupyterLab <https://jupyter.org/>`_: 交互式笔记本平台。
- `Euporie <https://github.com/joouha/euporie>`_: 基于终端的交互式计算环境。
- `Jupytext <https://jupytext.readthedocs.io/>`_: 在进行 Jupyter 版本控制时提供清晰且有意义的差异对比。

Compiling, packaging, or accelerating Xonsh:

- `AppImage <https://github.com/appimage>`_ 是一种用于分发 Linux 应用程序的格式，可用于 `创建独立的 Xonsh 包 <https://xon.sh/appimage.html>`_。
- `Nuitka <https://github.com/Nuitka/Nuitka>`_ 是一个优化的 Python 编译器，可 `构建原生 Xonsh 二进制文件 <https://github.com/xonsh/xonsh/issues/2895#issuecomment-3665753657>`_。
- `RustPython <https://github.com/RustPython/RustPython/>`_ 是一个用 Rust 编写的 Python 解释器，可 `在 Rust 之上运行 Xonsh <https://github.com/xonsh/xonsh/issues/5082#issue-1611837062>`_。


Welcome to the Xonsh shell community
************************************

Xonsh Shell 由志愿者社区共同开发。你可以通过以下几种方式提供帮助：

- 撰写关于 Xonsh 的笔记或文章。
- 将 Xonsh 链接分享给你喜欢的博主。
- 在第三方工具中添加 Xonsh 支持：`包管理器 <https://github.com/topics/package-manager>`_、`终端模拟器 <https://github.com/topics/terminal-emulators>`_、`控制台工具 <https://github.com/topics/console>`_、`IDE <https://github.com/topics/ide>`_。
- 为你喜欢的 Xonsh 仓库和 `xontribs <https://github.com/topics/xontrib>`_ 点赞（Star）。
- 解决 `热门 Issue <https://github.com/xonsh/xonsh/issues?q=is%3Aissue+is%3Aopen+sort%3Areactions-%2B1-desc>`_、`高优先级 Issue <https://github.com/xonsh/xonsh/issues?q=is%3Aopen+is%3Aissue+label%3Apriority-high+sort%3Areactions-%2B1-desc>`_ 或 `适合新手贡献的 Issue（good first issue）<https://github.com/xonsh/xonsh/issues?q=is%3Aopen+is%3Aissue+label%3A%22good+first+issue%22+sort%3Areactions-%2B1-desc>`_。你可以从 `开发者指南 <https://xon.sh/devguide.html>`_ 开始。欢迎使用 LLM（如 `GitHub Copilot <https://github.com/copilot>`_）辅助开发。
- 采纳一个 `创意点子 <https://github.com/xonsh/xontrib-template/issues?q=is%3Aopen+is%3Aissue+label%3Aidea+sort%3Areactions-%2B1-desc>`_，并 `创建新的 xontrib <https://github.com/xonsh/xontrib-template#why-use-this-template>`_。
- 为 `Xonsh API <https://github.com/xonsh/xonsh/tree/main/xonsh/api>`_ 做出贡献。
- 通过深入探索 Xonsh 内部机制成为核心开发者。例如，我们目前缺乏 Windows 支持方面的贡献者。
- 使用编译器、解释器或优化工具测试 Xonsh，并向上游报告问题（如 `Nuitka <https://github.com/xonsh/xonsh/issues/2895#issuecomment-3665753657>`_、`RustPython <https://github.com/xonsh/xonsh/issues/5082#issue-1611837062>`_）。
- 设计更多 `Logo 和图像 <https://github.com/anki-code/xonsh-logo>`_，改进 `Xonsh 官网 <https://xon.sh/>`_（源码位于 `<https://github.com/xonsh/xonsh/blob/12f12ce94f1b6c92218e22fbdaaa846e16ac8b2d/docs/_templates/index.html#L9>`_）。
- `成为 Xonsh 的赞助者 <https://github.com/sponsors/xonsh>`_。

我们欢迎新贡献者的加入！

Credits
*******

- 感谢 `Zulip <https://zulip.com/>`_ 对 `Xonsh 社区 <https://xonsh.zulipchat.com/>`_ 的支持！
- 感谢 `HELLOTUX <https://www.hellotux.com/>`_ 分发 `Xonsh T恤、背包等周边商品 <https://www.hellotux.com/xonsh>`_！
- 感谢 ADS.FUND 对 `Xonsh Token <https://ads.fund/token/0xadf7478450b69a349ed9634b18584d2d3da81464>`_ 的支持！
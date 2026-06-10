# Empire

## 本项目已停止维护

Empire 是一个后渗透框架，包含纯 PowerShell 2.0 Windows 代理和纯 Python 2.6/2.7 Linux/OS X 代理。它合并了之前的 PowerShell Empire 和 Python EmPyre 项目。该框架提供密码学安全的通信和灵活的架构。在 PowerShell 方面，Empire 实现了无需 `powershell.exe` 即可运行 PowerShell 代理的能力，提供了从键盘记录器到 Mimikatz 的快速部署后渗透模块，以及可适应网络检测的灵活通信机制，所有这些都被封装在一个注重易用性的框架中。PowerShell Empire 于 [2015年BSidesLV](https://www.youtube.com/watch?v=Pq9t59w0mUI) 首次亮相，Python EmPyre 则于 HackMiami 2016 首发。

Empire 的底层功能很大程度上依赖于其他多个项目的工作。我们已尽力在此处[重点列出](http://www.powershellempire.com/?page_id=2)与我们有密切合作的人员，并在每个 Empire 模块的源代码中酌情包含了作者/参考链接信息。如果我们未能正确引用现有或先前工作，请告知我们。

Empire 由 [@harmj0y](https://twitter.com/harmj0y)、[@sixdub](https://twitter.com/sixdub)、[@enigma0x3](https://twitter.com/enigma0x3)、[rvrsh3ll](https://twitter.com/424f424f)、[@killswitch_gui](https://twitter.com/killswitch_gui) 和 [@xorrior](https://twitter.com/xorrior) 开发。

欢迎加入我们的 Slack！ https://bloodhoundgang.herokuapp.com

## 安装

运行 `sudo ./setup/install.sh` 脚本进行安装，或使用相应的 Docker 镜像 `docker pull empireproject/empire`。

此外，还有[快速入门指南](http://www.powershellempire.com/?page_id=110)和完整的[文档](http://www.powershellempire.com/?page_id=83)。

## 快速入门

请查看 [Empire Wiki](https://github.com/EmpireProject/Empire/wiki/Quickstart) 获取开始使用 Empire 的说明。

## 贡献指南

非常欢迎贡献！参与该项目的人越多，Empire 对每个人来说就越好。以下是提交贡献的一些准则：

* 从 v2.4 版本开始，我们仅支持排查 Kali、Debian 或 Ubuntu 的问题。其他操作系统将不再提供支持。我们理解这可能会令人沮丧，但希望新的 Docker 构建能提供替代方案。
* 请将 Pull Request 提交至 [dev 分支](https://github.com/powershellempire/Empire/tree/dev)。测试通过后，更改将合并到 master 分支。
* 根据你的开发内容，请基于 [./lib/modules/powershell_template.py](lib/modules/powershell_template.py) 或 [./lib/modules/python_template.py](lib/modules/python_template.py) 来创建模块。**注意**：对于某些模块，你可能需要使用 `Out-String` [处理输出格式](https://github.com/PowerShellEmpire/Empire/blob/0cbdb165a29e4a65ad8dddf03f6f0e36c33a7350/lib/modules/situational_awareness/network/powerview/get_user.py#L111)，以将其转换为易于显示的文本格式。
* 在模块的 **“Comments”**（注释）部分引用先前工作。
* 如果你的 `script.ps1` 逻辑较大、可能被多个模块复用或经常更新，请考虑将逻辑实现在相应的 **data/module_source/*** 目录中，并在任务下发时[将脚本内容拉取到模块中](https://github.com/PowerShellEmpire/Empire/blob/0cbdb165a29e4a65ad8dddf03f6f0e36c33a7350/lib/modules/situational_awareness/network/powerview/get_user.py#L85-L95)。
* 所有函数请使用[官方批准的 PowerShell 动词](https://technet.microsoft.com/en-us/library/ms714428(v=vs.85).aspx)。
* **强烈建议**保持与 PowerShell 版本 2 的兼容性。 
* 测试你的模块！在提交 Pull Request 之前，务必通过 Empire 代理运行它，以确保一切正常运行。
* 有关 PowerShell 代码的额外规范，请参阅 [PowerSploit 风格指南](https://github.com/PowerShellMafia/PowerSploit/blob/master/README.md)。
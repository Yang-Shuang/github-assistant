![Claude Code Action 回复评论](https://github.com/user-attachments/assets/1d60c2e9-82ed-4ee5-b749-f9e021c85f4d)

# Claude Code Action

这是一个面向 GitHub PR（Pull Request）和 Issue 的通用 [Claude Code](https://claude.ai/code) Action，能够回答问题并实现代码变更。该 Action 会根据你的工作流上下文智能检测激活时机——无论是回复 @claude 提及、分配 Issue，还是使用显式提示词执行自动化任务。它支持多种认证方式，包括 Anthropic 直连 API（API Key 或 Workload Identity Federation）、Amazon Bedrock、Google Vertex AI 和 Microsoft Foundry。

## Features

- 🎯 **智能模式检测**：根据工作流上下文自动选择最合适的执行模式，无需额外配置
- 🤖 **交互式代码助手**：Claude 可回答关于代码、架构和编程的问题
- 🔍 **代码审查**：分析 PR 变更并提出改进建议
- ✨ **代码实现**：可执行简单修复、重构，甚至开发新功能
- 💬 **PR/Issue 集成**：与 GitHub 评论和 PR 审查无缝协作
- 🛠️ **灵活的工具访问**：可调用 GitHub API 及执行文件操作（可通过配置启用更多工具）
- 📋 **进度跟踪**：带有复选框的可视化进度指示器，随 Claude 完成任务动态更新
- 📊 **结构化输出**：获取经过验证的 JSON 结果，并自动转换为复杂自动化流程中的 GitHub Action 输出变量
- 🏃 **运行于自有基础设施**：Action 完全在您的 GitHub Runner 上执行（Anthropic API 调用将发往您选择的提供商）
- ⚙️ **简化配置**：统一的 `prompt` 和 `claude_args` 输入参数提供简洁强大的配置，与 Claude Code SDK 保持一致

## 📦 从 v0.x 升级？

**请参阅我们的 [迁移指南](./docs/migration-guide.md)**，获取将工作流更新至 v1.0 的分步说明。新版本简化了配置流程，同时兼容大多数现有设置。

## 快速上手

通过终端中的 [Claude Code](https://claude.ai/code) 设置此 Action 是最简单的方法。只需打开 `claude` 并运行 `/install-github-app`。

该命令将引导你完成 GitHub App 及相关密钥的配置。

**注意**：
- 你必须具备仓库管理员权限才能安装 GitHub App 并添加密钥
- 此快速上手方法仅适用于直接使用 Anthropic API 的用户。如需配置 AWS Bedrock、Google Vertex AI 或 Microsoft Foundry，请参阅 [docs/cloud-providers.md](./docs/cloud-providers.md)。

## 📚 解决方案与使用场景

正在寻找特定的自动化模式？查看我们的 **[解决方案指南](./docs/solutions.md)**，获取完整的可运行示例，包括：
- **🔍 自动 PR 代码审查** - 全流程审查自动化
- **📂 路径特定审查** - 针对关键文件变更触发
- **👥 外部贡献者审查** - 专门处理新贡献者的代码
- **📝 自定义审查清单** - 强制执行团队规范
- **🔄 计划维护** - 自动化仓库健康检查
- **🏷️ Issue 分类与打标** - 自动归类处理
- **📖 文档同步** - 随代码变更自动更新文档
- **🔒 安全导向审查** - 符合 OWASP 标准的安全分析
- **📊 自定义进度跟踪** - 在自动化模式中创建进度追踪评论

每个解决方案均包含完整的可运行示例、配置说明及预期效果。

## 文档

- **[Solutions Guide](./docs/solutions.md)** - 🎯 开箱即用的自动化模式
- **[Migration Guide](./docs/migration-guide.md)** - ⭐ 从 v0.x 升级至 v1.0
- [Setup Guide](./docs/setup.md) - 手动配置、自定义 GitHub App 及安全最佳实践
- [Usage Guide](./docs/usage.md) - 基础用法、工作流配置及输入参数说明
- [Custom Automations](./docs/custom-automations.md) - 自动化工作流示例与自定义提示词
- [Configuration](./docs/configuration.md) - MCP 服务器、权限（permission）、环境变量及高级设置
- [Experimental Features](./docs/experimental.md) - 执行模式与网络限制
- [Cloud Providers](./docs/cloud-providers.md) - AWS Bedrock、Google Vertex AI 和 Microsoft Foundry 配置指南
- [Capabilities & Limitations](./docs/capabilities-and-limitations.md) - Claude 的能力与限制说明
- [Security](./docs/security.md) - 访问控制、权限管理及 Commit 签名
- [FAQ](./docs/faq.md) - 常见问题与故障排除

## 📚 常见问题解答 (FAQ)

遇到问题或有疑问？请查阅我们的 [Frequently Asked Questions](./docs/faq.md)，获取常见问题的解决方案，以及关于 Claude 能力与限制的详细说明。

## License

本项目采用 MIT 许可证开源——详情请参阅 LICENSE 文件。
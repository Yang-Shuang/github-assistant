<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=12,14,25,27&height=200&section=header&text=Claude%20Skills&fontSize=80&fontColor=ffffff&animation=fadeIn&fontAlignY=35&desc=66%20Skills%20%E2%80%A2%209%20Workflows%20%E2%80%A2%20Built%20for%20Full-Stack%20Devs&descSize=20&descAlignY=55" width="100%"/>
</p>

<p align="center">
<a href="https://trendshift.io/repositories/20667" target="_blank"><img src="https://trendshift.io/api/badge/repositories/20667" alt="Jeffallan%2Fclaude-skills | Trendshift" style="width: 200px; height: 44px;" width="200" height="44"/></a>
<a href="https://github.com/hesreallyhim/awesome-claude-code"><img src="https://awesome.re/mentioned-badge.svg" alt="Mentioned in Awesome Claude Code" style="width: 200px; height: 44px;" width="200" height="44"/></a>
</p>

<p align="center">
  <a href="https://github.com/jeffallan/claude-skills"><img src="https://img.shields.io/badge/version-0.4.15-blue.svg?style=for-the-badge" alt="Version"/></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-green.svg?style=for-the-badge" alt="License"/></a>
  <a href="https://github.com/jeffallan/claude-skills"><img src="https://img.shields.io/badge/Claude_Code-Plugin-purple.svg?style=for-the-badge" alt="Claude Code"/></a>
  <a href="https://github.com/jeffallan/claude-skills/stargazers"><img src="https://img.shields.io/github/stars/jeffallan/claude-skills?style=for-the-badge&color=yellow" alt="Stars"/></a>
  <a href="https://github.com/jeffallan/claude-skills/actions/workflows/ci.yml"><img src="https://img.shields.io/github/actions/workflow/status/jeffallan/claude-skills/ci.yml?branch=main&style=for-the-badge&label=CI" alt="CI"/></a>
</p>

---

## 快速开始 (Quick Start)

```bash
/plugin marketplace add jeffallan/claude-skills
```
**然后，安装技能：**
```bash
/plugin install fullstack-dev-skills@jeffallan
```

如需查看所有安装方法及入门步骤，请参阅 [**快速开始指南**](QUICKSTART.md)。

**完整文档：** [jeffallan.github.io/claude-skills](https://jeffallan.github.io/claude-skills)

## 技能 (Skills)

<!-- SKILL_COUNT -->66<!-- /SKILL_COUNT --> 项专业技能，涵盖语言、后端/前端框架、基础设施、API、测试、DevOps、安全、数据/机器学习及平台专家等 12 个类别。

完整列表、决策树及工作流组合请参阅 [**技能指南**](SKILLS_GUIDE.md)。

## 使用模式 (Usage Patterns)

### 上下文感知激活 (Context-Aware Activation)

技能会根据你的请求自动激活：

```bash
# Backend Development
"Implement JWT authentication in my NestJS API"
→ Activates: NestJS Expert → Loads: references/authentication.md

# Frontend Development
"Build a React component with Server Components"
→ Activates: React Expert → Loads: references/server-components.md
```

### 多技能工作流 (Multi-Skill Workflows)

复杂任务会组合使用多项技能：

```
Feature Development: Feature Forge → Architecture Designer → Fullstack Guardian → Test Master → DevOps Engineer
Bug Investigation:   Debugging Wizard → Framework Expert → Test Master → Code Reviewer
Security Hardening:  Secure Code Guardian → Security Reviewer → Test Master
```

## 上下文工程 (Context Engineering)

使用 `/common-ground` 命令揭示并验证 Claude 对你项目的隐藏假设。完整文档请参阅 [**共同上下文指南**](docs/COMMON_GROUND.md)。

## 项目工作流 (Project Workflow)

<!-- WORKFLOW_COUNT -->9<!-- /WORKFLOW_COUNT --> 个工作流命令用于管理史诗（Epic）从需求发现到回顾的全过程，并与 Jira 和 Confluence 集成。完整命令参考及生命周期图表请参阅 [**工作流命令参考**](docs/WORKFLOW_COMMANDS.md)。

> [!TIP]
> **配置：** 工作流命令需要安装 Atlassian MCP Server。请参阅 [**Atlassian MCP 配置指南**](docs/ATLASSIAN_MCP_SETUP.md)。

## 文档索引 (Documentation)

- [**快速开始指南**](QUICKSTART.md) - 安装与入门步骤
- [**技能指南**](SKILLS_GUIDE.md) - 技能参考与决策树
- [**共同上下文**](docs/COMMON_GROUND.md) - 使用 `/common-ground` 进行上下文工程
- [**工作流命令**](docs/WORKFLOW_COMMANDS.md) - 项目工作流命令指南
- [**Atlassian MCP 配置**](docs/ATLASSIAN_MCP_SETUP.md) - Atlassian MCP Server 安装与配置
- [**本地开发**](docs/local_skill_development.md) - 本地技能开发指南
- [**贡献指南**](CONTRIBUTING.md) - 参与贡献规范
- **skills/\*/SKILL.md** - 各技能独立文档
- **skills/\*/references/** - 深度参考资料

## 参与贡献 (Contributing)

添加技能、编写参考资料及提交 Pull Request 的规范，请参阅 [**贡献指南**](CONTRIBUTING.md)。

## 更新日志 (Changelog)

完整版本历史记录与发布说明，请参阅 [版本历史](CHANGELOG.md)。

## 开源协议 (License)

MIT 开源协议 - 详细信息请参阅 [LICENSE](LICENSE) 文件。

## 获取帮助 (Support)

- **问题反馈：** [GitHub Issues](https://github.com/jeffallan/claude-skills/issues)
- **讨论区：** [GitHub Discussions](https://github.com/jeffallan/claude-skills/discussions)
- **代码仓库：** [github.com/jeffallan/claude-skills](https://github.com/jeffallan/claude-skills)

## 作者 (Author)

由 [**jeffallan**](https://jeffallan.github.io) [<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/linkedin/linkedin-original.svg" width="16" height="16" alt="LinkedIn"/>](https://www.linkedin.com/in/jeff-smolinski/) 开发

**首席顾问**，任职于 [**Synergetic Solutions**](https://synergetic.solutions) [<img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/linkedin/linkedin-original.svg" width="16" height="16" alt="LinkedIn"/>](https://www.linkedin.com/company/synergetic-holdings)

专注于全栈工程、安全工程、合规性及技术尽职调查。

## 社区 (Community)

[![Stargazers repo roster for @Jeffallan/claude-skills](https://reporoster.com/stars/Jeffallan/claude-skills)](https://github.com/Jeffallan/claude-skills/stargazers)

## 星标历史 (Star History)

[![Star History Chart](https://api.star-history.com/svg?repos=Jeffallan/claude-skills&type=date&legend=top-left)](https://www.star-history.com/#Jeffallan/claude-skills&type=date&legend=top-left)

---

**专为 Claude Code 打造** | **<!-- WORKFLOW_COUNT -->9<!-- /WORKFLOW_COUNT --> 个工作流** | **<!-- REFERENCE_COUNT -->366<!-- /REFERENCE_COUNT --> 个参考资料文件** | **<!-- SKILL_COUNT -->66<!-- /SKILL_COUNT --> 项技能**
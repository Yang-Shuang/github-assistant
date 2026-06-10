<div align="left">
  <a href="https://swarms.world">
    <img src="https://github.com/kyegomez/swarms/blob/master/images/new_logo.png" style="margin: 15px; max-width: 350px" width="70%" alt="Logo">
  </a>
</div>


<p align="left">
  <!-- Main Navigation Links -->
  <a href="https://swarms.ai">Swarms Website</a>
  <span>&nbsp;&nbsp;•&nbsp;&nbsp;</span>
  <a href="https://docs.swarms.world">Documentation</a>
  <span>&nbsp;&nbsp;•&nbsp;&nbsp;</span>
  <a href="https://swarms.world">Swarms Marketplace</a>
</p>


<p align="left">
  <a href="https://pypi.org/project/swarms/" target="_blank">
    <picture>
      <source srcset="https://img.shields.io/pypi/v/swarms?style=for-the-badge&color=3670A0" media="(prefers-color-scheme: dark)">
      <img alt="Version" src="https://img.shields.io/pypi/v/swarms?style=for-the-badge&color=3670A0">
    </picture>
  </a>
  <a href="https://pypi.org/project/swarms/" target="_blank">
    <picture>
      <source srcset="https://img.shields.io/pypi/dm/swarms?style=for-the-badge&color=3670A0" media="(prefers-color-scheme: dark)">
      <img alt="Downloads" src="https://img.shields.io/pypi/dm/swarms?style=for-the-badge&color=3670A0">
    </picture>
  </a>
  <a href="https://twitter.com/swarms_corp/">
    <picture>
      <source srcset="https://img.shields.io/badge/Twitter-Follow-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white" media="(prefers-color-scheme: dark)">
      <img src="https://img.shields.io/badge/Twitter-Follow-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white" alt="Twitter">
    </picture>
  </a>
  <a href="https://discord.gg/EamjgSaEQf">
    <picture>
      <source srcset="https://img.shields.io/badge/Discord-Join-5865F2?style=for-the-badge&logo=discord&logoColor=white" media="(prefers-color-scheme: dark)">
      <img src="https://img.shields.io/badge/Discord-Join-5865F2?style=for-the-badge&logo=discord&logoColor=white" alt="Discord">
    </picture>
  </a>
</p>

## 概述 (Overview)

>
> Swarms：企业级生产就绪型多智能体编排框架 

Swarms 是目前最可靠、可扩展且自适应的多智能体编排框架。我们提供了一套全面的生产就绪型预构建多智能体架构，包括顺序执行、并发执行和分层系统。此外，Swarms 还提供了与主流智能体框架的向后兼容性，并支持与 MCP、x402、Skills 等协议的互操作。


## 安装 (Install)

### 使用 pip

```bash
$ pip3 install -U swarms
```

### 使用 uv（推荐）

[uv](https://github.com/astral-sh/uv) 是一款用 Rust 编写的快速 Python 包安装器和解析器。

```bash
$ uv pip install swarms
```

### 使用 poetry

```bash
$ poetry add swarms
```

### 从源码构建

```bash
# Clone the repository
$ git clone https://github.com/kyegomez/swarms.git
$ cd swarms
$ pip install -r requirements.txt
```

<!-- ### Using Docker

The easiest way to get started with Swarms is using our pre-built Docker image:

```bash
# Pull and run the latest image
$ docker pull kyegomez/swarms:latest
$ docker run --rm kyegomez/swarms:latest python -c "import swarms; print('Swarms is ready!')"

# Run interactively for development
$ docker run -it --rm -v $(pwd):/app kyegomez/swarms:latest bash

# Using docker-compose (recommended for development)
$ docker-compose up -d
```

For more Docker options and advanced usage, see our [Docker documentation](/scripts/docker/DOCKER.md). -->

---

## 环境配置

[在此了解更多环境配置信息](https://docs.swarms.world/environment-setup)

```
OPENAI_API_KEY=""
WORKSPACE_DIR="agent_workspace"
ANTHROPIC_API_KEY=""
GROQ_API_KEY=""
```


### 你的第一个智能体 (Agent)

**智能体（Agent）**是蜂群系统的基本构建块——一个由 LLM + 工具 + 记忆驱动的自主实体。[在此了解更多](https://docs.swarms.world/api/agent)

```python
from swarms import Agent

# Initialize a new agent
agent = Agent(
    model_name="gpt-5.4", # Specify the LLM
    max_loops="auto",              # Set the number of interactions
    interactive=True,         # Enable interactive mode for real-time feedback
)

# Run the agent with a task
agent.run("What are the key benefits of using a multi-agent system?")
```

### 使用 `max_loops="auto"` 的自主智能体

设置 `max_loops="auto"` 后，智能体会自行判断任务何时完成——它会持续进行推理和行动，直到满足停止条件，而不是在固定迭代次数后强制中断。这是开放式、多步骤任务的推荐模式，尤其适用于执行步数无法预先确定的场景。

```python
from swarms import Agent

agent = Agent(
    agent_name="Autonomous-Research-Agent",
    agent_description="An autonomous agent that conducts multi-step research independently.",
    system_prompt=(
        "You are an autonomous research agent. Break down complex tasks into steps, "
        "execute each step thoroughly, and signal completion only when the full task is done."
    ),
    model_name="gpt-5.4",
    max_loops="auto",       # Agent decides when it's done — no fixed iteration cap
    autosave=True,
    verbose=True,
)

# The agent will keep looping — planning, executing, and reflecting — until it
# determines the task is fully complete.
result = agent.run(
    "Research the current state of quantum computing, identify the top three "
    "hardware approaches, and summarize the key challenges each faces."
)
print(result)
```

**何时使用 `max_loops="auto"`：**
- 开放式研究或分析任务
- 需要迭代优化的任务（例如：撰写 → 审查 → 修订）
- 任何执行步数依赖于中间结果的工作流

**何时使用固定的 `max_loops` 值：**
- 对延迟或成本敏感的生产流水线
- 具有明确定义且步骤有限的任务

### 你的第一个蜂群 (Swarm)：多智能体协作

一个 **蜂群（Swarm）** 由多个协同工作的智能体组成。这个简单的示例创建了一个用于研究和撰写博客文章的双智能体工作流。[了解更多关于 SequentialWorkflow](https://docs.swarms.world/api/sequential-workflow)

```python
from swarms import Agent, SequentialWorkflow

# Agent 1: The Researcher
researcher = Agent(
    agent_name="Researcher",
    system_prompt="Your job is to research the provided topic and provide a detailed summary.",
    model_name="gpt-5.4",
)

# Agent 2: The Writer
writer = Agent(
    agent_name="Writer",
    system_prompt="Your job is to take the research summary and write a beautiful, engaging blog post about it.",
    model_name="gpt-5.4",
)

# Create a sequential workflow where the researcher's output feeds into the writer's input
workflow = SequentialWorkflow(agents=[researcher, writer])

# Run the workflow on a task
final_post = workflow.run("The history and future of artificial intelligence")
print(final_post)

```

-----

## 可用的多智能体架构 (Available Multi-Agent Architectures)

`swarms` 提供了多种强大的预构建多智能体架构，使你能够以不同方式编排智能体。为你的具体问题选择合适的结构，即可构建高效且可靠的生产级系统。

| **架构** | **描述** | **适用场景** |
|---|---|---|
| **[SequentialWorkflow](https://docs.swarms.world/api/sequential-workflow)** | 智能体按线性链条依次执行任务；前一个智能体的输出将作为下一个智能体的输入。 | 具有明确顺序的步骤流程，如数据转换管道和报告生成。 |
| **[ConcurrentWorkflow](https://docs.swarms.world/api/concurrent-workflow)** | 多个智能体同时运行任务以实现最大效率。 | 高吞吐量任务，如批处理和并行数据分析。 |
| **[AgentRearrange](https://docs.swarms.world/api/agent-rearrange)** | 动态映射智能体之间复杂的关系（例如 `a -> b, c`）。 | 灵活且自适应的工作流、任务分发和动态路由。 |
| **[GraphWorkflow](https://docs.swarms.world/api/graph-workflow)** | 将智能体作为有向无环图 (DAG) 中的节点进行编排。 | 具有复杂依赖关系的复杂项目，如软件构建流程。 |
| **[MixtureOfAgents (MoA)](https://docs.swarms.world/api/mixture-of-agents)** | 并行使用多个专家智能体并综合其输出结果。 | 复杂问题解决及通过协作实现最先进的性能表现。 |
| **[GroupChat](https://docs.swarms.world/api/group-chat)** | 智能体通过对话界面进行协作与决策。 | 实时协同决策、谈判和头脑风暴。 |
| **[ForestSwarm](https://docs.swarms.world/api/forest-swarm)** | 动态选择最适合给定任务或其子树结构的智能体。 | 任务路由、优化专业领域匹配以及复杂决策树。 |
| **[HierarchicalSwarm](https://docs.swarms.world/api/hierarchical-swarm)** | 编排具有主管的智能体系统，由主管制定计划并将任务分发给专业化的执行智能体。 | 复杂项目管理、团队协调及带有反馈循环的分层决策。 |
| **[HeavySwarm](https://docs.swarms.world/api/heavy-swarm)** | 实现包含五个阶段的复杂工作流（研究、分析、备选方案、验证），由专业化智能体负责全面的任务分析。 | 复杂的调研与分析任务、金融分析、战略规划及综合报告生成。 |
| **[SwarmRouter](https://docs.swarms.world/api/swarm-router)** | 一个通用编排器，提供单一接口以动态选择并运行任意类型的蜂群系统。 | 简化复杂工作流、在不同蜂群策略间切换以及统一的多智能体管理。 |

-----

### SequentialWorkflow

`SequentialWorkflow` 按严格顺序执行任务，形成流水线架构，每个智能体都基于前一个智能体的成果进行后续处理。该架构非常适合具有清晰有序步骤的流程，确保存在依赖关系的任务能够被正确处理。

```python
from swarms import Agent, SequentialWorkflow

# Agent 1: The Researcher
researcher = Agent(
    agent_name="Researcher",
    system_prompt="Your job is to research the provided topic and provide a detailed summary.",
    model_name="gpt-5.4",
)

# Agent 2: The Writer
writer = Agent(
    agent_name="Writer",
    system_prompt="Your job is to take the research summary and write a beautiful, engaging blog post about it.",
    model_name="gpt-5.4",
)

# Create a sequential workflow where the researcher's output feeds into the writer's input
workflow = SequentialWorkflow(agents=[researcher, writer])

# Run the workflow on a task
final_post = workflow.run("The history and future of artificial intelligence")
print(final_post)
```

-----


### ConcurrentWorkflow

`ConcurrentWorkflow` 同时运行多个智能体，允许任务并行执行。该架构大幅缩短了可并行处理任务的执行时间，使其成为高吞吐量场景的理想选择（即多个智能体并发处理相似任务）。

```python
from swarms import Agent, ConcurrentWorkflow

# Create agents for different analysis tasks
market_analyst = Agent(
    agent_name="Market-Analyst",
    system_prompt="Analyze market trends and provide insights on the given topic.",
    model_name="gpt-5.4",
    max_loops=1,
)

financial_analyst = Agent(
    agent_name="Financial-Analyst", 
    system_prompt="Provide financial analysis and recommendations on the given topic.",
    model_name="gpt-5.4",
    max_loops=1,
)

risk_analyst = Agent(
    agent_name="Risk-Analyst",
    system_prompt="Assess risks and provide risk management strategies for the given topic.",
    model_name="gpt-5.4", 
    max_loops=1,
)

# Create concurrent workflow
concurrent_workflow = ConcurrentWorkflow(
    agents=[market_analyst, financial_analyst, risk_analyst],
    max_loops=1,
)

# Run all agents concurrently on the same task
results = concurrent_workflow.run(
    "Analyze the potential impact of AI technology on the healthcare industry"
)

print(results)
```

---

### AgentRearrange

受 `einsum` 启发，`AgentRearrange` 允许你使用简单的字符串语法定义智能体之间复杂的非线性关系。[了解更多](https://docs.swarms.world/api/agent-rearrange)。该架构非常适合编排动态工作流，其中智能体可以按任意组合并行、顺序或混合执行任务。

```python
from swarms import Agent, AgentRearrange

# Define agents
researcher = Agent(agent_name="researcher", model_name="gpt-5.4")
writer = Agent(agent_name="writer", model_name="gpt-5.4")
editor = Agent(agent_name="editor", model_name="gpt-5.4")

# Define a flow: researcher sends work to both writer and editor simultaneously
# This is a one-to-many relationship
flow = "researcher -> writer, editor"

# Create the rearrangement system
rearrange_system = AgentRearrange(
    agents=[researcher, writer, editor],
    flow=flow,
)

# Run the swarm
outputs = rearrange_system.run("Analyze the impact of AI on modern cinema.")
print(outputs)
```


### GraphWorkflow

`GraphWorkflow` 将智能体作为有向无环图 (DAG) 中的节点进行编排。每个节点是一个智能体，每条边声明了依赖关系，因此一个节点只有在所有上游节点完成后才会执行。拓扑排序保证了正确的执行顺序，而独立分支会自动并行运行。 

当你的工作流包含扇出/扇入模式、条件依赖或任何不符合严格线性或扁平并行的结构时，`GraphWorkflow` 是最佳选择。[了解更多关于 GraphWorkflow](https://docs.swarms.world/api/graph-workflow)

```python
from swarms import Agent, GraphWorkflow, Node, Edge, NodeType

# Define agents
researcher = Agent(agent_name="Researcher", system_prompt="Research the given topic and produce key findings.", model_name="gpt-5.4")
writer     = Agent(agent_name="Writer",     system_prompt="Write a clear article from the research provided.", model_name="gpt-5.4")
reviewer   = Agent(agent_name="Reviewer",   system_prompt="Review the article for accuracy and clarity.",      model_name="gpt-5.4")
publisher  = Agent(agent_name="Publisher",  system_prompt="Format the final reviewed article for publication.", model_name="gpt-5.4")

# Build the graph: Researcher -> Writer -> Reviewer -> Publisher
workflow = GraphWorkflow()
workflow.add_node(Node(id="researcher", type=NodeType.AGENT, agent=researcher))
workflow.add_node(Node(id="writer",     type=NodeType.AGENT, agent=writer))
workflow.add_node(Node(id="reviewer",   type=NodeType.AGENT, agent=reviewer))
workflow.add_node(Node(id="publisher",  type=NodeType.AGENT, agent=publisher))

workflow.add_edge(Edge(source="researcher", target="writer"))
workflow.add_edge(Edge(source="writer",     target="reviewer"))
workflow.add_edge(Edge(source="reviewer",   target="publisher"))

workflow.set_entry_points(["researcher"])
workflow.set_end_points(["publisher"])

# Run the graph
results = workflow.run("Produce a short article on the rise of small language models.")
print(results)
```

`GraphWorkflow` 的优势在于：
- **复杂依赖关系**：支持表达任意 DAG，包括扇出、扇入和菱形模式
- **自动并行化**：独立分支无需额外配置即可并发执行
- **节点级可观测性**：通过回调钩子监听节点完成状态，实现流式输出与进度追踪

----

### SwarmRouter：通用蜂群编排器

`SwarmRouter` 通过提供单一接口来运行任意类型的蜂群系统，从而简化了复杂工作流的构建。你无需导入和管理不同的蜂群类，只需更改 `swarm_type` 参数即可动态选择所需类型。[阅读完整文档](https://docs.swarms.world/api/swarm-router)

这使得你的代码更加简洁灵活，便于轻松切换不同的多智能体策略。以下是一个完整的示例，展示了如何定义智能体并使用 `SwarmRouter` 以不同的协作策略执行相同任务。

```python
from swarms import Agent, SwarmRouter, SwarmType

# Define a few generic agents
writer = Agent(agent_name="Writer", system_prompt="You are a creative writer.", model_name="gpt-5.4")
editor = Agent(agent_name="Editor", system_prompt="You are an expert editor for stories.", model_name="gpt-5.4")
reviewer = Agent(agent_name="Reviewer", system_prompt="You are a final reviewer who gives a score.", model_name="gpt-5.4")

# The agents and task will be the same for all examples
agents = [writer, editor, reviewer]
task = "Write a short story about a robot who discovers music."

# --- Example 1: SequentialWorkflow ---
# Agents run one after another in a chain: Writer -> Editor -> Reviewer.
print("Running a Sequential Workflow...")
sequential_router = SwarmRouter(swarm_type=SwarmType.SequentialWorkflow, agents=agents)
sequential_output = sequential_router.run(task)
print(f"Final Sequential Output:\n{sequential_output}\n")

# --- Example 2: ConcurrentWorkflow ---
# All agents receive the same initial task and run at the same time.
print("Running a Concurrent Workflow...")
concurrent_router = SwarmRouter(swarm_type=SwarmType.ConcurrentWorkflow, agents=agents)
concurrent_outputs = concurrent_router.run(task)
# This returns a dictionary of each agent's output
for agent_name, output in concurrent_outputs.items():
    print(f"Output from {agent_name}:\n{output}\n")

# --- Example 3: MixtureOfAgents ---
# All agents run in parallel, and a special 'aggregator' agent synthesizes their outputs.
print("Running a Mixture of Agents Workflow...")
aggregator = Agent(
    agent_name="Aggregator",
    system_prompt="Combine the story, edits, and review into a final document.",
    model_name="gpt-5.4"
)
moa_router = SwarmRouter(
    swarm_type=SwarmType.MixtureOfAgents,
    agents=agents,
    aggregator_agent=aggregator, # MoA requires an aggregator
)
aggregated_output = moa_router.run(task)
print(f"Final Aggregated Output:\n{aggregated_output}\n")
```


`SwarmRouter` 是简化多智能体编排的强大工具。它提供了一种一致且灵活的方式来部署不同的协作策略，使你能够用更少的代码构建更复杂的应用程序。

-------

### AutoSwarmBuilder：自主智能体生成

`AutoSwarmBuilder` 会根据你的任务描述自动生成专业化的智能体及其工作流。只需描述你的需求，它就会创建一个完整的多智能体系统，包含详细的提示词和最优的智能体配置。[了解更多关于 AutoSwarmBuilder](https://docs.swarms.world/api/auto-swarm-builder)

```python
from swarms import AutoSwarmBuilder
import json

# Initialize the AutoSwarmBuilder
swarm = AutoSwarmBuilder(
    name="My Swarm",
    description="A swarm of agents",
    verbose=True,
    max_loops=1,
    return_agents=True,
    model_name="gpt-5.4",
)

# Let the builder automatically create agents and workflows
result = swarm.run(
    task="Create an accounting team to analyze crypto transactions, "
         "there must be 5 agents in the team with extremely extensive prompts. "
         "Make the prompts extremely detailed and specific and long and comprehensive. "
         "Make sure to include all the details of the task in the prompts."
)

# The result contains the generated agents and their configurations
print(json.dumps(result, indent=4))
```

`AutoSwarmBuilder` 提供：

- **自动智能体生成**：根据任务需求创建专业化智能体
- **智能提示词工程**：为每个智能体生成全面、详细的提示词
- **最优工作流设计**：确定最佳智能体交互模式与工作流结构
- **生产就绪配置**：返回完全配置好、可直接部署的智能体
- **灵活架构**：支持多种蜂群类型和智能体专业化方向

此功能非常适合快速原型开发、复杂任务分解以及无需手动配置即可创建专业智能体团队。

-------

### MixtureOfAgents (MoA)

`MixtureOfAgents` 架构通过将任务并行分发给多个“专家”智能体进行处理，随后由聚合器智能体综合其多样化输出，最终生成高质量结果。[在此了解更多](https://docs.swarms.world/examples/mixture-of-agents-example)

```python
from swarms import Agent, MixtureOfAgents

# Define expert agents
financial_analyst = Agent(agent_name="FinancialAnalyst", system_prompt="Analyze financial data.", model_name="gpt-5.4")
market_analyst = Agent(agent_name="MarketAnalyst", system_prompt="Analyze market trends.", model_name="gpt-5.4")
risk_analyst = Agent(agent_name="RiskAnalyst", system_prompt="Analyze investment risks.", model_name="gpt-5.4")

# Define the aggregator agent
aggregator = Agent(
    agent_name="InvestmentAdvisor",
    system_prompt="Synthesize the financial, market, and risk analyses to provide a final investment recommendation.",
    model_name="gpt-5.4"
)

# Create the MoA swarm
moa_swarm = MixtureOfAgents(
    agents=[financial_analyst, market_analyst, risk_analyst],
    aggregator_agent=aggregator,
)

# Run the swarm
recommendation = moa_swarm.run("Should we invest in NVIDIA stock right now?")
print(recommendation)
```

----

### GroupChat

`GroupChat` 创建一个对话环境，允许多个智能体进行交互、讨论并协作解决问题。你可以定义发言顺序或让其动态决定。该架构非常适合受益于辩论和多视角推理的任务，例如合同谈判、头脑风暴或复杂决策。

```python
from swarms import Agent, GroupChat

# Define agents for a debate
tech_optimist = Agent(agent_name="TechOptimist", system_prompt="Argue for the benefits of AI in society.", model_name="gpt-5.4")
tech_critic = Agent(agent_name="TechCritic", system_prompt="Argue against the unchecked advancement of AI.", model_name="gpt-5.4")

# Create the group chat
chat = GroupChat(
    agents=[tech_optimist, tech_critic],
    max_loops=4, # Limit the number of turns in the conversation
)

# Run the chat with an initial topic
conversation_history = chat.run(
    "Let's discuss the societal impact of artificial intelligence."
)

# Print the full conversation
for message in conversation_history:
    print(f"[{message['agent_name']}]: {message['content']}")
```

----

### HierarchicalSwarm

`HierarchicalSwarm` 实现了主管-执行者模式，其中中央主管智能体制定全面计划并将具体任务分发给专业化的执行智能体。主管会评估结果并在反馈循环中发布新指令，使其非常适合复杂的项目管理和团队协调场景。

```python
from swarms import Agent, HierarchicalSwarm

# Define specialized worker agents
content_strategist = Agent(
    agent_name="Content-Strategist",
    system_prompt="You are a senior content strategist. Develop comprehensive content strategies, editorial calendars, and content roadmaps.",
    model_name="gpt-5.4"
)

creative_director = Agent(
    agent_name="Creative-Director", 
    system_prompt="You are a creative director. Develop compelling advertising concepts, visual directions, and campaign creativity.",
    model_name="gpt-5.4"
)

seo_specialist = Agent(
    agent_name="SEO-Specialist",
    system_prompt="You are an SEO expert. Conduct keyword research, optimize content, and develop organic growth strategies.",
    model_name="gpt-5.4"
)

brand_strategist = Agent(
    agent_name="Brand-Strategist",
    system_prompt="You are a brand strategist. Develop brand positioning, identity systems, and market differentiation strategies.",
    model_name="gpt-5.4"
)

# Create the hierarchical swarm with a director
marketing_swarm = HierarchicalSwarm(
    name="Marketing-Team-Swarm",
    description="A comprehensive marketing team with specialized agents coordinated by a director",
    agents=[content_strategist, creative_director, seo_specialist, brand_strategist],
    max_loops=2,  # Allow for feedback and refinement
    verbose=True
)

# Run the swarm on a complex marketing challenge
result = marketing_swarm.run(
    "Develop a comprehensive marketing strategy for a new SaaS product launch. "
    "The product is a project management tool targeting small to medium businesses. "
    "Coordinate the team to create content strategy, creative campaigns, SEO optimization, "
    "and brand positioning that work together cohesively."
)

print(result)
```

`HierarchicalSwarm` 的优势在于：
- **复杂项目管理**：将大型任务拆解为专业化的子任务
- **团队协调**：确保所有智能体朝着统一目标努力
- **质量控制**：主管提供反馈与优化循环
- **可扩展工作流**：按需轻松添加新的专业化智能体

---

### HeavySwarm

`HeavySwarm` 实现了一种受 X.AI Grok 重型实现启发的复杂五阶段工作流。它使用专业化智能体（研究、分析、备选方案、验证）通过智能提问生成、并行执行和结果综合来提供全面的任务分析。该架构在处理需要深入调查和多视角分析的复杂研究与分析任务时表现出色。

```python
from swarms import HeavySwarm

# Pip install swarms-tools
from swarms_tools import exa_search

swarm = HeavySwarm(
    name="Gold ETF Research Team",
    description="A team of agents that research the best gold ETFs",
    worker_model_name="claude-sonnet-4-20250514",
    show_dashboard=True,
    question_agent_model_name="gpt-4.1",
    loops_per_agent=1,
    agent_prints_on=False,
    worker_tools=[exa_search],
    random_loops_per_agent=True,
)

prompt = (
    "Find the best 3 gold ETFs. For each ETF, provide the ticker symbol, "
    "full name, current price, expense ratio, assets under management, and "
    "a brief explanation of why it is considered among the best. Present the information "
    "in a clear, structured format suitable for investors. Scrape the data from the web. "
)

out = swarm.run(prompt)
print(out)

```

`HeavySwarm` 提供：

- **五阶段分析**：提问生成、研究、分析、备选方案与验证

- **专业化智能体**：每个阶段使用量身定制的智能体以获得最佳结果

- **全面覆盖**：多视角分析与深入调查

- **实时仪表盘**：可选的分析过程可视化展示

- **结构化输出**：组织清晰且可操作的结果

该架构非常适合金融分析、战略规划、研究报告以及任何需要深度多维度分析的任务。[了解更多关于 HeavySwarm](https://docs.swarms.world/api/heavy-swarm)

---

### 社交算法 (Social Algorithms)

**社交算法**提供了一个灵活的框架，用于定义智能体之间自定义的通信模式。你可以上传任意可调用函数作为社交算法来定义通信序列，使智能体能够以复杂的方式进行交互。[了解更多关于社交算法](https://docs.swarms.world/api/social-algorithms)

```python
from swarms import Agent, SocialAlgorithms

# Define a custom social algorithm
def research_analysis_synthesis_algorithm(agents, task, **kwargs):
    # Agent 1 researches the topic
    research_result = agents[0].run(f"Research: {task}")
    
    # Agent 2 analyzes the research
    analysis = agents[1].run(f"Analyze this research: {research_result}")
    
    # Agent 3 synthesizes the findings
    synthesis = agents[2].run(f"Synthesize: {research_result} + {analysis}")
    
    return {
        "research": research_result,
        "analysis": analysis,
        "synthesis": synthesis
    }

# Create agents
researcher = Agent(
  agent_name="Researcher",
  agent_description="Expert in comprehensive research and information gathering.",
  model_name="gpt-4.1"
)
analyst = Agent(
  agent_name="Analyst",
  agent_description="Specialist in analyzing and interpreting data.",
  model_name="gpt-4.1"
)
synthesizer = Agent(
  agent_name="Synthesizer",
  agent_description="Focused on synthesizing and integrating research insights.",
  model_name="gpt-4.1"
)

# Create social algorithm
social_alg = SocialAlgorithms(
    name="Research-Analysis-Synthesis",
    agents=[researcher, analyst, synthesizer],
    social_algorithm=research_analysis_synthesis_algorithm,
    verbose=True
)

# Run the algorithm
result = social_alg.run("The impact of AI on healthcare")
print(result.final_outputs)
```

非常适合实现复杂的多智能体工作流、协同问题解决以及自定义通信协议。

---

### 智能体编排协议 (AOP)

**智能体编排协议（Agent Orchestration Protocol, AOP）**是一个用于部署和管理分布式服务化智能体的强大框架。AOP 使智能体能够通过标准化协议被发现、管理和执行，非常适合构建可扩展的多智能体系统。[了解更多关于 AOP](https://docs.swarms.world/api/aop)

```python
from swarms import Agent, AOP

# Create specialized agents
research_agent = Agent(
    agent_name="Research-Agent",
    agent_description="Expert in research and data collection",
    model_name="anthropic/claude-sonnet-4-5",
    max_loops=1,
    tags=["research", "data-collection", "analysis"],
    capabilities=["web-search", "data-gathering", "report-generation"],
    role="researcher"
)

analysis_agent = Agent(
    agent_name="Analysis-Agent", 
    agent_description="Expert in data analysis and insights",
    model_name="anthropic/claude-sonnet-4-5",
    max_loops=1,
    tags=["analysis", "data-processing", "insights"],
    capabilities=["statistical-analysis", "pattern-recognition", "visualization"],
    role="analyst"
)

# Create AOP server
deployer = AOP(
    server_name="ResearchCluster",
    port=8000,
    verbose=True
)

# Add agents to the server
deployer.add_agent(
    agent=research_agent,
    tool_name="research_tool",
    tool_description="Research and data collection tool",
    timeout=30,
    max_retries=3
)

deployer.add_agent(
    agent=analysis_agent,
    tool_name="analysis_tool", 
    tool_description="Data analysis and insights tool",
    timeout=30,
    max_retries=3
)

# List all registered agents
print("Registered agents:", deployer.list_agents())

# Start the AOP server
deployer.run()
```

非常适合部署大规模多智能体系统。[阅读完整的 AOP 文档](https://docs.swarms.world/api/aop)

---

## 文档 (Documentation)

完整文档位于 **[docs.swarms.world](https://docs.swarms.world)**。以下是使用 Swarms 构建应用时（面向人类开发者和 AI 编程助手）最实用的资源：

| 资源 | 链接 | 用途 |
|---|---|---|
| **主文档** | [docs.swarms.world](https://docs.swarms.world) | 指南、API 参考、教程 |
| **`llms.txt`（LLM 可解析文档）** | [docs.swarms.world/llms.txt](https://docs.swarms.world/llms.txt) | 单一机器可读索引，专为 LLM 和 AI IDE（Cursor、Claude Code 等）优化，支持单次拉取完整文档 |
| **MCP 集成指南** | [docs.swarms.world/mcp](https://docs.swarms.world/mcp) | 如何将 Swarms `Agent` 连接到任意 [Model Context Protocol](https://modelcontextprotocol.io) 服务器，自动发现其工具并从蜂群中调用它们 |
| **API 参考** | [docs.swarms.world/api](https://docs.swarms.world/api) | `Agent`、`SequentialWorkflow`、`ConcurrentWorkflow`、`AgentRearrange`、`GraphWorkflow`、`SwarmRouter` 及所有多智能体架构的类级参考文档 |
| **环境配置** | [docs.swarms.world/environment-setup](https://docs.swarms.world/environment-setup) | API 密钥、模型提供商和配置选项 |

> **给 AI 编程助手的提示：** 将你的工具（Claude Code、Cursor、Windsurf、Continue 等）指向 `https://docs.swarms.world/llms.txt`。它将一次性拉取完整文档索引，并直接生成符合规范的 Swarms 代码，无需逐问查询。

---

## 配合 AI 编程助手使用 Swarms

仓库根目录提供了一个 [`CLAUDE.md`](./CLAUDE.md) —— 一份专注指南，教导 Claude Code、Cursor 及其他 AI 编程助手如何使用 Swarms 进行开发。它涵盖了 `Agent` 基础组件、所有多智能体架构（`SequentialWorkflow`、`ConcurrentWorkflow`、`AgentRearrange`、`GraphWorkflow`、`MixtureOfAgents`、`HierarchicalSwarm`、`SwarmRouter` 等）、工具、流式传输、记忆、MCP 集成以及各场景下的最佳实践模式。

将 `CLAUDE.md`（或将其软链接为 `AGENTS.md` / `.cursorrules`）放入任何依赖 `swarms` 的项目中，你的 AI 助手就能一次性写出符合规范的 Swarms 代码——无需额外提示。

---

## 特性 (Features)

Swarms 提供了一个全面的企业级多智能体基础设施平台，专为生产规模部署和与现有系统的无缝集成而设计。[在此了解更多 swarms 功能集](https://docs.swarms.world/community/features)

| 类别 | 特性 | 优势 |
|----------|----------|-----------|
| **企业架构** | • 生产就绪型基础设施<br>• 高可用系统<br>• 模块化微服务设计<br>• 全面可观测性<br>• 向后兼容性 | • 99.9%+ 可用性保障<br>• 降低运维开销<br>• 无缝遗留系统集成<br>• 增强系统监控能力<br>• 零风险迁移路径 |
| **多智能体编排** | • 分层智能体蜂群<br>• 并行处理管道<br>• 顺序工作流编排<br>• 基于图的网络架构<br>• 动态智能体组合<br>• 智能体注册表管理 | • 复杂业务流程自动化<br>• 可扩展任务分发<br>• 灵活的工作流适配<br>• 优化资源利用率<br>• 集中式智能体治理<br>• 企业级智能体生命周期管理 |
| **企业集成** | • 多模型提供商支持<br>• 自定义智能体开发框架<br>• 丰富的企业工具库<br>• 多种记忆系统<br>• 与 LangChain、AutoGen、CrewAI 向后兼容<br>• 标准化 API 接口 | • 厂商无关架构<br>• 定制解决方案开发<br>• 扩展功能集成<br>• 增强知识管理<br>• 无缝框架迁移<br>• 降低集成复杂度 |
| **企业级可扩展性** | • 并发多智能体处理<br>• 智能资源管理<br>• 负载均衡与自动扩缩容<br>• 水平扩展能力<br>• 性能优化<br>• 容量规划工具 | • 高吞吐量处理<br>• 成本效益型资源利用<br>• 按需弹性伸缩<br>• 线性性能扩展<br>• 优化的响应时间<br>• 可预测的增长规划 |
| **开发者体验** | • 直观的企业级 API<br>• 完善的文档体系<br>• 活跃的企业社区<br>• CLI & SDK 工具<br>• IDE 集成支持<br>• 代码生成模板 | • 加速开发周期<br>• 降低学习曲线<br>• 专家社区支持<br>• 快速部署能力<br>• 提升开发者生产力<br>• 标准化开发模式 |


## 支持的协议与集成

Swarms 无缝集成了行业标准协议和开放规范，解锁了强大的工具集成、支付处理、分布式智能体编排及模型互操作性功能。

| 协议 | 描述 | 文档 |
|----------|-------------|---------------|
| **[MCP (Model Context Protocol)](https://docs.swarms.world/integrations/mcp)** | AI 智能体通过 MCP 服务器与外部工具和服务交互的标准化协议。支持动态工具发现与执行。 | [MCP 集成指南](https://docs.swarms.world/integrations/mcp) |
| **[X402](https://docs.swarms.world/examples/integrations/x402-payment)** | API 端点的加密货币支付协议。支持按使用量付费的智能体货币化模型。 | [X402 快速入门](https://docs.swarms.world/examples/integrations/x402-payment) |
| **[AOP (Agent Orchestration Protocol)](https://docs.swarms.world/examples/multi-agent/aop-medical)** | 部署和管理分布式服务化智能体的框架。通过标准化协议实现智能体发现、管理与执行。 | [AOP 参考文档](https://docs.swarms.world/api/aop) |
| **[Swarms Marketplace](https://swarms.world)** | 发现和共享生产就绪型提示词、智能体和工具的平台。支持从市场自动加载提示词，并直接从代码发布你自己的提示词。 | [Marketplace 教程](https://docs.swarms.world/integrations/marketplace) |
| **[Open Responses](https://www.openresponses.org/)** | 基于 OpenAI Responses API 的开源规范与生态系统，提供多提供商、可互操作的 LLM 接口。提供统一的数据模型和工具链，用于调用语言模型、流式传输结果及编排智能体工作流（独立于具体提供商）。 | [Open Responses 官网](https://www.openresponses.org/) |
| **[Agent Skills](https://docs.swarms.world/agents/agent-skills)** | Anthropic 引入的轻量级 Markdown 格式，用于定义模块化、可复用的智能体能力。通过加载简单的 SKILL.md 文件即可实现智能体专业化，无需修改代码。 | [Agent Skills 文档](https://docs.swarms.world/agents/agent-skills) |


---

## 示例 (Examples)

探索全面的示例和教程，学习如何高效使用 Swarms。

| 类别 | 示例 | 描述 | 链接 |
|----------|---------|-------------|------|
| **基础示例** | Basic Agent | 简单智能体设置与使用 | [Basic Agent](https://docs.swarms.world/examples/basic-agent) |
| **基础示例** | Agent with Tools | 配合各种工具使用的智能体 | [Agent with Tools](https://docs.swarms.world/examples/agent-with-tools) |
| **基础示例** | Agent with Structured Outputs | 处理结构化数据输出 | [Structured Outputs](https://docs.swarms.world/agents/structured-outputs) |
| **基础示例** | Agent with MCP Integration | Model Context Protocol 集成 | [MCP Integration](https://docs.swarms.world/integrations/mcp) |
| **基础示例** | Vision Processing | 具备图像处理的智能体 | [Vision Processing](https://docs.swarms.world/examples/vision-agent) |
| **基础示例** | Multiple Images | 处理多张图片 | [Multiple Images](https://docs.swarms.world/examples/vision-agent) |
| **基础示例** | Vision and Tools | 结合视觉与工具使用 | [Vision and Tools](https://docs.swarms.world/examples/vision-agent) |
| **基础示例** | Agent Streaming | 实时智能体输出流式传输 | [Agent Streaming](https://docs.swarms.world/examples/agents/agent-streaming) |
| **基础示例** | Agent Output Types | 不同的输出格式与类型 | [Output Types](https://docs.swarms.world/agents/structured-outputs) |
| **基础示例** | Gradio Chat Interface | 构建交互式聊天界面 | [Gradio UI](https://docs.swarms.world/examples/basic-agent) |
| **模型提供商** | Model Providers Overview | 支持模型的完整指南 | [Model Providers](https://docs.swarms.world/integrations/model-providers) |
| **模型提供商** | OpenAI | OpenAI 模型集成 | [OpenAI Examples](https://docs.swarms.world/integrations/model-providers) |
| **模型提供商** | Anthropic | Claude 模型集成 | [Anthropic Examples](https://docs.swarms.world/integrations/model-providers) |
| **模型提供商** | Groq | Groq 模型集成 | [Groq Examples](https://docs.swarms.world/integrations/model-providers) |
| **模型提供商** | Cohere | Cohere 模型集成 | [Cohere Examples](https://docs.swarms.world/integrations/model-providers) |
| **模型提供商** | DeepSeek | DeepSeek 模型集成 | [DeepSeek Examples](https://docs.swarms.world/integrations/model-providers) |
| **模型提供商** | Ollama | 本地 Ollama 模型集成 | [Ollama Examples](https://docs.swarms.world/integrations/model-providers) |
| **模型提供商** | OpenRouter | OpenRouter 模型集成 | [OpenRouter Examples](https://docs.swarms.world/integrations/model-providers) |
| **模型提供商** | XAI | XAI 模型集成 | [XAI Examples](https://docs.swarms.world/integrations/model-providers) |
| **模型提供商** | Llama4 | Llama4 模型集成 | [Llama4 Examples](https://docs.swarms.world/integrations/model-providers) |
| **多智能体架构** | HierarchicalSwarm | 分层智能体编排 | [HierarchicalSwarm Examples](https://docs.swarms.world/examples/hierarchical-swarm-example) |
| **多智能体架构** | Hybrid Hierarchical-Cluster Swarm | 高级分层模式 | [HHCS Examples](https://docs.swarms.world/api/hhcs) |
| **多智能体架构** | GroupChat | 多智能体对话 | [GroupChat Examples](https://docs.swarms.world/examples/group-chat-example) |
| **多智能体架构** | Sequential Workflow | 逐步执行的工作流 | [Sequential Examples](https://docs.swarms.world/examples/sequential-workflow-example) |
| **多智能体架构** | SwarmRouter | 通用蜂群编排器 | [SwarmRouter Examples](https://docs.swarms.world/architectures/swarm-router) |
| **多智能体架构** | MultiAgentRouter | 最小化路由器示例 | [MultiAgentRouter Examples](https://docs.swarms.world/api/multi-agent-router) |
| **多智能体架构** | ConcurrentWorkflow | 并行执行智能体 | [Concurrent Examples](https://docs.swarms.world/examples/concurrent-workflow-example) |
| **多智能体架构** | Mixture of Agents | 专家智能体协作 | [MoA Examples](https://docs.swarms.world/examples/mixture-of-agents-example) |
| **多智能体架构** | Unique Swarms | 专用蜂群模式 | [Unique Swarms](https://docs.swarms.world/architectures/overview) |
| **多智能体架构** | Agents as Tools | 在流程中将智能体作为工具使用 | [Agents as Tools](https://docs.swarms.world/architectures/overview) |
| **多智能体架构** | Aggregate Responses | 综合多个智能体输出 | [Aggregate Examples](https://docs.swarms.world/architectures/mixture-of-agents) |
| **多智能体架构** | Interactive GroupChat | 实时智能体交互 | [Interactive GroupChat](https://docs.swarms.world/examples/group-chat-example) |
| **部署方案** | Agent Orchestration Protocol (AOP) | 以分布式服务形式部署智能体，支持发现与管理 | [AOP Reference](https://docs.swarms.world/api/aop) |
| **应用场景** | Advanced Research System | 受 Anthropic 研究方法启发的多智能体研究系统 | [AdvancedResearch](https://github.com/The-Swarm-Corporation/AdvancedResearch) |
| **应用场景** | Hospital Simulation | 使用多智能体架构的医疗模拟系统 | [HospitalSim](https://github.com/The-Swarm-Corporation/HospitalSim) |
| **应用场景** | Browser Agents | 基于智能体的网页自动化 | [Browser Agents](https://docs.swarms.world/examples/integrations/browser-use) |
| **应用场景** | Medical Analysis | 医疗领域应用 | [Medical Examples](https://docs.swarms.world/examples/multi-agent/aop-medical) |
| **应用场景** | Finance Analysis | 金融领域应用 | [Finance Examples](https://docs.swarms.world/examples/use-cases/financial-analysis) |
| **示例与模板** | Examples Overview | 完整示例目录索引 | [Examples Index](https://docs.swarms.world/examples/) |
| **示例与模板** | Cookbook Index | 精选示例合集 | [Cookbook](https://docs.swarms.world/examples/overviews/cookbook) |
| **示例与模板** | Paper Implementations | 学术论文实现 | [Paper Implementations](https://docs.swarms.world/examples/overviews/paper-implementations) |
| **示例与模板** | Templates & Applications | 可复用模板 | [Templates](https://docs.swarms.world/examples/overviews/templates) |

---

## 贡献 (Contribute to Swarms)

Swarms 是一个开源、社区驱动的项目，旨在通过提供用于部署和编排数百万智能体的强大基础设施，加速迈向完全自主的世界。通过参与贡献，你可以推动多智能体 AI 的发展，与志同道合的开发者协作，塑造智能体经济，并提升自身技术实力。 

了解更多如何产生有意义影响的详情，请查看我们的 [贡献者指南](https://docs.swarms.world/community/contributing)。

### 如何贡献

我们简化了参与流程。以下是你可以提供帮助的方式：

1. **寻找可处理的问题：** 最好的起点是访问我们的 [**贡献项目看板**](https://github.com/users/kyegomez/projects/1)。查找标记为 `good first issue` 的问题——这些是为新贡献者专门筛选的入门级任务。

2. **报告 Bug 或请求功能：** 有新想法或发现某些功能不符合预期？我们非常欢迎你的反馈。请在我们的 GitHub Issues 页面 [**提交 Bug 报告或功能请求**](https://github.com/kyegomez/swarms/issues)。

3. **了解我们的工作流与规范：** 在提交代码前，请查阅完整的 [**贡献指南**](https://github.com/kyegomez/swarms/blob/master/CONTRIBUTING.md)。为保持代码质量，我们也鼓励你阅读我们的 [**代码整洁度指南**](https://docs.swarms.world/community/contributing-to-docs)。

4. **参与讨论：** 要参与路线图讨论并与其它开发者建立联系，请加入我们在 [**Discord**](https://discord.gg/EamjgSaEQf) 的社区。

### 感谢我们的贡献者

感谢你为 swarms 做出的贡献。你的工作备受认可与赞赏。

<a href="https://github.com/kyegomez/swarms/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=kyegomez/swarms" />
</a>


## 加入 Discord

加入数千名智能体构建者和 AI 工程师所在的 **[Swarms Discord](https://discord.gg/EamjgSaEQf)**，获取技术支持、项目展示、协作机会以及最新的 swarms 生态更新。

[加入 Swarms Discord →](https://discord.gg/EamjgSaEQf)

-----

## 加入 Swarms 社区！

加入我们的智能体工程师与研究人员社区，获取技术支持、前沿动态及独家世界级智能体工程洞察！

| 平台 | 描述 | 链接 |
|----------|-------------|------|
| Documentation | 官方文档与指南 | [docs.swarms.world](https://docs.swarms.world) |
| Blog | 最新动态与技术文章 | [Medium](https://medium.com/@kyeg) |
| Discord | 实时聊天与社区支持 | [Join Discord](https://discord.gg/EamjgSaEQf) |
| Twitter | 最新资讯与公告 | [@swarms_corp](https://twitter.com/swarms_corp) |
| LinkedIn | 专业网络与更新 | [The Swarm Corporation](https://www.linkedin.com/company/the-swarm-corporation) |
| YouTube | 教程与演示 | [Swarms Channel](https://www.youtube.com/channel/UC9yXyitkbU_WSy7bd_41SqQ) |
| Events | 参与我们的社区活动 | [在此报名](https://lu.ma/swarms_calendar) |
| Onboarding Session | 与 Swarms 创建者兼首席维护者 Kye Gomez 一起完成入职引导 | [预约会议](https://cal.com/swarms/swarms-onboarding-session) |

------

## 引用 (Citation)

如果你在研究中使用了 **swarms**，请通过引用 [CITATION.cff](./CITATION.cff) 中的元数据来标注该项目。

```bibtex
@misc{SWARMS_2022,
  author  = {Kye Gomez and Pliny and Zack Bradshaw and Ilumn and Harshal and the Swarms Community},
  title   = {{Swarms: Production-Grade Multi-Agent Infrastructure Platform}},
  year    = {2022},
  howpublished = {\url{https://github.com/kyegomez/swarms}},
  note    = {Documentation available at \url{https://docs.swarms.world}},
  version = {latest}
```

---

# 许可证 (License)

Swarms 采用 Apache License 2.0 开源协议。[在此了解更多](./LICENSE)
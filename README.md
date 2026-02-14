# Building Agents in Azure AI Foundry

Build an AI agent. Give it tools. Deploy it to the cloud.

> Start with the **single-agent pattern** — one agent orchestrating multiple tools. Master this foundation, then level up to multi-agent systems and MCP.

**Jump to:** [The Big Picture](#the-big-picture) · [Assignments](#assignments) · [Labs](#labs-divide-and-conquer) · [Getting Started](#getting-started) · [Resources](#resources)


## The Big Picture 

### *Single Agent vs Multi-Agent*

A **single agent** is one AI entity that reasons, decides, and acts. It's the right choice when:
- The task can be handled by one "brain" with the right tools
- You want atomic, predictable decisions
- Complexity is manageable without delegation

When tasks require specialization, parallel work, or debate between perspectives — that's when you graduate to **multi-agent systems**. But start simple. Most problems don't need an orchestra; they need one good musician with the right instruments.

### *Tool Calling*

When you create an agent in **Azure AI Foundry**, you get a powerful AI runtime in the cloud. But agents become truly useful when they can take **actions** — calling APIs, processing data, sending notifications, etc.

To add actions, we register **tools**. Tools can be:
- **In-process functions** (code that runs inside the agent)
- **External services** like **Azure Functions** or **Logic Apps** (decoupled, cloud-based)

These labs focus on the decoupled approach: your agent lives in AI Foundry, and your tools live independently in Azure — clean, scalable, and production-ready. See the [Labs](#labs-divide-and-conquer) below.

### *MCP: Model Context Protocol*

**MCP** is an open standard for connecting AI agents to tools via a client-server architecture. Instead of hardcoding tool integrations:

- **MCP Server** = exposes tools (your functions, APIs, databases)
- **MCP Client** = the agent that discovers and calls those tools

Why it matters:
- **Reusability** — Build a tool once, use it across many agents
- **Security** — Centralized auth, audit, and access control
- **Discovery** — Agents can find and learn new tools dynamically

In Labs 4-5, you'll build an MCP server with Azure Functions and connect it to an AI agent using Microsoft's Agent Framework.

## Assignments

See the full assignment details: **[Assignments](docs/asigments.md)**

| Week | Topic | Lab |
|------|-------|-----|
| Week 3 | Single Agent + External Tools | Labs 1-5 |
| Week 4 | Multi-Agent Orchestration | Lab 6 |
| Week 5 | Operationalization | Labs 7-9 |

## Labs (Divide and Conquer)

Build step by step — don't try to do everything at once:

### Part 1: HTTP Tool Pattern (Labs 1-3)
Connect agents to tools via direct HTTP calls.

| Lab | What You'll Build |
|-----|-------------------|
| [Lab 1: Azure Functions](notebooks/lab1_azure_functions.ipynb) | Create and deploy an Azure Function as an HTTP tool |
| [Lab 2: Logic Apps](notebooks/lab2_logic_apps.ipynb) | Create a Logic App as an HTTP tool (no code) |
| [Lab 3: Single Agent + HTTP Tools](notebooks/lab3_single_agent_tool_calling.ipynb) | Build an agent and connect it to your HTTP tools |

### Part 2: MCP Pattern (Labs 4-5)
Connect agents to tools via the Model Context Protocol.

| Lab | What You'll Build |
|-----|-------------------|
| [Lab 4: MCP Server](notebooks/lab4_mcp_server_azure_functions.ipynb) | Build an MCP server using Azure Functions |
| [Lab 5: Agent + MCP](notebooks/lab5_single_agent_mcp_integration.ipynb) | Connect an agent to MCP servers (local & remote) |

### Part 3: Multi-Agent Systems (Lab 6)
Coordinate multiple agents to solve complex problems.

| Lab | What You'll Build |
|-----|-------------------|
| [Lab 6: Multi-Agent Orchestration](notebooks/lab6_multi_agent_orchestration.ipynb) | Implement 5 orchestration patterns (Concurrent, Sequential, Group Chat, Magentic, Handoff) |

### Part 4: Operationalization (Labs 7-9)
Add safety, evaluation, and observability for production deployment.

| Lab | What You'll Build |
|-----|-------------------|
| [Lab 7: Guardrails](notebooks/lab7_agent_guardrails.ipynb) | Defense-in-depth safety controls and content filtering |
| [Lab 8: Evaluations](notebooks/lab8_safety_evaluations.ipynb) | Quality metrics, custom evaluators, and red teaming |
| [Lab 9: Observability](notebooks/lab9_tracing_observability.ipynb) | OpenTelemetry tracing and Azure Monitor integration |

**Path:**
```
┌─────────────────────────────────────┐     ┌─────────────────────────────────┐
│  Part 1: HTTP Tools (Week 3)        │     │  Part 2: MCP (Week 3)           │
│                                     │     │                                 │
│  Lab 1 (Azure Function) ──┐         │     │  Lab 4 (MCP Server)             │
│                           ├─▶ Lab 3 │     │         │                       │
│  Lab 2 (Logic App) ───────┘         │     │         ▼                       │
│                                     │     │  Lab 5 (Agent + MCP)            │
└─────────────────────────────────────┘     └─────────────────────────────────┘
                      │                                   │
                      └───────────────┬───────────────────┘
                                      ▼
                    ┌─────────────────────────────────────┐
                    │  Part 3: Multi-Agent (Week 4)       │
                    │                                     │
                    │  Lab 6 (Multi-Agent Orchestration)  │
                    │  • Concurrent, Sequential           │
                    │  • Group Chat, Magentic, Handoff    │
                    └──────────────────┬──────────────────┘
                                       │
                                       ▼
                    ┌─────────────────────────────────────┐
                    │  Part 4: Operationalization (Week 5)│
                    │                                     │
                    │  Lab 7 (Guardrails)                 │
                    │  Lab 8 (Evaluations & Red Teaming)  │
                    │  Lab 9 (Tracing & Observability)    │
                    └─────────────────────────────────────┘
```

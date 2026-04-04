# Claude Code 10x — Series Overview

## Vision

What does a dev need to know to demystify agentic programming with Claude Code?

That's the question driving this entire project. Not "how to install Claude Code" or "10 prompts that will blow your mind." The goal is deeper: build the mental models that let someone understand what's actually happening when an AI agent writes code, why it works, why it sometimes doesn't, and how to get consistently good results.

A dev who finishes all three series will go from "I've heard of this but don't know where to start" to "I understand the technology, I can build real projects with it, and I can extend the system to fit my needs." That's the full arc: understand → build → extend.

The series is opinionated. We think agentic programming is a paradigm shift on par with the move from assembly to high-level languages. But we also think most of the content out there is either hype ("AI will replace all devs") or surface-level tutorials that don't explain what's happening under the hood. We're going for the middle ground: technically honest, practically useful, and accessible to anyone who writes code for a living.

## Audience

Software devs with 2+ years of experience. Comfortable writing code in at least one language. May work on mobile, web, backend, infra — the concepts apply regardless of stack.

What they probably know: how to use an IDE, Git, CI/CD, basic terminal. May have used ChatGPT to ask questions or GitHub Copilot for autocomplete. Have heard "AI is changing everything" but don't really know what "agentic" means or how these tools work internally.

What they probably don't know: what a token is, what a context window is, how LLMs actually generate text, what MCP is, what "harness engineering" means, how to configure Claude Code beyond the defaults, how to structure a project for agentic development.

May be skeptical. May have tried an AI tool and been disappointed. May fear being replaced. The series meets them where they are, acknowledges the valid concerns, and builds from there.

## Pedagogical approach

### The knowledge staircase

Borrowed from the KMP-101 series that inspired this project. Each article builds on the previous one. You can't understand harness engineering (article 8) without understanding context (article 4), which requires understanding how models work (article 2). The order is intentional.

Within each article, the structure also follows a staircase: start with what the reader already knows, introduce one new concept at a time, ground it with an analogy or data point, and build toward the next step.

### The factory analogy

The central metaphor that threads through the entire 101 series and beyond. Software development is a factory. In traditional dev, you operate the machines by hand. As AI tools evolve, the factory upgrades: first a conveyor belt (autocomplete), then a consultant (chat), then smarter machines (multi-file editing), then autonomous machines (agentic coding). The paradigm shift is going from operating the factory to designing it.

This analogy isn't just decorative. It creates a persistent mental model that readers can reference as concepts get more complex. "Context is the fuel tank" is easier to remember than a technical definition.

### The three pillars framework

Introduced in 101 Part 1, these three pillars organize the practical knowledge:

1. **Prompt engineering** — how you communicate with the agent
2. **Context engineering** — what information the agent has access to
3. **Harness engineering** — how the surrounding system is configured

Each pillar gets a dedicated article in 101 (parts 6, 7, 8) and is practiced extensively in 102.

## How the series connect

| Series | Question it answers | Outcome | Prerequisite |
|--------|-------------------|---------|--------------|
| **101 — Foundations** | "What is agentic programming, and what do I need to understand to use it professionally?" | Understands the paradigm, the technology, and the three pillars | None |
| **102 — Applied** | "How do I build real projects with Claude Code?" | Can configure projects, use patterns, measure results | 101 recommended |
| **103 — Advanced** | "How do I extend and push the boundaries?" | Can build MCP servers, orchestrate multi-agent systems, create custom tools | 101 + 102 recommended |

Each series can be read independently, but the knowledge staircase works best in order. 102 references concepts from 101 without re-explaining them. 103 assumes familiarity with both.

## The factory analogy — master progression

| Stage | Concept | Factory image | Series |
|-------|---------|--------------|--------|
| Manual labor | Traditional development | Assembling products by hand, one at a time | 101.1 |
| Conveyor belt | Autocomplete (2021-2022) | Moves pieces faster, but you still assemble | 101.1 |
| Consultant | Chat-based AI (2022-2023) | Brilliant advisor who can't touch the machines | 101.1 |
| Control panels | Multi-file editing (2024) | Sophisticated machines, but you operate each panel | 101.1 |
| Autonomous machines | Agentic coding (2024+) | Machines that operate themselves, you supervise | 101.1 |
| The engine | Language models (LLMs) | The motor that powers the machines | 101.2 |
| The control panel | Claude Code architecture | How the machine is wired internally | 101.3 |
| The fuel tank | Context window | Limited, precious resource that powers everything | 101.4 |
| First startup | Setting up Claude Code | Turning on the machine for the first time | 101.5 |
| Control language | Prompt engineering | Instructions you give to the machine operator | 101.6 |
| Technical docs | Context engineering | Manuals and specs you provide to the team | 101.7 |
| Factory infrastructure | Harness engineering | Conveyor belts, sensors, safety systems | 101.8 |
| Building a factory | Project setup | Configuring a new production line from scratch | 102.1 |
| Automation systems | Hooks and agents | Automated quality checks and delegation | 102.2 |
| Blueprints | Spec Driven Development | Detailed plans before production starts | 102.3 |
| Production patterns | Development patterns | Proven approaches for different product types | 102.4 |
| Retrofitting | Existing projects | Upgrading an old factory with new machines | 102.5 |
| Quality control | Metrics and costs | Measuring output, managing costs, maintaining standards | 102.6 |
| Custom machines | MCP Servers | Building machines for specific operations | 103.1 |
| Factory network | Multi-agent orchestration | Coordinating multiple factories | 103.2 |
| Machine shop | Custom tools | Building tools that build tools | 103.3 |
| The next factory | Future of agentic programming | What's coming next | 103.4 |

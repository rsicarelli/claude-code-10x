# Claude Code 103 — Advanced Agentic

## Series premise

103 answers one question: "How do I extend and push the boundaries of agentic programming?"

After finishing these 4 articles, a dev will be able to build custom MCP servers to connect agents to any external service, orchestrate multi-agent systems for complex workflows, create domain-specific tools that extend the agent's capabilities, and think critically about where this technology is heading.

Prerequisite: 101 + 102 recommended. 103 assumes fluency with Claude Code configuration, the three pillars, and development patterns from the previous series.

---

## Article 1: MCP Servers — Extending the Agent's Capabilities

### What

Deep dive into Model Context Protocol (MCP). What MCP servers are and how they work architecturally. Building a custom MCP server from scratch (step-by-step). Connecting Claude Code to external APIs, databases, and services. The MCP ecosystem: existing servers, community packages. Security considerations when exposing external services to an agent.

### Why

MCP is what transforms Claude Code from a code-editing tool into a platform that can interact with anything. After mastering the basics (101) and building projects (102), the natural next step is extending what the agent can do. Most devs don't realize they can connect Claude Code to Jira, Slack, databases, internal APIs — MCP makes this possible.

### How

Build a real MCP server during the article — something practical like a database connector or an internal API bridge. Show the full lifecycle: design, implement, configure in `.mcp.json`, test with Claude Code. The factory analogy: "custom machines — building machines designed for specific operations that off-the-shelf machines can't handle."

---

## Article 2: Multi-agent Orchestration

### What

Coordinating multiple agents for complex workflows. CI/CD integration with Claude Code (GitHub Actions, automated PR review). Asynchronous agent execution. Agent teams: how to decompose a large task into sub-tasks handled by different agents. Cron scheduling for recurring agent tasks. Real-world orchestration patterns from production systems.

### Why

Single-agent usage hits a ceiling for complex projects. Multi-agent orchestration is where agentic programming scales. This is also where the gap between "using AI tools" and "building AI systems" becomes clearest. Devs who master orchestration can automate entire workflows that currently require human coordination.

### How

Show a real multi-agent workflow: a GitHub Action that triggers Claude Code to review PRs, a cron job that audits documentation weekly, a system where specialized agents handle different layers of a feature (data, UI, tests). The factory analogy: "a network of factories — coordinating production across multiple sites, each specialized in different operations."

---

## Article 3: Custom Tools — Building Domain-Specific Capabilities

### What

Creating custom tools that extend Claude Code's built-in toolset. When to build a tool vs when to use Bash. Tool design philosophy: simplicity, composability, safety. Building tools for domain-specific needs (e.g., database migration helpers, API testing tools, deployment scripts). Packaging and sharing tools across projects.

### Why

The built-in tools (Read, Write, Bash, etc.) cover 90% of use cases. The remaining 10% is where custom tools shine — and it's often the 10% that's most specific to your project or domain. This article teaches devs to think about tools as first-class abstractions, not just Bash scripts.

### How

Build 2-3 custom tools during the article, progressing from simple (a project-specific linter) to complex (a domain-specific code generator). Show how tools compose with the agentic loop. The factory analogy: "a machine shop — building tools that build other things. The meta-level of manufacturing."

---

## Article 4: The Future of Agentic Programming

### What

Emerging trends: computer use (agents controlling GUIs), web agents, fully autonomous coding pipelines. The evolving role of the developer — from engineer to architect to director. Ethical considerations: code ownership, accountability, security responsibility. The skills that will matter in 2-3 years. What's likely overhyped vs what's genuinely transformative.

### Why

The series closer for the entire project. After 18 articles across 3 series, the reader has gone from "what is agentic?" to building and extending agentic systems. This final article zooms out and looks forward: where is this going, what should devs invest in learning, and what should they be cautious about?

### How

This is the most opinion-heavy article in the series. Take positions. Make predictions. Be honest about uncertainty. Reference the data from throughout the series (adoption trends, quality metrics, cost trajectories) and extrapolate thoughtfully. The factory analogy comes full circle: "the next factory — what will the factory of 2027 look like? Who will work there, and what will they do?" End the series with something memorable and forward-looking, not a recap.

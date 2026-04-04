# Claude Code 102 — Applied Agentic Development

## Series premise

102 answers one question: "How do I build real projects with Claude Code?"

After finishing these 6 articles, a dev will be able to set up a Claude Code project from scratch with proper configuration, use hooks and sub-agents for automation, follow the Spec Driven Development methodology, apply proven development patterns, onboard Claude Code to existing codebases, and measure the effectiveness and cost of their agentic workflow.

Prerequisite: 101 is recommended. 102 references concepts like context window, harness, prompt engineering, and the three pillars without re-explaining them.

---

## Article 1: Building a Claude Code Project

### What

Setting up a real project for agentic development from zero. Writing an effective CLAUDE.md. Creating custom skills (slash commands). Defining project rules with glob patterns. Configuring settings.json. The anatomy of a well-configured agentic project — what goes where and why.

### Why

This is the bridge from "I understand the theory" (101) to "I'm building something real." The first thing anyone does after learning the foundations is try to set up their own project. This article ensures they do it right from the start, rather than discovering configuration patterns through trial and error.

### How

Hands-on, step-by-step. Start with an empty repository, end with a fully configured project. Show the thought process behind each configuration decision: "Why this rule? Why this skill? Why this permission?" Use a realistic project (not a toy example) so the patterns feel applicable. Reference the factory analogy: "this is building a new production line from scratch."

---

## Article 2: Hooks, Agents, and Sub-agents in Practice

### What

Deep dive into hooks (pre-tool, post-tool). Creating custom automation flows (e.g., block unsafe commands, enforce conventions). The concept of sub-agents and delegation — when and how to spawn specialized agents for specific tasks. Multi-agent workflows: parallel execution, sequential orchestration. Real-world patterns for agent teams.

### Why

After setting up a project (article 1), the next level is automation. Hooks and sub-agents are what turn a "Claude Code project" into an "agentic system." This is where the harness engineering pillar from 101.8 becomes deeply practical. Most devs don't know these capabilities exist, let alone how to use them effectively.

### How

Show real hook configurations with real effects (command blocking like the rocky project, convention enforcement). Show agent definitions with clear role separation. Demonstrate dispatching sub-agents in parallel for independent tasks. The factory analogy: "automation systems — quality checks that run without human intervention, and delegation to specialized workers."

---

## Article 3: Spec Driven Development

### What

SDD as the primary methodology for agentic development. Writing specs before code. Using plan mode to refine specs collaboratively with the agent. The spec → implementation → validation cycle. How SDD leverages the agent's strengths (fast execution) while mitigating weaknesses (needs clear direction). Comparison with TDD and BDD.

### Why

Tools and configuration are necessary but not sufficient. Devs also need a methodology — a way of working that consistently produces good results. SDD is the natural methodology for agentic development because it front-loads the human's strength (defining intent clearly) and delegates the agent's strength (executing at speed). Without a methodology, devs fall into "vibe coding."

### How

Walk through a complete SDD cycle on a realistic feature: write the spec, refine with the agent in plan mode, implement, validate against the spec. Show what happens when you skip the spec (poor results) vs when you invest in it (excellent results). The factory analogy: "blueprints — detailed plans before production starts."

---

## Article 4: Agentic Development Patterns

### What

Collected patterns from the community and from practice. Skeleton-first development (agent creates structure, human refines). Test-driven agentic (write tests first, agent implements until they pass). Documentation-first (write docs before code, agent implements to match). Review-then-implement (human plans, agent executes, human reviews). Anti-patterns to avoid. When to let the agent lead vs when to take control.

### Why

After learning the methodology (SDD, article 3), devs need a broader toolkit of approaches. Not every task is a greenfield feature that fits SDD perfectly. Bug fixes, refactoring, code review, documentation — each has patterns that work better than others with agentic tools. This article is the "pattern catalog" that devs will reference repeatedly.

### How

Pattern-by-pattern, each with: when to use it, step-by-step process, real example, common pitfalls. Include anti-patterns with the same structure but focused on "why this fails." The factory analogy: "production patterns — proven approaches for different product types. You don't manufacture electronics the same way you manufacture furniture."

---

## Article 5: Working with Existing Projects

### What

Onboarding Claude Code to a codebase that already exists. Progressive adoption strategy (start small, expand). How to teach the agent your project's conventions. Exploring and understanding legacy code with agentic tools. Refactoring with agents. Strategies for large codebases that don't fit in the context window.

### Why

Most devs aren't starting from scratch. They have existing projects with years of accumulated code, conventions, and technical debt. This article addresses the most common real-world scenario: "I have a codebase, how do I use Claude Code with it?" It's the article that will drive the most practical adoption.

### How

Start with a real (or realistic) existing project. Show the progressive approach: first explore the codebase with Claude Code (read-only), then create CLAUDE.md based on what you discover, then start with small tasks, then expand. Show context management strategies for large codebases. The factory analogy: "retrofitting — upgrading an old factory with new machines. You don't tear down and rebuild, you upgrade one section at a time."

---

## Article 6: Quality, Costs, and Metrics

### What

Measuring the effectiveness of agentic programming. Token cost analysis and optimization strategies. Quality gates and review processes — how to review AI-generated code effectively. When agentic programming helps vs when it hurts. Building a sustainable workflow that balances speed, quality, and cost. The honest numbers: what productivity gains are realistic?

### Why

The series closer. After learning to build and work with agentic tools (articles 1-5), devs need to answer the business question: "Is this actually worth it?" This article provides the framework for measuring and optimizing, including the uncomfortable truths (the METR study, security vulnerabilities, cost unpredictability). It also wraps up 102 and bridges to 103.

### How

Data-driven. Reference the research from 101.1 (market data, adoption stats, critical studies) but go deeper into per-project metrics. Show how to track token usage, estimate monthly costs, measure code quality. Include a realistic cost model. The factory analogy: "quality control and cost management — measuring output, managing costs, maintaining standards." End with a strong teaser for 103: "You now know how to build and run the factory. In the next series, we build custom machines."

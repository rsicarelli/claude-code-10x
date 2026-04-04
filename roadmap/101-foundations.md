# Claude Code 101 — Foundations of Agentic Programming

## Series premise

101 answers one question: "What is agentic programming, and what do I need to understand to use it professionally?"

After finishing these 8 articles, a dev will understand the paradigm (where it came from, what makes it different), the underlying technology (how LLMs work, what tokens and context windows are), the primary tool (Claude Code's internal architecture), and the three pillars of agentic engineering (prompt, context, harness). They won't have built a project yet — that's 102 — but they'll have the mental models to understand everything that follows.

No prerequisites beyond basic software development experience. The series starts from zero and assumes nothing about AI/ML knowledge.

---

## Article 1: Introduction to Agentic Programming

**Status:** Draft complete (PT-BR)

### What

The paradigm overview. Traces the evolution from traditional development through autocomplete, chat, multi-file editing, to agentic coding. Maps the current tool landscape (Claude Code, Cursor, Copilot, Aider, OpenCode, Codex CLI). Introduces the factory analogy and previews the three pillars (prompt engineering, context engineering, harness engineering). Presents both the optimistic data ($7.37B market, 84% dev adoption) and the honest caveats (METR study, security vulnerabilities, Gartner predictions).

### Why

This has to come first because everything else depends on understanding what "agentic" means and why it's different from what came before. Without this foundation, articles about context windows or harness engineering float without anchor. It also sets the tone for the entire series: technically honest, not hype, not fear.

### How

Parallels KMP-101 Part 1 (paradigm introduction with comparative framework). The factory analogy is introduced here and must appear in every section, progressing from manual labor through each upgrade. Research source: `research/01-panorama-programacao-agentica.md`. Key rhetorical move: acknowledge the reader's skepticism ("then a colleague types a paragraph in a terminal...") before building the case.

---

## Article 2: Demystifying Language Models

### What

What a token is, how words become numbers (BPE tokenization), what a context window is and why it matters, how next-token prediction works, temperature/top-p parameters, model families (Claude, GPT, Gemini, DeepSeek, Llama), the difference between reasoning/fast/coding models, what models can't do (hallucinations, confidence without accuracy), and how pricing works (input/output tokens).

### Why

Before touching Claude Code or any agentic tool, devs need to understand the raw material: the language model. Most people use LLMs without understanding that they're essentially next-token predictors with a fixed memory window. This understanding changes how you interact with every tool built on top of them. It explains why context management matters, why prompts need structure, and why the AI sometimes confidently says something wrong.

### How

Factory analogy: "the engine of the machines." This article opens the hood and explains the motor. Parallel to KMP-101 Part 2 (how Kotlin compiles to multiple platforms — understanding the underlying technology). Heavy on visualizations: token breakdown diagrams, context window pie charts, model comparison tables. Research needed: `prompts/03-fundamentos-llms-para-devs.md`. Tone should be "you don't need a PhD to understand this" — demystify, don't intimidate.

---

## Article 3: Demystifying Claude Code — Internal Architecture

### What

How Claude Code works internally: the agentic loop (query → plan → tool use → observation → response → self-correction), the complete tool system (Read, Write, Edit, Bash, Glob, Grep, Agent, etc.), what a "harness" is (the software wrapping the model), how the system prompt instructs the model, how queries/conversations/turns work, the permission model, and the key insight: there's no magic, it's all software abstractions over API calls.

### Why

This is the "demystification" article. After understanding the model (article 2), devs need to see that Claude Code is just well-engineered software orchestrating that model. This kills the "it's magic" mystique and replaces it with "I can understand and configure this." It also plants the vocabulary (tools, harness, loop, permissions) that every subsequent article will use.

### How

Factory analogy: "the control panel of the machine." You've seen the engine, now you see how it's wired and controlled. Parallel to KMP-101 Part 3 (source sets — the mental model for how code is organized). Heavy reference to `research/reference-claude-code-source-deep-dive.md` which maps the Claude Code architecture course (50 lessons, 8 chapters). Research needed: `prompts/02-arquitetura-claude-code.md`. Mermaid diagrams for the agentic loop, tool taxonomy, and harness architecture.

---

## Article 4: Understanding Context — The Context Window as Resource

### What

The context window as the most precious resource in agentic programming. How context gets consumed (system prompt, conversation history, tool results, file contents). Context management strategies. Plan mode as "aim mode" — narrowing context for precision. Cost awareness: tokens = money. The relationship between context quality and output quality. How Claude Code compacts context when the window fills up.

### Why

After understanding the model (article 2) and the tool (article 3), devs need to understand the constraint that governs everything: context. Every decision in agentic programming — what to include, what to exclude, when to start a new conversation, how to structure CLAUDE.md — is ultimately a context management decision. This is the bridge between "understanding the technology" and "using it effectively."

### How

Factory analogy: "the fuel tank." Limited, expensive, and everything stops when it runs out. You don't fill the tank with anything you find — you use the right fuel for the job. Parallel to KMP-101 Part 3/4 hybrid (deepening conceptual understanding before practice). Diagrams: context window breakdown (what consumes how much), comparison table of window sizes across models. Research needed from prompt 02 (architecture) and prompt 04 (context engineering).

---

## Article 5: Setting Up and Exploring Claude Code

### What

Installing Claude Code. Authentication and API keys. Basic commands and navigation. The different modes: interactive, plan, headless. The permission model in practice (accept, reject, skip). First practical session: use Claude Code to explore a small project. Understanding what happens under the hood during a simple interaction. Cost monitoring and usage tracking.

### Why

This is the "Hello World" article. After four articles of theory and mental models, the reader finally gets hands-on. The timing is intentional: armed with understanding of models, architecture, and context, the first session will make much more sense than if they'd jumped in blind. Every action in the terminal now maps to concepts they already know.

### How

Factory analogy: "starting the machine for the first time." You know the engine, the control panel, the fuel — now you press the button. Parallel to KMP-101 Part 5 (creating and running your first project). This is the most practical article so far: step-by-step installation, screenshots of terminal sessions, annotated examples of real interactions. Show what happens in the agentic loop during a simple request. Make the reader feel "I can do this."

---

## Article 6: Prompt Engineering for Agentic Programming

### What

Prompting as the primary interface with the agent. Anatomy of a good prompt: clarity, specificity, structure. Common anti-patterns (vague requests, overloaded prompts). Prompt patterns for coding: bug description, feature request, refactoring, code review. The critical difference between chat-style prompting and agentic prompting (giving the agent autonomy vs micro-managing). Task decomposition. Iterative refinement.

### Why

This is the first of the three pillar deep-dives. After setting up and running Claude Code (article 5), the immediate question is "how do I talk to this thing effectively?" Most people default to chat-style prompting ("fix this bug") which dramatically underuses agentic capabilities. This article teaches the difference and provides concrete patterns.

### How

Factory analogy: "the control language — the instructions you give to the machine operator." Clear instructions = good output. Vague instructions = garbage. Parallel to KMP-101 Part 7 (expect/actual — the mechanism for connecting platforms). Concrete before/after examples: bad prompt → mediocre result, structured prompt → excellent result. Research needed: `prompts/04-context-e-prompt-engineering.md`. Include the "vibe coding vs professional agentic coding" distinction from article 1 as a callback.

---

## Article 7: Context Engineering — What the Agent Needs to Know

### What

Context engineering as the discipline of curating what the agent knows. CLAUDE.md as the project's "manifest file." How to structure rules for maximum impact. The hierarchy: global rules > project rules > session context. Providing relevant files, documentation, and examples. The concept of "retrieval" — helping the agent find what it needs. Anti-patterns: dumping entire codebases, contradictory rules, stale documentation.

### Why

The second pillar. After learning to communicate with the agent (article 6), devs need to learn to control what the agent knows. This is where the context window understanding from article 4 becomes practical. A well-engineered context is the difference between an agent that produces generic code and one that follows your project's conventions perfectly.

### How

Factory analogy: "the documentation and specs you provide to the team." A brilliant new hire with no documentation produces inconsistent work. The same hire with clear specs, conventions docs, and architectural guidelines produces exactly what you need. Parallel to KMP-101 Part 8 (dependencies — the ecosystem). Show real CLAUDE.md examples, rules files, and their effect on output quality. Research needed: `prompts/04-context-e-prompt-engineering.md`.

---

## Article 8: Harness Engineering — Configuring the Machine

### What

The third pillar. What "harness" means: the software surrounding and orchestrating the model. The configuration surface area: settings.json, hooks, MCP servers, custom skills. How hooks work (pre/post tool execution automation). Introduction to MCP (Model Context Protocol) — extending the agent's capabilities. The relationship between all three pillars. Series wrap-up and teaser for 102.

### Why

The final foundational article. After prompt engineering (how to talk) and context engineering (what to share), the remaining piece is the infrastructure itself. This completes the mental model: you now understand the technology (articles 2-4), you've practiced using it (article 5), and you know the three engineering disciplines (articles 6-8). The dev is ready to build real projects.

### How

Factory analogy: "the factory infrastructure — conveyor belts, sensors, safety systems, automation." The factory that produces the most isn't the one with the best workers, it's the one with the best infrastructure. Parallel to KMP-101 Part 8 (wrapping up foundational series). Show real hooks, real MCP configurations, real settings.json. End with a strong bridge to 102: "You now understand the factory. In the next series, we build one from scratch." Research needed: `prompts/02-arquitetura-claude-code.md` (architecture details for hooks/MCP).

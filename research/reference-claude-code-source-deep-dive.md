# Claude Code Source Deep Dive

> Source: https://www.markdown.engineering/learn-claude-code
> Architecture Course v1.0 — 50 lessons, 8 chapters, 1,902 source files dissected

---

## Mapping to CC-101/102/103

| Chapter | CC-101 Articles | CC-102/103 Articles |
|---|---|---|
| Ch01: Core Architecture | Art 3 (Internal Architecture) | — |
| Ch02: Tool System | Art 3 + Art 8 (Harness) | CC-102 Art 1 (Skills) |
| Ch03: Agent Intelligence | Art 3 | CC-102 Art 2 (Agents/Sub-agents) |
| Ch04: Interface | Art 5 (Exploring CC) | — |
| Ch05: Infrastructure | Art 4 (Context) + Art 8 (Harness) | CC-102 Art 1 (Config) |
| Ch06: Connectivity | — | CC-102/103 |
| Ch07: Unreleased Features | — | CC-103 |
| Ch08: Big Picture | Art 2 (Models) + Art 3 | — |

---

## Chapter 01: Core Architecture (tag: arch)

- **Boot Sequence** — how Claude Code initializes
- **Query Engine** — query processing, how requests are handled
- **State Management** — session state management
- **System Prompt** — how the system prompt is built and injected
- **Architecture Overview** — overall architecture overview

## Chapter 02: The Tool System (tag: tools)

- **Tool System** — tool system architecture
- **Bash Tool** — shell command execution
- **File Tools** — Read, Write, Edit, Glob
- **Search Tools** — Grep, codebase search
- **MCP Integration** — Model Context Protocol, external tools
- **Skills System** — customizable slash commands

## Chapter 03: Agent Intelligence (tag: agents)

- **Agent System** — how agents and sub-agents work
- **Coordinator Mode** — multi-agent orchestration
- **Teams & Swarm** — agent teamwork
- **Memory System** — persistent memory system
- **Auto-Memory & Dreams** — automatic memory

## Chapter 04: The Interface (tag: ui)

- **Ink Renderer** — terminal rendering (React Ink)
- **Commands** — command system (slash commands)
- **Dialog & UI** — dialogs and UI components
- **Notifications** — notification system
- **Vim Mode** — integrated vim mode
- **Keybindings** — keyboard shortcuts
- **Fullscreen Mode** — fullscreen mode
- **Theme & Styling** — themes and styling

## Chapter 05: Infrastructure (tag: infra)

- **Permissions** — permission model (accept, reject, etc.)
- **Settings & Config** — settings.json, CLAUDE.md, configurations
- **Session Management** — session management
- **Context Compaction** — context compaction when window fills up
- **Analytics** — telemetry and metrics
- **Migrations** — version migrations
- **Plugin System** — plugin system
- **Hooks System** — pre/post tool execution hooks
- **Error Handling** — error handling

## Chapter 06: Connectivity (tag: net)

- **Bridge & Remote** — remote connection, IDE bridge
- **OAuth** — authentication
- **Git Integration** — Git integration
- **Upstream Proxy** — request proxy
- **Cron & Scheduling** — task scheduling
- **Voice System** — voice system

## Chapter 07: Unreleased Features (tag: leak)

- **BUDDY Companion** — AI companion
- **ULTRAPLAN** — advanced planning
- **Entrypoints & SDK** — SDK for building custom agents
- **KAIROS Always-On** — always-on agent
- **Cost Analytics** — cost analysis
- **Desktop App** — desktop application

## Chapter 08: The Big Picture (tag: meta)

- **Model System** — how models are managed and selected
- **Sandbox Security** — security and sandboxing
- **Message Processing** — message processing
- **Task System** — task system
- **REPL Screen** — REPL screen

---
name: write-article
description: "Draft a new article following all project conventions. Use when starting a new article or continuing a draft. NOT for auditing, translating, or planning."
---

## What this skill does

Orchestrates the full article writing workflow by dispatching the `writer` agent with proper context.

## Process

1. **Gather context** before dispatching:
   - Confirm series and part number (e.g., CC-101 Part 2)
   - Check if research exists in `research/` for the topic
   - Identify the previous article path for continuity
   - Identify relevant research docs

2. **Dispatch the writer agent:**

```
Agent(subagent_type: "writer", prompt: "
Write CC-{series} Part {N}: '{title}'.

Previous article: posts/{series}/part{N-1}/pt-br.md
Research: research/{relevant files}
KMP-101 reference: /Users/rsicarelli/Workspace/Personal/KMP-101/posts/kmp101/KMP101-parte{N}.md

Read all rules in .claude/rules/ before writing.
Write to: posts/{series}/part{N}/pt-br.md
")
```

3. **After writer returns**, run `/audit-article` to validate the draft.

## Rules

- Always dispatch the `writer` agent. Never write the article directly in the main session.
- PT-BR is always written first. English comes later via `/translate-article`.
- If research is missing, suggest running `/research-deep-dive` first.
- If no article plan exists, suggest running `/plan-article` first.

## Related skills

- `/plan-article` — Create the outline before writing
- `/audit-article` — Validate the draft after writing
- `/research-deep-dive` — Gather material if research is missing
- `/translate-article` — Create English version after PT-BR is finalized

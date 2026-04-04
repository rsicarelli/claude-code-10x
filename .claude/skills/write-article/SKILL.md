---
name: write-article
description: "Draft a new article following all project conventions. Use when starting a new article or continuing a draft. NOT for auditing, translating, or planning."
---

## What this skill does

Orchestrates the full article writing workflow by dispatching the `writer` agent with proper context.

## Process

1. **Gather context** before dispatching:
   - Confirm series and part number (e.g., CC-101 Part 2)
   - Read the roadmap entry for this article (`roadmap/{series}-*.md`) — this is the source of truth for what/why/how
   - Check if research exists in `research/` for the topic
   - Identify the previous article path for continuity
   - Identify relevant research docs

2. **Dispatch the writer agent:**

```
Agent(subagent_type: "writer", prompt: "
Write CC-{series} Part {N}: '{title}'.

Roadmap: roadmap/{series}-*.md (read the entry for Part {N})
Previous article: posts/{series}/part{N-1}/pt-br.md
Research: research/{relevant files}
KMP-101 reference: /Users/rsicarelli/Workspace/Personal/KMP-101/posts/kmp101/KMP101-parte{N}.md

Read all rules in .claude/rules/ before writing.
Write to: posts/{series}/part{N}/pt-br.md
")
```

3. **After writer returns**, run `/generate-diagrams` to create PNG assets from Mermaid blocks.

4. **After diagrams generated**, run `/audit-article` to validate the draft.

## Article format

Every article must follow this exact structure:

```markdown
# Claude Code {series}: {Title}

> Por [Rodrigo Sicarelli](https://dev.to/rsicarelli) · CC-{series} Parte {N}
>
> 🔗 dev.to/rsicarelli/... <!-- link added after publication -->

> * [Section 1](#anchor)
> * [Section 2](#anchor)
> * ...
> * [Considerações finais](#considerações-finais)

{Opening / hook}

---

## Section 1
...
## Considerações finais
...

---

> 🤖 Este artigo foi escrito com assistência do Claude (Anthropic).
>
> Conteúdo pesquisado, verificado e editado por um humano.
>
> Encontrou algum erro ou crédito faltando? Me manda uma mensagem!

---

## Referências

1. [Source](url) — description
...
```

## Key patterns

- **Header**: `#` title + blockquote with author, series, publication link
- **TOC**: blockquote `> *` bullets with anchors matching every `##` heading
- **Diagrams**: Mermaid code block + PNG fallback image below (run `/generate-diagrams` after writing)
- **References**: numbered in order of first appearance, every one with a URL
- **Tool hyperlinks**: first mention of every tool/project gets `**[Name](url)**`

## Rules

- Always dispatch the `writer` agent. Never write the article directly in the main session.
- PT-BR is always written first. English comes later via `/translate-article`.
- If research is missing, suggest running `/research-deep-dive` first.
- If no article plan exists, suggest running `/plan-article` first.
- After writing, always run `/generate-diagrams` before `/audit-article`.

## Related skills

- `/plan-article` — Create the outline before writing
- `/audit-article` — Validate the draft after writing
- `/research-deep-dive` — Gather material if research is missing
- `/translate-article` — Create English version after PT-BR is finalized

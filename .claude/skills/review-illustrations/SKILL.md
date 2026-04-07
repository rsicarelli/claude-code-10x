---
name: review-illustrations
description: "Review article illustrations for visual comprehension. Use after writing or editing an article with diagrams. NOT for creating illustrations."
---

## What this skill does

Dispatches the `illustration-reviewer` agent to dissect an article section by section and produce detailed illustration briefs. The agent evaluates existing diagrams, proposes new ones, and ensures the full set tells a progressive visual story anchored in the article's analogy system.

## Process

1. **Identify the article** file path (e.g., `posts/101/part2/pt-br.md`).

2. **Identify the roadmap entry** for the article's series and part number (e.g., `roadmap/101-foundations.md`).

3. **Dispatch the illustration-reviewer agent:**

```
Agent(subagent_type: "illustration-reviewer", prompt: "Review illustrations for {file path}.

Read the article at {file path} and its roadmap entry at {roadmap path}.

For each ## section, produce an illustration brief following your output format. Evaluate existing diagrams, propose replacements or new illustrations, and assess the visual narrative as a whole.

The article's central analogy is {analogy — e.g., LEGO}. All proposed illustrations must be grounded in this analogy system.")
```

4. **Present the report** to the user with the full illustration brief.

## Rules

- Always provide the roadmap path so the agent understands the article's intended scope and analogy progression.
- Never auto-generate illustrations from the report. Present the brief and let the user decide what to create.
- This skill is independent from `/audit-article` but can run alongside it.
- The agent is read-only. It produces briefs, not illustrations.

## Checklist

- [ ] Article file path identified
- [ ] Roadmap entry identified and provided to agent
- [ ] Central analogy explicitly stated in the prompt
- [ ] Agent dispatched with full context
- [ ] Report presented with section-by-section briefs
- [ ] Visual narrative assessment included

## Related skills

- `/audit-article` — Audits grammar, cohesion, and conventions (separate concern)
- `/generate-diagrams` — Generates PNG assets from Mermaid blocks (run AFTER illustrations are decided)
- `/write-article` — Writes the article (run illustration review after writing)

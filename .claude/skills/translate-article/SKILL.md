---
name: translate-article
description: "Create the English version of an article from its PT-BR original. Use after PT-BR is finalized and audited. NOT for writing new content or editing PT-BR."
---

## What this skill does

Dispatches the `writer` agent in translation mode to create the English version of a finalized PT-BR article.

## Process

1. **Verify PT-BR is ready:**
   - Check that the PT-BR file exists and is finalized
   - Recommend running `/audit-article` first if not done

2. **Dispatch the writer agent in translation mode:**

```
Agent(subagent_type: "writer", prompt: "
Translate to English:
Source: posts/{series}/part{N}/pt-br.md
Target: posts/{series}/part{N}/en.md

Read .claude/rules/bilingual.md for translation rules.
Translate naturally — adapt tone for English-speaking dev audience.
Keep technical terms in English. Translate analogies and conversational tone.
Do NOT transliterate.
")
```

3. **After writer returns**, optionally run `/audit-article` on the EN version.

## Rules

- Always dispatch the `writer` agent. Never translate directly in the main session.
- PT-BR must be finalized before translating. Never translate a draft.
- The EN version is a natural adaptation, not a literal translation.

## Related skills

- `/audit-article` — Audit PT-BR before translating, or audit EN after
- `/write-article` — Write the PT-BR version first

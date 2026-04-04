---
name: research-deep-dive
description: "Research a topic and compile findings for article writing. Use when preparing material for a new article. NOT for writing articles directly."
---

## What this skill does

Conducts research on a topic, compiles findings into a structured document, and saves it for later use during article writing.

## Process

1. **Check for existing prompt** — Look in `prompts/` for a research prompt matching the topic.
2. **Gather information** — Use WebSearch and WebFetch to find:
   - Official documentation and blog posts
   - Research papers and surveys (Stack Overflow, JetBrains, DORA, etc.)
   - Community discussions (Reddit, HackerNews, dev.to)
   - Market data and adoption statistics
3. **Compile findings** — Write a structured research document in English.
4. **Map to articles** — Note which CC-101/102/103 article(s) each finding is relevant to.
5. **Save** to `research/{NN}-{topic-kebab-case}.md`.

## Rules

- All research docs in English
- Include source links for every claim
- Flag data that may become stale (market numbers, survey percentages) with the date
- Organize by topic sections, not as a raw link dump
- Prioritize sources from 2024-2026
- Be honest about contradictions in the data (e.g., METR study vs vendor claims)

## Checklist

- [ ] Existing prompt in `prompts/` consulted
- [ ] Multiple source types used (official docs, papers, community)
- [ ] Source links included
- [ ] Findings organized by topic
- [ ] Mapped to relevant articles
- [ ] Saved with correct naming convention
- [ ] Written in English

## Related skills

- `/plan-article` — Use research to plan an article outline
- `/write-article` — Use research as source material when writing

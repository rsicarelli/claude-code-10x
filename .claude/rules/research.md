---
globs: research/**/*.md, prompts/**/*.md
---

# Research and Prompts

## Language
All research and prompt docs are written in English.

## File naming
- Research: `research/{NN}-{topic-kebab-case}.md` (e.g., `01-panorama-programacao-agentica.md`)
- Prompts: `prompts/{NN}-{topic-kebab-case}.md` (e.g., `03-fundamentos-llms-para-devs.md`)
- Number prefix matches the article it feeds into when applicable

## Research documents
- Include source links whenever available
- Organize by topic sections, not as raw dump
- Note which CC-101/102/103 article(s) each finding maps to
- Flag data points that need verification (surveys change yearly, market numbers shift)

## Prompt documents
- Write as conversational briefings, not bulleted specs
- Each prompt reads like you're briefing a research assistant
- No "topic: thing -- other thing" pattern — use flowing paragraphs
- Specify the time range for sources (e.g., "2024-2026")

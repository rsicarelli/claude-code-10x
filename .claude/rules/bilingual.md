---
globs: posts/**/en.md, posts/**/pt-br.md
---

# Bilingual Articles

Every article is published in two languages simultaneously.

## Workflow
1. Write PT-BR version first (`pt-br.md`) — this is the primary
2. Translate to English (`en.md`) after PT-BR is finalized
3. Never translate PT-BR to English mid-draft — finish and audit PT-BR first

## What stays the same across both versions
- Article structure (sections, subsections, order)
- Mermaid diagrams (labels can be translated)
- Reference numbers and links
- Data points and citations
- Technical terms (already in English)

## What can differ
- Cultural references and colloquialisms (adapt, don't literally translate)
- Tone adjustments (PT-BR is more casual with contractions; English can be slightly more direct)
- Examples or analogies that don't land in one language

## Translation rules
- DO NOT translate: tool names, technical terms, code, API names, MCP, LLM, etc.
- DO translate: analogies, conversational tone, section headers, diagram labels
- The factory analogy should feel natural in both languages (not a literal translation)

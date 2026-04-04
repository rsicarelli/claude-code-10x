---
globs: posts/**/*.md
---

# Article Structure

Every article must align with its roadmap entry at `roadmap/`. The roadmap defines the scope (what/why/how) — the article structure rules define the format.

Every article follows the KMP-101 template structure.

## Required sections (in order)
1. **Table of contents** — blockquote with `> *` bullet anchors to all H2 sections
2. **Opening** — 2-4 paragraphs: hook → context → article promise with series reference
3. **Horizontal divider** `---`
4. **Main content** — H2 sections (`##`) with H3 subsections (`###`)
5. **Considerações finais / Conclusion** — forward-looking, teases next article
6. **AI disclaimer** — blockquote with 🤖 emoji
7. **References** — numbered list in order of appearance

## Factory analogy progression
The factory analogy MUST appear in every `##` or `###` section. It doesn't need to be a full paragraph — a phrase, a word, or an image is enough. But the analogy must progress, not repeat.

The progression for CC-101 follows the upgrade path:
manual → esteira → consultor → painel de controle → máquinas autônomas → fornecedores → controle de qualidade → projetar a fábrica → instruções + documentação + infraestrutura → matéria-prima / motor

## Diagrams
- Use Mermaid code blocks for diagrams
- Provide `[🔗 Versão interativa](mermaid.live/edit#...)` link above the diagram when available
- Add static PNG fallback in `posts/assets/` after publication

## References and hyperlinks
- Number references in order of first appearance: `[[1]](#referências)`
- First mention of any tool or project gets a hyperlink: `**[Claude Code](https://...)**`
- Subsequent mentions don't need the link
- References section at the end with numbered entries matching the inline citations

## Continuity
- Every article (except Part 1) must reference the previous article in the opening
- The conclusion must tease the next article's topic
- Factory analogy terms introduced in previous articles can be used without re-explaining

---
globs: posts/**/*.md
---

# Article Structure

Every article must align with its roadmap entry at `roadmap/`. The roadmap defines the scope (what/why/how) — these rules define the format.

## Required sections (in order)

1. **H1 title** — `# Claude Code {series}: {Title}`
2. **Author blockquote** — `> Por [Rodrigo Sicarelli](https://dev.to/rsicarelli) · CC-{series} Parte {N}`
3. **Publication link** — `> 🔗 dev.to/rsicarelli/...` (placeholder until published)
4. **Table of contents** — blockquote `> *` bullet anchors to every `##` heading
5. **Opening** — prose paragraphs (hook → context → series promise). No heading.
6. **Horizontal divider** `---`
7. **Main content** — `##` sections with `###` subsections
8. **Considerações finais** — forward-looking close, teases next article
9. **Horizontal divider** `---`
10. **AI disclaimer** — blockquote with 🤖
11. **Horizontal divider** `---`
12. **Referências** — `## Referências` with numbered list

## Table of contents rules

- One `> *` entry per `##` heading (not `###`)
- Anchor format: lowercase, hyphens, no accents in the anchor even if the heading has accents
- Every `##` must be in the TOC, every TOC item must have a matching `##`

## References and hyperlinks

- Number references in order of first appearance: `[[1]](#referências)`
- Every reference MUST have a URL. No text-only references.
- First mention of any tool or project gets a hyperlink: `**[Name](url)**`
- Subsequent mentions don't need the link

## Diagrams

- Use Mermaid code blocks with `<br/>` for line breaks (never `\n`)
- After writing, run `/generate-diagrams` to create PNG assets
- Each Mermaid block must have a PNG fallback image below it:
  ```
  ![Alt text](https://github.com/rsicarelli/claude-code-10x/blob/main/posts/assets/{name}.png?raw=true)
  ```
- PNG naming: `cc{series}-part{N}-{NN}-{description}.png`

## Factory analogy progression

The factory analogy MUST appear in every `##` or `###` section. Can be a phrase, not always a paragraph. Must progress, not repeat.

CC-101 progression:
manual → esteira → consultor → painel de controle → máquinas autônomas → fornecedores → controle de qualidade → projetar a fábrica → instruções + documentação + infraestrutura → matéria-prima / motor

## Continuity

- Every article (except Part 1) must reference the previous article in the opening
- The conclusion must tease the next article's topic
- Factory analogy terms from previous articles can be used without re-explaining

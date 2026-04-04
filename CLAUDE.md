# Claude Code 10x

Article series on agentic programming. Published on [dev.to/rsicarelli](https://dev.to/rsicarelli) in PT-BR + English.

## Quick reference

- Series roadmaps: `roadmap/` (source of truth for what each article covers)
- Article index: `README.md`
- Writing rules: `.claude/rules/`
- Skills: `.claude/skills/`
- Research: `research/`
- KMP-101 reference: `/Users/rsicarelli/Workspace/Personal/KMP-101/`

## Available skills

- `/write-article` — Draft a new article following all conventions
- `/audit-article` — Check article for quality and convention compliance
- `/translate-article` — Create English version from PT-BR
- `/research-deep-dive` — Research a topic and save findings
- `/plan-article` — Create section-by-section outline with factory analogy mapping
- `/skill-conventions` — Guide for creating new skills

## Available agents

| Agent | Model | Role |
|-------|-------|------|
| `writer` | opus | Writes article drafts and translations. Only agent with Write/Edit access. |
| `grammar-reviewer` | opus | Checks grammar, spelling, natural phrasing in PT-BR and EN. Read-only. |
| `cohesion-reviewer` | sonnet | Checks narrative flow, analogy progression, transitions. Read-only. |
| `convention-auditor` | haiku | Mechanical checks: TOC, refs, hyperlinks, word count. Read-only. |
| `fact-checker` | sonnet | Verifies data points, quotes, dates against research and live sources. Read-only. |

Agents are dispatched by skills, not manually. Use `/write-article`, `/audit-article`, `/translate-article` to trigger them.

## Series structure

- **101**: Foundations of Agentic Programming (8 articles)
- **102**: Applied Agentic Development (6 articles)
- **103**: Advanced Agentic (4 articles)

## Article conventions (summary)

- Two languages: `pt-br.md` first, `en.md` after
- Gender-neutral PT-BR: "dev", "você", "quem desenvolve"
- Technical terms stay in English
- Factory analogy must progress in every section
- Human tone, no AI writing patterns
- See `.claude/rules/` for full details

## Naming

- Articles: `posts/{series}/part{N}/pt-br.md` and `posts/{series}/part{N}/en.md`
- Research: `research/{NN}-{topic-kebab-case}.md`
- Prompts: `prompts/{NN}-{topic-kebab-case}.md`
- Assets: `posts/assets/`

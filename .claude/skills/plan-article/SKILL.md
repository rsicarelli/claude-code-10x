---
name: plan-article
description: "Create a section-by-section outline for an article with factory analogy mapping. Use before writing a new article. NOT for writing the article itself."
---

## What this skill does

Produces a detailed article plan including section outlines, factory analogy mapping, and diagram planning. The plan becomes the blueprint for `/write-article`.

## Process

1. **Read series roadmap** — Check `README.md` for the article's position in the series.
2. **Read previous article** — Understand where the narrative left off (tone, analogy state, teaser).
3. **Read research** — Load relevant docs from `research/`.
4. **Read KMP-101 equivalent** — Find the corresponding article in `/Users/rsicarelli/Workspace/Personal/KMP-101/posts/kmp101/` for structural inspiration.
5. **Design sections** — For each planned section, define:
   - Header (H2 or H3)
   - Content summary (what this section covers)
   - Key data points to include
   - Factory analogy parallel
   - Diagram needed (if any)
6. **Produce analogy mapping table** — Table with columns: Section | Theme | Explanation | Factory analogy

## Output format

```markdown
# Article Plan: CC-101 Part N — "{Title}"

## Context
What this article covers and why it matters in the series.

## Previous article recap
What was covered, where the analogy left off.

## Section plan

### Section 1: {Header}
- **Content:** ...
- **Key data:** ...
- **Factory analogy:** ...
- **Diagram:** ...

### Section 2: {Header}
...

## Factory analogy mapping

| Section | Theme | Explanation | Analogy |
|---------|-------|-------------|---------|
| ... | ... | ... | ... |

## Diagrams needed

| # | Type | Title | Section |
|---|------|-------|---------|
| ... | ... | ... | ... |
```

## Rules

- Every `##` and `###` section must have a factory analogy entry
- The analogy must progress (no repeating the same image)
- Reference specific research data points to include
- Note which KMP-101 article inspired the structure

## Checklist

- [ ] Series position confirmed
- [ ] Previous article read
- [ ] Research consulted
- [ ] KMP-101 equivalent identified
- [ ] Every section has content + analogy + diagram plan
- [ ] Analogy mapping table produced
- [ ] Analogy progresses without repetition

## Related skills

- `/research-deep-dive` — Gather research before planning
- `/write-article` — Execute the plan

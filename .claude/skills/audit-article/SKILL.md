---
name: audit-article
description: "Audit an article for quality and convention compliance. Use after writing or editing an article. NOT for writing new content."
---

## What this skill does

Dispatches 3 review agents in parallel to audit an article from different angles, then optionally dispatches a fact-checker. Consolidates all reports into a single action list.

## Process

1. **Identify the article** to audit (file path).

2. **Dispatch 3 review agents IN PARALLEL:**

```
Agent(subagent_type: "grammar-reviewer", prompt: "Review {file path} for grammar, spelling, and natural language quality.")

Agent(subagent_type: "cohesion-reviewer", prompt: "Review {file path} for narrative flow, factory analogy progression, and transitions.")

Agent(subagent_type: "convention-auditor", prompt: "Audit {file path} for structural convention compliance: TOC, references, hyperlinks, word count, disclaimer.")
```

3. **Wait for all 3 reports.** Consolidate into a single summary with:
   - Combined issue count
   - Prioritized fix list (critical first, suggestions last)
   - Pass/fail per category

4. **Optionally dispatch fact-checker** (if the article has data points or claims):

```
Agent(subagent_type: "fact-checker", prompt: "Fact-check {file path} against research docs in research/ and live sources.")
```

5. **Present the consolidated report** to the user with actionable fixes.

## Rules

- Always dispatch all 3 review agents in parallel for efficiency.
- Fact-checker is optional but recommended for data-heavy articles.
- Never apply fixes automatically. Present the report and let the user decide.
- If an article has 5+ critical issues, recommend fixing before translating.

## Output format

```markdown
## Audit Summary: {file path}

### By category
| Category | Agent | Issues | Critical |
|----------|-------|--------|----------|
| Grammar & language | grammar-reviewer | {N} | {N} |
| Cohesion & analogy | cohesion-reviewer | {N} | {N} |
| Conventions | convention-auditor | {N} | {N} |
| Facts (optional) | fact-checker | {N} | {N} |

### Prioritized fixes
1. {Critical: ...}
2. {Critical: ...}
3. {Suggestion: ...}
...

### Overall: {PASS / NEEDS FIXES / MAJOR ISSUES}
```

## Related skills

- `/write-article` — Write the article (run audit after)
- `/translate-article` — Translate to English (audit PT-BR first)

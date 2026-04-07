---
globs: posts/**/*.md
---

# Agent Dispatch

When working with article files, always use specialized agents instead of doing the work directly.

## Writing
When writing a new article or continuing a draft, dispatch the `writer` agent via the `/write-article` skill. Never write article content directly in the main session.

```
Agent(subagent_type: "writer", prompt: "<full context: series, part number, research refs, previous article path>")
```

## Reviewing
When auditing or reviewing an article, dispatch all 3 review agents in parallel via the `/audit-article` skill:

```
Agent(subagent_type: "grammar-reviewer", prompt: "<file path>")
Agent(subagent_type: "cohesion-reviewer", prompt: "<file path>")
Agent(subagent_type: "convention-auditor", prompt: "<file path>")
```

## Fact-checking
When verifying data points, dispatch the fact-checker:

```
Agent(subagent_type: "fact-checker", prompt: "<file path + research directory>")
```

## Illustration review
When reviewing visual comprehension of an article, dispatch the illustration-reviewer via `/review-illustrations`:

```
Agent(subagent_type: "illustration-reviewer", prompt: "<file path + roadmap path + central analogy>")
```

## Translating
When creating the English version, dispatch the writer in translation mode via `/translate-article`:

```
Agent(subagent_type: "writer", prompt: "Translate <source path> to <target path>. Read .claude/rules/bilingual.md.")
```

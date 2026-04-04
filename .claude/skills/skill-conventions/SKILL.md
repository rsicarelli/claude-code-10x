---
name: skill-conventions
description: "Guide for creating and maintaining skills in this project. Use when adding a new skill. NOT for using existing skills."
---

## What this skill does

Documents the conventions for creating new skills in the `.claude/skills/` directory.

## Skill file structure

Every skill lives in its own directory with a single `SKILL.md` file:

```
.claude/skills/{skill-name}/SKILL.md
```

## Template

```markdown
---
name: {skill-name}
description: "{Verb phrase}. Use when {trigger context}. NOT for {exclusions}."
---

## What this skill does

One paragraph explaining the skill's purpose.

## Process

Numbered steps for how to execute the skill.

## Rules

Constraints and guardrails specific to this skill.

## Checklist

- [ ] Item 1
- [ ] Item 2
...

## Related skills

- `/other-skill` — When to use instead or in combination
```

## Conventions

- **Directory name**: kebab-case (e.g., `write-article`, `audit-article`)
- **Description**: Starts with a verb. Includes "Use when" trigger and "NOT for" exclusion.
- **Process**: Numbered steps. Actionable. References specific files/paths.
- **Checklist**: Every item has corresponding content in the body. No orphan checkboxes.
- **Related skills**: Cross-references to prevent confusion about which skill to use.
- **Language**: All skill files in English.

## Checklist

- [ ] Directory name is kebab-case
- [ ] SKILL.md has correct frontmatter (name + description)
- [ ] Description starts with verb, has "Use when" and "NOT for"
- [ ] Process has numbered steps
- [ ] Checklist items match body content
- [ ] Related skills section present
- [ ] Written in English

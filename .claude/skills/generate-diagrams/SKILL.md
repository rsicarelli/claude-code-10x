---
name: generate-diagrams
description: "Extract Mermaid diagrams from an article and generate PNG assets. Use after writing or editing diagrams in an article. NOT for writing article content."
---

## What this skill does

Extracts all Mermaid code blocks from an article, generates PNG images with consistent styling, saves them to `posts/assets/`, and adds image fallback references in the article for dev.to compatibility.

## Process

1. **Extract Mermaid blocks** from the article:

```bash
python3 -c "
import re, sys
with open(sys.argv[1]) as f:
    content = f.read()
blocks = re.findall(r'\`\`\`mermaid\n(.*?)\`\`\`', content, re.DOTALL)
for i, block in enumerate(blocks):
    path = f'/tmp/mermaid-gen/block-{i}.mmd'
    with open(path, 'w') as f:
        f.write(block.strip())
    print(f'{i+1}. block-{i}.mmd ({len(block.strip().splitlines())} lines)')
" posts/101/part1/pt-br.md
```

2. **Generate PNGs** for each block:

```bash
echo '{"theme": "dark"}' > /tmp/mermaid-gen/config.json

npx -y @mermaid-js/mermaid-cli \
  -i /tmp/mermaid-gen/block-0.mmd \
  -o posts/assets/{name}.png \
  -e png \
  --scale 3 \
  --width 1200 \
  --backgroundColor transparent \
  --configFile /tmp/mermaid-gen/config.json
```

3. **Review each PNG** visually before committing. Check for:
   - Text clipping (subgraph titles too long, nodes overflowing)
   - `\n` appearing as literal text (use `<br/>` instead in Mermaid)
   - Readability at normal zoom
   - Consistent dark theme across all diagrams

4. **Add image fallback** below each Mermaid block in the article:

```markdown
```mermaid
...diagram code...
​```

![Description](https://github.com/rsicarelli/claude-code-10x/blob/main/posts/assets/{name}.png?raw=true)
```

5. **Commit and push** so GitHub raw URLs resolve.

## Configuration

- **Theme:** dark
- **Background:** transparent
- **Scale:** 3 (retina quality)
- **Width:** 1200px
- **Tool:** `npx -y @mermaid-js/mermaid-cli` (no install needed)
- **Config file:** `{"theme": "dark"}`

## Naming convention

```
cc{series}-part{N}-{NN}-{short-description}.png
```

Examples:
- `cc101-part1-01-autocomplete-vs-chat.png`
- `cc101-part1-02-evolution-timeline.png`
- `cc102-part3-01-sdd-cycle.png`

## Image reference pattern

GitHub raw URL for dev.to:
```
![Alt text](https://github.com/rsicarelli/claude-code-10x/blob/main/posts/assets/{filename}.png?raw=true)
```

## Common issues

| Problem | Cause | Fix |
|---------|-------|-----|
| `\n` shows as literal text | Mermaid uses `<br/>` not `\n` | Replace `\n` with `<br/>` inside quotes |
| Text clipped in subgraph | Title too long | Shorten subgraph labels |
| Dark background with light theme | Transparent bg + dark viewer | Use `{"theme": "dark"}` config |
| Timeline text cut off | Timeline type has rendering limits | Use wider `--width` or switch to `flowchart TD` |

## Checklist

- [ ] All Mermaid blocks extracted
- [ ] Config file uses dark theme
- [ ] Each PNG reviewed visually (no clipping, no literal `\n`, readable)
- [ ] Naming follows convention `cc{series}-part{N}-{NN}-{description}.png`
- [ ] Image fallback added below each Mermaid block in article
- [ ] Committed and pushed (raw URLs need the push to resolve)

## Related skills

- `/write-article` — Diagrams are part of writing
- `/audit-article` — Convention auditor checks for Mermaid presence

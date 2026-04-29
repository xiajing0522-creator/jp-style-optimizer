# Step 4: Token Architecture

## Layer Budget

| Layer | File | Target | Content |
|-------|------|--------|---------|
| 0 Metadata | SKILL.md frontmatter | ≤100w | name, description, trigger phrases |
| 1 Router | SKILL.md body | ≤1000w | stance, red lines, style routing table, command format |
| 2 Workflow | references/style-guide.md (~1400w) | ≤2000w | 4 style specs with examples + red line checkpoints |
| 3 Reference | (none) | — | Not needed; style specs fit in Layer 2 |

## Sub-command Decision

No sub-commands — single operation (optimize). Style is a parameter, not a sub-command.

## Always-loaded token estimate

Layer 0+1: ~600w. Layer 2 loaded on every invocation (single workflow): ~1400w. Total: ~2000w < 3000w limit. ✓

## Token Declarations in SKILL.md

```
- `references/style-guide.md` (~1400w) — loaded on every invocation
```

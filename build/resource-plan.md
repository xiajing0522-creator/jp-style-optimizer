# Step 5: Resource Plan

## references/

| File | Justification | Used in scenarios |
|------|--------------|-------------------|
| `style-guide.md` | 4 style specs with constraints and examples; too large for SKILL.md router; used in every invocation | All 5 examples from Step 1 |

## scripts/

None. Execution delegated to `python main.py style` backend. Verification logic (RL-1,3,4,5,6) lives in `style_optimizer.py`, not in skill files.

## assets/

None.

## Dependency audit (P1)

- `python main.py style` — required; no lighter alternative (Claude alone lacks glossary term lock)
- `style-guide.md` — justified; used in 100% of invocations; cannot be a script (content, not executable)

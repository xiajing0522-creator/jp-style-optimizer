---
name: token-audit
type: diagnosis
skill: jp-style-optimizer
updated: 2026-04-28
---

# Token Audit

## Word Count Measurements (2026-04-28)

| Component | Words (est.) | Threshold | Status |
|-----------|-------------|-----------|--------|
| SKILL.md body (excl. frontmatter) | ~2,480 | ≤ 3,000 | WARNING — 83% of budget |
| `references/style-guide.md` | ~4,500 | ≤ 5,000 (soft) | WARNING — 90% of ceiling |
| Always-loaded total | ~6,980 | monitor | Approaching capacity |

**Method**: `wc -w` equivalent estimate from line count × avg words/line. SKILL.md: ~340 lines. style-guide.md: ~907 lines.

**Comparison to previous audit (pre-v4.0.0)**: SKILL.md grew from ~530 → ~2,480 words (+368%). style-guide.md grew from ~750 → ~4,500 words (+500%). Growth driven by v4.0.0 two-tier routing expansion (5 styles × 20 scenes), v4.1.0 quality framework, and v4.2.x localization patterns.

## Loading Strategy Assessment

- `references/style-guide.md`: **Always loaded** ("Read before executing" — Step 4 instruction). Contains all T1/T2 specs.
- `references/case-library.md` (planned): **Conditional load** — only when brand-specific output requested or input contains a listed brand name.

## Budget Warnings

1. **SKILL.md has ~520 words of headroom.** Any substantial addition requires compression elsewhere. The backward compatibility table (lines 158-166, ~50 words) and keyword inference list (lines 168-188, ~150 words) are candidates for relocation to style-guide.md.

2. **style-guide.md has ~500 words to soft ceiling.** Adding new scenes or substantial new constraints will push it over. If Layer 3 case assets were placed here (rather than in a separate file), the ceiling would be exceeded immediately.

3. **Future architecture consideration**: If the skill grows beyond v5.0.0, consider splitting style-guide.md into per-Tier-1 files (marketing-guide.md, report-guide.md, etc.) with conditional loading by routed style.

## Compression Opportunities

| Opportunity | Savings | Risk |
|-------------|---------|------|
| Move keyword inference list from SKILL.md to style-guide.md | ~150 words from SKILL.md | Adds to style-guide.md; net positive since SKILL.md is tighter |
| Compress backward compat table to single line | ~40 words from SKILL.md | Minor readability loss |
| Move Swipe Patterns to separate reference file | ~300 words from style-guide.md | Adds conditional load complexity |

## Verdict

Token budget is under pressure but manageable with planned compression (Phase 4E). The split of case assets into a separate conditional-load file (case-library.md) is essential — placing them in style-guide.md is not viable.

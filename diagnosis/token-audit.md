---
name: token-audit
type: diagnosis
skill: jp-style-optimizer
version_assessed: 6.5.0
date: 2026-05-12
target_version: 6.6.0
---

# Token Audit (v6.6.0 Boost — moomoo JP Routing Integration)

## Word Count Measurements (2026-05-12)

Measured via `wc -w` after authoring `references/moomoo-jp-routing.md`:

| Component | Words | Threshold | Status |
|-----------|-------|-----------|--------|
| SKILL.md (incl. frontmatter / trigger list) | 3,194 | ≤ 3,500 (post-v6.0 budget) | OK — 91% |
| `references/style-guide.md` | 668 | ≤ 1,500 (always-loaded routing table) | OK — 45% |
| `references/case-library.md` | 1,310 | ≤ 5,000 (conditional) | OK — 26% |
| `references/campaign-guide.md` | 529 | ≤ 1,500 (conditional) | OK |
| `references/trade-ideas-guide.md` | 852 | ≤ 1,500 (conditional) | OK |
| `references/news-guide.md` | 683 | ≤ 1,500 (conditional) | OK |
| `references/product-guide.md` | 271 | ≤ 1,500 (conditional) | OK |
| `references/compliance-guide.md` | 338 | ≤ 1,500 (conditional) | OK |
| `references/moomoo-jp-routing.md` (NEW) | **1,050** | ≤ 1,500 (conditional) | OK — 70% |
| **Always-loaded total (SKILL.md + style-guide.md)** | **3,862** | monitor ≤ 5,000 | OK |

## Loading Strategy

| File | Load Strategy | Rationale |
|------|---------------|-----------|
| `references/style-guide.md` | Always-loaded — Step 3 | Routing inference table |
| `references/case-library.md` | Conditional — Step 3.5 brand match | Loaded when brand name detected |
| `references/moomoo-jp-routing.md` (NEW) | **Conditional** — Step 3 + Step 3.5 when input contains `moomoo` / `moomoo証券` | Brand-specific channel ↔ scene mapping with RL-4 limits already applied |
| `references/{style}-guide.md` | Conditional — Step 4 after `--style` route | T1+T2 specs |
| `diagnosis/moomoo-jp-control-group.md` (NEW) | Not runtime-loaded; for boost test only | 31 control samples for A/B regression |

## Budget Impact of v6.6.0 Additions

| Change | Word Delta | Always-loaded? |
|--------|-----------|----------------|
| Add 1-line References row in SKILL.md for moomoo-jp-routing.md | +20 | Yes (negligible) |
| Add 1-line note in style-guide.md routing inference (moomoo brand → conditional load) | +15 | Yes (negligible) |
| New moomoo-jp-routing.md | +1,050 | **No — conditional** |
| New moomoo-jp-control-group.md (diagnosis) | +1,200 | **No — never loaded** |
| Net always-loaded delta | **+35** | Within 1% — no compression needed |

## Verdict

**OK — well within budget.** Always-loaded total goes from 3,827 → 3,862 (≈+0.9%). Adding a conditional brand-routing file is the same load pattern as `case-library.md` and adds no fixed cost. No compression action required.

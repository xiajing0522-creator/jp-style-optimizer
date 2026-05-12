---
report: boost
skill: jp-style-optimizer
release: moomoo JP routing integration ([Unreleased])
date: 2026-05-12
boost_workflow: mojo-skill-creator/boost
---

# Boost Report — moomoo JP Routing Integration

## Summary

Adds brand-routing reference for moomoo JP (`references/moomoo-jp-routing.md`) and 31-sample boost-effect control group (`diagnosis/moomoo-jp-control-group.md`) sourced from 飞书 wiki `OGQQwEmmhi0FFJkGwSYcasNCnyh` (5 sheets, 539 lines / ~120KB merged). Codifies the brand-routing extraction pattern as **ADR-011** so future complex-channel brands follow a consistent shape.

Purely additive release — no architecture change, no breaking change, no red-line modification.

## File Delta

### Created (3)
| File | Words / Lines | Purpose |
|------|---------------|---------|
| `references/moomoo-jp-routing.md` | 1,050w | Brand routing tables (5 T1 × channels × scenes × RL-4 limits + segment table + checklist) |
| `diagnosis/moomoo-jp-control-group.md` | ~1,200w / 386 lines | 31 verbatim samples for boost A/B regression |
| `docs/adr/ADR-011-brand-routing-extraction-pattern.md` | 640w | Records the extract-into-3-files pattern + extraction trigger |

### Edited (5)
| File | Change |
|------|--------|
| `SKILL.md` | +1 row in References table (moomoo-jp-routing.md load condition). Word count 3,194 → 3,232. |
| `references/style-guide.md` | +1 section "Brand-Specific Routing Overlay" with brand-trigger table. Word count 668 → 751. |
| `references/case-library.md` | moomoo entry: added "Companion files" pointer; expanded "Primary scenes" to cover all 5 T1. Word count 1,310 → 1,358. |
| `diagnosis/structural-audit.md` | Refreshed for v6.6.0 release; 9-item check PASS. |
| `diagnosis/token-audit.md` | Refreshed; always-loaded delta +35w (negligible). |
| `diagnosis/platform-check.md` | Refreshed; CLEAN. |
| `diagnosis/synthesis.md` | Appended Phase 1 summary + Phase 2 prescription (8 actions) + Phase 3 verification. |
| `CHANGELOG.md` | New `[Unreleased]` section above `[6.0.0]`. |

## Word-Count Verification

| Component | Before | After | Threshold | Status |
|-----------|--------|-------|-----------|--------|
| SKILL.md | 3,194 | 3,232 | ≤ 3,500 | ✓ (+38, 92%) |
| references/style-guide.md | 668 | 751 | ≤ 1,500 | ✓ (+83, 50%) |
| Always-loaded total (SKILL.md + style-guide.md) | 3,862 | 3,983 | ≤ 5,000 | ✓ (+121, 80%) |
| references/moomoo-jp-routing.md (new conditional) | — | 1,050 | ≤ 1,500 | ✓ (70%) |
| references/case-library.md (conditional) | 1,310 | 1,358 | ≤ 5,000 | ✓ (27%) |
| ADR-011 | — | 640 | n/a | — |

## ADR

**ADR-011 — Brand-Routing Reference Extraction Pattern**
- **Decision**: When a brand exceeds the channel-inventory threshold (≥ 5 channels in any T1 OR ≥ 3 T1 with channel-level RL-4 differences), split brand content into three files: (1) `case-library.md` voice-signature entry, (2) `references/{brand}-routing.md` channel↔scene↔RL-4 tables, (3) `diagnosis/{brand}-control-group.md` boost regression samples. Brands below the threshold stay single-file in `case-library.md`.
- **First application**: moomoo. Re-evaluate Nomura / Rakuten / SBI when their channel inventories grow.

## Acceptance Check (8 items)

| # | Check | Result |
|---|-------|--------|
| 1 | Structural 9-item check PASS | ✓ (structural-audit.md) |
| 2 | Token budgets respected | ✓ (token-audit.md) |
| 3 | Platform-agnostic | ✓ (platform-check.md) |
| 4 | No breaking change to published interfaces (P6) | ✓ (existing `--style` / `--scene` calls unaffected) |
| 5 | New conditional reference correctly registered in SKILL.md References table | ✓ (one row added; load condition specified) |
| 6 | Brand trigger documented in style-guide.md routing inference layer | ✓ (Brand-Specific Routing Overlay section) |
| 7 | ADR for new pattern recorded with all 5 sections | ✓ (ADR-011) |
| 8 | Changelog [Unreleased] entry with Added / Changed / Backward Compatibility | ✓ (CHANGELOG.md) |

## Next

The 31-sample control group is in place but **not yet executed**. Recommended follow-up boost cycle:

1. Save current skill state as `boost-before` (git tag).
2. Apply this release (the `boost-after` state).
3. For each of the 31 samples, run the same `--style` × `--scene` × `--segment` against both states.
4. Compare:
  - RL-4 character-limit compliance rate
  - Red-line violation counts (RL-1 through RL-12)
  - AC-1 through AC-16 pass rate
  - Brand-voice match against case-library.md moomoo benchmarks
5. Aggregate into a boost-effect score per Tier 1.

Coverage gaps in the control group (campaign/remind, campaign/lastday, campaign/result, campaign/seasonal, trade-ideas/earnings, trade-ideas/morning, news/indicator, compliance/faq, compliance/guide) can be filled in the next cycle by feeding new moomoo briefs through the boost-after skill and adding the outputs as experimental-group samples.

## Files Touched

```
references/moomoo-jp-routing.md        (NEW, 1,050w)
diagnosis/moomoo-jp-control-group.md   (NEW, 386 lines)
docs/adr/ADR-011-brand-routing-extraction-pattern.md  (NEW, 640w)
SKILL.md                               (EDIT, +1 row)
references/style-guide.md              (EDIT, +1 section)
references/case-library.md             (EDIT, moomoo entry pointer)
diagnosis/structural-audit.md          (REFRESH)
diagnosis/token-audit.md               (REFRESH)
diagnosis/platform-check.md            (REFRESH)
diagnosis/synthesis.md                 (APPEND v6.6.0 section)
CHANGELOG.md                           (PREPEND [Unreleased])
build/boost-report-moomoo-jp-routing.md (THIS FILE)
```

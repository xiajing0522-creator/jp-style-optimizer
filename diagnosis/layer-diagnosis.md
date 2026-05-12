---
name: layer-diagnosis
type: diagnosis
skill: jp-style-optimizer
version_assessed: 5.2.0
date: 2026-04-29
target_version: 6.0.0
---

# Knowledge Layer Diagnosis (v6.0.0 Boost)

## Verdict: Layer 2

The skill operates at Layer 2 (Patterns). It recognizes 5 scenario types and applies register-specific transformation patterns to each, with inline verification. Evidence below.

---

## Layer 1 Test

**Test**: Two different inputs → same style → do outputs share identical structure/rhythm regardless of topic?

**Finding**: PASS (above Layer 1). The skill's routing table defines structurally distinct T1+T2 patterns. A `marketing/lp` output (利益→証明→特徴→CTA) differs structurally from a `report/report` output (背景/現状→分析→見通し). Different style targets produce structurally differentiated outputs, not a generic template.

**Evidence**: style-guide.md contains ≥20 T2 scene specifications with distinct information structure, sentence length targets, and tone markers. The Layer 1 uniform-template pattern is not present.

---

## Layer 2 Test

**Test**: "In the style of [specific reference]" — does the skill capture the general category but miss specific parameters?

**Finding**: PARTIAL PASS. The skill correctly identifies T1+T2 register parameters and has category-level constraints (verb endings, CTA requirements, character limits, hedging patterns). It performs competently at register-level transformation.

However, the v6.0.0 redesign surfaces 3 specific Layer 2 weaknesses:

1. **New T1 styles not modeled**: campaign, trade-ideas, and news are not present in v5.2.0. Any input requesting these styles cannot be properly handled.

2. **T1 routing ambiguity**: The old `marketing` style conflates campaign (期間限定特典) and marketing (恒常的商品訴求). The old `report` style conflates news (事実速報) and analytical report. These ambiguities cause category mis-routing.

3. **trade-ideas dual-register blocked**: RL-11 currently prohibits the だ/である + です/ます mixing that trade-ideas requires at section level. This is a hard Layer 2 failure for that domain.

**Evidence**: build/domain-research-trade-ideas.md and build/domain-research-campaign.md both document workflows that don't map to any current T1+T2 combination.

---

## Layer 3 Test

**Test**: Output in reference style + deliberate error → does skill auto-detect and correct?

**Finding**: FAIL for subtler errors. The skill detects mechanical violations (RL-1 term check, RL-4 char limits, RL-5 register purity) via Step 5 inline verification. However:
- It cannot detect that 〜との見方が広がっている is more authentic than 〜と見られる for Daiwa-style output
- It cannot detect that a campaign reminder message shifted CTA temperature from Hot to Cold across the lifecycle
- It cannot detect that a trade-ideas piece included a specific buy recommendation (crossing the investment advice line subtly)

The skill's verification is **mechanically complete but semantically shallow** at Layer 2.

---

## Layer Assessment: Layer 2 (Solid)

| Dimension | Current State |
|-----------|--------------|
| Generic template application (L1) | Absent ✓ |
| Register-specific pattern application (L2) | Present ✓ |
| Reference-specific calibration (L2.5) | Partial — case-library.md has brand benchmarks but matching is manual |
| Case-based auto-detection and correction (L3) | Absent |

---

## Upgrade Path for v6.0.0

### Priority 1: Complete Layer 2 coverage (fix the T1 gaps)

The v6.0.0 redesign addresses this by adding campaign, trade-ideas, and news as proper T1 styles with complete constraint sets. This moves the skill from "Layer 2 with gaps" to "Layer 2 complete."

### Priority 2: Layer 2 → Layer 2.5 (reference calibration)

The case-library.md brand matching (Step 3.5) already supports this. v6.0.0 should add brand benchmarks for the new T1 styles: moomoo campaign examples, moomoo/楽天 trade-ideas examples.

### Priority 3: Layer 2.5 → Layer 3 foundation (future)

A full Layer 3 upgrade requires a case asset library with 3-5 benchmark examples per T1 style, plus an error-detection step. This is post-v6.0.0 scope. The v6.0.0 redesign should not attempt Layer 3 — the architectural foundation (complete T1 coverage) must be correct first.

---

## Layer After v6.0.0

**Expected**: Layer 2 (Complete) — from Layer 2 (with gaps). The upgrade eliminates T1 routing ambiguity and adds proper constraint sets for campaign, trade-ideas, news, and merged compliance. Layer 3 upgrade remains a future opportunity.

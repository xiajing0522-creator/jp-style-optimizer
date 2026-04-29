---
name: cross-style-quality-rubric
type: diagnosis
skill: jp-style-optimizer
version: 5.2.0
date: 2026-04-28
---

# Cross-Style Quality Rubric — jp-style-optimizer v5.2.0

## Purpose

Extends the marketing quality rubric (D1–D8 shared + D9 per-style) to all 5 Tier 1 styles. D1–D8 definitions remain identical across styles. D9 is redefined per style to measure each style's primary effectiveness goal.

---

## Shared Dimensions (D1–D8)

See `marketing-quality-rubric.md` for full D1–D8 scoring criteria. These apply universally:
- D1 Term Integrity, D2 Information Fidelity, D3 Register Consistency
- D4 CTA/Action Effectiveness (adapted per style), D5 Character/Length Compliance
- D6 Scene Structure, D7 Naturalness, D8 Brand Fit (when applicable)

---

## D9 Per-Style Definitions

### Marketing: D9 — Persuasive Appeal
See `marketing-quality-rubric.md` for full definition.

### Report: D9 — Analytical Authority

Measures whether a professional reader trusts the analysis and has sufficient basis for investment decisions.

| Score | Criteria |
|-------|---------|
| 1 | Pure description (no analysis layer); uniform hedge level; no attribution; reader cannot make decisions |
| 2 | Analysis intent present but evidence→conclusion chain broken; only one hedge type; low info density |
| 3 | Evidence chain intact; 2+ hedge levels used; core data attributed; but density average, decision relevance weak |
| 4 | Complete evidence chain; all 3 hedge levels; full attribution; high density; clear decision direction |
| 5 | All dimensions: precise hedge gradient + zero logic jumps + high density + full attribution + reader can form investment judgment. Reads like Nomura/Daiwa weekly |

**Per-scene focus**: report=evidence chain, press=fact density, deck=scan efficiency, hottopic=character efficiency, topic=objectivity+engagement balance.

### Product: D9 — Comprehension & Confidence

Measures whether the reader quickly understands features, maps them to personal benefit, and feels "I can use this."

| Score | Criteria |
|-------|---------|
| 1 | Pure feature list (no benefit mapping); company-centric; jargon unexplained; reader doesn't know relevance |
| 2 | Benefit mentioned but buried; term explanations incomplete; vague claims (convenient/safe without specifics) |
| 3 | Feature→Benefit present for 50%+ claims; terms explained; but abstract, lacking numbers/scenarios |
| 4 | All features have F→B conversion; terms explained; specific; user-centric; minor confidence gap |
| 5 | Full stack: every feature→specific benefit→user perspective; minimal cognitive load; scene-appropriate confidence signals |

**Per-scene focus**: short=instant differentiation, detail=complete F→B, manual=zero-backtrack, script=single-listen comprehension.

### Legal: D9 — Regulatory Precision & Risk Completeness

Measures whether the text passes compliance review without rework and protects the company legally.

| Score | Criteria |
|-------|---------|
| 1 | Missing risk warnings; colloquial liability language; undefined terms; fails compliance review |
| 2 | Risk warnings present but incomplete; obligation framing mixed (request vs regulatory style) |
| 3 | All required warnings present; liability framework adequate; but conditional ambiguity or undefined first-use terms |
| 4 | Risks complete, liability precise, definitions clear, obligations enforceable; compliance officer has minor wording suggestions only |
| 5 | Full regulatory coverage + precise causation chain + consistent definitions + zero ambiguity; submittable to FSA without rework |

**Per-scene focus**: disclosure=risk type coverage+conditional precision, terms=enforceability+exception marking, disclaimer=liability limitation+precaution hedge.

### Support: D9 — Resolution Efficiency & User Reassurance

Measures whether the reader knows exactly what to do, feels respected, and won't need to contact support again.

| Score | Criteria |
|-------|---------|
| 1 | Vague answer; no channels; no steps; blunt/commanding tone |
| 2 | Answer present but indirect; single channel; steps incomplete; inconsistent keigo |
| 3 | Direct answer + basic channels + mostly complete steps; but missing fallback/recovery phrase; 1 keigo gap |
| 4 | All sub-criteria met; user knows what to do and feels reassured; minor phrasing optimization only |
| 5 | Maximum self-service resolution: direct answer + complete steps + all channels + recovery phrase + reassurance tone; CS manager has zero edits |

**Per-scene focus**: faq=direct-answer-first+channel clarity, guide=step completeness+branching+processing time.

---

## Pass Criteria (All Styles)

| Style | Total max | Pass threshold | Hard gates |
|-------|-----------|---------------|------------|
| Marketing (branded) | 45 | ≥34 | D1≥3, D2≥3, D9≥3 |
| Marketing (unbranded) | 40 | ≥30 | D1≥3, D2≥3, D9≥3 |
| Report | 40 (D4=N/A for report/hottopic) | ≥30 | D1≥3, D2≥3, D9≥3 |
| Product | 40 (D8=N/A unless branded) | ≥30 | D1≥3, D2≥3, D9≥3 |
| Legal | 35 (D4=N/A, D8=N/A) | ≥26 | D1≥3, D2≥3, D9≥3 |
| Support | 35 (D4=functional only, D8=N/A) | ≥26 | D1≥3, D2≥3, D9≥3 |

Universal: No dimension ≤1 (hard fail, must revise).

---

## D4 Adaptations Per Style

| Style | D4 measures | Score 5 signal |
|-------|-------------|---------------|
| Marketing | CTA with action verb + buyer-stage alignment | Scene-optimized phrasing |
| Product | Actionability (CTA optional but natural if present) | Reader knows next step |
| Report | N/A for report/hottopic; Attribution quality for press/deck/topic | Every claim has source |
| Legal | N/A (legal has no CTA) | — |
| Support | Functional navigation (channels stated) | All channels + recovery phrase |

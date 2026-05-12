---
id: ADR-001
title: Merge legal + support into compliance (Tier 1)
date: 2026-04-29
status: accepted
deciders: jp-style-optimizer v6.0.0 redesign
affects: SKILL.md, references/compliance-guide.md, references/case-library.md
---

# ADR-001: Merge `legal` + `support` into `compliance`

## Context

v5.2.0 has `legal` (法律合規) and `support` (客服支援) as separate Tier 1 styles. In practice, these two styles:
- Share the same top-level goal: building institutional trust
- Share the same prohibition set: zero promotional tone, no urgency markers, no benefit claims
- Share the same dominant proof dimension: Ethos
- Co-occur frequently in real documents (FAQ末尾にdisclaimer, guide内にterms参照)

Keeping them separate creates routing confusion: input like "add a disclaimer to this FAQ answer" has no clear routing path.

## Decision

Merge `legal` and `support` into a single Tier 1 style: **`compliance`** (合規服務類).

Sub-register differentiation is handled at Tier 2 (scene level):
- `compliance/disclosure`, `compliance/terms`, `compliance/disclaimer` → legal sub-register (だ/である or です/ます; 謙譲語II limited)
- `compliance/faq`, `compliance/guide` → support sub-register (です/ます; 謙譲語II全面)

## Consequences

**Positive:**
- Single routing decision for all trust-building documents
- RL-11 register mixing check simplified to scene-level table lookup
- Eliminates duplicate prohibitions across the two old Tier 1 styles

**Negative:**
- Breaking change: `--style legal` and `--style support` no longer valid (mitigated by backward compat aliases)
- `compliance/disclosure` has だ/である uniqueness within the compliance T1 — requires careful documentation

## Backward Compatibility

Add aliases: `legal → compliance`, `support → compliance`. Scene defaults: `--style legal` → `compliance/disclaimer`; `--style support` → `compliance/faq`.

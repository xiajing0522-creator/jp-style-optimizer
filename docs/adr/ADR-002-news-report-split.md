---
id: ADR-002
title: Split `report` into `news` (事実速報) + `trade-ideas` (赚效分析)
date: 2026-04-29
status: accepted
deciders: jp-style-optimizer v6.0.0 redesign
affects: SKILL.md, references/news-guide.md, references/trade-ideas-guide.md
---

# ADR-002: Split `report` into `news` + `trade-ideas`

## Context

v5.2.0's `report` style covers everything from pure fact-reporting (日経スタイル) to analytical market commentary to community engagement posts. This produces routing ambiguity: "改成市況速報" (want pure facts, no analysis, no CTA) and "改成投資アイデア" (want analysis + action bridge) both route to `report` with conflicting constraint sets.

Key conflicts in v5.2.0 `report`:
- `report` prohibits CTA, but `report/topic` allows it (community engagement)
- `report` allows unlimited analysis, but pure news should cap analysis at ≤30%
- `report` is CTA-free, but trade-ideas content requires an action bridge (TI-5)
- RL-11 applies uniformly but trade-ideas needs だ/である + です/ます section mixing

## Decision

Split `report` into two Tier 1 styles:

1. **`news`** (新聞事件類): Objective financial event reporting. Zero CTA, ≤30% analysis, strict だ/である, mandatory timeliness annotation. Corresponds to: 日経, Reuters JP, Bloomberg JP style.

2. **`trade-ideas`** (赚效内容類): Market analysis with action bridge. Dual-register allowed at section level, action bridge mandatory, investment disclaimer required for ≥500w content. Corresponds to: 楽天証券マーケット情報, moomoo証券ホットトピック style.

## Boundary Rule

Distinguish at routing: if content is pure event reporting (≤30% analysis, no action suggestion) → `news`. If content leads to a specific "what you can do now" conclusion → `trade-ideas`.

## Consequences

**Positive:**
- Clean separation of constraints — news gets strict Logos, trade-ideas gets Logos+action bridge
- RL-11 exception for trade-ideas is localized to one T1, not a global rule change
- routing precision improves for the largest use cases (market content)

**Negative:**
- `--style report` is now ambiguous — requires backward compat disambiguation logic
- Existing `report/hottopic` → maps to `news/flash`; `report/topic` → maps to `trade-ideas/community`

## Backward Compatibility

`--style report` with disambiguation: analysis < 30% + no CTA → `news`; action bridge present → `trade-ideas`. `--scene hottopic` → `news/flash`; `--scene topic` → `trade-ideas/community`.

---
name: constraint-enforcement-audit
type: diagnosis
skill: jp-style-optimizer
version_assessed: 5.2.0
date: 2026-04-29
target_version: 6.0.0
---

# Constraint Enforcement Audit (v6.0.0 Boost)

## Red Line Classification (v5.2.0: RL-1 through RL-12)

| Red Line | Stakes | Mechanically Checkable | Current Axis | Do Mechanism | Enforcement |
|----------|--------|------------------------|--------------|--------------|-------------|
| RL-1: Term lock | HIGH — financial terms legally significant | Yes — scan output for each listed term | **Think+Do** | Step 2 term list → Step 5 verification against list | ✓ Do |
| RL-2: Information injection | HIGH — adds claims not in source | Partial — scan for numbers/named entities/causal claims | **Think+Do** | Step 5 explicit scan (a) numbers (b) named entities (c) causal claims; flag with ⚠ RL-2 | ✓ Do |
| RL-3: No subjective in 情報分析 | HIGH — breaks register | Yes — grep for 思います|感じます patterns | **Think+Do** | Step 5 explicit grep; state「主観表現なし: ✓」 | ✓ Do |
| RL-4: Scene hard char limits | HIGH — platform hard limits | Yes — count characters per field | **Think+Do** | Step 5 per-field count; RL-4 table enforced; compression rules if over | ✓ Do |
| RL-5: Disclosure register purity | HIGH — breaks formal register | Yes — grep for です|ます | **Think+Do** | Step 5 explicit scan; state「です/ますなし: 確認済み」 | ✓ Do |
| RL-6: Translation deflection | Medium | Yes — detect input language | **Think+Do** | Step 1 language gate; returns delegation message | ✓ Do |
| RL-7: No double negatives | Medium | Yes — pattern match 〜ないわけではない | **Think+Do** | Step 5 explicit scan; state finding | ✓ Do |
| RL-8: No noun stacking | Medium | Yes — count consecutive nouns | **Think+Do** | Step 5 explicit scan; state finding | ✓ Do |
| RL-9: Unattributed numbers in 情報分析 | HIGH — report credibility | Yes — scan for bare numbers without attribution | **Think+Do** | Step 5 explicit; state「要出典: [数値]」or 「未出典数値なし: ✓」 | ✓ Do |
| RL-10: No passive stacking | Low | Yes — count 〜される|〜られる per sentence | **Think+Do** | Step 5 explicit scan; state finding | ✓ Do |
| RL-11: No register mixing | HIGH — register purity | Partial — 4 pattern checks | **Think+Do** | Step 5 explicit scan; state「文体統一: ✓」; topic exceptions documented | ✓ Do |
| RL-12: Marketing CTA | HIGH — conversion loss | Yes — scan for action verb | **Think+Do** | Step 5 explicit; state「CTA確認: ✓」or flag + revise | ✓ Do |

## Enforcement Ratio

**Current v5.2.0**: 12/12 = **100%** (all constraints have Do mechanisms via Step 5 inline verification)

This is a significant improvement from the pre-v4.0.0 state (0/6 = 0%). All 12 constraints are enforced via the explicit inline verification block in Step 5.

## Top 3 Highest-Stakes Think-Only Constraints

All current constraints have Do mechanisms, but the following have **partial Do enforcement** (the Do check can produce false negatives):

1. **RL-2 Information injection** — The scan covers (a) numbers, (b) named entities, (c) causal claims. However, subtle injection (e.g., reframing that changes implication without adding explicit claims) is Think-only. Highest stakes: legal documents and report content.

2. **RL-11 Register mixing (pattern 4: tone markers)** — The check for 「！」in press/legal/report/support is mechanical. However, more subtle register mixing (e.g., marketing-style enthusiasm words in report output that don't trigger the explicit markers) remains Think-only.

3. **RL-1 Term lock** — The verification checks that listed terms appear in output, but cannot detect whether the term's grammatical role or contextual meaning has been distorted. The term 「当期純利益」could appear unchanged but be placed in a syntactically misleading position.

## v6.0.0 Constraint Updates Required

### RLs that reference old style names (must update):

| RL | Current Reference | v6.0.0 Update |
|----|-------------------|----------------|
| RL-3 | 「情報分析 (report/press/deck/hottopic/topic)」 | Change to 「news (flash/wrap/earnings/indicator/digest/alert) + trade-ideas/theme」 |
| RL-4 hard limits table | `marketing/sns`, `marketing/push`, etc. | Change to `campaign/`, `trade-ideas/` etc. as appropriate |
| RL-9 | 「情報分析 scenes (report/press/deck/hottopic/topic)」 | Change to news T1 scenes + trade-ideas T1 scenes |
| RL-11 | Lists `press/legal/report/support` in tone marker prohibition | Change to reflect new T1 style names |
| AC-8 | References `report/hottopic` | Change to `news/flash` |

### New RLs needed for v6.0.0:

| Proposed RL | Style Scope | Type |
|-------------|------------|------|
| RL-13: trade-ideas dual-register exception | trade-ideas only | RL-11 exception clause |
| RL-14: campaign deadline mandate (CA-1) | campaign only | New hard constraint |
| RL-15: compliance zero promotional tone (C-1) | compliance only | Mechanical (grep for 「！」, 「今すぐ」) |

**Alternative approach (recommended)**: Rather than multiplying global RLs, encode campaign/trade-ideas/compliance specific constraints within the T1 style definition in SKILL.md (parallel to how RL-12 already applies only to `marketing`). Keep global RLs truly global (RL-1 through RL-12) and add T1-scoped additive constraints in the routing table.

## ADR Gap (Phase 1.9 → Phase 2.1)

Three major v6.0.0 architectural decisions require ADR records:

| Decision | Files Affected | Priority |
|----------|----------------|----------|
| legal+support → compliance merger | SKILL.md, style-guide.md, case-library.md | HIGH |
| news/report split (analysis % boundary) | SKILL.md, style-guide.md | HIGH |
| RL-11 exception for trade-ideas dual-register | SKILL.md | Medium |

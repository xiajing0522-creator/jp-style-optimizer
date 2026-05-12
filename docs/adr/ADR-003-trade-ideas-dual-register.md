---
id: ADR-003
title: RL-11 exception for trade-ideas section-level dual register
date: 2026-04-29
status: accepted
deciders: jp-style-optimizer v6.0.0 redesign
affects: SKILL.md (RL-11), references/trade-ideas-guide.md
---

# ADR-003: RL-11 Exception for trade-ideas Dual Register

## Context

RL-11 prohibits mixing だ/である体 and です/ます within the same output. This is correct for all styles except `trade-ideas`.

`trade-ideas` content in Japanese financial media (楽天証券マーケット情報, moomoo証券コミュニティ, 野村証券市場見通し) consistently uses a dual-register pattern:
- **Analysis section**: だ/である体 (客観的分析体 — consistent with news/report register)
- **Reader-action section**: です/ます体 (読者への提案 — engagement促進)

This is not register mixing in the prohibited sense (RL-11 targets incoherent mixing). It is **section-level register differentiation**, a documented pattern in Japanese financial media.

Example:
```
【市場分析】
米国10年債利回りが4.5%を上回った。これを受け、ドル/円は151円台まで上昇している。（だ/である体）

この動きに注目しています。ドル建て資産をお持ちの方は、為替リスクをご確認ください。（です/ます体）
```

## Decision

Add explicit exception to RL-11:

> **RL-11 trade-ideas exception**: In `trade-ideas` output, section-level register mixing is permitted when: (1) the analysis section uses だ/である throughout; (2) the reader-action section uses です/ます throughout; (3) mixing does not occur within a single paragraph. State「デュアルレジスタ: 分析=だ/である ✓ / 読者=です/ます ✓」in verification block.

## Scope

This exception applies ONLY to `--style trade-ideas`. All other styles remain under the full RL-11 prohibition.

## Consequences

**Positive:**
- trade-ideas output matches authentic Japanese financial media register
- RL-11 remains strict for all other T1 styles

**Negative:**
- RL-11 now has two behaviors — must be clearly documented to avoid mis-application
- Step 5 verification requires a trade-ideas-specific check (dual-register state report)

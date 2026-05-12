---
name: domain-research
type: diagnosis
skill: jp-style-optimizer
version_assessed: 5.2.0
date: 2026-04-29
target_version: 6.0.0
---

# Domain Research Summary (v6.0.0 Boost)

Full per-style research documents are in `build/domain-research-*.md`. This file provides the synthesis-ready summary and expert-vs-skill workflow mapping.

---

## Sources by Style (≥ 5 entries)

| # | Style | Source File | Key References |
|---|-------|------------|----------------|
| 1 | campaign | build/domain-research-campaign.md | 楽天証券キャンペーンLP, SBI証券「新規口座開設特典」, moomoo証券アプリ通知, 各社メルマガ |
| 2 | trade-ideas | build/domain-research-trade-ideas.md | 楽天証券「マーケット情報」, moomoo証券「ホットトピック」, 野村証券「市場見通し」, SBI証券「テーマ株」 |
| 3 | news | build/domain-research-news.md | 日経電子版, NHK経済ニュース, Reuters JP, Bloomberg JP, 共同通信 |
| 4 | product | build/domain-research-product.md | SBI証券「操作ガイド」, 楽天証券「使い方ガイド」, moomoo証券YouTube, マネックス証券「ツール」 |
| 5 | compliance | build/domain-research-compliance.md | 金融庁「ディスクロージャー実務指針」, 金融商品取引法第37条の3, 日本証券業協会「広告指針」, 野村証券サポートページ |

---

## Expert Workflow vs. Skill Workflow Mapping

### campaign (v5.2.0 gap: ~80% uncovered)

| Expert Phase | Alloc | v5.2.0 Coverage | Gap |
|---|---|---|---|
| Incentive/特典設計 | 30% | `marketing/event` covers structural template only | MISSING: lifecycle, 特典具体化, 金額表現ルール |
| CTA stage alignment (Cold/Warm/Hot) | 20% | Segment feature covers psychology, not CTA temperature | PARTIAL |
| Lifecycle sequencing (launch→remind→lastday→result) | 25% | Not modeled | MISSING |
| Legal compliance (景品表示法, 金商法広告) | 15% | Not explicitly modeled for campaign | MISSING |
| Brand consistency across lifecycle | 10% | Not modeled | MISSING |

### trade-ideas (v5.2.0 gap: ~100% uncovered — entirely new)

| Expert Phase | Alloc | v5.2.0 Coverage | Gap |
|---|---|---|---|
| Market timing & speed (速報性) | 25% | Not modeled | MISSING |
| Analysis-to-action bridge | 30% | `report` prohibits CTA — opposite behavior | MISSING |
| Dual-register (分析:だ/である + 読者:です/ます) | 15% | RL-11 prohibits this mixing | CONFLICT — needs RL-11 exception |
| Investment disclaimer (投資助言非該当) | 20% | `legal/disclaimer` exists but separate style | PARTIAL |
| Risk/opportunity balance (両面提示) | 10% | Not modeled | MISSING |

### news (v5.2.0 gap: ~30% — covered by `report` but imprecisely)

| Expert Phase | Alloc | v5.2.0 (`report`) | Gap |
|---|---|---|---|
| Fact-first mandatory structure | 40% | `report` allows 背景先行 | PARTIAL — needs strict enforcement |
| Zero analysis (主観ゼロ) / analysis cap (≤30%) | 35% | RL-3 covers subjective; `report` allows analysis | PARTIAL — analysis cap not explicit |
| Attribution (出典) | 15% | RL-9 present | OK |
| Timeliness annotation (時間属性必須) | 10% | Not modeled | MISSING |
| CTA absolute prohibition | required | Present in `report` | OK |

### product (v5.2.0 gap: ~25% — mostly covered)

| Expert Phase | Alloc | v5.2.0 | Gap |
|---|---|---|---|
| Feature→Benefit mandatory pairing | 40% | Present in `product/detail` | OK |
| Terminology onboarding | 15% | Not in explicit RL | MISSING |
| Scannability (箇条書き/表構造) | 20% | Not modeled | MISSING |
| release/onboard/compare scenes | 25% | 3 scenes not modeled | MISSING |
| CTA level calibration (optional, low-commitment) | 10% | RL-12 requires CTA for marketing; conflict | CONFLICT |

### compliance (v5.2.0 gap: ~20% — legal+support covered, merger logic missing)

| Expert Phase | Alloc | v5.2.0 | Gap |
|---|---|---|---|
| Legal precision (法的正確性) | 50% | RL-5, disclosure register present | OK |
| Risk/liability language | 30% | disclaimer scene present | OK |
| Precaution hedge (正確性保証構文) | 10% | Not modeled | MISSING |
| Structural completeness gate | 10% | Not enforced | MISSING |
| Cross-reference (FAQ末尾にdisclaimer付加等) | recurring | Separate T1 blocks this | MISSING — merger solves this |

---

## Cross-Disciplinary Findings

| Finding | Source Domain | Application |
|---------|--------------|-------------|
| Lifecycle messaging architecture | Direct marketing / email | campaign 4-phase scene design |
| Dual-register in financial media | 日経, Bloomberg JP | trade-ideas RL-11 section-level exception |
| Analysis-to-action bridge (% threshold) | CFA Institute content standards | news/trade-ideas distinction at 30% analysis cap |
| Precaution hedge before disclaimer | Legal communication best practice | compliance C-5 constraint |
| F→B mandatory pairing (not optional) | SaaS product marketing | product PC-1 as hard constraint |
| Zero promotional tone as compliance anchor | 金融庁 guidance | compliance C-1 unifying all 5 scenes |

---

## Key Constraints by Style (v6.0.0 additions)

| Style | Count | Core Constraints |
|-------|-------|-----------------|
| campaign | 8 (CA-1–8) | 期限明示必須, 条件透明性, 特典具体化, 金額表現, CTA stage alignment, lifecycle一貫性, multi-state整合, 煽り適正化 |
| trade-ideas | 8 (TI-1–8) | 投資助言非該当, 推測表現義務化, データ出典, 市場タイミング, 行動橋渡し設計, リスク両面提示, 免責文言, 主観排除 |
| news | 7 (NC-1–7) | 事実先出し, 数値完全保持, 主観ゼロ, 時間属性必須, CTA禁止, 出典処理, レジスタ純度 |
| product | 8 (PC-1–8) | F→B必須ペア, 専門用語初出説明, 誇張禁止, CTA任意, 1アクション/1ステップ, スキャナビリティ, 能動態優先, 数値具体化 |
| compliance | 7 (C-1–7) | 宣伝性ゼロ, 術語完全保持, レジスタ一貫性, リスク責任言語, 情報正確性保証構文, 法的フレーミング, 構造完全性 |

---
name: marketing-sample-eval
type: diagnosis
skill: jp-style-optimizer
version: 5.1.0
date: 2026-04-28
source: edm_data.json (moomoo win-back campaign EDM, S10/S11)
---

# Marketing Sample Evaluation — jp-style-optimizer v5.1.0

## Methodology

6 real samples extracted from `edm_data.json`. For each:
1. **Source** (cn field) = draft Japanese copy
2. **Human localization** (loc field) = production-quality output by native localizer
3. **Skill simulation** = expected output if current v5.0.0 workflow applied to source
4. **D1–D8 scoring** per marketing-quality-rubric.md
5. **Gap identification** where skill output < human localization

---

## S1 — Greeting (edm scene)

**Source:** 「moomooをご利用の皆様へ」

**Human loc:** 「moomoo証券をご利用の皆様へ」

**Skill simulation:** The skill should catch this via Shared Constraint "Securities brand suffix in body copy" + Swipe Pattern `moomoo → moomoo証券`. Expected output: 「moomoo証券をご利用の皆様へ」

**Score:**

| D1 | D2 | D3 | D4 | D5 | D6 | D7 | D8 | Total |
|----|----|----|----|----|----|----|----|----|
| 5 | 5 | 5 | N/A | N/A | 4 | 5 | 5 | 29/30 (adj) |

**Gap:** None — this pattern is fully captured in v5.0.0 Swipe Patterns and Shared Constraints. Skill output should match human loc exactly.

---

## S2 — Introduction (edm scene)

**Source:**
「お久しぶりです。お戻りを心よりお待ちしておりました。
これまでのご利用に感謝申し上げます。moomooはこの間も機能改善を重ね、より快適な投資体験をお届けできるよう進化してきました。
日頃のご信頼への感謝として、専属特典をご用意しました：株式キャッシュバック／分配金利回り上乗せクーポン／手数料優待カード（内容はページ表示に準じます）。この特典とともに、今こそ資産成長の旅を再開しませんか。」

**Human loc:**
「いつもmoomoo証券をご利用いただきありがとうございます。
moomoo証券では、より快適にお取引いただけるよう、機能改善とサービス向上を重ねてまいりました。
この度、皆さまへの日頃の感謝を込めて「取引再開の特典」をご用意しました。
株式キャッシュバック券、MMF利回りアップ券、取引手数料優待カードの特典をプレゼント！内容の詳細は、キャンペーンページをご確認ください。
この機会に、moomooでのお取引を再開しませんか？」

**Skill simulation analysis:**

The skill should catch:
- `お久しぶりです` → `いつもmoomoo証券をご利用いただきありがとうございます` (Swipe Pattern + Win-back opening constraint) ✓
- `moomoo` → `moomoo証券` (brand suffix) ✓
- `株式キャッシュバック` → `株式キャッシュバック券` (reward terminology) ✓
- `分配金利回り上乗せクーポン` → `MMF利回りアップ券` (reward terminology) ✓
- `手数料優待カード` → `取引手数料優待カード` (reward terminology) ✓

Potential misses:
- **「資産成長の旅」→ more concrete phrasing**: The metaphorical「資産成長の旅」is not in any Swipe Pattern. Human loc dropped it entirely, replacing with direct CTA 「moomooでのお取引を再開しませんか？」. The skill has no explicit rule against metaphorical marketing language in EDM body.
- **「専属特典をご用意しました：」→「「取引再開の特典」をご用意しました。」**: The human localizer gave the offer a named wrapper (取引再開の特典). This naming convention is not captured.
- **Structural reorganization**: Human loc broke the long paragraph into shorter, more scannable segments. The skill's edm structure guidance focuses on three-section structure (subject/preheader/body) but doesn't specify body paragraph segmentation.

**Score:**

| D1 | D2 | D3 | D4 | D5 | D6 | D7 | D8 | Total |
|----|----|----|----|----|----|----|----|----|
| 5 | 4 | 5 | 3 | 4 | 3 | 3 | 4 | 31/40 |

**Gaps identified:**
1. **GAP-S2a**: No rule against metaphorical/abstract benefit language in EDM body (「資産成長の旅」should become concrete action language). → Need Swipe Pattern or EDM constraint.
2. **GAP-S2b**: No guidance on offer naming convention (wrapping offers in「」brackets with a descriptive name). → Need EDM body structure enhancement.
3. **GAP-S2c**: EDM body paragraph segmentation guidance missing — body should be broken into short scannable blocks, not dense paragraphs. → Need EDM Checkpoint item.

---

## S3 — Title / Section Header (edm/banner scene)

**Source:** 「チャンス密集中の市場へ、特典付きで再スタートしませんか」

**Human loc:** 「取引を再スタートして、変動の市場を捉えませんか？」

**Skill simulation:** The skill should catch `チャンス密集中` → `変動の市場` via Swipe Pattern (added in v4.2.1). Expected output should replace the subjective market framing with objective description per "Market context copy in titles" constraint.

However: the skill would likely produce something like「変動の市場へ、特典付きで再スタートしませんか」— preserving「特典付きで」. The human loc dropped「特典付きで」and restructured to be more action-forward:「取引を再スタートして」(action first) +「変動の市場を捉えませんか？」(objective + capture framing).

**Score:**

| D1 | D2 | D3 | D4 | D5 | D6 | D7 | D8 | Total |
|----|----|----|----|----|----|----|----|----|
| 5 | 5 | 5 | 4 | 4 | 3 | 3 | 4 | 33/40 |

**Gaps identified:**
1. **GAP-S3a**: Title rewriting guidance lacks "action-first" principle. Human localizer puts the user's action (「取引を再スタートして」) before the market context. Current style-guide says "numbers and percentages placed at start" for banner but has no equivalent action-first rule for EDM/LP titles. → Need title rewriting pattern.
2. **GAP-S3b**: No "capture/seize" framing pattern for market context. Human loc uses「捉える」(capture/seize) which is more empowering than「再スタートしませんか」(restart). → Need Swipe Pattern: passive benefit framing → active market capture framing.

---

## S4 — Market Context Module (edm/lp scene)

**Source (S10 row 11, market section):**
「最近の市場はどうなっている？
🛡️ 地政学リスクが再燃：米・イラン停戦交渉が長期化し、リスク回避ムードが強まっています。金・原油のボラティリティが拡大、ヘッジ需要が急回復中です。
📈 利下げ観測でバリュエーション修復：...
💻 テック・半導体に資金回帰：AI計算資源と半導体セクターへの資金流入が再加速。...
🚀 宇宙産業の材料が続々：...
相場が急速にローテーションし、チャンスが密集している今こそ、仕込みのタイミングです。」

**Human loc:** [obj] — rich formatted object; not available as flat text in edm_data.json. Based on the sheet10 analysis, the localized version likely maintained the emoji+topic structure but applied these corrections:
- Removed subjective urgency closing (「チャンスが密集」→ objective framing)
- Used 「資金回帰」(sector rotation reframing per case-library.md)
- Standardized emoji bullet structure

**Skill simulation analysis:**

The skill should catch:
- `チャンスが密集` → objective framing (Market context in titles constraint) ✓
- `テック・半導体に資金回帰` already uses correct term (case-library.md) ✓
- Emoji bullet structure matches moomoo voice signature ✓

Potential misses:
- **「仕込みのタイミングです」**: This is subjective urgency copy in what functions as a market context module title/closer. The skill has a rule about titles but not about closing sentences within market context modules.
- **Overall module length**: 4 bullet items totaling ~300 chars. No guidance on whether to compress or preserve in EDM context.

**Score:**

| D1 | D2 | D3 | D4 | D5 | D6 | D7 | D8 | Total |
|----|----|----|----|----|----|----|----|----|
| 5 | 4 | 5 | N/A | 3 | 3 | 4 | 4 | 28/35 (adj) |

**Gaps identified:**
1. **GAP-S4a**: No rule for market context module closing sentences — subjective urgency copy (「仕込みのタイミング」) should follow the same objectivity rule as titles. → Extend "Market context copy in titles" constraint to cover module closers.
2. **GAP-S4b**: No market context module length guidance for EDM. LP has the 4-layer win-back structure, but EDM body doesn't specify how many market insight items are appropriate. → Add EDM-specific market context module guidance.

---

## S5 — CTA (edm scene)

**Source CTA:** [obj] (rich object — likely a button element)
**Human loc CTA:** 「取引を再開」(S10 row 18) / [obj] (S10 row 9, S10 row 14)

**Skill simulation:** For EDM CTA, the skill requires imperative form with action verb ≤15 chars. 「取引を再開」= 5 chars, action verb ✓, well within limit.

However, 「取引を再開」is a noun phrase (missing する). The skill's RL-12 says "specific action verb" — should this be 「取引を再開する」(with する) for full imperative form?

**Score:**

| D1 | D2 | D3 | D4 | D5 | D6 | D7 | D8 | Total |
|----|----|----|----|----|----|----|----|----|
| 5 | 5 | 5 | 4 | 5 | 4 | 4 | 5 | 37/40 |

**Gaps identified:**
1. **GAP-S5a**: CTA form ambiguity — noun phrase CTA (「取引を再開」) vs full verb CTA (「取引を再開する」) not distinguished. In practice, EDM CTA buttons often use abbreviated noun-phrase form. Banner already specifies "noun phrases preferred" but EDM doesn't. → Clarify EDM CTA allows noun-phrase form for button text.

---

## S6 — Full Email Assembly (edm scene)

Assembled from S10 rows 3-18:

**Source email:**
- Subject: 「moomoo証券で取引を再開して特典をゲットしよう！」
- Preview: 「チャンス到来!?取引再開で最大5万円相当の特典！」
- Greeting: 「moomooをご利用の皆様へ」
- Introduction: [S2 source]
- Title: [S3 source]
- Market Context: [S4 source]
- CTA: [S5 source]

**Human loc email:**
- Subject: same (already localized)
- Preview: same
- Greeting: 「moomoo証券をご利用の皆様へ」
- Introduction: [S2 loc]
- Title: [S3 loc]
- Market Context: [obj - formatted]
- CTA: 「取引を再開」

**Full email evaluation — additional observations:**

1. **Subject-to-body coherence**: Subject mentions「特典をゲットしよう」but body uses formal register「ご用意しました」— this is an intentional register gradient (subject casual → body formal) that is standard in Japanese EDM. The skill has no guidance on cross-section register gradient.

2. **Preview complementarity**: Preview adds「最大5万円相当」which doesn't repeat subject. This follows the EDM Checkpoint. ✓

3. **Section transitions**: Human loc uses clear paragraph breaks and 「この度」「この機会に」as transition phrases. Source uses longer flowing text. The skill has no transition phrase guidance.

**Score:**

| D1 | D2 | D3 | D4 | D5 | D6 | D7 | D8 | Total |
|----|----|----|----|----|----|----|----|----|
| 5 | 4 | 4 | 4 | 4 | 3 | 3 | 4 | 31/40 |

**Gaps identified:**
1. **GAP-S6a**: No guidance on cross-section register gradient in EDM (subject can be casual/inviting, body must be formal). → Add EDM Mandatory Constraint.
2. **GAP-S6b**: No transition phrase inventory for EDM body sections. → Add recommended transition phrases to EDM spec.
3. **GAP-S6c**: Overall structural gap — current EDM Checkpoint has 3 items (subject length, preheader non-repetition, CTA length) but misses body structure quality. → Add body Checkpoint items.

---

## Gap Summary

### Critical Gaps (affect multiple samples, structural)

| ID | Gap | Impact | Fix Location |
|----|-----|--------|-------------|
| GAP-S2c | EDM body paragraph segmentation guidance missing | D6, D7 | style-guide.md edm Checkpoint |
| GAP-S6c | EDM Checkpoint lacks body structure items | D6 | style-guide.md edm Checkpoint |
| GAP-S3a | Title rewriting lacks "action-first" principle | D6, D7 | style-guide.md marketing Shared Constraints |
| GAP-S4a | Market context module closers allow subjective urgency | D2, D7 | style-guide.md marketing Shared Constraints |

### Moderate Gaps (single sample, pattern-level)

| ID | Gap | Impact | Fix Location |
|----|-----|--------|-------------|
| GAP-S2a | No rule against metaphorical benefit language in body | D7 | style-guide.md marketing Swipe Patterns |
| GAP-S2b | No offer naming convention (「」bracket naming) | D7, D8 | style-guide.md edm spec |
| GAP-S3b | No active market "capture" framing pattern | D7 | style-guide.md marketing Swipe Patterns |
| GAP-S4b | No market context module length guidance for EDM | D5, D6 | style-guide.md edm spec |
| GAP-S5a | CTA noun-phrase form vs full verb form ambiguity | D4 | style-guide.md edm Mandatory Constraints |
| GAP-S6a | No cross-section register gradient guidance | D3 | style-guide.md edm Mandatory Constraints |
| GAP-S6b | No transition phrase inventory | D7 | style-guide.md edm spec |

### Aggregate Scores (D1–D9)

| Sample | D1 | D2 | D3 | D4 | D5 | D6 | D7 | D8 | D9 | Total | Pass? |
|--------|----|----|----|----|----|----|----|----|----|----|-------|
| S1 | 5 | 5 | 5 | — | — | 4 | 5 | 5 | 3 | 32/35 | ✓ |
| S2 | 5 | 4 | 5 | 3 | 4 | 3 | 3 | 4 | 2 | 33/45 | ✗ (D9<3) |
| S3 | 5 | 5 | 5 | 4 | 4 | 3 | 3 | 4 | 3 | 36/45 | ✓ (borderline) |
| S4 | 5 | 4 | 5 | — | 3 | 3 | 4 | 4 | 3 | 31/40 | ✓ (borderline) |
| S5 | 5 | 5 | 5 | 4 | 5 | 4 | 4 | 5 | 4 | 41/45 | ✓ |
| S6 | 5 | 4 | 4 | 4 | 4 | 3 | 3 | 4 | 2 | 33/45 | ✗ (D9<3) |

**D9 scoring rationale:**
- S1 (greeting): D9=3 — greeting itself is neutral; brand suffix adds trust but no persuasive trigger
- S2 (introduction): D9=2 — source uses company-centric framing (「当社は機能改善を重ね」) and metaphorical benefit (「資産成長の旅」); skill catches terminology but doesn't restructure to reader-centric benefit framing. Human loc scored higher by leading with reader benefit
- S3 (title): D9=3 — after gap fix (action-first rule), the output should lead with action; but still lacks strong emotional trigger
- S4 (market context): D9=3 — emoji bullets create visual interest; sector rotation language is engaging; but closing sentence subjective urgency was a weakness (now fixed)
- S5 (CTA): D9=4 — direct action verb, clear intent, minimal friction
- S6 (full email): D9=2 — aggregation of S2's company-centric intro + weak benefit framing; the email as a whole doesn't build a compelling persuasive arc from open to click

**Weakest dimensions across samples**: D9 (Persuasive Appeal, avg 2.8), D6 (Scene Structure, avg 3.3), D7 (Naturalness, avg 3.7)
**Strongest dimensions**: D1 (Term Integrity, avg 5.0), D3 (Register Consistency, avg 4.8)

**Conclusion**: Term-level constraints (RL-1, RL-11) are well-captured. The main quality gaps are:
1. **D9 Persuasive Appeal** (avg 2.8) — skill corrects terminology and structure but doesn't actively restructure company-centric copy into reader-centric benefit framing. This is the #1 gap.
2. **D6 Scene Structure** (avg 3.3) — EDM body organization and title rewriting (partially addressed by v5.1.0 gap fixes)
3. **D7 Naturalness** (avg 3.7) — phrasing conventions and transition quality

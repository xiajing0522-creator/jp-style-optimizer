# CHANGELOG — jp-style-optimizer

Format: narrative summary for major changes + Keep a Changelog item list.

---

## [5.2.0] — 2026-04-28

### Cross-style optimization: D9 per-style, Business Goals, quality rubric expansion

Major release extending optimization from marketing-only to all 5 Tier 1 styles. Adds per-style D9 effectiveness dimension, Business Goals for all 20 scenes, and deep spec improvements for report, product, legal, and support styles. Addresses marketing D9 gap (avg 2.8) with reader-centric reframing.

#### Added
- **D9 — Persuasive Appeal** (marketing): 5 sub-criteria + per-scene emotional triggers. Pass criteria: ≥34/45 branded, D9≥3 gate.
- **D9 per-style definitions** in `diagnosis/cross-style-quality-rubric.md`: Report=Analytical Authority, Product=Comprehension & Confidence, Legal=Regulatory Precision & Risk Completeness, Support=Resolution Efficiency & User Reassurance. Pass thresholds: Report/Product ≥30/40, Legal/Support ≥26/35.
- **`diagnosis/cross-style-quality-rubric.md`** (new): Consolidated D1–D8 shared + D9 per-style scoring, pass criteria table, D4 adaptations per style.
- **14 Business Goals**: One per non-marketing scene (report, press, deck, hottopic, topic, short, detail, manual, script, disclosure, terms, disclaimer, faq, guide). Each defines conversion objective and key quality levers.
- **Report hedging confidence gradient**: 3 levels (High: 見込み/見通し, Medium: と見られる/と考えられる, Low: 可能性がある/リスクがある). Added to report T1 Shared Constraints + 4 new Swipe Patterns (だろう→見込み, unattributed→attributed, vague→precise hedge, assertion→risk framing).
- **Report Checkpoints expanded**: 2→5 items (added だ/である consistency, zero first-person, attribution check).
- **FAQ Rewrite Patterns** (3 new): 仕様です→敬語, 待って→恐れ入ります, 調べて→確認いただけます.
- **Guide Rewrite Patterns** (3 new): 別の部署→窓口案内, 書類送って→所定書類ご郵送, 未完了→処理中ご連絡.
- **Guide constraints**: Processing time (通常X営業日以内), branching procedures (条件→ルート分岐).
- **Product Swipe Patterns** (4 new): 可能となっております→できます, 多彩な→具体列挙, セキュリティ万全→具体措置, 簡単→数字化.
- **Manual constraints**: UI element「」brackets, completion confirmation (最終ステップで成功確認), error recovery in cautions.
- **Shared Constraint: Reader-centric reframing** — Company-subject sentences reframed to reader-benefit subject. 3 new Swipe Patterns.
- **Layer 3 marketing reader-centricity check** in SKILL.md Step 4.
- **Product enhancements**: Multi-feature ordering rule (strongest first), PASONA compressed, number-first rule for short, detail Rewrite Patterns (2) + expanded Checkpoint (2→4), script hook-opening rule.
- **Report enhancements**: Press 5W Rewrite Pattern, deck multi-bullet ordering rule.
- **Legal enhancements**: Disclaimer non-advice Rewrite Pattern + Checkpoint item, terms register verification Checkpoint item.
- **Support enhancements**: FAQ multi-topic splitting rule, guide caution Rewrite Pattern (審査時間).
- **Manual**: Caution Rewrite Pattern (審査には通常3営業日).

#### Changed
- **Legal T1**: Register defaults clarified — disclosure=だ/である exclusively, terms/disclaimer=です/ます.
- **Support T1**: Compressed Rewrite Patterns from 5→3 rows (scene-level patterns now cover 手続きの説明です and エラーです).
- **style-guide.md compressed**: Topic examples condensed, Register Mixing section reduced to quick reference, Routing Inference Table tabularized, marketing Swipe Patterns merged. Net result: 5,491→5,191 words despite ~700 words of new content added.

#### Token budget
- SKILL.md: ~2,450 words
- style-guide.md: ~5,191 words (compressed from 5,491; soft ceiling 5,000)
- cross-style-quality-rubric.md: ~650 words (diagnosis file, not always-loaded)

---

## [5.1.0] — 2026-04-28

### Marketing deep optimization: Business goals, quality rubric, real sample evaluation

Release introducing per-scene business goal definitions, a quantifiable 8-dimension quality scoring rubric, and real sample comparison testing using production EDM data. 11 gaps identified and fixed in marketing style specifications.

#### Added
- **Business Goal fields** for all 6 marketing scenes (lp/sns/event/push/edm/banner) in style-guide.md — defines conversion objective and key quality levers per scene.
- **`diagnosis/marketing-quality-rubric.md`**: 8-dimension scoring framework (D1 Term Integrity through D8 Brand Fit), each scored 1–5 with explicit criteria. Pass criteria: total ≥30/40, hard gates on D1+D2.
- **`diagnosis/marketing-sample-eval.md`**: 6 real sample evaluations (S1–S6) from moomoo win-back EDM campaign comparing skill output vs human localization. Identifies 11 gaps with D1–D8 scoring.
- **4 new Swipe Patterns**: metaphorical→concrete benefit language, subjective→objective closers, context-first→action-first titles, unnamed→bracket-named offers.
- **3 new Shared Constraints**: action-first title construction, no metaphorical benefit language in body, market context objectivity extended to module closers (not just titles).
- **5 new EDM Mandatory Constraints**: register gradient (casual subject OK / formal body), offer bracket naming, transition phrases, body paragraph segmentation, market context module length limit (2–3 items).
- **2 new EDM Checkpoint items**: body paragraph segmentation, offer bracket naming.
- **EDM CTA clarification**: noun-phrase form acceptable for button text (not only full verb form).

#### Token budget
- SKILL.md: ~2,400 words (unchanged)
- style-guide.md: ~4,950 words (99% of 5,000-word soft ceiling — includes Business Goals + gap fixes)
- marketing-quality-rubric.md: ~650 words (diagnosis file, not always-loaded)
- marketing-sample-eval.md: ~1,200 words (diagnosis file, not always-loaded)

---

## [5.0.0] — 2026-04-28

### Layer 3 foundation: Brand voice matching, case library, eval suite expansion

Major release introducing brand-specific voice matching (Layer 3 foundation), expanding the behavioral eval suite from 5 to 13 tests, fixing Cross-Style Red Line Summary inconsistencies, and housekeeping stale diagnosis files.

#### Added
- **Step 3.5 — Brand Voice Match**: Optional workflow step that loads brand-specific voice constraints from `references/case-library.md` when input contains a listed brand name. Adds brand voice signature to Step 4 transform and brand benchmark comparison to Step 6 naturalness check.
- **`references/case-library.md`**: New conditional-load reference file with 4 brand voice entries:
  - 野村証券 (Nomura): hedging hierarchy (3 levels), attribution rules, anti-patterns
  - 楽天証券 (Rakuten): なら構文, social proof numbers, hot-stage CTA
  - SBI証券 (SBI): zero abbreviations, だ/である exclusive, conditional precision
  - moomoo証券: brand suffix, win-back formula, reward terminology, sector rotation reframing, emoji bullet structure, asset-class CTA customization
- **Step 6 Proxy check 4 — Brand voice match**: Compares output against brand benchmark excerpt and anti-patterns when Step 3.5 identified a brand. States「ブランド適合: [brand] ✓」.
- **8 new behavioral eval tests** (T6–T13): marketing/push (RL-1 vs RL-4 priority), marketing/edm (three-section structure), marketing/banner (ultra-short copy), marketing/sns (140-char + emoji), report/topic Variant A (8-part + register exceptions), report/topic Variant B (UGC curation + disclaimer), product/script (spoken rhythm), product/manual (numbered steps). Test priority tiers added.
- **Routing Inference Table** moved to style-guide.md (was inline in SKILL.md) — reduces SKILL.md token load.

#### Changed
- **Cross-Style Red Line Summary** (style-guide.md): Fixed 4 scope inconsistencies — RL-3 now includes hottopic/topic, RL-4 expanded to all 6 limit scenes, RL-9 includes hottopic/topic with exception note, RL-12 includes edm/banner with push exemption note.
- **SKILL.md backward compatibility table**: Compressed from 7-row table to single-line summary (–40 words).
- **SKILL.md keyword inference list**: Moved to style-guide.md, replaced with pointer (–150 words).
- **References table**: Added case-library.md entry with conditional load description.

#### Archived
- 4 stale diagnosis files (synthesis.md, structural-audit.md, platform-check.md, constraint-enforcement-audit.md) marked with archive headers — pre-v4.0.0 findings, resolved.
- token-audit.md rewritten with current measurements (SKILL.md: ~2,400w at 80% budget; style-guide.md: ~4,600w at 92% ceiling).

#### Token budget
- SKILL.md: ~2,400 words (80% of 3,000-word budget — net reduction from compression)
- style-guide.md: ~4,600 words (92% of 5,000-word soft ceiling — includes routing inference table)
- case-library.md: ~500 words (conditional load, not counted in always-loaded budget)

---

## [4.6.0] — 2026-04-28

### Consolidated: Scene expansion, topic variants, Push/EDM/Banner support

Covers changes from v4.3.0 through v4.6.0 that were not individually documented. These releases expanded the scene catalog from 14 to 20 scenes, added the topic scene's dual-variant structure, and extended RL-4 and RL-12 scope to cover the new marketing scenes.

#### Added
- **6 new scenes**: push, edm, banner, manual, script, topic — bringing total from 14 to 20
- **topic scene**: Variant A (話題シェア, 8-part structure) and Variant B (人気投稿まとめ, 6-part structure with fixed transition sentence and mandatory disclaimer)
- **RL-11 topic exceptions**: (a) です/ます体 for topic body (not だ/である); (b) casual/タメ口 in 投稿例 section; (c) invitation form (〜しよう！) in push subtitle
- **RL-4 expanded to 6 scenes**: marketing/sns (≤140), marketing/push (title≤20/body≤60), marketing/edm (subject≤40/preheader≤80/CTA≤15), marketing/banner (main≤15/sub≤25/CTA≤8), report/hottopic (≤140), report/deck (≤25/bullet)
- **RL-12 expanded to 5 scenes**: lp, sns, event, edm, banner (push exempt — uses リンク先示唆)
- **RL-1 vs RL-4 priority rule**: For push scene, character limits take precedence over term integrity when in conflict
- **Push brand injection prohibition**: Brand suffix rule only applies when source text already mentions the brand
- **AC-4 updated**: Per-scene character count format in verification block (multi-field for push/edm/banner, total for sns/hottopic, per-bullet for deck)

#### Changed
- Step 5 verification expanded with per-scene character count formats and RL-12 push exemption logic
- Cross-Style Red Line Summary in style-guide.md updated: RL-3 scope to include hottopic/topic, RL-4 scope to all 6 limit scenes, RL-9 scope to include hottopic/topic with exception, RL-12 scope to include edm/banner with push exemption

#### Token budget
- SKILL.md: ~2,480 words (83% of 3,000-word budget)
- style-guide.md: ~4,500 words (90% of 5,000-word soft ceiling)

---

## [4.2.2] — 2026-04-27

### LP-derived patterns: brand name scope, win-back LP structure, multi-state consistency

This patch codifies 3 structural and naming patterns extracted from analysis of the live moomooおかえりキャンペーン LP (invest.jp.moomoo.com/churnrecall). The LP contained a copy violation (「エヌビディアの有力な対抗馬」in an AMD stock description — the existing brand name convention rule applied but was scoped only to campaign headlines), and introduced two structural patterns not previously captured: the 4-layer win-back LP body structure, and cross-state register consistency for multi-state CTA modules.

#### Added
- **Brand name convention scope clarified**: Rule now explicitly covers all marketing copy locations — campaign headlines, LP body text, stock/investment content descriptions, and market commentary. AMD in stock descriptions (e.g., AMD as NVIDIA competitor) must use English, not katakana form.
- **Win-back / Re-engagement LP Structure** (added to `marketing/lp` T2 section): 4-layer body structure for チャーンリコール campaigns — (1) re-engagement hook, (2) market context module (Pathos+Logos dual trigger), (3) 特典詳細, (4) 信任背書 (trust anchor). Source: moomooおかえりキャンペーン LP.
- **Multi-state copy consistency** (added to `marketing/event` Checkpoint): Multi-state copy modules (参加前/達成/未達成/期限切れ) must maintain consistent register across all states — no tone shift between states of the same module.
- **1 Swipe Pattern row** added: エヌビディアの有力な対抗馬（株式説明・市況コメント内）→ NVIDIAの有力な対抗馬

#### Token budget
- SKILL.md: ~1,950 words (no change — all additions in style-guide.md)

---

## [4.2.1] — 2026-04-27

### Localization patterns: EDM win-back email conventions and reward terminology

This patch codifies 5 additional localization patterns extracted from comparative analysis of draft vs. human-localized copy in sheets 10 (EDM_可用悬赏≥500) and 11 (EDM_可用悬赏＜500) of JP-26Q2流失召回活动更新WBS. The source copy in these sheets was already in Japanese (not Chinese), so the comparison is draft Japanese vs. localization Japanese — surfacing brand voice and naming conventions not previously captured.

#### Added
- **Shared Constraint: Securities brand suffix in body copy** — Body copy must use full brand form (e.g.,「moomoo証券」not「moomoo」). Applies to greetings, CTAs, and self-references in email body.
- **Shared Constraint: Win-back / re-engagement email opening** — Must open with「いつも[ブランド名]をご利用いただきありがとうございます」. Colloquial openers (「お久しぶりです」「お戻りを心よりお待ちしておりました」) are prohibited — inconsistent with securities brand voice.
- **Shared Constraint: Reward product terminology** — Standard names: 株式キャッシュバック→株式キャッシュバック**券**; 分配金利回り上乗せクーポン→**MMF利回りアップ券**; 手数料優待カード→**取引手数料優待カード**.
- **Shared Constraint: Market context copy in titles** — Avoid subjective framing (「チャンス密集中」) in section/module titles. Use objective descriptions (「変動の市場」「市場の動向」). Benefit/urgency copy belongs in body, not titles.
- **6 Swipe Pattern rows** added: moomoo→moomoo証券, お久しぶりです→いつも〜ご利用いただきありがとうございます, 株式キャッシュバック→券, 分配金利回り上乗せクーポン→MMF利回りアップ券, 手数料優待カード→取引手数料優待カード, チャンス密集中→変動の市場.

#### Token budget
- SKILL.md: ~1,950 words (no change — all additions in style-guide.md)

---

## [4.2.0] — 2026-04-27

### Localization patterns: marketing/event compliance and brand conventions

This release codifies 6 localization patterns extracted from comparative analysis of machine-translated vs. human-localized copy across a live securities campaign (sheets 6, 8, 10, 11 of JP-2026入金活動-WBS). The patterns address compliance gaps (prize probability claims, prize amount hedging), brand consistency (Western brand name encoding), and lexical register accuracy (取引 vs ディーリング, 賞品 vs 賞金).

#### Added
- **Shared Constraint: Brand name convention** — Western brands in English characters, not katakana (NVIDIA not エヌビディア). Japanese company names unchanged.
- **Shared Constraint: Prize amount hedging** — Monetary reward values must append「相当」(e.g.,「最大5万円相当」). Required for compliance in prize/reward campaigns.
- **Shared Constraint: Probability claims** — Avoid「100%当選」. Accepted alternatives:「必ずもらえる」/「必ず特典ゲット」for guaranteed-reward framing.
- **Shared Constraint: 取引 vs ディーリング** — Use「取引」in general marketing/event copy; reserve「ディーリング」for derivatives-specific contexts.
- **Shared Constraint: Campaign prize concept** — Use「賞品を山分け」not「賞金プール」in lottery/share-type prize campaigns (賞金 implies cash payment; 賞品 is correct for stock/gift certificates).
- **Shared Constraint: Email subject format** — Push and email subjects use【】bracket format for campaign names.
- **6 Swipe Pattern rows** added to Tier 1 marketing table: エヌビディア→NVIDIA, 賞金プール→賞品を山分け, 100%当選→必ずもらえる/必ず特典ゲット, チャレンジカウントダウン→チャレンジ終了まで, キャンペーンルール→キャンペーンの詳細, ご支援ありがとうございます（終了/拒否通知）→ご理解の程よろしくお願いいたします.

#### Token budget
- SKILL.md: ~1,950 words (no change — constraints added to style-guide.md only)

---

## [4.1.0] — 2026-04-24

### Quality framework: Scene Fit layer and naturalness proxy checks

This release completes the three-layer quality framework: Compliance (binary RL gates) → Scene Fit (Checkpoint X/N score) → Reference Match (proxy-based naturalness check).

Previously, quality evaluation consisted only of binary RL pass/fail checks and an unexplained `改動幅度 X/100` score with no defined calculation method. This release replaces that with structured, auditable evaluation at each layer.

#### Added
- **RL-12**: `marketing / scenes: lp, sns, event` must contain at least one CTA with a specific action verb. Generic「こちら」alone does not satisfy. Hard gate — must revise before delivery.
- **AC-7 updated**: Benefit specificity requirement (a concrete detail: number, feature name, or named outcome). CTA requirement moved to RL-12.
- **Step 5 — Scene Fit check**: After all RL checks, run each scene's Checkpoint from style-guide.md. Report 場面適合: X/N ✓. All items must pass (X = N) before Step 6.
- **Step 6 rewritten**: Three proxy checks replace generic naturalness description:
  - Proxy 1: Cross-register vocabulary leakage (register-specific scan patterns per Tier 1)
  - Proxy 2: Sentence variety (uniform length = mechanical output flag)
  - Proxy 3: Reference comparison against style-guide.md Example for this scene
- **14 Checkpoints rewritten** in style-guide.md: RL duplicates removed from all scene Checkpoints; scene-specific structural items added. Each Checkpoint now contains 3 auditable items independent of RL gates.
- **RL-12 row added** to Cross-Style Red Line Summary in style-guide.md.
- **Buyer-stage CTA alignment** added to `marketing/lp` Checkpoint: cold → warm → hot scale.
- **`diagnosis/behavioral-eval-suite.md`**: 5 regression test cases covering RL-12, RL-11 keigo, routing inference, RL-2 injection resistance, and legal/disclosure Scene Fit.

#### Changed
- **RL-2 operationalized**: Added 3 concrete scan targets — (a) numbers not in input; (b) named entities not in input; (c) causal claims not derivable from input. Each flagged with `⚠ RL-2: [injected content]`.
- **RL-4 scope clarified**: Explicitly scoped to `marketing / scene: sns` (was "marketing/sns" — ambiguous).
- **RL-11 extended to 4 mixing patterns**: (1) verb endings だ/である + です/ます; (2) keigo level: 謙譲語II outside support or plain inside support; (3) modality markers 〜と見られる/〜見込み in marketing output; (4) tone markers「！」/「今すぐ」in press/legal/report/support.
- **Step 5 RL-11 check updated**: Now explicitly scans all 4 mixing patterns.
- **Output Format**: `改動幅度：X/100` removed. `場面適合: X/N ✓` and `自然さ:` added to 検証 block.
- **RL-11 row updated** in Cross-Style Red Line Summary: 4-category scan listed.

#### Token budget
- SKILL.md: ~1,950 words (within 3,000-word always-loaded limit — no layer split needed)

---

## [4.0.0] — 2026-04-24

### Architecture: Two-tier routing + 14 scenes

This was a major structural rework introducing the two-parameter routing system (--style + --scene), expanding from 4 styles to 5 styles × 14 scenes.

#### Added
- **Two-tier routing**: `--style` (Tier 1 register) × `--scene` (Tier 2 structural template)
- **5 Tier 1 styles**: `marketing`, `product`, `report`, `legal`, `support`
- **14 Tier 2 scenes**: `lp`, `sns`, `event`, `short`, `detail`, `manual`, `report`, `press`, `deck`, `disclosure`, `terms`, `disclaimer`, `faq`, `guide`
- **Scene inference rules**: Automatic `--scene` default when only `--style` is specified
- **Backward compatibility**: Old single-flag calls (e.g., `--style formal` → `legal/disclosure`) still work
- **Style + scene inference**: Keyword-to-route mapping for flagless calls
- **RL-7**: No double negatives (〜ないわけではない / 〜なくはない)
- **RL-8**: No noun-phrase stacking (4+ consecutive nouns without particles)
- **RL-9**: 情報分析 unattributed numbers must be flagged with `要出典:`
- **RL-10**: No passive stacking (2+ passive constructions in one sentence)
- **RL-11**: No register mixing (initial version: verb-ending check only — see v4.1.0 for full extension)
- **Step 2**: Term Lock + Source Analysis (2a Term Lock, 2b Information Priority, 2c Dominant Proof)
- **Step 3**: Explicit style + scene routing with stated output
- **Step 4**: Three-layer transform (Structure → Language → Proof & Frame) with Proof-register mapping
- **Step 5**: Inline verification with per-RL and per-scope checks
- **Step 6**: Naturalness check (initial version — see v4.1.0 for proxy check rewrite)
- **style-guide.md**: Full Tier 1 + Tier 2 specifications for all 14 scenes with Checkpoints, Examples, Swipe Patterns, Rewrite Patterns

#### Changed
- Version bumped from 3.x to 4.0.0 (non-backward-compatible routing architecture change)
- SKILL.md completely rewritten; original 4-style workflow replaced

---

## [3.0.0] — (prior)

### Original 4-style skill

Initial version with 4 styles (`formal`, `marketing`, `report`, `sns`), 6 red lines (RL-1 through RL-6), 3 acceptance criteria, and basic post-execution verification. Single-axis routing via `--style` flag.

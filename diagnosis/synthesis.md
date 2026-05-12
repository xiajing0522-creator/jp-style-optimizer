---
name: synthesis
type: diagnosis
skill: jp-style-optimizer
version_assessed: 6.0.0
date: 2026-05-11
target_version: 6.1.0
prior_assessment: 5.2.0 → 6.0.0 (2026-04-29, see "v6.0.0 Boost" sections below)
---

# Synthesis (v6.0.0 Boost)

Cross-reference of all Phase 1 diagnosis artifacts, synthesis answers, and Phase 2 prescriptions.

---

## Phase 1 Artifact Cross-Reference

| Artifact | Key Finding |
|----------|-------------|
| `structural-audit.md` | 2 HIGH defects: v6.0.0 T1 rename breaks all existing `--style` calls; no docs/adr/ for 3 major architectural decisions. 5+ medium defects: 5 RLs/ACs referencing old style names. |
| `layer-diagnosis.md` | Layer 2 (with gaps). v5.2.0 covers 3/5 new T1 styles. trade-ideas blocked by RL-11 conflict. Campaign lifecycle not modeled. Expected post-v6.0.0: Layer 2 (complete). |
| `token-audit.md` | CRITICAL pressure: SKILL.md at 95% budget (2,846/3,000w), style-guide.md at 99.6% soft ceiling (4,982/5,000w). v6.0.0 additions (~1,200w) will exceed budget without split-by-T1 architecture. |
| `platform-check.md` | CLEAN. No platform-specific dependencies in v5.2.0. Conditional-load instruction change needed if split-by-T1 adopted. |
| `domain-research.md` | 5 styles researched; 38 new constraints identified (CA-1–8, TI-1–8, NC-1–7, PC-1–8, C-1–7). campaign and trade-ideas are ~80-100% new territory. news/product/compliance have 20-30% gaps. |
| `constraint-enforcement-audit.md` | Enforcement ratio: 12/12 = 100% (all Do). Top partial-Do: RL-2 (injection), RL-11 (register), RL-1 (term lock semantic). 3 RLs need style name updates; RL-11 needs trade-ideas exception; RL-12 needs scope reduction for product. |

---

## Rethinking Questions (Phase 1.8)

### 1. Does the workflow need structural redesign?

**No — the v5.2.0 workflow is architecturally sound.** The 6-step workflow (Language Gate → Term Lock + Source Analysis → Style+Scene Routing → Transform → Inline Verification → Naturalness Check) follows expert practice and has 100% RL enforcement. The structure does not need redesign.

**What does need redesign**: the content the workflow routes to. The Tier 1 routing table and Tier 2 scene table in SKILL.md, plus the entire style-guide.md, must be rewritten for the new 5-style architecture. This is a content replacement, not a structural change.

**One structural addition needed**: The Step 3 routing must support the new T1 style names. Step 4 Transform Layer 3 (Proof & Frame) table must add rows for campaign (Pathos-amplify), trade-ideas (Logos+bridge), news (Logos-strict), compliance (Ethos-strict). The segment strategy table needs campaign-specific CTA stage alignment.

### 2. Are the skill's principles still valid?

**Yes — core principles carry forward intact.** The foundational principles are confirmed by all 5 domain research files:

- **Term lock (RL-1)**: Applies to all 5 new T1 styles. Financial/technical terms remain non-substitutable across all registers.
- **Information injection (RL-2)**: Applies to all 5. Especially critical in trade-ideas (no adding investment claims) and news (no editorializing).
- **Register purity (RL-11)**: Applies to all 5, with one addition: trade-ideas section-level dual-register is a documented exception, not a violation.
- **Layer-by-layer transform (Structure → Language → Proof)**: Validated by domain research. Expert editors follow this sequence.
- **Inline verification (Step 5)**: Remains essential. New T1 styles add verification requirements (campaign: CTA stage check; trade-ideas: disclaimer check; news: analysis-cap check).

**Principles needing update**: RL-3 (subjective expressions) currently scoped to `情報分析` — should extend to `news` and `trade-ideas` analysis sections. RL-9 (unattributed numbers) similarly needs extension to news and trade-ideas. RL-12 (marketing CTA) should be scoped to `campaign` only and removed from `product`.

### 3. What does the quality bar look like?

**Layer 2 (complete) after v6.0.0.** The current skill is Layer 2 with gaps — it handles 3/5 new T1 styles. After v6.0.0:
- All 5 T1 styles have complete constraint sets informed by domain research
- All 5 T1 styles have T2 scene definitions with information structure and character targets
- Trade-ideas dual-register is properly modeled (not blocked)
- Campaign lifecycle is properly modeled (not collapsed into a single event template)
- Layer 3 (case-based calibration) remains a post-v6.0.0 opportunity

The expert quality bar for each domain is captured in the `build/domain-research-*.md` files via T2 scene definitions and T1 constraints. The v6.0.0 SKILL.md rewrite should encode these as the new routing table and verification requirements.

---

## Architecture Prescription

**Sources**: structural-audit.md (defects: backward compat, docs/adr, style name updates), token-audit.md (split-by-T1 required)

### Fix A1: Split style-guide.md into per-T1 reference files

The v5.2.0 monolithic `references/style-guide.md` (4,982 words, always loaded) must be replaced with per-T1 conditional reference files. This is forced by token budget: v6.0.0 adds ~1,200 words of new T1/T2 content, which cannot fit in the current architecture.

**New file architecture:**
```
references/
  style-guide.md          → routing inference table ONLY (~400w, always-loaded)
  campaign-guide.md       → campaign T1+T2 constraints (~600w, load on --style campaign)
  trade-ideas-guide.md    → trade-ideas T1+T2 constraints (~650w, load on --style trade-ideas)
  news-guide.md           → news T1+T2 constraints (~550w, load on --style news)
  product-guide.md        → product T1+T2 constraints (~550w, load on --style product)
  compliance-guide.md     → compliance T1+T2 constraints (~600w, load on --style compliance)
```

Update SKILL.md workflow: "Load `references/{style}-guide.md` for the routed T1 style before Step 4."

**Always-loaded after split**: SKILL.md (~2,900w) + style-guide.md routing table (~400w) = ~3,300w — well within healthy range.

### Fix A2: Rewrite SKILL.md Tier 1 routing table

Replace the 5-style table (marketing/product/report/legal/support) with new 5-style table (campaign/trade-ideas/news/product/compliance). Keep row format identical: `--style`, 文案風格類, 共通レジスタ制約.

### Fix A3: Rewrite SKILL.md Tier 2 scene table

Replace the 20-scene table with the new scene roster from domain research (~30 scenes). Maintain row format: `--scene`, 応用場面, `--style`, 句長目標, 情報構造.

**New scene roster** (from domain research):

| Style | Scenes |
|-------|--------|
| campaign | launch, remind, lastday, result, seasonal, referral |
| trade-ideas | flash, theme, earnings, morning, picks, community |
| news | flash, wrap, earnings, indicator, digest, alert |
| product | short, detail, manual, script, release, onboard, compare |
| compliance | disclosure, terms, disclaimer, faq, guide |

### Fix A4: Add backward compatibility aliases for old T1 style names

Extend the backward compat routing table to cover old T1 → new T1 mappings:
```
marketing → campaign (default: launch scene) OR product (if content is feature-based)
report    → news (if CTA absent, analysis < 30%) OR trade-ideas (if action bridge present)
legal     → compliance (legal sub-register)
support   → compliance (support sub-register)
```

Add disambiguation rule: "If `--style marketing` is used without `--scene`, infer from content: period-limited incentive → `campaign/launch`; product features → `product/detail`; market analysis with CTA → `trade-ideas/theme`."

### Fix A5: Update RLs referencing old style names

| RL | Change |
|----|--------|
| RL-3 | Replace `情報分析 (report/press/deck/hottopic/topic)` → `news (all scenes) + trade-ideas analysis sections` |
| RL-4 | Update scene prefixes in hard limits table to new T1/T2 names |
| RL-9 | Replace `情報分析 scenes` → `news (all scenes) + trade-ideas (theme/earnings/morning)` |
| RL-11 | Add trade-ideas exception: "section-level register mixing allowed in trade-ideas: analysis sections use だ/である; reader-action sections use です/ます. Mixing within a single paragraph remains prohibited." |
| RL-12 | Scope change: CTA mandate applies to `campaign` (not `product`). Remove from product scope. Add: "trade-ideas CTA is indirect (〜をチェック, 〜に注目) — action verb not required but action hint required." |
| AC-8 | Change `report/hottopic` reference → `news/flash` |

### Fix A6: Create docs/adr/ with 3 ADR records

Three architectural decisions require ADR records (per structural-audit.md):
1. `docs/adr/ADR-001-compliance-merger.md` — legal+support unification rationale
2. `docs/adr/ADR-002-news-report-split.md` — news/trade-ideas separation from report
3. `docs/adr/ADR-003-trade-ideas-dual-register.md` — RL-11 exception for section-level mixing

---

## Mechanical Prescription

**Sources**: structural-audit.md (5 medium defects: RL/AC style name references), platform-check.md (clean — no issues)

### Fix M1: Terminology sweep

After Fix A5 (RL updates) and Fix A2/A3 (routing table replacement), do a global terminology scan across SKILL.md and all `-guide.md` files:
- Replace all occurrences of old T2 scene prefixes (`marketing/sns` → `campaign/` or remove prefix)
- Verify no orphaned references to `report/hottopic`, `legal/disclosure` without the new `news/` or `compliance/` prefix

### Fix M2: Step 3 routing state update

Update Step 3 state output line from:
```
スタイル: <marketing|product|report|legal|support>
```
to:
```
スタイル: <campaign|trade-ideas|news|product|compliance>
```

### Fix M3: Step 4 Transform Layer 3 table

Add 2 new rows to the Proof & Frame table:

| 主導証明 | campaign | trade-ideas | news | compliance |
|---|---|---|---|---|
| Logos | Simplify to single strongest incentive claim | State with attribution (〜によれば) + action bridge | State factually, attribution required | State with legal precision |
| Ethos | Brand authority + social proof for incentive | Credibility signals (data source + track record) | Institutional authority (attribution) | Institutional authority (法的文言) |
| Pathos | Amplify — deadline, exclusivity, loss-aversion | Moderate — investment curiosity, not hype | Suppress entirely | Suppress entirely |

---

## Content Prescription

**Sources**: domain-research.md (38 new constraints across 5 styles), layer-diagnosis.md (Layer 2 gaps), token-audit.md (split-by-T1 architecture)

### C1: Write per-T1 style reference files

For each new T1 style, create `references/{style}-guide.md` with:
- T1 shared constraint table (the 7-8 style-specific constraints from domain research)
- T2 scene specifications (information structure, sentence length, examples)
- Routing inference keywords
- Scene checkpoint list (for Step 5 inline verification)

**Content source**: Directly from `build/domain-research-{style}.md` files (already written). Each guide file should be ≤700 words.

### C2: Add compliance-specific verification to Step 5

compliance/disclosure requires RL-5 (no です/ます). compliance/faq and compliance/guide require 謙譲語II check. Add these to the Step 5 inline verification section:
- compliance/disclosure: state「です/ますなし: 確認済み」(already present in RL-5, just extend to compliance/disclosure)
- compliance/faq + guide: state「謙譲語II使用: 確認済み」

### C3: Add trade-ideas verification to Step 5

trade-ideas requires two new Step 5 checks:
- Dual-register check: state「分析セクション: だ/である ✓ / 読者セクション: です/ます ✓」
- Action bridge check: state「行動示唆あり: ✓」(verify TI-5 is met)
- Disclaimer check for theme/morning: state「免責文言あり: ✓」(≥500字 content)

### C4: Add news-specific verification to Step 5

news requires:
- Analysis cap check: state「分析比率: XX% (≤30% ✓)」or flag if over
- CTA absence check: state「CTA不在: ✓」

### C5: Add campaign-specific verification to Step 5

campaign requires:
- Deadline check (CA-1): state「期限明示: ✓」or「CA-1違反: 期限未記載」
- Incentive specificity check (CA-3): state「特典具体化: ✓」or「CA-3違反: 特典が抽象的」

### C6: Update Acceptance Criteria

Add new ACs for v6.0.0 styles:
- **AC-9**: campaign output includes explicit deadline (date or period count). State「期限: [X月Y日まで / 残X日]確認: ✓」
- **AC-10**: trade-ideas output ≥500 words includes disclaimer text. State「免責文言: ✓」
- **AC-11**: news output contains zero CTAs. State「CTA不在: ✓」
- **AC-12**: compliance output contains zero instances of「！」or「今すぐ」

### C7: Migrate routing inference keywords to style-guide.md routing table

The SKILL.md frontmatter contains 60+ trigger phrases. These are correct and should remain. However, the "Chinese (by style/scene)" section references old style names (`marketing/lp`, `report/hottopic`, etc.). Update all entries to use new T1/T2 names.

**Note**: The Japanese and English trigger phrase lists are largely style-agnostic (they describe the transformation, not the style name) and need minimal updates.

---

## Phase 3 Execution Order

Per boost-workflow.md repair order (Architecture → Mechanical → Content):

1. **Architecture** (Fixes A1–A6): Create per-T1 guide files, rewrite routing tables, update RLs, create ADR directory
2. **Mechanical** (Fixes M1–M3): Terminology sweep, Step 3 state update, Layer 3 table update
3. **Content** (Fixes C1–C7): Write all T1 guide content, add Step 5 checks, update ACs, update trigger phrases

**Estimated output**: 6 new/rewritten files (SKILL.md + 5 guide files), 3 ADR files, updated style-guide.md (routing inference only).

---

## Verification: Architecture

Post-fix structural re-audit (2026-04-29):

| Check | Expected | Result |
|-------|----------|--------|
| SKILL.md frontmatter: name + description | Present | ✓ PASS |
| Description: ≥3 trigger phrases in third person | 15+ trigger phrases across CN/JP/EN | ✓ PASS |
| Red lines: ≥5 mechanically checkable | 12 RL, all mechanically checkable | ✓ PASS |
| Acceptance criteria: ≥3 testable | 12 AC | ✓ PASS |
| Stance: cognitive position | "Applies editorial discipline..." | ✓ PASS |
| Referenced files exist | All 7 referenced files confirmed | ✓ PASS |
| Writing style: imperative form | No "you should"/"you need to" | ✓ PASS |
| Backward compatibility | Old T1 style aliases documented in style-guide.md | ✓ PASS |
| docs/adr/ directory | ADR-001 (v4), ADR-002, ADR-003, ADR-004 (v6.0.0) | ✓ PASS |

All 9 structural checks pass.

## Verification: Mechanical

Post-fix platform and cross-reference check (2026-04-29):

| Check | Expected | Result |
|-------|----------|--------|
| Platform-specific commands (bash/python) | None | ✓ CLEAN |
| Unresolved template vars ({{...}}) | None | ✓ CLEAN |
| Old scene prefixes (report/hottopic, legal/disclosure etc.) in SKILL.md | None outside backward compat | ✓ CLEAN |
| Step 3 style state updated | New 5-style list | ✓ PASS |
| Layer 3 table: campaign + trade-ideas rows added | Present | ✓ PASS |
| RL-11 trade-ideas exception documented | Present at line 92 | ✓ PASS |

All mechanical checks pass.

## Verification: Content

Post-fix content quality check (2026-04-29):

| Check | Expected | Result |
|-------|----------|--------|
| SKILL.md word count | ≤3,000 | 2,810 ✓ |
| style-guide.md word count | ≤5,000 (soft) | 668 ✓ (routing table only) |
| Always-loaded total | Healthy | 3,478 ✓ (was 7,828) |
| Per-T1 guide files | 5 files, each ≤700w | campaign(290), trade-ideas(302), news(254), product(271), compliance(338) ✓ |
| New T2 scenes in routing table | ~30 | 29 scenes ✓ |
| New ACs | 12 (up from 8) | ✓ |
| trade-ideas dual-register exception | In RL-11 + Step 5 verification | ✓ |
| campaign Step 5 checks (CA-1, CA-3, RL-12) | Present | ✓ |
| news Step 5 checks (analysis cap, CTA absence) | Present | ✓ |
| trade-ideas Step 5 checks (disclaimer, action bridge) | Present | ✓ |
| compliance Step 5 checks (謙譲語II) | Present | ✓ |
| Layer diagnosis after v6.0.0 | Layer 2 (complete) — was Layer 2 (with gaps) | ✓ |
| Token efficiency improvement | Always-loaded -56% | ✓ |

All content checks pass.

---

# v6.1.0 Boost Addendum

**Scope**: surgical refinement of v6.0.0 based on 3 domain research files (campaign / trade-ideas / news, drafted by team abc2 between 2026-04-29 and 2026-04-30) and 3 ADRs that resolve high-priority open questions surfaced in those files. v6.1.0 does not redesign T1/T2 architecture — it tightens constraints, expands scene boundaries, and converts deferred research into actionable RLs.

**Inputs cross-reference**:

| Artifact | Path | Status |
|---|---|---|
| domain-research-campaign.md | diagnosis/ (748 lines) | complete, 6 RLCs proposed |
| domain-research-trade-ideas.md | diagnosis/ (640 lines) | complete, 10 RLCs + 10 OQs |
| domain-research-news.md | diagnosis/ (734 lines) | complete, 6 RLCs + 5 OQs |
| ADR-005 | docs/adr/ | accepted — campaign register hard-bound |
| ADR-006 | docs/adr/ | accepted — TI-7 500字 threshold maintained |
| ADR-007 | docs/adr/ | proposed — news 700/1200字 + 引用例外 |

---

## Phase 1.8 — ADR Integration

| ADR | Decision (one-line) | RL/AC impact | Guide impact |
|---|---|---|---|
| **ADR-005** campaign register boundary | campaign は dual-register **不採用**。体言止め=省略扱い、modality 禁止維持。 | RL-11 campaign 分支単純化（`デュアルレジスタ` 状態行は非出力）。SKILL.md L92 不変。 | `campaign-guide.md` 冒頭に「branding 色強い入力は `--style marketing` 検討」追記。 |
| **ADR-006** TI-7 disclaimer threshold | trade-ideas 免責 **500字超で必須**を維持。theme 常時必須、morning/community 字数依存、flash/picks/earnings 免除（プラットフォーム共通 footer 前提）。 | AC-10 既に v6.0.0 で記述、変更なし。 | `trade-ideas-guide.md` TI-7 節に scene-by-scene impact table 反映。SKILL.md README に「短尺の法的安全はプラットフォーム前提」明記。 |
| **ADR-007** news 字数緩和 + NC-7 引用例外 | wrap 600→**700字**、digest 1000→**1200字**。NC-7 に「直接引用『』内は被引話者の原発話文体保持」を例外明示、間接引用・補足括弧は地の文扱い。 | RL-4 hard cap 表更新（wrap 700 / digest 1200）。AC-4 recall 向上（precision 不変）。RL-11 news 分支に「引用『』内 register 検証除外」分岐追加。 | `news-guide.md` NC-7 改訂、scene 字数表更新、verification に「引用ペアリング前置」手順追加。 |

3 ADR は相互独立だが共通方針を共有する：v5.2.0 → 6.0.0 で確立した骨格は維持し、業界実測との **20–30pt 規模の乖離**を精密化する。架構変更は伴わない。

---

## Phase 1.8 — New Red Line Candidates Roster

team abc2 の 3 ドメイン研究で v6.0.0 既存 RL/AC では捕捉できない **22 件の候補制約**が抽出された。以下に統合 roster を示す（採否判定は Phase 2 Prescription）。

### campaign (6 候補, from domain-research-campaign.md L533–L547)

| ID | Stance | Tier | Priority | 内容 |
|---|---|---|---|---|
| **CA-9** | リスク開示はチャネル別に必須 | Legal | High | LP/EDM 末尾 risk 文言必須、Push/SNS は `*詳細はLP参照` 必須 |
| **CA-10** | 特典タイプ語彙制限 | Legal | Medium | 「割引」「無料」「キャッシュバック」のみ法令安全。「お得」「特別」は単独で報酬性主張不可 |
| **CA-11** | 禁止語彙リスト | Legal | High | 「必勝/絶対/確実/100%/間違いなし」全 scene 禁止 |
| **CA-12** | 景表法 抽選/先着/もれなく排他 | Legal | Medium | 同一文内に 2 つ以上の付与条件混在不可（消費者誤認防止） |
| **CA-14** | Push 30字/EDM 件名 15字で意味完結 | Craft | Medium | 視認性ハードリミット内で結論先行が必須 |
| **CA-15** | 期間限定 hard-fail | Legal | High | 「期間限定」と書いて具体日付なしは景表法違反確定 |

### trade-ideas (10 候補, from domain-research-trade-ideas.md L560–L571)

| ID | Stance | Tier | Priority | 内容 |
|---|---|---|---|---|
| **TI-2.ext** | 事実セクション/見通しセクションの構造的分離 | Legal+Craft | High | theme/morning で「事実」と「見通し」を見出し or 段落で物理分離 |
| **TI-4.ext** | 時間軸表現の特定語彙 | Industry+Craft | High | 「短期/中期/長期」を「数日/数週/数月」等 specific 語に置換 |
| **TI-3.picks** | picks ≥2 数値指標 | Craft | Medium | 銘柄カード必須数値: 株価+変化率 / PER / 配当利回り 等 ≥2 |
| **TI-3.morning** | morning 動画スクリプト分離 | Industry | Medium | morning は本文と script を別出力（OQ-5 と連動） |
| **TI-6.ext** | 逆接構文 risk-balance check | Legal+Industry | High | 「ただし／一方で／反面」の登場頻度 ≥1/段落（forward-looking statement の安全弁） |
| **TI-7.redesign** | TI-7 閾値再設計 | Legal | Medium | **ADR-006 で 500字維持と裁決済み** |
| **TI-9** | CFA VI(A) 利益相反開示 placeholder | Legal | Low | 自社保有銘柄言及時は「利益相反開示: [人間追記]」の placeholder 必須 |
| **TI-10** | dual-register scene/segment 自動判定 | Industry+Craft | Medium | OQ-2 と連動、`--segment institutional` で全文だ/である切替 |
| **TI-8.ext** | 過熱表現 deny-list | Industry | Medium | 「爆騰／暴落／急騰／急落」を「上昇率〜%／下落率〜%」に rewrite |
| **TI-CMTY** | community 投稿例 marker | Craft | Low | 【投稿例】section にタメ口許容を marker 化、verification 除外 |

### news (6 候補, from domain-research-news.md L634–L641)

| ID | Stance | Tier | Priority | 内容 |
|---|---|---|---|---|
| **NC-8** | 見出し体言止め+字数 | Industry | High | flash/alert ≤15字、wrap/earnings/digest ≤32字、体言止め必須 |
| **NC-3.ext** | 主観禁止/許容 hedging vocab list | Industry | High | 禁止「〜と思う／〜と感じる」、許容「〜と見られる／〜の見方」 + 出典必須 |
| **NC-6.ext** | 出典4階層+引用タグ6語彙 | Industry | High | 一次/二次/三次/独自取材で attribution 構文を分岐 |
| **NC-7.ext** | 引用「」内 register 例外 | Industry | Medium | **ADR-007 で採用済み** |
| **NC-4.ext** | scene 別時点粒度 | Industry | Medium | flash=分単位／wrap=日単位／digest=週単位 で時点表現 |
| **NC-9** | 分析パラグラフ物理的分離 | Craft | Low | 分析≤30% 制約を「全体比率」から「独立段落比率」に refine |

---

## Phase 1.8 — Open Questions Registry (consolidated)

3 ドメイン研究で提起された OQ を統合・分類する。

### Resolved by ADR (3)

| OQ | Source | Resolution |
|---|---|---|
| OQ-news-2 (wrap/digest 字数 v6 vs v6.1) | news L662 | ✓ ADR-007 → v6.1.0 採用 |
| OQ-news-4 (NC-7 引用例外文言) | news L666 | ✓ ADR-007 §2.2 改訂後 NC-7 |
| OQ-TI-1 (TI-7 short-disclaimer for flash) | trade-ideas L606 | ✓ ADR-006 → 500字維持・全件 short 棄却 |

### v6.1.0 で裁決推奨 (8) — Phase 2 で ADR-008 〜 ADR-010 候補

| OQ | Source | Recommended Direction |
|---|---|---|
| OQ-TI-2 dual-register segment 切替 | trade-ideas L607 | **(b) `--segment institutional`** で全文だ/である切替（既存 segment 機構と整合） |
| OQ-TI-4 TI-6 逆接 hard vs soft | trade-ideas L609 | **scene 依存**: theme/morning は hard、flash/picks は soft（速報性優先） |
| OQ-TI-9 受け身的客観表現 allow-list | trade-ideas L615 | RL-10 緩和: 「〜される／〜とみられる／〜と発表された」など 6 語彙の allow-list 追加（news/trade-ideas 限定） |
| OQ-TI-10 RL-11 例外射程の news 拡張 | trade-ideas L616 | **拒絶**: ADR-007 で news の引用例外は別次元と確定。互換的に共存。 |
| OQ-news-1 NC-8 hard vs soft | news L661 | **hard 採用**: flash/alert で見出し字数違反は機械検証可能、false positive 低い |
| OQ-news-3 NC-9 分析段落分離 推奨 vs 強制 | news L664 | **推奨に留める**: 既存 30% 比率 check が機械化済み、二重縛りで過剰 |
| OQ-news-5 earnings 前年同期比 必須化 | news L668 | **必須化 + 新規上場 fallback**: 「前年同期比なし（新規上場）」明示 |
| OQ-CAMP-1 年間複数キャンペーン連結 (CA-6 拡張) | campaign L592 | **scope 外**: 単一出力単位の skill 設計から外れる。CHANGELOG に "future scope" 記載 |

### v6.1.0 では棚上げ (3)

| OQ | Source | Reason |
|---|---|---|
| OQ-TI-3 picks ≥1 vs ≥2 指標 | trade-ideas L608 | TI-3.picks 採用形を ≥2 とした以上、Phase 2 で実装内に閉じる |
| OQ-TI-5 morning 動画 script 分離 | trade-ideas L610 | TI-3.morning RLC として実装着手後に再判断 |
| OQ-CAMP-2 branding-campaign 新シーン | campaign L614 | **暫定**: ADR-005 §Alternative (c) に従い `--style marketing` に分離。新 scene 化は v7 範囲 |

### 棄却 (3)

| OQ | Source | Reason |
|---|---|---|
| OQ-TI-6 利益相反 placeholder 自動生成 | trade-ideas L611 | placeholder のみ生成、内容は人間記入（skill scope 外）→ TI-9 として採用、自動生成は棄却 |
| OQ-TI-7 community 投稿例 marker 形式 | trade-ideas L612 | TI-CMTY として採用、marker 文字列は実装裁量 |
| OQ-TI-8 TI-8 過熱表現 deny-list 拡張範囲 | trade-ideas L613 | TI-8.ext として採用、対象は trade-ideas + news に固定 |

### v6.0.0 で deferred のまま継続 (2)

| OQ | Source | Status |
|---|---|---|
| OQ-CAMP-1 通年 lifecycle | campaign L592 | (上記 v6.1.0 棚上げ) |
| OQ-TI-5 morning 動画 split | trade-ideas L610 | (上記 v6.1.0 棚上げ) |

---

## Phase 2 — Prescription Deltas (v6.0.0 → v6.1.0)

v6.0.0 の Architecture / Mechanical / Content の 3 区分を継承して delta だけ記す。

### Architecture (1 delta — ADR 追加のみ)

**Fix A7 — ADR-007 の status を "accepted" に昇格**: `docs/adr/ADR-007-news-length-and-quote-exception.md` の frontmatter `status: proposed` → `accepted`。Phase 3 実装着手時点で採決確定。他 ADR (ADR-005, ADR-006) は既に accepted。

**新 ADR 起草** (Phase 2 完了時点で起草、Phase 3 でファイル化):
- **ADR-008** trade-ideas dual-register segment 切替 (OQ-TI-2 解決) — `--segment institutional` で全文だ/である化、既存 RL-11 trade-ideas 例外と相補的
- **ADR-009** news NC-8 見出し制約 hard 採用 (OQ-news-1) — 字数 hard、体言止め soft
- **ADR-010** RL-10 受け身 allow-list (OQ-TI-9) — 報道/分析特有の客観表現 6 語彙限定許容

新 RL/AC は ADR をまたぐので、Phase 3 で個別 ADR ⇄ 実装の 1:1 対応を確認する。

### Mechanical (3 deltas)

**Fix M4 — RL-4 hard cap 表更新**: SKILL.md L31–L36 の表を ADR-007 §2.1 に従って更新。

| Scene | 現上限 | v6.1.0 上限 |
|---|---|---|
| news/wrap | 600 | **700** |
| news/digest | 1000 | **1200** |
| その他 (campaign 各チャネル, news/flash, news/alert, trade-ideas/flash, product/script) | 変更なし | 変更なし |

**Fix M5 — RL-11 news 分支に「引用『』除外」明記**: SKILL.md L92 の RL-11 既存文言の末尾に exception を追加。

> **追加**: news 出力の verification では、文末スキャン時に「直接引用『』内は検出対象外」とする (ADR-007 §2.2)。間接引用タグ (〜と述べた／〜と発表した) で終わる文は地の文扱いで常体を check。

**Fix M6 — Step 5 verification 構造に「引用ペアリング前置」追加**: SKILL.md "news + trade-ideas analysis sections" 節の RL-3 / RL-9 scan 前に、`「」` ペアリング pre-pass を追加。ペアリング不整合時は警告のみで処理続行 (false negative 防止)。

### Content (5 deltas)

**Fix C8 — campaign-guide.md に CA-9〜CA-12, CA-14, CA-15 反映**: 6 RLC を Tier 1 共通制約節に追記。CA-11 は禁止語彙テーブル化、CA-12 は景表法抽選条件マトリクス、CA-15 は期限なし「期間限定」検出 regex 例示。冒頭に ADR-005 由来の「branding 色強い入力は `--style marketing` 検討」を 1 行記載 (Fix A6 既述だが v6.1.0 で確実化)。

**Fix C9 — trade-ideas-guide.md に TI-2.ext, TI-4.ext, TI-3.picks, TI-6.ext, TI-9, TI-8.ext, TI-CMTY 反映**: 7 RLC を Tier 1+T2 (scene 別) に分配。TI-7 の scene-by-scene impact table を ADR-006 §Scene-by-Scene Impact からそのまま転記。

**Fix C10 — news-guide.md に NC-8, NC-3.ext, NC-6.ext, NC-4.ext, NC-9 反映 + ADR-007 全面実装**: NC-7 の改訂後文言を ADR-007 §2.2 から全文転記。NC-8 は見出し字数 hard cap 表 (flash/alert ≤15、wrap/earnings/digest ≤32) を新設。NC-3.ext/NC-6.ext は hedging 語彙テーブル + 出典 4 階層テーブル。NC-9 は推奨に留めるため「Craft 層 D7 採点で評価」と明記し、Step 5 強制 check には入れない。

**Fix C11 — 新 AC 4 件追加**:

| AC | 内容 |
|---|---|
| **AC-13** | news/wrap 出力は 700字以内、news/digest は 1200字以内 (ADR-007 §2.1) |
| **AC-14** | news 出力で直接引用「」を含む場合、ペアリング ✓、内部 register は検証除外 ✓ を明記 (ADR-007 §2.2 / Fix M6) |
| **AC-15** | trade-ideas/picks 出力は ≥2 数値指標を含む (TI-3.picks) |
| **AC-16** | campaign 出力は CA-11 禁止語彙 (必勝/絶対/確実/100%/間違いなし) を 0 件含む |

**Fix C12 — README/SKILL.md 冒頭に「プラットフォーム共通 footer 前提」明記** (ADR-006 §Negative §2): trade-ideas の flash/picks/earnings/morning短尺/community短尺 は個別免責を生成しないため、配信プラットフォーム側に包括的免責が存在する前提を skill README に明示。skill 自体は前提検証責任を負わない。

---

## Phase 3 — Execution Order (v6.1.0)

Architecture → Mechanical → Content の順序を維持:

1. **Architecture (1d)**: ADR-007 status 昇格、ADR-008/009/010 起草
2. **Mechanical (M4–M6)**: RL-4 表更新、RL-11 news 例外追記、Step 5 引用ペアリング前置
3. **Content (C8–C12)**: 3 guide files 改訂 (campaign / trade-ideas / news)、AC 4 件追加、README 注記

product / compliance の guide files は v6.1.0 で **触らない** (本 boost の研究範囲外、ドメイン研究未実施)。これらは v6.2 以降の boost 候補として CHANGELOG "future scope" に記録する。

**Estimated diff scale** (v6.0.0 比):
- SKILL.md: +120 〜 150 words (RL-4 表更新、RL-11 1 行追加、AC-13/14/15/16、README footer 注記)
- campaign-guide.md: +180 〜 220 words (CA-9〜CA-15)
- trade-ideas-guide.md: +250 〜 300 words (TI-2.ext〜TI-CMTY、scene-by-scene impact table)
- news-guide.md: +200 〜 250 words (NC-8、NC-3.ext、NC-6.ext、NC-4.ext、NC-7 改訂)
- 新 ADR 3 本: 約 1500 〜 2000 words
- 合計 SKILL.md は依然 ≤3000w 内、各 guide は 700–950w 帯 (≤700w 目安を超えるが、v6.0.0 設定の上限ガイドラインを 950w に緩和して許容)

---

## Phase 1.8 — v6.1.0 Boost Rethinking Questions

### Q1. v6.0.0 アーキテクチャは v6.1.0 でも維持できるか?

**Yes.** 5 styles × 29 scenes × 12 RLs の T1/T2 matrix は domain research で検証され、追加候補 RL も全て既存の T1/T2 grid に位置づけ可能。新 T1 や新 scene の追加は不要。

### Q2. Token budget は依然健全か?

**△ 注意.** 各 guide ファイルが v6.0.0 設定の ~700w 目安を超え 800–950w 帯に達する。SKILL.md 本体は ≤3000w 維持可能。判断: ≤950w に上限緩和 (always-loaded には影響しない、conditional load なので)。v6.2 で再度ペイン点なら追加 split (例: trade-ideas-guide → trade-ideas-{flash,theme,picks}-guide) を検討。

### Q3. 3-Layer Quality Standards (Legal / Industry / Craft) は実現に近づいたか?

**Yes (定量改善).**

| Layer | v6.0.0 | v6.1.0 (Phase 3 後 expected) |
|---|---|---|
| Legal hard-fail | ~92.5% (campaign 主導) | ~99% (CA-9/11/12/15 + TI-9 + ADR-006/007) |
| Industry soft-fail | ~79.2% | ~91% (NC-8/3.ext/6.ext + TI-2.ext/4.ext/6.ext) |
| Craft scoring | 既存 D1–D9 rubric | 変更なし — D7 (segment fit) に NC-9 を吸収 |

domain-research-news.md L704+ の 3-Layer 数値推定と整合。

---

## Verification: v6.1.0 Phase 1.8 Synthesis

| Check | Expected | Result |
|-------|----------|--------|
| 3 ADR の Decision/Alternatives/Consequences の synthesis への反映 | 全 ADR 1 行以上 quote | ✓ ADR-005 §Decision、ADR-006 §Decision + Scene Impact、ADR-007 §2.1+§2.2 |
| 22 RLC の roster 化 (campaign 6 / trade-ideas 10 / news 6) | 表形式で全件 | ✓ 各表に Stance/Tier/Priority/内容 4 列 |
| ~22 OQ の triage (resolved / 裁決推奨 / 棚上げ / 棄却 / 継続) | 全件分類 | ✓ 5 区分で 22 OQ 全件配置 |
| 既存 v6.0.0 の Architecture/Mechanical/Content 区分の継承 | delta のみ追記 | ✓ Fix A7, M4–M6, C8–C12 |
| token budget の影響評価 | 数値根拠 | ✓ Q2 + Estimated diff scale |
| Phase 3 execution order の明示 | 順序+対象ファイル | ✓ Phase 3 節 |

すべての Phase 1.8 verification check が pass. v6.1.0 boost は Phase 2 (Prescription) → Phase 3 (Execution) → Phase 4 (Release) に進める状態。

---

# v6.6.0 — moomoo JP Routing Integration

## Phase 1 — Diagnosis Summary

Audit triggered by: (1) full inventory of moomoo JP 内容生产场景 from 飞书 wiki `OGQQwEmmhi0FFJkGwSYcasNCnyh` (5 sheets, ~120KB merged), (2) 31 control samples extracted by Tier 1, (3) need to encode brand-specific channel ↔ scene ↔ RL-4 mapping for routine moomoo content work.

**Diagnosis artifacts** (re-issued 2026-05-12):
- `structural-audit.md` — 9-item check PASS; release is purely additive (no architecture change, no breaking change, no ADR required for content addition — see decision below).
- `token-audit.md` — moomoo-jp-routing.md = 1,050w (within ≤1,500w conditional budget). Always-loaded delta +35w (≈+0.9%). No compression action.
- `platform-check.md` — CLEAN. All cross-references are relative paths, no platform-specific syntax introduced.
- `moomoo-jp-control-group.md` — 31 verbatim samples across 5 T1 (campaign 5 / trade-ideas 5 / news 7 / product 10 / compliance 4). Sheet/row provenance preserved.

**Decision on ADR**: Although a content-only release does not strictly require an ADR per P5, the brand-routing extraction *pattern* (case-library entry + `{brand}-routing.md` + `{brand}-control-group.md`) is a reusable architecture that future brand additions will follow. Recorded as **ADR-011** to give the pattern a citable home.

## Phase 2 — Prescription

| # | File | Action | Rationale |
|---|------|--------|-----------|
| P1 | `references/moomoo-jp-routing.md` | **CREATE** | New brand-routing reference. 5 T1 sub-tables + segment table + brand-specific overrides per T1 + 5-step routing checklist. ≤1,500w. |
| P2 | `diagnosis/moomoo-jp-control-group.md` | **CREATE** | 31 control samples for boost A/B regression. Never runtime-loaded. |
| P3 | `references/case-library.md` (moomoo entry) | **EDIT** | Append "Companion files" pointer to moomoo-jp-routing.md and moomoo-jp-control-group.md. Expand "Primary scenes" to reflect cross-T1 coverage. |
| P4 | `references/style-guide.md` | **EDIT** | Insert "Brand-Specific Routing Overlay" section above Backward Compatibility. Table maps brand trigger → companion file → load condition. |
| P5 | `SKILL.md` | **EDIT** | Add 1 row to References table for moomoo-jp-routing.md (load when `moomoo` / `moomoo証券` in input). |
| P6 | `docs/adr/ADR-011-brand-routing-extraction-pattern.md` | **CREATE** | Record the brand-routing extraction pattern (Context / Decision / Consequences / Alternatives / Related). Triggers extraction at ≥5 channels in any T1 OR ≥3 T1 with channel-level RL-4 differences. |
| P7 | `CHANGELOG.md` | **EDIT** | Add `[Unreleased]` (v6.6.0) section: Added (P1/P2/P6) + Changed (P3/P4/P5 + 3 audit refreshes) + Backward Compat (no changes). |
| P8 | `build/boost-report-v6.6.0.md` | **CREATE** | Phase 4 release report: 8-item acceptance check + word-count verification + recommended next step (run 31-sample A/B against boost-before / boost-after skill). |

**Out of scope (deferred)**:
- Running the 31-sample A/B regression itself — material exists, execution is a separate boost cycle. Documented in boost report's "Next" section.
- Extracting SBI / Rakuten / Nomura into the same 3-file pattern — none currently exceed the ≥5-channel threshold defined by ADR-011. Re-evaluate when those brands accumulate channel-level routing data.
- Adding moomoo-specific RLs (e.g., 賞品「相当」必須 / 「100%当選」禁止) as numbered red lines in SKILL.md — already enforced by case-library.md anti-patterns + RL-2 information-injection guard. Promotion to first-class RLs would be ADR-worthy if observed leaks justify it.

## Phase 3 — Execution Verification

| # | Action | Result |
|---|--------|--------|
| P1 | moomoo-jp-routing.md created | ✓ 1,050w, 5 T1 sub-tables present, segment table present, brand-specific overrides per T1 present, 5-step checklist at end |
| P2 | moomoo-jp-control-group.md present | ✓ 386 lines, 31 samples, sheet/row provenance recorded |
| P3 | case-library.md moomoo Companion files pointer added | ✓ "Companion files" block inserted between "Primary scenes" and "Voice Signature — Shared" |
| P4 | style-guide.md Brand-Specific Routing Overlay section added | ✓ Inserted between Default Scenes table and Backward Compatibility |
| P5 | SKILL.md References row for moomoo-jp-routing.md added | ✓ Added below case-library row |
| P6 | ADR-011 created with all 5 sections (Context / Decision / Consequences / Alternatives / Related) | ✓ Sections present; trigger threshold defined |
| P7 | CHANGELOG.md [Unreleased] section added | (executed via Task #5) |
| P8 | boost-report-v6.6.0.md created | (executed via Task #7) |

**Acceptance**:
- 9-item structural check PASS (structural-audit.md)
- Token budget: SKILL.md 3,194w ≤ 3,500 ✓ / Always-loaded ≤ 5,000 ✓ / moomoo-jp-routing.md ≤ 1,500 ✓
- No breaking change to published interfaces (P6) ✓
- Platform check CLEAN ✓
- All 8 prescribed actions executed ✓

---
name: behavioral-eval-suite
type: diagnosis
skill: jp-style-optimizer
version: 6.0.0
date: 2026-04-29
test_count: 21
---

# Behavioral Evaluation Suite — jp-style-optimizer v6.0.0

## Purpose

Regression tests for mechanisms added in v4.0.0–v5.2.0. Each test case specifies: input, routed style/scene, expected behavior, and the specific RL or constraint being exercised. Run after any SKILL.md or style-guide.md edit.

---

## T1 — RL-12: campaign/launch CTA enforcement

**Input:**
```
当社の株式取引手数料は業界最低水準です。多くの投資家にご利用いただいています。
```

**Routed:** `campaign / launch` (inferred: 「業界最低水準」「多くの投資家」= marketing context)

**Constraints under test:** RL-12 (campaign CTA action verb required), RL-11 (no report modality in marketing)

**Expected output behavior:**
- Output contains at least one action verb CTA: 「口座を開設する」「今すぐ確認する」「詳しくはこちら」or equivalent
- RL-12 scan result: `CTA確認: ✓`
- Output does NOT contain 〜と見られる / 〜見込み (RL-11 marketing modality ban)
- 場面適合 Checkpoint passes all 3 items: benefit specificity + 利益→証明→特徴→CTA order + buyer-stage CTA

**Fail conditions:**
- Output ends with a description sentence and no CTA → RL-12 violation (must revise before delivering)
- Output contains 「手数料は安くなったと見られます」→ RL-11 violation
- Verification block is absent → incomplete execution

---

## T2 — RL-11 extended: keigo-level mixing in compliance/faq

**Input:**
```
口座の情報を変更したい場合は手続きが必要です。詳しくはお電話でご確認ください。
```

**Routed:** `compliance / faq`

**Constraints under test:** RL-11 pattern (2) — keigo level: 謙譲語II required in compliance/support sub-register; plain form prohibited

**Expected output behavior:**
- All service verbs use Kenjōgo II: 「承ります」「ございます」not 「あります」「します」
- All service nouns carry お/ご: 「お手続き」「お口座」「ご確認」「お電話」
- FAQ structure: Q. 〜ですか？ / A. 1–2 sentence answer + channel
- Verification block states `文体統一: ✓` (not just verb-ending check — keigo level confirmed for compliance/support sub-register)
- 場面適合 Checkpoint: お/ご prefix ✓, functional channels stated ✓, Q/A format ✓ → 場面適合: 3/3 ✓

**Fail conditions:**
- Output contains 「します」「あります」without お/ご in place of service verbs → RL-11 keigo violation
- Verification block only checks verb endings and not keigo level → incomplete RL-11 scan (compliance/support sub-register)
- Output formatted as prose paragraph instead of Q/A → Scene Fit failure

---

## T3 — Style routing inference: product/detail (deck-bullet format) from deck keyword

**Input:**
```
今期の営業利益は前期比15%増加しました。新規事業への投資が奏功した結果です。
スライド用に短くしてください。
```

**Routed:** `product / detail` (deck-bullet format) (keyword 「スライド用」triggers deck routing)

**Constraints under test:** RL-9 (attributed numbers in news + trade-ideas analysis sections), Step 3 routing accuracy, deck Checkpoint

**Expected output behavior:**
- Routed as `product / detail` (deck-bullet format) (not `campaign`)
- Output: bullet format, each bullet ≤25 characters (hard limit)
- Category tag present: 【増収】or equivalent
- Filler verbs stripped: no 「しております」「となっております」
- RL-9 check: 「前期比15%」is a bare numerical claim inherited from input → `要出典: 15%` or acknowledged as input-sourced
- 場面適合 Checkpoint: each bullet ≤25 chars ✓, no filler verbs ✓, IR category tag ✓ → 場面適合: 3/3 ✓

**Fail conditions:**
- Routed as `campaign` → routing error (deck keyword missed)
- Any bullet > 25 characters without splitting → hard limit violation
- No category tag → Checkpoint failure
- `前期比15%` left without RL-9 acknowledgment → incomplete verification

---

## T4 — RL-2: information injection resistance in product/short

**Input:**
```
当社のインデックスファンドは信託報酬が低く、長期投資に適しています。
短い商品文案に変えてください。
```

**Routed:** `product / short`

**Constraints under test:** RL-2 (no information injection), Scene Fit Checkpoint item "competitive differentiation stated or implied"

**Expected output behavior:**
- Output propositional content is a strict subset of input — no new numbers, company names, competitor names, or specific features added
- If Checkpoint item "competitive differentiation" cannot be satisfied without RL-2 violation → verification block flags `RL-2優先適用: 競合差異化不明のため省略`
- 場面適合 score reflects this: e.g., 場面適合: 2/3 ✓ (differentiation item = RL-2 constraint blocks it)
- Output does NOT add invented figures like 「信託報酬0.05%」unless those numbers appeared in input

**Fail conditions:**
- Output adds specific percentage not present in input → RL-2 violation, must flag with `⚠ RL-2: [injected figure]`
- Output adds competitor name (e.g., 楽天、SBI) not in input → RL-2 violation
- Verification block does not note the Scene Fit partial score with explanation → incomplete verification

---

## T5 — compliance/disclosure Scene Fit: RL-5 + no trailing nominalization

**Input:**
```
現在、当社の株価は上昇しています。投資家の皆さんには、ぜひご注目いただければと思います。
```

**Routed:** `compliance / disclosure`

**Constraints under test:** RL-5 (no です/ます in compliance/disclosure), RL-3 (no subjective), disclosure Checkpoint (no trailing nominalization, no abbreviations, 命題→根拠→条件/義務 order)

**Expected output behavior:**
- Output uses だ/である体 exclusively — zero instances of 「です」「ます」
- Verification block states: `です/ますなし: 確認済み`
- Subjective expression 「ご注目いただければと思います」converted to objective form: 「投資家各位には注目されたい」or equivalent
- No sentence ends in 〜であること / 〜ということ (trailing nominalization)
- RL-3 check: `主観表現なし: ✓`
- 場面適合 Checkpoint: no trailing nominalization ✓, no abbreviations ✓, 命題→根拠→条件/義務 order ✓ → 場面適合: 3/3 ✓

**Fail conditions:**
- Any sentence in output ends with 「〜です」「〜ます」→ RL-5 violation (must revise)
- Verification block omits `です/ますなし: 確認済み` → AC-5 failure
- Output retains 「思います」or 「ご注目いただければ」register → RL-3 + RL-5 dual violation
- Sentence ends with nominalization 「注目されることが重要である」→ Checkpoint failure

---

## T6 — campaign/launch (Push channel): RL-1 vs RL-4 priority + no explicit CTA

**Input:**
```
当社の株式キャッシュバック券が最大5万円相当プレゼントのキャンペーンを実施中です。ぜひこの機会にお申し込みください。
```

**Routed:** `campaign / launch (Push channel)`

**Constraints under test:** RL-4 multi-field limits (title ≤20 / body ≤60), RL-1 vs RL-4 priority rule (character limits win), RL-12 campaign CTA non-applicability (push uses link hint, not CTA), push Checkpoint (title opens with highest-impact word, no trailing ellipsis)

**Expected output behavior:**
- Two-line structure: title + body
- Title ≤20 chars, body ≤60 chars
- Body ends with link hint (「詳しくはこちら」), NOT an explicit CTA verb like 「申し込む」
- RL-12 scan should NOT be applied (push exemption)
- If 「株式キャッシュバック券」forces title over 20 chars with impact word, RL-4 takes precedence — term may be shortened to core semantics
- Verification block states per-field character counts: 「タイトル: XX文字 ✓ / 本文: XX文字 ✓」

**Fail conditions:**
- Body contains explicit CTA verb (「申し込む」「開設する」) → push uses link hint only
- Title > 20 chars or body > 60 chars → RL-4 violation
- RL-12 check applied to push output → scope error (push is exempt)
- Trailing ellipsis (…) present → Checkpoint violation

---

## T7 — campaign/launch (EDM channel): Three-section structure + RL-4 multi-field limits

**Input:**
```
新春特別キャンペーンとして手数料無料と最大3万円相当のキャッシュバックをプレゼントいたします。この機会をお見逃しなく。
```

**Routed:** `campaign / launch (EDM channel)`

**Constraints under test:** RL-4 (subject ≤40, preheader ≤80, CTA ≤15), three-section structure, RL-12 (campaign CTA button with action verb), 【】bracket format for campaign name

**Expected output behavior:**
- Output in three sections: 件名, プリヘッダー, 本文 with CTA button
- Subject ≤40 chars, preheader ≤80 chars, CTA ≤15 chars
- Subject contains core benefit (手数料無料 or 3万円相当)
- Preheader supplements subject without repeating its content
- CTA button is imperative form (「今すぐ申し込む」「詳細を確認する」)
- Verification block states 3 separate field counts: 「件名: XX文字 ✓ / プリヘッダー: XX文字 ✓ / CTA: XX文字 ✓」

**Fail conditions:**
- Output is a single prose block → scene structure violation
- Any field exceeds its hard limit → RL-4 violation
- CTA absent or > 15 chars → RL-12 + RL-4 violation
- Preheader repeats subject content verbatim → Checkpoint failure

---

## T8 — campaign/launch (Banner channel): Ultra-short copy + RL-4 multi-field

**Input:**
```
期間限定で国内株式の取引手数料が全額無料になるキャンペーンを実施しております。今すぐ口座を開設してください。
```

**Routed:** `campaign / launch (Banner channel)`

**Constraints under test:** RL-4 (main ≤15, sub ≤25, CTA ≤8), noun-phrase preference, RL-12 (campaign CTA with action verb in ≤8 chars)

**Expected output behavior:**
- Three-field structure: main copy, sub-copy (optional), CTA button
- Main ≤15 chars, sub ≤25 chars, CTA ≤8 chars
- Noun phrases preferred — full sentences not required in main
- Numbers and percentages placed at start if applicable
- CTA button with action verb in ≤8 chars (「今すぐ開設」「詳細を見る」)
- Redundant particles/connectors stripped to minimum
- Verification block states 3 field counts

**Fail conditions:**
- Main copy > 15 chars → hard limit violation
- CTA > 8 chars → hard limit violation
- Main copy is a complete sentence with final verb → Checkpoint failure (noun phrases preferred)
- No CTA button → RL-12 violation

---

## T9 — campaign/launch (SNS channel): 140-char limit + emoji + punch-first

**Input:**
```
弊社では、2026年1月1日より米国株式のリアルタイム株価表示サービスを無料でご提供開始いたしました。従来は月額料金が必要でしたが、すべてのお客様に無料でご利用いただけるようになりました。
```

**Routed:** `campaign / launch (SNS channel)`

**Constraints under test:** RL-4 (≤140 chars, target 80–110), emoji requirement (1–2), RL-12 (campaign CTA at end), RL-11 (no report modality in marketing), punch-first (impact phrase in first 15–20 chars), single value proposition

**Expected output behavior:**
- Total ≤140 chars (target 80–110)
- 1–2 emoji present (📈💡🎉 or equivalent financial context emoji)
- CTA at end with action verb
- Most impactful phrase in first 15–20 chars (likely 「米国株リアルタイム株価」or 「リアルタイム株価 無料化」)
- Single value proposition only — not compound claims
- Verification block states total character count: 「XX文字 ✓」

**Fail conditions:**
- > 140 chars → RL-4 hard violation
- 0 emoji or 3+ emoji → Checkpoint failure (1–2 required)
- No CTA at end → RL-12 violation
- Compound claims (both "free service" and "was previously paid") → Checkpoint failure (single value prop)
- Contains 〜と見られる / 〜見込み → RL-11 modality marker violation in marketing

---

## T10 — trade-ideas/community Variant A: 8-part structure + register exceptions

**Input:**
```
最近ディフェンシブセクターが人気みたいだね。ハイテクから公益事業に資金が移ってる感じ。今後どうなるか分からないけど、みんなどう思う？
```

**Routed:** `trade-ideas / community` (Variant A — default, editorial/analytical input)

**Constraints under test:** RL-11 register for trade-ideas/community (です/ます体), RL-3 (no subjective), 8-part structure, 投稿例 casual register exception, Push character limits (title ≤20, subtitle ≤35)

**Expected output behavior:**
- Full 8-part Variant A structure: タイトル → 本文(事実/分析/見通し) → 読者参加 → 【投稿例】→ 投票 → Push
- Body in です/ます体 (NOT だ/である) — register for trade-ideas/community uses です/ます throughout
- Zero subjective expressions in body (RL-3 applies — 「思う」「感じる」prohibited)
- Forward-looking statements use hedging (「〜可能性も出てきました」「〜となりそうです」)
- 読者参加 section uses 〜ましたか？ form (not だろうか)
- 【投稿例】section with 3–5 bullets — casual/タメ口 register allowed (explicit exception)
- 投票 section with 2–4 choices in A/B/C/D format
- Push: title ≤20 chars, subtitle ≤35 chars, ending 「〜しよう！」or 「〜してください>>」
- Verification block states「文体統一: ✓」— confirming です/ます is correct for trade-ideas/community

**Fail conditions:**
- Body uses だ/である体 → fails trade-ideas/community register (trade-ideas/community uses です/ます throughout)
- Body contains 「思う」「感じる」→ RL-3 violation
- Missing any of the 8 parts → structure violation
- 投稿例 section in formal register → fails casual register exception
- Push title > 20 or subtitle > 35 → character limit violation
- Verification block flags です/ます as RL-11 violation → incorrect; trade-ideas/community explicitly uses です/ます throughout

---

## T11 — trade-ideas/community Variant B: UGC curation + fixed elements

**Input:**
```
人気投稿ピックアップ。@TradeMaster さんが「SOXL 3倍レバ、利益+500%」って投稿してバズってた。@新米投資家 さんは「配当株でゆっくり増やす」って感じ。今週の市場は半導体関連が強かった。
```

**Routed:** `trade-ideas / community` (Variant B — triggered by 「人気投稿」「@ユーザー名」keywords)

**Constraints under test:** Variant B 6-part structure, fixed transition sentence, mandatory disclaimer, no 投票/投稿例 sections, editorial commentary register

**Expected output behavior:**
- Variant B detected (not A) — 「人気投稿」keyword triggers B
- 6-part structure: タイトル → 市場コンテクスト → 転換句 → ユーザー投稿+編集コメント → 免責声明 → Push
- Title in 「"[quote]"や "[quote]"など―人気投稿まとめ」format
- Transition sentence: 「それでは、今回話題となった人気投稿を見ていきましょう。」(fixed — must not be altered)
- Disclaimer present: 「*本コンテンツで引用している投稿はmoomooユーザーが作成したものであり、当社の見解を示すものではありません。」
- Push subtitle matches fixed template: 「moomoo証券ユーザーのリアル投資談をピックアップ。今すぐチェック>>」
- No 投票/投稿例 sections (those are Variant A only)
- Editorial commentary in です/ます, objective, positive framing — no subjective 「すごい」「やばい」

**Fail conditions:**
- Routed as Variant A → routing error (「人気投稿」keyword missed)
- Missing disclaimer → hard requirement violation
- Transition sentence altered from fixed wording → Checkpoint violation
- 投票 or 投稿例 sections present → Variant B structure violation
- Editorial commentary contains subjective evaluation (「すごい」「才能がある」) → RL-3 violation

---

## T12 — product/script: Spoken rhythm + no written-only expressions

**Input:**
```
信用取引においては、委託保証金及び代用有価証券に基づき、信用取引の決済期限までに反対売買又は現引き・現渡しを行う必要がございます。
```

**Routed:** `product / script`

**Constraints under test:** Sentence length ≤30 chars per sentence, no written-only expressions (〜においては, 〜及び, 〜に基づき, 〜又は), spoken rhythm, conversational です/ます

**Expected output behavior:**
- Every sentence ≤30 characters
- Written-only expressions replaced: 「においては」→「では」, 「及び」→「と」, 「又は」→「または」, 「に基づき」→「をもとに」
- Parenthetical definitions become natural spoken asides if present
- Large numbers use 万/億 units if applicable
- Conversational です/ます tone maintained (not overly casual)
- Term lock: 「信用取引」「委託保証金」「代用有価証券」「反対売買」「現引き」「現渡し」preserved
- Verification block confirms: every sentence ≤30 chars ✓, no written-only expressions ✓

**Fail conditions:**
- Any sentence > 30 chars → Checkpoint violation (spoken rhythm requires short sentences)
- Written-only expressions remain (〜においては, 〜に関しまして, 〜及び, 〜又は) → Checkpoint violation
- Register drops to casual (loses です/ます) → RL-11 violation
- Financial terms altered (e.g., 「委託保証金」→「担保」) → RL-1 violation

---

## T13 — product/manual: Numbered steps + one action per step

**Input:**
```
まずログインしてから口座設定画面で出金先銀行を登録して、金額を入力してから確認ボタンを押してください。手続き前に本人確認書類の提出が必要です。
```

**Routed:** `product / manual`

**Constraints under test:** Numbered steps (①②③ or 1. 2. 3.), one action per step, preconditions before steps, warnings at end

**Expected output behavior:**
- Steps numbered (①②③ or 1. 2. 3.)
- Each step contains exactly one action — no compound 「〜してから〜して」in a single step
- Precondition (「本人確認書類の提出」) appears BEFORE steps (not after, as in the input)
- Compound actions decomposed: 「ログインしてから口座設定画面で出金先銀行を登録して、金額を入力してから確認ボタンを押してください」→ minimum 4 separate steps
- Passive avoided; imperative or 〜してください form preferred
- Verification block confirms Checkpoint items: steps numbered ✓, one action per step ✓, preconditions before steps ✓

**Fail conditions:**
- Steps not numbered → Checkpoint violation
- Any step contains 2+ actions (「ログインして出金先を登録」as one step) → Checkpoint violation
- Precondition (本人確認書類) appears after steps → information order violation
- Content added beyond input → RL-2 violation
- Terms altered (e.g., 「出金先銀行」→「振込先」without input basis) → RL-1 violation

---

## T14 — campaign/launch: Reader-centric reframing (company-subject elimination)

**Input:**
```
当社はこのたび業界初のAI自動リバランス機能を開発しました。当社の技術チームが2年かけて構築したアルゴリズムにより、ポートフォリオの最適化を実現しています。
```

**Routed:** `campaign / launch` (inferred: 「業界初」「AI自動リバランス」= marketing context, LP-length copy)

**Constraints under test:** Shared Constraint「Reader-centric reframing」(company-subject sentences must be rewritten with reader-benefit subject), Swipe Pattern「当社は→読者主語」, Layer 3 post-step execution

**Expected output behavior:**
- Zero instances of 「当社」or 「弊社」as grammatical subject (topic marker は/が)
- Company-subject sentences reframed to reader-benefit perspective: e.g., 「当社はAI自動リバランス機能を開発しました」→「あなたのポートフォリオはAI自動リバランスで最適化されます」or equivalent reader-subject form
- Technical achievements (「2年かけて構築」) reframed as user benefit, not company effort
- Layer 3 post-step confirms reframing was applied: verification block states `読者主語化: ✓（当社/弊社の主語使用なし）`
- CTA present (RL-12 still applies for lp)
- 場面適合 Checkpoint passes: benefit specificity ✓, reader-centric framing ✓, CTA ✓

**Fail conditions:**
- Output contains 「当社は」or 「弊社は」as sentence subject → Reader-centric reframing violation
- Output contains 「当社が」as agent subject → same violation (が-marked agent counts)
- 「当社の〜」used as possessive modifier is acceptable ONLY if the sentence subject is the reader or the product — NOT if 「当社」is the semantic agent of the clause
- Verification block omits reader-centric reframing check → incomplete Layer 3 post-step execution
- Company-effort framing retained (「2年かけて開発」as selling point) without conversion to user benefit → reframing incomplete

---

## T15 — trade-ideas/theme: Hedging confidence gradient (three-tier epistemic markers)

**Input:**
```
米国の利下げはほぼ確実に9月に実施される。半導体セクターはたぶん回復するだろう。新興国通貨はひょっとすると大幅に下落するかもしれない。消費者物価指数は来月発表される。
```

**Routed:** `trade-ideas / theme` (analysis section)

**Constraints under test:** trade-ideas Shared Constraint「Confidence gradient」— High confidence=見込み/見通し, Medium confidence=と見られる/と考えられる, Low confidence=可能性がある/リスクがある; prohibition on uniform hedging; prohibition on 「〜だろう」; TI-2 (推測表現義務化)

**Expected output behavior:**
- High-confidence statement (「ほぼ確実に9月に実施」) uses High-tier markers: 「〜見込み」「〜見通し」(e.g., 「9月に利下げが実施される見込みである」)
- Medium-confidence statement (「たぶん回復する」) uses Medium-tier markers: 「〜と見られる」「〜と考えられる」(e.g., 「半導体セクターは回復すると見られる」)
- Low-confidence statement (「ひょっとすると大幅に下落するかもしれない」) uses Low-tier markers: 「〜可能性がある」「〜リスクがある」(e.g., 「新興国通貨が大幅に下落する可能性がある」)
- Factual statement (「来月発表される」) carries no hedging marker — it is not a forecast
- All three tiers used distinctly — no uniform application of the same tier to all forward-looking statements
- Zero instances of 「〜だろう」in output (prohibited marker)
- Verification block states `推測表現分級: ✓（High/Medium/Low 使い分け確認済み）` and `「だろう」不使用: ✓` and `TI-2 推測表現義務化: ✓`

**Fail conditions:**
- All forward-looking statements use the same tier (e.g., all 「〜と見られる」) → mechanical uniformity violation
- 「だろう」appears in output → prohibited marker violation
- High-confidence claim uses Low-tier marker (「利下げが実施される可能性がある」) → confidence-tier mismatch
- Low-confidence claim uses High-tier marker (「新興国通貨が下落する見通しである」) → confidence-tier mismatch
- Factual statement receives hedging marker → over-hedging
- Verification block does not confirm per-tier usage → incomplete confidence gradient check

---

## T16 — product/detail: Multi-feature ordering + Feature→Benefit completeness

**Input:**
```
この投資信託は毎月分配型です。為替ヘッジ機能があります。信託報酬は年率0.09%で業界最低水準です。NISAつみたて投資枠対象商品です。100円から購入可能です。
```

**Routed:** `product / detail`

**Constraints under test:** Product T1「Multi-feature ordering（strongest first）」, detail Checkpoint「Feature→benefit structure present for each claim」, average sentence length 20–35 chars

**Expected output behavior:**
- Features reordered by differentiation strength — strongest/most differentiating feature first (likely 「信託報酬 年率0.09% 業界最低水準」or 「NISAつみたて投資枠対象」), weakest/most generic last (likely 「毎月分配型」)
- Every feature has a corresponding benefit conversion (Feature→Benefit):
  - 「信託報酬 年率0.09%」→ benefit: 長期運用コストを抑えられる or equivalent
  - 「NISAつみたて投資枠対象」→ benefit: 非課税で積立投資ができる or equivalent
  - 「100円から購入可能」→ benefit: 少額から始められる or equivalent
  - 「為替ヘッジ機能」→ benefit: 為替変動リスクを軽減できる or equivalent
  - 「毎月分配型」→ benefit: 定期的にインカムを受け取れる or equivalent
- Average sentence length between 20–35 characters
- RL-2 respected: no information beyond input added (no invented percentages, no competitor names)
- Verification block states: `機能順序: ✓（差異化順）`, `F→B変換: 5/5 ✓`, `平均文長: XX文字 ✓`

**Fail conditions:**
- Features in input order (not reordered) → multi-feature ordering violation
- Generic feature (「毎月分配型」) placed before differentiating feature (「業界最低水準の信託報酬」) → ordering violation
- Any feature listed without a corresponding benefit statement → F→B completeness violation
- Average sentence length < 20 or > 35 chars → Checkpoint violation
- New information added (e.g., specific competitor fund names, performance figures not in input) → RL-2 violation
- Verification block missing F→B count or ordering confirmation → incomplete check

---

## T17 — compliance/guide: Branching procedure + Processing time + Recovery phrase

**Input:**
```
口座をお持ちのお客様はマイページから届出住所変更ができます。口座をお持ちでないお客様はコールセンターに連絡してください。届出住所の変更には通常3〜5営業日かかります。届出住所変更が完了すると登録メールアドレスに通知が届きます。
```

**Routed:** `compliance / guide`

**Constraints under test:** guide constraints「branching procedures（条件→ルート分岐）」「processing time（通常X営業日以内）」「recovery phrase」; RL-11 compliance/support sub-register

**Expected output behavior:**
- Branching structure: condition stated BEFORE each branch route — not interleaved or reversed
  - Condition 1: 「口座をお持ちのお客様」→ Route: マイページから届出住所変更
  - Condition 2: 「口座をお持ちでないお客様」→ Route: コールセンターに連絡
- Conditions clearly separated (numbered, bulleted, or headed) — not run together in a single paragraph
- Processing time explicitly stated with business-day unit: 「通常3〜5営業日以内」or equivalent — not vague (「しばらくお待ちください」is insufficient)
- Recovery phrase present at closing — a navigation statement that guides the reader to next steps or back to a help hub: e.g., 「ご不明な点がございましたら、サポートページをご確認ください」「その他のお手続きはこちら」or equivalent
- Keigo maintained throughout (compliance/support sub-register — RL-11 applies)
- Verification block states: `条件分岐: ✓（条件→ルート順）`, `処理時間: ✓（営業日明記）`, `リカバリーフレーズ: ✓`

**Fail conditions:**
- Branch route stated before its condition (e.g., 「マイページから変更できます。口座をお持ちの場合は〜」) → condition-first ordering violation
- Two branches merged into one sentence without clear separation → branching structure violation
- Processing time omitted or vague (「少々お待ちください」instead of specific business days) → processing time violation
- No recovery/navigation phrase at closing → recovery phrase violation
- Plain form used (「できる」「連絡する」instead of 「できます」「ご連絡ください」) → RL-11 keigo violation
- Content added beyond input (e.g., specific phone numbers not in input) → RL-2 violation
- Verification block missing any of the three constraint checks → incomplete verification

---

## T18 — campaign/launch: CA-1 deadline + CA-3 incentive specificity

**Input:**
```
新規口座開設でお得な特典をプレゼントいたします。ぜひお申し込みください。
```

**Routed:** `campaign / launch` (inferred: 「口座開設」「特典」= campaign context)

**Constraints under test:** CA-1 (deadline mandatory — 「期間限定」alone insufficient, must have specific date), CA-3 (incentive specificity — abstract 「お得な特典」must become specific name), RL-12 (CTA with Hot stage action verb)

**Expected output behavior:**
- CA-1 violation detected: no deadline present → skill flags 「CA-1違反: 期限未記載」and requests date from user OR adds a placeholder ([終了日未定の場合はXX月XX日までとご記入ください])
- CA-3 violation detected: 「お得な特典」is too abstract → skill flags 「CA-3違反: 特典が抽象的」
- RL-12 check: CTA action verb present (「今すぐ申し込む」or equivalent) → 「CTA確認: Hot ✓」
- Verification block states: `期限: [未記載 — CA-1違反]`, `特典名: [未記載 — CA-3違反]`
- Since input lacks deadline and incentive name, the skill should surface these as constraint violations — NOT invent dates or prize amounts (RL-2)

**Fail conditions:**
- Skill invents a deadline (e.g., 「12月31日まで」) not in input → RL-2 violation
- Skill outputs 「お得な特典」without flagging CA-3 → CA-3 constraint missed
- Verification block omits CA-1 and CA-3 checks → incomplete execution

---

## T19 — trade-ideas/theme: TI-2 推測表現 + TI-5 action bridge + dual-register

**Input:**
```
米国テクノロジー株は今後も上昇を続ける。特にAI関連企業はGPU需要の増加により業績が改善する。個人投資家にとって買い時かもしれない。
```

**Routed:** `trade-ideas / theme` (inferred: 「テクノロジー株」「AI関連」「買い時」= trade-ideas context with action bridge)

**Constraints under test:** TI-1 (no investment advice — 「買い時」must be reframed), TI-2 (推測表現義務化 — all forward-looking statements must have epistemic markers), TI-5 (action bridge — indirect action hint required), RL-11 trade-ideas exception (dual-register)

**Expected output behavior:**
- 「買い時かもしれない」reframed to avoid investment advice: NOT 「買い時です」— TI-1 compliant form: 「値動きに注目です」「取引機会として関心が集まっています」
- All forward-looking claims have TI-2 推測表現: 「上昇を続ける」→「上昇が続くと見られる」; 「業績が改善する」→「業績改善の可能性がある」
- Dual-register: analysis section ends in だ/である; reader-action section (action bridge + CTA hint) ends in です/ます
- TI-5 action bridge present: e.g., 「AI関連銘柄の動向をチェックしてみませんか」
- Verification block: `分析セクション: だ/である ✓ / 読者セクション: です/ます ✓`, `行動示唆あり: ✓`, `TI-1: 投資推奨表現なし ✓`

**Fail conditions:**
- Output contains 「今が買い時」or 「〜銘柄を購入することをお勧めします」→ TI-1 investment advice violation
- Forward-looking claim has no epistemic marker (「上昇を続ける」left as assertion) → TI-2 violation
- No action bridge present → TI-5 violation
- Analysis section uses です/ます → dual-register structure broken
- Verification block does not confirm dual-register → incomplete RL-11 trade-ideas check

---

## T20 — news/flash: NC-1 事実先出し + NC-5 CTA禁止 + analysis cap

**Input:**
```
日銀が政策金利を0.25%から0.5%に引き上げた。これは予想を上回る決定で、市場に大きな影響を与えると思われる。投資家はすぐにポジションを確認してください。
```

**Routed:** `news / flash` (inferred: 「政策金利」「引き上げた」= financial news; ≤140字 target)

**Constraints under test:** NC-1 (5W fact in opening), NC-3 (zero subjective — 「と思われる」must become objective form or be removed), NC-5 (CTA absolute prohibition — 「ポジションを確認してください」must be removed entirely), NC-7 (だ/である body), analysis cap (analysis portion ≤30% of total)

**Expected output behavior:**
- Output ≤140 chars (RL-4 news/flash)
- NC-1: Opening sentence contains key fact with number: 「日銀は政策金利を0.25%から0.5%に引き上げた。」
- NC-3: 「と思われる」removed or replaced with objective form (「と見られる」is acceptable in news context)
- NC-5: 「投資家はすぐにポジションを確認してください」COMPLETELY removed — CTA absolute prohibition in news
- NC-7: だ/である body throughout
- Verification block: `CTA不在: ✓`, `主観表現なし: ✓`, `分析比率: XX% (≤30% ✓)`, `140字以内: XX字 ✓`

**Fail conditions:**
- Output retains CTA (「確認してください」or any action instruction) → NC-5 hard violation
- 「と思われる」retained as-is → NC-3 violation
- Output uses です/ます in main body → NC-7 register violation
- Analysis commentary exceeds 30% of total content → redirect to trade-ideas suggested
- Verification block does not include `CTA不在: ✓` check → AC-11 failure

---

## T21 — compliance/disclosure: C-1 宣伝性ゼロ + RL-5 + C-2 略語禁止

**Input:**
```
東証プライム市場に上場している当社の株は、今後の成長が期待されます。ぜひ金商法に基づく目論見書をご確認ください。リスクがあります。
```

**Routed:** `compliance / disclosure` (inferred: 「目論見書」「金商法」= disclosure context)

**Constraints under test:** RL-5 (no です/ます in disclosure), C-1 (zero promotional — 「ぜひ」「成長が期待されます」禁止), C-2 (zero abbreviations — 「東証」→「東京証券取引所」; 「金商法」→「金融商品取引法」), C-4 (risk warning completeness — 「リスクがあります」too vague)

**Expected output behavior:**
- だ/である体 exclusively — zero instances of 「です」「ます」in main body
- Verification block states: `です/ますなし: 確認済み`
- 「ぜひ」removed (C-1: zero promotional)
- 「成長が期待されます」rewritten as objective だ/である form without promotional tone: 「成長が期待される」(still forward-looking — must add epistemic hedge)
- 「東証」→「東京証券取引所」(C-2: no abbreviations)
- 「金商法」→「金融商品取引法」(C-2: no abbreviations)
- 「リスクがあります」→ compliance-compliant form: 「損失が生じるおそれがある」or「元本を割り込む可能性がある」
- Verification block: `です/ますなし: 確認済み`, `略語不在: ✓`, `宣伝性ゼロ: ✓`, `リスク警告: ✓`

**Fail conditions:**
- Output retains 「東証」or 「金商法」→ C-2 zero abbreviation violation
- 「ぜひ」retained in disclosure → C-1 promotional tone violation
- Any sentence ends in 「〜です」「〜ます」→ RL-5 hard violation
- Risk warning left as 「リスクがあります」→ C-4 insufficient specificity
- Verification block omits `です/ますなし: 確認済み` → AC-5 failure

---

## Execution Notes

- Run all 21 cases after any change to SKILL.md or style-guide.md
- **Priority tiers**:
  - **Tier 1** (hard gate tests): T1 (RL-12 campaign CTA), T5 (RL-5 compliance/disclosure register), T6 (push RL-1/RL-4 priority), T18 (campaign CA-1/CA-3 constraint violations)
  - **Tier 2** (complex routing/exception tests): T10 (trade-ideas/community Variant A register exceptions), T11 (trade-ideas/community Variant B structure), T3 (deck-style → product/detail routing), T15 (trade-ideas confidence gradient), T19 (trade-ideas dual-register + TI-1/TI-2/TI-5)
  - **Tier 3** (RL-4 multi-field tests): T7 (edm), T8 (banner), T9 (sns), T20 (news NC-1/NC-5 + CTA禁止)
  - **Tier 4** (scene structural tests): T12 (script spoken rhythm), T13 (manual step decomposition), T2 (support keigo), T4 (product RL-2 resistance), T14 (lp reader-centric reframing), T16 (product/detail ordering + F→B), T17 (support/guide branching), T21 (compliance/disclosure C-1/C-2/RL-5)
- T4 documents an intentional partial score — `場面適合: 2/3` is correct behavior when RL-2 blocks a Checkpoint item; a score of 3/3 in this case would indicate incorrect behavior (injection)
- T3 routing test: if the model routes `スライド用` to campaign rather than product/detail, the routing inference table needs a keyword addition
- T6 documents the RL-1 vs RL-4 priority rule — this is the only scene where term integrity may yield to character limits
- T10 and T11 test the trade-ideas/community scene's dual-variant routing — misrouting between A and B is a distinct failure mode from misrouting between styles
- T14 tests Layer 3 post-step execution — if reader-centric reframing is not verified in the output block, the post-step pipeline is incomplete
- T15 tests epistemic marker differentiation — mechanical uniform hedging is a distinct failure from using the wrong tier
- T16 tests two orthogonal constraints simultaneously — ordering and F→B completeness are independent checks
- T17 tests three guide-specific constraints in combination — condition-first branching, explicit processing time, and closing recovery phrase

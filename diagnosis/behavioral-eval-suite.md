---
name: behavioral-eval-suite
type: diagnosis
skill: jp-style-optimizer
version: 5.0.0
date: 2026-04-28
test_count: 13
---

# Behavioral Evaluation Suite — jp-style-optimizer v5.0.0

## Purpose

Regression tests for mechanisms added in v4.0.0 and v4.1.0. Each test case specifies: input, routed style/scene, expected behavior, and the specific RL or constraint being exercised. Run after any SKILL.md or style-guide.md edit.

---

## T1 — RL-12: marketing/lp CTA enforcement

**Input:**
```
当社の株式取引手数料は業界最低水準です。多くの投資家にご利用いただいています。
```

**Routed:** `marketing / lp` (inferred: 「業界最低水準」「多くの投資家」= marketing context)

**Constraints under test:** RL-12 (CTA action verb required), RL-11 (no report modality in marketing)

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

## T2 — RL-11 extended: keigo-level mixing in support/faq

**Input:**
```
口座の情報を変更したい場合は手続きが必要です。詳しくはお電話でご確認ください。
```

**Routed:** `support / faq`

**Constraints under test:** RL-11 pattern (2) — keigo level: 謙譲語II required in support; plain form prohibited

**Expected output behavior:**
- All service verbs use Kenjōgo II: 「承ります」「ございます」not 「あります」「します」
- All service nouns carry お/ご: 「お手続き」「お口座」「ご確認」「お電話」
- FAQ structure: Q. 〜ですか？ / A. 1–2 sentence answer + channel
- Verification block states `文体統一: ✓` (not just verb-ending check — keigo level confirmed)
- 場面適合 Checkpoint: お/ご prefix ✓, functional channels stated ✓, Q/A format ✓ → 場面適合: 3/3 ✓

**Fail conditions:**
- Output contains 「します」「あります」without お/ご in place of service verbs → RL-11 keigo violation
- Verification block only checks verb endings and not keigo level → incomplete RL-11 scan
- Output formatted as prose paragraph instead of Q/A → Scene Fit failure

---

## T3 — Style routing inference: report/deck from deck keyword

**Input:**
```
今期の営業利益は前期比15%増加しました。新規事業への投資が奏功した結果です。
スライド用に短くしてください。
```

**Routed:** `report / deck` (keyword 「スライド用」triggers deck routing)

**Constraints under test:** RL-9 (attributed numbers in 情報分析), Step 3 routing accuracy, deck Checkpoint

**Expected output behavior:**
- Routed as `report / deck` (not `marketing`)
- Output: bullet format, each bullet ≤25 characters (hard limit)
- Category tag present: 【増収】or equivalent
- Filler verbs stripped: no 「しております」「となっております」
- RL-9 check: 「前期比15%」is a bare numerical claim inherited from input → `要出典: 15%` or acknowledged as input-sourced
- 場面適合 Checkpoint: each bullet ≤25 chars ✓, no filler verbs ✓, IR category tag ✓ → 場面適合: 3/3 ✓

**Fail conditions:**
- Routed as `marketing` → routing error (deck keyword missed)
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

## T5 — legal/disclosure Scene Fit: RL-5 + no trailing nominalization

**Input:**
```
現在、当社の株価は上昇しています。投資家の皆さんには、ぜひご注目いただければと思います。
```

**Routed:** `legal / disclosure`

**Constraints under test:** RL-5 (no です/ます in disclosure), RL-3 (no subjective), disclosure Checkpoint (no trailing nominalization, no abbreviations, 命題→根拠→条件/義務 order)

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

## T6 — marketing/push: RL-1 vs RL-4 priority + no explicit CTA

**Input:**
```
当社の株式キャッシュバック券が最大5万円相当プレゼントのキャンペーンを実施中です。ぜひこの機会にお申し込みください。
```

**Routed:** `marketing / push`

**Constraints under test:** RL-4 multi-field limits (title ≤20 / body ≤60), RL-1 vs RL-4 priority rule (character limits win), RL-12 non-applicability (push uses link hint, not CTA), push Checkpoint (title opens with highest-impact word, no trailing ellipsis)

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

## T7 — marketing/edm: Three-section structure + RL-4 multi-field limits

**Input:**
```
新春特別キャンペーンとして手数料無料と最大3万円相当のキャッシュバックをプレゼントいたします。この機会をお見逃しなく。
```

**Routed:** `marketing / edm`

**Constraints under test:** RL-4 (subject ≤40, preheader ≤80, CTA ≤15), three-section structure, RL-12 (CTA button with action verb), 【】bracket format for campaign name

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

## T8 — marketing/banner: Ultra-short copy + RL-4 multi-field

**Input:**
```
期間限定で国内株式の取引手数料が全額無料になるキャンペーンを実施しております。今すぐ口座を開設してください。
```

**Routed:** `marketing / banner`

**Constraints under test:** RL-4 (main ≤15, sub ≤25, CTA ≤8), noun-phrase preference, RL-12 (CTA with action verb in ≤8 chars)

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

## T9 — marketing/sns: 140-char limit + emoji + punch-first

**Input:**
```
弊社では、2026年1月1日より米国株式のリアルタイム株価表示サービスを無料でご提供開始いたしました。従来は月額料金が必要でしたが、すべてのお客様に無料でご利用いただけるようになりました。
```

**Routed:** `marketing / sns`

**Constraints under test:** RL-4 (≤140 chars, target 80–110), emoji requirement (1–2), RL-12 (CTA at end), RL-11 (no report modality in marketing), punch-first (impact phrase in first 15–20 chars), single value proposition

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

## T10 — report/topic Variant A: 8-part structure + register exceptions

**Input:**
```
最近ディフェンシブセクターが人気みたいだね。ハイテクから公益事業に資金が移ってる感じ。今後どうなるか分からないけど、みんなどう思う？
```

**Routed:** `report / topic` (Variant A — default, editorial/analytical input)

**Constraints under test:** RL-11 topic exception (です/ます体), RL-3 (no subjective), 8-part structure, 投稿例 casual register exception, Push character limits (title ≤20, subtitle ≤35)

**Expected output behavior:**
- Full 8-part Variant A structure: タイトル → 本文(事実/分析/見通し) → 読者参加 → 【投稿例】→ 投票 → Push
- Body in です/ます体 (NOT だ/である) — topic register exception from report T1
- Zero subjective expressions in body (RL-3 applies — 「思う」「感じる」prohibited)
- Forward-looking statements use hedging (「〜可能性も出てきました」「〜となりそうです」)
- 読者参加 section uses 〜ましたか？ form (not だろうか)
- 【投稿例】section with 3–5 bullets — casual/タメ口 register allowed (explicit exception)
- 投票 section with 2–4 choices in A/B/C/D format
- Push: title ≤20 chars, subtitle ≤35 chars, ending 「〜しよう！」or 「〜してください>>」
- Verification block states「文体統一: ✓」— confirming です/ます is correct for topic

**Fail conditions:**
- Body uses だ/である体 → fails topic register exception (RL-11 note says topic uses です/ます)
- Body contains 「思う」「感じる」→ RL-3 violation
- Missing any of the 8 parts → structure violation
- 投稿例 section in formal register → fails casual register exception
- Push title > 20 or subtitle > 35 → character limit violation
- Verification block flags です/ます as RL-11 violation → incorrect; topic is explicitly exempted

---

## T11 — report/topic Variant B: UGC curation + fixed elements

**Input:**
```
人気投稿ピックアップ。@TradeMaster さんが「SOXL 3倍レバ、利益+500%」って投稿してバズってた。@新米投資家 さんは「配当株でゆっくり増やす」って感じ。今週の市場は半導体関連が強かった。
```

**Routed:** `report / topic` (Variant B — triggered by 「人気投稿」「@ユーザー名」keywords)

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

## Execution Notes

- Run all 13 cases after any change to SKILL.md or style-guide.md
- **Priority tiers**:
  - **Tier 1** (hard gate tests): T1 (RL-12 marketing CTA), T5 (RL-5 disclosure register), T6 (push RL-1/RL-4 priority)
  - **Tier 2** (complex routing/exception tests): T10 (topic Variant A register exceptions), T11 (topic Variant B structure), T3 (deck routing)
  - **Tier 3** (RL-4 multi-field tests): T7 (edm), T8 (banner), T9 (sns)
  - **Tier 4** (scene structural tests): T12 (script spoken rhythm), T13 (manual step decomposition), T2 (support keigo), T4 (product RL-2 resistance)
- T4 documents an intentional partial score — `場面適合: 2/3` is correct behavior when RL-2 blocks a Checkpoint item; a score of 3/3 in this case would indicate incorrect behavior (injection)
- T3 routing test: if the model routes `スライド用` to marketing rather than report/deck, the routing inference table needs a keyword addition
- T6 documents the RL-1 vs RL-4 priority rule — this is the only scene where term integrity may yield to character limits
- T10 and T11 test the topic scene's dual-variant routing — misrouting between A and B is a distinct failure mode from misrouting between styles

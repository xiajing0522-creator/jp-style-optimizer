---
name: jp-style-optimizer
version: 5.2.0
description: >
  Activate when the user provides existing Japanese text and requests a register or
  style change — NOT translation. Trigger phrases by language:

  Chinese (general): "润色日语文案", "日语润色", "日文润色", "日语文案优化",
  "日语优化", "优化日语", "文案优化", "把这段日语改成…", "日语文体转换",
  "改写日语", "让日语更正式", "让日语更口语", "让日语更简短", "让日语更专业".

  Chinese (by style/scene):
  marketing/lp="改成营销文案/营销化/日语营销化/改成推广文案/改成广告风格/日语广告化" /
  marketing/sns="改成SNS格式" /
  marketing/event="改成活动通知/改成campaign文案" /
  marketing/push="改成Push通知文案/改成推送文案" /
  marketing/edm="改成EDM文案/改成邮件营销文案" /
  marketing/banner="改成Banner文案/改成横幅文案/改成应用内横幅" /
  product/short="改成短产品文案/改成卖点文案/产品卖点提炼" /
  product/detail="改成产品说明/商品文案" /
  product/manual="改成使用说明/改成操作指南" /
  product/script="改成视频脚本/改成配音稿/改成动画脚本" /
  report/report="改成研报风格/研报风格润色" /
  report/hottopic="改成市况速报/改成Hot Topic/改成快讯" /
  report/topic="改成话题文案/改成社区话题/改成Topic文案/改成投资社区文案" /
  report/press="改成新闻稿/改成公告体" /
  report/deck="改成PPT文案/幻灯片体/资料文案" /
  legal/disclosure="改成正式体/改成开示文书" /
  legal/terms="改成利用规约/改成合规文案/改成规约体" /
  legal/disclaimer="改成免责声明/改成法律条款" /
  support/faq="改成FAQ格式/改成问答格式" /
  support/guide="改成客服体/改成支持页面文案/改成手续说明".

  Japanese: "文体を変えて", "レポート風に直して", "SNS向けに短くして",
  "マーケティング向けに書き直して", "です/ます体に変えて",
  "だ/である体に変えて", "研究レポート風に", "広告コピーに", "硬い文体に",
  "柔らかい文体に", "140文字以内に", "客観的な文体に", "書き言葉に直して",
  "スライド用に短くして", "箇条書き向けに", "商品説明文に", "短い商品文案に",
  "使用説明に", "プレスリリース風に", "キャンペーン告知文に", "Push通知文に",
  "EDM・メール文に", "バナーコピーに", "動画スクリプトに", "市況速報に",
  "話題記事に", "コミュニティ投稿に", "トピック記事に",
  "FAQ形式に", "手続き案内に", "利用規約風に", "免責事項風に".

  English: "rewrite in report style", "make SNS-friendly", "change to formal Japanese",
  "convert to marketing copy", "make deck-ready", "convert to product copy",
  "rewrite as press release", "convert to event/campaign copy",
  "convert to short product copy", "convert to push notification",
  "convert to EDM copy", "convert to banner copy", "convert to video script",
  "convert to hot topic", "convert to topic article", "convert to community post",
  "rewrite as FAQ", "convert to user guide",
  "rewrite as terms of service", "rewrite as disclaimer".

  Implicit trigger: user pastes Japanese text alongside a style keyword
  (formal / report / marketing / sns / 正式 / 研報 / 営業 / SNS / 商品説明 / FAQ).

  Do NOT activate for: translation requests (→ lark-cn2jp-finance),
  summarization, or non-Japanese text without existing Japanese input.
---

# jp-style-optimizer

## Stance

Applies editorial discipline to existing Japanese financial text. Does not translate, does not add information, does not generate new claims.

---

## Red Lines

- **RL-1 Term lock** — Never change a financial/technical term to a synonym, abbreviation, or colloquial equivalent. Extract all terms before transforming. Verify every extracted term appears unchanged in output.
- **RL-2 Information injection** — Never add facts, figures, or claims not present in the source text. Output propositional content must be a strict subset of input. Verify by scanning output for: (a) any specific number not present in input; (b) any named entity (company, product, person, feature name) not in input; (c) any causal or outcome claim not derivable from input. Flag each found item with「⚠ RL-2: [injected content]」before delivering.
- **RL-3 情報分析 + subjective** — 情報分析 (report/press/deck/hottopic/topic) output must not contain 「思います」「感じます」「〜と思う」「〜と感じる」. Scan output before delivery.
- **RL-4 Scene hard character limits** — The following scenes have hard character ceilings (full-width = 1 char). Output must state per-field counts in the verification block. If over limit, apply compression rules from style-guide.md before delivering.

  | Scene | Field | Hard limit |
  |-------|-------|-----------|
  | marketing/sns | 全文 | ≤140 |
  | marketing/push | タイトル / 本文 | ≤20 / ≤60 |
  | marketing/edm | 件名 / プリヘッダー / CTA | ≤40 / ≤80 / ≤15 |
  | marketing/banner | メイン / サブ / CTA | ≤15 / ≤25 / ≤8 |
  | report/hottopic | 全文 | ≤140 |
  | report/deck | 各bullet | ≤25 |
- **RL-5 Disclosure register purity** — legal/disclosure scene output must not contain 「です」「ます」. State「です/ますなし: 確認済み」in verification block.
- **RL-6 Translation deflection** — If input is not Japanese (Chinese, English, etc.), return: 「このテキストは日本語ではありません。翻訳が必要な場合は lark-cn2jp-finance を使用してください。」Do not optimize.
- **RL-7 No double negatives** — Avoid 二重否定 (〜ないわけではない / 〜なくはない). Rewrite as a direct positive or qualified statement.
- **RL-8 No noun-phrase stacking** — No sequence of 4+ consecutive nouns without intervening particles. Break up into readable syntax.
- **RL-9 情報分析: unattributed numbers** — In 情報分析 scenes (report/press/deck/hottopic/topic), specific numerical claims must include attribution (〜によれば / 〜によると / 〜の見通しでは). Flag unattributed numbers to the user. Exception: topic scene allows factual market data without formal attribution when the data is widely reported (e.g., index levels, consecutive-day records).
- **RL-10 No passive stacking** — No sentence with 2+ passive constructions (〜される/〜られる). Rewrite to reduce passive load.
- **RL-11 No register mixing** — Output must maintain a single consistent register throughout. Four prohibited mixing patterns: (1) **Verb endings**: だ/である体 + です/ます in same output; (2) **Keigo level**: 謙譲語II (承ります/ございます) outside support register, or plain form inside support register; (3) **Modality markers**: 〜と見られる / 〜と考えられる / 〜見込み in marketing output; (4) **Tone markers**: 「！」or urgency CTA (「今すぐ」) in press/legal/report/support output. Scan all sentence-final forms and tone markers before delivery. State「文体統一: ✓」or list violations. **topic scene exceptions**: (a) topic uses です/ます体 (not だ/である) despite being report T1, because it is community engagement content; (b) 【投稿例】section allows casual/タメ口 register; (c) push subtitle allows invitation form (〜しよう！).
- **RL-12 Marketing CTA** — marketing style output (scenes: lp / sns / event / edm / banner) must contain at least one CTA phrase with a specific action verb. Generic「こちら」alone does not satisfy. Accepted forms: 「開設する」「申し込む」「確認する」「登録する」「今すぐ〜」or scene-equivalent (edm: CTA button ≤15字; banner: CTA button ≤8字). Note: push uses「リンク先示唆」(link destination hint) instead of explicit CTA — RL-12 does not apply to push. Verify: scan output for action verb; if absent → constraint violation, revise before delivering.

---

## Acceptance Criteria

- **AC-1** Input containing 「当期純利益」converted across styles → 「当期純利益」appears verbatim in all outputs.
- **AC-2** Casual Japanese text converted to 情報分析/report → output contains zero instances of 「思います」「感じます」.
- **AC-3** All RL-4 covered scenes → output states per-field character counts in the verification block, and no field exceeds its hard limit.
- **AC-4** Per-scene character count format in verification block: marketing/sns and report/hottopic include total count (e.g.,「87文字 ✓」); marketing/push includes title and body counts (e.g.,「タイトル: 18文字 ✓ / 本文: 55文字 ✓」); marketing/banner includes main/sub/CTA counts; marketing/edm includes subject/preheader/CTA counts; report/deck includes per-bullet counts.
- **AC-5** legal/disclosure output includes 「です/ますなし: 確認済み」in the verification block.
- **AC-6** 情報分析 output with bare numerical claims includes a flag: 「要出典: [数値]」.
- **AC-7** 営業推広 output → at least one benefit claim names a specific detail (number, feature name, or named outcome). [CTA action verb requirement: see RL-12]
- **AC-8** report/hottopic output → zero subjective expressions (思います/感じます) + numerical claims have attribution + total character count ≤ 140.

---

## Style Routing

Two-parameter routing: `--style` sets Tier 1 register; `--scene` sets Tier 2 structural template and sentence targets.

### Tier 1 — 文案風格類

| `--style` | 文案風格類 | 共通レジスタ制約 |
|-----------|----------|----------------|
| `marketing` | 営業推広 | です/ます体; CTA必須; ベネフィット先行; 能動態; Pathos主導 |
| `product` | 産品説明 | です/ます体; 機能→ベネフィット構造; 専門用語初出説明; Logos主導 |
| `report` | 情報分析 | 第三者・客観体; 推測表現必須; 無主観; Logos/Ethos主導 |
| `legal` | 法律合規 | 免責構文; リスク警告必須; 宣伝ゼロ; Ethos主導 |
| `support` | 客服支援 | 謙譲語II (承ります/ございます); お/ご接頭辞全体; 機能的CTAのみ; Ethos主導 |

### Tier 2 — 応用場面

| `--scene` | 応用場面 | `--style` | 句長目標(字/文) | 情報構造 |
|-----------|---------|-----------|----------------|---------|
| `lp` | LP・落地页 | marketing | 20–35 | 利益→証明→特徴→CTA |
| `sns` | SNS・ソーシャル | marketing | 10–25 (総計≤140) | フック→主張→CTA |
| `event` | 活動告知・キャンペーン | marketing | 15–25 | 期限/名称→条件→特典→CTA |
| `push` | Push通知 | marketing | タイトル≤20; 本文≤60 | タイトル→本文→リンク先示唆 |
| `edm` | EDM・メールマーケティング | marketing | 件名≤40; プリヘッダー≤80; 本文20–35 | 件名→プリヘッダー→本文(利益→詳細→CTA) |
| `banner` | アプリ内バナー | marketing | メイン≤15; サブ≤25 | メインコピー→サブコピー→CTAボタン |
| `short` | 短産品文案・卖点提炼 | product | 15–25 | 卖点→差異化→CTA（任意）|
| `detail` | 詳細説明ページ | product | 20–35 | 機能→ベネフィット→説明→CTA（任意）|
| `manual` | 使用説明・手順書 | product | 20–40 | 目的→前提条件→手順→注意事項 |
| `script` | 動画・音声スクリプト | product | ≤30 | 導入(フック)→説明→まとめ/CTA |
| `report` | 研報・週報 | report | 20–35 | 背景/現状→分析→見通し |
| `press` | プレスリリース | report | 20–40 | 5W概要→詳細→背景 |
| `deck` | スライド・デッキ | report | ≤25/bullet | 数値/キーワード→簡潔な修飾 |
| `hottopic` | 市況速報・ホットトピック | report | 15–25 (総計≤140) | 事実→影響/背景→見通し(任意) |
| `topic` | 話題記事・コミュニティ投稿 | report | 25–50 | タイトル→事実/現状→分析/背景→見通し/焦点→読者参加→投稿例→投票→Push |
| `disclosure` | 開示文書・目論見書 | legal | 30–50 | 命題→根拠→条件/義務 |
| `terms` | 利用規約 | legal | 40–60 | 対象範囲→義務→条件→例外 |
| `disclaimer` | 免責事項 | legal | 40–60 | 対象範囲→義務→条件→免責→リスク警告 |
| `faq` | FAQ・よくある質問 | support | 20–35 | 質問→回答→手順/チャネル |
| `guide` | 手続き案内 | support | 20–40 | 手続き種別→手順/チャネル→代替案内 |

### Routing Rules

**Scene inference** (when `--scene` is omitted):

| `--style` | Default `--scene` |
|-----------|-------------------|
| marketing | `lp` |
| product | `detail` |
| report | `report` |
| legal | `disclaimer` |
| support | `faq` |

**Backward compatibility**: Old single-flag calls map to: `formal`→`legal/disclosure`, `sns`→`marketing/sns`, `event`→`marketing/event`, `press`→`report/press`, `deck`→`report/deck`.

**Style + scene inference** (when flags are omitted): See keyword-to-route mapping in `references/style-guide.md` § Routing Inference Table.

### User Segment Strategy (optional `--segment`)

When `--segment` is provided, the optimizer injects segment-specific psychological strategy constraints alongside T1+T2. Same text + different segment → different copy angle and CTA tone.

| `--segment` | Label | Funnel Stage | Psychology | CTA Stage |
|-------------|-------|-------------|-----------|-----------|
| `churn` | 流失召回 | re-engagement | loss_aversion, curiosity_gap | warm |
| `never_traded` | 未首交 | activation | low_barrier, social_proof | cold |
| `high_value` | 高資産・高潜在 | expansion | exclusivity, performance | hot |
| `jp_stock_only` | 日本株のみ | cross-sell | opportunity, fomo | warm |
| `us_stock_only` | 米国株のみ | cross-sell | opportunity, fomo | warm |
| `inactive` | 無効戸 | reactivation | low_barrier, incentive | cold |

**CTA stage alignment**: Cold→「まずは詳しくみる」/ Warm→「もう一度チェック」/ Hot→「今すぐ申し込む」. The segment's `cta_stage` overrides the generic T1 CTA guidance.

**Auto-detection from spreadsheet D column**: `resolve_segment(raw_text)` maps D column text (e.g., "流失召回", "高资高潜", "无效户") to segment keys via pattern matching. Returns `None` if unrecognized.

---

## Workflow

Read `references/style-guide.md` before executing.

### Step 1 — Language Gate (RL-6)

Detect input language. If not Japanese → return delegation message. Do NOT proceed.

### Step 2 — Term Lock + Source Analysis

**2a. Term Lock** — List all financial and technical terms found in the input.

```
術語ロック: [term1], [term2], [term3], ...
```

If no financial terms found, state「専門用語なし」.

**2b. Information Priority** — Identify the sequence in which information is ordered in the source text. Choose one:
- `結論先行` — conclusion/claim appears before supporting evidence
- `背景先行` — background/context precedes the main claim
- `手順型` — sequential steps (A→B→C)
- `並列型` — parallel items with no priority hierarchy

```
情報構造: <結論先行|背景先行|手順型|並列型>
```

**2c. Dominant Proof** — Identify which rhetorical dimension dominates the source:
- `Logos` — data, logic, evidence
- `Ethos` — authority, credibility, institutional voice
- `Pathos` — emotion, urgency, aspiration

```
主導証明: <Logos|Ethos|Pathos>
```

These three outputs inform Step 4 restructuring decisions. They do not change what is said — only what gets reordered or foregrounded.

### Step 3 — Style + Scene Routing

Determine `--style` (Tier 1) and `--scene` (Tier 2) from flags or infer per Routing Rules. State both:

```
スタイル: <marketing|product|report|legal|support>
シーン: <lp|sns|event|push|edm|banner|short|detail|manual|script|report|press|deck|hottopic|topic|disclosure|terms|disclaimer|faq|guide>
```

### Step 3.5 — Brand Voice Match (optional)

If input contains a brand name listed in `references/case-library.md`, or user requests brand-specific voice:
1. Load the matching brand entry from case-library.md.
2. Add brand voice signature constraints to Step 4 transform parameters.
3. In Step 6, compare output against the brand's benchmark excerpt and anti-patterns.

State「ブランド: [brand name]」or「ブランド: なし（汎用）」.

### Step 3.6 — Segment Resolution (optional)

If `--segment` is provided or if the source context includes user segment metadata (e.g., spreadsheet D column text like "流失召回", "高资高潜", "无效户"):

1. Resolve segment key via `resolve_segment(raw_text)` or accept explicit `--segment` value.
2. Load segment strategy from `SEGMENTS[key]` — psychology triggers, funnel stage, CTA stage, angle, avoid rules.
3. Inject segment constraints into transform parameters (alongside T1+T2).
4. CTA stage from segment overrides generic T1 CTA guidance.

State「セグメント: [label]（[funnel_stage] / CTA: [cta_stage]）」or「セグメント: なし」.

**Segment affects Layer 3 (Proof & Frame)**: The segment's psychology list determines which persuasion dimension to foreground. For example, `loss_aversion` → emphasize missed opportunities; `low_barrier` → minimize perceived risk; `exclusivity` → highlight premium/advanced features.

### Step 4 — Transform

Transform in three layers, in order. Do not add claims not in the source.

**Layer 1 — Structure** (uses 情報構造 + target scene's 情報構造 from Tier 2 table)

Compare source 情報構造 against the target scene's required sequence. If they differ, reorder content to match target priority before applying any linguistic changes.

**Layer 2 — Language** (uses Tier 1 shared constraints + Tier 2 scene constraints from style-guide.md)

Apply sentence-by-sentence: verb endings, keigo level, voice (active/passive), sentence length, vocabulary register. Reference term lock list throughout — every locked term must appear unchanged.

**Layer 3 — Proof & Frame** (uses 主導証明)

Adjust how the dominant proof is expressed for the target Tier 1:

| 主導証明 | legal / report | marketing / event / sns | product / support |
|---|---|---|---|
| Logos | State factually or with attribution (〜によれば) | Simplify to single strongest claim | Feature→benefit structure |
| Ethos | Institutional language, full terms | Brand authority + social proof | Credibility signals, reassurance |
| Pathos | Suppress — reframe as factual consequence | Amplify — urgency, aspiration, loss-aversion | Moderate — user reassurance only |

Do not change the argument or add claims. Only change which dimension is foregrounded and how it is expressed.

**Marketing reader-centricity check** (Layer 3 post-step): After Layer 3, scan marketing output for company-subject sentences (「当社は」「弊社は」as grammatical subject). Each must be reframed to reader-benefit or experience subject. See style-guide.md Shared Constraints: Reader-centric reframing + Swipe Patterns.

### Step 5 — Inline Verification

Run all applicable checks and state results explicitly:

**All styles:**
- RL-1: Confirm each term in the lock list appears in output. If any is missing → revise before continuing.
- RL-7: Scan for 〜ないわけではない / 〜なくはない. State findings or「二重否定なし: ✓」
- RL-8: Scan for 4+ consecutive nouns. State findings or「名詞連続なし: ✓」
- RL-10: Scan for sentences with 2+ passive constructions. State findings or「受け身連続なし: ✓」
- RL-11: Scan (1) verb endings for だ/である + です/ます mixing; (2) keigo level for 謙譲語II outside support or plain form inside support; (3) modality markers 〜と見られる/〜見込み in marketing; (4) tone markers 「！」/「今すぐ」in press/legal/report/support. State「文体統一: ✓」or list violations and revise.

**legal/disclosure only:**
- RL-5: Scan output for「です」「ます」. State「です/ますなし: 確認済み」or list found instances and revise.

**情報分析 (report/press/deck/hottopic/topic) only:**
- RL-3: Scan for「思います|感じます|と思う|と感じる」. State「主観表現なし: ✓」or revise.
- RL-9: Identify bare numerical claims. State「要出典: [数値]」for each, or「未出典数値なし: ✓」

**Scenes with hard character limits (RL-4):**
- Count characters per field as defined in the RL-4 table. State per-field counts (e.g.,「87文字 ✓」for whole-text scenes; 「タイトル: 18文字 ✓ / 本文: 55文字 ✓」for multi-field scenes). If any field exceeds its hard limit, apply compression rules from style-guide.md and recount.
- Applies to: marketing/sns, marketing/push, marketing/edm, marketing/banner, report/hottopic, report/deck.

**marketing / scenes: lp, sns, event, edm, banner only:**
- RL-12: Scan output for action verb CTA. If absent → constraint violation; add CTA before delivering. State「CTA確認: ✓」or「RL-12違反: CTA欠如 → [revised CTA]」. Note: push uses「リンク先示唆」instead of explicit CTA — RL-12 does not apply to push.

**All styles — sentence length soft check:**

Compute average characters per sentence. Check against the target scene's 句長目標 from the Tier 2 table.

- **Hard limits**: RL-4 表中所有場面 → must revise if over limit.
- **Soft limits**: all other scenes — flag but do not force revision unless Step 6 also flags.

State「平均X字/文 ✓」or「平均X字/文 — 要確認」.

**All scenes — Scene Fit check:**

Run this scene's Checkpoint from style-guide.md. For each item state ✓ or ✗; for each ✗ apply correction before continuing. State「場面適合: X/N ✓」(X = passed, N = total). All items must pass (X = N) before Step 6.

### Step 6 — Naturalness Check

**Primary test**: Would a native editor at the reference organization (listed in style-guide.md Source field for this style) approve this output without revision?

**Proxy check 1 — Cross-register vocabulary leakage**: Scan for vocabulary characteristic of a *different* register tier that has leaked into the output:
- marketing output: flag 〜に際しまして / 〜において / 〜との観点から (formal leakage)
- report output: flag すごく / やっぱり / とても / もちろん (colloquial leakage)
- legal output: flag お得 / ぜひ / 今すぐ / 絶対 (promotional leakage)
- support output: flag 「！」or bare imperative forms without honorific (urgency leakage)

If any found → revise. State「語彙漏れなし: ✓」or list found items.

**Proxy check 2 — Sentence variety**: For outputs of ≥3 sentences, check that sentence lengths vary (not all identical). Uniform length across all sentences signals mechanical output. State「文長分布: 自然」or「文長分布: 単調 — 要調整」.

**Proxy check 3 — Reference comparison**: Compare output structure against the closest Example in this scene's T2 section in style-guide.md. State「参照一致: ✓」or note the structural gap.

**Proxy check 4 — Brand voice match** (only when Step 3.5 identified a brand): Compare output against the brand's benchmark excerpt and anti-patterns in case-library.md. Check that no anti-pattern appears in output. State「ブランド適合: [brand] ✓」or list deviations.

If all applicable proxy checks pass → state「自然さ: 問題なし」. If any fail → revise before delivering.

---

## Output Format

```
術語ロック: [terms]
スタイル: <style> / シーン: <scene>
セグメント: <label (funnel_stage / CTA: cta_stage)> or なし

原文：<original>
润色：<styled>

検証:
  [verification results from Step 5]
  平均X字/文: <✓ or 要確認>
  場面適合: X/N ✓
  自然さ: [naturalness note or「問題なし」]

改動：[change1] [change2] ...
```

---

## References

| File | Content | Load When |
|------|---------|-----------|
| `references/style-guide.md` | Per-style/scene constraints, rewrite patterns, examples, routing inference | Always — before Step 4 |
| `references/case-library.md` | Brand voice signatures, benchmarks, anti-patterns | When input contains a brand name or brand-specific voice requested (Step 3.5) |
| `diagnosis/cross-style-quality-rubric.md` | D1–D9 scoring criteria, per-style D9 definitions, pass thresholds | When evaluating output quality or diagnosing style-specific effectiveness |

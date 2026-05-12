---
name: jp-style-optimizer
version: 6.0.0
description: >
  Activate when the user provides existing Japanese text and requests a register or
  style change — NOT translation. Trigger phrases by language:

  Chinese (general): "润色日语文案", "日语润色", "日文润色", "日语文案优化",
  "日语优化", "优化日语", "文案优化", "把这段日语改成…", "日语文体转换",
  "改写日语", "让日语更正式", "让日语更口语", "让日语更简短", "让日语更专业".

  Chinese (by style/scene):
  campaign/launch="改成活动文案/营销活动化/改成推广文案/改成广告风格/日语广告化/改成SNS格式/改成Push通知/改成EDM" /
  campaign/remind="改成提醒文案/催促文案" /
  campaign/lastday="改成最后一天文案/截止日提醒" /
  trade-ideas/theme="改成投资分析/改成赚效内容/改成市场分析+行动建议" /
  trade-ideas/flash="改成市场速报/改成热点" /
  trade-ideas/earnings="改成财报分析" /
  trade-ideas/morning="改成早间简报/改成日报" /
  news/flash="改成客观速报/改成新闻体/纯事实报道" /
  news/earnings="改成决算速报" /
  product/short="改成短产品文案/改成卖点文案/产品卖点提炼" /
  product/detail="改成产品说明/商品文案" /
  product/manual="改成使用说明/改成操作指南" /
  product/script="改成视频脚本/改成配音稿" /
  product/release="改成更新日志/改成发布说明" /
  compliance/disclosure="改成正式体/改成开示文书" /
  compliance/terms="改成利用规约/改成合规文案/改成规约体" /
  compliance/disclaimer="改成免责声明/改成法律条款" /
  compliance/faq="改成FAQ格式/改成问答格式" /
  compliance/guide="改成客服体/改成支持页面文案/改成手续说明".

  Japanese: "文体を変えて", "レポート風に直して", "SNS向けに短くして",
  "マーケティング向けに書き直して", "です/ます体に変えて",
  "だ/である体に変えて", "研究レポート風に", "広告コピーに", "硬い文体に",
  "柔らかい文体に", "140文字以内に", "客観的な文体に", "書き言葉に直して",
  "スライド用に短くして", "箇条書き向けに", "商品説明文に", "短い商品文案に",
  "使用説明に", "プレスリリース風に", "キャンペーン告知文に", "Push通知文に",
  "EDM・メール文に", "バナーコピーに", "動画スクリプトに", "市況速報に",
  "話題記事に", "コミュニティ投稿に", "トピック記事に",
  "FAQ形式に", "手続き案内に", "利用規約風に", "免責事項風に",
  "投資アイデアに", "朝の市場ブリーフに", "決算ハイライトに".

  English: "rewrite as campaign copy", "make SNS-friendly", "change to formal Japanese",
  "convert to marketing copy", "convert to product copy", "rewrite as press release",
  "convert to event/campaign copy", "convert to short product copy",
  "convert to push notification", "convert to EDM copy", "convert to banner copy",
  "convert to video script", "convert to hot topic", "convert to topic article",
  "convert to community post", "rewrite as FAQ", "convert to user guide",
  "rewrite as terms of service", "rewrite as disclaimer", "convert to investment idea",
  "convert to trade ideas", "convert to news flash", "convert to morning brief".

  Implicit trigger: user pastes Japanese text alongside a style keyword
  (formal / report / marketing / sns / 正式 / 研報 / 営業 / SNS / 商品説明 / FAQ /
  キャンペーン / 速報 / 投資アイデア / 合規).

  Do NOT activate for: translation requests (→ lark-cn2jp-finance),
  summarization, or non-Japanese text without existing Japanese input.
---

# jp-style-optimizer

## Stance

Applies editorial discipline to existing Japanese financial text. Does not translate, does not add information, does not generate new claims.

**Platform footer assumption** (ADR-006): trade-ideas/{flash, picks, earnings, morning短尺, community短尺} outputs do NOT include an individual disclaimer line. They presuppose that the delivery platform (app push, broker dashboard, SNS feed) carries a blanket disclaimer footer. The skill does not verify this presupposition — operators are responsible for ensuring platform-level coverage. Long-form scenes (theme / morning長尺 ≥ 500字) still require an inline disclaimer per AC-10.

---

## Red Lines

- **RL-1 Term lock** — Never change a financial/technical term to a synonym, abbreviation, or colloquial equivalent. Extract all terms before transforming. Verify every extracted term appears unchanged in output.
- **RL-2 Information injection** — Never add facts, figures, or claims not present in the source text. Output propositional content must be a strict subset of input. Verify by scanning output for: (a) any specific number not present in input; (b) any named entity (company, product, person, feature name) not in input; (c) any causal or outcome claim not derivable from input. Flag each found item with「⚠ RL-2: [injected content]」before delivering.
- **RL-3 news + trade-ideas: no subjective expressions** — news and trade-ideas analysis sections must not contain「思います」「感じます」「〜と思う」「〜と感じる」. Scan output before delivery.
- **RL-4 Scene hard character limits** — The following scenes have hard character ceilings (full-width = 1 char). Output must state per-field counts in the verification block. If over limit, apply compression rules from the style's guide file before delivering.

  | Scene | Field | Hard limit |
  |-------|-------|-----------|
  | campaign (all scenes) / sns channel | 全文 | ≤140 |
  | campaign / push channel | タイトル / 本文 | ≤20 / ≤60 |
  | campaign / edm channel | 件名 / プリヘッダー / CTA | ≤40 / ≤80 / ≤15 |
  | campaign / banner channel | メイン / サブ / CTA | ≤15 / ≤25 / ≤8 |
  | trade-ideas/flash | 全文 | ≤140 |
  | news/flash | 全文 | ≤140 |
  | news/alert | 全文 | ≤100 |
  | news/wrap | 全文 | ≤700 |
  | news/digest | 全文 | ≤1200 |
  | news/flash | 見出し | ≤15 |
  | news/alert | 見出し | ≤15 |
  | news/wrap | 見出し | ≤32 |
  | news/earnings | 見出し | ≤32 |
  | news/digest | 見出し | ≤32 |
  | news/indicator | 見出し | ≤24 |
  | product/script | 各文 | ≤30 |
- **RL-5 Disclosure register purity** — compliance/disclosure output must not contain「です」「ます」. State「です/ますなし: 確認済み」in verification block.
- **RL-6 Translation deflection** — If input is not Japanese (Chinese, English, etc.), return:「このテキストは日本語ではありません。翻訳が必要な場合は lark-cn2jp-finance を使用してください。」Do not optimize.
- **RL-7 No double negatives** — Avoid 二重否定 (〜ないわけではない / 〜なくはない). Rewrite as a direct positive or qualified statement.
- **RL-8 No noun-phrase stacking** — No sequence of 4+ consecutive nouns without intervening particles. Break up into readable syntax.
- **RL-9 news + trade-ideas: unattributed numbers** — In news scenes and trade-ideas analysis sections, specific numerical claims must include attribution (〜によれば / 〜によると / 〜の見通しでは). Flag unattributed numbers. Exception: widely reported data (index levels, consecutive-day records) is exempt.
- **RL-10 No passive stacking** — No sentence with 2+ passive constructions (〜される/〜られる). Rewrite to reduce passive load. **Exception (news + trade-ideas analysis sections only)**: Passive forms in PASSIVE_ALLOW_LIST (とみられる / と発表された / と報じられた / と見込まれる / と指摘される / と位置付けられる, incl. 表記揺れ 見られる/位置づけられる) are excluded from the 2+受け身 count. Other passive constructions in the same sentence still count toward the limit. Allow-list does NOT apply to campaign / product / compliance, nor to trade-ideas reader-action sections.
- **RL-11 No register mixing** — Output must maintain a single consistent register throughout. Four prohibited mixing patterns: (1) **Verb endings**: だ/である体 + です/ます in same output; (2) **Keigo level**: 謙譲語II (承ります/ございます) outside compliance/support sub-register, or plain form inside; (3) **Modality markers**: 〜と見られる / 〜と考えられる / 〜見込み in campaign output; (4) **Tone markers**: 「！」or urgency CTA (「今すぐ」) in news/compliance output. Scan all sentence-final forms and tone markers before delivery. State「文体統一: ✓」or list violations. **Exceptions**: (a) trade-ideas allows section-level dual-register: analysis sections だ/である; reader-action sections です/ます — mixing within a single paragraph still prohibited. State「デュアルレジスタ: 分析=だ/である ✓ / 読者=です/ます ✓」. (b) trade-ideas/community allows casual/タメ口 in 【投稿例】section. (c) **news direct-quote carve-out** (ADR-007 §2.2): in news output, verification scans must exclude content inside direct-quote brackets「」— the speaker's original register (です／ます／口語 etc.) is preserved verbatim. Sentences ending in indirect-quote tags (〜と述べた／〜と発表した／〜との見方) are treated as narrative and must be in だ/である体. Run a「」pairing pre-pass before the register scan; on unmatched brackets, emit a warning but continue scanning (treat as narrative for safety).
- **RL-12 Campaign CTA** — campaign output must contain at least one CTA phrase with a specific action verb appropriate to CTA stage: Cold→「まずは詳しくみる」/ Warm→「参加する」/ Hot→「今すぐ申し込む」. Generic「こちら」alone does not satisfy. Verify: state「CTA確認: [stage] ✓」or「RL-12違反: CTA欠如 → [revised CTA]」. Exception: compliance and news output must have NO CTA.

---

## Acceptance Criteria

- **AC-1** Input containing「当期純利益」converted across styles → 「当期純利益」appears verbatim in all outputs.
- **AC-2** Casual Japanese text converted to news or trade-ideas analysis → output contains zero instances of「思います」「感じます」.
- **AC-3** All RL-4 covered scenes → output states per-field character counts in the verification block, and no field exceeds its hard limit.
- **AC-4** Per-scene character count format: flash/sns states total (e.g.,「87文字 ✓」); push states title/body (e.g.,「タイトル: 18文字 ✓ / 本文: 55文字 ✓」); banner states main/sub/CTA; edm states subject/preheader/CTA.
- **AC-5** compliance/disclosure output includes「です/ますなし: 確認済み」in the verification block.
- **AC-6** news or trade-ideas output with bare numerical claims includes a flag:「要出典: [数値]」.
- **AC-7** campaign output → at least one benefit/incentive claim names a specific detail (amount, period, condition). CTA action verb present (RL-12).
- **AC-8** news/flash output → zero subjective expressions + numerical claims attributed + total ≤ 140字.
- **AC-9** campaign output includes explicit deadline (具体的な日付 or 残X日).
- **AC-10** trade-ideas/theme or /morning output ≥ 500字 includes disclaimer text at end.
- **AC-11** news output contains zero CTA phrases.
- **AC-12** compliance output contains zero instances of「！」or「今すぐ」.
- **AC-13** news/wrap output ≤ 700字; news/digest output ≤ 1200字 (ADR-007 §2.1). Verification block states「全文: X字 ✓」.
- **AC-14** news output containing direct-quote「」spans → verification block states「引用ペアリング: N組 ✓」and confirms register scan excluded quote interiors (ADR-007 §2.2).
- **AC-15** trade-ideas/picks output contains ≥2 numerical metrics (price target, P/E, growth rate, yield, etc.). State「数値指標: N件 (≥2 ✓)」.
- **AC-16** campaign output contains zero instances of CA-11 prohibited vocabulary (必勝 / 絶対 / 確実 / 100% / 間違いなし). State「禁止語彙: 0件 ✓」or list violations.

---

## Style Routing

Two-parameter routing: `--style` sets Tier 1 register; `--scene` sets Tier 2 structural template and sentence targets.

### Tier 1 — 文案風格類

| `--style` | 文案風格類 | 共通レジスタ制約 |
|-----------|----------|----------------|
| `campaign` | 营销活动类 | です/ます体; CTA必須(stage別); 期限必須; Pathos主導 |
| `trade-ideas` | 赚效内容类 | デュアルレジスタ(分析:だ/である + 読者:です/ます); 行動橋渡し必須; Logos主導 |
| `news` | 新聞事件类 | だ/である体; CTA禁止; 分析≤30%; 時点明示必須; Logos主導 |
| `product` | 产品运营类 | です/ます体; F→B必須ペア; CTA任意(低コミットメント); Logos主導 |
| `compliance` | 合規服務类 | scene別レジスタ(disclosure=だ/である; 他=です/ます+謙譲語II); 宣伝性ゼロ; Ethos主導 |

### Tier 2 — 応用場面

| `--scene` | 応用場面 | `--style` | 句長目標(字/文) | 情報構造 |
|-----------|---------|-----------|----------------|---------|
| `launch` | キャンペーン開始告知 | campaign | LP:20–35; Push:≤20/≤60 | 特典名称→条件→期限→CTA |
| `remind` | リマインド・中間アラート | campaign | Push:≤80; EDM:200–400 | 残り期間→現状→行動促進→CTA |
| `lastday` | 最終日・ラストチャンス | campaign | Push:≤80; SNS:≤140 | 「本日最終」→特典→CTA(Hot) |
| `result` | 結果通知・達成報告 | campaign | Push:≤80; アプリ内100–200 | 結果→特典→次のステップ |
| `seasonal` | 季節/イベント連動型 | campaign | LP:400–1000 | 市場コンテクスト→特典→条件→期限→CTA |
| `referral` | 紹介・友達招待型 | campaign | SNS/EDM:200–400 | 紹介特典(双方)→条件→方法→CTA |
| `flash` | 市場速報 | trade-ideas | ≤140 | 事実(数値)→影響→行動示唆 |
| `theme` | テーマ分析・投資アイデア | trade-ideas | 500–1500 | テーマ背景→データ→銘柄→投資視点→免責 |
| `earnings` | 決算ハイライト | trade-ideas | 200–500 | 決算概要→ポイント→株価反応→見通し |
| `morning` | 朝のブリーフ・デイリー | trade-ideas | 300–800 | 前日振り返り→本日注目→注目銘柄/セクター |
| `picks` | 注目銘柄カード | trade-ideas | 80–200/銘柄 | 銘柄名→注目理由→基本指標→テーマタグ |
| `community` | コミュニティ投資話題 | trade-ideas | 400–800+参加モジュール | タイトル→事実→投資視点→読者参加 |
| `flash` | 市況速報 | news | ≤140 | 事実(数値)→影響 |
| `wrap` | 市場まとめ・ラップアップ | news | 300–600 | 主要指標→個別イベント→明日注目点 |
| `earnings` | 決算速報 | news | 150–400 | 決算概要→主要数値→会社コメント |
| `indicator` | 経済指標速報 | news | 100–300 | 指標名→実績/予想/前回→影響 |
| `digest` | ニュースダイジェスト | news | 500–1000 | 見出し→事実サマリー(繰り返し) |
| `alert` | 相場アラート | news | ≤100 | 閾値到達事実→数値→時点 |
| `short` | 短産品文案・USPカード | product | 30–80 | 卖点→差異化→CTA(任意) |
| `detail` | 詳細説明ページ | product | 200–500/セクション | 機能→ベネフィット→説明→CTA(任意) |
| `manual` | 使用説明・手順書 | product | 150–400 | 目的→前提→手順→注意事項 |
| `script` | 動画・音声スクリプト | product | ≤30/文 | 導入(フック)→説明→まとめ/CTA |
| `release` | リリースノート・更新情報 | product | 100–300 | バージョン/日付→変更点→影響→手順 |
| `onboard` | オンボーディング | product | 200–500 | ゴール提示→ステップ→達成確認 |
| `compare` | 比較表・USP対比 | product | 100–200+表 | 比較軸→表→補足1–2文 |
| `disclosure` | 開示文書・目論見書 | compliance | 30–50 | 命題→根拠→条件/義務 |
| `terms` | 利用規約・取引約款 | compliance | 40–60 | 対象範囲→義務→条件→例外 |
| `disclaimer` | 免責事項 | compliance | 40–60 | 対象範囲→義務→条件→免責→リスク警告 |
| `faq` | FAQ・よくある質問 | compliance | 20–35 | 質問→回答→手順/チャネル |
| `guide` | 手続き案内・操作ガイド | compliance | 20–40 | 手続き種別→手順→チャネル→代替案内 |

### Routing Rules

**Scene inference** (when `--scene` is omitted):

| `--style` | Default `--scene` |
|-----------|-------------------|
| campaign | `launch` |
| trade-ideas | `theme` |
| news | `flash` |
| product | `detail` |
| compliance | `disclaimer` |

**Backward compatibility**: See `references/style-guide.md` Backward Compatibility table for old `--style marketing/report/legal/support` and legacy single-flag calls.

**Style + scene inference** (when flags omitted): See keyword-to-route mapping in `references/style-guide.md` § Routing Inference Table.

### User Segment Strategy (optional `--segment`)

When `--segment` is provided, inject segment-specific psychological strategy constraints alongside T1+T2. Segment affects Layer 3 proof foregrounding and CTA temperature.

| `--segment` | Label | Funnel Stage | Psychology | CTA Stage |
|-------------|-------|-------------|-----------|-----------|
| `churn` | 流失召回 | re-engagement | loss_aversion, curiosity_gap | warm |
| `never_traded` | 未首交 | activation | low_barrier, social_proof | cold |
| `high_value` | 高資産・高潜在 | expansion | exclusivity, performance | hot |
| `jp_stock_only` | 日本株のみ | cross-sell | opportunity, fomo | warm |
| `us_stock_only` | 米国株のみ | cross-sell | opportunity, fomo | warm |
| `inactive` | 無効戸 | reactivation | low_barrier, incentive | cold |

**CTA stage override**: Segment's `cta_stage` overrides generic T1 CTA guidance for campaign style. `resolve_segment(raw_text)` maps metadata text (e.g., "流失召回", "高资高潜", "无效户") to segment keys. Returns `None` if unrecognized.

---

## Workflow

Load `references/style-guide.md` before Step 3. After routing, load `references/{style}-guide.md` before Step 4.

### Step 1 — Language Gate (RL-6)

Detect input language. If not Japanese → return delegation message. Do NOT proceed.

### Step 2 — Term Lock + Source Analysis

**2a. Term Lock** — List all financial and technical terms found in the input.

```
術語ロック: [term1], [term2], ...
```

If no financial terms found, state「専門用語なし」.

**2b. Information Priority** — Identify source text information order. Choose one:
- `結論先行` — conclusion before evidence
- `背景先行` — context precedes main claim
- `手順型` — sequential steps
- `並列型` — parallel items

```
情報構造: <結論先行|背景先行|手順型|並列型>
```

**2c. Dominant Proof** — Identify source dominant dimension:
- `Logos` — data, logic, evidence
- `Ethos` — authority, credibility
- `Pathos` — emotion, urgency, aspiration

```
主導証明: <Logos|Ethos|Pathos>
```

### Step 3 — Style + Scene Routing

Determine `--style` (Tier 1) and `--scene` (Tier 2) from flags or infer per Routing Rules. State both:

```
スタイル: <campaign|trade-ideas|news|product|compliance>
シーン: <launch|remind|lastday|result|seasonal|referral|flash|theme|earnings|morning|picks|community|wrap|indicator|digest|alert|short|detail|manual|script|release|onboard|compare|disclosure|terms|disclaimer|faq|guide>
```

Load `references/{style}-guide.md` for T1 and T2 constraints.

### Step 3.5 — Brand Voice Match (optional)

If input contains a brand name listed in `references/case-library.md`, or user requests brand-specific voice:
1. Load the matching brand entry from case-library.md.
2. Add brand voice signature constraints to Step 4 transform parameters.
3. In Step 6, compare output against the brand's benchmark excerpt and anti-patterns.

State「ブランド: [brand name]」or「ブランド: なし（汎用）」.

### Step 3.6 — Segment Resolution (optional)

If `--segment` is provided or source context includes segment metadata:
1. Resolve segment key via `resolve_segment(raw_text)` or accept explicit `--segment` value.
2. Load segment strategy from the Segment table — psychology triggers, funnel stage, CTA stage.
3. Inject segment constraints into transform parameters (alongside T1+T2).
4. CTA stage from segment overrides generic T1 CTA guidance.

State「セグメント: [label]（[funnel_stage] / CTA: [cta_stage]）」or「セグメント: なし」.

### Step 4 — Transform

Transform in three layers, in order. Do not add claims not in the source.

**Layer 1 — Structure** (uses source 情報構造 + target scene's 情報構造 from Tier 2 table)

Compare source 情報構造 against the target scene's required sequence. If they differ, reorder content to match target priority before applying linguistic changes.

**Layer 2 — Language** (uses T1 shared constraints + T2 scene constraints from `{style}-guide.md`)

Apply sentence-by-sentence: verb endings, keigo level, voice (active/passive), sentence length, vocabulary register. Reference term lock list throughout — every locked term must appear unchanged.

**Layer 3 — Proof & Frame** (uses 主導証明 + T1 Dominant Proof target)

| 主導証明 | compliance / news | campaign | trade-ideas | product |
|---|---|---|---|---|
| Logos | State factually with attribution | Simplify to single strongest incentive claim | State with attribution + action bridge | Feature→Benefit structure |
| Ethos | Institutional language, full terms | Brand authority + social proof for incentive | Credibility signals (data source) | Credibility signals, reassurance |
| Pathos | Suppress entirely | Amplify — deadline, exclusivity, loss-aversion | Moderate — curiosity, not hype | Suppress — user reassurance only |

**Reader-centricity check** (Layer 3 post-step for campaign): Scan for company-subject sentences (「当社は」「弊社は」as grammatical subject). Each must be reframed to reader-benefit or experience subject.

### Step 5 — Inline Verification

Run all applicable checks. State results explicitly.

**All styles:**
- RL-1: Confirm each term in the lock list appears in output. Missing → revise before continuing.
- RL-7: Scan for 〜ないわけではない / 〜なくはない. State findings or「二重否定なし: ✓」
- RL-8: Scan for 4+ consecutive nouns. State findings or「名詞連続なし: ✓」
- RL-10: Scan for sentences with 2+ passive constructions. State findings or「受け身連続なし: ✓」
- RL-11: Scan (1) verb endings; (2) keigo level; (3) modality markers 〜と見られる/〜見込み in campaign; (4) tone markers「！」/「今すぐ」in news/compliance. State「文体統一: ✓」or list violations and revise. trade-ideas: state「デュアルレジスタ: 分析=だ/である ✓ / 読者=です/ます ✓」.

**compliance/disclosure only:**
- RL-5: State「です/ますなし: 確認済み」or list found instances and revise.

**news + trade-ideas analysis sections:**
- **Quote pairing pre-pass (news only, ADR-007 §2.2)**: Before running RL-3 / RL-9 / RL-11 register scans, pair all「」brackets and mark direct-quote spans. State「引用ペアリング: N組 ✓」or「⚠ 引用ペアリング不整合: [位置] (警告のみ、scan は地の文として続行)」. Direct-quote spans are excluded from RL-3 subjective scan, RL-11 register scan, and RL-9 attribution scan (the speaker's own utterance is the attribution). Indirect-quote tags (〜と述べた／〜と発表した／〜との見方) are scanned as narrative.
- RL-3: Scan for「思います|感じます|と思う|と感じる」outside direct-quote spans. State「主観表現なし: ✓」or revise.
- RL-9: Identify bare numerical claims outside direct-quote spans. State「要出典: [数値]」for each, or「未出典数値なし: ✓」

**news only:**
- Analysis cap: calculate analysis content as % of total. State「分析比率: XX% (≤30% ✓)」. If >30% → flag for re-routing to trade-ideas.
- CTA absence: State「CTA不在: ✓」.

**trade-ideas — theme/morning (≥500字):**
- Disclaimer check: State「免責文言: ✓」or add standard disclaimer before delivering.
- Action bridge check: State「行動示唆あり: ✓」.

**campaign:**
- CA-1: Deadline明示. State「期限: [日付/残日数]確認: ✓」or「CA-1違反: 期限未記載」.
- CA-3: Incentive specificity. State「特典具体化: ✓」or「CA-3違反: 特典が抽象的」.
- RL-12: Scan for action verb CTA. State「CTA確認: [stage] ✓」or flag + revise.

**compliance/faq + guide:**
- State「謙譲語II使用: 確認済み」.

**Scenes with hard character limits (RL-4):**
- Count characters per field. State per-field counts. If any field exceeds its hard limit, apply compression rules from `{style}-guide.md` and recount.

**All styles — sentence length soft check:**
Average characters per sentence vs. target scene's 句長目標. State「平均X字/文 ✓」or「平均X字/文 — 要確認」.

**All scenes — Scene Fit check:**
Run the scene's Checkpoint from `{style}-guide.md`. For each item state ✓ or ✗; for each ✗ apply correction. State「場面適合: X/N ✓」. All items must pass before Step 6.

### Step 6 — Naturalness Check

**Primary test**: Would a native editor at the reference organization for this style approve this output without revision?

**Proxy check 1 — Cross-register vocabulary leakage**: Scan for vocabulary from a different register:
- campaign output: flag 〜に際しまして / 〜において (formal leakage)
- trade-ideas/news output: flag すごく / やっぱり (colloquial leakage)
- compliance output: flag お得 / ぜひ / 今すぐ (promotional leakage)

If any found → revise. State「語彙漏れなし: ✓」or list items.

**Proxy check 2 — Sentence variety**: For ≥3 sentences, check lengths vary. State「文長分布: 自然」or「文長分布: 単調 — 要調整」.

**Proxy check 3 — Reference comparison**: Compare output structure against the closest example in `{style}-guide.md`. State「参照一致: ✓」or note the gap.

**Proxy check 4 — Brand voice match** (only when Step 3.5 identified a brand): Compare against brand's benchmark and anti-patterns in case-library.md. State「ブランド適合: [brand] ✓」or list deviations.

If all applicable checks pass → state「自然さ: 問題なし」. If any fail → revise before delivering.

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
| `references/style-guide.md` | Routing inference table, T1 overview, backward compat | Always — before Step 3 |
| `references/campaign-guide.md` | campaign T1+T2 constraints, scenes, checkpoints | When `--style campaign` routed |
| `references/trade-ideas-guide.md` | trade-ideas T1+T2 constraints, scenes, checkpoints | When `--style trade-ideas` routed |
| `references/news-guide.md` | news T1+T2 constraints, scenes, checkpoints | When `--style news` routed |
| `references/product-guide.md` | product T1+T2 constraints, scenes, checkpoints | When `--style product` routed |
| `references/compliance-guide.md` | compliance T1+T2 constraints, scenes, checkpoints | When `--style compliance` routed |
| `references/case-library.md` | Brand voice signatures, benchmarks, anti-patterns | When input contains a brand name (Step 3.5) |
| `references/moomoo-jp-routing.md` | moomoo JP channel ↔ scene ↔ RL-4 limit map (5 T1 sub-tables + segment table + checklist) | When input contains `moomoo` / `moomoo証券` (Step 3 + Step 3.5; load alongside case-library moomoo entry) |
| `diagnosis/cross-style-quality-rubric.md` | D1–D9 scoring criteria | When evaluating output quality |

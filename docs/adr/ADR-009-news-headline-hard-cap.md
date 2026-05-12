---
id: ADR-009
title: news 見出し字数制約 NC-8 を hard cap として採用、体言止めは soft 推奨
date: 2026-05-11
accepted_date: 2026-05-11
status: accepted
deciders: jp-style-optimizer v6.1.0 boost (team abc2 / Phase 2 prescription)
affects: SKILL.md (RL-4 hard cap 表 — news/{flash,alert,wrap,earnings,digest} 見出し行追加), references/news-guide.md (NC-8)
related: ADR-002-news-report-split, ADR-007-news-length-and-quote-exception, OQ-news-1
---

# ADR-009: news Headline Hard Cap (NC-8) — 字数 Hard, 体言止め Soft

## Context

`diagnosis/domain-research-news.md` Source 1 (共同通信『記者ハンドブック』第 13 版 §見出し)、Source 2 (日経スタイルブック §見出し作成基準)、Source 4 (Reuters Handbook §Headlines)、Source 8 (株探・MINKABU PRESS 配信フォーマット) は、業界横断で **見出し字数の物理的上限**と**体言止め優先**の規範を持つ。実測：

| 配信元 | flash 見出し | wrap 見出し | digest 見出し | earnings 見出し | alert 見出し |
|---|---|---|---|---|---|
| 日経電子版 | 12–18 字 | 22–32 字 | 24–36 字 | 18–28 字 | 10–16 字 |
| Reuters JP | 14–20 字 | 24–30 字 | 26–34 字 | 20–26 字 | 12–18 字 |
| Bloomberg Japan | 12–16 字 | 22–28 字 | 26–34 字 | 18–24 字 | 10–14 字 |
| QUICK | 10–15 字 | — | — | 18–25 字 | 8–14 字 |
| 株探 | — | — | — | 20–30 字 | — |
| 共通中央値 | 14 字 | 26 字 | 30 字 | 22 字 | 12 字 |
| 共通 95-pct 上限 | **15 字** | **32 字** | **32 字** | **32 字** | **15 字** |

体言止めは flash / alert / wrap / digest 見出しで支配的（実測 70-90%）、earnings 見出しは「会社名 + 動詞」型（「○○、増益」「△△、減配」）と体言止め型が混在。

OQ-news-1 (`domain-research-news.md` L661) は NC-8 を **hard 制約** (字数違反は機械検証で fail) とするか **soft 推奨** (Craft 層 D7 採点で評価) とするかを保留していた。

### 候補比較

| 軸 | hard | soft |
|---|---|---|
| 字数上限 | 機械検証可能、false positive 低い (実測 95-pct 境界に合致) | 配信元差分を許容するが境界が曖昧 |
| 体言止め | LLM 出力の自由度を奪う、false positive 高い (動詞型 earnings 見出しを誤判定) | 自然な多様性を保つ |

両軸を分離して扱うのが適切。

## Decision

### NC-8 (見出し制約) を 2 階層で採用する

- **(a) 字数 hard cap**: 各 scene の見出し字数を機械検証可能な hard 制約として SKILL.md RL-4 表に追加。
- **(b) 体言止め soft 推奨**: 体言止め (名詞・名詞句で終止) は推奨だが、scene/対象によって動詞型を許容。Craft 層 D7 採点で評価し、Step 5 強制 check には入れない。

### RL-4 表への追加行 (Fix M4 と統合)

| Scene | Field | Hard limit |
|-------|-------|-----------|
| news/flash | 見出し | ≤15 |
| news/alert | 見出し | ≤15 |
| news/wrap | 見出し | ≤32 |
| news/earnings | 見出し | ≤32 |
| news/digest | 見出し | ≤32 |
| news/indicator | 見出し | ≤24 |

`indicator` は他 4 scene と異なり「指標名 + 実績/予想差分」の半構造化テンプレ ("CPI、予想超え") が支配的なため、24 字で実測 90-pct をカバー。

### NC-8 完全形 (`references/news-guide.md` 追記)

> **NC-8 見出し制約**
> (a) 各 scene の見出し字数は RL-4 表の hard limit に従う。違反は Step 5 で機械検出し fail。
> (b) 体言止めまたは「主語 + 動詞 (連用)」型を推奨。flash / alert / wrap / digest 見出しは体言止め優先 (実測 70-90%)。earnings は動詞型混在を許容 ("○○、増益" / "△△、減配" 等)。indicator は半構造テンプレ ("指標名、評価語") を許容。
> (c) 見出しに modality marker (〜と見られる、〜の見方) を含めない (NC-3 緩和拒絶 — 見出しは事実宣告)。違反は Step 5 で fail。
> (d) 見出しに `！` `？` `…` を使用しない。違反は Step 5 で fail。

(c) と (d) は字数とは独立した hard 制約。`！?…` は news 全 scene で禁止 (NC-7 / RL-11 の延長) で、見出しでも例外なし。

### Verification ブロック追加項目

- 「見出し: X 字 (≤Y) ✓」 — Y は scene 別 hard limit
- 「見出し modality: なし ✓」 (〜と見られる / 〜の見方 / 〜の可能性 検出時は flag)
- 「見出し終止符: なし ✓」 (`！？…` 検出時は flag)
- 「見出し体言止め推奨: ✓ / 動詞型 (許容)」 — Craft 層、強制ではない

## Alternatives Considered

### 候補 A-1: 字数も体言止めも全 hard
- **却下**: earnings 動詞型見出し ("○○、増益") が false positive で fail する。実測 30-40% が動詞型のため、業界規範と乖離する。

### 候補 A-2: 字数も体言止めも全 soft
- **却下**: 字数違反 (例: flash 見出し 25 字) は配信不能事案で、Push 通知/RSS feed/モバイル UI で truncate されて意味が破壊される。soft 化すると恒常的な字数 over が解消されない。

### 候補 A-3 (本 ADR 推奨): 字数 hard / 体言止め soft
- **採用**: 字数は物理境界で機械検証に向き、体言止めは文体多様性を残す soft 推奨。両者の性質差を反映した混合戦略。

### 候補 A-4: 字数 hard、体言止め hard、ただし scene 例外 (earnings のみ動詞型許容)
- **却下**: scene 例外を hard 制約に持ち込むと検証ロジックが複雑化。soft 化で同じ表現力が得られる。Craft 層 D7 で earnings の動詞型は適切に評価可能。

### 候補 B (modality / 終止符): 緩和して `…` のみ許容
- **却下**: `…` (三点リーダー) は省略・余韻を示し、news の事実宣告 (Logos 主導) と相反する。共同通信『記者ハンドブック』も見出しでの三点リーダー使用を非推奨。例外を作る根拠なし。

## Consequences

### Positive

1. **業界実測 95-pct 境界との一致**: 各 scene の hard limit は実測 95-pct に基づき、false positive を実質的に排除。
2. **Push / RSS / モバイル UI との互換**: 字数 hard cap が物理 truncate 境界と整合し、配信フローでの意味破壊を防ぐ。
3. **earnings 動詞型を排除しない**: 体言止め soft 化により、業界慣行 ("○○、増益") が natural register として扱える。
4. **modality / 終止符 hard は news 全体規範との整合**: NC-3 (modality) と NC-7 (register/終止符) の見出し延長として論理的に位置付く。

### Negative

1. **RL-4 hard cap 表の行数増 (現 7 行 → 13 行)**: SKILL.md RL-4 表が見出し行を 6 件追加することで肥大化。→ 緩和策: 見出し行をひとつのグループ "news 見出し" として表内でサブセクション化、視覚的に折り畳む。
2. **見出し / 本文の 2 階層字数管理**: 本文字数 (ADR-007) と見出し字数 (本 ADR) の 2 つを scene ごとに維持する必要。実装上は同じテーブルを参照するが、ユーザー認知上は独立した 2 つの制約として理解する必要がある。→ 緩和策: news-guide.md 冒頭に「news scene の字数管理は **見出し** と **本文** が独立した 2 階層」と明示。
3. **体言止め soft が "事実上 hard" 化するリスク**: Craft 層 D7 採点で体言止め違反が連続的に減点される実装になると、実質的に hard と変わらなくなる。→ 緩和策: Craft 層 D7 採点ルーブリックに「earnings の動詞型は減点対象外」を明記 (Phase 3 で `diagnosis/cross-style-quality-rubric.md` 改訂時に反映)。

### Scene-by-Scene Impact (見出し)

| Scene | 字数 hard | 体言止め推奨 | 動詞型許容 | 備考 |
|---|---|---|---|---|
| flash | ≤15 | ✓ | △ (短すぎて動詞型困難) | Push 通知互換 |
| alert | ≤15 | ✓ | △ | 「閾値到達」型多い |
| wrap | ≤32 | ✓ | △ (体言止め支配的) | "東京株、続伸" 等 |
| earnings | ≤32 | ○ | ✓ | "○○、増益" 動詞型 30-40% |
| indicator | ≤24 | ○ | ✓ | "CPI、予想超え" 半構造型 |
| digest | ≤32 | ✓ | △ | 体言止め支配的 |

### テスト・互換性

- 新規追加: `build/tests/news-headline-*.snapshot.md` を 6 scene × 体言止め/動詞型 で各 1 件、計 12 件の検証サンプル想定。
- 既存 news snapshot で見出しが 32 字を超えるものは再生成必要（推定 2-4 件、wrap/digest/earnings の長め見出し）。
- AC への追加: AC-18「news 全 scene 見出し字数は hard limit 内 ✓」(Phase 3 判断、Phase 1.8 synthesis では未含)。

## References

### Internal
- `diagnosis/domain-research-news.md` — Source 1 (共同通信)、Source 2 (日経)、Source 4 (Reuters)、Source 5 (Bloomberg)、Source 8 (株探)、Source 7 (QUICK)、Open Question OQ-news-1
- `docs/adr/ADR-007-news-length-and-quote-exception.md` — 本文字数 (wrap 700 / digest 1200) と見出し字数の 2 階層管理
- `docs/adr/ADR-002-news-report-split.md` — news T1 確立
- `references/news-guide.md` — Phase 3 で NC-8 を追加する対象
- `diagnosis/cross-style-quality-rubric.md` — D7 採点ルーブリック (Phase 3 で体言止め soft 推奨を追記)

### External
- **共同通信社『記者ハンドブック — 新聞用字用語集』第 13 版** §見出し作成 — 体言止め優先、字数厳守、modality 排除
- **日本経済新聞社『日経スタイルブック』** §見出し基準 — 字数帯 (flash 15 / wrap 30 / digest 32)
- **Reuters Handbook of Journalism** §Headlines — "active, present-tense, factual"
- **株探 / MINKABU PRESS 配信フォーマット仕様**（編集部公開ガイド） — earnings 動詞型見出し慣行

---
id: ADR-008
title: trade-ideas に `--segment institutional` を追加し全文だ/である単一レジスタへ切替
date: 2026-05-11
accepted_date: 2026-05-11
status: accepted
deciders: jp-style-optimizer v6.1.0 boost (team abc2 / Phase 2 prescription)
affects: SKILL.md (Segment table, RL-11 trade-ideas exception, Step 3.6), references/trade-ideas-guide.md (TI-2.ext)
related: ADR-003-trade-ideas-dual-register, OQ-TI-2
---

# ADR-008: trade-ideas Institutional Segment — Full だ/である Single-Register Override

## Context

ADR-003 は `trade-ideas` に **section-level dual-register** を許容した（分析セクション=だ/である、読者呼びかけセクション=です/ます、段落跨ぎ混在は禁止）。これはリテール向け配信の現実 — 機関的な分析根拠と読者向け行動橋渡しの両立 — を反映した妥協である。

しかし domain-research-trade-ideas.md (Source 9 CFA Standards V(B)/VI(A)、Source 5 野村・大和 機関投資家向けレポート、Source 11 QUICK Money World プロ向けセクション) は、**機関投資家向け / プロ専用配信**では一貫して全文だ/である体・読者直接呼びかけ無し・CTA 抑制の文体規範を採用していることを示した。リテール dual-register と機関単一-register の境界は **読者層**で決まる。

現 v6.0.0 の `--segment` パラメータは 6 値（churn/never_traded/high_value/jp_stock_only/us_stock_only/inactive）でリテール顧客層のファネル位置を表現するが、**機関読者層**に対応する segment は存在しない。OQ-TI-2 (`domain-research-trade-ideas.md` L607) はこの欠落を指摘し、解決策として (a) 新 T1 style の追加 / (b) 既存 segment 機構の拡張 / (c) `--style report` の復活 の 3 案を提示した。

### 候補比較

| 案 | 内容 | Pros | Cons |
|---|---|---|---|
| **(a) 新 T1 style `institutional-research`** | 6 番目の T1 を追加 | 制約セットを完全分離可能 | T1 = 5 styles の v6.0.0 アーキテクチャを破壊。case-library / 全 RL の 1 列拡張が必要。複雑度 vs 価値が見合わない |
| **(b) 本 ADR 推奨**: `--segment institutional` を 7 番目の segment 値として追加 | 既存 Step 3.6 segment resolution に組込み | アーキテクチャ無傷、構成変更最小、CTA stage 抑制と register 切替を同一機構で表現可能 | RL-11 trade-ideas 例外文言に segment 条件を追加する必要 |
| **(c) `--style report` を ADR-002 で merge した状態から復活** | 旧 v5.x 互換 | 名称が直感的 | ADR-002 で確定済みの news/report split を撤回することになり、依存系統が広範囲に波及 |

## Decision

**`--segment institutional` を 7 番目の segment 値として追加する**。`trade-ideas` style 適用時に限り、既存の RL-11 dual-register 例外を**上書き**して全文だ/である単一-register を強制する。campaign / news / product / compliance では `--segment institutional` は無視される（後方互換のため、warning は出さず resolve_segment が既定値 None を返す）。

### Segment 表への追加行

| `--segment` | Label | Funnel Stage | Psychology | CTA Stage | Register Override |
|-------------|-------|-------------|-----------|-----------|------------------|
| `institutional` | 機関投資家・プロ | research | logos_only, attribution_first | none | だ/である単一（trade-ideas のみ） |

### RL-11 trade-ideas 例外の改訂（追記のみ、既存文言は不変）

> **Exceptions**: (a) trade-ideas allows section-level dual-register: analysis sections だ/である; reader-action sections です/ます — mixing within a single paragraph still prohibited. State「デュアルレジスタ: 分析=だ/である ✓ / 読者=です/ます ✓」.
> **(a-1) ただし `--segment institutional` 指定時は dual-register 例外を抑制し、全文だ/である体を強制する**。CTA stage = none。状態申告:「institutional segment: 単一レジスタ だ/である ✓ / 読者呼びかけセクション抑制 ✓」。
> (b) trade-ideas/community allows casual/タメ口 in 【投稿例】section.

### resolve_segment 実装上の挙動

- 入力テキスト中の "機関投資家向け / プロ向け / institutional / 機関専用" メタデータを `institutional` にマップ。
- 明示的 `--segment institutional` が他 style と組み合わされた場合 (例: `--style campaign --segment institutional`)、segment は採用するが register 切替効果は trade-ideas のみ。campaign の場合は psychology=logos_only, CTA=none の効果のみ適用される。

### Verification ブロック追加項目（trade-ideas + institutional segment 時のみ）

- 「institutional segment: 単一レジスタ だ/である ✓」
- 「読者呼びかけセクション: 不在 ✓」(です/ます セクションが残存していれば違反)
- 「CTA stage: none ✓」(action verb CTA 検出時は flag)

## Alternatives Considered

### 候補 (a): 新 T1 style `institutional-research`
- **却下**: アーキテクチャ侵襲が大きい。5 T1 styles という設計は SKILL.md の Style Routing 表・case-library 構造・全 RL の T1 分支判定に組み込まれており、6 番目を追加するとほぼ全ての横断 table に 1 列追加が必要。`--segment` 拡張は Step 3.6 の追加 1 行で完了する。
- 仮に新 T1 が必要となるほど制約セットが trade-ideas と乖離する場合は、v7 で再考。現時点では trade-ideas の制約セット (TI-1〜TI-9) はそのまま流用可能で、変化点は register と CTA のみ。

### 候補 (c): `--style report` の復活
- **却下**: ADR-002 が news/report を merge し、`report` 名称を廃止した経緯は字数帯と文体規範の重複から。これを撤回すると ADR-002 の根拠も失効するため、設計の整合性が崩れる。
- `institutional segment` は文体規範 (register/CTA) のみを切替えるためのフラグで、scene 仕様 (theme/morning/picks/earnings の構造) は trade-ideas 既存定義をそのまま継承できる。

### 候補 (d): 既存 trade-ideas に「institutional モード」を SKILL.md ハードコード
- **却下**: segment 機構を介さない直接 flag (例: `--institutional`) は、既存の 2 パラメータ routing (`--style` + `--scene`) との整合性を欠く。segment は v6.0.0 で導入済みの第 3 の任意パラメータで、psychology や CTA stage の override に既に使われている — 同じレールに乗せるのが自然。

## Consequences

### Positive

1. **機関投資家配信フローへの直接適合**: 野村・大和・SBI 機関向けレポート (Source 5)、QUICK Money World プロ版 (Source 11) の文体規範と一致。skill 出力をそのままプロ向け配信に流せる。
2. **既存 dual-register 設計を破壊しない**: ADR-003 のリテール向け dual-register は既定動作として維持。institutional segment 指定時のみ抑制される opt-in 拡張。
3. **CFA V(B) 整合**: 機関向けでは「読者を持ち上げる行動橋渡し」より「事実と見解の峻別 + attribution」が優先される。CTA stage = none は CFA V(B) Communication with Clients の prescription と整合。
4. **TI-7 免責との互換**: institutional segment でも TI-7 (≥501字 で disclaimer) は変わらず適用。機関向けでは免責文言自体が JSDA 雛形に加え CFA-style "for institutional use only" を含む長尺版が業界標準。
5. **後方互換**: `--segment institutional` を指定しなければ v6.0.0 と同一動作。既存テスト・既存出力への影響ゼロ。

### Negative

1. **Segment table の認知負荷増 (6→7 行)**: SKILL.md の Segment 表が 1 行増える。Funnel Stage 列の "research" は他 6 segment が表現するファネル位置 (re-engagement/activation/expansion/cross-sell/reactivation) と性質が異なるため、表内で他と並列に置かれることへの違和感がある。→ 緩和策: Segment 表の冒頭または末尾に institutional を配置し、コメントで「読者層 segment であってファネル segment ではない」と注記。
2. **Register override の semantic を `--segment` に持たせる是非**: 本来 segment は **読者の心理状態** を表すパラメータで、register override は文体規範の話。意味論が混在する。→ 緩和策: ADR-008 で「institutional は他 6 segment と性質が異なる読者層 segment である」ことを明記し、将来 segment が増える場合は **読者層** と **ファネル** を 2 列に分割する余地を残す (v7 候補)。
3. **trade-ideas 以外 style での institutional 指定の挙動**: campaign で `--segment institutional` を指定しても register 切替は発生しない (campaign は ADR-005 で全 6 シーン です/ます 単一を確定)。psychology=logos_only と CTA=none のみ適用される。これは「campaign を機関向けに転用する」用途を支える妥当な挙動だが、ユーザーが register 切替を期待した場合の sub-surprise リスクがある。→ 緩和策: SKILL.md README に "institutional segment は trade-ideas のみで register override 効果を持つ" と 1 行明記。

### Scene-by-Scene Impact (trade-ideas + institutional)

| Scene | 既定 (segment 無し) | + institutional | 主な差分 |
|---|---|---|---|
| `flash` | 分析=だ/である / 行動=です/ます | だ/である単一 | 行動橋渡し節を削除または短い fact-only 文に置換 |
| `theme` | 分析=だ/である / 読者呼びかけ=です/ます (末尾) | だ/である単一 | 末尾の「ぜひご検討ください」等を「投資判断の参考とされたい」へ転換 |
| `morning` | 分析=だ/である / 読者向け=です/ます | だ/である単一 | 「本日のチェックポイント」等の見出しは保持、本文は単一 |
| `earnings` | 分析=だ/である / 読者向け=です/ます (任意) | だ/である単一 | 数値 + attribution + 簡潔評価のみ |
| `picks` | カード見出し体言止め + です/ます 解説 | だ/である単一 | 各銘柄解説をだ/である化、CTA 削除 |
| `community` | 投稿例カジュアル + です/ます 地の文 | だ/である単一（投稿例除外） | 投稿例の casual/タメ口 例外は維持 (RL-11 (b)) |

community の RL-11 (b) 例外は本 ADR で **保持**。投稿例は読者参加を促すモジュールで、機関向け配信でも「他読者の声」として引用される文脈が成立するため、例外を抑制する根拠がない。

### テスト・互換性

- 新規追加: `build/tests/trade-ideas-institutional-*.snapshot.md` を 6 scene × 2 (リテール / institutional) で各 1 件、計 12 件のサンプル想定。最小実装は 6 件 (institutional 全 scene)。
- 既存 trade-ideas snapshot は影響なし。
- AC への追加: 本 ADR 採用時に AC-17「`--segment institutional` 指定時、trade-ideas 出力は です/ます 0 件 + CTA 不在 + verification ブロックに institutional segment 確認行」を追加可能 (Phase 3 で AC 追加判断、Phase 1.8 synthesis では未含)。

## References

### Internal
- `diagnosis/domain-research-trade-ideas.md` — Source 5 (野村・大和 機関向けレポート)、Source 9 (CFA V(B)/VI(A))、Source 11 (QUICK Money World プロ版)、Open Question OQ-TI-2
- `docs/adr/ADR-003-trade-ideas-dual-register.md` — 本 ADR の前提となる dual-register 例外
- `docs/adr/ADR-002-news-report-split.md` — `--style report` 廃止経緯（候補 (c) 却下根拠）
- `references/trade-ideas-guide.md` — Phase 3 で TI-2.ext を追加する対象
- `diagnosis/synthesis.md` Phase 2 — Fix A7 §新 ADR 起草

### External
- **CFA Institute "Standards of Practice Handbook" 11th ed. — Standard V(B), VI(A)** https://www.cfainstitute.org/en/ethics-standards/codes/standards-of-practice-handbook — 機関向けコミュニケーションでの事実/見解峻別、attribution-first 規範
- **野村證券・大和証券 機関投資家向けリサーチレポート公開ライブラリ** — register 規範の業界実例
- **QUICK Money World 法人向けプロ画面** — institutional 配信の文体実例

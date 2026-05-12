---
name: trade-ideas-guide
skill: jp-style-optimizer
tier1: trade-ideas
description: trade-ideas T1+T2 constraints — load when --style trade-ideas
---

# Trade-Ideas Guide（赚效内容类）

## T1 Shared Constraints

**Register**: デュアルレジスタ制（RL-11例外）— 分析パート: だ/である体; 読者アクションパート: です/ます体。同一段落内の混在禁止。
**Dominant proof**: Logos（データ・分析根拠）+ 行動橋渡し（TI-5必須）。
**CTA**: 間接的行動示唆必須（「〜をチェック」「〜に注目です」）。投資助言的CTA禁止（「今すぐ買おう」）。

| Constraint | Rule | Verification |
|-----------|------|-------------|
| TI-1 投資助言非該当 | 「おすすめ」「買い/売り推奨」「必ず上がる」禁止。情報提供フレームを維持 | TI-1 scan |
| TI-2 推測表現義務化 | forward-looking記述に推測表現必須。confidence gradient: 見込み > と見られる > 可能性がある | TI-2 check |
| TI-3 データ出典 | 具体的数値（株価・騰落率・EPS等)に出典付記。広く報道済みのデータは免除 | TI-3 scan |
| TI-4 市場タイミング | 日付/時点明示（「本日時点」「X月X日終値ベース」） | TI-4 check |
| TI-5 行動橋渡し必須 | 分析パート後に必ず次のステップ示唆。direct CTA or 間接示唆 | 「行動示唆あり: ✓」 |
| TI-6 リスク両面提示 | ポジティブ訴求時にリスク要因/下落シナリオも必須記載 | TI-6 check |
| TI-7 免責文言 | 500字超コンテンツに末尾免責文言必須（scene 別適用は下記表） | 「免責文言: ✓」 |
| TI-8 主観排除 | 「面白い」「ヤバい」等の主観的評価禁止。「注目されている」等の客観的注目度表現は許容 | TI-8 scan |

**Dual-register verification**: state「分析セクション: だ/である ✓ / 読者セクション: です/ます ✓」in Step 5.

### Tier 1 Extensions (v6.1.0)

| Constraint | Rule | Verification |
|-----------|------|-------------|
| TI-2.ext 事実/見通し構造分離 | theme/morning で「事実」と「見通し」を別段落 or 明示見出し（例: 「### 見通し」）で物理分離。同一段落内に実績数値と推測語尾の混在禁止 | 段落境界 + 推測語尾分布検査、状態申告「事実/見通し分離: ✓」 |
| TI-4.ext 時間軸特定語彙 | 「短期/中期/長期」等の曖昧表現を「数日内/数週内/数か月内」「前場終値で」「時間外取引で」等 specific 語に置換 | 曖昧時間表現 deny + 具体時間枠 allow scan |
| TI-6.ext 逆接構文必須 | リスク両面提示の機械検証として「ただし/一方で/反面/半面/その一方」の逆接構文を ≥1/risk-balance 段落で要求 | 逆接マーカー + リスク語彙の共起チェック |
| TI-8.ext 過熱表現 deny-list | 「爆騰/爆上げ/暴落/急騰/急落/神銘柄/爆益」を deny。客観的数値表現「上昇率○%/下落率○%」に rewrite | enumerated deny-list scan |
| TI-9 受け身 allow-list（ADR-010） | 分析セクション(だ/である体) に限り、RL-10 受け身連続スキャンから 6 語彙「とみられる/と発表された/と報じられた/と見込まれる/と指摘される/と位置付けられる」を除外。読者呼びかけセクションには allow-list 不適用 | 状態申告「受け身連続なし: ✓ (allow-list 適用)」 |

### TI-7 Scene-by-Scene Impact (ADR-006 §Scene-by-Scene Impact 転記)

| Scene | 字数レンジ | TI-7 適用 | 理由 |
|---|---|---|---|
| **flash** | ≤140 | 免除 | プラットフォーム Push footer が担保 |
| **picks** | 80–200/銘柄 | 免除 | アプリ内カード UI、共通 footer が担保 |
| **earnings** | 200–500 | 免除（境界 500 で要付加） | 速報性優先、境界超過時は安全側に倒す |
| **morning** | 300–800 | 字数依存（≥501 で必須） | 短尺版は免除、長尺版は必須 |
| **theme** | 500–1500 | **常に必須** | レンジ下限が閾値と一致、事実上全件 |
| **community** | 400–800 | 字数依存（≥501 で必須） | 短尺版は免除、長尺版は必須 |

短尺コンテンツ（flash/picks/earnings/morning短尺/community短尺）は配信プラットフォーム共通 footer / 規約ページ側で包括免責が担保される前提（skill scope 外、人間レビュー確認）。

### Institutional Segment Override (ADR-008)

`--segment institutional` 指定時は本ガイド既定の dual-register 例外を抑制し、trade-ideas 全文だ/である単一レジスタを強制する。CTA stage = none（行動橋渡し節を削除または fact-only に置換、「ぜひご検討ください」等は「投資判断の参考とされたい」へ転換）。verification ブロックに「institutional segment: 単一レジスタ だ/である ✓ / 読者呼びかけセクション: 不在 ✓ / CTA stage: none ✓」を追加。TI-7 免責は通常通り適用、community の【投稿例】RL-11(b) 例外も保持。TI-9 allow-list は institutional モードでは全文に適用（register 性質が分析セクションに最も近いため）。

## T2 Scene Specifications

### flash（市場速報・フラッシュ）
**字数**: ≤140字（Push/SNS同時生成用）
**情報構造**: 事実（数値付き）→ 影響 → 見通し（≤1文）
**Register**: だ/である体主体; 末尾1文のみ間接示唆（です/ます許容）
**Checkpoint**: 数値明記 ✓ / 影響1文 ✓ / 140字以内 ✓

### theme（テーマ分析・投資アイデア）
**字数**: 500–1500字
**情報構造**: テーマ背景 → 市場データ → 関連銘柄/商品 → 投資視点 → 免責
**Register**: 分析=だ/である; 投資視点=です/ます（デュアルレジスタ）
**必須**: 末尾免責文言（TI-7）; リスク両面（TI-6 + TI-6.ext 逆接構文）; 推測表現全forward-looking文; 事実/見通し構造分離（TI-2.ext）
**Checkpoint**: 分析/読者セクション分離 ✓ / 両面提示 ✓ / 免責あり ✓

### earnings（決算ハイライト）
**字数**: 200–500字
**情報構造**: 決算概要（実績vs予想）→ ポイント分析 → 株価反応 → 見通し
**必須**: 実績と予想の両方を数値で記載; 見通しに推測表現
**Checkpoint**: 実績vs予想明記 ✓ / 株価反応言及 ✓ / 見通し推測体 ✓

### morning（朝のブリーフ・デイリー）
**字数**: 300–800字
**情報構造**: 前日振り返り（主要指標）→ 本日注目材料 → 注目銘柄/セクター
**Register**: 前日振り返り=だ/である; 注目ポイント以降=です/ます（デュアル）
**必須**: 末尾免責（TI-7、≥501字時）; 日付/時点明示（TI-4）; 事実/見通し構造分離（TI-2.ext）
**Checkpoint**: 前日指標3件以上 ✓ / 本日注目明示 ✓
**棲み分け**: テキスト朝刊ブリーフに限定。動画ナレーション/音声スクリプトは product/script に再ルーティング。

### picks（注目銘柄カード）
**字数**: 80–200字/銘柄
**情報構造**: 銘柄名 → 注目理由（1–2文）→ 基本指標 → 関連テーマタグ
**Register**: です/ます体（読者向け短尺コンテンツ）
**必須**: TI-1（推奨表現禁止）; 注目理由は客観的根拠を含む
**TI-3.picks**: 各銘柄カードに数値指標 ≥2 件必須（株価+前日比変化率 / PER / PBR / 配当利回り / 時価総額 から 2 つ以上）。指標ゼロ or 1 件のみは soft-fail 警告
**Checkpoint**: 銘柄名明記 ✓ / 推奨表現不在 ✓ / 数値指標 ≥2 ✓

### community（コミュニティ投資話題）
**字数**: 400–800字 + 参加モジュール
**情報構造**: タイトル → 事実/現状 → 投資視点 → 読者参加（投票/コメント促進）
**Register**: です/ます体（エンゲージメント重視）
**TI-CMTY**: 投稿例セクションは `【投稿例】` 見出し marker で明示的に区切る。marker 内のカジュアル体/タメ口/口語受け身は RL-11(b) 例外として verification 除外（RL-3 主観排除・RL-10 受け身連続・TI-8.ext 過熱表現スキャンも適用外）。marker 不在時は地の文として標準スキャンを適用
**Checkpoint**: 読者参加要素あり ✓ / CTA（「どう思いますか？」等）✓ / 投稿例 marker 適用 ✓

## Distribution Channels（配信チャネル軸）

trade-ideas は **scene（内容類型）× channel（配信チャネル/版位）** の 2 層直交ルーティング。`--style trade-ideas --scene flash --channel push` のような組み合わせ指定が予期される用法。channel は scene と独立して字数硬制約 + 形態（テキスト/画像併用）を規定する。

| # | Channel | 子分類 | 形態 | 字数硬制約 | 推奨 scene |
|---|---|---|---|---|---|
| 1 | `push` | / | 純テキスト | タイトル ≤20字 / 本文 ≤60–80字 | flash / picks |
| 2 | `search-watermark` | / | 純テキスト | ≤30字 | flash |
| 3 | `bubble` | / | 純テキスト | ≤25字（CTA ≤8字） | picks / flash 引流 |
| 4 | `market-alert` | / | 純テキスト | ≤120字（事象トリガー型） | flash |
| 5 | `in-app-ad` | 闪屏 / 一級 popup / 個股詳情 banner / 取引 tab banner / 資訊 tab 要聞 banner / 我的 tab banner / 活動中心 / 悬浮球 / 宝箱任務詳情 banner | 図+文 | 主見出し ≤15字 / 副 ≤25字 / CTA ≤8字 | picks / flash 引流 |
| 6 | `product-popup` | 活動視図 | 図主体 | 補足文 ≤40字 | picks |
| 7 | `edm` | / | 文+図 | 件名 ≤30字 / 本文 300–800字 | morning / theme |
| 8 | `lp-h5` | / | 文+図 | 200–1500字（scene 依存） | theme / morning |
| 9 | `lp-web` | / | 文+図 | 500–2000字（scene 依存） | theme |

**Channel × Scene mapping（指針）**:
- `push` / `market-alert` → 短尺・即時性 → flash, picks（事象トリガー型は flash 優先）
- `search-watermark` / `bubble` / `in-app-ad` / `product-popup` → 引流系・極短文 → picks カード短縮版 or flash 1 文要約
- `edm` / `lp-h5` / `lp-web` → 長尺分析 → theme（lp-web 優先）/ morning（edm 優先）
- TI-7 免責は **scene の字数レンジで判定**（channel 依存ではない）。例: `--scene theme --channel lp-h5` は theme 長尺なので常に免責必須。

**Future scope**: channel taxonomy の正式 ADR-011 起草を v6.2+ で予定（現 v6.1.0 では scene と直交する文書記述に留め、SKILL.md routing への正規パラメータ昇格は保留）。

## Routing Inference Keywords

```
trade-ideas: 「投資アイデア」「銘柄分析」「テーマ株」「取引チャンス」「注目銘柄」
「市場動向+行動示唆」「ホットトピック+CTA」
flash: 「市況速報」「速報」「急騰」「急落」「サプライズ」≤140字
theme: 「テーマ分析」「投資テーマ」「AI株」「高配当」「インバウンド」
earnings: 「決算」「EPS」「売上」「上方修正」「下方修正」「サプライズ」
morning: 「朝の」「デイリー」「本日の注目」「前日振り返り」
picks: 「注目銘柄」「銘柄カード」「ピックス」
community: 「コミュニティ」「みんなはどう思う」「話題」「投票」
channel: 「Push通知」「EDM」「H5」「LP」「弹窗」「banner」「気泡」「行情通知」「闪屏」「站内广告」
```

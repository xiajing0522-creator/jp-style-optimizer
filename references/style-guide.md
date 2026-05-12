# Style Guide: Routing Reference

Two-tier routing: `--style` (Tier 1 register) + `--scene` (Tier 2 structural template). T1 constraints are additive with T2. Load the corresponding `references/{style}-guide.md` for per-style and per-scene details.

---

## Tier 1 Overview

| `--style` | 文案風格類 | Dominant Proof | Register |
|-----------|----------|----------------|---------|
| `campaign` | 营销活动类 | Pathos (deadline, incentive) | です/ます; CTA必須(Hot/Warm/Cold段階別) |
| `trade-ideas` | 赚效内容类 | Logos + action bridge | デュアルレジスタ (分析:だ/である + 読者:です/ます) |
| `news` | 新聞事件类 | Logos (fact-only) | だ/である; CTA禁止; 分析≤30% |
| `product` | 产品运营类 | Logos (Feature→Benefit) | です/ます; CTA任意(低コミットメントのみ) |
| `compliance` | 合規服務类 | Ethos (institutional trust) | scene別 (下表参照); 宣伝性ゼロ |

---

## Routing Inference Table

Infer `--style` + `--scene` when flags are omitted.

### campaign（营销活动类）
| Keyword Pattern | → Route |
|----------------|---------|
| 「期間限定」「特典」「〇〇月〇〇日まで」「もれなく」「抽選」「先着」 | campaign |
| 「新規告知」「キャンペーン開始」「スタート」 | campaign/launch |
| 「残りX日」「まだ間に合う」「リマインド」 | campaign/remind |
| 「最終日」「本日限り」「ラストチャンス」「今日で終了」 | campaign/lastday |
| 「達成」「結果報告」「おめでとう」「特典付与」 | campaign/result |
| 「年末年始」「新NISA」「季節キャンペーン」+ 特典 | campaign/seasonal |
| 「友達紹介」「紹介特典」「招待」 | campaign/referral |

### trade-ideas（赚效内容类）
| Keyword Pattern | → Route |
|----------------|---------|
| 「投資アイデア」「銘柄分析+行動示唆」「取引チャンス」「注目銘柄+CTA」 | trade-ideas |
| 「速報」「急騰」「急落」+ 行動示唆 ≤140字 | trade-ideas/flash |
| 「テーマ分析」「AI株」「高配当」「インバウンド」500字以上 | trade-ideas/theme |
| 「決算ハイライト」「EPS」「上方修正」+ 見通し | trade-ideas/earnings |
| 「朝の市場」「デイリー」「前日振り返り+本日注目」 | trade-ideas/morning |
| 「注目銘柄カード」「銘柄ピックス」80–200字/銘柄 | trade-ideas/picks |
| 「コミュニティ」「投票」「みんなの意見」+ 市場テーマ | trade-ideas/community |

### news（新聞事件类）
| Keyword Pattern | → Route |
|----------------|---------|
| 「速報」「ニュース」「客観的に」「分析なし」「事実のみ」 | news |
| 「速報」「〇〇が急落/急騰」≤140字 CTA不要 | news/flash |
| 「本日のまとめ」「振り返り」「ラップアップ」 | news/wrap |
| 「決算速報」「決算結果」CTA不要 | news/earnings |
| 「経済指標」「雇用統計」「CPI」「GDP」 | news/indicator |
| 「複数ニュース」「ダイジェスト」500字以上 | news/digest |
| 「〇〇円突破」「閾値」「アラート」≤100字 | news/alert |

### product（产品运营类）
| Keyword Pattern | → Route |
|----------------|---------|
| 「商品説明」「機能説明」「使い方」「ツール紹介」「プロダクト」 | product |
| 「1行で」「短く」「卖点」「USP」30–80字 | product/short |
| 「詳細説明」「機能詳細」「商品説明ページ」 | product/detail |
| 「手順」「操作方法」「マニュアル」「ガイド」 | product/manual |
| 「動画スクリプト」「ナレーション」「音声」 | product/script |
| 「リリースノート」「更新情報」「バージョン」「アップデート」 | product/release |
| 「オンボーディング」「はじめ方」「初回設定」「入門」 | product/onboard |
| 「比較」「他社比較」「差別化」「違い」 | product/compare |

### compliance（合規服務类）
| Keyword Pattern | → Route |
|----------------|---------|
| 「利用規約」「免責」「FAQ」「手続き案内」「ヘルプ」「合規」 | compliance |
| 「目論見書」「開示文書」「正式体」「だ/である体の法律文書」 | compliance/disclosure |
| 「利用規約」「取引約款」「規約体」 | compliance/terms |
| 「免責事項」「免責声明」「リスク説明」 | compliance/disclaimer |
| 「FAQ」「よくある質問」「Q&A」「問答形式」 | compliance/faq |
| 「手続き案内」「操作ガイド」「客服体」「サポートページ文案」 | compliance/guide |

---

## Default Scenes (when `--scene` omitted)

| `--style` | Default `--scene` |
|-----------|------------------|
| campaign | `launch` |
| trade-ideas | `theme` |
| news | `flash` |
| product | `detail` |
| compliance | `disclaimer` |

---

## Brand-Specific Routing Overlay

When the input or brief contains a brand name, also load the brand's voice entry from `case-library.md` (Step 3.5). For brands with extracted channel-routing references (per ADR-011), load the companion file alongside the case-library entry:

| Brand trigger | Companion file | Loads when |
|---|---|---|
| `moomoo` / `moomoo証券` | `references/moomoo-jp-routing.md` | input or brief mentions moomoo |

Brand-routing overlays apply per-channel RL-4 limits and brand-specific terminology rules on top of the generic T1+T2 routing inferred above.

---

## Backward Compatibility

Old `--style` calls route to new T1+T2:

| Old call | New route | Disambiguation |
|----------|----------|----------------|
| `--style marketing` | `campaign/launch` | Period-limited incentive content |
| `--style marketing --scene event` | `campaign/launch` | |
| `--style marketing --scene lp` | `product/detail` or `campaign/launch` | If features only → product; if incentive → campaign |
| `--style marketing --scene sns` | `campaign/launch` (SNS channel) | |
| `--style marketing --scene push` | `campaign/launch` (Push channel) | |
| `--style marketing --scene edm` | `campaign/launch` (EDM channel) | |
| `--style marketing --scene banner` | `campaign/launch` (Banner channel) | |
| `--style report` | `news/flash` (if ≤140字, no CTA) or `trade-ideas/theme` (if CTA/action present) | |
| `--style report --scene hottopic` | `news/flash` | |
| `--style report --scene topic` | `trade-ideas/community` | |
| `--style report --scene press` | `news/wrap` | |
| `--style report --scene deck` | `product/detail` (bullet形式) | |
| `--style report --scene report` | `trade-ideas/morning` or `news/wrap` | |
| `--style legal` | `compliance` (legal sub-register) | |
| `--style legal --scene disclosure` | `compliance/disclosure` | |
| `--style legal --scene terms` | `compliance/terms` | |
| `--style legal --scene disclaimer` | `compliance/disclaimer` | |
| `--style support` | `compliance` (support sub-register) | |
| `--style support --scene faq` | `compliance/faq` | |
| `--style support --scene guide` | `compliance/guide` | |
| `--style product` (unchanged) | `product/{scene}` | All product scenes map directly |
| `formal` (legacy) | `compliance/disclosure` | |
| `sns` (legacy) | `campaign/launch` (SNS channel) | |
| `press` (legacy) | `news/wrap` | |
| `deck` (legacy) | `product/detail` | |

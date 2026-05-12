---
name: compliance-guide
skill: jp-style-optimizer
tier1: compliance
description: compliance T1+T2 constraints — load when --style compliance
---

# Compliance Guide（合規服務类）

## T1 Shared Constraints

**Sub-register A (legal)**: disclosure/terms/disclaimer — 法的正確性優先。宣伝性ゼロ。
**Sub-register B (support)**: faq/guide — 対人信頼優先。謙譲語II全面使用。
**Dominant proof**: Ethos（制度的権威 or 対人的信頼）。Pathosゼロ。

| Constraint | Rule | Verification |
|-----------|------|-------------|
| C-1 宣伝性ゼロ | 「！」「お得」「今すぐ」「便利」(as selling point)「簡単」(as selling point) 全面禁止 | C-1 scan |
| C-2 術語完全保持 | legal: 略語ゼロ（「東京証券取引所」not「東証」）。定義済み術語の言い換え禁止 | C-2 check |
| C-3 レジスタ一貫 | 各シーンのレジスタ指定を厳守（下表参照） | 「レジスタ: [scene]準拠 ✓」 |
| C-4 リスク責任言語 | 法律文書: リスク警告必須（「損失が生じるおそれがあります」）+ 免責構文必須 | C-4 check |
| C-5 正確性保証構文 | 免責前に努力表明必須（「万全を期しておりますが」「正確を期すよう努めておりますが」） | C-5 check (disclaimer/faq) |
| C-6 法的フレーミング | legal: 「ご自身の判断と責任において」。support: 「〜いただけます」「〜お願いいたします」。「〜しましょう」禁止 | C-6 check |
| C-7 構造完全性 | 各シーン必須構造要素の欠落禁止（下表参照） | 「構造完全: ✓」 |

**Scene-specific register matrix:**

| Scene | 語尾 | 敬語 | 禁止 |
|-------|------|------|------|
| disclosure | だ/である | ゼロ敬語 | です/ます, お/ご接頭辞 |
| terms | です/ます | 丁寧語 | だ/である, 謙譲語II |
| disclaimer | です/ます + 謙譲語II(限定) | 謙譲語II OK | だ/である, 「！」 |
| faq | です/ます + 謙譲語II | 謙譲語II全面 | だ/である, 裸命令形 |
| guide | です/ます + 謙譲語II | 謙譲語II全面 | だ/である, 裸命令形 |

## T2 Scene Specifications

### disclosure（開示文書・目論見書）
**字数**: 30–50字/文
**情報構造**: 命題 → 根拠 → 条件/義務
**Register**: だ/である体 exclusively（RL-5相当: 「です/ますなし: 確認済み」）
**必須**: 術語略語ゼロ（C-2）; リスク警告（C-4）
**Checkpoint**: 「です/ますなし: 確認済み」✓ / 略語不在 ✓ / リスク警告あり ✓

### terms（利用規約・取引約款）
**字数**: 40–60字/文
**情報構造**: 対象範囲 → 義務 → 条件 → 例外
**Register**: です/ます体。義務構文「〜するものとします」必須
**Checkpoint**: 義務構文あり ✓ / 条件/例外明記 ✓

### disclaimer（免責事項）
**字数**: 40–60字/文
**情報構造**: 対象範囲 → 義務 → 条件 → 免責 → リスク警告
**必須**: precaution hedge（C-5）→ 免責本体の順
**Checkpoint**: precaution hedge先行 ✓ / 免責+リスク警告あり ✓

### faq（FAQ・よくある質問）
**字数**: 20–35字/文
**情報構造**: Q → A → 手順/チャネル
**Register**: です/ます + 謙譲語II全面（承ります/ございます/いただけます）
**必須**: 投資判断関連QへはC-6責任移転文付加
**Checkpoint**: 謙譲語II全面 ✓ / 手順またはチャネル案内 ✓

### guide（手続き案内・操作ガイド）
**字数**: 20–40字/文
**情報構造**: 手続き種別 → 手順 → チャネル → 代替案内
**Register**: です/ます + 謙譲語II全面
**必須**: 番号付き手順; チャネル（電話/メール/アプリ）を明示
**Checkpoint**: 番号付き手順 ✓ / チャネル明示 ✓ / 代替案内あり ✓

## Routing Inference Keywords

```
compliance: 「利用規約」「免責」「FAQ」「手続き案内」「ヘルプ」「合規」「法的」
disclosure: 「目論見書」「開示文書」「有価証券報告書」「だ/である体」「正式体」
terms: 「利用規約」「取引約款」「規約体」「〜するものとします」
disclaimer: 「免責事項」「免責声明」「リスク説明」「法律条款」
faq: 「FAQ」「よくある質問」「Q&A」「問答形式」
guide: 「手続き案内」「操作ガイド」「客服体」「サポートページ」
```

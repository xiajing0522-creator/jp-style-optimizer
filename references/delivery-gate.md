---
name: delivery-gate
type: reference
skill: jp-style-optimizer
version: 6.2.0
date: 2026-05-13
attractiveness_proxy: P2-A (per-style, soft-warn only)
load: at Step 7 entry (not in always-loaded Phase 1 bundle)
---

# Delivery Quality Gate — 交付質量門禁

## Purpose

Step 5/6 で実行した検証項目を **3 段階の severity** に分類し、「この出力を user に渡してよいか」を一意に決定する。本ファイルは **唯一の交付判定権威**。SKILL.md Step 7 から always 参照される。

評価(D1–D9 rubric)とは職責分離:
- **rubric**(`diagnosis/cross-style-quality-rubric.md`):事後品質スコアリング
- **gate**(本ファイル):交付前 go/no-go 判定

---

## 三段階 Severity Model

| Tier | 名称 | 違反時の挙動 |
|------|------|--------------|
| **P0** | Hard Block | revise loop(同一会話内 最大 3 周)。3 周で解決せず → `🛑 交付不可` ラベル付きで部分結果を返す。`✅` を絶対に付けない |
| **P1** | Conditional Block | 源稿が必要情報を含む場合 → 修正必須。源稿が情報欠落で修正不能 → 保持し、検証ブロックに `⚠` を立てて交付 |
| **P2** | Soft Warn | 検証ブロックに記録するのみ。交付ブロックなし |

---

## P0 — Universal(5 styles 全適用)

| ID | 内容 | 派生元 |
|----|------|--------|
| U-1 | 術語ロック完全一致(全項) | RL-1 |
| U-2 | 情報注入ゼロ(数値/固有名詞/因果のいずれも源稿外なし) | RL-2 |
| U-3 | 二重否定ゼロ | RL-7 |
| U-4 | 名詞 4 個以上連続なし | RL-8 |
| U-5 | 同一文内 受け身 2 個以上連続なし(news/trade-ideas analysis は PASSIVE_ALLOW_LIST 例外) | RL-10 |
| U-6 | 文体混用なし(news 引用 carve-out / trade-ideas dual-register 例外) | RL-11 |
| U-7 | RL-4 場面ハード文字数:2 回圧縮を試みても超過 → P0 違反 | RL-4 |
| U-8 | D1 ≥ 3 かつ D2 ≥ 3 | rubric |

> **U-9 — 言語ゲート**(RL-6)は P0 より上の **pre-gate**。日本語以外 → 翻訳デリゲーションを返し、本 gate は実行しない。

---

## P0 — Style 専属

### campaign

| ID | 内容 | 派生元 |
|----|------|--------|
| CMP-1 | CTA に動作動詞あり、stage と segment に整合 | RL-12 |
| CMP-2 | 禁止語彙(必勝/絶対/確実/100%/間違いなし) = 0 | AC-16 |
| CMP-3 | 「保証」型断言なし(誇大表現) | C-1 流用 |

### trade-ideas

| ID | 内容 | 派生元 |
|----|------|--------|
| TI-A | 主観表現(分析セクションかつ引用外) = 0 | RL-3 |
| TI-B | theme / morning ≥ 500 字 → 免責文言あり | AC-10 |
| TI-C | dual-register 段落内不混在(分析=だ/である / 読者=です/ます) | TI-7 |

### news

| ID | 内容 | 派生元 |
|----|------|--------|
| NW-A | 主観表現(引用外) = 0 | RL-3 |
| NW-B | CTA = 0(action verb / 「こちら」誘導いずれも禁止) | AC-11 |
| NW-C | 分析比率 ≤ 30%(超過 → `🛑 交付不可`、trade-ideas へ re-route 提案) | NC-9 |
| NW-D | 「！」「今すぐ」 = 0 | AC-12 |

> 引用ペアリング不整合(AC-14)は **warning のみ**(ADR-007 §2.2)。P2 として処理。

### product

| ID | 内容 | 派生元 |
|----|------|--------|
| PR-A | 各 feature claim に F→B ペア存在 | PC-1 |
| PR-B | 誇張表現(「業界最速」「No.1」など無根拠) = 0 | PC-3 |

### compliance

| ID | 内容 | 派生元 |
|----|------|--------|
| CP-A | disclosure サブレジスタで「です/ます」 = 0 | RL-5 |
| CP-B | 「！」「今すぐ」 = 0 | AC-12 |
| CP-C | 宣伝性表現(お得 / ぜひ / 限定特典型) = 0 | C-1 |
| CP-D | CTA = 0 | C-1 流用 |
| CP-E | faq / guide サブレジスタで謙譲語 II 使用 | C-3 |

---

## P1 — Conditional(可修則修、源稿不可なら ⚠ 付き交付)

| ID | 内容 | 不可修条件(⚠ 交付) |
|----|------|---------------------|
| C-AC9 | campaign 期限明示 | 源稿に期限情報なし → ⚠「期限未明示(源缺)」 |
| C-CA3 | campaign 特典具体化 | 源稿に金額/期間/条件の数値なし → ⚠「特典抽象(源缺)」 |
| C-RL9 | news / trade-ideas 数値出典 | 源稿に出典記載なし → 各数値に `要出典: [数値]` を付して交付 |
| C-AC15 | trade-ideas/picks ≥ 2 数値指標 | 源稿に指標 1 件以下 → ⚠「指標不足(源缺)」 |

---

## P2 — Soft Warn(記録のみ、交付ブロック無し)

| ID | 内容 | 派生元 |
|----|------|--------|
| S-1 | 平均字/文 が場面 句長目標 から ±20% 超 | Step 5 soft check |
| S-2 | 文長分布 単調 | Step 6 Proxy 2 |
| S-3 | 跨レジスタ語彙渗透(campaign の formal leakage、news/trade-ideas の colloquial leakage 等) | Step 6 Proxy 1 |
| S-4 | ブランド声紋偏差(case-library 比較) | Step 6 Proxy 4 |
| S-5 | 場面 Checkpoint が満点未達かつ 60% 以上 | `{style}-guide.md` Checkpoint |
| S-6 | 引用ペアリング不整合(news) | AC-14 / ADR-007 |

---

## P2-A — Attractiveness Proxy(Per-Style 吸引力代理)

各 style に「吸引力」の意味が異なるため、5 styles 別個に定義。**配信決定には影響しない**(P2 と同じく soft warn)。`✓ / ✗` で記録、score = `✓ 件数 / 総件数` を Verification Block に表示。

> 主観性が含まれる指標なので hard gate にはしない。score 0/N でも `✅ 交付可` は出る。

### campaign — 転換吸引力

> 開頭 1〜2 文で読者に「クリック / 参加 / 続きを読みたい」と思わせる力。

| ID | 維度 | スキャン |
|----|------|---------|
| A-CMP1 | Benefit-First Urgency | 第1文(冒頭 ≤ 30 字)に「金額・特典 token」+「期限 token」が共存 |
| A-CMP2 | Lifecycle Consistency | キャンペーン名・期限表記が出力全体で同一形 |
| A-CMP3 | Concrete Density | 抽象形容詞(便利/お得/簡単)率 ≤ 20%、数値 ≥ 1 件 |
| A-CMP4 | Benefit-Deadline Co-Location | 「金額/特典 token」と「期限 token」が同一文または隣接 2 文以内に共起(離間配置 ✗) |
| A-CMP6 | Numeric Plurality | 数値 ≥ 2 件(金額 / 期間 / 残数 / 達成率 等)、汎用「お得」のみは ✗ |
| A-CMP7 | CTA Visibility | CTA 動作動詞句が冒頭 ≤ 50 字以内に出現、または視覚分離(太字 / ボタン化マークアップ / 独立行配置)あり |
| A-CMP8 | Single CTA Focus | 出力全体で CTA 動作動詞のユニーク数 ≤ 2 種(3 種以上で分散 ✗)。lifecycle 段階差(cold/warm/hot)による意図的差異は例外 |
| A-CMP9 | Hook Strength | 第1文に いずれか ≥ 1 件:curiosity gap(実は / 知ってますか / 3 つの理由)/ loss aversion(残り / 最後 / 今だけ / 逃すと)/ 数値 anchor(金額 / 残数 / 達成率の具体数値) |
| A-CMP10 | Friction Reduction | 行動コスト明示シグナル ≥ 1 件:「3 タップで」「1 分で」「登録不要」「○○のみ」等の動作回数 / 所要時間 / 前提省略表現。抽象「簡単」のみは ✗ |

### trade-ideas — 分析吸引力

> 分析を読み切らせ、次に何を見るべきか即座に分かる力。

| ID | 維度 | スキャン |
|----|------|---------|
| A-TI1 | Analytical Credibility Stack | 事実層→影響層→見通し層 が物理的(段落 / 箇条書き)に分離 |
| A-TI2 | Market Timing Specificity | 「前場終値」「14時35分」「時間外」等の具体時間枠語彙 ≥ 1 件(汎用「本日」のみは ✗) |
| A-TI3 | Risk Both-Sides Articulation | 見通し段に逆接マーカー(ただし/半面/その反面)+ リスク語彙 共起 |
| A-TI4 | Confidence Calibration | 推測語尾の階層化:強(と見込まれる)/ 中(と見られる)/ 弱(可能性がある)が同一文書内で混在し単一語尾連発でない |
| A-TI5 | Numeric Precision Gradient | 数値の精度が文脈に整合(速報=円単位、決算=億円/%、長期見通し=兆円/前年比%)。過剰精度・粗精度の混在 ✗ |
| A-TI6 | Causal Markers | 影響層の文に因果マーカー(背景に / を受けて / が要因 / の結果)≥ 1 件 |
| A-TI7 | Theme-Sector-Stock Chain | テーマ→セクター→個別銘柄 の連鎖が出力内に ≥ 1 本(銘柄列挙のみ ✗) |
| A-TI8 | Past-Case Recency | 過去事例引用がある場合、事例の時点が ≤ 24 ヶ月以内 or 明示的時点記載 |
| A-TI9 | Calendar Linkage | 直近イベント(FOMC / 日銀会合 / 雇用統計 / 決算発表日)への参照 ≥ 1 件 |
| A-TI10 | Consensus Contrast | 自説と「市場予想 / コンセンサス / アナリスト見方」の対比あり |
| A-TI11 | Ticker Explicitness | 銘柄識別子(日本株 4 桁コード / 米国株ティッカー)≥ 1 件(picks ≥ 2 / theme・morning ≥ 1)。銘柄名のみ + コードなし ✗ |
| A-TI12 | Entry/Exit Specificity | 価格目標 / エントリーゾーン / レジスタンス・サポート の数値 ≥ 1 件(picks / theme / morning)。「割安水準」のみは ✗ |
| A-TI13 | Risk Line Visibility | 損切ライン / 撤退条件 / 下値メド の数値または条件文 ≥ 1 件(picks / theme)。**Carve-out**:同一出力内 ticker ≥ 5 件 → 広範情報提供と判定し本項免除 |
| A-TI14 | Action-Bridge Verb Specificity | 行動橋渡し動詞 ≥ 1 件:高転化型(自選追加 / アラート設定 / 指値注文 / 成行で買う / ポジション構築)。「検討」「視野」「注目」のみは ✗ |
| A-TI15 | Decision Path Compactness | 「テーマ/事象 → 銘柄識別子 → 行動動詞」三要素が連続 ≤ 3 段落以内(picks / morning)、≤ 5 段落以内(theme) |

### news — 情報吸引力

> 見出し+第1文で読者の判断材料が揃う(scan-to-decision 効率)。

| ID | 維度 | スキャン |
|----|------|---------|
| A-NW1 | 5W Compression(第1文) | 第1文に 主体+行為+数値+時点 が共存 |
| A-NW2 | Scene-Specific Timeliness | flash/alert=分秒 / wrap=日付+本日 / earnings=会計期間 / indicator=対象月四半期 — scene 別粒度に整合 |
| A-NW3 | Headline 体言止め | 見出し末尾が名詞(発表/突破/再開 等)。動詞終止 ✗ |
| A-NW4 | Attribution Sophistication | 出典タグの scene + 情報源タイプ別使い分け:公式発表=「発表した」/ 独占報道=「報じた」/ 観測情報=「明らかになった」/ 観測筋=「との見方」 — 単一タグ連発 ✗ |
| A-NW7 | 5W+Unit Completeness | 第1文に 主体+行為+数値+単位(円/%/件/人)+時点 が共存 |
| A-NW8 | Modality-Free Headline | 見出しに推測語尾(可能性 / 見通し / 見込み)0 件、断定 / 体言止めのみ |
| A-NW9 | Factuality-Analysis Boundary | 事実段と分析段が物理的(段落分け / 接続詞「一方」「これに対し」)に分離 |

### product — 理解吸引力

> 4 目的のマルチターゲット:**理解**(看懂)/ **使用転化**(开始用)/ **継続**(retention)/ **クロスセル**(升级)。各維度がいずれかの目的に紐づく。

| ID | 維度 | スキャン |
|----|------|---------|
| A-PR1 | Jargon Onboarding | 初出専門用語の 100% に括弧説明 or 修飾句あり |
| A-PR2 | Scanability | 平均段落 ≤ 4 文、bullet/見出し で視覚分離あり |
| A-PR3 | Concrete Specificity | 抽象形容詞(簡単/便利/安心)率 ≤ 15%、具体場面名詞(出張中/通勤時 等)あり |
| A-PR4 | Action-Per-Step Minimalism | manual / script で 1 ステップ = 1 アクション、総ステップ ≤ 5 |
| A-PR5 | Use-Case Specificity | 利用場面(出張中 / 通勤時 / 朝の確認 / 週末リバランス 等)≥ 1 件明示 |
| A-PR6 | Outcome Quantification | ベネフィット記述に数値(時間短縮 / 件数 / コスト)≥ 1 件、抽象「便利」のみ ✗ |
| A-PR7 | Negative-Space Avoidance | 「〜できない」「〜不要」の連発 ✗(逆説型表現 ≤ 全文の 20%) |
| A-PR8 | Version/Compare-Axis Explicitness | release / compare scene 限定:バージョン番号 or 比較軸ラベルが明示 |
| A-PR9 | First-Action Anchor | 第 1 ステップが 具体動作動詞 + UI 要素名 で明示(例「右下のメニューをタップ」「設定 → アカウント」)。「アプリで簡単に」のみ ✗ |
| A-PR11 | Trial-Verb CTA | 試行型動詞(試す / 始める / やってみる / 無料で / お試し)≥ 1 件。初出に課金確定動詞(購入する / 申込む)のみは ✗(trial barrier 低減) |
| A-PR12 | Frequency Cue | 利用頻度語彙(毎日 / 週 X 回 / 月次 / 朝の / 寝る前の 等)≥ 1 件 |
| A-PR13 | Cumulative Value | 累積価値表現(「使うほど」「続けるほど」「履歴」「分析が深まる」「累計○○」)≥ 1 件 |
| A-PR15 | Upsell Path Visibility | 上位機能 / 上位プラン / 隣接サービスへの誘導 ≥ 1 件(「Premium」「Pro」「上級者向け機能」「もっと詳しく」) |
| A-PR17 | User-Tier Segmentation | 利用者層別表現(初心者 / 上級者 / プロ / 個人事業主 等)≥ 1 件、対象セグメント明示 |
| A-PR19 | Goal-Oriented Entry | 目的別見出し / 入口(「米国株を始める」「FIRE を目指す」「IPO 投資に挑戦」等)≥ 2 件。汎用「機能一覧」のみは ✗ |
| A-PR20 | Testimonial Density | 利用者の声 / レビュー引用ブロック ≥ 3 件(detail / onboard / compare scene)。1 件のみ・要約のみは ✗ |
| A-PR21 | Tenure Proof | 創業年 / 提供開始年 / 運営年数 等の歴史証明 ≥ 1 件(「2013 年創業」「サービス開始から 10 年」) |
| A-PR23 | Adoption Scale | 利用者規模数値(累計 N 人 / N 名突破 / DL N 万件 / 導入 N 社)≥ 1 件。「多くの方に」「人気の」のみは ✗ |
| A-PR24 | Empathic Identity Hook | 第 1 段に共感型 hook(「わたしでもできた」「初心者でも」「面倒な方へ」「忙しい人向け」)≥ 1 件 |
| A-PR25 | Authoring Credentialing | 監修者 / 著者の実名 + 資格(CFP / FP 技能士 / 証券アナリスト / 認定テクニカルアナリスト 等)+ 経歴 明示 ≥ 1 名(detail / manual / compare scene) |
| A-PR26 | Reading-Outcome Preview | 導入部に「この記事でわかること」型のサマリー bullet ≥ 3 項(detail / onboard scene)。本文の最初の 30% 以内に出現 |
| A-PR27 | Both-Sides Disclosure | メリット / デメリット(または「向いている人 / 向いていない人」)を別段落で並列構造で記述。片側のみは ✗ |
| A-PR28 | FAQ Coverage | 末尾に「よくある質問」段 ≥ 3 件(detail / manual / compare scene)。質問は具体的(「○○は△△ですか?」型)、汎用「お問い合わせ」誘導のみは ✗ |
| A-PR29 | Authoritative Reference | 公的機関(金融庁 / 日銀 / 各省庁)/ 大手メディア(Bloomberg / Reuters / 日経 等)への参照リンク or 出典記載 ≥ 1 件(detail / compare scene) |
| A-PR30 | Headline-Embedded Numerals | H1 / H2 見出しに数値(N 選 / N 社比較 / N% 還元 / 第 N 位 等)≥ 1 件(compare / detail scene) |

### compliance — 信頼吸引力

> 宣伝性ゼロ前提で「ここなら安心」感を喚起する力。

| ID | 維度 | スキャン |
|----|------|---------|
| A-CP1 | Risk Language Density | リスク語彙(損失/減少/欠損/不可/恐れ)率 ≥ 5%、boilerplate 200–400 字 |
| A-CP2 | Accuracy Guarantee Syntax | 「本開示は〇〇時点の情報に基づく」or 参照リンク 等の時点注記あり |
| A-CP3 | Precaution Hedge Placement | 努力表明(「万全を期しておりますが」「正確を期すよう努めておりますが」等)が 免責文 / リスク警告 の直前に配置 |
| A-CP4 | Support Channel Visibility | faq / guide サブレジスタ限定:サポート窓口(電話 / メール / アプリ / 店舗)≥ 1 件明示 |

---

## 交付決定アルゴリズム

```
1. 言語ゲート(RL-6 / U-9)
   非日本語 → デリゲーションメッセージを返し、STOP。

2. P0 全項目を実行
   全 ✓ → ステップ 3 へ
   1 件以上 ✗ → revise loop(最大 3 周)
     3 周で解決 → ステップ 3 へ
     未解決 → 検証ブロック末尾に
       「🛑 交付不可: P0 [項目ID 列挙]」
       現時点最良案を提示し ✅ ラベルは付けない、STOP。

3. P1 全項目を実行
   各項につき:
     源稿に必要情報あり and 違反 → 修正、再検査
     源稿不可 → 保持、検証ブロックに ⚠ を立てる

4. P2 全項目を実行
   違反項目を検証ブロックに記録、修正は任意

5. 標準化 Verification Block を出力(下節参照)

6. 末尾に Delivery Decision 1 行:
   ✅ 交付可     — P0 全 ✓ / P1 全 ✓ / P2 軽微
   ⚠ 注記交付   — P0 全 ✓ / P1 のうち N 件は源缺により ⚠ 保留
   🛑 交付不可  — P0 のうち N 件未解決
```

---

## 標準化 Verification Block

Step 5/6 の散点出力を本書式に統合。SKILL.md Output Format から参照。

```
=== Delivery Gate ===
[P0] Universal:
  U-1 術語ロック(N項) ✓ / U-2 情報注入なし ✓
  U-3 二重否定なし ✓ / U-4 名詞連続なし ✓ / U-5 受け身連続なし ✓
  U-6 文体統一 ✓ / U-7 RL-4 文字数 [field: X字 ✓ ...]
  U-8 D1=4 / D2=4
[P0] Style [<style>]:
  <style 専属 ID> [結果]
[P0] Scene [<scene>]:
  Checkpoint X/N ✓
[P1] 条件:
  なし  ←または ⚠ <ID>: <理由>
[P2] 注:
  平均X字/文 ✓ / 語彙漏れなし ✓ / 文長分布 自然
[P2-A] 吸引力:
  <A-XXX ✓/✗ ...> → N/M
Delivery Decision: ✅ 交付可
```

> **[P2-A] は配信決定に影響しない**(score 0/M でも ✅ 交付可は出る)。可視化のみが目的。

**規則**:
- すべての P0 行を出力(該当なくても `該当なし` と記載しない、項目を省略する)
- P1 が空なら `なし` と明記(空行禁止)
- Delivery Decision は **必ず最終行**(後ろに何も書かない)

---

## Backward Compatibility

旧 Step 5/6 の散点表現(「主観表現なし: ✓」「期限: [日付]確認: ✓」等)は本書式の **構成要素** として保持。既存呼び出し元(SKILL.md Step 5/6 を直読する評価系)が読み続けられるよう、措辞は変更しない。

新規追加要素:
- `[P0]/[P1]/[P2]` セクションラベル
- `Delivery Decision` 末行

---

## Examples

### Example A — campaign/launch、完全源稿

```
[P0] Universal:
  U-1 術語ロック(3項) ✓ / U-2 情報注入なし ✓
  U-3..U-6 ✓ / U-7 タイトル 18字 ✓ / 本文 55字 ✓
  U-8 D1=4 / D2=5
[P0] Style [campaign]:
  CMP-1 CTA(Cold「まずは詳しくみる」) ✓ / CMP-2 禁止語彙 0件 ✓ / CMP-3 ✓
[P0] Scene [launch]:
  Checkpoint 3/3 ✓
[P1] 条件: なし
[P2] 注: 平均22字/文 ✓ / 語彙漏れなし ✓ / 文長分布 自然
[P2-A] 吸引力: A-CMP1 ✓ / A-CMP2 ✓ / A-CMP3 ✗(抽象形容詞 25%) / A-CMP4 ✓ / A-CMP6 ✓ / A-CMP7 ✓ / A-CMP8 ✓ / A-CMP9 ✓ / A-CMP10 ✓ → 8/9
Delivery Decision: ✅ 交付可
```

### Example B — campaign、源稿に期限なし

```
[P1] 条件: ⚠ C-AC9: 源稿に期限情報なきため未記載
Delivery Decision: ⚠ 注記交付
```

### Example C — news/wrap、分析比率 60%

```
[P0] Style [news]:
  NW-C 分析比率 60% ✗ (≤30% 違反)
revise loop(3 周試行)→ 60→55→48% で 30% に到達せず。
Delivery Decision: 🛑 交付不可:NW-C(分析比率超過)。trade-ideas/theme への re-route を提案。
```

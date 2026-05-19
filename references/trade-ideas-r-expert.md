---
name: trade-ideas-r-expert
type: reference
skill: jp-style-optimizer
version: 0.2.0
date: 2026-05-14
status: partial-empirical — moomoo 3 篇抽样完了(R-2.ext / R-X.E / R-X.T 観察済)、R-1 / R-3 / R-4 短型部分は framework-only で v1.0.0 抽样待ち
source: |
  - moomoo news/community 3 篇抽样(2026-05-14 取得):
    1. NVIDIA Q4 earnings deep-dive(feedId 116134849085446、author Sherry、~6500-7500 字)→ R-X.E
    2. Anthropic ショック / 恩恵銘柄抽出(author Julie、~4500-5500 字)→ R-X.T
    3. NVIDIA 決算速報(postId 66020469、author Zeber、~1300-1500 字)→ R-2.ext
  - 既存 skill 内部知識(TI-1〜TI-9 / RL-3 / RL-9 / RL-10 / RL-11 / ADR-008 / ADR-010)
  - Type B(かぶリッジ 22 篇)との対比合成
load: at Step 4 entry when --style trade-ideas かつ Type R 判定時のみ lazy-load
purpose: |
  trade-ideas Type R(券商 research / morning brief / 短型市場速報 + brand-bound long-form deep-dive)
  sub-form 専用の構造・文体ベンチマーク。Type B(SEO 個別株深掘、かぶリッジ系)は別ファイル
  `trade-ideas-b-expert.md` に分離。
---

# Trade-Ideas **Type R** Expert Module — 券商 Research / Morning Brief / Brand-Bound Long-Form ベンチマーク

## Stance

Provides **frame templates** and **micro-pattern repertoire** for `--style trade-ideas` の **Type R** sub-form 群専用。

**v0.2.0 status**:moomoo 3 篇抽样により **R-2.ext(Earnings Flash 中型)** と **R-X(Brand-Bound Long-Form Deep-Dive)** を新設。R-1(Market Flash)/ R-3(Morning Brief)/ R-4(Picks Card)短型は依然 framework-only。引用例 5.6〜5.9 は moomoo 抽样からの verbatim、5.1〜5.5 は v1.0.0 で実 sample 置換予定。

### Type R 内部の sub-form 拡張(v0.2.0 で 4→6 に拡張)

| Sub-form | 代表媒体 | レジスタ | 字数 | 主導 scene | 抽样状況 |
|----------|---------|---------|-----|----------|---------|
| **R-1** Market Flash | みんかぶ・株探・各社 daily flash | dual-register | 80–140 | flash | framework-only |
| **R-2** Earnings Flash 短型 | 各社 morning report 短報 | dual-register | 150–400 | earnings | framework-only |
| **R-2.ext** Earnings Flash 中型 ※新設 | moomoo ニュース速報(Zeber 系) | **全文 だ/である**(末尾 CTA 1 文のみ「ください」) | **800–2000** | earnings | **moomoo 1 篇 verbatim** |
| **R-3** Morning Brief 短型 | 各社モーニングレポート | dual-register | 300–500 | morning(短) | framework-only |
| **R-4** Picks Card | アプリ内銘柄カード | です/ます一貫 | 80–200/銘柄 | picks | framework-only |
| **R-X.E** Brand-Bound Long-Form Earnings Deep-Dive ※新設 | moomoo community(Sherry 系) | **dual-register**(本体 だ/である + 末尾「ご確認ください」) | **4000–10000** | earnings 拡張 | **moomoo 1 篇 verbatim** |
| **R-X.T** Brand-Bound Long-Form Theme/Sector Deep-Dive ※新設 | moomoo news(Julie 系) | **全文 だ/である**(soft 誘導 CTA) | **3500–7000** | theme 拡張 | **moomoo 1 篇 verbatim** |

**含意**:
- R-1/R-2/R-3 短型適用時 → trade-ideas P0 の **TI-C(dual-register)厳格運用**
- **R-2.ext 適用時 → TI-C は緩和**(全文 だ/である、末尾 1 文のみ「ください」許容)
- **R-X.E 適用時 → TI-C 通常運用**(段落間 dual-register、末尾 brand-app CTA で「ください」)
- **R-X.T 適用時 → TI-C は institutional override 寄り**(全文 だ/である単一、CTA は soft 誘導「~に注目したい」「~であろう」型 = ADR-008 institutional モードに準じる)
- R-4 picks → 従来どおり「です/ます一貫」

### Type R 判定ヒント(Step 3 ルーティング時、v0.2.0 拡張)

以下のいずれかが該当 → Type R → 本ファイル lazy-load:

**短型ルート(R-1/R-2/R-3/R-4)**
- 字数 ≤ 500 字
- 媒体タイプ:券商 research note / morning brief / app push / market alert / EDM 短型
- 速報トーン:発表・公表 → 影響 → 見通し の 3 段スピード構成
- 機関投資家・トレーダー向け語彙(「前場終値」「コンセンサス対比」「サプライズ」)
- 単一段落内に「だ/である」分析 + 「です/ます」読者向けが共存(dual-register シグナル)

**中型ルート(R-2.ext)**
- 字数 800–2000、決算速報主体
- bullet 駆動 H3 sections(「決算サマリー」「事業別内訳」「見通し」「コメント」「規制」「関税」等)
- bullet 末尾に出典タグ(「(会社発表)」「(CFO 発言)」)強制付帯
- 表情アイコン不在
- ticker 4-6 銘柄(主体銘柄 + benchmark 比較)
- brand-app CTA(moomoo / SBI app push 等)

**長型ルート(R-X.E / R-X.T)**
- 字数 3500–10000、brand-bound community/news
- 表情アイコン分隔 H2(NVIDIA 篇 8 種多様 / Anthropic 篇 3 種固定)
- ticker 12+ 銘柄、Carve-out 適用域
- moomoo brand voice signature:自動翻訳注 / 「ーmoomoo ニュース [氏名]」型署名 / 出所「moomoo + 外部メディア + 企業 IR」
- R-X.E 識別: dual-register + Option strategies 含む可
- R-X.T 識別: 全文 だ/である + ETF 推奨段含む可 + 「~であろう」「~構造にあろう」末尾

該当しない(SEO 長型 ≥5,000 字、個人投資家向け口語、かぶリッジ系) → Type B → `trade-ideas-b-expert.md` を load。

---

## 1. Macro Framework — Type R の 7 sub-form と章節テンプレート

### 1.1 Type R-1 — Market Flash / 市場速報(80–140 chars / framework-only)

**該当 trade-ideas scene**:`flash`

**章節テンプレート**(必須順、≤140 字):

| 順 | 内容 | 役割 |
|----|------|------|
| 1 | 事象+数値+時点 | リード(20–40 字、体言止め or だ/である短文) |
| 2 | 影響(因果マーカー使用) | 1 文(20–40 字) |
| 3 | 見通し or 行動示唆 | 末尾 1 文(20–40 字、です/ます許容) |

**特徴**:体言止め多用 / 因果マーカー必須 / 末尾 1 文のみ「です/ます」許容。

(framework-only、引用例 5.1 参照、v1.0.0 で実 sample 置換予定)

### 1.2 Type R-2 — Earnings Flash 短型(150–400 chars / framework-only)

**該当 trade-ideas scene**:`earnings`(短型 / 1Q-flash 風)

**章節テンプレート**:銘柄+決算期+数値 → 主要数値 yoy → 株価反応 → 会社コメント → 投資家示唆。

**特徴**:前 3〜4 段は「だ/である」、末尾 1 文のみ「です/ます」。

(framework-only、引用例 5.2 参照、v1.0.0 で実 sample 置換予定)

### 1.3 **Type R-2.ext** — Earnings Flash 中型(800–2000 chars / moomoo 1 篇実測 ✓)

**該当 trade-ideas scene**:`earnings`(中型 / 速報網羅型)

**観察源**:moomoo postId 66020469「【エヌビディア決算速報】時間外一時上昇!4Q売上高$68.1B…」(author Zeber、2026-02-26 公開、~1300-1500 字、引用例 5.6)。

**章節テンプレート**(観察、必須順):

| 順 | 章節タイトル | 役割 |
|----|------|------|
| 1 | リード(2 文 = 主体 + 決算アクション + 株価反応) | ~40-80 字 |
| 2 | 株価ウィジェット(自動挿入) | ticker / 株価 / 騰落率 / ET 時点 |
| 3 | **ヘッドライン**(段落型サマリー、200-300 字) | 良材料 → 「一方」逆接 → 悪材料 |
| 4 | **決算サマリー(4Q)** bullet | 売上高 / EPS / セグメント主要数値 |
| 5 | **事業別内訳(4Q)** bullet | コンピュート / ネットワーキング / ゲーミング 等 |
| 6 | **見通し(1Q)** bullet | 会社ガイダンス vs 市場予想 |
| 7 | **コメント** bullet | CEO / 会社発言 |
| 8 | **特殊論点** bullet(規制 / 関税 / 在庫 等)| risk-side carve-out |
| 9 | **その他(提携観測等)** bullet | tail risk / catalysts |
| 10 | **市場の見方** bullet | アナリスト氏名 + direct quote |
| 11 | 末尾(自動翻訳注 + 出所 + 著者署名 + brand-app CTA)| moomoo 標準 footer |

**観察された差分(R-X.E earnings deep-dive との)**:

| 項目 | R-2.ext(本 sub-form) | R-X.E(deep-dive) |
|---|---|---|
| 字数 | 800-2000 | 4000-10000 |
| 表情アイコン | **不在** | 8 種(Cool/Cheer/Smart/Yeah/Respect/Toasted/Hey 等) |
| 構造 | bullet 駆動 H3 | 段落 + 表情アイコン H2 |
| 出典タグ密度 | bullet 単位(高) | 段落単位 |
| ticker 数 | 4-6(benchmark 比較) | 12+(ecosystem) |
| Option 戦略 | 不在 | あり |
| 編集スピード | 速報重視 | 深掘重視 |

**特徴**(moomoo 1 篇観察、N=1 ⚠ 命中率は v1.0.0 で N≥3 時に再評価):
- bullet 末尾に出典タグ「(会社発表)」反復(本 sample で 12 回)
- 「実績 vs 予想」並列形式「681 億ドル(市場予想:658 億ドル)」型
- ヘッドライン段で A-TI3 両面提示明示「を上回り、一方、~が材料となった」
- 末尾「ーmoomoo ニュース [氏名]」型署名
- brand-app CTA「moomoo アプリ内の『検索』>『決算発表』でご確認ください」(末尾 1 文のみ「です/ます」)

### 1.4 Type R-3 — Morning Brief 短型(300–500 chars / framework-only)

**該当 trade-ideas scene**:`morning`(短尺版、TI-7 免除レンジ)

**章節テンプレート**:前日米国 → 本日見通し → 本日注目 → 注目銘柄 → 行動橋渡し。

**特徴**:4-5 セクション見出し付(`【】` マーカー)、前 4 セクション「だ/である」、末尾「です/ます」、A-TI9 Calendar Linkage 必中。

(framework-only、引用例 5.3 参照、v1.0.0 で実 sample 置換予定)

### 1.5 Type R-4 — Picks Card(80–200 chars/銘柄 / framework-only)

**該当 trade-ideas scene**:`picks`

**Register**:本タイプは **「です/ます」一貫**(picks scene の T2 規定)。

**特徴**:TI-1 厳守 / 数値指標 ≥2 必須(AC-15)/ レジスタ単一。

(framework-only、引用例 5.4 参照、v1.0.0 で実 sample 置換予定)

### 1.6 **Type R-X.E** — Brand-Bound Long-Form Earnings Deep-Dive(4000–10000 chars / moomoo 1 篇実測 ✓)

**該当 trade-ideas scene**:`earnings`(拡張型 / 既定 200-500 字レンジ超過)

**観察源**:moomoo feedId 116134849085446「[NVIDIA 決算 Summary] 圧倒的な業績と『真の起爆剤』!…」(author Sherry、~6500-7500 字、引用例 5.7)。

**章節テンプレート**(観察):

| 順 | 章節 | アイコン | 役割 |
|----|------|---------|------|
| 1 | リード(業界文脈 → 主体 → 強気宣言) | なし | 200-400 字 |
| 2 | 主要財務データ | [Cool Guy] | 売上高 / 粗利 / EPS / 通期 |
| 3 | データセンター事業 | [Cheerlead] | yoy + 構成比 + 宇宙 DC 等 catalysts |
| 4 | ネットワーキング事業 | [Smart] | yoy + segment |
| 5 | 主力製品出荷 + Big Tech CapEx | [Yeah!] | 数量 + ecosystem 投資循環 |
| 6 | エコシステム拡大 | [Respect] | 多銘柄列挙(8-12 銘柄) |
| 7 | 不確実性(中国 / 競争 / SC) | [Toasted] | risk-side carve-out |
| 8 | 次期ガイダンスの背後論理 | [Hey] | フォワードルッキング |
| 9 | オプション戦略(具体 strike + 戦略名) | [Yeah!] | 5 種戦略 + 注意書き |
| 10 | 末尾(免責 + 出所 + 自動翻訳注 + brand-app CTA) | なし | moomoo 標準 footer |

**特徴**(moomoo 1 篇観察、N=1 ⚠):
- 表情アイコン分隔 H2(8 種多様、speed-priority な R-2.ext と差別化)
- dual-register: 本体 だ/である + 末尾「moomoo アプリ内の『マーケット』>『オプション』>『米国株』>『決算情報』でご確認ください」
- 数値密度 極めて高い(売上高 6812.7 億ドル / 粗利率 75% / 通期 2159 億ドル / 自社株買い 411 億ドル / Blackwell 600 万個 / Big Tech CapEx 7000 億ドル / オプション IV 53% 等)
- ticker 12+(ecosystem chain)
- **Option 戦略段が定義要素**:具体 strike price + 期日 + 戦略名 + 「ネイキッド売り回避」型注意書き
- 末尾免責標準文 + 「※ オプション取引には元本を超える損失が生じるリスクがあります」付帯
- 著者「ーmoomoo ニュース Sherry」

### 1.7 **Type R-X.T** — Brand-Bound Long-Form Theme/Sector Deep-Dive(3500–7000 chars / moomoo 1 篇実測 ✓)

**該当 trade-ideas scene**:`theme`(セクター・テーマ深掘、券商 research 風)

**観察源**:moomoo news(Julie 著、2026-02-05 作成)「Anthropic ショック / アンソロピック関連の恩恵銘柄抽出」(~4500-5500 字、引用例 5.8)。

**章節テンプレート**(観察):

| 順 | 章節 | アイコン | 役割 |
|----|------|---------|------|
| 1 | リード(修辞疑問先行 → ショック認識 → 構造的勝者選別宣言) | なし | 200-400 字 |
| 2 | ショック 1(主因) | [悲しい顔] | 200-400 字 |
| 3 | ショック 2(追い打ち) | [悲しい顔] | 200-400 字 |
| 4 | 恩恵カテゴリ A 導入 | [ほほえみ] | 100-200 字 |
| 5-N | カテゴリ A 個別銘柄カード ×4 | [ラッキー] | 各 200-300 字、3 段固定構造 |
| N+1 | 恩恵カテゴリ B 導入 | [ほほえみ] | 100-200 字 |
| ... | カテゴリ B 個別銘柄カード ×4 | [ラッキー] | 各 200-300 字 |
| 終-2 | 影響銘柄(Risk side) | [悲しい顔] | 両面提示段、CRM/NOW/ADBE/SNOW 等 |
| 終-1 | 備考:セクター・ローテーション + ETF | [ほほえみ] | 4 ETF 列挙 |
| 終 | 著者署名 + 出所 | なし | アナリスト Julie / 「moomoo 証券作成」 |

**個別銘柄カード固定構造(本 sample で 8/8 = 100%)**:
1. 段 1:銘柄事業説明(汎用ロジック、1-2 文)
2. 段 2:**Anthropic との具体的関係**(出資 / 契約 / 採用 + 数値)
3. 段 3:**中長期恩恵示唆**(「~期待できよう」「~押し上げよう」「~構造にあろう」)

**特徴**(moomoo 1 篇観察、N=1 ⚠):
- 表情アイコン 3 種固定([悲しい顔]ショック / [ほほえみ]カテゴリ導入 / [ラッキー]個別銘柄)= 編集テンプレート化
- **全文 だ/である 単一**(NVIDIA earnings deep-dive と異なり dual-register でない)
- 推量末尾「~であろう」「~押し上げよう」「~構造にあろう」「~期待できよう」が定義要素
- ticker 16+(主役 + ecosystem + ETF 4 本)
- A-TI3 強い:逆接マーカー「しかし」「ただ」「一方」「もっとも」多用
- **CTA:brand-app 導線 不在 → soft「~に注目したい」「合理的な選択肢かもしれない」**(institutional override 寄り、ADR-008 適用候補)
- 末尾免責 標準文不在(出所注のみ)→ platform footer 担保前提
- 著者:アナリスト個人名(Julie)、ニュース編集部署名と差別化

---

## 2. Micro Patterns — Type R 文案特点

### 2.1 Dual-Register 切換ポイント

| パターン | 切換マーカー | 適用 sub-form |
|---------|-------------|--------------|
| 末尾 1 文転換型 | 本体だ/である → 末尾「~です/ます」「~してください」 | R-1 / R-2 / **R-2.ext**(末尾 brand-app CTA のみ) |
| セクション見出し転換型 | `【まとめ】` `【行動】` 以降を です/ます | R-3 |
| 段落間転換型 | 分析段落と読者向け段落が独立(空行区切) | R-3 長型寄り / R-X.E |
| **全文単一(dual-register 抑制)** | 全文 だ/である 単一、CTA = soft 「~に注目したい」型 | **R-X.T**(institutional override 適用) |

**禁止**:同一文内の混在(「~である一方、~と思います」型)。RL-11 違反 + TI-C P0 ゲート発動。

**v0.2.0 追加**:R-X.T 適用時は ADR-008 institutional segment override に準じ、TI-C は緩和(全文 だ/である許容)、verification は「単一レジスタ だ/である ✓ / 読者呼びかけ不在 ✓ / soft CTA: ~に注目したい / ~であろう ✓」を要求。

### 2.2 リード(冒頭)パターン

| パターン | スキャン | 適用 sub-form |
|---------|---------|--------------|
| 数値先行型 | 第 1 文に主要数値 ≥ 1 件 | R-1 / R-2 / R-3 |
| 体言止めヘッドライン型 | 第 1 文末尾が名詞 | R-1 |
| 時点明示型 | 「前場終値」「14:35」「時間外取引で」 | R-1 / R-2 / R-2.ext |
| コンセンサス対比型 | 「市場予想を上回る/下回る」 | R-2 / **R-2.ext**(本 sub-form の定義要素) |
| **業界文脈先行型** | 「過去数ヶ月間、~では『~論』をめぐる議論が…」 | **R-X.E**(NVIDIA 篇観察) |
| **修辞疑問先行型** | 「~は補完者か、それともすべてを瓦解させる破壊者か――」 | **R-X.T**(Anthropic 篇観察) |
| **ナラティブ強調語** | 「残酷な現実」「真の勝者」「総悲観」「圧倒的」 | R-X.E / R-X.T(RL-3 境界、要監視) |

### 2.3 受け身 PASSIVE_ALLOW_LIST 利用パターン(TI-9 / ADR-010)

Type R 分析セクションは RL-10「受け身 2 個以上連続」スキャンから 6 語彙除外:

```
とみられる / と発表された / と報じられた / と見込まれる / と指摘される / と位置付けられる
```

**観察(moomoo 3 篇)**:
- R-2.ext:「と述べた」「(会社発表)」が高密度、allow-list 適用域
- R-X.E:「と確認された」「と捉えている」「と見ている」混在
- R-X.T:「とみられる」「と指摘した」「~発表された」混在

### 2.4 因果マーカー(必須)

| 強度 | マーカー | 適用 sub-form |
|------|---------|--------------|
| 強(明示因果) | 「を背景に」「を受けて」「が要因」「により」 | 全 sub-form(R-X 系で多用) |
| 中(間接因果) | 「を反映して」「に起因して」 | R-3 / R-X.T |
| 弱(状況描写) | 「のなか」「を踏まえ」 | R-3 / R-X.T |

**観察(moomoo 3 篇)**:R-X.T(Anthropic 篇)で「を背景に」「を受けて」「が要因」が密度最高(ほぼ全段落)。R-2.ext(NVIDIA flash)で bullet 単位「に伴う」「が寄与」「に関連する」が反復。

### 2.5 出典タグ(A-NW4 系の波及)

| 情報源タイプ | タグ | 適用 sub-form |
|-------------|------|--------------|
| 公式発表 | 「~と発表した」「~と公表した」「(会社発表)」「(CFO 発言)」 | R-2 / **R-2.ext**(bullet 単位反復) |
| 報道 | 「~と報じられた」「Bloomberg は~と指摘した」 | R-3 / R-X.T |
| 市場観測 | 「~とみられる」「との見方」 | R-3 / R-X.T |
| アナリスト | 「~氏は~と述べた」「~の見通しでは」 | **R-2.ext**(direct quote) / **R-X.E** / **R-X.T** |
| **企業 IR** | 「~の会社資料によると(2025年10月)」 | **R-X.T**(Anthropic 篇観察) |

**観察(moomoo 3 篇)**:出典タグの **bullet 単位密度** が R-2.ext の差別化マーカー(本 sample で「(会社発表)」12 回)。

### 2.6 推測語尾の階層化(A-TI4 / TI-2)

```
強(と見込まれる / 公算が大きい / と確認された)
中(と見られる / ~であろう / ~押し上げよう / ~構造にあろう)
弱(可能性がある / 余地がある / ~期待できよう / ~かもしれない)
```

**観察(moomoo 3 篇)**:
- R-2.ext:強(過去事実)+ 弱(規制 / 提携の不確実性)の極化、中層が薄い
- R-X.E:中(「と捉えている」「決定される見込み」)が支配
- **R-X.T:中の「~であろう」「~押し上げよう」「~構造にあろう」が定義要素**(institutional voice signature)

### 2.7 末尾(行動橋渡し)パターン

TI-5 の Type R 実装。CTA 動詞は **A-TI14 高転化型**:

| パターン | 例 | 強度 | 適用 sub-form |
|---------|----|------|--------------|
| アプリ機能誘導 | 「ウォッチリスト追加」「価格アラートのセット」 | 高 | R-3 |
| **brand-app 導線** | 「moomoo アプリ内の『~』>『~』でご確認ください」 | **高(ブランド転化)** | **R-2.ext / R-X.E** |
| 判断材料提供 | 「投資判断の参考とされたい」「ご検討ください」 | 中 | R-2 / institutional override |
| **soft 観察示唆** | 「~に注目したい」「~局面に入りつつある」「合理的な選択肢かもしれない」 | **低(institutional voice)** | **R-X.T** |

**institutional segment override**(ADR-008):`--segment institutional` 時は CTA stage = none、行動橋渡し節を削除 or「投資判断の参考とされたい」へ転換。**R-X.T は brand voice 上 institutional override に近い**。

### 2.8 **moomoo brand voice signature(v0.2.0 新設、3 篇共通要素)**

R-2.ext / R-X.E / R-X.T 3 sub-form に共通する moomoo 固有マーカー:

| 要素 | 内容 | 観察 |
|------|------|------|
| 自動翻訳注 | 「この記事は一部自動翻訳を利用しています」 | R-2.ext / R-X.E ✓、R-X.T △ |
| 出所明示 | 「出所:moomoo、[外部メディア]、[企業 IR]」 | 3/3 |
| 著者署名 | 「ーmoomoo ニュース [氏名]」(R-2.ext / R-X.E)/「マーケットアナリスト [氏名]」(R-X.T) | 3/3 |
| brand-app CTA | 「moomoo アプリ内の『~』>『~』でご確認ください」 | R-2.ext / R-X.E ✓、R-X.T 不在 |
| 末尾免責 | R-X.E のみ標準文 + Option リスク警告 | R-X.E のみ ✓ |

→ `case-library.md` に「moomoo voice signature」エントリ追加候補(別 PR)。

---

## 3. Scene 別適用ガイド(v0.2.0 拡張)

| trade-ideas scene | 主推荐タイプ | 字数 | 必須要素 |
|-------------------|------------|-----|---------|
| `flash` | R-1 | 80–140 | 数値+時点+影響+因果マーカー / TI-7 免除 |
| `earnings`(短型) | R-2 | 150–400 | 実績 vs 予想 / 株価反応 / 見通し推測体 / TI-7 免除 |
| **`earnings`(中型 / brand-bound)** | **R-2.ext** | **800–2000** | **bullet 駆動 H3 / 出典タグ bullet 単位 / benchmark 比較 / brand-app CTA** |
| `earnings`(深掘 / brand-bound + Option) | **R-X.E** | **4000–10000** | **表情アイコン分隔 / dual-register / Option 戦略段 / 多銘柄 ecosystem** |
| `morning`(短) | R-3 | 300–500 | 前日米国 / 本日見通し / カレンダー連動 |
| `morning`(長) | Type R 範囲外 → R-X.T 寄り判定 or `trade-ideas-guide.md` 参照 | 501–800 | TI-7 必須 |
| `picks` | R-4 | 80–200/銘柄 | 数値指標 ≥2 / レジスタ単一 / TI-1 厳守 |
| **`theme`(brand-bound 中長型)** | **R-X.T** | **3500–7000** | **修辞疑問リード / 銘柄カード固定 3 段構造 / 全文 だ/である / soft CTA / ETF 補足** |
| `theme`(SEO 個別株深掘 / かぶリッジ系) | Type B 範囲 | 6000–16000 | `trade-ideas-b-expert.md` 参照 |
| `community` | Type B 範囲 | 400–800 | 同上 |

---

## 4. Anti-Patterns(避けるべき書き方、v0.2.0 拡張)

| anti-pattern | 衝突 | 代替 |
|-------------|-----|------|
| 同一文内 だ/である + です/ます 混在 | RL-11 / TI-C P0 | 文を分ける、レジスタ切換マーカー使用 |
| 主観表現「強い」「魅力的」「お得」 | RL-3 / TI-A P0 | 「上昇率 X%」「PER XX 倍と相対的に低水準」 |
| 「絶対上がる」「100% 確実」「必ず」 | RL-3 / AC-16 流用 | 「上昇余地がある」「上昇シナリオが意識される」 |
| 数値出典なし「業績好調」「サプライズ決算」 | RL-9 / TI-3 / C-RL9 P1 | 「営業利益 +XX%(同社発表)」「市場予想を XX% 上回る」 |
| 曖昧時間「短期」「中期」「いずれ」 | TI-4.ext | 「数日内」「数週内」「前場終値で」 |
| 過熱表現「爆騰」「神銘柄」「爆益」 | TI-8.ext | 「+XX% 上昇」「年初来高値更新」 |
| 推奨断定「〇〇を買おう」「〇〇から逃げろ」 | RL-12 流用 / TI-1 | 「投資判断の材料となる」「注目に値する」 |
| 末尾免責欠落(R-X.E / theme / morning ≥501 字) | TI-7 / TI-B P0 | 標準免責文言を末尾追加(R-X.E は Option リスク警告も) |
| picks で数値指標 1 件以下 | AC-15 / C-AC15 P1 | 株価+前日比、PER、配当利回り から 2 項以上 |
| 因果マーカー欠落 | A-TI6(P2-A) | 「半導体需要回復を背景に」型を必ず挿入 |
| 単一推測語尾連発 | A-TI4(P2-A) | 強/中/弱を混在 |
| Calendar Linkage 欠落(morning) | A-TI9(P2-A) | 「来週 FOMC」「明日 雇用統計」等を必ず付記 |
| **R-2.ext で表情アイコン乱用** | speed-priority と矛盾(observation-based) | bullet 駆動 H3 のみ使用 |
| **R-X.E で dual-register 抑制** | brand voice 逸脱(本来 dual-register が moomoo deep-dive の標準) | 末尾 brand-app CTA で「~ご確認ください」を必ず保持 |
| **R-X.T で brand-app CTA を強引に挿入** | institutional voice 逸脱(observation-based) | 「~に注目したい」「~であろう」型 soft 誘導を維持 |
| **R-2.ext で出典タグ bullet 単位欠落** | brand voice 逸脱 / RL-9 弱化 | 各 bullet 末尾に「(会社発表)」「(CFO 発言)」付帯 |

---

## 5. 引用例

### 例 5.1 — Type R-1 Market Flash(framework、v1.0.0 で実 sample 置換予定)

> 日経平均、3 万 8,000 円台回復(2026 年 5 月 14 日 前場終値)
> 前日比 +X.X% の上昇で 5 営業日ぶり高値。半導体株主導の買い戻しが背景。
> 来週の FOMC を受けて推移を注視したい。

(レジスタ:本体 だ/である → 末尾「注視したい」で読者向け転換)

### 例 5.2 — Type R-2 Earnings Flash 短型(framework、v1.0.0 で実 sample 置換予定)

> 〇〇(XXXX)、26 年 3 月期 3Q 営業利益 +XX%
> 発表によれば、営業利益は前年同期比 +XX% の▲▲億円。市場予想(▲▲億円)を上回った。
> 通期見通しは据え置き。発表後の時間外で株価は +X% 反応した。
> 半導体需要回復が業績を牽引したとみられ、通期上方修正期待が高まりそうです。

### 例 5.3 — Type R-3 Morning Brief(framework、v1.0.0 で実 sample 置換予定)

> 【前日 NY 市場】ダウ +0.X%、S&P +0.X%、ナスダック +0.X% と続伸。雇用統計の好結果を受けて景気拡大期待が高まった。為替はドル円 XXX.XX 円台。
>
> 【本日の見通し】日経平均は前日終値比 +XXX 円水準で寄り付く公算。先物では XX,XXX 円付近が意識される。
>
> 【本日注目】14:00 景気動向指数発表、〇〇(XXXX)第 3Q 決算。
>
> 【行動】寄付前にウォッチリストへの追加と価格アラートのセットをご検討ください。

### 例 5.4 — Type R-4 Picks Card(framework、v1.0.0 で実 sample 置換予定)

> 〇〇(XXXX)
> 半導体製造装置の需要回復を背景に注目度上昇。直近決算で営業利益率が大幅改善し、通期上方修正期待が高まっています。
> 株価 X,XXX 円(前日比 +X.X%)/ PER XX 倍 / 配当利回り X.X%
> タグ:#半導体 #業績拡大 #高配当

### 例 5.5 — institutional segment override(framework、ADR-008)

> 〇〇(XXXX)、26 年 3 月期 3Q 営業利益は前年同期比 +XX% の▲▲億円。市場予想(▲▲億円)を上回った。
> 通期見通しは据え置き。発表後の時間外で株価は +X% 反応した。
> 半導体需要回復が業績を牽引したとみられる。投資判断の参考とされたい。

### **例 5.6 — Type R-2.ext Earnings Flash 中型(moomoo verbatim、postId 66020469)**

リード + ヘッドライン段:

> 半導体大手の $エヌビディア (NVDA.US)$ は、2026 FY Q4決算を発表した。時間外で一時株価が上昇。
>
> NVIDIAは2026会計年度第4四半期(4Q)の利益・売上高が市場予想を上回り、2027会計年度第1四半期(1Q)売上高見通しも市場予想を上回った。一方、対中規制対応(H200の限定ライセンス)や、H20の過剰在庫・購入義務に伴う45億ドルの費用計上、関税負担(H200の米国輸入時25%)が材料となった。

bullet section + 出典タグ密度:

> ・売上高:681億ドル(市場予想:658億ドル)
> ・調整後EPS:1.62ドル
> ・データセンター売上高:623億ドル(市場予想:おおむね603億ドル)
> ・データセンター売上高の顧客構成:ハイパースケーラーが「50%強」(CFO発言)

第三者 quote:

> Deepwater Asset ManagementのGene Munster氏は、株価反応が限定的なのは「AIトレードが終盤か、まだ始まったばかりか」を巡る議論を映すと述べた

末尾(brand voice signature):

> この記事は一部自動翻訳を利用しています
> 出所:moomoo、みんかぶ、Bloomberg、エヌビディアIR
> ーmoomooニュースZeber
>
> 決算ポイントを確認しよう「決算速報」で完全網羅!moomooアプリ内の「検索」>「決算発表」でご確認ください。

(レジスタ:全文 だ/である、末尾 brand-app CTA 1 文のみ「ください」)

### **例 5.7 — Type R-X.E Brand-Bound Long-Form Earnings Deep-Dive(moomoo verbatim、feedId 116134849085446)**

(NVIDIA Q4 决算 Summary、author Sherry。引用は構造観察済 `/tmp/moomoo_sample_116134849085446.md` 参照。代表的な要素:)

- リード:業界文脈先行型「過去数ヶ月間、米市場では『AIバブル論』をめぐる議論が絶えない」
- 主体提示:「日本時間2月26日、世界の『AI業界のトップ企業』 $NVIDIA (NVDA.US)$ は、完璧とも言える第4四半期の決算を発表」
- 表情アイコン分隔 H2:[Cool Guy] / [Cheerlead] / [Smart] / [Yeah!] / [Respect] / [Toasted] / [Hey] / [Yeah!]
- Option 戦略段:「カバードコール / リスクリバーサル / コール買い / プット買い / ターゲットバイイング」5 種、具体 strike + 期日 + 「※ 絶対にネイキッドでのコール売りは避けること」型注意書き
- 末尾免責:「※ オプション取引には元本を超える損失が生じるリスクがあります」+ 標準免責 boilerplate
- brand-app CTA:「moomoo アプリ内の『マーケット』>『オプション』>『米国株』>『決算情報』でご確認ください」
- 著者:「ーmoomoo ニュース Sherry」

(レジスタ:dual-register、本体 だ/である + 末尾「ご確認ください」)

### **例 5.8 — Type R-X.T Brand-Bound Long-Form Theme Deep-Dive(moomoo verbatim、Anthropic ショック / Julie 著)**

リード(修辞疑問先行型):

> 「AIは既存ビジネスの補完者か、それともすべてを瓦解させる破壊者か――」
> 2月3日、米ハイテク市場を襲った激震の正体は、新興勢力アンソロピック(Anthropic)が突きつけた「AIによる既存ソフト代替」という残酷な現実である。これまでのAI楽観論は一転し、市場には「淘汰」への恐怖が連鎖。

両面提示転換(逆接マーカー):

> しかし、総悲観による投げ売りについて「過剰反応」との指摘も上がっている。構造的なAIシフトの恩恵を中長期で享受する「真の勝者」は、こうした局面でこそ選別されるべきであろう。

個別銘柄カード固定 3 段構造(GOOG 例):

> AnthropicはGoogle CloudとTPUを大規模に活用しており、Claudeの高度化が進むほどTPU需要は構造的に拡大する。AI競争の激化は投資負担ではなく、Googleが自社設計半導体を外部AI企業に供給できる強みを可視化する局面であり、TPUを軸としたクラウド収益の持続性に注目したい。
>
> AnthropicとGoogle Cloudは2023年に戦略的パートナーシップを発表。また、Anthropicは2025年10月に「Google Cloud TPUとサービスの利用拡大」を発表した。Googleと提携し、最大100万個のTPUにアクセスする契約を締結している。この契約により、2026年までに1ギガワット超の計算能力が稼働する予定となっている。

soft 誘導 CTA(institutional voice):

> ハイテク株に偏重したポートフォリオを保有する投資家にとって、リスク分散の観点からこれらのETFや関連銘柄をポートフォリオの一部に組み入れる戦略は合理的な選択肢かもしれない。

末尾(brand voice signature、R-X.E と差別化):

> 26年2月5日作成 マーケットアナリスト Julie
> 出所:Bloombergや会社資料および各種資料をもとにmoomoo証券作成

(レジスタ:全文 だ/である 単一、推量末尾「~であろう」「~押し上げよう」「~構造にあろう」「合理的な選択肢かもしれない」、brand-app CTA 不在 → soft 誘導型)

---

## 6. P2-A との対応マッピング(v0.2.0 部分実測)

trade-ideas P2-A 15 項に対する Type R 各 sub-form 期待実装。**moomoo 3 篇観察分は実測値付記、それ以外は framework hypothesis(v1.0.0 で実測)**:

| P2-A ID | R-2.ext(N=1) | R-X.E(N=1) | R-X.T(N=1) | R-1/R-2/R-3/R-4(framework) |
|---------|----|----|----|---|
| A-TI1 Analytical Credibility Stack | ✓ ヘッドライン → bullet → コメント | ✓ 表情アイコン分隔で物理分離 | ✓ ショック → 恩恵カテゴリ → ETF | 高(全 type 必須構造) |
| A-TI2 Market Timing Specificity | ✓「02/25 16:37 ET」「2026 年 2 月」 | ✓「日本時間 2 月 26 日」「3 月の GTC」 | ✓「2 月 3 日」「2025 年 10 月」「2026 年まで」 | 高 |
| A-TI3 Risk Both-Sides | ✓ ヘッドライン段「一方」逆接 | ✓ [Toasted] 不確実性 section | ✓ 「しかし」「ただ」「一方」「もっとも」多用 | 中〜高 |
| A-TI4 Confidence Calibration | △ 強+弱の極化、中層薄 | ✓ 強/中/弱 階層混在 | ✓「~であろう」「~押し上げよう」中層支配 | 中〜高 |
| A-TI5 Numeric Precision Gradient | ✓ bullet 単位 億ドル/% 統一 | ✓ 億ドル/%/IV%/個数 多層 | ✓ 億ドル/%/個数 | 高 |
| A-TI6 Causal Markers | ✓「に伴う」「が寄与」「に関連する」 | ✓「に起因」「が寄与」「を導入し」 | ✓「を背景に」「を受けて」ほぼ全段落 | 高 |
| A-TI7 Theme-Sector-Stock Chain | △(銘柄主体、テーマ言及薄) | ✓ ecosystem 拡大段で連鎖 | ✓ ショック→セクター→銘柄→ETF | 中 |
| A-TI8 Past-Case Recency | ✓「ChatGPT 登場以降約 13 倍」 | ✓「前回 GTC」 | △ 直近事例参照少 | 中 |
| A-TI9 Calendar Linkage | △ 1Q ガイダンス言及のみ | ✓「3 月 GTC」「2026 年 4 月 1 日付」 | ✓「2025 年 10 月」「2026 年まで 1GW」 | R-3 ほぼ必中 |
| A-TI10 Consensus Contrast | ✓ bullet 全件「実績 vs 市場予想」 | ✓「アナリスト予想を大きく上回る」 | △ 直接対比は薄、影響銘柄段で間接 | R-2 ほぼ必中 |
| A-TI11 Ticker Explicitness | ✓ 4 銘柄 | ✓ 12+ 銘柄 | ✓ 16+ 銘柄(Carve-out 適用) | R-2/R-4 必須 |
| A-TI12 Entry/Exit Specificity | △ benchmark ranking のみ | ✓ Option strike price 明示 | △ ETF 名のみ | R-4 中 |
| A-TI13 Risk Line Visibility | ✗ 損切ライン不在 → 規制リスク列挙で代替 | ✓ Option pros/cons 明示 + Carve-out | ✗ 損切ライン不在 → Carve-out(ticker ≥ 5) | 低 |
| A-TI14 Action-Bridge Verb | ✓ brand-app | ✓ brand-app(深い階層誘導) | △ soft 誘導(institutional voice) | R-3 高 |
| A-TI15 Decision Path Compactness | △ 10 H3 sections、bullet で圧縮 | ✗ 8 sections、決定経路長 | ✗ 10 sections、決定経路長 | R-3/R-4 高 |

**v0.2.0 観察まとめ**(N=1 ⚠ small sample warning):
- R-2.ext は A-TI10(consensus contrast)が定義要素、A-TI3 / A-TI6 が高密度
- R-X.E は A-TI12(Option strike)/ A-TI4(階層化)が突出、A-TI15(コンパクトさ)で劣化
- R-X.T は A-TI3(両面提示)/ A-TI7(チェーン)/ A-TI9(カレンダー)が突出、A-TI10(対比)/ A-TI14(action-bridge)で institutional voice により劣化

**Type R(短型) vs R-X(長型) 比較**:R-2.ext は短型 R-2 と長型 R-X の中間ポジションを占める。R-X 系は decision path compactness で必然的に劣化(brand-bound deep-dive の本質)。

---

## 7. 使用方法

本ファイルは `--style trade-ideas` + Type R 判定が成立した時のみ lazy-load される(判定ヒントは Stance 章参照)。Type B 判定時は load しない。

### 併用関係

- `trade-ideas-guide.md` — T1 + T2 制約。**dual-register 制約(TI-C)は sub-form 別に運用**:R-1/R-2/R-3 厳格 / R-2.ext 末尾 1 文のみ許容 / R-X.E 通常 / R-X.T 緩和(institutional override 寄り)/ R-4 全文「です/ます」
- `trade-ideas-r-expert.md` — **Type R 構造・修辞ベンチマーク**(本ファイル)
- `trade-ideas-b-expert.md` — Type B(SEO 個別株深掘)構造・修辞ベンチマーク
- `case-library.md` — ブランド固有 voice signature(任意、moomoo voice の追加は別 PR)
- `delivery-gate.md` — TI-A / TI-B / TI-C P0 ゲート定義 + P2-A 採点

**典型ワークフロー**(Type R 経路):

1. Step 3 ルーティング → `--style trade-ideas --scene flash|earnings|morning|theme|picks`
2. Type B/R 判定 + sub-form 判定:
   - source 字数 ≤500 + 速報トーン → R-1/R-2/R-3 短型
   - 字数 800-2000 + bullet 駆動 + brand-app footer → **R-2.ext**
   - 字数 4000-10000 + 表情アイコン + 多銘柄 + Option/ETF → **R-X.E or R-X.T**
   - 字数 ≥5000 + SEO 個別株深掘 + かぶリッジ系 → Type B(本ファイル非 load)
3. **本ファイル lazy-load**、TI-C 運用ポリシーを sub-form 別に決定
4. Step 4 Layer 1(Structure)で本ファイルの 1.1〜1.7 章節テンプレートを参照
5. Step 4 Layer 2(Language)で 2.1〜2.8 micro-pattern を適用
6. Step 6 Naturalness Check の Proxy 3(Reference comparison)で本ファイルの引用例 5.6〜5.8(verbatim)と比較。framework 例 5.1〜5.5 は v1.0.0 で実 sample 置換予定

---

## 8. Out of Scope(v0.2.0 → v1.0.0 ロードマップ)

### v0.2.0 で完了

- ✓ R-2.ext(Earnings Flash 中型)sub-form 新設(N=1)
- ✓ R-X.E(Brand-Bound Earnings Deep-Dive)sub-form 新設(N=1)
- ✓ R-X.T(Brand-Bound Theme Deep-Dive)sub-form 新設(N=1)
- ✓ moomoo brand voice signature 観察(N=3)
- ✓ 引用例 5.6〜5.8 verbatim 化

### v1.0.0 で実施予定

- **R-1 / R-2 / R-3 / R-4 短型の実 sample 抽样 各 2-3 篇**:
  - kabutan.jp / minkabu.jp / 各券商 morning report(WebFetch 制限により 2026-05-14 時点未完了)
  - 引用例 5.1〜5.5 を verbatim に置換
- **R-2.ext / R-X.E / R-X.T 各 N≥3 への拡充**:
  - moomoo 系を中心に同 author 横断比較(Sherry / Julie / Zeber 系の voice 差分)
  - 異なる brand(SBI / 楽天証券 community 等)との比較
- **章節テンプレート命中率の実測**:全 sub-form で構造構成要素の出現率を計算
- **Micro pattern 統計**:2.1〜2.8 各パターンの抽样命中率(N/M 形式)
- **P2-A 命中率テーブル**(6 章)の実測値充填(N=1 → N≥3)
- **Type B との定量比較**(A-TI 各項の命中率差分)

### Out of scope(別 PR)

- ブランド固有 voice signature(moomoo Sherry / Julie / Zeber、楽天 / SBI 各 community)→ `case-library.md` 追加
- D1〜D9 評価 rubric の Type R/B + sub-form 別キャリブレーション → `diagnosis/cross-style-quality-rubric.md`
- channel × Type R sub-form マッピング(push / market-alert / EDM 短型 ↔ R-1/R-2、community feed ↔ R-X.E/R-X.T)→ ADR-011 / channel taxonomy ADR で扱う
- institutional vs retail Type R の差分 → ADR-008 拡張(R-X.T が institutional override 寄りという観察を反映)

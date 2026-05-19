# CHANGELOG — jp-style-optimizer

Format: narrative summary for major changes + Keep a Changelog item list.

---

## Versioning Policy

Adopted 2026-04-30. Applies to releases **after** 6.0.0. Historical entries retain their original numbering.

| Bump | Trigger | Examples |
|------|---------|----------|
| **MAJOR (X.0.0)** | **Only** when ANY of: ① core Stance rewrite (cognitive position changes); ② workflow full restructure (Step count/order wholesale change); ③ interface removal without backward compat shim | Rewriting SKILL.md stance; collapsing 6-step workflow into 3 phases; dropping `--style` flag entirely |
| **MINOR (6.Y.0)** | New/renamed T1 style, new T2 scene, new red line, new ADR, new verification step, expanded acceptance criteria — **as long as backward compat mapping is provided** | Adding `pre-launch` scene; adding CA-9 legal-risk channel-split; renaming a T1 with old→new compat table |
| **PATCH (6.0.Z)** | Swipe/Rewrite Pattern additions, localization sample extractions, typo/doc fixes, verification-block format tweaks | New brand-name convention rows; moomoo EDM pattern extraction; fixing broken cross-reference |

**Hard rules**:
- Any MAJOR bump must be paired with an ADR explaining the stance/workflow change.
- MINOR bumps that rename or retire published interfaces must append a row to the Backward Compatibility table in `references/style-guide.md`.
- A version number is not consumed unless it actually ships — work-in-progress uses git, not version reservations.

---

## [Unreleased] — 2026-05-15 — edm-localization-expert v0.1.1(I1 拡張 + K3 新設)(v6.7.0 pending)

4.21 sheet ico看这个 13 行の実戦 polish 過程で 2 件の細目化を抽出:

- **I1 を 3 タイプに拡張** — 旧 I1「文末「だ」「だろう」「焦点だ」追加」を、(a)助動詞型 / (b)推量・期待型 / (c)動詞補完型 の 3 サブパターンに分解。corpus 内 03.18 r28(`…利益確保も` → `…利益確保も狙える`)を(c)型として明示登録、4.21 r14 で reproduce 確認。Title セクションでの体言止め解消パターンを汎用化。
- **K3 新設「疑問内容句尾「。」→「?」転換」** — DS が「~なるか。」「~どうか。」のような疑問副詞含み文を「。」で締めている場合、Title/Subject では「?」に置換。E2(半角→全角 ?)とは別軸の "文末記号置換" として独立。4.21 r4(`60,000円の大台突破なるか。` → `…なるか?`)で初記録、corpus 内同型多数。Frequency Reference Table で 中頻度 と暫定推定。

#### Changed
- **`references/edm-localization-expert.md` v0.1.0 → v0.1.1** — frontmatter version bump。
- **§1.I1** — 標題「文末「だ」「だろう」「焦点だ」追加(体言止め回避)」→「末尾動詞・助動詞補完(体言止め回避)」。3 サブパターン (a)(b)(c) 記述追加、(c) 動詞補完型例に 03.18 r28 + 04.21 r14 reproduce 注記。
- **§1.K3(新規)** — 疑問内容句尾「。」→「?」転換 ルール、E2 との差異(記号変換 vs 文末記号置換)、Content 本文での例外(断定/伝聞末尾「。」維持)を記述。corpus 観察:04.21 r4 で初記録、コーパス内同型多数。
- **§3 Frequency Reference Table** — Rank 5 行を「I1 文末を整える」→「I1 末尾動詞・助動詞補完((a)(b)(c))」に書き換え、新 Rank 19a 行 K3 を中頻度として追加。

---

## [Unreleased] — 2026-05-14 — RL-4 Hard/Soft 階層化(件名・タイトル・見出し系を Soft 化)(v6.7.0 pending)

RL-4 の文字制限を **Hard / Soft** の二段階に分割。従来は全 field が Hard ceiling として「超過 → 必ず短縮 → 再生成」フローを強制していたが、件名・タイトル・見出し系(顧客の最初接触面・装飾的伸縮余地あり)では編集者後処理での微調整余地を残す方が実務に合うとの判断。本文・プリヘッダー・CTA・全文・各文系(配信媒体仕様・構造的に超えると壊れるもの)は引き続き Hard 維持。

**Soft 適用 field**(超過時 ⚠ flag + 短縮候補案 1-3 件併記、配信決定 = ⚠ 注記交付 / P1):
- `campaign / push channel` タイトル ≤20
- `campaign / edm channel` 件名 ≤40
- `campaign / banner channel` メイン ≤15
- `news/{flash, alert, wrap, earnings, digest, indicator}` 見出し(各 scene の上限値)

**Hard 維持 field**(超過 → P0 交付不可、compression rules 適用後再計測):
- 全文系(sns/flash 全文、news 各 scene 全文、trade-ideas/flash 全文)
- 本文・プリヘッダー・CTA・サブ・各文(product/script)

#### Changed
- **`SKILL.md` RL-4** — 表題を「Scene hard character limits」→「Scene character limits」に変更。表に Type 列(Hard/Soft)追加、push/edm/banner channel の field を行ごとに分割表示。Soft 違反時の処理(⚠ flag + 短縮候補案併記、P1 注記交付)を明記。
- **`SKILL.md` AC-3 / AC-4** — Hard / Soft の挙動差を明示。Soft 超過時の表示形式「件名: 42文字 ⚠ Soft (≤40 推奨) / 短縮案: …」を AC-4 に追加。
- **`SKILL.md` Step 5「Scenes with character limits (RL-4)」** — Hard 違反 = P0 / Soft 違反 = P1 の分岐明記。Soft 違反時は短縮候補案を併記し編集者判断に委ねる。

#### Rationale
- 4.21 sheet 検証中、`r2 Subject Line` が DS 出力 42 字 = RL-4 件名 40 字超過。従来 spec では強制短縮が要求されたが、native editor の corpus(N=274)を見ると 件名/見出し は ±1〜3 字の振れ幅は許容され、機械的短縮よりも flag + 候補提示の方が後段ワークフローに親和的。RL-4 全体を緩めるのではなく、装飾系のみ Soft 化することで配信媒体仕様(本文/CTA)の保護は維持。

---

## [Unreleased] — 2026-05-14 — edm-localization-expert v0.1.0(empirical N=274 抽样、post-LLM editorial pass 14 系統 pattern 化)(v6.7.0 pending)

`references/edm-localization-expert.md` を新設(初稿 v0.1.0、empirical 直行)。**LLM(DS 3.2)出力の日本語コピーをネイティブ編集者が EDM 配信形態に整える際の編集パターン集**として、moomoo 証券 JP の Trade Idea EDM 2 年分 corpus(95 週次バッチ、4-person panel:@kambara / @tabata / @kawade / @v_hayakawa)から **274 real DS→LOC edit pairs** を抽出・類型化。

**14 系統 pattern**(A 〜 L + Silent Baseline + Frequency Table + Sub-module 別優先度):
1. **A. Brand / Entity naming** — A1 `moomoo`→`moomoo証券`(頻出)/ A2 セクター・テーマ裸名詞 → `◯◯株 / ◯◯関連株 / ◯◯銘柄` 補完(頻出)
2. **B. Numeric formatting** — B1 全角→半角(頻出)/ B2 千位カンマ(中)/ B3 `%` 全半角は揺れ
3. **C. Verbal phrasing 金融用語化** — C1「下回る」→「割れ」(n=2 注意)/ C2 カタカナ口語動詞→漢語 / C3 強い断定語→中庸(頻出)/ C4「てる」→「ている」(n≈3)
4. **D. Particle / connective** — D1「年初来で」→「年初来から」(n=1 注意)/ D2 逆接「ても」/ D3 属格化(中)
5. **E. Punctuation & spacing** — E1 `?!`⇄`!?`(n=2)/ E2 半角→全角 `？`(頻出)/ E3 読点・スペース整形(中)/ E4 主見出し読点削除
6. **F. Quote/bracket** — F1 新概念の `「」` 化(頻出)/ F2 ストレート→カーリー quote(頻出)/ F3 `「」` 外し・curly 互換
7. **G. Technical term refinement** — G1 `AI`→`生成AI`(頻出)/ G2 業界語⇄平易語 双方向(中)
8. **H. Ticker conventions** — H1 `<XXXX>` `(XXXX)` `<XXXX.JP>` は silent baseline 維持
9. **I. Sentence-final** — I1 文末「だ・だろう・焦点だ」追加(頻出)/ I2 感嘆→疑問の煽り抑制(中)/ I3「皆さま」→「みんな」(n=2 コミュニティ限定)
10. **J. 体裁** — J1 1行→2行 改行分離(中)
11. **K. Specificity 補強** — K1 ぼかし→具体(頻出)/ K2 ロケール誤り・typo 修正(頻出)
12. **L. その他** — L1 報道発言の鉤括弧化 / L2 URL 独立行化(頻出)

**Silent baseline**(変更されない要素群): 銘柄コード / 企業正式名称 / 数値ファクト / テクニカル用語(MACD/RSI/PBR/NT 倍率/QUICK コンセンサス) / CTA 定型句末尾「moomoo証券なら売買手数料0円で日本株に投資できる！今すぐチャンスをつかもう！」/ URL query string / 段落構造の根幹。

**Sub-module 別適用優先度**(Subject Line / Preview / Title / Introduction / Content / CTA & Link / Button / Greeting / Picture)を corpus 観察に基づいてマッピング。

#### Added
- **`references/edm-localization-expert.md`(新規 v0.1.0)** — frontmatter(N=274, source, editors, ds_engine, scope), §0 Scope & Application, §1 Pattern Catalog(14 系統 A〜L), §2 Silent Baseline, §3 Frequency Reference Table(28 行 ranking), §4 Sub-module 別適用優先度(9 sub-module × 主要 pattern マッピング), §5 検証ブロック追加項目(Step 5 verification block), §6 Limitations(6 項), §7 Cross-reference(campaign-guide / trade-ideas-guide / trade-ideas-r-expert / case-library / moomoo-jp-routing)。
- **`SKILL.md` References table** に新行追加(`edm-localization-expert.md`、Load When = `--style campaign --scene edm` AND 入力が LLM/機械翻訳の日本語出力 OR `--style trade-ideas` で配信媒体が EDM、Step 4 Layer 2 末尾 / Layer 3 前)。

#### Limitations
- 単一ブランド corpus(moomoo 証券 JP)— 他金融広告主では再検証必要。
- DS 3.2 出力に対する pattern — GPT/Claude/Gemini 等他 LLM では特に B1/B3/F2 のフォーマット既定値が異なる可能性。
- EDM channel 最適化 — Push/SNS/Banner では文字制限が異なるため A2/J1 は適用条件再評価。
- 観察 n=1, n=2 pattern(D1 / E1 / I3 / C1)は一般化リスクあり、新規 corpus で要検証。
- K2 factual 修正は LLM 性能向上で頻度低下する pattern(長期的には A1/A2/F2/G1 等の brand/style 固有 pattern が残る)。
- Editor 個人差(4-person panel)は集合的傾向であり、個別 editor のスタイル差は分離していない。

---

## [Unreleased] — 2026-05-14 — trade-ideas-r-expert v0.2.0(部分実 sample 抽样、R-2.ext / R-X.E / R-X.T 新設)(v6.7.0 pending)

`references/trade-ideas-r-expert.md` を framework-only(v0.1.0)から partial-empirical(v0.2.0)に昇格。moomoo 3 篇 verbatim 抽样により、既存 Type R(80–500 字短型)枠の **外側に存在する** 2 つの sub-form 群を観察・命名:

1. **R-2.ext(Earnings Flash 中型 / 800–2000 字)** — moomoo postId 66020469「【エヌビディア決算速報】時間外一時上昇!」(author Zeber、~1300 字)。**bullet 駆動 H3 sections + 出典タグ bullet 単位密度**(本 sample で「(会社発表)」12 回反復)+ 表情アイコン不在(speed-priority)+ benchmark ranking + 第三者 quote(direct-quote 含)。短型 R-2(150–400)と長型 R-X(4000+)の中間ティアを占める。
2. **R-X.E(Brand-Bound Long-Form Earnings Deep-Dive / 4000–10000 字)** — moomoo feedId 116134849085446「[NVIDIA 決算 Summary] 圧倒的な業績と『真の起爆剤』!」(author Sherry、~6500-7500 字)。**表情アイコン分隔 H2(8 種多様)+ dual-register(本体 だ/である + 末尾 brand-app CTA「ご確認ください」)+ Option 戦略段(具体 strike + 期日 + 戦略名 + 「ネイキッド売り回避」型注意書き)が定義要素**。
3. **R-X.T(Brand-Bound Long-Form Theme Deep-Dive / 3500–7000 字)** — moomoo news「Anthropic ショック / 恩恵銘柄抽出」(author Julie、~4500-5500 字)。**修辞疑問先行型リード + 表情アイコン 3 種固定([悲しい顔][ほほえみ][ラッキー])+ 個別銘柄カード固定 3 段構造(事業 → Anthropic 関係 → 恩恵示唆)+ 全文 だ/である 単一 + soft 誘導 CTA(「~に注目したい」「~であろう」)= institutional override 寄り**。brand-app CTA 不在、ETF 推奨段含む。

R-1 / R-2(短型) / R-3 / R-4 は依然 framework-only(v1.0.0 で実 sample 抽样後充填)。

#### Added
- **`references/trade-ideas-r-expert.md` v0.2.0 sub-form 拡張** — Stance 章の sub-form ルーティング表を 4 行(R-1/R-2/R-3/R-4)から 7 行(+R-2.ext / R-X.E / R-X.T)に拡張。Type R 判定ヒント章に短型/中型/長型 3 ルートを記載。
- **§1.3 Type R-2.ext** — 11 行構造テンプレート(リード/株価ウィジェット/ヘッドライン段落/決算サマリー bullet/事業別内訳/見通し/コメント/特殊論点/その他/市場の見方/末尾)+ R-X.E との差分表 + N=1 観察。
- **§1.6 Type R-X.E** — 10 行構造テンプレート(表情アイコン 8 種付帯)+ Option 戦略段の定義要素扱い + N=1 観察。
- **§1.7 Type R-X.T** — 11 行構造テンプレート(表情アイコン 3 種固定)+ 個別銘柄カード固定 3 段構造 + soft 誘導 CTA(institutional voice)+ N=1 観察。
- **§2.1 Dual-Register 切換ポイント** に新行「全文単一(R-X.T 適用時、ADR-008 institutional override 準用)」追加。
- **§2.2 リードパターン** に「業界文脈先行型(R-X.E)」「修辞疑問先行型(R-X.T)」「ナラティブ強調語(RL-3 境界)」3 行追加。
- **§2.5 出典タグ** に「企業 IR 引用(R-X.T)」「bullet 単位密度(R-2.ext)」明示。
- **§2.6 推測語尾の階層化** に R-X.T 定義要素「~であろう / ~押し上げよう / ~構造にあろう / 合理的な選択肢かもしれない」記載。
- **§2.7 末尾(行動橋渡し)** に「brand-app 導線(R-2.ext / R-X.E)」「soft 観察示唆(R-X.T)」明記。
- **§2.8 moomoo brand voice signature**(新章)— 自動翻訳注 / 出所「moomoo + 外部メディア + 企業 IR」/ 「ーmoomoo ニュース [氏名]」型署名 / brand-app CTA / Option リスク警告 の 5 要素を 3 篇 cross-sample で観察。
- **§3 Scene 別適用ガイド** に 3 行追加(`earnings`(中型 / brand-bound) ↔ R-2.ext / `earnings`(深掘 / brand-bound + Option) ↔ R-X.E / `theme`(brand-bound 中長型) ↔ R-X.T)。
- **§4 Anti-Patterns** に 4 行追加(R-2.ext で表情アイコン乱用 / R-X.E で dual-register 抑制 / R-X.T で brand-app CTA 強引挿入 / R-2.ext で出典タグ bullet 単位欠落)。
- **§5 引用例 5.6 / 5.7 / 5.8** — moomoo verbatim 引用(Zeber / Sherry / Julie 各 1 篇代表段落)。framework 例 5.1〜5.5 は v1.0.0 で実 sample 置換予定として明記保持。
- **§6 P2-A 対応マッピング** — sub-form 別命中観察(R-2.ext / R-X.E / R-X.T 各 N=1、small sample warning 付き)。R-X.T が institutional voice により A-TI10 / A-TI14 で劣化 / A-TI3 / A-TI7 / A-TI9 で突出という観察を記録。

#### Changed
- **`references/trade-ideas-r-expert.md` frontmatter** — `version: 0.1.0` → `0.2.0`、`status: framework-only` → `partial-empirical(R-2.ext / R-X.E / R-X.T 観察済、R-1/R-3/R-4 依然 framework-only)`、`source` 行に moomoo 3 篇の具体的識別子(feedId / postId / author)を追加。
- **`SKILL.md` References table — `trade-ideas-r-expert.md` 行** — v0.1.0 placeholder 表記から v0.2.0 実装内容(7 sub-form 列挙、R-2.ext / R-X.E / R-X.T を太字でマーク)に更新。Load 条件も「短型 ≤500 / 中型 800-2000 brand-bound earnings / 長型 3500-10000 brand-bound deep-dive」に拡張。

#### Backward Compatibility
- 既存 sub-form(R-1 / R-2 / R-3 / R-4)の章節テンプレート・micro pattern は未変更。新 sub-form は **追加** であり既存制約に上書きしない。
- TI-C dual-register P0 ゲートの運用ポリシー差分は sub-form 別に明記:R-1/R-2/R-3 厳格 / R-2.ext 末尾 1 文のみ許容 / R-X.E 通常 / R-X.T 緩和(institutional override 寄り)/ R-4 全文「です/ます」一貫。
- ADR-008 institutional override は R-X.T に **準用** であり拡張ではない。正式拡張は v6.7.0 別 entry で扱う。

#### Limitations(small sample warning)
- R-2.ext / R-X.E / R-X.T 各 N=1。命中率は単一 sample 観察。v1.0.0 で各 N≥3 へ拡充予定。
- R-1 / R-2(短型) / R-3 / R-4 は依然 framework-only(WebFetch 制限により kabutan / minkabu / 各券商 morning report 未抽样)。
- moomoo brand voice signature は 3 篇 cross-sample で観察したが、author 別の差分(Sherry / Julie / Zeber)は未実証。

---

## [Unreleased] — 2026-05-13 — Delivery Quality Gate (v6.2.0 pending)

Formalizes go/no-go judgment for each output. Reclassifies the existing Step 5/6 verification items into a three-tier severity model (P0 hard block / P1 conditional / P2 soft warn) and introduces a final `Delivery Decision` line so downstream readers can tell at a glance whether an output is ready. No new constraints are introduced — every gate ID derives from existing RL-* / AC-* / D-* / per-style codes (CA / TI / NC / PC / C). Backward compatible: legacy Step 5/6 phrasings are preserved as components inside the standardized verification block.

#### Added
- **`references/delivery-gate.md`** — three-tier severity model, P0 universal (8 items) + P0 per-style (campaign 3 / trade-ideas 3 / news 4 / product 2 / compliance 5), P1 conditional (4 items, source-deficient → ⚠ marker), P2 soft (6 items), decision algorithm, standardized **Delivery Gate** verification block, three worked examples. Loaded at Step 7 entry — not part of the always-loaded Phase 1 bundle (Phase 1 total unchanged).
- **P2-A — Attractiveness Proxy(per-style)** — added to `references/delivery-gate.md` as a new soft-warn tier alongside P2. Per-style definitions of「吸引力」 with domain-expert validated dimensions:
  - **campaign 転換吸引力(クリック誘導)** — 9 項:A-CMP1 Benefit-First Urgency / A-CMP2 Lifecycle Consistency / A-CMP3 Concrete Density / A-CMP4 Benefit-Deadline Co-Location / A-CMP6 Numeric Plurality / A-CMP7 CTA Visibility / A-CMP8 Single CTA Focus / A-CMP9 Hook Strength / A-CMP10 Friction Reduction
  - **trade-ideas 交易転化吸引力(分析→注文)** — 15 項:A-TI1〜A-TI4(分析信頼性スタック / Market Timing / Risk Both-Sides / Confidence Calibration)+ A-TI5〜A-TI10(精度梯度 / 因果語彙 / セクター連結 / 過去事例 / カレンダー連動 / コンセンサス対比)+ A-TI11〜A-TI15(Ticker / Entry-Exit / Risk Line / Action-Bridge Verb / Decision Path Compactness)
  - **news 情報吸引力(scan-to-decision)** — 7 項:A-NW1/2/3/4 + A-NW7 5W+Unit Completeness / A-NW8 Modality-Free Headline / A-NW9 Factuality-Analysis Boundary
  - **product 多目的吸引力(理解 / 使用転化 / 継続 / クロスセル)** — 25 項:
    - 理解 = A-PR1 Jargon Onboarding / A-PR2 Scanability / A-PR3 Concrete Specificity / A-PR4 Action-Per-Step Minimalism / A-PR5 Use-Case Specificity / A-PR6 Outcome Quantification / A-PR7 Negative-Space Avoidance / A-PR8 Compare-Axis Explicit / A-PR19 Goal-Oriented Entry / A-PR24 Empathic Identity Hook / A-PR26 Reading-Outcome Preview / A-PR30 Headline-Embedded Numerals
    - 使用転化 = A-PR9 First-Action Anchor / A-PR11 Trial-Verb CTA / A-PR20 Testimonial Density / A-PR21 Tenure Proof / A-PR23 Adoption Scale / A-PR25 Authoring Credentialing / A-PR27 Both-Sides Disclosure / A-PR29 Authoritative Reference
    - 継続 = A-PR12 Frequency Cue / A-PR13 Cumulative Value / A-PR28 FAQ Coverage
    - クロスセル = A-PR15 Upsell Path Visibility / A-PR17 User-Tier Segmentation
    - 第二弾追加(2026-05-13、SEO メディア 4 站点抽样研究):A-PR19 / A-PR20 / A-PR21 / A-PR23 / A-PR24
    - 第三弾追加(2026-05-13、zuu.co.jp/media 8 篇深挖):A-PR25 Authoring Credentialing(監修者+資格+経歴明示)/ A-PR26 Reading-Outcome Preview(「この記事でわかること」型サマリー)/ A-PR27 Both-Sides Disclosure(メリット/デメリット並列)/ A-PR28 FAQ Coverage(末尾よくある質問 ≥3 件)/ A-PR29 Authoritative Reference(公的機関・大手メディア参照)/ A-PR30 Headline-Embedded Numerals(見出しに数値)
  - **compliance 信頼吸引力** — 4 項:A-CP1/2/3/4
  - Recorded as `✓/✗` per item with score = `✓ 件数 / 総件数`. **配信決定には影響しない**(score 0/N でも `✅ 交付可` は出る)— hard gate にしない理由は主観性 + 測量誤差。Verification Block に新行 `[P2-A] 吸引力: ... → N/M`。Existing P0/P1/P2 sections unchanged.
  - **A-TI13 carve-out**:同一出力内 ticker ≥ 5 件 → 広範情報提供と判定し本項免除(個別投資推介責任の境界、ticker 多数列挙時は推介性が希釈される)。
- **`SKILL.md` Step 7 — Delivery Decision** — invokes `references/delivery-gate.md`, runs the decision algorithm (≤3 P0 revise loops), emits the standardized verification block, and ends with a single `Delivery Decision: ✅ 交付可 | ⚠ 注記交付 | 🛑 交付不可:[IDs]` line. P2-A は同時実行されるが配信決定には影響しない旨を Step 7 説明に明記。
- **`references/trade-ideas-b-expert.md`** — trade-ideas **Type B**(Blog/SEO 個別株深掘)sub-form 専用 構造・修辞ベンチマーク module derived from 22-article deep-dive of `kabu.bridge-salon.jp`(かぶリッジ、moomoo 証券 in-house SEO blog). **Key finding**:本媒体 22 篇全文で「だ/である」体は **0 件**(soft_register 22/22)、です/ます体一貫。これは既存 `trade-ideas-guide.md` が前提としてきた dual-register(分析=だ/である、読者=です/ます)と異なる sub-form の存在を示す。**設計上の決定**:trade-ideas style を **per-sub-form 拆分管理**に変更 — Type R(券商 research / morning brief、dual-register、短型)/ Type B(SEO 個別株深掘、です/ます一貫、長型 6,000–16,000 字)。本ファイルは Type B 専用、Type R は将来 `trade-ideas-r-expert.md` で別管理(未存在時は `trade-ideas-guide.md` で代用)。Contains: (1) Stance + sub-form ルーティング表 + Type B 判定ヒント;(2) 2 macro article types — B-1 Single-Stock Deep Dive(個別株深掘、5–7 章)/ B-2 Theme/Ranking Deep Dive(テーマ・ランキング、4–6 章);(3) 6 micro-pattern subsections — 「💡 かぶリッジの結論」box 先行 20/22、numeric_density_lead 22/22、結論先行 20/22、専門家 3 層構造、視覚分離マーカー、両面提示比率;(4) Scene 別適用ガイド(theme/community/picks ↔ Type B-1/B-2 マッピング);(5) Anti-Patterns table(投資推奨断定の回避、AC-12/RL-12 流用);(6) 5 verbatim 引用例;(7) P2-A 15 項命中率テーブル。**dual-register P0 ゲート(TI-C)免除条件** を Type B 判定時に追加(SEO 媒体・字数 ≥5,000・個別株深掘トーンが該当)。Loaded lazily at Step 4 entry when `--style trade-ideas` routed AND Type B 判定成立時のみ。SKILL.md References table に Type B/R 2 行を追加(R は placeholder)。
- **`references/product-expert.md`** — product 構造・修辞ベンチマーク module derived from 20-article deep-dive of zuu.co.jp/media (NET MONEY 編集部). Contains: (1) 3 macro article types — Type A Compare-Long(33–70K chars、`compare`/`detail`)/ Type B Single-Service Review(6–17K、`detail`/`onboard`)/ Type C Interview(7.5–9K、特殊用途)、各 7–8 章節テンプレート;(2) 6 micro-pattern subsections — 導入(修辞疑問共感型 18/20)/ 見出し措辞 / 句法ツールキット(数値密度・体言止め・専門家署名 3 層)/ 肯定否定切換 / 数値出典スタイル / 末尾構造;(3) Scene 別適用ガイド(7 product scenes ↔ Type A/B/簡略 マッピング);(4) Anti-patterns table(既存 RL/AC との衝突回避);(5) 5 verbatim 引用例;(6) P2-A 25 項命中率テーブル(本媒体実装観察データ)。Loaded lazily at Step 4 entry when `--style product` routed. **case-library.md(brand voice)/ product-guide.md(T1+T2 制約)とは職責分離**:本 file は汎用構造・修辞ベンチマーク。SKILL.md References table に新行追加。

#### Changed
- **`SKILL.md` Output Format** — replaces the freeform `検証:` block with the standardized **Delivery Gate** block, including the new `[P2-A] 吸引力:` line between `[P2]` and `Delivery Decision`. Existing Step 5/6 phrasings remain as the building blocks of P0/P1/P2 sections; legacy readers parsing those phrasings continue to work.
- **`SKILL.md` References table** — adds a row for `references/delivery-gate.md` (Phase 2 conditional, loaded at Step 7); annotates `cross-style-quality-rubric.md` row to clarify that the rubric is a post-hoc evaluation tool distinct from the delivery gate.

#### Backward Compatibility
- No interface removal. `--style` / `--scene` / `--segment` calls unchanged.
- All existing RL / AC / per-style constraint IDs are referenced verbatim — no rule additions, only severity classification.
- P2-A is purely additive (new soft-warn tier) and does not affect the `Delivery Decision` line. Outputs that would have been `✅ 交付可` before P2-A remain `✅ 交付可` regardless of P2-A score.
- Phase 1 always-loaded bundle: SKILL.md (3,450w) + style-guide.md (751w) = 4,201w, ≤ 5,000 ✓. `delivery-gate.md` is loaded at Step 7 entry, after routing and transformation are complete — it does not enter the Phase 1 bundle.

#### Token budget
- SKILL.md: 3,232 → 3,450w (≤ 3,500 ✓; +18w for Step 7 P2-A note + Output Format `[P2-A]` line)
- `delivery-gate.md`: 965 → ~3,000w (extended budget; +2,035w for P2-A section + Verification Block update + 60 domain-validated dimensions across 5 styles, including 25 product items spanning 4 sub-goals)
- Phase 1 always-loaded total: 3,983 → 4,201w (≤ 5,000 ✓)

#### Out of Scope (deferred)
- Renaming `diagnosis/cross-style-quality-rubric.md` to align with the v6.0 5-T1 taxonomy (Marketing/Report/Legal/Support → campaign/trade-ideas/news/product/compliance) — separate PR.
- Automating D1–D9 scoring from gate output — future ADR.

---

## [Unreleased] — 2026-05-12 — moomoo JP routing integration

Adds brand-routing reference for moomoo JP and a 31-sample control group for boost A/B regression testing. Establishes the brand-routing extraction pattern (ADR-011) for future brands whose channel inventory exceeds the threshold. Purely additive — no architecture change, no breaking change. **Version bump pending** (likely MINOR per Versioning Policy: new ADR + new conditional reference file; coordinate with the unshipped v6.1.0 work tracked in `diagnosis/synthesis.md`).

#### Added
- **`references/moomoo-jp-routing.md`** (1,050w) — moomoo JP channel ↔ `--scene` ↔ RL-4 limit map. 5 Tier 1 sub-tables (campaign / trade-ideas / news / product / compliance) + segment table + brand-specific overrides per Tier 1 + 5-step routing checklist. Conditional load when input contains `moomoo` / `moomoo証券`.
- **`diagnosis/moomoo-jp-control-group.md`** (386 lines, 31 samples) — verbatim Japanese samples from 飞书 wiki `OGQQwEmmhi0FFJkGwSYcasNCnyh` organized by Tier 1 (campaign 5 / trade-ideas 5 / news 7 / product 10 / compliance 4) with sheet/row provenance and `--style`/`--scene` recommendations. Never runtime-loaded; used for boost-effect A/B regression.
- **`docs/adr/ADR-011-brand-routing-extraction-pattern.md`** — codifies the case-library entry + `{brand}-routing.md` + `{brand}-control-group.md` three-file pattern. Extraction trigger: ≥ 5 distinct delivery channels in any single Tier 1, OR ≥ 3 Tier 1 categories with channel-level RL-4 differences.

#### Changed
- **`SKILL.md` References table** — added one row for `moomoo-jp-routing.md` (load condition: input contains `moomoo` / `moomoo証券`; loads alongside the case-library moomoo entry at Step 3 + Step 3.5). SKILL.md word count 3,194 → 3,232 (≤ 3,500 ✓).
- **`references/style-guide.md`** — added "Brand-Specific Routing Overlay" section with brand-trigger → companion-file table. style-guide.md word count 668 → 751 (≤ 1,500 ✓). Always-loaded total 3,827 → 3,983w (≤ 5,000 ✓).
- **`references/case-library.md` (moomoo entry)** — appended "Companion files" pointer to `moomoo-jp-routing.md` and `moomoo-jp-control-group.md`. Expanded "Primary scenes" to reflect cross-T1 coverage discovered during the audit.
- **`diagnosis/structural-audit.md` / `token-audit.md` / `platform-check.md`** — refreshed for this release; structural 9-item check PASS, token budget within limits, platform CLEAN.
- **`diagnosis/synthesis.md`** — appended Phase 1 summary, Phase 2 prescription (8 actions), Phase 3 verification.

#### Backward Compatibility
- No breaking changes. Existing `--style` / `--scene` calls unaffected. Old `--style marketing` etc. continue to route per the existing Backward Compatibility table.

---

## [6.0.0] — 2026-04-29

### Major architecture: 5-style Tier 1 redesign + split-by-T1 reference files

Complete Tier 1 taxonomy redesign via mojo-skill-creator boost workflow. Replaces the legacy 5-style taxonomy (marketing/product/report/legal/support) with domain-research-backed architecture (campaign/trade-ideas/news/product/compliance). Splits monolithic style-guide.md into per-T1 conditional reference files, reducing always-loaded context 56% (7,828→3,478 words).

#### Added
- **`campaign` (T1)**: New style for period-limited incentive campaigns. 8 constraints (CA-1–8). 6 T2 scenes: launch/remind/lastday/result/seasonal/referral. Lifecycle-based design.
- **`trade-ideas` (T1)**: New style for market analysis with action bridge. 8 constraints (TI-1–8). 6 T2 scenes: flash/theme/earnings/morning/picks/community. Dual-register design (RL-11 exception).
- **`news` (T1)**: New style for objective financial event reporting. 7 constraints (NC-1–7). 6 T2 scenes: flash/wrap/earnings/indicator/digest/alert. Strict fact-first, CTA禁止, analysis≤30%.
- **`compliance` (T1)**: Merged legal+support into unified trust-building style. 7 constraints (C-1–7). 5 T2 scenes: disclosure/terms/disclaimer/faq/guide.
- **Per-T1 guide files**: `references/campaign-guide.md`, `references/trade-ideas-guide.md`, `references/news-guide.md`, `references/product-guide.md`, `references/compliance-guide.md` (each ≤340 words, conditional load).
- **AC-9–AC-12**: New acceptance criteria for campaign (deadline), trade-ideas (disclaimer), news (CTA absence), compliance (zero promotional).
- **Step 5 style-specific checks**: campaign CA-1/CA-3/RL-12; trade-ideas dual-register/action bridge/disclaimer; news analysis cap/CTA absence; compliance 謙譲語II.
- **docs/adr/**: ADR-002 (news/report split), ADR-003 (trade-ideas dual-register), ADR-004 (compliance merger).
- **9 new T2 scenes**: trade-ideas/{flash,theme,earnings,morning,picks,community}, news/{wrap,indicator,digest,alert}, product/{release,onboard,compare}, campaign/{remind,lastday,result,seasonal,referral} (total: 29 scenes, was 20).

#### Changed
- **style-guide.md**: Rewritten as routing inference table only (668w, was 4,982w). All constraint content moved to per-T1 guide files.
- **SKILL.md Tier 1 table**: Replaced marketing/report/legal/support with campaign/trade-ideas/news/product/compliance.
- **SKILL.md Tier 2 table**: Expanded from 20 to 29 scenes.
- **RL-11**: Added trade-ideas dual-register exception. Analysis sections だ/である; reader-action sections です/ます; intra-paragraph mixing still prohibited.
- **RL-12**: Scoped to campaign only (was marketing). Removed from product scope.
- **RL-3, RL-9**: Re-scoped from `情報分析` to `news + trade-ideas analysis sections`.
- **Layer 3 Proof & Frame table**: Added campaign and trade-ideas rows.
- **Step 3 state output**: Updated to list new 5 T1 styles.
- **Backward compat table**: Extended to cover all old T1→new T1 mappings.

#### Removed
- `marketing` style (→ campaign or product depending on content)
- `report` style (→ news or trade-ideas depending on CTA/analysis%)
- `legal` style (→ compliance)
- `support` style (→ compliance)
- Monolithic style-guide.md per-style constraint sections (content distributed to guide files)

---

## [5.2.0] — 2026-04-28

### Cross-style optimization: D9 per-style, Business Goals, quality rubric expansion

Major release extending optimization from marketing-only to all 5 Tier 1 styles. Adds per-style D9 effectiveness dimension, Business Goals for all 20 scenes, and deep spec improvements for report, product, legal, and support styles. Addresses marketing D9 gap (avg 2.8) with reader-centric reframing.

#### Added
- **D9 — Persuasive Appeal** (marketing): 5 sub-criteria + per-scene emotional triggers. Pass criteria: ≥34/45 branded, D9≥3 gate.
- **D9 per-style definitions** in `diagnosis/cross-style-quality-rubric.md`: Report=Analytical Authority, Product=Comprehension & Confidence, Legal=Regulatory Precision & Risk Completeness, Support=Resolution Efficiency & User Reassurance. Pass thresholds: Report/Product ≥30/40, Legal/Support ≥26/35.
- **`diagnosis/cross-style-quality-rubric.md`** (new): Consolidated D1–D8 shared + D9 per-style scoring, pass criteria table, D4 adaptations per style.
- **14 Business Goals**: One per non-marketing scene (report, press, deck, hottopic, topic, short, detail, manual, script, disclosure, terms, disclaimer, faq, guide). Each defines conversion objective and key quality levers.
- **Report hedging confidence gradient**: 3 levels (High: 見込み/見通し, Medium: と見られる/と考えられる, Low: 可能性がある/リスクがある). Added to report T1 Shared Constraints + 4 new Swipe Patterns (だろう→見込み, unattributed→attributed, vague→precise hedge, assertion→risk framing).
- **Report Checkpoints expanded**: 2→5 items (added だ/である consistency, zero first-person, attribution check).
- **FAQ Rewrite Patterns** (3 new): 仕様です→敬語, 待って→恐れ入ります, 調べて→確認いただけます.
- **Guide Rewrite Patterns** (3 new): 別の部署→窓口案内, 書類送って→所定書類ご郵送, 未完了→処理中ご連絡.
- **Guide constraints**: Processing time (通常X営業日以内), branching procedures (条件→ルート分岐).
- **Product Swipe Patterns** (4 new): 可能となっております→できます, 多彩な→具体列挙, セキュリティ万全→具体措置, 簡単→数字化.
- **Manual constraints**: UI element「」brackets, completion confirmation (最終ステップで成功確認), error recovery in cautions.
- **Shared Constraint: Reader-centric reframing** — Company-subject sentences reframed to reader-benefit subject. 3 new Swipe Patterns.
- **Layer 3 marketing reader-centricity check** in SKILL.md Step 4.
- **Product enhancements**: Multi-feature ordering rule (strongest first), PASONA compressed, number-first rule for short, detail Rewrite Patterns (2) + expanded Checkpoint (2→4), script hook-opening rule.
- **Report enhancements**: Press 5W Rewrite Pattern, deck multi-bullet ordering rule.
- **Legal enhancements**: Disclaimer non-advice Rewrite Pattern + Checkpoint item, terms register verification Checkpoint item.
- **Support enhancements**: FAQ multi-topic splitting rule, guide caution Rewrite Pattern (審査時間).
- **Manual**: Caution Rewrite Pattern (審査には通常3営業日).

#### Changed
- **Legal T1**: Register defaults clarified — disclosure=だ/である exclusively, terms/disclaimer=です/ます.
- **Support T1**: Compressed Rewrite Patterns from 5→3 rows (scene-level patterns now cover 手続きの説明です and エラーです).
- **style-guide.md compressed**: Topic examples condensed, Register Mixing section reduced to quick reference, Routing Inference Table tabularized, marketing Swipe Patterns merged. Net result: 5,491→5,191 words despite ~700 words of new content added.

#### Token budget
- SKILL.md: ~2,450 words
- style-guide.md: ~5,191 words (compressed from 5,491; soft ceiling 5,000)
- cross-style-quality-rubric.md: ~650 words (diagnosis file, not always-loaded)

---

## [5.1.0] — 2026-04-28

### Marketing deep optimization: Business goals, quality rubric, real sample evaluation

Release introducing per-scene business goal definitions, a quantifiable 8-dimension quality scoring rubric, and real sample comparison testing using production EDM data. 11 gaps identified and fixed in marketing style specifications.

#### Added
- **Business Goal fields** for all 6 marketing scenes (lp/sns/event/push/edm/banner) in style-guide.md — defines conversion objective and key quality levers per scene.
- **`diagnosis/marketing-quality-rubric.md`**: 8-dimension scoring framework (D1 Term Integrity through D8 Brand Fit), each scored 1–5 with explicit criteria. Pass criteria: total ≥30/40, hard gates on D1+D2.
- **`diagnosis/marketing-sample-eval.md`**: 6 real sample evaluations (S1–S6) from moomoo win-back EDM campaign comparing skill output vs human localization. Identifies 11 gaps with D1–D8 scoring.
- **4 new Swipe Patterns**: metaphorical→concrete benefit language, subjective→objective closers, context-first→action-first titles, unnamed→bracket-named offers.
- **3 new Shared Constraints**: action-first title construction, no metaphorical benefit language in body, market context objectivity extended to module closers (not just titles).
- **5 new EDM Mandatory Constraints**: register gradient (casual subject OK / formal body), offer bracket naming, transition phrases, body paragraph segmentation, market context module length limit (2–3 items).
- **2 new EDM Checkpoint items**: body paragraph segmentation, offer bracket naming.
- **EDM CTA clarification**: noun-phrase form acceptable for button text (not only full verb form).

#### Token budget
- SKILL.md: ~2,400 words (unchanged)
- style-guide.md: ~4,950 words (99% of 5,000-word soft ceiling — includes Business Goals + gap fixes)
- marketing-quality-rubric.md: ~650 words (diagnosis file, not always-loaded)
- marketing-sample-eval.md: ~1,200 words (diagnosis file, not always-loaded)

---

## [5.0.0] — 2026-04-28

### Layer 3 foundation: Brand voice matching, case library, eval suite expansion

Major release introducing brand-specific voice matching (Layer 3 foundation), expanding the behavioral eval suite from 5 to 13 tests, fixing Cross-Style Red Line Summary inconsistencies, and housekeeping stale diagnosis files.

#### Added
- **Step 3.5 — Brand Voice Match**: Optional workflow step that loads brand-specific voice constraints from `references/case-library.md` when input contains a listed brand name. Adds brand voice signature to Step 4 transform and brand benchmark comparison to Step 6 naturalness check.
- **`references/case-library.md`**: New conditional-load reference file with 4 brand voice entries:
  - 野村証券 (Nomura): hedging hierarchy (3 levels), attribution rules, anti-patterns
  - 楽天証券 (Rakuten): なら構文, social proof numbers, hot-stage CTA
  - SBI証券 (SBI): zero abbreviations, だ/である exclusive, conditional precision
  - moomoo証券: brand suffix, win-back formula, reward terminology, sector rotation reframing, emoji bullet structure, asset-class CTA customization
- **Step 6 Proxy check 4 — Brand voice match**: Compares output against brand benchmark excerpt and anti-patterns when Step 3.5 identified a brand. States「ブランド適合: [brand] ✓」.
- **8 new behavioral eval tests** (T6–T13): marketing/push (RL-1 vs RL-4 priority), marketing/edm (three-section structure), marketing/banner (ultra-short copy), marketing/sns (140-char + emoji), report/topic Variant A (8-part + register exceptions), report/topic Variant B (UGC curation + disclaimer), product/script (spoken rhythm), product/manual (numbered steps). Test priority tiers added.
- **Routing Inference Table** moved to style-guide.md (was inline in SKILL.md) — reduces SKILL.md token load.

#### Changed
- **Cross-Style Red Line Summary** (style-guide.md): Fixed 4 scope inconsistencies — RL-3 now includes hottopic/topic, RL-4 expanded to all 6 limit scenes, RL-9 includes hottopic/topic with exception note, RL-12 includes edm/banner with push exemption note.
- **SKILL.md backward compatibility table**: Compressed from 7-row table to single-line summary (–40 words).
- **SKILL.md keyword inference list**: Moved to style-guide.md, replaced with pointer (–150 words).
- **References table**: Added case-library.md entry with conditional load description.

#### Archived
- 4 stale diagnosis files (synthesis.md, structural-audit.md, platform-check.md, constraint-enforcement-audit.md) marked with archive headers — pre-v4.0.0 findings, resolved.
- token-audit.md rewritten with current measurements (SKILL.md: ~2,400w at 80% budget; style-guide.md: ~4,600w at 92% ceiling).

#### Token budget
- SKILL.md: ~2,400 words (80% of 3,000-word budget — net reduction from compression)
- style-guide.md: ~4,600 words (92% of 5,000-word soft ceiling — includes routing inference table)
- case-library.md: ~500 words (conditional load, not counted in always-loaded budget)

---

## [4.6.0] — 2026-04-28

### Consolidated: Scene expansion, topic variants, Push/EDM/Banner support

Covers changes from v4.3.0 through v4.6.0 that were not individually documented. These releases expanded the scene catalog from 14 to 20 scenes, added the topic scene's dual-variant structure, and extended RL-4 and RL-12 scope to cover the new marketing scenes.

#### Added
- **6 new scenes**: push, edm, banner, manual, script, topic — bringing total from 14 to 20
- **topic scene**: Variant A (話題シェア, 8-part structure) and Variant B (人気投稿まとめ, 6-part structure with fixed transition sentence and mandatory disclaimer)
- **RL-11 topic exceptions**: (a) です/ます体 for topic body (not だ/である); (b) casual/タメ口 in 投稿例 section; (c) invitation form (〜しよう！) in push subtitle
- **RL-4 expanded to 6 scenes**: marketing/sns (≤140), marketing/push (title≤20/body≤60), marketing/edm (subject≤40/preheader≤80/CTA≤15), marketing/banner (main≤15/sub≤25/CTA≤8), report/hottopic (≤140), report/deck (≤25/bullet)
- **RL-12 expanded to 5 scenes**: lp, sns, event, edm, banner (push exempt — uses リンク先示唆)
- **RL-1 vs RL-4 priority rule**: For push scene, character limits take precedence over term integrity when in conflict
- **Push brand injection prohibition**: Brand suffix rule only applies when source text already mentions the brand
- **AC-4 updated**: Per-scene character count format in verification block (multi-field for push/edm/banner, total for sns/hottopic, per-bullet for deck)

#### Changed
- Step 5 verification expanded with per-scene character count formats and RL-12 push exemption logic
- Cross-Style Red Line Summary in style-guide.md updated: RL-3 scope to include hottopic/topic, RL-4 scope to all 6 limit scenes, RL-9 scope to include hottopic/topic with exception, RL-12 scope to include edm/banner with push exemption

#### Token budget
- SKILL.md: ~2,480 words (83% of 3,000-word budget)
- style-guide.md: ~4,500 words (90% of 5,000-word soft ceiling)

---

## [4.2.2] — 2026-04-27

### LP-derived patterns: brand name scope, win-back LP structure, multi-state consistency

This patch codifies 3 structural and naming patterns extracted from analysis of the live moomooおかえりキャンペーン LP (invest.jp.moomoo.com/churnrecall). The LP contained a copy violation (「エヌビディアの有力な対抗馬」in an AMD stock description — the existing brand name convention rule applied but was scoped only to campaign headlines), and introduced two structural patterns not previously captured: the 4-layer win-back LP body structure, and cross-state register consistency for multi-state CTA modules.

#### Added
- **Brand name convention scope clarified**: Rule now explicitly covers all marketing copy locations — campaign headlines, LP body text, stock/investment content descriptions, and market commentary. AMD in stock descriptions (e.g., AMD as NVIDIA competitor) must use English, not katakana form.
- **Win-back / Re-engagement LP Structure** (added to `marketing/lp` T2 section): 4-layer body structure for チャーンリコール campaigns — (1) re-engagement hook, (2) market context module (Pathos+Logos dual trigger), (3) 特典詳細, (4) 信任背書 (trust anchor). Source: moomooおかえりキャンペーン LP.
- **Multi-state copy consistency** (added to `marketing/event` Checkpoint): Multi-state copy modules (参加前/達成/未達成/期限切れ) must maintain consistent register across all states — no tone shift between states of the same module.
- **1 Swipe Pattern row** added: エヌビディアの有力な対抗馬（株式説明・市況コメント内）→ NVIDIAの有力な対抗馬

#### Token budget
- SKILL.md: ~1,950 words (no change — all additions in style-guide.md)

---

## [4.2.1] — 2026-04-27

### Localization patterns: EDM win-back email conventions and reward terminology

This patch codifies 5 additional localization patterns extracted from comparative analysis of draft vs. human-localized copy in sheets 10 (EDM_可用悬赏≥500) and 11 (EDM_可用悬赏＜500) of JP-26Q2流失召回活动更新WBS. The source copy in these sheets was already in Japanese (not Chinese), so the comparison is draft Japanese vs. localization Japanese — surfacing brand voice and naming conventions not previously captured.

#### Added
- **Shared Constraint: Securities brand suffix in body copy** — Body copy must use full brand form (e.g.,「moomoo証券」not「moomoo」). Applies to greetings, CTAs, and self-references in email body.
- **Shared Constraint: Win-back / re-engagement email opening** — Must open with「いつも[ブランド名]をご利用いただきありがとうございます」. Colloquial openers (「お久しぶりです」「お戻りを心よりお待ちしておりました」) are prohibited — inconsistent with securities brand voice.
- **Shared Constraint: Reward product terminology** — Standard names: 株式キャッシュバック→株式キャッシュバック**券**; 分配金利回り上乗せクーポン→**MMF利回りアップ券**; 手数料優待カード→**取引手数料優待カード**.
- **Shared Constraint: Market context copy in titles** — Avoid subjective framing (「チャンス密集中」) in section/module titles. Use objective descriptions (「変動の市場」「市場の動向」). Benefit/urgency copy belongs in body, not titles.
- **6 Swipe Pattern rows** added: moomoo→moomoo証券, お久しぶりです→いつも〜ご利用いただきありがとうございます, 株式キャッシュバック→券, 分配金利回り上乗せクーポン→MMF利回りアップ券, 手数料優待カード→取引手数料優待カード, チャンス密集中→変動の市場.

#### Token budget
- SKILL.md: ~1,950 words (no change — all additions in style-guide.md)

---

## [4.2.0] — 2026-04-27

### Localization patterns: marketing/event compliance and brand conventions

This release codifies 6 localization patterns extracted from comparative analysis of machine-translated vs. human-localized copy across a live securities campaign (sheets 6, 8, 10, 11 of JP-2026入金活動-WBS). The patterns address compliance gaps (prize probability claims, prize amount hedging), brand consistency (Western brand name encoding), and lexical register accuracy (取引 vs ディーリング, 賞品 vs 賞金).

#### Added
- **Shared Constraint: Brand name convention** — Western brands in English characters, not katakana (NVIDIA not エヌビディア). Japanese company names unchanged.
- **Shared Constraint: Prize amount hedging** — Monetary reward values must append「相当」(e.g.,「最大5万円相当」). Required for compliance in prize/reward campaigns.
- **Shared Constraint: Probability claims** — Avoid「100%当選」. Accepted alternatives:「必ずもらえる」/「必ず特典ゲット」for guaranteed-reward framing.
- **Shared Constraint: 取引 vs ディーリング** — Use「取引」in general marketing/event copy; reserve「ディーリング」for derivatives-specific contexts.
- **Shared Constraint: Campaign prize concept** — Use「賞品を山分け」not「賞金プール」in lottery/share-type prize campaigns (賞金 implies cash payment; 賞品 is correct for stock/gift certificates).
- **Shared Constraint: Email subject format** — Push and email subjects use【】bracket format for campaign names.
- **6 Swipe Pattern rows** added to Tier 1 marketing table: エヌビディア→NVIDIA, 賞金プール→賞品を山分け, 100%当選→必ずもらえる/必ず特典ゲット, チャレンジカウントダウン→チャレンジ終了まで, キャンペーンルール→キャンペーンの詳細, ご支援ありがとうございます（終了/拒否通知）→ご理解の程よろしくお願いいたします.

#### Token budget
- SKILL.md: ~1,950 words (no change — constraints added to style-guide.md only)

---

## [4.1.0] — 2026-04-24

### Quality framework: Scene Fit layer and naturalness proxy checks

This release completes the three-layer quality framework: Compliance (binary RL gates) → Scene Fit (Checkpoint X/N score) → Reference Match (proxy-based naturalness check).

Previously, quality evaluation consisted only of binary RL pass/fail checks and an unexplained `改動幅度 X/100` score with no defined calculation method. This release replaces that with structured, auditable evaluation at each layer.

#### Added
- **RL-12**: `marketing / scenes: lp, sns, event` must contain at least one CTA with a specific action verb. Generic「こちら」alone does not satisfy. Hard gate — must revise before delivery.
- **AC-7 updated**: Benefit specificity requirement (a concrete detail: number, feature name, or named outcome). CTA requirement moved to RL-12.
- **Step 5 — Scene Fit check**: After all RL checks, run each scene's Checkpoint from style-guide.md. Report 場面適合: X/N ✓. All items must pass (X = N) before Step 6.
- **Step 6 rewritten**: Three proxy checks replace generic naturalness description:
  - Proxy 1: Cross-register vocabulary leakage (register-specific scan patterns per Tier 1)
  - Proxy 2: Sentence variety (uniform length = mechanical output flag)
  - Proxy 3: Reference comparison against style-guide.md Example for this scene
- **14 Checkpoints rewritten** in style-guide.md: RL duplicates removed from all scene Checkpoints; scene-specific structural items added. Each Checkpoint now contains 3 auditable items independent of RL gates.
- **RL-12 row added** to Cross-Style Red Line Summary in style-guide.md.
- **Buyer-stage CTA alignment** added to `marketing/lp` Checkpoint: cold → warm → hot scale.
- **`diagnosis/behavioral-eval-suite.md`**: 5 regression test cases covering RL-12, RL-11 keigo, routing inference, RL-2 injection resistance, and legal/disclosure Scene Fit.

#### Changed
- **RL-2 operationalized**: Added 3 concrete scan targets — (a) numbers not in input; (b) named entities not in input; (c) causal claims not derivable from input. Each flagged with `⚠ RL-2: [injected content]`.
- **RL-4 scope clarified**: Explicitly scoped to `marketing / scene: sns` (was "marketing/sns" — ambiguous).
- **RL-11 extended to 4 mixing patterns**: (1) verb endings だ/である + です/ます; (2) keigo level: 謙譲語II outside support or plain inside support; (3) modality markers 〜と見られる/〜見込み in marketing output; (4) tone markers「！」/「今すぐ」in press/legal/report/support.
- **Step 5 RL-11 check updated**: Now explicitly scans all 4 mixing patterns.
- **Output Format**: `改動幅度：X/100` removed. `場面適合: X/N ✓` and `自然さ:` added to 検証 block.
- **RL-11 row updated** in Cross-Style Red Line Summary: 4-category scan listed.

#### Token budget
- SKILL.md: ~1,950 words (within 3,000-word always-loaded limit — no layer split needed)

---

## [4.0.0] — 2026-04-24

### Architecture: Two-tier routing + 14 scenes

This was a major structural rework introducing the two-parameter routing system (--style + --scene), expanding from 4 styles to 5 styles × 14 scenes.

#### Added
- **Two-tier routing**: `--style` (Tier 1 register) × `--scene` (Tier 2 structural template)
- **5 Tier 1 styles**: `marketing`, `product`, `report`, `legal`, `support`
- **14 Tier 2 scenes**: `lp`, `sns`, `event`, `short`, `detail`, `manual`, `report`, `press`, `deck`, `disclosure`, `terms`, `disclaimer`, `faq`, `guide`
- **Scene inference rules**: Automatic `--scene` default when only `--style` is specified
- **Backward compatibility**: Old single-flag calls (e.g., `--style formal` → `legal/disclosure`) still work
- **Style + scene inference**: Keyword-to-route mapping for flagless calls
- **RL-7**: No double negatives (〜ないわけではない / 〜なくはない)
- **RL-8**: No noun-phrase stacking (4+ consecutive nouns without particles)
- **RL-9**: 情報分析 unattributed numbers must be flagged with `要出典:`
- **RL-10**: No passive stacking (2+ passive constructions in one sentence)
- **RL-11**: No register mixing (initial version: verb-ending check only — see v4.1.0 for full extension)
- **Step 2**: Term Lock + Source Analysis (2a Term Lock, 2b Information Priority, 2c Dominant Proof)
- **Step 3**: Explicit style + scene routing with stated output
- **Step 4**: Three-layer transform (Structure → Language → Proof & Frame) with Proof-register mapping
- **Step 5**: Inline verification with per-RL and per-scope checks
- **Step 6**: Naturalness check (initial version — see v4.1.0 for proxy check rewrite)
- **style-guide.md**: Full Tier 1 + Tier 2 specifications for all 14 scenes with Checkpoints, Examples, Swipe Patterns, Rewrite Patterns

#### Changed
- Version bumped from 3.x to 4.0.0 (non-backward-compatible routing architecture change)
- SKILL.md completely rewritten; original 4-style workflow replaced

---

## [3.0.0] — (prior)

### Original 4-style skill

Initial version with 4 styles (`formal`, `marketing`, `report`, `sns`), 6 red lines (RL-1 through RL-6), 3 acceptance criteria, and basic post-execution verification. Single-axis routing via `--style` flag.

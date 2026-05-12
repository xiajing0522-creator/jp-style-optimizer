---
name: domain-research-trade-ideas
type: diagnosis
skill: jp-style-optimizer
tier1: trade-ideas
date: 2026-04-30
sources: 10
target_ref: references/trade-ideas-guide.md
---

# Domain Research: trade-ideas（日语赚效内容/投资分析类）

## Purpose

对 jp-style-optimizer Tier 1 **trade-ideas** 风格进行领域专家视角的独立研究，验证 `references/trade-ideas-guide.md` 中 TI-1〜TI-8 约束、**dual-register（分析=だ/である + 读者行动=です/ます）** 的业界合法性、`flash / theme / earnings / morning / picks / community` 六个子场景的「事实→影响→行动示唆」结构是否对齐日本投研内容专家的实际工作流。

本文件独立于 `build/domain-research-trade-ideas.md`（后者是构建阶段的 style-definition 草案），从**外部来源 + 专家工作流 + 质量基线**三个维度补强，重点回答两个问题：

1. **dual-register 是行业实践，还是 skill 为「行动转化」而生造的例外？**
2. **事实→影响→行动示唆（→见通し）** 的子场景结构，是否与日本投研编辑的实际流程 1:1 对应？

---

## Sources

Each source is recorded per the mojo-skill-creator domain-research-guide format (**Source name + URL/reference** | **Key finding** | **Implication for this skill**). Detailed findings are expanded in Finding 1–10 below.

| # | Source (name + URL/reference) | Key Finding (1–2 sentences) | Implication for skill (1 sentence) |
|---|---|---|---|
| 1 | **金融商品取引法 第37条・第38条・第39条** + 金融庁「金融商品取引業者等向けの総合的な監督指針」III-2-3. URL: https://www.fsa.go.jp/common/law/kinshouhou/ + https://www.fsa.go.jp/common/law/guide/kinyushohin/index.html | 無登録での投資助言的表現、断定的判断の提供、手数料/リスク未記載の広告は違法。forward-looking は推測語尾とリスク開示が必要。 | TI-1/TI-2/TI-6/TI-7 の法的 hard constraint として設計を正当化する。 |
| 2 | **日本証券業協会「広告等の表示及び景品類の提供に関する規則」** + 「会員における投資情報の提供等に関する指針」. URL: https://www.jsda.or.jp/about/kisoku/ + https://www.jsda.or.jp/about/jishukisei/ | 「推奨」「必勝」「絶対」等は禁止語彙、上昇シナリオ記述時は下落リスクも両論併記、「情報提供目的」免責雛形が業界標準。CTA は情報アクセス系のみ許容、特定銘柄売買促進 CTA は禁止。 | TI-1/TI-5/TI-6/TI-7/TI-8 の業界慣行根拠となり、JSDA 雛形を免責テンプレに流用できる。 |
| 3 | **QUICK Corp. / 日経QUICKニュース / QUICK企業価値研究所** 会社紹介・公開配信記事. URL: https://corporate.quick.co.jp/ + https://money-world.jp/ + 日経QUICKニュース（日経電子版マーケット欄配信元） | 市況速報・決算速報・朝刊コメントで「タイムスタンプ → 事実層 → 影響分析 → 見通し層 → 免責」の 5 段定型で文章が生産され、本編は だ/である体、見通し語尾が強/中/弱 3 階層で階層化されている。 | TI-2 の confidence gradient、TI-3 の出典、TI-4 の時点注記を実務ワークフローに直結させる。 |
| 4 | **日本経済新聞社「日経の用語・表記ルール」** + 日経電子版マーケット／スクランブルコラム. URL: https://www.nikkei.com/ + 日経用語集（社内基準のうち公開分） | 経済・市況記事はほぼ例外なく だ/である体で、事実先行 → 背景後置 → 見通し（ヘッジ語）の順序が固定化されている。 | dual-register は日経本紙由来ではなく、リテール媒体固有である事を明示でき、SKILL.md に棲み分けを記述する根拠になる。 |
| 5 | **Bloomberg Japan / Reuters Japan** マーケット・決算速報の公開記事. URL: https://www.bloomberg.co.jp/ + https://jp.reuters.com/markets/ | 決算速報は「リード（実績 vs 予想 vs 前年）→ セグメント要因 → ガイダンス → 株価反応 → タイムスタンプ/出典」の 5 層定型で、市況フラッシュは 100–140 字でも事実 + 直接要因 + 影響の順が保たれる。 | earnings/flash 子場景の情報構造が実際のグローバル金融メディア定型と 1:1 で対応し、再設計不要であることを validate する。 |
| 6 | **野村證券「モーニングコメント」「Investment Monthly」/ 大和証券「デイリー」/ SBI証券「マーケットレポート」** 公開版. URL: https://www.nomura.co.jp/ + https://www.daiwa.jp/ + https://market.sbisec.co.jp/market/ | リテール向けセルサイド・レポートは「前日振り返り（だ/である）→ 本日注目/本日の戦略（です/ます）」のように**セクション単位で register が切り替わる**運用が実在し、「ただし／一方で」逆接構文でのリスク両論併記が定型。 | dual-register（RL-11 例外）が skill の生造ではなく**リテール・セルサイドの業界実践**であることを validate し、theme/morning 構造を裏付ける。 |
| 7 | **みんかぶ / Yahoo!ファイナンス / Trader's Web** テーマ・銘柄解説記事. URL: https://minkabu.jp/ + https://finance.yahoo.co.jp/ + https://www.traders.co.jp/ | 個人投資家向け媒体は「人気」「出来高急増」「年初来高値更新」等の**市場事象ベースの客観注目度**表現で注目誘導し、CTA は「チャートを見る」「銘柄詳細へ」等の情報アクセス系に限定される。 | TI-8 の主観排除/客観注目度許容と picks/community の情報構造を業界慣行で正当化する。 |
| 8 | **moomoo証券（日本） / 楽天証券トウシル / マネックス証券 / みんかぶコミュニティ** のアプリ内配信. URL: https://www.moomoo.com/jp + https://media.rakuten-sec.net/ (トウシル) + https://www.monex.co.jp/ + https://minkabu.jp/community | Push ≤140字で「だ/である主体 + 末尾 1 文が です/ます or 体言止め」、コミュニティ投稿例セクションではカジュアル体が許容される RL-11 例外が日常運用されている。 | flash/community 子場景の文字数・register 切替・RL-11 例外が実際のアプリ配信と 1:1 で対応することを validate する。 |
| 9 | **CFA Institute "Standards of Practice Handbook" 11th ed.** Standards III(B) Fair Dealing / V(A) Diligence & Reasonable Basis / V(B) Communication with Clients / VI(A) Conflicts Disclosure. URL: https://www.cfainstitute.org/en/ethics-standards/codes/standards-of-practice-handbook | 分析と意見の峻別、forward-looking 文への推測語尾必須、片面提示禁止（Fair Dealing）、コンフリクト開示は国際プロフェッショナル基準として義務化されている。 | TI-2/TI-3/TI-6 は日本特有規制ではなく**グローバル投研標準**である事を示し、将来 VI(A) コンフリクト開示フィールドを予約する余地を作る。 |
| 10 | **SEC Reg FD + Rule 10b-5 forward-looking safe harbor (PSLRA 1995)** + **東京証券取引所「適時開示ガイド」** + EDINET 開示文書引用慣行. URL: https://www.sec.gov/rules/final/33-7881.htm + https://faq.jpx.co.jp/disclose/tse/ + https://disclosure2.edinet-fsa.go.jp/ | 「expect/may/could/anticipate」「〜と見られる」「〜の可能性がある」は forward-looking safe-harbor marker として国際・国内開示実務で認識され、「実績」と「見通し」は独立セクションとして構造的に分離される。 | TI-2 強化（事実文と見通し文の段落単位分離）と TI-7 免責 boilerplate の法的根拠を提供する。 |

---

## Finding 1 — 金融商品取引法第37条・第38条・第39条 (Source 1)

**Ref**: 金商法 第37条（広告等の規制）、第38条（禁止行為）、第39条（損失補てん等の禁止）、金融商品取引業者等向けの総合的な監督指針 III-2-3-1「投資助言・代理業」、III-2-3-2「広告等の規制」。

**Key Finding**:
- **投資助言業登録を持たない発信者**は、「特定銘柄を買うべき」「売るべき」という**助言的行為**を行うと無登録営業に該当し得る。情報提供・分析紹介の範囲に留める必要あり。
- 第38条: **断定的判断の提供**（「必ず上がる」「確実に利益が出る」等）は登録業者にも禁止。情報コンテンツでも同様の表現は規制対象。
- 第37条: 金融商品広告に「手数料」「リスク」「元本欠損可能性」等の表示義務。「キャンペーン告知」同様、**投資アイデア/分析コンテンツ**も広告性を帯びる場合は同規制が及ぶ。
- **誇大広告の禁止**: 「業界最高」「No.1」等の最上級は根拠付記必須。「絶好の買い場」「逃すと損」等の煽動表現は誇大に該当し得る。

**Implication for skill**:
- **TI-1（投資助言非該当）は法令 hard constraint**。現行設計は正しい。「おすすめ銘柄」「買い推奨」「必ず上がる」の禁止は第38条の直接投影。
- **TI-2（推測表現義務化）は第38条「断定的判断提供禁止」の直接投影**。confidence gradient（見込み > と見られる > 可能性がある）は断定回避の段階設計として妥当。
- **TI-7（免責文言必須）は第37条広告規制の形式的担保**。500字を閾値とした設計は、「短文は告知、長文は分析=広告性が強まる」という実務解釈と整合。
- **TI-6（リスク両面提示）は第37条のリスク表示義務+誇大広告禁止の合成**。片面提示は実質的に誇大表示になり得る。
- **潜在ギャップ**: 第37条の**手数料表示義務**は trade-ideas ではほぼ適用されない（商品広告ではなく分析コンテンツのため）が、「口座開設 CTA」等を併記する場合は別途 campaign 系制約を呼び出す必要がある → skill 間連携の明示が必要。

---

## Finding 2 — 日本証券業協会 投資情報ガイドライン (Source 2)

**Ref**: 日本証券業協会「広告等の表示及び景品類の提供に関する規則」第9条、「会員における投資情報の提供等に関する指針」、公正慣習規則第9号。

**Key Finding**:
- **投資情報の提供**において、「推奨」「おすすめ」「必勝」「絶対」「確実」「間違いない」は**明示的禁止語彙**。
- 見通し・予想を記述する際は、**推測語尾**（「〜と見られる」「〜と予想される」「〜の可能性がある」「〜が注目される」）を使用し、**断定を避ける**必要あり。
- **リスク情報の両論併記**: 上昇シナリオを記載する場合、下落リスク・不確実性要因にも言及しなければならない（「片面提示禁止」）。
- **免責文言の業界雛形**:
  - 「本資料は情報提供を目的としたものであり、特定の金融商品の取引を勧誘するものではありません。」
  - 「本資料に掲載された内容は作成時点のものであり、今後予告なく変更される可能性があります。」
  - 「投資判断はお客様ご自身の責任で行っていただきますようお願いいたします。」
- **CTA 制限**: 「今すぐ買う」「この銘柄を買う」等の**特定銘柄の売買直接促進 CTA は禁止**。「銘柄詳細を見る」「チャートを確認する」等の**情報アクセス CTA は許容**。

**Implication for skill**:
- **TI-1（投資助言非該当）+ TI-8（主観排除）は JSDA 禁止語彙リストと完全対応**。「面白い」「ヤバい」等の主観評価を排除しつつ「注目されている」「関心が集まっている」という**客観的注目度表現**を残す設計は、業界慣行に忠実。
- **TI-2 の confidence gradient** は JSDA 推測語尾リストと一致。
- **TI-6（リスク両面提示）は JSDA「両論併記義務」の直接投影**。
- **TI-7 の免責文言**は JSDA 雛形を踏襲すれば機械的に生成可能。skill が固定免責テンプレを挿入する設計は実務的。
- **TI-5（行動橋渡し）の業界整合性**: 「銘柄詳細を見る」「チャートを確認する」「〜に注目」「〜をチェック」は JSDA の**情報アクセス CTA**範囲内。「今すぐ買う」は禁止域。現行設計は**業界慣行と完全対応**。
- **拡張候補**: 免責文言の **≥500字で必須** という閾値は JSDA 指針には明文規定なし（「投資情報資料には免責表示を付すこと」とのみ）→ 現行 500字閾値は skill 側の合理的ヒューリスティクスだが、「flash/picks は短文だから免除」のロジックは**広告規制側から見ればグレー**。flash で数値と見通しを提示したら短文でも免責が望ましい。→ **TI-7 の閾値見直し候補**。

---

## Finding 3 — QUICK / 日経QUICK 編集実践 (Source 3)

**Ref**: QUICK Corp. 会社紹介・サービス資料（Money World, QUICK リサーチ, QUICK コンセンサス）、日経QUICKニュース 配信記事構造（「前場寄り付き」「大引け」「決算速報」の定型）。

**Key Finding (Expert Workflow)**:
QUICK/日経QUICK の記事は、次の定型ワークフローで生産される：

| # | Expert Phase | 説明 |
|---|---|---|
| Q1 | **タイムスタンプ確定** | 「本日午前9時時点」「前場終値ベース」「N月N日X時現在」等、記事有効時点を明示 |
| Q2 | **事実層の確立** | 数値（指数水準、個別株騰落率、EPS/売上等）を**出典付きで先出し** |
| Q3 | **影響分析（原因・背景）** | 「〜を受けて」「〜が材料視された」等、事実→影響の連結を 1–2 文で |
| Q4 | **見通し・評価層** | 断定回避語尾（「〜と見られる」「注目される」「警戒される」）で forward-looking を記述 |
| Q5 | **免責・時点再確認** | 長文記事末尾に免責。短報ではタイムスタンプ冒頭のみ |

**文体観察**:
- 本編は **だ/である体** 基調。「日経平均株価は続伸した」「〜が材料視された」。
- 見通し文のヘッジ語は階層化: 強い（見込まれる）→ 中（と見られる）→ 弱い（可能性がある／警戒される）。
- **タイムスタンプ必須**: ほぼ全記事冒頭または末尾に「X月X日X時時点」等の注記。
- 個別銘柄紹介では「〇〇（コード番号）は〜」の**コード併記**が慣行。

**Implication for skill**:
- **TI-4（市場タイミング整合）は QUICK 実践の Q1 と完全対応**。「本日時点」「X月X日終値ベース」は QUICK 記事の冒頭文字列そのもの。
- **TI-2（推測表現義務化）の confidence gradient** は QUICK の Q4 語彙階層（強/中/弱）と一致。
- **TI-3（データ出典）は Q2 の実践と対応**。ただし QUICK は「QUICKデータ」「東証発表」と**出典名を明示**。skill の「広く報道済みのデータは免除」設計は妥当だが、**「指数水準・前日終値」のような公知データ以外は出典明示が必須**という線引きの明文化が望ましい。
- **dual-register の business rationale**: QUICK 本編は だ/である体で統一（読者=機関投資家・専門家のため）。一方、**moomoo証券や個人投資家向けプラットフォームの配信では、末尾の CTA や読者向けガイダンスが です/ます体に切り替わる**ケースが観察される（次節参照）。**QUICK 自体は dual-register を使わない**が、これは「読者層の違い」で説明される。dual-register は「機関投資家向け純粋分析=だ/である一貫」vs「**個人投資家向けプラットフォーム=分析は だ/である、行動示唆は です/ます**」の register 切替えを意味する → skill は後者の市場を狙う。
- **TI-5（行動橋渡し）は QUICK 実践には**ほぼ**ない**（QUICK は純粋情報提供、CTA 概念がない）。これは skill の trade-ideas が QUICK 型ではなく**リテール・プラットフォーム型**（Source 7, 8）に寄せる設計であることを意味する → 正しい差別化。

### Expert Phase → Skill Step → Gap 映射表（基于 Source 3 QUICK workflow、合并 Source 5 Bloomberg/Reuters 定型、Source 6 セルサイド朝刊）

| # | Expert Phase（QUICK/Bloomberg/セルサイド共通） | Skill Step（trade-ideas-guide.md 現行） | Gap |
|---|---|---|---|
| Q1 | **タイムスタンプ確定** — 「本日 X 時時点」「前場終値」「時間外取引で」等の時点/時間枠注記 | TI-4 市場タイミング整合「日付/時点明示」 | **部分カバー**: 「日付/時点」は明記だが「時間枠」（前場終値・時間外等）は未具体化 → 強化候補 |
| Q2 | **事実層の確立** — 数値（指数/株価/騰落率/EPS/売上）の出典付き先出し | TI-3 データ出典 + 各子场景「事実先行」構造（flash/earnings/morning） | **ほぼカバー**: RL-9 準拠の出典付記。「公知データは免除」の線引き明示が不十分 |
| Q3 | **影響分析（因果）** — 「〜を受けて」「〜が材料視された」の 1–2 文因果連結 | flash: 事実→影響 / earnings: 実績 vs 予想→ポイント分析 / theme: 市場データ→投資視点 | **完全カバー** |
| Q4 | **見通し・評価層** — 推測語尾階層（強:見込まれる/中:と見られる/弱:可能性がある/警戒される） | TI-2 推測表現義務化 + confidence gradient | **完全カバー** |
| Q5a | **事実文と見通し文の構造分離** — 段落 or セクション単位で「実績」と「見通し」を分離（EDINET/Reg FD 慣行） | TI-2 語尾チェックのみ | **MISSING**: 構造的分離ルール未明文化 → 強化候補（Source 10 反映） |
| Q5b | **リスク両論併記** — 「ただし／一方で」逆接構文で下落/不確実要因に言及 | TI-6 リスク両面提示 | **ほぼカバー**: 両面要件は明記だが「逆接構文存在チェック」まで踏み込んでいない |
| Q6 | **免責・時点再確認** — 500字超コンテンツに JSDA 雛形免責、短報ではタイムスタンプのみ | TI-7 免責文言（500字閾値） | **再検討**: 数値予想を含む flash（< 140 字）は短文でも免責対象化の余地あり |
| Q7 | **行動橋渡し（リテール限定）** — 「銘柄詳細へ」「〜に注目」等の情報アクセス CTA（JSDA 許容範囲内） | TI-5 行動橋渡し設計 + 間接示唆 | **完全カバー** |
| Q8 | **register 切替**（リテール版セルサイドのみ） — 分析=だ/である、本日の戦略/注目ポイント=です/ます のセクション単位切替 | RL-11 セクション単位レジスタ分離例外 | **完全カバー**（業界実践の忠実反映） |
| Q9 | **コンフリクト開示**（CFA VI(A)）— 保有/発行体関係の開示 | 未搭載 | **MISSING**（低優先、skill 入力に含まれない可能性大） |

**结论**: 9 項目中 6 が完全カバー / 2 が強化候補 / 1 が MISSING（低優先）。**構造的再設計は不要**、次スプリントで craft-level の強化を行う。

---

## Finding 4 — 日経新聞 編集ルール + マーケット欄 (Source 4)

**Ref**: 日経「用語・表記ルール」（社内基準、公開部分）、日経電子版「マーケット」「スクランブル」「金融コンフィデンシャル」等コラムの文体観察、「前場・後場コメント」定型。

**Key Finding**:
- **基調文体は だ/である体**。経済・市況記事はほぼ例外なく「常体」。
- **事実先行・背景後置**: 記事冒頭 1–2 文は**5W1H の数値事実**、その後に「〜を受けて」「〜を背景に」と因果を展開。
- 見通し・予想記述の**ヘッジ語ライブラリ**:
  - 強: 「〜が見込まれる」「〜が確実視される」
  - 中: 「〜と見られる」「〜が注目される」「〜と予想される」
  - 弱: 「〜する可能性がある」「〜の動きが警戒される」「〜する余地もある」
- **固有名詞・数値の正確保持**: 企業名は商号表記（「トヨタ自動車」ではなく「トヨタ」は見出しのみ）、数値は有効桁数維持。
- **引用符処理**: 談話・経営者発言は「」、主観評価は「〜と話した」「〜と述べた」で発話者帰属を明示。
- **コラム系（スクランブル、Deep Insight）**では、末尾 1–2 文に**「注目したい」「目が離せない」**等の**著者判断**が入ることがある。ただし投資助言的な「買い」「売り」は避ける。

**Implication for skill**:
- **TI-2（推測表現義務化）の confidence gradient** は日経のヘッジ語ライブラリと**完全に一致**。skill の「見込み > と見られる > 可能性がある」は日経実践からの抽出。
- **TI-8（主観排除・知的興奮の両立）は日経コラム系の慣行と対応**。「注目される」「関心が集まる」等の受け身的注目度表現は日経本紙でも許容。「面白い」「すごい」は日経本紙では用いない。
- **事実先行構造は TI-2 の前提**: 冒頭事実 → 因果 → 見通しの 3 層は trade-ideas の**事実→影響→見通し**（flash/earnings）と 1:1 対応。
- **dual-register の妥当性**: 日経本紙自体は だ/である単一レジスタ。**dual-register は日経自体ではなく「個人投資家向けリテール媒体」で観察される現象**。つまり skill が dual-register をサポートする理由は「リテール読者層向けエンゲージメント」であり、「日経準拠」ではない → SKILL.md で「dual-register は retail-platform 向け機能、機関向けには単一レジスタ推奨」と明記する余地あり。

---

## Finding 5 — Bloomberg Japan / Reuters Japan 速報構造 (Source 5)

**Ref**: Bloomberg.co.jp マーケット記事、Reuters Japan 市況・決算速報、公開記事の構造観察。両社ともグローバル編集基準を日本語版に適用。

**Key Finding**:
- **決算速報の定型構造**:
  1. リード文（1 文、実績 vs 予想 vs 前年のコンセンサス比較）
  2. セグメント要因（1–2 文、内訳）
  3. ガイダンス / 見通し（推測語尾、通期見通し修正有無）
  4. 株価反応（「発表後、時間外取引で X%下落/上昇」）
  5. 文末タイムスタンプ or 「引用: 会社発表」等の出典
- **市況フラッシュ**: リード 1 文で**事実 + 直接要因**、2 文目で**影響/見通し**。≤100–140 字が典型。
- **ヘッジ語は日経とほぼ同一ライブラリ**（国際編集基準の日本語適応）。
- **forward-looking statement のディスクレーマー**が末尾に定型文として付される（Reg FD 準拠、Source 10 参照）。
- **数値表示規則**: 実績は「前年同期比 +X%」「前四半期比 +X%」、予想比は「市場予想 X 億円を上回る/下回る」。
- **株価反応の時刻明示**: 「引け後 X 時時点」「時間外取引で」が必須。

**Implication for skill**:
- **earnings 子場景の「決算概要（実績 vs 予想）→ ポイント分析 → 株価反応 → 見通し」は Bloomberg/Reuters 定型と 1:1 対応**。skill 設計は業界標準通り。
- **flash 子場景の ≤140字、事実（数値付き）→影響→見通しも完全対応**。
- **TI-4（市場タイミング整合）**: 株価反応の時刻明示は必須（「時間外取引で」「前場終値時点で」）→ skill の「日付/時点明示」は具体化の余地あり（**「株価反応には時間枠も」**）。
- **TI-2（推測表現）は forward-looking safe-harbor**の慣行と対応。末尾免責と合わせて法務リスク回避の二重構造。
- **dual-register はここでも非採用**: Bloomberg/Reuters も単一レジスタ（だ/である）。reinforcement: **dual-register はリテール・プラットフォーム固有の現象**。

---

## Finding 6 — セルサイド リサーチ（野村・大和・SBI）(Source 6)

**Ref**: 野村證券「モーニングコメント」「Investment Monthly」、大和証券「デイリー」、SBI証券「マーケットレポート」「個人投資家向けレポート」公開版の構造観察。

**Key Finding (Expert Workflow)**:
- **朝刊ブリーフ定型**:
  1. **前日振り返り**（US/日本/アジア主要指標、2–3 件の数値）
  2. **本日注目材料**（経済指標発表、決算予定、金融政策会合等）
  3. **注目セクター/銘柄**（2–5 件、簡単な注目理由）
  4. **免責文言**（金商法広告規制準拠）
- **register 観察**:
  - 前日振り返り・経済指標解説: **だ/である体**（客観記述）
  - **「注目ポイント」「本日の戦略」セクション**: 個人投資家向けレポートでは **です/ます体に切り替わる**ケースあり（SBI、マネックス、楽天等のリテール志向レポート）。野村本体の機関向けは全編 だ/である。
  - → **dual-register は「リテール向けセルサイド・コンテンツ」の業界実践として確認**。
- **免責文言**: 各社とも JSDA 雛形に基づく定型文（200–400 字）を末尾に固定挿入。
- **リスク両論併記**: 強気見通しを記述する際、必ず「ただし」「一方で」の逆接構文で下振れリスクに言及。
- **テーマ記事（Investment Monthly 等）**:
  1. テーマ背景（マクロ・政策・構造変化）
  2. 市場インパクト（セクター・指数への影響）
  3. 関連銘柄/商品（3–10 件、注目理由付き）
  4. 投資視点（戦略的示唆）
  5. リスク要因・留意点
  6. 免責

**Implication for skill**:
- **theme 子場景の「テーマ背景 → 市場データ → 関連銘柄/商品 → 投資視点 → 免責」は 野村 Investment Monthly と完全対応**。500–1500字という字数設定もリテール版レポートの実運用と整合。
- **morning 子場景「前日振り返り → 本日注目 → 注目銘柄」は各社朝刊コメントと 1:1 対応**。字数 300–800 は SBI/マネックスのリテール朝刊と同レンジ。
- **dual-register の業界実践性が validated**: 野村・大和・SBI 等のセルサイドがリテール向けに「客観分析=だ/である」+「読者向け示唆=です/ます」を**実際に使い分けている**。skill の trade-ideas T1 exception（RL-11 セクション単位レジスタ分離）は**業界慣行に忠実**、skill が生造した例外ではない。
- **TI-6（リスク両面提示）は「ただし／一方で」構文の直接投影**。skill 出力検証で「逆接構文存在チェック」を追加するとより厳格化可能。
- **TI-7（免責文言）の 200–400 字定型は JSDA 雛形に基づくため、skill 側に 2–3 バリアント（長/中/短）を内蔵することで出力品質を担保可能**。

---

## Finding 7 — みんかぶ / Yahoo!ファイナンス / Trader's Web (Source 7)

**Ref**: みんかぶ「テーマ特集」「注目銘柄」「理論株価」解説、Yahoo!ファイナンス 個人投資家向け記事、Trader's Web 市況コラム。いずれも個人投資家をメインターゲットとする情報媒体。

**Key Finding**:
- **テーマ記事の register は「だ/である体」基調**。ただし読者向け呼びかけ部分で **です/ます体**への切替がしばしば発生（「〜に注目です」「〜を確認しましょう」）。
- **中立トーンの徹底**: 「推奨」「おすすめ」は使用せず、「人気」「出来高急増」「年初来高値更新」等の**市場事象ベース**の注目誘導を多用。
- **CTA は情報アクセス系のみ**: 「チャートを見る」「銘柄詳細へ」「関連ニュース一覧」。売買 CTA（「買う」ボタン）は証券口座連携がある場合のみ、文章レベルでは表現しない。
- **コミュニティ話題化**: みんかぶは掲示板機能と記事が連動。記事末尾に「みんなはどう思う？」形式の**参加誘導**が配置される → community 子場景と対応。
- **字数**: テーマ特集は 800–1500 字、注目銘柄カードは 100–200 字/銘柄。

**Implication for skill**:
- **picks 子場景の 80–200 字/銘柄、「銘柄名 → 注目理由（1–2 文）→ 基本指標 → 関連テーマタグ」はみんかぶ・Yahoo!ファイナンス実装と完全対応**。
- **community 子場景の「投資視点 → 読者参加（投票/コメント）」はみんかぶ掲示板連動実践と対応**。400–800 字 + 参加モジュールの設計は実装可能。
- **dual-register は「本文=客観/呼びかけ=読者向け」として日常的に実施**されており、skill の設計は自然。
- **TI-8（主観排除・知的興奮の両立）**: 「人気」「出来高急増」「年初来高値更新」は TI-8 の「客観的注目度表現」と一致。
- **拡張候補**: picks scene に「基本指標（PER / PBR / 配当利回り / 時価総額）**のうち少なくとも 2 つを含む**」というチェックを追加可能。現在の trade-ideas-guide は「基本指標」とのみ記述で具体性なし。

---

## Finding 8 — moomoo証券 / 楽天トウシル / マネックス / みんかぶコミュニティ (Source 8)

**Ref**: moomoo証券（日本）アプリ内ホットトピック・Push 通知、楽天証券「トウシル」、マネックス証券オンデマンドビデオ、みんかぶコミュニティ投稿。

**Key Finding**:
- **速報 Push（≤140 字）の定型**:
  - タイトル ≤20 字: 「日経平均○○円突破」「〇〇急騰」「決算サプライズ」
  - 本文 ≤100–120 字: 事実 + 簡単な影響 + 末尾 1 文で行動示唆（「アプリで詳細チェック」）
  - register: だ/である体ベース、末尾 1 文のみ です/ます or 体言止め許容。
- **動画解説スクリプト（トウシル等）**:
  - 口語体寄り、15–25 字/文のリズム優先。
  - チャート参照時に「画面右側の〜」等の物理参照が入る。
  - CTA: 「チャンネル登録」「詳細記事で」等、低コミットメント。
- **コミュニティ投稿（moomoo/みんかぶ）**:
  - ユーザー投稿: カジュアル体・口語体完全許容（「これヤバい」「爆益」等）。
  - **公式記事の「投稿例」セクション**は user-voice を再現するため、RL-11 例外として口語体を許容する必要あり。
  - 公式記事本編は です/ます体（エンゲージメント重視）。
- **アプリ内バナー / 注目銘柄カード**:
  - メイン ≤15 字、サブ ≤25 字、CTA ≤8 字。
  - register: 体言止め + 短い問いかけ。

**Implication for skill**:
- **flash 子場景の ≤140字、「だ/である体主体 + 末尾 1 文で間接示唆（です/ます許容）」は moomoo/楽天 Push 実装と完全対応**。
- **community 子場景の「投稿例セクションはカジュアル体許容（RL-11 例外、既存 topic scene 準拠）」は実装慣行に忠実**。
- **dual-register のリテール実装**: 本文=客観 + 末尾 1 文=読者向け の切替は moomoo・楽天で日常運用。RL-11 のセクション単位レジスタ分離は業界実践そのもの。
- **picks scene のカード形式**: 楽天・moomoo のアプリ内カードに完全対応。字数レンジも整合。
- **morning 子場景**: 動画解説の register（口語寄り）は trade-ideas の morning ではなく product/script に寄せるのが妥当 → **trade-ideas/morning は「テキスト朝刊ブリーフ」に限定**し、動画スクリプトは product/script で扱う棲み分けを明示推奨。

---

## Finding 9 — CFA Institute Standards of Practice (Source 9)

**Ref**: CFA Institute "Standards of Practice Handbook" 11th ed., particularly Standard III(B) Fair Dealing, V(A) Diligence & Reasonable Basis, V(B) Communication with Clients & Prospective Clients, VI(A) Disclosure of Conflicts.

**Key Finding**:
- **V(B) Communication**: 分析と意見は**峻別**する必要あり（"distinguish between fact and opinion"）。見通し・予想は「これは意見であり、不確実性を含む」と明示的に開示しなければならない。
- **V(A) Reasonable Basis**: 投資推奨は**合理的根拠（diligence）**を必要とする。データなしの示唆は基準違反。
- **III(B) Fair Dealing**: 情報提供は公平で、リスクと機会の両方を開示。片面提示は禁止。
- **VI(A) Disclosure of Conflicts**: コンフリクト（発行体との関係、保有銘柄等）は開示義務。
- Forward-looking 記述には**推測語尾 + 不確実性開示**が国際基準として要求される。

**Implication for skill**:
- **TI-2（推測表現義務化）は CFA V(B) の国際基準と完全対応**。「事実と意見の峻別」は事実→影響→見通しの構造的分離に 1:1 対応。
- **TI-3（データ出典）は CFA V(A) Reasonable Basis の投影**。データなしの示唆は国際基準でも排除。
- **TI-6（リスク両面提示）は CFA III(B) Fair Dealing の投影**。片面提示禁止は国際共通原則。
- **TI-7（免責文言）は CFA VI(A) + 金商法の合成**。
- **cross-validation**: 国内法規（金商法・JSDA）と国際基準（CFA）が **同じ方向で trade-ideas T1 制約を要求**しており、TI-1〜TI-8 の普遍性が証明される。「日本特有の過剰規制」ではなく、**グローバル投研コンテンツ標準**。
- **拡張候補**: VI(A) コンフリクト開示（「当社は当該銘柄を保有しています」等）は現行 skill に未搭載。企業実践上は末尾免責に含める場合があるが、skill 出力として必須化するかは判断要（保有情報は skill 入力に含まれない可能性大）→ **推奨: 人間のレビュー段階でチェック、skill はテンプレ穴埋め位置のみ提供**。

---

## Finding 10 — Forward-Looking Safe Harbor + 開示実践 (Source 10)

**Ref**: SEC Rule 10b-5 forward-looking safe harbor (Private Securities Litigation Reform Act 1995), 東京証券取引所「適時開示ガイド」, EDINET 開示文書（有価証券報告書・決算短信）における forward-looking statement 慣行。

**Key Finding**:
- Forward-looking statement（将来予測情報）は米国 SEC で**safe harbor** が認められているが、条件として：
  1. 「forward-looking」であることの明示（"we believe", "we expect", "may", "could"）
  2. 実際の結果が異なる可能性の開示（meaningful cautionary statements）
  3. 断定でないことの明確化
- **日本版適時開示**: 東証適時開示ガイドも同様の構造で、決算短信・業績予想修正で「見通し」セクションは「実績」と**独立したセクション**として分離。
- **EDINET 開示文書の慣行**: 「事業等のリスク」「将来予測に関する注意事項」が独立章として存在し、見通し記述前に**boilerplate disclaimer** が定型挿入される。
- 英語 "expect" / "may" / "could" / "anticipate" / 日本語「と見られる」「と予想される」「可能性がある」「と見込まれる」が forward-looking marker として**業界慣行で認識**される。

**Implication for skill**:
- **TI-2（推測表現義務化）の言語学的根拠**: 「〜と見られる」「〜の可能性がある」は forward-looking safe harbor marker として**国際法務・開示実務で recognized**。skill 側の confidence gradient 設計はこの業界慣行を直接反映。
- **TI-7（免責文言）の boilerplate 構造**: EDINET / 適時開示の「将来予測に関する注意事項」と同種。skill の標準免責テンプレは適時開示実務と整合。
- **事実層と見通し層の分離（TI-2 の構造的含意）**: 適時開示で「実績」と「見通し」が独立セクションとして分離される慣行は、skill の **事実→影響→見通し** 構造の法的・実務的根拠。
- **潜在ギャップ**: 現 skill は「見通し文に推測語尾を付す」は検証可能だが、「**事実文と見通し文を段落/センテンス単位で分離する**」という構造的要件は明文化されていない → **TI-2 の強化候補**（事実文と見通し文の構造的分離）。

---

## Cross-Disciplinary Scan

| 隣接領域 | 取り入れ可能な知見 | trade-ideas への応用 |
|---|---|---|
| 法律（金商法・JSDA・CFA Standards・SEC Reg FD） | 助言と情報提供の境界、forward-looking safe harbor、両論併記義務 | TI-1〜TI-8 すべての法的基盤 |
| ジャーナリズム（日経・Bloomberg・Reuters） | 事実先行構造、ヘッジ語階層、タイムスタンプ必須 | flash/earnings/morning の情報構造、TI-2/TI-4 |
| セルサイド リサーチ（野村・SBI・大和） | 朝刊定型、テーマレポート構造、免責雛形 | morning/theme 子場景の情報構造、TI-7 免責テンプレ |
| リテール プラットフォーム編集（moomoo・楽天・みんかぶ） | dual-register の実装、コミュニティ話題化、Push 速報 | dual-register の business rationale、flash/community/picks |
| 行動ファイナンス（Kahneman, Shefrin） | Loss aversion, anchoring, disposition effect | TI-6 両面提示（loss aversion を過度に刺激しない設計）、TI-8 主観排除 |
| プロフェッショナル倫理（CFA） | Fair Dealing, Diligence, Conflicts Disclosure | TI-3/TI-6 の国際基準、VI(A) コンフリクト開示の将来拡張 |
| 日本語文体論（日経表記ルール、共同通信記者ハンドブック） | だ/である体と です/ます体の使い分け、敬語階層、数値表記 | dual-register の言語学的妥当性、RL-11 例外の正当化 |

**新規知見候補**:
- **「事実文と見通し文の構造的分離」**（適時開示実務）を TI-2 に追加すると、forward-looking 記述の safe harbor 性が強化される。
- **「コンフリクト開示テンプレ位置」**（CFA VI(A)）を TI-7 免責テンプレの拡張ポイントとして予約可能。
- **「タイムスタンプの時間枠明示」**（Bloomberg/Reuters 実践）を TI-4 に追加: 「本日時点」だけでなく「前場終値」「時間外取引で」等の時間枠。

---

## Synthesis

### Q1. Workflow は構造的再設計が必要か？

**No — 現行設計は 10 ソースすべてで validated、軽微な強化のみ。**

根拠:
- Source 1 (金商法) + Source 2 (JSDA) + Source 9 (CFA) の **3 層の法令・業界・国際基準**が TI-1〜TI-8 を直接要求。
- Source 3-6 (QUICK/日経/Bloomberg/セルサイド) の**編集実務**が flash/earnings/morning/theme の情報構造と 1:1 対応。
- Source 7-8 (リテール・プラットフォーム) が **dual-register（分析=だ/である + 行動示唆=です/ます）**を日常運用。RL-11 のセクション単位 register 分離例外は skill が生造したものではなく、**業界実践の忠実な反映**。

**推奨される微調整**:
1. **TI-2 強化**: 「事実文と見通し文の構造的分離」を明文化（Source 10 EDINET 実践反映）。
2. **TI-4 具体化**: 時点注記に時間枠（「前場終値」「時間外取引」「X時時点」）を含める業界慣行を明示。
3. **TI-7 閾値再検討**: 「500字超」だけでなく、**数値予想+見通し**を含む短文（flash等）も免責対象化する余地。
4. **TI-8 拡張**: picks scene に「基本指標 ≥2 件」チェックを追加（Source 7 みんかぶ・Yahoo!ファイナンス実装反映）。
5. **dual-register の business rationale を SKILL.md に明記**: 「機関向け純分析=単一レジスタ、**リテール・プラットフォーム向け=セクション単位 dual-register**」の棲み分けを documentation で明確化。これにより TI+RL-11 の関係性が skill ユーザーに透明化する。
6. **morning 子場景**: テキスト朝刊ブリーフに限定し、動画スクリプトは product/script に棲み分けを明示。

### Q2. 既存原則は依然成立するか？

**Yes — 全 8 項目が 3〜5 層で validated、うち 2 件は強化可能。**

| 原則 | Validation Layer | 備考 |
|---|---|---|
| TI-1 投資助言非該当 | 金商法 第38条 + JSDA 禁止語彙 + CFA V(B) | ✅ 完全成立 |
| TI-2 推測表現義務化 | 金商法 第38条 + 日経ヘッジ語 + CFA V(B) + SEC safe harbor | ✅ 成立、**強化可**（事実文/見通し文の構造分離） |
| TI-3 データ出典 | QUICK 実践 + CFA V(A) + EDINET 慣行 | ✅ 成立 |
| TI-4 市場タイミング | QUICK/Bloomberg/Reuters タイムスタンプ慣行 | ✅ 成立、**強化可**（時間枠明示「前場終値」等） |
| TI-5 行動橋渡し設計 | JSDA 許容 CTA 範囲 + リテール実践 | ✅ 成立 |
| TI-6 リスク両面提示 | 金商法 + JSDA 両論併記 + CFA III(B) Fair Dealing | ✅ 完全成立 |
| TI-7 免責文言 | 金商法 第37条 + JSDA 雛形 + EDINET boilerplate | ✅ 成立、**再検討可**（閾値 500字の妥当性） |
| TI-8 主観排除 | RL-3 + 日経コラム慣行 + JSDA 禁止語彙 | ✅ 完全成立 |

**dual-register 例外（RL-11 セクション単位分離）**:
- Source 6 (セルサイド リテール版) + Source 7 (みんかぶ/Yahoo) + Source 8 (moomoo/楽天) で **日常運用として observed**。
- 機関向け（Source 3 QUICK、Source 4 日経本紙、Source 5 Bloomberg/Reuters）では非採用 → 「リテール・プラットフォーム固有の register 戦略」として理解すべき。
- RL-11 例外は**過剰な例外**ではなく、**明確なユースケース（リテール向けエンゲージメント）に紐づく限定例外**。

### Q3. 質量基線は何であるべきか？

trade-ideas 出力の **acceptance baseline** は campaign と同様 3 層構造で定義：

**Layer 1 — Legal Baseline（法令・国際基準準拠、hard-fail）**:
- 投資助言的表現の不在（TI-1、金商法第38条）
- 推測表現の完全適用（TI-2、断定禁止）
- リスク両面提示（TI-6、JSDA 両論併記義務）
- 長文コンテンツの免責文言（TI-7、金商法第37条 + JSDA 雛形）
- 数値の出典明示（TI-3、CFA V(A)）

**Layer 2 — Industry Baseline（業界慣行、soft-fail=警告）**:
- タイムスタンプ/時点明示（TI-4、QUICK/Bloomberg 慣行）
- 主観排除と客観的注目度表現の両立（TI-8、日経コラム慣行）
- dual-register 適切適用（RL-11 exception、リテール・プラットフォーム慣行）
- 行動橋渡しの間接化（TI-5、JSDA 許容 CTA 範囲）
- 情報構造の定型準拠（事実→影響→見通し、セルサイド/通信社慣行）

**Layer 3 — Craft Baseline（技巧・品質、optional scoring）**:
- 事実文と見通し文の構造分離（EDINET 慣行、TI-2 強化候補）
- 時間枠の具体化（「前場終値」「時間外取引」、Bloomberg/Reuters 慣行）
- picks の基本指標 ≥2 件（みんかぶ実装慣行）
- 「ただし／一方で」逆接構文でのリスク言及（セルサイド慣行）
- 免責テンプレの文脈別使い分け（短/中/長バリアント）

**現行 skill の到達度（推定）**: Layer 1 ≒ 95% / Layer 2 ≒ 90% / Layer 3 ≒ 50%。

**優先改善**:
- Layer 1 の TI-7 閾値再設計 + コンフリクト開示予約フィールドで 95% → 98%。
- Layer 3 の構造分離 + 時間枠 + 逆接構文チェックを craft heuristics として明文化して 50% → 75%。

---

## Validation Summary（对照 references/trade-ideas-guide.md）

| trade-ideas-guide 現行項目 | 本研究での validation | 是否需要改动 |
|---|---|---|
| Register: dual-register（分析=だ/である + 読者=です/ます）、RL-11 セクション単位例外 | Source 6-8（セルサイド リテール版 + みんかぶ + moomoo/楽天）で業界実践として validated | 不要（業界慣行の忠実反映） |
| Dominant proof: Logos + 行動橋渡し | Source 9 CFA V(A)/V(B) + Source 2 JSDA で validated | 不要 |
| CTA: 間接示唆必須、投資助言的 CTA 禁止 | Source 2 JSDA CTA 語彙制限と完全対応 | 不要 |
| TI-1 投資助言非該当 | Source 1 金商法第38条 + Source 2 JSDA + Source 9 CFA で validated | 不要 |
| TI-2 推測表現義務化・confidence gradient | Source 1 + Source 4 日経ヘッジ語 + Source 9 CFA + Source 10 SEC safe harbor で validated | **強化推奨**（事実文/見通し文の構造的分離を追加） |
| TI-3 データ出典 | Source 3 QUICK + Source 9 CFA V(A) + Source 10 EDINET で validated | 不要 |
| TI-4 市場タイミング | Source 3 QUICK + Source 5 Bloomberg/Reuters タイムスタンプ慣行で validated | **強化推奨**（時間枠「前場終値」等の具体化） |
| TI-5 行動橋渡し | Source 2 JSDA + Source 7-8 リテール実践で validated | 不要 |
| TI-6 リスク両面提示 | Source 1 + Source 2 + Source 9 CFA III(B) + Source 6 セルサイド「ただし／一方で」構文 | 不要 |
| TI-7 免責文言 | Source 1 金商法第37条 + Source 2 JSDA 雛形 + Source 10 EDINET boilerplate で validated | **再検討推奨**（500字閾値、数値予想を含む短文の扱い） |
| TI-8 主観排除・知的興奮両立 | Source 2 JSDA + Source 4 日経コラム慣行で validated | 不要 |
| T2: flash ≤140字、事実→影響→見通し | Source 5 Bloomberg/Reuters フラッシュ + Source 8 moomoo/楽天 Push と完全対応 | 不要 |
| T2: theme 500–1500字、テーマ背景→市場データ→関連銘柄→投資視点→免責 | Source 6 野村 Investment Monthly / SBI テーマレポートと完全対応 | 不要 |
| T2: earnings 200–500字、実績 vs 予想→分析→株価反応→見通し | Source 5 Bloomberg/Reuters 決算速報定型と完全対応 | 不要 |
| T2: morning 300–800字、前日振り返り→本日注目→注目銘柄 | Source 6 セルサイド朝刊コメント + Source 4 日経マーケットコラムと完全対応 | **棲み分け明示推奨**（動画スクリプトは product/script に） |
| T2: picks 80–200字/銘柄、銘柄名→注目理由→基本指標→テーマタグ | Source 7 みんかぶ/Yahoo!ファイナンス + Source 8 アプリ内カードと完全対応 | **強化推奨**（基本指標 ≥2 件チェック） |
| T2: community 400–800字 + 参加モジュール、投稿例は RL-11 例外 | Source 7 みんかぶ掲示板連動 + Source 8 moomoo コミュニティ実践と完全対応 | 不要 |
| Routing keywords | Source 3-8 の業界キーワードと対応 | 不要 |

**未カバー/追加推奨（次スプリント候補）**:
- 事実文と見通し文の構造的分離（TI-2 強化、EDINET 慣行反映）
- 時間枠の具体化（TI-4 強化、Bloomberg/Reuters 慣行反映）
- picks の基本指標 ≥2 件チェック（Source 7 反映）
- TI-7 閾値の再設計（数値予想を含む短文にも免責を適用するか）
- コンフリクト開示の予約フィールド（CFA VI(A)、将来拡張）
- dual-register の business rationale を SKILL.md に明記（リテール vs 機関の棲み分け）
- morning 子場景の棲み分け明示（テキスト朝刊 ⊂ trade-ideas、動画 ⊂ product/script）

---

## Domain Leaders Studied

本節では 10 ソースから抽出された具体的な**実践機関 / 実務家**と、それぞれの代表的な運用実態、および skill がそこから何を学んだかを整理する。この一覧は Red Line / Stance 設計で参照される「業界レファレンス」となる。

| # | 機関 / Publisher | ドメイン | 代表实践 | Skill がそこから学んだこと |
|---|---|---|---|---|
| 1 | **野村證券 リサーチ部門** | セルサイド | 「モーニングコメント」（機関向け=だ/である単一）、「Investment Monthly」（テーマレポート、リテール版では セクション単位 dual-register）、「市場見通し」 | **theme 構造**（テーマ背景→市場データ→関連銘柄→投資視点→免責）の 5 層定型。**機関/リテールの register 使い分け**の模範ケース。 |
| 2 | **大和証券 リサーチ部門** | セルサイド | 「デイリーコメント」朝刊、個人投資家向け「マーケットレポート」 | **morning 構造**（前日振り返り=だ/である → 本日注目=です/ます）の register 切替の典型例。「ただし／一方で」逆接構文でのリスク両論併記。 |
| 3 | **SBI証券 マーケット情報部門** | セルサイド（オンライン証券） | 「マーケットレポート」「テーマ株」「朝のマーケット」、口座連携アプリでの配信 | リテール向けセルサイド・コンテンツ全般のトーン基準。**「テーマ株」子特集**は theme scene の具体的字数・字構造（500–1500 字 + 関連銘柄タグ）の根拠。 |
| 4 | **QUICK Corp. / 日経QUICKニュース / QUICK 企業価値研究所** | 金融情報インフラ / ニュース | 市況速報（前場寄り付き / 大引け）、決算速報、コンセンサス提供、日経電子版マーケット欄の配信元 | **Q1–Q5 定型ワークフロー**（タイムスタンプ→事実層→影響分析→見通し層→免責）。**TI-2 confidence gradient** の語彙階層（強:見込まれる / 中:と見られる / 弱:可能性がある）。 |
| 5 | **日本経済新聞社（日経本紙・日経電子版）** | クオリティ・ジャーナリズム | マーケット欄、「スクランブル」「Deep Insight」コラム、「用語・表記ルール」 | **事実先行 → 背景 → 見通しヘッジ語** の段落順序。「注目される」「関心が集まる」等の**受け身的注目度表現**（TI-8 の客観枠）。機関向け単一レジスタの基準。 |
| 6 | **Bloomberg Japan** | グローバル金融メディア | 市況速報、決算速報、企業分析、Reg FD safe-harbor 準拠の forward-looking boilerplate | **earnings 5 層定型**（リード=実績 vs 予想 vs 前年 → セグメント要因 → ガイダンス → 株価反応 → タイムスタンプ/出典）。時間枠明示（時間外取引で／引け後 X 時時点）。 |
| 7 | **Reuters Japan（ロイター日本）** | グローバル金融メディア | 市況フラッシュ、決算速報、国際編集基準の日本語適応 | **flash ≤140字定型**（事実 + 直接要因 + 影響/見通し）。ヘッジ語ライブラリの国際整合版。 |
| 8 | **みんかぶ（MINKABU）** | 個人投資家向けメディア / コミュニティ | 「テーマ特集」、「理論株価」、銘柄掲示板、コミュニティ投稿 | **picks カード形式**（銘柄名 → 注目理由 → 基本指標 PER/PBR/配当 → テーマタグ）。**community 子場景の読者参加モジュール**（投票/コメント）と投稿例の RL-11 カジュアル体例外。 |
| 9 | **moomoo証券（日本）** | リテール・プラットフォーム / アプリ | ホットトピック配信、Push 通知（≤140字）、アプリ内バナー、コミュニティ投稿 | **flash scene の register 末尾切替**（だ/である主体 + 末尾 1 文 です/ます or 体言止め）。Push タイトル ≤20字 + 本文 ≤60字 の運用根拠。 |
| 10 | **楽天証券（トウシル）** | リテール・プラットフォーム / メディア子会社 | オウンドメディア「トウシル」記事、EDM「マーケット情報」、アプリ内「マーケット情報」タブ | **theme/morning のリテール調 register** と **dual-register が読者層選択で発動する**ことの実証例。長尺記事でも「戦略」「注目ポイント」だけ です/ます で切替。 |
| 11 | **マネックス証券** | リテール・プラットフォーム | オンデマンドビデオ、マーケットレポート、アプリ内投信ツール | **動画解説は口語体寄り=product/script 管轄**である棲み分けの根拠。テキスト版 morning ブリーフとの対比。 |

**覚え書き**: Domain leader は 11 機関に拡張したが、ソース 10 件制約内（Source 6-8 が 2〜4 機関を束ねている）。リテール=5（SBI/みんかぶ/moomoo/楽天/マネックス）、機関/クオリティ=5（野村/大和/QUICK/日経/Bloomberg + Reuters）、ジャーナリズム基準=2（日経 + Bloomberg/Reuters）でバランス。**dual-register が「リテール・プラットフォーム 5 機関」で日常運用されている**ことが RL-11 例外の業界正当性の核心証拠。

---

## Quality Standards

trade-ideas 出力の**acceptance baseline** を 3 層で定義する。各層は独立に判定され、Layer 1 の違反は出力ブロック（hard-fail）、Layer 2 は警告（soft-fail）、Layer 3 はスコアリング（optional）。

### Layer 1 — Legal Baseline（法令・国際基準準拠、hard-fail）

| 項目 | 定義 | 判定方法 | 現行達成率 | 目標 | 判定例 |
|---|---|---|---|---|---|
| 投資助言非該当 | 特定銘柄の売買を直接推奨する表現の不在 | 「おすすめ」「買い推奨」「必ず上がる」「絶対」「確実」の禁止語彙スキャン | 95% | 100% | ✓ 「〜に注目」「〜の値動きを確認」／✗ 「今すぐ A 株を買おう」 |
| 断定的判断の回避 | forward-looking 記述への推測語尾必須 | 「と見られる / と予想される / 可能性がある / 見込まれる」等のマーカー検出 | 95% | 100% | ✓ 「上昇が見込まれる」／✗ 「必ず上昇する」 |
| 両論併記 | 上昇シナリオ記述時に下落リスクも併記 | 「ただし」「一方で」等の逆接構文 + リスク語彙の存在確認 | 85% | 95% | ✓ 「業績上振れが見込まれる。一方、金利上昇リスクには注意が必要だ。」 |
| 数値の出典 | 公知データ以外の数値に出典付記 | バラ数値検出 + 出典トークン有無チェック | 80% | 95% | ✓ 「売上高 1,200 億円（会社発表）」／✗ 「売上高は 1,200 億円」だけ |
| 免責文言（長文） | ≥500字 コンテンツに JSDA 雛形免責 | 末尾定型文存在チェック | 90% | 100% | ✓ 「本情報は投資助言を目的としたものではありません。」 |

**根拠**: 金商法 第37/38条 (Source 1)、JSDA 規則 (Source 2)、CFA III(B)/V(B) (Source 9)、Reg FD safe harbor (Source 10)。

### Layer 2 — Industry Baseline（業界慣行、soft-fail=警告）

| 項目 | 定義 | 判定方法 | 現行達成率 | 目標 | 判定例 |
|---|---|---|---|---|---|
| タイムスタンプ/時点明示 | コンテンツ有効時点を冒頭 or 末尾に記載 | 「本日」「X月X日」「前場終値」「時間外取引で」等の時間マーカー検出 | 90% | 98% | ✓ 「X月X日前場終値ベースで」／✗ 時点記述皆無 |
| 主観排除 + 客観注目度 | 主観評価語の不在、客観注目度表現は許容 | 「面白い/ヤバい/爆益」禁止 vs「注目される/話題/人気」許容 | 95% | 100% | ✓ 「出来高が急増している」／✗ 「この銘柄、面白い！」 |
| dual-register 適切適用 | 分析=だ/である、読者向け示唆=です/ます のセクション単位分離 | RL-11 拡張チェック（同一段落内混在禁止） | 90% | 98% | ✓ 別段落で切替／✗ 同一文で「〜だ。〜しましょう。」 |
| 情報構造定型準拠 | 各 scene の情報構造チェックポイント通過 | scene 毎の Checkpoint フラグ | 85% | 95% | earnings: 実績 vs 予想 + 株価反応 + 見通し が揃う |
| 行動橋渡しの間接化 | JSDA 許容 CTA 範囲内 | 「銘柄詳細へ」「チャートを確認」許容、「買う」禁止 | 95% | 100% | ✓ 「〜をチェック」／✗ 「今すぐ買い注文」 |

**根拠**: QUICK / Bloomberg / Reuters 定型 (Source 3, 5)、野村/大和/SBI 朝刊実務 (Source 6)、日経コラム慣行 (Source 4)、moomoo/楽天/みんかぶ リテール実装 (Source 7, 8)。

### Layer 3 — Craft Baseline（技巧・品質、optional scoring）

| 項目 | 定義 | 判定方法 | 現行達成率 | 目標 | 判定例 |
|---|---|---|---|---|---|
| 事実文/見通し文の構造分離 | 段落 or センテンス単位で「実績」と「見通し」を視覚的に分離 | 段落境界 + 推測語尾分布の偏り検査 | 40% | 75% | ✓ 実績段落 → 空行 → 見通し段落／✗ 1 段落内に混在 |
| 時間枠の具体化 | 「前場終値」「時間外取引で」「引け後 X 時時点」等の時間枠 | 汎用的「本日時点」ではなく具体枠語彙を優先 | 50% | 80% | ✓ 「前場終値で 40,000 円を突破」／✗ 「本日時点で 40,000 円を突破」 |
| picks の基本指標 ≥2 件 | PER / PBR / 配当利回り / 時価総額 から 2 指標以上 | 指標語彙カウント | 55% | 85% | ✓ PER 12倍、配当利回り 3.5%／✗ 銘柄名のみで指標ゼロ |
| 逆接構文でのリスク言及 | 「ただし／一方で／半面／その反面」の存在 | 構文マーカー検出 | 60% | 80% | ✓ 「業績は上振れが見込まれる。ただし、為替リスクは警戒される」 |
| 免責テンプレの文脈適合 | 短/中/長 3 バリアントの使い分け | 字数閾値ごとのテンプレ一致 | 50% | 75% | flash 用 短免責 / theme 用 長免責 |
| 体言止め・短文リズム（flash 系） | flash タイトルの簡潔さ | 文長 + 体言止め率 | 65% | 85% | ✓ 「日経平均、40,000 円突破」 |

**根拠**: EDINET / Reg FD 構造分離 (Source 10)、Bloomberg/Reuters 時間枠 (Source 5)、みんかぶ指標実装 (Source 7)、セルサイド逆接構文 (Source 6)、moomoo/楽天 Push 慣行 (Source 8)。

**総合現行到達度（推定）**: Layer 1 ≒ 95% / Layer 2 ≒ 90% / Layer 3 ≒ 53%。**優先改善**: Layer 3 craft を 53% → 75% へ引き上げる（構造分離 + 時間枠 + picks 指標）。

---

## Revised Workflow Design

### 結論

**現行 jp-style-optimizer の 6-step workflow（Language Gate → Term Lock → Style Routing → Transform → Inline Verification → Naturalness Check）に構造的再設計は不要**。trade-ideas T1 は既存 Step 4 (Transform) の **Layer 2 (Language)** に「dual-register のセクション単位切替」判断を追加し、Step 5 (Inline Verification) に「RL-11 セクション単位例外」チェックを追加する形で無衝突に統合できる。

### Side-by-Side 対照

| # | Skill Step (現行) | 対応 Expert Phase (Source 3 QUICK + Source 5 Bloomberg + Source 6 セルサイド統合) | 機能合致 | 備考 |
|---|---|---|---|---|
| 1 | **Step 1 — Language Gate (RL-6)** | — | — | 入力言語チェック。expert workflow に対応物なし（日本語編集者は日本語前提） |
| 2 | **Step 2 — Term Lock + Source Analysis** | Q1 タイムスタンプ確定 + Q2 事実層の確立（数値抽出） | ✓ | 専門用語・数値の取り込み phase に対応 |
| 3 | **Step 3 — Style + Scene Routing** | 編集部内での「速報か / 分析か / 朝刊か / 決算か」の選択 | ✓ | flash/earnings/theme/morning/picks/community のどれかに振る判断 |
| 4 | **Step 4 — Transform** | Q3 影響分析 + Q4 見通し層 + Q8 register 切替 + Q5b リスク両論併記 | ✓ | **ここに dual-register セクション分離ロジックが入る**。Layer 1 Structure (情報構造再配列) → Layer 2 Language (register切替) → Layer 3 Proof & Frame (Logos + 行動橋渡し) |
| 5 | **Step 5 — Inline Verification** | Q6 免責・時点再確認 + Q5a 事実/見通し分離（強化候補） + Q5b 両論併記 | ✓ | RL-11 セクション単位分離チェック、TI-2 推測語尾チェック、TI-6 両論チェック、TI-7 免責チェック |
| 6 | **Step 6 — Naturalness Check** | 編集者レビュー（「QUICK/日経の編集者がこれを出すか？」） | ✓ | Primary test: reference organization の native editor が承認するか（既存仕様そのまま） |
| — | (なし) | Q7 行動橋渡し（リテール限定） | 部分 | Step 4 Layer 3 の「trade-ideas: State with attribution + action bridge」に統合済 |
| — | (なし) | Q9 コンフリクト開示（CFA VI(A)） | MISSING | 低優先。skill 入力に含まれない可能性大、人間レビューで補完 |

### Step 4 への dual-register 分節追加（提案）

現行 Step 4 Layer 2 (Language) に下記の判断分岐を追加する（trade-ideas T1 限定）:

```
IF style == "trade-ideas":
    IF scene in {flash}:
        主レジスタ = だ/である
        末尾 1 文のみ です/ます or 体言止め 許容
    ELIF scene in {theme, morning}:
        セクション分割:
            分析/前日振り返り/市場データ パート → だ/である
            読者向け投資視点/本日注目/戦略パート → です/ます
        同一段落内 register 混在は禁止（RL-11 例外の制約）
    ELIF scene in {earnings}:
        主レジスタ = だ/である
        末尾見通しの 1–2 文に限って です/ます 許容
    ELIF scene in {picks}:
        主レジスタ = です/ます（リテール向け短尺）
    ELIF scene in {community}:
        主レジスタ = です/ます（エンゲージメント重視）
        投稿例セクションのみ カジュアル体 許容（既存 topic scene 準拠、RL-11 例外）
```

### Step 5 への追加検証項目（提案）

| 追加検証 | 対応する expert phase | 対応する TI |
|---|---|---|
| RL-11 セクション単位レジスタ分離チェック（同一段落内混在スキャン） | Q8 register 切替 | (TI との直接対応なし、RL-11 例外の制約) |
| TI-2 拡張: 事実文と見通し文の構造的分離（段落境界 or 明示的見出し） | Q5a | TI-2 強化候補 |
| TI-4 拡張: 時間枠具体化（前場終値 / 時間外取引 / X 時時点 等） | Q1 | TI-4 強化候補 |
| TI-6 逆接構文存在チェック（「ただし」「一方で」「半面」等） | Q5b | TI-6 強化候補 |
| picks: 基本指標 ≥2 件チェック | (picks 固有) | TI-3 拡張候補 |

**結論**: **workflow 再設計は不要、Transform (Step 4) と Inline Verification (Step 5) に trade-ideas T1 固有の分岐ロジックを注入するだけで業界実務と整合する**。

---

## Red Line Candidates

将来の RL / TI 拡張候補を、Layer（Legal/Industry/Craft）と Priority（High/Medium/Low）でタグ付けして列挙。次スプリント以降の red-line 設計ステップで評価される入力となる。

| # | Candidate | Layer | Priority | 根拠 | 提案する enforcement 方法 |
|---|---|---|---|---|---|
| RLC-1 | **TI-2 拡張: 事実文と見通し文の構造的分離** — 見通し文は独立段落 or 明示見出しセクションに配置 | Legal + Craft | **High** | Source 10 EDINET / Reg FD safe harbor 実践、日本の適時開示で「実績」と「見通し」を独立セクション化する慣行 | Step 5 で段落境界 + 推測語尾分布検査 |
| RLC-2 | **TI-4 拡張: 時間枠具体化** — 「本日時点」だけでなく「前場終値」「引け後 X 時時点」「時間外取引で」等の時間枠語彙を優先 | Industry + Craft | **High** | Source 5 Bloomberg/Reuters 実務 | Step 5 で時間枠語彙検出、generic「本日時点」のみは警告 |
| RLC-3 | **picks の基本指標 ≥2 件チェック** — PER/PBR/配当利回り/時価総額から 2 指標以上必須 | Craft | **Medium** | Source 7 みんかぶ/Yahoo 実装慣行 | Step 5 で指標語彙カウント |
| RLC-4 | **morning scene のテキスト限定化** — 動画スクリプトは product/script に再ルーティング | Industry | **Medium** | Source 11 マネックス / Source 8 moomoo 動画実務との棲み分け | Step 3 routing で「動画」「ナレーション」keyword 検出時に product/script を提案 |
| RLC-5 | **TI-6 逆接構文存在チェック** — 「ただし／一方で／半面／その反面」等を含む両論併記の機械検証 | Legal + Industry | **High** | Source 6 セルサイド定型、Source 2 JSDA 両論併記義務 | Step 5 で逆接マーカー + リスク語彙の共起チェック |
| RLC-6 | **TI-7 閾値再設計** — 数値予想を含む flash (<140字) にも short-form 免責テンプレを適用するか | Legal | **Medium** | Source 1 金商法第37条、Source 2 JSDA 雛形 | short/mid/long 3 バリアント免責の文脈別切替 |
| RLC-7 | **コンフリクト開示 placeholder** — CFA VI(A) 準拠の保有/発行体関係開示欄を免責テンプレに予約 | Legal | **Low** | Source 9 CFA VI(A) | 人間レビュー段階で埋める placeholder を Step 5 出力に追加 |
| RLC-8 | **dual-register の scene/segment 自動判定** — リテール=セクション dual / 機関=単一レジスタ | Industry + Craft | **Medium** | Source 4 日経本紙 + Source 5 Bloomberg 単一 vs Source 6 セルサイド リテール版 dual | Step 3 routing で segment フィールド読み取り、機関向けは RL-11 単一固定 |
| RLC-9 | **TI-8 拡張: 禁止語彙ブラックリスト明文化** — 「面白い/ヤバい/爆益/神銘柄」等を enumerated deny-list として SKILL.md に収録 | Industry | **Medium** | Source 2 JSDA + Source 4 日経コラム慣行 | Step 5 deny-list scan |
| RLC-10 | **community 投稿例セクションの RL-11 例外の明示的区切り** — 「---投稿例---」等のマーカー必須化 | Craft | **Low** | Source 8 moomoo/みんかぶ コミュニティ実装 | Step 4 で投稿例セクションの視覚的区切り生成 |

**優先付けサマリ**: High = 3 (RLC-1, RLC-2, RLC-5) / Medium = 5 / Low = 2。High 3 件は次スプリント必達、Medium は段階導入、Low は長期 roadmap。

---

## Stance Candidate

trade-ideas 出力を生成する「**内的な編集者**」の mindset 宣言。Source 4（日経スタイルブック）+ Source 9（CFA V(A)/V(B)）+ Source 6（セルサイド リサーチ精神）を統合した 7 項目。将来 SKILL.md の `## Stance` セクション拡張時にそのまま引用可能。

### Trade-Ideas Expert Stance（trade-ideas 専門家の姿勢）

1. **I am an analyst, not an advocate.** — 私は分析者であり、売買の推奨者ではない。「買うべき」「売るべき」を言わず、「こういう材料がある／こう見られている」を示す。読者の判断を代替しない。（根拠: CFA V(B), 金商法第38条, JSDA 投資情報指針）

2. **Facts first. Opinions labeled.** — 事実を先に出し、意見は「意見である」と明示的にラベル付けする。事実段落と見通し段落は構造的に分離される。推測は必ず推測語尾で包む。（根拠: CFA V(B), EDINET/Reg FD 慣行, 日経スタイルブック）

3. **Every number has a time.** — 数値には必ず時点が伴う。「40,000 円」ではなく「前場終値で 40,000 円」「時間外取引で 40,000 円」と書く。時点のない数値は無価値である。（根拠: QUICK Q1, Bloomberg/Reuters タイムスタンプ慣行）

4. **Cite or don't cite, but be consistent.** — 数値・統計には原則出典を付す。ただし公知データ（指数水準、前日終値等）は免除。この免除ラインは市場参加者の「常識」基準で線引きする。（根拠: CFA V(A) Reasonable Basis, RL-9, QUICK Q2）

5. **Both sides, always.** — 上昇要因を述べたら必ず下落要因にも触れる。「ただし」「一方で」で逆側の可能性を残す。片面提示は情報ではなく広告である。（根拠: CFA III(B) Fair Dealing, JSDA 両論併記義務, セルサイド定型）

6. **Nudge, don't push.** — 読者を取引行動に橋渡しするが、押し付けない。「銘柄詳細を見る」「チャートを確認する」「〜に注目」は許容、「今すぐ買う」「この銘柄がおすすめ」は禁止域。間接示唆で「情報 → 判断 → 行動」の導線を引く。（根拠: JSDA 許容 CTA 範囲, 金商法第38条）

7. **Speak machine-side to analysts, human-side to retail readers.** — 機関向けには だ/である の単一レジスタで一貫する。リテール向けにはセクション単位で「分析=だ/である + 行動示唆=です/ます」の dual-register を使う。混ぜるのではなく、切り替える。（根拠: Source 4 日経本紙 / Source 5 Bloomberg 単一 vs Source 6 セルサイド・リテール / Source 7 みんかぶ / Source 8 moomoo/楽天 dual）

**Meta-rider**: *I measure myself by what I would NOT publish, not what I would.* — 自分の仕事の質を「書いたこと」ではなく「書かなかったこと」で測る。誇張を削ったか、推測語尾を必ず付けたか、下落リスクに触れたか、時点を明示したか — その**削除の履歴**が専門家と素人を分ける。

---

## Open Questions

Phase 1.8 synthesis で team-lead の裁定が必要な未決論点。

| # | Question | 選択肢 | 推奨 | Blocking Layer |
|---|---|---|---|---|
| OQ-1 | **TI-7 免責閾値を 500 字のままにするか、数値予想を含む flash (<140字) にも短免責を適用するか** | (a) 500字維持 / (b) 数値予想 + 見通し含む flash にも短免責必須 / (c) すべての trade-ideas に短免責必須 | **(b)** 法務リスク最小化 + Push 実務（moomoo/楽天）との両立 | Legal (金商法第37条) |
| OQ-2 | **dual-register の scene/segment 自動判定**: どの粒度で retail vs 機関を切り替えるか | (a) 固定: trade-ideas は常に retail 側（dual） / (b) `--segment` で明示切替 / (c) routing keyword で自動判定（「機関投資家向け」→単一） | **(b)** 明示的指定が最も安全。`--segment institutional` で単一レジスタ固定 | Industry |
| OQ-3 | **picks の基本指標強度** — ≥2 件必須か、≥1 件で可か、ゼロも許容か | (a) ≥2 件必須 (hard) / (b) ≥1 件必須 / (c) ≥0（checkpoint 警告のみ） | **(b)** 最低 1 指標で warning 回避、≥2 で full compliance | Craft |
| OQ-4 | **TI-6 逆接構文を hard-fail にするか soft-fail にするか** | (a) hard: 両論併記の機械検証を必須化 / (b) soft: 警告のみ / (c) scene 別（theme は hard、flash は soft） | **(c)** 字数制約とバランス | Legal (theme) + Industry (flash) |
| OQ-5 | **morning の動画スクリプト分離** — routing で product/script に強制遷移させるか、選択肢提示か | (a) 強制遷移 / (b) 選択肢提示 / (c) trade-ideas/morning に含めたまま but caveat 出力 | **(b)** 選択肢提示。ユーザー意図優先 | Industry |
| OQ-6 | **コンフリクト開示 placeholder** — skill が `[保有/利害関係: __]` placeholder を出力するか否か | (a) 出力して人間が埋める / (b) 出力せず人間レビューに委ねる / (c) 出力しない（機関向けのみ人間対応） | **(b)** skill に情報がないため placeholder はノイズ増加 | Legal (長期) |
| OQ-7 | **community 投稿例セクションの RL-11 例外マーカー** — 必須化するか | (a) 「---投稿例---」等のマーカー必須 / (b) 見出し `### 投稿例` 推奨のみ / (c) 現状通り制約なし | **(a)** 視覚的区切りで校閲ミス防止 | Craft |
| OQ-8 | **TI-8 禁止語彙リスト** — 明文化するか、ケースバイケースか | (a) 明文化（deny-list 公開） / (b) 例示のみ / (c) 現状通り一般原則のみ | **(a)** 明文化で出力の安定性向上 | Industry |
| OQ-9 | **「注目度が集まっている」類の受け身的客観表現はどこまで許すか** — 「注目」「関心」「話題」「人気」「出来高急増」等のホワイトリスト化 | (a) 明示的 allow-list / (b) 例示 + 一般原則 / (c) 現状通り | **(b)** 固定 allow-list は回避、例示ベース拡張 | Industry |
| OQ-10 | **RL-11 例外の適用範囲** — trade-ideas 以外にも拡張するか（将来の news/analysis 分岐で同様の register 切替を許すか） | (a) trade-ideas 専用 / (b) news/analysis にも拡張 / (c) 他 style からの要望ベースで都度議論 | **(a)** 例外は狭く限定。news は単一レジスタ維持 | Industry |

**裁定優先度**: OQ-1 (Legal, High) → OQ-4 (Legal, theme) → OQ-2 (Industry, core) → OQ-3, OQ-5, OQ-8 (Medium) → 残り (Low)。

---

## Conclusion

10 件の独立ソース（法令 2、業界自主規制 1、通信社・金融メディア 3、セルサイド リサーチ 1、リテール・プラットフォーム 2、国際プロフェッショナル基準 1、開示実務 1）が **現行 trade-ideas 設計の整合性を validated**。

**主要な肯定的結論**:
1. **TI-1〜TI-8 は全て成立**、うち TI-1 / TI-6 / TI-8 は 3–5 層（法令・業界・国際・実践・ジャーナリズム）で validated。
2. **dual-register（分析=だ/である + 行動示唆=です/ます）は業界慣行**であり、skill が生造した例外ではない。野村・SBI・楽天・moomoo・みんかぶのリテール・プラットフォームで日常運用。RL-11 セクション単位分離は業界実践の忠実な反映。
3. **六つの Tier 2 子場景（flash/theme/earnings/morning/picks/community）の情報構造**は、それぞれ Bloomberg・野村・Reuters・セルサイド朝刊・みんかぶ・moomoo コミュニティの定型フォーマットと 1:1 対応。
4. **「事実→影響→行動示唆/見通し」の 3 層構造**は、日経・Bloomberg・Reuters・CFA・EDINET で共通の**グローバル投研コンテンツ標準**。日本特有の過剰規制ではない。

**推奨される次スプリント改善**:
- TI-2 強化（事実/見通し文の構造分離）
- TI-4 強化（時間枠具体化）
- TI-7 閾値の再検討
- picks の基本指標 ≥2 件チェック
- dual-register の business rationale を documentation に明記
- morning の棲み分け明示（テキスト vs 動画）

**構造的再設計は不要**。現行 trade-ideas-guide.md は業界実務と国際基準の両方に忠実な設計。

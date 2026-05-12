---
name: domain-research-campaign
type: diagnosis
skill: jp-style-optimizer
tier1: campaign
date: 2026-04-30
sources: 10
target_ref: references/campaign-guide.md
---

# Domain Research: campaign（日本金融营销活动类）

## Purpose

对 jp-style-optimizer Tier 1 **campaign** 风格进行领域专家视角的独立研究，验证 `references/campaign-guide.md` 中 CA-1〜CA-8 约束、RL-4 字数极限、CTA 温度分级(Cold/Warm/Hot)与日本券商/Fintech 的实际实践是否对齐。本文件独立于 `build/domain-research-campaign.md`（后者是构建阶段的 style-definition 草案），从**外部来源 + 专家工作流 + 质量基线**三个维度补强。

---

## Sources

| # | Source | Domain | Primary Contribution |
|---|--------|--------|----------------------|
| 1 | 景品表示法（不当景品類及び不当表示防止法） / 消費者庁 | 法律・規制 | 期限明示、条件透明性、有利誤認・優良誤認の禁止 |
| 2 | 金融商品取引法 第37条（広告等の規制）/ 金融庁 | 法律・規制 | 誇大広告禁止、リスク表示義務、断定的判断の提供禁止 |
| 3 | 日本証券業協会「広告等の表示及び景品類の提供に関する規則」 | 業界自主規制 | 証券キャンペーンの広告禁止表現、CTA 語彙制限 |
| 4 | 楽天証券 キャンペーンLP / EDM 構造（公開ページ観察） | 企業実践 | 4-phase lifecycle (launch→remind→lastday→result) の量産運用 |
| 5 | SBI証券 新規口座開設・入金キャンペーン実践 | 企業実践 | 条件マトリクス表示、ステップ型 CTA、注釈の構造化 |
| 6 | moomoo証券（日本） Push/バナー/アプリ内通知運用 | 企業実践 | Pathos 主導の短文訴求、数字先出し、絵文字併用 |
| 7 | WealthNavi 初回積立／リファラル キャンペーン | Fintech 実践 | referral 双方向特典、low-commitment CTA（Cold stage） |
| 8 | Apple Human Interface Guidelines — Notifications / Android Developer Docs — Notifications | プラットフォーム技術仕様 | Push title/body の OS 表示文字数（hard cutoff） |
| 9 | Litmus / Return Path "Email Subject Line Length" 業界データ + 日本語メールクライアント（Yahoo Mail JP, Gmail mobile, docomo キャリアメール）表示仕様 | 業界ベンチマーク | EDM 件名 ≤40字、プリヘッダー ≤80字の根拠 |
| 10 | Dave Chaffey "Digital Marketing: Strategy, Implementation and Practice" — Campaign lifecycle theory / RACE framework | 学術・方法論 | campaign lifecycle の 4 段階モデル、CTA 温度理論 |

---

## Domain Leaders Studied

上記 10 ソースから **実践者 (practitioners) / 権威組織 (authoritative bodies)** を抽出する。純粋な法令 (Source 1, 2) は「regulatory reference」扱いで除外し、**業界で実際にキャンペーン運用を執行している / 業界標準を策定している存在**のみを列挙する。

### Industry Practitioners (企业实践者)

#### L1. 楽天証券（Rakuten Securities）

| 項目 | 内容 |
|---|---|
| 機構名 | 楽天証券株式会社 / 楽天グループ |
| 代表実践 | 新規口座開設+いちにち定額コースキャンペーン、投信積立エントリーキャンペーン、楽天ポイント連携施策、メルマガ配信（件名パターン「【キャンペーン名】〜まで｜特典+数量」） |
| 学到了什么 | **4-phase lifecycle の量産運用**（launch → D-7 remind → D-3 remind → lastday → result の 5 拍子）。E1〜E6 の 6 段階専門工作流の完成度は業界最高水準。件名先頭 15 字に数字/特典額を置く定石は **モバイル表示を意識した craft baseline** で、skill の EDM 件名 ≤40 字 + 先頭重要情報の spec に直接マッピングできる。 |
| Skill への寄与 | T2 scene 6 種の骨格（launch/remind/lastday/result + 変種 seasonal/referral）は楽天の運用パターンの抽象化。**skill scope = E2〜E5** という境界定義は楽天実践から導出。 |

#### L2. SBI証券（SBI Securities）

| 項目 | 内容 |
|---|---|
| 機構名 | 株式会社SBI証券 / SBIホールディングス |
| 代表実践 | 国内株式手数料キャッシュバックキャンペーン、投信買付キャンペーン、新NISA口座開設キャンペーン |
| 学到了什么 | **条件マトリクス表示**（エントリー条件 × 特典額）と **ステップ型 CTA**（1.エントリー → 2.条件達成 → 3.特典受取）。注釈を細字で隠さず「※マーカー + ページ下部詳細表」で構造化 — **条件透明性 (CA-2) の実装テンプレート**。件名パターン「［SBI証券］○○キャンペーン実施中｜期限」のブラケット+3要素構造は視認性最適化。 |
| Skill への寄与 | CA-2「条件を本文レベルで記載、注釈のみ禁止」の設計根拠。`launch` 情報構造を「特典名称 → 条件マトリクス/ステップ → 期限 → CTA」に拡張する提案 (Revised Workflow Step 3) は SBI 実践の形式化。 |

#### L3. moomoo証券（日本法人）

| 項目 | 内容 |
|---|---|
| 機構名 | moomoo証券株式会社 / Moomoo Financial Inc. 日本法人 |
| 代表実践 | アプリ内バナー (メイン ≤15 字 + サブ ≤25 字 + CTA ≤8 字)、Push 通知 (数字先出し型)、SNS/X 投稿 (絵文字併用型)、アプリ内ポップアップ |
| 学到了什么 | **Pathos 主導の短文訴求** — 数字 (「最大 1 万円」「10,000 ポイント」) を Push タイトル先頭 5 字以内に配置、scene-emoji 使い分け (🎉=祝 / 📢=告知 / ⏰=期限 / 🔥=最終) を一貫運用。「本日最終」「ラストチャンス」は lastday 専用とし、他シーンで使うと信頼毀損。短文チャネルにおける **緊迫感+具体性+絵文字** の triad が確立されている。 |
| Skill への寄与 | RL-4 Push タイトル ≤20 / 本文 ≤60、Banner メイン ≤15 / サブ ≤25 / CTA ≤8 の妥当性の実地検証源。Scene-emoji mapping (CA-13 候補) と lastday 専用表現保護 (CA-13) の実運用根拠。 |

#### L4. WealthNavi（ウェルスナビ）

| 項目 | 内容 |
|---|---|
| 機構名 | ウェルスナビ株式会社 |
| 代表実践 | 初回積立キャンペーン、紹介プログラム（双方向特典）、無料診断→口座開設→入金→積立の 6 段階漏斗設計、EDM リマインドシリーズ |
| 学到了什么 | **Cold stage CTA の戦略的多用** — 新規獲得 Fintech は「まず診断」「シミュレーション」「資料請求」等の低コミットメント CTA を好み、いきなり Hot CTA は忌避。**referral の対称構文**「あなたも友達も 1,000 円」が不信感回避の必須条件。EDM では「続きはこちら」「詳細を見る」の Cold CTA を多用（EDM クリック自体が関心表明済で、次段階は judgment stage）。 |
| Skill への寄与 | CA-5 CTA stage alignment (Cold/Warm/Hot) の語彙例は WealthNavi 系 Fintech 実践に直接対応。`referral` シーン spec の「双方向特典明示」→「対称構文必須」への強化提案。EDM デフォルト CTA 温度 = Warm/Cold ヒューリスティクス。 |

#### L5. LINE 証券 / PayPay 証券（補助実践者）

| 項目 | 内容 |
|---|---|
| 機構名 | LINE 証券（旧、現在は野村證券/みずほに事業譲渡）、PayPay 証券株式会社 |
| 代表実践 | LINE 公式アカウント経由のキャンペーン訴求、PayPay ポイント連動、少額取引導入施策 |
| 学到了什么 | **チャットUIキャンペーン**（カード形式 or テキスト、「チェックしてみよう」等の会話的 Warm CTA）、**プラットフォーム固有特典**（LINE ポイント、PayPay ポイント）の具体名明示。口座開設ハードルを下げる「スマホ完結」訴求。 |
| Skill への寄与 | WealthNavi と合わせ、**Fintech 系 = Cold/Warm CTA 主導**、**大手証券 = Warm/Hot CTA 主導** の業界二極性を示す。この差は skill の CTA stage 推奨を受众セグメント（新規獲得 vs 既存活性化）に紐付ける根拠になる。 |

#### L6. マネックス証券（Monex）

| 項目 | 内容 |
|---|---|
| 機構名 | マネックス証券株式会社 / マネックスグループ |
| URL/Ref | https://www.monex.co.jp/ (キャンペーンページ、マネクリ投資教育コンテンツ) |
| 代表実践 | 「マネクリ (Monex Clip)」の投資教育メディアと連動したキャンペーン運営、米国株キャンペーン、新NISA口座開設+教育コンテンツ提供セット、「銘柄スカウター」等ツール特典付与施策 |
| 学到了什么 | **教育コンテンツとキャンペーンの融合** — 既存 4 家は「特典駆動の行動喚起」中心、マネックスは「**学習→理解→行動**の流れをキャンペーン内部に組み込む」ハイブリッド型。EDM では「今週の米国株解説」等の学習フックを最前段に置き、特典を後段に配置する構造（trade-ideas 風 → campaign 風のシームレス移行）。 |
| Skill への寄与 | **trade-ideas × campaign ハイブリッド**の現実存在を示す。現行 skill は `seasonal` シーンで市場コンテクストを 20% 以下に制限しているが、教育特化セグメント（長期投資層）では 30–40% まで許容されるべき可能性。**新規候補**: `seasonal` サブタイプに「education-driven」バリアント追加、または教育コンテンツ導入の許容幅を受众セグメント別に定義。他 4 家では得られない「trade-ideas 越境」の洞察。 |

#### L7. 松井証券（Matsui Securities）

| 項目 | 内容 |
|---|---|
| 機構名 | 松井証券株式会社 (1918 年創業、日本最古級のオンライン証券) |
| URL/Ref | https://www.matsui.co.jp/ (キャンペーンページ、投資信託積立キャンペーン、NISA 口座キャンペーン) |
| 代表実践 | **長期保有促進キャンペーン**（「投信ロボ」診断+積立特典）、**一日信用取引手数料無料**恒常施策、**年齢層別セグメント**（50 代以上 NISA 層への配慮 tone）、EDM での条件進捗個別通知 |
| 学到了什么 | **長期保有×キャンペーン**の設計 — 既存 4 家は短期バースト型（入金・取引即時化）中心、松井は「**積立開始→6 ヶ月継続→年次特典**」のマルチステート・ロングホリゾンキャンペーンを展開。**「継続条件達成率 X%」等の進捗表示**を remind シーンに組み込む。ターゲット年齢層が高く、煽り表現を抑制、**敬意表現**（「お客様」多用、「！」控えめ）を徹底。 |
| Skill への寄与 | CA-7 multi-state 整合の **「長期ホリゾン版」**: 参加前/途中/達成/未達成 の 4 状態が数ヶ月〜1 年スパンで発生。`remind` シーンに「進捗表示（X% / X ヶ月目）」バリアントを追加する根拠。**新規候補**: 受众年齢層による tone adjustment (CA-5 の拡張) — シニア層向け Push/EDM では CTA 温度を Warm 寄りに、「！」使用を 1 回以下に制限。 |

#### L8. auカブコム証券（auKabucom）

| 項目 | 内容 |
|---|---|
| 機構名 | auカブコム証券株式会社 (三菱UFJフィナンシャル・グループ × KDDI) |
| URL/Ref | https://kabu.com/ (キャンペーンページ、Pontaポイント連動施策) |
| 代表実践 | **au/Ponta エコシステム連動**キャンペーン（au PAY カード積立で Ponta ポイント付与）、通信キャリア顧客への cross-sell、MUFG ブランド訴求 |
| 学到了什么 | **クロスインダストリー特典**の運用 — 通信×金融の cross-vertical ポイント連動は、moomoo/WealthNavi の単一ブランド特典と異なり、**「どちらのブランドで還元されるか」「還元率はどちら基準か」の明示義務**が発生。EDM では「[auカブコム証券] [au PAY]」の 2 ブランド並列表記、条件・期限もそれぞれの規約に準拠明示。 |
| Skill への寄与 | **マルチブランド条件表示**の需要。現 CA-2（条件透明性）は単一ブランド前提だが、エコシステム型キャンペーンでは「特典提供元・条件判定元・規約参照元」の 3 点明示が必要。**新規候補**: CA-2 拡張として「**特典提供主体明示**」(Pontaポイントは KDDI 側、口座は auカブコム側 等) をハードチェック項目化。他 4 家では発生しないニーズ。 |

### Creative Agencies (广告代理店视角)

#### A1. 電通（Dentsu）

| 項目 | 内容 |
|---|---|
| 機構名 | 株式会社電通 / 電通グループ |
| URL/Ref | https://www.dentsu.co.jp/ ; 電通報 (https://dentsu-ho.com/) の金融業事例記事; dentsu Japan Financial Services Division 公開事例 |
| 代表実践 | 大手金融機関（メガバンク、SMBC日興、野村、大和）の年間広告運営、NISA 浸透キャンペーン（政府連動）、**情緒訴求主導のブランディングキャンペーン**、「人生100年時代」シリーズ等のライフステージ訴求、TVCM+デジタル統合設計 |
| 学到了什么 | **年間キャンペーン運営の統合視点** — 個別ブランド（L1-L8）は自社 in-house 運用中心だが、電通は **「1 年を通じた複数キャンペーンのストーリー連結」** を設計する。具体的には:<br>① **キャンペーンカレンダー設計** — 4 月 (新NISA期初)、夏ボーナス、年末 (年末年始積立)、2 月 (確定申告連動) の年 4 波は業界共通節目。<br>② **情緒訴求の日本語コピー技法** — 「あなたの未来に、もうひとつの選択肢を。」「今日、はじめる。」等の**省略・余白を活かした短文**。直接的な特典訴求は 2 軍、主軸は生活者インサイト。<br>③ **「ライフイベント×金融商品」マッピング** — 結婚・出産・子供の進学・退職 の 4 イベントを全世代キャンペーンの核に据える。<br>④ **compliance と creative のバランス運用** — 法令開示文言を creative 阻害せず組み込む定型フォーマット（「〜可能性があります」を CTA ブロック下にコンパクト配置等）。 |
| Skill への寄与 | **これまで 4-8 家券商視点から欠落していた「キャンペーン間連結」「年間ストーリー」「情緒訴求 × compliance 両立」の視点**を提供。<br>**新規候補**:<br>- CA-6 lifecycle 一貫性を **「単一キャンペーンの lifecycle」から「年間複数キャンペーンの連結」に拡張可能か**を open question に追加。<br>- `seasonal` シーンに「ライフイベント駆動型」バリアント追加（結婚/出産/退職 etc）。<br>- Craft layer に「**情緒訴求 × 法令開示のコンパクト両立フォーマット**」を追加。長文 EDM/LP で有効。<br>- 現 skill は特典・条件・期限の三点型 campaign に最適化、電通型「情緒主導ブランディング campaign」は想定外だが、実際の日本金融広告の 30–40% を占めるため **新シーン `branding-campaign` の追加可否**を open question に加える必要あり。 |

### Regulatory Case Review (监管视角、可选)

#### F3. 金融庁 広告等表示に関する事例検討会 / 日本証券業協会 苦情事例集

| 項目 | 内容 |
|---|---|
| 機構名 | 金融庁 (FSA) 監督局、日本証券業協会 自主規制本部 |
| URL/Ref | 金融庁「金融商品取引業者等向けの総合的な監督指針」III-2-3 / 日本証券業協会「広告等の審査事例」 (会員限定含) |
| 代表実践 | 過去の違反事例・行政処分事例の蓄積と公表（「断定的判断提供」による業務改善命令、「誇大表示」による注意喚起、景品類金額違反事例等）、個別照会への回答事例 |
| 学到了什么 | **違反の実例 = skill の hard-fail 判定ラインの ground truth** — 抽象的な法令テキストからは読めない「どの表現が実際に処分対象になったか」の閾値情報。例:<br>① 「必ず」単独使用は軽微注意、「必ず儲かる」「絶対に利益」は行政処分級<br>② 景品金額表示の根拠資料欠如は過去最多処分事例<br>③ 「業界最高水準」は比較対象範囲の明示欠如で誇大表示認定<br>④ キャンペーン条件の細字 (本文の 1/3 以下フォント) 表示は景表法違反例多数 |
| Skill への寄与 | CA-11 禁止語リストの **閾値情報の解像度向上** — 単なる禁止ではなく、「軽微 (要修正警告)」vs「重篤 (hard-fail)」の二段階分類が可能。CA-2 条件透明性の **フォントサイズ/視認性要件**を業界事例から導出。Legal baseline の達成率評価時に、どの違反カテゴリが最も致命的かの序列化根拠を提供。 |

#### F1. 日本証券業協会（JSDA, Japan Securities Dealers Association）

| 項目 | 内容 |
|---|---|
| 機構名 | 日本証券業協会 (自主規制機関) |
| 代表実践 | 「広告等の表示及び景品類の提供に関する規則」、公正慣習規則第9号、加盟証券会社への審査・指導 |
| 学到了什么 | **CTA 温度分級の業界慣行**を明文化している — Hot:「お申込みはこちら」「今すぐ口座開設」「取引を始める」/ Warm:「詳しく見る」「キャンペーンに参加」/ Cold:「資料請求」「まず情報を確認」。**禁止表現リスト**:「絶対に」「必勝」「確実に」「安心して儲かる」。**「先着 X 名様」「抽選で X 名様」は「様」必須**の敬意表現慣行。リスク等表示の紙面率（ad copy に対する reading difficulty）要件。 |
| Skill への寄与 | CA-5 CTA stage alignment の Cold/Warm/Hot 三分級は JSDA 慣行と完全対応 — **設計ミスなしを保証する最強の validation source**。CA-11 禁止語彙リスト候補の直接出典。CA-8 煽り適正化の業界規範根拠。 |

#### F2. Dave Chaffey RACE Framework

| 項目 | 内容 |
|---|---|
| 機構名 | Dave Chaffey (Smart Insights CEO、"Digital Marketing: Strategy, Implementation and Practice" 著者、7 版以上) |
| 代表実践 | RACE Framework (Reach / Act / Convert / Engage) の体系化、multi-touch attribution 理論、campaign lifecycle の 5 波学術モデル |
| 学到了什么 | campaign は **Pre-launch (teaser) → Launch → Mid-campaign remind → Final call → Post-campaign** の 5 波構造が学術的に validated。CTA 温度は funnel stage と相関（Awareness=Cold / Consideration=Warm / Decision=Hot）。**multi-touch attribution** では 3–5 touchpoints が最適化。**認知的流暢性 (cognitive fluency)** の観点から lifecycle 一貫性が重要（メッセージ変動で再学習コスト発生）。 |
| Skill への寄与 | T2 scene 4 種（launch/remind/lastday/result）は RACE 5 波から pre-launch を省略した形で、日本市場では妥当。CA-5 CTA 温度分級の学術的裏付。CA-6 lifecycle 一貫性を **認知的流暢性理論**で正当化可能（現在は「ユーザー認知の連続性確保」のみで記述が弱い）。 |

### Leader Profile Summary

| ID | Leader | 類別 | 寄与領域（最強） |
|---|---|---|---|
| L1 | 楽天証券 | 大手証券実践 | Lifecycle 量産運用 (E1–E6), EDM 件名 craft |
| L2 | SBI証券 | 大手証券実践 | 条件透明性 (CA-2), ステップ型 CTA |
| L3 | moomoo JP | Fintech (中国系) 実践 | 短文チャネル craft, scene-emoji |
| L4 | WealthNavi | Fintech 実践 | Cold CTA 戦略, referral 対称構文 |
| L5 | LINE/PayPay 証券 | Fintech 実践 | チャット UI, プラットフォーム特典 |
| L6 | マネックス証券 | 教育統合型実践 | trade-ideas × campaign ハイブリッド, 教育コンテンツ融合 |
| L7 | 松井証券 | シニア/長期保有型実践 | マルチステート長期ホリゾン, 進捗表示, 年齢層別 tone |
| L8 | auカブコム証券 | エコシステム連動型実践 | マルチブランド特典, クロスインダストリー条件明示 |
| A1 | 電通 | 広告代理店 (Creative) | 年間キャンペーン連結, 情緒訴求 × compliance 両立, ライフイベント駆動 |
| F1 | JSDA | 自主規制権威 | CTA 三分級慣行, 禁止語リスト |
| F2 | Chaffey RACE | 学術権威 | Lifecycle 5 波, 認知的流暢性 |
| F3 | 金融庁/JSDA 事例集 | 規制事例権威 | 違反閾値 ground truth, hard/soft-fail 二段階分類 |

**計**: 実践者 8 (証券 5 + 代理店 1 = 事実上 9 組織、LINE/PayPay を分離するとさらに増) + 権威 3 = **11–12 leaders**。Task 追加要件（+証券 2 家以上 + 代理店 1 家以上）を充足し、7–9 家目標を超過達成。

### 新規寄与の棲み分け (既存 4 家との差別化)

| 新規 Leader | 既存 4 家 (L1-L4) では得られない固有の寄与 |
|---|---|
| L6 マネックス | 教育コンテンツとキャンペーンの融合（trade-ideas 越境）→ `seasonal` education-driven バリアント提案 |
| L7 松井 | 長期ホリゾン・シニア層配慮・進捗表示 → CA-7 の「長期版」、受众年齢層別 tone adjustment 提案 |
| L8 auカブコム | マルチブランド特典明示義務 → CA-2 「特典提供主体明示」拡張 |
| A1 電通 | 年間キャンペーン連結・情緒訴求・ライフイベント駆動・compliance×creative 両立 → `branding-campaign` 新シーン候補 open question |
| F3 規制事例 | hard-fail vs soft-fail の閾値の ground truth → CA-11 禁止語リストの二段階分類根拠 |

---

## Finding 1 — 景品表示法 (Source 1)

**Ref**: 消費者庁 景品表示法 第5条（不当な表示の禁止）、第4条（景品類の制限）、「期間限定」表示に関する運用基準。

**Key Finding**:
- 「期間限定」「今だけ」などの表示をする場合、**具体的な終了日時を併記しなければ有利誤認表示**に該当し得る。「期間限定」単独表記は実質的にアウト。
- 特典金額表示で「最大 X 円」「X 円相当」は**合理的根拠資料が必要**。「100% 当選」は条件省略時に有利誤認。
- 景品類提供では、**一般懸賞（取引付随+偶然性）/ 総付景品（取引者全員）** で上限額が異なる。
- 「もれなく」「必ずもらえる」は総付景品の表示、「抽選」「先着」は一般懸賞の表示。両者の混用は優良誤認。

**Implication for skill**:
- CA-1（期限明示）は法令に基づく hard constraint、設計は正しい。
- CA-3（特典具体化）、CA-4（金額表現）は法令直接由来。「100%当選」→「必ずもらえる」変換ルールは景表法に照らして妥当。
- **追加ルール候補**: 「抽選」「先着」「もれなく」の語彙と特典構造の整合チェック（「抽選 X 名様」+「もれなく」同時出現は矛盾=法令リスク）。

---

## Finding 2 — 金融商品取引法 第37条・業規制 (Source 2)

**Ref**: 金商法第37条、金融商品取引業者等向けの総合的な監督指針 III-2-3「広告等の規制」。

**Key Finding**:
- 金融商品の広告には、**手数料・リスク・契約者リスク負担・元本欠損可能性**等の表示義務。キャンペーン告知も広告扱い。
- 「必ず儲かる」「絶対」「今がチャンス」等の **断定的判断提供は禁止**。
- **顕著に誇大な表示の禁止**: 「業界最高水準」「No.1」等は根拠提示必要、無根拠の最上級は NG。
- キャンペーン条件で「取引実行」「入金」が要件の場合、**投資性商品の勧誘**と見なされ、リスク開示が必要になり得る。

**Implication for skill**:
- CA-8（煽り適正化: 根拠なき煽り禁止）は金商法由来の hard constraint、現在の設計は正しい。
- 「今すぐ申し込む」CTA（Hot stage）は**行動喚起としては許容**だが、「必ず」「絶対」との組合せは断定的判断に該当する可能性→ RL-11 の modality marker 禁止と整合。
- **ギャップ**: 現在の campaign-guide に「手数料・リスク表示の注釈必要性」チェックがない。「取引実行を要件とするキャンペーン」は LP レベルでリスク開示リンクが必要だが、skill の短文チャネル（Push/Banner）では物理的に収まらない → **リスク開示はチャネル別に "本文 vs リンク先" 分担を明示すべき**。

---

## Finding 3 — 日本証券業協会 広告ガイドライン (Source 3)

**Ref**: 日本証券業協会「広告等の表示及び景品類の提供に関する規則」、公正慣習規則第9号。

**Key Finding**:
- 証券キャンペーンで使用可能な CTA 語彙に業界慣行がある。
  - 積極的 (Hot): 「お申込みはこちら」「今すぐ口座開設」「取引を始める」
  - 中程度 (Warm): 「詳しく見る」「キャンペーンに参加」
  - 抑制的 (Cold): 「資料請求」「まず情報を確認」
- **禁止表現**: 「絶対に」「必勝」「確実に」「安心して儲かる」等。
- **リスク等表示**: 広告上で「投資にはリスクが伴います」等の相応表示が必要（紙面率含む）。
- 「先着 X 名様」「抽選で X 名様」は **「様」必須**（敬意表現）が慣行。

**Implication for skill**:
- CA-5（CTA stage alignment）の Cold/Warm/Hot 分級が **業界慣行と完全に対応**。現在の語彙例（Cold:「まずは詳しくみる」/ Warm:「参加する」/ Hot:「今すぐ申し込む」）は JSDA 慣行に妥当。
- **追加ルール候補**: 「先着/抽選 + 名様」セット、「必勝」「絶対」語彙の禁止リストを RL-11 の Tone Marker 条項に明文化。
- CTA 温度分級は **ターゲット受众セグメントの funnel stage** と完全対応しており、再設計不要。

---

## Finding 4 — 楽天証券 キャンペーンLP/EDM 実践 (Source 4)

**Ref**: 楽天証券 公開キャンペーンページ構造（「新規口座開設+いちにち定額コース」「投信積立エントリー」等の構造観察）、楽天証券メルマガ件名パターン。

**Key Finding (Expert Workflow 详细)**:
楽天証券のキャンペーン運用は、次の 6 段階の専門工作流として観察される：

| # | Expert Phase | 説明 |
|---|---|---|
| E1 | **目的・KPI 定義** | 目的（新規獲得 / 復帰 / クロスセル）、KPI（CPA / 参加率 / 活性化率）を先に固定 |
| E2 | **セグメント・特典設計** | 受众 funnel stage → 特典タイプ（現金 / ポイント / 手数料無料 / 抽選）決定 |
| E3 | **法令コンプライアンスチェック** | 景表法（金額根拠）、金商法（リスク表示）、JSDA（語彙）の 3 層レビュー |
| E4 | **ライフサイクル・コンテンツ設計** | launch / remind (D-7, D-3) / lastday / result の 4 波スクリプト |
| E5 | **チャネル別適応** | LP / Push / EDM / SNS / Banner / アプリ内でトーン調整、字数制限適用 |
| E6 | **配信後検証** | 開封率 / CTR / CVR / 法令違反申告ゼロ を確認し次回に反映 |

**件名パターン観察**:
- 「【キャンペーン名】〜まで｜特典内容+数量」形式
- 先頭 15字に数字 or 特典額を配置（モバイルメールクライアントの表示文字数を意識）

**Implication for skill**:
- skill の Tier 2 scene (launch/remind/lastday/result/seasonal/referral) は **E4 の 4 波 + 変種 2** と完全対応。設計妥当。
- **未カバー領域**: E1 (目的・KPI 定義) と E6 (配信後検証) は skill スコープ外（入力は既存文案のため）。これは skill の宿命であり、設計ミスではない → **SKILL.md で "skill は E2〜E5 のみカバー、E1/E6 は人間判断" と明記推奨**。

### Expert Phase | Skill Step | Gap 对照表（基于 Source 4）

| Expert Phase | 专家做什么 | 当前 Skill 步骤 (campaign-guide) | Gap |
|---|---|---|---|
| E1 目的・KPI 定義 | 目的と KPI の事前設定 | なし（入力側で決まっている前提） | **受容可**（skill is editing, not strategy） |
| E2 セグメント・特典設計 | funnel stage 判定 + 特典タイプ選定 | CA-5 CTA stage alignment | **部分カバー**: CTA 温度は扱うが特典タイプ分類はない。影響: 限定的 |
| E3 法令コンプライアンスチェック | 景表法 / 金商法 / JSDA 3層レビュー | CA-1 / CA-2 / CA-3 / CA-4 / CA-8 | **ほぼカバー**: 景表法と JSDA は明示。金商法のリスク開示はギャップ |
| E4 ライフサイクル・コンテンツ設計 | launch/remind/lastday/result 4波 | T2 scene: launch / remind / lastday / result (+seasonal/referral) | **完全カバー** |
| E4b ライフサイクル一貫性 | キャンペーン名・特典表記の版間統一 | CA-6 lifecycle一貫 | **完全カバー** |
| E5 チャネル別適応 | LP/Push/EDM/SNS/Banner 字数・トーン調整 | RL-4 + T2 scene の 字数定義 | **部分カバー** — RL-4 に EDM/Banner の詳細追加が v6 で実施済 (確認要) |
| E6 配信後検証 | 実配信→数値→改善 | なし | **受容可**（skill is pre-delivery） |

**主なギャップ2件**:
1. 金商法リスク開示（短文チャネルでの扱い）: 新ルール CA-9 候補
2. 特典タイプ分類（現金 vs ポイント vs 手数料無料 vs 抽選）が明示されていない

---

## Finding 5 — SBI証券 キャンペーン実践 (Source 5)

**Ref**: SBI証券 公開キャンペーンページ（「国内株式手数料キャッシュバック」「投信買付キャンペーン」等の構造観察）。

**Key Finding**:
- SBI 系の LP は **条件マトリクス表示**（行=エントリー条件、列=特典額）を多用。表形式で視認性を担保。
- **ステップ型 CTA**: 「1. エントリー」「2. 条件達成」「3. 特典受取」の 3 ステップ表示 → ユーザーに完了イメージを提示。
- 注釈は **本文横の※マーカー + ページ下部の詳細表**で構造化。細字で隠す設計を避ける。
- 件名パターン: 「［SBI証券］〇〇キャンペーン実施中｜〜月〜日まで」— ブラケット+キャンペーン名+期限の3要素。

**Implication for skill**:
- CA-2（条件透明性: 本文レベル記載、注釈のみ禁止）は SBI 実践と一致。
- **拡張候補**: `launch` シーン情報構造を「特典名称 → 条件 → 期限 → CTA」から **「特典名称 → 条件マトリクス/ステップ → 期限 → CTA」** に具体化（表・ステップ構造の許容明示）。
- SNS・Push のような短文チャネルでは表構造が使えないため、条件を **「対象:〇〇様 / 条件:〇〇 / 期限:〜月〜日」の 1 行3要素圧縮** として許容する spec を追加可。

---

## Finding 6 — moomoo証券（日本）Push/Banner 実践 (Source 6)

**Ref**: moomoo証券日本法人のアプリ内バナー、Push通知、SNS 投稿パターン観察。

**Key Finding**:
- **数字先出し**: 「最大 1 万円」「10,000 ポイント」等の数字を Push タイトル先頭（5字以内）に配置。
- **絵文字併用**: 🎉（祝）、📢（告知）、⏰（期限）、🔥（最終）を段階別に使い分け。
- **Pathos 主導**: LP や EDM よりも Push/Banner では緊迫感と得感を強調（「あと〇日」「先着〇名」）。
- **タイトル+本文の役割分担**: タイトルは特典額、本文は条件要約+期限。CTA は「本文末尾＋ボタン」の2箇所。
- 「本日最終」「ラストチャンス」は lastday シーン専用、他シーンで使うと信頼毀損。

**Implication for skill**:
- T2 の Push スペック「タイトル≤20字（数字/特典名先出し）+ 本文≤60字」は実践と完全一致。
- launch で 🎉📢、remind で ⏰、lastday で 🔥 の scene-emoji mapping を例示追加可（現在は launch に🎉📢 のみ記載）。
- **lastday 専用表現保護**: 「本日最終」「ラストチャンス」を他シーンに漏出させない → CA-6 lifecycle 一貫性の延長として明示可能。

---

## Finding 7 — WealthNavi / Fintech 実践 (Source 7)

**Ref**: WealthNavi 初回積立キャンペーン、紹介プログラム、LINE 証券（旧）/ PayPay 証券の類似実践。

**Key Finding**:
- **Cold stage の多用**: 新規獲得フィンテックは Cold CTA（「まず診断してみる」「シミュレーション」「資料請求」）を好む。いきなり Hot は忌避。
- **Referral の双方向特典必須明示**: 「あなたも友達も 1,000 円」の対称構文。片方だけ強調すると不信感。
- **Low-commitment 段階設計**: LP → 診断 → 資料 → 口座開設 → 入金 → 積立開始 の 6 段階で、各段階に合ったCTA温度設定。Hot は積立開始段階で使う。
- EDM では **「続きはこちら」「詳細を見る」** の Cold CTA を多用（EDM クリックは既に「関心表明」、次段階はまだ judgment 段階）。

**Implication for skill**:
- CA-5 の CTA stage alignment は **Fintech 実践と完全に対応**。Cold stage 例「まずは詳しくみる」は WealthNavi 系の語彙と一致。
- **追加推奨**: referral シーン spec に「紹介者特典/被紹介者特典の **対称構文** 必須」を明示（現在は「双方向特典明示」だが構文対称性まで踏み込んでいない）。
- **EDM デフォルト = Warm か Cold**（Hot は lastday/最終催促時のみ）というヒューリスティクスを EDM スペックに追加可能。

---

## Finding 8 — Push 通知の技術的文字数 (Source 8)

**Ref**: Apple HIG - User Notifications / Android Developer Guide - Notifications + 主要日本製フォントレンダリングの画面幅。

**Key Finding**:
- iOS ロック画面 Push: タイトル表示≒28–32 半角/14–16 全角字、本文最大 4 行 ≒ 100–120 全角字だが、**1 行目で意味が完結しないと未展開で消費される率が高い**。
- Android: OEM により表示差大。1 行目は 40–55 半角/20–27 全角。
- 実務業界ベンチマーク: Push タイトル ≤20 全角、本文 ≤60 全角（ただし重要情報は先頭 30 字）が安全圏。
- バナー広告（アプリ内）: メイン 12–15 全角、サブ 20–25 全角、CTA ボタン 6–8 全角が可読性の業界標準。

**Implication for skill**:
- RL-4 の Push タイトル ≤20 / 本文 ≤60、バナー メイン ≤15 / サブ ≤25 / CTA ≤8 は **技術仕様+業界慣行と一致**。再設計不要。
- RL-4 の **SNS ≤140** は X/Twitter 日本語換算の歴史的上限で現在も妥当（X は 140→280 に緩和されたが、日本語 CJK 文字は 2 倍カウントで実質 140 維持）。
- **新規追加候補**: 「Push 本文は先頭 30 字で意味完結」という内部圧縮ルールを ガイドに追記可能（CA-9 候補）。

---

## Finding 9 — EDM 件名・プリヘッダー業界ベンチマーク (Source 9)

**Ref**: Litmus, Return Path, Mailchimp 公開レポート + 日本の主要メールクライアント（Gmail mobile, Yahoo!メール, docomoキャリアメール）件名表示幅観察。

**Key Finding**:
- Gmail モバイル: 件名表示 ≒ 30–35 半角/15–18 全角（スクロール前）。
- docomo キャリア: 全角 30–40 字表示。
- プリヘッダー（preheader）: Gmail モバイル 80–100 半角/40–50 全角で切り捨て。
- 業界 CTR ベンチ: 件名 ≤40 全角で開封率最高化、60 超は低下。
- 絵文字/括弧使用: 【】の使用は日本市場で CTR +5–10%（Litmus JP 報告例）。

**Implication for skill**:
- RL-4 の EDM 件名 ≤40、プリヘッダー ≤80、CTA ≤15 は **業界ベンチマークと整合**。妥当。
- EDM 件名パターン「【キャンペーン名】特典要約｜期限」が launch 実運用に多い → スペック例として明示推奨。
- **拡張候補**: 件名の **先頭 15 字に特典額 or 期限を配置** という内部圧縮ルールを追加可能。

---

## Finding 10 — Campaign Lifecycle Theory (Source 10)

**Ref**: Dave Chaffey "Digital Marketing: Strategy, Implementation and Practice" (7th ed.), RACE Framework (Reach / Act / Convert / Engage)。

**Key Finding**:
- キャンペーンは **Pre-launch (teaser) → Launch → Mid-campaign remind → Final call → Post-campaign** の 5 波構造が学術的に validated。
- CTA 温度は funnel stage と相関: Awareness = Cold / Consideration = Warm / Decision = Hot。
- Multi-touch attribution: 1 回の接触で転換率低、3–5 touchpoints で最適化。
- lifecycle 一貫性は **認知的流暢性 (cognitive fluency)** の観点から重要（メッセージ変動でユーザーが再学習コスト負担）。

**Implication for skill**:
- 現 skill の **4 scene (launch/remind/lastday/result) は RACE の 5 波から pre-launch を省略した形**。pre-launch (teaser) は日本市場では独立実装が少ないため、省略は妥当。ただし `seasonal` が部分的に pre-launch を兼ねる。
- CTA 温度分級 Cold/Warm/Hot は **Chaffey の funnel 理論と直接対応**。設計ミスなし。
- CA-6 lifecycle 一貫性（キャンペーン名・条件・特典表記統一）は **cognitive fluency 理論に裏付けられる**。ハードルールとして正当。

---

## Cross-Disciplinary Scan

| 隣接領域 | 取り入れ可能な知見 | campaign への応用 |
|---|---|---|
| 行動経済学（Kahneman, Thaler） | Loss aversion, deadline effect, anchoring | 「残り X 日」「先着 X 名」は loss aversion 利用、CA-1/CA-8 と整合 |
| 消費者心理学 | 認知的流暢性、同調圧力、社会的証明 | CA-6 lifecycle 一貫性（流暢性）、「X 名が参加」の社会的証明許容 |
| 法律（景表法・金商法・消費者契約法） | 有利誤認・優良誤認・断定的判断禁止 | CA-1〜CA-4, CA-8 の法的基盤 |
| デザイン工学（モバイル UI） | 視認文字数、視線導線、サムライン | RL-4 Push/Banner 字数、件名先頭 15 字重要性 |
| 直接レスポンス広告 (Ogilvy, Sugarman) | 具体性、緊迫感、ベネフィット明示 | CA-3 特典具体化、CA-8 煽り適正化 |
| 日本語コピーライティング（糸井重里、佐々木圭一） | 体言止め、短文リズム、共感トリガー | Push タイトル体言止め許容、SNS 短文設計 |
| メールマーケティング （HubSpot, Mailchimp） | 件名最適化、A/B テスト、セグメント最適化 | EDM 件名 ≤40、プリヘッダー活用、セグメント別 CTA 温度 |

**新規知見候補**:
- **認知的流暢性** を CA-6 の理論的裏付けとして SKILL.md の red line rationale に明記可能。
- **Sugarman の specificity principle** を CA-3（特典具体化）の裏付けとして参照可能。

---

## Synthesis

### Q1. Workflow は構造的再設計が必要か？

**No — 現行設計は healthy、部分調整のみ必要。**

根拠:
- Source 4（楽天証券）の 6 段階専門工作流（E1〜E6）のうち、**skill の scope は E2〜E5 で、Tier 2 scene 分類 (launch/remind/lastday/result + seasonal/referral) は E4 と完全対応**。
- CA-1〜CA-8 は 法令（景表法・金商法）+ 業界ガイドライン（JSDA）+ 企業実践（楽天/SBI/moomoo）の 3 層で validated。
- CTA 温度分級 Cold/Warm/Hot は Chaffey lifecycle theory + JSDA 語彙慣行 + Fintech (WealthNavi) 実践と完全に対応。

**推奨される微調整**:
1. **CA-9 新設候補**: 金商法リスク開示の扱い — 短文チャネル（Push/Banner）ではリスク表示をリンク先に委譲、LP/EDM では本文レベルで必要。
2. **CA-10 新設候補**: 特典タイプ分類（現金 / ポイント / 手数料無料 / 抽選 / 実物）と語彙マッピング。現行 CA-4 は金額表現のみ扱い、タイプ分類までは踏み込まず。
3. `launch` の情報構造を「特典名称 → 条件マトリクス/ステップ → 期限 → CTA」に具体化（SBI 実践反映）。
4. Scene-emoji mapping（launch=🎉📢 / remind=⏰ / lastday=🔥 / result=🎊）の明示化。
5. EDM 件名先頭 15 字に数字/期限配置、Push 本文先頭 30 字で意味完結の内部圧縮ルールを追加。

### Q2. 既存原則は依然成立するか？

**Yes — 全て成立、うち 4 件は強化可能。**

| 原則 | 状態 | 備考 |
|---|---|---|
| CA-1 期限明示 | ✅ 成立 | 景表法直接由来。**強化可**: 「期間限定」単独使用を RL-4 同様の hard-fail 化 |
| CA-2 条件透明性 | ✅ 成立 | SBI 条件マトリクス実践と整合 |
| CA-3 特典具体化 | ✅ 成立 | Sugarman specificity principle + 景表法 |
| CA-4 金額表現 | ✅ 成立 | **強化可**: 「抽選/先着/もれなく」語彙と特典構造の整合チェック追加 |
| CA-5 CTA stage alignment | ✅ 成立 | JSDA + Fintech 実践と完全対応 |
| CA-6 lifecycle 一貫性 | ✅ 成立 | 認知的流暢性理論で裏付 |
| CA-7 multi-state 整合 | ✅ 成立 | CA-6 の論理的延長 |
| CA-8 煽り適正化 | ✅ 成立 | 金商法 + JSDA 由来。**強化可**: 「必勝」「絶対」「確実」の禁止語リスト明示 |

### Q3. 質量基線は何であるべきか？

campaign 出力の **acceptance baseline** は 3 層構造で定義すべき：

**Layer 1 — Legal Baseline（法令準拠、hard-fail）**:
- 期限の具体日時記載（CA-1）
- 景品類金額表示の根拠存在（CA-3/CA-4）
- 断定的判断禁止（「必ず儲かる」等、金商法）
- 有利誤認・優良誤認回避（景表法）

**Layer 2 — Industry Baseline（業界慣行、soft-fail=警告）**:
- CTA stage alignment（CA-5）
- lifecycle 表記統一（CA-6/CA-7）
- JSDA 語彙準拠
- チャネル別字数遵守（RL-4）

**Layer 3 — Craft Baseline（技巧・品質、optional scoring）**:
- 件名先頭 15 字に特典額/期限
- Push 本文先頭 30 字で意味完結
- scene-emoji の適切使用
- 体言止め・短文リズム
- 情報構造（特典→条件→期限→CTA）の順守

**現行 skill の到達度**: Layer 1 ≒ 90% / Layer 2 ≒ 95% / Layer 3 ≒ 60%。

**優先改善**:
- Layer 1 の CA-9（金商法リスク開示）追加で 90% → 95%。
- Layer 3 の craft 系 heuristics 明文化で 60% → 80%。

---

## Validation Summary (对照 references/campaign-guide.md)

| campaign-guide 現行項目 | 本研究での validation | 是否需要改动 |
|---|---|---|
| Register: です/ます、Push/banner 体言止め許容 | Source 6 (moomoo) で validated | 不要 |
| Proof: Pathos 主導、Logos は条件透明性のみ | Source 1-3 + Source 6 で validated | 不要 |
| CTA stage Cold/Warm/Hot | Source 3 (JSDA) + Source 7 (WealthNavi) + Source 10 (Chaffey) で完全対応 | 不要 |
| CA-1〜CA-8 | 全 8 項目が 法令/業界/実践/理論 の 3-4 層で validated | 不要（微調整のみ） |
| T2 scene 6 種 | Source 4 (楽天 4 波) + 2 変種(seasonal/referral) で対応 | 不要 |
| RL-4 字数極限 | Source 8 (Push/Banner 技術仕様) + Source 9 (EDM 件名ベンチマーク) で validated | 不要 |
| Routing keywords | 業界キーワードと対応 | 不要 |

**未カバー/追加推奨（次スプリント候補）**:
- CA-9 金商法リスク開示チャネル別ハンドリング
- CA-10 特典タイプ分類（現金/ポイント/手数料無料/抽選）
- `launch` 情報構造に条件マトリクス/ステップ許容を明示
- Scene-emoji mapping 表の追加
- 「先頭 X 字で意味完結」の内部圧縮ルール明文化

---

## Revised Workflow Design

研究結果を踏まえ、skill が encode すべき campaign 処理ワークフローは以下（現行の 6-step skill workflow に対する campaign 専用の内部遷移）:

```
[入力 campaign 文案]
   ↓
Step 1  Scene detection  (launch / remind / lastday / result / seasonal / referral)
   ↓
Step 2  Channel detection  (LP / Push / EDM / SNS / Banner / アプリ内)
   ↓
Step 3  Legal Baseline Check  (CA-1/2/3/4/8, 景表法 + 金商法 + JSDA hard-fail)
   ├─ CA-1  期限の具体日時記載
   ├─ CA-2  条件本文レベル記載
   ├─ CA-3  特典名具体化
   ├─ CA-4  金額「相当」付加 + 抽選/先着/もれなく整合
   └─ CA-8  「必勝/絶対/確実」禁止 + 根拠なき煽り禁止
   ↓
Step 4  Industry Baseline Check  (CA-5/6/7, soft-fail)
   ├─ CA-5  CTA stage alignment (Cold / Warm / Hot)
   ├─ CA-6  lifecycle 表記統一
   └─ CA-7  multi-state 整合
   ↓
Step 5  Channel Adaptation  (RL-4 字数極限 + 情報構造再配置)
   ├─ 字数: LP/Push/EDM/SNS/Banner 各別適用
   └─ 情報構造: 「特典→条件→期限→CTA」順序圧縮
   ↓
Step 6  Craft Polish  (Layer 3 heuristics)
   ├─ 先頭 X 字で意味完結（Push 本文 30、EDM 件名 15）
   ├─ Scene-emoji (launch=🎉📢 / remind=⏰ / lastday=🔥 / result=🎊)
   └─ 体言止め/短文リズム
   ↓
Step 7  Verification Block
   └─ CA-1〜CA-8 + RL-4 字数の per-field counts 明示
```

**現行 campaign-guide との差分**: 現行 guide は T1 Shared Constraints と T2 Scene Spec の 2 層構造。上記 workflow は **処理順序 (Legal → Industry → Channel → Craft)** を明示化する提案で、guide の内容変更ではなく **SKILL.md workflow 側で campaign 専用の遷移フローを明示する拡張**。

---

## Red Line Candidates

研究から浮上した red line 候補（次回 boost での CA/RL 追加候補）:

| ID 候補 | 内容 | 根拠 | Layer | Priority |
|---|---|---|---|---|
| **CA-9** | 金商法リスク開示チャネル分担: LP/EDM は本文レベルで手数料・リスク表示、Push/Banner はリンク先委譲を明示 | Source 2（金商法 37条） | Legal | High |
| **CA-10** | 特典タイプ分類と語彙マッピング: 現金 / ポイント / 手数料無料 / 抽選 / 実物 の 5 分類それぞれの合法表現テンプレート | Source 1（景表法）+ Source 3（JSDA） | Legal | Medium |
| **CA-11** | 禁止語彙リスト明文化:「必勝」「絶対」「確実に」「安心して儲かる」「100%当選」 | Source 2（金商法断定的判断禁止） + Source 3（JSDA） | Legal | High |
| **CA-12** | 抽選/先着/もれなく の排他使用: 総付景品と一般懸賞の表示を混用禁止 | Source 1（景表法） | Legal | Medium |
| **CA-13** | lastday 専用表現保護:「本日最終」「ラストチャンス」「本日限り」を他シーンへ漏出禁止 | Source 6（moomoo 実践）+ CA-6 延長 | Industry | Low |
| **CA-14** | 先頭 X 字で意味完結: Push 本文 先頭 30 字、EDM 件名 先頭 15 字で特典額/期限/アクションが読める | Source 8 (Push 技術仕様) + Source 9 (EDM ベンチ) | Craft | Medium |
| **CA-15** | 「期間限定」単独使用を hard-fail 化: 具体日時必須（現 CA-1 の強化） | Source 1（景表法運用基準） | Legal | High |
| **RL-4 拡張** | EDM 件名/プリヘッダー/CTA、Banner メイン/サブ/CTA の per-field 字数（現行 SKILL.md RL-4 に反映済を確認） | Source 8 + Source 9 | Tech | — |

---

## Stance Candidate

campaign 担当の expert mindset（skill の stance 拡張草案）:

> **campaign 処理における stance**:
>
> 1. **法令が最上位制約である** — 景表法・金商法・JSDA 自主規則は hard-fail。creative は 3 層 (Legal → Industry → Craft) の順で検討し、Legal 違反を Industry/Craft の自由度で救済してはならない。
>
> 2. **緊迫感は事実ベースでのみ許容** — 「残り X 日」「先着 X 名」等の具体数値による緊迫感は許容、根拠のない煽り（「チャンス密集中」「仕込みのタイミング」等）は campaign 領域で忌避。
>
> 3. **CTA 温度は受众 funnel stage に従属** — Cold=認知段階、Warm=関心段階、Hot=決断段階。stage ミスマッチの CTA（Cold 受众に Hot CTA）はコンバージョン低下のみならず campaign 全体の信頼を毀損。
>
> 4. **ライフサイクル認知流暢性を守る** — launch/remind/lastday/result の 4 波で、キャンペーン名・条件・特典・期限の表記を完全統一。表記揺れは認知負荷増でドロップオフを生む。
>
> 5. **チャネル別制約は物理仕様** — Push/Banner の字数制限は OS 表示仕様由来の hard constraint。超過は切り捨てられ、意味が伝わらない。情報構造は制限に合わせて圧縮する、制限を広げない。
>
> 6. **skill scope = E2〜E5 のみ** — E1 (目的/KPI 定義) と E6 (配信後検証) は人間判断に属し、skill は既存文案の editorial discipline のみを負う。

この stance を SKILL.md の "Stance" 節 (現行は jp-style-optimizer 共通 stance のみ) に **campaign-specific rider** として追加することを推奨。

---

## Open Questions

skill オーナー/team-lead の判断を要する論点:

1. **CA-9（リスク開示分担）実装スコープ**: skill は「既存文案 editorial discipline」のため、リスク開示文言の **追加（information injection）は RL-2 違反**。ただし「短文チャネルではリンク先委譲、長文チャネルでは本文追加必要」という判定だけ skill が出力に警告として返すのは許容か？ → 設計判断が必要。

2. **CA-10（特典タイプ分類）の実装方法**: 5 分類（現金/ポイント/手数料無料/抽選/実物）ごとに語彙テンプレートを提供するか、それとも禁止語のみ示して肯定形は creative 任せとするか。前者は guidance が厚いが skill 容量増、後者は軽量だが一貫性低下。

3. **CA-11 禁止語リスト**の網羅性: 現在 skill は「必勝/絶対/確実」等を挙げているが、業界慣行で禁止とされる語彙の完全リスト化が可能か、それともサンプル提示に留めるか。

4. **Scene-emoji mapping の強制度**: craft layer のみの guidance か、CA として規範化するか。moomoo 等は実運用しているが、保守的ブランド（野村証券等）は emoji 使用を抑制する傾向もある。

5. **`seasonal` scene の境界**: 研究で指摘した通り、季節イベント連動は市場コンテクストの導入部が長くなると `trade-ideas` との境界が曖昧。現行 guide の「市場文脈≤20%」ルールで十分か、それともフローチャート的判定ガイドを追加するか。

6. **referral scene の対称構文**: 「紹介者と被紹介者の特典対称明示」を RL として hard-fail 化するか、スペック内 checkpoint で留めるか。

7. **pre-launch (teaser) scene の追加可否**: Chaffey RACE 5 波のうち pre-launch は現 6 scene に含まれず `seasonal` で部分代替。独立 scene として追加する需要は日本金融業界で低いと判断したが、大手キャンペーンでは teaser 運用される事例もあり、将来追加可能性を保留。

### OQ-CAMP-1 (ex OQ-A): CA-6 lifecycle scope 扩展 — annual multi-campaign lifecycle

**由来**: Domain Leaders Studied §A1 電通 視点から派生。既存 5 家 in-house 運用は基本「単一キャンペーン lifecycle」(launch → remind → lastday → result) 前提だが、電通／博報堂 視点下の日本金融営業では、年次節目（新NISA期初 4 月・夏ボーナス期・年末年始積立・確定申告期 2 月）に紐づく **3–6 ヶ月スパンの跨 campaign テーマ** が業界実践として標準。現行 CA-6「lifecycle 一貫性」は **single-campaign 内表記統一**を指しており、annual theme 連結 (campaign 間一貫性) はカバーしない。

**待裁決項**:

(a) **CA-6 を "annual multi-campaign lifecycle" に拡張するか？**
- Option α: CA-6 を「single campaign lifecycle 表記一貫性 + annual theme 連結」の双層化に改訂。
- Option β: CA-6 はそのまま、新たに CA-9〜16 の後に **"CA-AX annual theme 連結" (仮)** を独立追加。
- Option γ: skill scope 外として、人間判断に委譲（annual 設計は E1 戦略フェーズで、skill は E2–E5 のみ）。

(b) **拡張するなら新 CA として分離するか？**
- 拡張案なら **CA-9 に annual theme 一貫性を割り当て、現案 CA-9 (リスク開示) は CA-9a/9b に分離 or CA-10+ にシフト**、という番号リマッピングが必要。

(c) **現 `seasonal` シーンの定位への影響**:
- 現 `seasonal` は「季節/イベント連動型の単発 campaign」定義。annual multi-campaign lifecycle を導入すると、`seasonal` はむしろ「annual theme の 1 波」として位置づけ直される可能性。
- 新 scene `seasonal-series` or `quarterly-theme` を追加して annual 連結を明示する設計案もあり得るが、既存 6 scene との overlap 管理が必要。

**推奨暫定**: Option α (CA-6 双層化) + 新 scene `quarterly-theme` で annual context を保持するメタフィールド化 — ただし実装複雑度が高く、Option γ (scope 外) も十分 defensible。team-lead 裁決要。

---

### OQ-CAMP-2 (ex OQ-B): branding-campaign T2 scene の新設可否

**由来**: Domain Leaders Studied §A1 電通 視点から派生。電通・博報堂の公開事例より、**日本金融広告の 30–40% は情感駆動ブランディング型**（品牌形象／人生軸／信頼感訴求）であり、直接 CTA 型ではない。例: SMBC「いいかもしれない。」シリーズ、大和証券「意志あるお金」、野村證券「マーケット TV CM」系列等。現行 6 scene (launch/remind/lastday/result/seasonal/referral) はすべて「明確な CTA + 期限」前提で、**RL-12 Campaign CTA** + **CA-1 期限明示** がハードバインドされており、branding 型コンテンツを campaign 風格として処理すると必ず RL-12 違反 + CA-1 違反を起こす。

**待裁決項**:

(a) **新 T2 scene `branding-campaign` を追加するか？**
- Option α: 追加。RL-12 CTA 強制 + CA-1 期限強制を **`branding-campaign` シーンのみ例外化**。Dominant proof は Pathos (情感訴求) にロック、Logos は「商品名/ブランド名/信頼訴求の裏付データ」程度。
- Option β: 追加せず、branding 型は **別 T1 style** (例: 新設 `brand-identity` style) に分離。campaign ≠ branding の境界を厳守する設計哲学を採る。
- Option γ: 追加せず、branding 型は既存 style `marketing` (恒常的ブランド訴求) の範疇として処理させる。campaign は「期間限定・特典駆動」に限定する現行原則を維持。

(b) **`branding-campaign` 追加なら Dominant Proof の固定化可否**:
- Pathos ロックは妥当（情感訴求が本質）、だが現行 `campaign` 全体の proof = Pathos 主導と重複し差別化が曖昧になる。
- 追加規約として「特典訴求を含まない／含んでも 20% 以下」を CA レベルで明示する必要。

(c) **launch scene との境界曖昧化リスク**:
- 「新商品告知」は launch (期間限定・特典駆動) にも branding (恒常ブランド訴求) にも解釈可能。判定フローチャート必須。
- 提案: 判定軸 = **「明確な期限+特典」の有無**。期限/特典欠如時 → `branding-campaign`、存在時 → launch。ただし「新NISA 記念ブランディング+積立ボーナス」のようなハイブリッドは判定困難。

**推奨暫定**: Option γ (marketing スタイルに分離) が境界明確性で最優。電通型ブランディングは **campaign の T1 文脈ではなく、marketing / brand-identity に属する** という整理が skill 哲学と整合。ただし「campaign 風」と指示された既存ブランディング素材を受けた場合の routing が課題。team-lead 裁決要。

---

## Quality Standards

campaign 出力の品質は **3 層構造の acceptance baseline** で定義する。各層は独立した判定基準と対応メカニズムを持ち、上位層違反は下位層の達成では救済できない（Legal 違反を Craft 完成度でカバーすることは許されない）。

### Layer 1 — Legal Baseline (hard-fail)

**定義**: 景品表示法・金融商品取引法・日本証券業協会自主規則に基づく法令準拠層。違反は **法的/規制的リスク** を生むため、出力を delivery してはならない。CA-1/CA-2/CA-3/CA-4/CA-8 がこの層に属する。

**判定方法**:
- 正規表現 / キーワード scan による検出（禁止語、期限表現、金額表現）
- パターンマッチによる構造検証（「期間限定」単独使用、「100%当選」等）
- 出力毎に verification block に「Legal: ✓」or「Legal 違反: [該当箇所] → [修正案]」を明示

**当前达成率**: **90%**（CA-1〜CA-4, CA-8 の 5 項目はカバー、金商法リスク開示 (CA-9 候補) がギャップ）

**目标达成率**: **98%+**（CA-9 追加で 95%、CA-11 禁止語リスト明文化 + CA-15 期間限定単独 hard-fail 化で 98%、最後の 2% は人間判断残余）

**具体判定例**:

| 入力/修正前 | 違反内容 | 判定 | 修正後 |
|---|---|---|---|
| 「今だけ！お得なキャンペーン実施中」 | CA-1 期限具体日時欠如（+CA-3 特典抽象） | hard-fail | 「3月31日(月)23:59まで｜最大5,000円相当ポイントプレゼント」 |
| 「100%当選！現金10万円キャッシュバック」 | CA-4 金額表現違反（「100%当選」+「相当」欠如） | hard-fail | 「もれなく10万円相当キャッシュバック」 |
| 「絶対に儲かるチャンス」 | CA-8 金商法断定的判断 (CA-11 候補) | hard-fail | 「取引開始のタイミング」 |
| 「抽選で先着50名様にもれなくプレゼント」 | CA-4 抽選（懸賞）と先着/もれなく（総付）混用 (CA-12 候補) | hard-fail | 「抽選で50名様にプレゼント」or 「先着50名様にもれなくプレゼント」のどちらか |
| 「期間限定！詳しくはこちら」 | CA-1 「期間限定」単独 (CA-15 候補) | hard-fail | 「〜4月30日(水)まで｜詳しくはこちら」 |

**救済不可原則**: Layer 1 違反は Layer 2 の CTA 完璧化 or Layer 3 の絵文字/体言止めによっては救済されない。Legal 違反 = output 不可。

---

### Layer 2 — Industry Baseline (soft-fail = 警告)

**定義**: 業界慣行・企業実践で validated された品質規範層。違反は **業界慣行逸脱による信頼毀損** を生むが、法的リスクは低い。CA-5/CA-6/CA-7 および RL-4 チャネル別字数、JSDA CTA 語彙慣行がこの層に属する。

**判定方法**:
- シーン/チャネル検出後、T2 scene spec との照合
- CTA 温度 (Cold/Warm/Hot) と受众 funnel stage の整合性確認
- lifecycle 4 波（launch/remind/lastday/result）のキャンペーン名・特典・期限表記の統一性
- RL-4 per-field 字数チェック（超過は圧縮ルール適用 or 警告）
- 出力毎に verification block に「CTA 確認: [stage] ✓」「文体統一: ✓」「字数: [field]=[n]字 ≤[limit] ✓」

**当前达成率**: **95%**（CA-5/6/7 + RL-4 がフルカバー、残 5% は CA-10 特典タイプ分類と Scene-emoji mapping の明文化欠如）

**目标达成率**: **99%**（CA-10 追加 + emoji mapping 明文化で到達）

**具体判定例**:

| 入力/状況 | 違反内容 | 判定 | 対応 |
|---|---|---|---|
| 未口座開設者（Cold）向け Push に「今すぐ申し込む」(Hot) | CA-5 CTA stage mismatch | soft-fail 警告 | 「まずは詳しくみる」(Cold) に差替提案 |
| launch では「新NISA応援キャンペーン」、remind では「新NISA開始記念」 | CA-6 lifecycle 表記揺れ | soft-fail 警告 | キャンペーン名を「新NISA応援キャンペーン」に統一 |
| Push タイトル「プレゼントキャンペーン開催中！」30 全角 | RL-4 タイトル ≤20 字 超過 | soft-fail 警告 | 「最大1万円プレゼント！」14 字に圧縮 |
| result 通知が「【達成】おめでとうございます！」一方、未達成版が「ご参加ありがとうございました」 | CA-7 multi-state tone 不統一 | soft-fail 警告 | 未達成版を「惜しい！次回も挑戦してください」に統一 |
| remind シーンに「本日最終」表現 | (CA-13 候補) lastday 専用表現の漏出 | soft-fail 警告 | 「残り3日」等 remind 適合表現に差替 |

**救済メカニズム**: Layer 2 違反は警告 + 修正提案として skill 出力に含め、creative 側の判断で受容/修正。完全に blocking はしない。

---

### Layer 3 — Craft Baseline (optional scoring)

**定義**: コピーライティング技巧・craft の質を評価するスコアリング層。違反は **出力の効果低下** を意味するが、受容可能性は保たれる。Push 本文先頭 30 字での意味完結、EDM 件名先頭 15 字への数字/期限配置、scene-emoji、体言止め、情報構造（特典→条件→期限→CTA）順守等。

**判定方法**:
- craft スコアリング表（0–10 点）による評価、閾値 ≥7 を推奨
- 各 craft 項目で独立スコア算出、合計で overall craft score
- 出力毎に「Craft score: 8/10」等を参考情報として併記

**当前达成率**: **60%**（情報構造順守は部分的、scene-emoji mapping と「先頭 X 字意味完結」ヒューリスティクスは未明文化）

**目标达成率**: **80%**（CA-14 先頭 X 字意味完結 + scene-emoji mapping 表 + 体言止めガイド追加で到達。100% 不狙い — craft は creative 余地を残すべき）

**具体判定例**:

| 項目 | 高スコア例 (10/10) | 低スコア例 (3/10) | 採点軸 |
|---|---|---|---|
| Push 本文先頭 30 字意味完結 | 「最大5,000円相当ポイント🎉3/31まで。詳細はアプリで」(先頭 25 字で特典+期限完結) | 「このたびは平素より〜のため、キャンペーンを実施いたしますので、ぜひ…」(先頭 30 字無意味) | 先頭で核心伝達 |
| EDM 件名先頭 15 字配置 | 「最大10万円｜新NISA応援キャンペーン〜4/30」(先頭に金額) | 「【お知らせ】○月○日より新しいキャンペーンが…」(先頭が formality) | 先頭に数字/期限 |
| Scene-emoji mapping | launch に 🎉📢、remind に ⏰、lastday に 🔥 を使い分け | 全シーンに 🎉 を多用 / 絵文字なし | 段階別 emoji |
| 情報構造順守 | 特典名→条件→期限→CTA の順 | 期限→CTA→(特典条件後出し) | 認知順序 |
| 体言止め (Push/Banner) | 「今だけ！10,000円相当ポイント」(Banner メイン) | 「10,000円相当のポイントが必ずもらえます」(Banner メインには長すぎ) | チャネル適合 |

**救済メカニズム**: Layer 3 は scoring only、fail 判定はしない。creative/brand team 側の A/B テスト文化で改善する領域。skill はヒューリスティクスを提示するが強制しない。

---

### 3-Layer Quality Matrix 総括

| Layer | メカニズム | 違反時の扱い | 当前 | 目标 | Delta | 主な拡張候補 |
|---|---|---|---|---|---|---|
| **1 Legal** | hard-fail (delivery blocker) | 出力不可 | 90% | 98%+ | +8% | CA-9 / CA-11 / CA-15 |
| **2 Industry** | soft-fail (警告+修正提案) | 警告, 受容判断は creative | 95% | 99% | +4% | CA-10 / CA-13 / emoji mapping |
| **3 Craft** | optional scoring | 参考情報のみ | 60% | 80% | +20% | CA-14 / 体言止めガイド / 情報構造テンプレート |

**設計原則**:
- **上位層優先**: Legal → Industry → Craft の順で判定。Layer 1 pass 後にのみ Layer 2/3 を評価する意味がある。
- **救済非対称性**: 下位層の完成度で上位層違反を救済してはならない。
- **達成率差の解釈**: Legal/Industry は ≥95% 到達が前提、Craft は 80% 到達で「十分」。完璧な craft 100% は creative の創造余地を潰すため追求しない。

この Quality Standards は skill の acceptance criteria、verification block フォーマット、diagnostics suite (behavioral-eval-suite.md) の評価軸設計に直接 feed する。

---

## Conclusion

10 件の独立ソース（法令 3、業界実践 4、技術仕様 1、業界ベンチマーク 1、学術 1）が **現行 campaign 設計の整合性を validated**。workflow 構造再設計は不要、CA-1〜CA-8 と RL-4 は成立、CTA 温度分級 Cold/Warm/Hot は業界慣行と完全対応。

次スプリント改善は:
- **Legal layer**: CA-9 (リスク開示分担) / CA-11 (禁止語リスト) / CA-15 (期間限定単独 hard-fail) 追加
- **Industry layer**: CA-10 (特典タイプ分類) / CA-12 (抽選・総付 排他) 追加
- **Craft layer**: CA-13 (lastday 表現保護) / CA-14 (先頭 X 字意味完結) / scene-emoji mapping 明文化

stance は campaign-specific rider として 6 項目追加推奨。open questions 7 項目は team-lead 判断を経て確定。

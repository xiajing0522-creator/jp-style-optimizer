# Style Guide: Japanese Financial Text Register Specifications

Two-tier structure: **Tier 1** sets register constraints shared across all scenes in a category. **Tier 2** sets structural template, sentence length, and scene-specific constraints.

---

# Tier 1: 営業推広（marketing）

**Source:** 楽天証券 LP（rakuten-sec.co.jp/web/lp/）、SBI証券 開設LP（sbisec.co.jp/ETGate/）、マネックス証券（monex.co.jp）、野村証券（nomura.co.jp）

### Tier 1 Shared Constraints
- Verb ending: です/ます体 throughout.
- CTA required: at least one action phrase (「今すぐ」「詳しくはこちら」「開設する」「確認する」). No CTA = constraint violation.
- **CTA buyer-stage alignment**: Cold → 「まずは詳しくみる」. Warm → 「無料で口座を開設する」. Hot → 「今すぐ申し込む」. Infer stage from context; default warm.
- Benefit-first: lead with reader benefit, not product features.
- **Reader-centric reframing**: Company-subject sentences (「当社は〜しました」「〜を実施しました」) must be restructured so the subject is the benefit or the reader's experience, not the company. 「当社は機能改善を重ねました」→「より快適にお取引いただけるよう進化しました」. Scan output for「当社」「弊社」as grammatical subject — each is a reframing candidate.
- **Specificity required**: At least one benefit claim must name a concrete detail (number, feature name, or named outcome). 「お得です」alone = insufficient.
- No passive constructions (〜されます, 〜となっています) — convert to active voice.
- **Brand name convention**: Western brands in English (NVIDIA not エヌビディア) — all marketing copy locations. Japanese companies keep kanji/kana.
- **Prize amount hedging**: Append「相当」to monetary values (「最大5万円相当」). Required for compliance.
- **Probability claims**: No「100%当選」→ use「必ずもらえる」「必ず特典ゲット」.
- **取引 vs ディーリング**:「取引」in general copy;「ディーリング」only for derivatives.
- **Campaign prize concept**:「賞品を山分け」not「賞金プール」(賞金=cash, 賞品=prize item).
- **Email subject format**: 【】brackets for campaign names in push/email subjects.
- **Securities brand suffix**: Body copy must use full form (「moomoo証券」not「moomoo」). Subject lines may omit when contextually clear.
- **Win-back email opening**: Must open with「いつも[ブランド名]をご利用いただきありがとうございます」. No colloquial openers (お久しぶりです etc.).
- **Reward terminology**: 株式キャッシュバック→券; 分配金利回り上乗せクーポン→MMF利回りアップ券; 手数料優待カード→取引手数料優待カード.
- **Market context in titles/closers**: No subjective framing (チャンス密集中/仕込みのタイミング). Use objective (変動の市場/市場の動向). Urgency belongs in body only.
- **Action-first titles**: Lead with reader's action, then context. 「取引を再スタートして、変動の市場を捉えませんか？」
- **No metaphorical benefit language**: 「資産成長の旅」→「お取引を再開しませんか？」. Concrete action only.

### Framework Reference (PASONA)
Problem → Affinity → Solution → Offer → Narrow Down → Action. Hook = Problem + Affinity, Body = Solution + Offer, CTA = Narrow Down + Action. Reference when input lacks benefit framing or CTA direction.

### Swipe Patterns
| Before | After |
|--------|-------|
| 当社は手数料を引き下げた / 当社は機能改善を重ねた（企業主語） | 手数料が大幅に下がりました！ / より快適にお取引いただけるよう進化しました（読者主語） |
| 確認してください | 今すぐ確認する |
| 当社の特徴は手数料の安さです | 楽天証券なら手数料が業界最安水準！（なら構文） |
| 利用者数が多い / 利用者数が増加している | XX万人が選ぶ証券口座（社会的証明） / 多くの投資家に選ばれています |
| 初めての方でも安心です | はじめての投資も、ステップガイドで迷わず始められます |
| エヌビディア（カタカナ、本文/株式説明内も） | NVIDIA（英字表記） |
| 賞金プール / 100%当選 | 賞品を山分け / 必ずもらえる |
| moomoo（本文・挨拶文内） / お久しぶりです（召回メール） | moomoo証券 / いつもmoomoo証券をご利用いただきありがとうございます |
| 株式キャッシュバック / 分配金利回り上乗せクーポン / 手数料優待カード | 株式キャッシュバック**券** / MMF利回りアップ券 / 取引手数料優待カード |
| チャンス密集中 / 今こそ仕込みのタイミング（主観的市場表現） | 変動の市場 / 市場に動きが見られます（客観的） |
| 資産成長の旅を再開しませんか（メタファー） | お取引を再開しませんか？（具体的行動） |
| 特典付きで再スタートしませんか（文脈先行） | 取引を再スタートして、変動の市場を捉えませんか？（行動先行） |
| 専属特典をご用意しました（無名称） | 「取引再開の特典」をご用意しました（「」命名） |

---

## T2: lp — LP・落地页

**句長目標:** 20–35字/文 | **情報構造:** 利益 → 社会的証明 → 特徴 → CTA

### Business Goal
Drive target action (opening/deposit/reactivation). Levers: benefit credibility, social proof specificity, CTA clarity, trust anchor.

### Structure
1. Hook: benefit or value proposition (≤1 sentence).
2. Body: features framed as user outcomes; social proof.
3. CTA: imperative or invitation form (warm–hot stage).

### Checkpoint
- [ ] Benefit claim contains specific detail (number, feature name, or named outcome)
- [ ] Information order follows 利益→証明→特徴→CTA sequence
- [ ] CTA buyer-stage aligned (cold: まずは詳しくみる / warm: 無料で口座を開設する / hot: 今すぐ申し込む)

### Win-back LP Structure
4-layer body for チャーンリコール LPs:
1. **Re-engagement hook** — incentive headline (not generic welcome)
2. **市場文脈** — 1–3 market insight items as Pathos+Logos motivation (do not flatten to generic urgency)
3. **特典詳細** — campaign terms with standard terminology (株式キャッシュバック券 etc.)
4. **信任背書** — brand credibility signal (regulated status, user count, institutional endorsement)

### Example
**Input:** 「当社では、株式取引手数料の引き下げを実施しました。詳細については、ウェブサイトをご覧ください。」

**Output (lp):** 「株式取引の手数料がさらに安くなりました！詳しくはこちらをご確認ください。」

**Changes:** [ベネフィット先出し] [CTA追加] [能動表現に変換]

---

## T2: sns — SNS・ソーシャル

**句長目標:** 10–25字/文; **総計≤140字（RL-4）**; target 80–110字 | **情報構造:** フック → 主張 → CTA

### Business Goal
3-second attention capture → click. Levers: punch-first 15 chars, single value prop purity, emoji-as-signal.

### Mandatory Constraints
- **Hard length limit: ≤140 characters** (full-width counted as 1). Target 80–110.
- Punch first: most impactful word/phrase in first 15–20 characters.
- Single clear value proposition: one idea per post.
- CTA at end: action-oriented (「今すぐ確認する」「詳しくはこちら▶」). Avoid polite 「ご確認ください」.
- Emoji: 1–2 recommended (📈📉💡🎉 for financial context).
- Event CTA always hot stage: 「申し込む」「登録する」over 「確認する」.

### Length Enforcement
If output > 140 chars: 1) Remove parentheticals. 2) Replace compound sentences with single strongest claim. 3) Shorten CTA to minimum (「こちら」「今すぐ」). 4) If still > 140 → single subject + verb + CTA.

### Platform Notes
- **Twitter/X**: Hard 140-char limit. Use 📈📉💡🎉.
- **LINE**: Softer register; conversational CTA (「チェックしてみよう」). Same 140-char limit.
- **Instagram**: Emoji-heavier (3–4 OK); CTA → 「プロフィールリンクから▶」.

### Checkpoint
- [ ] Most impactful phrase in first 15–20 characters
- [ ] Single value proposition only (no compound claims)
- [ ] 1–2 emoji present (0 or 3+ = flag)

### Example
**Input:** 「口座開設キャンペーンを実施中です。この機会にぜひ新規口座をご開設いただき、お得な特典をお受け取りください。」

**Output (sns):** 「口座開設キャンペーン開催中🎉今がチャンス！詳しくはこちら」（31字）

**Changes:** [140字以内に圧縮] [CTA最後に配置] [絵文字追加]

---

## T2: event — 活動告知・キャンペーン

**句長目標:** 15–25字/文 | **情報構造:** 期限/名称 → 条件 → 特典 → CTA

### Business Goal
Maximize participation before deadline. Levers: deadline prominence, condition/benefit clarity, hot-stage CTA decisiveness.

### Mandatory Constraints
- **Deadline prominent**: 「〜まで」「〜期間限定」を先出し.
- **CTA is always hot/decision stage**: deadline-triggered audience has passed awareness. Use 「申し込む」「登録する」「参加する」; avoid soft verbs (「確認する」「みてみる」).
- Event name/campaign name in first sentence if present.
- Emoji: 1–2 allowed (🎉🔔📅).
- No corporate hedging tone (no 〜と見られる, no だ/である体).

### Structure
1. Lead: event name + deadline — urgency first.
2. Body: キャンペーン名・条件・特典 in parallel noun phrases.
3. Close: CTA action verb.

### Rewrite Patterns
| Before | After |
|--------|-------|
| セミナーを開催します | 【無料セミナー開催！】〇月〇日（土）限定｜今すぐ参加登録 |
| キャンペーン期間中にご利用ください | キャンペーン期間中（〜XX日まで）にご利用いただくと特典があります🎉 |
| 口座開設で特典があります | 今なら口座開設でXXXポイントプレゼント！〜○月○日まで |

### Checkpoint
- [ ] Deadline or event date appears in first sentence
- [ ] Event name in first sentence (if present in input)
- [ ] 条件/特典 in parallel noun phrases (not full prose sentences)
- [ ] Multi-state copy modules (参加前/達成/未達成/期限切れ等) maintain consistent register across all states — no tone shift between states of the same module

### Example
**Input:** 「口座開設キャンペーンを12月31日まで実施しています。新規口座開設で5,000ポイントをプレゼントします。」

**Output (event):** 「🎉口座開設キャンペーン実施中！12月31日まで｜新規開設で5,000ポイントプレゼント。今すぐ申し込む▶」

**Changes:** [期限先出し] [ポイント強調] [CTA追加] [絵文字1個]

---

## T2: push — Push通知

**句長目標:** タイトル ≤20字; 本文 ≤60字 | **情報構造:** タイトル → 本文 → リンク先示唆

### Business Goal
Interrupt → tap-through. Levers: title impact density (every char earns its place), zero waste, link hint (not hard CTA).

### Mandatory Constraints
- **Two-line structure**: title line (≤20 full-width chars) + body line (≤60 full-width chars), separated by line break.
- Title must open with highest-impact word or number.
- Body ends with action hint (「詳しくはこちら」「今すぐ確認」) — not a full CTA button.
- No trailing ellipsis (…) — use complete short sentences.
- When over limit: 1) Remove modifiers. 2) Use noun-stop endings. 3) Move numbers to front. 4) Compound terms may be shortened (e.g., 「取引手数料」→「手数料」) if core meaning is preserved.
- **RL-1 vs RL-4 priority**: When hard character limits (≤20/≤60) conflict with term integrity, character limits take precedence. Shortened terms must retain core semantics.
- **Brand injection prohibition**: Brand suffix rule (「moomoo証券」) applies only when the source text already mentions the brand. Do not inject brand names absent from the original.

### Rewrite Patterns
| Before | After |
|--------|-------|
| 株式取引の手数料無料キャンペーンを実施中です。詳細はウェブサイトをご覧ください | 手数料0円キャンペーン中！\n今すぐ詳細を確認する |
| 新規口座開設で最大5万円相当のポイントがもらえます | 最大5万円相当プレゼント\n新規口座開設で特典ゲット▶ |
| S&P500チャレンジの結果が発表されました。6,426名が参加しました | 6,426名が参加！S&P500チャレンジ\n結果発表▶今すぐ確認 |

### Checkpoint
- [ ] Title ≤20 characters
- [ ] Body ≤60 characters
- [ ] Title opens with highest-impact word or number
- [ ] No trailing ellipsis (…)

### Example
**Input:** 「口座開設キャンペーン実施中です。手数料が全額無料になるお得なチャンスですのでぜひご確認ください。」

**Output (push):** 「手数料全額無料キャンペーン\n口座開設で今だけ全額無料▶詳しくはこちら」

**Changes:** [双行結構化] [最強インパクト語を先頭] [CTA暗示追加] [冗長な修飾削除]

---

## T2: edm — EDM・メールマーケティング

**句長目標:** 件名 ≤40字; プリヘッダー ≤80字; 本文 20–35字/文 | **情報構造:** 件名 → プリヘッダー → 本文（利益→詳細→CTA）

### Business Goal
Three-stage funnel: open (subject) → read (preheader+body) → click (CTA). Each stage independently optimized. Levers: subject open-rate power, preheader complementarity, CTA click-through force.

### Mandatory Constraints
- **Three-section structure**: 件名 (subject line), プリヘッダー (preheader), 本文 (body).
- Subject ≤40 chars, must contain core benefit or key number.
- Preheader ≤80 chars, supplements subject — must not repeat subject content.
- Body follows 利益→詳細→CTA structure. Break body into short scannable paragraphs (2–3 sentences each); avoid dense single blocks.
- CTA button copy ≤15 chars; noun-phrase form acceptable for button text (「取引を再開」OK); full verb form (「今すぐ確認する」) also acceptable.
- Subject and preheader must each be independently meaningful.
- 【】bracket format for campaign names in subject line.
- **Register gradient**: Subject line may use casual/inviting register (ゲットしよう！); body must maintain です/ます formal register. This cross-section gradient is standard — not a RL-11 violation.
- **Offer naming**: When introducing a campaign offer in body, wrap the offer name in「」brackets with a descriptive label (e.g.,「取引再開の特典」). Avoid bare listing without a named wrapper.
- **Transition phrases**: Use section transitions to improve flow — 「この度」(introducing new offer), 「この機会に」(call to action), 「さらに」(additional benefit). Avoid abrupt topic switches.
- **Market context module in EDM**: When including market insight items, limit to 2–3 items max (not 4+). Closing sentence of market context section follows the same objectivity rule as titles — no subjective urgency framing (「仕込みのタイミング」→「市場に動きが見られます」).

### Rewrite Patterns
| Before | After |
|--------|-------|
| キャンペーンのご案内です。今なら特典があります。 | 【件名】今なら口座開設で最大5万円相当プレゼント\n【プリヘッダー】先着順・名額限定のため、お早めに\n【本文】…\n今すぐ申し込む |
| 手数料引き下げのお知らせです。ぜひご利用ください。 | 【件名】手数料が大幅引き下げ！業界最安水準へ\n【プリヘッダー】国内株・米国株の取引手数料を一斉改定しました\n【本文】…\n詳細を確認する |

### Checkpoint
- [ ] Subject ≤40 chars and contains core benefit/number
- [ ] Preheader ≤80 chars and does not repeat subject content
- [ ] CTA button ≤15 chars
- [ ] Body broken into short scannable paragraphs (no single block > 4 sentences)
- [ ] Offer introduced with「」bracket naming (if campaign/reward content present)

### Example
**Input:** 「口座開設キャンペーンを実施中です。手数料が無料になり、最大5万円相当のポイントをプレゼントしています。お早めにどうぞ。」

**Output (edm):**
「【件名】手数料0円で口座開設！最大5万円相当プレゼント
【プリヘッダー】先着順のため名額に限りがあります。今すぐお申し込みで最大5万円相当の特典を。
【本文】今なら手数料無料で口座を開設できます。最大5万円相当の特典をプレゼントいたします。名額には限りがございますので、お早めにご確認ください。
今すぐ申し込む」

**Changes:** [三段構造化（件名/プリヘッダー/本文）] [件名に数字含有] [プリヘッダー件名と非重複] [CTA命令式]

---

## T2: banner — アプリ内バナー

**句長目標:** メイン ≤15字; サブ ≤25字 | **情報構造:** メインコピー → サブコピー → CTAボタン

### Business Goal
Instant cognition → tap. Levers: info density per char (noun phrases > sentences), number at start, CTA ≤8 chars.

### Mandatory Constraints
- **Ultra-short copy**: main copy ≤15 chars (hard limit).
- Sub-copy ≤25 chars (optional).
- CTA button ≤8 chars (「詳細を見る」「今すぐ」).
- Noun phrases preferred — full sentences not required.
- Visual-first: strip ALL redundant particles/connectors to minimum.
- Numbers and percentages placed at start.

### Rewrite Patterns
| Before | After |
|--------|-------|
| 期間限定で手数料が全額無料になります | 期間限定 手数料全額無料\n今すぐ開設 |
| 新規口座開設キャンペーン実施中です | 口座開設で特典ゲット\n詳細を見る |
| 決算発表シーズンに向けて注目銘柄をチェック | 決算シーズン注目銘柄\n今すぐチェック |

### Checkpoint
- [ ] Main copy ≤15 characters
- [ ] Sub-copy ≤25 characters (if present)
- [ ] CTA ≤8 characters
- [ ] No redundant particles/connectors

### Example
**Input:** 「期間限定で手数料が全額無料になるキャンペーンを実施中です。今すぐ口座を開設してください。」

**Output (banner):** 「期間限定 手数料全額無料\n今すぐ口座開設」

**Changes:** [メイン12字≤15字] [CTA8字≤8字] [冗余助詞削除] [名詞句化]

---

# Tier 1: 産品説明（product）

**Source:** SBI証券 商品説明ページ（sbisec.co.jp）、楽天証券 国内株式ページ（rakuten-sec.co.jp/web/domestic/）、野村証券 ソリューション（nomura.co.jp/solution/）

### Tier 1 Shared Constraints
- Verb ending: です/ます体.
- Structure: Feature → benefit (〜により、〜できます / 〜で、〜が可能です).
- First use of technical terms: add parenthetical plain explanation 「〜（○○とも呼ばれる）」.
- Second-person or impersonal — avoid 「当社では」as subject.
- No hedging on product descriptions (avoid 〜と見られる in feature descriptions).
- Multi-feature ordering: strongest/most differentiating first; if equal, user-benefit-magnitude descending.

### Framework Reference (PASONA)
Feature = Solution, benefit = Offer. If input lacks benefit framing, apply PASONA: Problem → Solution → Offer. Do not add claims — only surface latent benefits.

### Rewrite Patterns
| Before | After |
|--------|-------|
| 信用取引が利用できる | 信用取引（担保を活用して資金を借りて取引する手法）をご利用いただけます |
| 手数料が安い | 手数料が業界最低水準のため、取引コストを大幅に抑えられます |
| NISAに対応 | NISA口座での購入に対応しており、非課税メリットを活用できます |
| 初心者でも利用できます | 投資初心者の方でも気軽にはじめられます |
| 〜が可能となっております | 〜ができます / 〜いただけます |
| 多彩な機能を搭載 | チャート分析・スクリーナー・アラートを搭載（具体列挙）|
| セキュリティが万全です | 二段階認証とデータ暗号化で、お取引を守ります |
| 簡単に操作できます | 3ステップで注文完了（数字化）|

---

## T2: short — 短産品文案・卖点提炼

**句長目標:** 15–25字/文 | **情報構造:** 卖点 → 差異化 → CTA（任意）

### Business Goal
Instant differentiation in minimal words. Levers: single selling-point purity, number-first density, competitive contrast.

### Mandatory Constraints
- Single strongest selling point per output. No exhaustive feature lists.
- Competitive differentiation: what makes this different from alternatives (implied or stated).
- Active verbs, no hedging, no parenthetical explanations (reserve for detail scene).
- Number-first: if input contains a quantitative claim, lead with the number.
- CTA optional; if present, use「詳しくはこちら」or similar low-commitment form.

### Rewrite Patterns
| Before | After |
|--------|-------|
| 当社のインデックスファンドは信託報酬が低く、長期投資に適しています | 信託報酬XX%の低コストファンド。長期投資に最適 |
| 多くの機能があります | 国内株・外国株・投信、ひとつの口座でまとめて管理 |
| 初心者にも使いやすい画面設計です | 初めてでも迷わない、シンプル設計 |

### Checkpoint
- [ ] Single main selling point (not a feature list)
- [ ] Sentence length ≤ 25字 average
- [ ] Competitive differentiation stated or implied (vs. alternatives)

### Example
**Input:** 「当社のインデックスファンドは、信託報酬が年0.1%以下と低水準であり、長期的な資産形成を目指す投資家に適した商品となっております。」

**Output (short):** 「信託報酬0.1%以下のインデックスファンド。長期資産形成を、低コストで。」

**Changes:** [卖点先出し（数字）] [冗長な修飾削除] [簡潔な体言止め]

---

## T2: detail — 詳細説明ページ

**句長目標:** 20–35字/文 | **情報構造:** 機能 → ベネフィット → 説明 → CTA（任意）

### Business Goal
Full feature→benefit comprehension with zero jargon barriers. Levers: benefit conversion completeness, term explanation, scannable layout.

### Mandatory Constraints
- Full feature→benefit expansion for each feature.
- Technical terms explained on first use.
- CTA optional; if conversion-oriented: 「詳しくはこちら」.

### Rewrite Patterns
| Before | After |
|--------|-------|
| 株式取引と投資信託の取り扱いがあります | 株式取引で資産を積極的に運用でき、投資信託で手軽に分散投資を始められます |
| ツールが充実しています | チャート分析やスクリーニングなど、銘柄選びに役立つツールを揃えています |

### Checkpoint
- [ ] Feature→benefit structure present for each claim
- [ ] First-use technical terms have plain explanation
- [ ] Average sentence length 20–35字
- [ ] Multi-feature outputs: consistent F→B pair structure across all items

### Example
**Input:** 「当社はインデックスファンドの取り扱いがあります。」

**Output (detail):** 「インデックスファンド（市場全体に連動する低コスト投資信託）を豊富に取り揃えており、分散投資を手軽に始められます。」

**Changes:** [用語説明追加] [ベネフィット先出し] [二人称化]

---

## T2: manual — 使用説明・手順書

**句長目標:** 20–40字/文 | **情報構造:** 目的 → 前提条件 → 手順（番号付き）→ 注意事項

### Business Goal
Zero-backtrack task completion. Levers: one-action-per-step granularity, precondition visibility, completion confirmation, error recovery.

### Mandatory Constraints
- Sequential steps numbered (①②③ or 1. 2. 3.).
- One action per step: no compound actions in a single step.
- State preconditions before steps (「〜の前に」「〜が必要です」).
- Warnings/cautions at end, clearly marked (「※」「注意：」).
- Passive avoided; imperative or 〜してください form preferred.
- **UI elements** (button names, menu names, screen names) enclosed in「」brackets.
- **Completion confirmation**: final step must tell user how to verify success (e.g.,「〜が表示されたら完了です」).
- **Error recovery**: caution section should include what to do if operation fails.

### Rewrite Patterns
| Before | After |
|--------|-------|
| ログインしてから設定を変更してください | ①マイページにログインします。②「設定」をタップします。③変更内容を入力し、「保存」を押してください。 |
| 書類を用意して手続きを行ってください | 【必要書類】本人確認書類・マイナンバー確認書類 ①書類をご準備ください。②申込フォームに必要事項をご入力ください。 |
| 審査に時間がかかります | ※審査には通常3営業日ほどお時間をいただいております。あらかじめご了承ください |

### Checkpoint
- [ ] Steps are numbered (①②③ or 1. 2. 3.)
- [ ] One action per step (no compound steps)
- [ ] Preconditions stated before steps

### Example
**Input:** 「口座開設の際は本人確認書類が必要です。オンラインで手続きができます。」

**Output (manual):** 「【必要なもの】本人確認書類（運転免許証またはマイナンバーカード）① 公式サイトの「口座開設」ページにアクセスします。② 必要事項を入力し、本人確認書類をアップロードしてください。③ 審査完了後、登録メールアドレスに通知が届きます。」

**Changes:** [手順番号付き] [前提条件先出し] [1アクション/ステップ]

---

## T2: script — 動画・音声スクリプト

**句長目標:** ≤30字/文 | **情報構造:** 導入（フック）→ 説明 → まとめ/CTA

### Business Goal
Single-listen comprehension → "I want to try it." Levers: spoken rhythm (≤30 chars/sentence), zero written-only expressions, natural large-number formatting.

### Mandatory Constraints
- **Spoken rhythm**: each sentence ≤30 chars (≈3–4 seconds read aloud).
- Avoid written-only expressions: 「〜においては」→「〜では」, 「〜に関しまして」→「〜について」, 「〜及び」→「〜と」.
- Parenthetical definitions become natural spoken asides: 「〜（○○とも呼ばれる）」→「〜、つまり○○ですが、」.
- Large numbers in readable units: 万/億 (「15億円」not「1,500,000,000円」; 「3万人」not「30,000人」).
- Sentences separated by full stops (short pauses); avoid comma-chaining long clauses.
- Conversational です/ます, but not overly casual. Maintain product register.
- Hook opening: first sentence must state the listener's benefit or pose a question — not merely announce the topic.

### Rewrite Patterns
| Before | After |
|--------|-------|
| インデックスファンド（市場全体に連動する投資信託）においては、信託報酬が重要な指標となっております | インデックスファンド、つまり市場全体に連動する投資信託ですが、信託報酬がとても大切です |
| 1,500,000,000円の運用資産 | 15億円の運用資産 |
| 米国株式に関しましては、24時間取引が可能となっております | 米国株式については、24時間取引ができます |
| なお、当該サービスの利用及び口座開設に際しては | このサービスの利用と口座開設では |

### Checkpoint
- [ ] Every sentence ≤30 characters
- [ ] No written-only expressions (〜においては / 〜に関しまして / 〜及び / 〜となっております)
- [ ] Large numbers use 万/億 units

### Example
**Input:** 「オプション取引（デリバティブの一種）においては、原資産の価格変動に基づいて利益を得ることが可能となっております。」

**Output (script):** 「オプション取引についてお話しします。これはデリバティブの一つです。原資産の価格の動きで利益を狙えます。」

**Changes:** [口語化（〜においては→について）] [括弧注釈→自然な挿入] [1文≤30字に分割] [〜となっております→〜ます]

---

# Tier 1: 情報分析（report）

**Source:** 野村証券 マーケット・エクスプレス週報（2024Q1）、大和証券レポート、楽天証券 マーケット情報（rakuten-sec.co.jp/web/market/）、野村証券 マーケット（nomura.co.jp/market/）

### Tier 1 Shared Constraints
- Third-person, objective viewpoint exclusively.
- Every forward-looking or interpretive claim MUST use hedging. **Confidence gradient** (use appropriate level):
  - **High confidence** (見込み/見通し): 「〜の見込みだ」「〜との見通しが示されている」— for consensus forecasts, official guidance
  - **Medium confidence** (と見られる/と考えられる/と示唆される): 「〜と見られる」「〜と考えられる」— for analyst interpretation, implied conclusions
  - **Low confidence** (可能性がある/リスクがある/不透明感): 「〜の可能性がある」「〜リスクがある」— for speculative outcomes, tail risks
  - **Avoid 〜だろう** — too casual; use 〜と見られる instead. Uniform hedge level across all claims = mechanical; vary by actual confidence.
- No first-person (私, 当社, 弊社 as subject in analysis claims).
- No subjective expressions: zero「思います」「感じます」「〜と思う」「〜と感じる」(RL-3).
- Specific numbers must be attributed (RL-9).

### Rewrite Patterns
| Before | After |
|--------|-------|
| 株価は上がると思います | 株価は上昇する見込みだ |
| 投資家が増えている | 投資家数は増加傾向にあると見られる |
| これはリスクです | このような動向はリスク要因となり得る |
| 当社は成長している | 当該企業は成長軌道にあると考えられる |
| 株価は回復するだろう | 株価は回復する見込みだ |
| 売上は500億円に達した | 同社発表によれば、売上は500億円に達した |
| 大幅に下落した | 前日比X.X%安と、大幅な下落となった |
| インフレは収束する | インフレは収束に向かう可能性がある |

---

## T2: report — 研報・週報

**句長目標:** 20–35字/文 | **情報構造:** 背景/現状 → 分析 → 見通し

### Business Goal
Trusted analysis supporting investment decisions. Levers: hedge precision, attribution completeness, evidence→conclusion chain integrity.

### Mandatory Constraints
- Attribution for specific numbers: 「〜によれば」「〜によると」「〜の見通しでは」「〜発表資料では」.
- Assertions without hedging or attribution = error; rewrite as inference/outlook.

### Structure
1. Context: factual background (past/current state).
2. Analysis: interpretation with hedging expressions.
3. Outlook: forward-looking with 見込み/可能性.

### Checkpoint
- [ ] Every forward-looking claim uses hedging expression with appropriate confidence level
- [ ] Information order follows 背景/現状→分析→見通し
- [ ] だ/である体 consistent (zero です/ます)
- [ ] Zero first-person subject in analysis claims (私/当社/弊社)
- [ ] Specific numbers attributed (RL-9: 〜によれば/〜によると)

### Example
**Input:** 「現在、株価は上昇しています。投資家に人気で、これからも上がると思います。」

**Output (report):** 「現在、株価は上昇基調にあると見られる。投資家の注目度は高まっており、今後も堅調に推移する見込みだ。」

**Changes:** [主観表現を客観化] [推測表現追加] [三人称化]

---

## T2: press — プレスリリース

**句長目標:** 20–40字/文 | **情報構造:** 5W概要 → 詳細 → 背景

### Business Goal
Maximum-efficiency fact delivery meeting disclosure obligations. Levers: 5W first-paragraph density, zero marketing tone, date format compliance.

### Mandatory Constraints
- Third person. Company as subject: 「〜株式会社は〜を発表しました」.
- Opening formula: 「〔企業名〕は本日（YYYY年MM月DD日）、〔事項〕をお知らせいたします」— use いたします (Kenjōgo II).
- First paragraph = 5W summary (≤100 chars).
- No marketing tone: no「！」, no benefit-first, no CTA.
- Past tense for completed actions, future for upcoming.
- Date must appear: 「YYYY年MM月DD日」format.

### Rewrite Patterns
| Before | After |
|--------|-------|
| 手数料がめちゃくちゃ安くなりました！ | 株式取引手数料を引き下げたことを発表しました |
| 今すぐご確認ください | （削除 — CTA禁止）|
| 新サービスを始めました。便利です | 〇〇株式会社は本日、〔サービス名〕の提供を開始したことをお知らせいたします |

### Checkpoint
- [ ] First paragraph ≤100 chars and contains 5W (who/what/when/where/why)
- [ ] Date in 「YYYY年MM月DD日」 format
- [ ] Opening formula: 「〔企業名〕は本日（YYYY年MM月DD日）、〔事項〕をお知らせいたします」

### Example
**Input:** 「新しい積立サービスを始めました。毎月自動で積立できてすごく便利です。ぜひ使ってみてください。」

**Output (press):** 「〇〇証券株式会社は本日（2024年XX月XX日）、毎月定額を自動積立できる新サービスの提供を開始したことをお知らせいたします。」

**Changes:** [第三者視点に変換] [CTA削除] [5W先出し構造] [開始告知定型文]

---

## T2: deck — スライド・デッキ

**句長目標:** ≤25字/bullet（hard） | **情報構造:** 数値/キーワード → 簡潔な修飾

### Business Goal
Key insight per bullet in <3-second scan. Levers: info density per char, noun-stop endings, category tags for IR scannability.

### Mandatory Constraints
- Fragment OK — noun-stop endings preferred; complete sentences not required.
- **≤25 chars/bullet.** Split longer items.
- Strip filler verbs (〜しております/〜となっております) to core noun phrase.
- Numbers/key terms at bullet start.
- No conjunctions (また/さらに/なお) — each bullet standalone.
- Category tags: 【増収】【費用削減】【見通し】【リスク】etc.
- **Multi-bullet ordering**: quantified results first → qualitative analysis → outlook/risk last.

### Rewrite Patterns
| Before | After |
|--------|-------|
| 当社の純利益は前期比10%増加しました | 純利益：前期比+10% |
| コスト削減により収益性が改善しています | コスト削減→収益性改善 |
| リスク管理を強化する必要があります | 【リスク】リスク管理強化（要対応）|

### Checkpoint
- [ ] Each bullet ≤25 characters (hard limit)
- [ ] No 〜しております / 〜となっております — strip to noun phrase
- [ ] Category tag (【増収】【費用削減】【見通し】【リスク】etc.) present for IR-relevant bullets

### Example
**Input:** 「今期の営業利益は前期比15%増加しました。新規事業への投資が奏功した結果です。」

**Output (deck):** 「【増収】営業利益：前期比+15% / 新規事業投資が寄与」

**Changes:** [名詞止め] [数値先出し] [カテゴリタグ追加]

---

## T2: hottopic — 市況速報・ホットトピック

**句長目標:** 15–25字/文; **総計 ≤140字** | **情報構造:** 事実 → 影響/背景 → 見通し（任意）

### Business Goal
Core market fact + impact in ≤140 chars. Levers: first-sentence data hit rate, character efficiency, zero-subjectivity + calibrated hedging.

### Mandatory Constraints
- **1–3 sentences total, ≤140 characters.**
- Sentence 1 = core fact (MUST contain key number/data point).
- Sentence 2 = market impact or background (optional).
- Sentence 3 = short-term outlook with hedging (optional; use 「〜と見られる」「〜見込み」).
- Numbers must be preserved precisely (decimals, percentages, dates).
- だ/である体 (inherits report T1).
- No subjective evaluation: zero「思う」「感じる」; hedging expressions OK.
- No attribution required for widely-known data (index levels, rate decisions) — unlike full report style.

### Rewrite Patterns
| Before | After |
|--------|-------|
| 米連邦準備理事会が利上げを決定したことを受けて、日経平均株価が大きく下落しました。投資家心理は冷え込んでいると思われます | FRBの利上げを受け、日経平均は2.3%下落。投資家心理の冷え込みが見られる |
| 中国のGDP成長率が発表されて、予想を下回る結果となりました | 中国GDP成長率4.9%、市場予想を下回った。景気減速懸念が広がっている |
| 決算発表があり、売上高が前年同期比で増加しました | 売上高：前年同期比+15%。通期見通しの上方修正が見込まれる |

### Checkpoint
- [ ] Total character count ≤140
- [ ] First sentence contains key number/data point
- [ ] No subjective expressions (思う/感じる)

### Example
**Input:** 「米連邦準備理事会が25ベーシスポイントの利上げを発表し、日経平均株価は前日比2.3%下落して38,500円で取引を終えました。今後の市場動向に注目が集まっています。」

**Output (hottopic):** 「FRBの25bp利上げを受け、日経平均は2.3%安の38,500円で引けた。今後の金融引き締め継続が注視される。」（54字）

**Changes:** [140字以内に圧縮] [核心数字先出し] [客観化（注目→注視される）] [だ/である体統一]

---

## T2: topic — 話題記事・コミュニティ投稿

### Business Goal
Objective analysis driving community engagement (read→comment→vote). Levers: variant routing accuracy, register consistency, participation module completeness.

**句長目標:** 25–50字/文 | **情報構造:** Variant A: タイトル → 事実/現状 → 分析/背景 → 見通し/焦点 → 読者参加 → 投稿例 → 投票 → Push通知; Variant B: タイトル → 市場コンテクスト → 転換句 → ユーザー投稿+編集コメント → 免責 → Push

This scene has **two variants**. Detect from input:
- **Variant A (話題シェア)**: market theme → reader engagement. Default when input is editorial/analytical.
- **Variant B (人気投稿まとめ)**: UGC curation → editorial commentary. Triggered by 「人気投稿」「まとめ」「ピックアップ」「@ユーザー名」in input.

### Shared Constraints (A + B)
- **Register exception**: です/ます体 (not だ/である) — community engagement content exempted from report T1 客観体. See RL-11 topic exceptions.
- **Numbers**: precise carry-over (騰落率/株価/期間). Formal attribution not required for widely-reported market data (RL-9 exception).
- **No subjective evaluation**: zero「思う」「感じる」(RL-3 applies).
- Forward-looking statements require hedging (「〜可能性も出てきました」「〜となりそうです」「〜と見られています」「〜見込みです」).
- **Push通知**: タイトル ≤20 chars + サブタイトル ≤35 chars.
- No section headings between paragraphs — line breaks only.

### Variant A — 話題シェア (default)

**8-part structure**: タイトル → 本文(事実→分析→見通し, 400–800字) → 読者参加 → 投稿例 → 投票 → Push.

- **Title**: A) 「[Fact]！あなたの[戦略/成果]をシェアしよう」or B) 「[Fact]！[疑問形？]」
- **読者参加**: 「皆さんは〜ましたか？ぜひ〜をコメント欄でシェアしてください。」(ましたか form)
- **投稿例**: 3–5 bullets, タメ口OK (register exception)
- **投票**: 2–4 choices A/B/C/D. Pattern: 「[状況]、あなたの[対応]は？」
- **Push**: タイトル≤20 + サブタイトル≤35. Endings: 「〜しよう！」「〜チェック>>」

### Variant B — 人気投稿まとめ

**6-part structure**: タイトル → 市場コンテクスト(2–3段落) → 転換句(固定) → ユーザー投稿(3–5件)+編集コメント → 免責 → Push.

- **Title**: 「"[quote1]"や "[quote2]"など―人気投稿まとめ」
- **Transition** (fixed): 「それでは、今回話題となった人気投稿を見ていきましょう。」
- **User posts**: @ユーザー名 → bold title → original text (casual register preserved) → editorial commentary (です/ます, objective, 1–2 sentences)
- **Disclaimer** (mandatory): 「*本コンテンツで引用している投稿はmoomooユーザーが作成したものであり、当社の見解を示すものではありません。」
- **Push** (fixed): 「moomoo証券ユーザーのリアル投資談をピックアップ。今すぐチェック>>」
- No 投票/投稿例/読者参加 (Variant A only).

### Rewrite Patterns (Variant A)
| Before | After |
|--------|-------|
| 日経平均が連騰してて、みんな利益出てるっぽい | 日経平均が10日連続で上昇し、多くの投資家がリターンを実感しています |
| どうなるか分かりません | 今後どのような展開となるか注目されています |
| 思う/感じる | （削除 or 客観表現に置換 — RL-3） |
| みんなどう思う？コメントちょうだい | 皆さんはこの上昇相場にどう対応されましたか？ぜひ投資戦略をコメント欄でシェアしてください。 |
| A)買う B)売る | A) 押し目買いを継続 B) 利益確定を優先 C) 様子見で静観 D) ポートフォリオを再構成 |

### Rewrite Patterns (Variant B)
| Before | After |
|--------|-------|
| この人すごい儲かってる | 値動きの大きい局面を捉え、保有を継続されたことでパフォーマンスにつながっている点が際立ちます |
| 投資の才能がない | 長期で保有しながらリターンを積み上げている点自体が一つの特徴といえます |
| みんなの投稿紹介します | それでは、今回話題となった人気投稿を見ていきましょう。 |

### Checkpoint — Variant A (話題シェア)
- [ ] Title matches pattern A (fact + action) or B (fact + question)
- [ ] Body 400–800 chars, です/ます体
- [ ] Forward-looking statements use hedging expressions
- [ ] Zero subjective expressions (思う/感じる)
- [ ] 読者参加 section present (〜ましたか？ form)
- [ ] 【投稿例】section with 3–5 bullets
- [ ] 投票 section with 2–4 choices
- [ ] Push タイトル ≤20 chars, サブタイトル ≤35 chars

### Checkpoint — Variant B (人気投稿まとめ)
- [ ] Title in 「"[quote]"や "[quote]"など―人気投稿まとめ」format
- [ ] Market context 2–3 paragraphs
- [ ] Transition sentence 「それでは、今回話題となった…」present
- [ ] 3–5 user posts with editorial commentary each
- [ ] Disclaimer present
- [ ] Push subtitle matches fixed template
- [ ] No 投票/投稿例 sections (these are Variant A only)

### Example — Variant A (話題シェア)
**Input:** 「日経平均が最近すごい上がってて、10日連続で続伸中。みんな儲かってるのかな。テック株が特に強くて、半導体関連も好調。今後もこの勢いが続くのか気になる。みんなの意見聞きたい。」

**Output (topic/A):** 「日経平均10日連続続伸！あなたの投資成果をシェアしよう｜日経平均株価が10日連続で上昇しています。テクノロジー株を中心に…（400–800字本文）…皆さんはこの連騰相場にうまく乗れましたか？ぜひ投資戦略をコメント欄でシェアしてください。｜【投稿例】・10日連騰、利確した？…（3–5 bullets, タメ口OK）｜【投票】A) 押し目買いを継続 B) 利益確定を優先 C) 様子見 D) ポートフォリオ再構成｜Push: 日経平均10日連続上昇！ / あなたの投資成果をシェアしよう>>」

**Changes:** [です/ます体統一] [タイトル→事実+行動喚起型] [数字保持] [主観→客観化] [8パート全追加] [推測→「〜となりそうです」]

### Example — Variant B (人気投稿まとめ)
**Input:** user-post curation content with @usernames, screenshots, and ticker links.

**Output (topic/B):** 「"SOXL購入で利益1000%超"や "ガチホと押し目移動"など―人気投稿まとめ｜（市場コンテクスト2–3段落, 客観体）｜それでは、今回話題となった人気投稿を見ていきましょう。｜@ユーザー名 **タイトル** — 編集コメント（です/ます, 客観評価）× 3–5件｜*本コンテンツで引用している投稿は…（免責）｜Push: …今すぐチェック>>」

**Changes:** [市場コンテクスト客観化] [編集コメントです/ます体統一] [免責声明追加] [Push固定テンプレート]

---

# Tier 1: 法律合規（legal）

**Source:** SBI証券 目論見書・商品説明書（金融庁ガイドライン準拠）、野村証券 利用規約・免責事項（nomura.co.jp/terms/）

### Tier 1 Shared Constraints
- **Zero promotional tone**: no「！」, no benefit claims, no urgency markers.
- Risk warning mandatory for investment content: 「損失が生じるおそれがあります」or 「元本を割り込む可能性があります」.
- Responsibility transfer: 「ご自身の判断と責任において」for user-action clauses.
- Technical terms preserved verbatim (RL-1). Full form — no abbreviations (「東京証券取引所」not「東証」).
- Verb register: consistent within document (do not mix だ/である体 + です/ます — RL-11).
- **Register defaults by scene**: disclosure = だ/である体 exclusively (RL-5); terms = です/ます体 (user-facing); disclaimer = です/ます体 (user-facing, 謙譲語II「おりますが」OK).

---

## T2: disclosure — 開示文書・目論見書

**句長目標:** 30–50字/文 | **情報構造:** 命題 → 根拠 → 条件/義務

### Business Goal
Regulatory-grade risk disclosure with zero ambiguity. Levers: risk type coverage, conditional precision, zero abbreviation, だ/である purity.

### Mandatory Constraints
- Verb ending: だ/である体 exclusively. **No です/ます** (RL-5).
- No trailing nominalization as sentence-ender: avoid 〜であること/〜ということ to close sentences.
- No dangling modifiers; complete modification within clause.
- Sentence length target: 30–50 characters. Split longer sentences.
- No abbreviations even for well-known terms.

### Rewrite Patterns
| Before | After |
|--------|-------|
| 株価は上がっています | 株価は上昇している |
| ご確認ください | 確認されたい |
| 投資家の皆さんに | 投資家各位に |
| 〜と思います | 〜と考えられる / 〜である |

### Checkpoint
- [ ] No trailing nominalization as sentence-ender (〜であること / 〜ということ)
- [ ] No abbreviations even for well-known terms (東証 → 東京証券取引所)
- [ ] Information order follows 命題→根拠→条件/義務

### Example
**Input:** 「現在、当社の株価は上昇しています。投資家の皆さんには、ぜひご注目いただければと思います。」

**Output (disclosure):** 「現在、当社株価は上昇基調にある。投資家各位には注目されたい。」

**Changes:** [だ/である体に統一] [敬語除去] [不要な修飾削除]

---

## T2: terms — 利用規約

**句長目標:** 40–60字/文 | **情報構造:** 対象範囲 → 義務 → 条件 → 例外

### Business Goal
Enforceable rights/obligations framework with zero loopholes. Levers: obligation framing (するものとします), exception marking, defined-term consistency.

### Mandatory Constraints
- Liability scope: 「いかなる〜」「一切〜ない」for absolute disclaimers.
- Defined terms: initial definition with 「」brackets, subsequent uses unquoted.
- Conditional stacking for precision: 〜を除き〜の場合において〜でないときは.
- User obligation framing: 「〜するものとします」「〜してはなりません」.
- Exception clauses clearly marked: 「ただし、〜の場合はこの限りではない」.

### Rewrite Patterns
| Before | After |
|--------|-------|
| 自分で判断してください | ご自身の判断と責任においてご利用ください |
| 変更することがあります | 当社は事前の通知なく本規約を変更できるものとします |
| 禁止事項があります | 以下の行為を禁止します（以下「禁止行為」といいます）|

### Checkpoint
- [ ] User obligations framed as 〜するものとします (not 〜してください)
- [ ] Exception clauses present where applicable (「ただし、〜の場合はこの限りではない」)
- [ ] Defined terms introduced with 「」 brackets on first use
- [ ] Register consistency: です/ます体 throughout (no だ/である leakage)

### Example
**Input:** 「このサービスは変更することがあります。問題があればご連絡ください。」

**Output (terms):** 「当社は、本サービスの内容を予告なく変更できるものとします。本サービスに関するお問い合わせは、所定の窓口までご連絡ください。」

**Changes:** [規約構文化] [義務形式（〜できるものとします）] [窓口明示]

---

## T2: disclaimer — 免責事項

**句長目標:** 40–60字/文 | **情報構造:** 対象範囲 → 義務 → 条件 → 免責 → リスク警告

### Business Goal
Maximum liability limitation while maintaining user trust. Levers: precaution hedge, causation-limiting chain, risk warning completeness by product type.

### Mandatory Constraints
- Negated obligation as standard clause-ender: 「〜について責任を負うものではありません」.
- Causation-limiting preface: 「本サービスの情報に基づいて被った損害」— state input-to-loss chain.
- Precaution hedge before every limitation clause: 「万全を期しておりますが」or 「正確を期すよう努めておりますが」.
- Risk warning mandatory: 「損失が生じるおそれがあります」or 「元本を割り込む可能性があります」.

### Rewrite Patterns
| Before | After |
|--------|-------|
| 間違いがあっても責任は取りません | 万全を期しておりますが、本情報に基づいて被ったいかなる損害についても責任を負うものではありません |
| 損をすることもあります | 投資には価格変動等のリスクがあり、損失が生じるおそれがあります |
| これは参考情報です / おすすめです | 本情報は投資助言を目的としたものではありません |

### Checkpoint
- [ ] Liability negation form present (「責任を負うものではありません」or equivalent)
- [ ] Risk warning present for investment content (「損失が生じるおそれがあります」)
- [ ] Precaution hedge (「万全を期しておりますが」) before limitation clauses
- [ ] Non-advice disclaimer if content could be read as recommendation (「投資助言を目的としたものではありません」)

### Example
**Input:** 「この情報は参考用です。損をしても責任は取りません。自分で判断してください。」

**Output (disclaimer):** 「本情報は参考情報として提供するものであり、万全を期しておりますが、本情報に基づいて被ったいかなる損害についても責任を負うものではありません。投資に際してはご自身の判断と責任においてご利用ください。」

**Changes:** [免責構文化] [万全を期す前置き追加] [責任移転文追加]

---

# Tier 1: 客服支援（support）

**Source:** 野村証券 サポートページ（nomura.co.jp/support/）

### Tier 1 Shared Constraints
- Verb register: Kenjōgo II throughout — 「承ります」「ございます」preferred over 「あります」.
- Honorific prefix (お/ご) on ALL service nouns: 「お手続き」「ご相談」「ご不明点」「お問い合わせ」.
- **Zero promotional language**: no「！」, no benefit statements, no urgency markers (「今すぐ」).
- Second-person: 「お客様」consistently. No casual address.
- Navigation recovery phrase: 「お探しの情報が見つからない場合は」when directing to alternate channels.

### Rewrite Patterns
| Before | After |
|--------|-------|
| 電話してください | お電話にてお問い合わせください |
| できます / やります | 承ります |
| わからない場合は連絡してください | ご不明点がございましたら、お気軽にお問い合わせください |

---

## T2: faq — FAQ・よくある質問

**句長目標:** 20–35字/文 | **情報構造:** 質問 → 回答 → 手順/チャネル

### Business Goal
Self-service resolution reducing support ticket volume. Levers: direct-answer-first, channel clarity, お/ご全面覆盖, reassurance tone.

### Mandatory Constraints
- Question format: 「Q. 〜ですか？」or 「〜について知りたい」.
- Answer format: direct, concise (1–2 sentences), then steps or channel if needed.
- CTA form: functional navigation only (「お電話」「ご質問フォーム」「ご来店」).
- Multi-topic input: split into separate Q/A pairs; one question per Q block.

### Rewrite Patterns
| Before | After |
|--------|-------|
| 仕様です / できません | 現在のシステム仕様ではお取り扱いしておりません。ご不便をおかけいたします |
| ちょっと待ってください | お時間をいただき恐れ入ります。確認のうえ、改めてご案内いたします |
| 自分で調べてください | 以下のページにて詳細をご確認いただけます |

### Checkpoint
- [ ] All service nouns have お/ご prefix (お手続き/ご相談/お問い合わせ)
- [ ] Functional contact channels stated (お電話/ご質問フォーム/ご来店)
- [ ] Q/A format: Q. 〜ですか？ / A. direct answer in 1–2 sentences

### Example
**Input:** 「口座の情報を変更したい場合は、手続きが必要です。連絡してください。」

**Output (faq):** 「Q. 口座情報の変更はどのように行いますか？ A. お口座情報の変更をご希望の場合は、所定のお手続きが必要です。詳細はお電話またはご質問フォームにてお問い合わせください。」

**Changes:** [FAQ形式化] [敬語化（承ります体）] [お/ご接頭辞追加] [機能的チャネルCTA]

---

## T2: guide — 手続き案内

**句長目標:** 20–40字/文 | **情報構造:** 手続き種別 → 手順/チャネル → 代替案内

### Business Goal
Complete procedure guidance with zero user backtracking. Levers: step completeness, branching clarity, channel list, fallback recovery phrase.

### Mandatory Constraints
- Sequential steps if multiple actions required (①②③).
- State the procedure category upfront: 「〜についてのお手続き」.
- Close with channel options + recovery phrase.
- More detailed than FAQ: full step list, not just answer.
- State processing time when applicable (「通常X営業日以内」).
- For branching procedures, state condition before branch (「マイナンバーカードをお持ちの場合→ルートA」).

### Rewrite Patterns
| Before | After |
|--------|-------|
| それは別の部署です | 本件につきましては、〇〇窓口にてご対応しております |
| 書類を送ってください | 所定の書類をご準備のうえ、以下の宛先までご郵送ください |
| まだ完了してません | お手続きは現在処理中でございます。完了次第、登録のメールアドレスにご連絡いたします |

### Checkpoint
- [ ] Procedure category stated at start (「〜についてのお手続き」)
- [ ] Steps numbered if sequential (①②③)
- [ ] Channel list at close (お電話/ご質問フォーム/ご来店)
- [ ] Recovery phrase at close (「お探しの情報が見つからない場合は」or equivalent)

### Example
**Input:** 「住所変更の手続きはオンラインでできます。書類が必要な場合もあります。」

**Output (guide):** 「お住所変更のお手続きについてご案内いたします。① マイページの「お客様情報の変更」からオンラインでお手続きいただけます。② 書類のご提出が必要な場合は、所定の書類をご郵送ください。ご不明点がございましたら、お電話またはご質問フォームにてお問い合わせください。」

**Changes:** [手続き種別先出し] [手順番号付き] [チャネル一覧追加] [敬語化]

---

# Register Mixing (RL-11) — Quick Reference

Register mixing is a hard failure. Scan 4 categories after Step 4: (1) verb endings だ/である vs です/ます, (2) keigo level mismatch, (3) report hedging in non-report styles, (4) tone markers (「！」/「今すぐ」) in formal styles. If mixed → normalize to dominant register before Step 5. See Cross-Style Red Line Summary RL-11 for full scope.

---

# Routing Inference Table

When `--style` and `--scene` flags are omitted, infer from input keywords:

| Keywords | Route |
|----------|-------|
| 営業/推広/LP/広告 | marketing/lp |
| SNS/Twitter/X/LINE | marketing/sns |
| キャンペーン/イベント/セミナー | marketing/event |
| Push通知/プッシュ/推送 | marketing/push |
| EDM/メルマガ/メール配信 | marketing/edm |
| バナー/横幅/in-app banner | marketing/banner |
| 卖点/キャッチコピー/短い商品文案 | product/short |
| 商品説明/製品紹介/产品文案 | product/detail |
| 使用説明/マニュアル/操作手順 | product/manual |
| 動画/スクリプト/ナレーション | product/script |
| 研報/週報/レポート/マーケット分析 | report/report |
| プレスリリース/お知らせ/新闻稿 | report/press |
| スライド/デッキ/PPT/幻灯片 | report/deck |
| 市況速報/ホットトピック/快讯 | report/hottopic |
| 話題記事/トピック/コミュニティ投稿 | report/topic |
| 目論見書/開示文書/正式体/formal | legal/disclosure |
| 利用規約/terms/合规 | legal/terms |
| 免責事項/disclaimer/免责 | legal/disclaimer |
| FAQ/よくある質問/客服文案 | support/faq |
| 手続き/サポート/ガイド | support/guide |

---

# Cross-Style Red Line Summary

| Check | When | Inline Verification |
|-------|------|---------------------|
| RL-1: Term lock | All styles/scenes | List extracted terms before transform; confirm each present in output |
| RL-2: No injection | All styles/scenes | Output propositions ⊆ input propositions |
| RL-3: No subjective | 情報分析 (report/press/deck/hottopic/topic) | Scan for 思います\|感じます\|と思う\|と感じる; state「主観表現なし: ✓」|
| RL-4: Hard char limits | RL-4 scenes (sns/push/edm/banner/hottopic/deck) | Count chars per field; state per-field counts; compress if over limit |
| RL-5: No です/ます | legal/disclosure | Scan for です\|ます; state「です/ますなし: 確認済み」|
| RL-6: Lang deflect | non-Japanese input | Detect language; delegate if not Japanese |
| RL-7: No 二重否定 | All styles/scenes | Scan for 〜ないわけではない\|〜なくはない |
| RL-8: No noun stacking | All styles/scenes | Flag sequences of 4+ consecutive nouns |
| RL-9: Attributed numbers | 情報分析 (report/press/deck/hottopic/topic); topic: widely-reported data exempt | Flag bare specific numbers; state「要出典: [数値]」or「未出典数値なし: ✓」|
| RL-10: No passive stack | All styles/scenes | Flag sentences with 2+ 〜される\|〜られる |
| RL-11: No register mix | All styles/scenes | Scan (1) verb endings; (2) keigo level; (3) modality markers; (4) tone markers; state「文体統一: ✓」|
| RL-12: Marketing CTA | marketing (lp/sns/event/edm/banner); push exempt (リンク先示唆) | Scan for action verb CTA; if absent → revise; state「CTA確認: ✓」|

# Case Asset Library: Brand-Specific Voice Benchmarks

Load this file when input contains a brand name listed below, or when the user requests brand-specific voice output. Do not load for generic (unbranded) style optimization.

---

## Nomura (野村証券) — news / trade-ideas register

**Primary scenes:** trade-ideas (theme/morning), news (wrap/flash), product (detail)

### Voice Signature
- **Hedging hierarchy** (3 distinct levels, never interchangeable):
  - Observation: 「〜と見られる」「〜と示唆される」(what the data shows)
  - Interpretation: 「〜と考えられる」(what analysts infer)
  - Forecast: 「〜見込み」「〜の可能性がある」(forward-looking)
- **Anti-pattern**: Never use 「〜だろう」— too casual for Nomura house voice. Use 「〜と見られる」instead.
- **Attribution**: Bloomberg, company disclosures (「〇〇発表資料」), or named research sources. Bare numbers without attribution are rejected.
- **Structure (weekly report)**: 週間概況 → 来週の見通し → 注目イベント
- **Sentence length**: 20-35 chars. No compound sentences with 3+ clauses.

### Scene-Specific Constraints
- **trade-ideas/theme**: Full hedging hierarchy applies. Attribution mandatory for all specific numbers (RL-9). Structure: 背景/現状→分析→見通し. だ/である体 consistent.
- **news/wrap**: Company as subject (「野村證券株式会社は〜を発表しました」). Opening formula required (「〜は本日（YYYY年MM月DD日）、〜をお知らせいたします」). Hedging reserved for forward-looking statements only — completed actions stated as fact. Zero marketing tone (no「！」, no CTA).
- **news/flash**: Total ≤140 chars (RL-4). Sentence 1 = core fact with key number. Hedging reserved for optional outlook sentence. Attribution not required for widely-known data (index levels, rate decisions).
- **product/detail**: ≤25 chars/bullet (RL-4). Noun-stop endings. Category tags (【増収】【見通し】【リスク】). Strip hedging verbs to noun phrases (「上昇見込み」not「上昇する見込みだ」). Multi-bullet ordering: quantified results first → qualitative analysis → outlook/risk last.

### Benchmark Excerpt (trade-ideas/theme)
「米連邦準備理事会（FRB）は25bpの利上げを決定した。これにより、FF金利の誘導目標は5.25-5.50%となった。市場では年内の追加利上げ観測が後退していると見られる。」

### Benchmark Excerpt (news/flash)
「FRBの25bp利上げを受け、日経平均は2.3%安の38,500円。年内の追加利上げ観測は後退していると見られる。」（57字）

### Benchmark Excerpt (product/detail — deck)
「【金利】FF金利：5.25-5.50%（25bp利上げ後）」「【見通し】追加利上げ観測：後退」

### Anti-patterns (Nomura would NOT write)
- 「株価は上がるだろう」→ too casual; use 「〜と見られる」
- 「すごく注目されている」→ colloquial leakage in news/trade-ideas register
- 「投資家にとってチャンスです」→ promotional tone in report
- 「〜と思われる」→ too vague; prefer 「〜と見られる」
- 「！」in news/trade-ideas/product/detail → tone marker violation (RL-11)
- 「今すぐ確認」in any Nomura output → campaign urgency leakage in news/trade-ideas register (RL-11)

---

## Rakuten Securities (楽天証券) — campaign register

**Primary scenes:** campaign (launch/seasonal/referral)

### Voice Signature
- **なら構文**: Brand+benefit direct coupling — 「楽天証券なら[benefit]！」is the signature pattern.
- **Social proof**: Always specific numbers — 「XX万人が選ぶ」not 「多くの方が選ぶ」.
- **CTA**: Always hot-stage action verb — 「今すぐ申し込む」「無料で口座開設」. Never soft 「ご確認ください」.
- **Benefit quantification**: Specific numbers or named features, not abstract claims. 「手数料0円」not 「手数料がお得」.
- **・連結**: Enumerate with ・ for coverage feel — 「株式・投信・債券をまとめて運用」.
- **Scarcity markers**: 「〇月〇日まで限定！」「先着XX名様」— always with specific deadline or count.

### Scene-Specific Constraints
- **campaign/launch (LP)**: Full なら構文 + social proof + benefit quantification. Structure: 利益→証明→特徴→CTA. CTA buyer-stage aligned (default warm: 「無料で口座を開設する」). Sentence length 20-35 chars.
- **campaign/launch (SNS)**: ≤140 chars (RL-4). なら構文 compressed to fit limit. Social proof number in first 15 chars if applicable. 1-2 emoji. Single value proposition only — no ・連結 feature lists.
- **campaign/launch (event)**: Deadline prominent in first sentence. なら構文 in benefit line. CTA always hot stage (「今すぐ申し込む」「今すぐ参加登録」). Scarcity markers required (期限 or 先着). 1-2 emoji allowed (🎉🔔).
- **campaign/launch (EDM)**: Subject ≤40 chars with なら構文 or core benefit number. Preheader ≤80 chars supplements with social proof (non-repeating). Body follows 利益→詳細→CTA. 【】bracket format for campaign names in subject. CTA button ≤15 chars.

### Benchmark Excerpt (campaign/launch — LP)
「楽天証券なら手数料が業界最安水準！株式・投信・債券をまとめて運用できます。900万人が選ぶ証券口座で、今すぐ投資を始めましょう。」

### Benchmark Excerpt (campaign/launch — SNS)
「楽天証券なら手数料0円！900万人が選ぶ証券口座📈今すぐ口座開設▶」（33字）

### Benchmark Excerpt (campaign/launch — event)
「🎉楽天証券 口座開設キャンペーン｜12月31日まで！新規開設で5,000ポイントプレゼント。今すぐ申し込む▶」

### Anti-patterns (Rakuten marketing would NOT write)
- 「手数料が安いと見られる」→ news/trade-ideas hedging in campaign (RL-11 modality marker violation)
- 「ご確認ください」→ too polite/passive for Rakuten CTA
- 「当社の特徴は〜です」→ company-as-subject; should be benefit-first (reader-centric reframing)
- 「ぜひご検討ください」→ too weak; Rakuten prefers direct action verbs
- 「多くの方が選ぶ」→ vague social proof; must use specific number (「900万人が選ぶ」)
- 「お得です」without specifics → violates benefit quantification / specificity required (AC-7)

---

## SBI Securities (SBI証券) — compliance register

**Primary scenes:** compliance/disclosure, compliance/terms, compliance/disclaimer

### Voice Signature — Shared
- **Zero abbreviations**: 「東京証券取引所」not 「東証」. 「金融商品取引法」not 「金商法」. Even well-known abbreviations are spelled out.
- **Full-form defined terms**: Initial definition with 「」brackets, subsequent uses unquoted.
- **Liability language**: 「いかなる〜」「一切〜ない」for absolute disclaimers.
- **Conditional precision**: Stacked conditionals for legal precision — 「〜を除き、〜の場合において、〜でないときは」.

### Voice Signature — Disclosure Scene
- **だ/である体 exclusive**: No です/ます anywhere. No exceptions (RL-5).
- **Verb-final sentences**: Every sentence ends with a verb or verb-equivalent. No trailing nominalization (〜であること as sentence-ender).
- **Sentence length**: 30-50 chars.

### Voice Signature — Terms / Disclaimer Scenes
- **です/ます体**: User-facing register per style-guide legal T1 register defaults.
- **User obligation framing** (terms): 「〜するものとします」「〜してはなりません」. Exception clauses: 「ただし、〜の場合はこの限りではない」.
- **Negated obligation** (disclaimer): 「〜について責任を負うものではありません」.
- **Precaution hedge** (disclaimer): 「万全を期しておりますが」or「正確を期すよう努めておりますが」before limitation clauses. 謙譲語II「おりますが」is permitted.
- **Risk warning mandatory**: 「損失が生じるおそれがあります」or「元本を割り込む可能性があります」.

### Scene-Specific Constraints
- **compliance/disclosure**: だ/である exclusively (RL-5). Structure: 命題→根拠→条件/義務. No trailing nominalization. Sentence length 30-50 chars.
- **compliance/terms**: です/ます体. Structure: 対象範囲→義務→条件→例外. Obligation framing with「するものとします」. Sentence length 40-60 chars.
- **compliance/disclaimer**: です/ます体 (謙譲語II OK). Structure: 対象範囲→義務→条件→免責→リスク警告. Precaution hedge required before limitation clauses. Sentence length 40-60 chars.

### Benchmark Excerpt (disclosure)
「当社は、本情報の正確性および完全性について万全を期しているが、その内容を保証するものではない。本情報に基づいて被ったいかなる損害についても、当社は一切の責任を負わないものとする。」

### Benchmark Excerpt (terms)
「利用者は、本サービスの利用に際して、自己の判断と責任において行うものとします。当社は、利用者が本サービスを利用したことにより被ったいかなる損害についても、一切の責任を負わないものとします。」

### Benchmark Excerpt (disclaimer)
「本情報は投資助言を目的としたものではありません。当社は正確を期すよう努めておりますが、本情報に基づいて被ったいかなる損害についても責任を負うものではありません。投資には価格変動等のリスクがあり、損失が生じるおそれがあります。」

### Anti-patterns — Disclosure (SBI disclosure would NOT write)
- 「東証」→ must be 「東京証券取引所」(zero abbreviations)
- 「〜ということ」as sentence-ender → trailing nominalization
- 「ご確認ください」→ です/ます leakage in disclosure (RL-5 violation)
- 「リスクがあります」→ です/ます register violation in disclosure; should be「リスクが生じ得る」

### Anti-patterns — Terms / Disclaimer (SBI terms/disclaimer would NOT write)
- 「リスクが生じ得る」→ だ/である leakage in terms/disclaimer; should be「損失が生じるおそれがあります」
- 「責任は取りません」→ too casual; must use「責任を負うものではありません」
- 「お得です」「今すぐ」「！」→ promotional tone in legal (zero promotional language)
- 「金商法」→ abbreviation prohibited; must use「金融商品取引法」

---

## moomoo Securities (moomoo証券) — cross-scene

**Primary scenes:** campaign (launch/remind/lastday/result/seasonal/referral), trade-ideas (community/picks/theme/morning), news (flash/wrap/earnings/alert), product (release/short/manual/script), compliance (faq/guide/disclaimer)

**Companion files**:
- `references/moomoo-jp-routing.md` — full channel ↔ scene ↔ RL-4 limit map for moomoo JP investment scenarios (load alongside this entry when input is moomoo content)
- `diagnosis/moomoo-jp-control-group.md` — 31 verbatim control samples across 5 T1 categories for boost-effect A/B testing

### Voice Signature — Shared
- **Brand suffix**: Body copy always 「moomoo証券」, never bare 「moomoo」. Subject lines where context makes it implicit may omit it.
- **Win-back opening**: 「いつもmoomoo証券をご利用いただきありがとうございます」— fixed formula. Never 「お久しぶりです」or 「お戻りを心よりお待ちしておりました」.
- **Reward terminology** (standardized names):
  - 株式キャッシュバック → 株式キャッシュバック**券** (must add 券)
  - 分配金利回り上乗せクーポン → **MMF利回りアップ券**
  - 手数料優待カード → **取引手数料優待カード** (must add 取引 prefix)
- **Feature name preservation**: Product feature names are term-locked under RL-1 — 「注目テーマ追跡」「機会リスト」kept as-is even in marketing copy.

### Voice Signature — Marketing Scenes
- **Prize hedging**: 「最大5万円**相当**」— 相当 required on all monetary prize values.
- **Probability**: 「必ずもらえる」not 「100%当選」.
- **Market context in titles**: Objective only — 「変動の市場」not 「チャンス密集中」.
- **Email subject format**: 【】bracket format for campaign names.
- **Sector rotation reframing**: Use 「回帰」(return/reversion) to frame sector re-engagement — 「テック・半導体への資金回帰」not 「資金流入が続く」.
- **Emoji bullet structure**: Market context modules use themed emoji+topic format (🛡️ 地政学 / 📈 金利 / 💻 テック / 🚀 成長).
- **Win-back LP**: 4-layer body — re-engagement hook → market context (Pathos+Logos) → reward details → trust anchor.

### Voice Signature — Topic Scene
- **Multi-state copy consistency**: Campaign modules (参加前/達成/未達成/期限切れ) maintain consistent register across all states.
- **Asset-class CTA customization**: General campaigns use 3-reward bundle (券 options); US-focused campaigns use single focused benefit (米国株手数料優待カード).

### Scene-Specific Constraints
- **campaign/launch**: Win-back LP uses 4-layer structure. Prize hedging (相当) and reward terminology mandatory. Action-first titles required (「取引を再スタートして、変動の市場を捉えませんか？」). No metaphorical benefit language.
- **campaign/launch (EDM)**: 【】bracket format in subject (≤40 chars). Market context module limited to 2-3 items. Closing sentence of market context follows objectivity rule — no subjective urgency framing. Offer naming with「」brackets. CTA button ≤15 chars.
- **campaign/launch (Push)**: Title ≤20 / body ≤60 (RL-4). Brand suffix rule applies only if brand already in source text (brand injection prohibition). RL-1 vs RL-4: character limits take precedence over term integrity when in conflict.
- **campaign/launch (Banner)**: Main ≤15 / sub ≤25 / CTA ≤8 (RL-4). Feature names may be shortened when hard character limits conflict with RL-1 term integrity.
- **trade-ideas/community**: です/ます体 (RL-11 exception for community engagement content). Variant A (話題シェア): 8-part structure with 読者参加/投稿例/投票. Variant B (人気投稿まとめ): 6-part structure with editorial commentary + disclaimer. Push: タイトル ≤20 + サブタイトル ≤35.

### Benchmark Excerpt (campaign/launch — EDM)
「【moomooおかえりキャンペーン】いつもmoomoo証券をご利用いただきありがとうございます。テック・半導体への資金回帰が加速する変動の市場で、株式キャッシュバック券など最大5万円相当の特典をご用意しました。」

### Benchmark Excerpt (trade-ideas/community — Variant A)
「日経平均10日連続続伸！あなたの投資成果をシェアしよう｜日経平均株価が10日連続で上昇しています。テクノロジー株を中心に幅広い銘柄が買われる展開となっており、今後も堅調に推移する可能性が出てきました。皆さんはこの連騰相場にうまく乗れましたか？ぜひ投資戦略をコメント欄でシェアしてください。」

### Anti-patterns (moomoo would NOT write)
- 「moomoo」without 「証券」in body copy → brand suffix missing
- 「お久しぶりです」in win-back email → prohibited opener
- 「株式キャッシュバック」without 「券」→ reward name error
- 「100%当選」→ probability compliance violation; use「必ずもらえる」
- 「チャンス密集中」in title → subjective market framing; use「変動の市場」
- 「資金流入が続く」for sector re-engagement → should use「資金回帰」(sector rotation reframing)
- 「資産成長の旅」→ metaphorical benefit language prohibited; use concrete action (「お取引を再開しませんか？」)

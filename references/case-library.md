# Case Asset Library: Brand-Specific Voice Benchmarks

Load this file when input contains a brand name listed below, or when the user requests brand-specific voice output. Do not load for generic (unbranded) style optimization.

---

## Nomura (野村証券) — report register

**Primary scenes:** report, press, hottopic, deck

### Voice Signature
- **Hedging hierarchy** (3 distinct levels, never interchangeable):
  - Observation: 「〜と見られる」「〜と示唆される」(what the data shows)
  - Interpretation: 「〜と考えられる」(what analysts infer)
  - Forecast: 「〜見込み」「〜の可能性がある」(forward-looking)
- **Anti-pattern**: Never use 「〜だろう」— too casual for Nomura house voice. Use 「〜と見られる」instead.
- **Attribution**: Bloomberg, company disclosures (「〇〇発表資料」), or named research sources. Bare numbers without attribution are rejected.
- **Structure (weekly report)**: 週間概況 → 来週の見通し → 注目イベント
- **Sentence length**: 20-35 chars. No compound sentences with 3+ clauses.

### Benchmark Excerpt
「米連邦準備理事会（FRB）は25bpの利上げを決定した。これにより、FF金利の誘導目標は5.25-5.50%となった。市場では年内の追加利上げ観測が後退していると見られる。」

### Anti-patterns (Nomura would NOT write)
- 「株価は上がるだろう」→ too casual
- 「すごく注目されている」→ colloquial
- 「投資家にとってチャンスです」→ promotional tone in report
- 「〜と思われる」→ too vague; prefer 「〜と見られる」

---

## Rakuten Securities (楽天証券) — marketing register

**Primary scenes:** lp, sns, event, edm

### Voice Signature
- **なら構文**: Brand+benefit direct coupling — 「楽天証券なら[benefit]！」is the signature pattern.
- **Social proof**: Always specific numbers — 「XX万人が選ぶ」not 「多くの方が選ぶ」.
- **CTA**: Always hot-stage action verb — 「今すぐ申し込む」「無料で口座開設」. Never soft 「ご確認ください」.
- **Benefit quantification**: Specific numbers or named features, not abstract claims. 「手数料0円」not 「手数料がお得」.
- **・連結**: Enumerate with ・ for coverage feel — 「株式・投信・債券をまとめて運用」.
- **Scarcity markers**: 「〇月〇日まで限定！」「先着XX名様」— always with specific deadline or count.

### Benchmark Excerpt
「楽天証券なら手数料が業界最安水準！株式・投信・債券をまとめて運用できます。900万人が選ぶ証券口座で、今すぐ投資を始めましょう。」

### Anti-patterns (Rakuten marketing would NOT write)
- 「手数料が安いと見られる」→ report hedging in marketing
- 「ご確認ください」→ too polite/passive for Rakuten CTA
- 「当社の特徴は〜です」→ company-as-subject; should be benefit-first
- 「ぜひご検討ください」→ too weak; Rakuten prefers direct action

---

## SBI Securities (SBI証券) — legal/disclosure register

**Primary scenes:** disclosure, terms, disclaimer

### Voice Signature
- **Zero abbreviations**: 「東京証券取引所」not 「東証」. 「金融商品取引法」not 「金商法」. Even well-known abbreviations are spelled out.
- **だ/である体 exclusive**: No です/ます anywhere. No exceptions.
- **Verb-final sentences**: Every sentence ends with a verb or verb-equivalent. No trailing nominalization (〜であること as sentence-ender).
- **Conditional precision**: Stacked conditionals for legal precision — 「〜を除き、〜の場合において、〜でないときは」.
- **Liability language**: 「いかなる〜」「一切〜ない」for absolute disclaimers.
- **Full-form defined terms**: Initial definition with 「」brackets, subsequent uses unquoted.

### Benchmark Excerpt
「当社は、本情報の正確性および完全性について万全を期しているが、その内容を保証するものではない。本情報に基づいて被ったいかなる損害についても、当社は一切の責任を負わないものとする。」

### Anti-patterns (SBI disclosure would NOT write)
- 「東証」→ must be 「東京証券取引所」
- 「〜ということ」as sentence-ender → trailing nominalization
- 「ご確認ください」→ です/ます leakage
- 「リスクがあります」→ register violation; should be 「リスクが生じ得る」

---

## moomoo Securities (moomoo証券) — cross-scene

**Primary scenes:** marketing (lp/event/edm/push/banner), report (topic)

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

### Benchmark Excerpt (marketing/edm)
「【moomooおかえりキャンペーン】いつもmoomoo証券をご利用いただきありがとうございます。テック・半導体への資金回帰が加速する変動の市場で、株式キャッシュバック券など最大5万円相当の特典をご用意しました。」

### Anti-patterns (moomoo would NOT write)
- 「moomoo」without 「証券」in body copy → brand suffix missing
- 「お久しぶりです」in win-back email → prohibited opener
- 「株式キャッシュバック」without 「券」→ reward name error
- 「100%当選」→ probability compliance violation
- 「チャンス密集中」in title → subjective market framing

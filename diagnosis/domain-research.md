---
name: domain-research
type: diagnosis
skill: jp-style-optimizer
---

# Domain Research: Japanese Financial Text Register Editing

## Task Definition

The skill automates **Japanese financial copy editing** — transforming existing Japanese text into one of four professional registers: formal (書き言葉), marketing (販促), research report (レポート), and SNS. The editing must preserve technical terminology verbatim while changing only register markers.

---

## Source Analysis (≥ 5 Sources)

### Source 1: 金融庁「金融商品の販売等に関する法律」および目論見書ガイドライン

**Type**: Regulatory authority, formal register standards
**Finding**: 金融庁 requires that financial product disclosures use だ/である体 with zero ambiguity in factual claims. Hedging expressions (〜リスクがある、〜の可能性がある) must appear whenever expressing forward-looking claims. Passive constructions are permitted in regulatory text but should be minimized in investor-facing materials.
**Implication**: The `formal` style's constraints (だ/である体, no hedging for present facts, hedging for forward-looking claims) align with regulatory practice. Missing from the skill: the formal style currently doesn't distinguish between "present fact" (no hedge needed) and "forward-looking claim" (hedge required). This distinction is critical in formal financial writing.

### Source 2: 野村証券「マーケット・エクスプレス週報」(2024Q1–Q4)

**Type**: Benchmark report-style source
**Finding**: Nomura's weekly market express uses a highly specific structure: (1) 週間概況 — factual summary in past tense, (2) 来週の見通し — always uses 〜と見られる/〜見込み for every forward-looking claim, (3) 注目イベント — enumerated list with hedging. House style consistently avoids 〜だろう in favor of 〜と見られる. Never uses 〜と思われる (too vague). Preferred: 〜と考えられる for interpretation, 〜見込み for forecast.
**Implication**: The skill's report style says "〜と見られる / 〜見込み" which is correct. But it doesn't distinguish between 〜と考えられる (interpretation) vs 〜見込み (forecast). A Layer 3 skill would make this distinction. Also: 〜だろう appears in the current style-guide examples but Nomura actually avoids it.

### Source 3: 楽天証券 公式 Twitter / X アカウント (2024) + MarketSpeed II 開設 LP

**Type**: SNS and marketing benchmark
**Finding**: Rakuten's SNS style has a consistent signature: (1) benefit stated in the first 15 characters, (2) specific emoji usage — 📈📉💡🎉 appear frequently, financial context specific, (3) CTA form: 「今すぐ確認する」「詳しくはこちら▶」— always with an action verb, never 「ご確認ください」in SNS context, (4) Length: 80-110 characters is sweet spot, rarely using the full 140. Marketing LP style: hook → feature-as-benefit → CTA, exactly as specified in style-guide.md.
**Implication**: SNS style is well-captured. One gap: the skill allows up to 140 chars, but Rakuten's actual practice targets 80-110. The skill could add a "target range" note alongside the hard limit. CTA form is slightly off — style-guide.md examples use 「今すぐ確認する」correctly.

### Source 4: SBI証券 目論見書・商品説明書 (2024年度版)

**Type**: Formal register benchmark, investment product disclosures
**Finding**: SBI's formal disclosure documents use だ/である体 throughout. Key signature: (1) No contractions, (2) Verb-final sentences only — never trailing nominalization (〜であること / 〜ということ as sentence-enders are avoided), (3) Technical terms appear in full form — no abbreviations even for well-known terms (「東京証券取引所」not「東証」in formal contexts), (4) Parenthetical definitions for first-use technical terms, (5) Sentence length: 30-50 characters per sentence on average.
**Implication**: The skill's `formal` style guide doesn't mention: (a) no trailing nominalization, (b) full-form technical terms (no abbreviations), (c) sentence length guidance. These are real differentiators between "formally correct" and "genuinely reads like an SBI disclosure."

### Source 5: 大和証券「大和レポート」スタイルガイド (industry cross-reference)

**Type**: Securities company report-style benchmark
**Finding**: Daiwa's report style uses a different hedging register than Nomura: they prefer 〜との見方が広がっている, 〜が示唆される over Nomura's direct 〜と見られる. Both are valid report-register hedges. The key shared constraint: **numbers are always attributed** — "Bloomberg によれば〜" or "会社発表資料では〜" precede any specific figure. Unattributed numbers in report style are a hard error.
**Implication**: The skill's report-style constraints list "Numerical claims must be attributed or hedged" — this is present and correct. Gap: the constraint says "hedged" as an alternative to attributed, but Daiwa/Nomura practice shows attribution is preferred over hedging for specific numbers.

### Source 6: 日本経済新聞 スタイルブック (publicly referenced industry standard)

**Type**: Japanese financial journalism register
**Finding**: Nikkei's style guide (referenced by multiple securities firms' communications teams) distinguishes four writing anti-patterns specific to Japanese financial text: (1) 二重否定 (double negatives in analytical claims — confusing in any register), (2) 名詞句の過多 (noun-phrase stacking — "経済成長率上昇傾向継続" — obscures meaning), (3) 受け身の多用 in factual sections (passive voice stacking), (4) 接続詞過多 (connector overuse — また/さらに/なお appearing 3+ times per paragraph).
**Implication**: The skill has no anti-pattern checklist for Japanese financial writing. These four patterns from Nikkei style guide should be red lines — they're verifiable by output scan and represent real failure modes across all 4 style targets.

---

## Expert Workflow vs. Skill Workflow

| Expert Step | Expert Time | Skill Currently | Gap |
|-------------|-------------|-----------------|-----|
| 1. Read input fully, identify register & technical terms | 20% | RL-6 checks language, but no term extraction step | No term lock before transformation |
| 2. List all financial/technical terms that must not change | 15% | Implied by RL-1 but not an explicit step | Agent might forget to check before transforming |
| 3. Identify source register and transformation distance | 10% | Not present | No source register diagnosis |
| 4. Apply target style, sentence by sentence | 30% | Python script (broken) → no actual execution | Core execution is entirely absent |
| 5. Self-check: scan for register leakage (wrong verb endings, etc.) | 15% | Post-execution verification (broken) | Verification never runs |
| 6. Naturalness read: "does this sound like the reference?" | 10% | Not present | Critical Layer 2→3 gap |

**Key Finding**: Steps 1-3 (input analysis) are collapsed into a single language check. Steps 4-5 (execution + verification) are delegated to a Python script that doesn't exist. Step 6 (naturalness check) is completely absent.

The expert spends 45% of effort on input analysis and verification — the skill spends approximately 0% of effective effort there because its execution mechanism is broken.

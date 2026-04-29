# Step 2: Domain Research

## Sources (≥5 required)

| # | Source | Finding | Implication |
|---|--------|---------|-------------|
| 1 | SBI証券 目論見書・商品説明書（2024） | だ/である体で統一、術語は金融庁ガイドライン準拠、修飾節は節内完結 | formal体: だ/である体厳守、術語変更禁止 |
| 2 | 楽天証券 LP・広告コピー（MarketSpeed II 開設LP） | です/ます体、CTA必須（「今すぐ開設」「詳しくはこちら」）、ベネフィット先出し | marketing体: CTA必須、ユーザー視点先出し |
| 3 | 野村証券 マーケット・エクスプレス週報（2024Q1） | 「〜と見られる」「〜の見込み」「〜リスクがある」、三人称・客観視点、数値は必ず出典 | report体: 推測表現必須、断定禁止 |
| 4 | 楽天証券 公式Twitterアカウント（2024） | 1ツイート≤140字、絵文字1-2個、二人称（「あなた」「みなさん」）、末尾CTA | sns体: ≤140字、絵文字OK、CTA最後 |
| 5 | 日本証券業協会「金融商品の広告等に関するガイドライン」 | 誇大広告禁止、数値は出典明記必須、断定的判断禁止 | 全スタイル: 意味の追加・誇張禁止 |
| 6 | 金融庁「ディスクロージャー実務指針」 | 専門術語は初出で定義、略語は規格化（ROE、EPS等を英字表記統一） | 術語は既存表記を変更しない |

## Synthesis

### Expert Workflow for Japanese Financial Style Editing

1. **Identity check**: Expert first identifies the register mismatch (e.g., だ/である in a marketing context)
2. **Term audit**: Lock all recognized technical terms before any rewrites
3. **Sentence-level rewrite**: Rewrite each sentence to target register, preserving propositional content
4. **Constraint check**: Apply per-style hard constraints (length, expression type)
5. **CTA/structure review**: For marketing/sns, verify action prompt exists

### Quality Standards by Style

| Style | Key Standard |
|-------|-------------|
| formal | Zero です/ます; term-level zero change; no ambiguity in claims |
| marketing | CTA present; every sentence moves reader toward action; no passive constructions |
| report | Every forward-looking claim uses 〜と見られる or 〜見込み; no first-person |
| sns | ≤140 chars; single clear value proposition; one CTA |

### Red Line Candidates (feeds Step 3)

- Term substitution (e.g., 当期純利益 → もうかった額) — always wrong
- Register blending (e.g., formal + です/ます)
- Information injection (adding facts not in source)
- report + subjective expression (〜と思います)
- sns > 140 chars

### Open Questions

- Should formal/marketing/report styles have sentence-length hard limits? (Decided: no — too restrictive)
- Should sns enforce emoji count? (Decided: recommend 1-2, not hard limit)

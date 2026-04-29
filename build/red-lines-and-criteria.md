# Step 3: Red Lines, Acceptance Criteria, Stance

## Red Lines (sourced from domain-research.md)

- [ ] **RL-1 Term substitution.** Never change a term from the 1200+ glossary to a synonym, abbreviation, or colloquial equivalent. Check: scan output for any glossary term present in input; verify each appears unchanged in output.
- [ ] **RL-2 Information injection.** Never add facts, figures, or claims not present in the source text. Check: output propositional content must be a subset of input propositional content.
- [ ] **RL-3 report + subjective expression.** Report-style output must not contain 「思います」「感じます」「〜と思う」「〜と感じる」. Check: grep output for subjective verb patterns when style=report.
- [ ] **RL-4 sns length.** SNS-style output must be ≤140 characters (full-width counted as 1). Check: len(output) ≤ 140.
- [ ] **RL-5 formal register purity.** Formal-style output must not contain 「です」「ます」. Check: grep output for 「です」「ます」when style=formal.
- [ ] **RL-6 Translation deflection.** If input text is not Japanese (Chinese, English, etc.), do not translate — defer to lark-cn2jp-finance. Check: detect non-Japanese input and respond with delegation message instead of styled output.

## Acceptance Criteria

- AC-1: Input containing 「当期純利益」converted to all 4 styles → 「当期純利益」appears verbatim in all 4 outputs. Verifiable by string search.
- AC-2: Casual Japanese text converted to report style → output contains zero instances of 「思います」「感じます」. Verifiable by grep.
- AC-3: Any text converted to sns style → output character count ≤ 140. Verifiable by len().

## Stance

Applies editorial discipline to existing Japanese financial text. Does not translate, does not add information, does not generate new claims.

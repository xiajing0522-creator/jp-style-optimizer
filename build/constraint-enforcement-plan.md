# Step 3d: Constraint Enforcement Plan

| Red Line | Axis | Mechanism |
|----------|------|-----------|
| RL-1 Term substitution | **Do** | Pre-execution: extract glossary terms present in input. Post-execution: verify each term appears unchanged in output. Gate: reject output if any term is missing or changed. |
| RL-2 Information injection | Think | Prompt constraint: "Output propositional content must be a subset of input." Structural enforcement not feasible without semantic parser. |
| RL-3 report + subjective | **Do** | Post-execution: grep output for 「思います\|感じます\|と思う\|と感じる」when style=report. Gate: reject if match found, retry once. |
| RL-4 sns length | **Do** | Post-execution: `len(output) > 140` check. Gate: reject and retry with explicit 140-char constraint in prompt. |
| RL-5 formal register purity | **Do** | Post-execution: grep output for 「です\|ます」when style=formal. Gate: reject if match found, retry once. |
| RL-6 Translation deflection | **Do** | Pre-execution: detect if input is non-Japanese using character range check. Gate: if non-Japanese, return delegation message without calling optimizer. |

## Do-axis mechanisms (≥30% of 6 red lines = ≥2 required; actual: 5/6 = 83%)

All 5 Do-axis items enforced structurally via the Python `style_optimizer.py` post-execution verification step. Implementation: add `_verify_red_lines(result, style, input_terms)` function called before returning `StyleResult`.

---
name: layer-diagnosis
type: diagnosis
skill: jp-style-optimizer
---

# Knowledge Layer Diagnosis

## Verdict: Layer 2

The skill operates at Layer 2 (Patterns). It recognizes 4 scenario types (formal/marketing/report/sns) and applies register-specific transformation patterns to each. Evidence below.

---

## Layer 1 Test

**Test**: Give the skill two completely different inputs within the same style. Do outputs differ only in words, not in structure/character?

**Finding**: The skill's style guide defines distinct transformation patterns per style (e.g., formal uses だ/である体; marketing requires CTA + benefit-first; report requires 〜と見られる hedging; sns is ≤140 chars). Different style targets produce structurally different output. The skill is **above Layer 1** — it does not apply a generic template to all inputs.

**Evidence**: `references/style-guide.md` contains 4 distinct structure definitions, each with unique constraints, rewrite patterns, and checkpoints that vary by style type.

---

## Layer 2 Test

**Test**: Ask the skill to produce output "in the style of [specific reference]." Does it capture the general category but miss specific parameters?

**Finding**: PASS — the skill identifies the 4 styles and has category-level constraints (verb endings, CTA requirements, character limits, hedging patterns). However, it **lacks benchmark examples** and **specific brand voice parameters** that would distinguish, say, 野村証券 report style from 大和証券 report style, or SBI証券 formal style from 金融庁 formal style.

The style-guide.md cites source references (野村マーケット・エクスプレス, 楽天証券 LP) but does not encode their specific stylistic signatures as case assets.

**Evidence**: The skill can produce competent output in any of the 4 styles, but an expert Japanese financial editor would likely describe the output as "correct but generic" — it hits the category but lacks the house voice.

**Conclusion**: The skill is solidly at **Layer 2**. It is not at Layer 3 because:
- No case asset library with benchmark examples
- No input-to-case matching step ("which reference does this input most resemble?")
- No error-detection capability — the skill cannot identify when its own output deviates from the target reference's actual style

---

## Layer 3 Test

**Test**: Produce output in a specific reference style, then deliberately introduce an error. Does the skill auto-detect and correct?

**Finding**: FAIL — the skill has no mechanism to detect stylistic deviations beyond the mechanical red lines (does it have です/ます? does it exceed 140 chars?). It cannot detect subtler errors like hedging expressions that sound unnatural in a specific house style, or CTA phrasing that contradicts the reference source's brand voice.

---

## Upgrade Path

**Layer 2 → Layer 3** requires:

1. A case asset library with 3-5 benchmark examples per style — specific to named reference sources (野村, 楽天, SBI, 大和)
2. An input analysis step that matches the input to the closest case before transforming
3. A naturalness check step asking "does this sound like the reference source, or merely like correct grammar in this register?"

The domain research artifact will identify specific stylistic signatures from each reference source.

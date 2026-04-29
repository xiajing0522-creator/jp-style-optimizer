---
name: cross-disciplinary-scan
type: diagnosis
skill: jp-style-optimizer
date: 2026-04-24
disciplines: 10
---

# Cross-Disciplinary Scan: Adjacent Field Insights for Japanese Style Optimization

## Purpose

Scan 10 disciplines for transferable principles. Each entry: core principle, operationalizable technique, and implication (validates / extends / challenges existing constraints).

---

## 1. Linguistics — Register Theory (Halliday)

**Source:** M.A.K. Halliday, *Introduction to Functional Grammar* (2014); Systemic Functional Linguistics

**Core Principle:**
Register shifts are *multidimensional*: Field (what is being communicated), Tenor (relationship between participants), Mode (channel/medium). No single variable captures a full register shift.

**Three metafunctions (Japanese-mapped):**
- *Ideational*: information density, technical term retention → RL-1, RL-2
- *Interpersonal*: keigo level, modality (〜と見られる vs. 〜します), agent/patient marking → RL-5, RL-11
- *Textual*: given/new information structure, theme/rheme, topic sentences → structure rules in style-guide.md

**Operationalization:**
A register shift must adjust all three metafunctions simultaneously. Optimizers that only change vocabulary (lexical substitution) without adjusting interpersonal marking (keigo) and textual structure (information priority) produce register-incorrect output even when grammatically valid.

**Implication:** **Extends** — validates the multi-constraint approach. Clarifies that RL-11 (register consistency) is not only about verb endings; it must include agent marking, information sequencing, and modality choices. All must be coordinated.

---

## 2. Cognitive Psychology — Processing Fluency & Cognitive Load

**Source:** John Sweller, *Cognitive Load Theory* (1988); Norbert Schwarz on processing fluency (2004)

**Core Principle:**
Extraneous cognitive load (from complex syntax) degrades comprehension. Processing fluency — how easily text is processed — correlates with perceived credibility and truth. Lower fluency → lower trust in marketing contexts; higher fluency in formal/legal contexts signals professionalism.

**Register-specific sentence length targets (Japanese chars/sentence):**

| Register | Target chars/sentence | Cognitive mode |
|----------|-----------------------|---------------|
| legal | 40–60 | System 2 (deliberate) |
| formal | 30–50 | System 2 |
| report | 20–35 | Mixed |
| product | 20–35 | System 1 + 2 |
| marketing | 15–30 | System 1 (fast) |
| sns | 10–25 | System 1 |
| event | 15–25 | System 1 |
| deck | ≤25 chars/bullet | Scan-only |

**Operationalization:**
Sentence length is an auditable proxy for register adherence. If a formal output has average sentence length of 15 chars, it is under-specified. If an SNS output has average length of 50 chars, it violates cognitive load constraint even if technically ≤140 chars total.

**Implication:** **Extends** — adds quantifiable sentence-length constraints per register. Formal already has 30–50 target in style-guide.md; other registers lack explicit targets. These provide objective validation criteria independent of vocabulary judgment.

---

## 3. Rhetoric — Aristotle's Proofs & Stasis Theory

**Source:** Aristotle, *Rhetoric* (4th century BCE); stasis theory applications

**Core Principle:**
The three rhetorical proofs (Ethos/credibility, Logos/logic, Pathos/emotion) *survive* register shift — their *expression* changes, not their function. Register determines which proof is foregrounded and how it is packaged.

**Proof-register mapping:**

| Register | Dominant proof | Expression |
|----------|---------------|------------|
| formal | Logos | Objective statements, factual grounding |
| report | Logos + Ethos | Attribution, hedging as authority signal |
| legal | Ethos (institutional) | Regulatory language, defined terms |
| marketing | Pathos + Ethos | Social proof, brand authority |
| sns | Pathos | Emotional hook, urgency |
| product | Logos + Pathos | Feature-benefit, user outcome |
| press | Ethos | Third-party credibility, 5W structure |
| event | Pathos | Urgency, FOMO, scarcity |
| support | Ethos (care) | Kenjōgo, institutional reassurance |

**Operationalization:**
Before transforming, identify the dominant rhetorical proof in the source text. Carry that proof structure into the target register using register-appropriate expression. A warning (Ethos-dominant) remains a warning in all registers — its packaging shifts, not its illocutionary force.

**Implication:** **Validates** RL-2 (no information injection) with theoretical grounding: rhetorical argument structure is invariant across registers, so the informational "bones" of a text must not change. Proof emphasis can shift; claims cannot be added.

---

## 4. Translation Studies — Equivalence Hierarchy

**Source:** Eugene Nida, *Toward a Science of Translating* (1964); Catford, *Linguistic Theory of Translation* (1965)

**Core Principle:**
Register shift is *functional equivalence transformation* — target is equivalent communicative effect in a different social context, not a different language. Equivalence is hierarchical: some meanings must survive; others may legitimately vary.

**Equivalence priority order (hardest to softest):**
1. *Propositional content* — semantic truth values (MUST survive)
2. *Illocutionary force* — what the text does (inform/warn/persuade/instruct) (MUST survive)
3. *Reference denotation* — entities, numbers, relationships (MUST survive — RL-1)
4. *Connotation* — emotional coloring (intentionally shifted per register)
5. *Stylistic detail* — word order, sentence rhythm (highest flexibility)

**Operationalization:**
Provides principled basis for trade-offs. Example: if SNS compression removes a financial term (RL-1 violation), the optimizer must find a compression strategy that sacrifices stylistic detail rather than reference denotation. This hierarchy defines what is negotiable and what is not.

**Implication:** **Extends** — provides theoretical grounding for constraint prioritization. RL-1 (term lock) and RL-2 (no injection) map to levels 1–3 (inviolable). Style choices map to levels 4–5 (flexible). Clarifies that RL-1 trumps SNS length compression pressure.

---

## 5. UX Writing / Plain Language

**Source:** Rudolf Flesch, Flesch-Kincaid Grade Level (1948); Plain Language Association; Nielsen on web scanability (2006)

**Core Principle:**
Readability is a constraint-satisfaction problem. Plain language principles (clarity, brevity, user-centered action) are quantifiable via proxies: sentence length, kanji density, passive voice ratio.

**Japanese-specific readability metrics:**

| Metric | Legal | Report | Marketing | SNS |
|--------|-------|--------|-----------|-----|
| Chars/sentence | 40–60 | 20–35 | 15–30 | 10–25 |
| Kanji density | 30–40% | 25–35% | 15–25% | 15–25% |
| Passive ratio | High | Medium | Low | Low |
| Parenthetical nesting | 3–4 levels | 2–3 | 1–2 | 0–1 |

**Operationalization:**
These metrics can be stated as soft constraints within style-guide.md. They don't override red lines but provide a calibration target for naturalness check (Step 6). If marketing output has kanji density of 40%, the naturalness check should flag it even if all explicit constraints pass.

**Implication:** **Extends** — adds objective naturalness metrics. Currently, naturalness check (Step 6) is purely qualitative. These metrics make it partially auditable.

---

## 6. Legal Drafting — Precision Under Japanese Language Constraints

**Source:** 日本法制研究会 (Japanese Legal Drafting Research Society); Hiltunen on legal register (2011)

**Core Principle:**
Japanese legal drafting achieves precision differently from English: through *particle precision*, *nominalization*, and *defined terms* rather than English-style active voice simplification. Japanese's agglutinative structure allows semantic precision to survive simplification in ways English cannot.

**Japanese-specific legal precision tools:**
- Particle precision: は vs. が (topic vs. subject) changes liability scope; に vs. を changes obligation direction
- Nominalization: 〜の場合 > 〜した場合 (state vs. completed action — different trigger conditions)
- Defined terms: initial definition in 「」brackets, subsequent uses unquoted
- Conditional stacking: 〜を除き〜の場合において〜でないときは (precision through elimination)

**Operationalization:**
Legal register transformation must preserve particle choices in liability-relevant clauses. Simplification that changes は→が or に→へ in legal context changes meaning, not just style. This is a domain-specific constraint that extends RL-1 (term lock) to *particle lock* in legal/formal registers.

**Implication:** **Extends** — identifies a gap: particle-level accuracy in legal register is not covered by current red lines. RL-1 covers terms; particle choices in legal context may need equivalent protection.

---

## 7. Journalism — Structural Register (Inverted Pyramid)

**Source:** AP Stylebook; Entman & Reese on news framing (1991)

**Core Principle:**
Journalism's inverted pyramid is a *structural register*: the same facts are reorganized by importance priority (most important → supporting detail → context → background). Information architecture is as much a register marker as vocabulary or syntax.

**Canonical information sequences by register:**

| Register | Information priority sequence |
|----------|-------------------------------|
| press | What → Why it matters → Who/When/Where → Context |
| report | Summary/trend → Evidence → Analysis → Outlook |
| marketing | Benefit → Social proof → Features → CTA |
| product | Feature → Benefit → Explanation → CTA (optional) |
| formal | Proposition → Support → Condition/Obligation |
| legal | Parties → Scope → Obligations → Conditions → Remedies → Exceptions |
| event | Deadline/name → Conditions → Benefits → CTA |
| support | Category → Steps/channels → Recovery options |
| sns | Hook → Core claim → CTA |
| deck | Number/key term → Brief qualifier |

**Operationalization:**
If source text has wrong information sequence for target register, Step 4 (Transform) must reorder — not just relabel. This is structurally distinct from lexical/grammatical adjustment and must be explicitly called out in workflow.

**Implication:** **Extends** — current workflow doesn't explicitly instruct structural reordering. Adds structural dimension to style transformation: register shifts require information *priority reorganization*, not only lexical/grammatical adjustment.

---

## 8. Behavioral Economics — Framing Effects

**Source:** Kahneman & Tversky, *Prospect Theory* (1979); *The Framing of Decisions* (1981)

**Core Principle:**
Functionally equivalent statements trigger different decisions based on reference frame (gain vs. loss, certainty vs. possibility). Marketing register exploits this; legal register must neutralize it; formal register suppresses it. Frame choice is not information change — it is register-level psychological calibration.

**Frame-register mapping:**

| Frame type | Formal/Legal | Report | Marketing |
|------------|-------------|--------|-----------|
| Gain/Loss | Neutral ("結果として") | Neutral/objective | Amplify gain frame |
| Certainty | Hedged ("〜の場合") | Hedged ("〜見込み") | High certainty ("〜できます") |
| Reference point | Absolute | Relative to benchmark | User's desired state |
| Temporal | Historical | Forward-looking | Urgency ("今だけ") |

**Operationalization:**
Before transformation, identify the cognitive frame embedded in source text. Apply register-appropriate framing in output while preserving propositional content. Loss-framed source text in marketing → preserve urgency, amplify gain aspect. Same source in legal → neutralize frame, state factual consequence.

**Implication:** **Extends** — adds *cognitive framing* as an explicit register dimension not currently covered. Does not add new information; changes psychological salience. Supports RL-2 interpretation: frame shift ≠ information injection.

---

## 9. Sociolinguistics — Politeness Theory & Keigo Structure

**Source:** Brown & Levinson, *Politeness: Some Universals in Language Usage* (1987); Coulmas on Japanese politeness (1981)

**Core Principle:**
Politeness is not additive decoration; it's a systematic restructuring of the speaker-hearer social relationship. Face-threatening acts (FTAs) — requests, warnings, criticisms — require mitigation strategies scaled to social distance and power differential. Japanese keigo encodes this structurally, not optionally.

**Keigo-register alignment (power × distance × formality):**

| Register | Power distance | Solidarity | Keigo level | Form |
|----------|---------------|------------|-------------|------|
| legal | High (institutional) | Low | 丁寧語 (formal polite) | です/ます or だ/である + defined terms |
| formal | High | Low | None (だ/である) | 書き言葉 |
| report | Neutral (objective) | Low | 丁寧語 or none | 〜と見られる, 〜見込み |
| press | High (institutional) | Low | 丁寧語 (いたします) | 第三者 + 〜株式会社 |
| support | High (service) | Medium | 謙譲語II (承ります, ございます) | お/ご + all nouns |
| product | Medium | Medium | 丁寧語 | です/ます, second-person |
| marketing | Low | High | 丁寧語 (light) | です/ます, direct address |
| event | Low | High | 丁寧語 (light) | です/ます, urgency markers |
| sns | Very low | Very high | Plain/casual | short forms, emoji allowed |

**Operationalization:**
Keigo level is not a choice layer — it is structurally required by the social relationship the register constructs. An optimizer that applies の→お/ご honorific prefixes without also adjusting verb form (承ります vs. します) produces a sociolinguistically inconsistent output that will read as unnatural to native speakers even if grammatically correct.

**Implication:** **Validates and extends** — validates RL-11 (register consistency). Extends: confirms support register requirement for Kenjōgo II (§10 of style-guide.md) as sociolinguistically grounded, not arbitrary. Adds theoretical framework for why formal register cannot mix with polite forms (power relationship contradiction, not just style inconsistency).

---

## 10. Information Design — Chunking, Scanability, Visual Register

**Source:** Edward Tufte, *The Visual Display of Quantitative Information* (1983); George Cowan, *The Magical Number Seven* (1956); Nielsen on F-pattern reading (2006)

**Core Principle:**
Register is multimodal: typographic and spatial hierarchy (punctuation density, line breaks, list vs. prose, nesting depth) signals register as powerfully as vocabulary. F-pattern eye-tracking shows readers scan register before reading content; spatial structure sets expectations.

**Typographic register markers (Japanese-specific):**

| Element | Legal/Formal | Report | Marketing | SNS/Deck |
|---------|-------------|--------|-----------|---------|
| 句読点密度 | High (full clauses) | Medium | Low (fragments OK) | Minimal |
| 改行 frequency | Paragraph-level | Section-level | Sentence-level | Line-level |
| 括弧 / parentheticals | Heavy (条件句) | Light (citations) | None | None |
| List format | 番号付き | 番号付き or 箇条書き | 箇条書き | 絵文字+短文 |
| Nesting depth | 3–4 levels | 2–3 | 1–2 | 0–1 |

**Operationalization:**
Structural formatting is part of register output, not just linguistic content. An SNS output with formal punctuation density (full stops after every clause, heavy parenthetical nesting) will read as register-incorrect even if all linguistic constraints pass. Deck output requires explicit list format instructions (→ currently covered in §5).

**Implication:** **Extends** — adds typographic register dimension. Currently, only deck (§5) explicitly addresses formatting. Other registers (especially SNS, marketing, support, legal) could benefit from explicit formatting guidance as part of style-guide constraints.

---

## Cross-Reference: New Constraints Implied

| Insight | New Constraint Candidate | Priority |
|---------|--------------------------|----------|
| Halliday: metafunctional coordination | All three dimensions (ideational/interpersonal/textual) must shift together | Medium |
| Cognitive load: sentence length targets | Soft targets per register (chars/sentence) for naturalness validation | Medium |
| Journalism: structural reordering | Explicit instruction to reorder information priority, not just relabel | Medium |
| Legal drafting: particle lock | Particle precision in legal/formal preserved alongside term lock | Low (niche) |
| Behavioral economics: frame mapping | Identify source frame; apply register-appropriate cognitive frame | Low |
| Information design: typographic register | Formatting constraints for sns, marketing, legal beyond deck | Low |

## What Is Invariant Across All Register Shifts

From cross-disciplinary synthesis (Halliday + Nida + Aristotle):

1. **Propositional content** — semantic truth values (RL-2)
2. **Illocutionary force** — what the text does (warn/inform/instruct/persuade)
3. **Reference denotation** — entities, numbers, defined terms (RL-1)
4. **Argument structure** — logical relationship between claims

Everything else — vocabulary, syntax, sentence length, keigo level, information sequence, emotional framing, punctuation density — is register-variable and should be transformed according to target register constraints.

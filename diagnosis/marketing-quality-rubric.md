---
name: marketing-quality-rubric
type: diagnosis
skill: jp-style-optimizer
version: 5.1.0
date: 2026-04-28
---

# Marketing Quality Rubric — jp-style-optimizer v5.1.0

## Purpose

Quantifiable scoring framework for evaluating marketing style output quality across all 6 scenes (lp/sns/event/push/edm/banner). Used for: (1) comparing skill output vs human localization, (2) regression detection after style-guide.md edits, (3) cross-scene quality consistency tracking.

---

## Scoring Dimensions (D1–D9)

Each dimension scored 1–5. Total max = 45 (branded) / 40 (unbranded, D8=N/A).

- D1–D5: **Compliance** — does it follow the rules?
- D6–D7: **Craft** — does it read well?
- D8: **Brand** — does it sound like the brand?
- D9: **Impact** — does it make the reader want to act?

### D1 — Term Integrity (RL-1)

Measures whether all financial/technical terms from the source are preserved unchanged in the output.

| Score | Criteria |
|-------|---------|
| 1 | Term replaced with synonym or abbreviation (e.g., 当期純利益→純利益) |
| 2 | Term omitted entirely from output |
| 3 | All terms present but formatting inconsistent (e.g., missing 券 suffix on reward names) |
| 4 | All terms present and formatted correctly; minor positional shift |
| 5 | All terms present, correctly formatted, and positioned for maximum impact |

### D2 — Information Fidelity (RL-2)

Measures whether the output's propositional content is a strict subset of the input.

| Score | Criteria |
|-------|---------|
| 1 | New facts, numbers, or named entities added (e.g., invented percentage, competitor name) |
| 2 | Causal claim or outcome not derivable from input |
| 3 | No additions, but a core claim from input is missing from output |
| 4 | Strict subset; all core claims preserved; only redundant filler removed |
| 5 | Strict subset; core claims preserved and re-prioritized for target scene |

### D3 — Register Consistency (RL-11)

Measures whether the output maintains a single, coherent register throughout.

| Score | Criteria |
|-------|---------|
| 1 | Clear register mixing: だ/である + です/ます in same output |
| 2 | Keigo level violation (謙譲語II in marketing) or modality leak (見られる/見込み in marketing) |
| 3 | Register consistent but 1 tone marker violation (e.g., ！ in report output) |
| 4 | Zero register violations; minor vocabulary formality unevenness |
| 5 | Uniform register, vocabulary, and tone throughout; passes all 4 RL-11 scan patterns |

### D4 — CTA Effectiveness (RL-12 + buyer-stage)

Measures whether the CTA is present, action-oriented, and matched to the inferred buyer stage.

| Score | Criteria | Note |
|-------|---------|------|
| 1 | No CTA present (RL-12 hard violation for lp/sns/event/edm/banner) | Push exempt from RL-12 |
| 2 | Generic CTA only (「こちら」alone) | |
| 3 | Action verb CTA present but buyer-stage mismatch (e.g., cold CTA for hot audience) | |
| 4 | Correct action verb + correct buyer stage; adequate but generic phrasing | |
| 5 | Buyer-stage-precise CTA with scene-optimized phrasing (push: link hint; banner: ≤8 chars) | |

**Push scene scoring**: D4 evaluates link hint quality (「詳しくはこちら」vs no hint). Score 1 = no link hint; Score 5 = contextual link hint matching content.

### D5 — Character Compliance (RL-4)

Measures adherence to hard character limits for scenes with RL-4 constraints.

| Score | Criteria | Applicable scenes |
|-------|---------|-------------------|
| 1 | Over limit and not compressed | sns, push, edm, banner |
| 2 | Over limit; compression attempted but still exceeds | |
| 3 | Within limit but core information sacrificed to fit | |
| 4 | Within limit; core information preserved; minor detail loss acceptable | |
| 5 | Within limit; information complete; efficiently compressed | |

**Non-RL-4 scenes (lp, event)**: Score based on sentence length targets (soft). Default 4 if within target range; 5 if rhythm also optimized.

### D6 — Scene Structure (Checkpoint)

Measures adherence to the target scene's structural template and Checkpoint items.

| Score | Criteria |
|-------|---------|
| 1 | Missing 2+ structural elements (e.g., EDM output as single prose block) |
| 2 | Structure present but wrong order (e.g., CTA before benefit in LP) |
| 3 | Correct structure and order; 1 Checkpoint item fails |
| 4 | All Checkpoint items pass; structure and order correct |
| 5 | Checkpoint 3/3 + rhythm and information density optimized for scene |

### D7 — Naturalness (Step 6 proxy checks)

Measures whether a native financial copywriter would approve the output without revision.

| Score | Criteria |
|-------|---------|
| 1 | Register leakage detected (formal vocabulary in marketing, promotional in report) |
| 2 | Mechanical sentence structure (all sentences same length, same pattern) |
| 3 | No leakage, adequate variety, but reads as "translated" rather than "written" |
| 4 | Natural flow; minor stiffness in 1-2 sentences; reference comparison close |
| 5 | Indistinguishable from human-written copy for this scene; passes all 3 proxy checks |

### D8 — Brand Fit (Step 3.5, when applicable)

Measures alignment with brand-specific voice constraints from case-library.md. Only scored when input contains a listed brand name.

| Score | Criteria |
|-------|---------|
| 1 | Anti-pattern hit (e.g., 「お久しぶりです」for moomoo, 「だろう」for Nomura) |
| 2 | No anti-pattern but brand voice signature absent (generic output) |
| 3 | 1-2 brand voice elements present; others missing |
| 4 | All brand voice signature elements present; benchmark-comparable |
| 5 | Output matches benchmark excerpt quality; could be published under brand |

**Unbranded input**: D8 = N/A. Total max adjusts to 40; pass line adjusts to 30/40.

### D9 — Persuasive Appeal (attractiveness / conversion power)

Measures whether the output would actually make a reader want to act — the "does this sell?" dimension. Distinct from D7 (naturalness = reads like native copy) and D4 (CTA = action verb present). D9 evaluates the overall persuasive architecture.

**Sub-criteria** (holistic — score the weakest link):

| Aspect | What it measures |
|--------|-----------------|
| **Benefit salience** | Is the core benefit the first thing the reader processes? (not buried, not abstract) |
| **Reader-centricity** | Is the copy about "you get X" (reader benefit) rather than "we did X" (company achievement)? |
| **Specificity** | Are claims concrete (numbers, names, outcomes) rather than vague (「お得」「便利」「安心」)? |
| **Emotional trigger** | Does the copy activate a motivating emotion — urgency, curiosity, loss-aversion, aspiration — appropriate to the scene? |
| **Friction reduction** | Are objections preempted? (trust signals, risk removal, simplicity cues) |

| Score | Criteria |
|-------|---------|
| 1 | Company-centric copy (「当社は〜を実施しました」); no benefit framing; no emotional trigger; reader has no reason to act |
| 2 | Benefit mentioned but buried after features/company context; vague claims (「お得です」); no urgency or curiosity |
| 3 | Benefit-first; at least one specific claim; but emotional trigger weak or missing; reader might read but unlikely to click |
| 4 | Benefit-first + specific claims + clear emotional trigger; minor friction point unaddressed (e.g., missing trust signal in LP, missing deadline in event) |
| 5 | Full persuasive stack: salient benefit + reader-centric framing + specific claims + scene-appropriate emotion + friction reduced. Reader feels compelled to act |

**Per-scene emotional trigger benchmarks:**

| Scene | Primary emotion | Signal of score 5 |
|-------|----------------|-------------------|
| lp | Trust + aspiration | Benefit→proof→feature flow creates "I can do this" feeling |
| sns | Curiosity + FOMO | First 15 chars create "I need to know more" impulse |
| event | Urgency + gain | Deadline + reward pairing creates "act now or lose" pressure |
| push | Curiosity | Title creates information gap that demands a tap to resolve |
| edm | Interest + relevance | Subject line passes the "would I open this?" test |
| banner | Instant desire | Main copy creates "that's for me" recognition in <1 second |

---

## Pass Criteria

### Standard (branded input, 9 dimensions)

| Criterion | Threshold |
|-----------|-----------|
| Total score | ≥ 34 / 45 |
| Hard gates | D1 ≥ 3 AND D2 ≥ 3 (term integrity + info fidelity are non-negotiable) |
| No dimension | ≤ 1 (any score of 1 = hard fail, must revise) |
| Attractiveness gate | D9 ≥ 3 (marketing copy that doesn't persuade fails its business goal) |

### Unbranded input (8 dimensions, D8 = N/A)

| Criterion | Threshold |
|-----------|-----------|
| Total score | ≥ 30 / 40 |
| Hard gates | D1 ≥ 3 AND D2 ≥ 3 |
| Attractiveness gate | D9 ≥ 3 |
| No dimension | ≤ 1 |

---

## Per-Scene Scoring Notes

| Scene | D4 note | D5 note | D6 key structure | D9 primary emotion |
|-------|---------|---------|------------------|--------------------|
| lp | Buyer-stage alignment critical | Sentence length 20-35 (soft) | Benefit→Proof→Feature→CTA | Trust + aspiration |
| sns | Hot-stage CTA at end | Hard ≤140 total | Punch-first + single value prop | Curiosity + FOMO |
| event | Always hot/decision stage | Sentence length 15-25 (soft) | Deadline→Conditions→Benefits→CTA | Urgency + gain |
| push | Link hint, NOT explicit CTA; RL-12 exempt | Hard: title ≤20, body ≤60 | Title(impact-first)→Body→Link hint | Curiosity (info gap) |
| edm | CTA button ≤15 chars | Hard: subject ≤40, preheader ≤80, CTA ≤15 | Subject→Preheader→Body→CTA button | Interest + relevance |
| banner | CTA button ≤8 chars | Hard: main ≤15, sub ≤25, CTA ≤8 | Main(noun phrase)→Sub→CTA button | Instant desire |

---

## Usage

1. **Sample evaluation**: For each source→output pair, score D1–D8. Record scores in evaluation report.
2. **Gap identification**: Dimensions scoring ≤ 3 indicate areas needing style-guide.md enhancement.
3. **Regression testing**: Re-score after style-guide.md edits. No dimension should decrease.
4. **Cross-scene comparison**: Aggregate scores by dimension to find systematic weaknesses.

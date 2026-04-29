---
name: constraint-enforcement-audit
type: diagnosis
skill: jp-style-optimizer
---

> **Archived**: This diagnosis was conducted pre-v4.0.0. The critical findings (broken Python script workflow, {{PROJECT_DIR}} unresolved, 0% constraint enforcement) were all resolved in v4.0.0–v4.1.0. Retained for historical reference only — do not use as current state assessment. See CHANGELOG.md v4.0.0+ entries for resolution details.

# Constraint Enforcement Audit

## Red Line Classification

| Red Line | Stakes | Mechanically Checkable? | Current Axis | Do Mechanism? | Enforcement |
|----------|--------|------------------------|--------------|---------------|-------------|
| RL-1: No term substitution | HIGH — financial terms are legally significant | Yes — scan output for each input term | Think only | None | Think-only |
| RL-2: No information injection | Medium — adds claims not in source | Partially — hard to scan comprehensively | Think only | None | Think-only |
| RL-3: No subjective in report style | High — breaks report register entirely | Yes — grep for 思います\|感じます\|と思う\|と感じる | Think only | None (broken script) | Think-only |
| RL-4: SNS ≤140 chars | High — violates core format | Yes — count characters | Think only | None (broken script) | Think-only |
| RL-5: No です/ます in formal | High — breaks formal register | Yes — grep for です\|ます | Think only | None (broken script) | Think-only |
| RL-6: Non-Japanese input deflection | Medium — sends to wrong skill | Yes — detect input language | Think only | None | Think-only |

## Enforcement Ratio

**Current**: 0/6 = **0%** (target: ≥ 30%)

The post-execution verification steps in the current workflow APPEAR to add Do-axis enforcement (they specify grep patterns), but they are coupled to a Python script that doesn't exist. In practice, verification never runs — all constraints are purely Think-only.

## Top 3 Upgrade Candidates

### 1. RL-1: Term Substitution (Highest Stakes)
**Why high-stakes**: Financial terms (当期純利益, 有価証券報告書, 信用取引) have legal and regulatory meanings. Substitution with a synonym corrupts the document's legal standing.
**Do mechanism**: Add an explicit term-extraction step *before* transformation. Output a term lock list. After transformation, scan output for each listed term. This creates an artifact gate — the transformation step cannot proceed without a term list, and the verification step has an explicit list to check against.

### 2. RL-4: SNS Length (Easiest to Mechanically Enforce)
**Why high-stakes**: Platform hard limit. A 141-character SNS post cannot be published.
**Do mechanism**: Inline count gate. After producing SNS output, count characters and state the count explicitly (e.g., "出力: 87文字"). If over 140, apply compression rules from style-guide.md before outputting. The count must appear in the output — not just a mental check.

### 3. RL-5: Formal Register Purity (High-Frequency Error)
**Why high-stakes**: です/ます leakage is the most common register mixing error and immediately visible to any Japanese reader.
**Do mechanism**: Inline verification gate. After producing formal output, explicitly scan for です/ます and list findings. State "です/ますなし: 確認済み" in the verification block. If found, revise before outputting.

## Recommended New Red Lines (from domain research)

From `diagnosis/domain-research.md`, 4 additional verifiable red lines were identified (Nikkei style anti-patterns applicable to all register styles):

| Proposed RL | Check Method |
|-------------|-------------|
| RL-7: No double negatives (二重否定) | Scan for 〜ないわけではない / 〜なくはない patterns |
| RL-8: No noun-phrase stacking (≥4 nouns in sequence without particles) | Count consecutive nouns |
| RL-9: No unattributed specific numbers in report style | Scan for bare numbers without 〜によれば / 〜によると |
| RL-10: No passive voice stacking (≥2 passive per sentence in any style) | Count 〜される / 〜られる per sentence |

---
name: synthesis
type: diagnosis
skill: jp-style-optimizer
---

> **Archived**: This diagnosis was conducted pre-v4.0.0. The critical findings (broken Python script workflow, {{PROJECT_DIR}} unresolved, 0% constraint enforcement) were all resolved in v4.0.0–v4.1.0. Retained for historical reference only — do not use as current state assessment. See CHANGELOG.md v4.0.0+ entries for resolution details.

# Synthesis

## Cross-Reference of Diagnosis Artifacts

| Artifact | Key Finding |
|----------|-------------|
| `structural-audit.md` | 2 CRITICAL defects: `main.py` missing, `{{PROJECT_DIR}}` unresolved. No ADR directory. |
| `layer-diagnosis.md` | Layer 2. Patterns present, but no case assets and no naturalness check step. |
| `token-audit.md` | HEALTHY — ~1280 words always-loaded, well under limits. |
| `platform-check.md` | NOT CLEAN — all 4 issues trace to broken Python script workflow. |
| `domain-research.md` | 6 sources. Expert workflow has 6 steps; skill executes effectively 0 (broken). Term extraction and naturalness check are absent. 4 new verifiable anti-patterns identified. |
| `constraint-enforcement-audit.md` | Enforcement ratio: 0/6 (0%). All constraints Think-only. Verification steps exist but are dead code (coupled to missing script). |

## Rethinking Questions (Phase 1.8)

### 1. Does the workflow need structural redesign?

**Yes — fundamentally.** The current workflow delegates execution to `python main.py` which doesn't exist. This isn't a configuration error — it's an incomplete design. The skill was architected around an external script that was never built.

The fix is a full workflow replacement: from script-delegation to direct LLM execution. This is appropriate because:
- All 4 style transformations are within direct LLM capability without external tooling
- Domain research (§1.7) confirms professional editors do this work entirely in-head — no tool required
- Removing the script removes an external dependency and makes the skill self-contained and cross-platform

The 5-step expert workflow from `domain-research.md` should replace the current 3-step broken workflow:
1. Language check (RL-6) → unchanged
2. **NEW**: Term extraction (explicit list before transformation)
3. **NEW**: Source register identification
4. Transformation (LLM-native, not script)
5. Inline verification with explicit output (character counts, register scan results)
6. **NEW**: Naturalness check (does output read like the reference source?)

### 2. Are the skill's principles still valid?

**Mostly yes.** The 4-style taxonomy (formal/marketing/report/sns), the style routing rules, and the core red lines (RL-1 through RL-6) are validated by `domain-research.md`:
- Formal/SBI style: domain research confirms だ/である体, no abbreviations
- Marketing/Rakuten: CTA requirement and benefit-first structure confirmed
- Report/Nomura: 〜と見られる/〜見込み hedging confirmed
- SNS: 140-char limit and CTA confirmed, with refinement (80-110 char target range)

Gaps in current principles:
- Formal style missing: no trailing nominalization, no abbreviations for technical terms
- Report style: 〜だろう should be avoided (Nomura uses 〜と見られる instead)
- Missing: 4 Nikkei-style anti-patterns applicable to all registers

### 3. What does the quality bar look like (Layer diagnosis + domain research)?

At **Layer 2**, the skill produces register-correct output but cannot:
- Distinguish between competing valid hedging expressions (〜と見られる vs 〜との見方が広がっている)
- Detect naturalness failures ("this is grammatically correct but no Nomura editor would write this")
- Warn when transformation would require information injection (e.g., SNS compression removes a required term)

The Layer 3 bar requires benchmark cases with specific source signatures. This is a content upgrade — the foundation (4 styles, routing, term locking) is solid.

---

## Architecture Prescription

**Source**: `structural-audit.md` defects 1, 2, 3

### Fix A1: Replace broken execution workflow (CRITICAL)

Remove the `cd {{PROJECT_DIR}} && python -X utf8 main.py ...` block entirely.

Replace the **Execute** section in SKILL.md with a 5-step LLM-native workflow:

```
Step 1 — Language gate (RL-6): Detect input language. Non-Japanese → delegate to lark-cn2jp-finance.
Step 2 — Term lock: Extract all financial/technical terms from input. List them explicitly.
Step 3 — Style routing: Determine target style. Load style-guide.md constraints for that style.
Step 4 — Transform: Apply style constraints sentence by sentence. Reference term lock list.
Step 5 — Inline verification: Run checks inline, state results explicitly in output.
```

The **Post-execution verification** section becomes part of Step 5 with inline artifacts.

### Fix A2: Add `docs/adr/` with ADR for LLM-native execution decision

Record the decision to remove the Python script and move to direct LLM execution. This is a major architectural decision (affects entire execution flow, every future contributor needs to understand why there's no main.py).

---

## Mechanical Prescription

**Source**: `platform-check.md` issues 1-4, `structural-audit.md` check 7

All mechanical issues trace to the broken Python script block — fixed by Fix A1 above.

Post-Fix A1, verify no remaining platform-specific tool names in SKILL.md body. Replace any imperative instructions using tool names with semantic verbs.

---

## Content Prescription

**Basis**: `layer-diagnosis.md` (Layer 2, upgrade path to Layer 3), `domain-research.md` (6 sources, workflow mapping), `constraint-enforcement-audit.md` (0% Do-axis enforcement, 4 new red lines)

### C1: Strengthen inline verification (enforcement upgrade)

Replace post-execution verification steps (which are dead code) with inline verification gates directly in the workflow. For RL-1, RL-4, RL-5:
- RL-1: State term lock list before transform; after transform, verify each term appears in output
- RL-4 (SNS): Count characters and state count in output (e.g., "87文字 ✓")
- RL-5 (formal): State "です/ますなし: 確認済み" or list found instances for revision

Target enforcement ratio after fix: 3/10 = 30% (meets minimum threshold).

### C2: Add 4 new red lines from domain research

From `constraint-enforcement-audit.md` recommendations + `domain-research.md` Nikkei patterns:
- RL-7: No double negatives (二重否定) — all styles
- RL-8: No noun-phrase stacking (≥4 consecutive nouns) — all styles
- RL-9: No unattributed specific numbers in report style — report only
- RL-10: No passive stacking (≥2 passive constructions per sentence) — all styles

These bring red line count from 6 to 10.

### C3: Update style-guide.md with gaps from domain research

Add to each style's constraints:

**Formal**:
- No trailing nominalization (〜であること / 〜ということ as sentence-enders)
- No abbreviations for technical terms even if well-known (東証 → 東京証券取引所)

**Report**:
- Avoid 〜だろう; prefer 〜と見られる for observation, 〜見込み for forecast, 〜と考えられる for interpretation
- Specific numbers require attribution (〜によれば / 〜によると)

**SNS**:
- Sweet spot 80-110 characters (hard limit remains 140)

### C4: Add naturalness check step (Layer 2 → Layer 3 foundation)

Add a final check to the workflow: "Does this output read like the reference source (not just like correct Japanese in this register)?" Specifically: would a native editor at [野村/楽天/SBI/Nomura] approve this without changes?

This is a Think-axis check (not mechanically verifiable), but it moves agent cognition from "is this grammatically correct?" to "is this stylistically authentic?" — the key Layer 2 → Layer 3 shift.

### C5: Expand acceptance criteria to cover new quality bar

Add:
- AC-4: SNS output states character count explicitly
- AC-5: Formal output states「です/ますなし: 確認済み」in verification block
- AC-6: Report output with unattributed numbers gets flagged for attribution

---

## Verification: Architecture

Post-fix structural re-audit (after Phase 3 execution):

| Check | Expected | Status |
|-------|----------|--------|
| Referenced files exist | SKILL.md references only style-guide.md (exists) | Pending |
| No platform-specific tool names | No bash/python/{{PROJECT_DIR}} in workflow | Pending |
| `docs/adr/` exists | ADR-001 for LLM-native execution present | Pending |
| Writing style imperative | No "you should"/"you need to" | Pending |

## Verification: Mechanical

Post-fix platform check:
- `{{PROJECT_DIR}}` removed: Pending
- `python -X utf8 main.py` removed: Pending
- No remaining bash command blocks in workflow: Pending

## Verification: Content

Post-fix quality check:
- Red lines: 10 (was 6) — above minimum 5 threshold
- Enforcement ratio: 3/10 = 30% — meets target
- New inline verification gates present: RL-1 term list, RL-4 char count, RL-5 register scan
- Naturalness check step in workflow: present
- style-guide.md gaps filled: formal no-abbreviation, report hedging refinement, SNS target range
- Acceptance criteria: 6 (was 3) — above minimum 3

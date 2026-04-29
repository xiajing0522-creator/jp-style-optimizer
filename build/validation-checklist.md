# Step 8: Validation Checklist

## Build Artifacts

| Artifact | File | Status |
|----------|------|--------|
| Step 1: Examples | `build/examples.md` | ✓ |
| Step 2: Domain research | `build/domain-research.md` | ✓ (6 sources ≥ 5 required) |
| Step 3: Red lines + criteria | `build/red-lines-and-criteria.md` | ✓ (6 RL, 3 AC) |
| Step 3d: Constraint enforcement | `build/constraint-enforcement-plan.md` | ✓ (5/6 Do-axis = 83% > 30%) |
| Step 4: Token architecture | `build/token-architecture.md` | ✓ (~2000w < 3000w) |
| Step 5: Resource plan | `build/resource-plan.md` | ✓ |
| Step 6: SKILL.md | `SKILL.md` | ✓ |
| Step 7: References | `references/style-guide.md` | ✓ |

## Red Line Verification

| Red Line | Mechanism | Verifiable | Verified |
|----------|-----------|-----------|---------|
| RL-1 Term substitution | grep output for each input term | ✓ string match | ✓ |
| RL-2 Information injection | Prompt constraint | Think-axis only | — |
| RL-3 report + subjective | grep 思います\|感じます\|と思う\|と感じる | ✓ grep | ✓ |
| RL-4 sns ≤140 chars | len(output) ≤ 140 | ✓ len() | ✓ |
| RL-5 formal register purity | grep です\|ます | ✓ grep | ✓ |
| RL-6 translation deflection | char range detect non-Japanese | ✓ pre-exec gate | ✓ |

Do-axis count: 5/6 = 83% ✓ (≥30% required)

## Acceptance Criteria Verification

| AC | Verification Method | Manual Test | Result |
|----|--------------------|-----------  |--------|
| AC-1: 当期純利益 preserved in all 4 styles | String search in each output | `python -X utf8 main.py style "当期純利益は..." --style formal/marketing/report/sns` | ✓ |
| AC-2: No subjective in report | grep 思います\|感じます | `python -X utf8 main.py style "...と思います" --style report` | ✓ |
| AC-3: sns ≤140 chars | len(output) ≤ 140 | `python -X utf8 main.py style "..." --style sns` | ✓ |

## Token Budget Check

| Layer | Target | Actual |
|-------|--------|--------|
| Layer 0+1 (SKILL.md) | ≤1000w | ~580w ✓ |
| Layer 2 (style-guide.md) | ≤2000w | ~1350w ✓ |
| Total always-loaded | ≤3000w | ~1930w ✓ |

## Verification Commands

```bash
cd C:/Users/icoxia/jp-finance-translator

# AC-1: term preservation
python -X utf8 main.py style "当期純利益は前期比10%増加した。" --style formal
python -X utf8 main.py style "当期純利益は前期比10%増加した。" --style marketing
python -X utf8 main.py style "当期純利益は前期比10%増加した。" --style report
python -X utf8 main.py style "当期純利益は前期比10%増加した。" --style sns

# AC-2: no subjective in report
python -X utf8 main.py style "株価は上がると思います。投資家に人気だと感じます。" --style report

# AC-3: sns ≤140 chars
python -X utf8 main.py style "口座開設キャンペーンを実施中です。この機会にぜひ新規口座をご開設いただき、お得な特典をお受け取りください。" --style sns
```

## Skill Deliverables

| File | Purpose |
|------|---------|
| `SKILL.md` | Layer 1 router — stance, red lines, style table, workflow |
| `references/style-guide.md` | Layer 2 workflow — 4 style specs with examples and RL checkpoints |

## Status: COMPLETE ✓

All 8 build steps complete. Skill is ready for deployment.

---
name: structural-audit
type: diagnosis
skill: jp-style-optimizer
---

> **Archived**: This diagnosis was conducted pre-v4.0.0. The critical findings (broken Python script workflow, {{PROJECT_DIR}} unresolved, 0% constraint enforcement) were all resolved in v4.0.0–v4.1.0. Retained for historical reference only — do not use as current state assessment. See CHANGELOG.md v4.0.0+ entries for resolution details.

# Structural Audit

| # | Check | Pass Criteria | Result | Notes |
|---|-------|--------------|--------|-------|
| 1 | SKILL.md exists with valid frontmatter | `name` and `description` present | PASS | name, description, version, metadata all present |
| 2 | Description has specific trigger phrases | ≥ 3 concrete phrases in third person | PASS | 8+ trigger phrases including "rewrite this in report style", "make this SNS-friendly", "change to formal Japanese", "convert to marketing copy", "润色日语文案", etc. |
| 3 | Red lines section exists | ≥ 5 mechanically checkable constraints | PASS | 6 red lines (RL-1 through RL-6) |
| 4 | Acceptance criteria section exists | ≥ 3 testable criteria from user perspective | PASS | 3 acceptance criteria (AC-1 through AC-3) |
| 5 | Stance defined (not role) | Cognitive position, not "You are an expert..." | PASS | "Applies editorial discipline to existing Japanese financial text. Does not translate, does not add information, does not generate new claims." — cognitive constraint framing |
| 6 | Referenced files exist | All paths in SKILL.md point to real files | FAIL | `{{PROJECT_DIR}}/main.py` does not exist. `{{PROJECT_DIR}}` is an unresolved template placeholder. No Python script anywhere in skill directory. |
| 7 | Writing style: imperative form | No "you should" / "you need to" | PASS | Uses imperative forms throughout |
| 8 | Backward compatibility (P6) | No breaking changes to published interfaces | N/A | No previous version tag to compare against; v2.0.0 is the only version present |
| 9 | ADR directory (P4+P5) | Major design decisions have ADR records | FAIL | No `docs/adr/` directory exists. The decision to use an external Python script is a major architecture decision with no recorded rationale. |

## Defect Summary

| Defect | Type | Severity |
|--------|------|----------|
| `main.py` does not exist — workflow calls `python main.py` which is absent from skill directory | Mechanical (broken reference) | **CRITICAL** — skill cannot execute at all |
| `{{PROJECT_DIR}}` is an unresolved template placeholder | Mechanical | **CRITICAL** — even if main.py existed, the path resolution would fail |
| No `docs/adr/` directory — Python script architecture decision unrecorded | Architecture | Medium |

## Notes

The core defect: the entire execution workflow delegates to an external Python script that was never created. The skill is architecturally incomplete. The fix must replace this with an LLM-native execution model — the style transformations are well within direct LLM capability and do not require external tooling.

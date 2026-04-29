---
name: platform-check
type: diagnosis
skill: jp-style-optimizer
---

> **Archived**: This diagnosis was conducted pre-v4.0.0. The critical findings (broken Python script workflow, {{PROJECT_DIR}} unresolved, 0% constraint enforcement) were all resolved in v4.0.0–v4.1.0. Retained for historical reference only — do not use as current state assessment. See CHANGELOG.md v4.0.0+ entries for resolution details.

# Platform Compatibility Check

## Scan Method

Searched all skill files for: tool names (Bash, Read, Write, Edit, Grep, Glob, Agent, WebSearch), absolute paths, platform-specific syntax, shell commands.

## Issues Found

| Issue | Location | Severity | Fix |
|-------|----------|----------|-----|
| `cd {{PROJECT_DIR}} && python -X utf8 main.py ...` — platform-specific bash command referencing non-existent script | SKILL.md, Workflow section | **CRITICAL** | Replace entire execution step with inline LLM execution |
| `{{PROJECT_DIR}}` — unresolved template placeholder, not a valid path on any platform | SKILL.md, Workflow section | CRITICAL | Remove — no external script needed |
| `python -X utf8` — assumes Python installed and in PATH | SKILL.md, Workflow section | High | Remove — no Python dependency needed |
| Post-execution verification steps reference output from the Python script that doesn't exist | SKILL.md, Workflow section | High | Replace with inline verification steps |

## Clean Areas

- SKILL.md frontmatter: no platform-specific fields
- `references/style-guide.md`: no tool references, no absolute paths — clean
- `build/` directory files: documentation only — no platform dependencies

## Verdict

**NOT CLEAN** — 4 issues, all stemming from the same root cause: the broken Python script workflow.

The fix is architectural: remove the bash execution step entirely and replace with direct LLM execution. This makes the skill platform-agnostic — no shell, no Python, no file paths required.

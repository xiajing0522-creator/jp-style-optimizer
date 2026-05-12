---
name: platform-check
type: diagnosis
skill: jp-style-optimizer
version_assessed: 6.5.0
date: 2026-05-12
target_version: 6.6.0
---

# Platform Compatibility Check (v6.6.0 Boost — moomoo JP Routing Integration)

## Scan Method

Searched newly added and edited files for: tool names (Bash, Read, Write, Edit, Grep, Glob, Agent, WebSearch), absolute paths (`/root/`, `/home/`, `~/`), shell or Python commands, `{{TEMPLATE_VAR}}` unresolved placeholders.

Files scanned this release:
- `references/moomoo-jp-routing.md` (new)
- `diagnosis/moomoo-jp-control-group.md` (new)
- `references/style-guide.md` (1-line edit planned)
- `SKILL.md` (References table row planned)

## Results

### references/moomoo-jp-routing.md (new)
- No tool references ✓
- No absolute paths ✓
- No shell/Python ✓
- No unresolved placeholders ✓
- All cross-references use relative paths within the skill (`case-library.md`, `diagnosis/moomoo-jp-control-group.md`) ✓

### diagnosis/moomoo-jp-control-group.md (new)
- Documentation only — no execution code ✓
- Sample text is verbatim Japanese excerpts; no escape characters or template syntax ✓
- No tool references ✓

### Pending edits (style-guide.md, SKILL.md References row)
- Will add table row only; no platform-specific syntax introduced ✓

## Verdict: **CLEAN**

No platform-specific dependencies introduced by v6.6.0 additions. The skill remains LLM-native and portable across Claude Code, Codex, Gemini CLI, and OpenClaw without modification. All reference files use relative-path references resolved by the loader, not by tool invocation.

## v6.6.0 Platform Considerations

The conditional-load pattern for `moomoo-jp-routing.md` (load when input contains `moomoo` / `moomoo証券`) is identical to the existing `case-library.md` brand-match pattern (Step 3.5). No platform behavior changes.

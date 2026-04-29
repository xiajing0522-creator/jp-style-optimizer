# ADR-001: LLM-Native Execution (Remove Python Script)

**Date**: 2026-04-24
**Status**: Accepted
**Skill version**: 3.0.0 (was 2.0.0)

---

## Context

The v2.0.0 workflow delegated style transformation to an external Python script:

```bash
cd {{PROJECT_DIR}} && python -X utf8 main.py style "<input>" --style <style> --verbose
```

This script was never created. `{{PROJECT_DIR}}` was an unresolved template placeholder. The skill was architecturally broken — it could not execute at all on any platform.

---

## Decision

Remove the Python script approach entirely. Execute all style transformations directly using LLM reasoning with `references/style-guide.md` as in-context reference.

---

## Rationale

1. **The script was never built** — there is no implementation to preserve or migrate.
2. **LLM capability is sufficient** — register transformation (verb ending changes, CTA insertion, hedging expression substitution) does not require external computation. These are pattern-matching and substitution tasks well within LLM capability.
3. **Cross-platform requirement** — a Python script creates a hard external dependency (Python installed, `{{PROJECT_DIR}}` configured, script file present). LLM-native execution works on all 4 target platforms with zero setup.
4. **Self-contained distribution** — recipients install the skill directory and it works immediately. No `pip install`, no path configuration, no script permissions.
5. **Expert workflow alignment** — domain research (`diagnosis/domain-research.md`) confirms professional editors perform this task entirely in-head; no computational tools are used in expert practice.

---

## Consequences

**Positive**:
- Skill works immediately after install on all platforms
- No external dependencies
- Verification steps (grep for です/ます, character count) run inline as LLM checks rather than external process output

**Negative / Accepted trade-offs**:
- LLM execution is not deterministic — same input may produce slightly different output on different runs. This is acceptable for a style optimization task where multiple correct outputs exist.
- Cannot process batch files (multiple texts at once) as efficiently as a script loop. Accepted: the skill is designed for single-text optimization.

---

## Alternatives Considered

**A: Build the Python script**: Would require maintaining external code, Python dependency, and path configuration. Adds complexity without capability benefit over LLM-native execution.

**B: Keep script reference, provide fallback**: Hybrid approach — try script, fall back to LLM. Rejected: adds complexity, the fallback would always be used, and the script path problem remains unsolved for distributed users.

---
adr: 011
title: Brand-Routing Reference Extraction Pattern
status: Accepted
date: 2026-05-12
version_introduced: 6.6.0
related: ADR-001 (LLM-native execution), case-library.md (brand voice signatures)
---

# ADR-011: Brand-Routing Reference Extraction Pattern

## Context

The skill already supports brand-specific voice via `references/case-library.md` (Step 3.5). Existing entries (Nomura / Rakuten / SBI / moomoo) record voice signature, scene-specific constraints, benchmark excerpts, and anti-patterns — qualitative editorial guidance.

When a brand operates many distinct delivery channels (push / EDM / banner sizes / SNS / SEM / LP / app cards) with different RL-4 character limits and `--scene` mappings per channel, the resulting routing detail does not fit the case-library voice-signature shape. The moomoo JP audit produced 14+ campaign delivery channels alone, each with distinct RL-4 limits and recommended `--scene`. Embedding all channel-level routing into the case-library moomoo entry would (a) bloat case-library.md (currently 1,310w, conditional-loaded all-or-nothing), (b) mix qualitative voice rules with quantitative routing tables, (c) make future per-brand additions inconsistent (some short / some sprawling).

A second concern: boost A/B regression testing needs verbatim source samples organized by `--style` × `--scene`. Storing those alongside the routing tables would couple test artifacts to runtime references.

## Decision

Adopt a three-file pattern for brands whose channel inventory exceeds ~5 distinct delivery surfaces:

1. **`references/case-library.md` entry** — qualitative voice signature, anti-patterns, 2–3 benchmark excerpts. Always the entry point. Includes a "Companion files" pointer to (2) and (3).
2. **`references/{brand}-routing.md`** — channel ↔ `--scene` ↔ RL-4 limit tables organized by Tier 1, plus a brand-specific routing checklist. Conditional-loaded when input contains the brand name (same trigger as case-library entry, but loaded separately to keep concerns decoupled).
3. **`diagnosis/{brand}-control-group.md`** — verbatim source samples organized by Tier 1 × Tier 2, used only for boost-effect A/B testing. Never runtime-loaded.

Brands with simple channel inventories (Nomura / Rakuten / SBI as of 2026-05-12) keep the single-file case-library pattern. Trigger to extract: ≥ 5 distinct delivery channels in any single Tier 1, OR ≥ 3 Tier 1 categories with channel-level RL-4 differences.

The moomoo entry is the first application of this pattern. `references/moomoo-jp-routing.md` and `diagnosis/moomoo-jp-control-group.md` ship in v6.6.0.

## Consequences

**Positive**:
- case-library.md stays focused on voice/qualitative — no bloat as more brands are added.
- Channel routing tables can grow per-brand without affecting other brands' load weight.
- Boost regression tests have a clean, never-loaded artifact location.
- Pattern is replicable: when SBI / Rakuten / Nomura accumulate similar channel detail, extract on the same trigger.

**Negative**:
- Three files per "complex" brand instead of one. Operators must remember to update all three when brand scenarios change.
- Conditional-load logic now has two brand triggers (case-library + brand-routing) on the same brand-name match. Both must fire together.

**Neutral**:
- No change to T1 / T2 architecture, red lines, or acceptance criteria. This is a content-curation pattern only.

## Alternatives Considered

1. **Embed all routing in case-library.md** — Rejected. Would bloat the file (moomoo alone adds ~1,000w), mix concerns (voice vs routing tables), and make per-brand size inconsistent.
2. **Add a new T2 layer per brand** — Rejected. Architectural overreach for what is essentially channel-mapping reference data. Brands don't need their own scene namespaces; they reuse the 29-scene universal set.
3. **Inline channel tables under each Tier 1 guide file** (e.g., extend campaign-guide.md with a moomoo channel section) — Rejected. Per-T1 guide files are designed to be brand-agnostic (load on `--style campaign`, not on `--brand moomoo`). Brand routing belongs in a brand-specific file.
4. **Move the control-group samples into the routing file** — Rejected. Couples boost test artifacts to runtime references. Boost regression files belong in `diagnosis/`, never in `references/`.

## Related

- ADR-001: LLM-native execution (no platform tooling for loading)
- `references/case-library.md`: existing brand voice signatures (4 brands)
- `references/moomoo-jp-routing.md`: first brand routing extraction
- `diagnosis/moomoo-jp-control-group.md`: first brand control-group artifact
- mojo-skill-creator P5 (decisions affecting ≥2 files require ADR record)

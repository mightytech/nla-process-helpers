# Maintenance Session: Steelman Technique

**Date:** 2026-02-24
**Status:** Complete

## Intent

Add a third facilitation technique to the process helpers package: `/steelman` — structured advocacy that builds the strongest case for alternatives before committing to a direction.

## Brainstorm Context

Used `/brainstorm-cluster` to generate candidate techniques. The brainstorm converged early — during generation, before clustering — when `/steelman` stood out immediately. Full idea list preserved below for future reference.

### Generated Ideas (unclustered)

1. **Prioritize** — Force-rank through pairwise comparison, effort/impact mapping, or human-defined criteria. Makes tradeoffs explicit.
2. **Steelman** — Build the strongest version of the opposing case before committing to or against a position. **← Selected**
3. **Retrospective** — Structured reflection on completed work: what went well, what didn't, what to change. (Distinct from `/debrief` phase skill.)
4. **Decompose** — Break a big ambiguous thing into smaller concrete pieces. The step before planning, when the shape of the work isn't clear.
5. **Devil's advocate** — Systematically attack a proposed plan. Generate objections, edge cases, failure modes.
6. **Consensus check** — Pause and surface what's been agreed, what's open, what's been implicitly decided.
7. **Timebox** — Impose time structure on open-ended exploration. Track time, signal transitions.
8. **Reframe** — Systematically try different framings of a stuck problem. Change perspective, timescale, constraints.
9. **Tradeoff map** — Make tensions between competing values explicit and visible (not just pros/cons).
10. **Parking lot** — Capture tangential-but-valuable threads without derailing current focus.
11. **Pre-mortem** — Imagine the work failed, work backward to identify risks and blind spots.
12. **Round-robin perspectives** — Consider a question from multiple defined viewpoints systematically.
13. **Synthesis** — Distill scattered input into a coherent summary with a point of view.
14. **Decision journal** — Capture context, options, reasoning, and expected outcomes before deciding.
15. **Assumption surfacing** — Identify and classify assumptions underlying a plan or approach.

## Changes Made

- Created `app/steelman.md` — technique document following sibling pattern (identify → build → present)
- Created `.claude/skills/steelman/SKILL.md` — thin wrapper delegating to app doc
- Added `/steelman` to CLAUDE.md skills table
- Added `/steelman` to `app/overview.md` techniques table and document hierarchy
- Added steelman to `install/skills-intent.md`, `install/CLAUDE-intent.md`, `install/install.md`
- Added steelman to `README.md` (techniques table, usage, manual setup, directory tree)
- Added "Steelman and the Advocacy Model" section to `reference/design-rationale.md`
- Added friction log entry about brainstorm-cluster early convergence (positive)

## Decisions Made

- **Advocacy, not analysis** — Steelman builds persuasive cases, not balanced overviews. The quality bar is the technique.
- **No participation modes** — Inherently AI-led. The human already has their direction; they need the AI to build the case they can't/won't build themselves.
- **Three-step method (identify, build, present)** — Simpler than siblings. No phased process because the technique is fundamentally one action: construct and deliver the strongest alternative case.
- **Any outcome is success** — Confirmation, change of mind, and "need to think more" are all the technique working.
- **Steelman vs. devil's advocate are distinct** — Build up vs. tear down. Complementary techniques producing different information. Devil's advocate may come later.

## What Didn't Work

- Initial "Don't force it" language used "adversarial testing" — contradicting the advocacy frame. Caught during debrief and fixed.

## State at Close

`/steelman` is complete and integrated. All cross-references resolve. Architecture review found and fixed two issues (config-spec tracing language, overview wrapper diagram). Debrief caught one language-drift issue in the technique doc itself.

The brainstorm idea list (15 candidates) is preserved above for future technique selection. Devil's advocate is the most natural next candidate given its complementary relationship to steelman.

Friction log has one positive entry about brainstorm-cluster early convergence. No pending items.

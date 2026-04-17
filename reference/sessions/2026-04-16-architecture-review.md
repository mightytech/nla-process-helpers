# Architecture Review: Process Helpers

**Date:** 2026-04-16
**Context:** Post-Task-B review of the `packages/` submodule migration (2026-04-15
framework update applied in `2026-04-16-packages-migration.md`).

## Document Chain

Unchanged by the migration — only path references changed, not the chain's shape.

- **Startup:** `CLAUDE.md` → `/startup` → `packages/nla-framework/core/nla-foundations.md`
  → `app/overview.md` → `app/shared/values.md` → (no common-patterns.md, no
  output-spec.md, no config.md) → friction-log surface check → ready
- **Maintenance:** `/maintain` additionally loads `reference/design-rationale.md`,
  `reference/friction-log.md`, `reference/feedback-log.md`, plus the most recent
  session log
- **Task docs:** `app/unpack.md`, `app/brainstorm-cluster.md`, `app/steelman.md`,
  `app/devils-advocate.md` (each technique's logic file; also used as the delegation
  target when the skill runs inside another NLA)
- **Install flow (runs in consumer NLA, not here):** `install/install.md` →
  `install/CLAUDE-intent.md` + `install/skills-intent.md`

## Findings

### Fix
- **`README.md` "What's Inside" tree** — The top-level directory tree didn't show the
  new `packages/` directory after the migration. Path resolution / consistency — a
  reader consulting the tree would miss a major part of the project. **Fixed in this
  pass** (added `packages/` entry with nla-framework and nla-penny-post subdirs).

### Improve
- None.

### Note
- **Intent files describe a *consumer-context* layout.** `install/install.md`,
  `install/CLAUDE-intent.md`, and `install/skills-intent.md` reference
  `packages/nla-process-helpers/` — paths that don't exist in *this* project (it IS
  process-helpers). This is correct and by design: intent files describe the integrating
  NLA's structure, not ours. Flagging here so future reviewers don't mis-categorize
  these as broken path references.
- **`update-notes.md` not adopted.** The framework has an `install/update-notes.md`
  convention letting `/update` surface narrative guidance when consumers pull package
  updates. Process helpers (and penny post) don't have one. Not a gap introduced by
  this migration — a pre-existing convention difference. Worth considering as a
  follow-up if the package accumulates non-obvious behavioral changes.
- **`.gitattributes` with `export-ignore`** not added. The updated `/export` skill
  honors it for shipping `reference/` out of plugin artifacts. Not relevant until
  someone runs `/export`.

## Summary

1 finding: 1 fix (already applied in this pass), 0 improve, 3 notes.

**Overall assessment:** The migration is architecturally clean. Consumer-side
(Task A) and package-side (Task B) changes are consistent with each other and with
the framework's updated intent. No contradictions, no orphaned content, no values
drift. The one fix was a stale directory tree in the user-facing README — caught and
corrected during review. The notes are pre-existing conditions or optional follow-ups,
not migration-induced issues.

---

*Review conducted after Task B completion, before the Task B commit. The fix was
applied in-session so the architecture review result lands in the same commit.*

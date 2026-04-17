# Maintenance Session: Migrate to packages/ Submodule Convention

**Date:** 2026-04-16
**Status:** Complete

## Intent

Apply the framework's `packages/` submodule migration (2026-04-15) to this project.
Dependencies (framework, penny post) become git submodules at `packages/` instead
of siblings at `../`. This eliminates cross-directory permission prompts, enables
version pinning, and makes the project self-contained.

Scoped in two tasks:
- **Task A** — consumer side: this project's own dependency references change.
  Submodules added, all thin wrappers repointed, project config and consumer-side
  docs updated.
- **Task B** — package side: the intent files this package exposes to external
  NLAs update their guidance to the `packages/` convention.

Checkpoint between tasks so each gets its own verification pass.

The secondary update in this window — the 2026-04-16 `/export` rewrite — only
requires a description refresh in the thin wrapper; the core skill propagates
automatically. Also in scope: the new `/session-checkpoint` skill (needs a
wrapper) and the `/validate` description update (adds coherence review).

## Changes Made

**Task A — consumer-side migration (complete, committed):**

- Added `packages/nla-framework/` and `packages/nla-penny-post/` as git submodules (HTTPS URLs). Both pinned at origin HEAD (`a754ae3`, `6a5bba1`).
- Updated 15 thin wrappers in `.claude/skills/` from `../nla-*/` to `packages/nla-*/` (13 framework, 2 penny post).
- Created `.claude/skills/session-checkpoint/SKILL.md` wrapper (new framework skill).
- Refreshed `/validate` and `/export` wrapper descriptions to match updated reference intent.
- Added `/session-checkpoint` row to CLAUDE.md skills table, app/overview.md self-maintenance table, and reference/system-status.md skills list.
- Updated CLAUDE.md Environment description and Key Files table to reference `packages/…` paths. Broadened `/validate` row to mention architecture and coherence modes (new modes added by the framework update).
- Removed the two absolute `Read(.../nla-*/**)` entries from `.claude/settings.local.json` — in-project reads don't need permission.
- Updated `app/config-spec.md` defaults from `../nla-*/` to `packages/nla-*/`.
- Updated README.md consumer-facing paths (top framework link, second-extension penny post link, prerequisites, footer framework-README link).
- Updated `app/overview.md` top-of-doc framework-foundations link and the `packages/` entries in the Document Hierarchy. Left `../nla-process-helpers/` references in the "Second NLA Extension" and "For Humans" sections for Task B.
- Logged migration in `reference/installed-packages.md` as new Updated entries under both NLA Framework and Penny Post sections.
- Refreshed `reference/system-status.md` timestamp and added submodule-location notes.

**Task B — package-side migration (complete, committed):**

- Updated `install/install.md` Prerequisites section to instruct consumers to add this
  repo as a submodule at `packages/nla-process-helpers/` (HTTPS URL with explicit
  `git submodule add` command). Rewrote Permissions section to reflect that process
  helpers needs no pre-approval entries — it has no shell commands, external tools,
  or write needs, and reads are in-project now.
- Updated `install/CLAUDE-intent.md` reference line to point at
  `packages/nla-process-helpers/`.
- Updated `install/skills-intent.md` — all 8 path references across the 4 skill
  reference implementations changed to `packages/nla-process-helpers/app/`. Reworked
  the Wrapper Pattern section prose to describe submodule updates rather than sibling
  repo pulls.
- Updated `README.md` "For NLA Creators" section — setup steps now show the
  `git submodule add` command and all four wrapper examples use `packages/…` paths.
  Added a top-level `packages/` entry to the "What's Inside" directory tree (surfaced
  during architecture review).
- Updated `app/overview.md` "Second NLA Extension" section — prose and diagram now
  show consumer NLAs installing this package as a submodule. Updated "For Humans"
  section — install/update steps now use `git submodule add` and `/update`.
- Ran architecture review (`reference/sessions/2026-04-16-architecture-review.md`).
  One fix caught during review (README directory tree); applied in-session so it
  landed in the same Task B commit. Overall: migration is architecturally clean,
  consumer-side and package-side are consistent.

**Pre-tag cleanup (complete, committed):**

- Moved the `packages/nla-penny-post` submodule pointer from main HEAD (`6a5bba1`)
  back to tag `v0.0.1` (`1ef501e`). Maintainer surfaced the question "are we using
  tagged versions?" during pre-push review; framework was fortuitously at
  `HEAD == v0.0.3`, but penny post HEAD was one commit past its `v0.0.1` tag
  (session-log update, no behavior change). Both submodules now pinned at their
  tagged releases.
- Annotated `reference/installed-packages.md` Updated entries to note the tag
  versions for each submodule.

**Release (complete, pushed):**

- Tagged `v0.0.1` — first formal release of this package. Annotated tag describes
  the four facilitation techniques, the `packages/` submodule convention, and
  pinning against nla-framework v0.0.3 and nla-penny-post v0.0.1.
- Pushed all three commits and the `v0.0.1` tag to origin.

**Feedback (sent):**

- Submitted framework issue #23 with two items from this session:
  Item 1 — initial submodule install should default to tagged releases
  (the gap surfaced during pre-tag review). Item 2 — residual permission drift
  observation (Claude Code's auto-approval-and-record loop continues to accrete
  bash-command entries in settings.local.json, even after the packages/ migration
  closed out the Read-path accumulation concerns tracked by #6/#7/#12).
  Framework repo: https://github.com/mightytech/nla-framework/issues/23

## Decisions Made

- **Submodule URL style:** HTTPS for the framework and penny post (read-only
  consumption). This repo's own origin keeps its SSH alias because it's the
  authoritative dev clone. Confirmed with maintainer.
- **Sibling directories stay untouched.** `/home/container-user/workspace/nla-framework/`
  and `/home/container-user/workspace/nla-penny-post/` remain as independent dev
  clones used by other projects. Migration only stops this project from referencing
  them.
- **Split into two tasks with a commit checkpoint.** Consumer-side migration is
  independently verifiable; package-side migration is the contract this package
  exposes to others. Separate commits make each auditable.
- **Pin submodules at tagged releases, not HEAD.** `git submodule add` defaults
  to remote HEAD, which only equals the latest tag by coincidence. Tagged
  releases are the stable install target and what `/update`'s advance-path
  already recommends. Fixed as pre-tag cleanup; sent upstream as framework #23.
- **Tag this release as `v0.0.1`** — first formal release. Follows the
  ecosystem's `v0.0.X` convention (framework at `v0.0.3`, penny post at
  `v0.0.1`). Annotated tag documents the release shape.

## What Didn't Work

No dead ends. The two-task split worked well — Task A's validation caught a few
stale-doc issues (session-checkpoint missing from tables, validate description
needing a broaden, system-status.md skills list out of date) that would have been
harder to spot in a single-commit mega-change. Task B's architecture review
surfaced one stale README tree that slipped through structural validation because
no file reference was broken — the tree was just incomplete.

## Friction Log Entries Processed

*(None — this is framework update application, not friction resolution.)*

## Debrief

Ran a full `/debrief` at session close. Refined conclusions:

**Process observations worth preserving:**

- **The two-task-with-checkpoint pattern is load-bearing for migrations.** Task
  A's validation surfaced four stale-doc issues that would have been much
  harder to spot in a single mega-change (session-checkpoint missing from two
  tables, validate description needing broadening, system-status.md skills list
  stale, system-status.md timestamp old). Task B's architecture review caught
  one more (README "What's Inside" tree missing `packages/`). Neither Task
  would have worked as cleanly without the intermediate commit checkpoint.
  Worth remembering as a pattern for future migrations that have a natural
  seam (consumer-side / package-side, or similar).

- **Stale documentation mirrors are structurally invisible.** Structural
  validation looks for *broken* references — it doesn't catch *stale*
  hand-maintained trees. The README "What's Inside" tree had no broken
  reference; it was just incomplete. Architecture review (which checks path
  resolution / consistency at a higher level) caught it. The `/close` skill's
  "documentation mirrors" concept is the right framing for this class of
  problem — worth keeping in mind that migrations require both validation
  modes to catch both classes.

**Feedback sent upstream:**

- **Install-path tag pinning gap** (framework #23, Item 1). The principle was
  already in `update.md`'s advance-path; the install-path needs to inherit it.
  Concrete, actionable framework fix.
- **Residual permission drift** (framework #23, Item 2). Data point, not a
  request — the packages/ migration resolved the Read-path accumulation but
  bash-command auto-approval continues through a narrower channel.

**Session-local positive observations (not captured externally):**

- Maintainer's process-design instincts showed up three places and each one
  saved real friction: splitting into Tasks A/B, the SSH-vs-HTTPS URL strategy
  (SSH where we push, HTTPS where we only read), catching the untagged
  submodule pins. Treating infrastructure decisions with the same care as
  design decisions.

**Calibration:**

- Heavy, file-by-file plan proposals are a feature, not ceremony. Maintainer
  confirmed dense proposals are what let him respond tersely — "I get
  everything I need up front and don't need to ask questions." Saved as memory
  so future sessions don't drift toward lightweight summaries.

## State at Close

Migration to the `packages/` submodule convention is complete — both consumer-side
(this project's own dependency references) and package-side (the contract this
package exposes to external NLAs) are current with the 2026-04-15 framework update.

Also picked up in the same session:
- New `/session-checkpoint` framework skill — wrapper created, registered in CLAUDE.md
  and related tables
- `/validate` and `/export` description refreshes propagated to wrappers and the
  CLAUDE.md skills table

Three commits pushed to origin:
- `3f5d3cc` — Task A (consumer side)
- `c78d3c2` — Task B (package side)
- `22dee9f` — Pre-tag cleanup (pin penny post submodule at v0.0.1)

Tagged `v0.0.1` (annotated), pushed to origin. First formal release.

Submodules pinned at tagged releases: framework `v0.0.3`, penny post `v0.0.1`.

Framework feedback sent: issue #23 on `mightytech/nla-framework` (install-path
tag pinning + permission-drift observation).

Friction log and feedback log both empty. No pending work.

**Potential follow-ups (not blocking, not scheduled):**
- Consider adding `install/update-notes.md` to this package so future consumers get
  narrative guidance when they `/update` across breaking changes. Framework has this
  pattern; extension packages haven't adopted it.
- Consider a `.gitattributes` with `export-ignore` for `reference/` if/when anyone
  exports a plugin using this project — not relevant until then.
- Watch framework #23 for resolution. If Item 1 lands, re-run `/update` later to
  pick up the install-path tag-pinning check.

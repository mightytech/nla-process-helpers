# Maintenance Session: Migrate to packages/ Submodule Convention

**Date:** 2026-04-16
**Status:** In Progress

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

**Task B — package-side migration (pending).**

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

## What Didn't Work

*(None so far.)*

## Friction Log Entries Processed

*(None — this is framework update application, not friction resolution.)*

## Debrief

*(Pending session close.)*

## State at Close

*(Pending.)*

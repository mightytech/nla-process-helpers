# Maintenance Session: Framework Update and Penny Post Install

**Date:** 2026-03-08
**Status:** Complete

## Intent

Bring the process helpers current with three framework updates (accumulated since
2026-02-23), install the penny post extension for sending feedback upstream, and
send two feedback letters identified during the session.

## Changes Made

- **Framework update (3 updates in one pass):** Added `/close` (session wrap-up)
  and `/guide` (context-aware help) skill wrappers. Replaced accumulated one-off
  permission entries in `settings.local.json` with clean intentional baseline
  (framework reads + common bash patterns). Added Permissions section to package's
  own `install/install.md`.
- **Penny post install:** Created `/check-feedback` and `/write-letter` skill
  wrappers. Added penny post awareness to CLAUDE.md (skills table + key files).
  Updated all downstream files (overview, system-status, README).
- **Validation fix (pre-existing):** Added `/install` and `/update` to overview.md
  self-maintenance table — they were missing since project creation.
- **Permission pre-approval:** Added penny post read permission to settings.local.json.

## Decisions Made

- **Clean settings.local.json rather than append** — The existing file had ~45 one-off
  entries from Claude Code's auto-approval. Replaced entirely with 4 intentional
  pattern-based entries. Cleaner, and the patterns cover most recurring commands.
- **Structural validation only, not architectural** — All changes were mechanical
  (new wrappers, updated tables, new sections). No technique behavior or design
  patterns changed.

## Debrief

- **Permission accumulation pattern** is a real tension. The framework's intentional
  permission model (`Bash(git:*)`) conflicts with Claude Code's behavior of recording
  exact approved commands. The settings file will re-accumulate over time. Partially
  mitigatable: `git -C` instead of `cd && git` makes git commands match the pattern.
  Sent as feedback to framework (issue #12).
- **Pre-existing validation gaps are invisible without running validation.** The
  `/install` and `/update` gap in overview.md survived two update cycles. Running
  structural validation after updates catches these — good argument for always doing it.
- **Three-update batch worked smoothly.** The framework's update notes were well-written
  enough to process three updates in one pass without confusion.

## State at Close

All framework updates applied and validated. Penny post installed and functional.
Two feedback letters submitted (framework #12: git -C pattern, penny post #9:
manifest permissions). Friction log is empty. Feedback log is empty. Everything
committed and pushed.

No pending work. Next session starts clean.

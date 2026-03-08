# Installed Packages

Packages installed in this NLA, maintained by `/install` and `/update`.

Each entry records what package was installed, when, what state the package was in, and what changes were made. This log is how `/update` knows what's current and what needs changing.

---

## NLA Framework

**Installed:** 2026-02-22 (initial package creation)
**Source:** `../nla-framework/`

The process helpers package was created as a framework-based NLA. Framework skills are
thin wrappers in `.claude/skills/` delegating to `../nla-framework/core/skills/`.

### Updated 2026-02-23

**Package state:** c4dc338

| Intent File | What Changed | Changes Made |
|-------------|-------------|--------------|
| skills-intent.md | New `/check-updates` skill added; `/update` description broadened | Created `.claude/skills/check-updates/SKILL.md` wrapper; updated `/update` wrapper description |

**Downstream updates:** Added `/check-updates` to CLAUDE.md skills table, `app/overview.md`, `reference/system-status.md`, and `README.md` directory tree. Updated `/update` description in CLAUDE.md.

**Notes:** Core file changes (startup friction log surfacing, friction-log session awareness) propagate automatically via thin wrappers — no edits needed.

### Updated 2026-03-08

**Package state:** db32216

| Intent File | What Changed | Changes Made |
|-------------|-------------|--------------|
| skills-intent.md | New `/close` and `/guide` skills added | Created `.claude/skills/close/SKILL.md` and `.claude/skills/guide/SKILL.md` wrappers |
| install.md | New Permissions section declaring filesystem access needs | No action needed — this NLA is the framework consumer, not an installer of itself |
| structure-intent.md | `.claude/settings.local.json` documented; `overview.md` description broadened | Replaced one-off permission accumulation in `settings.local.json` with clean baseline (framework reads + common bash patterns) |

**Downstream updates:** Added `/close` and `/guide` to CLAUDE.md skills table, `app/overview.md` self-maintenance skills table, `reference/system-status.md` framework skills list, and `README.md` directory tree. Added Permissions section to package's own `install/install.md`.

**Notes:** Three framework updates applied in one pass: `/close` skill (2026-03-04), permission management model (2026-03-04), `/guide` skill + Working Rhythms (2026-03-05). Core changes (startup `/guide` awareness, maintain `/guide` mention, Working Rhythms in foundations, close delegation in maintain) propagate automatically via thin wrappers.

---

## Penny Post

**Source:** `../nla-penny-post/`
**Installed:** 2026-03-08
**Package state:** 6a43a8d

### What was done

| Intent File | Integration Point | Changes Made |
|-------------|------------------|--------------|
| skills-intent.md | .claude/skills/ | Created `check-feedback/SKILL.md` and `write-letter/SKILL.md` wrappers |
| CLAUDE-intent.md | CLAUDE.md | Added Penny Post Skills section to skills table; added penny post to Key Files |

### Notes

Package manifest predates the Permissions convention — no permission entries declared. Penny post reads are not pre-approved in settings.local.json; Claude Code will prompt on first use. Downstream files updated: app/overview.md (skills table + document hierarchy), reference/system-status.md, README.md directory tree.

---

<!-- /install and /update maintain this file. Each package gets a section with install
     history and update records. Don't remove old entries — they tell the full story. -->

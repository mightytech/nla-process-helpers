# Installed Packages

Packages installed in this NLA, maintained by `/install` and `/update`.

Each entry records what package was installed, when, what state the package was in, and what changes were made. This log is how `/update` knows what's current and what needs changing.

---

## NLA Framework

**Installed:** 2026-02-22 (initial package creation)
**Source:** `packages/nla-framework/` (git submodule — was `../nla-framework/` before 2026-04-16)

The process helpers package was created as a framework-based NLA. Framework skills are
thin wrappers in `.claude/skills/` delegating to `packages/nla-framework/core/skills/`.

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

### Updated 2026-04-16

**Package state:** a754ae3

| Intent File | What Changed | Changes Made |
|-------------|-------------|--------------|
| install.md, CLAUDE-intent.md, structure-intent.md, package-intent.md, skills-intent.md | `../nla-framework/` sibling convention replaced with `packages/nla-framework/` git submodule; `Read(../nla-framework/**)` permission retired (reads now in-project) | Added framework as git submodule at `packages/nla-framework/` (HTTPS URL). Updated all 13 framework thin wrappers to point at `packages/nla-framework/core/skills/`. Removed absolute `Read(.../nla-framework/**)` entry from `.claude/settings.local.json`. |
| skills-intent.md | New `/session-checkpoint` skill; `/validate` description adds coherence review; `/export` description reflects view-source plugin model | Created `.claude/skills/session-checkpoint/SKILL.md` wrapper; updated `/validate` and `/export` descriptions. |

**Downstream updates:** CLAUDE.md (`/session-checkpoint` added to skills table; Environment line and Key Files table updated to `packages/…`); README.md (framework links, prerequisites, and footer updated); `app/overview.md` top-of-doc framework link; `app/config-spec.md` defaults updated to `packages/…`.

**Notes:** Consumer-side portion of the `packages/` migration (2026-04-15 framework update). Package-side intent files (this package's own `install/`) to be updated in a separate pass.

---

## Penny Post

**Source:** `packages/nla-penny-post/` (git submodule — was `../nla-penny-post/` before 2026-04-16)
**Installed:** 2026-03-08
**Package state:** 6a43a8d

### What was done

| Intent File | Integration Point | Changes Made |
|-------------|------------------|--------------|
| skills-intent.md | .claude/skills/ | Created `check-feedback/SKILL.md` and `write-letter/SKILL.md` wrappers |
| CLAUDE-intent.md | CLAUDE.md | Added Penny Post Skills section to skills table; added penny post to Key Files |

### Notes

Package manifest predates the Permissions convention — no permission entries declared. Penny post reads are not pre-approved in settings.local.json; Claude Code will prompt on first use. Downstream files updated: app/overview.md (skills table + document hierarchy), reference/system-status.md, README.md directory tree.

### Updated 2026-04-16

**Package state:** 6a5bba1

| Intent File | What Changed | Changes Made |
|-------------|-------------|--------------|
| install.md, CLAUDE-intent.md, skills-intent.md | `../nla-penny-post/` sibling convention replaced with `packages/nla-penny-post/` git submodule | Added penny post as git submodule at `packages/nla-penny-post/` (HTTPS URL). Updated `check-feedback` and `write-letter` thin wrappers to point at `packages/nla-penny-post/app/`. Removed absolute `Read(.../nla-penny-post/**)` entry from `.claude/settings.local.json`. |

**Notes:** Phase 2 of the framework's `packages/` migration — applied alongside the framework update on the same date.

---

<!-- /install and /update maintain this file. Each package gets a section with install
     history and update records. Don't remove old entries — they tell the full story. -->

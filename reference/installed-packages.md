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

---

<!-- /install and /update maintain this file. Each package gets a section with install
     history and update records. Don't remove old entries — they tell the full story. -->

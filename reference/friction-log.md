# Friction Log

Running log of learnings from package development, NLA feedback, and maintenance observations. Each entry captures something worth remembering about the process helpers.

---

## How to Use This Log

**When to add entries:**
- When an NLA project encounters friction with a facilitation technique
- When you notice a pattern across multiple uses
- When something works surprisingly well
- When something fails unexpectedly during package maintenance

**Entry types:**
- `technique` — How a facilitation technique performed
- `process` — How package maintenance workflows function
- `documentation` — Clarity or gaps in package docs

**Severity includes positive:** Capture what works, not just what breaks.

---

## Entry Format

```markdown
### YYYY-MM-DD — [Brief descriptive title]

**Type:** technique | process | documentation
**Severity:** positive | minor | major
**Status:** pending | resolved | deferred | wont-fix

**Observation:**
[What happened or was noticed]

**Affected files:**
[Which files would need to change]

**Proposed fix:**
[Specific enough for /maintain to act on]
```

Not every entry needs all fields. The essentials are: Observation, Type, Severity, Status.

---

## Entries

*Entries are added chronologically, newest first.*

*No pending entries.*

---

## Patterns to Watch

*Recurring themes that may need deeper attention:*

1. **Technique composability** — How well do facilitation techniques layer on different active contexts? Watch for interference or confusion.

2. **Suggestion calibration** — When the AI suggests unpacking, is the threshold right? Too aggressive feels imposing; too conservative means missed opportunities.

---

*This log is maintained by the `/friction-log` skill (which creates entries) and the `/maintain` skill (which resolves and archives them). Resolved entries are moved to `friction-log-archive.md`.*

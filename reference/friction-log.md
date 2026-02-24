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

### 2026-02-24 — Brainstorm-cluster converged before clustering

**Type:** technique
**Severity:** positive
**Status:** resolved

**Observation:**
Used `/brainstorm-cluster` to generate candidate techniques for the package. The human picked a winner (`/steelman`) during the Generate phase — before clustering or evaluation. The brainstorm was useful faster than the five-phase process assumes.

This is actually a mark of success: the technique's value was in structuring the generation, not in completing all phases. The phase-jump language in the technique doc ("Skip clustering, I know which ideas I like" is valid) handled this gracefully.

**Resolved:** No fix needed — the technique already supports early convergence through its phase-jump design. Worth noting as validation that "no forced completion" works in practice.

---

## Patterns to Watch

*Recurring themes that may need deeper attention:*

1. **Technique composability** — How well do facilitation techniques layer on different active contexts? Watch for interference or confusion.

2. **Suggestion calibration** — When the AI suggests unpacking, is the threshold right? Too aggressive feels imposing; too conservative means missed opportunities.

---

*This log is maintained by the `/friction-log` skill (which creates entries) and the `/maintain` skill (which resolves and archives them). Resolved entries are moved to `friction-log-archive.md`.*

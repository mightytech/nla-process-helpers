# Configuration Spec

This document defines what users of the process helpers can configure. The `/preferences` skill reads this to guide the configuration conversation and enforce constraints.

---

## What's Configurable

### Framework Path

If the NLA Framework is not at the standard sibling location (`../nla-framework/`), users can specify the actual path.

**Default:** `../nla-framework/`

### Process Helpers Location

If the process helpers package is not at the standard sibling location:

- **Local path** — Where this repo is cloned

**Default:** `../nla-process-helpers/` (sibling directory).

### Tracing

Runtime tracing logs the LLM's decisions during facilitation — which threads it identified, how it proposed structuring them, what transitions it signaled.

**Trace level:**

- **Off** — No tracing. Default.
- **Standard** — Log major decisions: thread identification, proposed sets, transitions, human adjustments.
- **Detailed** — Log everything including alternatives considered and threads that were identified but not proposed.
- **Custom** — User writes natural language describing exactly what to trace.

**Trace output:** `reference/sessions/trace-YYYY-MM-DD.md`.

**Default:** Tracing off.

---

## Constraints

- The human always controls conversation structure. Techniques propose; humans decide. This is non-configurable — it's the Cardinal Rule applied to facilitation.

---

## Guidance for the Config Conversation

This is a minimal package. Most users won't need to configure anything — the defaults work. If they're running the package directly (maintaining the techniques), framework path and tracing are the main options.

---

*This spec is maintained by the app developer via `/maintain`. Users interact with config through `/preferences`.*

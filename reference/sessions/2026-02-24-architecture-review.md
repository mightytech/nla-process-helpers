# Architecture Review: Process Helpers

**Date:** 2026-02-24
**Trigger:** Addition of /brainstorm-cluster technique

## Document Chain

The LLM reads documents in this sequence from startup through task execution:

```
CLAUDE.md
  -> "Run /startup" at session start
  -> .claude/skills/startup/SKILL.md
    -> ../nla-framework/core/skills/startup.md
      -> 1. ../nla-framework/core/nla-foundations.md
      -> 2. app/overview.md
      -> 3. app/shared/values.md
      -> 4. app/shared/common-patterns.md     [DOES NOT EXIST in process helpers]
      -> 5. app/shared/output-spec.md          [DOES NOT EXIST, handled: "if it exists"]
      -> 6. config.md                          [DOES NOT EXIST, handled: "if it exists"]
      -> 7. app/startup.md                     [DOES NOT EXIST, handled: "if it exists"]
  -> User invokes a task skill
  -> .claude/skills/brainstorm-cluster/SKILL.md  (or unpack/SKILL.md)
    -> app/brainstorm-cluster.md               (or app/unpack.md)
```

Values are loaded at startup and are in context for all task execution. The technique docs don't explicitly reference values.md but don't need to -- values are already loaded and shape judgment implicitly.

## Findings

### Fix

- **reference/design-rationale.md**: "Selective Installation" section says "Not implemented yet because with one technique there's nothing to select." There are now two techniques. The section's premise is stale -- selective installation is no longer a future direction but a currently-relevant concern. The section should be updated to reflect that the package now has multiple techniques and note whether selective installation should be implemented or deferred for other reasons. -- Consistency

- **README.md** (line 123): Same stale language in "Future Directions" -- "This isn't implemented yet -- with one technique, there's nothing to select." Should match the updated reality of two techniques. -- Consistency

- **app/config-spec.md** (lines 25-31): Tracing descriptions use exclusively unpack-specific terminology: "which threads it identified," "proposed sets," "thread identification," "threads that were identified but not proposed." With brainstorm-cluster now in the package, tracing descriptions should cover both techniques or use generic facilitation language. A brainstorm-cluster trace would log participation mode choices, idea generation counts, cluster formation decisions, evaluation proposals -- none of which fit the current descriptions. As written, a user enabling tracing during a brainstorm-cluster session would get undefined behavior. -- Language breadth

### Improve

- **CLAUDE.md** (line 15): "Structured underneath, flexible on top" gives examples as "thread identification, progress tracking, transition signaling." These are all unpack concepts. Brainstorm-cluster's structure (phase sequencing, participation mode management, idea generation/clustering) is not represented. Consider broadening to "phase management, participation tracking, transition signaling" or using "e.g." to make the illustrative nature explicit. -- Language breadth
  - **Skipped.** On review, the examples (thread identification, progress tracking, transition signaling) are actually generic enough — brainstorm-cluster does all three. Not as unpack-specific as it initially appears.

- **CLAUDE.md** (line 21): "Non-determinism is a feature" uses "The same conversation may be unpacked differently" -- using technique-specific vocabulary ("unpacked") in a package-level principle. With two techniques, this should be more generic: "The same conversation may be facilitated differently" or "structured differently." -- Language breadth
  - **Fixed.** Changed "unpacked" to "facilitated."

- **app/overview.md** (line 24): "How Techniques Work" gives only `/unpack` as the layering example: "When you invoke `/unpack` during a `/think` session..." Consider adding a brainstorm-cluster example or generalizing to "When you invoke a process helper during a `/think` session..." The next sentence (line 26) is already well-balanced with examples from both techniques. -- Language breadth
  - **Skipped.** Using a concrete example is clearer than generalizing, and adding a second example would clutter the section. The existing text illustrates the layering concept well enough with one example.

- **README.md** (lines 41-45): Manual setup instructions only show creating the `/unpack` wrapper and adding `/unpack` to the CLAUDE.md skills table. The usage section immediately below (lines 49-52) correctly shows both techniques. Either show both techniques in the setup steps, or say "repeat for each technique you want to install." -- Consistency
  - **Fixed.** Added brainstorm-cluster wrapper to manual setup example.

- **reference/design-rationale.md**: No mention of brainstorm-cluster or participation modes anywhere. The document explains why process helpers is a package, the phase/process distinction, selective installation, and facilitation techniques as a category -- but doesn't document any design decisions about the second technique. When brainstorm-cluster was added, its design decisions (the participation mode system, the five-phase method, the "AI leads" mode's relationship to "the human decides" principle) should have been recorded here. -- Orphaned content / missing rationale
  - **Fixed.** Added "Brainstorm-Cluster and Participation Modes" section to design-rationale.md.

### Note

- **Framework issue -- startup.md item 4**: `app/shared/common-patterns.md` is listed without an "if it exists" qualifier, unlike `output-spec.md` (item 5) and `config.md` (item 6). When the process helpers run /startup, the LLM will attempt to read a file that doesn't exist. In practice the LLM handles file-not-found gracefully, but the startup skill should be consistent -- either all optional files get "if it exists" or the framework should document that common-patterns.md is expected for all NLAs. This is a framework-level issue, not a process-helpers issue. -- Conditional completeness (framework)

- **brainstorm-cluster.md simultaneous mode** (lines 87-89): The instruction "Generate your list but don't show it yet" requires the LLM to produce content and withhold it across a conversational turn. The LLM can do this, but the mechanics are ambiguous -- does it generate internally and reproduce later? Write it in a collapsed section? Generate it fresh when revealing? Different LLMs or different sessions may implement this differently. The current prose is clear enough for reasonable execution but could benefit from a clarifying sentence about the expected mechanism (e.g., "Generate your list in your reasoning, then present only the prompt to the human. When they finish, write out both lists."). -- Prerequisite sufficiency

- **Participation modes and "the human decides"**: The "AI leads" mode is well-aligned with the cardinal rule despite the potentially conflicting name. The prose is careful: "The AI does the work and presents results. The human reacts, reshapes, and decides." The human chooses the mode, the human can switch at any transition, and evaluation is explicitly "a proposal, not a verdict." No contradiction. -- Values consistency (clean)

- **Technique sibling coherence**: brainstorm-cluster.md and unpack.md share clear structural DNA -- opening identity statement, "When to Suggest This," Method, "What This Isn't," Scope, closing italicized reflection. Brainstorm-cluster adds two sections (Participation Modes, Phase Transitions) that are organic to its more complex process. The closing reflections use the same rhetorical pattern. These feel like siblings from the same family. -- Consistency (clean)

- **SKILL.md wrapper coherence**: Both wrappers follow the same structure -- frontmatter, heading, opening paragraph, Execute, Input, Key Principles. Brainstorm-cluster has one additional principle ("Diverge then converge") appropriate to its technique. The Input sections are correctly technique-specific. No inconsistencies. -- Consistency (clean)

- **Install intent coherence**: CLAUDE-intent.md and skills-intent.md both describe brainstorm-cluster consistently with how they describe unpack. The descriptions match, the reference implementations follow the same pattern, and the intent language is parallel. -- Consistency (clean)

- **Cross-reference integrity**: All paths resolve correctly. Local SKILL.md files use `app/` paths (project-root-relative). Install intent files use `../nla-process-helpers/app/` paths (for external NLAs). The overview's document hierarchy matches the actual file structure. -- Path resolution (clean)

## Summary

**Counts:** 3 Fix, 5 Improve, 7 Note (of which 4 are clean/positive observations)

**Overall assessment:** The brainstorm-cluster addition is architecturally sound. The technique doc, SKILL.md wrapper, and install intent files are well-crafted and follow established patterns. The structural coherence between the two technique docs is strong -- they clearly belong to the same family.

The issues that need attention are primarily about the *existing* docs not being updated to reflect that the package now has two techniques instead of one. The stale "one technique" language in design-rationale.md and README.md is the most urgent fix because it actively contradicts reality and could mislead a maintaining AI. The config-spec.md tracing descriptions are a real functional gap -- a user enabling tracing for brainstorm-cluster would get inadequate coverage.

The CLAUDE.md language breadth issues (unpack-specific vocabulary in package-level principles) are worth improving but aren't causing incorrect behavior -- they just subtly bias toward unpack as the "default" technique.

The design-rationale.md gap is the most architecturally significant finding. The participation mode system is a novel concept in this package -- it introduces a three-way interaction pattern (AI leads, human leads, simultaneous) that didn't exist with unpack. The design decisions behind this (why these three modes, how "AI leads" squares with "the human decides," why simultaneous mode works as described) should be documented for future maintainers.

---

## State at Close

All 3 Fix items and all actionable Improve items have been resolved:

- **design-rationale.md selective installation** — Updated to reflect two techniques; reframed as practically relevant.
- **README.md stale language** — Removed "one technique" phrasing; updated manual setup to show both techniques.
- **config-spec.md tracing descriptions** — Broadened to generic facilitation language covering both techniques.
- **design-rationale.md brainstorm-cluster section** — Added "Brainstorm-Cluster and Participation Modes" documenting the design decisions.
- **CLAUDE.md "unpacked" wording** — Changed to "facilitated."

2 Improve items were deliberately skipped (CLAUDE.md structure examples, overview.md layering example) — reviewed and judged adequate as-is.

Nothing pending. The package documentation is consistent with the two-technique reality.

---

*Review performed by reading all 14 specified files plus the framework startup skill. No structural validation was performed (already passed clean). Focus was prose-architecture coherence.*

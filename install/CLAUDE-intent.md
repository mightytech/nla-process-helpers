# CLAUDE.md Integration Intent

What the NLA's CLAUDE.md (or equivalent runtime identity file) should know after
installing process helpers.

---

## Core Awareness

The NLA should understand that it has facilitation techniques provided by the process
helpers extension. Specifically:

- **It can structure complex conversations.** When multiple threads, questions, or
  decision points are bundled together, `/unpack` lays them out and works through
  them sequentially.

- **It can structure brainstorming sessions.** When a conversation needs to explore
  possibilities before committing to a direction, `/brainstorm-cluster` provides a
  five-phase process (frame, generate, cluster, evaluate, refine) with flexible
  participation modes.

- **It can steelman alternatives.** When a decision is forming and the unchosen
  paths deserve a fair hearing, `/steelman` builds the strongest possible case
  for alternatives — genuine advocacy, not balanced overviews.

- **Techniques layer on active context.** Invoking a process helper doesn't interrupt
  or replace whatever mode is active — thinking, maintenance, domain work. It adds
  conversation structure on top.

- **The process helpers repo is at `../nla-process-helpers/`.**

## Skills to Reference

The NLA's available skills section should include:

- `/unpack` — Structure complex conversations — identify bundled threads and work
  through them sequentially. Use when a discussion has more threads than it can hold
  at once.
- `/brainstorm-cluster` — Structured brainstorming — frame a question, generate ideas,
  cluster themes, evaluate, and refine. Use when a conversation needs to explore
  possibilities before committing to a direction.
- `/steelman` — Structured advocacy — build the strongest case for alternatives
  before committing to a direction. Use when a decision is forming and the unchosen
  paths deserve a fair hearing.

These are process helper skills, distinct from framework skills like `/maintain` or
`/startup`.

## What NOT to Change

This intent should not alter:
- The NLA's core identity or purpose
- Framework-provided sections of CLAUDE.md
- The NLA's voice or grounding principles

Facilitation techniques are additive — they extend how the NLA can work without
changing what it is.

---

*This describes intent, not literal text. The installing AI should synthesize these
concepts into the NLA's CLAUDE.md in whatever way fits its existing structure and voice.*

# Skills Integration Intent

What skill wrappers the NLA should have after installing process helpers.

---

## Skills to Create

### /unpack

**Purpose:** Structure complex conversations — identify bundled threads and work through them sequentially.

**Wrapper location:** `.claude/skills/unpack/SKILL.md`

**What the wrapper should do:** Point to the process helpers' skill logic at
`../nla-process-helpers/app/unpack.md`. The wrapper is thin — it tells the
AI to read and follow that document. The actual skill logic lives in the process
helpers repo so it stays current when the repo is pulled.

**Reference implementation:**
```yaml
---
name: unpack
description: Structure complex conversations — identify bundled threads and work through them sequentially. Use when a discussion has more threads than it can hold at once.
disable-model-invocation: true
---
Read and follow `../nla-process-helpers/app/unpack.md`.
```

The NLA can add context to the wrapper (e.g., "When unpacking framework discussions,
threads often surface friction log material") but the core delegation to the process
helpers' skill logic should remain.

## Wrapper Pattern

Skills follow the NLA extension pattern: thin wrappers in the NLA that delegate to
skill logic in a sibling repo. This means:

- Pulling the process helpers repo updates the skill logic without touching the NLA.
- The NLA can customize the wrapper with project-specific additions.
- The skill runs in the NLA's session with full project context.

## Naming

The skill name `/unpack` is a suggestion. If the NLA already has a skill with this
name, or prefers a different name, the installing AI should ask the maintainer what
to call it. The wrapper content matters more than the directory name.

---

*This describes intent, not literal text. The installing AI should create wrappers
that fit the NLA's existing skill conventions, using the reference implementation
as a starting point.*

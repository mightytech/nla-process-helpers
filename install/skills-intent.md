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

### /brainstorm-cluster

**Purpose:** Structured brainstorming — frame a question, generate ideas, cluster themes, evaluate, and refine.

**Wrapper location:** `.claude/skills/brainstorm-cluster/SKILL.md`

**What the wrapper should do:** Point to the process helpers' skill logic at
`../nla-process-helpers/app/brainstorm-cluster.md`. Same thin wrapper pattern as
`/unpack`.

**Reference implementation:**
```yaml
---
name: brainstorm-cluster
description: Structured brainstorming — frame a question, generate ideas, cluster themes, evaluate, and refine. Use when a conversation needs to explore possibilities before committing to a direction.
disable-model-invocation: true
---
Read and follow `../nla-process-helpers/app/brainstorm-cluster.md`.
```

### /steelman

**Purpose:** Structured advocacy — build the strongest case for alternatives before committing to a direction.

**Wrapper location:** `.claude/skills/steelman/SKILL.md`

**What the wrapper should do:** Point to the process helpers' skill logic at
`../nla-process-helpers/app/steelman.md`. Same thin wrapper pattern as
`/unpack`.

**Reference implementation:**
```yaml
---
name: steelman
description: Structured advocacy — build the strongest case for alternatives before committing to a direction. Use when a decision is forming and the unchosen paths deserve a fair hearing.
disable-model-invocation: true
---
Read and follow `../nla-process-helpers/app/steelman.md`.
```

## Wrapper Pattern

Skills follow the NLA extension pattern: thin wrappers in the NLA that delegate to
skill logic in a sibling repo. This means:

- Pulling the process helpers repo updates the skill logic without touching the NLA.
- The NLA can customize the wrapper with project-specific additions.
- The skill runs in the NLA's session with full project context.

## Naming

Skill names (`/unpack`, `/brainstorm-cluster`) are suggestions. If the NLA already has
a skill with a given name, or prefers a different name, the installing AI should ask
the maintainer what to call it. The wrapper content matters more than the directory name.

---

*This describes intent, not literal text. The installing AI should create wrappers
that fit the NLA's existing skill conventions, using the reference implementation
as a starting point.*

# Process Helpers

A facilitation technique package for NLA projects, built on the [NLA Framework](../nla-framework/).

---

## What It Is

The process helpers package provides facilitation techniques — skills that shape how conversations proceed, layering on top of whatever work is already active.

It's the second **NLA extension** (after [penny post](../nla-penny-post/)). Most users interact with it through skills installed in their own NLA, not by opening this project directly.

### Why a Package, Not Core

Phase skills like `/think` and `/debrief` define *when* in the work lifecycle — they're universal infrastructure that belongs in the framework core. Process helpers define *how* within conversations — and how is preference. Different people prefer different conversation management approaches: sequential thread-by-thread, document-for-inline-annotation, everything-at-once. This package provides one set of techniques; others may provide alternatives.

### Current Techniques

| Technique | Purpose |
|-----------|---------|
| `/unpack` | Structure complex conversations — identify bundled threads and work through them sequentially |
| `/brainstorm-cluster` | Structured brainstorming — frame, generate, cluster, evaluate, refine |

---

## For NLA Creators: Installing Process Helpers

### Prerequisites

- **NLA Framework** at `../nla-framework/`
- **Claude Code** installed

### Setup

1. Clone this repo as a sibling to your NLA: `../nla-process-helpers/`
2. From your NLA, run `/install` and point it at `../nla-process-helpers/`

Or add skill wrappers manually (see `install/skills-intent.md` for details):

```
# .claude/skills/unpack/SKILL.md
Read and follow `../nla-process-helpers/app/unpack.md`.

# .claude/skills/brainstorm-cluster/SKILL.md
Read and follow `../nla-process-helpers/app/brainstorm-cluster.md`.
```

3. Add the skills to your NLA's CLAUDE.md skills table

### Usage from Your NLA

```
/unpack              # Structure a complex conversation into threads
/brainstorm-cluster  # Structured brainstorming with flexible participation
```

The skill runs in your NLA's session with full project context. It layers on whatever's already active — thinking, maintenance, domain work.

---

## What's Inside

```
├── CLAUDE.md                        # Runtime identity and configuration
├── app/                             # The application (LLM reads and executes)
│   ├── overview.md                  # What this package does, how pieces connect
│   ├── shared/
│   │   └── values.md               # Facilitation values
│   ├── config-spec.md              # What users can configure
│   ├── unpack.md                   # Unpack skill logic
│   └── brainstorm-cluster.md       # Brainstorm-cluster skill logic
├── install/                         # Package manifest (for NLA integration)
│   ├── install.md                   # Orchestrator — what this package needs
│   ├── CLAUDE-intent.md             # Intent for NLA's CLAUDE.md
│   └── skills-intent.md            # Intent for skill wrappers
├── reference/                       # Maintenance records
│   ├── design-rationale.md          # Why the system is built this way
│   ├── friction-log.md              # Learning journal (active entries)
│   ├── friction-log-archive.md      # Resolved entries
│   ├── feedback-log.md              # Accepted external feedback (pending)
│   ├── feedback-log-archive.md      # Resolved feedback
│   ├── installed-packages.md        # Record of installed NLA packages
│   ├── system-status.md             # Current state snapshot
│   └── sessions/                    # Maintenance session archives
└── .claude/skills/                  # Skill entry points
    ├── unpack/                      # Process helper skill
    ├── brainstorm-cluster/          # Process helper skill
    ├── startup/                     # Framework wrapper
    ├── maintain/                    # Framework wrapper
    ├── friction-log/                # Framework wrapper
    ├── validate/                    # Framework wrapper
    ├── preferences/                 # Framework wrapper
    ├── install/                     # Framework wrapper
    ├── update/                      # Framework wrapper
    ├── check-updates/               # Framework wrapper
    ├── export/                      # Framework wrapper
    ├── think/                       # Framework wrapper
    └── debrief/                     # Framework wrapper
```

---

## Running Process Helpers Directly

Most interaction happens from other NLAs. But when maintaining the package itself:

1. Start Claude Code in this directory
2. Run `/startup` to load foundational context
3. Run `/maintain` to edit the techniques
4. Use `/friction-log` to capture observations

---

## The Improvement Loop

```
Observe something → /friction-log captures it → /maintain implements changes
```

The process helpers improve by improving their documentation. The friction log captures observations; maintenance sessions turn them into doc changes; the docs improve; the techniques improve.

---

## Future Directions

**Selective installation.** With multiple techniques in the package, users should be able to choose which ones to install rather than getting all of them. The `/install` skill would present the available techniques and let the user pick.

**More techniques.** Card sorting, naming exercises, and other process interventions that work regardless of subject matter. These share the same shape as `/unpack` and `/brainstorm-cluster`: they layer on active context, they structure how conversations happen, and different users will want different ones.

---

## Contributing

Submit feedback about the **NLA framework** by opening an issue on the framework repo.

Submit feedback about **process helpers** by opening an issue on this repo.

---

*For more about the NLA Framework, see the [framework README](../nla-framework/README.md).*

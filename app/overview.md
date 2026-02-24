# System Overview

This document describes what this NLA does and how its pieces fit together. For what NLAs are and the principles behind them, see [nla-foundations.md](../nla-framework/core/nla-foundations.md).

---

## What the Process Helpers Package Is

A facilitation technique package — conversation-shaping skills that layer on top of whatever work is already active. The techniques structure *how* conversations proceed without changing *what* they're about.

### The Phase/Process Distinction

The NLA framework provides phase skills that define *when* in the work lifecycle:

- `/think` — explore what to build and why (before planning)
- `/debrief` — reflect on process and experience (after work)

These are universal — every NLA does work, every NLA has a lifecycle.

Process helpers define *how* within conversations — and how is preference. Sequential thread-by-thread (/unpack) is one approach. Document-for-inline-annotation is another. Getting everything at once and steering is another. This package provides techniques for people who find them useful; it doesn't impose a working style.

### How Techniques Work

Techniques layer on active context without replacing it. When you invoke `/unpack` during a `/think` session, both are active — the thinking posture plus the unpacking structure. Multiple skills compose naturally because they shape different dimensions of the conversation.

A technique's job is done when its purpose is served — when the threads are resolved, when the brainstorm converges, when the exercise completes. No formal exit needed; the conversation returns to its prior rhythm.

### The Second NLA Extension

The penny post was the first NLA extension — a capability that other NLAs install and use from within their own sessions. Process helpers is the second, following the same pattern: thin wrappers in the NLA point to skill logic in `../nla-process-helpers/`.

```
your-nla/
  .claude/skills/
    unpack/SKILL.md        → ../nla-process-helpers/app/unpack.md
../nla-framework/          # Foundation
../nla-process-helpers/    # Extension (facilitation techniques)
```

---

## Techniques Provided

| Technique | Purpose | When to Use |
|-----------|---------|-------------|
| `/unpack` | Structure complex conversations — identify bundled threads and work through them sequentially | When a discussion has more threads than it can hold at once |

### Skills for Self-Maintenance

When running as a standalone NLA (maintaining itself), the process helpers also use framework skills:

| Skill | Purpose |
|-------|---------|
| `/startup` | Load foundational context |
| `/maintain` | Edit the package's own docs and techniques |
| `/friction-log` | Capture observations about how the techniques work |
| `/validate` | Check system consistency |
| `/check-updates` | Check for available updates without making changes |
| `/preferences` | Configure user preferences |
| `/export` | Export as a plugin for Claude Code or Cowork |
| `/think` | Collaborative design exploration |
| `/debrief` | Post-work reflection |

---

## Installation

The process helpers ship an `install/` directory that describes what an NLA needs to integrate the package. Each file describes the **intent** of changes at a specific integration point — what the NLA's CLAUDE.md should know, what skill wrappers to create.

The `/install` skill (framework-level) reads these intent files and synthesizes them into the NLA's existing structure. Manual setup works fine too — the intent files serve as documentation of what's needed.

See `install/install.md` for the full manifest.

## For Humans

**To install process helpers for your NLA:**
1. Clone this repo as a sibling to your NLA: `../nla-process-helpers/`
2. Add skill wrappers to your NLA's `.claude/skills/` (see `install/skills-intent.md` for details)
3. Add the skills to your CLAUDE.md skills table

**To keep up with upstream:**
- `git pull` the process helpers repo for technique updates

---

## Document Hierarchy

```
app/
├── overview.md                      ← This file
│
├── shared/
│   └── values.md                   ← Facilitation values
│
├── config-spec.md                   ← What users can configure
│
└── unpack.md                        ← Unpack skill logic

config.md                            ← User preferences (gitignored)

install/
├── install.md                       ← Package manifest (orchestrator)
├── CLAUDE-intent.md                 ← Intent for NLA's CLAUDE.md
└── skills-intent.md                 ← Intent for skill wrappers

../nla-framework/core/
├── nla-foundations.md               ← What NLAs are (framework)
└── skills/                          ← Framework skill logic

reference/
├── design-rationale.md              ← Why the system is built this way
├── friction-log.md                  ← Learning journal (active entries)
├── friction-log-archive.md          ← Resolved entries (searchable history)
├── feedback-log.md                  ← Accepted external feedback (pending)
├── feedback-log-archive.md          ← Resolved feedback (searchable history)
├── installed-packages.md            ← Record of installed NLA packages
├── system-status.md                 ← Current state snapshot
└── sessions/                        ← Maintenance session archives
```

---

*This is a living document. As the process helpers evolve, update this overview to reflect the current state.*

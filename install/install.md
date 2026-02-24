# Process Helpers — Install Manifest

This directory describes what an NLA needs to integrate the process helpers package.
An `/install` or `/update` skill reads these files and applies them to the target NLA.

---

## What This Package Is

The process helpers package provides facilitation techniques for NLA projects —
conversation-shaping skills that layer on top of whatever work is already active.
Currently provides `/unpack` for structuring complex conversations into sequential
threads, `/brainstorm-cluster` for structured brainstorming with flexible
participation modes, `/steelman` for building the strongest case for alternatives,
and `/devils-advocate` for stress-testing plans and proposals.

## Prerequisites

- **NLA Framework** — The target NLA must be built on the NLA framework.
- **This repo cloned as a sibling** — `../nla-process-helpers/` relative to the NLA.

## What's in This Directory

Each file describes the **intent** of changes needed at a specific integration point
in the target NLA. The installing AI reads these intents and synthesizes them into
the NLA's existing files in whatever way fits that NLA's structure and voice.

| File | Integration Point | Purpose |
|------|------------------|---------|
| `CLAUDE-intent.md` | NLA's CLAUDE.md | What the NLA's runtime identity should know about facilitation techniques |
| `skills-intent.md` | NLA's .claude/skills/ | What skill wrappers to create |

## How Installation Works

1. Read each intent file in this directory.
2. For each one, examine the target NLA's current state at that integration point.
3. Synthesize the intent into the NLA's existing files — don't paste, integrate.
   Match the NLA's voice, structure, and conventions.
4. Log what was done and why in the NLA's install log (see below).

## The Install Log

After making changes, the installing AI should record what it did in the target NLA.
This log is how future updates and uninstalls know what came from this package.

For each integration point changed, record:
- Which package and intent file prompted the change
- What the intent was (in your own words)
- What concrete changes were made and where
- The state of this install directory at the time (commit hash or date)

The format and location of this log is up to the NLA. A reasonable default:
`reference/installed-packages.md`.

## Updating

When this install directory changes (new intent, revised intent, removed intent),
the NLA's `/update` skill should:

1. Diff this directory against the state recorded in the install log.
2. For changed intents, re-read the intent and re-synthesize. Use the install log
   to understand what was previously done.
3. For removed intents, use the install log to understand what to undo.
4. Update the install log.

## Removing

To uninstall process helpers, read the NLA's install log for all changes attributed to
this package, reverse them, and remove the log entries.

---

*This manifest is maintained as part of the process helpers package. Changes here should
be deliberate — they affect every NLA that has process helpers installed.*

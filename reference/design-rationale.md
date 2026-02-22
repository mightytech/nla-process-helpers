# Design Rationale

This document explains WHY the process helpers package is built the way it is.

**Audience:** Package maintainers (human or AI) who need to understand the decisions before modifying them.

---

## Why a Package, Not Core

Process helpers were originally considered for the framework's core (and `/unpack`
started there). The /think session that led to this package identified a key distinction:

**Phase skills define *when*.** `/think` (before planning), `/debrief` (after work) —
these are about the work lifecycle. Every NLA does work. Every NLA has a lifecycle.
Phase skills are universal infrastructure.

**Process helpers define *how*.** `/unpack` (sequential thread-by-thread) is one way
of managing complex conversations. Other valid approaches: document-for-inline-annotation,
everything-at-once-and-steer, structured Q&A. How you manage conversations is a
preference, not infrastructure.

The reframing that clinched it: "unpack is useful across sessions — but it's also the
way *I* like to work. I can imagine other people preferring different ways." When a
skill reflects a personal working style rather than a universal need, it belongs in
an installable package where users opt in.

## The Phase/Process Distinction

An analogy: phase skills are "what meeting are we in?" (standup, retrospective, planning).
Process helpers are "what facilitation technique are we using?" (round-robin, parking lot,
dot voting). You always need meetings (phases). You choose your facilitation style
(process).

## Selective Installation (Future Direction)

When this package has multiple techniques, users should be able to choose which ones
to install. The `/install` skill would present available techniques and let the user
pick. This changes what a package *is* — from "install all as a unit" to "a catalog
of related capabilities, take what you want."

Not implemented yet because with one technique there's nothing to select. The mechanism
would be a general `/install` enhancement, not specific to this package — penny post
might benefit too.

## Facilitation Techniques as a Category

The design rationale for `/unpack` in the framework's `reference/design-rationale.md`
identified a new skill category: "technique skills that layer on active context rather
than replacing it." This package is where that category lives.

Characteristics of facilitation techniques:
- They layer on whatever's already active (no mode switch)
- They structure *how* conversations happen, not *what* they're about
- Multiple can be active simultaneously (they compose)
- They end naturally when their purpose is served (no formal exit)
- Subject matter expertise comes from the active context, not the technique

---

## Adding Decisions

When you make architectural changes to this package, add an entry here documenting:
- What was decided
- Why (including what alternatives were considered)
- What it affects

---

*This document is updated by the `/maintain` skill when architectural decisions are made.*

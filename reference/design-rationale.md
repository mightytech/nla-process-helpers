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

With two techniques now in the package (`/unpack` and `/brainstorm-cluster`), selective
installation is practically relevant. The mechanism would be a general `/install`
enhancement, not specific to this package — penny post might benefit too.

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

## Brainstorm-Cluster and Participation Modes

`/brainstorm-cluster` is the second facilitation technique, adding structured
brainstorming (frame → generate → cluster → evaluate → refine). It validates the
package model — techniques that share a shape (layering, composability, natural exit)
but serve different facilitation needs.

The technique introduces **participation modes** — a pattern not present in `/unpack`.
At each phase, the human chooses: AI leads, human leads, or simultaneous. This was
driven by a key insight: the same brainstorming process should scale from quick
low-stakes uses (AI runs everything, human reviews) to deep high-stakes exploration
(human engages at every phase) without changing the process itself. The structure is
fixed; the participation is flexible.

**Why three modes, not two?** AI-leads and human-leads cover the obvious cases.
Simultaneous mode exists specifically to avoid anchoring — when the AI shows ideas
first, the human's thinking narrows around them. In simultaneous mode, the AI
generates but withholds, the human generates independently, then both reveal. Neither
constrains the other. This matters most during initial generation, where anchoring
has the biggest impact.

**"AI leads" and the Cardinal Rule.** "AI leads" means the AI does the *work* — it
generates ideas, proposes clusters, offers evaluations. It doesn't mean the AI
*decides*. The human chose the mode, can switch at any transition, and the technique
is explicit that evaluations are "proposals, not verdicts." The cardinal rule ("the
human decides") operates at the decision level, not the labor level.

**Carry-forward confirmation.** Rather than asking "who should lead?" at every phase
(overhead) or setting it once at the start (inflexible), the technique carries forward
the last answer and confirms briefly at each transition. This emerged from the insight
that a simple "yes" should keep things flowing, while any other response naturally
redirects. Low friction when the human wants to stay hands-off, easy to change gears
when they don't.

## Steelman and the Advocacy Model

`/steelman` is the third facilitation technique. Where `/unpack` structures complex
conversations and `/brainstorm-cluster` explores possibility spaces, `/steelman`
ensures alternatives get a fair hearing before a decision is committed.

**Why advocacy, not analysis?** The technique deliberately builds *cases*, not
*comparisons*. A pros/cons list is neutral; a steelman is persuasive. The
distinction matters because a balanced overview lets you nod along — a genuinely
persuasive case for an alternative forces you to engage with it seriously. The
quality bar is high: a weak steelman gives false confidence that alternatives
were considered.

**Why no participation modes?** Unlike brainstorm-cluster, where anchoring is a
real concern and the human may want to generate independently, steelman is
inherently AI-led. The human already has their preferred direction — they're
asking the AI to make the case they can't (or won't) make for themselves. If
the human could already build the strongest case for the alternative, they
probably wouldn't need the technique.

**Why "any outcome is success"?** The technique's value is the fair hearing, not
the reversal. A human who commits to their original direction after hearing the
strongest possible alternative case is making a better decision than one who
commits without hearing it. Changed mind, confirmed direction, and "I need to
think about this more" are all the technique working.

**Steelman vs. devil's advocate.** These came up as separate items in the
brainstorm that generated `/steelman`. They're complementary: steelman builds up
alternatives (advocacy), devil's advocate tears down proposals (adversarial
testing). You could run both on the same decision and get different information.
They may both end up in the package eventually.

---

## Adding Decisions

When you make architectural changes to this package, add an entry here documenting:
- What was decided
- Why (including what alternatives were considered)
- What it affects

---

*This document is updated by the `/maintain` skill when architectural decisions are made.*

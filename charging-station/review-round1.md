# Project Review — Round 1

**Reviewer:** project-reviewer agent
**Source of truth:** `/home/user/GolfAI/CLAUDE.md`
**Reviewing:** `design-concepts-round1.md` (room-designer) + `electronics-plan-round1.md` (electronics-expert)

## Verdict: NONE APPROVED YET

No concept is cleared to move to printing-expert/builder this round. The
electronics plan itself is solid and close to final — the port math, labeling
scheme, and safety flags all check out against the brief. The gap is in the
**fit between the two documents**: several of the electronics plan's own
hard requirements are either not met, or not yet confirmed as met, by any of
the three forms as currently described. These are concrete, fixable gaps,
not a rejection of the whole direction.

**Recommended path:** Concept 2 ("Keepsake Chest") is the closest to
approvable and should be the primary target for round 2 fixes. Concept 1
("Gallery Mantel") stays alive as the ambitious option pending fixes.
Concept 3 ("Conservatory Bench") is held back — not because water-adjacent
electronics is disqualifying on principle (the electronics plan already
gives an acceptable mitigation path), but because Concept 3's own writeup
contradicts itself on what that mitigation actually is.

---

## Cross-cutting issue #1 (applies to ALL THREE concepts): brass near the watch-puck coils

Electronics plan §2.1 / §5.5 is explicit and physics-based: **no metal
(brass inserts, screws, magnets, foil paint) within ~20 mm of the puck
coil** — eddy heating and alignment interference. This is a real
engineering constraint, not a style note.

Every concept currently puts real brass immediately around the puck wells:

- Concept 1: "brass-ringed collar" directly around each puck well.
- Concept 2: "miniature gallery rail... stock brass rod" around the valet
  tray holding the puck wells.
- Concept 3: "brass-collared flush wells."

**Action for room-designer:** keep the brass, but move it outside the 20 mm
exclusion radius from each puck's coil center — e.g., brass trim on the
*outer* edge of the tray/valet area rather than a ring directly circling
each well, with the immediate puck surround done in matte-black or
Rub 'n Buff-finished plastic (which Concept 2 already proposes elsewhere as
a brass-look treatment). This should be a small, low-risk redraw for all
three concepts, but it must show up explicitly in round 2 — don't just
assert "collar is decorative" and hope the radius works out.

## Cross-cutting issue #2: vent geometry isn't specified precisely enough to confirm the diagonal cross-flow requirement

Electronics plan §4 requires **low intake on one side of the brick chamber
and high exhaust on the other side**, specifically to force a diagonal flow
*across* the brick (not just up-and-out one shared wall), plus ≥10 cm² net
open area on each of intake and exhaust independently.

- **Concept 1:** describes "a vent band" (singular) disguised as dentil
  molding at the rear. As written this reads as one register at one height,
  not a separated low-intake / high-exhaust pair. Dentil-molding "teeth" are
  also a tight, decorative geometry — it needs a real check that it can hit
  10 cm² per field without the teeth becoming obviously oversized and
  blowing the disguise.
- **Concept 2:** "full-height slatted vent" on the rear panel is a good
  instinct (it does span low-to-high) but it's a single wall, so intake and
  exhaust both live on the same face — this doesn't obviously produce a
  diagonal path *across* the brick, it may just short-circuit near-field air
  at that one wall. Needs either a second vent field on the opposite side of
  the brick chamber, or the electronics-expert should confirm a single-wall
  low+high pair is acceptable given the brick's placement (their call, but
  it needs to be said explicitly, not assumed by the room-designer).
- **Concept 3:** "arched apron cutouts front and back" — front and back is
  actually closer to the intent (opposite sides), but the writeup doesn't
  say which is low/intake vs. high/exhaust, and an apron cutout is usually
  at the *bottom* of a bench face on both sides, which wouldn't give a high
  exhaust point at all.

**Action for room-designer (whichever concept proceeds):** state explicitly,
in the geometry, which vent field is low-intake, which is high-exhaust,
that they're on different sides of the brick chamber (not the same wall),
and a rough slot count/size showing the 10 cm² floor is achievable in that
decorative language. **Action for electronics-expert:** confirm in round 2
whether a single-wall low+high pair (Concept 2's case) is thermally
acceptable, or whether true opposite-side venting is a hard requirement —
right now the plan states the rule but doesn't rule on this specific
question.

## Cross-cutting issue #3: rear-wall clearance risk

All three concepts route the brick's AC cord exit and (in Concepts 1 and 2)
the only vent field through the **rear** face. Credenzas are typically
pushed close to a wall. If this one is flush or near-flush, a rear-only
vent/cord-exit could be significantly restricted in practice, independent of
the on-paper vent math. This isn't in the brief as a stated dimension, so
I'm flagging it as an assumption to verify rather than a hard defect:
**someone should confirm how much clearance exists behind the credenza**
before locking a rear-only vent/cord strategy. Concept 3's front-and-back
apron venting is naturally more robust to this risk than Concepts 1 and 2's
rear-only schemes — worth factoring into the final choice.

## Cross-cutting issue #4: second AC exit (Echo Dot's wall wart) is unresolved

Electronics plan §3.4 and §7.5 explicitly call this out as an open item and
ask the room-designer to answer it: the Echo Dot keeps its own wall-wart, so
there are **two independent AC paths** to the wall, not one. All three
concepts describe routing for the brick's coiled cord but say nothing about
where the Dot's wart sits or how its thin barrel cord reaches the Dot's nest
from a wall outlet or power strip. This needs an explicit answer in round 2
for whichever concept proceeds — it affects where the Echo Dot nest can
actually be positioned relative to the outlet.

---

## Per-concept notes

### Concept 1 — Gallery Mantel
Best answer to the brief's "disguise as decor" ask and the boldest fix for
the whole clutter tableau. Compatible with the port plan device-for-device.
Blocked on: canvas dimensions (self-flagged, fine to defer), the vent-field
issue above (highest risk of the three, given the decorative dentil
constraint), and confirmation the crown/top deck sitting over the brick
doesn't trap heat (electronics plan's rule about shelf-over-brick requiring
rear/high exhaust is nominally satisfied by intent, but needs the vent-field
fix above to actually deliver on it). Multi-part print risk is a
printing-expert problem, not a blocker at this stage.

### Concept 2 — Keepsake Chest
Closest to done. Real brass pulls doing most of the disguise work is a
strong, low-risk idea; full-height rear vent is workable pending the
vent-field question above; smallest footprint keeps the expansion story
simple. Two things to close before this can be approved: (1) the brass-rail
metal-exclusion conflict (Issue #1), (2) the concept's own flagged risk —
top-deck density (pucks + Dot + rotator on 11 x 7.5 in) — needs the
rotator's actual sweep envelope checked against the deck before we accept
it fits, not just accept the concept's own "acceptable fallback" hand-wave
about moving the rotator to a side pedestal. If it doesn't fit, say so now
and show the pedestal fallback as the real geometry, not a footnote.

### Concept 3 — Conservatory Bench — hold
The electronics plan's mitigation path for a planter near electronics
(sealed one-piece liner + overflow routed away from vents/cables) is a
reasonable, non-disqualifying answer *in principle*. But Concept 3's own
description contradicts itself on what the mitigation actually is:

- Device-placement section: "pot sits in a printed cachepot socket with a
  sealed drip liner... any overwater ends up on the credenza, not in the
  wiring." Routing overflow onto the bare oak credenza top is not an
  acceptable outcome on its own — that's swapping an electronics risk for a
  finish-damage risk to the actual piece of furniture the whole project
  exists to declutter.
- Materials section: "the planter cup interior gets a brushed-on waterproof
  coating (**or** simply holds a cheap nursery-pot saucer as the true
  liner)" — this is a different, less rigorous mitigation than the "sealed
  drip liner" claimed earlier, offered as an interchangeable alternative.

These need to resolve to **one** concrete answer (sealed liner with a
defined overflow catch that doesn't hit the credenza — e.g., a shallow
integrated saucer basin with its own small drain reservoir — not "or a
saucer" as a shrug), plus the vent-field fix (Issue #2) and the brass
exclusion fix (Issue #1), before Concept 3 is reconsidered. Given it also
has the weakest vent-field description of the three, it's the lowest
priority to fix unless the reviewer specifically wants the planter-disguise
angle — recommend not spending round 2 effort here unless Concepts 1/2 both
stall.

---

## What's already solid (no changes requested)

- Port assignment (C1/C2 → watch pucks, A2 → rotator, C3/A1/A3 → labeled
  swappables) matches the brief's 3-permanent/3-swappable math exactly, uses
  USB-A1's distinct/faster marking correctly per the brief's instruction not
  to assume all-A-ports-equal, and correctly excludes the Echo Dot and the
  optional Caniifoto chargers from brick port scope.
- Captive-cable-with-parked-tip approach for the 3 swappable ports is a good
  answer to "hides cabling" while keeping ports labeled and accessible.
- Label text (§6 of the electronics plan) is complete, all-caps,
  emboss-ready, and follows the device rather than the physical port —
  satisfies the brief's labeling requirement as-is.
- All three forms correctly scope to one Gakezi brick, no dual-bay
  over-building, and all three have a plausible flanking/stacking expansion
  story per the brief's "don't over-engineer, don't preclude a second unit"
  note.
- Echo Dot exposure (open top, open/grille sides, never fully enclosed) is
  handled correctly in all three concepts.

## Next steps

1. **room-designer:** pick Concept 2 as primary (Concept 1 as backup) and
   revise for: brass-exclusion-zone fix (Issue #1), explicit low/high
   vent-field geometry with a rough area check (Issue #2), an answer on the
   Echo Dot's wall-wart routing (Issue #4), and — for Concept 2 specifically
   — a real check (not a hand-wave) of the rotator's sweep envelope on the
   11 x 7.5 in deck. Also confirm/assume rear clearance behind the credenza
   (Issue #3) and note it as an assumption if no hard number is available.
2. **electronics-expert:** rule explicitly on whether a single-wall
   low+high vent pair (Concept 2's case) is thermally acceptable or whether
   true opposite-side venting is required — the current plan states the
   rule but not this edge case. Everything else in the round-1 electronics
   plan stands as-is; no rework needed there otherwise.
3. Once both are updated, bring back for a round-2 review before this goes
   to printing-expert. I'd expect round 2 to be a fast approval if the four
   cross-cutting items above are closed cleanly on Concept 2 (or Concept 1).

No consolidated spec is being handed to printing-expert/builder yet — there
isn't an approved concept to hand off.

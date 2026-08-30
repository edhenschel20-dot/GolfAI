# Project Review — Round 2

**Reviewer:** project-reviewer agent
**Source of truth:** `/home/user/GolfAI/CLAUDE.md`
**Reviewing:** `design-concepts-round2.md` (room-designer) against `review-round1.md`
and `electronics-plan-round1.md` (electronics-expert has not published a
round-2 update; no `electronics-plan-round2.md` exists at review time).

## Verdict: Concept 2 — "Keepsake Chest" — APPROVED to proceed to
printing-expert, with one narrow, explicit contingency gate before the
overall envelope is locked for final tooling.

All four round-1 cross-cutting fixes are closed with real geometry, not
assertions. One new item surfaced by the fix itself (the rotator sweep
envelope used to size the box is room-designer's own assumption, not a
measurement) is a genuine gap — but it gates only the chest's overall
footprint and the rotator bay cavity, not the rest of the design. Everything
else below is cleared and can move forward now.

---

## Round-1 findings: closed or not

### Issue #1 — brass within 20 mm of puck coils — **CLOSED**
Concept 2 relocates all brass to the front deck-edge rail (≥50 mm from
either coil center) and the two drawer pulls; the immediate puck zone (40 mm
radius, double the 20 mm floor) is plain, non-metallic espresso-stained
plastic, and the "Rub 'n Buff counts as metal" catch is a good, correct
catch by room-designer that round 1 didn't even ask for. Concept 1's
relocation (≥100 mm) is likewise closed. No metal fasteners within 40 mm of
either coil center — passed to printing-expert as a design rule. Verified
against electronics plan §2.1/§5.5 (≥20 mm floor) — both concepts clear it
with margin.

### Issue #2 — vent geometry (opposite-side low-intake/high-exhaust, ≥10 cm²
each) — **CLOSED**, verified by arithmetic
Concept 2: front toe-kick intake 280×4 mm = 11.2 cm²; rear+side shadow-gap
exhaust (330+240)×4 mm = 22.8 cm² gross / ≥14 cm² net. Both fields exceed
the 10 cm² floor, sit on genuinely opposite sides of the brick chamber
(front-low vs. rear/side-high), and the brick remains on standoff ribs with
clearance on all faces per §3.1. This resolves round 1's specific objection
that Concept 2's original single rear wall couldn't produce true cross-flow.
Concept 1's split (front 20 cm² intake / rear+side dentil 18 cm² exhaust)
clears the same floor. I'm treating this as sanity-checked against the
electronics plan's explicit numeric rule directly, since the rule itself is
a fixed floor with no form-dependent judgment call left — a formal
electronics-expert sign-off is welcome but not blocking.

### Issue #3 — rear-wall clearance risk — **ADEQUATELY MITIGATED, not fully
resolved (flagged, non-blocking)**
Because a majority of the exhaust area now lives on the sides (240 of 330mm
worth in Concept 2), the vent floor is met even if the credenza sits flush
to the wall. The AC-cord clearance-behind-credenza question is still an
open real-world measurement, but room-designer supplied a no-shell-change
fallback (route both cords sideways along the back edge) if clearance turns
out to be zero. This is an acceptable way to carry an unmeasured assumption
forward — it no longer blocks geometry.

### Issue #4 — Echo Dot's second AC path — **CLOSED**
Dedicated 8 mm grommet, walled-off corner chase, separate from the brick's
AC exit and from the USB cable bay, in both concepts. Two AC exits, two
openings, no shared channel — matches electronics plan §3.4 exactly.

---

## New item this round: rotator sweep envelope is an unverified assumption
— **this is a real gap, and it is the one thing I'm not signing off on
unconditionally**

Room-designer's Fix 4 is good-faith, real engineering: they actually ran a
fit-check on the round-1 deck, found it failed, and grew the footprint to
make it honestly fit — that is exactly the "show the fit, don't hand-wave
it" behavior round 1 asked for, and it's the right instinct.

But the number they fit-checked against — 200 × 100 × 190 mm swept volume —
is room-designer's own assumption, not a measurement from electronics-expert
(who owns this action item at electronics-plan-round1.md §2.2 and §7.3) or
from the user's physical rotator unit. The entire footprint growth (11×7.5in
→ 13×8in) and the rear-right bay's 150×120mm allocation trace back to this
one unverified number. The risk is asymmetric:

- If the real sweep is **smaller or equal**, the current 13×8×7in geometry
  is safe as-is — no rework needed.
- If the real sweep is **larger** in any dimension beyond the stated ≥20mm
  buffers, the zone map breaks (arm intrudes on the Echo Dot buffer or off
  the deck edge in an unintended way) and the box needs to change shape
  again — which is exactly the failure mode round 1 was trying to prevent by
  asking for a real fit-check in the first place.

**This is a blocking gap for locking the chest's *overall envelope* and the
rotator bay's *final cavity dimensions* — it is not a blocking gap for
everything else in this document.**

**What's needed, from whom, before printing-expert cuts final tooling
geometry for the chest body and rotator bay:**
- **electronics-expert** (this is their existing open action item, not a new
  ask) should physically measure — or have the user measure — the actual
  Pokémon-egg-hatcher rotator with a large phone mounted: full swept width ×
  depth × height of the rocking motion above the base, plus confirm the
  device-side and brick-side connector types called out in electronics-plan
  §2.2 while the unit is in hand.
- Compare against the 200×100×190mm assumption and the zone-map buffers in
  `design-concepts-round2.md`.
- **Decision rule (pre-approved, no further design-round needed either
  way):** if the measured envelope fits inside the current zone map with its
  stated ≥20 mm buffers, the 13×8×7in single-body Keepsake Chest geometry in
  this document is final. If it does not fit, use the already-drawn
  fallback in the same document (11×7.5×7in single-body chest + separate
  6×6×5in quarter-round side pedestal for the rotator, cable entering via a
  grommeted side port) rather than re-widening the single body a second
  time.

Printing-expert can proceed now with wall thickness, supports, part-split,
and material/finish work against the 13×8×7in primary geometry below — that
work is not wasted even if the fallback triggers, since the same techniques
carry over to the pedestal variant. Only the chest's outer envelope and the
rotator bay's cut lines should be held until the measurement lands.

**Routine, non-blocking confirmations** (normal printing-expert prep, not a
design-round issue): exact watch-puck diameter/height and connector type
(USB-C vs USB-A), exact USB-A1 wattage/spec text, hand-measured brick
dimensions vs. the 172×102×36mm spec. These affect small internal cutouts by
a few mm, not the macro form, and are appropriately left to printing-expert's
detailed-CAD pass per electronics-plan §7.

---

## What else was checked and passed

- **Hides the brick/cable mess:** yes — brick fully enclosed on standoffs
  with clearance, captive cables with parked labeled tips for the 3 swappable
  ports, both AC cords routed through separate walled-off chases. Nothing but
  connectors/devices visible.
- **Fits the room:** oak-toned wood-fill PLA + gel stain + real brass pulls,
  height (7in) stays below the canvas's lower third, sized to sit beside it.
- **Doubles as decor:** the two-drawer jewelry-chest disguise is intact and
  is doing real work — approved direction, unchanged from round 1's
  assessment.
- **Port/device plan:** unchanged from `electronics-plan-round1.md` and
  still solid — 3 permanent (C1 his watch, C2 her watch, A2 rotator) + 3
  swappable labeled (C3 fast-C, A1 fast-A, A3 slow-A) matches the brief's
  math exactly; Echo Dot correctly kept off the brick.
- **Form/electronics compatibility:** Echo Dot stays exposed (40% proud,
  open top/sides); cable routing (permanent runs, swappable park notches, two
  AC chases) is now explicitly mapped onto specific zones inside the stated
  330×203mm deck rather than asserted to "fit somewhere."
- **Safety/physics:** heat (two real vent fields, standoff clearance),
  puck alignment (metal exclusion with margin), AC pinch (separate relieved
  channels) — all check out against the electronics plan's hard rules.
- **Scope:** single Gakezi brick, no Caniifoto bay built in, mirrored-twin
  expansion story preserved qualitatively at the new size. The footprint
  growth is justified by a real fit-check failure, not scope creep.

## Not approved this round

- **Concept 1 — "Gallery Mantel":** fixes applied correctly and it remains a
  valid backup, but it's still self-gated on an unmeasured canvas
  width/height before its own geometry can be trusted, plus multi-segment
  print risk deferred to printing-expert. Not ready to hand off in parallel;
  revisit only if Concept 2's rotator measurement forces the pedestal
  fallback and the team wants to reconsider options.
- **Concept 3 — "Conservatory Bench":** one-line water-mitigation fix landed
  as requested, but per round 1's own guidance this stays deprioritized
  unless Concepts 1/2 stall. They haven't. No further action needed here.

---

## Consolidated spec — Keepsake Chest (for printing-expert and builder)

Everything below is the single source of truth for this build; no need to
re-read prior rounds.

### Form
Upright two-faux-drawer chest ("jewelry chest" disguise). Raised-panel faux
drawer fronts, two real ornate brass drawer pulls (matched to the credenza
hardware), overhanging rounded-edge top, bracket-foot plinth base (~19mm
riser), lift-off rear service panel. Finish: wood-fill PLA/PETG + golden-oak
gel stain + matte poly (or faux-grain paint alternate), real brass hardware.

### Dimensions
- **Primary (pending rotator-measurement confirmation, see gate above):**
  13 in W × 8 in D × 7 in H (330 × 203 × 178 mm).
- **Fallback (pre-approved, use only if measured rotator envelope exceeds
  the zone-map buffers below):** 11 × 7.5 × 7 in single-body chest + a
  separate 6 × 6 × 5 in quarter-round side pedestal for the rotator, butted
  to the chest's right face, cable entering through a grommeted side port.

### Top-deck zone map (330 × 203 mm deck, ≥20mm buffers between zones)
| Zone | Location | Footprint |
|---|---|---|
| Watch-puck valet tray | front-left | 150 × 75 mm, two seats, centers 70mm apart, tray front edge 20mm back from deck edge |
| Spare-tip park notches (3) | front-right | 90 × 60 mm |
| Echo Dot nest | rear-left | 110 mm dia, ~40% proud, open top/sides |
| Rotator bay | rear-right | 150 × 120 mm floor, base recessed 25 mm; sized against an **assumed** 200×100×190mm sweep envelope — confirm before final cut, see gate above |

### Port / device plan (unchanged from electronics-plan-round1.md)
| Brick port | Device | Type |
|---|---|---|
| USB-C1 | His Galaxy Watch puck | Permanent, hard-routed |
| USB-C2 | Her Galaxy Watch puck | Permanent, hard-routed |
| USB-A2 | Phone rotator cradle | Permanent, hard-routed |
| USB-C3 | Spare — fast 20W | Swappable, captive cable + parked tip |
| USB-A1 | Spare — fast (exact spec TBD, read off physical unit) | Swappable, captive cable + parked tip |
| USB-A3 | Spare — slow 5V | Swappable, captive cable + parked tip |

Echo Dot: own wall wart, not on the brick, needs venting/space only.
Optional Caniifoto chargers: not used in v1; hold as future Expansion
hardware.

### Vent fields
- **Low intake:** front toe-kick slot behind plinth reveal, 280×4mm ≈
  11.2 cm².
- **High exhaust:** shadow-gap reveal under top overhang, rear (330mm) +
  rear 120mm of each side ≈ (330+240)×4mm = 22.8 cm² gross / ≥14 cm² net
  after baffle ribs.
- Fields on opposite sides of the brick chamber (front-low → rear/side-high
  diagonal cross-flow). Brick on standoff ribs, ≥10mm clearance all faces.
- Material: brick-chamber walls/ribs in PETG/ASA (PLA only acceptable with
  full 10mm gap + verified airflow per electronics plan §4).

### AC routing (two independent paths, never shared)
- Brick's integrated coiled AC cord: exits low rear-right via keyhole/
  snap-cover channel; coil stored behind the shell, not in the warm chamber.
- Echo Dot's wall-wart barrel cord: enters via dedicated 8mm grommet low
  rear-left, rises through a walled-off corner chase (isolated from brick
  chamber and USB cable bay), emerges through the Dot nest floor. Wart itself
  stays outside the shell, behind the credenza.
- If behind-credenza clearance turns out to be ~0: both cords reroute
  sideways along the credenza back edge — no shell geometry change needed.

### Brass / metal exclusion
- No metal (brass, screws, foil paint, Rub 'n Buff) within 40mm of either
  watch-puck coil center (2x the 20mm electronics-plan floor).
- Brass lives at: the two drawer pulls, a front deck-edge gallery rail
  (≥50mm from either coil), optional small nameplate on the plinth face.
- No metal fasteners within 40mm of either coil center — that region snaps
  or glues (printing-expert design rule).

### Labels (emboss/engrave, ≥5mm cap height, all-caps)
| Location | Text |
|---|---|
| His watch puck seat | HIS WATCH |
| Her watch puck seat | HER WATCH |
| Rotator cradle base | EGG HATCHER — DO NOT UNPLUG |
| Spare tip park (C3) | SPARE C — FAST 20W |
| Spare tip park (A1) | SPARE A — FAST *(finalize wattage after reading A1's printed spec)* |
| Spare tip park (A3) | SPARE A — SLOW |
| Echo Dot nest (optional) | ECHO |
| Internal brick-end tags | C1 HIS / C2 HERS / A2 ROTATOR / C3 SPARE / A1 SPARE / A3 SPARE |
| Optional house-rule plate near spares | SPARES ONLY — EVERYTHING ELSE STAYS PUT. |

### Open items before final tooling
1. **Gating:** rotator sweep envelope — measure the physical unit with a
   large phone mounted (electronics-expert and/or user); confirm against
   200×100×190mm and the zone-map buffers before cutting the chest's outer
   envelope and rotator bay. Apply the fallback geometry above if it fails.
2. Routine (printing-expert detailed-CAD pass): exact watch-puck diameter/
   height and connector type; exact USB-A1 spec text for the label; hand-
   measured brick dimensions vs. 172×102×36mm spec.

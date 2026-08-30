# Manufacturability / Printability Pass — Round 1

**Author:** printing-expert agent
**Source of truth:** `/home/user/GolfAI/CLAUDE.md`
**Working from:** `review-round2.md` (consolidated "Keepsake Chest" spec, approved),
cross-referenced against `design-concepts-round2.md` and
`electronics-plan-round1.md` for supporting detail.
**Baseline geometry used throughout:** primary 13 x 8 x 7 in (330 x 203 x
178 mm) single-body chest, per the reviewer's explicit instruction to work
from primary and flag rotator-bay-specific numbers as provisional. Fallback
(11 x 7.5 x 7 in chest + separate 6 x 6 x 5 in pedestal) is addressed
wherever it changes the answer.

## Status / flags up front

Nothing here is severe enough to bounce back to project-reviewer as
"not manufacturable" — one item is the already-known, already-gated rotator
sweep measurement (carried forward below with provisional numbers, per
instruction, not re-litigated), and two items (watch-puck exact OD/height,
brass-rail hardware-vs-print method) are resolved below with parametric
designs rather than guessed fixed numbers, consistent with how
electronics-plan-round1.md §7 already left them for this pass. No new gaps
that block work.

One assumption I'm making explicit: the brief's confirmed brick dimensions
(6.77 x 4.01 x 1.41 in = 172.0 x 101.9 x 35.8 mm) are used as-is below; the
spec itself already flags a pre-final hand-measurement check, which I'm not
duplicating as a new blocker, just carrying forward.

---

## 1. Printability pass — orientation, overhangs, bridges

### Key structural decision: make the top deck a separate lid, not integral to the body walls

The zone map's "top deck" (330 x 203 mm) sits at 178 mm height, overhangs
the body walls by 12 mm on sides/rear, and has four pockets recessed into
its top face (puck wells, Dot nest, rotator bay). If this deck were printed
as the *top* of an otherwise-hollow body (walls rising from the plinth, deck
closing the top), it would have to bridge across the ~150-190 mm open brick
chamber unsupported — well beyond FDM's reliable unsupported bridge range
(~40-80 mm depending on material/cooling) — and the 12 mm overhang lip would
be a genuine unsupported cantilever over the vent gap in that orientation.

**Recommendation: split the deck out as its own printed lid, glued/screwed
onto the top edge of the wall/plinth assembly after both print.** This is a
zero-cost change relative to the part-splitting plan in §2 below (the deck
was already going to be split left/right for bed-size reasons) and it
eliminates both problems at once:

- **Body-Left / Body-Right** (plinth + walls + brick chamber, open top,
  rear cutout for the lift-off service panel): printed **plinth-down**, the
  natural/intended orientation. This is a straightforward open-top tray —
  no internal horizontal ceiling to bridge, no overhangs on the vertical
  walls. Clean, support-free print.
- **Deck-Left / Deck-Right** (the lid, carrying all four device zones):
  printed as a **flat panel**, fully bed-supported for its own print
  regardless of the 12 mm cantilever it has once assembled — the overhang
  only exists in the *assembled* state, not during the lid's own print, so
  it's a non-issue. Print topside-up (visible face up) so the pocket walls
  and emboss text get the finer top-layer control; recommend a 0.12-0.16 mm
  layer height for the last ~1.5-2 mm of the deck skin specifically for the
  puck wells, Dot nest lip, and emboss text crispness, with 0.2 mm for the
  bulk of the print.

If the builder instead prints the deck integral with the walls for any
reason, it will need tree supports filling most of the chamber, which are
genuinely hard to remove through vent-sized openings — I'd actively
recommend against that path rather than treat it as an equal option.

### Component-by-component

- **Drawer fronts (raised-panel appliques, x2, separate glued-on parts):**
  Raised-panel bevels are shallow (typically 10-25° off the panel plane),
  well under the ~45° self-supporting threshold — print flat, back face
  down on the bed, no supports. The recessed panel field is a shallow
  (1-2 mm) pocket, trivial. HIS WATCH / HER WATCH-style emboss elsewhere on
  the deck (not on the drawer fronts themselves, per the spec) should use
  ≥0.8 mm stroke width and ≥0.4-0.6 mm emboss height for legibility at the
  spec's ≥5 mm cap height — comfortably within one 0.4 mm nozzle's
  resolution.

- **Valet deck / puck wells:** Printed as part of the flat Deck-L lid
  (topside up), the pocket walls are simple vertical cylinder walls — no
  overhang. The cable channel exiting the pocket floor to the underside is a
  straight vertical hole; keep it ≤8 mm diameter (or a slight teardrop
  profile above that) so it bridges cleanly with zero support at any
  reasonable layer height.

- **Echo Dot nest:** A recessed bowl/cradle open at the top is inherently
  self-supporting when printed cup-up (each layer sits on a slightly wider
  layer below it, like any container) — no supports needed regardless of
  which lid half it ends up on.

- **Rotator bay:** Recessed floor pocket, same logic as the puck wells — no
  overhang concern for the pocket itself. The mounting boss for the
  anchoring screw (see electronics-plan §2.2's anchoring requirement) prints
  fine as a vertical boss with a heat-set insert added post-print.

- **Bracket-foot plinth:** The classic ogee/scroll bracket-foot profile
  curves *concave* — this is a genuine overhang if printed as part of the
  main body's natural (plinth-down) orientation. **Recommendation: make the
  four bracket feet separate small glued-on appliques**, each printed lying
  on its flat glue-face (i.e., reoriented independently of the main body),
  which removes the overhang entirely without supports. This also isolates
  the trickiest small-scale overhang geometry in the whole design into
  parts small enough that a failed print costs minutes, not a 15-hour body
  half.

- **Shadow-gap vent reveal (4 mm) and toe-kick intake slot (4 mm):** Both
  are simple thin slots cut into wall thickness, not open-air bridges (the
  intake sits inside the plinth's toe-kick recess; the exhaust reveal is
  cut into the underside of the now-separate deck lid, which is fully
  bed-supported during its own print as noted above). No overhang or
  bridging risk at 4 mm — see §5 for print-resolution confirmation.

- **AC keyhole/snap-cover channel:** A closed profile cut into a vertical
  wall — no overhang. The small snap-cover itself is a trivial flat part.

- **Rear service panel(s):** Flat/slatted lattice panel, printed flat, no
  overhang concern. See §2 for why this also gets split.

---

## 2. Part-splitting plan (bed-size math)

Design is currently specified in inches; converting: 13 in = 330 mm,
8 in = 203 mm, 7 in = 178 mm. A typical consumer FDM bed is roughly
220-300 mm on a side (Ender-class ~220x220, Prusa MK3/MK4 ~250x210,
Bambu X1/P1 ~256x256, up to ~300mm-class printers at the top end). **The
full 330 mm width exceeds essentially every bed in this range in a single
piece — splitting is required, not optional**, independent of the print
orientation questions in §1.

**Split plane: vertical, front-to-back, down the horizontal centerline.**
This conveniently falls in the ≥20 mm buffer gap the zone map already
reserves between the valet tray / spare-tip notches (front) and between the
Echo Dot nest / rotator bay (rear) — the seam doesn't cut through any
functional feature.

Resulting parts and footprints (primary 13x8x7in geometry):

| Part | Approx. footprint | Fits 220x220 bed? |
|---|---|---|
| Body-Left (plinth+walls+chamber half) | ~165 x 203 x ~160 mm tall | Yes, comfortably (>15 mm margin) |
| Body-Right (mirror) | same | Yes |
| Deck-Left lid (valet tray + Dot nest) | ~165 x 203 x ~8 mm | Yes |
| Deck-Right lid (spare notches + rotator bay) | ~165 x 203 x ~8 mm | Yes |
| Drawer-front applique x2 | ~140 x 110 x 8-12 mm | Yes, trivially |
| Rear service panel, split into 2 halves | ~165 x 140 x 4-6 mm each | Yes |
| Bracket-foot applique x4 | ~40 x 40 x 25 mm each | Yes, trivially |
| AC keyhole snap-cover x2 | ~20 x 30 x 4 mm each | Yes, trivially |

Every resulting part clears even the smallest common 220x220 mm bed with
real margin — **no diagonal-bed-packing tricks needed**, which is worth
calling out since a design this size could otherwise have forced that. I
recommend splitting the rear panel into matching left/right halves (rather
than one 330 mm-wide panel printed diagonally) purely for consistency of
approach and because it's hidden behind the credenza anyway, so a visible
centerline seam there costs nothing.

**Fallback geometry (11x7.5x7in chest + 6x6x5in pedestal):** if triggered,
the chest halves shrink further (~140 x 190 mm each — trivial fit on any
bed), and the pedestal (152 x 152 x 127 mm) is small enough to print as a
**single un-split piece** on essentially any consumer printer, which also
simplifies its internal cable/mounting design since it no longer has to
share a lid with the Dot nest and spare-tip zones. Net effect on time/cost
is roughly a wash (see §6) — the chest gets a bit cheaper, the pedestal is
a new but small extra print.

### Joinery

| Joint | Load | Method |
|---|---|---|
| Body-Left ↔ Body-Right (base/plinth band, bottom ~35 mm) | Structural — carries full assembled weight, resists racking | 3x M4 brass heat-set inserts + M4x16 SHCS through the plinth band, hidden inside the toe-kick shadow; plus 2x 6 mm dowel pins (real wood or nylon dowel, not printed plastic pins — better shear strength) for registration during glue-up |
| Body-Left ↔ Body-Right (wall face above plinth, up to deck line) | Cosmetic/stiffening | PETG-compatible plastic cement or 2-part epoxy along the full mating edge, clamped 30-60 min; seam disguised by a printed **center stile** (~12 mm wide applied vertical strip glued on after assembly, straddling the seam between the two faux drawer fronts) — this doubles as period-correct furniture styling (a center muntin between two drawers), so the structural seam becomes invisible rather than merely hidden |
| Deck-Left ↔ Deck-Right | Light — no functional feature straddles this seam per the zone map's buffers | 2x 4 mm dowel + glue, no screws needed |
| Deck lids ↔ Body tops (both sides) | **Primary load path** — puck wells, rotator vibration, Dot weight, hand resting on tray | M3 brass heat-set inserts (6-8 per side, ~40-50 mm spacing around the perimeter) + M3x10 screws driven up from underneath the overhang lip (hidden by the shadow-gap reveal), plus a full-perimeter glue bead. Mechanical, not glue-only, and keep every insert ≥40 mm from either watch-puck coil center (see §3) |
| Rear service panel(s) ↔ body | None — must lift off | 2x quarter-turn printed twist-tabs OR M4 thumbscrews into heat-set inserts per half; deliberately not glued, per the spec's "lift-off" requirement |
| Drawer-front appliques ↔ front wall | None (cosmetic) | Full-surface plastic cement/epoxy, clamp 24h — no fasteners, would be visible or need plugging |
| Bracket feet ↔ plinth corners | Minimal | Glue only; optional single alignment pin each for clamping |

---

## 3. Cutouts and tolerances

### Brick bay (172.0 x 101.9 x 35.8 mm confirmed dims)

This is a **standoff cradle, not a snug pocket** — per electronics-plan
§3.1/§4 the brick needs ≥10 mm air gap on all faces and ≥6 mm standoff
height off the floor, so the chamber's clear internal footprint should be
brick + 20 mm in each horizontal axis: **~192 x 122 mm clear**, with
interior chamber height at the brick's location ≥ 6 mm (standoff) + 35.8 mm
(brick) + 10 mm (top clearance to the deck underside) ≈ **≥52 mm**. No tight
tolerance is needed here — it's intentionally oversized for airflow, not a
fitted cutout. Re-confirm against a hand-measurement of the physical brick
before finalizing, per the spec's own note.

### USB-A / USB-C cutouts

Electronics-plan §2.4 recommends **captive cables with parked tips** over
panel-mount female couplers for all three spare ports (avoids known
PD-negotiation flakiness with USB-C extension couplers) — I'd reiterate that
as the default and only size panel-mount cutouts as a fallback:

- **Grommeted cable pass-throughs** (all 6 device runs + 2 AC exits): use
  bought snap-in rubber panel grommets rather than bare printed holes.
  Typical cable OD ~4-5 mm → 8 mm grommet for single cables, 10-12 mm for
  bundled pairs (the two watch-puck cables routed together). FDM-printed
  round holes commonly print 0.1-0.3 mm undersized vs. the CAD model at
  default 0.4 mm-nozzle settings — **print a quick calibration coupon**
  (holes at 7.8/8.0/8.2/8.4 mm etc.) before committing to a final hole size
  rather than trusting the nominal dimension blind.
- **Park-notch holsters** (3 swappable tips): size to the connector overmold
  + 1.0-1.5 mm clearance for easy one-handed insertion (USB-C overmold is
  ~12-13 mm wide x 6.5 mm tall per electronics-plan §5.6); add a small
  0.5-0.8 mm retention nub so the tip doesn't fall out unused. Print these
  in PETG, not PLA — PLA is more brittle for a thin flexing retention
  feature that gets handled daily.
- **Panel-mount fallback only, if the flush-socket route is chosen for the
  two A spares:** USB-A female receptacle cutout ≈ 13.0 x 6.5 mm nominal →
  cut 13.3 x 6.8 mm; USB-C female cutout ≈ 9.0 x 3.2 mm nominal → cut
  9.3 x 3.5 mm. These are generic allowances — get the exact coupler's
  datasheet dimensions before finalizing, they vary by manufacturer.

### Watch-puck seats — parametric (puck OD/height unmeasured, flagging rather than guessing)

Electronics-plan §2.1 already flags the puck as "typical 33-38 mm dia x
9-11 mm tall, hand-measure before final CAD" — I'm not guessing a fixed
number past that. Design rule instead:

- Pocket ID = **measured puck OD + 0.3 mm** for a snug friction fit (relies
  on the puck's own weight/friction), or **+ 0.6-0.8 mm** if adding a
  partial retention lip (needs the extra clearance for the lip to engage
  without binding on insertion).
- Pocket depth = **measured puck height − 0.5 mm**, biasing toward the
  puck sitting proud rather than exactly flush — the spec accepts
  "flush or 0.5-1 mm proud" but not recessed, and biasing proud is more
  forgiving of normal FDM z-tolerance (bed leveling / first-layer variance)
  than trying to hit exact-flush.
- Cable channel exiting the pocket floor: 6-8 mm dia straight hole, bridges
  cleanly with no support.
- **Fastener exclusion check:** the deck-to-body screw perimeter (§2) must
  stay ≥40 mm from either coil center per the spec's brass/metal exclusion
  rule. On the front-left panel (valet tray zone), that means omitting any
  perimeter insert directly in front of the tray and placing the nearest
  fasteners at the tray's left/right/front flanks instead, which the zone
  map's own ≥20 mm buffers make room for — confirm actual clearance once
  real coil-center coordinates exist in CAD, since "≥40 mm" needs checking
  against final geometry, not just the zone map's stated footprint.

### Rotator bay — PROVISIONAL, gated on the pending measurement

Per the reviewer's explicit note, these numbers are **not final**:

- Working baseline (primary 13x8x7in geometry): bay floor 150 x 120 mm,
  recessed 25 mm, sized against an **assumed, not measured** 200 x 100 x
  190 mm sweep envelope.
- Provisional wall thickness around the bay: 3-4 mm (matches body wall
  thickness elsewhere), with an M3 heat-set insert x2-3 at the pocket floor
  for the rotator's anchoring screw (per electronics-plan §2.2 — the
  rocking motion will walk an unanchored base into the walls over time).
  Cable exit: 8 mm grommet hole low in the bay's rear or side wall.
- The Deck-Right/Body-Right split line runs adjacent to this bay (§2) —
  that seam's exact position is also provisional until the bay's final
  cavity dimensions are locked, though the split-plane *concept* (centerline,
  in the buffer zone) is robust to modest changes in the bay's size.
- **If the measured sweep comes in at or under the assumed envelope:** the
  13x8x7in geometry and every number above stands as final.
- **If it exceeds the buffers:** per the pre-approved decision rule, switch
  to the fallback (11x7.5x7in chest + separate 6x6x5in pedestal) rather than
  re-widening the primary body again. This actually *simplifies* the
  printability picture for the rotator specifically — it becomes its own
  small, single-piece-printable enclosure, fully unconstrained by having to
  share a lid with the Dot nest and spare-tip zones, with its cavity/vent
  walls shaped directly around the real measured sweep once known. The
  pedestal needs no dedicated venting of its own (rotator draws ~2-3 W,
  negligible heat per electronics-plan §4) — just the grommeted side-port
  cable pass-through into the main chest already called out in the design
  concept.

---

## 4. Material and finish

**Structural filament: PETG throughout the Body-L/R chamber walls and both
Deck lids.** Electronics-plan §4 already requires PETG/ASA (not plain PLA)
for anything near the brick chamber; I'd extend that to the deck lids too,
since they take the repeated screw-in/out service load, the puck-well
retention-lip flex, and general dimensional stability against a sunny
credenza-top window scenario (PLA starts softening ~55-60°C; PETG holds up
meaningfully better). PLA is acceptable only for parts that never see
chamber heat or repeated flex: the drawer-front appliques and bracket-foot
appliques are fine in PLA if the builder wants easier printing/lower cost
for those cosmetic-only pieces — but PETG-throughout is my default
recommendation for consistency and lower risk.

**Wood-fill filament — flag a real tension:** commercially available
wood-fill filaments (ColorFabb woodFill, Fillamentum Timberfill, etc.) are
almost all PLA-based carriers; wood-fill PETG blends are rare/uncommon. You
can't get PETG's thermal/mechanical performance and a wood-fill blend in
the same filament for the chamber-adjacent parts. Practical resolution:
plain PETG for anything structural/hidden (chamber walls, deck ribs — grain
doesn't matter there, it's unseen), and reserve wood-fill PLA, if desired,
for purely cosmetic visible faces (deck top, drawer fronts, plinth face)
where its fleck texture gives stain something slightly more interesting to
grab onto. This is optional, not necessary — see below.

**Explicit call-out: a printed part alone, wood-fill or not, will not read
as real oak.** Oak's actual grain figure (open pores, ray flecks, a
directional pattern) is not something FDM layer lines or wood-fill flecking
replicates convincingly — at best you get "brown textured plastic," not
"oak." Recommended finishing path, in order:

1. Sand all visible printed surfaces progressively (150 → 220 → 400 grit)
   to knock down 0.2 mm layer lines — this step is mandatory regardless of
   filament choice, stain does not hide raw layer lines well.
2. **Bought-in finishing step (this is the one that actually gets you to
   "looks like oak"):** apply an adhesive-backed oak-grain veneer or
   wood-grain contact film to the flat visible faces (deck top, drawer
   fronts, plinth face) — sold for furniture refinishing, gives a real
   photographic/embossed grain pattern that stain-over-plastic cannot. This
   is more reliable than hoping wood-fill filament or gel stain alone gets
   there, and is the step I'd flag as non-optional if "looks like belongs
   next to real oak" is a hard requirement (it is, per CLAUDE.md).
   Alternative if veneer/film is skipped: hand-applied faux-grain glazing
   (base coat + grain comb/rocker + glaze) — a real furniture technique,
   achievable, but a genuine skill/time investment, likely more hours than
   the printing itself.
3. Matte or satin polyurethane topcoat over the stain/film for durability
   and a non-plasticky hand-feel.
4. **Real brass, not paint, for the pulls** (already specified) — buy
   pulls matched to the credenza hardware. For the gallery rail (≥50 mm
   from either coil, outside the metal-exclusion zone), real thin brass
   strip stock (e.g., K&S hobby brass strip, ~350 mm needed) gives the
   truest look and won't tarnish/wear like paint; Rub'n Buff brass wax on a
   printed rail is an acceptable budget alternative *only* for this rail,
   since it sits well clear of the puck-coil exclusion zone (Rub'n Buff is
   metal-flake wax and does count as "metal" for exclusion-zone purposes
   per the electronics plan, so keep it off anything near the pucks).

---

## 5. Structural / thermal notes

- **Valet deck (Deck-L/R lids):** 6-8 mm total slab thickness (not a thin
  3 mm sheet — needs real depth to carve the puck/Dot/rotator pockets
  into without punching through), with a 3-4 mm perimeter/top-bottom skin
  and internal ribs ~3 mm thick on a 20-25 mm grid rather than relying on
  slicer infill percentage alone — this gives predictable, modelable
  stiffness exactly where the rotator's mounting boss and the deck-to-body
  screw perimeter need a solid backing to anchor into, rather than hoping a
  15-20% grid infill happens to land in the right spot. This slab should not
  perceptibly flex under a resting hand or a phone being pressed into the
  rotator cradle.
- **Body walls (Body-L/R):** 2.4-3.2 mm walls (6-8 perimeter loops at a
  0.4 mm nozzle) is standard for furniture-scale FDM rigidity without
  excess weight; 15-20% grid or gyroid infill is fine for the general wall
  body since the actual load path is the deck-perimeter fasteners + plinth
  band + dowels, not the wall infill itself.
- **Brick chamber clear volume:** confirmed at ≥192 x 122 mm floor
  footprint, ≥52 mm clear height at the brick's location (§3) — restated
  here as a structural/thermal note because it's the number that makes the
  electronics plan's "≥10 mm gap on all faces" achievable in the actual
  print, not just on paper.
- **Vent geometry achievability — confirmed printable, no resolution
  concern:** both vent fields (11.2 cm² intake, 22.8 cm² gross / ≥14 cm²
  net exhaust) use 4 mm-wide slots. A 4 mm slot is ~10x a standard 0.4 mm
  nozzle's line width and well within reliable bridging/hole-printing
  range (FDM handles unsupported openings up to roughly 8-10 mm cleanly at
  normal cooling settings) — there is no print-resolution problem here at
  all; I'd only flag a concern if slot width were pushed below ~1.5-2 mm.
  Two practical refinements:
  - Model the slots at 4.3-4.5 mm nominal to compensate for typical
    0.2-0.4 mm FDM hole-narrowing, then verify post-print with a feeler
    gauge or drill bit rather than trusting the nominal CAD number blind.
  - Break each long slot into shorter segments (e.g., eight ~34 mm segments
    with ~1 mm ribs between them for the intake) rather than one continuous
    opening — easier to print cleanly, adds finger-safety, and stiffens the
    plinth's front rail and the deck's underside reveal. This is consistent
    with the "baffle ribs" already implied by the exhaust field's
    gross-vs-net area distinction in the approved spec.

---

## 6. Estimates

**These are order-of-magnitude estimates** for a "typical consumer printer"
at moderate speed (0.4 mm nozzle, 0.2 mm layer height, ~50-60 mm/s
effective) — a high-speed printer (Bambu X1C-class, tuned Klipper, etc.)
will cut times roughly in half; actual numbers depend heavily on printer,
settings, and infill choices above.

| Part (qty) | Approx. filament | Approx. print time (each) |
|---|---|---|
| Body-Left / Body-Right (x2) | ~180-220 g each | ~14-18 hrs each |
| Deck-Left / Deck-Right lids (x2) | ~120-150 g each | ~6-9 hrs each |
| Drawer-front appliques (x2) | ~35-45 g each | ~2-3 hrs each |
| Rear panel halves (x2) | ~50-70 g each | ~3-4 hrs each |
| Bracket-foot appliques (x4) | ~10-15 g each | ~0.75-1 hr each |
| AC snap-covers (x2) | ~5 g each | ~20 min each |
| **Total (primary geometry)** | **~900 g - 1 kg** | **~60-65 hrs total** |

Budget one full 1 kg spool plus a margin for failed prints/waste (~1.2-1.5
kg realistic). Across ~10 separate print jobs this is a multi-day project
(roughly 2-3 overnight prints for the two body halves alone, another 1-2
nights for the deck lids, an afternoon session for the small parts) — normal
for a project this size, not unusual.

**Fallback geometry:** chest halves shrink (~25-30% less material/time for
the chest body), the 6x6x5in pedestal adds a new single-piece print
(~80-100 g, ~5-6 hrs). Net total time/material is roughly a wash versus the
primary geometry, just redistributed into different-shaped parts.

### Hardware BOM (non-printed)

- 2x real brass drawer pulls, matched to credenza hardware (bought)
- ~350 mm real brass strip stock for the gallery rail (e.g., K&S hobby
  brass strip) — or budget alt: printed rail + Rub'n Buff brass wax
- Optional small brass nameplate blank (plinth face)
- Heat-set brass inserts: ~16-20x M3 (deck-to-body perimeter, both sides)
  + 6x M4 (plinth structural joint, 3 per side) + 4-6x M3 (rotator anchor
  boss + rear-panel thumbscrew bosses) — stock a mixed 30-50 pack
- Screws: ~20x M3x10 (deck fasteners), 6x M4x16 SHCS (plinth joint), 2-4x
  M4 thumbscrews (rear-panel quick release — or skip if using printed
  twist-tabs instead)
- Dowel pins: 4x 6 mm (wood or nylon rod, ~30 mm, Body-L/R registration) +
  2-4x 4 mm (Deck-L/R registration) — cut to length from hardware-store stock
- Snap-in cable grommets: ~8-10x, mixed 8/10/12 mm (6 device cable exits +
  2 AC exits + spare-tip pass-throughs as needed)
- 4x self-adhesive felt furniture pads for the underside of the plinth/feet
  — protects the credenza's actual oak finish from direct plastic contact,
  easy to forget, explicitly calling it out
- Plastic cement/2-part epoxy for structural PETG joints; CA or epoxy for
  PLA cosmetic appliques
- Finishing supplies: sandpaper (150/220/400 grit), plastic-appropriate
  primer-filler, gel stain (golden oak) or faux-grain paint kit, oak-look
  adhesive veneer/contact film (recommended, see §4), matte/satin
  polyurethane topcoat
- USB cables for the 3 permanent + 3 captive-spare runs per
  electronics-plan §2.4 (PD-rated C-to-C for C3, QC/AFC-capable A-to-C for
  A1, standard A-to-C/micro for A3)
- Panel-mount USB couplers — only needed if the flush-socket fallback is
  chosen over captive-cable+park-notch for the A spares

---

## Summary of what's provisional vs. final

- **Final now:** part-split plan and joinery (§2), brick-bay clearances
  (§3), puck-seat parametric design (§3), USB cutout/tolerance guidance
  (§3), material/finish plan (§4), wall-thickness/rib guidance (§5), vent
  achievability confirmation (§5), and the time/material estimates (§6) —
  all of this holds regardless of which geometry (primary or fallback) ends
  up used, since the same techniques carry over.
- **Provisional, pending the rotator sweep measurement:** the rotator bay's
  150 x 120 mm / 25 mm-recess cavity, its immediate wall thickness, and the
  exact position of the Deck-Right/Body-Right split line near it. Everything
  else in this document is unaffected by which way that measurement lands.

# Charging Station Enclosure — Design Concepts, Round 2 (Revision)

Author: room-designer agent
Source of truth: `/home/user/GolfAI/CLAUDE.md`
Revises: `design-concepts-round1.md` per `review-round1.md`
Companion doc: `electronics-plan-round1.md` (its §2.1, §3.4, §4, §5 rules are
treated as hard constraints below)
Status: awaiting round-2 review

This is a targeted revision, not a regenerate. Round-1 content stands except
where amended here. The four reviewer fixes are closed per concept:
(1) brass/metal 20 mm puck exclusion, (2) explicit low-intake / high-exhaust
vent fields with area math, (3) the Echo Dot's second AC path, (4) the
rotator sweep check on Concept 2's deck — which **failed at 11 x 7.5 in**,
so Concept 2's footprint has grown (details below). Concept 3 gets the
requested one-line fix only.

---

## Ranking (round 2)

1. **Concept 2 — "Keepsake Chest"** (now 13 x 8 x 7 in). Primary per
   reviewer direction; all four fixes closed with geometry, not assertions.
   *Tradeoff: grew 2 in wider to honestly fit the rotator — still the
   smallest, easiest, most convincing disguise.*
2. **Concept 1 — "Gallery Mantel"** (24 x 7.5 x 4.5 in). Backup, same
   fixes applied. *Tradeoff: boldest transformation, but still gated on
   measuring the canvas and still a multi-segment print.*
3. **Concept 3 — "Conservatory Bench"** — held, one-line fix noted at the
   end, no further round-2 effort per reviewer.

---

## Concept 2 — "Keepsake Chest" (PRIMARY, revised)

**Form (revised).** Upright two-faux-drawer chest, now **13 in W x 8 in D x
7 in H** (330 x 203 x 178 mm). Everything else from round 1 stands: raised-
panel faux drawer fronts with two real ornate brass pulls matched to the
credenza, overhanging rounded-edge top, bracket-foot plinth base, lift-off
rear panel for service. The 2 in of added width and 0.5 in of depth exist
solely to make the rotator fit honestly (Fix 4); at 13 in wide it still sits
comfortably beside the canvas and still reads as a jewelry chest, and the
mirrored-twin expansion story is unchanged.

### Fix 4 — rotator sweep check (the reason the footprint grew)

Working envelope assumption (flagged; final numbers come from electronics
plan §7.3's measurement): rotator base ~120 mm dia; with a large phone
mounted, the rocking arm sweeps a volume ≈ **200 mm wide x 100 mm deep x
190 mm tall** above the pivot.

On the round-1 deck (280 x 190 mm), that envelope could not coexist with a
110 mm Echo Dot nest and a 150 x 75 mm puck tray without overlaps —
**confirmed too tight; round-1 deck rejected, not hand-waved.**

Revised deck zone map (330 x 203 mm), all zones non-overlapping with ≥20 mm
buffers:

| Zone | Location | Footprint | Notes |
|---|---|---|---|
| Watch-puck valet tray | front-left | 150 x 75 mm | two puck seats, centers 70 mm apart, tray front edge set 20 mm back from deck edge |
| Spare-tip park notches | front-right | 90 x 60 mm | 3 labeled holsters (SPARE C — FAST 20W / SPARE A — FAST / SPARE A — SLOW) |
| Echo Dot nest | rear-left | 110 mm dia | Dot ~40% proud, open top and sides above deck line |
| Rotator bay | rear-right | 150 x 120 mm floor; base recessed 25 mm | sunken base lowers the sweep peak; 200 mm sweep width fits between the Dot buffer and the right deck edge (top of arc may briefly overhang the right edge into open air — acceptable) |

Fallback (documented as real geometry, per reviewer): if the measured sweep
exceeds the assumed envelope, the rotator moves to a **matching quarter-
round side pedestal**, 6 x 6 x 5 in, same finish system, butted to the
chest's right face with its cable entering the chest through a grommeted
side port — and the chest reverts to 11 in wide. This is a drawn fallback,
not a footnote; but the 13 in single-body version is the primary.

### Fix 1 — brass exclusion at the puck wells

The round-1 brass gallery rail around the valet tray is **deleted**. Revised
treatment:

- Immediate puck surrounds (everything within 40 mm of each coil center —
  double the required 20 mm for margin): **printed plastic only**, finished
  in a dark espresso/oxblood *non-metallic* stain to read as a leather valet
  liner. No brass, no screws, no Rub 'n Buff, no metallic paint in this
  zone — Rub 'n Buff is metal-flake wax and counts as metal per §2.1.
- HIS WATCH / HER WATCH embossed in the tray floor forward of each seat,
  inside the plastic-only zone (embossing is printed, so it's fine).
- Brass relocates to where it can't interfere: the two real drawer pulls
  (unchanged, still doing 80% of the disguise), a **brass gallery rail along
  the front deck edge only** — with the tray set 20 mm back and coil centers
  57 mm behind the deck edge, the rail sits ≥50 mm from either coil — and an
  optional small brass nameplate on the plinth face.
- Fastener rule passed to printing-expert: no metal screws or heat-set
  inserts in the deck within 40 mm of either coil center; that region snaps
  or glues.

### Fix 2 — vent fields (explicit low intake + high exhaust, opposite sides)

Two separated fields creating a diagonal front-low → rear/side-high path
across the brick, which sits on standoff ribs mid-chamber with ≥10 mm gap
all faces per electronics plan §3.1/§4:

- **Low intake — front toe-kick slot.** The bracket-foot plinth raises the
  body ~19 mm. A continuous slot is cut into the recessed underside face
  behind the front plinth reveal: **280 x 4 mm ≈ 11.2 cm²**, plus the open
  gaps between bracket feet as bonus area. Invisible at any normal viewing
  angle — you'd have to put your cheek on the credenza to see it.
- **High exhaust — shadow-gap reveal under the top overhang.** The top
  overhangs the body ~12 mm on the sides and rear. A continuous 4 mm reveal
  slot runs under the overhang along the **rear (330 mm) plus the rear
  120 mm of each side**: (330 + 240) x 4 mm ≈ **22.8 cm²** gross; ≥14 cm²
  net after internal baffle ribs. Reads as an intentional shadow line —
  traditional casework has these.
- Fields are on opposite sides of the brick chamber (front-low vs.
  rear/side-high), so this is a true cross-flow, not the round-1 single-wall
  rear slat panel. The rear slatted service panel remains but is now the
  removable access door, not the load-bearing vent.
- **Rear-wall robustness (reviewer Issue #3):** because 240 mm of the
  exhaust reveal is on the *sides*, the design still meets the 10 cm²
  exhaust floor even if the credenza is pushed flush to the wall.
  **Assumption flagged:** we still assume ≥25 mm behind the credenza for
  the two AC cords to drop to the outlet — user to confirm; if it's truly
  zero, cords route sideways along the credenza back edge instead, with no
  change to the shell.

### Fix 3 — Echo Dot's second AC path

- The Dot's wall wart plugs into the wall outlet (or existing strip)
  **behind the credenza, outside the shell** — never inside, per
  electronics plan §3.4.2.
- Its thin barrel cord enters the chest through a dedicated 8 mm grommet
  low on the **rear-left** of the rear panel, rises inside a printed
  **corner chase** (a vertical quarter-round conduit in the rear-left
  corner, fully walled off from the brick chamber and the USB cable bay),
  and emerges through the floor of the Dot nest. Zero visible cord.
- The brick's own coiled AC cord exits through its keyhole/snap-cover
  channel low on the **rear-right** (coil stored behind the shell, not in
  the warm chamber, per §3.4.1). Two AC paths, two separate openings,
  left/right of the removable rear panel — they can be dressed to the
  outlet as one tidy pair behind the credenza but never share an opening
  or a channel with each other or with USB runs.

**Materials/finish, footprint, expansion:** as round 1 (wood-fill PLA +
golden-oak gel stain + matte poly, or the faux-grain paint alternate; real
brass pulls), except the brass-rail relocation above. New footprint
13 x 8 in, 7 in tall — still below the canvas's lower third.

---

## Concept 1 — "Gallery Mantel" (BACKUP, same fixes applied)

Form, placement, materials, and expansion story stand from round 1
(24 x 7.5 x 4.5 in canvas plinth). Amendments only:

- **Fix 1 (brass at pucks):** the brass-ringed puck collars are **deleted**.
  Puck wells get plain printed collars in the espresso non-metallic finish;
  HIS/HERS embossed. Brass relocates to the two front-panel rosettes/knobs
  and the swappable-port grommets on the front-right deck edge, all ≥100 mm
  from the coils. Same no-metal-fasteners-within-40 mm rule for the deck
  around the wells.
- **Fix 2 (vent fields):** the round-1 single rear "dentil vent band" is
  split into two proper fields:
  - **Low intake:** continuous 4 mm shadow-gap reveal above the ogee base
    molding across the **front** face, 500 mm long ≈ **20 cm²** — reads as
    the natural joint line between base molding and case.
  - **High exhaust:** the dentil frieze moves to the top of the **rear**
    face plus the rear third of each side, directly under the crown lip:
    tooth gaps 6 x 15 mm, 20+ gaps ≈ **18 cm²**. At 6 mm the gaps stay in
    scale with a 4.5 in-tall piece — the dentil disguise survives the area
    requirement because the band now only has to carry exhaust, not both
    fields. Side-face teeth keep exhaust honest if the credenza sits flush
    to the wall (Issue #3), same as Concept 2's side reveals.
  - Diagonal path: front-low in, across the standoff-mounted brick,
    rear/side-high out. The solid top deck over the brick is explicitly
    compensated by the high rear/side exhaust ("chimney out the back"),
    satisfying §4.4.
- **Fix 3 (Dot's AC path):** the Dot turret is the right-end bookend post;
  its barrel cord enters via a dedicated 8 mm grommet low on the rear face
  directly behind the turret and rises inside the turret's hollow rear wall
  to the nest floor — walled off from the brick belly. Brick AC cord exits
  low rear-center as before; separate openings, never shared.
- Still gated on: measuring the canvas width/height before any geometry
  (unchanged self-flag), and the multi-segment print (printing-expert
  scope).

---

## Concept 3 — "Conservatory Bench" — held (one-line fix only, per reviewer)

The round-1 contradiction resolves to a single mitigation: the cachepot
socket is a **one-piece sealed printed cup draining into an integrated
shallow saucer basin (~100 ml reserve) printed into the pedestal base, with
overflow routed to that basin only — never onto the credenza and never
toward vents or cable openings**; the "or a nursery saucer" alternative is
withdrawn. No other round-2 work done here.

---

## Open items for other agents (round 2)

- **electronics-expert:** the reviewer's question about single-wall low+high
  venting is now moot for both live concepts — both use true opposite-side
  fields — but please sanity-check the two area calcs above against §4, and
  confirm the assumed rotator sweep envelope (200 x 100 x 190 mm) once the
  physical unit is measured (§7.3). Also confirm the 40 mm metal-free radius
  I adopted is comfortably conservative vs. your 20 mm floor.
- **project-reviewer:** decision needed on Concept 2's 13-in width vs. the
  drawn pedestal fallback, and please have someone measure (a) behind-
  credenza clearance and (b) the canvas, which still gates Concept 1.
- **printing-expert:** note the no-metal-fastener zone around the puck
  seats and the snap-cover AC keyhole channel — both affect part splits.

# Dining Room Charging Station — Project Brief

This file is the shared brief for a 3D-printed charging station build. It is
used by a small team of specialized subagents (see `.claude/agents/`) who
should read this file before doing any design or engineering work. Treat this
as the source of truth for constraints, inventory, and goals — don't invent
requirements that aren't here without flagging them as assumptions.

Reference photos of the actual credenza and hardware are in this session's
upload folder (three JPGs of the credenza top, the cable mess, and the phone
rotator device). Ask the user for these paths if a subagent needs to look at
them again.

## The problem

We have a wooden credenza (oak, brass drawer pulls) in the dining room. On top
of it sits a 100W USB charging brick with a nest of cables running to various
electronics. It looks messy and it's a visible part of the dining room, so
it has to look good, not just work. The mess also causes a behavioral
problem: people just grab whatever cable is closest to charge whatever they're
holding, so the "this always charges here" items get unplugged and wander off,
and the charger for the item that *actually* needed to charge overnight is now
missing.

## Goal

Design and 3D print an enclosure/organizer ("charging station shell") that:

1. Fully hides the charging brick and all loose cabling inside a printed
   shell — nothing but connectors and devices should be visible on the
   outside.
2. Gives every device a **fixed, labeled** spot. Some connections should be
   effectively permanent (cable exits the shell pre-routed to a fixed device
   cradle/slot and is not meant to be unplugged); others can be swappable but
   should still be clearly labeled for what they're for.
3. Looks like it belongs in the dining room — good enough to be a piece of
   decor in its own right, not just a tolerated appliance. Ideas that
   double the piece as something else (e.g., a planter stand, a base for the
   family photo canvas that already sits there, a sculptural object) are
   very much wanted. "Disguise it as furniture/decor" is the aesthetic goal.
4. Is designed as a first unit that could later be paired with a second,
   matching unit if we outgrow the capacity (see Expansion below). Don't
   over-engineer modularity now — just don't design something that can't be
   flanked or stacked later.

## The room

- Dining room credenza: medium-toned oak wood, ornate brass drawer pulls,
  traditional style (not modern/minimalist). See photos.
- A large canvas family photo currently leans/stands on top of the credenza,
  behind the clutter. The charging station should coexist with it (either
  sit beside it, or the design could incorporate/frame it).
- There are also potted plants on the credenza (a peace-lily-type plant and a
  philodendron/pothos in a pot) and a woven basket. Materials/colors that
  read as "warm wood + brass + greenery" will fit the room; stark
  white/glossy plastic will not — plan for a finish/paint/stain approach if
  the printed material doesn't match on its own.

## Devices that need a home

### 1. Charging brick (the core, must be fully enclosed) — CONFIRMED main unit
- **Brand/model: Gakezi 100W 6-Port GaN Fast Charging Brick** ("Hub Cube
  Box"), PD 3.0. Product page:
  https://www.amazon.com/dp/B0D815Z5SL
- Ports, per the manufacturer's spec sheet (labeled USB-A1/A2/A3 and
  USB-C1/C2/C3 top-to-bottom on the unit):
  - USB-C x3, each **PD 3.0, 20W** (12V/1.67A, 9V/2.22A, or 5V/3A)
  - USB-A x3, generic marketing spec sheet lists all three at 15W
    (5V/3A) with no distinction — **but the user has the physical unit
    in hand and reports the first USB-A port is visually marked
    differently (distinct port color) and labeled as faster than USB-A2/
    A3.** Trust the physical unit over the generic product-listing
    graphic: **treat USB-A1 as a genuinely faster/distinct port** (likely
    QC/AFC-capable at a higher voltage than the plain 5V/3A on A2/A3),
    pending exact confirmation of its rated spec. The electronics-expert
    agent should note this discrepancy and, if useful, ask the user to
    read the exact wattage/spec printed next to that port, but should not
    default back to "all three are identical" — that's now known wrong for
    this unit. USB-A1 is the natural candidate for a swappable slot that
    benefits from faster charging (e.g., a phone), given its distinct
    port marking.
  - Only smartphones/tablets negotiate fast charging at all; a fast-charge
    *cable* is required on the USB-C ports to get the rated 20W.
- **Confirmed physical dimensions** (manufacturer spec): **6.77 in (L) x
  4.01 in (W) x 1.41 in (H)**, weighs 0.54 lb. This is now locked in for
  enclosure geometry — no more guessing needed. (Still worth a quick
  hand-measurement to confirm before final print, since printed tolerances
  matter more than a spec sheet's rounding, but this is no longer a
  blocking unknown.)
- **Has an integrated AC power cord** (coiled cord to a standard 2-prong
  plug) — this is *not* a direct plug-into-the-wall wart. That means the
  brick body itself can sit anywhere inside the enclosure; only its power
  cord needs a routed exit path to a wall outlet, separate from the 6
  charging-cable exit points. The enclosure design must account for this
  extra cord run/exit, not just the 6 device cables.
- Ventilation/heat: a GaN brick like this gets warm under load with 6 devices
  charging at once — the enclosure must include real airflow (vents/slots),
  not just a sealed decorative box.

#### Optional supplemental charger — CONFIRMED, but deferred/optional

The user also owns a 2-pack of supplemental chargers that *could* be added
alongside the Gakezi brick, but is not required for v1:

- **Caniifoto 2-Pack USB-C Fast Charger Block**, 60W per unit, 5 ports each
  (2x USB-C PD 30W + 3x USB-A 3.1A). Product page:
  https://www.amazon.com/dp/B0DKXR4TYR
- Form factor: compact wall-plug cube with folding AC prongs, **no cord** —
  it plugs directly into an outlet or a power strip, unlike the corded main
  brick. That makes it harder to bury deep inside the enclosure unless it's
  fed by an internal power strip; if used, plan its bay near the enclosure's
  power-strip/cord-exit area rather than in the interior.
- Two identical units in the pack — either or both could be pressed into
  service.
- Status: the Gakezi brick's 6 ports are enough to cover all of v1's
  dedicated needs (2 watch pucks + phone rotator = 3 dedicated ports,
  leaving 3 free for swappable use) — see Port allocation logic below. Treat the Caniifoto units as **optional
  headroom**, not a v1 requirement: use one only if the electronics-expert
  agent's port math says 3 spare ports isn't enough swappable capacity, or
  reserve both, unused, as the literal hardware for the "Expansion" section's
  future second unit. Don't design a bay for them into v1 unless a real need
  shows up in the port-allocation pass.

### 2. Amazon Echo Dot (round smart speaker)
- Currently just sits loose on the credenza, plugged into its own wall wart
  (not the USB brick).
- Must stay **functionally usable in place**: its microphone array (top
  surface) needs to be able to hear normal room speech, and its speaker
  (side vents) needs to be able to project sound. This effectively means it
  can be recessed or nested into the design, but not fully enclosed/muffled
  — needs an open top and open side venting, or an acoustically transparent
  cutout/grille.
- Does not need to be removable — this is a "never removed" device.

### 3. Two Samsung Galaxy Watches (his and hers)
- Each watch normally sits on its own small magnetic/pogo-pin charging
  puck/cradle (visible in photos as small black charging dock pucks fed by
  a USB-C cable) — the watches do **not** charge via a plain USB tip
  directly, the puck is the connector.
- These charge nightly, so they should have a **dedicated, permanent
  home for each puck**, positioned so the watch can be set down flat and
  correctly seated on the puck without fiddling (correct puck-to-watch
  alignment matters for Qi/pogo charging).
- This is the flagship "nice to have" feature: a proper two-watch charging
  dock/shelf built into the design (his + hers side by side or stacked),
  not just two USB-C cables poking out of a hole.

### 4. Phone rotator / "Pokémon egg hatcher" cradle
- A motorized cradle that holds a phone and slowly rocks/rotates it back and
  forth to simulate walking distance (used for hatching eggs in Pokémon Go).
  It plugs in via USB for power and needs to keep moving while docked.
- This device needs its phone cradle to remain **exposed and reachable**
  (a phone gets placed in/removed from it regularly), but its power cable
  and body can be nested into the shell so only the cradle/phone-holder arm
  is visible, tidily emerging from the housing.
- This is a "not removed, but actively used daily" item — the base stays
  fixed permanently in the shell, the phone itself is the only thing that
  comes and goes.

### 5. Everything else (loose watch bands, misc cables, coasters, etc.)
- Not in scope for dedicated charging slots, but the finished piece should
  have zero loose cable clutter visible — anything not itself a charging
  target should be able to be tidied elsewhere, not accounted for in the
  charger enclosure.

## Port allocation logic (for the Electronics/Charging agent to firm up)

- 6 total outputs on the confirmed Gakezi brick: **USB-C1/C2/C3 (PD 20W
  each)** + **USB-A1 (distinct/faster port, per physical inspection —
  exact spec TBD), USB-A2, USB-A3 (plain 5V/3A)**.
- Some devices only need charging every other day (occasional) — these are
  candidates for a shared/swappable labeled port rather than a dedicated
  permanent one.
- Some devices need every-night charging or are "never unplug this" — these
  get dedicated, permanently-wired, clearly labeled ports/cradles.
- Two Galaxy Watch charging pucks will each permanently occupy one port
  (likely USB-C, confirm puck cable connector type).
- Phone rotator cradle needs one permanently wired port.
- That's 3 of the 6 ports spoken for, leaving 3 free as labeled swappable
  general-purpose slots for phones/misc devices that don't charge nightly —
  3 dedicated + 3 swappable comfortably fits within the one confirmed brick;
  the optional Caniifoto supplemental chargers above are not needed to make
  the numbers work for v1.
- Echo Dot keeps its own wall wart and does **not** need a brick port —
  it just needs physical space/venting in the design.
- Don't forget the brick's own AC power cord needs a routed exit to a wall
  outlet, separate from and in addition to the 6 device-cable exits.
- Final assignment of which physical port goes to which permanent device
  (and why) is a deliverable from the Electronics agent, not decided here.

## Labeling

Every output — permanent or swappable — should be clearly labeled in the
final physical piece (e.g., engraved/embossed text or a nameplate approach
that's part of the print, not a sticker) so anyone in the household knows
what belongs where and which ports are "off limits" for grabbing a random
cable.

## Expansion (future, not this round)

If total charging demand grows beyond this one brick, we may want to place a
second matching unit alongside this one later. Keep the design language
(materials, shape, module footprint) generic enough that a second, matching
unit could sit next to or stack with the first without looking mismatched.
Do not build a dual-brick enclosure now — design v1 for exactly one 100W
6-port brick plus the four devices above.

## Deliverables expected from this project

1. 2-3 concrete design concepts (room-appropriate aesthetic direction,
   including at least one "disguised as decor" idea, e.g. integrating a
   planter, sculptural form, or picture-frame/canvas base).
2. A feasibility/electronics pass on whichever concept(s) survive review:
   port assignment, cable routing, ventilation, and cutouts for the Echo Dot,
   the two watch pucks, and the phone rotator.
3. A buildability pass from the 3D printing expert: printable geometry
   (overhangs, supports, bed size, split into multi-part prints if needed),
   material/finish recommendation that can look like it belongs with oak +
   brass, and estimated print time/material cost.
4. Final output from the build agent: an actual 3D-printable model
   (parametric OpenSCAD source preferred, exported to STL) checked into this
   repo under `charging-station/`, plus a short build doc (print settings,
   assembly steps, BOM for pucks/cables/fasteners/paint).

## Team workflow

See `.claude/agents/`:

1. **room-designer** (model: fable) — generates room-appropriate aesthetic
   concepts and the "disguise it as decor" ideas.
2. **electronics-expert** (model: fable) — works out port assignment, wiring,
   connector types (USB-A/USB-C, watch puck connectors), ventilation and
   safety for whatever concept(s) the room designer proposes.
3. **project-reviewer** — looks at what the above two produce, checks it
   against this brief, and makes the call on which concept(s) are worth
   pursuing (or sends them back with specific gaps to fix).
4. **printing-expert** — takes the reviewed concept and turns it into
   printable geometry: tolerances, supports, split parts, material/finish.
5. **builder** (model: sonnet) — implements the final approved design as
   actual files (OpenSCAD/STL, docs) committed to this repo.

Typical flow: room-designer + electronics-expert work in parallel on the same
brief → project-reviewer evaluates and picks/refines a direction →
printing-expert validates manufacturability → builder produces the final
checked-in deliverable.

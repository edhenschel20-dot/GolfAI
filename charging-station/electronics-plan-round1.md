# Electronics & Port-Allocation Plan — Round 1

**Project:** Dining Room Charging Station (see `/home/user/GolfAI/CLAUDE.md`)
**Author:** electronics-expert agent
**Status:** Round 1 — generic plan, written before any enclosure concept is
locked. Everything here applies to any reasonable enclosure shape; sections
that depend on the room-designer's form are flagged as **FORM-DEPENDENT**.

---

## 1. Port assignment (final recommendation)

Gakezi 100W 6-port GaN brick, ports labeled top-to-bottom on the unit:
USB-A1 / A2 / A3, USB-C1 / C2 / C3.

| Brick port | Spec | Assignment | Type | Why this port |
|---|---|---|---|---|
| **USB-C1** (PD 20W) | 5V/3A, 9V/2.22A, 12V/1.67A | **His Galaxy Watch puck** | Permanent, hard-routed | Puck cable is USB-C terminated (verify — see §2.1). Watch draw is tiny (≤5W), so it wastes no meaningful capacity to park it on a PD port; the C ports are simply the only ports its plug fits. C1/C2 chosen adjacent so both watch cables leave the brick side-by-side into one channel. |
| **USB-C2** (PD 20W) | same | **Her Galaxy Watch puck** | Permanent, hard-routed | Same reasoning; pairing the two watch runs keeps internal routing symmetric and makes the his/hers dock a single cable bundle. |
| **USB-C3** (PD 20W) | same | **Spare — USB-C fast charge** | Swappable, labeled | The 20W PD ports are the fastest outputs on this brick. The best spare is the one a modern phone/tablet/earbud case actually negotiates with. Must be fitted with a PD-capable (fast-charge) C-to-C cable or the 20W never happens (brief calls this out). |
| **USB-A1** (distinct/faster port — exact spec TBD) | likely QC/AFC, >5V capable | **Spare — USB-A fast charge** | Swappable, labeled | Per the brief: physical unit shows A1 marked/colored as faster than A2/A3. A fast A port only pays off on a device that negotiates QC/AFC — i.e. a phone. No permanent device benefits (watches and rotator are ~5W loads), so the fast A port would be squandered on them. It goes to the swappable pool as the "grab this one for a Samsung phone" slot. **Open item:** user should read the wattage/voltage text printed next to A1 on the unit so the label and expectations match reality (§7). |
| **USB-A2** (5V/3A) | plain 15W | **Phone rotator / egg-hatcher cradle** | Permanent, hard-routed | The rotator is a small 5V motor + phone-holding cradle; it draws a couple of watts and negotiates nothing. A plain 5V/3A port is exactly right, and burning a plain port on it preserves both fast ports (A1, C3) for the swappable pool. A2 over A3 only for tidy top-to-bottom ordering next to A1. |
| **USB-A3** (5V/3A) | plain 15W | **Spare — USB-A basic 5V** | Swappable, labeled | Third spare, for earbuds, battery packs, book lights, anything that just wants 5V. Explicitly the "slow" spare so nobody is surprised. |

**Summary:** 3 permanent (C1, C2, A2) + 3 swappable (C3, A1, A3) — matches
the brief's 3+3 math exactly. **The optional Caniifoto supplemental chargers
are NOT needed for v1.** Do not design a bay for them; hold both as future
Expansion hardware per the brief.

**Echo Dot:** deliberately **not** on the brick. It keeps its own wall wart
(proprietary barrel connector — a brick USB port cannot power it anyway).
It costs the enclosure a *second AC path* to the wall, not a USB port (§3.4).

### Power-budget sanity check

Realistic worst nightly case: 2 watch pucks (~5W ea) + rotator (~3W) + one
phone on C3 at 20W + one phone on A1 at ~15-18W + misc on A3 at ~10W ≈ 60W —
comfortably inside the 100W envelope. Even the theoretical max (3×20W C +
~45W across A) is at/near 100W, which the brick will handle by derating —
an availability note, not a safety issue. No load-shedding rules needed.

---

## 2. Connector reality check

### 2.1 Galaxy Watch pucks — the puck IS the connector

- The watches do **not** plug into USB at all. Each charges on a magnetic /
  wireless charging puck with a **captive** (hardwired, non-detachable)
  cable, typically ~0.9-1.5 m, terminating in USB-C on current Samsung pucks
  (**VERIFY:** older Galaxy Watch pucks are USB-A terminated. If either puck
  turns out to be USB-A, swap that watch to A2 and move the rotator to a C
  port with an A-to-C-capable cable — the rotator doesn't care. The port
  labels in §6 stay with the *device*, not the silicon.)
- Enclosure requirement (**FORM-DEPENDENT** but mandatory in any form): each
  puck needs a **printed recess/seat** sized to the puck body (typical puck
  ≈ 33-38 mm dia × 9-11 mm tall — hand-measure before final CAD), with:
  - a snap-fit or slight friction fit so the puck can't rotate or pop out
    when a watch is lifted off it (the magnets are strong enough to lift a
    loose puck),
  - puck top surface **flush or 0.5-1 mm proud** of the surrounding shelf so
    the watch back seats fully on the magnets — do not recess the charging
    face below surrounding plastic,
  - a cable channel exiting the underside of the seat,
  - **no metal** (brass inserts, screws, magnets, foil paint) within ~20 mm
    of the puck coil — eddy heating and alignment interference,
  - open plastic only above/around the coil face; never a printed lid over
    a docked watch (inductive charging makes real warmth).
- The two seats must sit side by side or clearly mirrored ("his"/"hers"),
  reachable for a one-handed set-down in the dark. Angle 0-15° from
  horizontal is fine; steeper needs a retaining lip and is not recommended
  for magnet-only pucks.

### 2.2 Phone rotator cradle

- Powered via USB; **VERIFY** both ends: device-side jack (likely micro-USB
  or USB-C on the base) and brick-side plug (likely USB-A — assignment to
  A2 assumes this).
- The moving cradle arm needs a **swing/rock clearance envelope** — measure
  the full sweep with a large phone mounted before fixing the cutout. The
  base gets buried in the shell; only the cradle emerges. The base must be
  anchored (screw boss, strap, or printed pocket) because the rocking motion
  will walk an unanchored base into the shell walls (noise + wear).
- Its power lead is permanent: strain-relieved at the base entry and at the
  brick end so daily phone insertion force never tugs the connector.

### 2.3 Echo Dot

- Proprietary barrel-jack wall adapter, **not** USB. Needs: open top
  (mic array), acoustically open sides (speaker), and its adapter needs an
  AC route (§3.4). Nothing else from the electronics side.

### 2.4 Swappable ports — do not expose the brick's own port face

Recommended pattern for the 3 spares: **captive short cables with parked
tips**, not panel-mount female couplers.

- Permanently plug a quality ~0.5 m cable into each spare brick port (C3:
  PD-rated C-to-C; A1: QC/AFC-capable A-to-C; A3: A-to-C or A-to-micro per
  household need), route it through a grommeted exit, and give the free tip
  a **labeled printed holster/park notch** on the outside. Users grab the
  tip, charge, and re-park it. The brick is never touched or unplugged.
- Rationale: female USB-C *extension* couplers are technically out of USB-C
  spec and are a known source of flaky PD negotiation and (rarely) melted
  cheap couplers; captive cables avoid the whole class of problem, and also
  physically enforce the labeling scheme (each tip lives at its label).
- If the room-designer's form strongly wants flush sockets instead, use
  panel-mount extensions on the two **A** ports only, and keep C3 as a
  captive cable.

---

## 3. Cable routing (generic rules for any enclosure form)

### 3.1 Brick placement & orientation

- Brick (6.77 × 4.01 × 1.41 in ≈ 172 × 102 × 36 mm) sits on **printed
  standoff ribs**, ≥ 6 mm off the enclosure floor, with **≥ 10 mm air gap on
  all faces** — never face-flat against printed plastic (§4).
- Orient the **port face toward a single internal cable bay** so all 6 USB
  runs start in one place; AC cord leaves the opposite/rear end of the brick
  toward the wall-side exit. USB and AC paths should never share a channel.

### 3.2 Permanent runs (C1, C2 → watch pucks; A2 → rotator)

- Shortest sensible path; excess captive-cable length gets a **figure-8 in a
  dedicated slack shelf** on the *cool* side of the bay — never coiled
  tightly against the brick body.
- **Fixed in place:** zip-tie each cable to printed anchor posts (a) ~30-50
  mm after it leaves the brick port and (b) just inside its exit point, so
  neither end ever sees tension. Glue (if any) goes cable-jacket-to-plastic
  only — **never onto the brick housing** (heat trap + warranty + blocks
  future brick swap).
- Internal label at the brick end of each permanent cable too (small printed
  tag or flag: "C1 HIS", "C2 HERS", "A2 ROTATOR") so reassembly after a
  brick swap is idiot-proof.

### 3.3 Swappable runs (C3, A1, A3)

- Captive cables per §2.4; strain-relieved at the brick end and at the
  grommet, with ~15-20 cm of external working length to the park notch.
  These are the only cables with intentional external slack.

### 3.4 AC exits — there are TWO

1. **Brick's own coiled AC cord** (integrated, 2-prong plug): exits low at
   the rear/wall side through its own opening. The molded plug head needs
   roughly a **30 × 20 mm** opening *or* a split/keyhole channel closed by a
   snap cover so the cord can be laid in during assembly instead of threaded.
   Do **not** stow the coiled portion wrapped tight inside the hot chamber —
   let the coil live outside/behind the shell or in a cool rear pocket.
2. **Echo Dot wall wart + barrel cord**: the wart plugs into the wall outlet
   (or an external strip) *outside* the shell; only the thin DC barrel cord
   routes into the Dot's nest through its own grommet. Do not design the
   wart into the interior for v1.

### 3.5 General routing hygiene

- Every pass-through gets a chamfered/grommeted edge; minimum bend radius
  ≥ 4× cable diameter; no cable crosses a part-line where two printed shells
  screw together (pinch risk) unless a relief channel is printed in.

---

## 4. Heat & ventilation (hard requirements)

- Heat source math: GaN brick ≈ 92-94% efficient. Full 100W load ≈ **7-10 W
  continuous heat** inside the shell; realistic overnight load (2 watches +
  rotator + 1 phone) ≈ 3-5 W. Small numbers, but in a sealed printed box
  they accumulate fast; the brick's own case can reach 50-60 °C under
  sustained load even in open air.
- **Passive chimney convection is sufficient — active cooling is NOT needed
  — if and only if all of the following are met:**
  1. **Low intake vents** near the enclosure base on one side of the brick
     chamber and **high exhaust vents** above the brick on the other side,
     creating a diagonal flow path across the brick.
  2. **≥ 10 cm² of open intake area and ≥ 10 cm² of exhaust area** (e.g.
     eight 50 × 2.5 mm slots each end). Decorative patterns (brass-look
     grille, reeded slots) are fine as long as net open area is met.
  3. Brick on standoff ribs with ≥ 10 mm clearance all faces (§3.1) so air
     actually washes the case.
  4. Exhaust vents are **not capped by a solid decorative top** — if the
     form puts a planter, canvas base, or shelf directly above the brick,
     exhaust must move to high side/rear slots ("chimney out the back").
- **FORM-DEPENDENT vetoes:** a fully sealed sculptural form is rejected as
  proposed — the minimal change is always the two-vent-field chimney above.
  A planter directly over the brick chamber additionally requires a sealed
  waterproof liner with overflow routed *away* from vents (§5).
- **Material note for the printing-expert:** PLA softens ~55-60 °C — the
  brick chamber walls/ribs should be **PETG/ASA** (or PLA accepted only with
  the full 10 mm gap + verified airflow). Decorative outer skin can be
  anything.
- **Acceptance test:** load all 6 ports to realistic max for 60 min inside
  the finished shell; brick case should stay below ~60 °C and vent exhaust
  noticeably warm-not-hot. IR thermometer or careful touch test.

---

## 5. Electrical safety flags

1. **AC cord pinch:** the brick's cord must never be trapped under a shell
   edge or across a screwed part-line; dedicated relieved channel only.
2. **No sealed brick, ever** — restated because decor-first concepts will be
   tempted. Vent area in §4 is a floor, not a suggestion.
3. **Nothing adhered to the brick body**; mechanical cradling (ribs/straps
   around it) only. Keeps its case free to shed heat and keeps it swappable.
4. **Water + plants:** the credenza has live plants and the brief invites
   planter-integrated designs. Any planter element gets a one-piece sealed
   liner, watering overflow path routed away from all vents and cable
   openings, and vents never facing straight up beneath it.
5. **Qi/puck metal exclusion zone:** no metal hardware or metallic paint
   within ~20 mm of the watch-puck coils (§2.1).
6. **USB-C shell clearance at spare ports:** a C plug overmold is ~12-13 mm
   wide × ~6.5 mm tall; park notches and any recessed socket need ≥ 20 mm of
   finger clearance around the tip so people don't yank cables by the cord.
7. **Coiled-cord heat:** never store the AC coil compressed in the warm
   chamber; coiled cords under load warm up when bundled.
8. **Strain relief everywhere a human interacts:** rotator cradle (daily
   phone handling) and the three spare tips are the high-cycle points; both
   ends of those runs are anchored per §3.

---

## 6. Label text (final wording for emboss/engrave)

Short, all-caps, device-owned wording (labels follow the device even if the
underlying brick port changes per §2.1's verify step). Recommended ≥ 5 mm cap
height for embossed legibility.

| Location | Label text |
|---|---|
| His watch puck seat | **HIS WATCH** |
| Her watch puck seat | **HER WATCH** |
| Rotator cradle base | **EGG HATCHER — DO NOT UNPLUG** |
| Spare tip park #1 (USB-C3) | **SPARE C — FAST 20W** |
| Spare tip park #2 (USB-A1) | **SPARE A — FAST** *(finalize wattage after user reads A1's printed spec, e.g. "SPARE A — FAST 18W")* |
| Spare tip park #3 (USB-A3) | **SPARE A — SLOW** |
| Echo Dot nest (optional, small) | **ECHO** |
| Internal, at brick (tags) | **C1 HIS / C2 HERS / A2 ROTATOR / C3 SPARE / A1 SPARE / A3 SPARE** |

Optional single house-rule plate near the spares:
**"SPARES ONLY — EVERYTHING ELSE STAYS PUT."**

---

## 7. Open items to resolve before final CAD

1. **Read the printed spec next to USB-A1** on the physical brick (user
   action) — finalizes A1's label wattage and confirms QC/AFC assumption.
2. **Confirm both watch pucks are USB-C terminated** (vs. older USB-A pucks)
   and hand-measure puck diameter/height and captive cable length.
3. **Confirm rotator connectors** (device-side jack type, brick-side plug)
   and measure its cradle swing envelope with the largest household phone.
4. Hand-measure the brick (spec says 172 × 102 × 36 mm) before final print.
5. Room-designer form check: where do the two AC paths (brick cord, Echo
   wart cord) physically reach the wall outlet from the chosen position on
   the credenza?

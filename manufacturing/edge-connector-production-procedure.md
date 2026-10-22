# Precision edge-connector production procedure

Use this procedure for any board which is inserted directly into an Intellivision
cartridge socket. It is intended for this connector board and for related work
such as an Intellicart-style cartridge. It is a release gate: do not declare a
board production-ready merely because its Gerbers load in a board-house viewer.

The procedure distinguishes three things which are easy to conflate:

1. **Electrical pinout:** every contact reaches the intended net.
2. **Mechanical interface:** the board, fingers, bevel, and plating fit and
   survive the mating connector.
3. **Manufacturing data:** the Gerbers and order options tell the fabricator to
   make that interface, rather than an ordinary PCB with exposed copper.

## Scope and reference interface

The original Intellivision cartridge port is a 44-contact (2 x 22) edge-card
interface on a 2.54 mm / 0.100 in pitch. The Intellivoice has a corresponding
44-contact cartridge socket. For the canonical signal names and orientation,
use the repository's [cartridge-port reference](../documentation/intellivision-cartridge-port-reference.md)
and [pinout safety guide](../documentation/pinout-safety-guide.md), not a
reversed rendering or a photograph.

Do not assume that an Intellicart enclosure, a reproduction shell, or another
card-edge design has the same tongue length or relief geometry. Re-establish
the target connector's physical envelope from its drawing or a measured known-
good card before copying an outline.

## Release gate 1: source-layout audit

Perform these checks in the PCB editor and record the measured values.

| Check | Required result |
| --- | --- |
| Pin identity | Every J1 finger `n` connects only to intended circuit net `n`; for a passive adapter, J1 `n` to J2 `n`. |
| Side/orientation | Compare source coordinates, board front/rear renderings, and the canonical Intellivision table. Do not infer numbering from a mirrored fabrication preview. |
| Pitch and finger count | 44 contacts, 22 per face, at 2.54 mm pitch. |
| Finger geometry | Record finger width, plated length, pitch, and the exact board thickness. Confirm they match the intended mating connector. |
| Edge location | Gold fingers finish exactly at the routed insertion edge; no solder mask covers the contact area. |
| Copper layers | For a bevelled design, ensure no inner copper can be exposed at the insertion edge. A two-layer board satisfies this by construction. |
| Clearance | Keep PTH pads, SMD pads, and unrelated copper at least 2.00 mm from the top of the gold-finger region. Tracks which intentionally leave a finger are not unrelated copper. |
| Board outline | Measure width, tongue width, overall length, symmetric tapers/shoulders, and any keying features from `Edge.Cuts`. Check both extrema, not only the CAD dimension label. |
| Markings | Put unambiguous contact numbers on both views, and make the rear pinout table readable in the board-house rear-view convention. |

Run KiCad DRC after the final geometry, silkscreen, and net edits. Resolve every
error and unconnected item; warnings need a written, intentional justification.

## Release gate 2: fabrication selection

An edge connector is a special process. The base surface finish and the finger
finish are different selections.

For Eurocircuits, select:

- FR-4, with the board thickness required by the mating connector. This project
  uses **1.55 mm**.
- `Gold Edge Connectors` / selective **electroplated hard Ni/Au** fingers.
- `Edge Connector Bevelling`, normally the standard **30 degree** bevel.
- A base finish for the rest of the board. `Che Ni/Au` (ENIG) is suitable, but
  it is **not** a substitute for hard gold on the fingers.
- Electrical test when offered; select 100% test where the order flow makes a
  distinction.

Hard gold is the wear surface. Eurocircuits describes it as nickel plus
electroplated hard gold and specifically recommends it for repeated insertion:
[gold-plating process](https://www.eurocircuits.com/technical-guidelines/pcb-manufacturing-technology/gold-plating-for-edge-connectors/),
[edge-connector design limits](https://www.eurocircuits.com/technical-guidelines/pcb-design-guidelines/edge-connectors/).

In the order notes state: `J1 is an intentional selective hard-gold edge
connector. Copper intentionally reaches the insertion edge. Apply the specified
bevel.` This prevents a generic copper-to-board-edge warning from being treated
as an accidental data error.

## Release gate 3: gold-area calculation

Calculate this from the actual plated finger rectangles, not the whole card
edge and not only one face:

```text
total gold area (mm²) = fingers per face × plated width (mm)
                        × plated length (mm) × number of faces
```

For this board:

```text
22 × 1.27 mm × 8.84 mm × 2 = 493.98 mm²
```

Enter **494 mm² total for both outer layers**, unless Eurocircuits explicitly
confirms that a particular calculator field expects one-face area. The one-face
value is approximately **247 mm²**. Their published guidance says that the
gold-surface parameter is the total over both outer layers; preserve the
support response with the order record:
[Edge Connectors with Gold Surface](https://www.eurocircuits.com/edge-connector-gold-surface/).

Also confirm these special-process limits before release:

- plated-finger length is no more than 40 mm;
- plated pads are on an accessible outside board edge;
- the panel arrangement permits the plating-bar connection;
- the board dimension perpendicular to a standard bevel is 40–400 mm; and
- the requested thickness is within the board house's bevel capability.

## Release gate 4: deliverable audit

Export the manufacturing archive only after release gates 1–3 pass. The archive
must include front/back copper, mask, legend, profile, drill data, and job data.

Before uploading:

1. Open front and rear Gerber renders. Verify the rear image is a rear view;
   it is naturally mirrored relative to the front.
2. Verify every finger is bare copper/finish on the appropriate side, and that
   no mask opening or outline is offset.
3. Verify the back-side safety table and its header appear in the actual legend
   Gerber, not only in KiCad's editor.
4. Check the board-house detected dimensions against the intended finished
   outline. Any discrepancy is a release blocker, even if the checker calls the
   outline merely “uncertain”.
5. Upload the revisioned ZIP and retain its SHA-256 checksum, KiCad version,
   DRC report, drill report, and the exact order-option screenshot.

## Release gate 5: incoming inspection and first powered use

Fabrication review cannot prove fit in every aged console. Before attaching an
experimental circuit or applying power:

1. Inspect finger plating, bevel, solder mask boundary, board profile, and
   legibility of both silk sides under magnification.
2. Measure thickness in the contact region and finger pitch/width on one sample.
   Compare to the order and known-good card; note that the plating contributes
   only microns, while laminate tolerance dominates fit.
3. With a multimeter, test all 44 intended J1-to-J2 paths and verify no shorts
   between adjacent contacts. For an active cartridge, use its netlist instead
   of the passive-adapter one-to-one rule.
4. Insert one board gently into a known-good, unpowered Intellivision and then
   an Intellivoice socket. It must seat without excessive force, scraping, or
   interference with the shell.
5. Power only a proven-safe circuit. Begin with a current-limited supply or a
   sacrificial/known-good test fixture where practical. Never use an unverified
   experimental J2 harness on a console; this adapter exposes power, address,
   data, timing, audio, and video-related signals.

Keep the measured first-article results with the fabrication record. A board is
accepted only when the visual, mechanical, continuity, and in-system tests all
pass.

## Current-board release record

For `intelliputer_connector.kicad_pcb` revision 1.1:

- two copper layers; 1.55 mm nominal board;
- 44 fingers, 1.27 mm × 8.84 mm, 2.54 mm pitch, on both faces;
- calculated selective hard-gold surface: 493.98 mm² total;
- 44 × 1.00 mm finished plated drills for J2;
- source DRC: zero violations and zero unconnected items after the final
  silkscreen/thickness update.

The remaining order-time confirmations are the 494 mm² calculator convention,
the selected hard-gold-and-bevel options, and the fabricator's acknowledgement
of the intentional copper-to-edge contact region.

# Production release — J2 0.889 mm variant

Status: **approved for production**.

This release applies only to
`project/intelliputer-connector-j2-0.889mm/intelliputer_connector.kicad_pcb`
and its matching manufacturing archive
`Intelliputer-Connector-Gerbers-r1.1-j2-0.889.zip`.

## Verified fabrication details

- **J2 plated drills:** 0.889 mm in the KiCad source and Excellon drill file;
  Eurocircuits displays this as **0.90 mm**.
- **J1 edge-finger finish:** electroplated hard gold over nickel, on both
  sides of the J1 card edge.
- **Hard-gold area:** 494 mm² total (44 fingers × 1.27 mm × 8.84 mm).
- **J1 leading edge:** standard 30° bevel.

## Fabricator confirmation

Eurocircuits confirmed that the board can be produced using these order
details and that hard gold is suitable for this application. This confirmation
resolves the previous ambiguity between selective Che Ni/Au (ENIG) and the
required hard-gold edge-finger process.

## Release checks

- KiCad 10.0.7 DRC: zero violations, zero unconnected pads.
- Drill report: 44 plated holes at 0.889 mm.
- Gerber ZIP archive integrity: verified after generation.

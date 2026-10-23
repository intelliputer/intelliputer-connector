# Intelliputer Connector fabrication package

Manufacturing data is organized by J2 drill variant:

- [`intelliputer-connector-j2-1.000mm/`](intelliputer-connector-j2-1.000mm/)
  holds the released revision 1.1 export. It was generated with KiCad 10.0.7
  and passes DRC with zero violations and zero unconnected items. Its order
  archive is
  [`Intelliputer-Connector-Gerbers-r1.1.zip`](intelliputer-connector-j2-1.000mm/Intelliputer-Connector-Gerbers-r1.1.zip).
- [`intelliputer-connector-j2-0.889mm/`](intelliputer-connector-j2-0.889mm/)
  holds the KiCad 10.0.7 export for the M6x09-II-SBC-matched 0.889 mm
  (0.035 in) plated J2 drills. Its DRC also passes with zero violations and
  zero unconnected items. Its order archive is
  [`Intelliputer-Connector-Gerbers-r1.1-j2-0.889.zip`](intelliputer-connector-j2-0.889mm/Intelliputer-Connector-Gerbers-r1.1-j2-0.889.zip).
  Eurocircuits has confirmed it for production with hard-gold J1 fingers and
  a standard 30° bevel; see its
  [`production release`](intelliputer-connector-j2-0.889mm/PRODUCTION-RELEASE.md).

Orientation marking: viewing the component/front side with J2 at the top, the
J2 upper row is the even row (`44` at left to `2` at right); the lower row is
the odd row (`43` at left to square-pad `1` at right). J1 retains the matching
front-side edge labels, `44` at left and `2` at right.

Fabrication requirements:

- Two copper layers: F.Cu and B.Cu
- Finished board thickness: **1.55 mm**
- 44 plated through holes: **1.00 mm finished drill** in the baseline variant;
  **0.889 mm (0.035 in)** in the M6x09-matched variant
- Card-edge finger pitch: **2.54 mm**
- Card-edge contacts are exposed on both sides. Specify a suitable connector
  contact finish with the board house—hard gold over nickel is preferred for
  repeated insertion—and ask whether bevelled card-edge fingers are available.
- The board profile is supplied by
  `intelliputer_connector-Edge_Cuts.gbr`.

For the full repeatable release, ordering, and first-article acceptance process
for this and other Intellivision card-edge designs, see
[Precision edge-connector production procedure](edge-connector-production-procedure.md).

Files:

- `.gbr`: Gerbers for front/back copper, solder mask, silkscreen, and board
  profile (the filename identifies the layer)
- `.drl`: plated-through Excellon drill data
- `Intelliputer-Connector-DRC-*.txt`: KiCad DRC result
- `Intelliputer-Connector-Drill-Report-*.txt`: drill summary

# Intelliputer Connector fabrication package

Revision 1.1 was exported from `project/intelliputer_connector.kicad_pcb` with
KiCad 10.0.7. The source layout passes DRC with zero violations and zero
unconnected items. Use `Intelliputer-Connector-Gerbers-r1.1.zip` for this
revision; the non-revisioned archive is retained as the earlier fabrication
package.

Orientation marking: viewing the component/front side with J2 at the top, the
J2 upper row is the even row (`44` at left to `2` at right); the lower row is
the odd row (`43` at left to square-pad `1` at right). J1 retains the matching
front-side edge labels, `44` at left and `2` at right.

Fabrication requirements:

- Two copper layers: F.Cu and B.Cu
- Finished board thickness: **1.55 mm**
- 44 plated through holes: **1.00 mm finished drill**
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
- `Intelliputer-Connector-DRC-r1.1.txt`: KiCad DRC result
- `Intelliputer-Connector-Drill-Report-r1.1.txt`: drill summary

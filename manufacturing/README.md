# Intelliputer Connector fabrication package

This package was exported from `project/intelliputer_connector.kicad_pcb` with
KiCad 10.0.7. The source layout passes DRC with zero violations and zero
unconnected items.

Fabrication requirements:

- Two copper layers: F.Cu and B.Cu
- Finished board thickness: **1.6 mm**
- 44 plated through holes: **1.00 mm finished drill**
- Card-edge finger pitch: **2.54 mm**
- Card-edge contacts are exposed on both sides. Specify a suitable connector
  contact finish with the board house—hard gold over nickel is preferred for
  repeated insertion—and ask whether bevelled card-edge fingers are available.
- The board profile is supplied by
  `intelliputer_connector-Edge_Cuts.gm1`.

Files:

- `.gtl` / `.gbl`: front / back copper
- `.gts` / `.gbs`: front / back solder mask
- `.gto`: front silkscreen
- `.gm1`: board profile
- `.drl`: plated-through Excellon drill data
- `Intelliputer-Connector-DRC.txt`: KiCad DRC result
- `Intelliputer-Connector-Drill-Report.txt`: drill summary

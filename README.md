# Intelliputer Connector

Passive 44-contact Intellivision cartridge card-edge to 44-way ribbon-header adapter.

Open [the Intelliputer Connector design](project/intelliputer_connector.kicad_pcb) in KiCad. Its
card-edge contacts connect one-to-one with the 2×22 through-hole ribbon header;
the board uses the original cartridge outline.

## Current status

- The 1:1 routing is complete, including the repaired `CARD_14` connection.
- KiCad 10.0.7 DRC passes with **zero violations** and **zero unconnected
  items**.
- The current fabrication package is available as
  [Intelliputer-Connector-Gerbers.zip](manufacturing/Intelliputer-Connector-Gerbers.zip).
  It contains the `.gbr` Gerbers, Excellon drill data, drill map, and current
  DRC and drill reports.

See the [fabrication package notes](manufacturing/README.md) for board-house
requirements and file details.

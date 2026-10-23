# Intelliputer Connector

This is the stripped, passive replacement for the original Intellicart controller PCB.

Two independent KiCad project variants are provided:

- [`intelliputer-connector-j2-1.000mm/`](intelliputer-connector-j2-1.000mm/):
  baseline, 1.000 mm J2 plated drills.
- [`intelliputer-connector-j2-0.889mm/`](intelliputer-connector-j2-0.889mm/):
  M6x09-II-SBC-matched, 0.889 mm (0.035 in) J2 plated drills.

- **J1:** 44-contact (2 × 22) card-edge fingers, 2.54 mm pitch
- **J2:** 44-way (2 × 22), 2.54 mm through-hole ribbon/IDC header footprint
- **Mapping:** direct and one-to-one: J1 pin *n* connects only to J2 pin *n*
- **Board:** 1.55 mm FR-4, using the original Intellicart / Intellivision cartridge outline: 68.07 mm maximum width, a 58.19 mm card tongue, and 83.91 mm overall length.
- **Artwork:** a centered vintage-computer icon on the front silkscreen.

With the card-edge at the bottom and the component side facing the viewer, J2's upper row runs from 2 at the right through 44 at the left; its lower row runs from 1 at the right through 43 at the left. Pin 1 is the square plated-through hole and is marked on the silkscreen.

No active components, pull-ups, LEDs, switches, display connector, or controller hardware are included.

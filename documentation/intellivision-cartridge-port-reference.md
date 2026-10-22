# Intellivision cartridge port reference

This is an original, attributed transcription of the *technical facts* in the
[Intellivision Wiki cartridge-port reference](https://wiki.intellivision.us/index.php/Cartridge_Port),
adapted for the Intelliputer Connector. Consult that page for its original
wording and illustrations. The Intellivision Master Component uses a 44-contact,
0.1-inch-pitch card-edge port. In this repository, each card-edge contact is
routed directly to the same-numbered J2 header contact.

## Contact assignment

The source identifies the component/top side as the even contacts and the
solder/bottom side as the odd contacts. The Intelliputer PCB uses the same
numbering: odd contacts are B.Cu and even contacts are F.Cu.

| Top / component side (even) | Meaning | Bottom / solder side (odd) | Meaning |
| --- | --- | --- | --- |
| 2 — `GND` | Ground on Intellivision I; System Changer video input on Intellivision II; Intellivoice `C1` alternate use. | 1 — `GND` | Ground. |
| 4 — `CBLNK` | Character blank / horizontal-retrace timing; Intellivoice `C2` alternate use. | 3 — `~MSYNC` | Master-sync output. |
| 6 — `EXT AUDIO` | External audio input. | 5 — `DB7` | Address/data-bus bit 7. |
| 8 — `EXT VIDEO` | External video input on Intellivision I. | 7 — `DB8` | Address/data-bus bit 8. |
| 10 — `MCLK` | 3.579545 MHz master clock. | 9 — `DB6` | Address/data-bus bit 6. |
| 12 — `RESET` | Reset-pulse input. | 11 — `DB9` | Address/data-bus bit 9. |
| 14 — `SR1` | STIC timing / interrupt-related signal. | 13 — `DB5` | Address/data-bus bit 5. |
| 16 — `SER OUT` | Intellivoice serial-bus output. | 15 — `DB10` | Address/data-bus bit 10. |
| 18 — `SER IN` | Intellivoice serial-bus input. | 17 — `DB4` | Address/data-bus bit 4. |
| 20 — `ROM DISABLE` | Intellivoice external-speech-ROM disable input. | 19 — `DB11` | Address/data-bus bit 11. |
| 22 — `GND` | Ground. | 21 — `DB3` | Address/data-bus bit 3. |
| 24 — `GND` | Ground. | 23 — `DB12` | Address/data-bus bit 12. |
| 26 — `GND` | Ground. | 25 — `DB13` | Address/data-bus bit 13. |
| 28 — `GND` | Ground. | 27 — `DB2` | Address/data-bus bit 2. |
| 30 — `~BUSAK` | Active-low bus acknowledge; Intellivoice ROM-clock alternate use. | 29 — `DB14` | Address/data-bus bit 14. |
| 32 — `BC1` in | Reflected bus-control input 1. | 31 — `DB1` | Address/data-bus bit 1. |
| 34 — `BC2` in | Reflected bus-control input 2. | 33 — `DB0` | Address/data-bus bit 0. |
| 36 — `BDIR` in | Reflected bus-direction/control input. | 35 — `DB15` | Address/data-bus bit 15. |
| 38 — `BDIR` out | Duplicate raw bus-direction/control output. | 37 — `BDIR` out | Raw bus-direction/control output normally used by Mattel cartridges. |
| 40 — `BC2` out | Duplicate raw bus-control output 2. | 39 — `BC2` out | Raw bus-control output 2 normally used by Mattel cartridges. |
| 42 — `BC1` out | Duplicate raw bus-control output 1. | 41 — `BC1` out | Raw bus-control output 1 normally used by Mattel cartridges. |
| 44 — `GND` | Ground. | 43 — `VCC` | +5 V supply. |

## Signal descriptions

- `VCC` and `GND` supply +5 V and return respectively. The port exposes ground
  at contacts 1, 2 (on Intellivision I), 22, 24, 26, 28, and 44.
- `RESET` is edge-sensitive inside the console: a low-going pulse causes the
  STIC to assert `~MSYNC`. Holding it low is not equivalent to holding the
  system in reset.
- `~MSYNC` is driven low for at least 10 ms during reset.
- `MCLK` is the console's 3.579545 MHz master-clock output.
- `DB0` through `DB15` form the CP1610's multiplexed 16-bit address/data bus.
- `~BUSAK` goes low when the CP1610 relinquishes the bus for STIC DMA. The
  source notes that the scope for external access during this interval is not
  established.
- `SR1` connects to the CP1610 interrupt-mask input and indicates the STIC's
  vertical-refresh phase.
- `CBLNK` is character-blank/horizontal-retrace timing, used for genlocking the
  Keyboard Component video circuitry.
- `EXT AUDIO` accepts added audio, including from the Intellivoice or ECS sound
  hardware. `EXT VIDEO` was intended for Keyboard Component genlocked video;
  Intellivision II changes the video-input implementation for the System
  Changer and moves that function to contact 2.
- `C1`, `C2`, `C3`, `SER OUT`, `SER IN`, `ROM CLOCK`, and `ROM DISABLE` are
  alternate Intellivoice speech-ROM-expansion-bus uses of cartridge contacts.

## Bus-control path and normal loopbacks

`BC1`, `BC2`, and `BDIR` describe the CP1610 bus phase. Raw outputs appear in
duplicate at 37/38, 39/40, and 41/42. Conventional cartridges connect the
second copy to the reflected inputs: `38 -> 36` (`BDIR`), `40 -> 34` (`BC2`),
and `42 -> 32` (`BC1`). The reflected lines feed the EXEC ROMs, PSG, and 8-bit
RAM, while the raw connections preserve an interception point for external
hardware such as the Keyboard Component. The duplicates also make this routing
possible on a double-sided cartridge without vias.

The Intelliputer Connector is intentionally passive, so none of those three
bridges exists on the adapter. Fit them in the circuit attached to J2 when
normal cartridge-ROM behavior is wanted; omit or actively control them when
the attached hardware must mediate bus cycles.

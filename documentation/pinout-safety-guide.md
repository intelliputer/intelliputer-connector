# Intellivision pinout safety guide

Use this guide before connecting an experiment to the Intelliputer Connector.
It describes the production board orientation and the electrical identity of
every J2 contact. The PCB is passive: **J2 pin _n_ is connected only to
card-edge contact J1 pin _n_.**

The signal names and meanings follow the
[published Intellivision cartridge-port specification](https://wiki.intellivision.us/index.php/Cartridge_Port).
For fuller signal descriptions, see the
[local cartridge-port reference](intellivision-cartridge-port-reference.md).

## The one orientation rule to remember

Look at the **component/silkscreen side** of the board—the side with the
Intelliputer artwork and the J2 pin-1 square pad. Keep J2 at the top and the
card edge at the bottom:

```text
                    TOP / F.Cu — component side, inserted facing up

        J2 header, viewed from the component side
        left                                                     right
 upper:  44  42  40  38  36  34  32 ...  8   6   4   2
 lower:  43  41  39  37  35  33  31 ...  7   5   3  [1]  <- square J2 pin 1

        card edge, visible on this side (top/F.Cu)
        44  42  40  38  36  34  32 ...  8   6   4   2
        --------------------------------------------------  insertion edge
                                                     ^
                                     J2 pin 2 and this finger are the same net

        The contact opposite that rightmost visible pin-2 finger is J1 pin 1
        on the B.Cu bottom side. J2 pin 1, immediately below J2 pin 2,
        connects to that hidden contact.
```

In short: **the square J2 pad is pin 1; the visible card finger immediately
below it is pin 2.** This is correct, not a reversal.

When viewing the B.Cu side with the card edge still at the bottom, turn the
board over left-to-right. Its visible contacts then read `1, 3, 5 ... 43` from
left to right.

## Pin-for-pin wiring map

Each row is one physical J2 header column. “Upper” and “lower” mean the rows
in the orientation diagram above. The J1 contacts are on opposite sides of the
same card-edge column.

| J2 upper / lower | J1 bottom / top | Intellivision assignments | Use with care |
| --- | --- | --- | --- |
| 2 / 1 | 1 / 2 | `GND` / `GND` on Intellivision I; pin 2 is System Changer video input on Intellivision II | Do not assume pin 2 is ground on every console. |
| 4 / 3 | 3 / 4 | `~MSYNC` / `CBLNK` | Timing signals; do not drive them. |
| 6 / 5 | 5 / 6 | `DB7` / external audio input | Bus signal / console audio input. |
| 8 / 7 | 7 / 8 | `DB8` / external video input | Bus signal / console video input. |
| 10 / 9 | 9 / 10 | `DB6` / `MCLK` | `MCLK` is a 3.579545 MHz console output. |
| 12 / 11 | 11 / 12 | `DB9` / `RESET` | Reset responds to a low-going pulse. |
| 14 / 13 | 13 / 14 | `DB5` / `SR1` | `SR1` is STIC timing/interrupt-related. |
| 16 / 15 | 15 / 16 | `DB10` / Intellivoice `SER OUT` | Serial alternate function on 16. |
| 18 / 17 | 17 / 18 | `DB4` / Intellivoice `SER IN` | Serial alternate function on 18. |
| 20 / 19 | 19 / 20 | `DB11` / Intellivoice `ROM DISABLE` | Speech-ROM-expansion alternate function on 20. |
| 22 / 21 | 21 / 22 | `DB3` / `GND` |  |
| 24 / 23 | 23 / 24 | `DB12` / `GND` |  |
| 26 / 25 | 25 / 26 | `DB13` / `GND` |  |
| 28 / 27 | 27 / 28 | `DB2` / `GND` |  |
| 30 / 29 | 29 / 30 | `DB14` / `~BUSAK` | `~BUSAK` is active low. |
| 32 / 31 | 31 / 32 | `DB1` / reflected `BC1` input | See the loopback note below. |
| 34 / 33 | 33 / 34 | `DB0` / reflected `BC2` input | See the loopback note below. |
| 36 / 35 | 35 / 36 | `DB15` / reflected `BDIR` input | See the loopback note below. |
| 38 / 37 | 37 / 38 | raw `BDIR` output / duplicate raw `BDIR` output | Console-driven control outputs. |
| 40 / 39 | 39 / 40 | raw `BC2` output / duplicate raw `BC2` output | Console-driven control outputs. |
| 42 / 41 | 41 / 42 | raw `BC1` output / duplicate raw `BC1` output | Console-driven control outputs. |
| 44 / 43 | 43 / 44 | **+5 V** / `GND` | Pin 43 is the +5 V supply. Check this first. |

## Before powering an experiment

1. With the console **unpowered**, use continuity mode to confirm the intended
   J2 contact reaches the correct card-edge contact. In particular, verify J2
   43 reaches J1 43 (+5 V) and J2 44 reaches J1 44 (ground).
2. Do not inject a voltage onto any contact until its console direction and
   function are understood. Most `DB*`, timing, and bus-control signals are
   console-driven or bidirectional.
3. Do not treat J2 2 as universally safe ground: it is external video on an
   Intellivision II.
4. Add current limiting or a fuse when bringing up new powered hardware.
5. Connect the three conventional bus-control bridges only when the attached
   circuit needs normal cartridge-ROM operation: `38 -> 36`, `40 -> 34`, and
   `42 -> 32`. Leave them open when the experiment must intercept those bus
   cycles.

## PCB markings

The source PCB silkscreen marks all four J2 corner contacts: `2`/`1` at the
upper/lower right and `44`/`43` at the upper/lower left. At the card edge,
F.Cu marks the top/even
endpoints (`44` at left and `2` at right), while B.Cu marks the bottom/odd
endpoints (`43` at left and `1` at right in the PCB coordinate system). The
B.Cu side also carries the compact two-column 1–44 connection table above the
card tongue. These markings are orientation aids; this Markdown table retains
the fuller safety context.

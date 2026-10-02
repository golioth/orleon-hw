# Orleon

A small round battery-powered Bluetooth LE sensor board from Golioth, built
around the Nordic nRF52840 in WLCSP. Rev A.

Orleon was designed as part of Golioth's "Designing and Building an AirTag
Clone" webinar series (April 2025):
https://blog.golioth.io/designing-and-building-an-airtag-clone-a-new-series-from-golioth/

> **Status:** pre-release cleanup for open-hardware (OSHW) publication.
> Items marked **[UNKNOWN]** need confirmation before this README is final.

## Hardware summary (Rev A)

| Subsystem | Part / details | Notes |
|-----------|----------------|-------|
| Main SoC  | Nordic nRF52840-CKAA-F-R | WLCSP package |
| IMU       | ST LIS2DH12 | 3-axis accelerometer, I2C |
| Microphone| ST MP34DT05TR-A | PDM MEMS mic |
| Audio out | Raltron RDTE-4.000-3030-NS1 | electromagnetic transducer (buzzer) |
| BLE antenna | Taoglas WLA.04 | 2.4 GHz chip antenna |
| NFC       | Taoglas FXC.24.A flex antenna | |
| Battery   | CR2032 coin cell (HF1N holder) | |
| Board     | round, ~22 mm diameter | [UNKNOWN] confirm exact diameter |

## Hardware status (Rev A)

Rev A was manufactured by JLCPCB but **never fully validated**. Two issues
were found before the design was set aside:

1. **BGA copper pour.** The copper fill under the nRF52840 WLCSP was filled
   improperly at the fab. Recommended rework: remove the copper pour under
   the BGA entirely and instead place vias on each ball down to the ground
   layer.
2. **Buttons.** The side-firing button style was not a good fit for this
   form factor.

**This design was superseded by [Phial](https://github.com/golioth/phial-hw)**
(nRF54L15 + nPM2100), which is the better starting point for new work —
though note that Phial has its own validation issues (see that repo's README
for current status).

## Design files

- KiCad 9 project (`orleon.*`).
- JLCPCB was used for Rev A fabrication; commit history notes their 3.5 mil
  trace/space clearance constraint drove via/pad rework (see commit
  `cd74782`).
- `input/` — local symbol/footprint/3D sources and reference art.
- `orleon.pretty/` — project footprints (including Golioth and Orleon logo art
  footprints).

## Manufacturing outputs

**[UNKNOWN / TODO]** Rev A gerber packages (`orleon-a-*.zip`) were generated
for JLCPCB but never committed (gitignored). A fabrication package (gerbers,
drill, pick-and-place, BOM, schematic PDF) should be attached to a GitHub
Release before publication.

## Firmware

Firmware lives in a separate repo: [golioth/orleon-fw](https://github.com/golioth/orleon-fw)
(currently private).

## License

Hardware in this repository is released under the **CERN Open Hardware
Licence v2 — Permissive (CERN-OHL-P)**. See [LICENSE](LICENSE).

Note: `input/art/` contains vendor reference images (JLCPCB stackup, Taoglas
antenna drawings) that are **not** covered by this license and may be replaced
with links before publication.

## Credits

Designed by Chris Gammell at Golioth.

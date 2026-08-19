# Custom 4-bit Wallace Tree Multiplier — Transistor-Level IP Core

**Phase 1 of a custom ASIC project** · Designed and verified entirely at the CMOS transistor level in Cadence Virtuoso — no RTL, no synthesis tool.

From transistor-level schematics to 2.02 GHz operation: every gate, carry path, and timing parameter in this multiplier was designed, analyzed, and verified by hand at the transistor level.

---

## Overview

This project is a custom 4-bit Wallace Tree multiplier built as a full-custom IP core rather than a synthesized RTL block. Every partial product generator, adder, and carry path was hand-placed as a transistor-level schematic and verified through transient simulation — no HDL, no synthesis tool doing the reduction or gate mapping for you.

It's Phase 1 of a larger custom ASIC project; the RTL/standard-cell-flow continuation of this work is the [4×4 Pipelined MAC Unit](https://github.com/GithubJayanta/MAC_unit_4bit).

## The honest part first

At first, this genuinely felt like it wasn't going to work out. Transistor-level design is a different kind of hard — no RTL abstractions, no synthesis tool to catch mistakes, just a schematic and a waveform that refuses to make sense at 2 AM.

There were nights where the error signal wouldn't settle to zero, and it wasn't obvious whether the multiplier was actually broken or the simulation was being misread. It turned out to be switching glitches, not a functional failure — but getting to that conclusion took hours of staring at waveforms at midnight.

Going deeper instead of walking away is where the real learning happened.

## What was implemented

- Custom Wallace Tree reduction architecture at the transistor level
- Partial Product Generation, Half Adders, Full Adders, and a Carry Look-Ahead Adder
- Functional verification via transient simulation across comprehensive input combinations
- Expected-vs-actual output validation — glitches identified as switching artifacts, not functional failures
- Full PPA characterization: silicon area estimation, average dynamic power, and timing closure

## Performance results

| Metric | Value |
|---|---|
| Functional correctness | 100% verified via transient analysis and registered output comparison |
| Technology | 90 nm CMOS |
| Hardware complexity | 63 logic gates, 828 transistors (~207 gate-equivalents) |
| Estimated silicon area | 134–201 µm² |
| Average dynamic power | 2.22 µW |
| Critical combinational delay | 395 ps |
| Clock-to-Q delay | 72.691 ps |
| Setup time | 28 ps |
| Minimum clock period | 495.691 ps |
| Maximum operating frequency | ≈ 2.02 GHz |
| Power-Delay Product (PDP) | 0.877 fJ |

Working below RTL gives you a different perspective on what synthesis tools abstract away — carry propagation, silicon area costs, and timing closure when every transistor is placed by decision, not automation.

## Waveforms & schematics

| # | File | What it shows |
|---|---|---|
| 1 | `images/01_transistor_level_schematic.jpeg` | Full transistor-level schematic of the Wallace Tree multiplier |
| 2 | `images/02_functional_verification_all_io.jpeg` | Transient simulation of all inputs (a0–a3, b0–b3) and outputs (s0–s7) across comprehensive test vectors |
| 3 | `images/03_dff_register_transient.jpeg` | Clock / data / registered-output transient response for an output register |
| 4 | `images/04_clock_to_q_delay_measurement.jpeg` | Measured clock-to-Q delay (72.691 ps) |
| 5 | `images/05_critical_path_delay_measurement.jpeg` | Measured critical combinational path delay (~395 ps) |
| 6 | `images/06_dynamic_power_transient.jpeg` | Dynamic power transient response, showing switching-activity power spikes |
| 7 | `images/07_expected_vs_actual_output_validation_analog.jpeg` | Expected-vs-actual product output validation on the analog (continuous voltage) waveforms — used to isolate switching glitches from real functional failures |
| 8 | `images/08_expected_vs_actual_output_validation_discrete.jpeg` | Expected-vs-actual product output validation on the discretized (digital) output bits |

## Tools

Cadence Virtuoso (schematic capture, transient/transistor-level simulation)

## Timeline

June 2026

## Repo structure

```
.
├── README.md
└── images/
    ├── 01_transistor_level_schematic.jpeg
    ├── 02_functional_verification_all_io.jpeg
    ├── 03_dff_register_transient.jpeg
    ├── 04_clock_to_q_delay_measurement.jpeg
    ├── 05_critical_path_delay_measurement.jpeg
    ├── 06_dynamic_power_transient.jpeg
    ├── 07_expected_vs_actual_output_validation_analog.jpeg
    └── 08_expected_vs_actual_output_validation_discrete.jpeg
```

## Related work

- Phase 2 (RTL-to-GDSII, standard-cell flow): [4×4 Pipelined MAC Unit](https://github.com/GithubJayanta/MAC_unit_4bit)
- [4-bit Kogge-Stone Adder](https://github.com/GithubJayanta/4-Bit_Kogge_Stone_Adder) — a related micro-architecture/PPA study

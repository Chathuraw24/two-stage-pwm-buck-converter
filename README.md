# Two-Stage PWM Buck Converter — Solar-Powered Charging System

**Course:** EET 4304 – Power Electronics | Year 4, Semester 1
**Institution:** Rajarata University of Sri Lanka, Faculty of Technology
**Author:** W.M.C.P. Weerasinghe (ENT/2021/108)

## Overview

Design and analysis of a two-stage PWM-controlled DC–DC buck converter for a portable solar-powered charging system. The converter steps down a variable solar panel voltage to charge a 12V lead-acid battery, then further regulates the battery voltage to a stable 5V USB output.

- **Stage 1:** 15–20 V (solar) → 12–14.4 V (battery charging)
- **Stage 2:** 12–14.4 V (battery) → 5 V, 3 A (USB output)
- **Target efficiency:** >85% (achieved ~98% Stage 1, ~90% Stage 2 at midpoint conditions)

## Control Approach

Instead of a dedicated SMPS controller IC, the design uses a discrete analog closed-loop PWM control scheme:

| Function | Component |
|---|---|
| Ramp/sawtooth generator | NE555 (100 kHz) |
| Voltage reference & error sensing | TL431 |
| PWM comparator | LM311 |
| Gate driver | TC4420 |
| Power switch | IRLZ44N MOSFET |
| Freewheeling diode | Schottky (≥5 A) |

A resistor-divider feedback compares the output voltage to a TL431 reference; the resulting error signal is compared against the NE555 ramp on the LM311 to generate the PWM duty cycle, which is buffered by the TC4420 to drive the MOSFET.

## Repository Contents

| File | Description |
|---|---|
| `EET4304_Assignment1_1604__1_.pdf` | Full assignment report — design justification, hand calculations, component selection, MATLAB/Simulink & Proteus results, cost analysis, and conclusion |
| `Group_2.slx` | MATLAB/Simulink model of the two-stage buck converter |

## Key Design Calculations

- **Duty cycle (midpoint):** Stage 1 D₁ ≈ 0.823 (17.5V→14.4V), Stage 2 D₂ ≈ 0.379 (13.2V→5V)
- **Inductors:** L1 = 85 µH, L2 = 34.5 µH (100 kHz switching, 30% ripple)
- **Output capacitors:** C1 = 3.75 µF, C2 = 22.5 µF
- **Switching frequency:** 100 kHz (both stages)

## Simulation & Validation

The design was verified in two environments:
- **MATLAB/Simulink** — closed-loop transient response under 1000 W/m² and 500 W/m² solar irradiance, duty cycle stability, PV/battery/output voltage and current waveforms.
- **Proteus** — analog PWM control circuit and power stage schematic, with oscilloscope captures of sawtooth generation, duty cycle variation, and output regulation across the full input voltage range (12V–20V).

## Cost Analysis

Estimated total component cost: **~1,051 LKR**, using locally available, low-cost parts to support practical real-world implementation.

## Future Improvements

- Hardware prototyping and thermal analysis
- Synchronous rectification (replacing diode) to improve efficiency
- MPPT (Maximum Power Point Tracking) integration for better solar utilization under varying irradiance

## References

Full datasheet and source references are listed in the report (Section 10) — includes NE555, TL431, LM311, TC4420, and IRLZ44N datasheets from TI, Microchip, and Infineon.

# Mini 2A Buck Converter SMPS (AP6320X Family)

This repository contains the hardware design files in **KiCad** for an ultra-compact, high-efficiency **2A synchronous buck (step-down) converter**. The board layout is fully compatible with all four variants of the **AP6320X** integrated circuit from Diodes Incorporated, allowing the same PCB to be populated for different switching frequencies, operating modes, and output voltages.

## Technical Specifications

* **Input Voltage Range ($V_{IN}$):** 3.8 V to 32 V
* **Continuous Output Current ($I_{OUT}$):** 2 A
* **IC Package:** TSOT26
* **EMI Optimization:** Features Frequency Spread Spectrum (FSS) $\pm6\%$ and a proprietary gate driver system to eliminate switching node ringing without external components.
* **Form Factor:** Mini-size PCB layout optimized for tight spaces and minimal current loops.

---

## IC Variant Compatibility Matrix (AP63200 / 01 / 03 / 05)

The base PCB accommodates any of the four chip versions. Your component selection for the feedback network ($R_1$ and $R_2$) depends entirely on the specific IC you choose to solder:

| IC Variant | Frequency | Light-Load Mode | Output Voltage ($V_{OUT}$) | PCB Assembly Note |
| :--- | :--- | :--- | :--- | :--- |
| **AP63200** | 500 kHz | PFM (High Efficiency) | Adjustable (0.8 V to $V_{IN}$) | Populate feedback resistors $R_1$ and $R_2$ |
| **AP63201** | 500 kHz | Forced PWM | Adjustable (0.8 V to $V_{IN}$) | Populate feedback resistors $R_1$ and $R_2$ |
| **AP63203** | 1.1 MHz | PFM (High Efficiency) | **Fixed 3.3 V** | Solder $0\,\Omega$ jumper on $R_1$, omit $R_2$ |
| **AP63205** | 1.1 MHz | PFM (High Efficiency) | **Fixa 5.0 V** | Solder $0\,\Omega$ jumper on $R_1$, omit $R_2$ |

---

## Repository Structure

* `/hardware` : Core KiCad project files (`.kicad_pro`, `.kicad_sch`, `.kicad_pcb`).
* `/gerbers` : Production-ready Gerber and NC Drill files.
* `/docs` : Component [datasheets](https://diodes.com) and reference application notes.
* `/bom` : Interactive Bill of Materials (iBOM) or CSV component list.

---

## Mini PCB Layout Guidelines

Given the high-frequency nature of this switching regulator, strict layout constraints were implemented in this miniature design to guarantee stability and prevent EMI issues:

1. **Input Hot Loop:** The input ceramic capacitor ($C_{IN}$) is placed immediately adjacent to the `VIN` and `GND` pins of the IC to minimize parasitic trace inductance.
2. **Solid Ground Plane:** A 2-layer stackup where the bottom layer acts almost entirely as an uninterrupted, solid ground plane (`GND`).
3. **Switching Node (`SW`):** The copper trace connecting the `SW` pin to the power inductor is designed short and wide to carry 2 A, but kept small in area to avoid functioning as a radiating antenna.
4. **Thermal Vias:** Multiple vias connect the IC ground pads directly to the bottom layer copper to dissipate heat away from the TSOT26 package efficiently.

---

## Critical Component Selection

* **Power Inductor ($L_1$):** Shielded power inductor with a saturation current ($I_{SAT}$) rating strictly above **3 A** to prevent saturation during load transients.
* **Input/Output Capacitors ($C_{IN}$ / $C_{OUT}$):** **X7R** or **X5R** MLCC ceramic capacitors for low ESR and high capacitance retention under DC bias.
* **Feedback Resistors:** **1% tolerance** SMD resistors to maintain excellent target voltage accuracy (for adjustable versions).

---

## Requirements

* Designed and verified using **KiCad v7.0** or newer.

## License

This open-source hardware project is distributed under the **CERN OHL-W v2** (CERN Open Hardware Licence Weak) or equivalent open-source standard.

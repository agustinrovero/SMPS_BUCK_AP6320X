# Mini 2A Buck Converter SMPS (AP6320X Family)

This repository contains the hardware design files in **KiCad** for an ultra-compact, high-efficiency **2A synchronous buck (step-down) converter**. The board layout is fully compatible with all four variants of the **AP6320X** integrated circuit from Diodes Incorporated, allowing the same PCB to be populated for different switching frequencies, operating modes, and output voltages.

## Technical Specifications

* **Input Voltage Range ($V_{IN}$):** 3.8 V to 32 V
* **Continuous Output Current ($I_{OUT}$):** 2 A
* **EMI Optimization:** Features Frequency Spread Spectrum (FSS) and a proprietary gate driver system to eliminate switching node ringing without external components.
* **Form Factor:** $14.4\times15.4\text{ mm}^2$ mini-size PCB layout optimized for tight spaces and minimal current loops.

---

## IC Variant Compatibility Matrix

The base PCB accommodates any of the four chip versions. Your component selection for the feedback network ($R_1$ and $R_2$) depends entirely on the specific IC you choose to solder:

| Variant | Frequency | Light-Load Mode | Output Voltage ($V_{OUT}$) | PCB Assembly Note |
| :--- | :--- | :--- | :--- | :--- |
| **AP63200** | 500 kHz | PFM (High Efficiency) | Adjustable (0.8 V to $V_{IN}$) | Populate feedback resistors $R_1$ and $R_2$, and capacitor $C_{f1}$ |
| **AP63201** | 500 kHz | Forced PWM | Adjustable (0.8 V to $V_{IN}$) | Populate feedback resistors $R_1$ and $R_2$, and capacitor $C_{f1}$ |
| **AP63203** | 1.1 MHz | PFM (High Efficiency) | **Fixed 3.3 V** | Solder $0\,\Omega$ jumper on $R_1$, omit $R_2$ |
| **AP63205** | 1.1 MHz | PFM (High Efficiency) | **Fixa 5.0 V** | Solder $0\,\Omega$ jumper on $R_1$, omit $R_2$ |
---

## Repository Structure

* `Hardware`: Core KiCad project files (`.kicad_pro`, `.kicad_sch`, `.kicad_pcb`).
* `Docs`: Component [datasheets](https://diodes.com) and reference application notes.
* `Outputs/3D`:
* `Outputs/BOM`: Interactive Bill of Materials (iBOM) and CSV component list.
* `Outputs/Gerbers`: Production-ready Gerber and NC Drill files.

---

## Mini PCB Layout

* Capacitors, resistors ands LED are all 0603 size.
* Inductor uses a $6\times 6$ mm footprint.
  * The provided inductor was chosen to fulfill the 2 A output current requirement, but other inductors can be used, such as the Abracon LLC ASPI-0628-6R8M-T1 for up to 1 A (or 1.5 A) with a lower profile (only 2.8 mm instead of 4.5 mm).
*




## Critical Component Selection

* **Power Inductor ($L_1$):** Shielded power inductor with a saturation current ($I_{SAT}$) rating strictly above **3 A** to prevent saturation during load transients.
* **Input/Output Capacitors ($C_{IN}$ / $C_{OUT}$):** **X7R** or **X5R** MLCC ceramic capacitors for low ESR and high capacitance retention under DC bias.
* **Feedback Resistors:** **1% tolerance** SMD resistors to maintain excellent target voltage accuracy (for adjustable versions).

---

## Requirements

* Designed and verified using **KiCad v9.0.8**.

## License

This open-source hardware project is distributed under the **CERN OHL-W v2** (CERN Open Hardware Licence Weak) or equivalent open-source standard.

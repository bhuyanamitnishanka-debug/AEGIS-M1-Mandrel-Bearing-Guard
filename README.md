# AEGIS-M1: Non-Intrusive Condition Monitoring & Overhead Gantry Hydraulic-Lever System for Rolling Stand Mandrel Plain Bearings

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Status: PoC concept](https://img.shields.io/badge/Status-PoC%20concept-orange.svg)]()
[![Operating temperature](https://img.shields.io/badge/Operating%20range-45%E2%80%9380%C2%B0C-blue.svg)]()

> **Safety notice:** The repository contains a PoC concept, simulation dashboard, and illustrative control code. It is not independently validated or certified for industrial actuation or safety use. Physical deployment requires qualified mechanical, hydraulic, electrical, and control engineering review, hazard analysis, fail-safe interlocks, and site approval.

## Live Interactive Digital Twin & Dashboard

- **Live Web App (GitHub Pages):** https://bhuyanamitnishanka-debug.github.io/AEGIS-M1-Mandrel-Bearing-Guard/
- **Repository:** https://github.com/bhuyanamitnishanka-debug/AEGIS-M1-Mandrel-Bearing-Guard

---

## 1. Problem Statement

In high-speed steel rolling mills, mandrel plain bearings rely on a hydrodynamic oil film to separate the rotating roll shaft from the bearing liner. During low-RPM startup and coast-down regimes, insufficient shaft velocity may reduce the oil film and increase boundary-lubrication contact. This can cause asperity rubbing, wear, heat, debris, and unexpected stoppages.

Strict housing clearances, 45–80°C operating temperatures, mill scale, cooling-water spray, and low-frequency helical gear vibration make conventional intrusive or displacement-sensor installations difficult. AEGIS-M1 proposes external diagnostics combined with a gantry-mounted load-relief concept for engineering evaluation.

## 2. The AEGIS-M1 Solution

### 1. External High-Frequency Acoustic Emission Sensing

- Stud-mounted externally on the eccentric bearing housing, subject to site-specific attachment and qualification.
- Proposed diagnostic range: 100 kHz–1 MHz.
- The concept uses a nominal >150 kHz high-pass threshold to reduce lower-frequency gear and structural vibration components.
- The available C++ example is illustrative threshold logic, not a production signal-processing or safety system.

### 2. Inline Return-Line Oil Debris & Thermal Telemetry

- An external inductive wear-debris sensor and temperature probe could be installed in the oil scavenging/return line.
- Proposed monitoring includes ferrous/non-ferrous metallic debris in ppm and oil temperature across the 45–80°C envelope.
- The 45 ppm debris limit and 80°C limit are preliminary design values and require calibration and site-specific validation.

### 3. Overhead Gantry Hydraulic Lift & Dual-Side Compound Lever-Gear Control

- Hydraulic lift cylinders would be mounted on an overhead gantry bridge, keeping lower-deck infrastructure away from the hot billet area and mill scale.
- Dual ground-level ratchet controls could provide synchronized manual or mechanically linked operation at a safe distance.
- Preliminary proposal: 0.05–0.15 mm shaft load relief.
- Any real implementation requires structural and fatigue analysis, positive mechanical stops, pressure/load-holding valves, actuator feedback, guarding, emergency-stop integration, and fail-safe interlocks.
- The browser lever is a software demonstration only and is not connected to industrial actuators.

## 3. PoC Proposal Report

### Executive Summary

In continuous hot rolling operations, the Roll Shaft is supported inside an eccentric plain-bearing housing. A hydrodynamic oil wedge separates the shaft from the bearing liner at steady high speed. During startup, coast-down, and other low-RPM periods, lubrication conditions can change, allowing asperity contact and wear.

AEGIS-M1 combines external acoustic-emission sensing, return-line oil debris and temperature telemetry, and an overhead gantry load-relief concept. The purpose is to investigate whether such a system can provide earlier indication of boundary-lubrication events and support active load relief without internal bearing machining.

### Environmental and Engineering Constraints

- Limited internal clearance in the eccentric bearing housing
- Operating oil temperatures of approximately 45–80°C
- Mill scale, coolant spray, dust, heat, and vibration
- Low-frequency helical gear mesh noise can obscure conventional bearing vibration data
- Plain bearings lack characteristic rolling-element defect frequencies
- Exact thresholds must be established through site-specific testing

## 4. Proposed 8-Week PoC Execution Plan

| Phase | Timeline | Engineering activities | Proposed deliverable |
|---|---:|---|---|
| 1. Bench calibration and firmware validation | Weeks 1–2 | Calibrate AE and debris sensing on a variable-speed test rig; evaluate background gear noise and oil-temperature behavior. | Repeatable calibration report, tested code limitations, and approved sensor interfaces. |
| 2. Non-intrusive field retrofit | Weeks 3–4 | Complete engineering and safety review; mount approved external sensors and gantry concepts during scheduled maintenance. | Formal installation record and commissioning checklist. |
| 3. Shadow-mode baseline logging | Weeks 5–6 | Log passive telemetry across startup, steady rolling, shutdown, and multiple billet SKUs. | CSV/JSON baseline dataset with synchronized operating data. |
| 4. Controlled evaluation and ROI audit | Weeks 7–8 | Evaluate approved interventions under a controlled test plan and train authorized operators. | PoC sign-off report, measured performance, false-alarm review, and ROI assessment. |

Illustrative targets—such as SNR above 18 dB, 100+ rolling cycles, 60% alarm reduction, or sub-four-hour installation—must be treated as proposal targets until demonstrated at the selected site.

## 5. Software, Edge Firmware & Digital Twin

1. **C++17 edge-controller example** (`firmware/ae_edge_filter.cpp`)
   - Illustrates >150 kHz validity gating, 68 dB AE threshold evaluation, debris and temperature checks, and relay-style outputs.
   - It does not provide a certified filter, real-time hardware interface, fail-safe state machine, or actuator feedback.

2. **Python SCADA telemetry simulator** (`src/mandrel_monitor.py`)
   - Generates startup, high-speed, and shutdown test frames.
   - Demonstrates simple status output and alarm text.
   - Modbus TCP, OPC UA, and 4–20 mA integration would require platform-specific implementation and validation.

3. **Interactive web digital twin** (`index.html`)
   - Animated SVG gantry and compound-lever concept
   - Simulated KPI cards and AE chart
   - English, Hindi, and Odia technical tabs
   - CSV and JSON telemetry export

## 6. Detailed PoC Cost Breakdown (Indicative)

All costs are preliminary planning estimates in Indian Rupees (INR) for a single-stand pilot. Final pricing requires vendor quotations, taxes, structural design, plant integration, and site-specific installation work.

| Item | Component / Subsystem | Technical scope | Qty | Indicative cost |
|---:|---|---|---:|---:|
| 1 | Industrial AE sensor and pre-amplifier | 100 kHz–1 MHz, IP68, rugged thermal construction, mounting and armored cable | 1 set | ₹75,000 |
| 2 | Inline wear-debris and temperature sensor | Particle counting plus RTD/temperature sensing in the return line | 1 unit | ₹65,000 |
| 3 | Overhead gantry and hydraulic lift kit | Structural beam, cylinders, mechanical stops, and tie rods | 1 assembly | ₹60,000 |
| 4 | Dual-side ground lever-gear linkage | Cross-shaft, reduction gears, ratchet controls, and hydraulic valve | 1 set | ₹35,000 |
| 5 | Edge gateway and DAQ controller | High-speed acquisition, processor, industrial enclosure, plant interface | 1 unit | ₹35,000 |
| 6 | Installation, calibration, and PoC testing | Mounting, commissioning, baseline work, and test reporting | Lump sum | ₹25,000 |
| | **Indicative total PoC investment** | **Complete pilot scope for one stand** | | **₹2,95,000** |

## 7. Preliminary Return on Investment

The proposal assumes that a major bearing incident can halt a line for approximately 8–16 hours and cost about ₹6,00,000–₹9,00,000 in lost production and recovery. The supplied planning case estimates annual savings of ₹14,00,000–₹18,00,000 per stand and a payback below three months.

These are not measured results. A site-specific ROI study must use actual downtime, failure frequency, lost-tonnage value, replacement cost, labor, lubrication, liner life, and implementation cost.

## 8. Repository Structure

```text
AEGIS-M1-Mandrel-Bearing-Guard/
├── README.md
├── index.html
├── firmware/
│   └── ae_edge_filter.cpp
└── src/
    └── mandrel_monitor.py
```

## 9. Quick Start

### Browser dashboard

1. Open the GitHub Pages link above, or download `index.html` and open it in a browser.
2. Select Auto Cycle, Startup, High-Speed, or Shutdown.
3. Toggle the Gantry Lever demo.
4. Export simulated records as CSV or JSON.

All sensor values in the dashboard are simulated and have no connection to actual mill equipment.

### C++ demonstration

```bash
g++ -std=c++17 -O2 firmware/ae_edge_filter.cpp -o ae_edge_filter
./ae_edge_filter
```

### Python demonstration

```bash
python3 src/mandrel_monitor.py
```

## 10. GitHub Pages Setup

1. Open **Settings → Pages** in this repository.
2. Under **Build and deployment**, select **Deploy from a branch**.
3. Select `main` and `/ (root)`, then save.
4. Wait for the Pages deployment to complete on the **Actions** tab.
5. Open the repository-specific Pages URL:
   https://bhuyanamitnishanka-debug.github.io/AEGIS-M1-Mandrel-Bearing-Guard/

GitHub Pages requires lowercase `index.html` in the repository root. A private repository may require a GitHub plan that includes private Pages access or restricted Pages behavior. If deployment fails, inspect **Actions → pages-build-deployment** or the current Pages workflow logs.

## Formal Submission Letter: Tata InnoVerse

**To:**  
The Evaluation & Open Innovation Committee  
Tata InnoVerse Open Innovation Portal

**Subject:** Submission of Proof-of-Concept Solution — AEGIS-M1, Non-Intrusive Condition Monitoring and Overhead Gantry Hydraulic-Lever System for Rolling Stand Mandrel Plain Bearings

Respected Sir/Madam,

I am pleased to submit my engineering Proof-of-Concept solution, AEGIS-M1, in response to the industrial challenge concerning mandrel plain-bearing failure prevention in high-speed rolling mill stands.

In continuous hot rolling operations, mandrel plain bearings depend on effective lubrication to separate the rotating roll shaft from the bearing liner. During transient low-RPM startup and coast-down regimes, lubrication conditions may change and permit boundary contact, wear, debris, and interruption of production. Housing clearances, operating temperatures of 45–80°C, mill scale, cooling-water spray, and gear vibration can make conventional intrusive sensing impractical.

AEGIS-M1 proposes a three-pillar engineering architecture:

1. **External Acoustic-Emission Sensing:** A rugged piezoelectric AE transducer mounted outside the eccentric housing could investigate ultrasonic stress waves associated with rubbing, while a high-pass stage removes lower-frequency background vibration.
2. **Inline Oil Debris and Thermal Telemetry:** An external debris counter and temperature probe could quantify metallic particles and monitor oil condition in the return line.
3. **Overhead Gantry and Safe-Distance Lever-Gear Concept:** Cylinders mounted on an overhead gantry could provide a controlled load-relief concept. Synchronized ground-level controls could allow an operator to act at a safe distance. Real implementation requires structural, hydraulic, and functional-safety validation.

An interactive digital twin, animated gantry and lever blueprint, C++17 edge-code example, Python telemetry simulator, and CSV/JSON export have been developed and documented in the accompanying repository.

I look forward to the opportunity to demonstrate the concept and discuss a supervised feasibility pilot.

Sincerely,

**Amit Nishanka Bhuyan**  
Lead System Designer & Independent AI/Hardware Researcher  
Salipur, Cuttack, Odisha, India

**GitHub Repository:** https://github.com/bhuyanamitnishanka-debug/AEGIS-M1-Mandrel-Bearing-Guard  
**Live Interactive Dashboard:** https://bhuyanamitnishanka-debug.github.io/AEGIS-M1-Mandrel-Bearing-Guard/

## Author & Attribution

**Amit Nishanka Bhuyan** — Lead System Designer & Independent AI/Hardware Researcher

Licensed under the MIT License. See [LICENSE](LICENSE).

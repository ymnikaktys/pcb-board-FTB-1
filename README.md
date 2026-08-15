# High-Power PDB for 7" Experimental Drone Testbed (v1.0)

A custom power distribution board (PDB) with integrated filtering and surge protection, designed for a 7" experimental drone testbed (high-current loads up to 150A) and onboard companion logic.

Developed in Altium Designer. Hardware verification and transient analysis performed in QSPICE.

---

## 🛠 Hardware Specs

* **Copper Topology:** 4-Layer, 2 oz (70 µm) copper stackup with solid ground planes to minimize loop inductance and thermal dissipation on high-current traces.
* **Input Voltage:** 6S Li-Ion / LiPo (25.2V nominal, surge tolerant up to 35V).
* **Power Rail (VBAT / ESC):**
  * Peak Current: up to 150A pulse load.
  * Direct heavy-gauge solder pads for XT90-S (Anti-Spark) input and ESC power lines.
  * Bulk DC-Link: 4x 390 µF Low-ESR electrolytic capacitor array (1560 µF total).
  * High-Frequency Snubbing: 5x 22 µF 1210 MLCC ceramic array directly at the input rail.
* **TVS Protection:**
  * SMCJ26A bidirectional/unidirectional TVS diode clamping inductive spikes and regenerative braking overvoltage below 31.7V.
* **Logic & Peripheral Power Supply:**
  * Dedicated high-current pads for external Hobbywing 5A UBEC (5V_Logic rail).
  * Direct interface headers for **Orange Pi 5 Pro** (AI Companion PC), **Beitian M10 GPS**, and **ELRS Receiver**.
  * Damped series termination resistors (47 Ohm) on MAVLink UART lines for Ground Bounce protection.
* **Analog Video LC Filter:**
  * Shielded inductor (33 µH / 1.5A) + damped multi-stage ceramic filter providing -20 dB attenuation at 24 kHz and -33 dB at 48 kHz PWM switching frequency.
  * Star-ground isolation (`Video_GND`) via Net Tie (`NT1`) dedicated to **Rush Tank Solo 1.6W VTX** and **Caddx Ratel 2** camera.

---

## 📁 Repository Structure

```text
├── Hardware/
│   ├── PDB_Core_6S2P_v1.0.PrjPcb    # Main Altium project
│   ├── PDB_Schematic_v1.0.SchDoc    # Schematic document
│   └── PDB_Layout_2oz_v1.0.PcbDoc   # PCB layout document
├── Libraries/
│   ├── PDB_Components.SchLib        # Custom SCH library
│   └── PDB_Footprints_v1.0.PcbLib   # Custom PCB footprint library
├── Manufacturing/                    
│   └── Gerber_NC_Drill_v1.0.zip     # Production files
├──Simulations/
│   ├── MACRO.qsch                             # Full-system 6S2P power network macro-model & voltage sag analysis
│   ├── ESC_HF_PhaseShift_v1.0.qsch            # High-frequency MOSFET half-bridge inverter, switching ringing & snubber
│   ├── lc_filter_video.qsch                   # AC Bode analysis & PWM ripple attenuation for the video LC filter
│   ├── INRUSH CURRENT no deff.qsch            # Unprotected hot-plug inrush current transient (336A peak surge)
│   ├── INRUSH CURRENT wth deff.qsch           # Soft-start pre-charge simulation modeling XT90-S Anti-Spark behavior (4.5A)
│   ├── Power Integrity — PI.qsch              # 5V digital logic rail stability under pulsed NPU load (YOLOv8 inference)
│   └── Ground_Bounce_on_UART.qsch             # MAVLink telemetry UART Ground Bounce & signal integrity analysis
│── Simulations QSPICE.pdf                 # Full 45-page engineering calculations & simulation report (russion language)
├── top_layer.png                              # Top layer PCB preview image
├── bottom_layer.png                           # Bottom layer PCB preview image
└── README.md

# High-Power PDB for 7" Experimental Drone Testbed (v1.0)

A custom power distribution board (PDB) with integrated filtering and surge protection, designed for a 7" experimental drone testbed (high-current loads up to 150A) and onboard companion logic.

Developed in Altium Designer.

---

## 🛠 Hardware Specs

* **Copper Topology:** 2 Layer, 2 oz (70 µm) copper to reduce resistance and heat on the power planes.
* **Input Voltage:** 6S Li-Ion / LiPo (up to 25.2V nominal / pulses up to 30V+).
* **Power Rail (VBAT / ESC):**
  * Peak Current: up to 150A (3-5 sec pulse mode).
  * Direct integration of XT90-S connector pads and ESC power output.
  * Battery Filter: 4x low-inductance electrolytic capacitor array.
* **TVS Protection:**
  * SMCJ26A input suppressor for damping regenerative voltage spikes from 1900KV brushless motors during hard braking or throttle bursts.
* **Logic & Peripheral Power Supply:**
  * Integrated UBEC Hobbywing 5A module (5V_Logic output).
  * Ceramic LC filter for protecting Orange Pi Zero 3 and FC power supply from high-frequency PWM noise.
* **GND Isolation:**
  * Separation of power ground (`GND`) and clean Video/Logic circuit (`Video_GND`) via `Net Tie` component (`NT1`) to eliminate interference on the analog video line.
* **Interfaces:**
  * 17-pin PC connection hub (`SpeedyBee F405 V3`).
  * 8-pin `JST-SH` connector for connecting peripherals and VTX (`Rush Tank Solo 1.6W`).

---

## 📁 Repository Structure

```text
├── Hardware/
│   ├── PDB_Core_6S2P_v1.0.PrjPcb   # Main Altium project
│   ├── PDB_Schematic_v1.0.SchDoc    # Schematic document
│   └── PDB_Layout_2oz_v1.0.PcbDoc   # PCB layout document
├── Libraries/
│   ├── PDB_Components.SchLib        # Custom SCH library
│   └── PDB_Footprints_v1.0.PcbLib   # Custom PCB footprint library
├── Manufacturing/                   # Gerber & NC Drill (generated before production)
└── README.md

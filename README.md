# 🔥 Spatially Varying Wall Temperature Simulation using SU2

<div align="center">

![SU2](https://img.shields.io/badge/Solver-SU2%20CFD-blue?style=for-the-badge&logo=airplayvideo&logoColor=white)
![Python](https://img.shields.io/badge/Wrapper-Python-yellow?style=for-the-badge&logo=python&logoColor=white)
![RANS](https://img.shields.io/badge/Model-RANS%20%7C%20SST-green?style=for-the-badge)
![Flow](https://img.shields.io/badge/Flow-Compressible-red?style=for-the-badge)
![Mach](https://img.shields.io/badge/Mach-0.03059-orange?style=for-the-badge)

<br/>

```
  Freestream  ──────────────────────────────────────►
              ┌─────────────────────────────────────┐
              │           Fluid Domain              │
              └─────────────────────────────────────┘
                500 K ──────► 600 K ──────► 700 K
                  ●══════════════════════════●
               Leading                   Trailing
                Edge                       Edge
```

> **Compressible turbulent flat plate CFD simulation** using the **SU2 Python wrapper** to impose a spatially varying wall temperature — demonstrating dynamic boundary condition control during runtime.

</div>

---

## 📌 Project Idea

Typical CFD simulations use a **constant wall temperature**.  
In this study, the temperature **changes continuously along the plate**.

The wall temperature is defined as:

$$T_{wall}(s) = 500 + 200x$$

where $x$ = normalized position along the plate (0 → 1)

### 🌡️ Temperature Distribution

| 📍 Plate Position  | 🌡️ Temperature | 📊 Gradient |
|-------------------|---------------|-------------|
| **Leading Edge**  | 500 K         | ░░░░░░░░░░  |
| **Middle**        | 600 K         | ░░░░░█████  |
| **Trailing Edge** | 700 K         | ██████████  |

> This represents a **heated plate with increasing temperature downstream**, similar to many thermal engineering and aerospace applications.

---

## 🧠 Physics Model

| ⚙️ Parameter              | 📋 Value          |
|--------------------------|------------------|
| **Solver**               | RANS             |
| **Turbulence Model**     | k–ω SST          |
| **Flow Type**            | Compressible     |
| **Mach Number**          | 0.03059          |
| **Freestream Temperature** | 293.15 K       |
| **Freestream Pressure**  | 101,325 Pa       |

---

## 🧩 How the Python Wrapper Works

Instead of defining wall temperature in the `.cfg` file, the **Python wrapper updates the boundary condition every time step**:

```python
s = float(iVertex) / float(nVertex_CHTMarker)

WallTemp = 500.0 + 200.0 * s

SU2Driver.SetMarkerCustomTemperature(CHTMarkerID, iVertex, WallTemp)
```

> Every node on the plate receives a **different temperature value** depending on its location — enabling fully dynamic boundary condition control at runtime.

### 🔄 Wrapper Execution Flow

```
  SU2 Time Step Begins
         │
         ▼
  Python loops over all wall nodes
         │
         ▼
  Computes s = iVertex / nVertex  (0 → 1)
         │
         ▼
  WallTemp = 500 + 200 × s
         │
         ▼
  SetMarkerCustomTemperature(node, WallTemp)
         │
         ▼
  SU2 solves with updated BCs
         │
         ▼
  Next Time Step ──────────────► repeat
```

---

## 🧱 Mesh

Flat plate mesh generated using **quadrilateral elements** with expected boundary layer formation along the plate.

```
  Freestream
  ──────────────────────────────────►
  ┌──────────────────────────────────┐
  │                                  │
  │          Fluid Domain            │
  │                                  │
  └──────────────────────────────────┘
  ════════════════════════════════════
                Flat Plate
       500 K  ──────────────►  700 K
```

---

## ⚙️ Running the Simulation

```bash
python launch_unsteady_CHT_FlatPlate.py -f unsteady_CHT_FlatPlate_Conf.cfg
```

---

## 🔬 Key Observations

| 🔍 Observation | 💡 Description |
|---------------|----------------|
| 📏 **Boundary Layer** | Develops continuously along the flat plate |
| 🌡️ **Temperature Gradient** | Induces heat transfer along the surface |
| 🌀 **Turbulence Capture** | SST model accurately captures near-wall behavior |
| 🐍 **Python Control** | Wrapper enables dynamic boundary condition updates per step |

---

## 🚀 Applications

This type of simulation is useful for:

| 🏭 Field | 🎯 Application |
|---------|---------------|
| 🚀 **Rocket Engineering** | Nozzle cooling analysis |
| ✈️ **Turbomachinery** | Turbine blade thermal studies |
| 🛸 **Hypersonics** | Vehicle surface heating prediction |
| 🔁 **Heat Transfer** | Conjugate heat transfer studies |

---

## 🛠️ Tools Used

| 🔧 Tool       | 💡 Purpose                          |
|--------------|-------------------------------------|
| **SU2**      | CFD solver                          |
| **Python**   | Boundary condition control at runtime |
| **ParaView** | Flow field visualization            |

---

## 👨‍💻 Author

<div align="center">

### **Harsha**
*Mechanical Engineering*

[![GitHub](https://img.shields.io/badge/GitHub-harshaverse-black?style=for-the-badge&logo=github)](https://github.com/harshaverse)

🛩️ Aerodynamics &nbsp;|&nbsp; 💻 CFD &nbsp;|&nbsp; 🚀 Rocket Propulsion &nbsp;|&nbsp; ⚡ High-Performance Simulation

</div>

---

## ⭐ Acknowledgment

> Based on the **SU2 Python wrapper tutorial example** from the [SU2 Foundation](https://github.com/su2code/SU2).

---

<div align="center">

🌡️ **From 500 K to 700 K — one plate, one gradient, infinite possibilities.**

<sub>Built with ❤️ using SU2 + Python | Dynamic Boundary Condition Control via Python Wrapper</sub>

</div>

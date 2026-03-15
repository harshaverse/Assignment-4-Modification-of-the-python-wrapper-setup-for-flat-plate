🔥 Spatially Varying Wall Temperature Simulation using SU2

Computational Fluid Dynamics simulation of a compressible turbulent flat plate using the SU2 Python wrapper to impose a spatially varying wall temperature.

This project demonstrates how Python can dynamically control boundary conditions inside SU2 during runtime.

📌 Project Idea

Typical CFD simulations use constant wall temperature.
In this study, the temperature changes continuously along the plate.

The wall temperature is defined as

𝑇 
𝑤
𝑎
𝑙
𝑙
(
s
)
=
500
+
200
x
	​

(s)=500+200x

where

x = normalized position along the plate (0 → 1)

Temperature distribution
Plate Position	Temperature
Leading Edge	500 K
Middle	600 K
Trailing Edge	700 K

This represents a heated plate with increasing temperature downstream, similar to many thermal engineering and aerospace applications.

🧠 Physics Model Parameter	Value

Solver	RANS

Turbulence Model  𝑘−𝜔 SST 

Flow Type	Compressible

Mach Number	0.03059

Freestream Temperature	293.15 K

Freestream Pressure	101325 Pa

🧩 How the Python Wrapper Works

Instead of defining wall temperature in the .cfg file,
the Python wrapper updates the boundary condition every time step.

s = float(iVertex)  /  float(nVertex_CHTMarker)

WallTemp = 500.0 + 200.0 * x

SU2Driver.SetMarkerCustomTemperature(CHTMarkerID, iVertex, WallTemp)

This means every node on the plate receives a different temperature value depending on its location.

🧱 Mesh

Flat plate mesh generated using quadrilateral elements.

Expected boundary layer formation along the plate.

Freestream
------------------------------------>
 _________________________________
|                                 |
|           Fluid Domain          |
|_________________________________|
            Flat Plate

⚙️ Running the Simulation

python launch_unsteady_CHT_FlatPlate.py -f unsteady_CHT_FlatPlate_Conf.cfg

🔬 Key Observations

• Boundary layer develops along the flat plate
• Temperature gradient induces heat transfer along the surface
• Turbulence model captures near-wall behavior
• Python wrapper enables dynamic boundary condition control

🚀 Applications

This type of simulation is useful for

rocket nozzle cooling analysis

turbine blade thermal studies

hypersonic vehicle heating

conjugate heat transfer studies

🛠 Tools Used

SU2	CFD Solver
Python	Boundary condition control
ParaView	Visualization

👨‍💻 Author

Harsha
Mechanical Engineering

Interests:

Aerodynamics

CFD

Rocket propulsion

High performance simulation

⭐ Acknowledgment

Based on the SU2 Python wrapper tutorial example
from the SU2 Foundation.

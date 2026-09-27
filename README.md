# 3-Cell Hybrid Battery Thermal Management System (BTMS) CFD Simulation

![Ansys Fluent](https://img.shields.io/badge/CFD%20Solver-Ansys%20Fluent%202026%20R1-orange.svg)
![Domain](https://img.shields.io/badge/Domain-Conjugate%20Heat%20Transfer%20%28CHT%29-blue.svg)
![Phase Change](https://img.shields.io/badge/Thermal%20Buffer-PCM%20Melting%2FSolidification-green.svg)
![Application](https://img.shields.io/badge/Target-High--Discharge%20Drone%2FUAV%20Battery%20Packs-purple.svg)

A transient 3D Computational Fluid Dynamics (CFD) study evaluating a hybrid Phase Change Material (PCM) and forced convective air-cooling thermal management architecture for high-discharge cylindrical lithium-ion battery modules (18650 / 21700).

---

## 📌 Executive Summary
High C-rate discharges during aggressive UAV flight profiles generate intense localized Joule heating. This project models a passive-active hybrid BTMS pairing paraffin-based latent heat absorption jackets with an axial forced-air convection channel to ensure:
* Cell core and surface temperatures stay strictly within the optimal electrochemical operational window ($20^\circ\text{C} - 45^\circ\text{C}$).
* Mitigation of localized hotspot development and elimination of thermal runaway triggers ($>60^\circ\text{C}$).
* Thermal buffering via phase-change enthalpy absorption during transient heat spikes.

---

## 📥 Mesh & Solved Case Downloads (External Storage)
Due to GitHub browser upload limits (>25 MB), the heavy volumetric mesh and solved 3D transient solver case files are hosted on Google Drive:

* 🔗 **[Download Full Computational Volume Mesh (.msh - 116 MB)](https://drive.google.com/file/d/1ADYtc77lUDDHQwe-2Etr8EQA6WPn3gBg/view?usp=sharing)**
* 🔗 **[Download Solved Fluent Case Database (.cas.h5 - 56 MB)](https://drive.google.com/file/d/1onvHrmzy_ZYZvRdyciZXpNUiEOiPKcEI/view?usp=sharing)**

---

## 🔬 Computational Methodology & Physics Setup

| Physics Domain | Formulation / Governing Model | Discretization Scheme |
| :--- | :--- | :--- |
| **Fluid Flow** | Incompressible Navier-Stokes (Pressure-Based Solver) | Second-Order Upwind |
| **Turbulence** | Standard $k$-$\epsilon$ ($ske$) with Enhanced Wall Treatment | Coupled Pseudo-Transient |
| **Heat Transfer** | Conjugate Heat Transfer (CHT) across Solid-Fluid Interfaces | Second-Order Energy |
| **Phase Transition** | Solidification & Melting (Enthalpy-Porosity Formulation) | Mushy Zone Constant: $10^5$ |

* **Mesh Architecture:** Conformal polyhedral/hybrid computational volume mesh with inflation prism boundary layers along cell walls and PCM-duct interfaces to resolve viscous sublayers.
* **Boundary Conditions:**
  * **Inlet:** Velocity inlet ($3.0\text{ m/s} - 10.0\text{ m/s}$ convective air stream at $300\text{ K}$).
  * **Outlet:** Gauge pressure outlet ($0\text{ Pa}$).
  * **Cell Core:** Volumetric heat source generation corresponding to continuous high C-rate discharge.

---

## 📂 Repository Layout

```text
├── cad_and_mesh/
│   ├── 3_Cell_BTMS_Geometry.glb         # 3D interactive assembly asset
│   ├── 3_Cell_BTMS_Geometry.png         # CAD assembly preview image
│   └── 3_Cell_BTMS_Setup_Mesh.set       # Solver execution settings file
│
├── results/
│   ├── figures/                         # CFD contour plots and vector fields
│   │   ├── 3_Cell_BTMS_Geometry_Overview.png.png
│   │   ├── Area Average of Temperature on cell_boundary.png
│   │   ├── Area Average of Temperature on pcm_boundary.png
│   │   ├── Battery_Cells_3D.png
│   │   ├── Battery_Thermal_Midplane.png
│   │   ├── BTMS_3D_Coolant_Heat_Streamlines.png
│   │   ├── Complete_BTMS_Assembly.png
│   │   ├── Coolant_Pressure_Distribution.png
│   │   ├── Coolant_Streamlines_3D.png
│   │   ├── Coolant_Velocity_Vectors.png
│   │   ├── Coolant_Velocity_Vectors_Midplane.png
│   │   ├── Maximum Value of Temperature on cell_boundary.png
│   │   ├── Minimum Value of Temperature on cell_boundary.png
│   │   ├── PCM_Melting_Liquid_Fraction.png
│   │   └── PCM_Thermal_Absorption.png
│   └── data/                            # Transient solution monitor logs and profiles
│       ├── Battery_Axial_Height_Temperature_Plot.csv
│       ├── Battery_PCM_Temperature_Line_Plot.csv
│       ├── cell_temperature_history.out
│       ├── coolant_outlet_temperature.out
│       ├── parametric_design_points.csv
│       ├── pcm_liquid_fraction_history.out
│       ├── system_total_temperature.out
│       └── TempProfile.csv
│
├── docs/
│   ├── GenericReport/                   # Ansys Workbench automated audit assets
│   │   ├── ansys-part-of-synopsys-238x80.jpg
│   │   ├── Figure001.avz
│   │   ├── Figure001.png
│   │   ├── Figure002.avz
│   │   ├── Figure002.png
│   │   ├── Figure003.avz
│   │   └── Figure003.png
│   ├── GenericReport.html               # Main Workbench summary report
│   ├── cfd_post_visualization_state.cst # CFD-Post session state file
│   └── fluent_solver_summary.xml        # Solver setup audit log
│
└── README.md

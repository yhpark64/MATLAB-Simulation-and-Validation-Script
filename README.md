# Flexible Robot Dynamics and Control Simulation

[![License: GPL v2.0](https://img.shields.io/badge/License-GPL%20v2.0-blue.svg)](https://www.gnu.org/licenses/gpl-2.0)
[![MATLAB](https://img.shields.io/badge/MATLAB-R2023b%2B-orange)](https://www.mathworks.com/)

## Overview

This repository contains the core MATLAB implementation for the modeling, simulation, and control of flexible-link manipulators subject to large loads. This code accompanies the Ph.D. thesis **"Modelling and Control of Flexible Robots Subject to Large Loads: Application to Remote Handling"** by Younghwa Park.

The software implements a **Floating Frame of Reference (FFR)** formulation combined with **Craig-Bampton model order reduction** to simulate high-fidelity flexible dynamics in real-time. It includes a symbolic derivation of the Equations of Motion (EoM) and a Control Barrier Function (CBF) based controller.

## Features

* **FEA Integration:** Imports STL geometry and generates a quadratic tetrahedral mesh using the MATLAB PDE Toolbox.
* **Model Order Reduction:** Implements the Craig-Bampton method to reduce thousands of nodal degrees of freedom (DoFs) to a minimal set of rigid and modal coordinates.
* **Symbolic Dynamics:** Automatically derives the Lagrangian dynamics and Equations of Motion (EoM) using the MATLAB Symbolic Math Toolbox.
* **Stiff Solver Implementation:** Utilizes an L-stable integration scheme (`ode15s`) to handle the ill-conditioned mass matrices inherent in flexible multibody systems.
* **Validation:** Includes built-in benchmark data to validate results against commercial ANSYS Motion software.

## Prerequisites

To run this code, you need:

* **MATLAB** (R2021a or newer recommended)
* **Partial Differential Equation Toolbox** (for FEA meshing)
* **Symbolic Math Toolbox** (for deriving EoM)
* **Control System Toolbox** (optional, for advanced analysis)

## Installation & Usage

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/your-username/flexible-robot-dynamics.git](https://github.com/your-username/flexible-robot-dynamics.git)
    cd flexible-robot-dynamics
    ```

2.  **Setup Geometry:**
    Ensure the CAD file `cad/Part1.STL` is in the correct directory relative to the script.

3.  **Run the Simulation:**
    Open `baem7.m` in MATLAB and run the script.
    ```matlab
    >> beam7
    ```

    *Note: The first run may take several minutes as the code generates the mesh and performs the symbolic derivation. Subsequent runs can be accelerated by loading the pre-computed `sorosim.mat` if saved.*

## Code Structure

The main script is organized into the following sections:

1.  **Finite Element Model Generation:** Meshing and material property assignment.
2.  **Model Order Reduction:** Computation of component modes and reduced stiffness/mass matrices.
3.  **Symbolic Equations of Motion:** derivation of kinetic ($T$) and potential ($V$) energy.
4.  **Control Formulation:** Assembly of the affine control system $\dot{x} = f(x) + g(x)u$.
5.  **Numerical Simulation:** Time-domain integration.
6.  **Validation:** Plotting results against hard-coded ANSYS benchmark data.

## Validation Results

The simulation validates the proposed model against high-fidelity ANSYS Motion data. The script generates plots for:
* **Rigid Body Motion:** Verifying the kinematic transport.
* **Tip Deflection:** Validating the geometric stiffness under gravity.
* **Tip Acceleration:** Demonstrating the solver's ability to filter high-frequency noise.

## Citation

If you use this code in your research, please cite the associated thesis:

```bibtex
@phdthesis{Park2026,
  author  = {Younghwa Park},
  title   = {Modelling and Control of Flexible Robots Subject to Large Loads: Application to Remote Handling},
  school  = {University of Southern Denmark},
  year    = {2026},
  month   = {February}
}

# Simulation of a Schwarzschild Black Hole
### The Deflection of Light Around a Black Hole

**Author:** Sara Carlos Cardoso
**Institution:** Universidade de Aveiro, Departamento de Física (2024/2025)
**Supervisor:** Dr. Mercè Guerrero Román 

---

## Overview

This repository contains a Python notebook that implements a numerical ray-tracing framework to simulate photon trajectories in Schwarzschild spacetime. 

The primary goal of this project is to understand how the curvature of spacetime around a non-rotating black hole governs the fate of light rays. Furthermore, the simulation reproduces key observational features—such as the black hole shadow, lensing ring, and photon ring—that have gained renewed attention following the groundbreaking Event Horizon Telescope (EHT) results in 2019.

This work is heavily based on the theoretical framework developed in:
> **Gralla, Holz & Wald (2019)**, *Black Hole Shadows, Photon Rings, and Lensing Rings*, PRD 100, 024018.

---

## Theoretical Background

### The Schwarzschild Metric
The Schwarzschild solution is the unique spherically symmetric, static, vacuum solution to the Einstein Field Equations (setting $G = c = 1$). Two radii are of special importance in this metric:
* **Event Horizon ($r_s = 2M$):** The one-way causal boundary where no signal can escape.
* **Photon Sphere ($r_p = 3M$):** The radius of unstable circular photon orbits.
* **Critical Impact Parameter ($b_c = 3\sqrt{3}\,M \approx 5.196\,M$):** The boundary that separates captured rays from escaping rays.

### Null Geodesics & Photon Classification
The geodesic equation for a massless photon moving in the equatorial plane reduces to a single first-order ODE. Based on the impact parameter $b$ and the number of equatorial plane crossings $n$, photon trajectories fall into three distinct classes:

1.  **Direct Rays (Blue/Grey):** $n < 3/4$. These rays experience a single gravitational deflection and escape to infinity (or are absorbed if $b < b_c$).
2.  **Lensed Rays (Orange):** $3/4 < n < 5/4$. These rays wrap partially around the black hole before escaping, producing a demagnified image of the surrounding disk (the lensing ring).
3.  **Photon Ring Rays (Red):** $n > 5/4$. These rays orbit very close to the photon sphere ($r = 3M$) before either escaping or falling in, producing an extremely narrow, bright feature.

---

## Numerical Implementation

### Ray-Tracing Method
The simulation integrates the orbit equation $d\varphi/dr$ numerically using `scipy.integrate.solve_ivp` with the `DOP853` method (an explicit 8th-order Runge–Kutta scheme with adaptive step-size control). 

Each trajectory is evaluated in two segments:
1.  **Inbound Segment:** From $r_{\rm start} = 50\,M$ inward to the turning point $r_{\rm turn}$ (or the event horizon for absorbed rays).
2.  **Outbound Segment:** From $r_{\rm turn}$ back out to $r_{\rm final} = 50\,M$.

The turning point is found by scanning the effective potential for sign changes and refining the result using Brent's method (`scipy.optimize.brentq`). To ensure accuracy, numerical tolerances are tightened near the photon sphere where the potential is nearly flat.

---

## Outputs and Visuals

When running the simulation, the framework categorises and plots the rays based on their theoretical classification:
* **Direct Rays Plotting:** Evaluates 180 trajectories.
* **Lensed Rays Plotting:** Evaluates 112 trajectories.
* **Photon Ring Rays Plotting:** Evaluates 41 trajectories.


---

## Usage

1. Clone this repository.
2. Ensure you have Jupyter Notebook or JupyterLab installed.
3. Install required Python packages (e.g., `numpy`, `scipy`, `matplotlib`).
4. Run `Trajectories - Schwarszchild.ipynb`.

# Pharmacokinetic Modeling of Chiral Inversion: An ODE Simulation of (R)-Ibuprofen

## Project Overview
This project models the dynamic, unidirectional metabolic inversion of the inactive $(R)$-ibuprofen enantiomer into the therapeutically active $(S)$-enantiomer within the human hepatic system. Utilizing a deterministic one-compartment pharmacokinetic framework, this simulation demonstrates how endogenous enzymes (specifically $\alpha$-methylacyl-CoA racemase, or AMACR) actively refine racemic pharmaceutical mixtures.

---

## The Mathematical Framework

The system is governed by a set of coupled, first-order linear ordinary differential equations (ODEs) balancing concurrent hepatic inversion and renal clearance:

### Inactive Enantiomer Decay
$$\frac{dR}{dt} = -k_{inv}R$$

### Active Enantiomer Balancing
$$\frac{dS}{dt} = k_{inv}R - k_{el}S$$

### Analytical Solution (Derived via Integrating Factor)
By applying an integrating factor $I_F = e^{k_{el}t}$ to the coupled system, the exact kinetic path of the active drug payload over time is determined analytically:

$$S(t) = \left( S_0 - \frac{k_{inv} R_0}{k_{el} - k_{inv}} \right) e^{-k_{el} t} + \left( \frac{k_{inv} R_0}{k_{el} - k_{inv}} \right) e^{-k_{inv} t}$$

---

## Numerical Simulation (Euler's Method)

To approximate continuous calculus within a spreadsheet architecture, the system was discretized using Euler's Method with a step size of $\Delta t = 0.1 \text{ hours}$:

* $R(t + \Delta t) = R(t) + (-k_{inv} R(t)) \Delta t$
* $S(t + \Delta t) = S(t) + (k_{inv} R(t) - k_{el} S(t)) \Delta t$

### Simulation Parameters (Healthy Adult Baseline)
* **Initial Dose ($R_0$ / $S_0$):** $200\text{ mg}$ / $200\text{ mg}$ (Standard $400\text{ mg}$ racemic mix)
* **Inversion Rate ($k_{inv}$):** $0.35\text{ hr}^{-1}$
* **Elimination Rate ($k_{el}$):** $0.28\text{ hr}^{-1}$

---

## Results & Visualization

The simulation reveals an immediate exponential decay of the useless $(R)$-enantiomer alongside a paradoxical initial climb in the active $(S)$-enantiomer, peaking at **$208.4\text{ mg}$ at $t = 1.1\text{ hours}$**. This explicitly validates that endogenous generation temporarily outpaces systemic clearance. Total metabolic clearance hits **$99.72\%$** at the 24-hour mark.

![Pharmacokinetic Profile](Graph.png)

*Note: The complete step-by-step dataset can be found in the `ibuprofen_simulation_data.xlsx` file included in this repository.*

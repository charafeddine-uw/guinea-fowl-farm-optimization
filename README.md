# Guinea Fowl Farm Optimization

**A multi-period mixed-integer linear programming project using Python and PuLP.**

**Authors**
- Mohamed Khalid KACIMI
- Charafeddin El AKKAD

## Overview

This academic operations research project develops a decision-support model for a guinea fowl farm over **five years**, divided into **15 periods of four months**. The goal is to maximize the farm's final economic wealth: the cash balance plus the residual value of the remaining livestock.

The model chooses how many eggs, chicks, young birds, and adult birds to sell or keep in each period, while accounting for reproduction, mortality, available space, incubation capacity, operating costs, transportation costs, and cash availability.

## Main features

- **Mixed-integer linear programming (MILP)** with integer animal and egg counts and continuous cash balances.
- **Sex-specific population tracking:** females lay eggs, while a female-to-male breeding ratio is enforced.
- **Biological transitions:** eggs hatch into chicks; retained chicks become young birds; retained young birds become adults.
- **Operational constraints:** incubation capacity, occupied surface area, and nonnegative cash balances.
- **Transportation costs:** a simplified linear charge based on the total weight of eggs and birds sold, including chicks. The 500 kg reference is used to calculate the price per kilogram; it is **not** a binding shipment-capacity constraint.
- **Scenario analysis:** market demand limits, a minimum cash reserve, and sensitivity to the breeding ratio.

## Mathematical objective

The model maximizes final wealth at the end of period 15:

$$
\max Z = B_{15} + v_A A_{15} + v_J\left(C^P_{15}-M^P_{15}\right)
$$

where $B_{15}$ is the ending cash balance, $A_{15}$ is the adult population at the end of the planning horizon, and $C^P_{15}-M^P_{15}$ represents retained surviving chicks (valued as the next young cohort). This formulation avoids counting surviving young birds twice: they are already included in the end-of-period adult stock under the model's timing conventions.

## Project structure

```text
guinea-fowl-farm-optimization/
├── README.md
├── Projet_pintades.ipynb
├── requirements.txt
└── .gitignore
```

## Installation and execution

1. Install Python 3 and Jupyter Notebook or use VS Code with the Jupyter extension.
2. Install the dependencies:

   ```bash
   python -m pip install -r requirements.txt
   ```

3. Open `Projet_pintades.ipynb`.
4. Select **Restart Kernel and Run All Cells**. The notebook uses the CBC solver distributed with compatible PuLP installations.

The code includes a dependency-installation cell. If the dependencies are already installed, this step can be skipped.

## Results from the supplied notebook

The saved execution of the reference model reports:

| Metric | Reported value |
|---|---:|
| Final wealth | 158,078.21 monetary units |
| Final cash | 106,363.21 monetary units |
| Remaining adult birds | 1,951 |
| Total transportation cost | 607.89 monetary units |

The saved CBC run reports a proven optimum for the **reference model**. Results may differ if parameters, solver settings, or model assumptions are changed. Scenarios with market demand limits yielded feasible solutions, **without proof of optimality** within the configured solution time. These values should not be treated as exact optimal scenario comparisons.

## Assumptions and limitations

**This is an academic simulation, not a validated farming forecast.** Prices, biological rates, livestock weights, sex ratio, and market demand assumptions are illustrative and have not been calibrated against field data. The model also simplifies animal aging, deterministic mortality, and timing within each four-month period. Transportation is charged proportionally to shipment weight rather than by the actual number of vehicle trips.

The final wealth includes the initial resources and residual livestock valuation; it should **not** be interpreted as net profit.

## Tools

Python · PuLP · CBC · pandas · Matplotlib · Jupyter Notebook

## Academic attribution

Developed jointly by **Mohamed Khalid KACIMI** and **Charafeddin El AKKAD** as an operations research project. Both contributors should remain credited in any redistribution or portfolio presentation.

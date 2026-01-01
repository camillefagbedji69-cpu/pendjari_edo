# Project N°28: Dynamical Systems & ODEs for Wildlife Conservation

## 📌 Context & Overview
In the Pendjari National Park (Benin), the survival of large mammals like the African Buffalo (*Syncerus caffer*) depends on a fragile balance between water availability, forage biomass, and anthropogenic pressures. This project moves beyond static observation to **Dynamical System Modeling**, using **Ordinary Differential Equations (ODEs)** to predict long-term ecosystem stability.

## 🎯 Objectives
* **Mechanistic Modeling:** Building a 3-compartment ODE system (Water, Vegetation, Population).
* **Stability Analysis:** Calculating the Jacobian matrix and eigenvalues to determine the system's fate.
* **Management Scenarios:** Identifying critical thresholds for poaching and wildfire management using bifurcation theory.

## 🛠️ Mathematical Framework
We consider the following coupled system:

$$
\begin{cases}
\displaystyle \frac{dW}{dt} = P - (ET + I + R) - c_V V - c_N N \\
\displaystyle \frac{dV}{dt} = r_V V \left(1 - \frac{V}{K_V(W)}\right) - (f + d)V - c W \\
\displaystyle \frac{dN}{dt} = r_N N \left(1 - \frac{N}{K_N(V)}\right) - (m + p)N
\end{cases}
$$

### Key Mathematical Findings:
* **The Extinction Threshold:** Based on current data ($r_N = 0.0678$ vs $m+p = 0.1023$), the biological equilibrium is negative. The system possesses a **globally attractive equilibrium at (0,0,0)**.
* **Poaching Bifurcation:** The critical poaching rate was calculated at $p_{crit} = 0.0405$. Beyond this value, population recovery is mathematically impossible under current birth rates.
* **Jacobian Stability:** Eigenvalue analysis ($\lambda_i < 0$) confirms that the current trend leads to a stable extinction state, necessitating urgent management intervention.
* 
## 💻 Implementation & Simulation
The system was implemented in **Python 3.13** using `scipy.integrate.odeint`.

```python
# Key simulation snippet
def system(y, t, p, f):
    W, V, N = y
    dWdt = P_net - cv*V - cn*N
    dVdt = rv*V*(1 - V/(beta*W)) - (f+d)*V
    dNdt = rn*N*(1 - N/(gamma*V)) - (m+p)*N
    return [dWdt, dVdt, dNdt]

## Key Insights for Conservation
* **The $r_V$ Paradox**: The current vegetation regeneration rate ($0.0005$) is insufficient to offset wildfire and deforestation losses, creating a "resource sink."
* **Conservation Strategy**: A reduction of poaching below $4\%$ and fire management ($f < 0.01$) are the two primary levers identified to flip the system toward a stable positive equilibrium.
## 🔮 Perspectives
* **Stochastic Modeling**: Introducing Brownian motion into the water equation to simulate climate variability (SDEs).
* **Bifurcation Analysis**: Mapping the "Stability Region" in the $(p, f)$ parameter space.
* **Field Validation**: Calibrating $\beta$ and $\gamma$ parameters using multi-year satellite biomass data.

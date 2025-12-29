# Delta Hedging with Transaction Costs and GARCH Volatility

This repository contains a Jupyter notebook that studies the performance of a
delta-hedging strategy for European call options when proportional transaction
costs are present. The analysis is carried out in the framework of the
Clewlow–Hodges **inaction region**, where the hedger rebalances only when the
current delta moves outside a tolerance band.

The objective is not to price options, but to understand how transaction costs
and inaction bands affect:

- the frequency of rebalancing,
- total hedging costs,
- the final profit-and-loss of the writer.

---

## Methodology

### 1. Data and Volatility Estimation
Historical price data are converted into log-returns and used to estimate a
GARCH-type volatility model. An automatic selection routine tries several
specifications and distributions, selecting the best model based on AIC and
parameter significance.

The estimated model is then used to simulate **stochastic, time-varying**
volatility paths.

### 2. Monte Carlo Simulation
Using the simulated volatility, the underlying price is generated under a
Geometric Brownian Motion:

\[
S_{t+1}
=
S_t \exp\!\left[
\left(r - \frac{1}{2}\sigma_t^2\right)\Delta t
+
\sigma_t \sqrt{\Delta t}\, Z_t
\right].
\]

Thousands of paths are simulated to evaluate the hedging strategy.

### 3. Clewlow–Hodges Inaction Region
Instead of continuously hedging, the trader adjusts the hedge only when:

\[
\Delta_t \notin [\Delta_t - \Gamma k,\; \Delta_t + \Gamma k],
\]

where \(k\) is the transaction-cost rate and \(\Gamma\) controls band width.

All trades incur proportional costs, and the cash account accrues interest at
the risk-free rate.

### 4. Evaluation
For each simulation, the P&L of the option writer is computed:

\[
\text{P&L}_T =
C_0 + \text{cash}_T + \Delta_T S_T - (S_T - K)^+.
\]

We report:

- probability of profit,
- probability of exercise,
- number of rebalancings.

---

## Key Findings

- With **zero transaction costs**, the strategy can produce positive P&L in a
meaningful share of scenarios.
- When realistic costs are introduced, the strategy becomes **economically
unsustainable**: trading costs dominate the premium.
- The inaction region reduces trading frequency, but **not enough** to offset
frictions.
- The probability of exercise remains unchanged, since hedging does not affect
the price process.

---

## Disclaimer

This project is intended solely for academic purposes.  
The models rely on simplifying assumptions and do not represent trading advice.
Results illustrate theoretical behaviour and may not be replicable in real
markets.

---

## Requirements

- Python 3.10+
- NumPy  
- Pandas  
- Matplotlib  
- `arch` package  
- Jupyter Notebook  

Install dependencies:

```bash
pip install -r requirements.txt


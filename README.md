# Delta Hedging with Transaction Costs and GARCH Volatility

This project studies how a delta-hedging strategy for European call options behaves when transaction costs are present.  
The goal is not to price options, but to understand how trading frictions affect the strategy.

Specifically, the analysis focuses on three questions:

- How often does the hedge need to be rebalanced?
- How large are the total transaction costs?
- How do these costs impact the final profit-and-loss of the option writer?

---

## Methodology

1. Historical price data are used to estimate a GARCH-type model for volatility.  
2. Using the estimated volatility, many price paths are simulated.  
3. Instead of rebalancing continuously, the hedge is adjusted only when the delta moves outside a tolerance band (the “inaction region”).  
4. For each simulated scenario, the final P&L, the number of rebalancings, and the probability of option exercise are computed.

---

## Key Insights

- With zero transaction costs, the strategy can perform well in some scenarios.  
- Once realistic transaction costs are included, trading expenses dominate and profitability drops.  
- The inaction region helps reduce trading frequency, but usually not enough to offset costs.  
- Hedging does not change the likelihood that the option finishes in the money.

---

## Disclaimer

This project is for academic purposes only.  
The results rely on simplifying assumptions and should not be interpreted as investment advice.

---

## Requirements

- Python 3.10+
- NumPy  
- Pandas  
- Matplotlib  
- `arch`
- Jupyter Notebook

Install dependencies:

```bash
pip install -r requirements.txt

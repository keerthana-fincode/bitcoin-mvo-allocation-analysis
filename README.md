# Asset Allocation Engineering: Stress-Testing the Crypto Diversification Thesis

## Project Overview
ARK Invest’s research suggests that digital assets like Bitcoin introduce structural diversification to multi-asset class portfolios. This project constructs a quantitative portfolio engineering engine to evaluate this thesis using Markowitz Mean-Variance Optimization (MVO). 

The pipeline simulates a 7-asset class universe over a historical window (2018–2023), comparing an empirical 50,000-portfolio Monte Carlo simulation against analytical closed-form tangency solutions to locate the maximum Sharpe ratio boundary.

## Asset Universe & Proxies
The investment universe spans seven global capital vectors, mapping liquid ETFs as strategic proxies:
* **U.S. Equities:** Vanguard S&P 500 ETF (`VOO`)
* **Fixed Income:** iShares Corporate Bond ETF (`LQD`)
* **Real Estate:** iShares U.S. Real Estate ETF (`IYR`)
* **Broad Commodities:** Invesco Optimum Yield ETF (`PDBC`)
* **Currencies:** Invesco DB US Dollar Index Bullish Fund (`UUP`)
* **Precious Metals:** iShares Gold Trust (`IAU`)
* **Alternative Cryptography:** Bitcoin Spot Price (`BTC-USD`)

## Quantitative Allocation Matrix

### Allocation Weights by Optimization Routine
| Asset Proxy | Tangency (Unconstrained) | Tangency (Long-Only) | Global Min Variance | Monte Carlo Max Sharpe |
| :--- | :---: | :---: | :---: | :---: |
| **VOO** (Equities) | +12.77% | +0.00% | +4.39% | +1.15% |
| **LQD** (Corporate Bonds) | +70.49% | +0.00% | +21.02% | +0.89% |
| **IYR** (Real Estate) | -1.31% | +7.52% | +0.00% | +7.17% |
| **PDBC** (Commodities) | -14.98% | +27.05% | +14.68% | +25.53% |
| **UUP** (US Dollar) | +21.02% | +0.00% | +0.00% | +0.94% |
| **IAU** (Gold) | +55.11% | +0.00% | +58.56% | +6.49% |
| **BTC** (Bitcoin) | -43.10% | +65.43% | +1.34% | +57.82% |

### Portfolio Optimization Coordinates
* **Monte Carlo Tangency Output:** Expected Return: **6.87%** | Volatility: **12.68%** | Sharpe Ratio: **0.2264**
* **Monte Carlo Minimum Variance:** Expected Return: **3.15%** | Volatility: **3.62%** | Sharpe Ratio: **-0.2357**

## Strategic Analysis & Sensitivity Testing
* **Risk-Free Rate Hurdles:** Adjusting the risk-free rate assumption from 0% up to 5% forces a significant portfolio realignment, as the optimizer requires progressively higher risk-adjusted return hurdles to justify holding high-volatility assets.
* **Temporal Windows:** Sub-sample testing reveals deep regime variance. In pre-2021 market cycles, alternative assets showed stronger return-to-volatility generation, whereas subsequent macroeconomic contraction cycles (2021–2022) shifted allocations heavily toward defensive money market proxies.

## Technical Execution Environment
* **Language:** Python
* **Optimization Algorithms:** `scipy.optimize.minimize` (Sequential Least Squares Programming - SLSQP)
* **Statistical Simulation:** Stochastic Monte Carlo Array Modeling via `numpy` & `scipy`
* **Data Pipelines:** `yfinance` API core engine
* **Graphics Infrastructure:** `matplotlib` and custom correlation mapping engines

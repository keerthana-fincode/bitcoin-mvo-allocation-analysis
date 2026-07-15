# Asset Allocation Engineering: Stress-Testing the Crypto Diversification Thesis

## Project Framework & Objective
ARK Invest’s analytical white papers assert that allocating a 1% to 5% baseline exposure to alternative digital assets like Bitcoin introduces structural diversification and asymmetric upside to classic long-only institutional portfolios. This project builds a quantitative portfolio engineering engine to evaluate this thesis under the constraints of modern portfolio theory (MPT) and Markowitz Mean-Variance Optimization (MVO). 

The allocation framework evaluates a 7-asset class multi-asset universe over a multi-year macroeconomic timeline (2018–2023), comparing an empirical 50,000-portfolio long-only Monte Carlo simulation against analytical closed-form tangency boundaries to locate the maximum Sharpe ratio vector.

## Asset Class Universe & Proxies
The investment universe spans seven major global capital vectors, mapping liquid exchange-traded funds (ETFs) as strategic proxies:
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

---

## Empirical Analysis & Factor Sensitivity

### 1. Risk-Free Rate Hurdles & Capital Realignment
Adjusting the risk-free rate assumption from 0% up to 5% forces an intense portfolio realignment. As cash yields increase, the mathematical optimizer requires a significantly higher risk-adjusted return threshold to justify holding highly volatile, high-beta assets. This dynamically alters the slopes of both the Capital Allocation Line (CAL) and Capital Market Line (CML).

### 2. Analytical Capital Market Boundaries
The scatter visualization below maps the multi-asset investment topography, plotting the risk-minimized Efficient Frontier arc relative to the Capital Market Line (CML) anchored at a 4.0% risk-free rate cap:
<p align="center">
  <img src="MC_Efficient_Frontier.png" width="850" alt="Stochastic Portfolio Frontier Boundaries">
</p>

### 3. Covariance & Statistical Dependencies
The cross-asset dependency matrix maps underlying asset behaviors. The localized correlation profiles show a high degree of integration between digital assets and equity risk premiums during macroeconomic contractions, confirming that standard diversification properties can contract during periods of market stress:
<p align="center">
  <img src="Correlation_Matrix.png" width="700" alt="Asset Dependency Correlation Profile">
</p>

### 4. Temporal Sample Window Drift
Sub-regime backtesting documents an allocation shift over time. While pre-2021 market regimes favored alternative assets due to sharp upward volatility spikes, the subsequent macroeconomic contraction cycles (2021–2022) completely wiped out these advantages, shifting optimal portfolio weights heavily toward defensive dollar holdings and money market proxies.

## Technical Stack
* **Language:** Python
* **Optimization Algorithms:** `scipy.optimize.minimize` (Sequential Least Squares Programming - SLSQP)
* **Statistical Modeling:** Long-Only Dirichlet Distribution Simulations via `numpy` & `scipy`
* **Data Pipelines:** `yfinance` financial infrastructure engine
* **Graphics Framework:** `matplotlib` (Multi-panel axis matrices utilizing GridSpec grid maps)

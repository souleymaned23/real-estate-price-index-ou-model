# Real Estate Price Index Modeling with an Ornstein–Uhlenbeck Process

## Overview

This project investigates the dynamics of the French real estate price index using an Ornstein–Uhlenbeck (OU) process.

The objective is to model the historical evolution of the index, estimate the model parameters from INSEE data, and generate future scenarios through Monte Carlo simulation.

The OU process is a classical mean-reverting stochastic model widely used in quantitative finance and economics to describe variables that fluctuate around a long-run equilibrium level.

---

## Data

The dataset consists of historical observations of the French real estate price index published by INSEE.

After cleaning and formatting the data, a quarterly time series is obtained and used for parameter estimation and forecasting.

---

## Ornstein–Uhlenbeck Model

The real estate index $X_t$ is assumed to follow the stochastic differential equation

$$
dX_t=\kappa(\theta-X_t),dt+\sigma,dW_t
$$

where:

| Parameter | Description                |
| --------- | -------------------------- |
| $\kappa$  | Speed of mean reversion    |
| $\theta$  | Long-run equilibrium level |
| $\sigma$  | Volatility                 |
| $W_t$     | Standard Brownian motion   |

The drift component forces the process toward its long-run equilibrium level $\theta$, while the diffusion component introduces random fluctuations.

---

## Analytical Solution

The exact solution of the OU process is

$$
X_t=\theta+(X_0-\theta)e^{-\kappa t}+\sigma\int_0^t e^{-\kappa(t-s)},dW_s
$$

The conditional expectation is

$$
\mathbb{E}[X_t]=\theta+(X_0-\theta)e^{-\kappa t}
$$

and the conditional variance is

$$
\mathrm{Var}(X_t)=\frac{\sigma^2}{2\kappa}\left(1-e^{-2\kappa t}\right)
$$

As $t\rightarrow\infty$,

$$
X_t\sim\mathcal{N}\left(\theta,\frac{\sigma^2}{2\kappa}\right)
$$

which corresponds to the stationary distribution of the process.

---

## Discrete-Time Representation

Since the observations are available quarterly, the continuous-time model can be written in discrete form as

$$
X_{t+\Delta}=\theta+(X_t-\theta)e^{-\kappa\Delta}+\varepsilon_t
$$

with

$$
\varepsilon_t\sim\mathcal{N}\left(0,\frac{\sigma^2}{2\kappa}(1-e^{-2\kappa\Delta})\right)
$$

This representation is particularly useful for parameter estimation.

---

## Parameter Calibration

The parameters are estimated through the regression

$$
X_{t+\Delta}=a+bX_t+\varepsilon_t
$$

where

$$
b=e^{-\kappa\Delta}
$$

which implies

$$
\kappa=-\frac{\ln(b)}{\Delta}
$$

The long-run equilibrium level is recovered from

$$
\theta=\frac{a}{1-b}
$$

Finally, the volatility parameter is estimated using

$$
\sigma=\sqrt{\frac{2\kappa,\mathrm{Var}(\varepsilon)}{1-e^{-2\kappa\Delta}}}
$$

---

## Monte Carlo Simulation

Future trajectories are generated using the exact discretization of the OU process

$$
X_{t+\Delta}
============

\theta
+
(X_t-\theta)e^{-\kappa\Delta}
+
\sqrt{\frac{\sigma^2}{2\kappa}(1-e^{-2\kappa\Delta})},Z_t
$$

where

$$
Z_t\sim\mathcal{N}(0,1)
$$

independently across time steps.

Thousands of trajectories can be simulated to obtain future distributions of the real estate index and estimate the probability of different market scenarios.

---

## Main Features

* Historical analysis of the French real estate price index
* Calibration of an Ornstein–Uhlenbeck process
* Estimation of mean-reversion dynamics
* Monte Carlo simulation of future scenarios
* Probability estimation for future thresholds
* Sensitivity and robustness analysis
* Comparison of alternative specifications

---

## Technologies

* Python
* NumPy
* Pandas
* SciPy
* Matplotlib
* Statsmodels
* Scikit-Learn

---

## Project Structure

```text
real-estate-price-index-ou-model/
│
├── README.md
├── Real_Estate_Index_OU_Model_English.ipynb
│
├── data/
│   └── real_estate_index.csv
│
├── figures/
│   ├── historical_series.png
│   ├── simulated_paths.png
│   └── terminal_distribution.png
│
└── requirements.txt
```

---

## References

* Øksendal, *Stochastic Differential Equations*
* Shreve, *Stochastic Calculus for Finance II*
* Glasserman, *Monte Carlo Methods in Financial Engineering*
* INSEE Real Estate Price Index Database

---

## Author

**Souleymane Diabate**

M2 Probability & Finance (El Karoui)

Sorbonne Université

Interested in Quantitative Finance, Stochastic Modeling, Monte Carlo Methods, Derivatives Pricing, and Risk Management.

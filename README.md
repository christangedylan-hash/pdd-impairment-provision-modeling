# PDD Impairment Provision Modeling

This project studies the numerical estimation of a durable impairment provision for financial assets held by an insurance company.

The work was developed as part of a numerical methods project at ISFA. It combines stochastic asset modeling, stochastic interest rates, Monte Carlo simulation, barrier monitoring, Brownian bridge correction, model point aggregation and risk measurement.

## Objective

The objective is to estimate a durable impairment provision under a risk-neutral framework.

In insurance accounting, a durable impairment provision may be required when the market value of an asset remains below its acquisition value for a sufficiently long period. This project models that risk using stochastic processes and Monte Carlo simulation.

The project focuses on:

- simulating risky asset dynamics under a Black-Scholes-type model;
- modeling stochastic interest rates with a Vasicek process;
- estimating impairment losses over one or several periods;
- comparing a naive discretization method with a refined Brownian bridge approach;
- computing sensitivities of the provision to key market parameters;
- extending the framework to a multi-asset portfolio;
- comparing a full multi-asset simulation with an aggregated model point approach;
- estimating tail risk through Value-at-Risk.

## Financial and Actuarial Context

The project is motivated by asset impairment risk in insurance portfolios.

The insurer holds non-bond financial assets whose market value may fall below their acquisition value. When the loss is both significant and durable, a provision must be estimated.

This makes the problem both actuarial and financial:

- actuarial, because it relates to provisioning and balance sheet risk;
- financial, because the assets are modeled using stochastic market dynamics;
- numerical, because the provision is estimated through Monte Carlo simulation;
- risk-oriented, because the project studies sensitivity, aggregation and tail losses.

## Modeling Framework

The risky asset is modeled under the risk-neutral probability measure using a Black-Scholes-type dynamic:

```text
dS_t / S_t = r_t dt + sigma dW_t
```

The short rate follows a Vasicek process:

```text
dr_t = gamma * (b - r_t) dt + sigma_r dW_t^r
```

The Brownian motions driving the asset and the short rate may be correlated.

The provision is estimated by simulating asset paths and checking whether the impairment conditions are satisfied over each accounting period.

## Numerical Methods

The implementation includes two approaches.

### Naive Method

The naive method checks the barrier condition only on the simulated time grid.

It is simple and computationally efficient, but it may miss barrier crossings occurring between two discretization dates.

### Refined Brownian Bridge Method

The refined method uses a Brownian bridge correction to estimate the probability of crossing the impairment barrier between two consecutive simulated points.

This improves the detection of durable impairment events and reduces discretization bias, at the cost of additional computation time.

## Multi-Period Provision Estimation

The project extends the one-period setting to several horizons:

- 1 year;
- 2 years;
- 5 years;
- 10 years;
- 15 years.

For each horizon, the cumulative provision is estimated using Monte Carlo simulation.

The analysis compares the naive and refined approaches and studies how the provision evolves with time.

## Sensitivity Analysis

The project computes numerical sensitivities of the impairment provision using finite differences.

The main sensitivities are:

- Delta: sensitivity to the initial asset value;
- Vega: sensitivity to asset volatility;
- Rho: sensitivity to the initial short rate.

This helps identify the main risk drivers of the provision.

## Multi-Asset Portfolio and Model Point

The project also considers a portfolio of multiple risky assets with heterogeneous weights.

Two approaches are compared:

- a full multi-asset simulation, where each asset is simulated individually;
- an aggregated model point approach, where the full portfolio is approximated by one representative synthetic asset.

This comparison highlights the trade-off between:

- modeling accuracy;
- computational cost;
- diversification effects;
- practical implementation constraints.

## Risk Measurement

The project estimates tail risk through the empirical distribution of cumulative losses.

The following risk measures are computed:

- Value-at-Risk at 99%;
- Value-at-Risk at 99.5%;
- empirical loss distributions for different time horizons.

## Repository Structure

```text
notebooks/
  pdd_impairment_provision_modeling.ipynb

report/
  PDD_Impairment_Provision_Modeling_Report_FR.pdf

requirements.txt
README.md
```

The original academic report is written in French. This README provides an English summary of the project for international readability.

## Tech Stack

- Python
- NumPy
- pandas
- matplotlib
- Monte Carlo simulation
- Euler-Maruyama discretization
- Brownian bridge correction
- Vasicek interest rate model
- Black-Scholes asset dynamics
- Finite difference sensitivities
- Portfolio risk aggregation

## Key Skills Demonstrated

- Stochastic process simulation
- Risk-neutral modeling
- Monte Carlo estimation
- Barrier event detection
- Brownian bridge correction
- Actuarial provisioning
- Financial risk modeling
- Sensitivity analysis
- Multi-asset portfolio simulation
- Model point construction
- Value-at-Risk estimation

## Authors

Academic group project by:

- Salimata Diouf
- Christ Ange Dylan Kouamé
- Aboubakar Mohamed Ouattara
- Souleymane Ouattara

## Disclaimer

This project is for academic and educational purposes only. It does not constitute actuarial advice, accounting advice, investment advice or a production-ready provisioning model.

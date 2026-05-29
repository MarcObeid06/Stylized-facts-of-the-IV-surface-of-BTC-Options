# Stylized Facts of the Implied Volatility Surface of Bitcoin Options

<p align="center">
  <b>An Empirical Study of Maturity Effects, Skew, Risk Reversals and Butterfly Dynamics</b>
</p>

<p align="center">
  Bitcoin options · Implied volatility · Volatility smile · Risk reversals · Butterflies · Stochastic skew
</p>

---

## Overview

This repository contains the code and analysis for an empirical study of the Bitcoin options implied-volatility surface. The project studies how BTC implied volatility varies across strike, maturity and time, with a focus on volatility smiles, risk reversals, butterfly dynamics and spot-regime dependence.

The report is structured around three parts:

1. implied volatility, Black--Scholes inversion and BTC volatility smiles;
2. SPX at-the-money skew as a reference case;
3. BTC risk-reversal and butterfly dynamics across maturities and market regimes.

---

## Data

The empirical analysis uses SVI-implied volatility data for BTC options on Deribit.

| Item           | Description                                                                               |
| -------------- | ----------------------------------------------------------------------------------------- |
| Period         | 1 Jan 2023 -- 27 Feb 2025                                                                 |
| Observations   | 188,277                                                                                   |
| Timestamps     | 8,903                                                                                     |
| Calendar days  | 788                                                                                       |
| Surface inputs | ATM IV, OTM call/put IVs, BTC index price, underlying price, exchange, time to expiration |

The implied-volatility surface is observed at standardized moneyness levels, from 40% OTM puts to 40% OTM calls.

---

## Methodology

### 1. Implied volatility and BTC smiles

The first part recalls the Black--Scholes implied-volatility inversion problem and compares classical numerical inversion methods:

* bisection,
* Newton--Raphson,
* hybrid Newton/bisection,
* Brent's method.

The BTC data then shows that implied volatility cannot be described by a single constant volatility. It forms a dynamic surface depending on moneyness, maturity and time.

---

### 2. SPX ATM skew benchmark

The SPX market is used as a reference case because equity-index options usually display persistent negative skew. Several parametric models are calibrated to the SPX ATM skew term structure:

* fractional power law,
* shifted power law,
* single-scale exponential model,
* two-exponential model.

This benchmark shows that even a mature equity-index market requires regularized or multi-scale descriptions of the ATM skew term structure.

---

### 3. BTC risk reversals and butterflies

For (q \in {10,20,30,40}), the (q%) risk reversal is defined as

[
RR_q(T,t)
=========

## \sigma^{\mathrm{call}}_{q%\mathrm{OTM}}(T,t)

\sigma^{\mathrm{put}}_{q%\mathrm{OTM}}(T,t).
]

It measures the directional asymmetry of the smile. A negative value means that OTM puts are richer than OTM calls; a positive value means that OTM calls are richer than OTM puts.

The (q%) butterfly is defined as

[
BF_q(T,t)
=========

\frac{1}{2}
\left(
\sigma^{\mathrm{call}}*{q%\mathrm{OTM}}(T,t)
+
\sigma^{\mathrm{put}}*{q%\mathrm{OTM}}(T,t)
\right)
-------

\sigma^{\mathrm{ATM}}(T,t).
]

It measures non-directional smile curvature: how expensive the two wings are relative to ATM implied volatility.

---

## Constant-Maturity Panel

To compare smile indicators through time, the raw option surface is interpolated onto a daily constant-maturity panel. The selected target maturities are:

| Short            | Medium              | Long                         |
| ---------------- | ------------------- | ---------------------------- |
| 5, 7, 12, 20, 30 | 42, 56, 74, 90, 120 | 150, 180, 240, 270, 330, 360 |

No extrapolation is used. If a target maturity lies outside the available maturity range at a given timestamp, the value is left missing.

---

## Main Findings

### Maturity-dependent BTC skew

BTC risk reversals are strongly maturity-dependent. Short maturities are put-skewed on average, while longer maturities become closer to symmetric and can even become mildly call-skewed.

The finite-difference ATM skew therefore changes sign, unlike the SPX ATM skew, which remains persistently negative.

---

### Regime-dependent smile asymmetry

BTC smile asymmetry depends strongly on the spot regime.

During persistent rallies, short-dated BTC options can become call-skewed: upside calls become richer than downside puts. During selloffs, the short-end risk reversal becomes sharply negative, reflecting stronger demand for downside protection.

---

### Spot-trend drivers of (RR_{10})

The strongest descriptive drivers of (RR_{10}) are:

| Driver                    | Interpretation                                               |
| ------------------------- | ------------------------------------------------------------ |
| 20-day BTC return         | Size of the recent BTC trend                                 |
| 30-day return persistence | Fraction of positive daily returns over the previous 30 days |

This suggests that BTC smile asymmetry reacts not only to isolated daily moves, but also to sustained market regimes.

---

### Butterfly term structure

Butterflies behave differently from risk reversals. They remain positive, are less sensitive to spot regimes, and mainly describe short-end smile curvature.

The average (BF_{10}) term structure is well described by a simple power-law decay:

[
BF_{10}(T) = A T^{-\beta}.
]

Thus, BTC smile asymmetry is complex and regime-dependent, while BTC smile curvature has a simpler average maturity structure.

---

## Interpretation

The results support a stochastic-skew interpretation of the BTC volatility surface. The smile should not be viewed as a fixed deterministic curve: its direction changes with market conditions.

The average long-maturity smile can look close to symmetric, while the conditional smile on a given date can become strongly put-skewed or call-skewed depending on the BTC spot regime.

---

## Limitations and Extensions

The study is descriptive. The spot-regime classification is mechanical, and the constant-maturity panel relies on interpolation across available maturities.

Possible extensions include:

* extending the analysis to newer BTC data;
* comparing BTC with other crypto underlyings;
* testing stochastic-volatility or stochastic-skew models;
* studying the impact of major crypto-market events on the level, skew and curvature of the implied-volatility surface.

---

## References

The project builds on classical and recent work on option pricing, implied volatility, stochastic skew and ATM skew term structures:

* Black and Scholes (1973)
* Merton (1973)
* Carr and Wu (2007)
* Alexander and Imeraj (2023)
* Guyon and El Amrani (2022)
* Delemotte, De Marco and Ségonne (2023)

---

## Author

|             |                                           |
| ----------- | ----------------------------------------- |
| Author      | Marc Obeid                                |
| Institution | Bachelor of Science, École Polytechnique  |
| Supervisor  | Prof. Eduardo Abi Jaber                   |
| Laboratory  | Centre de Mathématiques Appliquées (CMAP) |

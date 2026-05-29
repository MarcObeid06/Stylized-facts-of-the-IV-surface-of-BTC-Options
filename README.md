````markdown
# Stylized Facts of the Implied Volatility Surface of Bitcoin Options

**An empirical study of maturity effects, skew, risk reversals and butterfly dynamics in BTC option markets.**

This repository contains the code and analysis behind a research project on the Bitcoin options implied-volatility surface. The study uses two years of BTC option data to investigate how implied volatility depends on strike, maturity and time, with a focus on volatility smiles, risk reversals, butterfly spreads and spot-regime dependence.

---

## Overview

The project starts from the Black--Scholes implied-volatility inversion problem and treats implied volatility as a market observable rather than as a constant model parameter. The empirical analysis then studies the BTC volatility surface across moneyness, maturity and time.

The main question is:

> How does the BTC implied-volatility smile behave across maturities and market regimes, and how does it compare with more classical equity-index skew behaviour?

---

## Data

The empirical part uses SVI-implied volatility data for BTC options on Deribit, covering:

- **Period:** 1 January 2023 -- 27 February 2025  
- **Observations:** 188,277  
- **Timestamps:** 8,903  
- **Calendar days:** 788  
- **Variables:** ATM implied volatility, OTM call/put implied volatilities, BTC index price, underlying price, exchange and time to expiration  

The dataset contains implied volatilities at standardized moneyness levels, from 40% OTM puts to 40% OTM calls.

---

## Structure of the Study

### 1. Implied Volatility and BTC Option Smiles

The first part introduces the Black--Scholes framework and the implied-volatility inversion problem. Numerical methods such as bisection, Newton--Raphson, hybrid Newton/bisection and Brent's method are compared on synthetic option prices.

The BTC data then shows that implied volatility cannot be described by a single volatility number. It forms a dynamic surface depending on:

- moneyness,
- maturity,
- calendar time,
- market regime.

Short maturities display steeper smiles and stronger wing effects, while longer maturities are generally smoother.

---

### 2. SPX ATM Skew as a Reference Case

The second part uses the SPX market as a benchmark. Since SPX options usually display persistent negative skew, the SPX ATM skew term structure provides a useful comparison for BTC.

Several maturity-decay models are calibrated to the SPX ATM skew:

- fractional power law,
- shifted power law,
- single-scale exponential model,
- two-exponential model.

The results show that even in a mature equity-index market, the ATM skew term structure is not fully captured by a single power law. Regularized or multi-scale models are needed.

---

### 3. BTC Risk Reversals and Butterfly Dynamics

The main empirical contribution studies two smile diagnostics:

$$
RR_q(T,t) = \sigma^{call}_{q\%OTM}(T,t) - \sigma^{put}_{q\%OTM}(T,t)
$$

and

$$
BF_q(T,t) =
\frac{1}{2}
\left(
\sigma^{call}_{q\%OTM}(T,t)
+
\sigma^{put}_{q\%OTM}(T,t)
\right)
-
\sigma^{ATM}(T,t).
$$

Risk reversals measure directional smile asymmetry, while butterflies measure non-directional smile curvature.

A daily constant-maturity panel is built by interpolating across maturities on the grid:

```text
5, 7, 12, 20, 30, 42, 56, 74, 90, 120, 150, 180, 240, 270, 330, 360 days
````

---

## Main Findings

### Maturity-dependent BTC skew

BTC risk reversals are strongly maturity-dependent. Short maturities are put-skewed on average, meaning that short-dated OTM puts are richer than OTM calls. However, the negative skew weakens rapidly with maturity, and longer maturities become close to symmetric or mildly call-skewed.

The finite-difference ATM skew changes sign around the medium-maturity range, unlike the SPX ATM skew, which remains persistently negative.

---

### Regime-dependent risk reversals

BTC smile asymmetry depends strongly on the spot regime.

During persistent rallies, short-dated BTC options can become call-skewed: upside calls become richer than downside puts. During selloffs, the short-end risk reversal becomes sharply negative, reflecting stronger demand for crash protection.

This makes BTC different from the classical equity-index case, where negative skew is more persistent.

---

### Spot-trend drivers

The strongest descriptive drivers of `RR10` are:

* the **20-day BTC return**,
* the **30-day return persistence**, measured as the fraction of positive daily returns over the previous 30 days.

This suggests that BTC smile asymmetry reacts not only to isolated daily moves, but also to sustained market regimes.

---

### Butterfly term structure

Butterflies behave differently from risk reversals. They remain positive and are much less sensitive to spot regimes.

The average `BF10` term structure is well described by a simple power-law decay:

$$
BF_{10}(T) = A T^{-\beta}.
$$

Thus, BTC smile asymmetry is complex and regime-dependent, while BTC smile curvature has a simpler average maturity structure.

---

## Interpretation

The results support a stochastic-skew interpretation of the BTC volatility surface. The smile should not be viewed as a fixed deterministic curve: its direction changes with market conditions.

The average long-maturity smile may look close to symmetric, while the conditional smile on a given date can be strongly put-skewed or call-skewed depending on the BTC spot regime.

---

## Limitations and Extensions

The study is descriptive. The spot-regime classification is mechanical, and the constant-maturity panel relies on interpolation across available maturities.

Possible extensions include:

* repeating the analysis on newer BTC option data,
* comparing BTC with other crypto underlyings,
* testing stochastic-volatility or stochastic-skew models,
* studying the impact of major crypto-market events on the level, skew and curvature of the implied-volatility surface.

---

## References

This project builds on classical and recent work on option pricing, implied volatility, stochastic skew and ATM skew term structures, including Black--Scholes, Merton, Carr--Wu, Alexander--Imeraj, Guyon--El Amrani, and Delemotte--De Marco--Ségonne.

---

## Author

**Marc Obeid**
Bachelor of Science, École Polytechnique
Research supervised by **Prof. Eduardo Abi Jaber**
Centre de Mathématiques Appliquées (CMAP)

```
```

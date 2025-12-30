# Forecastathon – Statistical Modeling for On-Chain Forecast Markets (Research Edition)


**Forecast Blockchain Academy**

*A high-level overview of my modeling strategy for the Autonity Forecastathon — without revealing implementation details during the competition.*

---

## Project Status

Work in progress — this repo will expand throughout the season.

---

## Introduction

The Autonity Forecastathon operates in an on-chain forecasting market, where predictions are continuously priced, traded, and scored under real economic incentives.

Unlike offline benchmarks or static datasets, forecasts in this environment directly impact market outcomes, requiring disciplined modeling, calibration, and decision-making.

Forecasting in this environment is fundamentally different from offline benchmarks: models are continuously evaluated under market pressure, partial information, and adversarial pricing dynamics.

This repository documents the **research, methodology, and modeling framework** I use in the **Autonity Forecastathon**, a forecasting competition covering macroeconomic indicators such as:

* **CPIZ25** – Inflation (MoM)
* **GDPF26** – GDP (QoQ)
* **UERF26** – Unemployment (MoM, forward)
* **UERZ25** – Unemployment (MoM, near-term contract)
* **BTCVOL** – Short-Term Implied Bitcoin Volatility Contracts

The goal here is to present:

* A clear **conceptual overview** of the forecasting pipeline
* A professional reference describing the modeling architecture behind the strategy

**Note:**

Participation in the Forecastathon followed direct outreach within the Clearmatics ecosystem.

---


## Project Goals

1. Build a **statistically grounded, explainable forecasting framework**.
2. Prioritize **GLMs** (Gaussian & Gamma) and classical statistical reasoning over blind black-box models.
3. Explicitly incorporate **lags**, **regimes**, and **economic structure** into model design.
4. Translate predictions into **forecast prices** aligned with Autonity’s mark-price mechanics.
5. Keep the workflow reproducible and modular for future research or portfolio use.

---

## Modeling Philosophy

### 1. Interpretability First

Instead of defaulting to ARIMA/Prophet/neural networks, the approach emphasizes:

* GLMs (Gaussian link = identity, Gamma link = log)
* Regime-aware decomposition
* Diagnostics-driven selection
* Economic plausibility

This keeps the model understandable and stable — qualities that matter in real forecasting, not just competitions.



### 2. Structured Lag Engineering

Macro signals rarely move instantly.
The framework systematically evaluates:

* 1–3 month lags
* Regime-lag interactions
* Stability across rolling windows

Only lags that make statistical and economic sense are kept.


### 3. Regime-Sensitive Modeling

Economic time series change character during:

* COVID
* High inflation periods
* Post-pandemic normalization

Ignoring regime shifts tends to mislead models.
This approach treats structural breaks as first-class modeling components.


### 4. Clean Prediction → Price Mapping

Autonity uses mark prices; forecasts must be translated accordingly.

The mapping layer uses:

* Predicted percentage change
* Price-mapping formulas
* Adjustments for volatility or regime uncertainty

This layer is intentionally private until the competition ends.

---

## Target Series

### CPIZ25 – Inflation (MoM)

* GLM-based modeling with Gaussian/Gamma alternatives
* Strong regime sensitivity
* Lag architecture to capture delayed drift
* Often close to consensus but improves turning-point detection


### GDPF26 – GDP (QoQ)

* Much smoother series
* Gaussian GLMs work well
* Lags matter less
* Focus is on stability rather than squeezing minor variance


### UERF26 – Unemployment (MoM, forward)

* Noisy, revision-prone series
* Requires extremely parsimonious models
* Regime detection is important
* Gaussian vs Gamma tested for asymmetry and tail behavior


### UERZ25 – Unemployment (MoM, near-term)

* More sensitive to immediate labor market shifts
* Helps cross-validate the UERF26 design
* Gamma (log link) often useful due to asymmetry and small-change clustering
* Final specification will be documented after the season


### BTCVOL – Short-Term Implied Bitcoin Volatility Contracts

In addition to macroeconomic indicators, the strategy was extended to
short-dated Bitcoin volatility contracts (weekly expiries).

These instruments require a fundamentally different treatment:
- No macro releases
- High-frequency price dynamics
- Expiry-driven behavior

A separate volatility-focused modeling layer was developed, intentionally
kept private during the competition due to its sensitivity.

---

## Forecast Submission Strategy (Decision Layer)

A key component of the framework is the separation between:

- Forecast generation
- Forecast submission

Forecasts are not submitted daily by default.
Submissions are made only when new information is detected, such as:
- Structural regime changes
- New macroeconomic releases
- Material divergence between forecast and mark price

This avoids overtrading and aligns with the scoring dynamics of the Forecastathon.

---

## Repository Structure (Post-Competition Release)

When the Forecastathon ends, the repository will include:

```
forecastathon-modeling-framework/

  src/			#R code
  
  models/

  notebooks/
    
  results/
     (released post-competition)
     forecasts/		# Automatic forecast CSVs
     charts/		# Automatically generated charts
     
  README.md
  
  LICENSE
```

---

## Code Availability

To preserve the integrity of ongoing and future Forecastathon seasons, 
implementation details are not publicly released during active participation.

After the competition period, I’m open to discussing the modeling approach 
and selected implementation details with recruiters or technical leads 
in a private, context-appropriate setting.


---

## External Context


Clearmatics is a London-based company focused on designing protocols
and market infrastructure for decentralized and institutional
financial systems.

Since the mid-2010s, Clearmatics has been cited in institutional
initiatives involving major global banks, particularly in efforts
related to blockchain-based settlement and financial market
infrastructure.

References:

- CoinDesk (2019) – [Top banks invest $50 million to build blockchain settlement system](https://www.coindesk.com/markets/2019/05/17/top-banks-investing-50-million-to-build-blockchain-settlement-system)
- CoinDesk (2019) – [Barclays and Clearmatics Call on Coders to Help Blockchains Talk to Each Other](https://www.coindesk.com/markets/2019/01/17/barclays-and-clearmatics-call-on-coders-to-help-blockchains-talk-to-each-other)
- CoinDesk (2025) – [Clearmatics' New DeFi Derivatives Let Traders Bet on Anything, but It's Not a Prediction Market](https://www.coindesk.com/business/2025/07/28/clearmatics-new-defi-derivatives-let-traders-bet-on-anything-but-it-s-not-a-prediction-market)

---


## Author

This project was developed by an engineer and data scientist with a background in:

* Postgraduate degree in **Data Science and Analytics (USP)**
* Bachelor's degree in **Computer Engineering (UERJ)**
* Special interest in statistical models, interpretability, and applied AI


---

## Contact  

- [LinkedIn](https://linkedin.com/in/celso-m-silva)  
- Or open an [issue](https://github.com/celsomsilva/forecastathon/issues)




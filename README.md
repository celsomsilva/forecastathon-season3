# Forecastathon – Statistical Modeling & Predictive Strategy (Research Edition)

**Forecast Blockchain Academy**

*A high-level overview of my modeling strategy for the Autonity Forecastathon — without revealing implementation details during the competition.*

---

## Project Status

Work in progress — this repo will expand throughout the season.

---

## Introduction

This repository documents the **research, methodology, and modeling framework** I use in the **Autonity Forecastathon**, a forecasting competition covering macroeconomic indicators such as:

* **CPIZ25** – Inflation (MoM)
* **GDPF26** – GDP (QoQ)
* **UERF26** – Unemployment (MoM, forward)
* **UERZ25** – Unemployment (MoM, near-term contract)**

The goal here is to present:

* A clear **conceptual overview** of the forecasting pipeline
* A structured place where the **full implementation** will be published **after the season ends**
* A professional reference describing the modeling architecture behind the strategy

**Note:**
No source code, formulas, or parameter details are included until the competition concludes.

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

## Target Series (Overview)

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

---

## Repository Structure (Post-Competition Release)

When the Forecastathon ends, the repository will include:

```
forecastathon-modeling-framework/
  src/
    glm_cpiz25.R
    glm_gdpf26.R
    glm_uerf26.R
    glm_uerz25.R
    preprocessing_utils.R
    diagnostics_utils.R

  models/
    cpiz25_model.rds
    gdpf26_model.rds
    uerf26_model.rds
    uerz25_model.rds

  notebooks/
    CPIZ25_analysis.ipynb
    GDPF26_analysis.ipynb
    UERF26_analysis.ipynb
    UERZ25_analysis.ipynb

  forecasts/
    rolling_forecasts.csv
    forecast_vs_mark_comparison.pdf

  report/
    strategy_summary.md
    model_diagnostics.md

  README.md
```

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




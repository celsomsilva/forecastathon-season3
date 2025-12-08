![Blockchain](https://img.shields.io/badge/Blockchain-Autonomy-blue)
![R](https://img.shields.io/badge/R-4.4.0-blue?logo=r)
![Contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg)


# **Forecastathon – Statistical Modeling & Predictive Strategy (Research Edition)** - Forecast Blockchain Academy 

*A high-level overview of my modeling approach for the Autonity Forecastathon, without exposing implementation details during the competition.*

---

## Project Status

This repository is **work-in-progress**.  

--

## Introduction

This repository documents my **research, methodology, and modeling framework** developed for the **Autonity Forecastathon**, a competitive environment where participants forecast macroeconomic indicators such as:

- **CPIZ25** – Inflation (MoM)  
- **GDPF26** – GDP growth (QoQ)  
- **UERF26** – Unemployment (MoM) – forward contract  
- **UERZ25** – Unemployment (MoM) – nearer expiry / alternative contract

The goal of this repository is to provide:

- A transparent **conceptual overview** of my forecasting pipeline  
- A **structured space** where the full implementation will be published **after the season ends**  
- A professional-level reference of the modeling architecture used throughout the competition

**Note**  
No source code, models, or exact formulas are included at this stage to preserve competitive integrity.  
All implementation assets will be released **after the Forecastathon concludes**.

---

## Project Goals

1. Build a **robust, explainable and statistically grounded forecasting framework**.  
2. Leverage **Generalized Linear Models (GLMs)** (Gaussian and Gamma families) and classical statistical techniques to outperform naïve or purely black-box models.  
3. Incorporate **structural regimes**, **lags**, and **economic reasoning** into model specification.  
4. Develop a **systematic approach** for mapping predicted changes into **forecast prices** used by Autex/Autonity.  
5. Maintain reproducibility and modularity for future research and portfolio demonstration.

---

## Modeling Philosophy

My strategy is built on the following pillars:

### 1. Statistical Interpretability First  

While many competitors rely on ARIMA, Prophet, or ad-hoc neural networks, this framework prioritizes:

- **GLMs** (Gaussian with identity link, Gamma with log link)  
- Regime-shift decomposition  
- Diagnostics-based model selection  
- Economic plausibility and parsimony  

This provides clarity, robustness, and explainability — essential in real-world forecasting.

---

### 2. Structured Lag Engineering

Macro indicators often respond with delay.  
The workflow systematically tests:

- `lag1`, `lag2`, `lag3` (when relevant)  
- Interactions with structural regimes  
- Stability under rolling windows and subperiods  

Only statistically significant or economically reasonable lags are retained.

---

### 3. Regime-Sensitive Modeling

Economic time series exhibit sharp structural breaks.  
The methodology accounts for regimes such as:

- **Pandemic period**  
- **High inflation period**  
- **Normalization / post-pandemic transition**  

This prevents models from being biased by extreme or atypical historical events.

---

### 4. Clean Mapping from Prediction → Price

Autonity uses *mark prices* as baseline for forecast markets.  
The framework computes **forecast prices** through:

- Predicted percentage change  
- Proper price-mapping equations  
- Adjustments for volatility and structural uncertainty when needed  

This price mapping layer is one of the key edges of the strategy — implementation details are released only after the competition.

---

## Target Series Overview

### 1. CPIZ25 – Inflation (MoM)  

- Modeled using GLMs with appropriate transformations when necessary  
- Combines **Gaussian** and **Gamma** experimentation in early stages, with selection guided by diagnostics (residuals, dispersion, tail behavior)  
- Sensitive to structural regimes (pandemic, high inflation, normalization)  
- Uses a hybrid lag/shift architecture  
- Produces forecasts close to market consensus but with systematic improvements on turning points

---

### 2. GDPF26 – GDP (QoQ)  

- Smoother and more stable series  
- Best modeled with **parsimonious Gaussian GLMs**  
- Lag effects are present but weaker compared to inflation  
- Price mapping is relatively straightforward and lower-volatility  
- Focus on stability and robustness rather than overfitting small variations

---

### 3. UERF26 – Unemployment (MoM, forward contract)  

- Noisy series, sensitive to revisions and local shocks  
- Requires careful specification and regular diagnostics  
- Regime modeling is important to avoid overreacting to unstable periods  
- Works best with ultra-parsimonious structures (few predictors, controlled lag structure)  
- Comparative experiments with **Gaussian vs. Gamma** address asymmetry and tail risk

---

### 4. UERZ25 – Unemployment (MoM, near-term / alternative contract)  

- Shorter horizon, often more sensitive to immediate labor market moves  
- Used both as a **standalone target** and as a **cross-check** for UERF26 dynamics  
- GLM framework tests **Gamma (log link)** and **Gaussian (identity)** to capture:  
  - Asymmetry in shocks  
  - Occasional spikes  
  - Concentration of mass near small monthly changes  
- Final family choice and specification are documented in detail in the post-competition release.

---

## Repository Structure (Post-Competition Release)

After the Forecastathon ends, this repository will include:

```text
forecastathon-modeling-framework/
│
├── src/
│   ├── glm_cpiz25.R
│   ├── glm_gdpf26.R
│   ├── glm_uerf26.R
│   ├── glm_uerz25.R
│   ├── preprocessing_utils.R
│   ├── diagnostics_utils.R
│
├── models/
│   ├── cpiz25_model.rds
│   ├── gdpf26_model.rds
│   ├── uerf26_model.rds
│   ├── uerz25_model.rds
│
├── notebooks/
│   ├── CPIZ25_analysis.ipynb
│   ├── GDPF26_analysis.ipynb
│   ├── UERF26_analysis.ipynb
│   ├── UERZ25_analysis.ipynb
│
├── forecasts/
│   ├── rolling_forecasts.csv
│   ├── forecast_vs_mark_comparison.pdf
│
├── report/
│   ├── strategy_summary.md
│   ├── model_diagnostics.md
│
└── README.md
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




# Insurance Claim Cost Modeling and Premium Estimation

## Overview
This project focuses on **insurance claim cost modeling** to support **fair and reliable premium estimation**.  
The approach decomposes claim costs into **frequency** and **severity** components, evaluates a range of machine learning models, and compares them with a **compound Tweedie regression** framework commonly used in actuarial practice.

The emphasis is on **robustness, computational efficiency, and uncertainty quantification** when working with large, zero-inflated, and highly skewed insurance datasets.

---

## Problem
Accurately estimating future claim costs is a core challenge for insurers, as it directly affects pricing fairness, risk management, and product design.

Key difficulties include:
- Zero-inflated claim counts and skewed loss distributions  
- Strong non-linearities between risk factors and outcomes  
- Trade-offs between model accuracy and computational cost  
- Limited reliability of point predictions without uncertainty measures  

This project evaluates whether modern machine learning methods can meaningfully improve upon traditional actuarial models under these constraints.

---

## Data
The analysis uses a large-scale motor insurance dataset derived from historical policy and claims records.

**Key characteristics**
- ~330,000 training observations  
- No missing values  
- Mix of categorical and numerical risk factors  

**Features include**
- Policy and exposure information  
- Vehicle characteristics (e.g. power, brand, age)  
- Driver attributes (e.g. age, region, density)  
- Claim counts and claim amounts  

The target variables are derived as:
- **Frequency** (claims per exposure)  
- **Severity** (claim amount given a non-zero claim)  
- **Pure Premium** (expected claim cost)

A separate holdout dataset with identical features (excluding targets) is used for out-of-sample evaluation.

**NOTE:** Dataset is confidential and it belongs to the property of Allianz and Liverpool Victoria. Access not disclosed in public.

---

## Methodology

### Modeling Strategy
Two complementary approaches are explored:

1. **Separate modeling**
   - Frequency and severity modeled independently  
   - Greater flexibility, but higher complexity and runtime  

2. **Compound modeling**
   - Tweedie regression to jointly model frequency and severity  
   - Simpler and faster, but less expressive  

### Models Evaluated
- GLM (Poisson + Gamma)
- Random Forest
- Gradient Boosting
- XGBoost
- LightGBM
- CatBoost
- Bayesian Ridge
- CANN
- AutoML

Hyperparameters were tuned using **RandomizedSearchCV**.

---

## Evaluation
Models were assessed using:
- **R²**, **MSE**, **MAE**
- Training and prediction time
- Stability under zero-inflation and skewness

To support risk-aware decision making, multiple **uncertainty quantification** methods were applied:
- Parametric intervals  
- Bootstrapped intervals  
- Quantile regression  
- Conformal prediction  

---

## Key Results
- **AutoML** achieved the strongest predictive accuracy  
- **Bayesian Ridge** provided the best speed–accuracy trade-off  
- **Random Forest** delivered high accuracy but was computationally expensive  
- **Compound Tweedie regression** showed strong efficiency and competitive error metrics, making it attractive for deployment  

Across models, prediction intervals achieved close to **95% empirical coverage**, though wide intervals highlight ongoing challenges in capturing variability.

---

## Takeaways
- Pure premium prediction remains difficult due to extreme variability  
- Modern ML improves performance, but gains are incremental  
- Computational efficiency is as important as accuracy in practice  
- Uncertainty quantification is essential for insurance pricing decisions  

---

## Limitations and Future Work
- Negative or near-zero R² values indicate limited variance capture  
- Prediction intervals remain wide despite good coverage  
- Future work could explore deep learning models, improved feature engineering, and tighter calibration of uncertainty estimates  

---




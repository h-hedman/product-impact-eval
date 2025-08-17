# Streamly Engagement Experiment: Product Impact Evaluation

This project simulates and analyzes the impact of a product feature rollout on user engagement for **Streamly**, a fictional media streaming platform. The analysis includes both causal inference and machine learning methods to measure treatment effects and predict user behavior.

---

## Project Objectives

- **Evaluate product impact** using generalized estimating equations (GEE) to quantify treatment effects over time.
- **Predict daily engagement** using an XGBoost regression model to assess feature importance and nonlinear effects.
- **Simulate user behavior** with structured treatment assignment to reflect a typical A/B test.
- **Compare statistical and machine learning methods** for internal validation and insight triangulation.

---

## Methods Overview

### 1. Generalized Estimating Equations (GEE)

- Clustered user-level model to control for repeated measures
- Covariates include: age, gender, device type, premium status, region, prior engagement
- Main coefficient of interest: `post_treated` (treatment × post-intervention)

**Key Findings:**

| Variable           | Coefficient | p-value  | Interpretation                         |
|--------------------|-------------|----------|----------------------------------------|
| `post_treated`     | +1.50       | < 0.001  | Significant increase in engagement due to treatment |
| `treatment`        | –0.001      | 0.561    | No standalone effect pre-intervention  |
| `post`             | +1.49       | < 0.001  | General time-based increase (likely anticipation effect) |
| `prior_engagement` | +0.80       | < 0.001  | Strong predictor of post-intervention behavior |

### 2. XGBoost Regression

- Predicts daily engagement from all features
- Captures nonlinear and interaction effects
- Trained on 80% of users, tested on remaining 20%

**Model Performance:**
- Root Mean Squared Error (RMSE): **1.085**

**Top Predictive Features:**
- `prior_engagement`
- `post_treated`
- `post`
- `device`
- `power_user`

---


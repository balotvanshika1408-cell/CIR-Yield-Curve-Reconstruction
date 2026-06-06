## Yield Curve Reconstruction Using the Cox-Ingersoll-Ross (CIR) Model

## Project Overview

This project implements the Cox-Ingersoll-Ross (CIR) interest rate model to reconstruct and predict the yield curve from a short-rate proxy. The model is calibrated using a cross-sectional optimization framework that simultaneously incorporates information from multiple maturities. The objective is to estimate the CIR parameters and evaluate how effectively the calibrated model can reproduce observed market yield curves.

The project focuses on:

* CIR bond pricing using closed-form analytical solutions.
* Cross-sectional calibration across multiple maturities.
* Yield curve reconstruction from a 3-month interest rate proxy.
* Out-of-sample testing and validation.
* Performance evaluation using RMSE, MAE, and R² metrics.
* Verification of the Feller stability condition.

---

## Mathematical Background

The CIR model assumes that the short-term interest rate follows the stochastic differential equation:

dr(t) = κ(θ − r(t))dt + σ√r(t)dW(t)

where:

* κ : Speed of mean reversion
* θ : Long-run mean interest rate
* σ : Volatility parameter
* W(t) : Standard Brownian motion

The CIR framework is widely used in fixed-income modelling because it naturally encourages non-negative interest rates and admits analytical bond pricing solutions.

Zero-coupon bond prices are obtained using the standard CIR functions A(T) and B(T):

P(T) = A(T)e^(-B(T)r_t)

The corresponding continuously compounded yield is:

y(T) = -ln(P(T))/T

---

## Dataset

The project uses historical yield curve data containing the following maturities:

| Maturity | Column   |
| -------- | -------- |
| 3 Months | ZC025YR  |
| 6 Months | ZC050YR  |
| 9 Months | ZC075YR  |
| 1 Year   | ZC100YR  |
| 2 Years  | ZC200YR  |
| 5 Years  | ZC500YR  |
| 10 Years | ZC1000YR |
| 20 Years | ZC2000YR |
| 30 Years | ZC3000YR |

The 3-month yield is used as a proxy for the instantaneous short rate.

---

## Methodology

### 1. Data Preprocessing

* Sort observations chronologically.
* Handle missing values using forward-fill and backward-fill methods.
* Extract relevant maturity columns.
* Convert yields into numerical matrices for calibration.

### 2. CIR Bond Pricing

Closed-form CIR bond pricing functions A(T) and B(T) are implemented to generate theoretical bond prices and yields.

### 3. Cross-Sectional Calibration

The CIR parameters:

* κ (kappa)
* θ (theta)
* σ (sigma)

are estimated using a cross-sectional optimization procedure.

For every trading day:

1. The observed 3-month yield is treated as the short-rate input.
2. The CIR model generates theoretical yields for all maturities.
3. Squared errors between market yields and model yields are calculated.
4. Errors are accumulated across all observations.

The objective function is minimized using the Nelder-Mead optimization algorithm.

### 4. Feller Condition Verification

After calibration, the following stability condition is checked:

2κθ ≥ σ²

If the condition is violated, a corrective adjustment is applied to maintain model stability.

### 5. Out-of-Sample Testing

The calibrated parameters are applied to unseen test data to reconstruct yield curves at selected maturities.

### 6. Performance Evaluation

Model accuracy is measured using:

* Root Mean Squared Error (RMSE)
* Mean Absolute Error (MAE)
* Coefficient of Determination (R²)

---

## Results

The project evaluates the ability of the CIR model to reconstruct yield curves from a short-rate proxy.

Key observations include:

* Cross-sectional calibration improves overall yield curve fitting.
* The model successfully reconstructs short- and medium-term maturities.
* The Feller condition helps maintain numerical stability.
* Out-of-sample testing provides an unbiased assessment of predictive performance.

Example evaluation metrics:

* RMSE: [Insert Value]
* MAE: [Insert Value]
* R²: [Insert Value]

---

## Project Structure

```text
├── data/
│   ├── train_data.csv
│   └── test_data.csv
│
├── notebooks/
│   └── Finance_project.ipynb
│
├── results/
│   ├── plots/
│   └── evaluation_metrics/
│
└── README.md
```

---

## Installation

Clone the repository:

```bash
git clone https://github.com/your-username/your-repository-name.git
```

Navigate to the project folder:

```bash
cd your-repository-name
```

Install dependencies:

```bash
pip install numpy pandas matplotlib scipy scikit-learn
```

---

## Running the Project

Open the notebook:

```bash
jupyter notebook
```

or upload the notebook directly to Google Colab.

Run all cells sequentially:

1. Data preprocessing
2. CIR calibration
3. Feller condition verification
4. Yield curve prediction
5. Performance evaluation

---

## Limitations

This implementation uses a single-factor CIR framework. While effective for yield curve reconstruction, several limitations remain:

* Parameters are assumed constant through time.
* Only one source of interest rate risk is modelled.
* Extreme market conditions may reduce predictive accuracy.
* Long-term yield dynamics may require multi-factor models.

---

## Future Extensions

Potential improvements include:

* Time-dependent CIR parameters
* Multi-factor CIR models
* CIR++ framework
* Physics-Informed Neural Networks (PINNs)
* Deep learning based yield curve forecasting

---

## Author

Vanshika Balot

M.Tech / Finance Modelling Project

Interest Rate Modelling and Yield Curve Reconstruction using the CIR Framework.




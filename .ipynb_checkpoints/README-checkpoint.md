📘 Football Betting Market Analysis

Machine learning–driven modelling, calibration, and strategy simulation for football betting markets.








📑 Table of Contents

Overview

Project Structure

Notebooks

01_exploration.ipynb

02_modelling.ipynb

03_market_simulation.ipynb

Installation

How to Run

Data Source

Results Summary

Future Improvements

License

Author

🔍 Overview

This repository contains a complete, end-to-end workflow for analysing football betting markets using machine learning, probability calibration, and betting strategy simulation.

The pipeline:

Loads and cleans historical Premier League match data

Trains and calibrates a probabilistic model for match outcomes

Simulates betting strategies such as flat staking and fractional Kelly

Evaluates portfolio-style performance (ROI, Sharpe, max drawdown)

Generates calibration diagnostics & sensitivity analysis

The goal is to quantify whether the model identifies market inefficiencies and whether any trading strategy would have been profitable out of sample.

📁 Project Structure
football-betting/
│
├── README.md
├── requirements.txt
│
├── data/
│   ├── raw/                      # Original football-data.co.uk CSVs (e.g. E0.csv)
│   ├── processed/                # Clean/tidy outputs (e.g., model_probabilities__tidy.csv)
│
├── notebooks/
│   ├── 01_exploration.ipynb      # Data cleaning + EDA + bookmaker calibration
│   ├── 02_modelling.ipynb        # Softmax model + calibration + test export
│   ├── 03_market_simulation.ipynp# EV, Kelly, backtesting, strategy optimisation
│
├── outputs/
│   ├── model_probabilities.csv   # Calibrated probabilities (test slice)
│   ├── softmax_odds_base.joblib
│   ├── softmax_odds_calibrated_sigmoid.joblib
│   ├── figures/
│   ├── reports/
│
└── scripts/                      # Future modularisation of reusable code

📓 Notebooks
📘 01_exploration.ipynb
Purpose

Initial data exploration. Cleans bookmaker odds, converts odds → implied probabilities, and analyses bookmaker calibration.

Key steps

Load raw Premier League data (E0.csv)

Standardise team names, match dates, and odds

Extract bookmaker odds (AvgH/AvgD/AvgA or fallback)

Compute implied and fair probabilities

Run bookmaker calibration analysis:

Predicted probability bins vs actual outcomes

Reliability curves

Outputs

Cleaned dataset used by NB2

Calibration plots for bookmaker probabilities

🤖 02_modelling.ipynb
Purpose

Train a 3-way outcome model (H/D/A), calibrate probabilities, evaluate predictive quality, and export predictions.

Key steps

Create features from bookmaker fair probabilities

Train multinomial logistic regression (softmax)

Hyperparameter search (C-values)

Apply sigmoid calibration (Platt scaling)

Metrics:

Log loss

Multiclass Brier score

Reliability curves

ECE (Expected Calibration Error)

Export:

Calibrated softmax model

Test-set probabilities

model_probabilities.csv for NB3

Outputs

outputs/:

softmax_odds_base.joblib

softmax_odds_calibrated_sigmoid.joblib

model_probabilities.csv (test sample)

Reliability plots & metrics CSVs

💰 03_market_simulation.ipynb
Purpose

Run an out-of-sample betting simulation using the calibrated probabilities.

Key steps

Merge bookmaker odds with model probabilities

Calculate expected value (EV) for all outcomes

Implement staking strategies:

Flat unit

Fractional Kelly (with cap)

Simulate bankroll evolution

Compute performance metrics:

ROI, hit rate

Turnover

Max drawdown

Sharpe-like ratio

Generate plots:

Equity curve

EV vs realised return

Market vs model probabilities

Run:

Multi-strategy comparison (Conservative/Balanced/Aggressive)

Full grid search optimisation

Outputs

outputs/figures/:

Equity curves

EV/return diagnostics

outputs/reports/:

Trade logs

Performance summaries

Strategy comparison

Sensitivity grid

🛠 Installation
git clone https://github.com/<sebastianclaridge>/football-betting.git
cd football-betting
pip install -r requirements.txt


Or using conda:

conda create -n betting python=3.10
conda activate betting
pip install -r requirements.txt

▶️ How to Run

Run the notebooks in order:

01_exploration.ipynb

02_modelling.ipynb

03_market_simulation.ipynb

Optional:
Export notebooks as HTML with:

jupyter nbconvert --to html notebooks/02_modelling.ipynb

📦 Data Source

This project uses data from:

📍 https://www.football-data.co.uk/

Specifically:

Premier League match data (E0.csv)

📊 Results Summary

Model shows improved calibration after sigmoid correction

Out-of-sample betting simulation highlights:

High variance under Kelly staking

More stable returns under conservative staking

Best strategies vary depending on EV thresholds and Kelly fractions

Automated grid search reveals profitable regions in parameter space

Outputs include thorough diagnostics and performance comparisons

🚀 Future Improvements

Add team strength ratings (Elo, SPI, expected-goals models)

Include multiple bookmakers for robust pricing

Extend to Asian handicaps and totals markets

Use Bayesian calibration instead of Platt scaling

Deploy as a match-day betting dashboard

Add walk-forward validation across seasons

📄 License

MIT License
(You can replace this with Apache 2.0 / GPL / proprietary as needed.)

👤 Author

Sebastian Claridge
GitHub: @sebastianclaridge
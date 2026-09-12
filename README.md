# Stock Price Movement Predictor — Solana (SOL-USD)

## Overview
Predicts next-day price direction (Up/Down) for Solana using historical OHLCV data and technical indicators. Built as part of a time-series ML classification task.

## Tech Stack
Python, pandas, scikit-learn, matplotlib, yfinance

## Approach

### Target Construction
Next-day direction label created using `shift(-1)` to avoid forward leakage. Verified explicitly in notebook.

### Technical Indicators (calculated in pandas)
- **Daily Return** — percentage change from previous close
- **SMA-5** — 5-day simple moving average
- **RSI-14** — 14-day relative strength index

### Time-Based Split
Last 100 days used as test set. Scaler fit on training data only to prevent data leakage.

### Models
- RandomForestClassifier with 100 estimators, 50 min samples leaf

## Results

| Model | Accuracy |
|---|---|
| Persistence Baseline | 0.5 |
| Majority Class Baseline | 0.52 |
| Raw Feature Model | 0.49 |
| Engineered Feature Model | 0.45 |

## Class Balance
| Class | Count | Proportion |
|---|---|---|
| Down (0) | 1183 | 50.4% |
| Up (1) | 1162 | 49.5% |

## Honest Interpretation
Both ML models failed to outperform naive baselines. This is consistent with the Efficient Market Hypothesis — in highly liquid crypto markets, historical price patterns are rapidly arbitraged away leaving little predictable signal. The near-perfect class balance confirms no dominant directional bias exists in Solana's price history.

Interestingly the raw OHLCV model slightly outperformed the engineered feature model, suggesting that technical indicators derived from price may not add predictive signal beyond raw price data itself for this asset.

Past OHLCV data alone is insufficient to generate trading edge on a volatile crypto asset like Solana.

## Files
- `solanafinal.ipynb` — full analysis
- `README.md` — this file
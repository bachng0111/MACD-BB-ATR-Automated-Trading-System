# MACD-BB-ATR Automated Trading System

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)

A stateful algorithmic trading strategy combining **MACD Histogram**, **Bollinger Bands**, and **ATR** indicators with momentum and mean-reversion principles. Features hyperparameter optimization via Optuna and portfolio allocation using Modern Portfolio Theory.

## Project Overview

This project implements an event-based backtesting framework with four distinct trading "legs":
- **Long Momentum (LM)**: Follow upward trend continuation
- **Short Momentum (SM)**: Follow downward trend continuation  
- **Long Reversion (LR)**: Buy oversold conditions near lower Bollinger Band
- **Short Reversion (SR)**: Sell overbought conditions near upper Bollinger Band

### Key Features
- **Robust MACD Scaling**: Uses Median/MAD instead of mean/std to reduce noise
- **Log-space Bollinger Bands**: For scale stability across different price levels
- **ATR-based Risk Management**: Dynamic TP/SL and trailing stops
- **Lifecycle Guards**: Cooldown periods, rebounce blocking, and time stops
- **Portfolio Optimization**: Tangent (Max Sharpe) portfolio via Gurobi solver
- **Hyperparameter Tuning**: Optuna-based optimization with early stopping

## Performance Targets

| Metric | Target |
|--------|--------|
| In-sample Sharpe Ratio | ≥ 1.5 |
| Maximum Drawdown | < 20% |
| Benchmark | Outperform equal-weighted MAANG portfolio |

## Results Highlights

On the test period (2018-2019):
- **Annualized Return**: 32.87% vs SPY's 11.62%
- **Maximum Drawdown**: ~10% vs SPY's ~20%
- **Average Monthly Return**: 2.48%
- Positive skew with contained downside risk

## Data

| Parameter | Value |
|-----------|-------|
| Assets | MAANG Stocks |
| Frequency | Daily |
| Full Window | 2010-01-01 → 2019-12-31 |
| Train Period | 2010-01-01 → 2017-12-31 |
| Test Period | 2018-01-01 → 2019-12-31 |
| Source | Yahoo Finance |

## Getting Started

### Prerequisites

- Python 3.8+
- Gurobi license (free academic license available at [gurobi.com](https://www.gurobi.com/academia/academic-program-and-licenses/))

### Installation

1. Clone the repository:
```bash
git clone https://github.com/bachng0111/MACD-BB-ATR-Automated-Trading-System.git
cd MACD-BB-ATR-Automated-Trading-System
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Open and run the notebook:
```bash
jupyter notebook MACD_BB_ATR_Trading_Strategy.ipynb
```

## Notebook Structure

1. **Data Import & Library Setup** - Load required packages and data
2. **Portfolio Selection** - Modern Portfolio Theory optimizer (Tangent portfolio)
3. **Common Classes** - Base classes for backtesting infrastructure
4. **Trading Strategy Class** - MACD+BB+ATR strategy implementation
5. **Hyperparameter Tuning** - Optuna optimization for Sharpe maximization
6. **Backtesting & Results** - Run strategy and analyze performance
7. **Visualization** - Equity curves, drawdowns, heatmaps, Q-Q plots

## Strategy Parameters

Key tunable parameters include:

| Parameter | Description |
|-----------|-------------|
| `macd_fast/slow/signal` | MACD indicator windows |
| `macd_k` | Robust scaling factor for thresholds |
| `bb_window`, `bb_std_dev` | Bollinger Bands configuration |
| `atr_window` | ATR lookback period |
| `tp_mult_*`, `sl_mult_*` | Take profit/stop loss ATR multipliers |
| `cooldown` | Bars to wait after exit |
| `rebounce_block` | Bars blocking opposite direction entry |
| `rebalance_freq` | Portfolio rebalancing period (days) |

## Team

**Group 6** - NUS Module Project (November 2025)

- To Bao Chau (A0276224E)
- Bryan Ngu (A0276298J)
- Ho Xin Yi (A0281754X)
- Lauren Dana Ho Min (A0278037X)
- Phua Xing Xi Charlene (A0282609X)
- Bach Nguyen (A0258905U)

# Hakimi AI Trader

> Multi-timeframe market regime detection for crypto, forex, and commodities — built by a trader, for traders.

[![Python](https://img.shields.io/badge/python-3.10%2B-blue)]()
[![License](https://img.shields.io/badge/license-MIT-green)]()
[![Status](https://img.shields.io/badge/status-active%20development-orange)]()

Hakimi AI Trader doesn't try to tell you "buy" or "sell." It tells you what the market is *doing* — whether price is trending up, down, or chopping sideways — and how confident the model is about that read across several timeframes at once. The output is a probability, not an order. What you do with it is your call.

I built this after years of watching single-timeframe indicators fall apart in fast markets. A 15-minute RSI screaming "oversold" means very little when the daily structure is in a clean downtrend. This project is my attempt to encode that kind of multi-timeframe context into something measurable.

---

## Why this exists

Most retail tooling is reactive. Indicators lag, signals fire late, and there's no sense of *regime* — the underlying state the market is in. A breakout strategy that prints money in a trend will get shredded in a range, and vice versa.

Hakimi AI Trader takes a different angle:

- It reads the **1H, 4H, and 1D timeframes together** instead of in isolation, so lower-timeframe noise gets weighed against higher-timeframe structure.
- It classifies the current **regime** (bullish / neutral / bearish) rather than spitting out fixed entry signals.
- It returns **calibrated probabilities**, which means you can size positions by conviction instead of going all-in on every flip.

The goal was never a black box that trades for you. It's a second opinion that's harder to fool than your own bias at 3 a.m.

---

## How it works

The pipeline is straightforward in shape, even if the internals get involved:

1. **Ingest** — Pull OHLCV data from Binance (crypto), CoinEx, or MetaTrader 4 (forex/commodities).
2. **Engineer features** — Compute the indicator set per timeframe (details below).
3. **Fuse timeframes** — Align 1H / 4H / 1D into a single feature matrix so the model sees all three contexts for the same moment.
4. **Predict** — Run the fused matrix through the trained classifier to get `P(bull)`, `P(neutral)`, `P(bear)`.
5. **Surface** — Push the result to a chart overlay or dashboard, color-coded by the dominant class and its confidence.

### Feature set

| Category | Features |
|---|---|
| Trend | EMA stack (9/21/50/200), EMA slope, price-vs-EMA position |
| Momentum | RSI(14), RSI divergence flags, rate of change |
| Volume | Volume delta, relative volume, OBV trend |
| Structure | Swing high/low detection, liquidity sweeps, candle-pattern embeddings |

Everything is computed per timeframe and then concatenated, so a single training row carries the full 1H/4H/1D picture.

---

## Models

The classifier is swappable. Three are wired up out of the box:

- **RandomForest** — fast baseline, surprisingly hard to beat on tabular features, and easy to inspect.
- **XGBoost** — the workhorse for the gradient-boosted setup; best raw accuracy in my testing.
- **LSTM** — for when sequence order matters and you want the model to learn temporal patterns the tree models flatten away.

All three are trained to output class probabilities, which feed directly into a risk-based sizing layer (bigger size on higher conviction, scaled down near the neutral zone).

---

## Quick start

```bash
git clone https://github.com/HakimiFinance/Hakimi-AI-Trader.git
cd Hakimi-AI-Trader
pip install -r requirements.txt
```

Set your exchange keys in a local `.env` (never commit this file):

```env
BINANCE_API_KEY=your_key
BINANCE_API_SECRET=your_secret
```

Run a prediction on a single symbol:

```bash
python predict.py --symbol BTCUSDT --timeframes 1h 4h 1d
```

Train from scratch on your own history:

```bash
python train.py --model xgboost --symbol BTCUSDT --history 730d
```

Example output:

```
BTCUSDT  |  2024-XX-XX 14:00
  Bull    0.71
  Neutral 0.18
  Bear    0.11
  -> Regime: BULLISH (high confidence)
```

---

## Project structure

```
Hakimi-AI-Trader/
├── data/            # raw + cached market data
├── features/        # indicator and feature-engineering modules
├── models/          # model definitions and saved weights
├── pipeline/        # ingest -> fuse -> predict orchestration
├── dashboard/       # chart overlay / visualization
├── train.py
├── predict.py
└── requirements.txt
```

---

## Honest limitations

I'd rather be upfront than oversell this:

- **Low-volume assets overfit.** Thin order books produce garbage features. Stick to liquid pairs.
- **Live latency is real.** Feature computation + inference adds delay; this is a context tool, not an HFT engine.
- **Regimes drift.** Markets change, and a model trained on last year's conditions will decay. Retraining is not optional.
- **Interpretability is a work in progress.** Probabilities are easy to read; *why* the model produced them is not. SHAP integration is on the roadmap.

---

## Roadmap

- Reinforcement learning layer for adaptive strategy selection per regime
- Deploy as a cloud microservice with a clean REST API
- SHAP-based explanations so users can see what's driving each call
- Native TradingView visualization module

---

## Disclaimer

This is decision-support software. It is **not financial advice**, and nothing it outputs is a recommendation to buy or sell anything. Markets carry real risk of loss. Use it as one input among many, and trade your own account at your own risk.

---

## About

Built by **Hamid Hakimi** ([HakimiFinance](https://github.com/HakimiFinance)).

The approach draws on ICT and Smart Money Concepts on the trading side, and standard ML practice on the engineering side. Originally developed as the capstone for the *Building AI* course (Reaktor × University of Helsinki), now maintained as an ongoing project.

Open to collaboration — reach out at **hakimiifinance@gmail.com**.

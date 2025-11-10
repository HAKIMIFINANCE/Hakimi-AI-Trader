# Hakimi-AI-Trader

Final project for the Building AI course

## Summary
Hakimi-AI-Trader is a multi-timeframe AI-powered trading system designed to predict market direction and trend strength across crypto, forex, and commodities markets.  
It uses deep learning models, multi-timeframe data fusion, and advanced feature engineering to identify high-probability setups with smart risk control.

## Background
Most retail traders rely on single-timeframe indicators that lag and fail in volatile markets.  
This project addresses that by integrating multi-timeframe structure analysis (1H / 4H / 1D), regime classification (bullish, neutral, bearish), and machine learning models (RandomForest, LSTM, or Gradient Boosting) to produce probabilistic trend forecasts instead of fixed buy/sell signals.

From personal experience as a trader, the motivation is to build an adaptive model that helps traders interpret market structure objectively and improve consistency in decision-making.

## How is it used?
The model runs on live market data via Binance, CoinEx, or MetaTrader APIs.  
It calculates engineered features such as EMAs, RSI, volume delta, candle pattern embeddings, and liquidity sweeps.  
Multiple timeframes are combined to form a unified feature matrix.  
The AI then predicts trend probability (Bull / Bear / Neutral) and outputs visual feedback directly to a chart or dashboard.

Main users:
- Active day traders  
- Swing traders  
- Quantitative analysts  

## Data sources and AI methods
Data sources:
- Binance API for crypto assets  
- CoinEx and MetaTrader 4 for forex and commodities  
- Derived technical indicators (EMA, RSI, volume, etc.)  
- Python libraries such as scikit-learn, pandas, numpy, matplotlib  

AI methods:
- RandomForestClassifier and XGBoost for classification  
- LSTM for sequential pattern recognition  
- Probabilistic output for risk-based position sizing  

## Challenges
- Model overfitting on assets with low volume  
- Real-time latency during live inference  
- Requires continuous retraining as market regimes evolve  
- Difficulty in interpretability for end users  

Ethical consideration:  
AI predictions must be treated as decision-support tools, not financial advice.

## What next?
- Add reinforcement learning for adaptive strategy selection  
- Deploy the model as a cloud microservice with API access  
- Integrate explainable AI (e.g., SHAP) for model transparency  
- Create TradingView-compatible visualization modules  

## Acknowledgments
Created by Hamid Hakimi (HakimiFinance)  
Inspired by ICT, Smart Money Concepts, and algorithmic AI systems  
Built as part of the Building AI course by Reaktor x University of Helsinki  
Open for collaboration — contact: hakimiifinance@gmail.com

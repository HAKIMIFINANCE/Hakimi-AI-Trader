# Hakimi-AI-Trader

Final project for the **Building AI** course by Reaktor x University of Helsinki

---

##Summary
Hakimi-AI-Trader is a **multi-timeframe AI-powered trading system** designed to predict market direction and trend strength across crypto, forex, and commodities markets.  
It uses deep learning models, multi-timeframe data fusion, and advanced feature engineering to identify high-probability setups with smart risk control.

---

## 🔍 Background
The problem: most retail traders rely on one-timeframe indicators that lag and fail in volatile conditions.  
This project solves that by integrating:
* multi-timeframe structure analysis (1H / 4H / 1D),
* regime classification (bullish, neutral, bearish),
* and machine learning models (RandomForest, LSTM, or Gradient Boosting)  
to generate **probabilistic trend forecasts** rather than fixed buy/sell signals.

Personal motivation:  
As a professional trader, I wanted to build an adaptive model that helps traders read market structure objectively and improve consistency.

---

## ⚙️ How it is used
1. The model loads live market data (via Binance, CoinEx, or MetaTrader APIs).  
2. It calculates engineered features: EMAs, RSI, volume delta, candle pattern embeddings, and liquidity sweeps.  
3. Multiple timeframes are merged to form a unified feature matrix.  
4. The model predicts **trend probability** (Bull / Bear / Neutral).  
5. Output is visualized directly on a chart or dashboard.

Main users:
* Active day traders
* Swing traders
* Quantitative analysts

---

## 📊 Data sources and AI methods
| Source | Description |
|---------|-------------|
| Binance API | Live and historical crypto data |
| CoinEx / MetaTrader 4 | Forex and commodity price feed |
| Technical indicators | Engineered features |
| Python libraries | scikit-learn, pandas, numpy, matplotlib |

AI techniques used:
* RandomForestClassifier / XGBoost for direction classification  
* Recurrent LSTM for sequential pattern detection  
* Risk-based position sizing using probabilistic output

---

## 🚧 Challenges
* Model overfitting on low-volume assets  
* Real-time latency during live inference  
* Requires continuous retraining as market regimes evolve  
* Interpretability — turning black-box AI predictions into trader-friendly insights  

Ethical consideration:
Ensure that AI-generated signals are **decision-support tools**, not financial advice.

---

## 🚀 What next?
Future development plans:
* Add reinforcement learning for adaptive strategy selection  
* Deploy on a cloud microservice with API access  
* Integrate explainable AI (SHAP values) for model transparency  
* Develop a TradingView-compatible visualization layer  

---

## 🙌 Acknowledgments
* Created by **Hamid Hakimi** (HakimiFinance)  
* Inspired by ICT, Smart Money Concepts, and algorithmic AI systems  
* Built as part of the **Building AI Course Project**  
* Open for collaboration — contact: [hakimiifinance@gmail.com](hakimiifinance@gmail.com)

---

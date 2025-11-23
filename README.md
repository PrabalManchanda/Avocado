# Avocado — Cost of Living Intelligence

**Avocado** is an affordability intelligence engine that helps users understand the true cost of living in any major city. Designed for students, newcomers, families, and relocating professionals, Avocado provides a complete data-driven breakdown of all major lifestyle expenses and city conditions.

The platform analyzes real-time data, economic indicators, news sentiment, and a custom weighted ML model to generate the **AvoScore**, a 0–10 affordability index that reflects how financially livable a city is.

**AvoScore Legend**  
- **3 → Low cost**  
- **4–7 → Mid cost**  
- **8+ → Expensive**  

Live demo: **https://avocado.amanpurohit.com**
![Demo](./frontend/avocado-demo.gif)

---

## What Avocado Delivers

Avocado provides a consolidated, real-time snapshot of a city’s livability, including:

- Cost-of-living data across rent, groceries, dining, and transit  
- Purchasing power and economic stability  
- Crime, safety, transportation, and finance-related news  
- Live weather and environmental conditions  
- City sentiment computed from real-time news feeds  
- A machine-learning powered affordability score (AvoScore)  
- Gemini-powered conversational insights for interpretation  

The goal is simple:  
**Help users make informed, data-backed decisions about where to live.**

---

## AvoScore — The Affordability Engine

The AvoScore is produced through a hybrid weighted ML model that combines classification, regression, and sentiment analysis to deliver a stable, interpretable affordability measure.

### Feature Inputs

| Category | Features |
|----------|----------|
| Housing | Rent index, price-to-income ratio |
| Groceries | Grocery index |
| Dining | Restaurant index |
| Safety | Crime index, safe-walking-at-night score |
| Economics | Local purchasing power, employment volatility |
| Transport | Transit accessibility and cost |
| Weather | Climate & comfort score |
| Sentiment | VADER sentiment from real-time news |

---

## EDA & Preprocessing

Libraries and methods used:

- **pandas** — data ingestion, merging, cleanup  
- **numpy** — numerical transformations  
- **matplotlib**, **seaborn** — visualization and correlation analysis  
- **scikit-learn** — scaling, preprocessing, and baselines  
- **scipy** — outlier detection (IQR trimming)  
- **NLTK (VADER)** — sentiment analysis  
- **pycountry**, **geopy** — city validation and coordinate mapping  

---

## Modeling Approach

Avocado uses a two-stage ML pipeline:

### 1. Logistic Regression (Classification Baseline)
Predicts affordability tiers:
- Low  
- Medium  
- High  

### 2. XGBoost Regressor  
Generates a continuous affordability score.

### Weighted Ensemble Formula

```
AvoScore =
  (0.70 * XGBoost) +
  (0.15 * city_sentiment) +
  (0.10 * weather_comfort) +
  (0.05 * local_purchase_power)
```

This weighted method provides balanced predictions across diverse cities, smoother scoring, and improved generalization.

---

## Sample Classification Performance

```
               precision    recall   f1-score    support
Low              0.86       0.82      0.84         52
Medium           0.92       0.89      0.90         88
High             0.88       0.94      0.91         67

accuracy                                  0.89       207
macro avg         0.89       0.88      0.88
weighted avg      0.89       0.89      0.89
```

---

## System Architecture

```
                         AVOCADO SYSTEM ARCHITECTURE
                         ----------------------------------

                          ┌─────────────────────────────────┐
                          │          Frontend (Vercel)      │
                          │        Next.js + TypeScript UI   │
                          │  - City search                   │
                          │  - City detail pages             │
                          │  - AvoScore visualizations       │
                          └───────────────┬─────────────────┘
                                          │  HTTPS Fetch
                                          ▼
                   ┌────────────────────────────────────────────────────┐
                   │                 Backend (Cloud Run)                │
                   │       Python FastAPI in Docker Container           │
                   │             Auto-scaled via Cloud Run             │
                   ├───────────────┬──────────────────────┬────────────┤
                   │               │                      │            │
     ┌─────────────▼───────┐ ┌────▼────────────────┐ ┌────▼───────────────┐
     │  Weather Service     │ │  News Aggregation    │ │ ML Affordability    │
     │  WeatherAPI.com      │ │ NewsData / Currents  │ │ Engine (AvoScore)   │
     │                      │ │ Crime/Finance/       │ │ Weighted Model      │
     │                      │ │ Transport/Events     │ │ XGBoost + LR        │
     └──────────────────────┘ └──────────────────────┘ └────────┬───────────┘
                                                                 │
                                                  ┌──────────────▼──────────────┐
                                                  │       AvoScore API           │
                                                  │    0–10 Affordability Index  │
                                                  │        + Explanations        │
                                                  └──────────────────────────────┘
```

---

## AI Assistant (Gemini Integration)

Avocado uses Gemini to provide conversational explanations, comparisons, and real-time insights about:

- Affordability breakdowns  
- City-to-city comparisons  
- Risk and volatility (economic or environmental)  
- Forecast trends and city outlook  

This turns data into interpretable, user-friendly guidance.

---

## Why Avocado?

Affordability influences every aspect of daily life — housing, transportation, food, lifestyle, and even small decisions like whether you can buy an avocado. Avocado makes the affordability question clear, actionable, and data-driven.

It delivers financial transparency for anyone making a major life decision about where to live.

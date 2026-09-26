<div align="center">

# NYC Uber Pricing Optimization

**Using EDA and Linear Regression to identify pricing drivers and simulate a revenue-optimized fare strategy**

![Python](https://img.shields.io/badge/Python-3.11-1AC0A3?style=flat-square)
![Pandas](https://img.shields.io/badge/pandas-data%20cleaning-1AC0A3?style=flat-square)
![scikit--learn](https://img.shields.io/badge/scikit--learn-regression-1AC0A3?style=flat-square)
![Tableau](https://img.shields.io/badge/Tableau-dashboard-1AC0A3?style=flat-square)

[**View Dashboard**](#) &nbsp;•&nbsp;  [**Key Findings**](#key-findings)

</div>

---

## Summary

Analyzed 200,000 NYC Uber trip records using exploratory data analysis and Linear Regression to identify which factors actually drive fare price. Simulated six peak-hour surge pricing scenarios against real trip revenue and identified a strategy projected to **increase revenue by 10%** with no change to base fares.

| | |
|---|---|
| **Dataset** | 200,000 NYC Uber trip records (193,026 after cleaning) |
| **Techniques** | Data cleaning, feature engineering, EDA, Linear Regression, revenue simulation |
| **Model performance** | R² = 0.718, RMSE = $5.11 |
| **Business outcome** | +10% projected revenue uplift via targeted peak-hour surge pricing |

---

## Table of Contents

1. [Problem Statement](#problem-statement)
2. [Dataset](#dataset)
3. [Methodology](#methodology)
4. [Key Findings](#key-findings)
5. [Model Results](#model-results)
6. [Pricing Simulation](#pricing-simulation)
7. [Dashboard](#dashboard)
8. [Tech Stack](#tech-stack)
9. [Repository Structure](#repository-structure)

---

## Problem Statement

Uber's static, distance-based pricing may not fully reflect demand patterns across hours, days, and passenger volume. This project analyzes real NYC trip data to identify what actually drives fare price, and tests whether a demand-aware pricing adjustment can increase revenue without materially harming rider experience.

## Dataset

| Field | Description |
|---|---|
| `fare_amount` | Trip fare in USD |
| `pickup_datetime` | Trip start timestamp |
| `pickup_/dropoff_longitude`, `latitude` | GPS coordinates |
| `passenger_count` | Number of riders |

**200,000** raw records → **193,026** clean records retained (96.5%)

## Methodology

### 1 · Data Cleaning

| Issue | Rows Removed |
|---|---|
| Invalid fares (≤ $0) | 22 |
| Invalid passenger count (0 or 208) | 710 |
| GPS coordinates outside NYC bounding box | 4,211 |
| Zero-distance trips | remainder |

### 2 · Feature Engineering

- Extracted `hour`, `day_of_week`, `month`, `year`, `is_weekend` from pickup timestamp
- Calculated trip `distance_km` from GPS coordinates using the Haversine formula

### 3 · Modeling

**Target:** `fare_amount` &nbsp; | &nbsp; **Features:** `distance_km`, `passenger_count`, `hour`, `day_of_week`, `is_weekend` &nbsp; | &nbsp; **Split:** 80/20 train-test

## Key Findings

- **Demand peaks in the evening** — trip volume is highest between 6–10 PM, with hour 19 (7 PM) the busiest hour of the day, plus a secondary midday peak at hour 13
- **Distance is the dominant fare driver** — by far the strongest relationship with fare amount of any variable tested
- **Weekend fares are underpriced** — holding distance and time constant, weekend trips price lower than weekday trips: a pricing gap, not a demand gap

## Model Results

| Feature | Coefficient | Interpretation |
|---|---|---|
| `distance_km` | **+2.19** | Dominant driver — each additional km adds ~$2.19 |
| `day_of_week` | +0.09 | Minor positive effect |
| `passenger_count` | +0.05 | Minor positive effect |
| `hour` | +0.01 | Negligible direct effect |
| `is_weekend` | **−0.67** | Weekend trips priced $0.67 lower, all else equal |

**Performance:** R² = 0.718 &nbsp;·&nbsp; RMSE = $5.11

## Pricing Simulation

A peak-hour surge multiplier (hours 13, 18–22 — the top-6 busiest hours) was applied to baseline revenue of **$2,189,900** across six scenarios:

| Surge Multiplier | Revenue Uplift |
|---|---|
| 5% | 1.67% |
| 10% | 3.33% |
| 14% | 5.00% |
| 19% | 6.67% |
| 25% | 8.33% |
| **30%** | **10.00%** |

> **Recommendation:** A 30% peak-hour surge is projected to increase revenue by 10% — achieved purely by concentrating pricing power in the hours demand data shows are already busiest, with no change to pricing at any other time.


## Tech Stack

- **Python** — pandas, numpy, scikit-learn, matplotlib, seaborn
- **Tableau** — interactive dashboard for demand and pricing visualization
- **Statistical methods** — Linear Regression, correlation analysis, revenue simulation

## Repository Structure

```
uber-pricing-optimization-nyc/
├── data/                          # raw and cleaned datasets
├── notebooks/
│   └── 01_data_cleaning_eda.ipynb # cleaning, EDA, modeling, simulation
├── outputs/                       # exported charts, dashboard.png
├── tableau/                       # Tableau data extracts + dashboard
├── uber_pricing_optimization.pptx # portfolio presentation
└── README.md
```

---

<div align="center">

*Portfolio project — feel free to reach out with questions or feedback.*

</div>

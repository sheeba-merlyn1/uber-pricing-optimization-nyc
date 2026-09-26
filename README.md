# uber-pricing-optimization-nyc


NYC Uber Pricing Optimization

Analyzed 200,000 NYC Uber trip records using EDA and Linear Regression to identify key pricing drivers and evaluate fare strategies. Proposed a pricing model demonstrating a potential 10% revenue increase through peak-hour surge pricing.

📊 View Interactive Dashboard on Tableau Public (add your Tableau Public link here)

📑 View Full Presentation

Problem Statement

Uber's static, distance-based pricing may not fully reflect demand patterns across hours, days, and passenger volume. This project analyzes real NYC trip data to identify which factors actually drive fare price, and tests whether a demand-aware pricing adjustment could increase revenue without materially harming rider experience.

Dataset
Source: NYC Uber fare dataset, 200,000 raw trip records
Raw fields: fare amount, pickup/dropoff GPS coordinates, pickup timestamp, passenger count
Final clean dataset: 193,026 rows (96.5% retained)
Methodology
1. Data Cleaning
Issue	Rows Removed
Invalid fares (≤ $0)	22
Invalid passenger count (0 or 208)	710
GPS coordinates outside NYC bounding box	4,211
Zero-distance trips	remainder
2. Feature Engineering
Extracted hour, day_of_week, month, year, is_weekend from pickup timestamp
Calculated trip distance_km from GPS coordinates using the Haversine formula
3. Exploratory Data Analysis
Demand peaks in the evening — trip volume highest between 6–10 PM, with hour 19 (7 PM) the busiest hour
Distance is the strongest fare driver of all variables tested
Weekend fares are priced lower than weekday fares at equivalent distance/time — a pricing gap, not a demand gap
Midday secondary peak at hour 13 (1 PM)
4. Modeling — Linear Regression

Target: fare_amount Features: distance_km, passenger_count, hour, day_of_week, is_weekend

Feature	Coefficient
distance_km	+2.19
day_of_week	+0.09
passenger_count	+0.05
hour	+0.01
is_weekend	-0.67

Performance: R² = 0.718, RMSE = $5.11

5. Pricing Simulation

Applied a peak-hour surge multiplier (hours 13, 18–22 — the top-6 busiest hours) to baseline revenue of $2,189,900 across six scenarios:

Surge Multiplier	Revenue Uplift
5%	1.67%
10%	3.33%
14%	5.00%
19%	6.67%
25%	8.33%
30%	10.00%

Recommendation: A 30% peak-hour surge is estimated to increase revenue by 10%, balancing meaningful gain against rider-experience impact.

Tech Stack
Python — pandas, numpy, scikit-learn, matplotlib, seaborn
Tableau — interactive dashboard for demand and pricing visualization
Statistical Methods — Linear Regression, correlation analysis, revenue simulation
Repository Structure
uber-pricing-optimization-nyc/
├── data/                          # raw and cleaned datasets
├── notebooks/
│   └── 01_data_cleaning_eda.ipynb # cleaning, EDA, modeling, simulation
├── outputs/                       # exported charts
├── tableau/                       # Tableau data extracts + dashboard
├── uber_pricing_optimization.pptx # portfolio presentation
└── README.md
Key Findings
Trip distance is by far the dominant driver of fare price
Demand is heavily concentrated in the evening rush window (6–10 PM) plus a midday peak at 1 PM
Weekend trips are currently underpriced relative to weekday trips at equivalent distance and time
A targeted 30% surge during the six busiest hours of the day is projected to increase total revenue by 10%, without changing pricing at any other time

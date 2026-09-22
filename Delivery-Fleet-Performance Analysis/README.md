# Delivery Fleet Performance

**Project #1 — Data Collaboration Portfolio (Logistics)**

SQL + Power BI: Bolu &nbsp;|&nbsp; Excel + Python (EDA): Gracie

## Overview

This project analyzes last-mile delivery performance using Amazon's public delivery dataset, looking at how area type, vehicle, weather, traffic, and agent characteristics affect delivery time. It's Project #1 of a shared 20-project tracker built with Gracie, part of a broader 30-project data analytics self-study roadmap.

## Dataset

**Amazon Delivery Dataset (Kaggle):**
[kaggle.com/datasets/sujalsuthar/amazon-delivery-dataset](https://www.kaggle.com/datasets/sujalsuthar/amazon-delivery-dataset)

| Field | Description |
|---|---|
| `Order_ID` | Unique order identifier |
| `Agent_Age`, `Agent_Rating` | Delivery agent's age and customer rating |
| `Store/Drop Latitude & Longitude` | Pickup and drop-off coordinates |
| `Order_Date`, `Order_Time`, `Pickup_Time` | Order and pickup timestamps |
| `Weather`, `Traffic` | Conditions at time of delivery |
| `Vehicle`, `Area`, `Category` | Delivery vehicle type, area classification, product category |
| `Delivery_Time` | Target metric — total delivery time in minutes |

## Workflow

### Step 1 — SQL (Bolu)
- Loaded raw CSV into PostgreSQL via pgAdmin (`\copy`)
- Cleaned NaN values (Excel pass + `NULLIF`/`TRIM` handling for stray whitespace in `Order_Time`/`Pickup_Time`)
- Verified row counts and per-column null counts post-load
- Built aggregate queries: avg `Delivery_Time` by Area, Vehicle, Weather × Traffic, Agent_Rating bucket, Agent_Age bucket

### Step 2 — Power BI (Bolu)
- Connected Power BI directly to the PostgreSQL table
- Built `Age_Brackets` and `Rating_Brackets` as conditional columns (with null-handling for missing `Agent_Rating`)
- Dashboard: KPI card panel, Area/Vehicle/Rating-bracket charts, Weather × Traffic view, Count of Orders by Month, Area/Weather/Traffic slicers
- Styled using Amazon's brand palette (`#FF9900` orange, `#131A22` dark navy, white/light-gray backgrounds)

### Step 3 — Excel + Python EDA (Gracie)
- Cross-checked the SQL exports in Excel pivot tables
- Charted delivery-time distributions and correlations in Python (pandas, seaborn) for the write-up

## Key Findings

- **Semi-Urban areas take dramatically longer** than any other area (238.6 min avg) — more than double the next-slowest category (Metropolitan, 129.7 min). Single biggest gap in the dataset.
- **"Jam" traffic is consistently the slowest condition** across every weather type (142–175 min), confirming Traffic as a strong driver of delivery time.
- **Sunny + Medium traffic** is the fastest recorded combination (96.0 min); **Cloudy + Jam** is the slowest (174.6 min).
- **Agents rated 4.5+ deliver noticeably faster** than every other rating bucket — about 50 minutes quicker than Low-rated agents (115.5 vs 174.1 min).
- Vehicle and Agent Age effects are real but smaller and less consistent than Area/Traffic/Rating — flagged for further exploration in Gracie's EDA rather than treated as conclusive.

## Data Quality Notes

- Trailing whitespace in Area/Weather/Traffic text values needed trimming before grouping/filtering worked cleanly
- A small number of rows had both Weather and Traffic blank — kept as an "Unknown"-style combination rather than dropped
- `Agent_Rating` had missing values; handled with an explicit Unknown bucket rather than defaulting them into the highest bracket
- `Agent_Age` had zero missing values — confirmed via null count before bucketing

## Tools Used

| Tool | Role |
|---|---|
| PostgreSQL | Data cleaning, aggregation, staging (Bolu) |
| Power BI | Interactive dashboard, conditional columns, slicers (Bolu) |
| Excel | Pivot table cross-checks (Gracie) |
| Python (pandas, seaborn) | Exploratory charts for the write-up (Gracie) |

## Next Steps

- Fix minor chart title typos ("Wether" → "Weather", "Order M onth" → "Order Month")
- Consider converting the Weather × Traffic line chart to a matrix/heatmap for clearer pattern visibility
- Rename report page from "Page 1" to "Delivery Fleet Performance"
- Move to Project #2: Warehouse Inventory Optimization

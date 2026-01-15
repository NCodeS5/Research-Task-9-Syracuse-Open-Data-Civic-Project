# Research-Task-9-Syracuse-Open-Data-Civic-Project


# Snowed In: Analyzing Vacancy and Winter Accessibility in Syracuse (Phase 3)

A civic data project using Syracuse Open Data to analyze **where vacant properties are concentrated** across Syracuse neighborhoods and to frame **winter accessibility risk** in a realistic, neighborhood-level way. The project also includes a lightweight, explainable **machine learning classifier** to flag neighborhoods with **high vacancy concentration** (top quartile) for prioritization and planning.

---

## Project Motivation

Vacant properties can signal disinvestment, safety concerns, and redevelopment opportunity. In a city like Syracuse—where winter conditions can affect mobility and emergency response—understanding **where vacancy is concentrated** is essential for:

- prioritizing neighborhood revitalization,
- planning winter service delivery,
- supporting community development strategies.

---

## Data Sources

- **Vacant Properties** (`Vacant_Properties.csv`)  
  Contains records of vacant properties (already filtered to vacant listings) with neighborhood, address, ZIP, owner fields, and coordinates.
- **Emergency Snow Routes** (`Emergency_Snow_Routes.csv`)  
  A GIS-based route/segment dataset representing emergency snow corridors.

> Note: These datasets represent different structures (parcel/address vs corridor/GIS segments). See **Methodology Note** below.

---

## What This Project Produces

### Key Outputs
- `neighborhood_vacancy_summary.csv`  
  Neighborhood vacancy counts + residential/commercial split + citywide share.
- `neighborhood_vacancy_winter_risk_summary.csv`  
  Final neighborhood-level “winter risk context” table (concentration of vacancy).
- `neighborhood_vacancy_ml_predictions.csv`  
  ML-based neighborhood classification (high vacancy risk vs lower).

### Key Visuals
- Top 15 neighborhoods by vacant property count  
- Neighborhood share of citywide vacancy (risk context)  
- Pareto curve (cumulative concentration)

---

## Methodology (Phase 3)

### 1) Analysis Pipeline (Raw → Clean → Analyze)
1. Load datasets  
2. Validate schema + missingness  
3. Aggregate vacant properties at neighborhood level  
4. Compute vacancy share citywide + ranking  
5. Visualize vacancy concentration  
6. Train a simple ML model (logistic regression) as an **exploratory classifier**

### 2) Winter Accessibility Integration (Important)
Initial attempts to match vacant properties to emergency snow routes at the **property/street level** produced **no valid matches**. This reflects a structural mismatch between:
- address-based parcels (`PropertyAddress`)
- GIS-based corridor segments (snow routes)

To avoid misleading precision, this Phase 3 analysis pivots to a **neighborhood-level framework**, using vacancy concentration as a winter risk context rather than claiming property-level snow-route proximity.

### 3) Machine Learning (Optional Enhancement)
A lightweight model predicts whether a neighborhood is **High Vacancy Risk (top quartile)** using:
- `vacant_properties`
- `residential`
- `commercial`

> This model does **not** predict future vacancy or causality. It is an exploratory classifier for prioritization.

---

## Repository Structure (Recommended)

```text
.
├── data/
│   ├── raw/
│   │   ├── Vacant_Properties.csv
│   │   └── Emergency_Snow_Routes.csv
│   └── outputs/
│       ├── neighborhood_vacancy_summary.csv
│       ├── neighborhood_vacancy_winter_risk_summary.csv
│       └── neighborhood_vacancy_ml_predictions.csv
├── notebooks/
│   └── Snowed_In_Analyzing_Vacancy_and_Winter_Accessibility_in_Syracuse_Phase_3.ipynb
├── docs/
│   ├── TECHNICAL.md
│   └── METHODOLOGY.md
├── requirements.txt
└── README.md

# EV Charging Demand Forecasting & Dynamic Tariff Optimization

![Python](https://img.shields.io/badge/python-3.8%2B-blue.svg)
![Jupyter](https://img.shields.io/badge/jupyter-%23FA0F00.svg?style=flat&logo=jupyter&logoColor=white)
![Machine Learning](https://img.shields.io/badge/Machine%20Learning-Agentic%20AI-orange)
![Pandas](https://img.shields.io/badge/pandas-Data_Engineering-150458?logo=pandas)
![License](https://img.shields.io/badge/license-MIT-green)

## Comprehensive Overview

Electric vehicle (EV) charging infrastructure currently suffers from a critical inefficiency: **static pricing**. Fixed tariffs ignore real-time network demand, spatial congestion, and station-level operational variations, leading to overloaded stations during peak hours and underutilized stations during off-peak windows. 

This project solves this limitation by introducing an **Agentic AI Framework for EV Charging Networks**. Designed as an end-to-end operational pipeline, this system does not just forecast demand—it actively simulates business decisions to optimize network health. 

**Core Capabilities:**
1. **Predictive Intelligence:** Forecast future demand, occupancy rates, and congestion risk.
2. **Network Monitoring:** Identify which stations are structurally overloaded or underutilized using spatial graph structures.
3. **Dynamic Tariffing:** Automatically generate optimized pricing actions based on live and predicted network conditions.
4. **Feedback Loop:** Continuously evaluate operational outcomes (revenue, wait times, utilization) to refine future decisions.

---

## Project Preview & Visuals

*(Note: Replace the placeholder image links with actual paths to your charts/screenshots located in the `figures/` folder)*

### 1. Demand Prediction vs. Actuals
> High-accuracy forecasting across 24-hour cycles.
> ![Demand Forecast Preview](figures/forecast_preview_placeholder.png)

### 2. Dynamic Tariff Simulation 
> Demonstrating how localized surge pricing redistributes demand and reduces peak congestion.
> ![Tariff Simulation Preview](figures/tariff_impact_placeholder.png)

### 3. Spatial Network Graph (UrbanEV)
> Mapping the proximity and influence of neighboring charging stations.
> ![Network Graph Preview](figures/network_graph_placeholder.png)

---

## Datasets & Data Engineering

This system processes two highly granular, official EV datasets:

* **ACN-Data (Adaptive Charging Network):** * **Scope:** >30,000 charging sessions from Caltech/JPL sites.
    * **Granularity:** Session-level (timestamps, energy delivered, session duration, station IDs, user behavior).
* **UrbanEV / ST-EVCDP:** * **Scope:** Large-scale urban network featuring 24,798 charging piles.
    * **Granularity:** 5-minute interval data. Crucial for extracting temporal demand variation, spatial charging behavior, and peak-hour localized congestion.

### The Data Pipeline
The **Data Layer** unifies these disparate formats into a single, master `station-time` tabular dataset. This involves timestamp alignment, missing value imputation, and merging spatial coordinates to build a graph representation of the physical network.

---

## Multi-Agent Architecture

Unlike standard regression models, this project utilizes a multi-agent framework to simulate autonomous decision-making:

1.  ** Demand Prediction Agent:** The predictive core. It ingests historical and engineered features to predict exact charging demand, station occupancy, and the probability of severe congestion at specific hours.
2.  ** Dynamic Tariff Agent:** The economic engine. It applies logic-based rules (and uncertainty thresholds) to the Demand Agent's predictions to recommend pricing changes—such as applying surcharges during overloads or discounts during off-peak windows.
3.  ** Monitoring Agent:** The evaluator. It measures the simulated effect of tariff changes on revenue, charger utilization, proxy wait times, and overall pricing efficiency.
4.  ** Coordinator Agent:** The orchestrator. It merges outputs from all sub-agents into a unified operational dashboard for stakeholders.

---

## Feature Engineering Dictionary

To achieve high predictive performance, the system constructs a rich spatio-temporal feature space:

| Feature Category | Engineered Variables | Purpose |
| :--- | :--- | :--- |
| **Temporal Signals** | Hour, weekday/weekend flags, month, cyclic time encoding (sin/cos). | Captures daily human routines and seasonal EV charging habits. |
| **Lag & Rolling** | Previous step demand/occupancy, rolling 24h means, rolling standard deviations. | Provides the model with short-term historical context and momentum. |
| **Spatial & Graph** | Nearest neighbor distance, average distance to top 3 neighbors, distance-weighted neighbor pressure. | Understands geographic density and if nearby stations can absorb overflow. |
| **Network Centrality** | Degree centrality, betweenness centrality, clustering coefficient, community ID. | Identifies "critical hub" stations vs. isolated edge stations. |
| **Economic/Congestion** | Congestion index, demand pressure, estimated baseline revenue. | Translates physical charging limits into actionable business metrics. |

---
## Modeling & Forecasting Engine

The forecasting layer relies on a time-aware, tabular prediction system. We move beyond simple time-series (like ARIMA) to robust tree-based models capable of handling high-dimensional, non-linear relationships.

* **Baseline Models:** Random Forest, XGBoost, LightGBM.
* **Advanced Techniques:** * **Ensemble Forecasting:** Combining base model predictions to reduce variance.
    * **Uncertainty Estimation:** Quantifying prediction confidence to prevent the Tariff Agent from making aggressive price changes based on low-confidence forecasts.

---

## Evaluation & Business Metrics

The system's success is evaluated across two distinct paradigms:

**1. Predictive Performance (How accurate is the AI?)**
* **MAE & RMSE:** Absolute and squared error of energy demand.
* **R²:** Variance explained by the model.
* **MAPE:** Percentage error for scale-independent evaluation.

**2. Operational Performance (How much value does it create?)**
* **Revenue Gain (%):** Simulated uplift in gross revenue against a static-price baseline.
* **Charger Utilization Rate:** Ensuring price hikes do not crash overall usage.
* **Off-Peak Uplift:** Measuring successful demand shifting to cheaper hours.
* **Waiting-Time Reduction:** Proxy metric for customer satisfaction and reduced queueing.

### Ablation Studies
To prove the necessity of the complex feature engineering, the notebook includes rigorous ablation tests. We systematically remove graph features, spatial features, and uncertainty features to benchmark how heavily the model relies on network-aware intelligence (Results confirm spatial features significantly reduce MAE).

---

## Repository Structure

```text
EV-Charging-Dynamic-Tariff/
│
├── README.md                                 # Project documentation
├── requirements.txt                          # Python dependencies
│
├── notebooks/
│   └── EV_Charging_Dynamic_Tariff_Project.ipynb  # Main end-to-end execution notebook
│
├── data/
│   ├── raw/                                  # Drop raw UrbanEV/ACN-Data here
│   └── processed/                            # Master station-time tables output here
│
├── outputs/                                  # Generated business logic & results
│   ├── evaluation_summary.csv
│   ├── final_results_table.csv
│   ├── forecast_results.csv
│   ├── dynamic_tariff_outputs.csv
│   └── ablation_results.csv
│
├── models/                                   # Serialized model artifacts
│   ├── xgboost.pkl
│   ├── lightgbm.pkl
│   └── random_forest_ensemble.pkl
│
└── figures/                                  # Visualizations for the presentation deck
    ├── forecast_vs_actual.png
    ├── tariff_impact_heatmap.png
    └── feature_importance_plot.png

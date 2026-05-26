An end-to-end intelligent system for forecasting EV charging demand, optimizing tariffs dynamically, and monitoring network performance using spatio-temporal data, graph structure, and agent-based decision logic.

Overview

Electric vehicle charging infrastructure is often priced using static tariffs that ignore real-time demand, spatial congestion, and station-level operational variation. This project addresses that limitation by building an agentic AI framework for EV charging networks that can:

predict future demand and congestion,
identify overloaded and underutilized stations,
optimize pricing dynamically based on network conditions,
monitor operational outcomes,
and continuously refine tariff decisions through feedback.

The project is designed as a full pipeline rather than a single model. It combines data engineering, exploratory analysis, forecasting, network intelligence, tariff optimization, and evaluation into one coherent system. The brief explicitly frames the system around demand prediction, optimal tariffing, and a monitoring/learning loop that improves revenue, utilization, and wait times.

Why this project matters

EV charging networks are not static systems. Demand varies by:

time of day,
day of week,
location,
charger type,
local congestion,
neighboring station usage,
and pricing conditions.

A fixed tariff cannot respond to this variation. This project builds a dynamic decision engine that uses historical and real-time patterns to recommend better charging prices, reduce congestion, and improve overall charging efficiency. The objective is not only predictive accuracy, but also operational improvement and business value.

Key objectives

This project is built to answer the following questions:

How does charging demand evolve over time?
Which stations are overused or underused?
How do nearby stations influence each other?
What tariff should be used under different congestion regimes?
Can dynamic pricing increase revenue without harming utilization?
Can an agent-based system learn from outcomes and improve future decisions?

The brief asks for demand forecasting, dynamic tariff optimization, charger utilization analysis, congestion reduction, and autonomous pricing intelligence with a feedback loop.

Datasets used

The project uses two official datasets:

1) ACN-Data (Adaptive Charging Network)

A session-level dataset with EV charging sessions, timestamps, energy delivered, session duration, station IDs, and user behavior. It is provided in JSON format and can be converted into tabular form for analysis. The brief notes that it contains more than 30,000 charging sessions from Caltech/JPL sites.

2) UrbanEV / ST-EVCDP

A large-scale urban charging dataset with 24,798 charging piles and 5-minute interval data. It is useful for analyzing temporal demand variation, spatial charging behavior, and peak-hour congestion. The brief identifies this dataset as the main source for urban station-level demand patterns.

Project architecture

The system is organized into five major layers:

1. Data Layer

Loads and aligns all source files into a unified station-time dataset.

2. Feature Engineering Layer

Creates temporal, lag, rolling, congestion, economic, and graph-based features.

3. Forecasting Layer

Predicts future charging demand, occupancy, and congestion risk.

4. Dynamic Tariff Layer

Uses predictions to determine station-wise pricing actions.

5. Monitoring and Learning Layer

Evaluates outcomes and feeds performance back into the system.

This architecture matches the brief’s emphasis on a self-improving agentic framework rather than a standalone regression model.

What the system does

The full pipeline performs the following steps:

Load and clean all charging network data.
Build a unified spatio-temporal station-time table.
Engineer time, demand, congestion, spatial, graph, and economic features.
Explore trends, station behavior, and network structure.
Train forecasting models for demand prediction.
Combine predictions into an ensemble forecast.
Estimate uncertainty and high-risk congestion periods.
Generate dynamic tariff recommendations.
Simulate revenue and utilization impact.
Evaluate forecasting and pricing performance.
Run ablation tests to verify which advanced features matter most.
Core agents
Demand Prediction Agent

Predicts future charging demand, station occupancy, and congestion behavior using historical and engineered features.

Dynamic Tariff Agent

Uses predicted demand and congestion to recommend pricing changes such as surcharges during overload and discounts during off-peak windows.

Monitoring Agent

Measures the effect of tariff changes on revenue, utilization, waiting-time proxy, and pricing efficiency.

Coordinator Agent

Combines outputs from all agents into one unified operational decision layer.

The brief specifically requires a demand prediction agent, a tariff pricing agent, and a monitoring/learning agent, with a self-improving feedback loop.

Feature engineering highlights

This project includes a rich feature set designed for spatio-temporal and operational learning:

Temporal features: hour, weekday, weekend, month, cyclic time encoding
Lag features: previous demand and occupancy values
Rolling features: rolling mean and rolling standard deviation
Congestion features: congestion index, demand pressure
Spatial features: nearest neighbor distance, mean neighbor distance
Network features: degree centrality, betweenness centrality, closeness centrality, clustering coefficient, community ID
Neighbor features: distance-weighted neighbor pressure
Economic features: estimated revenue, price change percentage, pricing efficiency

These engineered signals are used to improve forecasting quality and make tariff optimization context-aware.

Modeling approach

The forecasting layer is designed as a time-aware tabular prediction system.

Baseline models
Random Forest
XGBoost
LightGBM
Advanced methods
Ensemble forecasting
Uncertainty estimation
Multi-horizon forecasting
Congestion risk prediction

The goal is not only to predict the next demand value, but also to build a realistic forecasting engine that can support decision-making. The brief asks for demand forecasting using historical session features and evaluation using RMSE, MAE, and R².

Dynamic tariff logic

The tariff agent uses predicted demand, congestion risk, uncertainty, and network health to determine station-wise pricing actions.

Typical tariff actions include:

surge pricing during severe congestion,
price increases during high demand,
discounts during low demand,
stable pricing in balanced regions,
protection of critical network hubs.

The brief also specifies tariff logic that raises prices when utilization is high and lowers them when utilization is low, with the overall goal of maximizing revenue while reducing congestion and wait times.

Evaluation metrics

The project evaluates itself using both predictive and operational metrics.

Forecasting metrics
MAE
RMSE
R²
MAPE
Tariffing metrics
Revenue Gain %
Charger Utilization Rate
Off-Peak Uplift
Pricing Efficiency Score
Monitoring metrics
Average Waiting-Time Reduction
Customer Response Rate
Network Health Score
Price Change Impact

The brief lists the same categories of evaluation, including revenue gain, charger utilization, off-peak uplift, waiting-time reduction, and pricing efficiency.

Robustness and ablation studies

To verify that the advanced components actually help, the project includes ablation tests such as:

removing graph features,
removing spatial features,
removing uncertainty features,
comparing results against the full model.

This makes the work more rigorous and helps prove that the graph-aware and spatially-aware design improves performance.

Results summary

The current implementation produced strong results:

forecasting error is low,
ensemble forecasting is stable,
tariffing increases simulated revenue,
monitoring outputs are bounded and interpretable,
graph/network features improve the overall intelligence of the system.

The final notebook includes all major summaries, charts, and evaluation tables for easy review.

Repository structure

A clean repository layout can look like this:

.
├── README.md
├── notebooks/
│   └── EV_Charging_Dynamic_Tariff_Project.ipynb
├── data/
│   ├── raw/
│   └── processed/
├── outputs/
│   ├── evaluation_summary.csv
│   ├── final_results_table.csv
│   ├── forecast_results.csv
│   ├── dynamic_tariff_outputs.csv
│   └── ablation_results.csv
├── models/
│   ├── xgboost.pkl
│   ├── lightgbm.pkl
│   └── random_forest.pkl
└── figures/
How to run
Open the notebook in Google Colab.
Mount Google Drive or upload the CSV files into the Colab session.
Run the setup cells.
Load and inspect the data.
Build the master station-time table.
Run feature engineering.
Train forecasting models.
Run tariff optimization.
Evaluate the multi-agent system.
Export outputs and final results.
Deliverables

The project is structured to produce the following deliverables:

clean, reproducible notebook code,
saved outputs in CSV form,
presentation-ready charts,
trained forecasting models,
final evaluation tables,
ablation study comparisons,
and a concise presentation deck.

The brief explicitly lists code/notebooks, outputs in CSV files, and a 5–7 slide presentation as deliverables, along with supporting visualizations and appendix analysis.

Presentation deck contents

The presentation should include:

problem and motivation,
data landscape,
preprocessing decisions,
demand behavior insights,
forecasting results,
tariff optimization logic,
monitoring and feedback performance,
business and policy implications,
robustness checks.

These are exactly aligned with the deliverable expectations in the project brief.

Limitations

This project is designed as a forecasting-and-simulation system. It does not claim full causal impact unless explicitly supported by a causal design. The brief specifically asks that causal claims be avoided unless clearly justified, and that assumptions and limitations be stated transparently.

Future work

Possible extensions include:

reinforcement learning for tariff optimization,
real-time deployment on live charging data,
geospatial demand forecasting,
fairness-aware pricing,
vehicle-routing integration,
policy optimization under grid constraints,
simulation of larger urban charging networks.

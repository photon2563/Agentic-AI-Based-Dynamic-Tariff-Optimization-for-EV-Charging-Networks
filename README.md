# Agentic AI-Based Dynamic Tariff Optimization for EV Charging Networks

An end-to-end intelligent EV charging ecosystem that combines:

- Spatio-temporal demand forecasting  
- Multi-agent AI decision systems  
- Graph/network intelligence  
- Dynamic tariff optimization  
- Congestion-aware infrastructure management  

to improve:
- charging efficiency,
- revenue generation,
- congestion reduction,
- and operational stability.

---

# Overview

Electric vehicle charging networks are highly dynamic systems. Demand fluctuates continuously depending on:

- time of day,
- station location,
- charger type,
- traffic intensity,
- neighboring station behavior,
- occupancy levels,
- and pricing conditions.

However, most charging systems still rely on **static pricing mechanisms** that fail to adapt to real-time operational conditions.

This project addresses that limitation by building an **agentic AI framework** capable of:

 1. predicting future charging demand  
 2. detecting congestion before overload occurs  
 3. dynamically optimizing charging tariffs  
 4. monitoring network health continuously     
 5. balancing utilization across stations  
 6. simulating operational and revenue outcomes  

The system is designed as a **full intelligent infrastructure pipeline** rather than a standalone ML model.

---

# Key Features

## Advanced Forecasting System

The forecasting engine predicts:

- future charging demand,
- occupancy levels,
- congestion risk,
- and high-load periods.

### Models Used
- Random Forest
- XGBoost
- LightGBM
- Weighted Ensemble Forecasting

### Advanced Forecasting Capabilities
- Multi-horizon forecasting
- Forecast uncertainty estimation
- Confidence interval generation
- Peak-hour forecasting
- Congestion-aware evaluation

---

# Graph + Spatial Intelligence

Unlike traditional EV forecasting projects, this system integrates:

## Graph Intelligence
- Degree Centrality
- Betweenness Centrality
- Closeness Centrality
- Community Detection
- Network Health Scoring

## Spatial Intelligence
- Neighbor influence modeling
- Distance-weighted congestion propagation
- Spatial charging pressure estimation
- Regional load balancing analysis

These features help the system understand:
- how congestion spreads,
- which stations are bottlenecks,
- and how nearby stations influence demand behavior.

---

# Dynamic Tariff Optimization

The project implements a **dynamic pricing engine** that adjusts tariffs based on:

- predicted future demand,
- congestion risk,
- occupancy levels,
- network criticality,
- and forecast uncertainty.

## Pricing Behaviors
- Surge pricing during overload
- Price increases during high demand
- Discounts during underutilization
- Off-peak promotional pricing
- Critical hub protection pricing

The goal is to:
- maximize revenue,
- reduce congestion,
- balance charger utilization,
- and improve operational efficiency.

---

# Multi-Agent AI System

The system is built using multiple cooperating intelligent agents.

## Forecast Agent
Predicts future charging demand and uncertainty.

## Congestion Agent
Estimates overload risk using:
- occupancy,
- graph structure,
- neighbor pressure,
- and predicted demand.

## Tariff Agent
Determines optimal pricing actions dynamically.

## Recommendation Agent
Suggests:
- load redistribution,
- congestion mitigation,
- promotional pricing,
- and critical hub protection.

## Monitoring Agent
Tracks:
- network health,
- pricing impact,
- operational stability,
- and congestion intensity.

## Coordinator Agent
Combines outputs from all agents into a unified operational decision system.

---

# System Architecture

```text
Raw EV Charging Data
        ↓
Data Cleaning + Alignment
        ↓
Unified Spatio-Temporal Table
        ↓
Feature Engineering
        ↓
EDA + Graph Intelligence
        ↓
Forecasting Engine
        ↓
Ensemble + Uncertainty Layer
        ↓
Dynamic Tariff Optimization
        ↓
Multi-Agent Decision System
        ↓
Monitoring + Evaluation
        ↓
Operational Outputs

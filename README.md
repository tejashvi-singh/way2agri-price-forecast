# Way2Agri Monthly Price Forecasting Project

## Problem Statement
The objective of this project is to forecast the average monthly agricultural prices for the next 12 months using historical data. These predictions allow Way2Agribusiness to optimize inventory decisions, secure procurement contracts, and improve price realization for farmers.

## Modeling Approach
1. **Classical Baseline (SARIMAX):** Leveraged a statistical seasonal model to capture fundamental cyclic trends.
2. **Machine Learning Benchmark (Random Forest):** A lag-based Random Forest model (lag_1 to lag_12) was implemented to better handle nonlinear seasonal fluctuations and sudden structural regime shifts.

**Final Result:** The lag-based Random Forest model outperformed the baseline, achieving a final Mean Absolute Percentage Error (MAPE) of **13.33%** on the hold-out test set.

## Project Structure & Deployment Support Files
- `notebooks/agri_price_forecasting_assignment.ipynb`: The complete end-to-end data science workflow (cleaning, EDA, modeling, forecasting).
- `api/fastapi_app.py`: A lightweight FastAPI microservice starter for high-performance model inference.
- `django_notes/deployment_architecture.md`: Detailed system design covering the Django backend, FastAPI integration, and frontend consumption.

## Production Monitoring
The deployment architecture ensures continuous accuracy via:
- Input data drift monitoring.
- Ongoing MAPE tracking against newly realized prices.
- Automated monthly retraining and threshold-based trigger retraining.
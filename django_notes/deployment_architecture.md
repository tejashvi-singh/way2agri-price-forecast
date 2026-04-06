# Production Deployment Architecture

This document outlines the system integration and production deployment strategy for the Way2Agri Price Prediction system.

## 1. Django Responsibilities
- **Data Management & Admin:** Django acts as the core application serving the internal admin dashboard and handling relational data (user accounts, crop profiles, static data).
- **Authentication:** Handles JWT/Session auth for users and API clients.
- **Workflow Orchestration:** Coordinates cron jobs for data fetching and schedules retraining pipelines.

## 2. FastAPI Microservice Responsibilities
- **High-Performance Inference:** Serves the serialized Random Forest model (`.pkl` file via `joblib`) through lightweight, async `/predict` endpoints.
- **Data Validation:** Enforces strict Pydantic schemas (e.g., ensuring all `lag_1` through `lag_12` features are passed correctly).
- **Scalability:** Capable of horizontally scaling independently of the slower Django admin layer to handle high query volume.

## 3. Frontend Integration (Next.js / React Native)
- **Web Dashboard (Next.js):** Provides deep-dive analytical charts for business analysts to visualize 12-month forecasts.
- **Mobile App (React Native):** Delivers fast, real-time price alerts and summarized forecasts directly to field agents and farmers.

## 4. Production Monitoring & Drift Tracking
- **Data Drift:** Monitor inputs (`lag` features) to ensure the current market data distribution remains similar to the training data.
- **Concept Drift:** Continuously track the Mean Absolute Percentage Error (MAPE) against real-world realized prices.
- **System Metrics:** Track FastAPI endpoint latency and 500-error rates during inference.

## 5. Retraining Triggers
- **Scheduled:** Triggers automatically on a monthly schedule when newly realized monthly prices become available.
- **Threshold-Based:** Triggers mid-cycle if the MAPE exceeds the acceptable 15% threshold for multiple consecutive observation windows, indicating a sudden structural market shift.

# Methodology - FBO Operations Intelligence Dashboard

## Overview

This project uses public FAA airport operations data and aviation facilities metadata as a proxy for FBO service demand. Since actual FBO service event data is proprietary, the approach models operational pressure using publicly available airport movement statistics.

## Data Sources

- FAA ATADS: itinerant_air_carrier, itinerant_air_taxi, itinerant_general_aviation, local_civil, total_operations for TEB/HPN/PWK, 2024-2025
- FAA Aviation Facilities (NTAD): airport IDs, ICAO codes, coordinates, state

## Processing Steps

1. Load both Excel files using pandas
2. Standardise column names to lowercase with underscores
3. Filter to TEB, HPN, PWK only
4. Attempt ICAO join (0 matches due to code format differences) then airport ID join
5. Engineer FBO-relevant traffic = air_taxi + general_aviation
6. Compute YoY growth per airport per traffic type
7. Normalise columns to 0-1 for composite scoring

## Metric Formulas

### FBO Exposure Ratio
FBO Exposure Ratio = (itinerant_air_taxi + itinerant_general_aviation) / total_operations

### FBO Workload Score
FBO Workload Score = 0.50 x norm(itinerant_general_aviation) + 0.30 x norm(itinerant_air_taxi) + 0.20 x norm(total_operations)

Weights reflect operational judgement: GA creates broadest FBO demand, air taxi second, total ops as baseline volume.

### YoY Growth
YoY Growth (%) = ((2025 value - 2024 value) / 2024 value) x 100

### Sensitivity Simulation
Simulated +10% increase in itinerant_air_taxi for 2025, recomputed Workload Score, measured delta per airport.

## Limitations

- FAA ATADS provides annual totals only - no hourly granularity
- All metrics are proxy models, not measured FBO service volumes
- ATADS-to-facilities merge had key mismatch; metadata columns are null for most rows
- Only two years of data available; trend analysis is directional
- Metric weights are assumption-based and should be validated with real FBO records

## Extensions

- Add OpenSky hourly movement data
- Add weather data from Open-Meteo
- Extend to more Signature Aviation network airports
- Add Prophet/XGBoost forecasting layer
- Deploy as Streamlit app

*All analysis conducted in Google Colab using Python (pandas, matplotlib, seaborn).*

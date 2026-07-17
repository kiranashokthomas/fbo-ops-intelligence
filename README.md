# FBO Operations Intelligence Dashboard

> **A Signature Aviation-style case study** — analysing Fixed Base Operator (FBO) service pressure at three key U.S. business aviation airports using public FAA data.

![Python](https://img.shields.io/badge/Python-3.10-blue) ![Data](https://img.shields.io/badge/Data-FAA%20ATADS-orange) ![Status](https://img.shields.io/badge/Status-Active-green) ![Domain](https://img.shields.io/badge/Domain-Aviation%20Operations-lightblue)

---

## Project Overview

This project builds an FBO Operations Intelligence prototype using public FAA airport operations data and FAA aviation facilities metadata. It was designed as an end-to-end aviation analytics case study modelled on the operational needs of a Signature Aviation-style private aviation terminal network.

Signature Aviation operates 200+ private aviation terminals globally, providing aircraft handling, fueling, and flight support services. The core operational challenge for any FBO is predicting **when and where service pressure will be highest** so that staffing, fuel trucks, ramp space, and customer support can be positioned correctly.

This project answers that question using public data.

---

## Business Problem

> *Which airports create the highest FBO service pressure, and what does that mean for resource planning?*

An FBO does not care equally about every aircraft movement. A commercial airline turnaround is handled by the airline's own ground crew. It is the **itinerant air taxi and general aviation movements** — private jets, charter flights, and business aviation — that drive FBO demand for fueling, ramp handling, hangar services, lounge support, and crew assistance.

This project reframes raw FAA airport operations data into FBO-specific metrics to answer that question.

---

## Airports Analysed

| Airport | Code | Why Selected |
|---|---|---|
| Teterboro Airport, New Jersey | **TEB** | Flagship U.S. business aviation gateway; Signature FBO location; nearly all movements are business/GA aviation |
| Westchester County Airport, New York | **HPN** | High-value Northeast business aviation market; strong growth in FBO-relevant traffic |
| Chicago Executive Airport, Illinois | **PWK** | Signature FBO location; stable corporate/GA aviation profile; regional contrast to TEB and HPN |

---

## Data Sources

| Dataset | Source | What It Provides |
|---|---|---|
| FAA ATADS Airport Operations | FAA (opsnet.faa.gov) | Yearly counts of air carrier, air taxi, general aviation, and local operations per airport |
| FAA Aviation Facilities | FAA / Data.gov | Official aerodrome metadata — IDs, ICAO codes, coordinates, facility attributes |

> All data is public. No proprietary FBO service data was used. This is an intentional proxy model designed to simulate FBO operational intelligence from available public sources.

---

## Key Metrics for FBO Operations

### 1. FBO Exposure Ratio
```
FBO Exposure Ratio = (Itinerant Air Taxi + Itinerant General Aviation) / Total Operations
```
Measures what proportion of an airport's total movements are the types that directly generate FBO service demand. A higher ratio means the airport is more "FBO-heavy" — more of its traffic needs fueling, ramp handling, and customer services.

### 2. FBO Workload Score
```
FBO Workload Score = 0.50 x norm(Itinerant GA) + 0.30 x norm(Air Taxi) + 0.20 x norm(Total Ops)
```
A weighted composite that estimates overall service pressure on FBO staff, fuel trucks, and facilities. Combines volume with the intensity of FBO-relevant traffic types.

### 3. Year-on-Year Growth in FBO-Relevant Traffic
Tracks change in air taxi and general aviation movements from 2024 to 2025, identifying airports where FBO demand is rising and where proactive capacity planning is most critical.

### 4. Sensitivity to Air Taxi Fluctuations
Simulates a 10% increase in air taxi movements at each airport and measures the resulting change in FBO Workload Score. Identifies which airports are most exposed to short-term surges in business aviation traffic.

---

## Key Findings

### TEB — Structural High-Pressure FBO Location
- Nearly **100% of operations are FBO-relevant** (air taxi + general aviation).
- **Highest FBO Workload Score** across all three airports in both 2024 and 2025.
- **Most sensitive** to air taxi surges: a 10% increase in air taxi movements produces the largest workload score jump of the three airports.
- Despite a slight decline in total operations YoY (-0.96%), TEB remains the highest-pressure FBO environment by a significant margin.
- **Implication:** FBOs at TEB must maintain highly specialised staffing, efficient ramp control, and agile fueling capacity at all times.

### HPN — Growth-Pressure FBO Location
- **Fastest year-on-year growth** in FBO-relevant traffic: air taxi up +13.67%, general aviation up +1.20%.
- Total operations grew +4.24% from 2024 to 2025.
- Rising demand signals need for proactive FBO capacity planning, potential fuel storage expansion, and turnaround optimisation.
- **Implication:** HPN is the growth market. FBO investment and expansion planning should prioritise HPN to avoid bottlenecks as demand rises.

### PWK — Stable FBO Environment
- Significant FBO traffic mix but **more moderate growth** (+2.44% total operations).
- **Lower sensitivity** to air taxi fluctuations than TEB or HPN.
- More predictable day-to-day operational profile.
- **Implication:** PWK warrants consistent service quality and maintenance of current staffing levels, with less urgency for reactive capacity changes.

---

## Operational Summary Table

| Airport | FBO Exposure Ratio | FBO Workload Score | YoY Total Ops Growth | Air Taxi YoY Growth | Sensitivity Rank |
|---|---|---|---|---|---|
| TEB | Highest (~100%) | Highest | -0.96% | Low | 1st (most sensitive) |
| HPN | High | Mid | +4.24% | +13.67% | 2nd |
| PWK | Moderate | Lowest | +2.44% | Moderate | 3rd (most stable) |

---

## Notebook Structure

```
notebooks/
  fbo_service_pressure.ipynb
    - Section 1: Data Loading & Inspection
    - Section 2: Cleaning & Merging (ops_df)
    - Section 3: FBO Metrics (Exposure Ratio, Workload Score)
    - Section 4: Traffic Mix Analysis
    - Section 5: Year-on-Year Growth Analysis
    - Section 6: Sensitivity Simulation
    - Section 7: Visualisations
    - Section 8: Operational Summary & Findings
```

---

## Repository Structure

```
fbo-ops-intelligence/
  data/
    atads/          # FAA ATADS airport operations exports (Excel)
    metadata/       # FAA Aviation Facilities CSV
  notebooks/
    fbo_service_pressure.ipynb
  figures/          # Chart exports and dashboard screenshots
  reports/
    key_findings.md
    methodology.md
  README.md
  .gitignore
  requirements.txt
```

---

## Tools & Stack

| Tool | Purpose |
|---|---|
| Python (Pandas, NumPy) | Data loading, cleaning, feature engineering |
| Matplotlib / Seaborn | Visualisations |
| Google Colab | Development environment |
| FAA ATADS | Primary operations dataset |
| FAA Aviation Facilities | Airport metadata |
| GitHub | Version control and portfolio hosting |

---

## Limitations & Honest Scope

- This is a **public-data proxy model**. No proprietary FBO service timestamps, fuel volumes, or turnaround records were used.
- FAA ATADS provides airport-level yearly totals. Hourly or per-movement granularity would require additional data sources.
- The FBO Workload Score is a modelled metric based on FAA public data — it should be recalibrated with internal service event data if deployed operationally.
- Business aviation movement coverage varies by public source; completeness cannot be fully verified.

---

## How This Relates to Signature Aviation

Signature Aviation operates the world's largest network of private aviation FBO terminals, providing aircraft handling, fueling, lounge services, and flight support at 200+ locations. The metrics in this project are designed around the types of questions an FBO network operations team would ask:

- Where is our service demand most concentrated?
- Which locations are growing fastest and need proactive investment?
- How sensitive are our busiest locations to surges in business aviation traffic?

This project demonstrates how public FAA data can be translated into FBO-oriented operational intelligence to support staffing, fueling, and network-level planning decisions.

---

## Author

**Kiran Ashok Thomas**  
MSc Aviation Digital Technology & Management — Cranfield University (Distinction)  
GitHub: [kiranashokthomas](https://github.com/kiranashokthomas)  
LinkedIn: [linkedin.com/in/kiranashokthomas](https://linkedin.com/in/kiranashokthomas)

---

*Built as part of an aviation analytics portfolio. All data is sourced from public FAA databases.*

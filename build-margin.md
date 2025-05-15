# Build Margin

## Adjusting Prior‑Year Hourly Build‑Margin (BM) Data for Future‑Year Applications

### Introduction

The Granular Registry regularly relies on ClimateTRACE’s hourly Build‑Margin (BM) emissions‑rate dataset to quantify avoided emissions when current‑year BM data have not yet been released. This section explains how the 2023 BM series was adapted for 2024 reporting of a sample wind farm in ERCOT.

The wind farm’s output is strongly correlated with other wind generation in ERCOT; consequently, hours when the plant produces are also hours when incremental capacity additions on the grid are largely zero‑carbon. A simple around‑the‑clock average of BM would therefore overstate El Campo’s avoided emissions. To capture this temporal nuance while mitigating inter‑annual weather volatility, we:

1. **Compute generation‑weighted monthly BM averages for 2023.**
2. **Map each hour of 2024 generation to the BM average of its calendar month.**

This “generation‑profile anchoring” lowered the wind farm’s effective BM by roughly **30 %** versus a flat 2023 average, demonstrating the method’s ability to differentiate technologies and regions (e.g., wind in CAISO vs. solar in CAISO). The following sections document the data sources, calculation steps, quality assurances, and limitations.

***

### 1. Data Sources

| Dataset                     | Vintage     | Resolution | Provider                          | Notes                                       |
| --------------------------- | ----------- | ---------- | --------------------------------- | ------------------------------------------- |
| Hourly BM emissions factors | 2023        | 1‑hour     | ClimateTRACE                      | kg CO₂e ⁄ MWh; nodal granularity for ERCOT. |
| Project metered generation  | 2023 & 2024 | 1‑hour     | Plant SCADA / ISO settlement data | Net generation (MWh).                       |

***

### 2. Detailed Procedure

#### 2.1 Data Cleaning

* Drop BM hours flagged by ClimateTRACE with quality codes ‘Q’, ‘I’ or ‘E’.
* Forward‑fill single‑hour gaps (< 3 h); remove longer gaps from both series.
* Exclude generation hours coinciding with planned outages (> 0.5 h) or market curtailments.

#### 2.2 Time Alignment

Both series are converted to **UTC** and daylight‑saving transitions are reconciled.&#x20;

#### 2.3 Generation‑Weighted Monthly BM

For month _m_:

BMm=∑h∈mGh×BMh∑h∈mGh\mathrm{BM}\_m = \frac{\sum\_{h\in m} G\_h \times BM\_h}{\sum\_{h\in m} G\_h}

where GhG\_h is net generation and BMhBM\_h is BM (kg CO₂e/MWh). Output: 12 monthly factors with version metadata.

#### 2.4 Apply Monthly BM to 2024 Generation

Assign BMm(h)2023 GWBM\_{m(h)}^{2023\\,\text{GW\}} to each 2024 hour _h_, producing an 8 760‑row synthetic 2024 BM series.

***

### 3. Rationale

* **Technology bias correction** – Prevents overstatement where wind generation coincides with low‑carbon grid mix.
* **Temporal representativeness** – Monthly bins smooth extreme weather while preserving seasonal shape.
* **Data availability** – Enables timely reporting prior to ClimateTRACE’s Q4 release of new‑year BM data.

***

### 4. Limitations & Mitigations

| Issue                                       | Impact                | Mitigation                                                 |
| ------------------------------------------- | --------------------- | ---------------------------------------------------------- |
| Structural grid changes (e.g., retirements) | Under/over‑estimation | Sensitivity run with ERCOT marginal‑emissions projections. |
| Residual intra‑monthly covariance           | Bias                  | Explore weekly weighting when multi‑year data mature.      |
| ClimateTRACE revisions                      | Factor drift          | Lock factors via dataset ID; flag updates in registry.     |

***

### References

* ClimateTRACE v2024‑01 ERCOT nodal BM dataset.
* Clean Incentive Granular Registry – Methodology v2.1.
* GHG Protocol **Project Accounting Guidelines** (§ B.2 Combined Margin).

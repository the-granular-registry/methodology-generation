# Build Margin

## Definition & Importance

**Build‑Margin** represents the _long‑run_ marginal emissions intensity of the grid. It is calculated as the generation‑weighted average CO₂e‑per‑MWh of **newly built or credibly planned** power‑plant capacity that would have generated, or will generate, in the absence of the project under study. In the GHG Protocol’s _combined‑margin_ framework, BM pairs with the _Operating Margin (OM)_ to capture both short‑run dispatch and long‑run capacity‑planning effects.

### Why BM Matters for Carbon Impact Accounting

* **Structural signal** – BM reflects the carbon characteristics of _capacity additions_, not just moment‑to‑moment dispatch. A project displacing future fossil builds can have a higher impact than merely displacing existing low‑carbon generation.
* **Technology differentiation**—The hourly BM series exposes when zero‑carbon resources compete against each other (e.g., overlapping wind) versus when they offset high‑carbon speakers. This granularity makes avoided‑emissions claims more credible.
* **Policy relevance** – Emerging granular accounting standards encourage or require combined‑margin approaches. Accurate BM factors are therefore pivotal for registry‑grade certificate issuance.
* **Investment signaling** – Investors use BM‑adjusted avoided‑emissions metrics to rank projects and direct capital toward technologies with the most significant long‑term decarbonisation leverage.

## Adjusting Prior‑Year Hourly Build‑Margin (BM) Data for Future‑Year Applications

### Introduction

The Granular Registry regularly relies on ClimateTRACE’s hourly Build‑Margin (BM) emissions‑rate dataset to quantify avoided emissions when current‑year BM data have not yet been released. This section explains how the 2023 BM series was adapted for 2024 reporting of a sample wind farm in ERCOT.

The wind farm’s output is strongly correlated with other wind generation in ERCOT; consequently, hours when the plant produces are also hours when incremental capacity additions on the grid are largely zero‑carbon. A simple around‑the‑clock average of BM would therefore overstate El Campo’s avoided emissions. To capture this temporal nuance while mitigating inter‑annual weather volatility, we:

1. **Compute generation‑weighted monthly BM averages for 2023.**
2. **Map each hour of the 2024 generation to the BM average of its calendar month.**

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

Both series are converted to **UTC,** and daylight‑saving transitions are reconciled.&#x20;

#### 2.3 Generation‑Weighted Monthly BM

For month _m_:

$$
{BM}_m = \frac{\sum_{h\in m} G_h \times BM_h}{\sum_{h\in m} G_h}
$$

where GhG\_h is net generation and BMhBM\_h is BM (kg CO₂e/MWh). Output: 12 monthly factors with version metadata.

#### 2.4 Apply Monthly BM to 2024 Generation

Assign BMm(h)2023 GWBM\_{m(h)}^{2023\\,\text{GW\}} to each 2024 hour _h_, producing an 8,760-row synthetic 2024 BM series.

***

### 3. Rationale

* **Technology bias correction** – Prevents overstatement where wind generation coincides with low‑carbon grid mix.
* **Temporal representativeness** – Monthly bins smooth extreme weather while preserving seasonal shape.
* **Data availability** – Enables timely reporting before ClimateTRACE’s Q4 release of new‑year BM data.

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

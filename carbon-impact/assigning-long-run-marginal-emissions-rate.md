# Assigning Long Run Marginal Emissions Rate

## Overview

The Granular Registry employs the [GHG Protocol’s Project Accounting framework](https://ghgprotocol.org/project-protocol) to calculate and assign a combined marginal emissions rate—referred to here as the **Long Run Marginal Emissions Rate (Long Run MER)**—to each issued Granular Certificate (GC). This approach combines both short-term operational dynamics (Operating Margin) and long-term structural grid changes (Build Margin).

* **Operating Margin (OM)** for the change in emissions from how an action affects how existing power plants _operate._
* **Build Margin (BM)** for the change in emissions from how an action affects how much of which type of new power plants get _built_.

The registry adopts the standard GHG Protocol weighting of 50% Operating Margin (OM) and 50% Build Margin (BM), providing a balanced perspective that accurately reflects both immediate dispatch impacts and future capacity expansions induced by incremental generation or load.

## Methodology Details

### **Operating Margin (OM)**

* The OM reflects the short-run marginal emission rate derived from real-time or near-real-time dispatch data.
* It captures the emissions intensity of the marginal fossil fuel units actually operating in each hour.
* OM data is sourced from authoritative system operators or recognized market data providers on an hourly basis.

### **Build Margin (BM)**

The BM is calculated using the [ClimateTRACE Marginal Build Emissions Rate (MBER) methodology](https://www.gem.wiki/MBERs_methodology), aligned closely with GHG Protocol project accounting standards:

* **Scope & Data:** The BM identifies the emissions intensity of the last 20% of newly built generation capacity within a specified grid region. This capacity represents a robust proxy for the type of power plants most likely to be built next in response to increases in electricity demand.
* **Calculation Steps:**
  1. Compile a comprehensive dataset of all power plants within the relevant grid boundary, including start year, capacity, generation, and CO2 emissions.
  2. Identify the most recent consecutive years where cumulative generation reaches at least 20% of total grid generation and includes at least five new generation units.
  3. Sum total emissions and generation for this identified cohort.
  4. Calculate the BM emission rate by dividing total emissions by total generation for this subset.

### **Temporal Granularity**

* Ideally, hourly BM data is applied to each GC. However, recognizing that current-year hourly BM data may not always be available in a timely manner, the registry adopts the following fallback approach:
  * **Primary:** Use hourly BM emission factors calculated for the current year.
  * **Fallback:** If current-year hourly data is unavailable, the registry uses the monthly average BM emission factor calculated from the previous calendar year.

This approach balances precision with practical data availability constraints.

### Calculation of the Long Run MER

The registry calculates the Long Run MER for each GC using the standardized weighting formula from the GHG Protocol:

$$
\text{Long Run MER (kg CO}_2\text{/MWh)} = 0.5 \times \text{OM (kg CO}_2\text{/MWh)} + 0.5 \times \text{BM (kg CO}_2\text{/MWh)}
$$

Each GC issued by the Granular Registry will explicitly include this calculated Long Run MER, which will be clearly documented and transparently communicated to all stakeholders.

#### Rationale and Benefits

* **Credibility:** Aligns fully with the widely recognized and respected GHG Protocol project accounting framework, enhancing confidence in emissions claims.
* **Transparency:** Clear methodological guidelines ensure all stakeholders understand precisely how emissions rates are derived.
* **Practicality & Scalability:** The standardized 50/50 weighting and fallback monthly average ensure the approach remains globally scalable and implementable across diverse regions, even when current-year data is limited.

By adopting this standardized Long Run MER approach, the Granular Registry ensures that each GC credibly reflects short-term operational realities and long-term structural changes in the intensity of power grid emissions.

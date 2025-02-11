# Emissions Data Selection Process

## **Objective**

This specification outlines the methodology for combining each PEC with the Marginal Emissions Rate (MER) based on the location and hour of generation. The goal is to calculate the carbon impact for each PEC by multiplying the energy amount by the corresponding MER. The registry automates the selection of the most accurate and appropriate MER data sources to eliminate complexity and bias for corporate renewable energy buyers.

## **Registry's Emissions Data Selection Process**

**PEC Alliance Advisory Board Role**

* **Responsibilities:**
  * Evaluate and select the most accurate and appropriate MER data sources for each region.
  * Maintain and update a reference table mapping regions to selected data providers.
  * Consider user feedback and emerging data sources.
* **Selection Criteria:**
  * **Accuracy and Reliability:**\
    Preference for data providers with proven track records.
  * **Alignment with Registry Objectives:**\
    Data should support the registry's goal of precise, hourly carbon impact calculation.
  * **Compliance with Standards:**\
    Ensure data sources comply with international standards and best practices.

## **Handling Multiple Data Providers**

**Regional Selection**

* **Reference Table:**
  * The registry maintains a reference table mapping each region to its selected MER data provider.
*   **Example Table Format:**

    <table><thead><tr><th width="139">Region</th><th width="110">Data Provider</th><th width="139">Model Type</th><th>Time Resolution</th><th>Locational Resolution</th></tr></thead><tbody><tr><td>India - West</td><td>WattTime</td><td>Statistical</td><td>Hourly</td><td>Zonal</td></tr><tr><td>USA - PJM</td><td>REsurety</td><td>Dispatch</td><td>Hourly</td><td>Nodal</td></tr><tr><td>Germany</td><td>UNFCCC</td><td>Heat Rate</td><td>Annual</td><td>Country</td></tr></tbody></table>

## **Emissions Data Providers**

* Current Data Providers:
  * REsurety
  * WattTime
  * UNFCCC (United Nations Framework Convention on Climate Change)
* Selection Criteria:
  * Accuracy
  * Transparency
  * Data Availability
  * Model Scope and Type
  * Time and Locational Resolution

***

## **Model Scope**

**Historical Short-Run Marginal Emissions:**\
Focus on the immediate impact of changes in electricity demand or supply on emissions, reflecting the emissions rate of the marginal generator.

## **Model Types**

**Statistical Models:**

* **Description:**\
  Utilize regression analysis to determine how changes in load, locational marginal price (LMP), and time factors affect generation by fuel type.
* **Strengths:**
  * Can capture complex relationships and patterns in data.
  * Flexible in incorporating various influencing factors.
* **Considerations:**
  * Requires high-quality historical data.
  * May be less transparent due to model complexity.

**Dispatch Models:**

* **Description:**\
  Estimate marginal emissions at nodal resolution based on grid operators' standard LMP calculations, simulating how generators are dispatched to meet demand.
* **Strengths:**
  * Reflects actual grid dispatch practices.
  * High locational granularity.
* **Considerations:**
  * Dependent on detailed grid operation data.
  * May require significant computational resources.

**Heat Rate Models:**

* **Description:**\
  Calculate emissions using LMP, fuel prices (e.g., natural gas), and assumptions about the relationship between generator costs and emissions (heat rates).
* **Strengths:**
  * Simpler to implement with readily available data.
  * Provides reasonable estimates when detailed dispatch data is unavailable.
* **Considerations:**
  * Relies on assumptions that may not capture real-time operational nuances.
  * Less accurate for grids with diverse generation mixes.

## **Time Resolution**

* **Hourly:**
  * **Preference:**\
    High time resolution aligns with the hourly granularity of PECs.
  * **Benefits:**
    * Captures temporal variations in emissions rates.
    * More accurate reflection of grid dynamics.
* **Annual:**
  * **Use Cases:**\
    May be considered when hourly data is unavailable.
  * **Limitations:**
    * Masks short-term fluctuations.
    * Less precise for calculating carbon impact of specific PECs.

## **Locational Resolution**

* **Nodal:**
  * **Description:**\
    Emissions rates calculated for specific nodes (connection points) on the grid.
  * **Benefits:**
    * Highest spatial accuracy.
    * Reflects local grid conditions.
* **Zonal:**
  * **Description:**\
    Emissions rates averaged over larger zones within the grid.
  * **Benefits:**
    * Balances granularity with data availability.
    * Easier to manage than nodal data.
* **Balancing Authority:**
  * **Description:**\
    Emissions rates for the entire area managed by a grid operator.
  * **Benefits:**
    * Simplifies data management.
    * Suitable when finer granularity is unnecessary or unavailable.
* **Country Level:**
  * **Description:**\
    National average emissions rates.
  * **Limitations:**
    * Too coarse for accurate PEC-level calculations.
    * Not recommended for hourly REC registries.

## **Data Availability**

* **Near Real-Time:**
  * **Benefits:**\
    Provides the most current emissions data, enhancing accuracy.
  * **Use Cases:**\
    Ideal for registries requiring immediate data integration.
* **Monthly/Quarterly/Annual Releases:**
  * **Considerations:**\
    May introduce delays in data availability.
  * **Limitations:**\
    Less aligned with the need for timely carbon impact calculations.

### **Transparency**

* **Preference for Data Published by Grid Operators and Open-Source Models:**
  * **Reasons:**
    * Enhances trust and credibility.
    * Allows for independent verification.
  * **Transparency Metrics:**
    * Availability of methodology documentation.
    * Accessibility of underlying data.
    * Openness of modeling assumptions.

***

## **Data Provider Integration**

* **Technical Integration:**
  * Establish data feeds or APIs with selected providers.
  * Ensure data is ingested in a format compatible with the registry's systems.
* **Data Validation:**
  * Implement checks to verify data integrity.
  * Monitor for updates or changes in data provider methodologies.

***

## **User Transparency and Communication**

**Data Source Disclosure**

* **Information Provided:**
  * Data provider name.
  * Model type and scope.
  * Time and locational resolution.
  * Date of data publication.
* **Purpose:**
  * Enhance user trust.
  * Allow users to understand how carbon impacts are calculated.

**Emissions Data Updates**

* **Regular Updates:**
  * Update MER data as new releases become available.
  * Communicate significant changes or updates to users.
* **Change Management:**
  * Document changes in data sources or methodologies.
  * Provide impact assessments if changes affect carbon impact calculations.

***

***

## **Quality Assurance and Compliance**

**Data Quality Checks**

* **Validation Procedures:**
  * Cross-reference MER data with historical trends.
  * Check for anomalies or discrepancies.
* **Audit Trails:**
  * Maintain logs of data retrieval and calculation processes.

### **Regulatory Compliance**

* **Standards Alignment:**
  * Ensure the methodology aligns with international standards (e.g., GHG Protocol).
* **Reporting Obligations:**
  * Provide necessary reports to regulatory bodies as required.

***

## **Technical Implementation**

**System Architecture**

* **Data Integration Layer:**
  * APIs or data pipelines to ingest MER data from providers.
* **Calculation Engine:**
  * Automated system to perform carbon impact calculations upon PEC issuance or data updates.

***

### **Data Storage and Reporting**

* **Record Keeping:**
  * Store calculated carbon impacts alongside PEC records.
  * Maintain audit trails for data sources and calculation steps.
* **User Access:**
  * Provide users with access to carbon impact data for their PECs.
  * Include details on the MER data source and calculation methodology.

***

## **Conclusion**

Integrating MER with PECs enhances the value proposition of the hourly REC registry by providing precise, actionable carbon impact data. By automating data source selection and adhering to rigorous standards, the registry ensures accuracy, transparency, and reliability for corporate renewable energy buyers and other stakeholders.

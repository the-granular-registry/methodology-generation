# Meter Data Quality Checks

## **Time Interval Consistency**

* **Check for missing timestamps:** Ensure that all hourly intervals are accounted for without missing entries.
* **Check for duplicate timestamps:** Each timestamp should only appear once, representing a single observation for that hour.
* **Verify uniform intervals:** Ensure that the data points are evenly spaced with a consistent interval of one hour.

## **Data Completeness**

* **Identify missing values:** Look for any missing or NaN (Not a Number) values in the dataset. Missing data should be flagged, interpolated, or imputed as appropriate.
* **Check for zero values:** Validate whether zero values are legitimate or represent data errors.

## **Units and Format Consistency**

* **Verify units of measurement:** Ensure that all the data is in megawatt-hours (MWh) and convert any data that may be recorded in other units (e.g., kilowatt-hours).
* **Check for proper numeric format:** Ensure that the values are numerical, and any unexpected data types (e.g., text, special characters) are identified and corrected.

## **Value Range Validation**

* **Check for positive and negative values:** Positive values should represent generation, and negative values should represent consumption. Check if these conditions are respected.
* **Detect extreme or unrealistic values:** Flag any extreme or outlier values that may indicate erroneous readings (e.g., negative values for generation or excessively large values).

## **Data Consistency**

* **Cross-check with Project Metadata:** To ensure consistency, compare the data with project metadata, such as nameplate capacity.
* **Ensure temporal continuity:** Validate that the power generation and consumption follow expected patterns (e.g., gradual increases or decreases, no abrupt spikes unless justified).

## **Handling Anomalies**

* **Detect and correct anomalies:** Identify and document potential data entry errors or device malfunctions (e.g., meter resetting) that may cause anomalies in the data.
* **Outlier detection:** Implement statistical methods to identify and potentially remove or investigate outliers that could skew results.

{% hint style="info" %}
Out of range meter values are replaced with zero value.
{% endhint %}

## **Check for Consistent Data Availability Across Meters**

* **Ensure synchronization between multiple meters:** If data is collected from multiple power meters, ensure that each meter provides data for the same time intervals.

#### **Validation of Negative Consumption Data**

* **Consumption validation:** For periods showing negative values (indicating consumption), cross-validate against other consumption data sources or historical trends to ensure correctness.

{% hint style="info" %}
For CFE generation, power consumption is excluded from the process. All negative values are replaced with zero values.&#x20;
{% endhint %}

## **Data Timestamp Verification**

* **Verify time zone accuracy:** Ensure that the timestamps are aligned correctly with the expected time zone and that daylight saving time shifts are accounted for.
* **Handle potential time shifts:** Identify any discrepancies due to meter resets or synchronization issues (i.e. daylight savings time).

## **Check Data Provenance**

* **Verify data source and reliability:** Ensure that the data is coming from a reliable source and that any transformations or pre-processing steps are documented and traceable.

Documenting these data quality checks in the methodology ensures transparency of the PEC registry.

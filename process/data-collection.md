# Data Collection

This specification outlines the requirements and process for receiving hourly interval meter generation data from registered producers as part of the PEC registry's monthly or quarterly submission cycle.&#x20;

## 1. **Submission Frequency**

* **Data submission periods:** Producers are required to submit data either **monthly** or **quarterly**, as determined by the frequency of REC issuance.
* **Submission deadline:** Data submissions must be received by **10 days** after the end of the reporting period (monthly or quarterly).
* **Grace period:** An additional 5 days will be allowed for late submissions. After this, the submission will be marked as overdue.

## 2. **Data Format**

* **File format:** Data should be submitted in a machine-readable format such as **CSV, XML, or JSON**.
  * **File naming convention**: `ProjectID_year_month.csv`
* **Column headers (for CSV):** The data file must contain the following headers:
  * `Timestamp` – in ISO 8601 format (e.g., `2024-01-01T00:00:00Z`)
  * `Generation (MWh)` – positive values for generation, negative for consumption
  * `Meter_ID` – unique identifier for the meter
  * `PEC Project_ID` – unique identifier for the project, consistent with the onboarding metadata
* **Time zone:** All timestamps must be provided in **UTC** unless otherwise specified in the onboarding metadata.

## 3. **Submission Process**

* **Submission portal:** Producers must upload data through the REC registry web portal.
* **API submissions:** Producers also have the option to submit data via an API integration. The API endpoint and token will be provided during project onboarding.
* **Manual upload:** Producers without automation capabilities can manually upload data files via the web interface.

## 4. **Data Content Requirements**

* **Time interval:** Data must be submitted for **hourly intervals**.
* **Units:** All energy generation and consumption values must be expressed in **megawatt-hours (MWh)**.
* **Data validation rules**:
  * **Positive values**: Generation values must be positive.
  * **Negative values**: Consumption values must be negative.
  * **No zero values**: Zero values are only acceptable in cases where the system was non-operational (e.g., during downtime). Otherwise, they may indicate an error and should be flagged for review.
  * **No missing hours**: Each hour in the reporting period must have a corresponding data point.

## 5. **Quality Control Requirements**

* **Automated data checks**: Submitted data will undergo the following automated checks upon receipt:
  * **Time interval consistency**: Ensure there are no missing hours.
  * **Data completeness**: Verify all required fields are populated.
  * **Data format validation**: Ensure the data is in the correct format (e.g., proper timestamp formatting, numeric generation values).
  * **Outlier detection**: Flag any data points that deviate significantly from historical patterns or expected ranges.
* **Manual review**: In the case of flagged data, the producer may be required to provide additional documentation or resubmit corrected data.

## 6. **Data Resubmission**

* **Correction window**: Producers will have up to **10 business days** from the notification of errors to resubmit corrected data.
* **Flagging mechanism**: Producers will be notified via email or the portal about data quality issues that require resolution.
* **Versioning**: Resubmitted data will overwrite the previous submission, and the new version will be tracked in the system.

## 7. **Metadata Requirements**

* **Project metadata consistency**: Submitted data must match the metadata provided during onboarding, including:
  * Project ID
  * Meter ID
  * Installed capacity
* **Cross-referencing**: Data submission will be automatically cross-checked with the project’s onboarding details, including expected ranges for generation.

## 8. **Security and Authentication**

* **User authentication**: Only authorized users with valid credentials may upload or submit data.
* **Data encryption**: All data transfers, whether via the portal or API, must be encrypted using HTTPS.
* **Audit trail**: Each submission will be logged with a timestamp, user ID, and versioning to maintain a complete audit trail for compliance purposes.

## 9. **Notifications and Alerts**

* **Submission receipt**: Producers will receive an automatic confirmation once their data has been successfully uploaded and passed initial validation.
* **Error notifications**: If any issues are detected with the submitted data, producers will be notified with specific error messages (e.g., missing intervals, outliers) within **24 hours** of submission.

## 10. **Support and Assistance**

* **Technical support**: Producers can contact the REC registry support team via email or through the web portal for assistance with data submission or technical issues.
* **FAQ and Documentation**: Detailed submission guides and FAQs are available on the web portal to help producers with the submission process.

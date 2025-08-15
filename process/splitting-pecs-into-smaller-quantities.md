# Splitting GCs into Smaller Quantities

## **Objective**

To enable end-users to split GCs into smaller quantities of energy down to the watt-hour. This process involves canceling the parent GC and issuing multiple child GCs, ensuring that the sum of the energy for the child GCs matches the value of the parent GC.

***

## **Definitions**

* **Parent GC:** The original GC that is being split into smaller quantities.
* **Child GCs:** The new GCs issued as a result of splitting the parent GC. Each child GC represents a portion of the parent’s energy.

## **Process for Splitting GCs**

### **Step 1: Initiate Split Request**

* **End-User Action:**
  * The end-user requests to split a parent GC via the registry portal or API, specifying the desired energy amounts for each child GC.
* **Requirements:**
  * The total energy of the child GCs must equal the energy of the parent GC.
  * Energy amounts must be specified in watt-hours (Wh).

### **Step 2: Validate Split Request**

* **Registry Action:**
  * Verify the parent GC is active and eligible for splitting.
  * Ensure the sum of the child GCs' energy amounts equals the parent GC's energy amount.
  * Check for compliance with any regulatory or policy constraints.

### **Step 3: Cancel Parent GC**

* **Registry Action:**
  * Update the status of the parent GC to "Canceled due to split."
  * Record the cancellation event with a timestamp and reason.

### **Step 4: Issue Child GCs**

* **Registry Action:**
  * Generate new GC IDs for each child GC using the revised GC ID structure.
  * Assign the same `Project_ID`, `DateCode`, and `EAC_ID` as the parent GC.
  * Update the `[SequentialNumber]`based on the next unique value.
  * Update the `Energy_ID` to reflect the energy amount of each child GC.

### **Step 5: Update Registry Records**

* **Data Management:**
  * Link child GCs to the parent GC in the registry database.
  * Maintain an audit trail of the splitting process, including all GC IDs and associated energy amounts.

### **Step 6: Notify End-User**

* **Registry Action:**
  * Provide confirmation to the end-user detailing:
    * Cancellation of the parent GC.
    * Issuance of child GCs, including their GC IDs and energy amounts.
    * Instructions or links to view the updated GCs in their account.

***

### **Ensuring Energy Conservation**

* **Validation Checks:**
  * The registry system must enforce that the sum of the energy amounts of the child GCs exactly matches the energy amount of the parent GC.
  * Any discrepancies must be resolved before the split is executed.
* **Precision Handling:**
  * Energy amounts should be handled with sufficient precision to avoid rounding errors, ensuring accuracy down to the watt-hour.

***

### **Examples of the Splitting Process**

* **Parent GC:**
  * **GC ID:** `GC101-20240928-20003-0001-0750000`
  * **Energy Amount:** 750,000 Wh (0.75 MWh)
* **Split Request:**
  * Split into two child GCs:
    * **Child GC 1:** 500,000 Wh (0.5 MWh)
    * **Child GC 2:** 250,000 Wh (0.25 MWh)
* **Child GCs Issued:**
  * **Child GC 1:**
    * **GC ID:** `GC101-20240928-20003-0001-0500000`
    * **Energy Amount:** 500,000 Wh
  * **Child GC 2:**
    * **GC ID:** `GC101-20240928-20003-0001-0250000`
    * **Energy Amount:** 250,000 Wh
* **Registry Actions:**
  * Cancel parent GC `GC101-20240928-20003-0001-0750000`.
  * Record the issuance of child GCs with proper linkage.

***

## **Conclusion**

This specification outlines a robust process for splitting GCs into smaller quantities down to the watt-hour, ensuring accurate energy accounting and maintaining the integrity of the registry. The GC ID format accommodates the splitting process effectively, providing clarity and traceability for all stakeholders involved. By adhering to this methodology, the GC registry ensures precise, transparent, and user-friendly operations.

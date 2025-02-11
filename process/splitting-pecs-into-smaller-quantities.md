# Splitting PECs into Smaller Quantities

## **Objective**

To enable end-users to split PECs into smaller quantities of energy down to the watt-hour. This process involves canceling the parent PEC and issuing multiple child PECs, ensuring that the sum of the energy for the child PECs matches the value of the parent PEC.&#x20;

***

## **Definitions**

* **Parent PEC:** The original PEC that is being split into smaller quantities.
* **Child PECs:** The new PECs issued as a result of splitting the parent PEC. Each child PEC represents a portion of the parent’s energy.

## **Process for Splitting PECs**

### **Step 1: Initiate Split Request**

* **End-User Action:**
  * The end-user requests to split a parent PEC via the registry portal or API, specifying the desired energy amounts for each child PEC.
* **Requirements:**
  * The total energy of the child PECs must equal the energy of the parent PEC.
  * Energy amounts must be specified in watt-hours (Wh).

### **Step 2: Validate Split Request**

* **Registry Action:**
  * Verify the parent PEC is active and eligible for splitting.
  * Ensure the sum of the child PECs' energy amounts equals the parent PEC's energy amount.
  * Check for compliance with any regulatory or policy constraints.

### **Step 3: Cancel Parent PEC**

* **Registry Action:**
  * Update the status of the parent PEC to "Canceled due to split."
  * Record the cancellation event with a timestamp and reason.

### **Step 4: Issue Child PECs**

* **Registry Action:**
  * Generate new PEC IDs for each child PEC using the revised PEC ID structure.
  * Assign the same `Project_ID`, `DateCode`, and `EAC_ID` as the parent PEC.
  * Update the `[SequentialNumber]`based on the next unique value.
  * Update the `Energy_ID` to reflect the energy amount of each child PEC.

### **Step 5: Update Registry Records**

* **Data Management:**
  * Link child PECs to the parent PEC in the registry database.
  * Maintain an audit trail of the splitting process, including all PEC IDs and associated energy amounts.

### **Step 6: Notify End-User**

* **Registry Action:**
  * Provide confirmation to the end-user detailing:
    * Cancellation of the parent PEC.
    * Issuance of child PECs, including their PEC IDs and energy amounts.
    * Instructions or links to view the updated PECs in their account.

***

### **Ensuring Energy Conservation**

* **Validation Checks:**
  * The registry system must enforce that the sum of the energy amounts of the child PECs exactly matches the energy amount of the parent PEC.
  * Any discrepancies must be resolved before the split is executed.
* **Precision Handling:**
  * Energy amounts should be handled with sufficient precision to avoid rounding errors, ensuring accuracy down to the watt-hour.

***

### **Examples of the Splitting Process**

* **Parent PEC:**
  * **PEC ID:** `PEC101-20240928-20003-0001-0750000`
  * **Energy Amount:** 750,000 Wh (0.75 MWh)
* **Split Request:**
  * Split into two child PECs:
    * **Child PEC 1:** 500,000 Wh (0.5 MWh)
    * **Child PEC 2:** 250,000 Wh (0.25 MWh)
* **Child PECs Issued:**
  * **Child PEC 1:**
    * **PEC ID:** `PEC101-20240928-20003-0001-0500000`
    * **Energy Amount:** 500,000 Wh
  * **Child PEC 2:**
    * **PEC ID:** `PEC101-20240928-20003-0001-0250000`
    * **Energy Amount:** 250,000 Wh
* **Registry Actions:**
  * Cancel parent PEC `PEC101-20240928-20003-0001-0750000`.
  * Record the issuance of child PECs with proper linkage.

***

## **Conclusion**

This specification outlines a robust process for splitting PECs into smaller quantities down to the watt-hour, ensuring accurate energy accounting and maintaining the integrity of the registry. The PEC ID format accommodates the splitting process effectively, providing clarity and traceability for all stakeholders involved. By adhering to this methodology, the PEC registry ensures precise, transparent, and user-friendly operations.

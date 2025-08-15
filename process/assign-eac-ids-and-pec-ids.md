# Assign EAC IDs and GC IDs

## **Objective**

This specification outlines the methodology for assigning EAC IDs and GC IDs to split meter data. The process ensures that all energy generated, including fractions of a megawatt-hour (MWh), is accurately represented and traceable within the GC registry.

## **Definitions**

**Energy Attribute Certificate (EAC):**

* Represents 1.0 MWh of renewable energy generated.
* Assigned a unique **EAC ID**.
* Can be composed of whole, remainder, and filler energy records that sum to 1.0 MWh.

**Power Emissions Certificate (GC):**

* Represents any fraction of energy (including whole and partial MWh).
* Always associated with a EAC ID.
* Assigned a unique **GC ID** for every record, down to a single watt-hour (Wh).

## **Assignment of REC IDs and GC IDs**

### **Assigning REC IDs**

* **Whole Records:**
  * Each **Whole** record is assigned a **unique EAC ID**.
  * Represents a full 1.0 MWh generated within a single hour.
  * EAC IDs follow the format of the issuing EAC registry.
* **Remainder and Filler Records:**
  * **Remainder** and corresponding **Filler** records that together sum to 1.0 MWh are assigned the **same EAC ID**.
  * This EAC ID is unique and different from those assigned to Whole records.
  * Ensures that the combined energy totaling 1.0 MWh is tracked under a single EAC.

### **Assigning GC IDs**

* **All Records:**
  * Every individual record (Whole, Remainder, Filler) is assigned a **unique GC ID**.
  * GC IDs uniquely identify each fraction or whole unit of energy within the registry.
  * GC IDs are associated with their corresponding EAC IDs for traceability.

## Data Fields and ID Structure

### **GC ID Structure**

* **Format:**\
  `GC[Project_ID]-[Timestamp]-[EAC_ID]-[Energy_ID]`
* **Example:**\
  `GC101-20240928T153045Z-20003-0750000`

### **Components**

1. **Project\_ID:**
   * Unique identifier for the project, determined during onboarding.
   * **Example:** `101`
2. **EAC\_ID:**
   * Unique identifier from the EAC registry.
   * **Example:** `20003`
3. **Timestamp:**
   1. The ISO 8601 UTC timestamp of GC issuance or original split.
   2. _Example: 20240928T153045Z for September 28, 2024, at 15:30:45 UTC_
4. **Energy\_ID:**
   * A seven-digit value representing the energy amount in watt-hours (Wh).
   * Ranges between `0000001` (1 Wh) and `1000000` (1,000,000 Wh = 1 MWh).
   * **Example:** `0750000` represents 750,000 Wh or 0.75 MWh.

## **Example**

<table><thead><tr><th width="92">Hour</th><th width="139">Energy (MWh)</th><th width="94">EAC_ID</th><th>GC_ID</th></tr></thead><tbody><tr><td>1</td><td>1</td><td>1</td><td>GC101-<em>20240928T153045Z</em>-1-1000000</td></tr><tr><td>1</td><td>1</td><td>2</td><td>GC101-<em>20240928T153045Z</em>-2-1000000</td></tr><tr><td>1</td><td>1</td><td>3</td><td>GC101-<em>20240928T153045Z</em>-3-1000000</td></tr><tr><td>1</td><td>0.5</td><td>4</td><td>GC101<em>20240928T153045Z</em>-4-0500000</td></tr><tr><td>2</td><td>0.5</td><td>4</td><td>GC101-<em>20240928T153045Z</em>-4-0500000</td></tr><tr><td>2</td><td>1</td><td>5</td><td>GC101-<em>20240928T153045Z</em>-5-1000000</td></tr><tr><td>2</td><td>1</td><td>6</td><td>GC101-<em>20240928T153045Z</em>-6-1000000</td></tr><tr><td>2</td><td>0.1</td><td>7</td><td>GC101-<em>20240928T153045Z</em>-7-0100000</td></tr><tr><td>4</td><td>0.1</td><td>7</td><td>GC101-<em>20240928T153045Z</em>-7-0100000</td></tr><tr><td>5</td><td>0.8</td><td>7</td><td>GC101-<em>20240928T153045Z</em>-7-0800000</td></tr></tbody></table>

## **Conclusion**

This methodology ensures that all generated energy is accurately represented within the GC registry through systematic assignment of EAC IDs and GC IDs. By following this methodology, the registry maintains high data integrity, traceability, and compliance with renewable energy accounting standards.

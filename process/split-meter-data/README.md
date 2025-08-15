# Split Meter Data

## **Key Considerations**

* **Energy Conservation:** All generated energy is accounted for; no energy is lost or unassociated.
* **Time Association:** Energy remains linked to the specific hour(s) it was generated, even when used to complete a full MWh REC with energy from other hours.
* **Carryover Continuity:** Carryover values are continuously adjusted and passed to subsequent hours until sufficient energy is accumulated.
* **Record Traceability:** Each record should include references to the hours and energy amounts involved, ensuring transparency.

***

## **Record Types and Definitions**

* **"Whole":** Represents a full 1.0 MWh generated within a single hour.
* **"Remainder":** The fractional MWh remaining in an hour after accounting for whole MWh.
* **"Filler":** Energy from subsequent hours, when combined with the remainder, completes a full 1.0 MWh. This allows all GCs to be associated with an EAC.

***

## **Overview of the Process**

For each hour in the generation data:

* **Step 1:** Identify and create records for each whole 1.0 MWh of energy generated.
* **Step 2:** Identify and create records for any partial MWh ("Remainder")
* **Step 3:** Calculate a "Filler" value needed to form a full MWh when combined with the "Remainder" value.
* **Step 4:** Process the next hour's data to fulfill the "Filler" requirement, ensuring all energy is accounted for without losing its time association.

***

## **Process Details**

For every hour $$h$$ in the dataset:

### Step 1: Calculate Whole Energy

$$
Ewhole = floor(Eh)
$$

* Where $$Eh$$ is the total energy generated in hour $$h$$.

**Record Creation:**

* If $$Ewhole>0$$, create a record for each 1.0 MWh labeled "Whole"**.**

### **Step 2: Calculate Remainder Energy**

$$
Eremainder=Eh−Ewhole
$$

**Record Creation:**

* If $$Eremainder>0$$, create a record labeled **"Remainder"** for this partial MWh.

### **Step 3: Calculate Filler Value**

$$
Efiller = 1.0 MWh - Eremainder
$$

{% hint style="info" %}
The "Remainder" from hour $$h$$ and "Filler" from hour $$h+1$$ together form a full 1.0 MWh for association with a single EAC.
{% endhint %}

***

### **Process Filler with Subsequent Hours**

If there is _sufficient energy to satisfy the filler_ $$(E(h+1) >= Efiller)$$:

* **Record Creation:**

$$
E'(h+1) = E(h+1)-Efiller
$$

* Create a record labeled **"Filler"** for $$Efiller$$​ in hour $$h+1$$.
* Use $$E'(h+1)$$ for further processing in hour $$h+1$$.

If there is &#x69;_&#x6E;sufficient energy to satisfy filler_ $$(E(h+1) < Ch)$$_:_

* **Record Creation:**
  * Create a record labeled **"Remainder"** for $$Eremainder$$ in hour $$h+1$$.

$$
Eremainder= E(h+1)
$$

* **Adjust Filler Value:**

$$
Efiller'=Efiller−E(h+1)
$$

* **Pass Adjusted Filler Forward:**
  * The adjusted carryover $$Efiller'$$​ is carried over to hour $$h+2$$.

***

**Iterative Filler Handling**

* **Continue Processing:**
  * Repeat the process for subsequent hours until the Filler value is satisfied.

{% hint style="info" %}
Ensure that at each step, energy remains associated with the hour it was generated.
{% endhint %}

***

If there are no intervals left $$(E(h+1) = NaN)$$_:_

* **Record Creation:**
  * Create a record labeled **"Final Remainder"** for $$Eremainder$$ in hour $$h$$.
  * Create a record labeled **"Final Filler"** for $$Efiller$$ in hour $$h$$.

{% hint style="info" %}
The records Final Remainder and Final Carryover will be used in the next reporting period.
{% endhint %}

***

## **Example**

Raw data:

<table><thead><tr><th width="112">Hour</th><th width="87">Energy (MWh)</th></tr></thead><tbody><tr><td>1</td><td>3.5</td></tr><tr><td>2</td><td>2.6</td></tr><tr><td>3</td><td>0</td></tr><tr><td>4</td><td>0.1</td></tr><tr><td>5</td><td>1.5</td></tr></tbody></table>

Results Table:

<table><thead><tr><th width="111">Hour</th><th width="159">Energy (MWh)</th><th width="145">Type</th></tr></thead><tbody><tr><td>1</td><td>1</td><td>whole</td></tr><tr><td>1</td><td>1</td><td>whole</td></tr><tr><td>1</td><td>1</td><td>whole</td></tr><tr><td>1</td><td>0.5</td><td>remainder</td></tr><tr><td>2</td><td>0.5</td><td>filler</td></tr><tr><td>2</td><td>1</td><td>whole</td></tr><tr><td>2</td><td>1</td><td>whole</td></tr><tr><td>2</td><td>0.1</td><td>remainder</td></tr><tr><td>3</td><td>0</td><td><span class="math">Efiller</span> = 0.9</td></tr><tr><td>4</td><td>0.1</td><td>remainder</td></tr><tr><td>4</td><td>0</td><td><span class="math">Efiller'</span> = 0.8</td></tr><tr><td>5</td><td>0.8</td><td>carryover</td></tr><tr><td>5</td><td>0.3</td><td>remainder</td></tr><tr><td>6</td><td>0</td><td><span class="math">Efiller</span> = 0.7</td></tr></tbody></table>

***

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

## **Conclusion**

This methodology ensures that all generated energy is meticulously accounted for in the GC issuance process. By handling whole and partial MWh and carefully managing filler values between hours, we maintain the integrity and accuracy of the registry. This process also upholds the temporal association of energy generation, which is crucial for the GC registry.

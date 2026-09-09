# Path A Lab 4: Create a Model, Rule Set, Rules, POV, and Run a Calculation

## Introduction

### The ideas you need first

* **Model** &ndash; a container for the calculation logic. Running a model **layers** results on top of your loaded data without changing the loaded (input) numbers, so you can re-run or undo it.
* **Rule set** &ndash; an ordered group of rules inside a model. A **sequence** number decides the order. **Serial** means one rule at a time, in sequence order.
* **Rule** &ndash; one calculation step. There are two kinds:
  * **Custom calculation rule** &ndash; writes a value using a **formula** (for example, "add 10% to utilities").
  * **Allocation rule** &ndash; **moves** an amount from a **source** to one or more **destinations**, split by a **driver**, with an **offset** entry that cancels the amount at the source so nothing is double‑counted.
* **PCM_Balance members** (a system dimension) &ndash; EPCM keeps the pieces of each number separate: **`PCM_Input`** (what you loaded), **`PCM_Adjustment In`** (added by custom rules), **`PCM_Allocation In` / `PCM_Allocation Out`** (moved by allocation rules), and **`PCM_Net Balance`** (the running total of all of these). Rules read the **net balance** and never change `PCM_Input`.
* **POV (Point of View)** &ndash; one member each from **Years**, **Period**, **Scenario**, **Version** (here `FY24 / Jan / Actual / Working`). You calculate a model **for a POV**. A POV must have the status **Draft** to be calculated.
* **Model validation** &ndash; a check of the rules before you calculate. **Calculation** actually runs them.

### What this lab does and why the order matters

You will build a model with **two rules that run in this order**:

1. **`Example Utilities Adjustment`** (custom rule, **sequence 10**) &ndash; adds 10% to Utilities Expense, writing the extra amount to `PCM_Adjustment In`.
2. **`Allocate Service Center Costs`** (allocation rule, **sequence 20**) &ndash; moves the service‑centre costs to the operating centres, split by headcount.

The allocation takes its source amount from each account's **net balance** (input plus earlier adjustments). Because the custom rule runs **first**, the allocation moves the **adjusted** total. If the allocation ran first, it would move the un‑adjusted total and the adjustment would have no effect on the result. Sequence numbers are how you control this.

> The specific member selections below are an **example that works with the training data from Lab 3**. They are not a recommended design. Every organisation decides its own source, destination, driver, offset, and formulas.

Estimated Lab Time: 40 minutes

### Objectives

In this lab, you will:

* Create a model and a rule set
* Create a **custom calculation rule** (sequence 10) with a target range and a formula
* Create an **allocation rule** (sequence 20) with source, destination, driver, and offset
* Create a **Draft** POV
* Validate the model and run a calculation
* Check the result numbers and see why rule order matters

### Prerequisites

* You completed **Path A Lab 3**: members and training data are loaded and the database is refreshed
* You have read **Reference: EPCM Modeling Concepts**

## Task 1: Create a model

**Why:** the model is the container everything else goes in.

1. From the Home page, select **Modeling**, then **Models**.

2. Click the **Add** button.

3. In the **Create Model** dialog, enter:

  * **Name**: `Training Allocation Model`
  * **Description**: `Training model for Path A`

4. Click **Save**, then **Save and Close**.

**Success check:** `Training Allocation Model` appears in the **Models** list.

  > **Screenshot placeholder:** _Create Model dialog with the name and description entered._

## Task 2: Create a rule set

**Why:** the rule set groups the two rules and fixes the order they run in.

1. From the Home page, select **Modeling**, then **Designer**.

2. On the **Waterfall Setup** tab, use the drop-down next to **Designer** to select **Training Allocation Model**.

3. Click the **Add** button, then select **Rule Set**.

4. In the **Create Rule Set** panel, enter:

  * **Name**: `Training Rule Set`
  * **Description**: `Holds the training custom and allocation rules`
  * **Sequence**: `10`

5. Select **Serial** (rules run one at a time, in sequence order).

6. Select **Enabled**.

7. Click **Save**, then **Save and Close**.

**Success check:** `Training Rule Set` appears under `Training Allocation Model` on the **Waterfall Setup** tab.

  > **Screenshot placeholder:** _Create Rule Set panel with name, description, Sequence 10, Serial, and Enabled._

## Task 3: Create the custom calculation rule (sequence 10)

**Why:** this rule must run **before** the allocation so its adjustment is included in the amount the allocation moves.

### 3a. Definition

1. On the **Waterfall Setup** tab, select **Training Rule Set**.

2. Click the plus (**+**) icon and select **Custom Calculation Rule**.

3. On the **Create Custom Calculation Rule** page, on the **Definition** tab, enter:

  * **Rule Name**: `Example Utilities Adjustment`
  * **Description**: `Add 10% to Utilities Expense in the service centres`
  * **Sequence**: `10`

### 3b. Target and formula

The **target range** is the set of level‑0 intersections the rule visits. Keep it small &mdash; custom rules are slow over large ranges.

4. Open the **Target** tab.

5. For **Result Dimension**, select **PCM_Balance**. (The formula writes to the `PCM_Adjustment In` member of this dimension.)

6. Enter this formula (this is Oracle's documented "adjust utilities by 10%" example &mdash; it reads the input value and writes 10% of it to the adjustment member):

  ```
  [PCM_Adjustment In]:=([PCM_Input],[PCM_Rule])*.10;
  ```

  Formula rules: members go in square brackets `[ ]`, a group of members (a tuple) goes in parentheses `( )`, the line ends with a semicolon `;`, and any arithmetic must include a member of the **PCM_Rule** dimension.

7. Click **Validate** and confirm the formula is valid.

8. Select the target members, one per dimension:

  * **Account**: `Utilities Expense`
  * **Entity**: `Service Centers`
  * **Activity**: `NoActivity`
  * For any other dimension the page asks about, keep the proposed member. Years, Period, Scenario, and Version come from the calculation POV.

9. Click **Save**, then **Save and Close**.

**Expected outcome:** the rule is saved with sequence 10 and a valid formula.

**Success check:** on the **Waterfall Setup** tab, `Example Utilities Adjustment` shows sequence **10** inside `Training Rule Set`, and its formula validated without error.

  > **Screenshot placeholder:** _Custom calculation rule Target tab with Result Dimension PCM_Balance, the formula, and a successful Validate._

## Task 4: Create the allocation rule (sequence 20)

**Why:** this rule moves the (now adjusted) service‑centre costs to the operating centres.

1. On the **Waterfall Setup** tab, select **Training Rule Set**.

2. Click the plus (**+**) icon and select **Allocation Rule**.

3. On the **Create Allocation Rule** page, on the **Definition** tab, enter:

  * **Rule Name**: `Allocate Service Center Costs`
  * **Description**: `Move service centre costs to operating centres, split by headcount`
  * **Sequence**: `20`

4. Click **Save**. The rule now exists as a **definition**. It does not move anything until you complete Task 5.

**Success check:** `Allocate Service Center Costs` shows sequence **20**, after the custom rule, inside `Training Rule Set`.

  > **Screenshot placeholder:** _Create Allocation Rule Definition tab with Sequence 20._

## Task 5: Complete the allocation (source, destination, driver, offset)

> Example selections for the training data. Your real design will differ.

1. Open the **Source/Destination** tab.

2. Under **Source** (where the money starts), select:

  * **Account**: `Rent Expense`, `IT Expense`, `Utilities Expense` (the three expense members &mdash; not the `Total Cost Pool` parent, which also contains the statistics)
  * **Entity**: `Service Centers`
  * **Activity**: `NoActivity`

3. Under **Destination** (where the money goes), select:

  * **Account**: **Same As Source** (each expense stays as the same account)
  * **Entity**: `Operating Centers` (this includes its children `OPS-1`, `OPS-2`, `OPS-3`)
  * **Activity**: `NoActivity`

4. Click **Save**.

5. Open the **Driver** tab. The **driver** decides what share each destination gets: `its driver value / the total driver value`.

  * Choose **Specify Driver Location**
  * **Dimension**: `Account`
  * **Member**: `Headcount`

  With headcount 20 / 50 / 30, the shares are 20% / 50% / 30%.

6. Click **Save**.

7. Open the **Offset** tab. The **offset** writes the opposite entry at one place so the source nets to zero. Leave it at the **default (the source)**.

8. Click **Save**, then **Save and Close**.

**Success check:** the rule's **Source/Destination**, **Driver**, and **Offset** tabs all show the selections above with no validation warning on the rule.

  > **Screenshot placeholder:** _Source/Destination, Driver, and Offset tabs with the example selections._

## Task 6: Create a Draft POV

**Why:** a calculation always runs for one POV, and only a **Draft** POV can be calculated.

1. From the Home page, select **Application**, then **Overview**, then the **Point of View** tab.

2. Create a POV from `FY24`, `Jan`, `Actual`, `Working` &mdash; the members your training data was loaded to.

3. Confirm its status is **Draft**.

**Success check:** the POV `FY24 / Jan / Actual / Working` is listed with status **Draft**.

  > **Screenshot placeholder:** _Point of View tab with the FY24/Jan/Actual/Working POV in Draft status._

## Task 7: Validate the model

**Why:** validation catches rule problems before you spend time calculating.

1. From the Home page, select **Modeling**, then **Model Validation**.

2. In the **Model** drop-down, select **Training Allocation Model**.

3. Click **Run**.

**Success check:** validation completes with **no errors**. Warnings are acceptable (they flag rules that still run but are not best practice).

  > **Screenshot placeholder:** _Model Validation results for Training Allocation Model with no errors._

## Task 8: Run the calculation

1. From the Home page, select **Modeling**, then **Calculation Control**.

2. Select the **FY24 / Jan / Actual / Working** POV.

3. Click **Calculate Model**.

4. In the **Model** drop-down, select **Training Allocation Model**.

5. Under **Processing Options**:

  * Select **Clear Calculated Data** (clean first run)
  * Select **Run Calculation**
  * Select **Optimize for Reporting**
  * Set **Processing Range** to **All Rules**

6. Click **Run**.

7. Open **Jobs** and wait for the calculation job to show **Completed**.

**Success check:** the calculation job status is **Completed** with no errors.

  > **Screenshot placeholder:** _Calculation Control Processing Options set, and the Completed job in Jobs._

## Task 9: Check the results and see why order matters

Open an ad hoc grid or form for **`FY24 / Jan / Actual / Working`** and check the following (view the `PCM_Net Balance` member of PCM_Balance):

| Check | Expected |
| --- | --- |
| `Utilities Expense` at `SVC-1` (input + adjustment) | 33000 (30000 + 3000) |
| Sum of `Rent Expense` + `IT Expense` + `Utilities Expense` at `Operating Centers` | **243000** |
| `OPS-1` / `OPS-2` / `OPS-3` (all three expenses) | 48600 / 121500 / 72900 |
| `Rent Expense` + `IT Expense` + `Utilities Expense` at `Service Centers` | 0 (the offset) |

Then confirm the point of the sequence:

1. Open `Training Rule Set` and temporarily change `Allocate Service Center Costs` to sequence **10** and `Example Utilities Adjustment` to sequence **20**.
2. Re-run the calculation (Task 8).
3. The operating‑centres total is now **240000**, because the allocation moved the amount **before** the adjustment was posted.
4. Change the sequences back to **10** (custom) and **20** (allocation) and re-run to restore 243000.

Also open **Modeling &rarr; Rule Balancing** to see, per rule, the `PCM_Input`, `PCM_Adjustment In`, `PCM_Allocation In`, `PCM_Allocation Out`, and `PCM_Net Balance` amounts.

  > **Screenshot placeholder:** _Rule Balancing showing the adjustment and the allocation, with the 243000 operating-centres total._

## Learn More

* [Using the Rule Designer (Oracle EPCM documentation)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/using_the_rule_designer.html)
* [Calculating Models (Oracle EPCM documentation)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/calculating_models.html)

## Acknowledgements

* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, September 2026

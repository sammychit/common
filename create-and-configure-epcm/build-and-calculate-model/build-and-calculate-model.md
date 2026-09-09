# Path A Lab 4: Create a Model, Rule Set, Rules, POV, and Run a Calculation

## Introduction

### Terms you need first

* **Model** &ndash; holds the calculation logic. Running it lays results on top of your loaded numbers without changing them, so you can re-run or undo it.
* **Rule set** &ndash; an ordered group of rules. A **sequence** number sets the order. **Serial** = one rule at a time, in sequence order.
* **Rule** &ndash; one calculation step. Two kinds:
  * **Custom calculation rule** &ndash; writes a value with a **formula** (for example, "add 10% to utilities").
  * **Allocation rule** &ndash; **moves** an amount from a **source** to one or more **destinations**, split by a **driver**, with an **offset** that cancels the amount at the source.
* **PCM_Balance members** &ndash; EPCM keeps the parts of a number apart: **`PCM_Input`** (loaded), **`PCM_Adjustment In`** (from custom rules), **`PCM_Allocation In` / `Out`** (from allocation rules), and **`PCM_Net Balance`** (the running total). Rules read the net balance and never change `PCM_Input`.
* **POV** &ndash; one member each of Years, Period, Scenario, Version (`FY24 / Jan / Actual / Working`). A POV must be **Draft** to calculate.
* **Model validation** &ndash; checks the rules before you calculate. **Calculation** runs them.

### What this lab builds, and why order matters

You build one model with two rules, run in this order:

1. **`Example Utilities Adjustment`** (custom rule, **sequence 10**) &ndash; adds 10% to Utilities Expense, into `PCM_Adjustment In`.
2. **`Allocate Service Center Costs`** (allocation rule, **sequence 20**) &ndash; moves the service-centre costs to the operating centres, split by headcount.

The allocation takes its source from each account's **net balance** (input plus earlier adjustments). Because the custom rule runs first, the allocation moves the adjusted total. Run it first and the adjustment has no effect. Sequence numbers control this.

> The member choices below are an **example that fits the Lab 3 training data**. They are not a recommended design. Your organisation decides its own source, destination, driver, offset, and formulas.

Estimated Lab Time: 40 minutes

### Objectives

* Create a model and a rule set
* Create a **custom calculation rule** (sequence 10) with a target range and formula
* Create an **allocation rule** (sequence 20) with source, destination, driver, and offset
* Create a **Draft** POV
* Validate and calculate
* Check the numbers and see why rule order matters

### Prerequisites

* You finished **Path A Lab 3**: members and training data loaded, database refreshed
* You have read **Reference: EPCM Modeling Concepts**

## Task 1: Create a model

**Why:** the model is the container for everything else.

1. From the Home page, select **Modeling**, then **Models**.
2. Click **Add**.
3. Set **Name** to `Training Allocation Model` and **Description** to `Training model for Path A`.
4. Click **Save**, then **Save and Close**.

**Check:** `Training Allocation Model` is in the **Models** list.

## Task 2: Create a rule set

**Why:** the rule set groups the two rules and fixes their order.

1. From the Home page, select **Modeling**, then **Designer**.
2. On the **Waterfall Setup** tab, use the drop-down next to **Designer** to select **Training Allocation Model**.
3. Click **Add**, then **Rule Set**.
4. In **Create Rule Set**, set **Name** to `Training Rule Set`, **Description** to `Holds the training rules`, and **Sequence** to `10`.
5. Select **Serial**.
6. Select **Enabled**.
7. Click **Save**, then **Save and Close**.

**Check:** `Training Rule Set` is under `Training Allocation Model` on the **Waterfall Setup** tab.

## Task 3: Create the custom calculation rule (sequence 10)

**Why:** it must run before the allocation, so its adjustment is in the amount the allocation moves.

### 3a. Definition

1. On the **Waterfall Setup** tab, select **Training Rule Set**.
2. Click the plus (**+**) icon and select **Custom Calculation Rule**.
3. On the **Definition** tab, set **Rule Name** to `Example Utilities Adjustment`, **Description** to `Add 10% to Utilities Expense in the service centres`, and **Sequence** to `10`.

### 3b. Target and formula

The **target range** is the set of level-0 intersections the rule visits. Keep it small &ndash; custom rules are slow over large ranges.

4. Open the **Target** tab.
5. For **Result Dimension**, select **PCM_Balance**. The formula writes to its `PCM_Adjustment In` member.
6. Enter this formula (Oracle's documented "adjust utilities by 10%" example &ndash; it reads the input value and writes 10% of it to the adjustment member):

  ```
  [PCM_Adjustment In]:=([PCM_Input],[PCM_Rule])*.10;
  ```

  Formula rules: members in square brackets `[ ]`; a group of members (a tuple) in parentheses `( )`; the line ends with a semicolon `;`; arithmetic must include a **PCM_Rule** member.

7. Click **Validate** and confirm the formula is valid.
8. Select one target member per dimension: **Account** = `Utilities Expense`, **Entity** = `Service Centers`, **Activity** = `NoActivity`. Keep the proposed member for anything else; Years, Period, Scenario, and Version come from the POV.
9. Click **Save**, then **Save and Close**.

**Check:** on the **Waterfall Setup** tab, `Example Utilities Adjustment` shows sequence **10** in `Training Rule Set`, and its formula validated.

## Task 4: Create the allocation rule (sequence 20)

**Why:** it moves the now-adjusted service-centre costs to the operating centres.

1. On the **Waterfall Setup** tab, select **Training Rule Set**.
2. Click the plus (**+**) icon and select **Allocation Rule**.
3. On the **Definition** tab, set **Rule Name** to `Allocate Service Center Costs`, **Description** to `Move service centre costs to operating centres, split by headcount`, and **Sequence** to `20`.
4. Click **Save**. The rule is now a **definition**. It moves nothing until you finish Task 5.

**Check:** `Allocate Service Center Costs` shows sequence **20**, after the custom rule.

## Task 5: Fill in the allocation (source, destination, driver, offset)

> Example choices for the training data. Your real design will differ.

1. Open the **Source/Destination** tab.
2. Under **Source** (where the money starts):
  * **Account**: `Rent Expense`, `IT Expense`, `Utilities Expense` (the three expense members, not the `Total Cost Pool` parent, which also holds the statistics)
  * **Entity**: `Service Centers`
  * **Activity**: `NoActivity`
3. Under **Destination** (where it goes):
  * **Account**: **Same As Source**
  * **Entity**: `Operating Centers` (includes `OPS-1`, `OPS-2`, `OPS-3`)
  * **Activity**: `NoActivity`
4. Click **Save**.
5. Open the **Driver** tab. The driver sets each destination's share: *its driver value / the total*.
  * Choose **Specify Driver Location**
  * **Dimension**: `Account`
  * **Member**: `Headcount`

  Headcount 20 / 50 / 30 gives shares of 20% / 50% / 30%.
6. Click **Save**.
7. Open the **Offset** tab. Leave it at the **default (the source)**, so the source nets to zero.
8. Click **Save**, then **Save and Close**.

**Check:** the **Source/Destination**, **Driver**, and **Offset** tabs show the choices above, with no warning on the rule.

## Task 6: Create a Draft POV

**Why:** a calculation runs for one POV, and only a **Draft** POV can be calculated.

1. From the Home page, select **Application**, then **Overview**, then the **Point of View** tab.
2. Create a POV from `FY24`, `Jan`, `Actual`, `Working` &ndash; the members your data was loaded to.
3. Confirm its status is **Draft**.

**Check:** `FY24 / Jan / Actual / Working` is listed with status **Draft**.

## Task 7: Validate the model

**Why:** validation catches rule problems before you calculate.

1. From the Home page, select **Modeling**, then **Model Validation**.
2. In the **Model** drop-down, select **Training Allocation Model**.
3. Click **Run**.

**Check:** validation finishes with **no errors**. Warnings are fine (rules that run but are not best practice).

## Task 8: Run the calculation

1. From the Home page, select **Modeling**, then **Calculation Control**.
2. Select the **`FY24 / Jan / Actual / Working`** POV.
3. Click **Calculate Model**.
4. In the **Model** drop-down, select **Training Allocation Model**.
5. Under **Processing Options**: select **Clear Calculated Data**, **Run Calculation**, and **Optimize for Reporting**; set **Processing Range** to **All Rules**.
6. Click **Run**.
7. Open **Jobs** and wait for the job to show **Completed**.

**Check:** the calculation job is **Completed** with no errors.

## Task 9: Check the results, and why order matters

In an ad hoc grid for **`FY24 / Jan / Actual / Working`**, view the `PCM_Net Balance` member:

| Check | Expected |
| --- | --- |
| `Utilities Expense` at `SVC-1` (input + adjustment) | 33000 (30000 + 3000) |
| `Rent Expense` + `IT Expense` + `Utilities Expense` at `Operating Centers` | **243000** |
| `OPS-1` / `OPS-2` / `OPS-3` (all three expenses) | 48600 / 121500 / 72900 |
| The three expenses at `Service Centers` | 0 (the offset) |

Now see why the order matters:

1. In `Training Rule Set`, swap the sequences: `Allocate Service Center Costs` to **10**, `Example Utilities Adjustment` to **20**.
2. Re-run the calculation (Task 8).
3. The operating-centres total is now **240000** &ndash; the allocation moved the amount before the adjustment was posted.
4. Set the sequences back (custom **10**, allocation **20**) and re-run to get 243000 again.

Open **Modeling &rarr; Rule Balancing** to see `PCM_Input`, `PCM_Adjustment In`, `PCM_Allocation In`, `PCM_Allocation Out`, and `PCM_Net Balance` per rule.

## Learn More

* [Using the Rule Designer (Oracle EPCM documentation)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/using_the_rule_designer.html)
* [Calculating Models (Oracle EPCM documentation)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/calculating_models.html)

## Acknowledgements

* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, September 2026

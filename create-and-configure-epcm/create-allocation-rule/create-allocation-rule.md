# Create an Allocation Rule

## Introduction

An **allocation rule** distributes (allocates) amounts from a **source** to one or more **destinations**, split by a **driver basis**, with an optional **offset** entry that balances the source. Allocation rules are the primary way costs and revenues flow through an Enterprise Profitability and Cost Management model.

In this lab you add an allocation rule to the rule set created in the previous lab, define its four parts, and calculate a POV to see the result.

Estimated Lab Time: -- minutes

### Objectives

In this lab, you will:

* Create an allocation rule definition
* Define the **Source** and **Destination**
* Define the **Driver Basis**
* Define the **Offset**
* Calculate the model for a POV and review the allocated results

### Prerequisites

Ensure that:

* You have completed *Create a Model and Rule Set* (or are using a rule set in the **BksML50** sample application)
* You have a **Draft** Point of View to calculate

## Task 1: Create the allocation rule definition

1. From the Home page, select **Modeling**, then **Designer**.

2. On the **Waterfall Setup** tab, select your **model**, then select the **rule set**.

3. Click the plus (**+**) icon and select **Allocation Rule**.

4. On the **Create Allocation Rule** page, on the **Definition** tab, enter:

  * **Rule Name** &ndash; for example, `Rent Expense to Departments`
  * **Description** &ndash; the rule's purpose (appears in Model Documentation)
  * **Sequence** &ndash; a whole number from 1 to 9999
  * Optionally set **use rule set context** and **enable** the rule

  > **Screenshot placeholder:** _Create Allocation Rule page, Definition tab._

## Task 2: Define the Source and Destination

1. Click the **Source/Destination** tab.

2. Under **Source**, for each dimension click the space below the dimension name, click **Search**, and select the members that hold the data to allocate. Selecting a parent member automatically includes its descendants.

  * Use the **...** (options) button for **Add Multiple Members Source**, **Calculation Segmentation**, or to **Clear** selections.
  * By default, an allocation rule allocates **100%** of the amounts in the source intersections.

3. Under **Destination**, for each dimension click the space next to the dimension name, click **Search**, and select the members that receive the allocated data.

  * Use **...** to add multiple members, set a dimension to **Same As Source**, or clear selections.
  * Use the **Same As Dimension** list to reuse same-named members across dimensions, or paste dimension/member combinations as text.

4. Click **Save**.

  > **Screenshot placeholder:** _Source/Destination tab with source and destination member selections._

## Task 3: Define the Driver Basis

The driver determines what proportion each destination intersection receives, using the ratio *driver value / sum of all driver values*.

1. Click the **Driver** tab.

2. Choose the method:

  | Method | Behavior |
  | --- | --- |
  | **Specify Driver Location** (default) | Allocates proportionally using driver data. Select the **Dimension** and **Member** that hold the driver values (for example, a `Headcount` or `Square Footage` account). |
  | **Allocate Evenly** | Distributes the source amount equally across destinations, regardless of driver values. |

3. Click **Save**.

  > **Screenshot placeholder:** _Driver tab with Specify Driver Location and a driver member selected._

## Task 4: Define the Offset

The offset writes a balancing **negative entry** equal to the allocated amount, so the source nets to zero and is not allocated again downstream.

1. Click the **Offset** tab.

2. Specify the dimension and member to hold the offset value. If you do not change it, the offset **defaults to the source** location.

3. Click **Save**, then **Save and Close**.

  > **Screenshot placeholder:** _Offset tab showing the offset member selection._

## Task 5: Calculate and review

1. From the Home page, select **Modeling**, then **Calculation Control**.

2. Select a **Draft** POV. (Only POVs with a status of **Draft** can have calculation control actions performed on them.)

3. Run **all rules** or select your rule set / rule, choose whether to **clear calculated data** first, and start the calculation.

4. Monitor progress in **Jobs**.

5. Review results with a form, or use **Allocation Trace** to follow the allocated amounts from source to destination.

  > **Screenshot placeholder:** _Calculation Control page with a Draft POV selected and a completed calculation job._

## Learn More

* [Creating an Allocation Rule Definition](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/creating_an_allocation_rule_definition.html)
* [Defining a Source and Destination for Allocation Rules (Designer)](https://docs.oracle.com/en/cloud/saas/profit-cost-cloud/pcmad/defining_a_source_for_pcmcs_allocation_rules_designer.html)
* [Defining a Driver Basis for Allocation Rules (Designer)](https://docs.oracle.com/en/cloud/saas/profit-cost-cloud/pcmad/defining_a_driver_basis_for_pcmcs_allocation_rules_designer.html)
* [Calculating Models](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/calculating_models.html)

## Acknowledgements

* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, September 2026

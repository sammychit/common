# Create a Model and Rule Set

## Introduction

In Enterprise Profitability and Cost Management, calculation logic is organized into **models**, **rule sets**, and **rules**. A model is a container for allocation and custom calculation rules; when a model runs against a data POV, the results are layered on top of the source data without changing it, so a single rule, rule set, or the whole model can be undone. A rule set groups related rules and controls the order and mode in which they run.

This lab creates the model and rule set used by the *Create an Allocation Rule* and *Create a Custom Calculation Rule* labs.

Estimated Lab Time: -- minutes

### Objectives

In this lab, you will:

* Create a model
* Optionally define a model context
* Create a rule set inside the model and choose its calculation mode

### Prerequisites

Ensure that:

* You have an EPCM application open (the **BksML50** sample application, or an application you created)
* You have at least one **Draft** Point of View available for later calculation

## Task 1: Create a model

1. From the Home page, select **Modeling**, then **Models**.

2. On the **Models** page, click the **Add** button.

3. In the **Create Model** dialog, enter:

  * **Name** &ndash; the model name (it cannot contain special characters)
  * **Description** &ndash; a description of the model's purpose

4. Click **Save**, then **Save and Close**.

  > **Screenshot placeholder:** _Create Model dialog with Name and Description entered._

> **Tip:** Use separate models for different purposes, for example one model to calculate actuals and another to calculate plan or What If scenarios. The same rules can run against different data POVs.

## Task 2: Define a model context (optional)

A model context is a set of member selections that apply to every rule set and rule in the model, which saves time and keeps selections consistent.

1. On the **Models** page, click the model's hyperlink.

2. Define the member selections for the context.

3. Save the context.

  > **Screenshot placeholder:** _Model context member selections for the model._

## Task 3: Create a rule set

1. From the Home page, select **Modeling**, then **Designer**.

2. On the **Waterfall Setup** tab, click the drop-down next to **Designer** and select your model.

3. Click the **Add** button, then select **Rule Set**.

4. In the **Create Rule Set** panel, enter:

  * **Name** &ndash; for example, `Occupancy Expense Allocations`
  * **Description** &ndash; text that appears in the Model Documentation report
  * **Sequence** &ndash; a whole number from 1 to 9999 that determines run order

5. Select a **Rule Set Calculation** option:

  | Option | Behavior |
  | --- | --- |
  | **Serial** | Runs all rules one at a time, in sequence-number order. |
  | **Parallel** | Runs rules that share a sequence number at the same time, limited by the Calculation Threads setting. |
  | **Iterative** | Runs the rule set repeatedly to resolve reciprocal (circular) allocation relationships. |

6. Select **Enabled** so the rule set runs during calculation.

7. Optionally select **Model Context** so the model's member selections apply to all rules in this rule set.

8. Click **Save**, then **Save and Close** (or **Save and Next** to add another rule set).

  > **Screenshot placeholder:** _Create Rule Set panel showing Name, Description, Sequence, calculation option, and Enabled._

## Task 4: Review rule set actions

On the **Waterfall Setup** tab, click the **Actions** icon next to your rule set. From here you can:

* Edit the rule set or create a **Rule Set Context**
* Add an **allocation rule** or a **custom calculation rule** (used in the next labs)
* Duplicate or delete the rule set

## Learn More

* [About Models](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/about_models.html)
* [Creating a Model](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/creating_a_model_20.html)
* [Creating a Rule Set](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/creating_a_rule_set_20.html)

## Acknowledgements

* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, September 2026

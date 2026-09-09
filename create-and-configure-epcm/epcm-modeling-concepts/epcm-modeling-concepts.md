# Reference: EPCM Modeling Concepts

## Introduction

This is a short read, not a set of steps. It explains the terms used in the Path A modeling lab, in Path B validation, and in the PCM Agent section. The Oracle links at the end go deeper.

Estimated Lab Time: 10 minutes

## Cube

A **cube** is the database that stores the numbers and does the maths. EPCM has a **calculation** cube (where rules run) and a **reporting** cube. You pick the cube when you create a dimension and when you load data.

## Dimensions

A **dimension** is a list of things you analyse by. A **member** is one item in it. Members sit in a **parent / child** tree; a parent totals its children.

* **Required dimensions:** Account, Entity, Period, Years, Scenario, Version. Every EPCM application has them.
* **System dimensions** (EPCM manages these):
  * **PCM_Rule** &ndash; one member per rule, so each rule's effect is tracked on its own. Its **`PCM_No Rule`** member holds anything not made by a rule, such as data you load.
  * **PCM_Balance** &ndash; keeps the parts of a number apart:

    | Member | Holds |
    | --- | --- |
    | `PCM_Input` | What you loaded |
    | `PCM_Adjustment In` / `PCM_Adjustment Out` | Amounts a custom rule added or removed |
    | `PCM_Allocation In` / `PCM_Allocation Out` | Amounts an allocation rule moved in or out |
    | `PCM_Net Balance` | The running total &ndash; the number rules read and reports show |
* **Currency dimension:** exists only if you chose multicurrency when creating the application.
* **Custom dimensions:** extra dimensions your model needs (for example, Activity). You create and fill these yourself.

## Point of View (POV)

A **POV** is one member each from **Years**, **Period**, **Scenario**, and **Version** &ndash; for example `FY24 / Jan / Actual / Working`. You calculate a model **for a POV**. A POV must have the status **Draft** to be calculated.

## Model

A **model** holds the calculation logic. Running it lays results on top of your loaded numbers without changing them, so you can re-run or undo it. You can keep one model for actuals and another for plan.

## Rule set

A **rule set** is an ordered group of rules inside a model. A **sequence** number sets the order. It runs in one of three modes:

* **Serial** &ndash; one rule at a time, in sequence order
* **Parallel** &ndash; rules with the same sequence number run together
* **Iterative** &ndash; the set repeats to settle circular allocations

## The two kinds of rule

**Allocation rule** &ndash; moves an amount from one place to another. Four parts:

| Part | Meaning |
| --- | --- |
| **Source** | Where the amount starts. |
| **Destination** | Where it goes. |
| **Driver** | How it splits. Each destination gets *its driver value / the total driver value*. Or it splits evenly. |
| **Offset** | An equal, opposite entry so the source nets to zero. Sits at the source by default. |

**Custom calculation rule** &ndash; writes a value with a formula (`Result := Formula;`) instead of moving amounts. Used for adjustments, rates, and derived statistics.

## Validate and calculate

* **Model validation** checks the rules for errors before you calculate. Warnings are rules that run but are not best practice.
* **Calculation** runs a model's rules for a Draft POV. You can clear old results first and run all rules or some. Watch progress in **Jobs**.
* Check results with data forms, **Rule Balancing**, and **Calculation Analysis**.

## How you build these

* In **Path A Lab 4** you build the model, rule set, and rules by hand in **Modeling &rarr; Models** and **Modeling &rarr; Designer**, then validate and calculate.
* In the **PCM Agent section** you can do the same with typed commands. The agent creates the definitions; a working allocation still needs its source, destination, driver, offset, or formula filled in.

## Learn More

* [Overview of the PCM_Rule and PCM_Balance System Dimensions (Oracle EPCM documentation)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/overview_of_pcm_rule_and_pcm_balance.html)

## Acknowledgements

* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, September 2026

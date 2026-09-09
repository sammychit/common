# Reference: EPCM Modeling Concepts

## Introduction

This short reference defines the modeling terms used in the Path A modeling lab, in Path B validation, and in the optional PCM Agent section. There are no steps to perform. It is intentionally brief; the Oracle documentation links at the end cover each object in full.

Estimated Lab Time: 10 minutes

## Cubes

An EPCM application stores data in Oracle Essbase cubes. Calculations run in the **calculation cube**; results are also available in a **reporting cube**. You choose the cube when you create a dimension and when you load data.

## Dimensions

* **Required business dimensions:** Account, Entity, Period, Years, Scenario, Version. Every EPCM application has these.
* **System dimensions:** **PCM_Rule** (holds every allocation and custom rule, so each rule's result is tracked separately; its **`PCM_No Rule`** member holds data that did not come from a rule, such as what you load) and **PCM_Balance** (keeps the parts of a number separate). These are built and maintained for you.

  The main **PCM_Balance** members you will see:

  | Member | Holds |
  | --- | --- |
  | `PCM_Input` | The data you loaded |
  | `PCM_Adjustment In` / `PCM_Adjustment Out` | Amounts added or removed by custom calculation rules |
  | `PCM_Allocation In` / `PCM_Allocation Out` | Amounts moved in or out by allocation rules |
  | `PCM_Net Balance` | The running total of all of the above &ndash; the number rules read and reports show |
* **Currency dimension:** created only if you choose multicurrency when creating the application.
* **Custom dimensions:** any additional dimensions your model needs (for example, an activity or a product dimension). You create and populate these yourself.

## Point of View (POV)

A **POV** is one member each from **Years**, **Period**, **Scenario**, and **Version** &mdash; for example `FY24 / Jan / Actual / Working`. You calculate a model *for a POV*. A POV must exist and have the status **Draft** before it can be calculated.

## Model

A **model** is a container for rules. When a model runs against a POV, it layers results on top of the source data without changing it, so any rule, rule set, or the whole model can be re-run or undone. You can keep separate models for different purposes, such as one for actuals and one for plan.

## Rule set

A **rule set** is an ordered group of related rules inside a model. A **sequence** number sets the order. A rule set runs in one of three modes:

* **Serial** &ndash; one rule at a time, in sequence order
* **Parallel** &ndash; rules that share a sequence number run at the same time
* **Iterative** &ndash; the rule set repeats to resolve circular (reciprocal) allocations

## The two kinds of rule

**Allocation rule** &ndash; moves amounts from one place to another. It has four parts:

| Part | Meaning |
| --- | --- |
| **Source** | The intersection that holds the amount to allocate. |
| **Destination** | The intersections that receive the allocated amount. |
| **Driver basis** | How the amount is split. Each destination receives *its driver value / the total driver value*. Or the amount is split evenly. |
| **Offset** | A balancing entry (the opposite sign of the allocated amount) so the source nets to zero. Defaults to the source location. |

**Custom calculation rule** &ndash; writes a value using a formula instead of moving amounts. The formula has the form `Result := Formula;`. It is used for adjustments, rates, and derived statistics.

## Validation and calculation

* **Model validation** checks the rules in a model for errors before you calculate. Warnings identify rules that will still run but do not follow best practice.
* **Calculation** runs a model's enabled rules for a selected Draft POV. You can clear previously calculated data first, run all rules or a subset, and monitor progress in **Jobs**.
* After calculation you inspect results with data forms, **Rule Balancing**, and **Calculation Analysis**.

## How you build these

* In **Path A Lab 4** you create the model, rule set, and rules by hand in **Modeling &rarr; Models** and **Modeling &rarr; Designer**, then validate and calculate.
* In the **optional PCM Agent section** you can create and run the same objects with natural-language commands. The agent creates the *definitions*; a working allocation still needs valid source, destination, driver, offset, and/or formula selections.

## Learn More

* [About Models (Oracle EPCM documentation)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/about_models.html)
* [Overview of the PCM_Rule and PCM_Balance System Dimensions (Oracle EPCM documentation)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/overview_of_pcm_rule_and_pcm_balance.html)

## Acknowledgements

* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, September 2026

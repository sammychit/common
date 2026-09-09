# Path B Lab 4: Validate the Migrated Application and Complete Post-Migration Tasks

## Introduction

A migration can finish with status **Success** and still be wrong in detail &mdash; a member under the wrong parent, a formula that did not convert, a total that does not match. This lab is the check: confirm the **dimensions** (the lists you analyse by), the **models** and **rules** (the calculation logic), and the **data** (the numbers) all came across, recalculate, and compare against the source PCM application. Then list what migration did **not** bring and must be rebuilt.

**Why this matters:** this is your sign-off that the EPCM application is a faithful copy before anyone relies on it.

Estimated Lab Time: 30 minutes

### Objectives

In this lab, you will:

* Validate the migrated dimensions
* Validate the migrated models and rules
* Run model validation and recalculate migrated POVs
* Compare results with the source PCM application
* Identify and plan the artifacts you must recreate in EPCM

### Prerequisites

* You completed **Path B Lab 3**; the application exists on the target EPCM environment
* You can access the source PCM application for comparison

## Task 1: Validate the migrated dimensions

1. Sign in to the target EPCM environment as a Service Administrator.

2. Click **Application**, then **Overview**, then the **Dimensions** tab.

3. Confirm:

  * The six required dimensions are present: **Account, Period, Years, Entity, Version, Scenario**.
  * The system dimensions were renamed: **RULE &rarr; PCM_Rule**, **BALANCE &rarr; PCM_Balance**.
  * Custom dimensions from the PCM application are present.
  * Mapped members appear under the correct parents.
  * Any duplicate-member prefixes from the template were applied (for example, `Sce_What If 1`).

**Success check:** every dimension you expect is listed, `PCM_Rule` and `PCM_Balance` are present, and a sample of members sits under the parents you mapped in the template.

  > **Screenshot placeholder:** _Dimensions tab of the migrated application._

## Task 2: Validate the migrated models and rules

1. Click **Modeling**, then **Models**. Confirm that each POV group listed in the template's `modelpovs` became a model.

2. Open **Designer** and review the rule sets and rules for each model.

3. Spot-check a few rule formulas &mdash; renamed dimensions should be reflected (for example, `[PCM_Rule]` in place of `[Rule]`).

  > **Screenshot placeholder:** _Modeling &rarr; Models list and the Designer view for a migrated model._

## Task 3: Run model validation

1. Click **Modeling**, then **Model Validation**.

2. In the **Model** drop-down, select a migrated model.

3. Click **Run**.

4. Expect no errors. Warnings identify rules that run but do not follow best practice.

## Task 4: Recalculate the migrated POVs

1. Click **Calculation Control**.

2. Select the migrated POVs (use the header check box to select all).

3. Click **Calculate Model** and select a model.

4. Under **Processing Options**:

  * **Deselect** **Clear Calculated Data** (keep the migrated results for comparison)
  * Select **Run Calculation**
  * Select **Optimize for Reporting**
  * Set **Processing Range** to **All Rules**

5. Click **Run**, then open **Jobs** and wait for **Completed**.

  > **Screenshot placeholder:** _Calculation Control Processing Options for recalculating migrated POVs._

## Task 5: Compare results with PCM

1. Click **Modeling**, then **Rule Balancing**.

2. Select POV members and a Rule Balancing data form (create one if needed via **Navigator &rarr; Create and Manage &rarr; Forms**, with rules from `PCM_Rule` on rows and balance measures from `PCM_Balance` on columns).

3. Compare the balances with the corresponding **Model View** in the source PCM application.

4. Use **Calculation Analysis** to produce the **Calculation Statistics Report** and the **Model Snapshot Documentation Report**.

**Success check:** for at least one migrated POV, the EPCM net balances by rule match the equivalent PCM Model View (small rounding differences aside).

  > **Screenshot placeholder:** _Rule Balancing in EPCM next to the equivalent PCM Model View._

## Task 6: Complete post-migration tasks

The following artifacts are **not** migrated and must be recreated in EPCM:

| Area | Recreate |
| --- | --- |
| **Security** | Native groups and roles; member-level and cell-level security. |
| **Data integration** | Data Management / Data Integration load profiles and data load rules. |
| **Analytics and reporting** | Reports, profit curves, and custom analytics. |
| **Forms and dashboards** | Data entry forms, profit curve forms, allocation trace forms, rule balancing forms, dashboards, and infolets. Model views do not exist in EPCM &mdash; rebuild them as data forms. |
| **Multicurrency** | If applicable, flag input currencies to be included as reporting currencies. |

Plan and schedule this work before cutover.

## Learn More

* [Migrating from Profitability and Cost Management to Enterprise Profitability and Cost Management (Oracle tutorial)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/tutorial-migrate-pcm-to-epcm/index.html)

## Acknowledgements

* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, September 2026

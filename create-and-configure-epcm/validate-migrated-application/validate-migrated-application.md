# Path B Lab 4: Validate the Migrated Application and Complete Post-Migration Tasks

## Introduction

A migration can finish with status **Success** and still be wrong in detail: a member under the wrong parent, a formula that did not convert, a total that does not match. This lab is the check. You confirm the **dimensions**, the **models** and **rules**, and the **data** all came across, recalculate, and compare with the source PCM application. Then you list what migration did not bring and must be rebuilt.

**Why this matters:** this is your sign-off that the EPCM application matches the source, before anyone relies on it.

Estimated Lab Time: 30 minutes

### Objectives

* Check the migrated dimensions
* Check the migrated models and rules
* Run model validation and recalculate the migrated POVs
* Compare results with the source PCM application
* List and plan the items you must rebuild

### Prerequisites

* You finished **Path B Lab 3**; the application exists on the target EPCM environment
* You can open the source PCM application to compare

## Task 1: Check the migrated dimensions

**Why:** wrong parents or missing members break every later step.

1. Sign in to the target EPCM environment as a Service Administrator.
2. Click **Application**, then **Overview**, then the **Dimensions** tab.
3. Confirm:
  * The six required dimensions are there: **Account, Period, Years, Entity, Version, Scenario**.
  * The system dimensions were renamed: **RULE &rarr; PCM_Rule**, **BALANCE &rarr; PCM_Balance**.
  * Your custom dimensions from PCM are there.
  * Mapped members sit under the right parents.
  * Any duplicate-member prefixes from the template were applied (for example, `Sce_What If 1`).

**Check:** every expected dimension is listed, `PCM_Rule` and `PCM_Balance` are present, and a sample of members sits under the parents you mapped.

## Task 2: Check the migrated models and rules

**Why:** the models and rules are the calculation logic; they must match the source.

1. Click **Modeling**, then **Models**. Confirm each POV group from the template's `modelpovs` became a model.
2. Open **Designer** and review the rule sets and rules for each model.
3. Spot-check a few rule formulas &ndash; renamed dimensions should show (for example, `[PCM_Rule]` instead of `[Rule]`).

**Check:** the model list and rule counts match your Preview and Validate Report from Lab 3.

## Task 3: Run model validation

**Why:** it catches converted-rule problems before you calculate.

1. Click **Modeling**, then **Model Validation**.
2. In the **Model** drop-down, select a migrated model.
3. Click **Run**.

**Check:** validation finishes with no errors. Warnings are rules that run but are not best practice.

## Task 4: Recalculate the migrated POVs

**Why:** re-running proves the rules still produce the same numbers.

1. Click **Calculation Control**.
2. Select the migrated POVs (use the header check box to select all).
3. Click **Calculate Model** and select a model.
4. Under **Processing Options**: **deselect** **Clear Calculated Data** (keep the migrated results); select **Run Calculation** and **Optimize for Reporting**; set **Processing Range** to **All Rules**.
5. Click **Run**, then open **Jobs** and wait for **Completed**.

**Check:** the calculation job is **Completed** with no errors.

## Task 5: Compare with PCM

**Why:** matching totals is the real proof the migration worked.

1. Click **Modeling**, then **Rule Balancing**.
2. Select POV members and a Rule Balancing data form. Create one if needed via **Navigator &rarr; Create and Manage &rarr; Forms**, with rules from `PCM_Rule` on rows and balance members from `PCM_Balance` on columns.
3. Compare the balances with the matching **Model View** in the source PCM application.
4. Use **Calculation Analysis** for the **Calculation Statistics Report** and the **Model Snapshot Documentation Report**.

**Check:** for at least one migrated POV, the EPCM net balances by rule match the PCM Model View (small rounding aside).

## Task 6: Rebuild what did not migrate

These items are **not** migrated. Recreate them in EPCM:

| Area | Recreate |
| --- | --- |
| **Security** | Native groups and roles; member-level and cell-level security. |
| **Data integration** | Data Management / Data Integration load profiles and data load rules. |
| **Analytics and reporting** | Reports, profit curves, custom analytics. |
| **Forms and dashboards** | Data entry forms, profit curve forms, allocation trace forms, rule balancing forms, dashboards, infolets. EPCM has no model views &ndash; rebuild them as data forms. |
| **Multicurrency** | If used, flag input currencies to be included as reporting currencies. |

Plan and schedule this work before you switch users over.

## Learn More

* [Migrating from Profitability and Cost Management to Enterprise Profitability and Cost Management (Oracle tutorial)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/tutorial-migrate-pcm-to-epcm/index.html)

## Acknowledgements

* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, September 2026

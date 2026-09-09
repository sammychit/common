# Path A Lab 3: Configure Dimensions and Load Metadata and Data

## Introduction

### Terms you need first

* **Dimension** &ndash; a list you analyse by. A new EPCM application already has **Account**, **Entity**, **Period**, **Years**, **Scenario**, and **Version**.
* **Member** &ndash; one item in a dimension. Members sit in a **parent / child** tree; a parent totals its children. **Level-0** members (no children) hold the numbers.
* **Metadata** &ndash; the members and their tree. Load metadata **before** data.
* **Data** &ndash; the numbers, held where members cross (Account `Rent Expense` + Entity `SVC-1` + Period `Jan` = 120000).
* **Cube** &ndash; the database that stores data and does the maths.
* **System dimension** &ndash; one EPCM manages for you: **PCM_Rule** and **PCM_Balance**.

### What this lab does

Your application has the standard dimensions but no accounts, no entities, and no numbers, so nothing can be calculated yet. Here you add a small set of training members and load a small set of training numbers, ready for Lab 4.

The example files are in the **`files/`** folder beside this lab. **Read `files/README.md` first.** It says which members already exist, which the files add, and the load order.

Estimated Lab Time: 35 minutes

### Objectives

* Tell required, system, and custom dimensions apart
* Create one custom dimension (**Activity**)
* Load members into **Account**, **Entity**, and **Activity**
* Refresh the database
* Load the training data and confirm it landed

### Prerequisites

* You finished **Path A Lab 2** and the application is open
* You have the `files/` folder and have read `files/README.md`

## Task 1: Look at the dimensions you already have

**Why:** so you do not try to re-create something that is already there.

1. On the Home page, click **Application**, then **Overview**.
2. Select the **Dimensions** tab.

| Type | Dimensions | Notes |
| --- | --- | --- |
| **Required** | Account, Entity, Period, Years, Scenario, Version | Always present. Account already has a top member **`All Accounts`**; Entity already has **`Total Entity`**. |
| **System** | PCM_Rule, PCM_Balance | Managed by EPCM. Do not edit. |
| **Currency** | Currency | Only if you chose multicurrency in Lab 2. |
| **Custom** | none yet | You add these. |

**Check:** open **Account** and confirm **`All Accounts`** exists; open **Entity** and confirm **`Total Entity`** exists. Your files attach under these.

## Task 2: Create a custom dimension

**Why:** cost models often need an extra dimension. Here it is **Activity**.

1. On the **Dimensions** tab, next to **Cube**, select the calculation cube.
2. Click **Create**.
3. On the **Create Dimension** page, set **Dimension** to `Activity` and **Data Storage** to `Never Share`.
4. Under the cube list, select **Enabled** next to each cube that should use **Activity**.
5. Click **Done**.

**Check:** **Activity** is in the Dimensions list, with one member, `Activity`.

## Task 3: Load members (metadata)

**Why:** this builds the account, entity, and activity trees the data and rules need.

Load the files **in this order**: `account-metadata.csv`, then `entity-metadata.csv`, then `activity-metadata.csv`. Each file's `Parent` column points at a member that must already exist, so the order matters.

For **each** file:

1. On the **Dimensions** tab, click **Import**.
2. On the **Import Metadata** page, click **Create**.
3. For the location, select **Local**, click **Browse**, and choose the file.
4. For **File Type**, select **Comma delimited**.
5. Leave **Clear Members** off. (It deletes members not in the file. EPCM also blocks it for members it needs, such as those in Years, Period, Currency, PCM_Balance, and the calculation-rule and no-rule branches of PCM_Rule.)
6. Click **Validate**, then **Import**.
7. In the **Last Validate/Import** column, **Completed** means success. **Failed** is a link to the row and column that broke.

**Check:** open each dimension and confirm the tree:

* **Account:** `All Accounts` &rarr; `Total Cost Pool` &rarr; `Rent Expense`, `IT Expense`, `Utilities Expense`, and `Training Statistics` &rarr; `Headcount`, `Floor Area`
* **Entity:** `Total Entity` &rarr; `Service Centers` &rarr; `SVC-1`, `SVC-2`, and `Total Entity` &rarr; `Operating Centers` &rarr; `OPS-1`, `OPS-2`, `OPS-3`
* **Activity:** `Activity` &rarr; `Total Activity` &rarr; `NoActivity`, `Activity 1`, `Activity 2`

## Task 4: Refresh the database

**Why:** metadata changes only reach the cube after a refresh. Data loads and calculations use the cube.

1. On the **Application Overview** page, open **Actions**.
2. Run the database refresh action (for example **Refresh Database**) with the defaults.
3. Wait for it to finish in **Jobs**.

**Check:** the refresh job shows **Completed** with no errors.

## Task 5: Load the training data

**Why:** Lab 4 needs numbers to adjust and allocate.

1. On the **Application Overview** page, select **Actions**, then **Import Data**.
2. On the **Import Data** page, click **Create**.
3. For the location, select **Local** and **Browse** to `data-training-jan.csv`.
4. Keep the default **Source Type**. For **File Type**, select **Comma delimited**.
5. First check that `Jan`, `FY24`, `PCM_Input`, `PCM_No Rule`, and `PCM_CLC` in the file match your application (see the "Names to confirm" table in `files/README.md`). Edit the file if needed.
6. Click **Validate**, then **Import**.

**Check:** the import job shows **Completed** with 9 cells loaded. In an ad hoc grid at **`FY24` / `Jan` / `Actual` / `Working`**:

* `Rent Expense` at `SVC-1` = 120000
* `IT Expense` at `SVC-2` = 90000
* `Utilities Expense` at `SVC-1` = 30000
* `Headcount` at `OPS-1` / `OPS-2` / `OPS-3` = 20 / 50 / 30

## Task 6: Next

Continue with **Path A Lab 4: Create a Model, Rule Set, Rules, POV, and Run a Calculation**.

## Learn More

* [Importing Metadata (Oracle EPCM documentation)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/importing_metadata.html)
* [Importing Data (Oracle EPCM documentation)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/importing_data.html)

## Acknowledgements

* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, September 2026

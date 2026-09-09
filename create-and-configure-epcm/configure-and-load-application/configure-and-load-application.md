# Path A Lab 3: Configure Dimensions and Load Metadata and Data

## Introduction

### The ideas you need first

* **Dimension** &ndash; a list of things you analyse by. A new EPCM application already contains **Account** (accounts), **Entity** (parts of the organisation), **Period** (months), **Years**, **Scenario** (for example Actual or Plan), and **Version** (for example Working or Final).
* **Member** &ndash; one entry in a dimension, arranged in a **parent / child** tree. A **parent** is a total of its **children**. **Level-0** members (the ones with no children) are where numbers are stored.
* **Metadata** &ndash; the members and their tree structure. You load metadata **before** data.
* **Data** &ndash; the numbers, stored where members from different dimensions cross (for example Account `Rent Expense` + Entity `SVC-1` + Period `Jan` = 120000).
* **Cube** &ndash; the database that holds the data and does the maths. EPCM has a **calculation** cube (where allocations run) and a **reporting** cube.
* **System dimension** &ndash; a dimension EPCM manages for you: **PCM_Rule** (tracks each rule's result separately) and **PCM_Balance** (separates loaded input from adjustments and allocations).

### What this lab does and why it matters

Your application from Lab 2 has the standard dimensions but **no accounts, no entities, and no numbers**. Nothing can be calculated yet. In this lab you add a small, neutral set of training members and load a small set of training numbers, so Lab 4 has something real to calculate.

The example files are in the **`files/`** folder beside this lab. **Read `files/README.md` first** &mdash; it explains which members are seeded (already there), which the files add, and the exact load order.

Estimated Lab Time: 35 minutes

### Objectives

In this lab, you will:

* Tell required, system, and custom dimensions apart
* Create one custom dimension (**Activity**)
* Load members into **Account**, **Entity**, and **Activity** from CSV files
* Refresh the database so the new members reach the cube
* Load the training data and confirm it landed

### Prerequisites

* You completed **Path A Lab 2** and the application is open
* You have the files from this lab's `files/` folder and have read `files/README.md`

## Task 1: Look at the dimensions you already have

**Why:** so you can see what is seeded (and must not be re-created) before you add anything.

1. On the Home page, click **Application**, then **Overview**.

2. Select the **Dimensions** tab.

3. Look at the list:

  | Type | Dimensions | Notes |
  | --- | --- | --- |
  | **Required business** | Account, Entity, Period, Years, Scenario, Version | Always present. Account already has a top member **`All Accounts`**; Entity already has **`Total Entity`**. |
  | **System** | PCM_Rule, PCM_Balance | Managed by EPCM. Do not edit. |
  | **Currency** | Currency | Present only if you chose multicurrency in Lab 2. |
  | **Custom** | none yet | You add these. |

**Expected outcome:** the Dimensions tab lists the dimensions above.

**Success check:** open the **Account** dimension and confirm **`All Accounts`** exists; open **Entity** and confirm **`Total Entity`** exists. Your files attach under these.

  > **Screenshot placeholder:** _Dimensions tab of the Application Overview page listing the seeded dimensions, with All Accounts visible under Account._

## Task 2: Create a custom dimension

**Why:** many cost models need an extra dimension the standard set does not provide (here, **Activity**). Creating one shows how custom dimensions differ from the required and system ones.

1. On the **Dimensions** tab, next to **Cube**, select the calculation cube.

2. Click **Create**.

3. On the **Create Dimension** page, enter:

  * **Dimension**: `Activity`
  * **Data Storage**: `Never Share`

4. Under the cube list, select **Enabled** next to each cube that should use **Activity**.

5. Click **Done**.

**Expected outcome:** **Activity** appears in the Dimensions list with a single root member, `Activity`.

**Success check:** open **Activity** and confirm the only member is `Activity` (its children come from the file in Task 3).

  > **Screenshot placeholder:** _Create Dimension page with Dimension set to Activity._

## Task 3: Load members (metadata)

**Why:** this builds the account, entity, and activity trees your data and rules will use.

Load the files **in this order**: `account-metadata.csv`, then `entity-metadata.csv`, then `activity-metadata.csv`. Each file's `Parent` column points at a member that must already exist &mdash; that is why the order matters.

For **each** file:

1. On the **Dimensions** tab, click **Import**.

2. On the **Import Metadata** page, click **Create**.

3. For the file location, select **Local**, click **Browse**, and choose the file. (Use **Inbox** instead if you have uploaded the files to the server.)

4. For **File Type**, select **Comma delimited**.

5. Leave **Clear Members** unselected.

  > **Note:** **Clear Members** deletes any member not listed in the file. Leave it off. EPCM also blocks it for members it needs, such as those in Years, Period, Currency, the PCM_Balance dimension, and the calculation-rule and no-rule branches of PCM_Rule.

6. Click **Validate** (available for **Local** files) to check the file format.

7. Click **Import**.

8. Check the **Last Validate/Import** column: **Completed** means success; **Failed** is a link to the row and column that caused the error.

**Expected outcome after all three files:**

* **Account**: `All Accounts` &rarr; `Total Cost Pool` &rarr; `Rent Expense`, `IT Expense`, `Utilities Expense`, and `Training Statistics` &rarr; `Headcount`, `Floor Area`
* **Entity**: `Total Entity` &rarr; `Service Centers` &rarr; `SVC-1`, `SVC-2`, and `Total Entity` &rarr; `Operating Centers` &rarr; `OPS-1`, `OPS-2`, `OPS-3`
* **Activity**: `Activity` &rarr; `Total Activity` &rarr; `NoActivity`, `Activity 1`, `Activity 2`

**Success check:** open each dimension on the **Dimensions** tab and confirm the tree matches the list above (and `files/README.md`).

  > **Screenshot placeholder:** _Account dimension after import, showing Total Cost Pool and its children under All Accounts._

## Task 4: Refresh the database

**Why:** metadata changes live in the application definition until you push them into the cube. Data loads and calculations use the cube, so refresh first.

1. On the **Application Overview** page, open **Actions**.

2. Run the database refresh action (for example **Refresh Database**), keeping the defaults.

3. Watch it finish in **Jobs**.

**Expected outcome:** a refresh job with status **Completed**.

**Success check:** the refresh job shows **Completed** with no errors in **Jobs**.

  > **Screenshot placeholder:** _Actions menu with the database refresh option, and the completed refresh job in Jobs._

## Task 5: Load the training data

**Why:** Lab 4 needs real numbers to adjust and allocate.

1. On the **Application Overview** page, select **Actions**, then **Import Data**.

2. On the **Import Data** page, click **Create**.

3. For the file location, select **Local** and **Browse** to `data-training-jan.csv`.

4. For **Source Type**, keep the default (business-process format). For **File Type**, select **Comma delimited**.

5. Before running, open `data-training-jan.csv` against the "Names to confirm" table in `files/README.md` and check the `Jan`, `FY24`, `PCM_Input`, `PCM_No Rule`, and `PCM_CLC` values match your application. Edit the file if needed.

6. Click **Validate** (for **Local** files), then click **Import**.

**Expected outcome:** an import job with status **Completed** and 9 cells loaded.

**Success check:** open an ad hoc grid or form at **Years `FY24`, Period `Jan`, Scenario `Actual`, Version `Working`** and confirm:

* `Rent Expense` at `SVC-1` = 120000
* `IT Expense` at `SVC-2` = 90000
* `Utilities Expense` at `SVC-1` = 30000
* `Headcount` at `OPS-1` / `OPS-2` / `OPS-3` = 20 / 50 / 30

  > **Screenshot placeholder:** _Import Data job Completed, and a grid showing the four checks above._

## Task 6: Next

Your application now has members and input data. Continue with **Path A Lab 4: Create a Model, Rule Set, Rules, POV, and Run a Calculation**.

## Learn More

* [Importing Metadata (Oracle EPCM documentation)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/importing_metadata.html)
* [Importing Data (Oracle EPCM documentation)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/importing_data.html)

## Acknowledgements

* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, September 2026

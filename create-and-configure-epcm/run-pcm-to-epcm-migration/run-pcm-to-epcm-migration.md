# Path B Lab 3: Customize, Validate, and Run the PCM-to-EPCM Migration

## Introduction

In this lab you customize the migration template, upload it to the PCM **inbox** (the server folder the migration reads from), run a **standalone validation** that checks the template without changing anything, and then either **Generate Snapshot** (produce the files and move them yourself) or **Migrate to EPCM** (Oracle transfers and imports them for you).

**Why this matters:** validation is safe and repeatable; the actual migration creates the one application your target environment is allowed to hold. Validate until it is clean before you migrate.

Estimated Lab Time: 45 minutes

### Objectives

In this lab, you will:

* Customize the mandatory and optional template sections
* Upload the template to the PCM inbox
* Validate the template and review the Preview and Validate Report
* Generate the application snapshot and data extract, or run the direct migration
* Know how to safely repeat a migration

### Prerequisites

* You completed **Path B Lab 2** and have the generated `<YourPCMApplicationName>_Export.xml`
* The target EPCM environment is preconfigured and has no application

## Task 1: Customize the template

Edit the XML file. Keep a copy of each version you upload.

### Mandatory sections

1. **`dimensions`** &mdash; for each of `account_dimension`, `entity_dimension`, `year_dimension`, `period_dimension`, `scenario_dimension`, `version_dimension` (and `currency_dimension` if multicurrency), set `pcm_dimname` to the source dimension name and complete the `member_mapping` entries (map the source top member to the EPCM top member). Example shape:

  ```xml
  <account_dimension>
      <pcm_dimname>Account</pcm_dimname>
      <member_mapping>
          <pcm_member></pcm_member>
          <epcm_member>All Accounts</epcm_member>
      </member_mapping>
  </account_dimension>
  ```

  For `period_dimension`, set the frequency and fiscal start to match the source calendar.

2. **`modelpovs`** &mdash; for each group of POV-specific rules, add a `pov` entry mapping the source POV to an EPCM model name:

  ```xml
  <modelpovs>
      <pov>
          <pcmpov>2016,January,Actual</pcmpov>
          <epcmmodelname>Actuals Allocation Model</epcmmodelname>
      </pov>
  </modelpovs>
  ```

### Optional sections (edit only if needed)

* **`epcmappname`** &mdash; up to 8 characters.
* **`duplicatememberprefixes`** &mdash; add a `dimension` block with `name`, `duplicateprefix`, and `prefix_all` to make duplicate names unique (EPCM requires unique member names).
* **`rename_dimension_mapping`** / **`rename_member_mapping`** &mdash; `artifact_name` blocks with `pcm_name` and `epcm_name`.
* **`datapovs`** &mdash; `pov` blocks with `srcpov`, `destpov` (members in the order Years, Period, Scenario, Version), and `include_calculated_data`.

> **Note on reserved names:** member names beginning with prefixes reserved by other EPM business processes (for example `FCCS_`, `OEP_`, `OWP_`, `OPF_`, `OCX_`, `PCM_`, `TRCS_`) are handled specially during migration. The validation step flags names that must be prefixed or renamed. The system dimensions are renamed automatically: `RULE` becomes `PCM_Rule` and `BALANCE` becomes `PCM_Balance`.

## Task 2: Upload the template to the PCM inbox

1. On the source PCM Home page, click **Application**, then click the **Application** icon.

2. Select the **File Explorer** vertical tab.

3. Click **Upload**.

4. For **File Name**, browse to the customized `<YourPCMApplicationName>_Export.xml`.

5. For **Folder Location**, select **Inbox**.

6. Click **OK**. If prompted that the file exists, choose to overwrite.

  > **Tip:** You can also upload with EPM Automate: `epmautomate uploadFile "<FILE_NAME>" profitinbox`

  > **Screenshot placeholder:** _File Explorer Upload dialog with Folder Location set to Inbox._

## Task 3: Validate the template

1. On the source PCM Home page, click **Migrate to EPCM**.

2. Click **Validate**.

3. The **Migration Status** shows **Success** or **Failed** for the validation step. If it fails, click the **Failed** link for the row-level errors (common causes: period or year format, dimension order, duplicate members that need a prefix).

4. Fix the template, re-upload it to the **Inbox** (Task 2, overwrite), and validate again. Repeat until validation succeeds.

**Success check:** the **Migration Status** shows **Success** for the validation step and no **Failed** links remain.

  > **Screenshot placeholder:** _Migration Status page showing a successful Validate result._

## Task 4: Review the Preview and Validate Report

1. Click **Preview And Validate Report**.

2. Save `Preview_and_Validation_Report.txt` and open it.

3. Review: duplicate members between PCM and EPCM, prefix mappings applied, renamed dimensions and members, the POV groups that become models, rule counts per model, and any modified custom calculation formulas.

## Task 5: Choose Generate Snapshot or direct Migrate to EPCM

### Option A &ndash; Generate Snapshot (two-step, manual transfer)

1. On the **Migrate to EPCM** page, click **Generate Snapshot**.

2. When it completes, the source **outbox** contains three files:

  | File | Contents |
  | --- | --- |
  | `Migrated_<ApplicationName>_Export_Data.txt` | The data extract, converted to EPCM (Essbase) format. Load it later via **Application &rarr; Overview &rarr; Import Data**. |
  | `<ApplicationName>_<ExportDate>_<ExportTime>.zip` | The EPCM application snapshot. |
  | `<ApplicationName>_Export_Data.log` | The migration process log, for troubleshooting. |

3. Download the files. On the **target** EPCM environment, upload the snapshot, use **Migrate** on the Enterprise Profitability and Cost Management landing page to create the application from it, then import the data extract.

**Success check (either option):** the target environment now has an EPCM application, and **Migration Status** shows **Success** for the snapshot/import steps.

### Option B &ndash; Migrate to EPCM (direct)

1. On the **Migrate to EPCM** page, click **Migrate to EPCM**.

2. In the dialog, enter the target **Target URL**, the Service Administrator **username**, and **password**.

3. Click **Migrate**.

4. The process validates the template, generates the snapshot and data export into the outbox, connects to the target, uploads the snapshot and data, imports the application snapshot, and imports the data. The **Migration Status** shows Success or Failed for each step; click a failed step for details.

  > **Screenshot placeholder:** _Migrate to EPCM dialog with Target URL and credentials, and the step-by-step Migration Status._

## Task 6: Safely repeat a migration

If validation or import failed, or you need to migrate again with a changed template:

1. Sign in to the **target** EPCM environment as a Service Administrator.

2. Click **Application**, then **Overview**.

3. Click **Actions**, then **Inbox/Outbox Explorer**. If `Migrated_<ApplicationName>_Export_Data.txt` is present, select it, use its **Actions** column, click **Delete**, and confirm **Yes**.

4. Click **Close** to return to Application Overview. Click **Actions**, then **Remove Application**, and confirm **Yes**.

5. Edit the template, re-upload it to the source PCM **Inbox** (overwrite), run **Validate** again, then repeat Task 5.

  > **Screenshot placeholder:** _Inbox/Outbox Explorer on the target with the migrated data file selected for deletion, and the Remove Application action._

## Task 7: Next

Continue with **Path B Lab 4: Validate the Migrated Application and Complete Post-Migration Tasks**.

## Learn More

* [Migrating from Profitability and Cost Management to Enterprise Profitability and Cost Management (Oracle tutorial)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/tutorial-migrate-pcm-to-epcm/index.html)

## Acknowledgements

* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, September 2026

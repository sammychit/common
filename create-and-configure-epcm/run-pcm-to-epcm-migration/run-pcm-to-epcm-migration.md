# Path B Lab 3: Customize, Validate, and Run the PCM-to-EPCM Migration

## Introduction

You edit the migration template, upload it to the PCM **inbox** (the folder the migration reads from), run a **validation** that checks it without changing anything, then either **Generate Snapshot** (make the files and move them yourself) or **Migrate to EPCM** (Oracle moves and imports them for you).

**Why this matters:** validation is safe and repeatable; the migration itself creates the one application the target environment can hold. Validate until it is clean, then migrate.

Estimated Lab Time: 45 minutes

### Objectives

* Customize the required and optional template sections
* Upload the template to the PCM inbox
* Validate the template and read the Preview and Validate Report
* Generate the snapshot and data extract, or run the direct migration
* Repeat a migration safely if needed

### Prerequisites

* You finished **Path B Lab 2** and have `<YourPCMApplicationName>_Export.xml`
* The target EPCM environment is preconfigured and has no application

## Task 1: Customize the template

Edit the XML file. Keep a copy of every version you upload.

### Required sections

1. **`dimensions`** &ndash; for each of `account_dimension`, `entity_dimension`, `year_dimension`, `period_dimension`, `scenario_dimension`, `version_dimension` (and `currency_dimension` if multicurrency): set `pcm_dimname` to the source dimension name, and complete `member_mapping` (map the source top member to the EPCM top member). Example:

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

2. **`modelpovs`** &ndash; for each group of POV-based rules, add a `pov` entry mapping the source POV to an EPCM model name:

  ```xml
  <modelpovs>
      <pov>
          <pcmpov>2016,January,Actual</pcmpov>
          <epcmmodelname>Actuals Allocation Model</epcmmodelname>
      </pov>
  </modelpovs>
  ```

### Optional sections (edit only if needed)

* **`epcmappname`** &ndash; up to 8 characters.
* **`duplicatememberprefixes`** &ndash; a `dimension` block with `name`, `duplicateprefix`, `prefix_all`, to make duplicate names unique (EPCM needs unique member names).
* **`rename_dimension_mapping`** / **`rename_member_mapping`** &ndash; `artifact_name` blocks with `pcm_name` and `epcm_name`.
* **`datapovs`** &ndash; `pov` blocks with `srcpov`, `destpov` (members in the order Years, Period, Scenario, Version), and `include_calculated_data`.

> **Reserved names:** member names starting with prefixes used by other EPM business processes (for example `FCCS_`, `OEP_`, `OWP_`, `OPF_`, `OCX_`, `PCM_`, `TRCS_`) are handled specially. Validation flags names to prefix or rename. The system dimensions are renamed for you: `RULE` &rarr; `PCM_Rule`, `BALANCE` &rarr; `PCM_Balance`.

## Task 2: Upload the template to the PCM inbox

**Why:** the migration reads the template from the inbox, not from your computer.

1. On the source PCM Home page, click **Application**, then the **Application** icon.
2. Select the **File Explorer** tab.
3. Click **Upload**.
4. For **File Name**, browse to your edited `<YourPCMApplicationName>_Export.xml`.
5. For **Folder Location**, select **Inbox**.
6. Click **OK**. If asked, overwrite the existing file.

> **Tip:** you can also upload with EPM Automate: `epmautomate uploadFile "<FILE_NAME>" profitinbox`

**Check:** the file appears in **File Explorer** under **Inbox**.

## Task 3: Validate the template

**Why:** validation finds problems safely, before anything is created.

1. On the source PCM Home page, click **Migrate to EPCM**.
2. Click **Validate**.
3. **Migration Status** shows **Success** or **Failed**. If it fails, click the **Failed** link for the row-level errors (common causes: period or year format, dimension order, duplicate members needing a prefix).
4. Fix the template, re-upload to the **Inbox** (Task 2, overwrite), and validate again. Repeat until it succeeds.

**Check:** **Migration Status** shows **Success** for validation and no **Failed** links remain.

## Task 4: Read the Preview and Validate Report

**Why:** it shows exactly what the migration will do before you run it.

1. Click **Preview And Validate Report**.
2. Save `Preview_and_Validation_Report.txt` and open it.
3. Review: duplicate members between PCM and EPCM, prefixes applied, renamed dimensions and members, the POV groups that become models, rule counts per model, and any changed custom calculation formulas.

**Check:** the report matches what you expect from your template edits.

## Task 5: Generate Snapshot or Migrate directly

### Option A &ndash; Generate Snapshot (you move the files)

1. On the **Migrate to EPCM** page, click **Generate Snapshot**.
2. When it finishes, the source **outbox** holds three files:

  | File | Contents |
  | --- | --- |
  | `Migrated_<ApplicationName>_Export_Data.txt` | The data extract, in EPCM (Essbase) format. Load it later via **Application &rarr; Overview &rarr; Import Data**. |
  | `<ApplicationName>_<ExportDate>_<ExportTime>.zip` | The EPCM application snapshot. |
  | `<ApplicationName>_Export_Data.log` | The migration log, for troubleshooting. |

3. Download the files. On the **target** environment, upload the snapshot, use **Migrate** on the EPCM landing page to create the application from it, then import the data extract.

### Option B &ndash; Migrate to EPCM (Oracle moves the files)

1. On the **Migrate to EPCM** page, click **Migrate to EPCM**.
2. Enter the target **Target URL**, Service Administrator **username**, and **password**.
3. Click **Migrate**.
4. The process validates the template, builds the snapshot and data export, connects to the target, uploads them, and imports the application and data. **Migration Status** shows Success or Failed per step; click a failed step for details.

**Check (either option):** the target environment now has an EPCM application, and **Migration Status** shows **Success** for the snapshot and import steps.

## Task 6: Repeat a migration safely

If a step failed, or you want to migrate again with a changed template:

1. Sign in to the **target** EPCM environment as a Service Administrator.
2. Click **Application**, then **Overview**.
3. Click **Actions**, then **Inbox/Outbox Explorer**. If `Migrated_<ApplicationName>_Export_Data.txt` is there, select it, open its **Actions**, click **Delete**, confirm **Yes**.
4. Click **Close**. Click **Actions**, then **Remove Application**, confirm **Yes**.
5. Edit the template, re-upload it to the source PCM **Inbox** (overwrite), run **Validate** again, then repeat Task 5.

**Check:** the target has no application and no leftover migrated data file, ready for a clean re-run.

## Task 7: Next

Continue with **Path B Lab 4: Validate the Migrated Application and Complete Post-Migration Tasks**.

## Learn More

* [Migrating from Profitability and Cost Management to Enterprise Profitability and Cost Management (Oracle tutorial)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/tutorial-migrate-pcm-to-epcm/index.html)

## Acknowledgements

* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, September 2026

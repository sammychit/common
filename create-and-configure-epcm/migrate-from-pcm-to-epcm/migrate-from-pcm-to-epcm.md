# Migrate from PCM to EPCM

## Introduction

This lab describes how to migrate an existing Oracle Profitability and Cost Management (PCM) application to Enterprise Profitability and Cost Management (EPCM). An in-place migration is not possible because the two business processes have different requirements. Instead, you download a **migration template**, customize it, and use it to generate an **application snapshot** and a **data extract** that are compatible with EPCM &mdash; or migrate directly to a target EPCM instance.

Estimated Lab Time: -- minutes

### Objectives

In this lab, you will:

* Generate the migration template from your PCM application
* Customize the migration template to convert metadata, models, and data
* Upload the customized template to the PCM inbox
* Validate the template and review the validation report
* Generate the migration files, or migrate directly to an EPCM instance
* Validate the migration results in EPCM

### Prerequisites

Ensure that:

* You have **Service Administrator** access to the EPM Cloud instance containing the **Profitability and Cost Management** application you want to migrate.
* You have **Service Administrator** access to a **second** EPM Cloud instance with the **Enterprise Profitability and Cost Management** business process enabled. This instance must **not** already have an application created.

## Task 1: Prepare the PCM application

Before generating the template, review and clean up the source PCM application:

* Remove unused members and validate dimensions.
* Document allocation rules, calculation logic, and the POVs that contain rules.
* Note any Data Management (Data Integration) setups, reports, model views, and security &mdash; these are **not** carried by the migration and must be recreated in EPCM.

## Task 2: Generate the migration template

1. Sign in as a Service Administrator to your Profitability and Cost Management instance.

2. On the Home page, click **Application**, then click **Migrate to EPCM**.

3. On the **Migrate to EPCM** page, click **Generate Template**.

4. Save the generated file to your file system. It is named for your application, for example `<YourPCMApplicationName>_Export.xml`.

  > **Screenshot placeholder:** _Migrate to EPCM page with the Generate Template button._

## Task 3: Customize the migration template

Open the XML file in a text or XML editor and update the following sections. The template contains dimension-mapping, model-artifact, and data-mapping instructions that the migration process uses to convert the application into an EPCM-compatible import format.

**Mandatory sections:**

| Section | Purpose |
| --- | --- |
| `dimensions` | Map each source PCM dimension to the corresponding EPCM target dimension, and map top members. Used to build the application snapshot. For the Period dimension you also specify the period frequency and fiscal start. |
| `modelpovs` | Convert groups of POV-specific rules into named **Models**. Used to build the application snapshot. |

**Optional sections (update only if applicable):**

| Section | Purpose |
| --- | --- |
| `epcmappname` | Specify a name for the new Enterprise Profitability and Cost Management application. |
| `duplicatememberprefixes` | Control how duplicate member names are made unique. Used to build the application snapshot. |
| `rename_dimension_mapping` | Rename dimensions to comply with EPCM naming rules, or by preference. |
| `rename_member_mapping` | Rename members to comply with EPCM naming rules, or by preference. |
| `datapovs` | Convert existing data POVs to POVs compatible with the new EPCM application. Used to create the data extract. You can leave this empty and migrate data later. |

> **Note:** Member names that begin with prefixes reserved by other EPM business processes (for example, `FCCS_`, `OEP_`, `OWP_`, `OPF_`, `OCX_`, `PCM_`, `TRCS_`) are handled specially during migration. Review the current list and behavior in the Oracle documentation before you migrate.

## Task 4: Upload the customized template to the PCM inbox

1. Sign in as a Service Administrator to your Profitability and Cost Management instance.

2. On the Home page, click **Application**, then click **Application**.

3. Select the **File Explorer** tab, then click **Upload**.

4. Select the modified `<YourPCMApplicationName>_Export.xml` file, set the folder location to **Inbox**, and click **OK**. If prompted, choose to **overwrite** the existing file.

  > **Tip:** You can also upload with EPM Automate: `epmautomate uploadFile <FILE_NAME> profitinbox`

  > **Screenshot placeholder:** _File Explorer Upload dialog with Inbox selected._

## Task 5: Validate the migration template

1. On the Home page, click **Application**, then click **Migrate to EPCM**.

2. Click **Validate**.

3. When the job finishes, review the **Migration Status**. Click **Preview and Validate Report** to see the details.

4. If validation shows **Failed**, click the failed status for the error details, correct the template, re-upload it to the **Inbox** (Task 4), and validate again.

  > **Screenshot placeholder:** _Migration Status page showing a successful Validate result and the Preview and Validate Report link._

## Task 6: Generate the migration files or migrate directly

On the **Migrate to EPCM** page, choose one option:

**Option A &ndash; Generate Snapshot (manual transfer)**

1. Click **Generate Snapshot**.

2. When complete, the application snapshot and data extract files are placed in the application **outbox**. Download them.

3. On the target EPCM instance, upload the application snapshot, then on the Enterprise Profitability and Cost Management landing page click **Migrate** to create the application from the snapshot. Load the data extract separately.

**Option B &ndash; Migrate to EPCM (direct)**

1. Click **Migrate to EPCM**.

2. Provide the target EPCM instance URL and Service Administrator credentials.

3. The process validates the template, generates the application snapshot and data export, connects to the EPCM instance, imports the application, and imports the data.

  > **Screenshot placeholder:** _Migrate to EPCM dialog with target URL and credential fields._

## Task 7: Validate the migration results in EPCM

1. Sign in to the target Enterprise Profitability and Cost Management instance.

2. Click **Application**, then **Overview**, and check the **Dimensions** tab for the expected dimensions.

3. Click **Modeling**, then **Designer**, and review the models, rule sets, and rules created from `modelpovs`.

4. Run model validation and calculate a POV to confirm results.

## Best Practices

* Clean up and document the PCM application **before** generating the template &mdash; unused members and undocumented rule POVs are the most common causes of validation failures.
* Keep a copy of every version of the customized template; template changes require re-upload and re-validation.
* Validate first and resolve **all** errors before generating the snapshot or migrating directly.
* Plan to recreate items the migration does not carry: Data Integration/Data Management jobs, reports, model views, dashboards, and security.
* Use a non-production EPCM instance for the first migration pass, then compare calculated results against PCM before cutover.

## Learn More

* [Migrating from Profitability and Cost Management to Enterprise Profitability and Cost Management](https://docs.oracle.com/en/cloud/saas/profit-cost-cloud/pcmad/migrating_from_pcm_to_epcm.html)
* [Tutorial: Migrating from Profitability and Cost Management to Enterprise Profitability and Cost Management](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/tutorial-migrate-pcm-to-epcm/index.html)
* [Migrating to Enterprise Profitability and Cost Management (EPM Cloud snapshot migration)](https://docs.oracle.com/en/cloud/saas/enterprise-performance-management-common/cgsad/1_about_epm_cloud_epcm_snapshot_migration.html)

## Acknowledgements

* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, September 2026

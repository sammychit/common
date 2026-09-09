# Path B Lab 2: Prepare and Generate the PCM Migration Template

## Introduction

### What this path is

**PCM (Profitability and Cost Management)** is an older Oracle business process. **EPCM (Enterprise Profitability and Cost Management)** is the newer one. You cannot "upgrade in place": PCM and EPCM are built differently, so migration means **rebuilding the application on a second environment** from an export of the first.

### The words you will see

* **Migration template** &ndash; an **XML** file that Oracle generates from your PCM application. You edit it to say how PCM dimensions and rules map to EPCM.
* **Application snapshot** &ndash; a `.zip` that contains the whole EPCM application structure. **Data extract** &ndash; a text file of the numbers.
* **Inbox** / **outbox** &ndash; server folders each environment has for files you upload / files it produces.
* **POV (point of view)** &ndash; a year/period/scenario/version combination. In PCM, groups of rules are tied to POVs; in EPCM those groups become **models**.

### Why this lab matters

Most migration failures come from an untidy source application. Cleaning it up and reviewing its rules **before** you generate the template saves repeated validation cycles later.

> Do this path only if you have an **existing legacy PCM application**. If you are starting with no application, use **Path A**.

Estimated Lab Time: 25 minutes

### Objectives

In this lab, you will:

* Confirm the source and target prerequisites
* Review and clean up the source PCM application
* Generate and download the migration template
* Understand the template's required and optional sections

### Prerequisites

* **Service Administrator** access to the EPM Cloud environment that contains the **PCM application** you want to migrate (the **source**).
* **Service Administrator** access to a **separate** EPM Cloud environment with the **Enterprise Profitability and Cost Management** business process enabled and **no application created yet** (the **target**). Complete **Common Lab 1** on that environment first.
* Migration requires **both** environments. You cannot migrate within a single environment.

## Task 1: Review and clean up the source PCM application

Do this before generating the template. It prevents most validation failures later.

1. Sign in to the **source** PCM environment as a Service Administrator.

2. Remove unused members and validate every dimension.

3. Document your allocation and custom calculation logic, and note which **POVs** contain rules &mdash; you will group these into EPCM **models** in the template.

4. Note the artifacts that migration does **not** carry and will need to be recreated in EPCM (covered in Path B Lab 4): security, data integrations / load profiles, reports, profit curves, model views, dashboards, infolets, and forms.

**Success check:** every PCM dimension validates with no errors, and you have a written list of rule POV groups and of artifacts to rebuild later.

## Task 2: Generate the migration template

**Why:** the template is the file you will customize; it is the starting point for every later step.

1. On the source PCM Home page, click **Application**, then click **Migrate to EPCM**.

2. Click **Generate Template**.

3. Save the file to your computer. It is named for the application, for example `<YourPCMApplicationName>_Export.xml` (such as `BksML30_Export.xml`).

**Expected outcome:** an XML file downloads to your computer.

**Success check:** you can open the file in a text editor and see sections such as `<dimensions>` and `<modelpovs>`.

  > **Screenshot placeholder:** _Migrate to EPCM page with the Generate Template button, and the saved XML file._

## Task 3: Understand the template sections

Open the XML file in a text or XML editor and review its sections. You will edit them in the next lab.

**Mandatory:**

| Section | Purpose |
| --- | --- |
| `dimensions` | Map each source PCM dimension to its EPCM target dimension, and map top members. Contains `account_dimension`, `entity_dimension`, `year_dimension`, `period_dimension`, `scenario_dimension`, `version_dimension`, and optionally `currency_dimension` (multicurrency). The `period_dimension` also carries the period frequency and fiscal start. |
| `modelpovs` | Convert each group of POV-specific rules into a named EPCM **model**. Required if the application has rules. |

**Optional:**

| Section | Purpose |
| --- | --- |
| `epcmappname` | Name for the new EPCM application (maximum 8 characters). Defaults to the PCM application name. |
| `duplicatememberprefixes` | Make duplicate member names unique by adding a prefix per dimension. |
| `rename_dimension_mapping` | Rename dimensions for naming compliance or preference. |
| `rename_member_mapping` | Rename individual members. |
| `datapovs` | List the data POVs to migrate (mapping source members to EPCM members, in the order Years, Period, Scenario, Version). You can leave this empty and load data later. |

## Task 4: Next

Continue with **Path B Lab 3: Customize, Validate, and Run the PCM-to-EPCM Migration**.

## Learn More

* [Migrating from Profitability and Cost Management to Enterprise Profitability and Cost Management (Oracle tutorial)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/tutorial-migrate-pcm-to-epcm/index.html)

## Acknowledgements

* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, September 2026

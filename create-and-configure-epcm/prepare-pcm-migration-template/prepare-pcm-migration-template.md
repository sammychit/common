# Path B Lab 2: Prepare and Generate the PCM Migration Template

## Introduction

### What this path is

**PCM** is the older Oracle business process; **EPCM** is the newer one. You cannot upgrade in place &ndash; they are built differently. Migration means **rebuilding the application on a second environment** from an export of the first.

### Words you will see

* **Migration template** &ndash; an **XML** file Oracle makes from your PCM application. You edit it to say how PCM dimensions and rules map to EPCM.
* **Application snapshot** &ndash; a `.zip` of the whole EPCM application structure. **Data extract** &ndash; a text file of the numbers.
* **Inbox / outbox** &ndash; server folders for files you upload / files the environment produces.
* **POV** &ndash; a year/period/scenario/version combination. In PCM, groups of rules are tied to POVs; in EPCM those groups become **models**.

### Why this lab matters

Most migration failures come from an untidy source application. Tidying it up first saves repeated validation cycles later.

> Do this path only if you have an **existing PCM application**. Starting from nothing? Use **Path A**.

Estimated Lab Time: 25 minutes

### Objectives

* Confirm the source and target prerequisites
* Clean up the source PCM application
* Generate and download the migration template
* Learn the template's required and optional sections

### Prerequisites

* **Service Administrator** access to the environment holding the **PCM application** to migrate (the **source**)
* **Service Administrator** access to a **separate** environment, switched on for EPCM, with **no application yet** (the **target**). Do **Common Lab 1** there first.
* Migration needs **both** environments. You cannot migrate inside one environment.

## Task 1: Clean up the source PCM application

**Why:** this prevents most validation failures later.

1. Sign in to the **source** PCM environment as a Service Administrator.
2. Remove unused members and validate every dimension.
3. Write down your allocation and custom calculation logic, and which **POVs** hold rules. You will group these into EPCM **models** in the template.
4. Note the items migration does **not** carry, to rebuild later (Path B Lab 4): security, data integrations / load profiles, reports, profit curves, model views, dashboards, infolets, and forms.

**Check:** every PCM dimension validates with no errors, and you have a written list of rule POV groups and of items to rebuild.

## Task 2: Generate the migration template

**Why:** the template is the file you customize; every later step starts from it.

1. On the source PCM Home page, click **Application**, then **Migrate to EPCM**.
2. Click **Generate Template**.
3. Save the file. It is named for the application, for example `<YourPCMApplicationName>_Export.xml` (such as `BksML30_Export.xml`).

**Check:** the XML file downloads, and it contains sections such as `<dimensions>` and `<modelpovs>`.

## Task 3: Learn the template sections

Open the XML file in a text editor. You edit it in the next lab.

**Required:**

| Section | Purpose |
| --- | --- |
| `dimensions` | Map each PCM dimension to its EPCM dimension, and map the top members. Holds `account_dimension`, `entity_dimension`, `year_dimension`, `period_dimension`, `scenario_dimension`, `version_dimension`, and `currency_dimension` (if multicurrency). `period_dimension` also carries the period frequency and fiscal start. |
| `modelpovs` | Turn each group of POV-based rules into a named EPCM **model**. Required if the application has rules. |

**Optional:**

| Section | Purpose |
| --- | --- |
| `epcmappname` | Name for the new EPCM application (max 8 characters). Defaults to the PCM name. |
| `duplicatememberprefixes` | Make duplicate member names unique by adding a per-dimension prefix. |
| `rename_dimension_mapping` | Rename dimensions. |
| `rename_member_mapping` | Rename members. |
| `datapovs` | List the data POVs to migrate (source members mapped to EPCM members, in the order Years, Period, Scenario, Version). Leave empty to load data later. |

## Task 4: Next

Continue with **Path B Lab 3: Customize, Validate, and Run the PCM-to-EPCM Migration**.

## Learn More

* [Migrating from Profitability and Cost Management to Enterprise Profitability and Cost Management (Oracle tutorial)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/tutorial-migrate-pcm-to-epcm/index.html)

## Acknowledgements

* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, September 2026

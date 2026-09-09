# Introduction

## About This Workshop

This workshop is a practical, beginner-friendly guide to adopting **Oracle Enterprise Profitability and Cost Management (EPCM)** on an Oracle Cloud EPM Enterprise environment.

Oracle's product documentation explains each EPCM activity on its own detailed page. This workshop gives you an **ordered route** through the EPCM lifecycle so you can move from a brand-new, empty environment to a working application that calculates results, without having to work out the order of steps yourself.

### A few words before you start (plain language)

* **Cloud EPM** &ndash; Oracle's cloud platform for finance planning, close, and analysis. Your subscription lets you run one Oracle application, called a **business process**, per environment.
* **EPCM (Enterprise Profitability and Cost Management)** &ndash; the business process this workshop sets up. It works out **what things cost** and **how profitable they are** by spreading shared costs onto the products, services, or departments that cause them.
* **PCM (Profitability and Cost Management)** &ndash; an older, separate Oracle business process. If you already run PCM, Path B moves it to EPCM.
* **Allocation** &ndash; the act of spreading an amount from where it was recorded to where it belongs, using a **driver** (a basis such as headcount or floor area).
* **Metadata** &ndash; the lists and hierarchies you analyse by (accounts, departments, periods). **Data** &ndash; the numbers stored against them.
* **Model, rule, POV** &ndash; a **model** holds the calculation logic; a **rule** is one calculation step; a **POV (point of view)** is the year/period/scenario/version combination you calculate. These are explained fully in the *EPCM Modeling Concepts* reference.

You start from one of two situations:

* You have **no EPCM application** and want to build one. &rarr; **Path A**
* You have an **existing legacy Profitability and Cost Management (PCM) application** and want to move it to EPCM. &rarr; **Path B**

An optional final section shows the **PCM Agent**, a Generative AI assistant that can create and run modeling artifacts from natural-language instructions after an EPCM application exists.

Estimated Workshop Time: 10 minutes (this introduction)

## What You Will Learn

* How to choose the right adoption path
* How to enable the EPCM business process on your environment
* **Path A:** create a new application, configure dimensions, load supplied metadata and data, build a model / rule set / rule, validate, and calculate
* **Path B:** prepare and generate the PCM migration template, validate and run the migration, and complete post-migration tasks
* The essential EPCM configuration and modeling objects
* **Optional:** enable and use the PCM Agent

## Which Path Is Right for You?

| Your situation | Follow | Labs |
| --- | --- | --- |
| I have an EPM Enterprise subscription but **no EPCM application yet** | **Path A: Create a New EPCM Application** | Common Lab 1, then Path A Labs 2&ndash;4 |
| I have an **existing legacy PCM application** to move to EPCM | **Path B: Migrate a Legacy PCM Application** | Common Lab 1, then Path B Labs 2&ndash;4 |
| I **already have an EPCM application** (built here, migrated, or the BksML50 sample) and want to try the AI assistant | **Optional: Use PCM Agent** | Optional Labs |

Path A and Path B are **alternatives**. You do not need to do both. A learner creating a new application does **not** perform migration steps, and a learner migrating legacy PCM does **not** build an application from scratch.

## Workshop Structure

| Section | Lab | Time |
| --- | --- | --- |
| Common | Common Lab 1: Enable the EPCM Business Process | 25 minutes |
| Reference | EPCM Modeling Concepts (short read) | 10 minutes |
| Path A | Path A Lab 2: Create a New EPCM Application | 20 minutes |
| Path A | Path A Lab 3: Configure Dimensions and Load Metadata and Data | 35 minutes |
| Path A | Path A Lab 4: Create a Model, Rule Set, Rules, POV, and Run a Calculation | 40 minutes |
| Path B | Path B Lab 2: Prepare and Generate the PCM Migration Template | 25 minutes |
| Path B | Path B Lab 3: Customize, Validate, and Run the PCM-to-EPCM Migration | 45 minutes |
| Path B | Path B Lab 4: Validate the Migrated Application and Complete Post-Migration Tasks | 30 minutes |
| Optional | Optional Lab: Enable the PCM Agent | 10 minutes |
| Optional | Optional Lab: Use the PCM Agent | 20 minutes |

Approximate end-to-end time after your environment is available: **Path A about 2 to 2.5 hours**, **Path B about 2 to 2.5 hours** (excluding source-application cleanup and migration troubleshooting). The optional PCM Agent section adds **20&ndash;30 minutes**.

## Prerequisites

**All paths:**

* An **Oracle Cloud EPM Enterprise** subscription
* **Service Administrator** access to the environment
* Familiarity with basic Cloud EPM navigation (Home page, Application cluster, Jobs, File Explorer)

**Path A also requires:**

* An environment with **no application created yet**
* The supplied example metadata and data files (included with Lab 3, in its `files/` folder)

**Path B also requires:**

* A **source** environment that contains the legacy PCM application you want to migrate, with Service Administrator access
* A **separate target** environment with the **Enterprise Profitability and Cost Management** business process enabled and **no application created yet**
* Time to review and clean up the source PCM application before migrating

**Optional PCM Agent section also requires:**

* An existing EPCM application (from Path A, Path B, or the BksML50 sample)
* An environment on the **April 2026 (26.04)** update or later, on Oracle Cloud Infrastructure (OCI), in a region where **Generative AI** is available
* English-language use; all generated commands are reviewed before they run

## Notes on Scope

This workshop stays **generic**. It explains EPCM platform concepts and configuration mechanics in neutral terms and does not model a specific company or industry. The supplied example files are small, neutral training data. Your organization decides its own source, destination, driver, offset, and custom calculation logic; where this workshop shows specific selections, they are clearly labeled as illustrative choices for the training data only.

Screenshot placeholders in these labs describe what to capture. The workshop author adds the images.

## Learn More

* [Oracle Cloud EPM Enterprise Profitability and Cost Management documentation](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/index.html)
* [Migrating from Profitability and Cost Management to Enterprise Profitability and Cost Management (tutorial)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/tutorial-migrate-pcm-to-epcm/index.html)

## Acknowledgements

* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, September 2026

# Introduction

## About This Workshop

This workshop helps a first-time user set up **Oracle Enterprise Profitability and Cost Management (EPCM)** on an Oracle Cloud EPM Enterprise environment.

Oracle's documentation covers each step on its own page. This workshop puts the steps in order, so you can go from a new, empty environment to an application that calculates results.

### Words you will meet

* **Cloud EPM** &ndash; Oracle's cloud platform for finance. Each environment runs one Oracle application, called a **business process**.
* **EPCM** &ndash; the business process you set up here. It works out what things cost and how profitable they are, by spreading shared costs onto the products, services, or departments that cause them.
* **PCM (Profitability and Cost Management)** &ndash; an older, separate Oracle business process. If you already run PCM, Path B moves it to EPCM.
* **Allocation** &ndash; spreading an amount from where it was recorded to where it belongs, using a **driver** such as headcount.
* **Metadata** &ndash; the lists you analyse by (accounts, departments, periods). **Data** &ndash; the numbers held against them.
* **Model, rule, POV** &ndash; a **model** holds the calculation logic; a **rule** is one calculation step; a **POV (point of view)** is the year, period, scenario, and version you calculate. The *EPCM Modeling Concepts* reference explains these.

### Choose your path

* You have **no EPCM application** and want to build one &rarr; **Path A**.
* You have an **existing PCM application** and want to move it to EPCM &rarr; **Path B**.

Paths A and B are alternatives. You do only one.

The **PCM Agent** (an optional section) is an AI assistant that builds and runs modeling items from typed instructions, once an application exists. It is a helper, not the point of the workshop.

Estimated Workshop Time: 10 minutes (this introduction)

## What You Will Learn

* How to pick the right path
* How to switch the environment on for EPCM
* **Path A:** create an application, set up dimensions, load the supplied metadata and data, build a model and rules, validate, and calculate
* **Path B:** prepare the migration template, run the migration, and finish the post-migration work
* The core EPCM building blocks
* **Optional:** turn on and use the PCM Agent

## Which Path Is Right for You?

| Your situation | Follow | Labs |
| --- | --- | --- |
| I have a subscription but **no EPCM application yet** | **Path A** | Common Lab 1, then Path A Labs 2&ndash;4 |
| I have an **existing PCM application** to move | **Path B** | Common Lab 1, then Path B Labs 2&ndash;4 |
| I **already have an EPCM application** and want to try the AI assistant | **Optional PCM Agent** | Optional Labs |

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

After your environment is ready, each path takes about **2 to 2.5 hours**. The optional PCM Agent section adds **20 to 30 minutes**.

## Prerequisites

**All paths:**

* An **Oracle Cloud EPM Enterprise** subscription
* **Service Administrator** access
* You can find your way around Cloud EPM (Home page, the Application area, Jobs, File Explorer)

**Path A also needs:**

* An environment with **no application yet**
* The example files supplied with Lab 3 (in its `files/` folder)

**Path B also needs:**

* A **source** environment that holds the PCM application to move, with Service Administrator access
* A **separate target** environment, switched on for EPCM, with **no application yet**
* Time to tidy up the source PCM application first

**Optional PCM Agent section also needs:**

* An existing EPCM application (from Path A, Path B, or the BksML50 sample)
* An environment on the **April 2026 (26.04)** update or later, on Oracle Cloud Infrastructure (OCI), in a region where **Generative AI** is available
* English input; you review every command before it runs

## Scope

This workshop stays generic. It explains EPCM in neutral terms and does not model a real company. The example files hold small, made-up training numbers. Your organisation decides its own source, destination, driver, offset, and formulas; where a lab shows specific choices, they are marked as examples for the training data only.

## Learn More

* [Oracle Cloud EPM Enterprise Profitability and Cost Management documentation](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/index.html)
* [Migrating from Profitability and Cost Management to Enterprise Profitability and Cost Management (Oracle tutorial)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/tutorial-migrate-pcm-to-epcm/index.html)

## Acknowledgements

* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, September 2026

# Enable the Enterprise Profitability and Cost Management Business Process

## Introduction

Before you can build an application, an Oracle Cloud EPM environment must be enabled as an **Enterprise Profitability and Cost Management** business process. In this lab you confirm your subscription and readiness, then use the **EPM Enterprise Cloud Service landing page** to select the Enterprise Profitability and Cost Management business process and choose how the application will be created.

Estimated Lab Time: -- minutes

### Objectives

In this lab, you will:

* Confirm that your environment is an EPM Enterprise Cloud Service instance
* Select **Enterprise Profitability and Cost Management** on the landing page
* Understand the three ways to create the application: **Create** (sample), **Start** (new), and **Migrate** (from a snapshot)

### Prerequisites

Ensure that:

* You have an **EPM Enterprise Cloud Service** subscription
* You are a **Service Administrator** for the instance on which the application will be created
* The instance is **new** &mdash; no business process/application has been created on it yet

> **Note:** An EPM Enterprise Cloud Service environment allows you to create **only one** application. After you initiate creation of an application, you cannot return to the landing page. To create a different application, you must first reset the environment to its original state.

## Task 1: Confirm EPM Enterprise readiness

1. Sign in to your Cloud EPM environment as a Service Administrator.

2. If no application has been created, the **EPM Enterprise Cloud Service landing page** is displayed. It presents a card for each business process you can create (for example, Planning, Financial Consolidation and Close, Tax Reporting, Account Reconciliation, Profitability and Cost Management, Enterprise Profitability and Cost Management, Narrative Reporting, and Enterprise Data Management). The availability of these business processes indicates an **Enterprise** subscription.

  > **Screenshot placeholder:** _EPM Enterprise Cloud Service landing page showing the business process cards, with the Enterprise Profitability and Cost Management card visible._

## Task 2: Select the Enterprise Profitability and Cost Management business process

1. On the landing page, locate the **Enterprise Profitability and Cost Management** card and click **Select**.

2. Click **OK** to start pre-configuring the environment for this business process.

  * The environment is **not available** during pre-configuration, which takes approximately 20 minutes.

  > **Screenshot placeholder:** _Confirmation dialog after clicking Select, and the pre-configuration in-progress message._

3. When pre-configuration completes, the **Enterprise Profitability and Cost Management** business process landing page is displayed with the following options:

  | Option | What it does |
  | --- | --- |
  | **Create** | Creates the ready-to-use **sample application** (BksML50) with artifacts and data. |
  | **Start** | Launches the **Create Application** wizard to build a new, empty application. |
  | **Migrate** | Creates the application by importing a previously uploaded **application snapshot** (used for the PCM &rarr; EPCM migration). |

  > **Screenshot placeholder:** _Enterprise Profitability and Cost Management landing page showing the Create, Start, and Migrate options._

  > **Note:** In the **Create Application** wizard, the **Dimension Mapping** and **Customize** options are disabled and are not applicable for Enterprise Profitability and Cost Management.

## Task 3: Choose your path through the workshop

Depending on which lab you run next, choose one option now:

* **Create an EPCM application from scratch** &rarr; use **Start**. See the *Create an EPCM Application from Scratch* lab.
* **Migrate an existing PCM application** &rarr; use **Migrate**. See the *Migrate from PCM to EPCM* lab (it also covers generating and uploading the snapshot from the PCM side first).
* **Explore rules and the PCM Agent quickly** &rarr; use **Create** to deploy the **BksML50** sample application. The rule labs and the PCM Agent lab are written against this sample.

The **BksML50** sample application models "Bikes", a fictional bicycle manufacturer and distributor. It includes 8 rule sets containing 26 rules (a waterfall of currency conversions followed by allocations), with revenue and expenses dimensionalized across **Entity**, **Account**, **Activity**, **Product**, and **Customer**, plus analysis views.

To deploy it: on the business process landing page click **Create**, wait for the process to finish, and when the **Application created successfully** message appears, click **OK** to open the sample application.

## Learn More

* [Creating a Business Process from the EPM Enterprise Landing Page](https://docs.oracle.com/en/cloud/saas/enterprise-performance-management-common/cgsad/1_about_epm_enterprise_landing_page.html)
* [Creating the Sample Application](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/creating_a_sample_application.html)
* [Creating a New Application](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/creating_a_new_application.html)
* [Enterprise Profitability and Cost Management Quick Start Checklists](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/ckepf/epcmcs_service_admin_administer.html)

## Acknowledgements

* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, September 2026

# Path A Lab 2: Create a New EPCM Application

## Introduction

### What "create an application" means

In **Common Lab 1** you switched the environment on for EPCM (preconfiguration). That gave you an empty EPCM framework. **Creating an application** is the next step: a short **wizard** where you set the three things that are **fixed for the life of the application** &mdash; its **name**, its **calendar** (which years and periods it covers), and its **currency** setup. After the wizard, the application exists but is still empty; you add accounts, departments, and numbers in Lab 3.

### Why this lab matters

The calendar and the multicurrency choice **cannot be changed later**. Getting them right now avoids having to reset the whole environment and start over.

> Do this lab only if you are on **Path A**. If you are migrating a legacy PCM application, use **Path B**.

Estimated Lab Time: 20 minutes

### Objectives

In this lab, you will:

* Start the **Create Application** wizard
* Set the application **name and description**
* Set the **calendar** (period frequency, year range, first month)
* Set the **currency** option
* Review and create the application

### Prerequisites

* You completed **Common Lab 1**; the environment is preconfigured and you are on the **Enterprise Profitability and Cost Management** page
* No application has been created yet

## Task 1: Start the wizard

**Why:** this opens the guided setup.

1. On the **Enterprise Profitability and Cost Management** page, under **Create a new application**, click **Start**.

**Expected outcome:** the **Create Application** wizard opens at the **General** page.

**Success check:** you see a wizard with steps for General and Details.

  > **Note:** The **Dimension Mapping** and **Customize** options are disabled &mdash; they do not apply to EPCM.

  > **Screenshot placeholder:** _Enterprise Profitability and Cost Management page with the Start button under "Create a new application"._

## Task 2: Enter a name and description

**Why:** the name identifies the application. It cannot be changed after creation.

1. On the **Create Application: General** page, enter a **Name** (for example, `EPCMTRAIN`).

2. Enter a **Description** (optional).

3. Click **Next**.

**Success check:** the wizard moves to the **Details** page.

  > **Screenshot placeholder:** _Create Application: General page with Name and Description entered._

## Task 3: Set up the calendar

**Why:** the calendar creates the **Years** dimension (the fiscal years) and the **Period** dimension (the months). Its range and start month are permanent.

The calendar is in the **Period Frequency** section of the **Create Application: Details** page.

1. Choose a **period frequency**:

  | Frequency | Fields |
  | --- | --- |
  | **Monthly** | **Start and End Year**, **First Month of Fiscal Year**. If the first month is not January, also **Fiscal Year Start Date** (**Same Calendar Year** or **Previous Calendar Year**). |
  | **Quarterly** | **Start and End Year**, **First Fiscal Period Start Date**. |
  | **Custom** | **Start and End Year**, **Periods Per Year**, **Prefix**. |

  For this workshop, choose **Monthly**.

2. Set **Start and End Year** to **2024** to **2025**. This matches the training data in Lab 3 and creates the Years members `FY24` and `FY25`.

3. Set **First Month of Fiscal Year** to **January**. This builds the Period dimension as `Jan` &hellip; `Dec`.

**Success check:** the Period Frequency section shows Monthly, 2024&ndash;2025, and January.

  > **Screenshot placeholder:** _Period Frequency section with Monthly, the 2024-2025 range, and January._

## Task 4: Set up currencies

**Why:** this decides whether the application can hold input in more than one currency. It **cannot be changed after creation**.

Currencies are in the **Other Details** section of the **Create Application: Details** page.

1. Set **Main Currency** to your reporting currency (for example, **USD**).

2. Set **Multicurrency Support** to **No**. The Lab 3 training data has no currency member, so it expects a single-currency application. Choose **Yes** only for a real project that loads input in several currencies (then you must add a currency member to the data file).

  * If you select **Yes**, a **Currency** dimension is created and the Main Currency becomes its first member.

3. Click **Next**.

**Success check:** Other Details shows your Main Currency and **Multicurrency Support = No**.

  > **Screenshot placeholder:** _Other Details section with Main Currency and Multicurrency Support set to No._

## Task 5: Review and create

1. On the **Create Application: Review** page, check the summary against Tasks 2&ndash;4.

2. Click **Create**.

3. Wait for creation to finish, then open the application from the Home page.

**Expected outcome:** the application is created and opens on the Home page.

**Success check:** the Home page shows the **Application** cluster; **Application &rarr; Overview &rarr; Dimensions** lists Account, Entity, Period, Years, Scenario, Version, PCM_Rule, and PCM_Balance.

  > **Screenshot placeholder:** _Review page summary, and the new application open on the Home page._

## Task 6: Next

The application exists but has no members or data. Continue with **Path A Lab 3: Configure Dimensions and Load Metadata and Data**.

## Learn More

* [Creating a New Application (Oracle EPCM documentation)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/creating_a_new_application.html)
* [Setting Up Currencies (Oracle EPCM documentation)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/set_up_currencies.html)

## Acknowledgements

* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, September 2026

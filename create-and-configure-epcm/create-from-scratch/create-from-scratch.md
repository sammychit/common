# Path A Lab 2: Create a New EPCM Application

## Introduction

In Common Lab 1 you switched the environment on for EPCM. Now you **create the application** with a short wizard.

The wizard sets three things that **cannot be changed later**: the application **name**, the **calendar** (which years and months it covers), and the **currency** setup. After the wizard the application exists but is empty. You add accounts, departments, and numbers in Lab 3.

**Why this matters:** the calendar and the multicurrency choice are permanent. Getting them right now saves resetting the whole environment later.

> Do this lab only on **Path A**. To migrate a PCM application, use **Path B**.

Estimated Lab Time: 20 minutes

### Objectives

* Start the **Create Application** wizard
* Set the name, calendar, and currency
* Create the application

### Prerequisites

* You finished **Common Lab 1**; the environment is preconfigured and you are on the **Enterprise Profitability and Cost Management** page
* No application exists yet

## Task 1: Start the wizard

**Why:** this opens the guided setup.

1. On the **Enterprise Profitability and Cost Management** page, under **Create a new application**, click **Start**.

**Check:** the **Create Application** wizard opens at the **General** page. (The **Dimension Mapping** and **Customize** options are greyed out; they do not apply to EPCM.)

## Task 2: Enter a name

**Why:** the name identifies the application and is fixed after creation.

1. On the **Create Application: General** page, enter a **Name** (for example, `EPCMTRAIN`).
2. Enter a **Description** (optional).
3. Click **Next**.

**Check:** the wizard moves to the **Details** page.

## Task 3: Set the calendar

**Why:** the calendar builds the **Years** dimension (fiscal years) and the **Period** dimension (months). The range and start month are permanent.

The calendar is in the **Period Frequency** section of the **Create Application: Details** page.

1. For period frequency, choose **Monthly**.
2. Set **Start and End Year** to **2024** to **2025**. This matches the Lab 3 training data and creates the Years members `FY24` and `FY25`.
3. Set **First Month of Fiscal Year** to **January**. This builds the Period dimension as `Jan` to `Dec`.

**Check:** the Period Frequency section shows Monthly, 2024&ndash;2025, and January.

## Task 4: Set the currency

**Why:** this decides whether the application can hold input in more than one currency. It is permanent.

The currency fields are in the **Other Details** section of the same page.

1. Set **Main Currency** to your reporting currency (for example, **USD**).
2. Set **Multicurrency Support** to **No**. The Lab 3 training data has no currency member, so it needs a single-currency application. Choose **Yes** only for a real project that loads input in several currencies.
3. Click **Next**.

**Check:** Other Details shows your Main Currency and **Multicurrency Support = No**.

## Task 5: Review and create

1. On the **Create Application: Review** page, check the summary against Tasks 2 to 4.
2. Click **Create**.
3. When it finishes, open the application from the Home page.

**Check:** the Home page shows the **Application** area, and **Application &rarr; Overview &rarr; Dimensions** lists Account, Entity, Period, Years, Scenario, Version, PCM_Rule, and PCM_Balance.

## Task 6: Next

The application has no members or data yet. Continue with **Path A Lab 3: Configure Dimensions and Load Metadata and Data**.

## Learn More

* [Creating a New Application (Oracle EPCM documentation)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/creating_a_new_application.html)
* [Setting Up Currencies (Oracle EPCM documentation)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/set_up_currencies.html)

## Acknowledgements

* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, September 2026

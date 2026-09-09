# Common Lab 1: Enable the EPCM Business Process

## Introduction

### What EPCM is

**Enterprise Profitability and Cost Management (EPCM)** is one of the applications you can run in Oracle Cloud EPM. It works out what things cost and how profitable they are. It does this by **allocation**: spreading shared costs (rent, IT, utilities, support teams) onto the products, services, customers, or departments that cause them.

### Preconfigure vs. create

An Oracle Cloud EPM **environment** runs one Oracle application at a time, called a **business process**. Turning the environment on for EPCM is called **preconfiguring** it.

Preconfiguring is not the same as creating an application:

* **Preconfigure** installs the EPCM framework. It takes about **20 minutes**, and the environment is unavailable while it runs.
* **Create an application** comes later. That is where your own structure and data go in.

### Why this matters

An environment holds **only one application**. Once you create it, you cannot come back to this landing page without resetting the whole environment. Go slowly and check each screen.

Estimated Lab Time: 25 minutes

### Objectives

* Open the EPM Enterprise landing page
* Preconfigure the environment for EPCM
* See the three ways to create the application, and know which one your path uses

### Prerequisites

* An Oracle Cloud EPM Enterprise subscription
* **Service Administrator** access (you have it if you can sign in and reach the landing page)
* An environment with **no application yet**

## Task 1: Open the landing page

**Why:** this is where you turn the environment on for a business process.

1. Sign in to your environment.
2. Because no application exists, the **EPM Enterprise landing page** opens. It shows one card per business process.

**Check:** you can see a card named **Profitability and Cost Management**.

## Task 2: Start preconfiguration

**Why:** clicking **OK** begins the 20-minute setup. Nothing here creates an application yet.

1. On the **Profitability and Cost Management** card, click **Select**.
2. When asked, click **OK**.

The environment goes offline while it works.

**Check:** after about 20 minutes you can sign in again.

## Task 3: Select Enterprise Profitability and Cost Management

**Why:** this picks the specific business process you want.

1. Sign in again.
2. Click **Select** under **Enterprise Profitability and Cost Management**.

**Check:** the **Enterprise Profitability and Cost Management** page opens, showing the **CREATE**, **START**, and **MIGRATE** options.

## Task 4: Know the three choices

| Button | What it does | Who uses it |
| --- | --- | --- |
| **CREATE** | Builds a ready-made **sample application** with data, so you can explore right away. | Optional. Useful if you only want to try the PCM Agent. |
| **START** | Opens a wizard to build a **new, empty application** you set up yourself. | **Path A** |
| **MIGRATE** | Builds the application from a **snapshot** you uploaded earlier. | **Path B** |

Do not click yet unless you are carrying straight on. Once you create an application, this page is gone.

### Go to your next lab

* **Path A:** go to **Path A Lab 2: Create a New EPCM Application** (it uses **START**).
* **Path B:** go to **Path B Lab 2: Prepare and Generate the PCM Migration Template**. You return here and use **MIGRATE** in Path B Lab 3.

## Learn More

* [Preconfiguring Your Environment (Oracle EPCM documentation)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/preconfiguring_your_environment.html)

## Acknowledgements

* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, September 2026

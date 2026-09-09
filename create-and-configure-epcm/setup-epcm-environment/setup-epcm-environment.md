# Common Lab 1: Enable the EPCM Business Process

## Introduction

### What is EPCM?

**Enterprise Profitability and Cost Management (EPCM)** is one of the applications you can run in Oracle Cloud EPM. It helps an organisation work out **what things really cost** and **how profitable they are**, by spreading shared costs (rent, IT, utilities, support teams) onto the products, services, customers, or departments that actually cause them. That spreading is called **allocation**.

### What is a "business process", and what does "preconfigure" mean?

An Oracle Cloud EPM **environment** runs **one** Oracle application type at a time &mdash; called a **business process**. Before you can use EPCM, you switch the environment on for it. Oracle calls this **preconfiguring** the environment.

Preconfiguring is **not** the same as creating an application:

* **Preconfiguring** installs the EPCM framework on the environment. It takes about **20 minutes**, and the environment is **not available** while it runs.
* **Creating an application** is a later, separate step where *your* structure and data go in. Path A builds one from scratch; Path B builds one from a migrated PCM snapshot.

### Why this lab matters

This is the foundation for everything that follows, and it is mostly a **one-way** step: an environment holds **only one application**, and once you create that application you cannot return to this landing page without resetting the whole environment. Take it slowly and confirm each screen.

Estimated Lab Time: 25 minutes

### Objectives

In this lab, you will:

* Open the EPM Enterprise landing page
* Preconfigure the environment for Enterprise Profitability and Cost Management, using Oracle's current two-step Select flow
* See the three ways to create the application (**CREATE**, **START**, **MIGRATE**) and know which one your path uses

### Prerequisites

* An Oracle Cloud EPM Enterprise subscription
* **Service Administrator** access (you have this if you can sign in and reach the landing page)
* An environment where **no application has been created yet**

## Task 1: Open the EPM Enterprise landing page

1. Sign in to your environment.

2. Because no application exists yet, the **EPM Enterprise landing page** opens. It shows a card for each business process you could create (Planning, Financial Consolidation and Close, Profitability and Cost Management, and others).

**Expected outcome:** you see the landing page with the business process cards.

**Success check:** you can see a card labelled **Profitability and Cost Management**.

  > **Screenshot placeholder:** _EPM Enterprise landing page showing the business process cards, with the Profitability and Cost Management card visible._

## Task 2: Start preconfiguration

Oracle's current flow starts from the **Profitability and Cost Management** card (EPCM shares this starting point).

1. On the **Profitability and Cost Management** card, click **Select**.

2. When prompted, click **OK** to start preconfiguration.

**Why:** clicking **OK** begins the ~20‑minute preconfiguration. The environment is unavailable during this time. Nothing you do here creates an application yet.

**Expected outcome:** a message tells you preconfiguration has started; the environment becomes temporarily unavailable.

**Success check:** after roughly 20 minutes you can sign in again and continue with Task 3.

  > **Screenshot placeholder:** _Confirmation dialog after clicking Select, and the "preconfiguration in progress" message._

## Task 3: Select Enterprise Profitability and Cost Management

After preconfiguration finishes, you choose the specific business process.

1. Sign in again.

2. Click **Select** under **Enterprise Profitability and Cost Management**.

**Expected outcome:** the **Enterprise Profitability and Cost Management** page opens, showing three ways to create the application.

**Success check:** you can see the **CREATE**, **START**, and **MIGRATE** options described in Task 4.

  > **Screenshot placeholder:** _Enterprise Profitability and Cost Management page showing the CREATE, START, and MIGRATE options._

## Task 4: Understand the three creation choices

| Button | What it does | Who uses it |
| --- | --- | --- |
| **CREATE** | Creates a ready-made **sample application** with data and artifacts already built, so you can explore EPCM immediately. | Optional. Handy if you only want to try the PCM Agent. |
| **START** | Opens a wizard to build a **new, empty application** that you configure yourself. | **Path A** (the main new-application journey). |
| **MIGRATE** | Builds the application from an **application snapshot** you have already uploaded to the environment. | **Path B** (migrating a legacy PCM application). |

**Do not click yet unless you are continuing now.** Once you create an application, this landing page is no longer available.

### Choose your next lab

* **Path A &ndash; build a new application:** go to **Path A Lab 2: Create a New EPCM Application** (it uses **START**).
* **Path B &ndash; migrate a legacy PCM application:** go to **Path B Lab 2: Prepare and Generate the PCM Migration Template**. You will come back to this page and use **MIGRATE** in Path B Lab 3.

## Learn More

* [Preconfiguring Your Environment (Oracle EPCM documentation)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/preconfiguring_your_environment.html)

## Acknowledgements

* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, September 2026

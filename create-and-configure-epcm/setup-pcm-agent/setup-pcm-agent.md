# Optional Lab: Enable the PCM Agent

## Introduction

**Generative AI** turns a plain-English sentence into a structured EPCM command. The **PCM Agent** is that assistant, built into EPCM's modeling screens. You type a request; it proposes a command; you review it and confirm; then it runs as a normal EPCM job.

This lab turns the agent on. It is a convenience for building and running modeling items. Nothing earlier in the workshop needs it.

> This section is **optional** and needs an **EPCM application that already exists** &ndash; from Path A, Path B, or the **BksML50** sample (created with **Create** on the landing page).

Estimated Lab Time: 10 minutes

### Objectives

* Confirm the requirements for Generative AI
* Turn on Generative AI
* Reload the navigation flow and find the PCM Agent

### Prerequisites

* An EPCM application is open
* The environment is on the **April 2026 (26.04)** update or later
* The environment runs on **Oracle Cloud Infrastructure (OCI)** in a region where **Generative AI** is available (see *Availability of Generative AI* in the *Oracle EPM Cloud Operations Guide*)
* You are a Service Administrator

### Before you start

* The PCM Agent works in **English only**.
* Generative AI output can be wrong. The agent only proposes a command; **you review and confirm it** before it runs. Nothing runs on its own.
* Every confirmed command runs as a normal EPCM job, shown in **Jobs**.

## Task 1: Turn on Generative AI

1. On the Home page, click **Application**, then **Settings**.
2. Under **Enable AI**, select **Generative AI**.
3. Click **Save**.

**Check:** **Generative AI** shows as selected and saved under **Enable AI**.

## Task 2: Reload the navigation flow

**Why:** the PCM Agent only appears in the menus after a reload.

1. Click the arrow next to your user name (top right).
2. On the **Settings and Actions** menu, click **Reload Navigation Flow**.

**Check:** the page reloads without error.

## Task 3: Find the PCM Agent

1. Go back to the Home page.
2. If a **PCM Agent** card is shown (Home page or **Modeling** cluster), open it.
3. The agent is also inside the modeling screens: **Models**, the **Waterfall Setup** and **Mass Edit** tabs in **Designer**, and **Calculation Control**.

**Check:** you can open a PCM Agent panel and type into its request box.

## Task 4: Next

Continue with **Optional Lab: Use the PCM Agent**.

## Learn More

* [About Profitability and Cost Management (PCM) Agent (Oracle EPCM documentation)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/about_pcm_agent.html)

## Acknowledgements

* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, September 2026

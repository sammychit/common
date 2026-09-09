# Optional Lab: Enable the PCM Agent

## Introduction

**Generative AI** means the assistant can turn a plain-English sentence into a structured EPCM command. The **PCM Agent** is that assistant, built into EPCM's modeling screens. You type a request; it proposes a command; you review, refine, and confirm it; then it runs as a normal EPCM job. This optional lab turns it on. It is a convenience for building and running modeling artifacts &mdash; it is not required for anything earlier in the workshop.

> This section is **optional** and assumes an **EPCM application already exists** &mdash; built in Path A, migrated in Path B, or the **BksML50** sample created with **Create** on the landing page.

Estimated Lab Time: 10 minutes

### Objectives

In this lab, you will:

* Confirm the environment requirements for Generative AI
* Turn on Generative AI
* Reload the navigation flow and locate the PCM Agent

### Prerequisites

* An EPCM application is open
* The environment is on the **April 2026 (26.04)** update or later
* The environment runs on **Oracle Cloud Infrastructure (OCI)** in a region where **Generative AI** is available (see *Availability of Generative AI* in the *Oracle Enterprise Performance Management Cloud Operations Guide*)
* You are a Service Administrator

### Facts to know before you start

* The PCM Agent supports **English only**.
* Generative AI output can be incorrect. The agent proposes a command; **you review and refine it, and you confirm it before it runs**. Nothing executes without your confirmation.
* Each confirmed command runs as a standard EPCM job, visible in **Jobs**.

## Task 1: Turn on Generative AI

1. On the Home page, click **Application**, then **Settings**.

2. Under **Enable AI**, select **Generative AI**.

3. Click **Save**.

**Success check:** the **Generative AI** setting shows as selected/saved under **Enable AI**.

  > **Screenshot placeholder:** _Application Settings with Generative AI selected under Enable AI._

## Task 2: Reload the navigation flow

**Why:** the PCM Agent only appears in the menus after the navigation flow reloads.

1. Click the arrow next to your user name at the top right.

2. On the **Settings and Actions** menu, click **Reload Navigation Flow**.

## Task 3: Locate the PCM Agent

1. Return to the Home page.

2. If a **PCM Agent** card is shown (on the Home page or in the **Modeling** cluster), open it.

3. The agent is also embedded in the modeling screens: **Models**, the **Waterfall Setup** and **Mass Edit** tabs in **Designer**, and **Calculation Control**. Open any of these and use the agent panel there.

**Success check:** you can open a PCM Agent panel (from a card or from a modeling screen) and type into its request box.

  > **Screenshot placeholder:** _PCM Agent available from a modeling screen._

## Task 4: Next

Continue with **Optional Lab: Use the PCM Agent**.

## Learn More

* [About Profitability and Cost Management (PCM) Agent (Oracle EPCM documentation)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/about_pcm_agent.html)

## Acknowledgements

* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, September 2026

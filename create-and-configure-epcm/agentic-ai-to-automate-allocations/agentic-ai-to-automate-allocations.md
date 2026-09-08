# Automate Modeling with the PCM Agent (Generative AI)

## Introduction

The **PCM Agent** is a guided natural-language tool in Enterprise Profitability and Cost Management that uses Generative AI (GenAI) to carry out modeling tasks from plain-English requests. You describe what you want (create a rule set, copy rules, calculate a model, run a trace); the agent proposes a structured command with its parameters; you review, refine, and then run it. Every request runs as a normal EPCM job, so results are auditable and reversible in the usual ways.

In this lab you enable the PCM Agent and use it to perform rule-related modeling tasks against the **BksML50** sample application.

Estimated Lab Time: -- minutes

### Objectives

In this lab, you will:

* Enable Generative AI and the PCM Agent
* Understand the review / refine / run workflow
* Use the PCM Agent to create a rule set and rules
* Use the PCM Agent to copy rules and enable/disable rules
* Use the PCM Agent to calculate a model and run an analytic trace

### Prerequisites

Ensure that:

* Your environment runs the **April 2026 (26.04)** update or later. Beginning July 2026, Generative AI functionality is provided only for environments on 26.04 or later.
* Your environment is on **Oracle Cloud Infrastructure (OCI)** and in a **region where Generative AI is available**. See *Availability of Generative AI* in the Oracle Enterprise Performance Management Cloud Operations Guide.
* You are a **Service Administrator**.
* The **BksML50** sample application is deployed.

> **Note:** The PCM Agent supports **English only**. GenAI output may not always be factual, accurate, or appropriate &mdash; you are responsible for reviewing it before you run any command.

## Task 1: Enable Generative AI and the PCM Agent

1. From the Home page, click **Application**, then **Settings**.

2. Under **Enable AI**, select **Generative AI**, and click **Save**.

3. Click the down arrow next to your user name (top right). On the **Settings and Actions** menu, click **Reload Navigation Flow**.

4. Confirm the **PCM Agent** card now appears on the Home page and in the **Modeling** cluster.

  > **Screenshot placeholder:** _Application Settings with Generative AI selected under Enable AI._

> **About the two versions:** The enhanced PCM Agent is embedded directly in the modeling screens where the work happens &mdash; **Models**, the **Waterfall Setup** and **Mass Edit** tabs in **Designer**, and **Calculation Control**. The original stand-alone PCM Agent (its own card) is planned for removal in the October 2026 (26.10) update.

## Task 2: Learn the review / refine / run workflow

1. Open the **PCM Agent** (from the card, or from within a modeling screen).

2. Type a request in the text box, or click an action button. As you type an artifact name followed by a space and **@**, a smart-lookup list of matching artifacts appears.

3. The agent shows a **suggested command** with its **required** and **optional** parameters.

4. Use **Refine** to edit parameters, then **Resend**.

5. When the command is correct, click **Run Command**.

6. A **Job ID** is returned. Check progress and results in **Jobs** (or **View Jobs** in the agent).

  > **Screenshot placeholder:** _PCM Agent showing a suggested command with parameters and the Run Command button._

## Task 3: Create a rule set and rules with natural language

Try these requests (adjust names to your model). Review each suggested command before running it.

* Create a rule set:

  ```
  Create Rule Set 'Occupancy Expense Allocations'
      in '40 Plan Allocation Process' model,
      with the description 'Occupancy expenses are reassigned from cost centers
      where the expenses were paid to the cost centers that use the facilities'
  ```

* Create a custom rule in that rule set:

  ```
  Create custom rule 'Utilities Expense Adjustment'
      in the model '40 Plan Allocation Process'
      in ruleset 'Occupancy Expense Allocations'
      with description 'Increases utilities expenses by 15%'
      sequence 1
      use ruleset context True
      enable True
  ```

The agent supports creating, listing, enabling/disabling, and copying **rule sets and rules**, and adding or replacing members for multiple rules.

## Task 4: Copy rules and enable/disable rules

* Copy rules from one model into another:

  ```
  In model '10 Actuals Allocation Process' copy
      'Preallocated REV Translation to USD_Reporting'
      'Preallocated COGS Translation to USD_Reporting'
      rules within ruleset(s) 'Preprocessing Currency Translation'
      into model '40 Plan Allocation Process'
      overwriting existing rules
  ```

* Disable a set of rules:

  ```
  In model '40 Plan Allocation Process'
      disable all rules
      under ruleset 'Preprocessing Currency Translation-Alternate'
  ```

## Task 5: Calculate a model and run a trace

* Calculate a model for a POV:

  ```
  Calculate model '10 Actuals Allocation Process'
      povs FY23::Jan::Actual::Working
      run from rule 'Activity Costing Assignments'
  ```

* Run an analytic trace (Sankey diagram). Trace query terms are set up first under **Home** &rarr; **Modeling** &rarr; **AI Configure**, where you create a term and associate it with a trace form:

  ```
  run trace overtime costs pov FY23:Jan:Actual:Working
  ```

  You can focus a trace on a single node, for example `selection customer:Rose Town Bikes`.

  > **Screenshot placeholder:** _PCM Agent trace result rendered as a Sankey diagram._

## Task 6: Going further &ndash; AI Agent Studio (optional)

Beyond the built-in PCM Agent, Oracle Cloud EPM provides **AI Agent Studio** with preconfigured **EPM Assistants** (JSON agent definitions) that you use to assemble your own agents. These agents use GenAI and communicate with Cloud EPM through REST APIs. This is a broader, build-your-own approach; see the documentation below for setup steps.

## Learn More

* [About Profitability and Cost Management (PCM) Agent](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/about_pcm_agent.html)
* [Tutorial: Working with PCM Agent](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/epcm-tutorials-pcm-agent/index.html)
* [EPM Features with AI](https://docs.oracle.com/en/cloud/saas/fusion-ai/aiafl/epm-features-with-ai.html)
* [Generative AI Features Require Cloud EPM 26.04 or Later](https://docs.oracle.com/en/cloud/saas/readiness/epm/2026/epm-jul26/26jul-epm-wn-f50276.htm)

## Acknowledgements

* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, September 2026

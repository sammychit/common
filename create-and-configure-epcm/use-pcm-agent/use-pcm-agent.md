# Optional Lab: Use the PCM Agent

## Introduction

In this optional lab you use the PCM Agent to list artifacts, create a **sandbox** model / rule set / rule *definitions*, validate the model, calculate a POV, and review job status &mdash; all with natural-language commands.

Estimated Lab Time: 20 minutes

### Objectives

Use the PCM Agent to:

* List existing models and rules
* Create a sandbox model, rule set, and rule definitions
* Validate the sandbox model
* Calculate a POV and review the job

### Prerequisites

* You completed **Optional Lab: Enable the PCM Agent**
* An EPCM application is open (Path A, Path B, or BksML50)
* You have a **Draft** POV that is valid for your application

### Ground rules for this lab

* **Use the `WS_` sandbox prefix** for everything you create (`WS_Sandbox Model`, `WS_Sandbox Rule Set`, and so on). This keeps your work separate from existing content.
* **Do not** reuse names that already exist in the BksML50 sample, and do not assume any specific sample model name exists &mdash; run `list models` first and use a name that is not in the list.
* **Do not** run enable/disable, replace-member, clear-POV, or delete commands against existing (non-`WS_`) models, rule sets, or POVs.
* The agent creates **definitions**. A model, rule set, or rule it creates has no source, destination, driver, offset, or formula until you add them in the Designer. It does **not** produce a complete, business-ready allocation on its own.
* Use only commands shown here or in the Oracle command references linked at the end. For every proposed command: **review the parameters, refine if needed, then confirm.**

## Task 1: List existing artifacts

Enter each request, review the response, and confirm if it runs as a job:

```
list models
```

```
list rulesets in model "<a model name from the list above>"
```

```
list rules in ruleset "<a rule set name>" within model "<a model name>"
```

**Success check:** the agent returns a readable list of models (and, for the second and third requests, rule sets and rules). Nothing is changed by a `list` command.

  > **Screenshot placeholder:** _PCM Agent showing the results of `list models`._

## Task 2: Create a sandbox model

```
create model WS_Sandbox Model description Workshop sandbox model
```

Review the proposed command, then confirm. Check **Jobs** (or `list jobs`) for completion.

## Task 3: Create a sandbox rule set

```
for model WS_Sandbox Model create ruleset WS_Sandbox Rule Set description Workshop sandbox rules sequence 10 use model context true enable true
```

## Task 4: Create sandbox rule definitions

Allocation rule definition:

```
create allocation rule WS_Sandbox Allocation in ruleset WS_Sandbox Rule Set description Workshop sandbox allocation definition sequence 10 in model WS_Sandbox Model
```

Custom calculation rule definition:

```
create custom rule WS_Sandbox Custom in ruleset WS_Sandbox Rule Set description Workshop sandbox custom definition sequence 20 in model WS_Sandbox Model
```

Confirm each. Then list them:

```
list rules in ruleset WS_Sandbox Rule Set within model WS_Sandbox Model
```

**Success check:** `list rules` returns exactly the two rules you just created, `WS_Sandbox Allocation` and `WS_Sandbox Custom`, in `WS_Sandbox Rule Set`.

> To make `WS_Sandbox Allocation` actually move data, open **Modeling &rarr; Designer**, select `WS_Sandbox Model` and `WS_Sandbox Rule Set`, open the rule, and complete the **Source/Destination**, **Driver**, and **Offset** tabs. The agent does not choose these for you.

  > **Screenshot placeholder:** _PCM Agent listing the two WS_Sandbox rule definitions._

## Task 5: Validate the sandbox model

```
validate model WS_Sandbox Model
```

Review the validation output. A rule definition with no selections may report warnings or errors until it is completed in the Designer &mdash; that is expected for this sandbox exercise.

## Task 6: Calculate a POV and review the job

Use a Draft POV that is valid in your application (replace the members below):

```
calculate model WS_Sandbox Model for POV FY24::Jan::Actual::Working
```

Then:

```
list jobs
```

```
show job details for job <job id from the list>
```

**Success check:** `calculate model` returns a job id, and `show job details` reports that job as completed (or reports the specific error, which you can act on).

  > **Screenshot placeholder:** _PCM Agent job details for the WS_Sandbox Model calculation._

## Task 7: Clean up (optional)

If you want to remove the sandbox artifacts, delete `WS_Sandbox Model` from **Modeling &rarr; Models**. This removes its rule set and rule definitions with it. Leave all non-`WS_` content untouched.

## Note on analytic trace

Running an analytic trace with the agent requires a trace data form and a query term configured under **Modeling &rarr; AI Configure**. This lab does not set those up, so trace is not covered here. See the *Working with PCM Agent* tutorial if you want to configure and try it.

## Learn More

* [Model Design Commands (Oracle EPCM documentation)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/model_design_commands.html)
* [Calculation and Processing Commands (Oracle EPCM documentation)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/calculation_and_processing_commands.html)

## Acknowledgements

* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, September 2026

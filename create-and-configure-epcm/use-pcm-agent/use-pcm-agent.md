# Optional Lab: Use the PCM Agent

## Introduction

You use the PCM Agent to list items, create a **sandbox** model, rule set, and rule *definitions*, validate the model, calculate a POV, and check the job &ndash; all by typing plain-English commands.

Estimated Lab Time: 20 minutes

### Objectives

Use the PCM Agent to:

* List existing models and rules
* Create a sandbox model, rule set, and rule definitions
* Validate the sandbox model
* Calculate a POV and check the job

### Prerequisites

* You finished **Optional Lab: Enable the PCM Agent**
* An EPCM application is open (Path A, Path B, or BksML50)
* You have a **Draft** POV that is valid for your application

### Ground rules

* **Name everything you create with the `WS_` prefix** (`WS_Sandbox Model`, `WS_Sandbox Rule Set`, and so on). This keeps your work apart from what is already there.
* **Do not reuse a name from the BksML50 sample.** Run `list models` first and pick a name that is not in the list.
* **Do not run** enable/disable, replace-member, clear-POV, or delete commands against anything that is not `WS_`.
* The agent creates **definitions only**. A model, rule set, or rule it makes has no source, destination, driver, offset, or formula until you add them in the Designer. It does not build a working allocation on its own.
* Use only the commands shown here or in the Oracle references at the end. For every proposed command: **read it, adjust if needed, then confirm.**

## Task 1: List existing items

**Why:** to see what is already there and pick safe names.

Type each request, read the reply, and confirm if it runs as a job:

```
list models
```

```
list rulesets in model "<a model name from the list>"
```

```
list rules in ruleset "<a rule set name>" within model "<a model name>"
```

**Check:** the agent returns a readable list. `list` commands change nothing.

## Task 2: Create a sandbox model

```
create model WS_Sandbox Model description Workshop sandbox model
```

Read the proposed command, then confirm. Check **Jobs** (or `list jobs`) for completion.

**Check:** `WS_Sandbox Model` appears in `list models`.

## Task 3: Create a sandbox rule set

```
for model WS_Sandbox Model create ruleset WS_Sandbox Rule Set description Workshop sandbox rules sequence 10 use model context true enable true
```

**Check:** `WS_Sandbox Rule Set` appears in `list rulesets in model "WS_Sandbox Model"`.

## Task 4: Create sandbox rule definitions

Allocation rule:

```
create allocation rule WS_Sandbox Allocation in ruleset WS_Sandbox Rule Set description Workshop sandbox allocation definition sequence 10 in model WS_Sandbox Model
```

Custom calculation rule:

```
create custom rule WS_Sandbox Custom in ruleset WS_Sandbox Rule Set description Workshop sandbox custom definition sequence 20 in model WS_Sandbox Model
```

Confirm each, then list them:

```
list rules in ruleset WS_Sandbox Rule Set within model WS_Sandbox Model
```

**Check:** `list rules` returns exactly `WS_Sandbox Allocation` and `WS_Sandbox Custom`.

> To make `WS_Sandbox Allocation` move data, open **Modeling &rarr; Designer**, select `WS_Sandbox Model` and `WS_Sandbox Rule Set`, open the rule, and fill in the **Source/Destination**, **Driver**, and **Offset** tabs yourself.

## Task 5: Validate the sandbox model

```
validate model WS_Sandbox Model
```

**Check:** validation runs. A rule with no selections may show warnings or errors until you finish it in the Designer &ndash; that is expected here.

## Task 6: Calculate a POV and check the job

Use a Draft POV that is valid in your application (replace the members):

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

**Check:** `calculate model` returns a job id, and `show job details` reports it completed (or shows the exact error).

## Task 7: Clean up (optional)

To remove the sandbox, delete `WS_Sandbox Model` from **Modeling &rarr; Models**. Its rule set and rules go with it. Leave all non-`WS_` content alone.

## Note on analytic trace

An analytic trace through the agent needs a trace data form and a query term set up under **Modeling &rarr; AI Configure**. This lab does not set those up, so trace is not covered. See the *Working with PCM Agent* tutorial to try it.

## Learn More

* [Model Design Commands (Oracle EPCM documentation)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/model_design_commands.html)
* [Calculation and Processing Commands (Oracle EPCM documentation)](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/calculation_and_processing_commands.html)

## Acknowledgements

* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, September 2026

# Create a Custom Calculation Rule

## Introduction

A **custom calculation rule** modifies or creates data in place using a formula, rather than allocating amounts from a source to destinations. Custom calculation rules are typically used for adjustments, statistics, rates, and other derived values that feed later allocation rules.

In this lab you add a custom calculation rule to a rule set, define its target range and formula, and calculate the model.

Estimated Lab Time: -- minutes

### Objectives

In this lab, you will:

* Create a custom calculation rule definition
* Set the target range and result member
* Write a formula using the custom calculation rule formula syntax
* Calculate the model and verify the result

### Prerequisites

Ensure that:

* You have completed *Create a Model and Rule Set* (or are using a rule set in the **BksML50** sample application)
* You have a **Draft** Point of View to calculate

## Task 1: Create the custom calculation rule definition

1. From the Home page, select **Modeling**, then **Designer**.

2. On the **Waterfall Setup** tab, select your **model**, then select the **rule set**.

3. Click the plus (**+**) icon and select **Custom Calculation Rule**.

4. On the **Create Custom Calculation Rule** page, on the **Definition** tab, enter:

  * **Rule Name** &ndash; for example, `Utilities Expense Adjustment`
  * **Description** &ndash; the rule's purpose
  * **Sequence** &ndash; a whole number from 1 to 9999. Rules with the same sequence number run simultaneously when parallel calculation is enabled.

  > **Screenshot placeholder:** _Create Custom Calculation Rule page, Definition tab._

## Task 2: Set the target range

The **target range** defines the Level 0 intersections the rule visits. At each intersection the rule executes the formula and writes the result to the **result member**.

1. On the target range tabs, select the members for each dimension that scope where the rule runs.

2. Identify the **result** (Result dimension) member the formula will write to.

  > **Screenshot placeholder:** _Target range member selections for the custom calculation rule._

## Task 3: Write the formula

Custom calculation rule formulas use the format **`Result := Formula;`** &mdash; the left side (Result) and right side (Formula) are separated by `:=`.

Syntax rules:

* Enclose members in square brackets: `[MemberName]`.
* Enclose tuples in parentheses: `([Member1],[Member2])`.
* The **Result** must be a tuple containing a single **Level 0** member from the Result dimension. Dynamic members, attribute members, and member functions are not allowed on the left side.
* The **Formula** is a simple MDX numeric expression, must include at least one Result dimension member, and must end with a semicolon (`;`).
* Mathematical operations must include a **Rule** dimension member.
* Only basic math and `CASE` statements are supported; other MDX functions are not.
* For performance, use `NONEMPTYTUPLE` on one of the formula operand tuples preceding the formula.

Examples (from the Oracle formula syntax documentation):

```
[STAT1120] := 1;

[STAT1114] := ([STAT1305],[Rule]) * ([STAT1307],[Rule]);
```

Enter your formula, then click **Save** and **Save and Close**.

  > **Screenshot placeholder:** _Formula editor with a valid Result := Formula; expression._

## Task 4: Calculate and verify

1. From the Home page, select **Modeling**, then **Calculation Control**.

2. Select a **Draft** POV.

3. Run the rule set (or the full model), choosing whether to **clear calculated data** first.

4. Check the job in **Jobs**, then open a form or report to confirm the result member now holds the calculated value.

  > **Screenshot placeholder:** _Calculation Control job complete, and a form showing the adjusted value._

## Learn More

* [Creating a Custom Calculation Rule Definition](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/creating_a_custom_rule_definition.html)
* [About Custom Calculation Rule Formula Syntax](https://docs.oracle.com/en/cloud/saas/profit-cost-cloud/pcmad/pcmcs_custom_calculation_rule_formula_syntax.html)
* [Calculating Models](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/calculating_models.html)

## Acknowledgements

* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, September 2026

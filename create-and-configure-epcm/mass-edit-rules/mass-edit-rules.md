# Edit Rules in Bulk with Mass Edit

## Introduction

The **Mass Edit** page in the Designer lets you change many rules at once instead of opening them one by one. From this page you can list and filter rules, add or replace dimension members across multiple rules, and copy, clear, or delete POVs &mdash; each with a review step before execution.

In this lab you filter a set of rules and replace a dimension member across all of them in a single action.

Estimated Lab Time: -- minutes

### Objectives

In this lab, you will:

* Open the **Mass Edit** page and filter rules
* Select multiple rules
* Replace a dimension member across the selected rules
* Review and run the change, and confirm the result

### Prerequisites

Ensure that:

* You have an EPCM application with several rules (the **BksML50** sample application is ideal)
* You understand that **member replacement on the Mass Edit page cannot be undone** &mdash; take a snapshot with Migration first if you need a backup

## Task 1: Open the Mass Edit page and filter rules

1. From the Home page, select **Modeling**, then **Designer**.

2. Select the **Mass Edit** tab.

3. Use the search and filter controls to narrow the list to the rules you want to change (for example, all rules in a model or rule set, or rules that reference a particular member).

  > **Screenshot placeholder:** _Designer – Mass Edit tab showing a filtered list of rules._

## Task 2: Select the target rules

1. Select the check box before each rule you want to modify, or select all rules in the filtered list.

  > **Screenshot placeholder:** _Mass Edit list with several rules selected._

## Task 3: Replace a member across the selected rules

1. Click **Actions**, then select **Replace Member in Rules**.

2. Complete the find-and-replace information:

  | Field | Notes |
  | --- | --- |
  | **Dimension** | The dimension to change. The list includes attribute dimensions and UDA entries (for example, `Product -- UDA`). |
  | **Find Member** | The member to locate. Required. |
  | **Replace With Member(s)** | The replacement member(s). If left empty, the **Find Member** is **removed** rather than replaced. For a destination dimension you can choose **Same as Source**. |
  | **Target Rule Tab** | The rule page on which to make the replacement. For the **Rule** dimension, only the **Driver Basis** tab is available. |
  | **Preserve Filters** | Keeps any filters on the target member when it is replaced. |
  | **Job Comment** | Optional text shown in the Job Library list. |

3. Click **Run**.

  > **Screenshot placeholder:** _Replace Member in Rules dialog with Dimension, Find Member, and Replace With Member(s) set._

  > **Note:** Attribute and UDA members are replaced within the filters defined for each selected rule. This action cannot be undone.

## Task 4: Confirm the change

1. Open **Application** &rarr; **Jobs** and confirm the mass edit job completed.

2. Open one or two of the changed rules in the **Waterfall Setup** tab and verify the member was replaced on the expected tab.

  > **Screenshot placeholder:** _A rule definition showing the replaced member._

## Task 5: Other Mass Edit actions

From the **Mass Edit** tab you can also:

* **Add Member in Rules** &ndash; add a member to the selection on a chosen tab across multiple rules
* Create models, rule sets, and rules
* **Copy**, **Clear**, or **Delete POVs**, with a review of the affected artifacts and data before execution

## Learn More

* [Using the Rule Designer](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/using_the_rule_designer.html)
* [Replacing Members in Rules (Mass Edit Page)](https://docs.oracle.com/en/cloud/saas/profit-cost-cloud/pcmad/pcmcs_replace_members_designer.html)

## Acknowledgements

* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, September 2026

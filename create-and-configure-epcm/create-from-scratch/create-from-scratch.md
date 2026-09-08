# Create an EPCM Application from Scratch

## Introduction

In this lab you create a new, empty Enterprise Profitability and Cost Management application with the **Create Application** wizard, then configure it by creating dimensions, importing metadata, and loading data. This follows the Service Administrator quick-start sequence: create the application, create dimensions, load dimensions into the application, and populate the application with data.

Estimated Lab Time: -- minutes

### Objectives

In this lab, you will:

* Create a new application with the **Start** option and the **Create Application** wizard
* Create and configure dimensions
* Import metadata (dimension members)
* Import data
* Create a Point of View (POV) so models can be calculated

### Prerequisites

Ensure that:

* You have completed the *Enable the Enterprise Profitability and Cost Management Business Process* lab
* You are on the Enterprise Profitability and Cost Management business process landing page, with **no** application yet created
* You have your dimension and data files prepared (or use small sample files provided with this workshop)

> **Note:** An EPM Enterprise environment supports only one application, and you cannot return to the landing page after creating one. If you want to keep the **BksML50** sample for the rule labs, run this lab on a separate environment.

## Task 1: Create the application

1. On the Enterprise Profitability and Cost Management landing page, under **Create a new application**, click **Start**. The **Create Application** wizard opens.

2. Complete the wizard steps:

  | Wizard step | What you enter |
  | --- | --- |
  | **Name and Description** | A unique application name and an optional description. |
  | **Calendar** | The calendar's start and end year, the first month of the fiscal year, and the period frequency (for example, Monthly). |
  | **Currencies** | The main (reporting) currency, and whether the application is multicurrency. |
  | **Review** | Review the application information, then create the application. |

  > **Note:** The **Dimension Mapping** and **Customize** wizard options are disabled and are not applicable for Enterprise Profitability and Cost Management.

  > **Screenshot placeholder:** _Create Application wizard on the Review step, showing name, calendar, and currency selections._

3. When the application has been created, open it from the Home page.

## Task 2: Create and configure dimensions

Enterprise Profitability and Cost Management applications contain business dimensions (such as **Account** and **Entity**), any custom dimensions your model requires, the **POV** dimensions (**Years**, **Period**, **Scenario**, **Version**), and system dimensions (for example, **Rule** and **Balance**), which are created for you.

1. From the Home page, click **Application**, then **Overview**.

2. Select the **Dimensions** tab.

3. Click the drop-down next to **Cube** and select the cube to add the dimension to.

4. Click **Create** and, on the **Create Dimension** page, enter:

  * **Dimension** &ndash; a name that is unique across all dimensions
  * **Description** &ndash; optional
  * **Alias Table** and **Alias** &ndash; optional alternate name
  * **Apply Security** &ndash; select to allow security on the dimension's members
  * **Data Storage** &ndash; **Store**, **Dynamic Calc**, **Never Share**, or **Label Only**
  * **Display Option** &ndash; default display in the Member Selection dialog

5. Under the cube list, select **Enabled** next to each cube that will use the dimension, then click **Done**.

  > **Screenshot placeholder:** _Dimensions tab on the Application Overview page with the Create Dimension panel open._

6. Repeat for each dimension your model needs.

## Task 3: Import metadata (dimension members)

Build out each dimension's member hierarchy by importing metadata.

1. From the Home page, click **Application**, then **Overview**, and select the **Dimensions** tab.

2. Click **Import**.

3. Choose the source (a file in the inbox, or a local file), map the file to the dimension, and run the import as a job.

4. After the job completes, open each dimension in the **Dimensions** tab to verify the member hierarchy.

  > **Screenshot placeholder:** _Import Metadata dialog with a dimension file selected._

## Task 4: Import data

1. From the Home page, click **Application**, then **Overview**, and select the **Data** tab (or use **Application** &rarr; **Data Exchange**).

2. Click **Import**, select your data file, map it, and run the import.

3. Review the job status in **Application** &rarr; **Jobs**.

  > **Screenshot placeholder:** _Import Data dialog and the resulting job in the Jobs console._

## Task 5: Create a Point of View

A Point of View (POV) is a specific combination of **Years**, **Period**, **Scenario**, and **Version** members. You must create a POV before you can calculate models or analyze calculations against that data combination. Only POVs with a status of **Draft** can have calculation control actions performed on them.

1. From the Home page, click **Application**, then **Overview**, and select the **Point of View** tab.

2. Create a POV by selecting one member from each POV dimension (for example, `2024`, `Jan`, `Actual`, `Working`).

3. Confirm the new POV has a status of **Draft**.

  > **Screenshot placeholder:** _Point of View tab with a new Draft POV created._

## Task 6: Next steps

Your application now has dimensions, metadata, data, and at least one POV. Continue with:

* *Create a Model and Rule Set*
* *Create an Allocation Rule*
* *Create a Custom Calculation Rule*

## Learn More

* [Creating a New Application](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/creating_a_new_application.html)
* [Creating a Dimension](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/creating_a_dimension.html)
* [Importing Metadata](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/importing_metadata.html)
* [Importing Data](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/importing_data.html)
* [Understanding Points of View](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/pcmpl/understanding_points_of_view.html)
* [Enterprise Profitability and Cost Management Quick Start Checklists](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/ckepf/epcmcs_service_admin_administer.html)

## Acknowledgements

* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, September 2026

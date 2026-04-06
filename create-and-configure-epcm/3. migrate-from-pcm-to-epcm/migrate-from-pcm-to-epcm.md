# Migrate from PCM to EPCM

## Introduction
This section describes the process of migrating an existing Oracle Profitability and Cost Management (PCM) application to Enterprise Profitability and Cost Management (EPCM). 

Estimated Workshop Time: -- hours -- minutes

### Objectives
In this section, you will learn how to:
* Download the migration template
* Customize the migration template to convert metadata and data
* Upload the customized template to your Profitability and Cost Management inbox
* Validate the migration template and perform the migration

### Prerequisites
Ensure that:
* Have Service Administrator access to the EPM Cloud Service instance with the Profitability and Cost Management application you want to migrate.
* Have Service Administrator access to a second EPM Cloud Service instance with the Enterprise Profitability and Cost Management business process enabled. This instance should not already have an application created.

### Task 1: Download the Migration Template
* Note: Prepare the PCM Application: Review and clean up the PCM application by removing unused members, validating dimensions, and documenting allocation rules and calculation logic.
1. Log in as a Service Administrator to your Profitability and Cost Management instance.
2. On the home screen, click on **Application**, then click on **Migrate to EPCM** and click on **Generate Template**.
3. Save the template to your file system as <YourPCMApplicationName>_Export.xml

### Task 2: Customize the Migration Template
* Open the xml file, and update the following sections
1. <dimensions>: Map source dimensions to target dimensions (used to build the application snapshot) - **Mandatory**

Optionally, update the following fields if applicable. 
2. <epcmappname>: Specify a name for your Enterprise Profitability and Cost Management application - **Optional**
3. <duplicatememberprefixes>: Address the conversion of duplicate member names to unique member names (used to build the application snapshot) - **Optional**
4. <rename_dimension_mapping>: (Optional) Rename dimensions to comply with naming restrictions in Enterprise Profitability and Cost Management or because you want to change the name in the new application.
5. <rename_member_mapping>: (Optional) Rename members to comply with naming restrictions in Enterprise Profitability and Cost Management or because you want to change the name in the new application.
6. <modelpovs>: Convert groups of POV-specific rules into Models (used to build the application snapshot)
7. <datapovs>: (Optional) Convert existing POVs of data to data compatible with your new Enterprise Profitability and Cost Management application (used to create the data extract)

### Task 3: Upload the customized template to your Profitability and Cost Management inbox
1. Log in as a Service Administrator to your Profitability and Cost Management instance.
2. On the home screen, click on **Application**, then click on **Application** in the cluster.
3. In the vertical tabs on the left side, select **File Explorer** which would be the fourth option and click on Upload.
4. Upload the modified template and select folder location as **Inbox** and click on OK.

### Task 4: 
1. On the home screen, click on **Application**, then click on **Migrate to EPCM** in the cluster.

* Note that two files would have been generated. 1) Application Snapshot, 2) Data Extract. The following sections of the migration templates support the mappings required to generate migration files from your current application

### Best Practices


## Learn More
* [Oracle EPCM Admin Guide](https://docs.oracle.com/en/cloud/saas/enterprise-profitability-cost-management-cloud/index.html)

## Acknowledgements
* **Author** - Sameer Chitragar, Senior Associate - Oracle Cloud & Digital, PwC
* **Last Updated By/Date** - Sameer Chitragar, February 2025

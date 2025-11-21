# memo2
ignite25
Overview
Lab535 Archi.png

This lab showcases how Azure Databricks, Microsoft Fabric, Copilot Studio, and Microsoft Foundry work together to deliver a cost-effective, performance-optimized, cloud-native analytics solution pattern. the architecture unifies the enterprise data estate, enabling organizations to accelerate data value creation and unlock actionable insights with Microsoft's latest innovations: Azure Databricks, Microsoft Fabric, Microsoft Foundry, and Copilot Studio.

In today's data-driven world, organizations need solutions that seamlessly integrate analytics and AI to deliver actionable insights at scale. This hands-on lab will guide you through building a modern, cloud-native analytics and AI architecture using Microsoft's latest innovations: Azure Databricks, Microsoft Fabric, Microsoft Foundry, and Copilot Studio. You'll work through a real-world scenario featuring Zava, a global retailer acquiring Litware Inc., which introduces a rich set of curated marketing and sales data. This data is processed in Azure Databricks and stored in the gold layer of ADLS, forming the foundation for advanced analytics and AI-driven decision-making. Throughout the lab, you will:

Set up a Lakehouse architecture with Azure Databricks and orchestrate data pipelines using Lakeflow declarative pipelines.
Transform and enrich data with ETL processes, explore data lineage, and leverage AI-powered column-level insights.
Build AI-driven experiences using Genie and Microsoft Foundry, enabling conversational analytics and business Q&A.
Mirror Unity Catalog tables into Microsoft Fabric's OneLake, create semantic models in Direct Lake mode, and visualize insights in Power BI.
Develop low-code automation with Copilot Studio, creating conversational agents that integrate with Teams and respond to business queries like "What's the top-selling product this week?"
By the end of this immersive session, you'll have implemented a scalable, cost-effective, and performance-optimized solution that demonstrates how AI-powered analytics can reshape business outcomes-from data ingestion to intelligent insights and automation.

Table of Contents
Exercise 1: Lakehouse Setup & Data Orchestration with Azure Databricks and Lakeflow Spark declarative pipelines
Task 1.1: Set Up Azure Databricks Environment and load data into Unity Catalog
Task 1.2: Create Lakeflow Spark Declarative Pipeline for Data Transformation
Task 1.3: Generate column-level insights with AI Suggested Descriptions, then explore data lineage, table update history, and profiling in Azure Databricks
Exercise 2: AI-Driven Insights with Microsoft Foundry & Genie
Task 2.1: Create a Databricks Assistant AI/BI Genie
Task 2.2: Use Agent Created Inside Microsoft Foundry with Custom Web App
Exercise 3: Azure Databricks Mirrored Catalog in Microsoft Fabric
Task 3.1: Mirror Unity Catalog Table into Fabric's OneLake
Task 3.2: Create a semantic model in Direct Lake mode and use Power BI to visualize and generate insights
Exercise 4 [OPTIONAL]: Copilot Studio for Low-Code Automation
Task 4.1: Create an agent and connect Azure Databricks as its knowledge source to support Business Q&A
Task 4.2: Publish the agent in Microsoft Teams channels and make it accessible to users
Note 1: After logging into the VM, if you see the screen below, please click on Opt Out of backup.

Note 2: On the next screen, if you encounter the 'backup is recommended' message shown below, please select Skip for now.

bcp2.png

Open Click By Click in your browser tab for backup link

Exercise 1: Lakehouse Setup & Data Orchestration with Azure Databricks and Lakeflow Spark declarative pipelines
Task 1.1: Set Up Azure Databricks Environment and load data into Unity Catalog
Open a new tab in your browser and sign in to the Azure Databricks Workspace, by clicking on https://portal.azure.com/ and press ENTER.
Enter the following email by clicking on username User1-56880144@LODSPRODMSLEARNMCA.onmicrosoft.com and click on Next.
adb20.png

Enter the Temporary Access Pass by clicking on VZMy5cAe and click on Sign in.
adb21.png

If prompted to stay signed in, select Yes.
adb22.png

In the Azure portal, use the search bar to look for Azure Databricks, then select Azure Databricks from the results.
portal1.png

Click and open adb-fabric-56880144 from the results.
Note: Do not open the adb-fabric-zc0khqp Databricks resource.

portal4.png

Scroll down and click on Launch Workspace.
portal3.png

Note: If you encounter any permission-related issues, please refresh the page 2-3 times. The page should load correctly afterward.

Click on the Continue with Microsoft Entra ID.
adb19.png

On the Databricks workspace page, select the Catalog and click on zava_unity_catalog.
Note: If you are unable to see the catalog on your screen, please reduce your screen resolution or zoom level to 80% or below.

adb1.png

On the right-hand side, click Create Schema.
adb2.png

Enter schema56880144 in Schema name field and click on Create.
ex1t1i4.png

After creating the schema, search for the schema (schema56880144) you just created and select it.
Note: There will be schemas created by other attendees in the lab, so make sure to search for and select your schema accordingly.

adb63.png

Click the Create button and choose Volume to create a new volume.
adb64.png

Enter a volume name as fraud_raw_data, select zava_unity_catalog, and choose schema56880144 (if it's not selected by default). Then click Create.
vol1.png

On the newly created volume, click Upload to this Volume to upload the required files.
Task-2.3_1.png

In the Upload Files to Volume window, select the Browse option.
Task-2.3_1.png

Navigate to the C:\Users\LabUser\Desktop\volume, select all the files and then click Open.
adb4.png

Note: If you're not able to find the volume folder, please download the ZIP file by opening this URL in a new tab and then extract it: https://stignite25.blob.core.windows.net/zip/volume.zip

Choose Upload to complete the process.
adb5.png

Note: Wait for the upload to complete before proceeding to the next step.

From the left navigation, select Workspace, expand Shared, choose Analytics with ADB folder, and open 01.1-DLT-fraud-detection-SQL.
adb6.png

Note: If you are not able to see content in the notebook, please download the notebook by opening this url in a new tab and import the notebook to your workspace: https://stignite25.blob.core.windows.net/notebook/01.1-DLT-fraud-detection-SQL.ipynb

Press Ctrl + F to open the search bar, ensure its the notebook's search bar, then click the down arrow to the left of the search box to expand the Replace options. Type #schemaName# in the first field, enter schema56880144 in the second field, and then click Replace All to update all occurrences in the notebook.
adb7.png

Note: You may see a compressed view in case of a smaller window resolution. Please split the instructions screen or zoom out to view all menus correctly

Task 1.2: Create Lakeflow Spark Declarative pipeline for Data Transformation
From the left navigation pane, select Jobs & Pipelines, then choose ETL Pipeline.
adb8.png

From the dropdown list, select zava_unity_catalog.
Task-2.3_1.png

From the Schema dropdown list, search and select schema56880144 schema which you have created in the previous steps.
Note: If you encounter the error "Couldn't load schemas", click the Try again button, this will reload and display the schemas.

adb9.png

On the New Pipeline page, select Add Existing Assets.
Task-2.3_1.png

In the Pipeline root folder, click on notebook icon.
adb10.png

Choose the Analytics with ADB folder and click Select.
adb11.png

In the Source Code Path, select the 01.1-DLT-fraud-detection-SQL notebook from the Analytics with ADB folder, and then click Select.
Task-2.3_1.png

After adding the pipeline root folder and source code path, review the details and click Add.
Task-2.3_1.png

After adding, click Run Pipeline from the top-right corner to execute the pipeline.
Task-2.3_1.png

Note: Wait for the pipeline to complete. A pop-up will confirm that the pipeline executed successfully, and the graph will appear afterward.

adb12.png

Task 1.3: Generate column-level insights with AI Suggested Descriptions, then explore data lineage, table update history, and profiling in Azure Databricks.
Click on Catalog and search for the schema schema56880144 select it.
Note: There will be schemas created by other attendees in the lab, so make sure to search for and select your schema accordingly.

adb66.png

Note: If you're unable to find the schema56880144, first select the zava_unity_catalog, and then search for schema56880144.

Refresh the page if you don't see the tables.

Expand Tables and click on the bronze_transactions table.
adb67.png

On the right-hand side, scroll down and click AI generate.
adb14.png

Note: If a pop-up appears with the message "Saving comments in bulk could be slow", click Continue.

adb69.png

Review the AI-generated comments for the columns, then click Save all.

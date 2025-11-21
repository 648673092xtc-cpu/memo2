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

Exercise 2: AI-Driven Insights with Microsoft Foundry & Genie
Task 2.1: Create a Databricks Assistant AI/BI Genie
In this task, we will create Genie workspace in Databricks.

In the left menu bar, click on Genie.
databricks

Click on + New.
databricks

Search for schema56880144 schema in the search bar.

Select gold_transactions table.

Click on Create.

adb16.png

Click on New Space in the top left to edit the name and replace it with Zava_Genie and press enter.
databricks

Paste the following question in chat box and click on send.
what is the percentage of fraudulent transactions in my dataset?

Gini.png

Observe the response from Genie, then click Show code to view the code Genie used to formulate the answer.
Note: The responses from Genie may not match the ones in the screenshot but will provide a similar response.

Gini1.png

Task 2.2: Use Agent Created Inside Microsoft Foundry with Custom Web App
In this Task, You'll use the AI agent within a custom web application to deliver interactive, data-powered intelligence.

In a new tab of your VM browser enter the URL https://app-aifoundry-genieintegration.azurewebsites.net/#/landing-page and press Enter key.
Note: If a permissions request pop-up appears, click the Accept button.

AIFoundry1.png

Select the terms and conditions checkbox, then click Login.
Webapp Login.png

Click on the robot icon located at the bottom-right corner of the page.


Click on the first pre-populated question.


Observe the response.


Click on the second pre-populated question and observe the response.

Exercise 3: Azure Databricks Mirrored Catalog in Microsoft Fabric
Task 3.1: Mirror Unity Catalog Table into Fabric's OneLake
Mirroring the Azure Databricks Catalog structure in Fabric allows seamless access to the underlying catalog data through shortcuts. This means that any changes made to the data are instantly reflected in Fabric, without the need for data movement or replication. Let's step into Data Engineer's shoes to create a Mirrored Azure Databricks Catalog.

In a new tab of your VM browser enter the URL https://app.fabric.microsoft.com and press Enter key.
Note: Close any pop-up that appears on the screen throughout the lab.

adb49.png

From the left navigation pane, click on Workspaces and then the + New workspace button.
adb33.png

Type the name fabric56880144 validate the available name and click Apply.
adb34.png

Note: Close any pop-up that appears on the screen.

adb50.png

Select New item from menu bar.
adb36.png

In the New item window, search Mirrored Azure Databricks catalog and select it.
adb51.png

When the New source window pops up, click on the Create new connection and select Service principal from Authentication kind dropdown box, and enter the following details.
ADBC1.png

Enter the following details for the Service principal authentication.
In the URL field enter https://adb-3218079371877032.12.azuredatabricks.net

Tenant ID: f94768c8-8714-4abe-8e2d-37a64b18216a

Service principal client ID: 95121828-71fb-4854-a9e6-cb7294eff8a2

Service principal Key: BBk8Q~mXd82ufaAgW9jHB6CFSZYyueYTd0WqSdzC

click on the Connect button.
Task-2.3_7.png

Note: Close any pop-up that appears on the screen.

Click on Next button.
Task-2.3_7.1.png

In the Choose data screen, select the Catalog name as zava_unity_catalog from the dropdown box, and select the fraud-detection schema if not selected, scroll down then select the checkbox Automatically sync future catalog changes for the selected schema (to mirror future tables) if not ticked and click on Next button.
Task-2.3_8.png

Click on the Create button.
adb54.png

Note: Wait for the notification confirming that the mirroring is complete (as shown in the "Shortcuts created" message).

adb52.png

Click on the Monitor catalog button to track the mirroring status and then close it.
Task-2.3_10.1.png

Click on the View SQL endpoint button. You can also select the tables to preview data.
Task-2.3_10.png

Task 3.2: Create a semantic model in Direct Lake mode and use Power BI to visualize and generate insights
Click on New semantic model.


Paste the semantic model name as fraud_detection, search gold_transactions, select it and then click on Confirm.
adb60.png

Wait for the semantic model to be created, then select the workspace from the left menu.
adb55.png

Hover over the Semantic Model and click the Refresh icon.
refresh.png

Note: Wait for the semantic model to refresh.

Click on the Ellipses (3 dots) next to fraud_detection Semantic Model to load the dropdown menu. Select Create report from the dropdown.


Click on the Copilot button and click on Get started.
adb57.png

Paste the following question into the Copilot chat and on send.
What's in my data?

PowerBICopilot.png

Paste the following question into the Copilot chat and on send.
Create a report to analyse in detail only fraudulent transactions.

Note: Wait for the report to load.

semantic6.png

Look at the response.
Note: The responses from Copilot may not match the ones in the screenshot.

adb59.png

Paste the following question into the Copilot chat and take a look at the response.
Based on the data of this report, what can be done to reduce the fraudulent transactions, and should I focus on.

adb68.png

Exercise 4 [OPTIONAL]: Copilot Studio for Low-Code Automation
Task 4.1: Create an agent and connect Azure Databricks as its knowledge source to support Business Q&A.
In a new tab of your VM browser enter the URL https://copilotstudio.microsoft.com/ and press Enter key.

On the welcome screen for Microsoft Copilot Studio, Click on the Get Started button to proceed.

adb37.png

Select Agents from the left menu, and click + New agent.
Note: Wait for page to load and refresh the page

cs8.png

Note: Close any pop-up that appears on the screen.

adb38.png

Click on Configure, enter the agent name as Databricks Agent and add the description Responds to queries using data from your Databricks workspace.
config.png

On the right menu, click Create.
adb40.png

Note: Wait for the agent to load.

On the knowledge page, click + Add knowledge to include a knowledge source.
adb41.png

On the Add knowledge page, click Advanced, then select Azure Databricks.
Note: Ensure that you select Azure Databricks only, as Databricks is also available as a separate connection option.

adb62.png

On the Select Azure Databricks connection pane, click on Not connected dropdown and select Create new connection.
adb42.png

Navigate back to your Databricks workspace, click SQL Warehouses from the left menu, select SQL Warehouses at the top, and then click Serverless Starter Warehouse.


On the Serverless Starter Warehouse page, click on start button, then click Connection Details, and copy the Server Hostname and HTTP Path.


In Copilot Studio, on the Azure Databricks Connection page, paste the Server Hostname and HTTP Path you copied earlier and click on Create.


In the pop-up window, select your account and click Sign in.


Select zava_unity_catalog and click Select.


Search for schema56880144 schema, select the gold_transactions tables within it, and click Add to Agent.


Note: Wait for the agent to load.

Paste the following question to Test your agent.
What is the average transaction amount for fraudulent vs non-fraudulent transactions?

cs5.png

Click on Allow.
cs6.png

Look at the Response.
cs7.png

Note: The agent may not respond initially after adding a new data source. Re-enter the question or start a + New test session to get a response.

Task 4.2: Publish the agent in Microsoft Teams channels and make it accessible to users.
Click on +7 at the top, then select Channels from the dropdown menu to view channel options.
adb43.png

Note: The number displayed (such as +7) may vary depending on your screen's resolution or window size, as it indicates the count of additional menu options not visible in the main navigation bar.

The Microsoft Teams channel should appear in the list, for this lab the agent has already been published and added to Teams.
adb44.png

In a new tab of your VM browser enter the URL https://click-by-click.azurewebsites.net/#preview/mhw2w6exgz21zno97ch and press Enter key.
Follow click by click url, then navigate to Microsoft Teams to see the agent in action.
C2CTeams.png

Congratulations! As Data Engineers and Data Analysts, you have empowered Zava to transform its disparate data sources into actionable insights-driving growth, enhancing customer satisfaction, and securing a competitive edge.

Feedback
Your feedback is very useful to us and helps us improve our labs for future events. Please click on the link below for a short survey.

LAB 535 Feedback

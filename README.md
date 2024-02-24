# AZURE_DataFactory_and_AZURE_SYNAPSE_END_TO_END_project:

## Overview
This project is a comprehensive end-to-end data pipeline solution utilizing various Azure services for data ingestion, transformation, loading, and reporting. It aims to demonstrate the integration of on-premise SQL Server data with cloud-based analytics and reporting tools.

## Technology Stack
SQL Server: On-premise database managed using Microsoft SQL Server Management Studio.
JAVA JRE: Required for specific data processing tasks.
Microsoft Integration Runtime Configuration Manager: Used for connecting on-premise resources to Azure.
Azure Account Portal: Utilized for account management and resource creation.
Azure Data Factory: Orchestration tool for data movement and transformation.
Azure Databricks: Apache Spark-based analytics platform for data processing.
Azure Synapse: Unified analytics platform for big data and data warehouse solutions.
Storage Account: Azure Storage for storing various data sets.
Serverless Azure SQL Server: Serverless database for data storage and querying.
Languages: Python, PySpark, SQL for scripting and data manipulation.
Reporting Tool: Power BI for data visualization and reporting.
Key Vault: Secure storage for sensitive information.
Azure Active Directory: Used for managing access and authentication.


## Project Agenda
Part 1: Environment Setup
Login to Azure Portal

Create a resource group with:
Azure Databricks Workspace
Storage Account
Azure Data Factory
Azure Synapse Workspace
Azure Key Vaults for secure data storage

Part 2: Data Ingestion
Azure Integration Runtime Setup

Configure Azure Data Factory Integration Runtime for on-premise database connectivity.

Data Copy Operations

Copy tables from on-premise SQL Server to Azure Data Lake Storage Gen2 as Bronze layer.
Iterate over tables using ForEach loop in Data Factory pipeline.

Part 3: Data Transformation
Azure Databricks Data Processing

Create clusters for PySpark-based data transformation.
Transform data from Bronze to Silver layer, applying schema changes and data formatting.

Silver to Gold Transformation

Further refine data in Azure Databricks, e.g., renaming columns, aggregations, etc.

Part 4: Data Loading
Serverless SQL Database Creation in Azure Synapse

Set up serverless SQL database for storing transformed data.

View Creation for Gold Layer Tables

Use Azure Data Factory pipeline to create views in the serverless SQL database.

Part 5: Data Reporting
Power BI Integration
Connect Power BI to Azure Synapse SQL Database for reporting.
Create reports and dashboards for data visualization.

# PART 1 :

     --STEP 1 : LOGIN TO AZURE PORTAL
             1.create a resource group first :
                      --- 1.create workspace for azure databricks.
                      --- 2.create storageaccount 
                      --- 3.create azure datafactory
                      --- 4.create azure synapse workspace
                      --- 5.create a azure key vaults(store the sensitive data)
                      snapshots
                      1.databricks workspace :
                     ![databricks_work_space](https://github.com/AdityaDevadiga/AZURE_DataFactory_and_AZURE_SYNAPSE_END_TO_END_project/assets/72966036/021ce12d-0812-47af-853e-157b73f32a56)

                      

                      2.create storage account:
                      ![storage_account](https://github.com/AdityaDevadiga/AZURE_DataFactory_and_AZURE_SYNAPSE_END_TO_END_project/assets/72966036/70f804bb-08fe-4ccb-a8f9-3e26e4b24249)
                      
                      3.create azure data factory:
                      ![Uploading AZURE DATA FACTORY.png…]()

                      4.Azure synapse worksapce:
                      ![SYNAPSE](https://github.com/AdityaDevadiga/AZURE_DataFactory_and_AZURE_SYNAPSE_END_TO_END_project/assets/72966036/8c22ec32-edaf-43ea-aa10-59f3533e8bf3)

                      5.AZURE KEY VAULTS:
                      ![AZURE KEY VAULTS](https://github.com/AdityaDevadiga/AZURE_DataFactory_and_AZURE_SYNAPSE_END_TO_END_project/assets/72966036/dc81feae-4a4e-44d4-b620-c618ebb412a8)

                      6.SQL SERVER:
                         ![SQL SERVER](https://github.com/AdityaDevadiga/AZURE_DataFactory_and_AZURE_SYNAPSE_END_TO_END_project/assets/72966036/f3769ada-c817-4c74-a5df-ea617f5b2b5d)

## PART 2: INGESTION SNAPSHOTS AND STEPS:
           ---
                      1.To connect the onpremise database server through azure we want azure integration runtime we need to install that ,go to azure datafactory ---> manage-->integration runtime
                      ![INTEGRATION RUNTIME](https://github.com/AdityaDevadiga/AZURE_DataFactory_and_AZURE_SYNAPSE_END_TO_END_project/assets/72966036/15decdb7-adb7-460d-adae-de49d41f3491)

                      2.setup:![INTEGRATION RUNTIME SETUP](https://github.com/AdityaDevadiga/AZURE_DataFactory_and_AZURE_SYNAPSE_END_TO_END_project/assets/72966036/5f347fed-0440-4d85-99e6-259801a81d2b)

                      3.links to pick up the integration runtime :
                      ![LINKS FOR INTEGRATION RUNTIME](https://github.com/AdityaDevadiga/AZURE_DataFactory_and_AZURE_SYNAPSE_END_TO_END_project/assets/72966036/7070b70d-3443-4c79-a848-5c65e4e7706c)

                      4.copy only address table :

                      ---here we need to select the copy data field and select source as per our requirements in my case choosen sql server database 
                        ![choosing the database for copy data](https://github.com/AdityaDevadiga/AZURE_DataFactory_and_AZURE_SYNAPSE_END_TO_END_project/assets/72966036/ae1e25dc-8d98-4a2d-bed1-fe922db43fed)

                        ---- After that need to give the linked service using the integration runtime sql server credentials
                        ![sql_server_linked_service](https://github.com/AdityaDevadiga/AZURE_DataFactory_and_AZURE_SYNAPSE_END_TO_END_project/assets/72966036/e97a118e-5adf-43ef-b309-06682eaa8235)


                        ----Need to enable the access policies for data factory to acces key vaults values below are snapshots:

                        ![access_policies_for_azure_datafactory_to_keyvaults](https://github.com/AdityaDevadiga/AZURE_DataFactory_and_AZURE_SYNAPSE_END_TO_END_project/assets/72966036/18c0c475-a94e-4f4d-a687-408e6e7540f3)

                   ----------after that sink the data to azurestoragegen2 to data lake below are the snap :

                   ![sink the data from local sql server to azure data storage gen2](https://github.com/AdityaDevadiga/AZURE_DataFactory_and_AZURE_SYNAPSE_END_TO_END_project/assets/72966036/f8e32ee0-71b5-457d-9261-ed377cac5d9b)

                   after that copy the all the table present in the onpremise to azure datastorageaccount gen2 as bronze layer
                   script used for the ![script for all the tables need to sink to the bronze laye in the datalakestorage gen2](https://github.com/AdityaDevadiga/AZURE_DataFactory_and_AZURE_SYNAPSE_END_TO_END_project/assets/72966036/b0b2273a-c64d-4ca8-9ccf-9ece88c8c374)


------after that by using the foreach field in data factory need to add the all copy data field inside that because terate over the all the table in the database and need to store it in a datalakegen2 as per the table name 
![for_each field_will_takeof the all the ctables needs to sink to datalake storage as per the directory and tablename](https://github.com/AdityaDevadiga/AZURE_DataFactory_and_AZURE_SYNAPSE_END_TO_END_project/assets/72966036/1c9f3e62-2498-4719-8736-6881dcade26a)


FINALLY DATA INGESTION HAS BEEN DONE TO THE BROZE LAYER WHICH IS PRESENT IN THE DATALAKESTORAGE GEN2 in azure storage account for the bronze layer


# DATA TRANSFORMATION :
   --- Data tranformation i have done in azure databricks by taking the help of the pyspark;;;

   ---First i have created the cluster through enable the credentials passthorugh method so that azure synapse can be access for the paricular user 

   ----and i have created the layer like bronze ,silver and gold and by using the dbfs mount command i have mounted the all the layer .


   ----after that i have tranfer the first transformation like changing the data format below are the code you can go through
   ![for_each field_will_takeof the all the ctables needs to sink to datalake storage as per the directory and tablename](https://github.com/AdityaDevadiga/AZURE_DataFactory_and_AZURE_SYNAPSE_END_TO_END_project/assets/72966036/49e4bc4e-1bf4-4a2a-b6dd-fa8cd7c10b78)

   ---after that silver to gold i have added the another transformation like adrresiD should come as Address_ID for athe table
   ![databricks_silver_to_gold](https://github.com/AdityaDevadiga/AZURE_DataFactory_and_AZURE_SYNAPSE_END_TO_END_project/assets/72966036/15fa5d2f-7e65-4753-b6fd-3754c1bddd61)




  -----after that need to connect to the data factory so we nee d to link the databricks to datafactory using the linked services which is prsent the manage bar..
  
  ![linked to azure databrics for creating azure notebook pipeline](https://github.com/AdityaDevadiga/AZURE_DataFactory_and_AZURE_SYNAPSE_END_TO_END_project/assets/72966036/b5ad2631-13b2-4596-92e8-87e28095bc34)

  finally we created the pipeline with the azure databricks notebook which is help for the adding the transformatiom from bronze layer data to silver and adding the transformation to gold now we are ready for loading the data to AZURE SYNAPSE

  ### DATA LOADING:

  Create the SERVERLESS SQL DATABASE :

  ![Creating the serverless sql database in azure synapse](https://github.com/AdityaDevadiga/AZURE_DataFactory_and_AZURE_SYNAPSE_END_TO_END_project/assets/72966036/7a183bcf-c26b-4b96-bf8a-045faf991e6c)

  after that i have creating the view for the table which is present the gold_db database by using the pipeline through adding the stored procedure as per the table name 
  ![Uploading this is the pipeline for the creati g the view for the all the table needs to store it serverless db in azure synapse.png…]()


---below are the script ypu can create the views for the all the table

![image](https://github.com/AdityaDevadiga/AZURE_DataFactory_and_AZURE_SYNAPSE_END_TO_END_project/assets/72966036/f318db9a-d515-48f0-84c6-8b5a895e2c2e)

# NOW LOADING THE DATA TO SERVERLESS SQL DATABASE IN AZURE SYNAPSE ANALYTICS

### REPORTING :

Finally we are in the stage of the reporting the data throght the POWER BI
---connecting the azure SYNAPSE SQL TO DATA BASE THROUGH USING serverless endpoint url which is present in the properitries field and need to provide the password 


--- after the need to load the all the table to power bi 

--- before adding the rows to the customer table customer count value is : 849 once we ran the pipe line;

----after that addig the two rows to database which is present in the onpremise database now when we are ran the pipeline our pupeline will handle the two insert data we can seeing it report as customer count is 849


snapshots :  
connection to azure synapse : ![snapshots connecting the powerbi to serverless sqll database which is present in the synapse analytics](https://github.com/AdityaDevadiga/AZURE_DataFactory_and_AZURE_SYNAPSE_END_TO_END_project/assets/72966036/6d19eefc-4ec5-4f63-b8f0-8868d2f48ef3)

report after inserting the two record to customer table snapshot: ![report after adding the two rows to customer table when we ran the pipeline](https://github.com/AdityaDevadiga/AZURE_DataFactory_and_AZURE_SYNAPSE_END_TO_END_project/assets/72966036/6be02b9f-63d6-4883-8841-a12d2f6cb70f)


## Conclusion
This project showcases a complete data pipeline solution, leveraging Azure services for seamless integration between on-premise and cloud-based data systems. From data ingestion, transformation, loading, to reporting, it demonstrates the power of Azure's analytics capabilities in a real-world scenario.


  

  
  



                      




                      


                      

                     

                      

                      








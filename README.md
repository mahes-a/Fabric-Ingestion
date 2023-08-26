# Different ways to Ingest Data into Fabric
This tutorial guides you through all the options to inegst data in Microsoft Fabric

## Requirements
Complete these tasks before you begin this tutorial:

- Access to Fabric Workspace.  You can enable free trial [here](https://learn.microsoft.com/en-us/fabric/get-started/fabric-trial).
  
- Create an Azure Data Lake Storage Gen2 storage account. See [Create Storage Account](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-create?tabs=azure-portal)
  
- Bing Searh Resource, Refer [here](https://learn.microsoft.com/en-us/bing/search-apis/bing-web-search/create-bing-search-service-resource) to create a bing serach resource


## Create a Lakehouse
- Browse to your Fabric enabled workspace in Power Bi and switch to Data Engineering persona
      
   <img width="71" alt="image" src="https://github.com/mahes-a/2023/assets/120069348/2151ab70-9876-48d7-83b9-42a15490021c">
      
- Click on New Lakehouse and name your lakehouse 
      <img width="713" alt="image" src="https://github.com/mahes-a/2023/assets/120069348/dc56548d-f030-4200-b150-8b313ea920d9">
      
      <img width="254" alt="image" src="https://github.com/mahes-a/2023/assets/120069348/ab4a450d-320a-4de1-9f11-f819dea4c2e8">

## Using a Dataflow Gen2 to Ingest data

- Navigate to the Lakehouse created from your workspace and click "Get Data"-> "New Dataflow Gen2"

   <img width="331" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/ef936516-2636-4965-9366-79438cb47783">
   
   <img width="560" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/f6507cc1-21a1-4a21-b6d3-fc41ae37a1fb">

- Name the dataflow and choose the appropriate sensitivity label and click on "Import From Excel"

  <img width="959" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/f2a8fb4f-f6fa-4b99-abbd-892d0aea8b07">

  

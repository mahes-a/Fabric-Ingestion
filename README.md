# Different ways to Ingest Data into Fabric
This tutorial guides you through all the options to inegst data in Microsoft Fabric

## Requirements
Complete these tasks before you begin this tutorial:

- Access to Fabric Workspace.  You can enable free trial [here](https://learn.microsoft.com/en-us/fabric/get-started/fabric-trial).
  
- Create an Azure Data Lake Storage Gen2 storage account. See [Create Storage Account](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-create?tabs=azure-portal)
  
- Bing Searh Resource, Refer [here](https://learn.microsoft.com/en-us/bing/search-apis/bing-web-search/create-bing-search-service-resource) to create a bing serach resource

- Microsoft OneLake file explorer for Windows , Installation instructions are [here](https://learn.microsoft.com/en-us/fabric/onelake/onelake-file-explorer#installation-instructions)
  
## Create a Lakehouse
- Browse to your Fabric enabled workspace in Power Bi and switch to Data Engineering persona
      
   <img width="71" alt="image" src="https://github.com/mahes-a/2023/assets/120069348/2151ab70-9876-48d7-83b9-42a15490021c">
      
- Click on New Lakehouse and name your lakehouse 

  <img width="713" alt="image" src="https://github.com/mahes-a/2023/assets/120069348/dc56548d-f030-4200-b150-8b313ea920d9">
      
  <img width="254" alt="image" src="https://github.com/mahes-a/2023/assets/120069348/ab4a450d-320a-4de1-9f11-f819dea4c2e8">

## Approach 1: Using Dataflow Gen2 to Ingest data

- Navigate to the Lakehouse created from your workspace and click "Get Data"-> "New Dataflow Gen2"

   <img width="331" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/ef936516-2636-4965-9366-79438cb47783">
   
   <img width="560" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/f6507cc1-21a1-4a21-b6d3-fc41ae37a1fb">

- Name the dataflow and choose the appropriate sensitivity label and click on "Import From Excel"

  <img width="959" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/f2a8fb4f-f6fa-4b99-abbd-892d0aea8b07">

- Copy the raw url for the "CAWATXCOVID19.xlsx" file from the repo and input the url in the "File Path or URL" section and click Next . This dataset is based on an open dataset called ["Covid Tracking Project"](https://covidtracking.com/data/download) . Sample URL will be https://raw.githubusercontent.com/mahes-a/Fabric-Ingestion/main/CAWATXCOVID19.xlsx
  
  <img width="1044" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/10bab88c-c34a-4ca9-a3fd-9662c5ba9619">
  
- The Excel sheet has 3 tabs and select all 3 tabs and click create
  
  <img width="1044" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/0eb3f0e8-028c-4a01-9d5c-12e59b16c496">

- In the "CA" tab choose the Lakehouse settings from bottom right and selct the lakehouse and name the table name as "Covid_Combined_Data"
  
  <img width="1134" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/a179996b-70a7-4294-842c-be8787bf95f8">

  <img width="1030" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/c8aef0ac-35bc-4074-89c9-848bcc644d73">


- Select Append mode and save settings and Repeat the same steps for TX and WA tabs , We will append all the 3 tab data into "Covid_Combined_Data" table in the lakehouse , If there are any column mappings with type "Any" change the column type to Text

    
     <img width="1045" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/bf624b81-3647-48f9-b5f9-2dcfbd51339b">

     <img width="1032" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/ea0bb322-719f-4b48-b51b-b11a3b95483b">



- Click on Publish on bottom right in dataflow and wait for publish and refresh to complete in the workspace tab , After refresh click on refresh history to find the details of the refresh

  <img width="1121" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/be091937-4965-437e-8120-02a22e34ea62">

  <img width="955" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/d2d86883-c4c5-4a4f-ad69-ae4c8fcdad3b">

- Open the Lakehouse to verify the table and data

   <img width="839" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/bc9513bc-0dcf-4f23-9740-15f4236774d8">


## Approach 2: Using OneLake File Explorer to Sync files

- Sign in into the OneLake File Explorer with the same account you used to create the lakehouse
  
- Browse to the Lakehouse folder and the files folder

  <img width="1067" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/4f8f954e-d8d1-4872-89fa-154e6412c4d4">

- Copy the files into the OneLake File Explorer 

  <img width="1070" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/23405711-243a-4806-b404-12701da615c6">

- Navigate to the Lakehouse in [Fabric Portal](https://app.powerbi.com) and confirm the files are available in the Files section


  <img width="1132" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/58b330c6-6118-404a-9b6d-8809db546809">

- If unavailable click on Files and use Refresh option

  <img width="1110" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/eee657be-42ab-4408-bcd5-3ad2025add24">




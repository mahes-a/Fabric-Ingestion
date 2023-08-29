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

 ## Approach 1: Using upload to ingest data 

- Navigate to the Lakehouse created from your workspace and click "Get Data"-> "Upload"


  <img width="1142" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/61777f24-a10c-4b37-8a5f-eccf305576c6">

- Upload the all-states-hsitory.csv file from local system

  <img width="335" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/e95a32f3-5668-4413-b5de-96335f4b8f65">

- Uploaded CSV files are avilable in the Lakehouse files section 


## Approach 2: Using Data Pipelines to ingest Data 

- Navigate to the Lakehouse created from your workspace and click "Get Data"-> "New Data pipeline" , Name the pipeline and click create 

   <img width="331" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/ef936516-2636-4965-9366-79438cb47783">

   <img width="895" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/99a96d19-81ed-4398-bcd4-a85e09b0fd83">

 - Close the Copy Activity Wizard and add a Copy Activity

   <img width="966" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/514ef55b-85b4-4981-bf49-d67d9ada639e">

   <img width="664" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/f04c6ce3-b167-480b-8ade-e0b6f89cb79d">

 - In the Source section of copy activity add
     - Choose the bing connection created in previous step
     - Choose REST as connection  type
     - Choose Relative path as ?q=weatherinla&mkt=en-us&count=15 , the query to bing is provided following "q=" , here "weatherinla" is the bing search query

   <img width="589" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/edf61f71-b694-4129-ba3f-a76eb922d93a">

- From your Azure Portal Bing Search resource in Azure Keys and Endpoints section , copy the keys

  <img width="947" alt="image" src="https://github.com/mahes-a/StagingBuild/assets/120069348/be07fc54-3099-42db-8792-74d5da16a8c1">

- Click on Additional headers , click New and enter Name as "Ocp-Apim-Subscription-Key" and value as the Key copied

   <img width="620" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/a90d5d0b-d3a7-49e6-acbf-1f5ff2c49391">

- In the Destination Section
   - Choose the Lakehouse
   - Choose Files
   - Enter the folder path
   - Enter Json as the File Format

   <img width="934" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/d1067beb-ec3b-4729-b353-1a5cfae8cb0d">

- Click Run the pipeline and select Save and Run and wait for completion
    <img width="1132" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/fce89e4c-7fe5-424e-8874-4b7b803b4a61">

- Switch back to the destination Folder path selected in Lakehouse explorer and confirm the file creation

   <img width="866" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/e03950f6-8cb5-4306-ae56-c6449a0d09d8">


## Approach 3: Using Dataflow Gen2 to Ingest data

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

## Approach 4: Using Shortcuts to reference data without copying it

- Download the all-states-hsitory.csv from the repo to local system

- Open the Azure Data Lake Storage Gen2 storage account and create a container with any name\
  
- Open the container and upload the all-states-hsitory.csv file from local system

   <img width="1001" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/1d45e090-11ac-4fb2-a6e2-f2100bf3e86c">

   <img width="1011" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/debc478b-c306-41f4-a4a4-1987c50dc58e">
  
- Navigate to the Lakehouse created from your workspace and right click on files and "New Shortcut" option

   <img width="317" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/27d06d14-9fd9-4c3e-9eb3-3e2bfcb2e908">

- In the shortcut wizard choose the Azure Data Lake Storage Gen 2
  
  - In the URL section enter the url for the container , the url format would be https://<<storageaccountname>>.dfs.core.windows.net/<<containername>>
  - Add a name for your connection
  - Authentication choose Account Key method and copy the account key from Storage account , Refer [here](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal#view-account-access-keys) to get the account key

  
  <img width="964" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/56ae84d7-8bae-4d09-85d0-80c9ddff6359">
  

  <img width="905" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/0f133282-4cec-4e99-9230-35edab429ff9">



  <img width="956" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/0ccb9302-49bc-4947-9ee9-c582b6d5abb5">

- In the next step enter shortcut name and click create , If unavailable click on Files and use Refresh option
  
  <img width="929" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/ede88c4d-3b46-4577-bac6-59471c4872e5">


- The lakehouse automatically refreshes. The shortcut appears under Files in the Explorer pane.

  <img width="737" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/cb70cc3b-7cd7-433a-800e-6d418859e8a9">



## Approach 5: Using Notebooks to ingest Data 

- Navigate to the Lakehouse created from your workspace and click "Open notebook"-> "New notebook"
    
  <img width="716" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/f0bad0f8-eaff-4930-9b3a-8390c9098d28">

- In the First cell add below content  and execute to make REST calls to the bing search , Use the bing search key copied from Azure portal

                import json
                import os
                import requests
                
                #make REST Api call to bing search 
                search_url='https://api.bing.microsoft.com/v7.0/search'
                subscription_key='your key here'
                mkt = 'en-US'
                query='current weather in LA'
                params = { 'q': query, 'mkt': mkt ,"count":50, "answerCount":10 ,"textDecorations": True, "textFormat": "HTML","responseFilter":"webpages" }
                headers = { 'Ocp-Apim-Subscription-Key': subscription_key }

- Add a code cell and copy the below content and and execute to process the bing search results to a dataframe
  <img width="626" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/cdf97066-53aa-4f97-823d-9d409c39d254">
  
              #curate the response fron bing search to dataframe
              response = requests.get(search_url, headers=headers, params=params)
              response.raise_for_status()
              data= (response.json())
              df_bing = spark.createDataFrame(data['webPages']['value']).select('name','snippet','url')
              display(df_bing)
  
- In the next code cell ,copy the code below and execute , To learn more about V-ordering refer [here](https://learn.microsoft.com/en-us/fabric/data-engineering/delta-optimization-and-v-order?tabs=sparksql#what-is-v-order)

              #enable vordering for performance and set delta parquet file size
              spark.conf.set("spark.sql.parquet.vorder.enabled", "true")
              spark.conf.set("spark.microsoft.delta.optimizeWrite.enabled", "true")
              spark.conf.set("spark.microsoft.delta.optimizeWrite.binSize", "1073741824")

- In the next code cell ,copy the code below and execute to craete a table and after completion verify the table is created with data 

            #write dataframe to table 
            df_bing.write.mode("overwrite").format("delta").option("overwriteSchema", "true").save("Tables/bingresults")

  <img width="367" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/fc3d6049-b775-4bac-8e1c-39ee53246d8c">



## Approach 6: Using OneLake File Explorer to Sync files

- Sign in into the OneLake File Explorer with the same account you used to create the lakehouse
  
- Browse to the Lakehouse folder and the files folder

  <img width="1067" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/4f8f954e-d8d1-4872-89fa-154e6412c4d4">

- Copy the files into the OneLake File Explorer 

  <img width="1070" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/23405711-243a-4806-b404-12701da615c6">

- Navigate to the Lakehouse in [Fabric Portal](https://app.powerbi.com) and confirm the files are available in the Files section


  <img width="1132" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/58b330c6-6118-404a-9b6d-8809db546809">

- If unavailable click on Files and use Refresh option

  <img width="1110" alt="image" src="https://github.com/mahes-a/Fabric-Ingestion/assets/120069348/eee657be-42ab-4408-bcd5-3ad2025add24">



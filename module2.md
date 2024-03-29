
# ServerLessLab
A ServerLess Lab



# Module 2 - ServerLess nodejs. Blob Trigger

As part of our Car detection Service we need a mechanism to import easily our images to our CustomVision Service. As such we will need an event driven API to detect when a new image is uploaded and send it to our custom Vision service to figure out what type of car is in the image. 

This module will walk you through building, testing and publishing your first Azure Function in the clou. The Azure Function will be the serverless API to react the data on newly uploaded images 
## Pre-requisites 
* An Azure Subcription 
## Challenge 
Create an event driven Azure Serverless Function that procesess files stored on an azure storage account.  This function should receive the file and print the output to the functions log output. You will need to create a Function APP and add a new function which is triggered by new files in blob storage. At a later step we will add cosmosdb and Cognitive service. You should be able to upload a new file to blob storage to test.




### Guided instructions

<details><summary>Click to open</summary><p>

## Challenge 
Theres 3 steps that need to be peformed 
 * Create fucntion App 
 * Create Blob Triggered Function 
 * Test Function 


### Create Nodejs Function App

1. Open the Azure Portal on https://portal.azure.com, click on “Create a resource”
1. Type “Function App” in the search bar, click Create
1.	Enter a unique name for your function. Create a new resource group. Choose a name
1. OS: Windows
1.	Location: West Europe
1.	Runtime Stack: Node.js
1.	Storage: Create new (accept default)
1.	Click Create
 * ![CreateServerLess](/module2/severlesscreate.png)

### Create Blob Trigger Function 
1.	Click on "Resource Groups" and select your created rg
1.	Click on your Function
1.	Click on "+ New Function" button
1.	For Development environment select: "In-portal" and click on continue
1.	Select "More templates…", then "Finish and view templates"
1.	Select "Azure Blob Storage trigger"
1.	On the popup screen click on "Install" (for the extension). This can take up to 2 minutes. Wait and don’t leave the screen!
1.	Once done, click continue
1.	Pick a name. E.g. CarModelClassification
1.	Change the path to "images/{name}"
1.	Leave the rest and click Create
  ![CreateServerLess](/module2/StorageTrigger.png)

### Test Blob Trigger
Now that we have a blob trigger we want to verify if it is correctly triggering on new files under the storage account. By default the the Blob Trigger will listen on the default storage of your Function. To test this we need to create a new Blob container called "images"(the path we chose to listen on in the las step) and upload any file to the new blob container
1. Once the deployment of the Function App from the previous step is finshed (you will get a notification in the portal or you can also click on the little bell icon on the top of the page), continue:
1. Under the "Resource Group" blade select the group you created  
1. Once uploaded navigate to your function app and select the function you created, e.g. "CarModelClassification" 
1. Open the logs tab. Keep this open as this will output logs when we upload a new file 
1. In a new browser tab: Open the Azure Portal again (https://portal.azure.com) and click on Storage accounts on the left hand side.
1. Select the storage account that was created with your function App. (The name is similar to the name of your Function app)
1. Select "Blobs" 
1. Create a new container named "images". This is the container/folder the function is triggered on ![CreateServerLess](/module2/createblob.png)
1. Click on the name of the newly created container.
1. Upload any file to the container images. ![CreateServerLess](/module2/upload.png)
1. Naviagte back to the tab where the functions logs are open. You should see a new output which got triggered after we uploaded our new file. 
![CreateServerLess](/module2/logoutput.png)





Now we have a Function app which can be triggered by a new file in blob storage under the path images/* . We have not specified where exactly this is. But we have not connected the Function with the Blob storage account.

 </p></details>

 ## Documentation
* https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-storage-blob-triggered-function
* https://docs.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-blob
* https://docs.microsoft.com/en-us/azure/cosmos-db/serverless-computing-database
* https://docs.microsoft.com/en-us/azure/azure-functions/functions-bindings-cosmosdb-v2#input---javascript-examples



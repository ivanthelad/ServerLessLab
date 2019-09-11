
# ServerLessLab
A ServerLess Lab



# Module 2 - ServerLess nodejs. Blob Trigger

As part of our Car detection Service we need a mechanism to import easily our images to our CustomVision Service. As such we will need an event driven API to detect when a new image is uploaded and send it to our custom Vision service to figure out what type of car is in the image. 

This module will walk you through building, testing and publishing your first Azure Function in the clou. The Azure Function will be the serverless API to react the data on newly uploaded images 
## Pre-requisites 
* A Azure Subcription 
## Challenge 
Create an event driven Azure Serverless Function that procesess files stored on an azure storage account.  This function should receive the file and send it the trained Azure Cognitive service created in module0 and store the results in the cosmos db created in module1. As a first step you should c




expose the detect what type of car is in a image uploaded to the cloud. 

### Guided instructions

<details><summary>Click to open</summary><p>

## Challenge 

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
1.	Click on “Resource Groups” and select your created rg
1.	Click on your Function
1.	Click on “+ New Function” button
1.	In-portal
1.	More templates… Finish and view templates
1.	Azurce Blob Storage trigger
1.	Click on Install (for the extension). This can take up to 2 minutes. Wait and don’t leave the screen!
1.	Once done, click continue
1.	Pick a name. E.g. BmwModelClassification
1.	Change the path to “images/{name}”
1.	Leave the rest and click Create
 * ![CreateServerLess](/module2/StorageTrigger.png)

### Test Blob Trigger
Now that we have a blob trigger we want to verify if it is correctly triggering on new files under the storage account. By deault the the Blob Trigger will listen on the default storage you functions.  To Test this we need to create a new Blob container called "images"(the path we chose to listen on in the las step) and upload any file to the new blob container
1. Under the "Resource Group" blade select the Rg you created  
1. Once uploaded navigate to your function app and select the function your created "BmwModelClassification" 
1. Open the logs tab. Keep this open as this will output logs when we upload a new file 
1. In a new browser tab.Select the storage account that was created with your function App. 
1. Select "Blobs" 
1. Create a new Container "images". This was the container/folder the function is triggered on ![CreateServerLess](/module2/createblob.png)

1. upload any file to the container images . ![CreateServerLess](/module2/upload.png)

1. naviagte back to the tab where the functions logs are open. you should see a new output which got triggered aftert we uploaded our new file. 
![CreateServerLess](/module2/logoutput.png)





Now we have a function app which can be triggered by a new file in blob storage under the path images/*. we have not specified where exactly this is. But we have not connected the 

 </p></details>

 ## Documentation

* https://docs.microsoft.com/en-us/azure/azure-functions/functions-create-storage-blob-triggered-function
* https://docs.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-blob



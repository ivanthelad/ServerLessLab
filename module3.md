
# ServerLessLab
A ServerLess Lab



# Module 3 - ServerLess nodejs Blob Trigger. Cosmosdb 

As part of our Car detection service, anytime someone uploaded a new file to the blob storage we want to record this information in our cosmosdb. 
  

## Pre-requisites 
* A Azure Subcription 
## Challenge

Building upon module 3, we want to expand our BlobTrigger function to send output data to CosmosDB. This function will simply save file data to cosmostdb for now

### Guided instructions

<details><summary>Click to open</summary><p>



### CosmosDB output Blob Trigger


1. Under the "Resource Group" blade select the Rg you created  
1. navigate to your function app and select the function your created "ModelClassification" 
1. Click on “Integrate” and then on New Output
1. Select Azure Cosmos DB
1. Click on “Install” in the “Extension not installed warning” and wait again will finished
1. Click on “new” button next to “Azure Cosmos DB account connection”
1. Select your subscription and the Cosmos DB account that you created before
*<div style="width:150px; height:100px"> ![CreateServerLess](/module3/newconnection.png) </div>
1. Change Database Name to “ServerlessTutorial”
1. Change Collection Name to “Images”
1. Mark the Checkbox “If true, creates the database and collection”. Your config will look similar to the following 
* ![CreateServerLess](/module3/cosmosdbintegrateoutput.png)
1. Click save. 
### Update Nodejs function Code 
1. Select the function and replace the content of function (index.js) with the following code snippet. 
```javascript
module.exports = async function (context, myBlob) {
    context.log("JavaScript blob trigger function processed blob \n Name:", context.bindingData.name, "\n Blob Size:", myBlob.length, "Bytes");
    // writing to output binding
    context.bindings.outputDocument = JSON.stringify({
            image:  context.bindingData.uri,
            tag: "testtag",
            size: myBlob.length
        });
};
```
1. To test persitence to cosmosDB,  upload another image to the blob storage as you did in module2. while monitoring the functions. 
1. Naviagte back to the tab where the functions logs are open. you should see a new output which got triggered aftert we uploaded our new file. 
1. Navigate to CosmosDB in the ResourceGroup you created.
    * select Data Explorer 
    * you should see an entry under a collection called "images"
1. The output in data explorer show show the document with 3 attributes 
    * image
    * tag 
    * size






Now we have a function app which can be triggered by a new file in blob storage under the path images/*. The results are then saved in a cosmosdb collection. Next step will be to call our cognitive service 

 </p></details>

 ## Documentation
* https://docs.microsoft.com/en-us/azure/cosmos-db/sql-api-nodejs-get-started
* https://docs.microsoft.com/en-us/azure/azure-functions/functions-bindings-cosmosdb-v2
* https://docs.microsoft.com/en-us/azure/azure-functions/functions-reference-node#bindings


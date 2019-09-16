
# ServerlssLab
A ServerLess Lab



# Module 1 - CosmosDB 

For  this module we wil create a database to store the result of our custom vision API. This will enable us to query the results and classifications of the images being uploaded into our custom vision service. 


This module will walk you through creation of your first Cosmos DB. The database will serve as the data backed for our application. 


## Pre-requisites 
* An Azure Subcription 
## Challenge 
Create a Cosmos DB to store our custom vision results 

### Guided instructions

<details><summary>Click to open</summary><p>

1. Open the Azure Portal at https://portal.azure.com
1.	Click on "Create a resource" in the upper left corner
1.	Type "Azure Cosmos DB", select the first suggestion and then click "Create"
1.	Select the resource group that you created in step module0 where your CognitiveServices are running 
1.	Type a unique account name
1.	Location: West Europe. Leave the rest as default
1. Hit Review+Create. Then "Create" on the next page
 ![CreateServerLess](/module1/createCosmosDB.png)
</p></details>


 ## Documentation
* [Azure Cosmos DB Overview](https://docs.microsoft.com/en-us/azure/cosmos-db/introduction)
* [Azure Functions CosmosDB Binding (v2)](https://docs.microsoft.com/en-us/azure/azure-functions/functions-bindings-cosmosdb-v2)
* [Azure CosmosDB Visual Studio Code extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-cosmosdb)
* https://docs.microsoft.com/en-us/azure/cosmos-db/serverless-computing-database 

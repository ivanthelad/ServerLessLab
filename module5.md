
# ServerLessLab
A ServerLess Lab



# Module 5 - Query data HTTP Trigger 

For this module we wil create a http based trigger to query our newly created classification database.


## Pre-requisites 
* A Azure Subcription 
* Module 0-4 are complete 
## Challenge 
Create an cosmosDB to store our custom vision results 

### Guided instructions

<details><summary>Click to open</summary><p>

1.	“Create a resource” again
1.	Type “Cosmos DB”, click Create
1.	Select the resource group that you created in step module0 where your CognitiveServices are running 
1.	Type a unique account name
1.	Location: West Europe. Leave the rest as default and hit Review+Create. Then create
 * ![CreateServerLess](/module1/createCosmosDB.png)
</p></details>


 ## Documentation
* [Azure Cosmos DB Overview](https://docs.microsoft.com/en-us/azure/cosmos-db/introduction)
* [Azure Functions CosmosDB Binding (v2)](https://docs.microsoft.com/en-us/azure/azure-functions/functions-bindings-cosmosdb-v2)
* [Azure CosmosDB Visual Studio Code extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-cosmosdb)
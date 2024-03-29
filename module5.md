
# ServerLessLab
A ServerLess Lab



# Module 5 - Query data HTTP Trigger 

For this module we will create a http based trigger to query our newly created classification database.


## Pre-requisites 
* An Azure Subcription 
* Module 0-4 are complete 
## Challenge 
In this module you need to create a new nodejs Azure Function which is trigger with a http call. The function calls the cosmos db and returns a json object with following. The function will 
* Allow you to perform  GET on a specific endpoint and pass in a "tag" name as a paramerer . 
* The 'tag' name will return a list of cars that have been classified with that tag. 
*  For example if you did the following HTTP Request:
```
GET http://{myFunctionEndpoint}/api/cars?tag=mini
```
* the API will return 
```json
[
  {
    "id": "5b24c663-ed24-4478-b090-d06bc98d22c7",
    "image": "https://$url.blob.core.windows.net/images/280px-2004_Mini_Cooper_1.6.jpg",
    "classification": "mini",
    "probability": 0.999934435
  },
  {
    "id": "d34df041-f461-4c2e-a38d-02ac91e77524",
    "image": "https://$url.blob.core.windows.net/images/mini.jpg",
    "classification": "mini",
    "probability": 0.94435
  }
]
 
```
### Guided instructions

<details><summary>Click to open</summary><p>

### Create HTTP Trigger Function 
1.	Click on “Resource Groups” and select your created rg
1.	Click on your Function
1.	Click on “+ New Function” button
1.	Select "HTTP Trigger"
1.  A dialog appears 
    * Set name of function to "cars". This will be also the endpoint you access your https service on 
    * Set Authorization level to "Anonymous"
    * ![ddd](/module5/CreateHttpFunction.png)
1. A default http function will be created. You can test this functionality by calling the function url which can be found under  the top of the function
![ddd](/module5/testfunction.png) 

### Create Cosmos DB Input Binding
In this step we will bind the http trigger to fetch input from our cosmos db. This transparently will call to the database for data from the cosmos db and feed it as input to our function. 
1.	Under your newly created function,"Cars", select "Integrate"
1.  Create a new CosmosDB input binding by clicking on "new Input" and selecting "Azure Cosmos DB". This binding will fetch data stored in cosmos db from the previous step 
    *  ![ddd](/module5/createbinding.png)
1. Configure the following input bindings settings 
    * Collection name: This is the collection name you configured in [Step 9 in module 3](/module3.md) ("Images")
    * Database Name: This is the database name you configured in [Step 8 in module 3](/module3.md) ("ServerlessTutorial")
    * CosmosDB acccount connection: Configure the cosmosdb connection string. If it is not already pre-selected for you, click "add new" to select the cosmos db from module3.
    * SQL Query: This is the query that is used to fetch data stored in cosmosdb. Add "Select * from images i where i.tag = {tag}"
    * Ensure that Document Parameter name is "inputDocument"
    * ![ddd](/module5/Cosmosinputbinding.png)
1. Update the index.js script with the following code 
```javascript

function CarClassification(id, image,classification, probability){
    this.id = id;
    this.image= image; 
    this.classification = classification;
    this.probability = probability
}
module.exports = async function (context, req, inputDocument) {
    context.log('JavaScript HTTP trigger function processed a request. with tag='+req.query.tag);
    var classifications = []; 
    for(let val of inputDocument) {
      classifications.push(new CarClassification(val.id, val.image, val.tag, val.probability ) )
    }
    context.res = {
      status: 200,
      body: JSON.stringify( classifications),
      headers: { 'Content-Type': 'application/json' }
    };
    context.done(null,context.res);
}; 


```

Now you should be able to test the function. 

1. Copy the functions URL and add the tag parameter to the url. You can copy the URL from the link "Get function URL" above the code view of your function 
    * It should look similar to this: https://customvisioncardetection.azurewebsites.net/api/cars2?tag=Mini 
    * Make sure you write the tag, e.g. "Mini" exactly as you defined it in the custom vision service. It is case-sensitve.


</p></details>


## Documentation
* [Http webhook ](https://docs.microsoft.com/en-us/azure/azure-functions/functions-bindings-http-webhook)
* [Cosmosdb input binding ](https://docs.microsoft.com/en-us/azure/azure-functions/functions-bindings-cosmosdb-v2)

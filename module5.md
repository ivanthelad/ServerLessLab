
# ServerLessLab
A ServerLess Lab



# Module 5 - Query data HTTP Trigger 

For this module we wil create a http based trigger to query our newly created classification database.


## Pre-requisites 
* A Azure Subcription 
* Module 0-4 are complete 
## Challenge 
In this module you need to create a nodejs Azure Function which is trigger with a http call. The function calls the cosmos db and returns a json object with following. The function will 
* Allow you to perform  GET on a specific endpoint and pass in a "tag" name as a paramerer . 
* The 'tag' name will return a list of cars that have been classified with that tag. 
*  For example if you did the following HTTP Request:
```
GET http://{myFunctionEndpoint}/api/cars?type=mini
```
* the Api will return 
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
    * Set name of fucntion to "cars". this will be also the endpoint you access your https service from 
    * set Authorization level to "Anonymous"
    * ![ddd](/module5/CreateHttpFunction.png)
1. A default http function will be created. You can test  this functionality by calling the function url which can be found under in the top of the fucntion
![ddd](/module5/testfucntion.png) 

### Create Cosmos Input Binding
in this step we will bind the http trigger fetch input from  our cosmos db. This transparently will call to the database a fetch for data from the cosmos db and feed it as input to our function. 
1.	Under your newly created function,"Cars", select "Integrate"
1.  Create a new CosmosDB input binding. This binding will fetch data stored in cosmos db from the previous step 
    *  ![ddd](/module5/createbinding.png)
1. Configure the following input bindings settings 
    * Collection name: This is the collection name you configured in [Step 9 in module 3](/module3.md)
    * Database Name: This is the database name you configured in [Step 8 in module 3](/module3.md)
    * CosmosDB acccount connection: Configure the cosmosdb connection string. click "add new" to select the cosmos db from module3
    * SQl Query: This is the query that is used to fetch data stored in cosmosdb. Add "Select * from images i where i.tasg = {tag}"
    * Ensure that Document Parameter name is "inputDocument"
    * ![ddd](/module5/Cosmostinputbinding.png)
1. update the index.js script with the following code 
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

1. Now you should be able to test the function. Find the functions URL and add the tag parameter to the url 
    * https://customvisioncardetection.azurewebsites.net/api/cars2?tag=mini 


</p></details>


## Documentation
* [Azure Cosmos DB Overview](https://docs.microsoft.com/en-us/azure/cosmos-db/introduction)

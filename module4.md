<div>
img[src~="thumbnail"] {
   width:150px;
   height:100px;
}
img[src~="bordered"] {
   border: 1px solid black;
}
</div>

# ServerLessLab
A ServerLess Lab




# Module 4 - Model detection
For this module we need to update our Azure function to call our trained conigtive service. Our nodejs function will make an call to the Custom Vision and save the results to cosmosdb 

## Pre-requisites 
* An Azure Subcription 
* The Custom vision training from module 1 is complete.
## Challenge

Building upon module 3, we want to expand our BlobTrigger function to send output data to CosmosDB. This function will simply save image classification data to cosmosdb for now. This challenge will require that our custom vision API from  module1 is is finished training and published. 


### Guided instructions

<details><summary>Click to open Module4 steps </summary><p>

### Publish Custom Vision API. 
In this step we will publish our trained model 
1. Navigate to your previously created model from module1 in the cusotmviosn portal https://www.customvision.ai 
2. Verfiy your training was successful. The results should be above the 90% range ans should look similar to the following 
trained model. To use this model, we will make it available as a web service (publish). This creates a REST endpoint that we can call and get classifications for new images.
![trainedmodel](/module4/trainedmodel.png#thumbnail))
3. Publish API by click the "Publish" button under "Project->Perfromance". 
![trainedmodel](/module4/publishapi.png)
4. This will open a new dialog where you will need to select the predication Resource to deploy to.
![trainedmodel](/module4/publish.png#thumbnail))
5. When you click the button "Prediction URL" you can view the prediction URL and Key. You will need the settings from the section "If you have an image file". These settings will be required to be set as variables in the next step, so its recommend to copy them now to Notepad.  
![predictionurl](/module4/predictionURL.png#thumbnail))


### CosmosDB output Blob Trigger
In this step we call our newly published classfication API from our Function app and save the classfication results to the cosmosdb. This is done via the so called Function output binding. 

1. Under the "Resource Group" blade select the Rg you created  
1. Navigate to your function app and select the function your created, e.g. "ModelClassification" 
1. Select the function and replace the content of function (index.js) with the following code snippet. 
```javascript
const request = require('request');
const endpoint = 'ENTER YOUR CUSTOM VISION ENDPOINT';
const predictionKey = 'ENTER YOUR CUSTOM VISION PREDICTION KEY';

module.exports = function (context, myBlob) {
    context.log("JavaScript blob trigger function processed blob \n Name:", context.bindingData.name, "\n Blob Size:", myBlob.length, "Bytes");
	
    let options = {
        uri: endpoint,
        body: myBlob,
        headers: {
            'Content-Type': 'application/octet-stream',
            'Prediction-Key' : predictionKey
        }
    };

    context.log('Calling Custom Vision API now...');

    request.post(options, (error, response, body) => {
        if (error) {
            context.log('Error: ', error);         
            context.done();
        }
        js = JSON.parse(body);
        let jsonResponse = JSON.stringify(js, null, '  ');
        context.log('JSON Response:\n');
        context.log(jsonResponse);

        context.log('Custom Vision Result: Highest predicted tag: ' + js.predictions[0].tagName + ' - Probability: ' + js.predictions[0].probability);   
        
        context.log('Writing document to Cosmos DB now');

        context.bindings.outputDocument = JSON.stringify({
            image:  context.bindingData.uri,
            tag: js.predictions[0].tagName,
            probability: js.predictions[0].probability
        });
        
        context.done();
    });
};

```
1. You need to update the variables in the above code with setting from the prediction URL. These setting were copied from the previous step. [predictionurl](/module4/predictionURL.png)
   * Line 2: endpoint: Can be found under the overview Blade in the Vision service. 
   * Line 3: predictionKey: Select one of the keys from the "Keys" blade in the Vision Service 
1. Once you have obtained the prediction URL and prediction key from custom vision, copy them into the function code in lines 2 and 3
1. Click on save
1. If you try to rerun a test the code will fail with the following exception. This is because the Node.JS library "request" is not available yet. We will need to install the package  
  * ![npmerror](/module4/npmerror.png)
1. To install the NPM package "request", Click on Console on the bottom of the screen. 
1. Type "npm install request" and hit enter
* ![npmerror](/module4/npminstall.png)
1. Wait until done. The Red warnings can be ignored
1. Click on Logs (next to Console)


## Testing 
The function should now be ready to test 
1. To test persitence to cosmosDB, upload another image to the blob storage as you did in module2 while monitoring the functions. 
1. Naviagte back to the tab where the functions logs are open. You should see a new output which got triggered aftert we uploaded our new file. 
1. Navigate to CosmosDB in the ResourceGroup you created.
    * select Data Explorer 
    * you should see an entry under a collection called "images"
1. The output in data explorer show the document with 3 attributes 
    * image
    * tag 
    * size

Now we have a function app which can be triggered by a new file in blob storage under the path images/* which then calls our Custom Vision API and saves the results in a cosmosdb collection.
 </p></details>

 ### Documentation
* https://docs.microsoft.com/en-us/azure/cosmos-db/sql-api-nodejs-get-started
* https://docs.microsoft.com/en-us/azure/azure-functions/functions-bindings-cosmosdb-v2
* https://docs.microsoft.com/en-us/azure/azure-functions/functions-reference-node#bindings


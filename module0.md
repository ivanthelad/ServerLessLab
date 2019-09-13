# ServerLessLab
A ServerLess Lab



# Module 0 - Cognitive Services 
As part of this the architectue we will need to create a cognitive service to classify each car.  This service will expose an API which will accept an image and determine what type of car is in the image. Either a X5, Mini or z4.


This module will walk you through building, Training and testing your first Azure Cognitive Service, and publishing to the cloud.  The Service will be the serverless API to expose the detect what type of car is in a image uploaded to the cloud. 
## Pre-requisites 
* A Azure Subcription 

## Challenge
Create and train a  Custom Vision service that is able to detect what type of car is in a image. The customer vision service should detect if an image contains either
* X5 
* Mini
* Z4
### Guided instructions

<details><summary>Click to open</summary><p>



Create Cognitive Service 

1.	Unzip the file. It contains three folders (one for each model)
1.	Go to www.customvision.ai
1.	Login and create a new project
1.	Pick a name
1.	Classification. Multiclass. Domain: General 
1.	In the newly created project click on Add Images
1.	Select all images from one of the folder, e.g. X5
1.	Under My Tags enter e.g. X5 and hit enter. Then click on Upload 
1.	Repeat the step for all three models
1.	Once uploaded, click on the green Train button
1.12	Select Advanced Training. Leave the default of 1 hour training budget. Don’t worry, it will not run for an hour. Click Train
1.13	While this is running (10-15min), you con continue with the next step. Ideally in a new browser window/tab. Leave Custom Vision page open.
1.14	Once the training is finished, you will see the metrics. They should be in the range of 80-90%.
1.15	Click on publish to make this training available on a HTTP endpoint
1.16	Click on Prediction URL
1.17	Copy the second endpoint URL (“If you have an image file”), e.g. to Notepad. It looks something like this: https://southcentralus.api.cognitive.microsoft.com/customvision/v3.0/Prediction/xxxxxxx-xxxx-xxxxxx-xxx/classify/iterations/Iteration1/image
1.18	Also copy the Prediction-Key to Notepad

1.	“Create a resource” again
1.	Type “Cosmos DB”, click Create
1.	Select the resource group that you created in step module0 where your CognitiveServices are running 
1.	Type a unique account name
1.	Location: West Europe. Leave the rest as default and hit Review+Create. Then create
 * ![CreateServerLess](/module1/createCosmosDB.png)
</p></details>


![Custom Vision](/module1/CreateCustomVisionProject.png)
Format: ![Alt Text](url)

Run and test an Azure Function locally where you can do a `GET` on a specific endpoint and pass in a product ID.  The product ID will return information on the product flavor.  For example if you did the following HTTP Request:

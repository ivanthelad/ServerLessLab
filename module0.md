# ServerLessLab
A ServerLess Lab



# Module 0 - Cognitive Services 
As part of this the architectue we will need to create a cognitive service to classify each car.  This service will expose an API which will accept an image and determine what type of car is in the image. Either a X3, Mini or 5er.


This module will walk you through building, Training and testing your first Azure Cognitive Service, and publishing to the cloud.  The Service will be the serverless API to expose the detect what type of car is in a image uploaded to the cloud. 
## Pre-requisites 
* An Azure Subcription 

## Challenge
Create and train a  Custom Vision service that is able to detect what type of car is in a image. The customer vision service should detect if an image contains either
* X3 
* Mini
* 5er
### Guided instructions

<details><summary>Click to open</summary><p>



Create Cognitive Service 
### Create Project and upload training Images 
1.	Unzip the file. It contains 4 folders (one for each model)
1.	Go to https://customvision.ai. Please accept the terms and allow Azure Custom Vision to access your Azure subscription 
    * You should not have any projects in your account. 
1.	To create your first project, select New Project. The Create new project dialog box will appear.
    * Before creating a Project you will need to create a Cognitive Services Resource. Click "Create new "
    * Enter a name and a description for the project. 
    * Then select a Resource Group. If your signed-in account is associated with an Azure account, it will display all of your Azure subscriptions and Resource Groups that include a Custom Vision Service Resource.the Resource Group dropdown 
    *  ![CreateCognitiveService](/module0/Step2CreateCognitiveService.png)
1. After the Cognitive service is created then create the Project with the following config 
    * ***Project Types*** = "Classification"
    * ***Classification Type*** = "Multiclass (Single tag per image)"
    * ***Domains*** = "General"
    * ![CreateCognitiveService](/module0/CreateCustomVisionProject.png)
1. In the newly created project click on Add Images
    * ![CreateCognitiveService](/module0/addimages.png)
1.	Select all images from one of the folder, e.g. "X3"
1.	Under My Tags enter e.g. X3 and hit enter. Then click on Upload.
    *  ***Ensure you hit Enter/Return before clicking on Upload as other wise the Tag is not added***
    * ![CreateCognitiveService](/module0/imagetagging.png)
1.	Repeat the step for all three models

### Train Model 
1. Once uploaded, click on the green Train button	
1. Select Advanced Training. Leave the default of 1 hour training budget. Don’t worry, it will not run for an hour. Click Train
    * While this is running (10-15min), you can continue with the next module. Ideally in a new browser window/tab. Leave the Custom Vision page open, we will come back to it later.
    * Once the training is finished, you will see the metrics. They should be in the range of 80-90%.
1. Click on publish to make this training available on a HTTP endpoint
    *  ***the training can take time and we will come back to these steps later*** 
1.	Click on Prediction URL
1.	Copy the second endpoint URL (“If you have an image file”), e.g. to Notepad. It looks something like this: https://southcentralus.api.cognitive.microsoft.com/customvision/v3.0/Prediction/xxxxxxx-xxxx-xxxxxx-xxx/classify/iterations/Iteration1/image
1. 	Also copy the Prediction-Key to Notepad


</p></details>


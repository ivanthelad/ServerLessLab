# ServerLessLab
A ServerLess Lab



# Module 1 - Cognitive Services 

As part of this the architectue we will need to create a cognitive service to classify each car.  This service will expose an API which will accept an image and determine what type of car is in the image. Either a X5, Mini or z4


This module will walk you through building, Training and testing your first Azure Cognitive Service, and publishing to the cloud.  The Service will be the serverless API to expose the detect what type of car is in a image uploaded to the cloud. 
## Pre-requisites 
* A Azure Subcription 


## Challenge
Create a Custom Vision service that is trained to detect what type of BMW car is in a image.  The customer vision service should detect if an image contains 
* X5 
* Mini
* Z4


Run and test an Azure Function locally where you can do a `GET` on a specific endpoint and pass in a product ID.  The product ID will return information on the product flavor.  For example if you did the following HTTP Request:

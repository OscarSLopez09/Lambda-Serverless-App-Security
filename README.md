# Let's start with a high-level overview.

In this section I'm creating a usage plan and the API keys. Also, I'm creating the Prod stage and deploy it.

The API key consists of randomly generated characters of alphabets and numbers. You associate a specific API key with a specific API client. Since API usage is essentially one software module talking to another, the keys are associated with different software modules or applications that want to talk to your API. 

When an application sends API requests, the process works as follows:

1. The API server validates the requestor's authenticity with the unique API key.
2. If the API key doesn't match any of the permitted ones, the server declines the API call and sends a rejection message.
3. If the API key matches, the server fulfills the request and returns the expected response.

This way, API keys allow the API server to identify the origin of each API call. The server can then perform subsequent validations to authorize access to the API's data and services.

This is part 6 final part of the project, link to the other parts below:

- [Part 1 Lambda Serverless App ](https://github.com/OscarSLopez09/Lambda-Serverless-App)
- [Part 2 Testing the first part ](https://github.com/OscarSLopez09/Serverless-Testing-Part1)
- [Part 3 Creating the backend lambda](https://github.com/OscarSLopez09/Lambda-Serverless-App-Part2)
- [Part 4 Creating API Gateway ](https://github.com/OscarSLopez09/Serverless-App-Part2-API-GW)
- [Part 5 Creating CloudWatch event](https://github.com/OscarSLopez09/Serverless-Cloudwatch-Rule)

## Creating usage plan

* We go to the API Gateway console, we scroll down to Usage plans and click on it.
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Security/blob/main/Images/security00.PNG" height="90%" width="90%" alt="Disk Sanitization Steps"/>

* Select Create usage plan
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Security/blob/main/Images/security01.PNG" height="90%" width="90%" alt="Disk Sanitization Steps"/>

* On Usage plan details create the name - startupNewssentiment
* Rate - 1000
* Burst - 500
* Requests - 200
* Click on Create usage plan
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Security/blob/main/Images/security02.PNG" height="90%" width="90%" alt="Disk Sanitization Steps"/>

* Once the usage plan has been created

## Creating API keys

* Go to API keys and select Create API key
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Security/blob/main/Images/security04.PNG" height="90%" width="90%" alt="Disk Sanitization Steps"/>

* On the API key details
* Create name - StartupApiNews
* Click on Save
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Security/blob/main/Images/security05.PNG" height="90%" width="90%" alt="Disk Sanitization Steps"/>

* Now, copy the API key generated
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Security/blob/main/Images/security06.PNG" height="90%" width="90%" alt="Disk Sanitization Steps"/>

## Associate the API key with an usage plan

* Select Add to usage plan
* On Usage plan click the drop-down and select - StartupNewssentiment
* Click Save
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Security/blob/main/Images/security07.PNG" height="90%" width="90%" alt="Disk Sanitization Steps"/>

* Go back to Usage plan and add stage
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Security/blob/main/Images/security09.PNG" height="90%" width="90%" alt="Disk Sanitization Steps"/>

* On Stage details, click the drop-down API select - NewsReaderAPI
* On Stage select - Dev 
* Click on Add to usage plan
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Security/blob/main/Images/security10.PNG" height="90%" width="90%" alt="Disk Sanitization Steps"/>

* Go back to API, then Resources
* Click on POST 
* Click on Method request tab
* Select Edit
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Security/blob/main/Images/security13.PNG" height="90%" width="90%" alt="Disk Sanitization Steps"/>

* Click API key required check mark and click Save
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Security/blob/main/Images/security22.PNG" height="90%" width="90%" alt="Disk Sanitization Steps"/>

* Click on Deploy to deploy the API
* Deploy API Stage - Dev
* Click on Deploy
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Security/blob/main/Images/security16.PNG" height="90%" width="90%" alt="Disk Sanitization Steps"/>

## Now proceed to tested out.

* Copy the POST Invoke URL
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Security/blob/main/Images/security17.PNG" height="90%" width="90%" alt="Disk Sanitization Steps"/>

* On Postman paste the Invoke URL and click on Send
* We get the {"message":"Forbidden"}
* Getting the "Forbidden" message means that is workinng
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Security/blob/main/Images/security18.PNG" height="90%" width="90%" alt="Disk Sanitization Steps"/>

Now we need to configure the API key with Postman to be able to access the API Gateway.
 
* To configure the API key we click on Headers
* On key field type - x-api-key
* Value field paste the API key
* Click on Send 
* We received the sentiment with the news, this is the expected response
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Security/blob/main/Images/security19.PNG" height="90%" width="90%" alt="Disk Sanitization Steps"/>

* Go back to Resources and click on Deploy API to re deploy
* On Stage - New Stage name
* Stage name - Prod
* Click on Deploy
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Security/blob/main/Images/security20.PNG" height="90%" width="90%" alt="Disk Sanitization Steps"/>

* Go back to Usage plans
* Add the Prod Stage by clicking add stage
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Security/blob/main/Images/security21.PNG" height="90%" width="90%" alt="Disk Sanitization Steps"/>

* On Stage details select - NewsReaderAPI
* Select Stage - Prod
* Click on Add to usage plan
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Security/blob/main/Images/security24.PNG" height="90%" width="90%" alt="Disk Sanitization Steps"/>

* Go back to the API and select Stages
* Select the Prod Stage and copy the POST Invoke URL
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Security/blob/main/Images/security25.PNG" height="90%" width="90%" alt="Disk Sanitization Steps"/>

## Testing Prod stage on Postman

* Go back to the Postman
* Paste the Prod URL
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Security/blob/main/Images/security28.PNG" height="110%" width="110%" alt="Disk Sanitization Steps"/>

* Select Headers and on key type -x-api-key
* On Value field paste the API key
* Click on Send
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Security/blob/main/Images/security26.PNG" height="110%" width="110%" alt="Disk Sanitization Steps"/>

* The result is successful!
* The API is able to fetch the news with the sentiment
<img src="https://github.com/OscarSLopez09/Lambda-Serverless-App-Security/blob/main/Images/security29.PNG" height="90%" width="90%" alt="Disk Sanitization Steps"/>

Links to the other parts of the project:

- [Part 1 Lambda Serverless App ](https://github.com/OscarSLopez09/Lambda-Serverless-App)
- [Part 2 Testing the first part ](https://github.com/OscarSLopez09/Serverless-Testing-Part1)
- [Part 3 Creating the backend lambda](https://github.com/OscarSLopez09/Lambda-Serverless-App-Part2)
- [Part 4 Creating API Gateway ](https://github.com/OscarSLopez09/Serverless-App-Part2-API-GW)
- [Part 5 Creating CloudWatch event](https://github.com/OscarSLopez09/Serverless-Cloudwatch-Rule)






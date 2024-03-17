# Let's start with a high-level overview.

In this section I'm creating a usage plan and the API keys. Also, I'm creating the Prod stage and deploy it.

The API key consists of randomly generated characters of alphabets and numbers. You associate a specific API key with a specific API client. Since API usage is essentially one software module talking to another, the keys are associated with different software modules or applications that want to talk to your API. 

When an application sends API requests, the process works as follows:

1 The API server validates the requestor's authenticity with the unique API key
2 If the API key doesn't match any of the permitted ones, the server declines the API call and sends a rejection message
3 If the API key matches, the server fulfills the request and returns the expected response

This way, API keys allow the API server to identify the origin of each API call. The server can then perform subsequent validations to authorize access to the API's data and services.

We go to the API Gateway console, we scroll down to Usage plans and click on it.
Select Create usage plan
On Usage plan details create the name - startupNewssentiment
Rate -1000
Burst - 500
Requests -200
Click on Create usage plan
Once the usage plan has been created
Go to API keys and select Create API key
On the API key details
Create name - StartupApiNews
Click on Save
Now, copy the API key generated
Associate the API key with an usage plan
Select Add to usage plan
On Usage plan click the drop-down and select StartupNewssentiment
Click Save
Go back to Usage plan and add stage
On Stage details, click the drop-down on API select NewsReaderAPI
On Stage select - Dev 
Click on Add to usage plan
Go back to API, then Resources
Click on POST and edit Method request
On Method request settings
Click API key required check mark and click Save
Click on Deploy to deploy the API
Deploy API Stage - Dev
Click on Deploy
Now proceed to tested out.
Copy the POST Invoke URL
On Postman paste the Invoke URL and click on Send
We get the {"message":"Forbidden"}
API is requesting to use the API key to give access to the news sentiment
To configure the API key we click on Headers
On key field type - x-api-key
Value field paste the API key
Click on Send 
We get the response

Go back to Resources and click on Deploy API to re deploy
On Stage - New Stage name
Stage name - Prod
Click on Deploy

Go back to Usage plans
Add the Prod Stage by clicking add stage
On Stage details select - NewsReaderAPI
Select Stage - Prod
Click on Add to usage plan

Go back to the API and select Stages
Select the Prod Stage and copy the POST Invoke URL

Testing Prod stage on Postman
Go back to the Postman
Paste the Prod URL and click on Send
Select Headers and on key type -x-api-key
On Value field paste the API key
Click on Send
The result is successful!




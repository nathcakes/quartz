---
title: Deciphering the WeatherKit API
draft: false
tags:
  - technical
  - API
date: 2024-04-27
---
The current environmental conditions are an important factor when determining the heat stress of an individual and providing a recommendation on whether they should continue work. We needed to get the predicted conditions for the user's current location and store it for up to 5 days in case there was intermittent or reduced internet access. After investigating multiple solutions, I decided to use Apple's WeatherKit API as they use government sources from around the globe, and we receive a monthly quota of API calls as part of our license fees for developing iOS applications.

My first major hurdle was getting an API key; I only had prior experience using a standard API key that you pass along in your URL request. However, the industry has started to migrate to a more secure authentication method called JSON Web Token (JWT). This challenged me as it was difficult to understand this concept for the first time. I found an example repo on Github on generating a JWT, which assisted me in creating the required token. I've set this up to re-generate every 90 days so that if our information is ever compromised, it will become invalid at most after 90 days. Below is an example of how I accomplished this. 

```js title="Generating JWT"
//Import packages for storing the JWT value in AWS Secrets Manager & Getting the token file from S3
const {SecretsManagerClient, UpdateSecretCommand, GetSecretValueCommand, DescribeSecretCommand} = require("@aws-sdk/client-secrets-manager");
    const {S3Client, GetObjectCommand} = require("@aws-sdk/client-s3");
    const fs = require("fs");
    let jwt = require('jsonwebtoken');
    
    //Setup the communication infrastructure
    const secretClient = new SecretsManagerClient({region: "ap-southeast-2"});
    const updatedSecretRequest = new DescribeSecretCommand({"SecretId": "weather-kit_api"});
    const describeResponse = await secretClient.send(updatedSecretRequest);
    const secretUpdatedTime = Math.floor(new Date(describeResponse["LastChangedDate"]).getTime() / 1000);
    //get current timestamp
    const currentTime = new Date().getTime() / 1000;
    //If it's been over 30 days, we should generate a new secret
    if (currentTime - secretUpdatedTime > 2592000){
    //Create a new secret
        console.log("Trying to create a new secret")
        const s3Client = new S3Client({region: "ap-southeast-2"});
        let privateKeyData = await s3Client.send(new GetObjectCommand({Bucket: "omni-private-bucket", Key: "KEY_NAME_REDACTED"}));
        const privateKey = await privateKeyData.Body.transformToString();
        //These values are provided by Apple and have been redacted for security
        const signedKey = jwt.sign({}, privateKey, {algorithm: 'ES256', issuer: "REDACTED", subject: "REDACTED", notBefore: 0, expiresIn: 2629746, header: {"kid": "REDACTED", "id": "REDACTED" }})
        console.log(`New signedkey: ${signedKey}`)
        const newSecret = new UpdateSecretCommand({SecretId: "weather-kit_api", SecretString: signedKey});
        console.log("Sending new secret to AWS Secrets Manager")
        await secretClient.send(newSecret);
    }
    const secretResponse = await secretClient.send(new GetSecretValueCommand({SecretId: "weather-kit_api"}));
    console.log(secretResponse)
    const weatherKitKey = secretResponse["SecretString"];
```

My second major difficulty was understanding how to structure my API call. Apple's developer documentation details the results returned from their API but not how to correctly structure your calls to the API. For example, their documentation does not prescribe how to enter the timezone format, correctly structure the timestamps, or a list of accepted languages. Fortunately, I could piece this information together through trial and error and reading feedback given on the Apple Developer forums.


![[Pasted image 20240930183823.png]]
<p style="text-align: center; font-style: italic;">Artefact: Example API call to the Apple WeatherKit service </p> 
I intend to write a blog post in the coming weeks to provide a walkthrough of the steps I had to take and provide more complete documentation for using the API. This will help develop my writing skills and progress towards my goal of building an online presence this year to improve my resumé for a role as a developer relations manager. I also believe this was a good experience, as it reminded me of the importance of documenting my code and sharing resources with others, as that allowed me to complete my task more easily.
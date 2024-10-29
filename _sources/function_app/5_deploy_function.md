# Deploy the Azure Function on "The Cloud"

Now it is time to move your Cloud Function code to a Resource on Azure so it will be available on the web.

## Define the Settings for your Cloud Function
Execute the following commands at the Azure Cloud Shell command prompt, one at a time:

1. Create a variable that holds a random identifier
```
randomIdentifier=$(openssl rand -hex 4)
```
2. Create a unique name for the function using the random identifer
```
functionAppName="hello-world-${randomIdentifier}"
echo "Function App created with name: $functionAppName"
```
3. Create a variable that contains a Resource Group name
```
resourceGroup="mgmt_59000_func_hello_world"
```

4. Create a variable that contains YOUR Purdue career account username (this will help us make a unique storage account name)
```
careerAccount="YOURCAREERACCOUNT"
```
```{tip}
For example, I would input the following command:
`careerAccount="elliot62"`
```

5. Create a variable that holds a unique storage account name
```
storageAccount="hello_world_${careerAccount}_$(date +%s)"
echo "Your globally unique Storage Account is: ${storageAccount}"
```

6. Finally, use the following command to create a new Cloud Function using all the settings you defined above.
```
az functionapp create \
    --resource-group "${resourceGroup}" \
    --name "${functionAppName}" \
    --storage-account ${storageAccount} \
    --runtime python \
    --runtime-version 3.11 \
    --os-type linux \
    --consumption-plan-location eastus \
    --functions-version 4
```

Once this finishes running, your app will be created on Azure. However, it is not yet publicly available.

7. Publish the app
```
func azure functionapp publish "${functionAppName}"
```


## Test Your Remote Application

After publishing, you should receive a confirmation message that contains a URL. Copy this URL and put it in a new browser tab. You should see the successful deployment message.

Test the function by viewing a customized response to your custom input.

1. Edit the URL and append `api/hello_world` at the end
2. Note the message; your Cloud Function has received and responded to your request

Now we need to add a querystring parameter and argument to pass data into the function.

3. Append `?name=Fred` at the end of the URL and see the change in the response in the browser window
    * Your app is now accepting input and returning output
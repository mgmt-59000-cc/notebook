# Deploy the Azure Function on "The Cloud"

Now it is time to move your Cloud Function code to a Resource on Azure so it will be available on the web.

Remember the organization of a project on Azure:

* A **Resource Group** is a collection of multiple, related resources
* A **Cloud Function** *is* a resource, so it will be inside a Resource Group
* The code for your Cloud Function is stored on Azure in a **Storage Account**
    * Your Storage Account must be in the same Resource Group as your Cloud Function

## Define the Settings for your Cloud Function
Execute the following commands at the Azure Cloud Shell command prompt, one at a time:

### Create a Resource Group
1. Create a variable that contains a resource group name
```
resourceGroupName="mgmt_59000_func_hello_world"
```

2. Use the Azure CLI to create a new resource group with the name you just defined.
```
az group create --name "${resourceGroupName}" --location eastus
```

### Create a Storage Account
3. Create a variable that contains YOUR Purdue career account username (this will help us make a unique storage account name)
    * Only use lower-case letters
```
careerAccount="YOURCAREERACCOUNT"
```
```{tip}
For example, I would input the following command:
`careerAccount="elliot62"`
```

4. Create a variable that holds a globally unique storage account name
```
storageAccountName="hw${careerAccount}$(date +%s)"
echo "Your globally unique Storage Account is: ${storageAccountName}"
```

5. Use the Azure CLI to create a new storage account inside the resource group you just created
```
az storage account create --resource-group "${resourceGroupName}" --name "${storageAccountName}" --location eastus --sku Standard_LRS --kind StorageV2
```

### Create the Cloud Function App
6. Create a variable that holds a random identifier
```
randomIdentifier=$(openssl rand -hex 4)
```
7. Create a unique name for the function using the random identifer
```
functionAppName="hello-world-${randomIdentifier}"
echo "Function App name: $functionAppName"
```

8. Finally, use the following command to create a new Cloud Function using all the settings you defined above.
```
az functionapp create \
    --resource-group "${resourceGroupName}" \
    --name "${functionAppName}" \
    --storage-account ${storageAccountName} \
    --runtime python \
    --runtime-version 3.11 \
    --os-type linux \
    --consumption-plan-location eastus \
    --functions-version 4
```

Once this finishes running, your app will be created on Azure. However, it is *not yet publicly available*.

9. Publish the app
```
func azure functionapp publish "${functionAppName}"
```


## Test Your Remote Application

After publishing, you should receive a confirmation message that contains a URL. 

1. Copy this URL and put it in a new browser tab. 
    * You should see the default Cloud Function message

Test the function by viewing a customized response to your custom input. You need to add a querystring parameter and argument to pass data into the function.

2. Append `?name=Fred` at the end of the URL and see the change in the response in the browser window
    * Your app is now accepting input and returning output
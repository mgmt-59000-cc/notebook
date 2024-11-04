# Write the Function Code
You are now ready to write the function code and see it run when a file is uploaded to your storage account.

## Create the files for the function
Move into the working directory that will store your function's source code:

```
cd ~/clouddrive/blob_storage/function
```

### Initialize a new function
On the command line, initialize a new function:

```
func init
```

### Add boilerplate code to the function
Now customize the function code so it is triggered by Blob storage:

```
func new --name "process_order"
```

* The trigger is `Blob trigger`
* The container path is `inbox`
* Leave the Storage Account Connection String to the default

### View the Boilerplate Code
Open the code with the command:

```
code .
```

In `function_app.py` note that the **path** is set to `inbox`. Your function will watch this container for files.

The container will be in your "input" Storage Account that you created earlier. We must create a connection between the storage account and your function.

## Connect Your App to Your Storage
Even though

### Get the Connection String for the Storage Account that our function app will "watch" for new files

* Go to Azure portal to get the connection string for **input** storage account
    * Find the storage account with the name that begins with `input...` and click the name
    * In the left navigation, find and expand `Security + networking`
    * Click `Access keys`
    * Click the `Show` button beside the Connection string for key1
    * Copy the value of the Connection string
* In your Cloud Shell editor, open the `local.settings.json` file
* In `Values`, add a key for `BlobStorageConnectionString` and paste in the value of the connection string you just copied from the Azure portal

Your function now has the security permission to "watch" the input storage account.

### Get the Connection String for the Storage Account that will hold the source code for the function app
* Go to Azure portal to get the connection string for **source** storage account
    * Find the storage account with the name that begins with `source...` and click the name
    * In the left navigation, find and expand `Security + networking`
    * Click `Access keys`
    * Click the `Show` button beside the Connection string for key1
    * Copy the value of the Connection string
* In your Cloud Shell editor, open the `local.settings.json` file
* In `Values`, update the key `AzureWebJobsStorage` and paste in the value of the connection string you just copied from the Azure portal

## Download the support scripts to help set up your storage account
I've created a few script files that will help you setup (and cleanup) your storage accounts while you test this project.

I've also included a script that will generate data for you to use while running your function.

```
cd ~/clouddrive/blob_storage
git clone https://github.com/mgmt-59000-cc/bs_support
chmod +x bs_support/*.sh
```

## Create containers for the blobs we will manipulate with the function
I've written a script that will create the containers you need inside your input storage account. Run this script with the following command:

```
./bs_support/setup_containers.sh "${inputStorageAccountName}" "${resourceGroupName}"
```

View your input storage container on the Azure portal. 
* Click `Storage browser` in the left navigation
* Click `Blob containers` from the dashbboard
* Note that you now have containers (subdirectories) titled `inbox`, `east`, `west`, and `central`

## Test the function "locally"
Run the function from Cloud Shell with the following command:
```
cd ~/clouddrive/blob_storage/function
func host start
```

* Go to the browser and find the `input` storage account
* Go to the storage browser and then the `inbox` container 
* Upload any file from your computer 
* Watch the output from your running function in the Cloud Shell

Watch the output from the function app to see it trigger when a file is uploaded.

```{tip}
To stop the function app from running, press `Ctrl+C` on your keyboard. (You may need to do this two or three times.)
```

## Clean Up Storage Account Containers
I have written a script for you that will automatically delete blobs from your storage containers. You can use this whenever you are ready to test your function with empty containers.

Run this function with the following command:

```
~/clouddrive/blob_storage/bs_support/cleanup_containers.sh "${inputStorageAccountName}" "${resourceGroupName}"
```

## Publish the function on Azure
Now that you've tested the function, it's time to publish it on Azure. This means that your function will continuously watch for files uploaded to the `inbox` container of your input storage account.

Publish with the following command:
```
func azure functionapp publish "${functionAppName}"
```

## Add Connection String to Function on Azure
Just as you had to add the connection string to the storage account when you were running your function locally, you need to do the same for your function running on the Azure platform.

* In the Azure Portal, go to your Function App page
* In the left navigation, expand `Settings` and click on `Environment variables`
* Click `+ Add` and create a new variable with the name `BlobStorageConnectionString`
* For the value, paste in the value of the connection string stored in your `local.settings.json` file

## Set Up Permissions Between Your App and the Storage Account
Finally, you must give your Azure-based app permission to read and write files within your storage account.

First, you need to store your subscription ID in a variable:

```
subscriptionId=$(az account show --query id --output tsv)
```

You'll also need to create a managed identity (a service account, or a "fake user") who has permission to interact with your resources:

```
az functionapp identity assign --name "${functionAppName}" --resource-group "${resourceGroupName}"
```

Capture the ID of that managed identity in a variable:

```
functionId=$(az functionapp identity show --name "${functionAppName}" --resource-group "${resourceGroupName}" --query principalId --output tsv)
```

Now you must assign your function the roles of **reader** and **contributor**.

```
az role assignment create \
    --assignee $functionId \
    --role "Storage Blob Data Reader" \
    --scope "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$inputStorageAccountName"
```

```
az role assignment create \
    --assignee $functionId \
    --role "Storage Blob Data Contributor" \
    --scope "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$inputStorageAccountName"
```
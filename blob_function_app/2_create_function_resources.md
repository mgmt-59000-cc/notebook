# Create Function Resources
Start the project by creating the resources required: a resource group, a function app, and two storage accounts.

## Create a working directory on Cloud Shell
In Azure Cloud Shell, prepare your working directory.

```
mkdir ~/clouddrive/blob_storage
mkdir ~/clouddrive/blob_storage/function
cd ~/clouddrive/blob_storage
```

## Create a new Resource Group
Create a new resource group on Azure that will hold all the resources for this project.

```
resourceGroupName="blob_storage_function"
az group create --name "${resourceGroupName}" --location eastus
```

## Create a storage account for the function's source code
You need two storage accounts for this project: one for the project's source code, and one for the files that will be processed by the function.

Create the "source" storage account with these commands:

```
randomIdentifier=$(openssl rand -hex 4)
sourceStorageAccountName="source${randomIdentifier}"
echo "Your function's source files will be stored in: ${sourceStorageAccountName}"
az storage account create --resource-group "${resourceGroupName}" --name "${sourceStorageAccountName}" --location eastus --sku Standard_LRS --kind StorageV2
```

## Create a unique name for the function using the random identifer

Your function name must be unique, so use a randomizer to help create a new function app name.

```
functionAppName="process-order-${randomIdentifier}"
echo "Function App name: $functionAppName"
```

## Create a Function App on Azure
Use the resources you just created to create the function app on the Azure platform.

```
az functionapp create \
    --resource-group "${resourceGroupName}" \
    --name "${functionAppName}" \
    --storage-account "${sourceStorageAccountName}" \
    --runtime python \
    --runtime-version 3.11 \
    --os-type linux \
    --consumption-plan-location eastus \
    --functions-version 4
```

## Create a second storage account: This is where the function will watch for new files
As noted, you need a **second** storage account in your resource group. This is what your function will "watch" for new files.

```
inputStorageAccountName="input${randomIdentifier}"
echo "Your function's input files will be stored in: ${inputStorageAccountName}"
az storage account create --resource-group "${resourceGroupName}" --name "${inputStorageAccountName}" --location eastus --sku Standard_LRS --kind StorageV2
```
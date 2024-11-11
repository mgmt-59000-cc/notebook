# Continuing Work on Your Function
If you leave cloud shell and need to come back to finish working on your function, you'll need to first set local variables for several features of your project.

You can find these values in the Azure portal on each resource's page.

1. Find and set the value for your resource group
```
resourceGroupName=
```

2. Find and set the value for your "input" storage account
```
inputStorageAccountName=
```

3. Find and set the value for your function app name
```
functionAppName=
```

## Use the scripts for testing

As a reminder, there are several scripts that will help you test your function:

* Clear all files from the `inbox`, `east`, `west`, and `central` containers
```
~/clouddrive/blob_storage/bs_support/cleanup_containers.sh "${inputStorageAccountName}" "${resourceGroupName}"
```

* Generate new sample orders (replace the number at the end with the number of files to create)
```
python ~/clouddrive/blob_storage/bs_support/generate_orders.py -n 10
```

* Upload all your sample orders to the `inbox` for sorting
```
az storage blob upload-batch --account-name "${inputStorageAccountName}" --destination inbox --source ~/clouddrive/blob_storage/bs_support/sample_orders --auth-mode key
```
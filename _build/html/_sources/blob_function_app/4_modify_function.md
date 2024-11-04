# Modify the Function to Copy Files
You'll now update the function's source code so that it has the ability to move files from the `inbox` to one of the other containers you've created.

## Install Python package
We'll need to install another support package from Python to allow us to move files within our storage account.

On the command line, install the package with the following command:
```
pip install azure-storage-blob
```

Update the `requirements.txt` to include a reference to the Python package. Add the line:

```
azure-storage-blob
```

Ensure your `function_app.py` file also imports the package. At the top of the file, include the line:

```
from azure.storage.blob import BlobServiceClient, BlobClient, ContainerClient
```

You will also need some additional built-in Python packages, so also add the following lines to the top of your `function_app.py` file:

```
import csv
import io
import os
```

## Add Python Code
In the `function_app.py` file, **delete** or **comment out** the contents of the file **after** the line that begins `def process_order...`

Replace the contents of the file with the following:
```
    logging.warning(f"Processing blob: {myblob.name}, Size: {myblob.length} bytes")

    # Read the CSV file from the InputStream
    csv_content = myblob.read().decode('utf-8')
    csv_reader = csv.reader(io.StringIO(csv_content))
    rows = list(csv_reader) # Store the values of the CSV rows in a variable called "rows"
    first_row = rows[1] if len(rows) > 1 else [] # Get the value of the first data row (skipping the header row)

    logging.warning(f"First row: {first_row}")
```

## Publish Your Function's Changes
Move the new code for your function to Azure with the following command:
```
func azure functionapp publish "${functionAppName}"
```

## Create Sample Order File
I've written a Python program for you that will generate some fake order files. Generate a single order file with the following command:

```
python ~/clouddrive/blob_storage/bs_support/generate_orders.py -n 1
```

You can view the file that was created with this command:

```
ls ~/clouddrive/blob_storage/bs_support/sample_orders
```

## Upload Sample Order File(s)
Azure CLI has a built-in command that will upload multiple files into a Storage Account container. You'll use it to upload your auto-generated sample orders into your `inbox` container we previously created.

```
az storage blob upload-batch --account-name "${inputStorageAccountName}" --destination inbox --source ~/clouddrive/blob_storage/bs_support/sample_orders --auth-mode key
```

## Test With Multiple Orders
Your function will now run one time for each file uploaded to your `inbox` container. Let's test this by uploading more than one file.

First, clean out all existing files from the containers:
```
~/clouddrive/blob_storage/bs_support/cleanup_containers.sh "${inputStorageAccountName}" "${resourceGroupName}"
```

Then generate 10 new order files using the Python script:
```
python ~/clouddrive/blob_storage/bs_support/generate_orders.py -n 10
```

Upload all the orders as a single batch to the `inbox`:
```
az storage blob upload-batch --account-name "${inputStorageAccountName}" --destination inbox --source ~/clouddrive/blob_storage/bs_support/sample_orders --auth-mode key
```

You can now see that your files are uploading and each one triggers the logic of the function.
# Moving Files from One Container to Another
Your function is live and working but doesn't *do* anything with the imported files.

You'll add more logic to your function's Python code that will move the files from the `inbox` to the `central` container in the storage account.

## Update Function Code
In the `function_app.py` file, **delete** the contents and replace them with the following:
```
import azure.functions as func
import datetime
import json
import logging
import csv
import io
import os
from azure.storage.blob import BlobServiceClient

def copy_blob(connection_string, source_container, source_blob_name,
            dest_container, dest_blob_name):
   try:
       # Create blob service client
       blob_service_client = BlobServiceClient.from_connection_string(connection_string)
       
       # Get source container client and source blob
       source_container_client = blob_service_client.get_container_client(source_container)
       source_blob = source_container_client.get_blob_client(source_blob_name)

       # Get destination container client and destination blob 
       dest_container_client = blob_service_client.get_container_client(dest_container)
       dest_blob = dest_container_client.get_blob_client(dest_blob_name)

       # Download source blob content
       source_content = source_blob.download_blob()

       # Upload to destination
       dest_blob.upload_blob(source_content.readall(), overwrite=True)
       
       # Delete the source blob after successful copy
       source_blob.delete_blob()
       
       print(f"Successfully copied {source_blob_name} to {dest_container}/{dest_blob_name}")
       
   except Exception as e:
       print(f"Error copying blob: {str(e)}")
       raise

app = func.FunctionApp()

@app.blob_trigger(arg_name="myblob", path="inbox/{name}",
                               connection="BlobStorageConnectionString") 
def process_order(myblob: func.InputStream):

    the_file_name = myblob.name.split('/')[1]

    # Read the CSV file from the InputStream
    csv_content = myblob.read().decode('utf-8')
    csv_reader = csv.reader(io.StringIO(csv_content))
    rows = list(csv_reader) # Store the values of the CSV rows in a variable called "rows"
    first_row = rows[1] if len(rows) > 1 else [] # Get the value of the first data row (skipping the header row)

    logging.warning(f"First row: {first_row}")

    connection_string = os.getenv("BlobStorageConnectionString")
    copy_blob(
        connection_string=connection_string,
        source_container="inbox",
        source_blob_name=the_file_name, 
        dest_container="central",
        dest_blob_name=the_file_name
    )
```

## Update Dependencies
In the `requirements.txt` file, **delete** the contents and replace them with the following:

```
azure-functions
azure-storage-blob
```

## Re-Publish the Function
Move your updated code to Azure.

Publish with the following command:
```
func azure functionapp publish "${functionAppName}"
```

## Test the Newest Version of the Function

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
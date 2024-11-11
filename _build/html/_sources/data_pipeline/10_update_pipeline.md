# Update the Pipeline to Delete Used Files
You need to add a 2nd stage to your pipeline to delete the CSV file from the source when the process is completed. This will keep your storage **inbox** from becoming too cluttered.

## Delete Your Data
1. In your SQL database, execute the following query to remove the data from your database table:

```
TRUNCATE TABLE dbo.orders;
```

## Delete Your Source Files
1. In your Storage Account, go to the `inbox` container and delete all files

## Add a New Pipeline Stage
1. In Data Factory Studio, go to the Pipeline Orchestration screen
2. In the 'Activities' panel, search for `delete`
3. Drag the Delete tile into the pipeline work area
4. Connect the 'Copy data' stage to the 'Delete' stage by dragging an arrow from the green checkmark on 'Copy data' to 'Delete'

## Configure the Delete Stage
1. Click on the Delete tile
2. Click the **Source** tab in the Settings panel
3. For 'Dataset', choose `DelimitedText1`
4. Under 'Dataset properties', find the 'filePath' parameter. For 'Value', enter `@pipeline().parameters.filePath`
5. UNCHECK the checkbox next to 'Recursively'
6. Click the **Logging settings** tab
7. Uncheck 'Enable logging'

## Publish Your Pipeline
1. From the top of Data Factory Studio, click **Publish all...**

## Test Your Pipeline
1. In your Storage Account, go to the `inbox` container and upload a single CSV file
2. Wait for the pipeline to run, then view your data in your SQL database
3. Refresh your Storage account to confirm the CSV file you uploaded is no longer there

## Test Your Pipeline with Multiple Files
1. In your Storage Account, go to the `inbox` container and upload multiple CSV files
2. Wait for the pipeline to run, then view your data in your SQL database
3. Refresh your Storage account to confirm the CSV files you uploaded are no longer there
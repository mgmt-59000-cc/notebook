# Create the Pipeline
Use your Azure Data Factory to create the pipeline that will move data from flat files in Blob Storage to your SQL database.

```{important}
You **MUST** use Microsoft Edge or Google Chrome for this part of this tutorial!
```

1. From the Data Factory Studio home page, click **Orchestrate**
2. In the 'Parameters' tab of the settings panel, click **+ New**
3. For the Name of your parameter, enter `filePath`
4. In the 'Activities' panel, search for `Copy data`
5. Drag 'Copy data' from the panel into the pipeline work area
6. Click the 'Copy data' tile to see the settings panel beneath the work area
7. In the settings panel, click **Source**
8. Next to 'Source dataset', click **+ New**

## Create a Source Dataset
1. Choose `Azure Blob Storage` from the list of sources
2. Click **Continue**
3. Choose `DelimitedText` for the format
4. Click **Continue**
5. Under 'Linked service', click **+ New**

## Create a Data Source Linked Service
1. Find 'Azure subscription' and choose your Azure subscription (`Azure for Students...`)
2. For 'Storage account name', choose your storage account you created in a previous step (e.g. `elliottpipelinetutorial`)
3. At the bottom of the panel, click **Test connection**
4. When your test passes, click **Create**

## Configure the Data Source Linked Service
1. From the 'Set properties' panel, click the **Browse** (📁) button
2. Click `inbox`
3. For 'File name' enter `@dataset().filePath`
4. Click **OK**
5. Expand the 'Advanced' option and click **Open this dataset**
6. Choose the 'Parameters' tab in the dataset settings
7. Click **+ New**
8. For 'Name' enter `filePath`
9. For 'Default value' enter `@dataset().filePath`
10. Return to the **pipeline1** tab in the pipeline editor
11. Still in the 'Source' tab of the settings panel, note the parameter **filePath** appears
12. For 'Value', enter `@pipeline().parameters.filePath`
13. Uncheck the checkbox for 'Recursively'

## Configure the Sink for the Pipeline
1. Click the **Sink** tab in the pipeline settings panel
2. For 'Sink dataset', click **+ New**
3. In the 'New dataset' panel, search for `SQL` and choose `Azure SQL Database`
4. Click **Continue**
5. For 'Linked service', click **+ New**

## Configure the Data Sink Linked Service
1. Find 'Azure subscription' and choose your Azure subscription (`Azure for Students...`)
2. For 'Server name', choose your database server you created in a previous step (e.g. `elliott-data-sink`)
3. For 'Database name', choose your database server you created in a previous step (e.g. `data_sink`)
4. For 'Authentication type', choose `SQL authentication`
5. For 'Username', enter `azureadmin`
6. For 'Password', enter the password you created in a previous step
7. At the bottom of the panel, click **Test connection**
8. When your test passes, click **Create**
9. From the 'Set properties' panel: 
    * For 'Table name', choose `dbo.orders`
    * Click 'OK'

## Publish the Pipeline
1. Finally, click the **Publish all** button at the top of the screen to publish your pipeline, then click **Publish**
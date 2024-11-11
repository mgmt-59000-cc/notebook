# Create a Pipeline Trigger
You will now set your pipeline to trigger whenever new files are added to your Blob Storage.

1. In Data Factory Studio, choose **Add trigger**
2. Choose **New/Edit**
3. For 'Choose trigger...' choose **+ New**
4. For 'Type', choose **Storage events**
5. Find 'Azure subscription' and choose your Azure subscription (`Azure for Students...`)
6. For 'Storage account name', choose your storage account you created in a previous step (e.g. `elliottpipelinetutorial`)
7. For 'Container name', enter `/inbox/`
8. For 'Blob path ends with', enter `.csv`
9. For 'Event', choose **Blob created**
10. Click **Continue**
11. On the Data preview panel, click **Continue**
12. On the 'Trigger Run Parameters' panel, for Value, enter the following:
```
@triggerBody().fileName
```
13. On the New trigger panel, click **OK**
14. From Data Factory Studio, click **Publish all** at the top to make the changes to your pipeline, then click **Publish**

## Test Your Trigger
1. Return to the Azure Portal and upload ANY SINGLE CSV file to your Storage Account container as you did before
2. You can monitor your pipeline in Data Factory Studio
3. When your pipeline run has finished, return to your SQL database and query the data as you did in a previous step
4. You should see the new data in your database table
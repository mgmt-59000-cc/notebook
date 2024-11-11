# Test the Pipeline
Your data source, data sink, and pipeline are all created and connected. Run the pipeline manually to test it.

## Upload a Single Order
1. Download a .zip file of sample orders from [this repository](https://github.com/mgmt-59000-cc/pipeline_tutorial)
2. Unzip the file on your local computer
3. In the Azure portal, go to Home and into the Storage Account you created for this tutorial (e.g. `elliottpipelinetutorial`)
4. Click **Storage browser**, then **Blob containers**, then **inbox**
5. Use the **⬆️ Upload** button and upload the file named `1234test.csv` from the sample orders to your Storage Account

## Manually Trigger the Pipeline
1. In Azure Data Factory Studio, click **Add trigger**
2. Click **Trigger now**
3. For the 'filePath' parameter, enter `1234test.csv`
4. Click **OK**

## Review the Results
If your pipeline ran successfully, you should have data in your database table.

1. In Azure Portal, from the Home page choose your SQL database (e.g. `data_sink`)
2. Click the **Query editor (preview)**
3. Expand the 'Tables' folder and click the three dots (...) next to **dbo.orders**
4. Click **Select Top 1000 Rows**
5. Review your data in the table
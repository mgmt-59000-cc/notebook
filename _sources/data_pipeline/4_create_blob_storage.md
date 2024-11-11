# Create Blob Storage
You will store your collected data in Blob Storage to prepare for ingestion into your pipeline.

1. From the hamburger (navigation) menu, choose **All services**
2. Click **Storage** then **Storage accounts**
3. Click **+ Create**
4. Choose your Subscription
5. For 'Resource group' choose `data_pipeline_tutorial`
6. For 'Storage account name', create a *globally unique* storage account name (e.g. `elliottpipelinetutorial`)
7. For 'Region' choose `(US) East US`
8. For 'Primary service' choose `Azure Blob Storage or Azure Data Lake Storage Gen 2`
9. For 'Redundancy' choose `Locally-redundant storage (LRS)`
10. Click the **Review + create** button, then click **Create**
11. Wait for the resource to be created

## Create a Blob Container
1. From the home page of the Storage Account, click **Storage browser**
2. Click **Blob containers**
3. Click **+ Add container**
4. For 'Name', enter `inbox`
5. Click **Create**
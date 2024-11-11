# Create an SQL Database
You will create a SaaS database on Azure that will hold the data processed by your pipeline. This database will be your *sink*.

## Create the Database
1. From the hamburger (navigation) menu, choose **All services**
2. Click **Databases** then **SQL databases**
3. Click **+ Create**

```{tip}
You will likely see a purple box that asks if you want to try SQL Database for free. If so, click **Apply Offer (Preview)**.
```

4. On the **Basics** tab, do the following:
    * Ensure your Subscription is set
    * For 'Resource group', choose `data_pipeline_tutorial`
    * For 'Database name', enter `data_sink`
    * Under Server, click **Create new**

5. On the **Create SQL Database Server** page, do the following:
    * For 'Server name', add a *globally unique* name (e.g. `elliott-data-sink`)
    * For 'Location', choose `(US) East US 2`
    * For 'Authentication method', choose `Use SQL authentication`
    * For 'Server admin login', enter `azureadmin`
    * Enter and confirm a password of your choice
    * Click **OK**

6. Back on the **Basics** tab, do the following:
    * (If this question appearst) For 'Want to use SQL elastic pool?' choose **No**
    * (If this option appearst) For 'Workload environment' choose **Development**
    * Click the **Next: Networking >** button

7. On the **Networking** tab, do the following:
    * For 'Connectivity method' choose **Public endpoint**
    * Under 'Firewall rules' choose **Yes** for both 'Allow Azure services...' and 'Add current client IP address'
    * At the bottom of the page, click **Review + create**, then click **Create**
# Build a Data Pipeline in Azure
This exercise will show you how to combine Blob Storage, Data Factory, and SQL Server to build a data pipeline that moves data from flat files into a relational database.

All work in this exercise will occur in the Azure Portal.

```{important}
You **MUST** use Microsoft Edge or Google Chrome for part of this tutorial. Certain parts *will not work* in other browsers!
```

## Register EventGrid
Enable the EventGrid on you Azure subscription.
1. Go to **Home** > **Subscriptions**
2. Under **Settings** > **Resource providers** search for **Microsoft.EventGrid**
3. Check the box next to **Microsoft.EventGrid** and click **Register**
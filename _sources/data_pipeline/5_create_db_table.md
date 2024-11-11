# Create a Database Table
Your database should be deployed. Use it to create a database table that will hold the data processed by your pipeline.

1. From the Home page, click your **data_sink** database
    * If your database does not appear, click **All service** > **SQL databases** > `data_sink`
2. Click **Query editor (preview)**
3. Log in with the credentials you created in a previous step
4. Copy the query below to create an `orders` table in your database

```
CREATE TABLE dbo.orders
(
    ID int IDENTITY(1,1) NOT NULL,
    order_id varchar(50),
    timestamp varchar(50), 
    order_type varchar(50),
    customer_id varchar(50),
    shipping_state varchar(50),
    product_name varchar(50),
    product_category varchar(50),
    quantity int,
    unit_price numeric(10,2),
    total_amount numeric(10,2),
    assigned_warehouse varchar(50),
    shipping_priority varchar(50)
)
GO

CREATE CLUSTERED INDEX IX_order_ID ON dbo.orders (ID);
```

5. Click **▶️ Run**
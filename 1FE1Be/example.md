## 创建表
    
```sql
    CREATE TABLE IF NOT EXISTS load_local_file_test
    (
        id INT,
        age TINYINT,
        name VARCHAR(50)
    )
    unique key(id)
    DISTRIBUTED BY HASH(id) BUCKETS 3
    properties(
        "replication_num"="1"
    );


    CREATE TABLE demo_sales_data (
        product_id INT,
        sale_date DATEV2,
        category VARCHAR(255) REPLACE,
        sales_amount INT SUM
    )
    AGGREGATE KEY (product_id,sale_date)
    DISTRIBUTED BY HASH(product_id) BUCKETS 3
    PROPERTIES (
        "storage_type" = "COLUMN",
        "replication_num" = "1"
    );

以 product, sale_date 为聚合键，以 product_id 为分布键，分布到 3 个桶中。
当 product_id,sale_date 相同时，category 会被替换，sales_amount 会被累加。
```
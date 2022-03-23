# 17 Creating and Manipulating Tables

# 17.1 Basic Table Creation

```sql
CREATE TABLE Products
(
	prod_id     CHAR(10)       NOT NULL,
  vend_id     CHAR(10)       NOT NULL,
	prod_name   CHAR(245)      NOT NULL,
	prod_price  DECIMAL(8,2)   NOT NULL,
	prod_desc   VARCHAR(1000)  NULL  -- NULL is default, no need to type out
);
```

```sql
CREATE TABLE Orders
(
	order_num     INTEGER       NOT NULL,
	order_date    DATETIME      NOT NULL,
	cust_id       CHAR(10)      NOT NULL 
);
```

# 17.2 Specifying Default Values

```sql
CREATE TABLE OrderItems
(
	order_num    INTEGER     NOT NULL,
	quantity     INTEGER     NOT NULL DEFAULT 1,
);
```

# 17.3 Updating Tables

To update table definitions, you use the ALTER TABLE statement. 

- NOTE
    1. ideally, tables should never be altered after they contain data.
    2. You can add column, rename column, and others.

```sql
ALTER TABLE Vendors
ADD vend_phone CHAR(20);
```

Complex table structure changes usually require a manual move process:

1. Create a new table with the new column layout.
2. Use INSERT SELECT statement to copy the data from the old table to the new table
3. Verify that the new table contains the desired data
4. Rename the old table or delete it 
5. Rename the new table with the name previously used by the old table
6. Re-create any triggers, stored procedures, indexes, and foreign keys as need. 

# 17.4 Deleting Tables

```sql
DROP TABLE CustCopy;

# NO UN-DO!
```
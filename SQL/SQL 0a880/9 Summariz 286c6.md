# 9 Summarizing Data

# 9.1 Using Aggregate Functions

Want a summary of the data, not data itself.

```sql
/*
AVG ()         
COUNT ()       
MAX ()        
MIN ()        
SUM ()
*/
```

## 9.1.1 `AVG()` Function

May only be used to determine the average of a specific numeric column.

Column rows containing `NULL` values are ignored by the `AVG()` function.

```sql
SELECT AVG (prod_price) AS avg_price
FROM Products
WHERE vend_id = 'DLL01';
```

## 9.1.2 `COUNT()` Function

COUNT() can be used two ways:

1. `COUNT (*)` to count the number of rows in a table, whether columns contain values or `NULL` values.
2. `COUNT (column)` to count the number of rows that have values in a specific column, ignoring `NULL` values. 

```sql
SELECT COUNT (*) AS num_cust
FROM Customers;
```

```sql
SELECT COUNT (cust_email) AS num_cust
FROM Customers;
```

## 9.1.3 `MAX()` and `MIN()` Functions

Ignore `NULL` values.

Requires the column name be specified.

Can be used in textual columns: `MAX()` returns the last row data, `MIN()` returns the first row data.

## 9.1.4 `SUM()` Function

Can calculate the sum(total) of the values in a specific column.

Can also calculate the total values.

# 9.2 Aggregates on Distinct Values

`ALL` is default.

`DISTINCT` needs to be specified if needed.

```sql
SELECT AVG (DISTINCT prod_price) AS avg_price
FROM Products
WHERE vend_id = 'DLL01';
```

- NOTE
    1. NO `DISTINCT` with `COUNT(*)`
    2. NO value in using `DISTINCT` with `MAX()` or `MIN()`
    3. Some DBMSs support `TOP` and `TOP PERCENT` 

# 9.3 Combing Aggregate Functions

```sql
SELECT COUNT(*) AS num_items,
MIN (prod_price) AS price_min,
MAX (prod_price) AS price_max,
AVG (prod_price) AS price_avg
FROM Products;
```
# 3 Sorting Retrieved Data

# 3.1 Sorting

```sql
SELECT prod_name
FROM Products
ORDER BY prod_name;

SELECT prod_price
FROM Products
ORDER BY prod_price DESC; --descending order

```

```sql
#Multiple Columns
SELECT prod_id, prod_price, prod_name
FROM Products
ORDER BY prod_price,prod_name;

--same as
SELECT prod_id, prod_price, prod_name
FROM Products
ORDER BY 2,3;

```
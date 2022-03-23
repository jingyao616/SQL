# 2 Retrieving Data

# 2.1 Select

```sql
# use of distinct 
SELECT DISTINCT vend_id
FROM Product;

```

```sql
SELECT prod_name
FROM Products
LIMIT 3,5; -- first number is offset, and second number is limit

```

# 2.2 Comment out

```sql
/* abcde
abcdefg*/

# abcde
-- abcde

```
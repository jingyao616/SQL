# 14 Combining Queries

# 14.1 Creating Combined Queries

## 14.1.1 Using `UNION`

`UNION` instructs the DBMS to execute both `SELECT` statements and combine the output into a single query result set. 

```sql
SELECT cust_name, cust_contact, cust_email
FROM Customers
WHERE cust_state IN ('IL', 'IN', 'MI')

UNION

SELECT cust_name, cust_contact, cust_email
FROM Customers
WHERE cust_name = 'FUN4A11';
```

- NOTE
    1. Each query in a UNION must contain the same columns, expressions, or aggregate functions.
    2. Column datatypes must be compatible. They need not be the same name or the exact same type, but they must be of a type that the DBMS can implicitly convert. 
    3. By default, `UNION` will remove any duplicate rows, but can change by using `UNION ALL` instead of `UNION`. 

# 14.2 Sorting Combined Query Results

Can only use one `ORDER BY`, at the very end.

# 14.3 Challenges

Write a SQL statement which returns and combines product name (prod_name) from Products and customer name (cust_name) from Customers, and sort the result by product name.

```sql
SELECT prod_name
FROM Products
UNION
SELECT cust_name
FROM Customers
ORDER BY prod_name;
```

This will combine all prod_name and cust_name together, under a title prod_name.

This is a little nonsensical, I know, but it does reinforce a note earlier in this lesson. Must have same column title when use UNION, otherwise it will combine them all.
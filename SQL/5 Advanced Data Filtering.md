# 5 Advanced Data Filtering

# 5.1 using the `AND` and `OR` operator

```sql
SELECT prod_id, prod_price, prod_name
FROM Products
WHERE vend_id = 'DLL01' AND prod_price <=4;

```

```sql
SELECT prod_id, prod_price, prod_name
FROM Products
WHERE vend_id = 'DLL01' OR vend_id = 'BRS01';
```

## 5.1.1 Order matters

SQL processes `AND` operators **before** `OR` operators. 

**ALWAYS** Use parentheses. 

```sql
SELECT prod_price, prod_name
FROM Products
WHERE (vend_id = 'DLL01' OR vend_id = 'BRS01') 
			AND prod_price >=10;
```

# 5.2 using the `IN` operator

```sql
SELECT prod_price, prod_name
FROM Products
WHERE vend_id IN ('DLL01' ,'BRS01') 

/* Same as OR operator:
WHERE vend_id = 'DLL01' OR vend_id = 'BRS01' */
```

## 5.2.1 Advantage of `IN`

- easy to read
- easy to use with other AND and OR
- more quickly
- can contain another SELECT statement

# 5.3 using the `NOT` operator

```sql
SELECT prod_name
FROM Products
WHERE NOT vend_id = 'DLL01'; 

/* Same as <> operator:
WHERE vend_id <> 'DLL01' */
```
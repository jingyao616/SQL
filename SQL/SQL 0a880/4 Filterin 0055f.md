# 4 Filtering Data

# 4.1 WHERE - clause operators

```sql
=     Equality
<>    Nonequality
!=    Nonequality
<
<=
!<    Not less than
Between
is null 
```

# 4.2 Checking for Non-matches

```sql
SELECT vend_id, prod_name
FROM Products 
WHERE vend_id <> 'DLL01';
# same as use != 
```

# 4.2 Checking for a Range

```sql
SELECT prod_price, prod_name
FROM Products 
WHERE prod_price BETWEEN 5 AND 10;
```

# 4.3 Checking for No value

```sql
SELECT prod_name
FROM Products 
WHERE prod_price IS NULL;

# Must use "IS NULL", can't use = Null
```
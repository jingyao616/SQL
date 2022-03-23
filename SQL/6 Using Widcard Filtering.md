# 6 Using Wildcard Filtering

# 6.1 using the `LIKE`  operator

To use wildcards in search clauses, you must use the `LIKE` operator. `LIKE` instructs the DBMS that the following search pattern is to be compared using a wildcard match rather than a straight equality match. 

## 6.1.1 `%`

Wildcard searching can only be used with text fields (strings); you can't use wildcards to search fields of non-text datatypes. 

```sql
SELECT prod_id, prod_name
FROM Products

WHERE prod_name LIKE 'FISH%';  
WHERE prod_name LIKE '%bean bag%';
WHERE prod_name LIKE 'F%y'; -- eg. looking for email addresses WHERE email LIKE 'b%@forta.com'1';
```

## 6.1.2 `_`  underscore

Matches only single character.

```sql
SELECT prod_id, prod_name
FROM Products

WHERE prod_name LIKE '_ inch teddy bear';  
```

```sql
SELECT prod_id, prod_name
FROM Products

WHERE prod_name LIKE '% inch teddy bear';  
```

## 6.1.3 `[]` brackets

MySQL doesn't support.
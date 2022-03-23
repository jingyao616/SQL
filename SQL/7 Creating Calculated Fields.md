# 7 Creating Calculated Fields

# 7.1 Concatenating Fields

Joining values together to form a single long value.

MySQL use `Concat`

```sql
SELECT Concat (vend_name, '(', vend_country,')' )
FROM Vendors
ORDER BY vend_name
```

## 7.1.1 Alias

Nick name for a column  

```sql
SELECT Concat (vend_name, '(', vend_country,')' ) 
AS vend_title

FROM Vendors
ORDER BY vend_name
```

# 7.2 Mathematical Calculation

```sql
SELECT prod_id, 
			quantity, 
			item_price, 
			**quantity*item_price AS expanded_price**

FROM OrderItems
WHERE Order_num = 20008;
```
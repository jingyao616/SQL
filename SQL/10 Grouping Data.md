# 10 Grouping Data

# 10.1 Creating Groups

Grouping lets you divide data into logical sets so that you can perform aggregate calculations on each group.

```sql
SELECT vend_id, COUNT(*) AS num_prods
FROM Products
GROUP BY vend_id;
```

The `GROUP BY` clause instructs the DBMS to group the data and then perform the aggregate on each group rather than on the entire result set. 

- NOTE
    1. `GROUP BY` can contain as many columns as you want.
    2. All the columns specified are evaluated together when grouping is established.
    3. If an expression is used in the `SELECT` ,that same  expression must be specified in `GROUP BY`. **Aliases cannot be used**.
    4. Aside from the aggregate calculation statements , every column in your `SELECT` statement must be present in the `GROUP BY` clause.
    5. All rows with `NULL` values will be grouped  together.
    6. `GROUP BY` clause must come after any `WHERE` clause and before any `ORDER BY` clause 

# 10.2 Filtering Groups use `HAVING`

`WHERE` filters specific rows, where `HAVING` filters groups.

```sql
SELECT cust_id, COUNT(*) AS orders
FROM Orders
GROUP BY cust_id
HAVING COUNT(*) >=2;
```

<aside>
❗ `WHERE` filters before data is grouped, and `HAVING` filters after data is grouped. Rows that are eliminated by a `WHERE` clause will not be included in the group.

</aside>

```sql
# Example when WHERE and HAVING are used together.
SELECT vend_id, COUNT(*) AS num_prods
FROM Products
WHERE prod_price >=4
GROUP BY vend_id
HAVING COUNT(*) >=2;
```

# 10.3 Grouping and Sorting

`GROUP BY` is required if using column or expressions with aggregate functions.

Always remember to use `ORDER BY` if used `GROUP BY`

```sql
SELECT order_num, COUNT(*) AS items
FROM OrderItems
GROUP BY order_num
HAVING COUNT(*) >=3;
```

```sql
SELECT order_num, COUNT(*) AS items
FROM OrderItems
GROUP BY order_num
HAVING COUNT(*) >=3
ORDER BY items;
```

<aside>
💡 Eg. 1: It’s important to identify the best customers, so write a SQL statement to return the order number (order_num in OrderItems table) for all orders of at least 100 items.

</aside>

```sql
SELECT order_num  # Here we don't have to select SUM(quantity)
FROM OrderItems
GROUP BY order_num
HAVING SUM(quantity) >= 100
ORDER BY order_num;
```

<aside>
💡 Eg. 2: Another way to determine the best customers is by how much they have spent. Write a SQL statement to return the order number (order_num in OrderItems table) for all orders with a total price of at least 1000. Hint, for this one you’ll need to calculate and sum the total (item_price multiplied by quantity). Sort the results by order number.

</aside>

```sql
SELECT order_num, SUM(item_price*quantity) AS total_price 
								# Here we have to SELECT new SUM(item_price*quantity) field becuase it's a calculated field?
FROM OrderItems
GROUP BY order_num
HAVING SUM(item_price*quantity) >= 1000
ORDER BY order_num;
```
# 12 Joining Tables

# 12.1 Understand Relational Tables

Breaking data into multiple tables, connect with primary key and foreign key.

## 12.1.1 Creating a Join

```sql
SELECT vend_name, prod_name,prod_price
FROM Vendors, Products
WHERE Vendors.vend_id = Products.vend_id;
```

When you join two tables, what you are actually doing is pairing every row in the first table with every row in the second table. The `WHERE` clause acts as a filter to only include tows that match the specified filter condition — the join condition. 

```sql
# Example without WHERE condition:
SELECT vend_name, prod_name,prod_price
FROM Vendors, Products;

/*
The data will return every product with every vendor, 
including products with the incorrect vendor,
even vendors with no products at all
*/
```

## 12.1.2 Inner Joins

Same as the preceding `SELECT` statement, but use `INNER JOIN`.

The actual condition passes to special `ON` clause is the same as would be passed to `WHERE`.

# 12.2 Joining Multiple Tables

No limit of number of join tables

1. list all the tables
2. define the relationship between each

```sql
SELECT prod_name, vend_name, prod_price, quantity
FROM OrderItems, Products, Vendors
WHERE Products.vend_id = Vendors.vend_id
 AND OrderItems.prod_id = Products.prod_id
 AND order_num = 20007;
```

<aside>
💡 Recall the example in lesson 11. List of customers who ordered product RGAN01.

</aside>

[11 Working with Subqueries](11%20Working%20a097f.md)

```sql
SELECT cust_name, cust_contact
FROM Customers, Orders, OrderItems
WHERE Customers.cust_id = Orders.cust_id
	AND Orders.order_num = OrderItems.order_num
	AND prod_id = 'RGAN01';
```

# 12.3 Challenge

## 12.3.1

```sql
SELECT cust_name, order_num
FROM Customers, Orders
WHERE Customers.cust_id = Orders.cust_id

----------same as----------------------

SELECT cust_name, order_num
FROM Customers INNER JOIN Orders
 ON Customers.cust_id = Orders.cust_id;
```

## 12.3.2

Use `INNER JOIN` Retrieve all customer's email for anyone purchased product "BR01".

```sql
SELECT cust_email
FROM Customers 
	INNER JOIN Orders ON Customers.cust_id= Orders.cust_id
	INNER JOIN OrderItems ON Orders.order_num = OrderItems.order_num
WHERE prod_id = 'BR01';
```

## 12.3.3

Write a SQL statement that uses joins to return customer name and the total price of all orders greater than 1000. 

```sql
SELECT cust_name, SUM(item_price*quantity) AS total_price
FROM Customers 
 INNER JOIN Orders ON Customers.cust_id = Orders.cust_id 
 INNER JOIN OrderItems ON Orders.order_num = OrderItems.order_num
GROUP BY cust_name
HAVING SUM(item_price*quantity) > 1000
ORDER BY cust_name;
```
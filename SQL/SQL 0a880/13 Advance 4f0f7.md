# 13 Advanced Joining

# 13.1 Using Table Aliases

```sql
SELECT cust_name, cust_contact
FROM Customers AS C, Orders AS O, OrderItems AS OI
WHERE C.cust_id = O.cust_id
	AND O.order_num = OI.order_num
	AND prod_id = 'RGAN01';
```

Unlike column aliases, table aliases are never returned to the client.

# 13. 2 Different Join Types

## 13.2.1. Self Joins

Find customer contacts who work for the same company for which Jim Jones works.

```sql
SELECT C1.cust_id, C1.cust_name, C1.cust_contact
FROM Customers AS C1, Customers AS C2
WHERE C1.cust_name = C2.cust_name
	AND C2.cust_contact = 'Jim Jones';
```

## 13.2.2 Natural Joins

Standard joins return all data even multiple occurrences of the same column. 

A natural join eliminates those multiple occurrences so that only one of each column is returned. 

This is typically done using a wildcard *

```sql
SELECT C.*, O.order_num, O.order_date, OI.prod_id, OI.quantity, OI.item_price
FROM Customers AS C, Orders AS O, OrderItems AS OI
WHERE C.cust_id = O.cust_id
	AND OI.order_num = O.order_num
	AND prod_id = 'RGAN01';

#Each column in Customers table ll select?
```

## 13.2.3 Outer Joins

Most joins relate rows in one table with rows in another. But occasionally, you want to include rows that have no related rows. 

```sql
#a list of all customers and their orders:
SELECT customers.cust_id, Orders.order_num
FROM Customers
	INNER JOIN Orders ON Customers.cust_id = Orders.cust_id;
```

```sql
#a list of all customers **includling those who have not placed any orders**:
SELECT customers.cust_id, Orders.order_num
FROM Customers
	LEFT OUTER JOIN Orders ON Customers.cust_id = Orders.cust_id;
```

- NOTE
    1. must use the RIGHT or LEFT keywords to specify the table from which to include all rows

# 13.3 Using Joins with Aggregate Functions

Retrieve a list of all customers and the number of orders that each has placed. 

```sql
SELECT Customers.cust_id,
			COUNT(Orders.order_num) AS num_ord
FROM Customers,
	INNER JOIN Orders ON Customers.cust_id = Orders.cust_id
GROUP BY Customers.cust_id;
```
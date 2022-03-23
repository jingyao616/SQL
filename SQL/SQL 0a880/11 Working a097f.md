# 11 Working with Subqueries

# 11.1 Filtering by Subquery

Subqueries are embedded into other queries. 

<aside>
💡 Eg. List of all the customers who ordered item RGAN01.

</aside>

```sql
#1.Retrieve the order # of all orders containing item RGAN01
SELECT order_num
FROM OrderItems
WHERE prod_id = 'RGAN01';
/*
Output:
20007
20008*/

#2. Retrieve the customer ID of all the customers who have orders listed in the order # returned in step 1
SELECT cust_id
FROM Orders
WHERE order_num IN (20007,20008);
/*
Output:
1000000004
1000000005
*/

#3. Retrieve the customer information for all the customer IDs returned in step 2.
SELECT cust_name, cust_contact
FROM Customers
WHERE cust_id IN (1000000004,1000000008)
/*
Output:
'Fun4All','Denise L. Stephens'
'The Toy Store','Kim Howard'
*/
```

Now combine the three queries by turning the first into a subquery. Always process staring **innermost** statement and working outward. 

```sql
SELECT cust_name, cust_contact
FROM Customers
WHERE cust_id IN(SELECT cust_id
									FROM Orders
									WHERE order_num IN (SELECT order_num
																			FROM OrderItems
																			WHERE prod_id = 'RGAN01'));
```

- NOTE
    1. Subquery statements can only retrieve a single column.

<aside>
💡 See lesson 12 when use `JOIN` to perform.

</aside>

# 11.2 Use Subqueries as Calculated Fields

<aside>
💡 Eg. Display total number of orders placed by every customer in your Customers table.

</aside>

```sql
# THIS IS WRONG!!!
Select cust_name,
			(SELECT COUNT(*) 
			FROM Orders
			WHERE cust_id IN(SELECT cust_id
											FROM Customers))
			# this means WHERE cust_id = cust_id from Oders table
FROM Customers
Order by cust_name;
```

```sql
# THIS IS CORRECT.
SELECT cust_name, 
			(SELECT COUNT(*)
			FROM Orders
			WHERE Orders.cust_id = Customers.cust_id) AS Orders
FROM Customers
ORDER BY cust_name
```

The `WHERE` clause tells SQL to compare the cust_id in the Orders table to the one currently being retrieved from the Customers table: `WHERE` Orders.cust_id = Customers.cust_id.
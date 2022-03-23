# 18 Using Views

# 18.1 Understanding Views

If you have a complex JOIN table SQL, others need to understand the whole structure, it would be hard if other people want to modify.

You could wrap the entire query in a virtual table.

This table does not contain any columns or data. 

Instead, it contains a query. 

```sql
SELECT cust_name, cust_contact
FROM ProductCustomers
		# THIS table is a virtual table, not real table
WHERE prod_id = 'RGAN01';
```

- NOTE
    1. Views must be uniquely named
    2. no number limitation
    3. Views can be nested
    4. Many DBMSs prohibit the use of the `ORDER BY` clause in view queries.

# 18.2 Creating Views

```sql
CREATE VIEW ProductCustomers AS 
SELECT cust_name, cust_contact, prod_id
FROM Customers, Orders, OrderItems
WHERE Customers.cust_id = Orders.cust_id
	AND OrderItems.order_num = Orders.order_num;
```

To retrieve a list of customers who ordered product RGAN01, you can do the following:

```sql
SELECT cust_name, cust_contact
FROM ProductCustomers
WHERE prod_id = 'RGAN01';
```

<aside>
❗ To remove a view, use the `DROP` statement. To over write or update a view, you must first `DROP` it and then re-create it.

</aside>

# 18.3 Using Views to Reformat Retrieved Data

The following SQL returns vendor name and location in a single combined calculated column:

```sql
SELECT RTRIM(vend_name) + '(' +RTIM(vend_country) + ')'
			#RTRIM seems not working, use CONCAT instead.
			AS vend_title
FROM Vendors
ORDER BY vend_name;
```

Suppose you regularly needed results in this format, you could create a view and use that instead.

```sql
CREATE VIEW VendorLocations AS
SELECT Concat (vend_name, '(', vend_country,')' )
			AS vend_title
FROM Vendors;
```

To retrieve the data to create all mailing labels, simply do the following:

```sql
SELECT * FROM VendorLocations;
```

# 18.4 Using Views to Filter Unwanted Data

For example you want to define a CustomerEmailList view so that it filters out customers without email addresses:

```sql
CREATE VIEW CustomerEmailList AS 
SELECT cust_id, cust_name, cust_email
FROM Customers
WHERE cust_email IS NOT NULL;
# This WHERE clause filters out those rows that have NULL values in the cust_email column
```

# 18.5 Using Views with Calculated Fields

example in lesson 17:

```sql
SELECT prod_id, quantity, item_price, quantity*item_price AS expanded_price
FROM OrderItems
WHERE order_num = 20008;
```

To turn this into a view:

```sql
CREATE VIEW OrderItemsExpanded AS
SELECT prod_id, quantity, item_price, quantity*item_price AS expanded_price
FROM OrderItems;
```

Then:

```sql
SELECT *
FROM OrderItemsExpanded
WHERE order_num = 20008;
```

# 18.6 Challenge

What is wrong with the following SQL statement? (Try to figure it out without running it):

```sql
CREATE VIEW OrderItemsExpanded AS
SELECT order_num,
       prod_id,
       quantity,
       item_price,
       quantity*item_price AS expanded_price
FROM OrderItems
ORDER BY order_num;
```

ORDER BY is not allowed in views. Views are used like tables, if you need sorted data use ORDER BY in the SELECT that retrieves data from the view.
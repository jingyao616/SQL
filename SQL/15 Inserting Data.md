# 15 Inserting Data

# 15.1 Understanding Data Insertion

1. Inserting a single complete row
2. inserting a single partial row
3. inserting the results of a query

## 15.1.1 Inserting Complete Rows

```sql
#This is **not safe** because it is highly depend on the order of original columns.

INSERT INTO Customers
VALUES (1000000006, 
			'Toy Land', 
			'123 Any Street',
			'New York',
			'NY',
			'11111',
			'USA',
			NULL,
			NULL);
```

```sql
# This is more safer but more cumbersome

INSERT INTO Customers (cust_id, 
							cust_name, 
							cust_address, 
							cust_city, 
							cust_state, 
							cust_zip, 
							cust_country, 
							cust_contact, 
							cust_email)
VALUES (1000000006, 
			'Toy Land', 
			'123 Any Street',
			'New York',
			'NY',
			'11111',
			'USA',
			NULL,
			NULL);
```

## 15.1.2 Inserting Partial Rows

If the table allows `NULL` value in certain columns, you may omit columns from an `INSERT` operation. Or it has a default value.

## 15.1.3 Inserting Retrieve Data

`INSERT SELECT` is made up of an `INSERT` statement and a `SELECT` statement.

You can merge a list of customers from another table into your Customers table:

```sql
INSERT INTO Customers (cust_id, 
							cust_name, 
							cust_address, 
							cust_city, 
							cust_state, 
							cust_zip, 
							cust_country, 
							cust_contact, 
							cust_email)
SELECT cust_id, 
							cust_name, 
							cust_address, 
							cust_city, 
							cust_state, 
							cust_zip, 
							cust_country, 
							cust_contact, 
							cust_email
FROM CustNew;
```

<aside>
❗ The column names in two tables do not need to be the same. The name doesn't matter, but the **position** matters.

</aside>

# 15. 2 Copying from One Table to Another

To copy the contents of a table into a brand new table (one that is created on the fly), you an use the CREATE SELECT statement.

```sql
CREATE TABLE CustCopy AS SELECT * FROM Customer;
```

This creates a new table named CustCopy and copies the entire contents of the Customers table into it.
# 21 Using Cursors

# 21.1 Understanding Cursors

A cursor is a database query stored on the DBMS server- not a SELECT statement, but the result set retrieved by that statement. 

Once the cursor is stored, applications can scroll or browse up and down through the data as needed. 

# 21.2 Working with Cusors

Steps:

1. must be defined before use
2. must be open for use
3. with the cursor populated with data, individual rows can be fetched as needed
4. must be closed or deallocated after done.

## 21.2.1 Creating Cursors

Cursors are created using the DECLARE statement.

For example, create a cursor that retrieves all customers without email addresses, as part of an application enabling an operator to provide missing email addresses.

```sql
DECLARE CustCursor CURSOR
FOR 
SELECT * FROM Customers
WHERE cust_email IS NULL;
```

This DECLARE statement is used to define and name the cursor — CustCursor.

Now the cursor is defined, it is ready to be opened.

## 21.2.2 Using Cursors

```sql
OPEN CURSOR CustCursor
```

The query is executed, and the retrieved data is stored for subsequent browsing and scrolling.

```sql
DECLARE @cust_id CHAR(10),
				@cust_name CHAR(50),
				@cust_address CHAR(50)
				...
OPEN CustCursor
FETCH NEXT FROM CustCursor
		INTO @cust_id, @cust_name, @cust_address
...
WHILE @@FETCH_STATUS = 0
BEGIN

FETCH NEXT FROM CustCursor
		INTO @cust_id, @cust_name, @cust_address
...
END
CLOSE CustCursor
```

## 21.2.3 Closing Cursors

```sql
CLOSE CustCursor
DEALLOCATE CURSOR CustCursor
```
# 16 Updating and Deleting Data

# 16.1 Updating Data

<aside>
❗ Don't Omit the `WHERE` Clause

</aside>

It's too easy to mistakenly update every row in the table!!

Customer 1000000005 has no email address on file and how has an address:

```sql
UPDATE Customers
SET cust_email = 'kim@thetoystore.com'
WHERE cust_id = 1000000005;

#update without a WHERE clause will update all rows with new address!
```

# 16.2 Deleting Data

<aside>
❗ Don't Omit the `WHERE` Clause

</aside>

```sql
DELETE FROM Customers
WHERE cust_id = 1000000006;
```

It's good to define foreign keys because DBMS uses them to enforce referential integrity. 

You can't delete a row that was used as foreign key in other existing tables.

<aside>
❗ `DELETE` deletes entire rows, not columns. To delete specific columns, you use an `UPDATE` statement.

</aside>
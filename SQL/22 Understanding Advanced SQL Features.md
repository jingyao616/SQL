# 22 Understanding Advanced SQL Features

# 22.1 Understanding Constraints

Constraints

Rules that govern ow database data is inserted or manipulated

DBMS enforce referential integrity by imposing constraints on database tables. Most constrains are defined in table definitions. 

## 22.1.1 Primary Key

```sql
ALTER TABLE Vendors
ADD CONSTRAINT PRIMARY KEY (vend_id);
```

## 22.1.2 Foreign Key

Foreign keys are an extremely important part of ensuring referential integrity.

```sql
CREATE TABLE Orders
(
	order_num    INTEGER   NOT NULL  PRIMARY KEY,
	cust_id      CHAR(10)  NOT NULL  REFERENCES Customers(cust_id)
);
```

This can be accomplished using CONSTRAINT

```sql
ALTER TABLE Orders
ADD CONSTRAINT 
FOREIGN KEY (cust_id)  REFERENCES   Customers (cust_id);
```

## 22.1.3 Unique Constraints

Similar to primary keys, but there are some important distinctions:

1. A table can contain multiple unique constraints, but only one primary key is allowed
2. Unique constraint columns can contain NULL values
3. Unique constraint columns can be modified or updated
4. Unique constraint columns values can be reused
5. Unique primary keys, unique constraint columns cannot be used to define foreign keys.

For example, in a Employees Table, every one has different SIN, but won't use that as primary key. You will use employee ID as PK, but you also want to ensure that each SIN is unique.

```sql
CREATE TABLE Employees
(
	employee_id    INTEGER   NOT NULL  PRIMARY KEY,
	SIN            INTEGER   NOT NULL  UNIQUE
);
```

## 22.1.4 Check Constrains

```sql
CREATE TABLE OrderItems
(
	order_num    INTEGER   NOT NULL,
	order_item   INTEGER   NOT NULL,
	prod_id      CHAR(10)  NOT NULL,
	quantity     INTEGER   NOT NULL CHECK (quantity >0),
  item_price   MONEY     NOT NULL
);
```

```sql
ADD CONSTRAINT CHECK (gender LIKE '[MF]');
```

# 22.2 Understanding Indexes

Indexes are used to sort data logically to improve the speed of searching and sorting operations. 

```sql
CREATE INDEX prod_name_ind
ON Products (prod_name);
```

# 22. 3 Understanding Triggers

Triggers are a special stored procedures that are executed automatically when specific database activity occurs. 

Unlike stored procedures, triggers are tied to individual tables.

```sql
CREATE TRIGGER customer_state
ON Customers
FOR INSERT, UPDATE
AS 
UPDATE Customers
SET cust_state = UPPER(cust_state)
WHERE Customers.cust_id = inserted.cust_id;
```
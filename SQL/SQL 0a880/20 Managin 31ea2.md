# 20 Managing Transaction Processing

# 20.1 Understanding Transaction Processing

Transaction processing is a mechanism used to manage sets of SQL operations that must be executed in batches so as to ensure that databases never contain the results of partial perations.

If an error occurs, a rollback (undo) can occur to restore the database to a known and safe stage.

<aside>
❗ You cannot roll back `CREATE` or `DROP` operations.

</aside>

## 20.1.1 Using `ROLLBACK`

```sql
DELETE FROM Orders;
ROLLBACK;
```

## 20.1.2 Using Savepoints

The placeholders are called savepoints. 

```sql
SAVEPOINT delete1;
```

Each savepoint takes a unique name that identifies it so that, when you roll back, the DBMS knows where you are rolling back to.

```sql
ROLLBACK TO delete1;
```

<aside>
❗ Transactions are blocks of SQL statements that must be executed as a batch.

</aside>
# 8 Using Data Manipulation Functions

# 8.1 Functions

## 8.1.1 Text Manipulation Functions

```sql
/*
LEFT ()         Returns characters from left of stirng
LENGTH ()       Returns the length of a string
LOWER ()        
LTRIM ()        Trims white space form left of string
RIGHT ()
RTRIM ()
SUBSTRING ()    Extracts part of a string *Eg.1*
SOUNDEX ()      Returns SOUNDEX value *Eg.2*
UPPER ()
*/
```

<aside>
💡 Eg.1  SUBSTRING(string, start, length)

</aside>

The start position. Can be both a positive or negative number. If it is a positive number, this function extracts from the beginning of the string. If it is a negative number, this function extracts from the end of the string

```sql
SELECT SUBSTRING("SQL Tutorial", 5, 3) AS ExtractString;
```

<aside>
💡 Eg.2 A contact named Michelle Green was a typo, and it should be Michael Green

</aside>

```sql
SELECT cust_name, cust_contact
FROM Customers
WHERE SOUNDEX(cust_contact) = SOUNDEX('Michael Green');
```

## 8.1.2 Date and Time Manipulation Functions

Very different across different DBMSs

```sql
SELECT order_num
FROM Orders

WHERE YEAR (order_date) =2020
```

## 8.1.3 Numeric Manipulation Functions

Use for algebraic, trigonometric, or geometric calculations 

```sql
/*
ABS ()         Absolute value
COS ()         cosine
EXP ()         exponential value
PI ()          PI
SIN ()
SQRT ()
TAN ()       

*/
```
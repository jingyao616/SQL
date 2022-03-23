# LeetCode 总结

`Where` 是筛选某一行（一定要让结果处在横向同一行）

<aside>
💡 `Count` 总结
*此处设定count（a），其中a为变量，可以为各种值，下面根据a的不同值，得出不同的count(a)的结果*
1）当a = null时，count(a)的值为0；
2）当a != null 且不是表的列名的时候，count(a)为该表的行数；
3）当a是表的列名时，count(a)为该表中a列的值不等于null的行的总数，它和2)中的差值就是该表中a列值为null的行数

</aside>

<aside>
💡 `Count VS Sum` 总结
Action = “answer” - it returns a boolean True(1), False(0).
**Numerically, if 1, 1, 0, 0:
Count(Action = “answer”) = 4
Sum(Action = “answer”) = 2 --> This is what we need.

</aside>

# 577. **Employee Bonus**

```
Write an SQL query to report the name and bonus amount of each employee with a bonus less than 1000.

Input:
Employee table:
+-------+--------+------------+--------+
| empId | name   | supervisor | salary |
+-------+--------+------------+--------+
| 3     | Brad   | null       | 4000   |
| 1     | John   | 3          | 1000   |
| 2     | Dan    | 3          | 2000   |
| 4     | Thomas | 3          | 4000   |
+-------+--------+------------+--------+
Bonus table:
+-------+-------+
| empId | bonus |
+-------+-------+
| 2     | 500   |
| 4     | 2000  |
+-------+-------+
Output:
+------+-------+
| name | bonus |
+------+-------+
| Brad | null  |
| John | null  |
| Dan  | 500   |
+------+-------+
```

```sql
select  name, bonus
from employee e left join bonus b
on e.empid=b.empid
where bonus<1000 or bonus is null;
```

<aside>
💡 虽然left join会给出null值，但此题是要求数值小于1000（null不是0），所以必须加上 or bonus is null。

</aside>

# **1322. Ads Performance**

```
Write an SQL query to find the ctr of each Ad. Round ctr to two decimal points.

Return the result table ordered by ctr in descending order and by ad_id in ascending order in case of a tie.

The query result format is in the following example.

 

Example 1:

Input: 
Ads table:
+-------+---------+---------+
| ad_id | user_id | action  |
+-------+---------+---------+
| 1     | 1       | Clicked |
| 2     | 2       | Clicked |
| 3     | 3       | Viewed  |
| 5     | 5       | Ignored |
| 1     | 7       | Ignored |
| 2     | 7       | Viewed  |
| 3     | 5       | Clicked |
| 1     | 4       | Viewed  |
| 2     | 11      | Viewed  |
| 1     | 2       | Clicked |
+-------+---------+---------+
Output: 
+-------+-------+
| ad_id | ctr   |
+-------+-------+
| 1     | 66.67 |
| 3     | 50.00 |
| 2     | 33.33 |
| 5     | 0.00  |
+-------+-------+
Explanation: 
for ad_id = 1, ctr = (2/(2+1)) * 100 = 66.67
for ad_id = 2, ctr = (1/(1+2)) * 100 = 33.33
for ad_id = 3, ctr = (1/(1+1)) * 100 = 50.00
for ad_id = 5, ctr = 0.00, Note that ad_id = 5 has no clicks or views.
Note that we do not care about Ignored Ads.
```

```sql
select ad_id,
IFNULL(round(100*sum(action = 'Clicked')/sum(action = 'Clicked' OR action = 'Viewed'), 2), 0) as ctr
from Ads
group by ad_id
order by ctr desc, ad_id 
;
```

<aside>
💡 第一反应会用count去数，但直接用sum更合适，并且sum可以直接再括号里加条件 VS count只能数全表行count(*) 包括Null，或者某个列 count(列名) 不包含Null

</aside>

# **1484. Group Sold Products By The Date**

```
Write an SQL query to find for each date the number of different products sold and their names.

The sold products names for each date should be sorted lexicographically.

Return the result table ordered by sell_date.

The query result format is in the following example.

 

Example 1:

Input: 
Activities table:
+------------+------------+
| sell_date  | product     |
+------------+------------+
| 2020-05-30 | Headphone  |
| 2020-06-01 | Pencil     |
| 2020-06-02 | Mask       |
| 2020-05-30 | Basketball |
| 2020-06-01 | Bible      |
| 2020-06-02 | Mask       |
| 2020-05-30 | T-Shirt    |
+------------+------------+
Output: 
+------------+----------+------------------------------+
| sell_date  | num_sold | products                     |
+------------+----------+------------------------------+
| 2020-05-30 | 3        | Basketball,Headphone,T-shirt |
| 2020-06-01 | 2        | Bible,Pencil                 |
| 2020-06-02 | 1        | Mask                         |
+------------+----------+------------------------------+
Explanation: 
For 2020-05-30, Sold items were (Headphone, Basketball, T-shirt), we sort them lexicographically and separate them by a comma.
For 2020-06-01, Sold items were (Pencil, Bible), we sort them lexicographically and separate them by a comma.
For 2020-06-02, the Sold item is (Mask), we just return it.
```

```sql
SELECT
    sell_date,
    COUNT(DISTINCT product) AS num_sold,
    GROUP_CONCAT(DISTINCT product order by products SEPARATOR ',') AS products
FROM activities
GROUP BY sell_date
ORDER BY sell_date;
```

<aside>
💡 GROUP_CONCAT 的用法。Order by 和 separator 在这里其实可以省略，默认。

</aside>
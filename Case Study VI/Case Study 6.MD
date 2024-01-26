Performed on 58989 rows from the dataset provided.
```
mysql> select count(*) from transactions;
+----------+
| count(*) |
+----------+
|    58989 |
+----------+
1 row in set (0.02 sec)
```

**SQL QUERIES:**

**Monthly Transactions: Need how much amount we have processed each month commutative and every month.**
```
mysql>  select MONTH(STR_TO_DATE(transaction_timestamp, '%c/%e/%y %k:%i')) as Month, SUM(transaction_amount) as Monyhly_transaction_amount_Sum from transactions group by Month;
+-------+--------------------------------+
| Month | Monyhly_transaction_amount_Sum |
+-------+--------------------------------+
|     1 |                    22251416982 |
|     2 |                     7078837493 |
+-------+--------------------------------+
2 rows in set (0.07 sec)
```

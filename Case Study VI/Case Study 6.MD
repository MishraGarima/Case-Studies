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

**Most Popular Products/Services: Design a SQL query to identify the top 5 most popular products or services based on transaction counts.**
```
mysql> select merchant_type, count(*) as Count from transactions group by merchant_type order by Count DESC limit 5;
+--------------------+-------+
| merchant_type      | Count |
+--------------------+-------+
| Tech Products      |  3636 |
| Books & Literature |  2503 |
| Fashion            |  2353 |
| Artistic Products  |  1943 |
| Culinary Products  |  1916 |
+--------------------+-------+
5 rows in set (0.05 sec)
```

**Daily Revenue Trend: Formulate a SQL query to visualize the daily revenue trend over time.**
```
mysql> select DATE(STR_TO_DATE(transaction_timestamp, '%c/%e/%y %k:%i')) as transaction_date, SUM(transaction_amount) as sum_amt from transactions group by transaction_date;
+------------------+-----------+
| transaction_date | sum_amt   |
+------------------+-----------+
| 2023-01-01       | 725017008 |
| 2023-01-02       | 724684587 |
| 2023-01-03       | 712722676 |
| 2023-01-04       | 714804361 |
| 2023-01-05       | 716760504 |
| 2023-01-06       | 702433917 |
| 2023-01-07       | 728912673 |
| 2023-01-08       | 708287455 |
| 2023-01-09       | 702884876 |
| 2023-01-10       | 729200778 |
| 2023-01-11       | 719850026 |
| 2023-01-12       | 709917746 |
| 2023-01-13       | 725546863 |
| 2023-01-14       | 701528205 |
| 2023-01-15       | 715767550 |
| 2023-01-16       | 717146163 |
| 2023-01-17       | 730952781 |
| 2023-01-18       | 722609952 |
| 2023-01-19       | 709874993 |
| 2023-01-20       | 711645879 |
| 2023-01-21       | 731127957 |
| 2023-01-22       | 717728922 |
| 2023-01-23       | 745944139 |
| 2023-01-24       | 710544739 |
| 2023-01-25       | 728501623 |
| 2023-01-26       | 707946544 |
| 2023-01-27       | 715891693 |
| 2023-01-28       | 717841118 |
| 2023-01-29       | 710974546 |
| 2023-01-30       | 710992419 |
| 2023-01-31       | 723374289 |
| 2023-02-01       | 709407387 |
| 2023-02-02       | 705916012 |
| 2023-02-03       | 728607864 |
| 2023-02-04       | 706066434 |
| 2023-02-05       | 720715266 |
| 2023-02-06       | 699073687 |
| 2023-02-07       | 704870774 |
| 2023-02-08       | 712417646 |
| 2023-02-09       | 708065992 |
| 2023-02-10       | 683696431 |
+------------------+-----------+
41 rows in set (0.06 sec)
```

**Average Transaction Amount by Product Category: Formulate a SQL query to find the average transaction amount for each product category.**
```
mysql> select merchant_type, AVG(transaction_amount) as Average_transaction_amount from transactions group by merchant_type;
+------------------------+----------------------------+
| merchant_type          | Average_transaction_amount |
+------------------------+----------------------------+
| Art & Craft            |                497888.7320 |
| Artistic Products      |                502930.8641 |
| Auto Services          |                505297.7528 |
| Automotive             |                496417.8344 |
| Beauty & Personal Care |                495128.0286 |
| Beauty Products        |                504444.6530 |
| Books & Literature     |                492197.3879 |
| Books & Magazines      |                515978.4152 |
| Business Services      |                485774.2193 |
| Culinary               |                493545.3407 |
| Culinary Products      |                500570.1080 |
| Digital Services       |                480296.9852 |
| Eco-friendly Products  |                496151.8369 |
| Electronics            |                465584.5106 |
| Family Entertainment   |                491917.3552 |
| Fashion                |                500502.4131 |
| Fitness                |                492443.1778 |
| Food & Beverage        |                492644.2857 |
| Food & Drinks          |                496133.4196 |
| Gaming                 |                507949.0721 |
| Gaming Products        |                495593.4216 |
| Global Goods           |                504068.6820 |
| Health & Fitness       |                500998.9818 |
| Health & Wellness      |                487362.1780 |
| Hobbies & Crafts       |                501390.9870 |
| Home & Living          |                515420.0233 |
| Home Decor             |                497140.2590 |
| Kids Products          |                500381.7324 |
| Luxury Products        |                497116.7563 |
| Music & Entertainment  |                499998.1538 |
| Outdoor & Recreation   |                495498.3883 |
| Outdoor Products       |                498805.4371 |
| Pet Care               |                520747.0681 |
| Pet Supplies           |                490368.5961 |
| Smart Gadgets          |                506137.4038 |
| Smart Home             |                498662.6267 |
| Sports & Fitness       |                503367.3218 |
| Tech Products          |                497381.8122 |
| Technology             |                495475.0517 |
| Travel & Leisure       |                490835.6749 |
| Wellness               |                499938.7895 |
| Wellness Products      |                489310.7530 |
+------------------------+----------------------------+
42 rows in set (0.06 sec)
```

**Transaction Funnel Analysis: Create a SQL query to analyze the transaction funnel, including completed, pending, and cancelled transactions.**
```
mysql> select MONTH(STR_TO_DATE(transaction_timestamp, '%c/%e/%y %k:%i')) as Month,
    ->     COUNT(DISTINCT CASE WHEN transaction_status = '1829' THEN user_id END) AS status_1829,
    ->     COUNT(DISTINCT CASE WHEN transaction_status = '0' THEN user_id END) AS status_0,
    -> COUNT(DISTINCT CASE WHEN transaction_status = '1002' THEN user_id END) AS status_1002,
    -> COUNT(DISTINCT CASE WHEN transaction_status = '1006' THEN user_id END) AS status_1006,
    -> COUNT(DISTINCT CASE WHEN transaction_status = '1022' THEN user_id END) AS status_1022,
    -> COUNT(DISTINCT CASE WHEN transaction_status = '9102' THEN user_id END) AS status_9102
    -> FROM transactions
    -> GROUP BY Month;
+-------+-------------+----------+-------------+-------------+-------------+-------------+
| Month | status_1829 | status_0 | status_1002 | status_1006 | status_1022 | status_9102 |
+-------+-------------+----------+-------------+-------------+-------------+-------------+
|     1 |        7340 |     7441 |        7445 |        7465 |        7271 |        7309 |
|     2 |        2343 |     2409 |        2364 |        2399 |        2354 |        2364 |
+-------+-------------+----------+-------------+-------------+-------------+-------------+
2 rows in set (0.13 sec)
```

**Monthly Retention Rate: Design a SQL query to calculate the Monthly Retention Rate, grouping users into monthly cohorts. <br>
Note: Dummy dataset used for this query**
```
mysql> select
    ->     DATE_FORMAT(STR_TO_DATE(t1.transaction_timestamp, '%m/%d/%y %H:%i'), '%Y-%m') AS month,
    ->     COUNT(DISTINCT t1.user_id) AS total_users,
    ->     COUNT(DISTINCT t2.user_id) AS retained_users,
    ->     COUNT(DISTINCT t2.user_id) / COUNT(DISTINCT t1.user_id) * 100 AS retention_rate
    -> FROM t11 t1 LEFT JOIN t11 t2 ON t1.user_id = t2.user_id
    ->     AND MONTH(STR_TO_DATE(t1.transaction_timestamp, '%m/%d/%y %H:%i')) = MONTH(STR_TO_DATE(t2.transaction_timestamp, '%m/%d/%y %H:%i')) - 1
    -> GROUP BY month ORDER BY month;
+---------+-------------+----------------+----------------+
| month   | total_users | retained_users | retention_rate |
+---------+-------------+----------------+----------------+
| 2023-01 |           3 |              1 |        33.3333 |
| 2023-02 |           3 |              2 |        66.6667 |
| 2023-03 |           3 |              0 |         0.0000 |
+---------+-------------+----------------+----------------+
3 rows in set (0.00 sec)
```

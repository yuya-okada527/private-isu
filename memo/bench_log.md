# ベンチログ

## 初期状態

### ベンチマーク

```json
{
  "pass": true,
  "score": 315,
  "success": 365,
  "fail": 6,
  "messages": ["リクエストがタイムアウトしました (POST /login)"]
}
```

## ver2

### 変更点

- nginx のデバッグログを追加

### ベンチマーク

```json
{
  "pass": true,
  "score": 159,
  "success": 353,
  "fail": 13,
  "messages": [
    "リクエストがタイムアウトしました (GET /favicon.ico)",
    "リクエストがタイムアウトしました (POST /login)",
    "リクエストがタイムアウトしました (POST /register)"
  ]
}
```

### レイテンシ分析

```
+-------+-----+-----+-----+-----+-----+--------+------------------------------+-------+--------+---------+-------+-------+--------+--------+--------+-----------+-------------+--------------+------------+
| COUNT | 1XX | 2XX | 3XX | 4XX | 5XX | METHOD |             URI              |  MIN  |  MAX   |   SUM   |  AVG  |  P90  |  P95   |  P99   | STDDEV | MIN(BODY) |  MAX(BODY)  |  SUM(BODY)   | AVG(BODY)  |
+-------+-----+-----+-----+-----+-----+--------+------------------------------+-------+--------+---------+-------+-------+--------+--------+--------+-----------+-------------+--------------+------------+
|   189 |   0 | 184 |   0 |   5 |   0 | GET    | /image/[0-9]+\.(jpg|png|gif) | 0.002 |  6.920 | 303.934 | 1.608 | 4.444 |  5.042 |  6.915 |  1.708 |     0.000 | 1056749.000 | 38914480.000 | 205896.720 |
|    43 |   0 |  36 |   0 |   7 |   0 | GET    | /                            | 0.076 |  9.954 | 156.411 | 3.637 | 7.823 |  8.613 |  9.954 |  2.467 |     0.000 |   36410.000 |  1263326.000 |  29379.674 |
|    35 |   0 |   0 |  35 |   0 |   0 | POST   | /login                       | 0.003 |  7.804 |  75.560 | 2.159 | 6.622 |  7.786 |  7.804 |  2.643 |     0.000 |       0.000 |        0.000 |      0.000 |
|    17 |   0 |  16 |   0 |   1 |   0 | GET    | /favicon.ico                 | 0.002 | 10.002 |  64.987 | 3.823 | 8.884 | 10.002 | 10.002 |  3.385 |    43.000 |      43.000 |      688.000 |     40.471 |
|    17 |   0 |  15 |   0 |   2 |   0 | GET    | /js/timeago.min.js           | 0.002 |  6.041 |  40.213 | 2.365 | 5.588 |  6.041 |  6.041 |  1.854 |     0.000 |    1915.000 |    28725.000 |   1689.706 |
|    11 |   0 |  11 |   0 |   0 |   0 | GET    | /@[a-z]                      | 0.577 |  7.768 |  35.905 | 3.264 | 7.115 |  7.768 |  7.768 |  2.238 |  7817.000 |   22545.000 |   183956.000 |  16723.273 |
|    13 |   0 |  13 |   0 |   0 |   0 | GET    | /posts/[0-9]+                | 0.075 |  8.565 |  30.001 | 2.308 | 3.911 |  8.565 |  8.565 |  2.129 |  1709.000 |    5617.000 |    46043.000 |   3541.769 |
|    15 |   0 |  14 |   0 |   1 |   0 | GET    | /js/main.js                  | 0.001 |  6.911 |  28.409 | 1.894 | 3.218 |  6.911 |  6.911 |  1.987 |     0.000 |    1824.000 |    25536.000 |   1702.400 |
|     8 |   0 |   0 |   4 |   4 |   0 | POST   | /                            | 0.003 |  4.312 |  11.125 | 1.391 | 4.312 |  4.312 |  4.312 |  1.509 |     0.000 |       0.000 |        0.000 |      0.000 |
|    14 |   0 |  14 |   0 |   0 |   0 | GET    | /css/style.css               | 0.002 |  3.196 |  10.023 | 0.716 | 2.245 |  3.196 |  3.196 |  1.008 |  1549.000 |    1549.000 |    21686.000 |   1549.000 |
|     2 |   0 |   2 |   0 |   0 |   0 | GET    | /posts                       | 1.858 |  5.349 |   7.207 | 3.604 | 5.349 |  5.349 |  5.349 |  1.746 | 33975.000 |   34161.000 |    68136.000 |  34068.000 |
|     7 |   0 |   0 |   6 |   1 |   0 | POST   | /comment                     | 0.006 |  3.568 |   6.311 | 0.902 | 3.568 |  3.568 |  3.568 |  1.228 |     0.000 |       0.000 |        0.000 |      0.000 |
|     6 |   0 |   0 |   0 |   6 |   0 | GET    | /admin/banned                | 0.003 |  1.905 |   4.197 | 0.700 | 1.905 |  1.905 |  1.905 |  0.831 |     0.000 |       0.000 |        0.000 |      0.000 |
|     6 |   0 |   6 |   0 |   0 |   0 | GET    | /login                       | 0.004 |  1.653 |   3.473 | 0.579 | 1.653 |  1.653 |  1.653 |  0.755 |  1234.000 |    1234.000 |     7404.000 |   1234.000 |
|     7 |   0 |   0 |   7 |   0 |   0 | POST   | /register                    | 0.022 |  1.872 |   2.380 | 0.340 | 1.872 |  1.872 |  1.872 |  0.626 |     0.000 |       0.000 |        0.000 |      0.000 |
|     1 |   0 |   1 |   0 |   0 |   0 | GET    | /initialize                  | 0.032 |  0.032 |   0.032 | 0.032 | 0.032 |  0.032 |  0.032 |  0.000 |     0.000 |       0.000 |        0.000 |      0.000 |
|     1 |   0 |   0 |   1 |   0 |   0 | GET    | /logout                      | 0.003 |  0.003 |   0.003 | 0.003 | 0.003 |  0.003 |  0.003 |  0.000 |     0.000 |       0.000 |        0.000 |      0.000 |
+-------+-----+-----+-----+-----+-----+--------+------------------------------+-------+--------+---------+-------+-------+--------+--------+--------+-----------+-------------+--------------+------------+
```

- 画像ファイルの取得に時間がかかっている
  - MAX で 6 秒とかかかってる時もある
  - DB に画像ファイルを raw データで保存していそう
    - mediumblob で保存しているこれは、重そう
- あとは、TOP 画面の処理に時間がかかっている

### USE メソッド

![ctop](/memo/images/ctop_ver2.png)

- mysql に対する負荷が高い

### Next Action

- mysql に対する負荷の原因を深掘りする

## ver3

### 変更点

- mysql のスロークエリログを有効化

### ベンチマーク

```json
{
  "pass": true,
  "score": 103,
  "success": 326,
  "fail": 14,
  "messages": [
    "リクエストがタイムアウトしました (GET /favicon.ico)",
    "リクエストがタイムアウトしました (POST /login)",
    "リクエストがタイムアウトしました (POST /register)"
  ]
}
```

### スロークエリログ

```
cat webapp/logs/mysql/mysql-slow.log | pt-query-digest


# 1.6s user time, 40ms system time, 44.31M rss, 32.64G vsz
# Current date: Mon Aug 14 21:07:31 2023
# Hostname: okadayuuyanoMacBook-Pro.local
# Files: STDIN
# Overall: 18.89k total, 26 unique, 183.42 QPS, 0.68x concurrency ________
# Time range: 2023-08-14T12:05:26 to 2023-08-14T12:07:09
# Attribute          total     min     max     avg     95%  stddev  median
# ============     ======= ======= ======= ======= ======= ======= =======
# Exec time            70s     5us   135ms     4ms    46ms    11ms   138us
# Lock time           19ms       0   116us     1us     2us     3us       0
# Rows sent        428.07k       0   9.77k   23.20    2.90  455.24       0
# Rows examine     197.14M       0  97.68k  10.69k  97.04k  30.22k       0
# Query size         2.87M      10 1009.05k  159.44   80.10   9.98k   31.70

# Profile
# Rank Query ID           Response time Calls R/Call V/M   Item
# ==== ================== ============= ===== ====== ===== ===============
#    1 0x16849282195BE09F 50.6986 72.8%  1011 0.0501  0.00 SELECT comments
#    2 0x7539A5F45EB76A80 14.6969 21.1%  1022 0.0144  0.00 SELECT comments
#    3 0x99AA0165670CE848  1.1597  1.7%  6329 0.0002  0.00 ADMIN PREPARE
# MISC 0xMISC              3.0767  4.4% 10530 0.0003   0.0 <23 ITEMS>

# Query 1: 11.76 QPS, 0.59x concurrency, ID 0x16849282195BE09F at byte 4311198
# This item is included in the report because it matches --limit.
# Scores: V/M = 0.00
# Time range: 2023-08-14T12:05:43 to 2023-08-14T12:07:09
# Attribute    pct   total     min     max     avg     95%  stddev  median
# ============ === ======= ======= ======= ======= ======= ======= =======
# Count          5    1011
# Exec time     72     51s    27ms   135ms    50ms    56ms     5ms    48ms
# Lock time     14     3ms     1us    70us     2us     3us     3us     1us
# Rows sent      0   2.76k       0       3    2.80    2.90    0.73    2.90
# Rows examine  48  96.42M  97.66k  97.66k  97.66k  97.04k       0  97.04k
# Query size     2  81.06k      80      83   82.10   80.10    0.17   80.10
# String:
# Databases    isuconp
# Hosts        webapp_app_1.webapp_default
# Users        root
# Query_time distribution
#   1us
#  10us
# 100us
#   1ms
#  10ms  ################################################################
# 100ms  #
#    1s
#  10s+
# Tables
#    SHOW TABLE STATUS FROM `isuconp` LIKE 'comments'\G
#    SHOW CREATE TABLE `isuconp`.`comments`\G
# EXPLAIN /*!50100 PARTITIONS*/
SELECT * FROM `comments` WHERE `post_id` = 9982 ORDER BY `created_at` DESC LIMIT 3\G

# Query 2: 11.88 QPS, 0.17x concurrency, ID 0x7539A5F45EB76A80 at byte 4593854
# This item is included in the report because it matches --limit.
# Scores: V/M = 0.00
# Time range: 2023-08-14T12:05:43 to 2023-08-14T12:07:09
# Attribute    pct   total     min     max     avg     95%  stddev  median
# ============ === ======= ======= ======= ======= ======= ======= =======
# Count          5    1022
# Exec time     21     15s    13ms    33ms    14ms    16ms     2ms    14ms
# Lock time     13     3ms     1us    46us     2us     3us     2us     1us
# Rows sent      0    1022       1       1       1       1       0       1
# Rows examine  49  97.47M  97.66k  97.66k  97.66k  97.04k       0  97.04k
# Query size     2  64.97k      63      66   65.10   65.89    0.99   62.76
# String:
# Databases    isuconp
# Hosts        webapp_app_1.webapp_default
# Users        root
# Query_time distribution
#   1us
#  10us
# 100us
#   1ms
#  10ms  ################################################################
# 100ms
#    1s
#  10s+
# Tables
#    SHOW TABLE STATUS FROM `isuconp` LIKE 'comments'\G
#    SHOW CREATE TABLE `isuconp`.`comments`\G
# EXPLAIN /*!50100 PARTITIONS*/
SELECT COUNT(*) AS `count` FROM `comments` WHERE `post_id` = 9981\G

# Query 3: 73.59 QPS, 0.01x concurrency, ID 0x99AA0165670CE848 at byte 596
# This item is included in the report because it matches --limit.
# Scores: V/M = 0.00
# Time range: 2023-08-14T12:05:43 to 2023-08-14T12:07:09
# Attribute    pct   total     min     max     avg     95%  stddev  median
# ============ === ======= ======= ======= ======= ======= ======= =======
# Count         33    6329
# Exec time      1      1s    69us     6ms   183us   332us   141us   152us
# Lock time      0    20us       0     9us       0       0       0       0
# Rows sent      0       0       0       0       0       0       0       0
# Rows examine   0       0       0       0       0       0       0       0
# Query size     6 185.42k      30      30      30      30       0      30
# String:
# Databases    isuconp
# Hosts        webapp_app_1.webapp_default
# Users        root
# Query_time distribution
#   1us
#  10us  #
# 100us  ################################################################
#   1ms  #
#  10ms
# 100ms
#    1s
#  10s+
```

- レイテンシの 70%超が comments テーブルに対する select クエリ
  - `SELECT * FROM comments WHERE post_id = ? ORDER BY created_at DESC LIMIT 3`
- その次に多いのが comments テーブルに対する count クエリ
  - `SELECT COUNT(*) AS count FROM comments WHERE post_id = ?`
- 両方とも post_id に index を貼れば改善できそう

### 実行計画

```sql
mysql> EXPLAIN SELECT * FROM `comments` WHERE `post_id` = 9982 ORDER BY `created_at` DESC LIMIT 3;
+----+-------------+----------+------------+------+---------------+------+---------+------+-------+----------+-----------------------------+
| id | select_type | table    | partitions | type | possible_keys | key  | key_len | ref  | rows  | filtered | Extra                       |
+----+-------------+----------+------------+------+---------------+------+---------+------+-------+----------+-----------------------------+
|  1 | SIMPLE      | comments | NULL       | ALL  | NULL          | NULL | NULL    | NULL | 99445 |    10.00 | Using where; Using filesort |
+----+-------------+----------+------------+------+---------------+------+---------+------+-------+----------+-----------------------------+
```

```sql
mysql> EXPLAIN SELECT COUNT(*) AS `count` FROM `comments` WHERE `post_id` = 9981;
+----+-------------+----------+------------+------+---------------+------+---------+------+-------+----------+-------------+
| id | select_type | table    | partitions | type | possible_keys | key  | key_len | ref  | rows  | filtered | Extra       |
+----+-------------+----------+------------+------+---------------+------+---------+------+-------+----------+-------------+
|  1 | SIMPLE      | comments | NULL       | ALL  | NULL          | NULL | NULL    | NULL | 99445 |    10.00 | Using where |
+----+-------------+----------+------------+------+---------------+------+---------+------+-------+----------+-------------+
```

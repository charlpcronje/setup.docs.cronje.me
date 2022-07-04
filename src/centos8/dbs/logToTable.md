---
title: How to show the queries log in MySQL?
label: Server & Software Setup
order: 100
authors:
  - name: Charl Cronje
    email: charl@CRONje.ME
    link: https://blog.cronje.me
    avatar: https://assets.cronje.me/avatars/darker.jpg
edit:
  repo: "https://github.com/charlpcronje/setup.docs.devserv.me/edit/"
  base: /src
  branch: main
  label: Edit on GitHub
editor:
  enabled: false
favicon: favicon.png
links:
- text: Dashboard
  link: https://nav.cronje.me
- text: Blog / Portfolio
  link: https://blog.cronje.me
- text: Wiki, Tips and Docs 
  link: https://docs.cronje.me
- text: My CV
  link: https://cv.cronje.me
- text: LinkedIn
  link: https://www.linkedin.com/in/charlpcronje
- text: GitHub
  link: https://github.com/charlpcronje
- text: Upwork Profile
  link: https://www.upwork.com/freelancers/~01ccb1439024ec9c50
footer:
  copyright: "webAlly &copy; Copyright {{ year }}. All rights reserved."
---
<script type="text/javascript">(function(w,s){var e=document.createElement("script");e.type="text/javascript";e.async=true;e.src="https://cdn.pagesense.io/js/webally/f2527eebee974243853bcd47b32631f4.js";var x=document.getElementsByTagName("script")[0];x.parentNode.insertBefore(e,x);})(window,"script");</script>


## First, check if you already have the two tables slow_log and general_log existing in the mysql database.

If not, you have to create them, note that you have to create in the `mysql` database.

Create the general_log table:

```sql
    CREATE TABLE `general_log` (
       `event_time` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP
                              ON UPDATE CURRENT_TIMESTAMP,
       `user_host` mediumtext NOT NULL,
       `thread_id` bigint(21) unsigned NOT NULL,
       `server_id` int(10) unsigned NOT NULL,
       `command_type` varchar(64) NOT NULL,
       `argument` mediumtext NOT NULL
    ) ENGINE=CSV DEFAULT CHARSET=utf8 COMMENT='General log';
```

The general query log is a general record of what mysqld is doing. The server writes information to this log when clients connect or disconnect, and it logs each SQL statement received from clients. The general query log can be very useful when you suspect an error in a client and want to know exactly what the client sent to mysql

Create `slow_log` table

```sql
 CREATE TABLE `slow_log` (
   `start_time` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP 
                          ON UPDATE CURRENT_TIMESTAMP,
   `user_host` mediumtext NOT NULL,
   `query_time` time NOT NULL,
   `lock_time` time NOT NULL,
   `rows_sent` int(11) NOT NULL,
   `rows_examined` int(11) NOT NULL,
   `db` varchar(512) NOT NULL,
   `last_insert_id` int(11) NOT NULL,
   `insert_id` int(11) NOT NULL,
   `server_id` int(10) unsigned NOT NULL,
   `sql_text` mediumtext NOT NULL,
   `thread_id` bigint(21) unsigned NOT NULL
  ) ENGINE=CSV DEFAULT CHARSET=utf8 COMMENT='Slow log'
```

The slow query log consists of SQL statements that take more than `long_query_time` seconds to execute and require at `leastmin_examined_row_limit` rows to be examined. The slow query log can be used to find queries that take a long time to execute and are therefore candidates for optimization.

The minimum and default values of `long_query_time` are 0 and 10, respectively. The value can be specified to a resolution of microseconds.

## 2. Enable Query logging on the database

```sql
SET global general_log = 1;
SET global log_output = 'table';
```

## 3. Now you can view the log by running this query

```sql
SELECT
    *
FROM
    mysql.general_log;
```

## 4. If you want to disable query logging on the database, run this query:

```sql
SET global general_log = 0;
```
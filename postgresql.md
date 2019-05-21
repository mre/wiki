---
description: >-
  PostgreSQL is a great database. I will try to keep here some nice things about
  it.
---

# PostgreSQL

## `pg_stat_activity`

This is a table that helps me a lot when debugging my queries.

```sql
select * from pg_stat_activity;
```

it gives you a lot of useful information, for example you can see which queries are taking too long:

```sql
SELECT pid, query from pg_stat_activity
WHERE state = 'active' AND (now() - query_start) > interval '10 seconds';
```

## Index

Indexes are great for performance but they can be very painful if misused.

A database index is a data structure that improves the speed of data retrieval operations on a database table at the cost of additional writes and storage space to maintain the index data structure. -- [Wikipedia](https://en.wikipedia.org/wiki/Database_index)

Basically, if you query a table by certain columns **often enough** you can create an index that will improve the performance of such query greatly.

The cost is that you save that index into memory \(RAM\) which is limited.

This is a query that we use at [Fera.ai](https://www.fera.ai/) and that was created by someone \(maybe from this [gist](https://gist.github.com/izbor/8b4a91a23008bae1488ebde23f6a1911) or [this](https://gist.github.com/jayelkaake/efe336b613657c20f47a7fd4879d73cc)\) to mesure tables and indexes so we can improve our database server performance:

```sql
SELECT
  table_name,
  pg_size_pretty(table_size) AS table_size,
  pg_size_pretty(indexes_size) AS indexes_size,
  pg_size_pretty(total_size) AS total_size,
  ROUND(indexes_size/1024/1024) as indexes_size_mb,
  ROUND(total_size/1024/1024) as total_size_mb
FROM (
       SELECT
         table_name,
         pg_table_size(table_name) AS table_size,
         pg_indexes_size(table_name) AS indexes_size,
         pg_total_relation_size(table_name) AS total_size
       FROM (
              SELECT ('"' || table_schema || '"."' || table_name || '"') AS table_name
              FROM information_schema.tables
            ) AS all_tables
       ORDER BY total_size DESC
     ) AS pretty_sizes;
```

Basely on how much GB \(gigabytes\) we use today, how much GB the table that we want to add the index uses and how much GB are available in the server we may decided to add the index or find a different solution to improve performance.


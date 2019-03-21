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


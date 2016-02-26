# Show Database sessions

```
SELECT datname as database,
       pid as pid,
       usename as username,
       application_name as application,
       client_addr as client_address,
       query
  FROM pg_stat_activity

# more infos

SELECT * FROM pg_stat_activity
```

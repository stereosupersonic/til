# kill all active connections

http://www.postgresql.org/docs/current/static/functions-admin.html

```
select pg_terminate_backend(pid) from pg_stat_activity  where datname='DATABSE_NAME';
```

Terminate a backend. This is also allowed if the calling role is a member of the role whose backend is being terminated, however only superusers can terminate superuser backends.

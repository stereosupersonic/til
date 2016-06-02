# backup and restore


backup (compressed)
```
pg_dump -v -h my_host -U my_user -Fc my_database > my_file.sql
```
https://www.postgresql.org/docs/9.5/static/app-pgdump.html

restore (compressed)
```
pg_restore -v -C -d my_database < my_file
```

https://www.postgresql.org/docs/9.5/static/app-pgrestore.html

# Fix mysql replica

1. login to server and find issues in the logs

```
tail -n50 /var/log/mysqld.log
```

2. login to mysql, fix the issue and restart the slave

```
mysql -uroot -p

mysql> use DATABASE_NAME

mysql> delete from TABLENAME where id = XYZ

mysql>  START SLAVE;

```

3. or ignore the issue and restart slave

```
mysql> STOP SLAVE
mysql> SET GLOBAL SQL_SLAVE_SKIP_COUNTER = 1
mysql> START SLAVE
```

4. check the slave status

```
 SHOW SLAVE STATUS\G
```
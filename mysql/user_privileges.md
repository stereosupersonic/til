# MySQL User privileges 

## show privileges
```
 select user,host,password from mysql.user;
 ```

## create user with privileges for a database
```
GRANT ALL ON miceplace_production.* TO 'miceplace'@'%' IDENTIFIED BY 'miceplace_db' WITH GRANT OPTION; FLUSH PRIVILEGES;

# miceplace_db => password
# miceplace => user
# @'%' => access from everywhere 
```
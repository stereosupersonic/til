# Run postgres database 

https://hub.docker.com/_/postgres

## run postgreSQL 12 

```
docker run -d --name postgresdb -p 5432:5432 -e POSTGRES_PASSWORD=postgres_pw postgres:12
```

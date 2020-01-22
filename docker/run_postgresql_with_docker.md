# Run postgres database 

https://hub.docker.com/_/postgres

## run postgreSQL Version X (e.g. 12) 

```
docker run -d --name postgresdb -p 5432:5432 -e POSTGRES_PASSWORD=postgres_pw postgres:12
```

## use external data directory (e.g. /mnt/data)
```
docker run -d --name postgresdb -p 5432:5432 -e POSTGRES_PASSWORD=postgres_pw -v /mnt/data/volumes/postgresql/data:/var/lib/postgresql/data postgres:12

```

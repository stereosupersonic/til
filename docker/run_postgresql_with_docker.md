# Run postgres database 

https://hub.docker.com/_/postgres

## run postgreSQL Version X (e.g. 12) 

```
docker run -d       \ # run as deamon
  --name postgresdb \ # use the name postgresdb
  -p 5432:5432      \ # map the external port to the interanl
  --restart always \ #restart after reboot
  -e POSTGRES_PASSWORD=postgres_pw \ # set some env variables
  postgres:12       # name of the imarer
```

## use external data directory (e.g. /mnt/data)
```
docker run -d --restart always --name postgresdb -p 5432:5432 -e POSTGRES_PASSWORD=postgres_pw -v /mnt/data/volumes/postgresql/data:/var/lib/postgresql/data postgres:12

```

# Dockerize a rails app run with traefik

https://docs.traefik.io/

## run with docker compose

### docker-compose.traefik.yaml

```
version: '3'

services:
  <APPNAME>:
    build: .
    restart: always
    networks:
      - web 
    ports:
      - "${PORT}:3000"
    env_file:
      - .env
    labels:
      - traefik.http.routers. <APPNAME>.rule=Host(`<APPNAME>.<HOSTNAME>.de`)
networks:
  web:
    external: true

```


### .env 

create a new file .env

```
touch .env
```

```
PORT=3001 # depend on the other containers
RAILS_MASTER_KEY=XXX # from config config/master.key

DATABASE_HOST="192.168.1.69" # depend on your setup
DATABASE_USERNAME=postgres
DATABASE_PASSWORD=postgresdb
DATABASE_NAME=toread_production
```

### build image

```
docker-compose -f docker-compose.traefik.yml build
```


### run image

```
docker-compose -f docker-compose.traefik.yml up -d
```

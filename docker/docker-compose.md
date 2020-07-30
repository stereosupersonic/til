# docker compose 

## compose file

https://docs.docker.com/compose/compose-file/

## comands 

### up starts all services 
```
docker-compose up -d --build # -d background --build if needed 

# uses a diffent compose file 
# --remove-orphans   remove containers which were created in a previous 
docker-compose -f traefik.yml up -d 
```

### logs

```
docker-compose logs -f  # Follow log output
docker-compose logs --tail 100 # last 100
```
### down: Stop and remove containers, networks, images, and volumes

```
docker-compose -f docker-compose.traefik.yml down
```

```
### stop

```
docker-compose stop
```


### events: docker events

```
docker-compose  events
```

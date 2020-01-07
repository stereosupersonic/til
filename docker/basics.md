# Docker basics

## build a image

```
docker build -t myimage:1.0 . 
```

## run 

### Run a command in an image (not runnint)

```
docker run -it --name myimage debian:buster /bin/bash
```

-d = daemon mode

## exec 

## Run commands in a container (running image)

```
docker exec -it myimage rails c
```


## cleanup

### remove any stopped containers and all unused images

```
docker system prune -a
```

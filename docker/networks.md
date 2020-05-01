# networks

https://docs.docker.com/network/

## types

### bridge

The default network driver. If you don’t specify a driver, this is the type of network you are creating. Bridge networks are usually used when your applications run in standalone containers that need to communicate

### host


### overlay


## create 

```
docker network create my-net
```

## connect a container 

```
docker create --name my-nginx \
  --network my-net \
  --publish 8080:80 \  # maps the interanl port 80 to the host port 8080
  nginx:lates
```

sidenode: Warning: The --link flag is a legacy feature of Docker  

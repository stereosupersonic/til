# Volumes

you have two options

## 1. create a volume

```
docker volume create mydata
``` 

i gets created as a directory under `/var/lib/docker/volumes/`

inspect: 'docker volume inspect mydata`

### mount

```
docker run -d \
  --name devtest \
  -v mydata:/app \
  nginx:latest
```

readonly 

```
docker run -d \
  --name=nginxtest \
  -v mydata:/usr/share/nginx/html:ro \
  nginx:latest
```

## 2. mount an existing folder or file (bind mounts)

```
docker run -d \
  --restart always --name postgresdb -p 5432:5432 -e POSTGRES_PASSWORD=postgres_pw \
  -v /mnt/data/volumes/postgresql/data:/var/lib/postgresql/data \
  postgres:12
```

it mounts the directory /mnt/data/volumes/postgresql/data to the postrges container

```
docker run -d \
  -it \
  --name devtest \
  -v "$(pwd)"/target:/app:ro \
  nginx:latest
```

BE AWARE OF FILE PERMISSIONS

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


### more complex example

```
docker run -d --name alpachinator-miceportal-alpha-primary \
-p 88:80 -p 451:443 -v /srv/files:/srv/files \
-v /etc/ssl-hotelbsde:/etc/ssl \
--env KONVENATOR_PORT=81 \
--env KONVENATOR_SSL_PORT=444 \
--env HP_DOMAIN=miceportal.com \
--env HEALTH_SSL_PORT=443 \
--env HEALTH_PORT=80  \
--env SSL_CERT=hotelbs.de \
--env BALANCE1_reaktor_3332=mice-pre-web1.mice.boreus.de:15000,15001 \
--env BALANCE1_konnektor_3333=mice-pre-web1.mice.boreus.de:15900 \
--env BALANCE1_katalysator_3336=mice-pre-web1.mice.boreus.de:15100,15101 \
--env BALANCE1_auftragsbuch_3339=mice-pre-web1.mice.boreus.de:15200,15201 \
--env BALANCE1_arbitrator_3331=mice-pre-web1.mice.boreus.de:15700 \
--env BALANCE1_ratefinder2_3338=mice-pre-web1.mice.boreus.de:15300 \
--env BALANCE1_casinator_3334=mice-pre-web1.mice.boreus.de:15600,15601 \
--env BALANCE1_indikator_3337=mice-pre-web1.mice.boreus.de:15500 \
--env BALANCE1_oscillator_3340=mice-pre-web1.mice.boreus.de:15800 \
--env BALANCE1_auditor_3341=mice-pre-web1.mice.boreus.de:16000 \
--env APP_DOMAIN=hotelbs.de \
--env KONVENATOR_PORT=81 \
--env KONVENATOR_SSL_PORT=444 miceportal/alpachinator
```

## exec 

### Run commands in a container (running image)

```
docker exec -it myimage rails c
```

## cleanup

### remove any stopped containers and all unused images

```
docker system prune -a
```

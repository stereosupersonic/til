# Treafik setup

## create a new network

```
 docker network list # list all networks

 docker network create web # create a new bridge netwark with the name 'web'
```

## create docker-compose file 

example: https://gist.github.com/Mau5Machine/00401feb19433cf0387cc66c8e90c26c
from this video: https://www.youtube.com/watch?v=Gk9WER6DunE

```
version: '3'

services:
  traefik:
    # The official v2 Traefik docker image
    image: traefik:v2.2
    restart: always
    container_name: traefik
    ports:
      - "80:80" # <== http
      - "8080:8080" # <== :8080 is where the dashboard runs on
      - "443:443" # <== https
    command:
    # Enables the web UI and tells Traefik to listen to docker
    #### These are the CLI commands that will configure Traefik and tell it how to work! ####
      ## API Settings - https://docs.traefik.io/operations/api/, endpoints - https://docs.traefik.io/operations/api/#endpoints ##
      - --api.insecure=true # <== Enabling insecure api, NOT RECOMMENDED FOR PRODUCTION
      - --api.dashboard=true # <== Enabling the dashboard to view services, middlewares, routers, etc...
      - --api.debug=true # <== Enabling additional endpoints for debugging and profiling
    ## Log Settings (options: ERROR, DEBUG, PANIC, FATAL, WARN, INFO) - https://docs.traefik.io/observability/logs/ ##
      - --log.level=DEBUG # <== Setting the level of the logs from traefik
      ## Provider Settings - https://docs.traefik.io/providers/docker/#provider-configuration ##
      - --providers.docker=true # <== Enabling docker as the provider for traefik
      - --providers.docker.exposedbydefault=false # <== Don't expose every container to traefik, only expose enabled ones
      - --providers.docker.network=web # <== Operate on the docker network named web
      ## Entrypoints Settings - https://docs.traefik.io/routing/entrypoints/#configuration ##
      - #--entrypoints.web.address=:80 # <== Defining an entrypoint for port :80 named web
      - #--entrypoints.web-secured.address=:443 # <== Defining an entrypoint for https on port :443 named web-secured
      ## Certificate Settings (Let's Encrypt) -  https://docs.traefik.io/https/acme/#configuration-examples ##
      - #--certificatesresolvers.mytlschallenge.acme.tlschallenge=true # <== Enable TLS-ALPN-01 to generate and renew ACME certs
      - #--certificatesresolvers.mytlschallenge.acme.email=theafkdeveloper@gmail.com # <== Setting email for certs
      - #--certificatesresolvers.mytlschallenge.acme.storage=/letsencrypt/acme.json # <== Defining acme file to store cert information
    volumes:
      # So that Traefik can listen to the Docker events
      - /var/run/docker.sock:/var/run/docker.sock
    networks:
      - web

  whoami:
    # A container that exposes an API to show its IP address
    restart: always
    image: containous/whoami
    container_name: "simple-service"
    labels:
      - "traefik.http.routers.whoami.rule=Host(`whoami.deimel.de`)"

networks:
  web:
    external: true
```
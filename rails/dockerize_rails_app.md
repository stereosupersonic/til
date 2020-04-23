# Dockerize a rails app

## Dockerize

### .dockerignore

```
# Git
.git
.gitignore
#Logs
log/*
# Temp files
tmp/*
# Editor temp files
*.swp
*.swo
.DS_Store

# more
Dockerfile

.bundleignore
.bundle
.byebug_history
.idea


public/packs
public/packs-test
node_modules
yarn-error.log
```

### Dockerfile for webpacker

```
FROM ruby:2.6.3
LABEL maintainer="michael@deimel.de"

# Define basic environment variables
ENV NODE_ENV production
ENV RAILS_ENV production
ENV RAILS_LOG_TO_STDOUT true
ENV RAILS_SERVE_STATIC_FILES true
ENV SECRET_KEY_BASE= XXX # TODO
ENV APP_HOME /app

RUN apt-get update -yqq && apt-get install -yqq --no-install-recommends \
  apt-transport-https

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -

RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -  
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | \
  tee /etc/apt/sources.list.d/yarn.list 

RUN apt-get update -yqq && apt-get install -yqq --no-install-recommends \
  nodejs \
  yarn

RUN gem update --system && \
    gem install bundler

# specify everything will happen within the /app folder inside the container
RUN mkdir -p $APP_HOME
WORKDIR $APP_HOME

# We copy these files from our current application to the /app container
COPY Gemfile Gemfile.lock ./

# $(nproc) runs bundler in parallel with the amount of CPUs processes 
RUN bundle config set without development test && bundle check || bundle install -j $(nproc)

# caching yarn
COPY package.json yarn.lock ./
RUN yarn install --check-files

COPY . ./

RUN RAILS_ENV=production bin/rake assets:precompile --trace

EXPOSE 3000

ENTRYPOINT $APP_HOME/entrypoint.sh
```

### entrypoint.sh
```
#!/bin/bash

# Start the run once job.
echo "Docker container has been started"

echo "run migrations"
bundle exec rails db:migrate

echo "start rails server"
mkdir -p /app/tmp/pids
rm -f /app/tmp/pids/server.pid 
bundle exec rails server -b 0.0.0.0 -p 3000
```

```
chmod +x entrypoint.sh
```

### docker-compose.yml

```
version: '3'

services:
  database:
    image: postgres:12.1
    ports:
      - "5433:5432"
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgresdb
      POSTGRES_DB: <APPNAME>_development

  web:
    build: .
    ports:
      - "3000:3000"
    environment:
      DATABASE_HOST: database
      DATABASE_USERNAME: postgres
      DATABASE_PASSWORD: postgresdb
      DATABASE_NAME: <APPNAME>_development
      RAILS_LOG_TO_STDOUT: "true" 
```


## README.md

###  adjust with
~~~~
```
## docker

### docker-compose

```
 docker-compose build
```

```
  docker-compose up
  // or with recreare
  docker-compose up --build --force-recreate

```
~~~~


### (run in production with traefik)[rails/traefik.md]
# Create a new rails 6 app with webpacker and some usefule defaults (2020)

### with postgresql and removed stuff
```
  rails new <APPNAME> -T -d postgresql --skip-sprockets --skip-action-mailer --skip-action-mailbox --skip-action-text --skip-active-storage --skip-action-cable --skip-test-unit 
```


### setup git with github

```
git init
git add .
git commit -m "init"
git remote add origin git@github.com:stereosupersonic/<APPNAME>.git
git push origin master
```


### setup database

#### config/database.yml
```
default: &default
  adapter: postgresql
  encoding: unicode
  host: <%= ENV.fetch('DATABASE_HOST', 'localhost') %>
  port: <%= ENV.fetch('DATABASE_PORT', 5432) %>
  username: <%= ENV.fetch("DATABASE_USERNAME", "postgres") %>
  password: <%= ENV.fetch("DATABASE_PASSWORD", "postgrespw") %>
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>

development:
  <<: *default 
  host: <%= ENV.fetch('DATABASE_HOST', '0.0.0.0') %>
  database: <%= ENV.fetch("DATABASE_NAME", "<APPNAME>_development") %>

test:
  <<: *default
  database: toread_test

production:
  <<: *default
  database: <%= ENV.fetch('DATABASE_NAME', "<APPNAME>_production") %>
```


```
rails db:setup
rails db:migrate
```

## libaries 

### add pry

```
# group :development, :test do
gem "pry-rails"
gem "pry-nav"
```

### add haml

```
# Gemfile
gem "haml-rails", "~> 2.0"

# convert existing layout
HAML_RAILS_DELETE_ERB=true rails haml:erb2haml
```

### add bootstrap

```
yarn add bootstrap
yarn add jquery popper.js
``` 


```
  # remove old assets folder
  rm -rf app/assets
  # create packs folder
  mkdir -p app/javascript/css
  touch app/javascript/css/site.scss
```

```
# app/javascript/packs/application.js
import 'bootstrap'
$(document).on("turbolinks:load", () => {
  $('[data-toggle="tooltip"]').tooltip()
  $('[data-toggle="popover"]').popover()
})

// stylesheets
import "css/site.scss"
```

```
# app/javascript/css/site.scss
@import "~bootstrap/scss/bootstrap.scss";
```

```
# config/webpack/environment.js
const { environment } = require('@rails/webpacker')
const webpack = require("webpack") 

environment.plugins.append("Provide", new webpack.ProvidePlugin({ 
  $: 'jquery',
  jQuery: 'jquery',
  Popper: ['popper.js', 'default']
}))  

module.exports = environment
```

### add fortawesome

```
yarn add @fortawesome/fontawesome-free 

# app/javascript/packs/application.js
import "@fortawesome/fontawesome-free/css/all.css";
```

### Application layout

```
!!!
%html
  %head
    %meta{:content => "text/html; charset=UTF-8", "http-equiv" => "Content-Type"}/
    %title Toread
    = csrf_meta_tags
    = csp_meta_tag
    
    = stylesheet_pack_tag 'application', media: 'all', 'data-turbolinks-track': 'reload'
    = javascript_pack_tag 'application', 'data-turbolinks-track': 'reload'
  %body{:class => "#{controller_name} #{action_name}"}
    %ul.nav.navbar-light.bg-light
      %a.navbar-brand{:href => root_path} Home
      %li.nav-item
        %a.nav-link{:href => "#"} Link
    .container
      .row
        - flash.each do |name, msg|
          - if msg.is_a?(String)
            %div{:class => "alert alert-#{name == :notice ? "success" : "error"}"}
              %a.close{"data-dismiss" => "alert"} ×
              = content_tag :div, msg, :id => "flash_#{name}"
      .row
        .col
          = yield
```

### add welcome controller

```
rails generate controller welcome index
```

#### config/routes.rb
```
root to: "welcome#index"
```

#### app/views/welcome/index.html.haml
```
%h1 Welcome

%i.fa.fa-heart.fa-w-16.fa-9x

%h2 Debug
%p= debug ENV.sort_by {|k,_| k}.map { |k,v| "#{k}: #{v}"}

%p= ActiveRecord::Base.connection.execute("SELECT version();").first["version"]
```


## Dockerize

### Dockerfile

```
FROM ruby:2.6.3
LABEL maintainer="michael@deimel.de"

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

RUN mkdir -p /app
WORKDIR /app

# caching bundler: This creates a separate, independent layer. Docker’s cache for this layer will only be busted if either of these two files change.
COPY Gemfile* /app/
# $(nproc) runs bundler in parallel with the amount of CPUs processes 
RUN bundle config set without development test && bundle install -j $(nproc)
# caching yarn
COPY package.json yarn.lock /app/
RUN yarn install

COPY . /app

ENV RAILS_ENV production
ENV NODE_ENV production
ENV RAILS_SERVE_STATIC_FILES true

RUN mkdir -p tmp/pids 

ENV SECRET_KEY_BASE=XXXX # TODO rake secret

RUN RAILS_ENV=production bin/rake assets:precompile

EXPOSE 3000

ENTRYPOINT /app/entrypoint.sh
```

### entrypoint.sh
```
#!/bin/bash

# Start the run once job.
echo "Docker container has been started"

declare -p | grep -Ev 'BASHOPTS|BASH_VERSINFO|EUID|PPID|SHELLOPTS|UID' > /container.env

echo "run migrations"
bundle exec rails db:migrate

echo "start rails server"
rm -f /app/tmp/pids/server.pid 
bundle exec rails server -b 0.0.0.0 -p 3000
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
    volumes:
      - .:/app
    environment:
      DATABASE_HOST: database
      DATABASE_USERNAME: postgres
      DATABASE_PASSWORD: postgresdb
      DATABASE_NAME: <APPNAME>_development
      RAILS_LOG_TO_STDOUT: "true" 
      RAILS_SERVE_STATIC_FILES: "true"
```

## development

### bin/server
``` 
bundle exec rails s -p 3000

```

```
chmod +x  bin/server
```

#### README.md

~~~~
```
# README

## development setup

### setup 

```
 bin/rails db:setup
```

### start 

``` 
  bin/webpack-dev-server
  bin/server

```

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

## Testing

### rspec

```
#in Gemfile group :development, :test add 
gem "rspec-rails"
#in command line
bundle install
rails generate rspec:install
```

### TODO

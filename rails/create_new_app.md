# Create a new rails 6 app with webpacker and some usefule defaults (2020)

## templates 

* check out https://railsbytes.com/
* check out https://www.rubidium.io/


### with postgresql and removed stuff
```
  rails new <APPNAME> -T \
  -d postgresql \
  --skip-action-mailer \
  --skip-action-mailbox \
  --skip-action-text \
  --skip-active-storage  \
  --skip-action-cable \
  --skip-spring \
  --skip-sprockets \
  --skip-turbolinks \
  --skip-test-unit 
```


### setup git with github

```
git init
git add .
git commit -m "init"
git remote add origin git@github.com:stereosupersonic/<APPNAME>.git
git push origin master
```

add gitignore 
```
curl -L https://gist.githubusercontent.com/stereosupersonic/77e929b47aec7a05d2322ce03a314706/raw > .gitignore
```

### config/application.rb

```
  config.time_zone = "Berlin"
  config.i18n.default_locale = :de

    config.generators do |g|
      g.template_engine :haml
      g.test_framework :rspec,
         :fixtures        => true,
         :view_specs      => false,
         :helper_specs    => false,
         :routing_specs   => false,
         :controller_specs => false,
         :request_specs    => false
    end
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

### setup webpacker

```
gem 'webpacker', '~> 5.x'

yarn add core-js regenerator-runtime

bundle exec rails webpacker:install
```


### add twitter bootstrap

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

### add some helpers
```
curl -L https://gist.githubusercontent.com/stereosupersonic/c4e6a7e55fece204fb38767c320a1abf/raw/a1f82ec1026852f24d5fa82bb399cd7b6d5bce79/application_helper.rb > app/helpers/application_helper.rb
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

### setup annotate 

```
# group :development do
gem "annotate"

rails g annotate:install
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
~~~~

## [setup testing](rspec_and_capybara_setup.md)

## Addional Setup

### [multi enviroment credentials](multi_enviroment_credentials.md)

### error tracker like https://rollbar.com/

### [setup rubocop](rubocop_setup.md)

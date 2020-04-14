# Create a new rails app with some usefule defaults (2020)

### postgresql
```
  rails new homie -T -d postgresql --skip-action-text --skip-active-storage --skip-action-cable --skip-test-unit 
```

### rspec

```
#in Gemfile group :development, :test add 
 gem "rspec-rails"
#in command line
bundle install
rails generate rspec:install
```


### setup git with github

```
git init
git add .
git commit -m "init"
git remote add origin git@github.com:stereosupersonic/homie.git
git push origin master
```

### setup database

```
rails db:setup
rails db:migrate
```

## libaries 

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
# app/javascript/packs/application.js
require("jquery");
require("bootstrap");
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

### add welcome controller

```
rails generate controller welcome index
```

```
# config/routes.rb
root to: "welcome#index"
```

## Dockerize

### TODO

# create new Rails 7


## install alpha
```
 gem install rails --no-document --pre
```

## create app
```
rails new <APPNAME> -T postgresql --skip-test-unit --skip-spring --javascript=esbuild --css bootstrap
```

## adjust package.json
```
  // append this
  "scripts": {
    "build": "esbuild app/javascript/*.* --bundle --outdir=app/assets/builds",
    "build:css": "sass ./app/assets/stylesheets/application.bootstrap.scss ./app/assets/builds/application.css --no-source-map --load-path=node_modules"
  }
```

## start dev servers
```
bin/dev
```

# how to use multi enviroment credentials

https://blog.bigbinary.com/2019/07/03/rails-6-adds-support-for-multi-environment-credentials.html

PR: https://github.com/rails/rails/pull/33521/files

## setup

create default settings
```
EDITOR=vim rails credentials:edit
```

its a YAML and it looks like:

```
mailbox:
  user: "mydefault"
  password: "test123"
```

in the appliction 
```
  Rails.application.credentials.mailbox[:user]
```

create a production setting  
```
EDITOR=vim rails credentials:edit --environment production
```

ATTENTION put this to .gitignore ```/config/credentials/*```

## use in production

you have to start your app with the RAILS_MASTER_KEY from your config/credentials/production.key

addjust you dockerfile

```
ARG RAILS_MASTER_KEY
RUN RAILS_MASTER_KEY=${RAILS_MASTER_KEY} RAILS_ENV=production bin/rake assets:precompile --trace
```

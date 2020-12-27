# Heroku

## CLI

```
brew install heroku
```

## login

```
 heroku login
```

## stats

```
heroku ps
heroku apps:info 
```


## create new app

```
heroku apps:create MYAPP
```
## deploy

```
git checkout master
git push heroku

heroku run rake db:migrate --trace
heroku run rake clear_cache --trace

```

## console (Rails)

```
heroku console
```

## logs

```
 heroku logs --tail
```

## Database Backups

https://devcenter.heroku.com/articles/heroku-postgres-backups

### create a backup

```
heroku pg:backups:capture
```

### download latest backup

```
heroku pg:backups:download # => "latest.dump
```

### schedule autom. backup
https://devcenter.heroku.com/articles/heroku-postgres-backups#scheduling-backups

```
heroku pg:backups:schedule DATABASE_URL --at '02:00 Europe/Berlin' --app wartenberger
```

### restore backups

```
heroku pg:backups:restore <BACKUP> DATABASE_URL --app  <APP>
```

# Bundler tips


```
bundle open mygem # opens gem

bundle pristine # Restores installed gems to their pristine condition- Good after you changed a gem locally with bundle open

bundle outdated #show outdated gems

bundle update --conservative. # Use bundle install conservative update behavior and do not allow shared dependencies to be updated.

bundle update --strict # Do not allow any gem to be updated past latest --patch | --minor | --major.
```

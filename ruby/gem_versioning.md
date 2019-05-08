# Gem Versioning 


```
Semantic versioning boils down to:

PATCH 0.0.x level changes for implementation level detail changes, such as small bug fixes
MINOR 0.x.0 level changes for any backwards compatible API changes, such as new functionality/features
MAJOR x.0.0 level changes for backwards incompatible API changes, such as changes that will break existing users code if they update
```

1. update Version number in gemspec file


2. commit and push your changes to master

```

git commit -am "my commit message"
git push origin/master

```

3. tag version

``` 
git tag -a v0.0.1 -m 'some release text here. for release 0.0.1'
git push origin v0.0.1
```

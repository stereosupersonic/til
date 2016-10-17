# search inside selected files


## grep 'main' in ruby files

```
 grep --color -Ri -C5  --include="*.rb" "main" .
 ```

 for more files

 ```
 grep --color -Ri  --include=*.{py,pl,sh} "main" /my/path

 ``

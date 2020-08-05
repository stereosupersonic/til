# environment variables

## set variable

### shell variable
Shell variables are variables that are contained exclusively within the shell in which they were set or defined. They are often used to keep track of ephemeral data, like the current working directory.

```
TEST_VAR='Hello World!'
```

### make environment variable out of it
Environmental variables are variables that are defined for the current shell and are inherited by any child shells or processes. Environmental variables are used to pass information into processes that are spawned from the shell.

```
export TEST_VAR
# or 
export TEST_VAR='Hello World!'

# test via
printenv | grep TEST_VAR

```

### set varibable with default value

```
HOST="${1:-https://mein.miceplace.miceportal.de}"
VARIABLE=${1:-DEFAULTVALUE}    #set VARIABLE with the value of 1st arg from a script
```
${variable:-default}. With :- it returns the default if the variable is undefined or defined but empty

## get variable

```
echo $TEST_VAR
````

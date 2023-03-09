# Python

* The Python Standard Library: https://docs.python.org/3.5/library/
* Style Guide: https://www.python.org/dev/peps/pep-0008/
* Zen of Python: https://www.python.org/dev/peps/pep-0020/

## using in REPL (Read-Eval-Print Loop)

only call python in a shell and you get a python shell
`python3 `

>>> print("hello, world!") #=> hello, world!
>>> import this #=> zen of python

## virtual environment

```
 # install
 python3 -m venv venv
 # activate
 source venv/bin/activate
 # deactivate
 deactivate
```

## pip - install packages

```
  pip3 install gunicorn
  # or special version
  pip install gunicorn==20.1.0
```

create requirements.txt from installed packages

`pip freeze > requirements.txt`


## strings

### interpolation with f-strings

```
  first_name = "Tom"
  f"{first_name} is my first name."    # Pythonic
```

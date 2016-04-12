# Fibonacci-Folge [wikipedia](https://de.wikipedia.org/wiki/Fibonacci-Folge)

```
0,1,1,2,3,5,8,13
0+1,1+1,1+2,2+3,3+5,5+8
```


## Ruby
```
def fib(n)
  return n if n < 2
  return fib(n- 1) + fib(n - 2)
end
```

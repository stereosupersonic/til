# Bitwise OR assignment

Usful if you need a uniq list of elements

x |= y

is shorthand for:

x = x | y

example:

```
x = [1,2,3]
x |= [3,4,5]
x #=> [1, 2, 3, 4, 5]
```

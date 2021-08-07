# Usages of asterisks in Python

## Mathematical operator

- Single `*` for the multiplication operation.
- Double `**` for the exponentiation operation.

```
>>> 2*3
>>> 6
>>> 2**3
>>> 8
```

## To capture args and kwargs
- A parameter prefixed by one * can capture any number of positional arguments into a tuple.
- A parameter prefixed by two * can capture any number of keyword arguments into a dict.

```
def func(*args, **kwargs):
    pass
```

## To restrict to keyword-only arguments
```
def genius(*, first_name, last_name):
    print(first_name, last_name)

genius(first_name='Yang', last_name='Zhou')
```

## Iterables unpacking
```
A = [1, 2, 3]
B = (4, 5, 6)
C = {7, 8, 9}
L = [*A, *B, *C] # [1, 2, 3, 4, 5, 6, 8, 9, 7]

D = {'first': 1, 'second': 2, 'third': 3}
print('{first},{second},{third}'.format(**D))
# 1,2,3

L = [1, 2, 3, 4, 5, 6, 7, 8]
a, *b = L
print(a)
# 1
print(b)
# [2, 3, 4, 5, 6, 7, 8]
```

## More info
 - [Medium post](https://medium.com/techtofreedom/5-uses-of-asterisks-in-python-3007911c198f)

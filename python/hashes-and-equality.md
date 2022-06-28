# Hashes and Equality in Python

Based on (Python Hashes and Equality)[https://hynek.me/articles/hashes-and-equality/] by Hynek Schlawack

## Equality among __ALL__ objects

Currently, the methods needed to determine are (or are not) equal in Python are:

* [`__eq__(self, other)`](https://docs.python.org/3/reference/datamodel.html#object.__eq__): The equality method
* [`__ne__(self, other`](https://docs.python.org/3/reference/datamodel.html#object.__eq__): The inequality method

Those method are inherited from the [object](https://docs.python.org/3/library/functions.html#object). A common mistake in Python 2 was to override only `__eq__()` and forget about `__ne__()` . Python 3 is friendly enough to implement an obvious `__ne__()` for you, if you don’t yourself.

## Hashes for objects

A [hash](https://docs.python.org/3/library/functions.html?highlight=hash#hash) is merely an integer representing an object using the hash() function if the object is hashable. That leads to: Barring the unlikely event of a hash collision, two instances of the same class will always have different hashes, no matter what data they carry.

Since this is usually good enough, most Pythonistas don’t realize there’s even a thing called hashing until they try to add an unhashable object into a set or a dictionary:

```
>>> set().add({})
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'dict'
unhashable type: 'dict'
```
Therefore, hashes are important because sets and dictionaries use them for their lookup tables to quickly find their keys. To do that effectively, we must realize that, an
object is hashable if it has a hash value which never changes during its lifetime (it needs a ` __hash__()` method), and can be compared to other objects (it needs` __eq__()`)

So if you decide to implement `__hash__()` and `__eq__()` by yourself, you have to keep these concepts in mind, otherwise weird things may happen

```
>>> class C:
...     def __init__(self, x):
...         self.x = x
...     def __repr__(self):
...         return f"C({self.x})"
...     def __hash__(self):
...         return hash(self.x)
...     def __eq__(self, other):
...         return (
...             self.__class__ == other.__class__ and
...             self.x == other.x
...         )
>>> d = dict()
>>> s = set()
>>> c = C(1)
>>> d[c] = 42
>>> s.add(c)
>>> d, s
({C(1): 42}, {C(1)})
>>> c in s and c in d  # c is in both!
True
>>> c.x = 2
>>> c in s or c in d   # c is in neither!?
False
>>> d, s
({C(2): 42}, {C(2)})   # but...it's right there!
```

This explains why all immutable data structures like tuples or strings are hashable while mutable ones like lists or dictionaries aren’t.

Given this behavior we’ve found another assumption made by sets and dictionaries:

```
Hashable objects which compare equal must have the same hash value.
```

## What Does All of This Mean?

* You can’t base your hash on mutable values. If an attribute can change in the lifetime of an object, you can’t use it for hashing or very funky things happen.
* Hashes can be less picky than equality checks. Since key lookups are always followed by an equality check, your hashes don’t have to be unique. That means that you can compute your hash over an immutable subset of attributes that may or may not be a unique “primary key” for the instance.
* You shouldn’t compare by value but hash by identity. This approach fails to take the second assumption into account. That said, it usually works perfectly fine because it takes a rather unlikely hash collision to become a problem. However it’s still a violation of the contract with the Python runtime and may lead to problems; albeit only possibly in the future. Python feels so strongly about this that as of Python 3, it automatically makes classes unhashable if you implement __eq__ but not __hash__. Python 2 lets you happily shoot off your foot.

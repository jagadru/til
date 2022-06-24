# BaseException.message deprecated in Python 2.6

### Background
In the newer versions of Python (from 2.6) we are supposed to inherit our custom exception classes from `Exception` which ([starting from Python 2.5](http://docs.python.org/library/exceptions.html#exceptions.Exception)) inherits from BaseException.

```python
class BaseException(object):

    """Superclass representing the base of the exception hierarchy.
    Provides an 'args' attribute that contains all arguments passed
    to the constructor.  Suggested practice, though, is that only a
    single string argument be passed to the constructor."""
```

`__str__` and `__repr__` are already implemented in a meaningful way, especially for the case of only one arg (that can be used as message).

You do not need to repeat `__str__` or `__init__` implementation.

### Solution - almost no coding needed
Just inherit your exception class from `Exception` and pass the message as the first parameter to the constructor

Example:

```python
class MyException(Exception):
    """My documentation"""

try:
    raise MyException('my detailed description')
except MyException as my:
    print my # outputs 'my detailed description'
```

You can use `str(my)` or (less elegant) `my.args[0]` to access the custom message.

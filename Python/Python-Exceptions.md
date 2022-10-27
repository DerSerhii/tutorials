# Exceptions (Исключения)

## AttributeError

Пример: <br>
`AttributeError: type object 'Car' has no attribute '__max_carrying'`

`AttributeError: 'frozenset' object has no attribute 'add'`


## TypeError
```python
>>> None + 1
Traceback (most recent call last):
    ...
TypeError: unsupported operand type(s) for +: 'NoneType' and 'int'
```
```python
>>> class Class_A:
...     def __init__(self, var):
...             return var
... 
>>> obj = Class_A(20)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: __init__() should return None, not 'int'
```


## ValueError
```python
>>> range(1, 10, 0)
Traceback (most recent call last):
    ...
ValueError: range() arg 3 must not be zero
```

## SyntaxError
```python
>>> ord(`100`)
    ...
    ord(`100`)
        ^
SyntaxError: invalid syntax
```
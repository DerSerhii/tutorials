# Tuple (Кортеж)
**Tuple (Кортеж)** — это [immutable (неизменяемый)](Python-DataTypes(Типы%20данных).md)
тип данных. 

**Tuple** — неизменяемый [список](Python-DataTypes-List(Список).md)

## Зачем нужны кортежи, если есть списки?
1. Защита от дурака. То есть кортеж защищен от изменений, как намеренных, так и случайных.
2. Меньший размер
 ```python
>>> a = (1, 2, 3, 4, 5, 6)
>>> b = [1, 2, 3, 4, 5, 6]
>>> a.__sizeof__()
36
>>> b.__sizeof__()
44
```
3. Возможность использовать кортежи в качестве ключей [dict (словаря)](Python-DataTypes-Dict(Словарь).md):
```python
>>> d = {(1, 1, 1) : 1}
>>> d
{(1, 1, 1): 1}
  
>>> d = {[1, 1, 1] : 1}
Traceback (most recent call last):
...
TypeError: unhashable type: 'list'
```
Хотя есть нюанс! ...

## Операции с ***tuple*** и его методы 
### Create ***tuple***
Создать **кортеж** можно несколькими способами:<br> 

1. Обработать любой [итерируемый](Python-Iterator&Iterable.md) объект 
[встроенной функцией](Python-Встроенные%20функции.md)`tuple()`:
```python
>>> a = tuple('hello, world!')
>>> a
('h', 'e', 'l', 'l', 'o', ',', ' ', 'w', 'o', 'r', 'l', 'd', '!')

>>> a = tuple()  
>>> a
()
```

2. С помощью литерала`( )`: 
```python
>>> a = ()   
>>> a
()
```
***Нюансы*** при создании **кортежа** из *одного* элемента:
```python
>>> a = ('s')   # неправильно !
>>> a
's'             # получилась строка !!
>>> type(a)
<class 'str'>

>>> a = ('s',) # правильно !
>>> a
('s',) 
>>> type(a)
<class 'tuple'>


>>> a = 's',    # можно и так, но лучше со скобками !
>>> a
('s',)
```

### Retrieve ***tuple***  
Все операции над [list (списками)](Python-List%20(Списки).md), не изменяющие список

Гордость программистов на python - поменять местами значения двух переменных:

```python
a, b = b, a
```

Можна раскрыть кортеж итерируемой распаковкой:
```python
>>> student_tuple = 'Lisa', 'Simpson', 'A'

>>> first, last, grade = student_tuple
>>> first
'Lisa'
>>> last
'Simpson'
>>> grade
'A'

>>> name, *other = student_tuple 
>>> name
'Lisa'
>>> other
['Simpson', 'A']
```

## Named Tuples (Именованные кортежи)

**Named Tuples (Именованные кортежи)** — это кортежи, которые позволяют обращаться к 
своим элементам по имени, а не просто по индексу!

```python
>>> from collections import namedtuple
>>> Student = namedtuple('Student', ['first', 'last', 'grade'])
```
Или можно использовать одну строку с именами, разделенными пробелами:
```python
>>> Student = namedtuple('Student', 'first last grade')
```
Кроме операций с стандартных кортежами можна делать следующее:
```python
>>> named_student_tuple = Student('Lisa', 'Simpson', 'A')
>>> named_student_tuple.first
'Lisa'
>>> named_student_tuple.last
'Simpson'
>>> named_student_tuple.grade
'A'

>>> named_student_tuple._asdict()
{'first': 'Lisa', 'last': 'Simpson', 'grade': 'A'}

>>> vars()['named_student_tuple']
Student(first='Lisa', last='Simpson', grade='A')

>>> named_student_tuple
Student(first='Lisa', last='Simpson', grade='A')

>>> new_named_student_tuple = named_student_tuple._replace(first='Bart', grade='C')
>>> new_named_student_tuple
Student(first='Bart', last='Simpson', grade='C')
```

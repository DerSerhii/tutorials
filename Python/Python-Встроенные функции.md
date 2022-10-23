# Встроенные функции Python

## Преобразование типов
- `dict(object)` — преобразование к [словарю](Python-Dict(Словарь).md)
```python
>>> dict(short='dict', long='dictionary')
{'short': 'dict', 'long': 'dictionary'}

>>> dict([(1, 1), (2, 4)])
{1: 1, 2: 4}
```
- `list(object)` — преобразование к [списку](Python-List(Список).md)
```python
>>> list('список')
['с', 'п', 'и', 'с', 'о', 'к']

>>> list({'a': 1, 'b': 2})
['a', 'b']

>>> list(range(10))
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

- `tuple(object)` — преобразование к [кортежу](Python-Tuple(Кортеж).md)
```python
>>> tuple('hello, world!')
('h', 'e', 'l', 'l', 'o', ',', ' ', 'w', 'o', 'r', 'l', 'd', '!')
```

`set(object)` — создает [множество](Python-Set%20(Множество).md)

`frozenset([последовательность])` - возвращает [неизменяемое множество](Python-Set%20(Множество).md)


`str([object], [кодировка], [ошибки])` — строковое представление объекта. Использует метод `__str__`

`slice([start=0], stop, [step=1])` — объект среза от `start` до `stop` с шагом `step`

`object()` — возвращает безликий объект, являющийся базовым для всех объектов

- `int([object], [основание системы счисления])` — преобразование к целому числу
     ```python
     >>> a = '1'
     >>> b = 'int'
     >>> int(a)
     1
     >>> int(b)
     Traceback (most recent call last):
     ...
     ValueError: invalid literal for int() with base 10: 'int'
     ```

`bool(x)` — преобразование к типу `bool`, использующая стандартную процедуру проверки истинности. 
Если х является ложным или опущен, возвращает значение `False`, в противном случае она возвращает `True`

`bytearray([источник [, кодировка [ошибки]]])` — преобразование к bytearray. Bytearray - изменяемая последовательность 
целых чисел в диапазоне `0 ≤ x < 256`. Вызванная без аргументов, возвращает пустой 
массив байт

`bytes([источник [, кодировка [ошибки]]])` — возвращает объект типа `bytes`, который 
является неизменяемой последовательностью целых чисел в диапазоне `0 ≤ x < 256`.
Аргументы конструктора интерпретируются как для `bytearray()`

`complex([real[, imag]])` — преобразование к комплексному числу

`hash(x)` — возвращает хеш указанного объекта

- `hex(х)` — преобразование целого числа в шестнадцатеричную строку
```python
>>> a = 10
>>> id(a)
140450275050000
>>> hex(id(a))
'0x7fbd20c0c210'

```
- `bin(x)` — преобразование целого числа в двоичную строку
```python
>>> bin(2)
'0b10'
>>> bin(10)
'0b1010'
>>> bin(1)
'0b1'
```

## Математическими операциями 
`pow(x, y[, r])` — ( x ** y ) % r.

`sum(iter, start=0)` — сумма членов последовательности

`abs(x)` — возвращает абсолютную величину (модуль числа)

`range([start=0], stop, [step=1])` — арифметическая прогрессия от `start` до `stop` с шагом `step`


## Встроенные функции для работы с [атрибутами](../ООП-Атрибуты%20классов%20и%20объектов.md) 

`setattr(объект, имя, значение)` — устанавливает атрибут объекта

`getattr(object, name ,[default])` — извлекает атрибут объекта с именем `name` или `default`

`delattr(object, name)` — удаляет атрибут с именем `name`

- `dir(object)` — возвращает list (список) действительных атрибутов для данного 
объекта. Если аргумент не предоставлен, то он возвращает список имен в текущем 
локальном объеме.
```python
>>> dir()
['__annotations__', '__builtins__', '__doc__', '__loader__', '__name__', '__package__', '__spec__', 'a', 'd', 'flexiple', 'i', 'j', 'l', 'number', 's']

>>> l = {1, 2}
>>> dir(l)
['__and__', '__class__', '__class_getitem__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__iand__', '__init__', '__init_subclass__', '__ior__', '__isub__', '__iter__', '__ixor__', '__le__', '__len__', '__lt__', '__ne__', '__new__', '__or__', '__rand__', '__reduce__', '__reduce_ex__', '__repr__', '__ror__', '__rsub__', '__rxor__', '__setattr__', '__sizeof__', '__str__', '__sub__', '__subclasshook__', '__xor__', 'add', 'clear', 'copy', 'difference', 'difference_update', 'discard', 'intersection', 'intersection_update', 'isdisjoint', 'issubset', 'issuperset', 'pop', 'remove', 'symmetric_difference', 'symmetric_difference_update', 'union', 'update']
```
- `vars(object)` — возвращает dict (словарь) из атрибутов объекта. Эквивалент: `object.__dict__`  
Если аргумент не предоставлен - эквивалент: `locals()`
```python
>>> class A:
...     ...
... 
>>> a = A()
>>> a.atr = 10
>>> vars(a)
{'atr': 10}

>>> vars()
{'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <class '_frozen_importlib.BuiltinImporter'>, '__spec__': None, '__annotations__': {}, '__builtins__': <module 'builtins' (built-in)>}

>>> vars() == locals()
True
```


## Встроенные функции для работы в консоли

- `input([prompt])` — возвращает введенную пользователем строку. 
Prompt - подсказка пользователю
```python
>>> inp = input("Введите целые числа через пробел: ")
Введите целые числа через пробел:
1 2 3 4 
>>> inp
'1 2 3 4'
```
- `help([object])` — вызов встроенной справочной системы
```python
>>> help(print)
Help on built-in function print in module builtins:
print(...)
    print(value, ..., sep=' ', end='\n', file=sys.stdout, flush=False)
    
    Prints the values to a stream, or to sys.stdout by default.
    Optional keyword arguments:
    file:  a file-like object (stream); defaults to the current sys.stdout.
    sep:   string inserted between values, default a space.
    end:   string appended after the last value, default a newline.
    flush: whether to forcibly flush the stream.
```

## Встроенные функции с [итератором](Python-Iterator&Iterable.md)

- `iter(x)` — возвращает объект итератора (эквивалентно `x.__iter__()`)
- `next(x)` — возвращает следующий элемент итератора (эквивалентно `x.__next__()`) 
```python
>>> l = [5, 3, 7]
>>> it = iter(l)
>>> it
<list_iterator object at 0x000002A941359610>
>>> next(it)
5
>>> next(it)
3
>>> next(it)
7
>>> next(it)
Traceback (most recent call last):
    ...
StopIteration
```
- `zip(*iterable, strict=False)` — создает итератор, который возвращает [tuple(кортежи)](Python-Tuple%20(Кортежи).md),
состоящие из соответствующих элементов аргументов-последовательностей
```python
>>> number = [1, 2, 3, 4]
>>> char = ['a', 'b', 'c', 'd']
>>> f = zip(number, char)
>>> f
<zip object at 0x000002B23351E400>
>>> list(f)
[(1, 'a'), (2, 'b'), (3, 'c'), (4, 'd')]

>>> list(zip(range(5), range(7)))
[(0, 0), (1, 1), (2, 2), (3, 3), (4, 4)]

>>> list(zip(range(5), range(7), strict=True))
Traceback (most recent call last):
...
ValueError: zip() argument 2 is longer than argument 1
```

- `enumerate(iterable, start=0)` — создает итератор, возвращающий tuple(кортеж) из номера и 
соответствующего члена последовательности
```python
>>> numbers = [1,2,3]
>>> enumerate_var = enumerate(numbers)
>>> enumerate_var
<enumerate object at 0x7ff975dfdd80>
>>> next(enumerate_var)
(0, 1)
``` 
 
- `map(func, *iterables)` — создает итератор, получившийся после применения к каждому 
элементу последовательности функции `func`<br>
```python
>>> number = [1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> char = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i']
>>> my_zip = map(lambda x, y: (x, y), number, char)
>>> my_zip
<map object at 0x000002B2338DC700>
>>> list(my_zip)
[(1, 'a'), (2, 'b'), (3, 'c'), (4, 'd'), (5, 'e'), (6, 'f'), (7, 'g'), (8, 'h'), (9, 'i')]
```

- `filter(func, iterable)` — возвращает [итератор](Python-Iterator&Iterable.md) из тех 
элементов, для которых `func` возвращает истину
```python
>>> l = [55, 20, 66, 90, 68, 59, 76, 60, 88, 74, 81, 65, 5, 71]
>>> f = filter(lambda x: x > 70, l)
>>> f
<filter object at 0x000001BCB8CB6940>
>>> list(f)
[90, 76, 88, 74, 81, 71]
```

- `open(file, mode='r', buffering=None, encoding=None, errors=None, newline=None, 
closefd=True)` — создает итератор, открывает файл и возвращает соответствующий [поток](Поток%20%25%20Процесс.md)
```python
>>> f = open('foo.txt')
>>> next(f)
'bar\n'
>>> next(f)
'baz\n'
```

`reversed(object)` — Итератор из развернутого объекта.

## Встроенные функции для работы с [типами данных](Python-Переменные&Типы данных.md)
- `type(object)` — возвращает тип объекта
```python
>>> a = 10 
>>> type(a)
<class 'int'>

>>> type(int)
<class 'type'>

>>> type(type)
<class 'type'>
```

## Другие встроенные функции

`all(последовательность)` — Возвращает `True`, если все элементы истинные (или, если последовательность пуста).

`any(последовательность)` — Возвращает `True`, если хотя бы один элемент - истина. Для пустой последовательности возвращает False.

`ascii(object)` — Как `repr()`, возвращает строку, содержащую представление объекта, но заменяет не-ASCII символы на экранированные последовательности.

- `callable(x)` — возвращает `True` для объекта, поддерживающего вызов (как функции)
```python
>>> a = print 
>>> b = 133
>>> callable(a)
True
>>> callable(b)
False
```
`chr(x)` — Возвращает односимвольную строку, код символа которой равен x.

`classmethod(x)` — Представляет указанную функцию методом класса.

`compile(source, filename, mode, flags=0, dont_inherit=False)` — Компиляция в программный код, который впоследствии может выполниться функцией eval или exec. Строка не должна содержать символов возврата каретки или нулевые байты.


`divmod(a, b)` — Возвращает частное и остаток от деления a на b.

`eval(expression, globals=None, locals=None)` — Выполняет строку программного кода.

`exec(object[, globals[, locals]])` — Выполняет программный код на Python.

`format(value[,format_spec])` — Форматирование (обычно форматирование строки).

`globals()` — Словарь глобальных имен.

`hasattr(object, name)` — Имеет ли объект атрибут с именем 'name'.

- `id(object)` — возвращает "адрес" объекта. Это целое число, которое гарантированно 
будет уникальным и постоянным для данного объекта в течение срока его существования.
```python
>>> a = 10
>>> id(a)
140450275050000
>>> a += 1
>>> id(a)
140450275050032

>>> lst = [1, 2]
>>> id(lst)
140450272770432
>>> lst.extend([1,2])
>>> id(lst)
140450272770432

>>> id(None)
94261142246368
```

`isinstance(object, ClassInfo)` — Истина, если объект является экземпляром ClassInfo или его подклассом. Если объект не является объектом данного типа, функция всегда возвращает ложь.

`issubclass(класс, ClassInfo)` — Истина, если класс является подклассом ClassInfo. Класс считается подклассом себя.

`len(x)` — Возвращает число элементов в указанном объекте.

`locals()` — Словарь локальных имен.

`max(iter, [args ...] * [, key])` — Максимальный элемент последовательности.

`min(iter, [args ...] * [, key])` — Минимальный элемент последовательности.

`oct(х)` — Преобразование целого числа в восьмеричную строку.

`ord(с)` — Код символа.

`repr(obj)` — Представление объекта.

`print([object, ...], *, sep=" ", end='\n', file=sys.stdout)` — Печать.

`property(fget=None, fset=None, fdel=None, doc=None)`

`round(X [, N])` — Округление до N знаков после запятой.

`sorted(iterable[, key][, reverse])` — отсортированный список.

`staticmethod(function)` — статический метод для функции.

`super([тип [, объект или тип]])` — доступ к родительскому классу

`type(name, bases, dict)` — возвращает новый экземпляр класса `name`




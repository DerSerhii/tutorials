# Встроенные функции Python

## Преобразование типов
- `dict(iterable)` — преобразование к [словарю](Python-DataTypes-Dict(Словарь).md)
```python
>>> dict(short='dict', long='dictionary')
{'short': 'dict', 'long': 'dictionary'}

>>> dict([(1, 1), (2, 4)])
{1: 1, 2: 4}
```
- `list(iterable)` — преобразование к [списку](Python-DataTypes-List(Список).md)
```python
>>> list('список')
['с', 'п', 'и', 'с', 'о', 'к']

>>> list({'a': 1, 'b': 2})
['a', 'b']

>>> list(range(10))
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

- `tuple(iterable)` — преобразование к [кортежу](Python-DataTypes-Tuple(Кортеж).md)
```python
>>> tuple('hello, world!')
('h', 'e', 'l', 'l', 'o', ',', ' ', 'w', 'o', 'r', 'l', 'd', '!')
```

- `set(iterable)` — преобразование к [множеству](Python-DataTypes-Set&FrozenSet(Множество).md)
```python
>>> set('hello!')
{'!', 'e', 'o', 'h', 'l'}

>>> set([1, 1, 1, 2, 3])
{1, 2, 3}
```

- `frozenset(iterable)` — преобразование к [неизменяемому множеству](Python-DataTypes-Set&FrozenSet(Множество).md)
```python
>>> frozenset('hello!')
frozenset({'!', 'h', 'e', 'o', 'l'})

>>> frozenset([1, 1, 1, 2, 3])
frozenset({1, 2, 3})
```

- `str(object, [кодировка], [ошибки])` — преобразование к [строке](Python-DataTypes-Str(Строка).md)<br>
Строковое представление объекта (метод`__str__`)
```python
>>> str(1_000)
'1000'
```

`slice([start=0], stop, [step=1])` — объект среза от `start` до `stop` с шагом `step`

`object()` — возвращает безликий объект, являющийся базовым для всех объектов

- `int(x, base=10)` — преобразование числа или строки в целое число.<br>
Возврящает`0`если нет аргументов. <br>
Если`x`число, то возврящает`x.__int__()`. <br>
Если число с плавающей точкой, то усекается до целого числа.
 
```python
>>> int('1')
1

>>> int(25.65)
25

>>> int('25.65')
Traceback (most recent call last):
    ...
ValueError: invalid literal for int() with base 10: '25.65'

>>> int(float('25.65'))
25

>>> int()
0

>>> int('0b100', base=2)
4
>>> int('100', base=2)
4
```

- `float(x)`— преобразование строки или числа в число с плавающей запятой, если это возможно.
```python
>>> float(25.65)
25.65
>>> float('25.65')
25.65

>>> float()
0.0
```

`bytearray([источник [, кодировка [ошибки]]])` — преобразование к bytearray. Bytearray - изменяемая последовательность 
целых чисел в диапазоне `0 ≤ x < 256`. Вызванная без аргументов, возвращает пустой 
массив байт

`bytes([источник [, кодировка [ошибки]]])` — возвращает объект типа `bytes`, который 
является неизменяемой последовательностью целых чисел в диапазоне `0 ≤ x < 256`.
Аргументы конструктора интерпретируются как для `bytearray()`

`complex([real[, imag]])` — преобразование к комплексному числу

- `hash(x)` — возвращает хеш указанного объекта
```python
>>> hash(None)
5926932636734

>>> hash(100)
100

>>> hash("s")
-5210461911571117569
```

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

- `oct(х)` — преобразование целого числа в восьмеричную строку
```python
>>> oct(100)
'0o144'
 
>>> oct(True)
'0o1'
```
- `bool(x)` — преобразование к типу`bool`, использующая стандартную процедуру 
проверки истинности. Если`х`является ложным или не указан, возвращает
значение`False`, в противном случае она возвращает`True`
```python
>>> bool("Serhii")
True
>>> bool(10)
True

>>> bool()
False
>>> bool(None)
False

>>> bool('')
False
>>> bool(' ')
True
```

## Булевые операции

- `all(iterable)` — возвращает`True`, если все элементы истинные 
(или, если последовательность пуста)
```python
>>> a=[]
>>> all(a)
True

>>> a=[1]
>>> all(a)
True

>>> a=[1,0]
>>> all(a)
False
```

- `any(iterable)` — возвращает`True`, если хотя бы один элемент - истина. 
Для пустой последовательности возвращает`False`.
```python
>>> a=[]
>>> any(a)
False

>>> a=[1]
>>> any(a)
True

>>> a=[1,0]
>>> any(a)
True
```

## Математические операции 
`pow(x, y[, r])` — ( x ** y ) % r.

- `min(iterable, [args ...] * [, key])` — минимальный элемент последовательности
```python
>>> min(2,3,4,5)
2

>>> min('serhii')
'e'
```

- `max(iterable, [args ...] * [, key])` — максимальный элемент последовательности
```python
>>> max(2,3,4,5)
5

>>> max('serhii')
's'
```

- `sum(iterable, start=0)` — сумма членов последовательности
```python
>>> sum((2,3,4,5))
14

>>> sum((2,3,4,5), 100)
114

>>> sum('serhii')
Traceback (most recent call last):
    ...
TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

`abs(x)` — возвращает абсолютную величину (модуль числа)

- `range([start=0], stop, [step=1])` — арифметическая прогрессия от`start`до`stop(не включая его)` с 
шагом`step`
```python
>>> frozenset(range(-1,2))
frozenset({0, 1, -1})

>>> tuple(range(1,10,2))
(1, 3, 5, 7, 9)

>>> list(reversed(range(11)))
[10, 9, 8, 7, 6, 5, 4, 3, 2, 1, 0]

>>> list(range(10,-1,-1))
[10, 9, 8, 7, 6, 5, 4, 3, 2, 1, 0]

>>> range(1, 10, 0)
Traceback (most recent call last):
    ...
ValueError: range() arg 3 must not be zero
```

- `round(number, n=None)` — округление`number`до`n`знаков после запятой.
```python
>>> round(0.5)
0
>>> round(1.5)
2
>>> round(2.5)
2
>>> round(3.5)
4
>>> round(4.5)
4

>>> round(565.5556, -1)
570.0
>>> round(565.5556, -2)
600.0
>>> round(565.5556, -3)
1000.0

a = 1/6
print(a)
print(round(a, 2))

>>> a = 1/6
>>> a
0.16666666666666666
>>> round(a, 2)
0.17
```


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
 
- `map(func, *iterables)` — создает [генератор](Python-Generator(Генератор).md)
(ленивый итератор), который отдает значения, получившиеся после применения к каждому 
элементу последовательности функции`func`<br>
```python
>>> number = [1, 2, 3, 4, 5]
>>> char = ['a', 'b', 'c', 'd', 'e']
>>> my_zip = map(lambda x, y: (x, y), number, char)
>>> my_zip
<map object at 0x000002B2338DC700>
>>> list(my_zip)
[(1, 'a'), (2, 'b'), (3, 'c'), (4, 'd'), (5, 'e')]

>>> list(map(int, '12345'))
[1, 2, 3, 4, 5]
>>> list(int(i) for i in '12345')  # аналогичное выражение-генератор   
[1, 2, 3, 4, 5]
```

- `filter(func, iterable)` — создает [генератор](Python-Generator(Генератор).md) (ленивый итератор)
из тех элементов, для которых`func`возвращает`True`
```python
>>> l = [55, 20, 66, 90, 68, 59, 76, 60, 88, 74, 81, 65, 5, 71]

>>> f = filter(lambda x: x > 70, l)
>>> f
<filter object at 0x000001BCB8CB6940>
>>> list(f)
[90, 76, 88, 74, 81, 71]
                            
>>> f = (x for x in l if x > 70) # аналогичное выражение-генератор
>>> list(f)
[90, 76, 88, 74, 81, 71]

>>> f = filter(None, [0, '', 'hello', 100, False])
>>> list(f)
['hello', 100]
```

- `open(file, mode='r', buffering=None, encoding=None, errors=None, newline=None,
  closefd=True)` — создает итератор, открывает файл и возвращает 
соответствующий [поток](Поток%20%25%20Процесс.md)
```python
>>> f = open('foo.txt')
>>> next(f)
'bar\n'
>>> next(f)
'baz\n'
```

- `reversed(object)` — итератор из развернутого объекта.
```python
>>> [i for i in reversed(range(10))]
[9, 8, 7, 6, 5, 4, 3, 2, 1, 0]

>>> reversed(range(3))
<range_iterator object at 0x7f226c5a72a0>
```

## Встроенные функции для работы с [типами данных](Python-DataTypes(Типы данных).md)
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

## Встроенные функции для работы с [символами](Python-DataTypes-Str(Строка).md)

- `ord(symbol)` — для символа`symbol`вернет число, из таблицы символов Unicode
представляющее его позицию. <br>
Функция`ord()`обратная`chr()` 
```python
>>> ord('a')
97
>>> ord(' ')
32
>>> ord('€')
8364
```
Для символа строки 8-бит возвращает значение байта. <br>
Если передан символов Unicode и Python собран с`UCS2 Unicode`, то позиция 
кода должна находиться в диапазоне от`0`до`65535`включительно, иначе 
возбуждается исключение`TypeError`.
```python
>>>ord('\u2020')
8224
```
- `chr(integer)` — принимает целочисленный аргумент`integer`и возвращает строку, 
представляющую символ в этой кодовой точке. <br> 
Функция`chr()`обратная`ord()`
```python
>>> chr(97)
'a'
>>> chr(32)
' '
>>> chr(8364)
'€'
>>> chr(8224)
'†'
```
- `repr(object)` — возвращает строку, содержащую печатное представление`объекта`.
```python
>>> repr("price€")
"'price€'"

>>> repr(10)
'10'
``` 
- `ascii(object)` — возвращает строку, содержащую печатное представление`объекта`.<br>
  Но экранирует символы, отличные от ASCII, в строке с помощью `\x`,`\u`или`\U`.
```python
>>> ascii("price€")
"'price\\u20ac'"

>>> ascii(10)
'10'
```

## Другие встроенные функции

- `callable(x)` — возвращает`True`для объекта, поддерживающего вызов (как функции)
```python
>>> a = print
>>> b = 133

>>> callable(a)
True
>>> callable(b)
False

>>> callable(None)
False
```
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

- `len(x)` — возвращает число элементов в указанном объекте
```python
>>> s = '0123456789'
>>> len(s)
10
```

`locals()` — Словарь локальных имен.

`print([object, ...], *, sep=" ", end='\n', file=sys.stdout)` — Печать.

`property(fget=None, fset=None, fdel=None, doc=None)`

`sorted(iterable[, key][, reverse])` — отсортированный список.

`staticmethod(function)` — статический метод для функции.

`super([тип [, объект или тип]])` — доступ к родительскому классу

`type(name, bases, dict)` — возвращает новый экземпляр класса `name`




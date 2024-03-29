# Dict (Словарь)
***Dict (Словарь)*** — это коллекция произвольных объектов с доступом по ключу. 

Их иногда ещё называют *ассоциативными массивами* или [хеш-таблицами](Python-HashTable(HashMaps).md).

До Python 3.6 нет гарантии сохранения порядка вставки ключей.

**Dict**  — это [mutable (изменяемый)](Python-DataTypes(Типы%20данных).md)
тип данных.


Ключом словаря может быть **хешируемый объект (неизменяемый тип данных)**.  

## Операции с ***list*** и его методы
### Create ***dict***
Создать **словарь** можно несколькими способами.<br> 
1. С помощью [встроенной функции](Python-Встроенные%20функции.md)`dict()`:
```python
>>> d = dict(short='dict', long='dictionary')
>>> d
{'short': 'dict', 'long': 'dictionary'}

>>> d = dict([(1, 1), (2, 4)])
>>> d
{1: 1, 2: 4}
```

2. С помощью литерала`{ }`:
```python
>>> d = {}
>>> d
{}
>>> d = {'dict': 1, 'dictionary': 2}
>>> d
{'dict': 1, 'dictionary': 2}
```

3. C помощью [classmethod](../OOP/ООП-Методы%20классов.md)`dict.fromkeys(seq[, value])`, 
который создает словарь с ключами из`seq`и значением`value`(по умолчанию `None`):
```python
>>> d = dict.fromkeys(['a', 'b'])
>>> d
{'a': None, 'b': None}

>>> d = dict.fromkeys(['a', 'b'], 100)
>>> d
{'a': 100, 'b': 100}
```

4. C помощью генераторов словарей, которые очень похожи на [генераторы списков](../Python-Генераторы%20списков.md).
```python
>>> d = {a: a ** 2 for a in range(7)}
>>> d
{0: 0, 1: 1, 2: 4, 3: 9, 4: 16, 5: 25, 6: 36}
```

### Retrieve ***dict***
Извлечение значения осуществляется по ключу:
```python
>>> d = {1: 2, 2: 4, 3: 9}
>>> d[1]
2
>>> d[4] = 4 ** 2
>>> d
{1: 2, 2: 4, 3: 9, 4: 16}
>>> d['1']
Traceback (most recent call last):
...
d['1']
KeyError: '1'
```
`dict.get(key[, default])` — возвращает значение ключа, но если его нет,
не бросает исключение, а возвращает`default`(по умолчанию`None`)

`dict.keys()` — возвращает ключи в словаре

`dict.values()` — возвращает значения в словаре

`dict.items()` — возвращает пары (ключ, значение)

`dict.copy()` — возвращает копию словаря

### Update ***dict***
Обновление словаря:
```python
>>> d = {1: 2, 2: 4, 3: 9}

>>> d[4] = 4 ** 2
>>> d
{1: 2, 2: 4, 3: 9, 4: 16}

>>> d[4] = None
>>> d
{1: 2, 2: 4, 3: 9, 4: None}
```
`dict.setdefault(key[, default])` — возвращает значение ключа, но если его нет,
не бросает исключение, а создает ключ со значением `default` (по умолчанию `None`)

`dict.update([other])` — обновляет словарь, добавляя пары (ключ, значение) из `other`.
Существующие ключи перезаписываются. Возвращает `None` (не новый словарь!)

### Delete ***dict*** item

`dict.clear()` — очищает словарь

`dict.pop(key[, default])` — удаляет ключ и возвращает значение.
Если ключа нет, возвращает `default` (по умолчанию бросает исключение)

- `dict.popitem()` — удаляет и возвращает пару (ключ, значение). <br>
Если словарь пуст, бросает исключение`KeyError`. 
```python
>>> d = dict(a=1, b=2, c=3)
>>> d
{'a': 1, 'b': 2, 'c': 3}

>>> d.popitem()
('c', 3)
>>> d
{'a': 1, 'b': 2}

>>> d.popitem(0)
Traceback (most recent call last):
    ...
TypeError: dict.popitem() takes no arguments (1 given)

>>> empty = {}
>>> empty
{}

>>> empty.popitem()
Traceback (most recent call last):
    ...
KeyError: 'popitem(): dictionary is empty'
```

# OrderedDict

Если нужен *упорядоченный словарь* и быть *обратно совместимым*, необходимо 
использовать **OrderedDict** (модуль`collections`).

В **OrderedDict** есть опции не встроенные в стандартный`dict`:
- поддерживает обратную итерацию;
- удаление первого или последнего элемента в словаре;
- перемещение элемента в начало или конец словаря.

Сравнение равенства`==`не ведет себя одинаково:
- сравнение:`dict`vs`dict` -> порядок ключей НЕ имеет значения;
- сравнение:`OrderedDict`vs`OrderedDict` -> порядок ключей имеет значение;
- сравнение:`OrderedDict`vs`dict` -> порядок ключей НЕ имеет значения.

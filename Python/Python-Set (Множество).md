# Set & Frozenset (Множество)

### Set
**Set (Множество)** в python - "контейнер", содержащий *не повторяющиеся*
элементы в случайном порядке.

Создаём множества:
```
>>> a = set()
>>> a
set()
>>> a = set('hello')
>>> a
{'h', 'o', 'l', 'e'}
>>> a = {'a', 'b', 'c', 'd'}
>>> a
{'b', 'c', 'a', 'd'}
>>> a = {i ** 2 for i in range(10)} # генератор множеств
>>> a
{0, 1, 4, 81, 64, 9, 16, 49, 25, 36}
>>> a = {}  # А так нельзя!
>>> type(a)
<class 'dict'>
```

Как видно из примера, множества имеет тот же литерал, 
что и [словарь](Python-Dict%20(Словари).md), но пустое множество с помощью литерала 
создать нельзя.

Множества удобно использовать для удаления повторяющихся элементов:
```
>>> words = ['hello', 'daddy', 'hello', 'mum']
>>> set(words)
{'hello', 'daddy', 'mum'}
```

С множествами можно выполнять множество операций: находить объединение, пересечение...

`len(s)` — число элементов в множестве (размер множества)

`x in s` — принадлежит ли `x` множеству `s`

`set.isdisjoint(other)` — истина, если `set` и `other` не имеют общих элементов

`set == other` — все элементы `set` принадлежат `other`, все элементы `other` принадлежат `set`

`set.issubset(other)` или `set <= other` — все элементы `set` принадлежат `other`

`set.issuperset(other)` или `set >= other` — аналогично

`set.union(other, ...)` или `set | other | ...` — объединение нескольких множеств

`set.intersection(other, ...)` или `set & other & ...` — пересечение

`set.difference(other, ...)` или `set - other - ...` — множество из всех элементов `set`, не принадлежащие ни одному из `other`

`set.symmetric_difference(other)`; `set ^ other` — множество из элементов, встречающихся в одном множестве, но не встречающиеся в обоих

`set.copy()` — копия множества

И операции, непосредственно изменяющие множество:

`set.update(other, ...)`; `set |= other | ...` — объединение

`set.intersection_update(other, ...)`; `set &= other & ...` — пересечение

`set.difference_update(other, ...)`; `set -= other | ...` — вычитание

`set.symmetric_difference_update(other)`; `set ^= other` — множество из элементов, встречающихся в одном множестве, но не встречающиеся в обоих

`set.add(elem)` — добавляет элемент в множество

`set.remove(elem)` — удаляет элемент из множества. `KeyError`, если такого элемента не существует

`set.discard(elem)` — удаляет элемент, если он находится в множестве

`set.pop()` — удаляет первый элемент из множества. Так как множества не упорядочены, нельзя точно сказать, какой элемент будет первым

`set.clear()` — очистка множества

### Frozenset

Единственное отличие `set` от `frozenset` заключается в том, что <br>
`set` — изменяемый тип данных <br>
`frozenset` - нет <br> 
Примерно похожая ситуация со [списками](Python-List%20(Списки).md) и [кортежами](Python-Tuple%20(Кортежи).md).

```
>>> a = set('qwerty')
>>> b = frozenset('qwerty')
>>> a == b
True

>>> type(a - b)
<class 'set'>
>>> type(a | b)
<class 'set'>

>>> a.add(1)
>>> b.add(1)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'frozenset' object has no attribute 'add'
```

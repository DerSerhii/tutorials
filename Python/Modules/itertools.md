# Module itertools

`itertools` — функції, що створюють [ітератори](../Functions/Python-Iterator&Iterable.md) для ефективного циклу.

Модуль стандартизує основний набір швидких, ефективних інструментів пам’яті, які корисні окремо або в комбінації. Разом вони утворюють «алгебру ітераторів», що дає змогу створювати спеціалізовані інструменти лаконічно та ефективно на чистому Python.

- `itertools.groupby(iterable, key=None)` <br>
Створює ітератор, який повертає послідовні ключі та групи з`iterable`. <br>
Ключ — це функція, яка обчислює значення ключа для кожного елемента. 
Якщо не вказано або має значення`None`, `key`за замовчуванням використовується як функція ідентифікації та повертає елемент без змін. <br>
Як правило,`iterable` вже має бути відсортований за тією самою ключовою функцією.

```python
groups = []
uniquekeys = []
data = sorted(data, key=keyfunc)
for k, g in groupby(data, keyfunc):
    groups.append(list(g))      # Store group iterator as a list
    uniquekeys.append(k)
```
Приклад (дано):
```python
from itertools import groupby
things = [
    ("animal", "bear"), ("animal", "duck"), 
    ("plant", "cactus"),
    ("vehicle", "speed boat"), ("vehicle", "school bus")
]
```
...
```python
for key, group in groupby(things, lambda x: x[0]):
    for thing in group:
        print("A %s is a %s." % (thing[1], key))
    print()

# Result
A bear is a animal.
A duck is a animal.

A cactus is a plant.

A speed boat is a vehicle.
A school bus is a vehicle.
```
...
```python
print(groupby(things, lambda x: x[0]))
print(list(groupby(things, lambda x: x[0])))
print(([i for i in list(groupby(things, lambda x: x[0]))][0][1]))
print(next([i for i in list(groupby(things, lambda x: x[0]))][0][1]))

# Result
<itertools.groupby object at 0x7f9dc04609a0>
[('animal', <itertools._grouper object at 0x7f9dc046f910>), ('plant', <itertools._grouper object at 0x7f9dc046f8e0>), ('vehicle', <itertools._grouper object at 0x7f9dc046f8b0>)]
<itertools._grouper object at 0x7f9dc046f940>
Traceback (most recent call last):
  File "/home/serhii/Projects/storage/temp.py", line 75, in <module>
    print(next([i for i in list(groupby(things, lambda x: x[0]))][0][1]))
StopIteration
```
Повернена група сама є ітератором, який **ділиться** основним ітератором із`groupby()`.
Оскільки джерело є спільним, коли об’єкт`groupby()`розширено, попередня група більше 
не відображається. Отже, якщо ці дані знадобляться пізніше, їх слід зберегти як список:
```python
groups = []
uniquekeys = []
for k, g in groupby(things, lambda x: x[0]):
    uniquekeys.append(k)
    groups.append(list(g))  # Store group iterator as a list

print(things)
print(uniquekeys)
print(groups)

# Result
[('animal', 'bear'), ('animal', 'duck'), ('plant', 'cactus'), ('vehicle', 'speed boat'), ('vehicle', 'school bus')]
['animal', 'plant', 'vehicle']
[[('animal', 'bear'), ('animal', 'duck')], [('plant', 'cactus')], [('vehicle', 'speed boat'), ('vehicle', 'school bus')]]
```
# List Comprehension (Генератор списков)

**List Comprehension** — это встроенный механизм ***генерации списков***. 

У него только одна задача — это построить [список](Python-List%20(Списки).md).<br> 
List Comprehension строит список из любого [итерируемого типа](../Паттерн/Паттерн-Итератор.md), 
преобразуя (фильтруя) поступаемые значения.

Синтаксис:
>[<способ формирования значения> for <переменная> in <итерируемый объект>]

<переменная> доступна *только* внутри генератора списка 

Non-list comprehension
```python
cart = [3, 4, 12, 17, 19, 21, 23, 26, 30]

cashier = []
for item in cart:
    cashier.append(item)

print(cashier)
Output: [3, 4, 12, 17, 19, 21, 23, 26, 30]
```
list comprehension
```python
cart = [3, 4, 12, 17, 19, 21, 23, 26, 30]

cashier = [item for item in cart]

print(cashier)
Output: [3, 4, 12, 17, 19, 21, 23, 26, 30]
```

**Non-list comprehension** vs **list comprehension**
```python
cashier = []
for item in cart:             VS       cashier = [item for item in cart]
    cashier.append(item)
```
**List Comprehension** работает при том быстрее чем `for` или `while`

Примеры:
```python
>>> inp = input("Целые числа через пробел: ")
Целые числа через пробел: >? 1 2 3 4
>>> inp
'1 2 3 4'

>>> list_comp = [int(i) for i in inp.split()]
>>>list_comp
[1, 2, 3, 4]
```

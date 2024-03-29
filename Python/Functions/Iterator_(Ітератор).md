# Итератор — Iterator

## Паттерн Iterator
< *Поведенческие* паттерны определяют эффективные способы между взаимодействия 
между объектами > 

[**Итератор**](https://refactoring.guru/ru/design-patterns/iterator) — это *поведенческий* 
[паттерн проектирования](../../Паттерн/Паттерн.md), который даёт возможность последовательно обходить элементы 
составных объектов, не раскрывая их внутреннего представления.

Идея паттерна **Итератор** состоит в том, чтобы вынести поведение обхода коллекции из самой коллекции 
в отдельный класс (т.е. сделать *универсальный механизм* обхода для разных типов коллекций).

## Iterator в Python

***Итерируемый объект (Iterable)*** — это объект, который предоставляет возможность
обойти поочередно свои элементы. <br>
Кроме того, это объект, из которого можно получить итератор. <br>
Примеры итерируемых объектов: все последовательности: [*str, list, range, set, dict, ...*]

***Итератор (Iterator)*** — это объект, порождаемый функцией `iter()` и 
поддерживающий функцию `next()`, который помнит, какой элемент будет взят следующим. 

Каждый итерируемый объект предоставляет доступ к своим элементам через итератор:
```
Iterator objеct, it:    it = iter(a)

Iterable object, a:   |      5      |      3      |      7      |

                           ^ it            ^ it          ^ it          ^ it
>>>   next()   >>>     next(a) = 5        ...       next(a) = 7     StopIteration
```

Итератор не имеет индексов и может быть использован **только один раз**!

### Протокол итератора:
1. Чтобы получить итератор мы должны передать функции`iter()`итерируемый объект.
2. Далее мы передаём итератор функции`next()`для перебора значений.
3. Когда элементы в итераторе закончились, порождается исключение`StopIteration`.

```python
>>> a = [5, 3, 7]
>>> it = iter(a)
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
Особенности:

- Любой объект, передаваемый функции `iter()` без исключения `TypeError` — **итерируемый объект**.
- Любой объект, передаваемый функции `next()` без исключения `TypeError` — **итератор**.
- Любой объект, передаваемый функции `iter()` и возвращающий сам себя — **итератор**.

Плюсы итераторов:
1. Итераторы работают "лениво" (*eng:* lazy). <br>
А это значит, что они не выполняют какой-либо работы, до тех пор, пока мы их об 
этом не попросим.
2. Таким образом, мы можем оптимизировать потребление ресурсов ОЗУ и CPU, 
а так же создавать бесконечные последовательности.

При работе с файлом в памяти будет находиться не весь файл, а только одна строка 
файла.

___
[Статья на Хабр](https://habr.com/ru/post/488112/)
##  Конструктор, инициализатор, деструктор класса 

`__new__(cls) и __init__(self)` — **конструктор** класса <br> 
`__init__(self)` — **инициализатор** класса <br>
`__del__(self)` — **деструктор** | **финализатор** класса <br>

Конструктор объекта:
- Шаг 1. Создание объекта в памяти устройства (метод `__new__`) <br>
- Шаг 2. Инициализация - создание локальных свойств|атрибутов объекта (метод `__init__`) <br>


## Метод `__new__`

`__new__(cls, *args, **kwargs)` — создает объект в оперативной памяти устройства <br>

*Принимает* в качестве параметров: <br>
`cls` — ссылку на текущий [класс](ООП.md) <br>
`*args, **kwargs` — и потом любые другие аргументы, которые будут переданы в `__init__` <br>

Всегда должен *возвращать* адрес нового созданного объекта !

`__new__(cls) и __init__(self)` — вместе это **конструктор** класса <br>
Вызываются последовательно при создании объекта.

Зачем два метода при создании объекта? <br>
Иногда надо что-то сделать до окончательного создания объекта! <br>
*Например*, реализация [паттерна](../Паттерн/Паттерн.md) Singleton.


А так`__new__`используется весьма редко, но иногда бывает полезен, в частности, 
когда класс наследуется от *immutable* (неизменяемого) типа данных, такого как 
tuple (кортеж) или str (строка).

## Метод `__init__`

`__new__(cls) и __init__(self)` — вместе это **конструктор** класса 

Инициализация объекта — это создание *локальных свойств* (добавление атрибутов) 
объекту.

`__init__(self, *args, **kwargs)` — это **инициализатор** класса <br>
Ему передаётся всё, с чем был вызван первоначальный конструктор <br> 

`__init__` всегда должен возвращать`None`!

*Например*, если мы вызываем `x = SomeClass(10, 'foo')`, <br> 
`__init__` получит `10` и `'foo`' в качестве аргументов. 


## Метод  `__del__(self)`

`__del__(self)` — это **деструктор** или **финализатор** класса <br>
Автоматически вызывается перед уничтожением экземпляра класса сборщиком мусора.  

Он *не определяет* поведение для выражения `del x` 
(поэтому этот код не эквивалентен `x.__del__()`).<br> 
Скорее, он определяет поведение объекта в то время, когда объект попадает 
в сборщик мусора.<br> 
Это может быть довольно удобно для объектов, которые могут требовать дополнительных 
чисток во время удаления, таких как сокеты или файловыве объекты. <br>
Однако, *нужно быть осторожным*, так как нет гарантии, что `__del__` будет вызван, 
если объект продолжает жить. 

[Лекция тут](https://github.com/PonomaryovVladyslav/PythonCources/blob/master/lesson16.md)
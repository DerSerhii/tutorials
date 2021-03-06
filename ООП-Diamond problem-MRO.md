# Diamond problem. MRO

Классы-наследники могут использовать родительские методы. 
Но что, если у нескольких родителей будут одинаковые методы? 
Какой метод в таком случае будет использовать наследник? 
##### Рассмотрим классический пример:
```python
class A:
    def hi(self):
        print("A")
 
class B(A):
    def hi(self):
        print("B")
 
class C(A):
    def hi(self):
        print("C")
 
class D(B, C):
    pass
 
d = D()
d.hi()
```
Эта ситуация, так называемое **ромбовидное наследование (diamond problem)** решается в Python 
путем установления ***порядка разрешения методов (MRO)***. 

В Python3 для определения порядка используется алгоритм поиска ***в ширину***, 
то есть сначала интерпретатор будет искать метод hi в классе B, 
если его там нету - в классе С, потом A. 

В Python2 используется алгоритм поиска в глубину, то есть в данном случае - сначала B, 
потом - А, потом С. 

В Python3 можно посмотреть в каком порядке будут проинспектированы 
родительские классы при помощи метода класса **mro()**:
```python
>>> D.mro()
[<class '__main__.D'>, <class '__main__.B'>, <class '__main__.C'>, <class '__main__.A'>, <class 'object'>]
```
Если необходимо использовать метод конкретного родителя, например hi() класса С, 
нужно напрямую вызвать его по имени класса, передав self в качестве аргумента:
```python
class D(B, C):
    def call_hi(self):
        C.hi(self)
 
d = D()
d.call_hi()
```

[Лекция тут](https://github.com/PonomaryovVladyslav/PythonCources/blob/master/lesson16.md)
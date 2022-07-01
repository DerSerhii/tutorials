# Super

__`super()`__ - это функция, что обращается к классу, от которого наследуется текущий класс.

```python
class A:
    def some_method(self):
        print('Spam, eggs!!1')


class B(A):
    def some_method(self):
        print('Hello, World!')


x = B()
x.some_method()

>>>Hello, World!
```
Мы ***перегрузили метод родительского класса***.

Но что, если нам потребуется всего лишь немного дополнить его? 
Как нам дополнить родительский метод, не копируя его полностью и не изобретая велосипедов? 
Тут нам и нужен super():
```python
class A:
    def some_method(self):
        print('Spam, eggs!!1')


class B(A):
    def some_method(self):
        super().some_method()
        print('Hello, World!')


x = B()
x.some_method()

>>>Spam, eggs!!1
>>>Hello, World!
```
С помощью super().some_method() мы вызвали родительский метод, а после дополнили свой. 
Именно для этого чаще всего используется эта функция.

[Лекция тут](https://github.com/PonomaryovVladyslav/PythonCources/blob/master/lesson16.md)
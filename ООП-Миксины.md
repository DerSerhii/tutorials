# Миксины
__`Наследование`__ - одна из основных парадигм [ООП](ООП.md).

В наследовании могут участвовать классы-примеси - **миксины**

__`Миксин`__ - это тип классов которые нужны, что бы добавлять к обычным классам какой-то метод 
или атрибут, но эти классы не используются в чистом виде, только как примесь.

Представим, что мы программируем класс для автомобиля. Мы хотим, чтобы у нас была возможность 
слушать музыку в машине. Конечно, можно просто добавить метод play_music() в класс Car:
```python
class Car:
    def ride(self):
        print("Riding a car")
 
    def play_music(self, song):
        print("Now playing: {} ".format(song))
 
>>> c = Car()
>>> c.ride()
Riding a car
>>> c.play_music("Queen - Bohemian Rhapsody")
Now playing: Queen - Bohemian Rhapsody
```
Но что если, у нас есть еще и телефон, радио или любой другой девайс, с которого мы будем 
слушать музыку. В таком случае, лучше вынести функционал проигрывания музыки в отдельный 
класс-миксин:

```python
class MusicPlayerMixin:
    def play_music(self, song):
        print("Now playing: {}".format(song))
```
Мы можем "домешивать" этот класс в любой, где нужна функция проигрывания музыки:
```python
class Smartphone(MusicPlayerMixin):
    pass
 
 
class Radio(MusicPlayerMixin):
    pass
 
 
class Amphibian(Auto, Boat, MusicPlayerMixin):
   pass
```

[Лекция тут](https://github.com/PonomaryovVladyslav/PythonCources/blob/master/lesson16.md)

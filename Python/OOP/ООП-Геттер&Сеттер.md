 # Геттер & Сеттер
 
Основное назначение – обеспечение [инкапсуляции](ООП-Инкапсуляция.md).

**Геттеры & сеттеры** применяются для доступа к инкапсулированным атрибутам извне класса. <br>
Их назначение не только в *доступе*, но и в *проверке* корректности данных.

```python
class Geek:
    def __init__(self, age = 0):
         self._age = age
      
    # getter method
    def get_age(self):
        return self._age
      
    # setter method
    def set_age(self, x):
        self._age = x
```
Дополнительно можно осуществлять контроль за изменениями атрибутов путем перегрузки
[магических методов](ООП-Magic%20methods.md): `__setattr__()`, `__getattribute__()`, `__getattr__()`, `__detattr__()`

- `__setattr__(self, name, value)` – автоматически вызывается при изменении свойства
`name` класса;
- `__getattribute__(self, name)`– автоматически вызывается при получении свойства 
класса с именем `name`;
- `__getattr__(self, name)` – автоматически вызывается при получении несуществующего 
свойства `name` класса;
- `__delattr__(self, name))` – автоматически вызывается при удалении свойства `name` 
(неважно: существует оно или нет).
```python
class Point:
	MAX_COORD = 100
	MIN_COORD = 0

	def __init__(self, x, y):
		self.x = x
		self.y = y

	def set_coord(self, x, y):
		if self.MIN_COORD <= x <= self.MAX_COORD:
			self.x = x
			self.y = y

	def __getattribute__(self, item):
		print('__getattribute__')
		if item == 'x':
			raise ValueError('Access is denied')
		else:
			return object.__getattribute__(self, item)

	def __setattr__(self, key, value):
		print('__setattr__')
		if key == 'z':
			raise AttributeError('invalid attribute name')
		else:
			self.__dict__[key] = value

	def __getattr__(self, item):
		print('__getattr__' + item)
		return False

	def __delattr__(self, item):
		print('__delattr__: ' + item)
		object.__delattr__(self, item)

pt1 = Point(1, 2)
pt2 = Point(10, 20)

pt1.z = 5
print(pt1.z)
print(pt1.yy)
del pt1.x
```

# Тестирование

### Расположение тестов в Django

Несмотря на то, что Django создаёт для нас в приложении файл `tests.py`, 
им практически никогда *не пользуются*.

Существует два самых распространённых способа хранения тестов: 
1. Если повезло и на вашем проекте есть специальные тестировщики. То ваша задача, это только 
***юнит тесты***.

И тогда в папке приложения создаётся еще одна папка `tests` в которой уже создаются файлы для тестов
различных частей, например `test_models.py`,` test_forms.py` итд.
```python
    > my_app
      > tests
        test_models.py
        test_forms.py
        test_view.py
```
2. Если не повезло, и на проекте вы и за автотестеров, то тогда в этой же папке (tests) создаётся 
еще 3 папки: `unit`, `integration` и `acceptance` и уже в них описываются различные тесты.

### Запуск тестов

Предположим, что у нас в приложении `animals`, есть папка `tests`, в ней папка `unit` и в ней файл `test_models`.

```python
from django.test import TestCase
from myapp.models import Animal

class AnimalTestCase(TestCase):
    def setUp(self):
        Animal.objects.create(name="lion", sound="roar")
        Animal.objects.create(name="cat", sound="meow")

    def test_animals_can_speak(self):
        """Animals that can speak are correctly identified"""
        lion = Animal.objects.get(name="lion")
        cat = Animal.objects.get(name="cat")
        self.assertEqual(lion.speak(), 'The lion says "roar"')
        self.assertEqual(cat.speak(), 'The cat says "meow"')
```

То для запуска тестов используется менедж команда `test`

```python
# Запустить все тесты в приложении, в папке тестов
$./manage.py test animals.tests

# Запустить все тесты в приложении
$./manage.py test animals

# Запустить один тест кейс
$./manage.py test animals.tests.unit.test_models.AnimalTestCase

# Запустить один тест из тест кейса
$./manage.py test animals.tests.unit.test_models.AnimalTestCase.test_animals_can_speak
```

Лекция по тестированию [тут](https://github.com/PonomaryovVladyslav/PythonCources/blob/master/lesson40.md
)


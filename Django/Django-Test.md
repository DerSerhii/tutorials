# Тестирование

### Уровни тестирования

![](https://camo.githubusercontent.com/2e981f10a73edc74f8080b4ed525cea5eb6063a75013b5559ab1cbe76e137bbb/68747470733a2f2f686162726173746f726167652e6f72672f73746f72616765322f6563332f3832352f6337662f65633338323563376630373130663966656436383134633839623739346465642e6a7067)

Существует 4 основных уровня тестирования функционала.

- `Модульные тесты (Unit tests)` — это тесты проверяющие функционал конкретного модуля минимального размера. 

*Например*, вы переписали метод `get_context_data`, то юнит тестом будет попытка вызвать этот метод с разными входными 
данными, и посмотреть на то, что вернёт результат.

Юнит-тест подразумевает проверка модуля с подачей разных данных (правильных и нет) на вход. 

- `Интеграционные тесты (Integration tests)` — это тесты проверяющие целостность работы системы без сторонних средств. 

*Например*, вы переписали метод `get_context_data`, выполняем запрос при помощи кода, и смотрим,
изменилась ли переменная `context` в ответе на наш запрос.

*Интеграционный подразумевает "request-response".*

- `Приёмочные "ацептанс" тесты (Acceptance tests)` — это тесты с полной имитацией действий пользователя. 

При помощи специальных средств (например Selenium), мы прописываем код открытия браузера, поиска необходимых элементов 
на странице, имитация ввода данных, нажатие кнопок, перехода по ссылкам итд.

*Ацептанс тест подразумевает имитацию браузера.*

- `Ручные тесты (Manual tests)` — это такие тесты, когда мы полностью повторяем потенциальные действия пользователя.

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

### База данных для тестирования
Для тестов используется отдельная база данных, которая будет указана в переменной `TEST` в переменной `DATABASES`
в файле `settings.py`:
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'USER': 'mydatabaseuser',
        'NAME': 'mydatabase',
        'TEST': {
            'NAME': 'mytestdatabase',
        },
    },
}
```
Эта база будет изначально пустая, и будет очищаться после каждого выполненного тест кейса !!

**Ваш юзер должен иметь права на создание и очистку базы данных !!**

Создание и подключение БД [тут](../Django-Подключние%20БД%20.md)

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


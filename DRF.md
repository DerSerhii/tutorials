# Django REST Framework

Django Rest Framework (DRF) — это пекедж (пакет), который работает со стандартными 
[моделями](Django-MVT-Model.md) Django 
для создания [API](REST%20API.md) для проекта c применением [REST](REST%20API.md) архитектуры.

---
Установка: `pip install djangorestframework`

Не забываем добавить в `INSTALLED_APPS` — `'rest_framework'`

### Основная архитектура
API DRF состоит из 3-х слоев: 
- `Serializer (Сериалайзер)`
- `View (Вид)` 
- `Router (маршрутизатор)`

[Serializer (Сериалайзер)](DRF-Сериалайзеры.md) преобразует информацию (хранящуюся в базе данных и 
определенную с помощью [моделей](Django-MVT-Model.md) Django) в формат, который легко и эффективно 
передается через API. Сериалайзеры анализирует информацию в обоих направлениях (чтение и запись).

[View (Вид)](DRF-View.md) определяет функции CRUD (чтение, создание, обновление, удаление), 
которые будут доступны через API.

[Router (маршрутизатор)](DRF-Router.md) определяет URL-адреса, которые будут предоставлять 
доступ к каждому View (виду).

### Serializer (Сериализатор)

[Модели](Django-MVT-Model.md) Django (интуитивно) представляют данные, хранящиеся в базе, 
но [API](REST%20API.md) должен передавать информацию в менее сложной структуре. 
Хотя данные будут представлены как экземпляры классов Model, их необходимо перевести 
в (формат JSON) для передачи через API.

Сериалайзер DRF производит это преобразование. Когда пользователь передает информацию 
(например, создание нового экземпляра) через API, сериалайзер берет данные, 
проверяет их и преобразует в нечто, что Django может сложить в экземпляр модели. 
Аналогичным образом, когда пользователь обращается к информации через API, 
соответствующие экземпляры передаются в сериалайзер, который преобразовывает их в формат, 
который может быть легко передан пользователю (как JSON).

Наиболее распространенной формой, которую принимает сериалайзер DRF, является тот, 
который привязан непосредственно к модели Django:
```python
class ThingSerializer(serializers.ModelSerializer):
  class Meta:
    model = Thing
    fields = (‘name’, )
```

Сериалайзеры — это невероятно гибкий и мощный компонент DRF. 
Хотя подключение сериалайзера к модели является наиболее распространенным, 
сериалайзеры могут использоваться для создания любой структуры данных Python через API 
в соответствии с определенными параметрами.

### View (Вид)

[View](DRF-View.md) - это тот код, в котором мы определяем доступные операции. 
Наиболее распространенным ModelViewSet, который имеет следующие 
встроенные операции:

- `create()` — создание экземпляра
- `retrieve()` — получение/чтение экземпляра 
- `update()` или `partial_update()` — обновление экземпляра (все или только выбранные поля) 
- `destroy()` - уничтожение/удаление экземпляра 
- `list()` - список экземпляров (с разбивкой по страницам по умолчанию) 

Каждая из этих функций может быть переопределена, если требуется другое поведение, 
но стандартная функциональность работает с минимальным кодом.

### Router (маршрутизатор)

Роутеры предоставляют верхний уровень API. 
Чтобы избежать создания бесконечных URL-адресов вида: «списки», «детали» и «изменить», 
маршрутизаторы DRF объединяют все URL-адреса, необходимые для данного вида в одну строку для 
каждого ViewSet, например:
```python
# Инициализация роутера DRF. Только один раз на файл urls.py
# из маршрутизаторов импорта rest_framework

router = routers.DefaultRouter()

# Регистрация ViewSet
router.register(r'thing', main_api.ThingViewSet)
```

Затем все ViewSet, которые зарегистрированные в роутере, можно добавить к обычным url_patterns:
```python
url_patterns + = url (r '^', include (router.urls))
```
Теперь через API можно получить данные точно так же, как и любые другие обычные страницы Django.

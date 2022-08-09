# Сериалайзеры

***Сериалайзер*** в [DRF](DRF.md) — это класс для преобразования данных в требуемый формат (Обычно JSON).

 ***Сериализация*** — это процесс преобразования данных в формат, который может быть сохранен или 
передан, с последующим его восстановлением. 

---
1. Поля сериалайзеров и их особенности
2. Валидация сериалайзеров
3. 
---

### 1. Поля сериалайзеров и их особенности

Любое из полей может иметь такие аргументы:

 `read_only=` — поле только для чтения (по дефолту False)

Используется для полей которые не планируются к заполнению (*например*, время создания комментария),
но планируются к чтению (*например*, отобразить когда был написан комментарий). 
Такие поля не принимаются при создании или изменении.

`write_only=`— поле только для записи (по дефолту False)

Поля не планируемые для отображения, но необходимые для записи (Пароль, номер карточки, итд.). 

`required=` — обязательность поля (по дефолту True)

`default=` — значение по умолчанию, если не указано ничего другого. 

Не поддерживается при частичном обновлении.

`allow_null=` — позволить значению поля быть None (по дефолту False)

`source=` — поле, значение которого необходимо получить в модели. *К примеру:*

- при помощи какого-то метода <br>
(вычисление полного адреса из его частей при помощи метода модели и декоратора
property `CharField(source='get_full_address')`)
- какого-то вложенного объекта <br>
(Foreign Key на юзера, но необходим только его имейл, а не целый объект, 
`EmailField(source='user.email'))`
- имеет спец значение `*` <br>
  (обозначает что источник данных будет передан позже, тогда его нужно будет указать в 
необходимых методах. По дефолту, это имя поля)

`validators=` — список валидаторов

`error_messages=` - словарь с кодом ошибок

### 2. Валидация сериалайзеров

(*Валидация* — это проверка на соответствие заданным критериям) 

Для валидации сериалайзеров существует метод `is_valid()`

Сериализируемые данные **от пользователя** — ***валидируем*** !! 
- передаём в сериалайзер через атрибут `data=` 
- сериалайзер валидируем `is_valid()`

В данных могут быть ошибки 
```python
serializer = CommentSerializer(data={'user': {'email': 'foobar', 'username': 'doe'}, 'content': 'baz'})
serializer.is_valid()
# False
serializer.errors
# {'user': {'email': ['Enter a valid e-mail address.']}, 'created': ['This field is required.']}
```

- если ошибок нет, то данные будут находиться в атрибуте `validated_data`
```python
serializer.is_valid()
serializer.validated_data
# OrderedDict([('title', ''), ('code', 'print("hello, world")\n'), ('linenos', False), ('language', 'python'), ('style', 'friendly')])
```

Сериализируемые данные **из БД** — ***нет необходимости*** валидировать !! 

- передаем без каких-либо атрибутов
- данные будут находиться в атрибуте `data` 
```python
comment = Comment.objects.first()
serializer = CommentSerializer(comment)
serializer.data
```

По аналогии с [формами](Django-Формы(Form%20&%20ModelForm).md), мы можем добавить валидацию 
*каждого отдельного поля*

Метод `validate_<field_name>` возвращает значение или рейзит ошибку валидации:
```python
class BlogPostSerializer(serializers.Serializer):
    title = serializers.CharField(max_length=100)
    content = serializers.CharField()

    def validate_title(self, value):
        if 'django' not in value.lower():
            raise serializers.ValidationError("Blog post is not about Django")
        return value
```
Так же валидация может быть осуществлена *на уровне объекта*. 
Метод `validate`:
```python
class EventSerializer(serializers.Serializer):
    description = serializers.CharField(max_length=100)
    start = serializers.DateTimeField()
    finish = serializers.DateTimeField()

    def validate(self, data):
        if data['start'] > data['finish']:
            raise serializers.ValidationError("finish must occur after start")
        return data
```
Так же можно прописать валидаторы как отдельные функции:
```python
def multiple_of_ten(value):
    if value % 10 != 0:
        raise serializers.ValidationError('Not a multiple of ten')


class GameRecord(serializers.Serializer):
    score = IntegerField(validators=[multiple_of_ten])
    ...
```
Или указать в `Meta`, используя уже существующие валидаторы:
```python
class EventSerializer(serializers.Serializer):
    name = serializers.CharField()
    room_number = serializers.IntegerField(choices=[101, 102, 103, 201])
    date = serializers.DateField()

    class Meta:
        # Each room only has one event per day.
        validators = [
            UniqueTogetherValidator(
                queryset=Event.objects.all(),
                fields=['room_number', 'date']
            )
        ]
```


#### Вложенные сериалайзеры:

Сериалайзер, может полем другого сериалайзера, такие сериалайзеры, называются 
***вложенными***.

Вложенное поле с атрибутом __`many=True`__  означает что оно принимает ***список*** 
или [***кверисет***](Django-MTV-Model-ORM.md) таких объектов.


### Метод save
У моделсериалайзеров, по аналогии с [моделформами](Django-Формы(Form & ModelForm).md), есть метод 
`save()`, но в отличие от моделформ, дополнительные данные можно передать 
прямо в атрибуты метода сейв.


Лекция [тут](https://github.com/PonomaryovVladyslav/PythonCources/blob/master/lesson37.md)
# Сериалайзеры Django Rest Framework

***Serializer DRF (Сериалайзер)*** — это класс для преобразования данных
(хранящихся в [базе данных](../БД/БД-DataBases.md) и определенных с помощью 
[моделей](../Django/Django-MVT-Model.md) Django) в требуемый формат для передачи 
через API (обычно в формат JSON). 

Сериалайзеры преобразуют данные ***в обоих направлениях*** (чтение и запись).

### Чтение данных пользователем
Сериализируемые данные из *базы данных* — нет необходимости валидировать !!
- передаем без каких-либо атрибутов
- данные будут находиться в атрибуте `.data`
```commandline
>>> serializer = SnippetSerializer(snippet)
>>> serializer.data
{'id': 2, 'title': '', 'code': 'print("hello, world")\n', 'linenos': False}
```
Можно сериализовать ***queryset*** наборы запросов вместо **экземпляров модели**. <br>
Для этого мы просто добавляем флаг `many=True` к аргументам сериализатора.
```commandline
>>> serializer = SnippetSerializer(Snippet.objects.all(), many=True)
>>> serializer.data
[OrderedDict([('id', 1), ('title', ''), ('code', 'foo = "bar"\n'), ('linenos', False)]),
 OrderedDict([('id', 2), ('title', ''), ('code', 'print("hello, world")\n'), ('linenos', False)]),
 OrderedDict([('id', 3), ('title', ''), ('code', 'print("hello, world")'), ('linenos', False)])]
```


### Запись данных от пользователя
Сериализируемые данные *от пользователя* — ***валидируем*** !! <br>

- данные передаём в сериалайзер через атрибут `data=` 
- сериалайзер валидируем при помощи метода `is_valid()`
- если ошибок нет, то данные будут находиться в атрибуте `.validated_data`
- создаем запись в БД методом `save()` сериалайзера <br>
[если метод `create()` реализован]
```commandline
>>> serializer = SnippetSerializer(data=data)
>>> serializer.is_valid()
True
>>> serializer.validated_data
OrderedDict([('title', ''), ('code', 'print("hello, world")\n'), ('linenos', False)])
>>> serializer.save()
<Snippet: Snippet object>
```
## Валидация сериалайзеров
(*Валидация* — это проверка на соответствие заданным критериям) <br>
Валидация сериалайзера производиться при помощи метода `is_valid()`


По аналогии с [формами](../Django/Django-Формы(Form%20&%20ModelForm).md), мы можем добавить валидацию 
*каждого отдельного поля*

Метод `validate_<field_name>()` возвращает значение или рейзит ошибку валидации:
```python
class BlogPostSerializer(serializers.Serializer):
    title = serializers.CharField(max_length=100)
    content = serializers.CharField()

    def validate_title(self, value):
        if 'django' not in value.lower():
            raise serializers.ValidationError("Blog post is not about Django")
        return value
```
Так же валидация может быть осуществлена *на уровне объекта*. <br>
Метод `validate()`:
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
Или указать в `class Meta`, используя уже существующие валидаторы:
```python
class EventSerializer(serializers.Serializer):
    name = serializers.CharField()
    room_number = serializers.IntegerField(choices=[101, 102, 103, 201])
    date = serializers.DateField()

    class Meta:
        validators = [
            UniqueTogetherValidator(
                queryset=Event.objects.all(),
                fields=['room_number', 'date']
            )
        ]
```

## Поля сериалайзеров и их особенности

Любое из полей может иметь такие аргументы:

`read_only=` — **поле только для чтения** (*по дефолту **False***) <br>
Используется для полей которые *не планируются к заполнению* <br>
(*например*, время создания комментария), <br>
но *планируются к чтению* <br>
(*например*, отобразить когда был написан комментарий). <br>
Такие поля не принимаются при создании или изменении.

`write_only=`— **поле только для записи** (*по дефолту **False***) <br>
Поле *не планируемые для отображения*, <br>
но необходимые для записи <br>
(*например*, пароль, номер карточки, итд). 

`required=` — **обязательность поля** (*по дефолту **True***)

`default=` — **значение по умолчанию**, если не указано ничего другого. <br>
Не поддерживается при частичном обновлении.

`allow_null=` — **позволить значению поля быть ***None***** (*по дефолту **False***)

`source=` — **поле, значение которого необходимо получить в модели.** <br>
- при помощи какого-то метода <br>
(вычисление полного адреса из его частей при помощи метода модели и декоратора
property `CharField(source='get_full_address')`)
- какого-то вложенного объекта <br>
(Foreign Key на юзера, но необходим только его имейл, а не целый объект, 
`EmailField(source='user.email'))`
- имеет спец значение `*` <br>
  (обозначает что источник данных будет передан позже, тогда его нужно будет указать в 
необходимых методах. По дефолту, это имя поля)

`validators=` — **список валидаторов**

`error_messages=` — **словарь с кодом ошибок**

## Вложенные сериалайзеры

Сериалайзер, может полем другого сериалайзера, такие сериалайзеры, называются 
***вложенными***.

Вложенное поле с атрибутом __`many=True`__  означает что оно принимает *список* 
или [*кверисет*](../Django/Django-MTV-Model-ORM.md) таких объектов.


## ModelSerializers - сериалайзеры модели
Так же, как Django предоставляет `Form`классы и `ModelForm`классы, среда REST включает 
в себя `Serializer`классы и `ModelSerializer`классы.

`ModelSerializer`классы не делают ничего волшебного, они просто ярлык для создания 
классов сериалайзера:
- автоматически определяемый набор полей;
- реализация по умолчанию методов `create()`и `update()`
### Метод save
У `ModelSerializer` по аналогии с [ModelForm](../Django/Django-Формы(Form%20&%20ModelForm).md), 
есть метод `save()`, но в отличие от форм, дополнительные данные можно передать 
**прямо в атрибуты метода**.


Лекция [тут](https://github.com/PonomaryovVladyslav/PythonCources/blob/master/lesson37.md)
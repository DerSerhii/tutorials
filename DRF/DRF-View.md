# Представления Django Rest Framework

***View (Представление) [DRF](DRF.md)*** — определяет действия CRUD (чтение, создание, обновление, удаление), 
которые будут доступны через [API](REST%20API.md).

DRF предоставляет две оболочки, которые можно использовать для написания 
представлений API:
- `@api_view`— декоратор для работы с представлениями на основе функций.
- `APIView`класс — для работы с представлениями на основе классов.

## Class Based View DRF
Cайт по Class Based View DRF — [CFRF](https://www.cdrf.co/)

### APIView
DRF`APIView`класс — подкласс Django`View`класс. <br>
Используется с той же целью, что и Django`View`: входящий запрос направляется соответствующему 
методу обработчика <br>
"Магия" превращения HTTP-методов (`GET`,`POST`, etc) в Python-методы (`get()`, `post()`, etc) 

### GenericAPIView

`GenericAPIView` — базовый класс для всех generic view (наследуется от `APIView`)

В нём описаны такие атрибуты как: <br>
`queryset = None` — хранит кверисет <br>
`serializer_class = None` — хранит сериалайзер <br>
`lookup_field = pk` — название атрибута в модели который будет отвечать за `pk` <br>
`lookup_url_kwarg = None` — название атрибута в запросе который будет отвечать за `pk` <br>
`filter_backends = []` — фильтры запросов <br>
`pagination_class = None` — пагинация запросов <br>
`paginator` — объект пагинации <br>

И методы: <br>
`get_queryset()`— получение кверисета <br>
`get_object()` — получение одного объекта <br>
`get_serializer()` — получение объекта сериалайзера <br>
`get_serializer_class()` — получение класса сериалайзера <br>
`get_serializer_context()` — получить контекст сериалайзера <br>
`filter_queryset()` — отфильтровать кверисет <br>
`paginate_queryset()` — пагинировать кверисет <br>
`get_paginated_response()` — получить пагинированый ответ <br>

*Такой класс не работает самостоятельно, только вместе с определёнными миксинами !*

### Mixins
В DRF существует 5 миксинов: <br>
`CreateModelMixin` — создание экземпляра модели <br>
`RetrieveModelMixin` — получение экземпляра модели <br>
`UpdateModelMixin` — обновление экземпляра модели <br>
`DestroyModelMixin` — удаление экземпляра модели <br>
`ListModelMixin` — отображение кверисета, страничная пагинация <br>

### Generics классы
По аналогии с Django, существуют классы с заранее описанными CRUD действиями. <br>
Эти классы наследуют логику работы с данными из необходимого **миксина**, <br>
общие методы из `GenericAPIView`, <br>
и дальше описываются методы тех видов запросов, которые нужно обрабатывать,
вызывая необходимый метод из **миксина**.

Generic DRF: <br>
`CreateAPIView` — view'ха для создания экземпляра модели (описан метод `post()`)<br>
`DestroyAPIView` — view'ха для удаления экземпляра модели (описан метод `delete()`)<br>
`ListAPIView` — view'ха для отображения кверисета (описан метод `get()`)<br>
`ListCreateAPIView` — view'ха для отображения кверисета и создания экземпляра модели (описаны методы `get()`и`post()`) <br>
`RetrieveAPIView` — view'ха для получения экземпляра модели (описан метод `get()`)<br>
`RetrieveUpdateAPIView` — view'ха для получения и обновления экземпляра модели (описаны методы `get()`,`put()`и`patch()`) <br>   
`RetrieveDestroyAPIView` — view'ха для получения и удаления экземпляра модели (описаны методы `get()`и`delete()`) <br>
`RetrieveUpdateDestroyAPIView` — view'ха для получения, обновления и удаления экземпляра модели (описаны методы `get()`,`put()`,`patch()`и`delete()`)
`UpdateAPIView` — view'ха для обновления экземпляра модели (описаны методы `put()`и`patch()`) <br>

***Переписываются методы `create()`, `destroy()` итд, а не `get()`, `post()` !***

### ViewSets классы
`ViewSet` — базовый класс для всех ViewSet, по умолчанию не предоставляет никаких действий. 

---
Лекция [тут](https://github.com/PonomaryovVladyslav/PythonCources/blob/master/lesson38.md)




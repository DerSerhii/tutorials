# CBV

CBV — абстрактные классы, реализующие общие задачи веб-разработки.<br>
Они мощные, с широким функционалом, расширяемые, широко используют [множественное наследование](ООП-Множественное%20наследование.md).


Мега сайт — [Classy Class-Based Views](https://ccbv.co.uk/)

## TemplateView

**TemplateView** — простенький класс view для рендера `html` файлов.

Основные атрибуты:
```python
template_name = None  # Имя html файла который нужно рендерить
extra_content = None  # Словарь с контентом
```
Основные методы:
- описан метод `get()` 
```python
def get(self, request, *args, **kwargs):
    context = self.get_context_data(**kwargs)
    return self.render_to_response(context)
```
- `get_context_data()` — метод возвращающий данные которые будут добавлены в контекст

Лекция по [TemplateView](https://github.com/DerSerhii/PythonCources/blob/master/lesson33.md#class-templateview)


## DetailView

**DetailView** — класс view, который необходим для того что бы сделать страницу для 
просмотра одного объекта.

Ему необходимо передать `pk` либо `slug` и это позволит отобразить один объект (статью, товар итд.)

Если `template_name` не указан явно, то Django, будет пытаться отобразить 
`templates/app_name/model_detail.html`,<br> 
где `app_name` - название приложения, `model` - название модели, `detail` - константа.

Важные параметры:
```python
pk_url_kwarg = 'pk'  # Как переменная называется в urls.py, например `<int:my_id>`
queryset = None  # если указан, то возможность ограничить доступ только для части объектов (например, убрать из возможности обновления деактивированные объекты).
template_name = None  # указать имя шаблона.
model = None  # класс модели, если не указан queryset, сгенерирует queryset из модели.
```
Важные методы:<br>
`get_queryset()` - переопределить queryset<br>
`get_context_data()` - метод возвращающий данные, которые будут добавлены в контекст<br>
`get_object()` - определяет логику получения объекта

## UpdateView

**UpdateView** — класс view для обновления объекта c отображением на темплейте.

Методы и атрибуты почти полностью совпадают с *CreateView*, только перед действиями 
вызывает метод `get_object()`, для получения нужного объекта, и `url` должен принимать 
`pk` или `slug` для определения этого объекта.

#### Некоторые методы:
- `get_initial()` — возвращает исходные данные используемые в 
[формах](Django-Формы(Form%20&%20ModelForm).md) в этом представлении.<br>
Можно переопределить:
```python
def get_initial():
    return {'template' : 'foo' }
```

Лекция по [UpdateView](https://github.com/DerSerhii/PythonCources/blob/master/lesson33.md#class-updateview)


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


## CreateView

**CreateView** — класс view для создания объектов.

В класс нужно передать либо `ModelForm`, либо модель и поля, что бы класс 
сам сгенерировал такую форму.

Метод `get` откроет страницу, на которой будет переменая `form`, как и другие *view*,
к которым добавляется форма.

Метод `post` выполнит те же действия, что и `FormView`, но в случае валидности 
формы, предварительно выполнит `form.save()`.

***Важные параметры:***<br>
Такие же, как у `FormView` и еще свои:
```python
form_class = None  # Должен принимать ModelForm
model = None  # Можно указать модель вместо формы, что бы сгенерировать её на ходу
fields = None  # Поля модели, если не указана форма
```
***Важные методы:*** <br>
Все методы из `FormView`, но дополненные под создание объекта: <br>
- `post()` — предварительно добавит классу атрибут `self.object = None` <br>
- `form_valid()` — дополнительно выполнит такую строку `self.object = form.save()` <br>

Лекция по [CreateView](https://github.com/PonomaryovVladyslav/PythonCources/blob/master/lesson33.md#class-createview)



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

Лекция по [UpdateView](https://github.com/PonomaryovVladyslav/PythonCources/blob/master/lesson33.md)

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


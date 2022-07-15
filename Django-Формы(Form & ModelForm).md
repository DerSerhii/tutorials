# Формы

### Валидность

**Валидность** — это соответствие заданным критериям. 

Например, если мы ожидаем, что нам пришлют возраст, и мы ожидаем цифру, но нам присылают букву, это значит, что данные не валидны.

Некоторые распространённые виды валидаций можно указать как атрибут поля формы, например, 
максимальную длинну для строки, или максимальное и минимальное значение для числа.

## ModelForm

[**ModelForm**](https://docs.djangoproject.com/en/3.1/topics/forms/modelforms/) - это тип 
формы который генерируется напрямую из модели.

```python
from django.forms import ModelForm

class AuthorForm(ModelForm):
    class Meta:
        model = Author
        fields = ['name', 'title', 'birth_date']


class BookForm(ModelForm):
    class Meta:
        model = Book
        exclude = ['dob']
```

Поле `fields` либо `exclude` являются *обязательными* !

### Валидация
Помимо стандартного метода `is_valid()` у ModelForm существует так же встроенный метод `full_clean()`

Если первый отвечает за валидацию формы, то второй отвечает за валидацию для объекта модели.

### Метод `save()` у формы
Метод `save()` в **ModelForm** объекте выполняет по сути два действия:
1. получает объект модели основываясь на переданных данных 
2. вызывает метод `save()`, но уже для модели

Метод `save()` может принимать аргумент `commit=`, который по умолчанию `True`. 

Если указать `commit=` как `False`, метод `save()` *модели* не будет вызван 
(объект не будет сохранён в базу), будет только создан предварительный объект модели.

Используется, когда нужно "дополнить" данные перед сохранением в базу. 
Очень часто используется! Например, для добавления пользователя из `request`.
```python
form = PartialAuthorForm(request.POST)
author = form.save(commit=False)
author.title = 'Mr'
author.save()
```

### Передача объекта

Такая форма может принимать не только данные, но и целый объект из базы:

```python
from myapp.models import Article
from myapp.forms import ArticleForm

# Create a form instance from POST data.
f = ArticleForm(request.POST)

# Save a new Article object from the form's data.
new_article = f.save()

# Create a form to edit an existing Article, but use
# POST data to populate the form.
a = Article.objects.get(pk=1)
f = ArticleForm(request.POST, instance=a)
f.save()
```
Так как мы можем не только создавать новый инстанс, но и обновлять существующий.

Лекция [тут](https://github.com/PonomaryovVladyslav/PythonCources/blob/master/lesson33.md)
# Модуль pickle

Модуль`pickle`реализует мощный алгоритм **сериализации** и **десериализации**
объектов Python.

**pickling** - процесс преобразования объекта Python в поток байтов, <br> 
**unpickling** - обратная операция, в результате которой поток байтов преобразуется 
обратно в Python-объект. 

Так как поток байтов легко можно записать в файл, модуль`pickle`широко применяется
для сохранения и загрузки сложных объектов в Python.

>Не загружайте с помощью модуля pickle файлы из ненадёжных источников. <br> 
>Это может привести к необратимым последствиям.

Модуль`pickle`предоставляет следующие функции для удобства сохранения/загрузки 
объектов:

- `pickle.dump(obj, file, protocol=None, *, fix_imports=True)` <br> 
Записывает *сериализованный* объект в файл. <br> 
Дополнительный аргумент`protocol`указывает используемый протокол. <br>
По умолчанию равен 3 и именно он рекомендован для использования в Python 3
(несмотря на то, что в Python 3.4 добавили протокол версии 4 с некоторыми оптимизациями).<br>
В любом случае, записывать и загружать надо с одним и тем же протоколом.


- `pickle.dumps(obj, protocol=None, *, fix_imports=True)` <br>
Возвращает *сериализованный* объект. <br>
Впоследствии вы его можете использовать как угодно.


- `pickle.load(file, *, fix_imports=True, encoding="ASCII", errors="strict")` <br>
Загружает объект из файла.


- `pickle.loads(bytes_object, *, fix_imports=True, encoding="ASCII", errors="strict")` <br>
Загружает объект из потока байт.

Модуль`pickle`также определяет несколько [исключений](Python-Exceptions.md):
- pickle.PickleError
  - pickle.PicklingError - случились проблемы с сериализацией объекта.
  - pickle.UnpicklingError - случились проблемы с десериализацией объекта.

```python
>>> import pickle

>>> data = {
...     'a': [1, 2.0, 3, 4+6j],
...     'b': ("character string", b"byte string"),
...     'c': {None, True, False}
... }

>>> with open('data.pickle', 'wb') as f:
...     pickle.dump(data, f)
...
>>> with open('data.pickle', 'rb') as f:
...     data_new = pickle.load(f)
...

>>> print(data_new)
{'c': {False, True, None}, 'a': [1, 2.0, 3, (4+6j)], 'b': ('character string', b'byte string')}
```
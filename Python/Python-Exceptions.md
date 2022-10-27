# Exceptions (Исключения)

## Иерархия исключений
```python
BaseException
 +-- SystemExit
 +-- KeyboardInterrupt
 +-- GeneratorExit
 +-- Exception
      +-- StopIteration
      +-- StopAsyncIteration
      +-- ArithmeticError
      |    +-- FloatingPointError
      |    +-- OverflowError
      |    +-- ZeroDivisionError
      +-- AssertionError
      +-- AttributeError
      +-- BufferError
      +-- EOFError
      +-- ImportError
      |    +-- ModuleNotFoundError
      +-- LookupError
      |    +-- IndexError
      |    +-- KeyError
      +-- MemoryError
      +-- NameError
      |    +-- UnboundLocalError
      +-- OSError
      |    +-- BlockingIOError
      |    +-- ChildProcessError
      |    +-- ConnectionError
      |    |    +-- BrokenPipeError
      |    |    +-- ConnectionAbortedError
      |    |    +-- ConnectionRefusedError
      |    |    +-- ConnectionResetError
      |    +-- FileExistsError
      |    +-- FileNotFoundError
      |    +-- InterruptedError
      |    +-- IsADirectoryError
      |    +-- NotADirectoryError
      |    +-- PermissionError
      |    +-- ProcessLookupError
      |    +-- TimeoutError
      +-- ReferenceError
      +-- RuntimeError
      |    +-- NotImplementedError
      |    +-- RecursionError
      +-- SyntaxError
      |    +-- IndentationError
      |         +-- TabError
      +-- SystemError
      +-- TypeError
      +-- ValueError
      |    +-- UnicodeError
      |         +-- UnicodeDecodeError
      |         +-- UnicodeEncodeError
      |         +-- UnicodeTranslateError
      +-- Warning
           +-- DeprecationWarning
           +-- PendingDeprecationWarning
           +-- RuntimeWarning
           +-- SyntaxWarning
           +-- UserWarning
           +-- FutureWarning
           +-- ImportWarning
           +-- UnicodeWarning
           +-- BytesWarning
           +-- ResourceWarning
```

## Обзор исключений
- `BaseException` - базовое исключение, от которого берут начало все остальные.
  - ***SystemExit*** - исключение, порождаемое функцией sys.exit при выходе из программы.
  - ***KeyboardInterrupt*** - порождается при прерывании программы пользователем (обычно сочетанием клавиш Ctrl+C).
  - ***GeneratorExit*** - порождается при вызове метода close объекта generator.
  - ***Exception*** - а вот тут уже заканчиваются полностью системные исключения (которые лучше не трогать) и начинаются обыкновенные, с которыми можно работать.
    - **StopIteration** - порождается встроенной функцией next, если в итераторе больше нет элементов.
    - **ArithmeticError** - арифметическая ошибка.
      - *FloatingPointError* - порождается при неудачном выполнении операции с плавающей запятой. На практике встречается нечасто.
      - *OverflowError* - возникает, когда результат арифметической операции слишком велик для представления. Не появляется при обычной работе с целыми числами (так как python поддерживает длинные числа), но может возникать в некоторых других случаях.
      - *ZeroDivisionError* - деление на ноль.
    - **AssertionError** - выражение в функции assert ложно.
    - **AttributeError** - объект не имеет данного атрибута (значения или метода).
    - **BufferError** - операция, связанная с буфером, не может быть выполнена.
    - **EOFError** - функция наткнулась на конец файла и не смогла прочитать то, что хотела.
    - **ImportError** - не удалось импортирование модуля или его атрибута.
    - **LookupError** - некорректный индекс или ключ.
       - *IndexError* - индекс не входит в диапазон элементов.
       - *KeyError* - несуществующий ключ (в словаре, множестве или другом объекте).
    - **MemoryError** - недостаточно памяти.
    - **NameError** - не найдено переменной с таким именем.
      - *UnboundLocalError* - сделана ссылка на локальную переменную в функции, но переменная не определена ранее.
    - **OSError** - ошибка, связанная с системой.
        - *BlockingIOError*
        - *ChildProcessError* - неудача при операции с дочерним процессом.
        - *ConnectionError* - базовый класс для исключений, связанных с подключениями.
          - BrokenPipeError
          - ConnectionAbortedError
          - ConnectionRefusedError
          - ConnectionResetError
        - *FileExistsError* - попытка создания файла или директории, которая уже существует.
        - *FileNotFoundError* - файл или директория не существует.
        - *InterruptedError* - системный вызов прерван входящим сигналом.
        - *IsADirectoryError* - ожидался файл, но это директория.
        - *NotADirectoryError* - ожидалась директория, но это файл.
        - *PermissionError* - не хватает прав доступа.
        - *ProcessLookupError* - указанного процесса не существует.
        - *TimeoutError* - закончилось время ожидания.
      - **ReferenceError** - попытка доступа к атрибуту со слабой ссылкой.
      - **RuntimeError** - возникает, когда исключение не попадает ни под одну из других категорий.
      - **NotImplementedError** - возникает, когда абстрактные методы класса требуют переопределения в дочерних классах.
      - **SyntaxError** - синтаксическая ошибка.
        - *IndentationError* - неправильные отступы.
          - TabError - смешивание в отступах табуляции и пробелов.
      - **SystemError** - внутренняя ошибка.
      - **TypeError** - операция применена к объекту несоответствующего типа.
      - **ValueError** - функция получает аргумент правильного типа, но некорректного значения.
      - **UnicodeError** - ошибка, связанная с кодированием / раскодированием unicode в строках.
        - *UnicodeEncodeError* - исключение, связанное с кодированием unicode.
        - *UnicodeDecodeError* - исключение, связанное с декодированием unicode.
        - *UnicodeTranslateError* - исключение, связанное с переводом unicode.
      - **Warning** - предупреждение.

## Часто встречающиеся Exception

### AttributeError
**AttributeError** — объект не имеет данного атрибута (значения или метода).

Пример: <br>
`AttributeError: type object 'Car' has no attribute '__max_carrying'`

`AttributeError: 'frozenset' object has no attribute 'add'`

### OSError
**OSError** — ошибка, связанная с системой.

#### FileNotFoundError
**FileNotFoundError** — файл или директория не существует.

```python
>>> open('sys.txt', 'r')
Traceback (most recent call last):
    ...
FileNotFoundError: [Errno 2] No such file or directory: 'sys.txt'
```

### SyntaxError
**SyntaxError** — синтаксическая ошибка
```python
>>> ord(`100`)
    ...
    ord(`100`)
        ^
SyntaxError: invalid syntax
```
```python
>>> print '\'
  File "<stdin>", line 1
    print '\'
          ^
SyntaxError: unterminated string literal (detected at line 1)

```
### TypeError
**TypeError** — операция применена к объекту несоответствующего типа.
```python
>>> None + 1
Traceback (most recent call last):
    ...
TypeError: unsupported operand type(s) for +: 'NoneType' and 'int'
```
```python
>>> class Class_A:
...     def __init__(self, var):
...             return var
... 
>>> obj = Class_A(20)
Traceback (most recent call last):
    ...
TypeError: __init__() should return None, not 'int'
```

### ValueError
**ValueError** — функция получает аргумент правильного типа, но некорректного значения.
```python
>>> range(1, 10, 0)
Traceback (most recent call last):
    ...
ValueError: range() arg 3 must not be zero
```

---
Лекция [тут](https://github.com/DerSerhii/PythonCources/blob/master/lesson18.md)
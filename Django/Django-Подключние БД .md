# Подключение базы данных

Будем использовать PostgreSQL, для этого предварительно нужно эту базу установить.

### Создание базы и пользователя базы

Предположим, что база установлена, и пароль для пользователя `postgres` создан.

Заходим в консоль базы данных.

Под Windows: `psql -U postgres`

Под Linux: `sudo -u postgres psql`

Создаём базу *"mydb"* с кодировкой *'UTF8'*, что бы избежать проблем с русским и другими языками в базе:<br>
`create database mydb with encoding 'UTF8';`

Создаём пользователя *"myuser"* для пользования этой базой: <br>
`create user myuser with password 'mypass';`

Даём новому пользователю права для использования новой базой: <br>
`grant all on database mydb to myuser;`

Для выхода из консоли набираем `\q` и жмем Enter.

### Конфигурация Django

Открываем проект, и в нём файл `settings.py`

И находим строку `DATABASES`

Заменяем на:
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'mydb',
        'USER': 'myuser',
        'PASSWORD': 'mypass',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}
```
Где `ENGINE` это "движок" он же модуль отвечающий за работу базы данных,
`NAME` это имя базы,

`USER` это имя пользователя,

`PASSWORD` это пароль пользователя,

`HOST` это хост(урл, расположение базы),

`PORT` это порт (5432 стандартный порт для postgres, если вы его изменили при установке, укажите свой).

Для того, что бы это работало, нужно установить тот самый "движок".
```
pip install psycopg2  # windows
pip install psycopg2-binary  # unix
```

Лекция по моделям [тут](https://github.com/PonomaryovVladyslav/PythonCources/blob/master/lesson30.md)
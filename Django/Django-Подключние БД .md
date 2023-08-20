# Подключение базы данных PostgreSQL

## Создание базы и пользователя базы

Предположим, что база установлена, и пароль для пользователя `postgres` создан.

Заходим в консоль базы данных. <br>
Linux:
```commandline
sudo -u postgres psql
```
Windows:
```commandline
psql -U postgres
```
Создаём базу *"mydb"* с кодировкой *'UTF8'*, что бы избежать проблем с русским и другими языками в базе:<br>
```commandline
create database mydb with encoding 'UTF8';
```
Создаём пользователя *"myuser"* для пользования этой базой: <br>
```commandline
create user myuser with password 'mypass';
```
Даём новому пользователю права для использования новой базой: <br>
```commandline
grant all on database mydb to myuser;
```
Для тестов используется отдельная база данных, которая будет указана в переменной `TEST`.
Эта база будет изначально пустая, и будет очищаться после каждого выполненного тест кейса.<br>
Юзер должен иметь права на создание и очистку базы данных:
```commandline
ALTER USER myuser CREATEDB;
```
Для выхода из консоли набираем `\q` и жмем Enter.

## Конфигурация Django

Открываем проект, и в нём файл `settings.py`

И находим строку `DATABASES`

Заменяем на:
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'testproject',
        'USER': 'myuser',
        'PASSWORD': 'mypass',
        'HOST': 'localhost',
        'PORT': '5432',
        'TEST': {
            'NAME': 'testdb',
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

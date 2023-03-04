# Quick commands

Способ №1 <br>
`$ sudo -i -u postgres` - подключение к postgres;
затем: <br>
`$ psql -l` - просмотра существующих баз данных; <br>
`$ createdb any_db` - консольная команда для создания базы данных в postgres; <br>
`$ psql any_db` - подключение к базе данных; <br>

`$ psql` - доступ к командной строке postgres;

Способ №2 <br>
`sudo -u postgres psql` - *сразу* доступ к командной строке postgres;

### В командной строке postgres:
`postgres=# \l` - list databases; <br>
`postgres=# \c any_db` - подключение к базе данных; <br>
`any_bd=# \dt` - демонстрации списка доступных таблиц; <br>
`any_bd=# \d` - краткое описание таблицы; <br>
`any_bd=# \d any_table` - просмотр таблицы; 

`create database mydb with encoding 'UTF8';` - создаём базу с кодировкой 'UTF8', <br>
`create user myuser with password 'mypass';` - создаём пользователя для пользования этой базой; <br>
`grant all on database mydb to myuser;` - даём новому пользователю права для использования новой базой;  <br>
Если postgres >= 15, то дополнительно: <br>
`\c mydb` -> <br>
`grant all on schema public to myuser;` - предоставляем вашему пользователю права к схеме public в новой базе данных.



`postgres=# \q` - exit


`create database any_db;` - создание базы данных; <br>
`create table cars(id serial, brand text not null);` - создание таблицы;


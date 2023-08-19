# Дамп и восстановление БД

## Утилита pg_dump

В **PostgreSQL** есть встроенный инструмент для создания резервных копий — 
утилита `pg_dump`.<br> 
Утилита имеет простой синтаксис:
```
pg_dump <параметры> <имя базы> > <файл для сохранения копии> 
```
В простейшем случае достаточно указать *имя базы данных*, которую в дальнейшем нужно 
будет восстановить. <br>
Резервная копия создается следующей командой:
```commandline
pg_dump -h localhost -U postgres cinemadb > ~/Projects/Cinema-Project/dumps/cinema.dump
```
Создание дампа данных с определенными таблицами:
```commandline
pg_dump -h source_host -U source_user -d source_database -t table1 -t table2 > data_dump.sql
pg_dump -h localhost -U postgres cinemadb -t cinema_screencinema> ~/Projects/Cinema-Project/dumps/cinema_screen.dump
```


## Утилита pg_restore
Базу данных потребуется создать перед восстановлением и пользователя 
(которому принадлежит восстанавливаемая база данных).

Утилита позволяет восстанавливать данные из резервных копий. <br>
Например, чтобы восстановить только определенную БД, 
нужно запустить эту утилиту с параметром -d:
```commandline
pg_restore -d eshopdb /tmp/eshopdb.bak
```
Также утилитой pg_restore можно восстановить данные из архивного 
файла:
```commandline
pg_restore -d eshopdb -Ft /tmp/eshopdb.tar
```
Восстановить данные из дампа также возможно при помощи psql:
```commandline
psql eshopdb < /tmp/eshopdb.dump
```
Восстановление только данных из дампа:
```commandline
pg_restore -h target_host -U target_user -d target_database --data-only data_dump.sql
```
Подробное описание — [Резервное копирование и восстановление PostgreSQL: 
pg_dump, pg_restore, wal-g](https://selectel.ru/blog/postgresql-backup-tools/)


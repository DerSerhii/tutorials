# Интерактивная среда Shell 

***Shell*** в Django представляет собой *интерактивную среду командной строки*, которая позволяет взаимодействовать
с проектом Django и его моделями.

Shell обеспечивает доступ к функциональности Django ORM, что позволяет выполнять операции с базой данных и
манипулировать данными.

Запуск:`~$ python manage.py shell`

Импорт моделей:`from some_project.models import some_models`

Для просмотра SQL запросов:
```commandline
>>> from django.db import connection
>>> connection.queries
{'sql': 'SELECT "e_shop_product"."id", "e_shop_product"."name", "e_shop_product"."slug", "e_shop_product"."description", "e_shop_product"."price", "e_shop_product"."photo", "e_shop_product"."amount", "e_shop_product"."category_id", "e_shop_product"."is_available" FROM "e_shop_product" ORDER BY "e_shop_product"."name" ASC LIMIT 1 OFFSET 1', 'time': '0.000'}
```


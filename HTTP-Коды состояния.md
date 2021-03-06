# Коды состояния HTTP

---

`200 OK` — запрос выполнен успешно 

`201 Created` — запрос выполнен успешно и привёл к созданию ресурса.

Новый ресурс эффективно создаётся до отправки этого ответа. 
И новый ресурс возвращается в теле сообщения, его местоположение представляет 
собой либо URL-адрес запроса, либо содержимое заголовка Location.

---

`400 Bad Request` — указывает, что сервер не смог понять запрос из-за 
недействительного синтаксиса.

Клиент не должен повторять этот запрос без изменений.

`401 Unauthorized` — выдается сервером в случае возникновения проблем с аутентификацией или 
авторизацией на сайте:
- данные для аутентификации не переданы;
- указанные имя пользователя и пароль не верны;
- ошибка в настройках сайта или в коде скрипта сайта, отвечающих за аутентификацию или авторизацию.



# Permissions DRF

**Permissions** (eng: "разрешения") — ограничение(разрешения) права доступа.

Задать разрешения можно:
- на уровне проекта 
- на уровне ресурса

Что бы задать на уровне **проекта**, в `settings.py` необходимо добавить:
```python
REST_FRAMEWORK = {
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.IsAuthenticated',
    ]
}
```
Для описания на уровне **объектов** используется аргумент `permission_classes`:
```python
from rest_framework import permissions

class ExampleModelViewSet(ModelViewSet):
    permission_classes = [permissions.IsAuthenticatedOrReadOnly]
```
Существует достаточно много заготовленных пермишенов:
- `AllowAny` — можно всем
- `IsAuthenticated` — только авторизированным пользователям
- `IsAdminUser` — только администраторам
- `IsAuthenticatedOrReadOnly` - залогиненым или только на чтение

Но если нужны кастомные, то мы можем создать их отнаследовавшись от `permissions.BasePermission` 
и переписав один из, или оба метода `has_permisson` и `has_object_permission`.

`has_permission` — отвечает за доступ к *спискам объектов*.

`has_object_permission` — отвечает за доступ к *конкретному объекту*.

Например, владельцу можно выполнять любые действия, а остальным только чтение объекта:
```python
from rest_framework import permissions

class IsOwnerOrReadOnly(permissions.BasePermission):
    """
    Custom permission to only allow owners of an object to edit it.
    """

    def has_object_permission(self, request, view, obj):
        # Read permissions are allowed to any request,
        # so we'll always allow GET, HEAD or OPTIONS requests.
        if request.method in permissions.SAFE_METHODS:
            return True

        # Write permissions are only allowed to the owner of the snippet.
        return obj.owner == request.user

    def has_permission(self, request, view):
        return True
```
Пермишены можно указывать через запятую если их несколько:
```python
permission_classes = [permissions.IsAuthenticatedOrReadOnly, IsOwnerOrReadOnly]
```

Если у вас нет доступов, вы получите вот такой ответ:
```
{
    "detail": "Authentication credentials were not provided."
}
```

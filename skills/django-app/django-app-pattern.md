# Django App Architecture Pattern

All placeholders below: `{app_name}` = app name (e.g., `fund`), `{ModelName}` = model class (e.g., `Fund`), `{model_name}` = snake_case (e.g., `fund`).

## File Structure

```
apps/{app_name}/
├── __init__.py      (created by startapp)
├── admin.py
├── apis.py          # django-ninja Router, defines interfaces only
├── apps.py
├── migrations/      (created by startapp)
├── models.py
├── schemas.py       # django-ninja ModelSchema
├── services.py      # business logic layer
├── tests.py
└── views.py         (created by startapp, leave empty)
```

## apps/{app_name}/apps.py

```python
from django.apps import AppConfig


class {AppName}Config(AppConfig):
    default_auto_field = "django.db.models.BigAutoField"
    name = "apps.{app_name}"
    label = "{app_name}"
```

## apps/{app_name}/models.py

All field `verbose_name` must use **zh-TW (繁體中文)**.

```python
from django.db import models


class {ModelName}(models.Model):
    name = models.CharField("名稱", max_length=100)
    # other fields with zh-TW verbose_name...
    created_at = models.DateTimeField("建立時間", auto_now_add=True)
    updated_at = models.DateTimeField("更新時間", auto_now=True)

    class Meta:
        ordering = ["-created_at"]
        verbose_name = "{ModelName 的中文名}"
        verbose_name_plural = "{ModelName 的中文名}"

    def __str__(self):
        return self.name  # adjust to appropriate field
```

## apps/{app_name}/schemas.py

```python
from ninja import ModelSchema

from .models import {ModelName}


class {ModelName}In(ModelSchema):
    class Meta:
        model = {ModelName}
        fields = [...]  # writable fields only, exclude id and timestamps


class {ModelName}Out(ModelSchema):
    class Meta:
        model = {ModelName}
        fields = "__all__"
```

## apps/{app_name}/services.py

Business logic layer. All data operations go here, not in apis.py.

```python
from django.shortcuts import get_object_or_404

from .models import {ModelName}


def list_{model_name}s():
    return {ModelName}.objects.all()


def retrieve_{model_name}(id: int):
    return get_object_or_404({ModelName}, id=id)


def create_{model_name}(**data):
    return {ModelName}.objects.create(**data)


def update_{model_name}(id: int, **data):
    obj = get_object_or_404({ModelName}, id=id)
    for attr, value in data.items():
        setattr(obj, attr, value)
    obj.save()
    return obj


def destroy_{model_name}(id: int):
    obj = get_object_or_404({ModelName}, id=id)
    obj.delete()
    return {"success": True}
```

## apps/{app_name}/apis.py

Defines interfaces only (routes, request/response schemas, decorators). Delegates to services.

If `server/settings.py` has `CACHE_CONTROL`, add `@decorate_view(cache_control(**settings.CACHE_CONTROL))` to `list` and `retrieve` endpoints. Otherwise omit the decorator and its imports.

```python
from django.conf import settings
from django.views.decorators.cache import cache_control
from ninja import Router
from ninja.decorators import decorate_view
from ninja.pagination import LimitOffsetPagination, paginate

from .schemas import {ModelName}In, {ModelName}Out
from . import services

router = Router(tags=["{app_name}"])


@router.get("/", response=list[{ModelName}Out])
@paginate(LimitOffsetPagination)
@decorate_view(cache_control(**settings.CACHE_CONTROL))
def list_{model_name}s(request):
    return services.list_{model_name}s()


@router.get("/{id}", response={ModelName}Out)
@decorate_view(cache_control(**settings.CACHE_CONTROL))
def retrieve_{model_name}(request, id: int):
    return services.retrieve_{model_name}(id)


@router.post("/", response={ModelName}Out)
def create_{model_name}(request, payload: {ModelName}In):
    return services.create_{model_name}(**payload.dict())


@router.put("/{id}", response={ModelName}Out)
def update_{model_name}(request, id: int, payload: {ModelName}In):
    return services.update_{model_name}(id, **payload.dict())


@router.delete("/{id}")
def destroy_{model_name}(request, id: int):
    return services.destroy_{model_name}(id)
```

## apps/{app_name}/admin.py

```python
from django.contrib import admin

from .models import {ModelName}


@admin.register({ModelName})
class {ModelName}Admin(admin.ModelAdmin):
    list_display = ["id", "__str__", "created_at"]
    readonly_fields = ["created_at", "updated_at"]
```

## apps/{app_name}/tests.py

```python
import pytest
from ninja.testing import TestClient

from .apis import router
from .models import {ModelName}

client = TestClient(router)


@pytest.mark.django_db
def test_create_{model_name}():
    response = client.post("/", json={...})  # fill with valid data
    assert response.status_code == 200


@pytest.mark.django_db
def test_list_{model_name}s():
    response = client.get("/")
    assert response.status_code == 200


@pytest.mark.django_db
def test_retrieve_{model_name}():
    obj = {ModelName}.objects.create(...)  # fill with valid data
    response = client.get(f"/{obj.id}")
    assert response.status_code == 200


@pytest.mark.django_db
def test_update_{model_name}():
    obj = {ModelName}.objects.create(...)
    response = client.put(f"/{obj.id}", json={...})
    assert response.status_code == 200


@pytest.mark.django_db
def test_destroy_{model_name}():
    obj = {ModelName}.objects.create(...)
    response = client.delete(f"/{obj.id}")
    assert response.status_code == 200
    assert not {ModelName}.objects.filter(id=obj.id).exists()
```

## Registration

### server/settings.py

Add `"apps.{app_name}"` under `# Applications` in INSTALLED_APPS.

### server/apis.py

Use string import (lazy loading), do NOT import the router directly:

```python
api.add_router("/{app_name}s/", "apps.{app_name}.apis.router")
```

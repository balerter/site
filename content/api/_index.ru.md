+++
title = "API"
date = 2020-02-04T16:08:54+03:00
weight = 6
pre = "<b>VI. </b>"
+++

В конфигурации в секции `Global` вы можете указать адрес, на котором будет слушать HTTP API сервер.
По-умолчанию это `127.0.0.1:2000`.

Запросы к API осуществляются на этот адрес по пути `/api/<API_VERSION>/<API_QUERY>` 

---
Версия API `v1` 

## Описания моделей

### `AlertInfo`

|field|type|description|
|-----|----|-----------|
|name|string| имя алерта |
|level|int| текущий уровень алерта (error/warning/success) |
|count|int| количество вызовов данного уровня алерта с момента последнего изменения |
|updated_at|datetime| время, когда последний раз было изменения уровня алерта, формат time.RFC3339 (YYYY-MM-DDTHH:mm:ssZoffset) |

Пример:

```
{
    "count": 2,
    "last_change": "2020-02-17T14:03:05.403478+03:00",
    "level": "error",
    "name": "alert-name",
}
```

> Пояснения по полю `Count`:

> Допустим, ваш скрипт выполянется 1 раз в минуту. И каждый свой запуск он для алерта 'alert-name' указывает статус Success. В этом случае, если вы вызовете метод API для получения спсика алертов, то для алерта 'alert-name' поле Count будет равно 5. Так как, к этому моменту скрипт 5 раз "сказал", что этот алерт имеет статус `Success` 

## Методы API

### `GET /liveness`

Используется для проверки живости сервиса

Возвращает строку `ok`

### `GET /api/v1/alerts?name=<NAME1>,<NAME2>&level=<LEVEL1>,<LEVEL2>`

Получение списка Алертов

Необязательные Query аргументы `name` и `level` позволяют отфильтровать выдачу по имени и/или уровню. Вы можете указать несколько имен или уровней через запятую

Ответ:

```
[
  {
    "count": 2,
    "last_change": "2020-02-17T14:03:05.403478+03:00",
    "level": 2,
    "name": "a1",
  },
  ...
]
```

Примеры запросов:

```
GET /api/v1/alerts
GET /api/v1/alerts?name=foo
GET /api/v1/alerts?name=foo,bar
GET /api/v1/alerts?level=error
GET /api/v1/alerts?level=error,success
GET /api/v1/alerts?level=error,success&name=foo,bar
GET /api/v1/alerts?name=foo&level=error
```

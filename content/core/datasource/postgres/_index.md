---
title: "Postgres"
date: 2020-02-04T19:23:28+03:00
draft: false
weight: 2
---


Модуль `datasource.postgres` позволяет получать данные из базы данных **Postgres**

Подключение:
```
local db = require('datasource.postgres.<NAME_FROM_CONFIG>')
```

### Методы

#### `query('<SQL QUERY>') result, error`

Выполнение запроса и получение результата. В случае ошибки, вторая возвращаемая переменная будет содержать текст ошибки

Формат результата:

```
{
    -- row 1
    {
        <FIELD1_NAME> = <FIELD1_VALUE>,
        <FIELD2_NAME> = <FIELD2_VALUE>,
        ...
    },
    -- row 2
    {
        <FIELD1_NAME> = <FIELD1_VALUE>,
        <FIELD2_NAME> = <FIELD2_VALUE>,
        ...
    },
    -- row N
    ...
}
``` 

Например: 
Допустим, у нас есть таблица `users`, которая имеет колонки `id` и `name`

```
local db = require('datasource.postgres.dev')

local res, err = db.query("SELECT id, name FROM users")
if err ~= nil then
    return
end

-- res будет содержать примерно следующие данные
{
    {
        id = 1,
        name = 'root',
    },
    {
        id = 2,
        name = 'admin',
    },
    {
        id = 4,
        name = 'user1',
    },
}

```
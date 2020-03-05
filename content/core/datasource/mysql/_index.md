---
title: "MySQL"
date: 2020-02-04T19:23:28+03:00
draft: false
weight: 4
---


Модуль `datasource.mysql` позволяет получать данные из базы данных **MySQL**

Подключение:
```
local db = require('datasource.myqsl.<NAME_FROM_CONFIG>')
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
local db = require('datasource.mysql.dev')

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

## Поддержка типов полей

На данный момент не поддерживаются поля GEOMETRY, ENUM, BIT

Если вам необходима их поддержка, создайте [issue на github](https://github.com/balerter/balerter/issues)
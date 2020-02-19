---
title: "Clickhouse"
date: 2020-02-04T19:23:28+03:00
draft: false
weight: 1
---

Модуль `datasource.clickhouse` позволяет получать данные из базы данных [**Clickhouse**](https://clickhouse.tech)

Подключение:
```
local db = require('datasource.clickhouse.<NAME_FROM_CONFIG>')
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

```
local db = require('datasource.clickhouse.dev')

local res, err = db.query("SELECT table, sum(bytes) AS size FROM system.parts WHERE active AND database = 'system' GROUP BY table")
if err ~= nil then
    return
end

-- res будет содержать примерно следующие данные
{
    {
        table = 'query_thread_log',
        size = 943846427
    },
    {
        table = 'metric_log',
        size = 656645852
    },
    {
        table = 'query_log',
        size = 997251520
    },
    {
        table = 'part_log',
        size = 2037035728
    }
}

```

### Поддерживаемые типы данных

В данный момент при разборе ответа Clickhouse поддерживаются следующие типы данных:
- UInt8, UInt16, UInt32, UInt64
- Int8, Int16, Int32, Int64
- Float32, Float64
- String
- UUID
- Date
- DateTime
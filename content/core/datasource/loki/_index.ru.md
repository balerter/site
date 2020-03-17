---
title: "Loki"
date: 2020-02-04T19:23:28+03:00
draft: false
weight: 5
---

Модуль `datasource.loki` позволяет получать данные из источников, которые поддерживают язык запросов LogQL от **Grafana Loki**

Подробнее о [Loki](https://github.com/grafana/loki)

Подключение:
```
local loki = require('datasource.loki.<NAME_FROM_CONFIG>')
```

### Методы

#### `query('<QUERY>'[, <QUERY_OPTIONS>]) result, error`

Запрос [Instant Query](https://github.com/grafana/loki/blob/master/docs/api.md#get-lokiapiv1query)

Формат результата:

```
{
    {
        lables = {
            <LABEL_NAME> = <LABEL_VALUE>,
            ...
        },
        entries = {
            {
                timestamp = <TIMESTAMP>,
                line = <VALUE>
            },
            ...
        }
    },
    ...
}
``` 

Опции:
```
{
    time = <TIME RFC3339|Timestamp> -- Evaluation timestamp
    direction = [backward|forward]  -- порядок сортировки логов, поддерживаемые значения: forward или backward. По умолчанию: backward
    limit = <NUMBER>                -- максимальное количество записей
}
```

Например:

```
local loki = require('datasource.loki.dev')

local res, err = loki.query('{service="srv1"}')
if err ~= nil then
    return
end

-- res будет содержать примерно следующие данные
{
    ...
    {
        labels = {
            service = srv1
            level = 1
        }
        entries = {
            {
                timestamp = 1581934085
                line = 'Log line'
            }
        }
    },
    {
        labels = {
            service = srv1
            level = 2
        }
        entries = {
            {
                timestamp = 1581934085
                line = 'Log line'
            }
        }
    },
    ...
 }
```

#### `range('<QUERY>'[, <QUERY_OPTIONS>]) result, error`

Запрос [Range Query](https://github.com/grafana/loki/blob/master/docs/api.md#get-lokiapiv1query_range)

Формат результата аналогичен выводу метода `query`

Опции:
```
{
    start = <TIME RFC3339|Timestamp>    -- start time
    end = <TIME RFC3339|Timestamp>      -- end time
    step = <NUMBER>                     -- Query resolution step width in duration format or float number of seconds
    direction = [backward|forward]      -- порядок сортировки логов, поддерживаемые значения: forward или backward. По умолчанию: backward
    limit = <NUMBER>                    -- максимальное количество записей
}
```


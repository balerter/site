---
title: "Prometheus"
date: 2020-02-04T19:23:28+03:00
draft: false
weight: 3
---


Модуль `datasource.prometheus` позволяет получать данные из источников, которые поддерживают язык запросов PromQL от **Prometheus**

Это может быть как сам Prometheus, так и, например, [Victoria Metrics](https://victoriametrics.com)

Подключение:
```
local db = require('datasource.prometheus.<NAME_FROM_CONFIG>')
```

### Методы

#### `query('<QUERY>'[, <QUERY_OPTIONS>]) result, error`

Запрос [Instant Query](https://prometheus.io/docs/prometheus/latest/querying/api/#instant-queries)

Формат результата:

```
{
    {
        metrics = {
            <METRIC_NAME> = <METRIC_VALUE>,
            ...
        },
        value = {
            timestamp = <TIMESTAMP>,
            value = <VALUE>
        }
    },
    ...
}
``` 

Опции:
```
{
    time = <TIME RFC3339|Timestamp> -- Evaluation timestamp
}
```

Например:

```
local prom = require('datasource.prometheus.dev')

local res, err = prom.query("node_cpu_seconds_total")
if err ~= nil then
    return
end

-- res будет содержать примерно следующие данные
{
    ...
    {
        metrics = {
            __name__ = node_cpu_seconds_total
            cpu = 7
            datacenter = dc1
            job = node_exporter
            mode = softirq
        }
        value = {
            timestamp = 1581934085
            value = 118687.2
        }
    },
    {
        metrics = {
            __name__ = node_cpu_seconds_total
            cpu = 6
            datacenter = dc1
            job = node_exporter
            mode = idle
        }
        value = {
            timestamp = 1581934085
            value = 3.95205464e+06
    },
    ...
 }
```

#### `range('<QUERY>'[, <QUERY_OPTIONS>]) result, error`

Запрос [Range Query](https://prometheus.io/docs/prometheus/latest/querying/api/#range-queries)

Формат результата:

```
{
    {
        metrics = {
            <METRIC_NAME> = <METRIC_VALUE>,
            ...
        },
        values = {
            {
                timestamp = <TIMESTAMP>,
                value = <VALUE>
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
    start = <TIME RFC3339|Timestamp>    -- start time
    end = <TIME RFC3339|Timestamp>      -- end time
    step = <NUMBER>                     -- Query resolution step width in duration format or float number of seconds
}
```

Например:

```
local prom = require('datasource.prometheus.dev')

local res, err = prom.range("node_cpu_seconds_total")
if err ~= nil then
    return
end

-- res будет содержать примерно следующие данные
{
    ...
    {
        metrics = {
            __name__ = node_cpu_seconds_total
            cpu = 7
            datacenter = dc1
            job = node_exporter
            mode = softirq
        }
        values = {
            {
                timestamp = 1581837350,
                value = 186776.71
            },
            {
                timestamp = 1581840950,
                value = 186770.40
            },
            ...
        }
    },
    {
        metrics = {
            __name__ = node_cpu_seconds_total
            cpu = 6
            datacenter = dc1
            job = node_exporter
            mode = idle
        }
        values = {
            {
                timestamp = 1581837350,
                value = 186776.71
            },
            {
                timestamp = 1581840950,
                value = 186770.40
            },
            ...
        }
    },
    ...
 }
```
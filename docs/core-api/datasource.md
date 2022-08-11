This endpoint allows to use [datasource](/core-modules/datasource/about) core module

Basic request format:

`POST /datasource/{type}/{name}/{method}`

## clickhouse

### query

#### request

> `POST /datasource/clickhouse/{name}/query`

- request body - SQL query

Example:

```bash
curl -X "POST" "http://127.0.0.1:2020/datasource/clickhouse/ch1/query" \
     -H 'Content-Type: text/plain; charset=utf-8' \
     -d "SELECT 'foo' AS name, 42 AS age, now() AS time"
```

Its request is analogous to the following lua script:

```lua title="script.lua"
local ds = require("datasource.clickhouse.ch1")
result = ds.query('SELECT 'foo' AS name, 42 AS age, now() AS time')
```

#### response

```json
{
  "status": "ok",
  "result": [
    {
      "age": 42,
      "name": "foo",
      "time": "2022-08-11T17:46:25.738789+03:00"
    }
  ]
}
```

## postgres

All methods are analogous to the ones for clickhouse.

> `POST /datasource/clickhouse/{name}/query`

## mysql

All methods are analogous to the ones for clickhouse.

> `POST /datasource/mysql/{name}/query`

## prometheus

### query

#### request

> `POST /datasource/prometheus/{name}/query`

- request body - prometheus query

| Query Arg  | Description          |
|------------|----------------------|
| `time`     | evaluation timestamp |

Example:

```bash
curl -X "POST" "http://127.0.0.1:2020/datasource/prometheus/prom1/query" \
     -H 'Content-Type: text/plain; charset=utf-8' \
     -d "sum(go_goroutines)"
```

Its request is analogous to the following lua script:

```lua title="script.lua"
local ds = require("datasource.prometheus.prom1")
result = ds.query('sum(go_goroutines)')
```

#### response

```json
{
  "status": "ok",
  "result": [
    {
      "metric": {},
      "value": {
        "Timestamp": 1660229686,
        "Value": 2366701
      }
    }
  ]
}
```

### range

#### request

> `POST /datasource/prometheus/{name}/range`

- request body - prometheus query

| Query Arg  | Description                                                               |
|------------|---------------------------------------------------------------------------|
| `start`    | start timestamp                                                           |
| `end`      | end timestamp                                                             |
| `step`     | query resolution step width in duration format or float number of seconds |

Example:
```bash
curl -X "POST" "http://127.0.0.1:2020/datasource/prometheus/prom1/range" \
     -H 'Content-Type: text/plain; charset=utf-8' \
     -d "sum(go_goroutines)"
```

Its request is analogous to the following lua script:

```lua title="script.lua"
local ds = require("datasource.prometheus.prom1")
result = ds.range('sum(go_goroutines)')
```

#### response

```json
{
  "status": "ok",
  "result": [
    {
      "metric": {},
      "values": [
        {
          "Timestamp": 1660229402,
          "Value": 2379968
        },
        {
          "Timestamp": 1660229702,
          "Value": 2338777
        }
      ]
    }
  ]
}
```

## loki

### query

#### request

> `POST /datasource/loki/{name}/query`

- request body - loki query

| Query Arg   | Description                                                                 |
|-------------|-----------------------------------------------------------------------------|
| `limit`     | the max number of entries to return                                         |
| `time`      | the evaluation time for the query as a nanosecond Unix epoch                |
| `direction` | determines the sort order of logs. Supported values are forward or backward |

Example:

```bash
curl -X "POST" "http://127.0.0.1:2020/datasource/loki/loki1/query" \
     -H 'Content-Type: text/plain; charset=utf-8' \
     -d "{level=\"error\"}!=\"cache\""
```

Its request is analogous to the following lua script:

```lua title="script.lua"
local ds = require("datasource.loki.loki1")
result = ds.query('{level="error"}!="cache"')
```

#### response

```json
{
  "status": "ok",
  "result": [
    {
      "stream": {
        "alloc": "5fa29686-90d5-9bee-d205-4f0b0503479e",
        "datacenter": "eu-1",
        "filename": "/var/lib/nomad/data/alloc/5fa29686-90d5-9bee-d205-4f0b0503479e/alloc/logs/crcheck.stderr.50",
        "job": "nomad_log",
        "level": "error",
        "node": "node44"
      },
      "values": [
        {
          "Timestamp": 1660229986334893409,
          "Value": "loki message"
        },
        {
          "Timestamp": 1660229971536920460,
          "Value": "loki message"
        },
        {
          "Timestamp": 1660229963513371299,
          "Value": "loki message"
        }
      ]
    }
  ]
}
```

### range

#### request

> `POST /datasource/loki/{name}/range`

- request body - loki query

| Query Arg   | Description                                                                 |
|-------------|-----------------------------------------------------------------------------|
| `limit`     | the max number of entries to return                                         |
| `start`     | start timestamp                                                             |
| `end`       | end timestamp                                                               |
| `step`      | query resolution step  width in duration format or float number of seconds  |
| `direction` | determines the sort order of logs. Supported values are forward or backward |

Example:

```bash
curl -X "POST" "http://127.0.0.1:2020/datasource/loki/loki1/range" \
     -H 'Content-Type: text/plain; charset=utf-8' \
     -d "{level=\"error\"}!=\"cache\""
```

Its request is analogous to the following lua script:



Its request is analogous to the following lua script:

```lua title="script.lua"
local ds = require("datasource.loki.loki1")
result = ds.range('{level="error"}!="cache"')
```

#### response

```json
{
  "status": "ok",
  "result": [
    {
      "stream": {
        "datacenter": "eu-1",
        "filename": "/var/log/syslog",
        "job": "varlogs",
        "level": "error",
        "node": "node53"
      },
      "values": [
        {
          "Timestamp": 1660230001560593865,
          "Value": "loki message"
        },
        {
          "Timestamp": 1660230000057450107,
          "Value": "loki message"
        }
      ]
    },
    {
      "stream": {
        "datacenter": "eu-1",
        "filename": "/var/log/syslog",
        "job": "varlogs",
        "level": "error",
        "node": "node24"
      },
      "values": [
        {
          "Timestamp": 1660229666612267117,
          "Value": "loki message"
        }
      ]
    }
  ]
}
```

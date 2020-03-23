+++
title = "API"
date = 2020-02-04T16:08:54+03:00
weight = 6
pre = "<b>VI. </b>"
+++

In the `global` section you can define listen address. By default `127.0.0.1:2000`

API path `/api/<API_VERSION>/<API_QUERY>`

---
Current API version `v1` 

## Models

### `AlertInfo`

|field|type|description|
|-----|----|-----------|
|name|string| alert name |
|level|int| current alert level (error/warning/success) |
|count|int| count current level checks after last level change  |
|updated_at|datetime| time of last level change. Format RFC3339 (YYYY-MM-ddTHH:mm:ssZoffset) |

An example:

```
{
    "count": 2,
    "last_change": "2020-02-17T14:03:05.403478+03:00",
    "level": "error",
    "name": "alert-name",
}
```

> Comment for the `Count` field:

> Your script runs 1 times per minute. After 5 minutes your script 5 times calls 'alert.off(...)'
> If your script change alert level, counter will be reset 
> Field `count` represents this counter

## API methods

### `GET /liveness`

Use for check a service liveness

Returns a string: `ok`

### `GET /api/v1/alerts?name=<NAME1>,<NAME2>&level=<LEVEL1>,<LEVEL2>`

Get alerts list

Not mandatory Query arguments `name` and `level` allow filtering results by name and/or level. You can defined multiple values with comma delimiter

Response:

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

Query examples:

```
GET /api/v1/alerts
GET /api/v1/alerts?name=foo
GET /api/v1/alerts?name=foo,bar
GET /api/v1/alerts?level=error
GET /api/v1/alerts?level=error,success
GET /api/v1/alerts?level=error,success&name=foo,bar
GET /api/v1/alerts?name=foo&level=error
```


### `GET /api/v1/kv`

Obtain KV pairs from a storage

A response:

```
[
    {
        name = <NAME>,
        value = <VALUE>
    },
    ...
]
```

An example:

```
GET /api/v1/kv
```

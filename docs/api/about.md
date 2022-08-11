In the `api` section of configuration file you can define listen address. By default `127.0.0.1:2000`

API path `/api/<API_VERSION>/<API_QUERY>`

Current API version `v1`

## API methods

### Get alerts list

> `GET /api/v1/alerts?levels=<LEVEL1>,<LEVEL2>`

Not mandatory query argument `levels` allow filtering results by alert levels. 
You can defined multiple values with comma delimiter

Allowed `levels` values: `success`, `warning`, `warn`, `error`

Response:

```json
[
  {
    "name": "alert-id-1",
    "level": "success",
    "level_num": 1,
    "count": 2,
    "last_change": "2021-03-02T13:26:20Z",
    "start": "2021-02-21T17:48:22Z"
  },
  {
    "name": "fooabr2",
    "level": "error",
    "level_num": 3,
    "count": 10,
    "last_change": "2021-02-21T19:19:30Z",
    "start": "2021-02-21T19:19:30Z"
  }
]
```

### Get an alert by the name

> `GET /api/v1/alerts/{ALERT_NAME}`

Response example:

```json
{
  "name": "foobar2",
  "level": "error",
  "level_num": 3,
  "count": 1,
  "last_change": "2021-02-21T19:48:23Z",
  "start": "2021-02-21T19:43:12Z"
}
```

### Update the alert status

> `POST /api/v1/alerts/{ALERT_NAME}`

Payload: 

```json
{
    "level":    "success",
    "text":     "foo",
    "channels": ["chan1","chan2"],
    "quiet":    true,
    "repeat":   5,
    "image":    "https://domain.com/image.png"
}
```

Only `level` and `text` fields are required.

Return the updated alert model

```json
{
  "name": "foobar2",
  "level": "error",
  "level_num": 3,
  "count": 1,
  "last_change": "2021-02-21T19:48:23Z",
  "start": "2021-02-21T19:43:12Z"
}
```

### Get KV pairs from a storage

> `GET /api/v1/kv`

A response example:

```json
{
  "foo": "bar"
  "bar": "2",
  "baz": "true"
}
```

### Run script

> `POST /api/v1/runtime/run/{SCRIPT_NAME}`

You should specify the script name in full format. For example: `folder.name1.script_name` (see [more](../scripts/about.html#naming) about script naming)

The script will be run with no respect `@ignore` tag.

You can get the request information with `api` [module](/core-modules/api)
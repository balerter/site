This endpoint allows to use [log](/core-modules/log) core module

## info

### request

> `POST /log/info`

- request body - log message

Example

```bash
curl -X "POST" "http://127.0.0.1:2020/log/info" \
     -H 'Content-Type: text/plain; charset=utf-8' \
     -d "foo bar baz"
```

Its request is analogous to the following lua script:

```lua title="script.lua"
local log = require("log")
result = log.info('foo bar baz')
```

### response

```json
{
  "status": "ok"
}
```

## error

> `POST /log/error`

Same as `info`

## warn

> `POST /log/warn`

Same as `info`

## debug

> `POST /log/debug`

Same as `info`

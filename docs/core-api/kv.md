This endpoint allows to use [kv](/core-modules/kv) core module

## all

### request

> `POST /kv/all`

Example

```bash
curl -X "POST" "http://127.0.0.1:2020/kv/all" \
     -H 'Content-Type: text/plain; charset=utf-8' 
```

Its request is analogous to the following lua script:

```lua title="script.lua"
local kv = require("kv")
result = kv.all()
```

### response

```json
{
  "status": "ok",
  "result": {
    "var1": "barbaz",
    "var2": "foobar"
  }
}
```

## put

### request

> `POST /kv/put/{key}`

- `{key}` - key to put
- request body - value to put

Example

```bash
curl -X "POST" "http://127.0.0.1:2020/kv/put/var1" \
     -H 'Content-Type: text/plain; charset=utf-8' \
     -d "barbaz"
```

Its request is analogous to the following lua script:

```lua title="script.lua"
local kv = require("kv")
kv.put('var1', 'barbaz')
```

### response

```json
{
  "status": "ok"
}
```

## upsert

### request

> `POST /kv/upsert/{key}`

- `{key}` - key to put
- request body - value to put

Example

```bash
curl -X "POST" "http://127.0.0.1:2020/kv/upsert/var1" \
     -H 'Content-Type: text/plain; charset=utf-8' \
     -d "barbaz"
```

Its request is analogous to the following lua script:

```lua title="script.lua"
local kv = require("kv")
kv.upsert('var1', 'barbaz')
```

### response

```json
{
  "status": "ok"
}
```

## get

### request

> `POST /kv/get/{key}`

- `{key}` - key to get

Example

```bash
curl -X "POST" "http://127.0.0.1:2020/kv/get/var1" \
     -H 'Content-Type: text/plain; charset=utf-8' 
```

Its request is analogous to the following lua script:

```lua title="script.lua"
local kv = require("kv")
result = kv.get('var1')
```

### response

```json
{
  "status": "ok",
  "result": "barbaz"
}
```

## delete

### request

> `POST /kv/delete/{key}`

- `{key}` - key to delete

Example

```bash
curl -X "POST" "http://127.0.0.1:2020/kv/delete/var1" \
     -H 'Content-Type: text/plain; charset=utf-8' 
```

Its request is analogous to the following lua script:

```lua title="script.lua"
local kv = require("kv")
kv.delete('var1')
```

### response

```json
{
  "status": "ok"
}
```


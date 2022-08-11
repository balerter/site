This endpoint allows to use [runtime](/core-modules/runtime) core module

## get

### request

> `POST /runtime/get`

Example

```bash
curl -X "POST" "http://127.0.0.1:2020/runtime/get"
```

Its request is analogous to the following lua script:

```lua title="script.lua"
local rt = require("runtime")
result = rt.get()
```

### response

```json
{
  "status": "ok",
  "result": {
    "log_level": "DEBUG",
    "is_debug": true,
    "is_once": false,
    "with_script": "",
    "config_source": "balerter.hcl",
    "safe_mode": false
  }
}
```


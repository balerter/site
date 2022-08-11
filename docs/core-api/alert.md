This endpoint allows to use [alert](/core-modules/alert) core module

## methods

### success

Call `alert` module with `success` level

#### request

> `POST /alert/success/{id}`
 
- `{id}` - alert name (id)
- request body - alert message with `text/plain` content type

| Query Arg  | Description                                         |
|------------|-----------------------------------------------------|
| `channels` | channels,  comma-separated string                   |
| `quiet`    | `true` for quiet enabled                            |
| `repeat`   | number                                              |
| `image`    | image url or base64 encoded raw image data          |
| `fields`   | `<key>:<value>` pairs, comma-separated              |
| `escalate` | `<number>:<channel>,<channel>`, semicolon-separated |

Example

```bash
curl -X "POST" "http://127.0.0.1:2020/alert/error/id1?image=https%3A%2F%2Fwww.google.com%2Fimages%2Fbranding%2Fgooglelogo%2F2x%2Fgooglelogo_color_272x92dp.png&repeat=2" \
     -H 'Content-Type: text/plain; charset=utf-8' \
     -d "alert message"
```

Its request is analogous to the following lua script:

```lua title="script.lua"
local alert = require("alert")
alert.error('id1', 'alert message', { image = 'https://www.google.com/images/branding/googlelogo/2x/googlelogo_color_272x92dp.png', resend = 2 })
```

#### response

```json
{
  "status": "ok",
  "result": {
    "alert": {
      "name": "id1",
      "level": 3,
      "last_change": "2022-08-05T12:07:59.58757+03:00",
      "start": "2022-08-05T12:07:59.58757+03:00",
      "count": 4
    },
    "level_was_updated": false
  }
}
```

### warning

Call `alert` module with `warning` level

> POST /alert/warning/{id}

See details in [success](#success)

### error

Call `alert` module with `error` level

> POST /alert/error/{id}

See details in [success](#success)

### get

Get an alert by the name

#### request

> POST /alert/get/{id}

- `{id}` - alert name (id)

#### response

```json
{
  "status": "ok",
  "result": {
    "alert": {
      "name": "id1",
      "level": 3,
      "last_change": "2022-08-05T12:07:59.58757+03:00",
      "start": "2022-08-05T12:07:59.58757+03:00",
      "count": 4
    },
    "level_was_updated": false
  }
}
```


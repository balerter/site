??? failure "Core API"
    This module is not available in Core API

The `http` allows to send HTTP requests

Usage:

```lua title="script.lua"
local http = require('http')
```

## Methods

### get,post,put,delete

`response, err = http.get(<URI>, <BODY>, <HEADERS>) ` `get/post/put/delete`

Send a request with http method 'get', 'post', 'put' or 'delete'

```lua title="script.lua"
http.get('https://domain.com') 
http.post('https://domain.com', 'foo=bar') 
http.delete('https://domain.com') 
http.put('https://domain.com', 'foo=bar', { Authorizaion = 'Basic ABCDE'}) 
```

Returns a [response](#response)

If an error occurred, it will be returns as second value

Default timeout for these methods: 30s. If you want to use a custom timeout, you should to use a `http.request' method

### request 

`response, err = http.request(options)`

Send a request

```lua
options = {
    method = http.methodGet,
    uri = 'https://domain.com',
    body = nil,
    headers = {
        Authentication = 'Basic ABCDEF'
    },
    insecureSkipVerify = true, -- default: false
    timeout = "10s" -- Valid time units are "ns", "us" (or "µs"), "ms", "s", "m", "h". Default: 0
}

http.request(options)
```

Returns a [response](#response)

If an error occurred, it will be returns as second value

## response

```
{
    status_code = <INT>
    body = <STRING>
    headers = {
        <KEY> = <VALUE>,
        ...
    }
}
```

## http methods constants

- methodGet
- methodHead
- methodPost
- methodPut
- methodPatch
- methodDelete
- methodConnect
- methodOptions
- methodTrace

```lua title="script.lua"
http = require('http')

options = {
    method = http.methodPost,
    ...
}

http.request(options)
```
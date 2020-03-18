---
title: "HTTP"
date: 2020-02-04T19:23:28+03:00
draft: false
weight: 3
---

The `http` allows send HTTP requests 

Usage:

```
local http = require('http')
```

### Methods

#### `response, err = http.get(<URI>, <BODY>, <HEADERS>) ` `get/post/put/delete`

Send a request with http method 'get', 'post' or 'put'

```
http.get('https://domain.com') 
http.post('https://domain.com', 'foo=bar') 
http.put('https://domain.com', 'foo=bar', { Authorizaion = 'Basic ABCDE'}) 
```

Returns a [response](#response)

If an error occurred, it will be returns as second value

#### `response, err = http.request(optsion)`

Send a request

```
options = {
    method = http.methodGet,
    uri = 'https://domain.com',
    body = nil,
    headers = {
        Authentication = 'Basic ABCDEF'
    }
}

http.request(options)
```

Returns a [response](#response)

If an error occurred, it will be returns as second value

#### response 

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

#### http methods constants

- methodGet
- methodHead
- methodPost
- methodPut
- methodPatch
- methodDelete
- methodConnect
- methodOptions
- methodTrace

```
http = require('http')

options = {
    method = http.methodPost,
    ...
}

http.request(options)
```
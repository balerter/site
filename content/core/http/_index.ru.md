---
title: "HTTP"
date: 2020-02-04T19:23:28+03:00
draft: false
weight: 3
---

Модуль `http` позволяет отправлять http запросы

Подключение:

```
local http = require('http')
```

### Методы

#### `response, err = http.get(<URI>, <BODY>, <HEADERS>) ` `get/post/put/delete`

Отправить соотвествующий запрос

```
http.get('https://domain.com') 
http.post('https://domain.com', 'foo=bar') 
http.put('https://domain.com', 'foo=bar', { Authorizaion = 'Basic ABCDE'}) 
```

Возвращает структуру [response](#response)

Если произошла ошибка, она возвращается вторым параметром

#### `response, err = http.request(optsion)`

Отправить произвольный запрос

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

Возвращает структуру [response](#response)

Если произошла ошибка, она возвращается вторым параметром

#### response - результат запроса

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

#### константы http методов

Модуль содержит константы http методов, которые вы можете использовать при построении request options

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
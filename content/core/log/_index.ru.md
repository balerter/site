---
title: "Log"
date: 2020-02-04T19:23:28+03:00
draft: false
weight: 1
---

Модуль `log` используется для логгирования сообщений

Использование:

```
local log = require('log')

log.error('message')
log.warn('message')
log.info('message')
log.debug('message')
```

Методы `error`, `warn`, `info` и `debug` принимают один параметр - строку сообщения. И выводят это сообщение с соответствующим уровнем логгирования.
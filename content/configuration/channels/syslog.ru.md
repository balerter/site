---
title: "Тип Syslog"
date: 2020-02-04T16:50:16+03:00
draft: false
weight: 3
---

Сообщения, сериализованные в json, будут отправляться на syslog сервер.

```
syslog:
  - name: default
    tag: balerter
    network: tcp
    address: 127.0.0.1:10515
    priority: 'EMERG|DAEMON'
```

### name 

> Обязательное поле, Уникальное значение

Название канала уведомлений, в том числе используется при логгировании

В названии могут использоваться латинские символы, цифры, знаки минуса и подчеркивания

### tag

> По-умолчанию: пустая строка

Тег syslog 

### network

> По-умолчанию: пустая строка

Тип сети для syslog сервиса.
- `udp`
- `tcp`
- пустая строка для использования локального сервиса

### address

> По-умолчанию: пустая строка

Адрес syslog сервера

### priority

> По-умолчанию: `EMERG`

Формат параметра: `<SEVERITY>[|<FACILITI>]`

Возможные варианты Severity & Facility:

Severity:
- EMERG
- ALERT
- CRIT
- ERR
- WARNING
- NOTICE
- INFO
- DEBUG

Facility:
- KERN
- USER
- MAIL
- DAEMON
- AUTH
- SYSLOG
- LPR
- NEWS
- UUCP
- CRON
- AUTHPRIV
- FTP
- LOCAL0
- LOCAL1
- LOCAL2
- LOCAL3
- LOCAL4
- LOCAL5
- LOCAL6

Например:
```
priority: 'ALERT'
priority: 'ALERT|USER'
priority: 'INFO|LOCAL0'
```
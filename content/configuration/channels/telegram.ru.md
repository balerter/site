---
title: "Тип Telegram"
date: 2020-02-04T16:50:16+03:00
draft: false
weight: 2
---

```
telegram:
  - name: tg1
    token: TELEGRAM-BOT-TOKEN
    chatId: 100500
    timeout: 5s
    proxy:
      address: 10.20.30.40:5060
      auth:
        username: user
        password: secret
```

### name 

> Обязательное поле, Уникальное значение

Название канала уведомлений, в том числе используется при логгировании

В названии могут использоваться латинские символы, цифры, знаки минуса и подчеркивания

### token

> Обязательное поле

Токен telegram бота 

### chatId

> Обязательное поле

ID чата

### timeout

> По умолчанию: 5s

Таймаут

### proxy

> По-умолчанию: не используется

Настройки socks5 прокси для отправки уведомлений

Если указана секция auth, то будут использоваться указанные имя пользователя и пароль  

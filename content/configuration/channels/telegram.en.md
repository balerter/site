---
title: "Telegram"
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

> Required, Unique

Channel name

### token

> Required

Telegram bot API token 

### chatId

> Required

Chat ID

### timeout

> By default: 5s

timeout

### proxy

> Default: empty, not use

Socks5 proxy settings 

If `auth` section is defined, it will use for authentication

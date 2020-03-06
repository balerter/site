---
title: "Telegram"
date: 2020-02-04T16:50:16+03:00
draft: false
---

```
telegram:
  - name: tg1
    token: TELEGRAM-BOT-TOKEN
    chat_id: 100500
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

### chat_id

> Required

Chat ID

### proxy

> Default: empty, not use

Socks5 proxy settings 

If `auth` section is defined, it will use for authentication

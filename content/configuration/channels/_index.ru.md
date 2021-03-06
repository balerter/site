---
title: "Раздел Channels"
date: 2020-02-04T16:48:31+03:00
draft: false
weight: 4
---

В секции `scripts.channels` описываются каналы доставки уведомлений

- [slack](slack)
- [telegram](telegram)
- [syslog](syslog)
- [notify](notify)

```
channels:
  slack:
    - name: slack-notification
      token: SLACK-APPLICATION-TOKEN
      channel: notification

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
  syslog:
    - name: default
      tag: balerter
      network: tcp
      address: 127.0.0.1:10515
      priority: 'EMERG|DAEMON'

  notify:
    - name: default
      icons:
        success: /path/to/logo-success.png
        error: /path/to/logo-error.png
        warning: /path/to/logo-warning.png
```


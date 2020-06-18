---
title: "Chapter Channels"
date: 2020-02-04T16:48:31+03:00
draft: false
weight: 4
---

In the `scripts.channels` section describes notification channels

- [slack](slack)
- [telegram](telegram)
- [syslog](syslog)
- [notify](notify)
- [email](email)
- [discord](discord)

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

  email:
    - name: default
      from: foo@bar.com
      to: alert@bar.com
      cc: alert-cc@bar.com
      host: bar.com
      port: 1234
      username: user
      password: secret
      secure: ssl
      timeout: 1000

  discord:
    - name: default
      token: 'ABCD'
      channelId: 1234
```


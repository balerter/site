---
title: "Пример конфигурации"
date: 2020-02-04T16:37:04+03:00
draft: false
weight: 1
---

Файл конфигурации описывается в `yaml` формате

Секции конфигурации высшего уровня:

- [scripts](../scripts) - описание источников скриптов
- [datasources](../datasources) - описание источников данных
- [channels](../channels) - описание каналов отправки уведомлений
- [global](../global) - глобальные настройки

Пример:

```
scripts:
  sources:
    folder:
      - name: scripts
        path: /opt/scripts
        mask: '*.lua'
        update_interval: 5s

datasources:
  clickhouse:
    - name: ch1
      host: domain.com
      port: 6440
      username: username
      password: password
      database: database
      ssl_cert_path: /path/to/cert.crt

  prometheus:
    - name: prom1
      url: domain.com
      basic_auth:
        username: username
        password: password

  postgres:
    - name: pg1
      host: domain.com
      port: 5432
      username: username
      password: password
      database: database
      ssl_mode: verify-full
      ssl_cert_path: /path/to/cert.crt

channels:
  slack:
    - name: slack-notification
      token: SLACK-APPLICATION-TOKEN
      channel: notification
      prefixes:
        error: ':sos: '
        success: ':eight_spoked_asterisk: '

global:
  send_start_notification:
    - slack-notification
  send_stop_notification:
    - slack-notification
  api:
    address: 127.0.0.1:2000
```


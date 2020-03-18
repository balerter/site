+++
title = "Конфигурация"
date = 2020-02-04T16:35:56+03:00
weight = 2
pre = "<b>II. </b>"
+++

Файл конфигурации описывается в `yaml` формате

Секции конфигурации высшего уровня:

- [scripts](../scripts) - описание источников скриптов
- [datasources](../datasources) - описание источников данных
- [channels](../channels) - описание каналов отправки уведомлений
- [storages](../storages) - описание хранилищ для загрузки данных, например, изображений. И для хранения информации об алертах и KV
- [global](../global) - глобальные настройки

Пример:

```
scripts:
  updateInterval: 5s
  sources:
    folder:
      - name: scripts
        path: /opt/scripts
        mask: '*.lua'

datasources:
  clickhouse:
    - name: ch1
      host: domain.com
      port: 6440
      username: username
      password: password
      database: database
      sslCertPath: /path/to/cert.crt

  prometheus:
    - name: prom1
      url: domain.com
      basicAuth:
        username: username
        password: password

  postgres:
    - name: pg1
      host: domain.com
      port: 5432
      username: username
      password: password
      database: database
      sslMode: verify-full
      sslCertPath: /path/to/cert.crt
  
  mysql:
    - name: mysql1
      dsn: user:secret@tcp(127.0.0.1:3306)/database

  loki:
    - name: loki1
      url: domain.com
      basicAuth:
        username: username
        password: password

channels:
  slack:
    - name: slack-notification
      token: SLACK-APPLICATION-TOKEN
      channel: notification

  telegram:
    - name: tg1
      token: TELEGRAM-BOT-TOKEN
      chatId: 100500
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

storages:
  core:
    file:
      - name: primaryFile
        path: /path/to/file
  upload:
    s3:
      - name: dev
        region: us-east1
        key: SOME_KEY
        secret: SOME_SECRET
        endpoint: SOME_ENDPOINT
        bucket: SOME_BUCKET

global:
  sendStartNotification:
    - slack-notification
  sendStopNotification:
    - slack-notification
  api:
    address: 127.0.0.1:2000
    metrics: true
  storages:
    alert: file.primaryFile
    kv: memory
```

+++
title = "Configuration"
date = 2020-02-04T16:35:56+03:00
weight = 2
pre = "<b>II. </b>"
+++

Configuration file has `yaml` format

Top-level configuration sections:

- [scripts](scripts) - script sources
- [datasources](datasources) - data sources
- [channels](channels) - notification channels
- [storages](storages) - storages for upload data, for example, images. And for store alert/kv date (core storage)
- [global](global) - global settings

An example:

```
scripts:
  updateInterval: 5s
  sources:
    folder:
      - name: scripts
        path: /opt/scripts
        mask: '*.lua'
    file:
      - name: demo1
        filename: /path/to/demo.lua

datasources:
  clickhouse:
    - name: ch1
      host: domain.com
      port: 6440
      username: username
      password: password
      database: database
      sslCertPath: /path/to/cert.crt
      timeout: 3s

  prometheus:
    - name: prom1
      url: domain.com
      timeout: 3s
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
      timeout: 3s
  
  mysql:
    - name: mysql1
      dsn: user:secret@tcp(127.0.0.1:3306)/database
      timeout: 3s

  loki:
    - name: loki1
      url: domain.com
      timeout: 5s
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

storages:
  core:
    file:
      - name: primaryFile
        path: /path/to/file
        timeout: 1s
  upload:
    s3:
      - name: dev
        region: us-east1
        key: SOME_KEY
        secret: SOME_SECRET
        endpoint: SOME_ENDPOINT
        bucket: SOME_BUCKET

global:
  luaModulesPath: /modules/?.lua;/modules/?/?.lua
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


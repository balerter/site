---
title: "Раздел global"
date: 2020-02-04T17:06:21+03:00
draft: false
weight: 6
---

В секции `global` описываются общие настройки приложения

```
global:
  send_start_notification:
    - slack-notification
  send_stop_notification:
    - slack-notification
  api:
    address: 127.0.0.1:2000
    metrics: true
```

### `send_start_notification` 

Список каналов, куда будет отправлено уведомление **о старте** приложения. Если не указано, уведомление отправлено не будет.

### `send_stop_notification` 

Список каналов, куда будет отправлено уведомление **об остановке** приложения. Если не указано, уведомление отправлено не будет.

### `api`

Настройки HTTP API сервера приложения

- `address` (по умолчанию `127.0.0.1:2000`) - адрес, на котором будет слушать HTTP API сервер

- `metrics` (boolean, по умолчанию `false`) - если `True`, то по адресу `<API_ADDRESS>/metrics` будут доступны Prometheus метрики
  